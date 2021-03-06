---
title: Kubernetes-gRPC per sviluppatori WCF
description: Esecuzione di ASP.NET Core Servizi gRPC in un cluster Kubernetes.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 819c761a7a55485612b7fb0c8b392971751d8724
ms.sourcegitcommit: 337bdc5a463875daf2cc6883e5a2da97d56f5000
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/24/2019
ms.locfileid: "72846636"
---
# <a name="kubernetes"></a>Kubernetes

Sebbene sia possibile eseguire manualmente i contenitori negli host Docker, per i sistemi di produzione affidabili è preferibile usare un motore di orchestrazione contenitore per gestire più istanze in esecuzione in più server in un cluster. Sono disponibili vari motori di orchestrazione del contenitore, tra cui Kubernetes, Docker Swarm e Apache Mesos. Tuttavia, con questi motori, Kubernetes è molto più usato, quindi sarà l'obiettivo di questo capitolo.

Kubernetes include le funzionalità seguenti:

- La **pianificazione** esegue i contenitori su più nodi all'interno di un cluster, garantendo un uso bilanciato della risorsa disponibile, mantenendo i contenitori in esecuzione in caso di interruzioni e gestendo gli aggiornamenti in sequenza alle nuove versioni di immagini o nuove configurazioni.
- I **controlli di integrità** monitorano i contenitori per garantire un servizio continuo.
- Il **servizio di individuazione DNS &** gestisce il routing tra i servizi all'interno di un cluster.
- Il traffico in **ingresso** espone i servizi selezionati esternamente e in genere fornisce il bilanciamento del carico tra le istanze di tali servizi.
- **Gestione risorse** connette risorse esterne, ad esempio l'archiviazione ai contenitori.

In questo capitolo viene illustrato in dettaglio come distribuire un servizio ASP.NET Core gRPC e un sito Web che utilizza il servizio in un cluster Kubernetes. L'applicazione di esempio usata è disponibile nel repository [DotNet-Architecture/grpc-for-WCF-Developers](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/KubernetesSample) su GitHub.

## <a name="kubernetes-terminology"></a>Terminologia di Kubernetes

Kubernetes USA DSC ( *desired state Configuration*): l'API viene usata per descrivere oggetti quali *Pod*, *distribuzioni* e *Servizi*e il *piano di controllo* si occupa dell'implementazione dello stato desiderato in tutti i *nodi.* in un *cluster*. Un cluster Kubernetes dispone di un nodo *Master* che esegue l' *API Kubernetes*, che può essere comunicata a livello di codice o tramite lo strumento da riga di comando `kubectl`. `kubectl` possibile creare e gestire oggetti usando gli argomenti della riga di comando, ma funziona meglio con i file YAML che contengono dati di dichiarazione per gli oggetti Kubernetes.

### <a name="kubernetes-yaml-files"></a>File YAML Kubernetes

Ogni file YAML di Kubernetes avrà almeno tre proprietà di primo livello.

```yaml
apiVersion: v1
kind: Namespace
metadata:
  # Object properties
```

La proprietà `apiVersion` viene utilizzata per specificare la versione (e l'API) per cui il file è destinato. La proprietà `kind` specifica il tipo di oggetto rappresentato da YAML. La proprietà `metadata` contiene proprietà dell'oggetto, ad esempio `name`, `namespace` o `labels`.

La maggior parte dei file YAML di Kubernetes include anche una sezione `spec` che descrive le risorse e la configurazione necessarie per creare l'oggetto.

### <a name="pods"></a>Baccelli

I pod sono le unità di base di esecuzione in Kubernetes. Possono eseguire più contenitori, ma vengono usati anche per eseguire singoli contenitori. Il Pod include anche le risorse di archiviazione richieste dai contenitori e l'indirizzo IP di rete.

### <a name="services"></a>Servizi

I servizi sono metaoggetti che descrivono pod (o set di Pod) e forniscono un modo per accedervi all'interno del cluster, ad esempio il mapping di un nome di servizio a un set di indirizzi IP pod tramite il servizio DNS del cluster.

### <a name="deployments"></a>Distribuzioni

Le distribuzioni sono gli oggetti di *stato descritti* per i pod. Se si crea un pod manualmente, al termine non verrà riavviato. Le distribuzioni vengono usate per indicare al cluster quali pod e quante repliche di tali Pod devono essere in esecuzione al momento attuale.

### <a name="other-objects"></a>Altri oggetti

Pod, servizi e distribuzioni sono solo tre dei tipi di oggetti di base. Sono disponibili dozzine di altri tipi di oggetti gestiti da un cluster Kubernetes. Per ulteriori informazioni, vedere la documentazione relativa ai [concetti relativi a Kubernetes](https://kubernetes.io/docs/concepts/) .

### <a name="namespaces"></a>Namespaces

I cluster Kubernetes sono progettati per la scalabilità fino a centinaia o migliaia di nodi ed eseguono un numero simile di servizi. Per evitare conflitti tra i nomi degli oggetti, gli spazi dei nomi vengono utilizzati per raggruppare gli oggetti come parte delle applicazioni più grandi. I servizi di Kubernetes vengono eseguiti in uno spazio dei nomi `default`. Tutti gli oggetti utente devono essere creati nei rispettivi spazi dei nomi per evitare potenziali conflitti con gli oggetti predefiniti o altri tenant nel cluster.

## <a name="get-started-with-kubernetes"></a>Introduzione a Kubernetes

Se si sta eseguendo Docker desktop per Windows o macOS, Kubernetes è già disponibile. È sufficiente abilitarla nella sezione Kubernetes della finestra impostazioni.

![Abilitare Kubernetes in Docker desktop](media/kubernetes/enable-kubernetes-docker-desktop.png)

Per eseguire un cluster Kubernetes locale in Linux, vedere [minikube](https://github.com/kubernetes/minikube)o [MicroK8s](https://microk8s.io/) se la distribuzione di Linux supporta gli [snap](https://snapcraft.io/)-in.

Per verificare che il cluster sia in esecuzione e accessibile, eseguire il comando `kubectl version`.

```console
kubectl version
Client Version: version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.6", GitCommit:"96fac5cd13a5dc064f7d9f4f23030a6aeface6cc", GitTreeState:"clean", BuildDate:"2019-08-19T11:13:49Z", GoVersion:"go1.12.9", Compiler:"gc", Platform:"windows/amd64"}
Server Version: version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.6", GitCommit:"96fac5cd13a5dc064f7d9f4f23030a6aeface6cc", GitTreeState:"clean", BuildDate:"2019-08-19T11:05:16Z", GoVersion:"go1.12.9", Compiler:"gc", Platform:"linux/amd64"}
```

In questo esempio, sia l'interfaccia della riga di comando di `kubectl` che il server Kubernetes eseguono la versione 1.14.6. Ogni versione di `kubectl` dovrebbe supportare la versione precedente e successiva del server, pertanto `kubectl` 1,14 dovrebbe funzionare anche con le versioni del server 1,13 e 1,15.

## <a name="run-services-on-kubernetes"></a>Eseguire i servizi in Kubernetes

Nell'applicazione di esempio è presente una directory `kube` contenente tre file YAML. Il file di `namespace.yml` dichiara uno spazio dei nomi personalizzato, `stocks`. Il file di `stockdata.yml` dichiara la distribuzione e il servizio per l'applicazione gRPC e il file di `stockweb.yml` dichiara la distribuzione e il servizio per un'applicazione Web MVC ASP.NET Core 3,0 che usa il servizio gRPC.

Per utilizzare un file di `YAML` con `kubectl`, utilizzare il comando `apply -f`.

```console
kubectl apply -f object.yml
```

Il comando `apply` verificherà la validità del file YAML e visualizzerà gli eventuali errori ricevuti dall'API, ma non attenderà che tutti gli oggetti dichiarati nel file siano stati creati perché questa operazione può richiedere del tempo. Usare il comando `kubectl get` con i tipi di oggetto pertinenti per verificare la creazione di oggetti nel cluster.

### <a name="the-namespace-declaration"></a>Dichiarazione dello spazio dei nomi

La dichiarazione dello spazio dei nomi è semplice e richiede solo l'assegnazione di una `name`.

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: stocks
```

Utilizzare `kubectl` per applicare il file di `namespace.yml` e verificare che lo spazio dei nomi venga creato correttamente.

```console
> kubectl apply -f namespace.yml
namespace/stocks created

> kubectl get namespaces
NAME              STATUS   AGE
stocks            Active   2m53s
```

### <a name="the-stockdata-application"></a>Applicazione StockData

Il file di `stockdata.yml` dichiara due oggetti: una distribuzione e un servizio.

#### <a name="the-stockdata-deployment"></a>Distribuzione di StockData

La parte relativa alla distribuzione fornisce le `spec` per la distribuzione stessa, incluso il numero di repliche necessarie e una `template` per la creazione e la gestione degli oggetti pod da parte della distribuzione. Si noti che gli oggetti di distribuzione vengono gestiti con l'API `apps`, come specificato in `apiVersion`, anziché l'API Kubernetes principale.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stockdata
  namespace: stocks
spec:
  selector:
    matchLabels:
      run: stockdata
  replicas: 1
  template:
    metadata:
      labels:
        run: stockdata
    spec:
      containers:
      - name: stockdata
        image: stockdata:1.0.0
        imagePullPolicy: Never
        resources:
          limits:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 80
```

La proprietà `spec.selector` viene utilizzata per associare i pod in esecuzione alla distribuzione. La proprietà `metadata.labels` del Pod deve corrispondere alla proprietà `matchLabels` o la chiamata API avrà esito negativo.

La sezione `template.spec` dichiara il contenitore da eseguire. Quando si usa un cluster Kubernetes locale, ad esempio quello fornito da Docker desktop, è possibile specificare le immagini che sono state compilate localmente, purché dispongano di un tag Version.

> [!IMPORTANT]
> Per impostazione predefinita, Kubernetes verificherà sempre e tenterà di eseguire il pull di una nuova immagine. Se non riesce a trovare l'immagine in uno dei repository noti, la creazione del Pod avrà esito negativo. Per usare le immagini locali, impostare il `imagePullPolicy` su `Never`.

La proprietà `ports` specifica quali porte del contenitore devono essere pubblicate sul Pod.  L'immagine `stockservice` esegue il servizio sulla porta HTTP standard, quindi viene pubblicata la porta 80.

La sezione `resources` applica i limiti delle risorse al contenitore in esecuzione nel pod. Si tratta di una procedura consigliata che impedisce a un singolo pod di consumare tutta la CPU o la memoria disponibile in un nodo.

> [!NOTE]
> ASP.NET Core 3,0 è stato ottimizzato e ottimizzato per l'esecuzione in contenitori con limitazioni di risorse e l'immagine di Docker `dotnet/core/aspnet` imposta una variabile di ambiente per indicare al runtime di `dotnet` che si trova in un contenitore.

#### <a name="the-stockdata-service"></a>Il servizio StockData

La parte del servizio del file YAML dichiara il servizio che fornisce l'accesso ai pod all'interno del cluster.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: stockdata
  namespace: stocks
spec:
  ports:
  - port: 80
  selector:
    run: stockdata
```

La specifica del servizio usa la proprietà `selector` per trovare la corrispondenza con `Pods` in esecuzione, in questo caso la ricerca di Pod con un'etichetta `run: stockdata`. Il `port` specificato nei Pod corrispondenti viene pubblicato dal servizio denominato. Gli altri pod in esecuzione nello spazio dei nomi `stocks` possono accedere a HTTP su questo servizio usando `http://stockdata` come indirizzo. I pod in esecuzione in altri spazi dei nomi possono usare il nome host `http://stockdata.stocks`. È possibile controllare l'accesso al servizio tra gli spazi dei nomi usando i [criteri di rete](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

#### <a name="deploy-the-stockdata-application"></a>Distribuire l'applicazione StockData

Utilizzare `kubectl` per applicare il file di `stockdata.yml` e verificare che la distribuzione e il servizio siano stati creati.

```console
> kubectl apply -f .\stockdata.yml
deployment.apps/stockdata created
service/stockdata created

> kubectl get deployment stockdata --namespace stocks
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
stockdata   1/1     1            1           17s

> kubectl get service stockdata --namespace stocks
NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
stockdata   ClusterIP   10.97.132.103   <none>        80/TCP    33s
```

### <a name="the-stockweb-application"></a>Applicazione StockWeb

Il file di `stockweb.yml` dichiara la distribuzione e il servizio per l'applicazione MVC.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stockweb
  namespace: stocks
spec:
  selector:
    matchLabels:
      run: stockweb
  replicas: 1
  template:
    metadata:
      labels:
        run: stockweb
    spec:
      containers:
      - name: stockweb
        image: stockweb:1.0.0
        imagePullPolicy: Never
        resources:
          limits:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 80
        env:
        - name: StockData__Address
          value: "http://stockdata"
        - name: DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_HTTP2UNENCRYPTEDSUPPORT
          value: "true"

---

apiVersion: v1
kind: Service
metadata:
  name: stockweb
  namespace: stocks
spec:
  type: NodePort
  ports:
  - port: 80
  selector:
    run: stockweb
```

#### <a name="environment-variables"></a>Variabili di ambiente

La sezione `env` dell'oggetto di distribuzione specifica le variabili di ambiente da impostare nel contenitore che esegue le immagini del `stockweb:1.0.0`.

La variabile di ambiente **`StockData__Address`** viene mappata all'impostazione di configurazione `StockData:Address` grazie al provider di configurazione EnvironmentVariables. Questa impostazione Usa doppi caratteri di sottolineatura tra i nomi per separare le sezioni. L'indirizzo USA il nome del servizio `stockdata`, che viene eseguito nello stesso spazio dei nomi Kubernetes.

La variabile di ambiente **`DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_HTTP2UNENCRYPTEDSUPPORT`** imposta un'opzione di <xref:System.AppContext> che consente connessioni http/2 non crittografate per <xref:System.Net.Http.HttpClient>. Questa variabile di ambiente equivale a impostare l'opzione nel codice come illustrato di seguito.

```csharp
AppContext.SetSwitch("System.Net.Http.SocketsHttpHandler.Http2UnencryptedSupport", true);
```

L'uso di una variabile di ambiente per l'opzione indica che l'impostazione può essere facilmente modificata a seconda del contesto in cui l'applicazione è in esecuzione.

#### <a name="service-types"></a>Tipi di servizio

Per rendere accessibile l'applicazione Web dall'esterno del cluster, viene utilizzata la proprietà `type: NodePort`. Questo tipo di proprietà fa in modo che Kubernetes pubblichi la porta 80 nel servizio in una porta arbitraria sui socket di rete esterni del cluster. È possibile trovare la porta assegnata usando il comando `kubectl get service`.

Il servizio `stockdata` non deve essere accessibile dall'esterno del cluster, quindi ha usato il tipo predefinito, `ClusterIP`.

I sistemi di produzione utilizzeranno con maggiore probabilità un servizio di bilanciamento del carico integrato per esporre le applicazioni pubbliche a utenti esterni. I servizi esposti in questo modo devono usare il tipo di `LoadBalancer`.

Per ulteriori informazioni sui tipi di servizio, vedere la documentazione relativa ai [servizi di pubblicazione Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) .

#### <a name="deploy-the-stockweb-application"></a>Distribuire l'applicazione StockWeb

Utilizzare `kubectl` per applicare il file di `stockweb.yml` e verificare che la distribuzione e il servizio siano stati creati.

```console
> kubectl apply -f .\stockweb.yml
deployment.apps/stockweb created
service/stockweb created

> kubectl get deployment stockweb --namespace stocks
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
stockweb   1/1     1            1           8s

> kubectl get service stockweb --namespace stocks
NAME       TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
stockweb   NodePort   10.106.141.5   <none>        80:32564/TCP   13s
```

L'output del comando `get service` Mostra che la porta HTTP è stata pubblicata per la porta `32564` sulla rete esterna; per Docker desktop, questo sarà localhost. È possibile accedere all'applicazione passando a `http://localhost:32564`.

### <a name="testing-the-application"></a>Test dell'applicazione

L'applicazione StockWeb Visualizza un elenco delle scorte del NASDAQ che vengono recuperate da un semplice servizio request/reply. A scopo dimostrativo, ogni riga Mostra anche l'ID univoco dell'istanza del servizio che lo ha restituito.

![Schermata StockWeb](media/kubernetes/stockweb-screenshot.png)

Se il numero di repliche del servizio `stockdata` è stato aumentato, è possibile che il valore del **Server** venga modificato da riga a riga, ma di fatto tutti i record 100 vengono sempre restituiti dalla stessa istanza. Se si aggiorna la pagina a intervalli di pochi secondi, l'ID del server rimane invariato. Perché si verifica questo problema? Ci sono due fattori da giocare qui.

In primo luogo, il sistema di individuazione del servizio Kubernetes usa il bilanciamento del carico "Round Robin" per impostazione predefinita. La prima volta che si esegue una query sul server DNS, viene restituito il primo indirizzo IP corrispondente per il servizio. La volta successiva, l'indirizzo IP successivo nell'elenco e così via fino alla fine, a quel punto viene eseguito il loopback fino all'inizio.

In secondo luogo, il `HttpClient` usato per il client gRPC dell'applicazione StockWeb viene creato e gestito da [ASP.NET Core HttpClientFactory](../microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests.md)e una singola istanza di questo client viene usata per ogni chiamata alla pagina. Il client esegue solo una ricerca DNS, quindi tutte le richieste vengono instradate allo stesso indirizzo IP. Inoltre, poiché il `HttpClientHandler` viene memorizzato nella cache per motivi di prestazioni, più richieste in rapida successione utilizzeranno *tutti* lo stesso indirizzo IP, fino alla scadenza della voce DNS memorizzata nella cache o all'eliminazione dell'istanza del gestore per qualche motivo.

Ciò significa che per impostazione predefinita le richieste a un servizio gRPC non sono bilanciate tra tutte le istanze del servizio nel cluster. Diversi consumer utilizzeranno istanze diverse, ma ciò non garantisce una distribuzione adeguata delle richieste e un uso bilanciato delle risorse.

Il capitolo successivo, [mesh dei servizi](service-mesh.md), esaminerà il modo in cui risolvere questo problema.

>[!div class="step-by-step"]
>[Precedente](docker.md)
>[Successivo](service-mesh.md)
