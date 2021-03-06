---
title: Configurazione delle funzionalità di traccia
ms.date: 03/30/2017
helpviewer_keywords:
- tracing [WCF]
ms.assetid: 82922010-e8b3-40eb-98c4-10fc05c6d65d
ms.openlocfilehash: bc23aff2f049f205d02e2fb1b5f8798c7f6a9931
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044230"
---
# <a name="configuring-tracing"></a>Configurazione delle funzionalità di traccia
In questo argomento viene illustrato come attivare la funzionalità di traccia, configurare origini di traccia affinché vengano create tracce e impostati livelli di traccia, impostare traccia e propagazione di attività per supportare la correlazione tra tracce end-to-end e configurare i listener di traccia affinché accedano alle tracce.  
  
 Per indicazioni sulle impostazioni di traccia in ambiente di produzione o di debug, vedere [le impostazioni consigliate per la traccia e la registrazione dei messaggi](../../../../../docs/framework/wcf/diagnostics/tracing/recommended-settings-for-tracing-and-message-logging.md).  
  
> [!IMPORTANT]
> In Windows 8 è necessario eseguire l'applicazione con privilegi elevati (Esegui come amministratore) affinché l'applicazione generi i log di traccia.  
  
## <a name="enabling-tracing"></a>Abilitazione della traccia  
 Windows Communication Foundation (WCF) restituisce i dati seguenti per la traccia diagnostica:  
  
- Tracce per le attività cardine dei processi in tutti i componenti delle applicazioni, ad esempio chiamate dell'operazione, eccezioni del codice, avvisi e altri eventi di elaborazione significativi.  
  
- Eventi di errore di Windows quando la funzionalità di traccia non viene eseguita correttamente. Vedere [registrazione degli eventi](../../../../../docs/framework/wcf/diagnostics/event-logging/index.md).  
  
 La traccia WCF è basata su <xref:System.Diagnostics>. Per utilizzare la funzionalità di traccia, è necessario definire le origini di traccia nel file di configurazione o nel codice. WCF definisce un'origine di traccia per ogni assembly WCF. L' `System.ServiceModel` origine di traccia è l'origine di traccia WCF più generale e registra le attività cardine di elaborazione nello stack di comunicazione WCF, dall'immissione/uscita dal trasporto all'immissione o all'uscita del codice utente. L'origine della traccia `System.ServiceModel.MessageLogging` registra tutti i messaggi che vengono propagati nel sistema.  
  
 Per impostazione predefinita, la traccia non è attivata. Per attivare la traccia, è necessario creare un listener di traccia e impostare un livello di traccia diverso da "off" per l'origine di traccia selezionata nella configurazione; in caso contrario, WCF non genera alcuna traccia. Se non si specifica un listener, la traccia verrà disattivata automaticamente. Se viene definito un listener ma non è specificato alcun livello, per impostazione predefinita viene selezionato il livello "Disattivo", ovvero non viene generata alcuna traccia.  
  
 Se si usano punti di estendibilità WCF, ad esempio invoker di operazioni personalizzati, è necessario creare tracce personalizzate. Questo perché se si implementa un punto di estendibilità, WCF non può più creare le tracce standard nel percorso predefinito. Se non si implementa il supporto della traccia manuale creando tracce, è possibile che le tracce previste non vengano visualizzate.  
  
 È possibile configurare la funzionalità di traccia modificando il file di configurazione dell'applicazione, Web.config per applicazioni di tipo host Web o Appname.exe.config per applicazioni indipendenti. Di seguito è riportato un esempio di modifica applicabile. Per ulteriori informazioni su queste impostazioni, vedere la sezione "configurazione dei listener di traccia per l'utilizzo di tracce".  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <sources>  
            <source name="System.ServiceModel"   
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
            <listeners>  
               <add name="traceListener"   
                   type="System.Diagnostics.XmlWriterTraceListener"   
                   initializeData= "c:\log\Traces.svclog" />  
            </listeners>  
         </source>  
      </sources>  
   </system.diagnostics>  
</configuration>  
```  
  
> [!NOTE]
> Per modificare il file di configurazione di un progetto di servizio WCF in Visual Studio, fare clic con il pulsante destro del mouse sul file di configurazione dell'applicazione, ovvero Web. config per le applicazioni ospitate sul Web o Appname. exe. config per l'applicazione self-hosted in **Esplora soluzioni**. Scegliere quindi la voce del menu di scelta rapida **modifica configurazione WCF** . Verrà avviato lo [strumento Editor di configurazione (SvcConfigEditor. exe)](../../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md), che consente di modificare le impostazioni di configurazione per i servizi WCF usando un'interfaccia utente grafica.  
  
## <a name="configuring-trace-sources-to-emit-traces"></a>Configurazione delle origini di traccia per la generazione di tracce  
 WCF definisce un'origine di traccia per ogni assembly. I listener definiti per tale origine accedono alle tracce generate all'interno di un assembly. Vengono definite le origini di traccia seguenti:  
  
- System.ServiceModel: Registra tutte le fasi dell'elaborazione WCF, ogni volta che viene letta la configurazione, un messaggio viene elaborato in trasporto, elaborazione della sicurezza, un messaggio viene inviato nel codice utente e così via.  
  
- System.ServiceModel.MessageLogging: Registra tutti i messaggi che passano attraverso il sistema.  
  
- System.IdentityModel.  
  
- System.ServiceModel.Activation.  
  
- System.IO.Log: Registrazione per l'interfaccia .NET Framework al Common Log File System (CLFS).  
  
- System.Runtime.Serialization: Registra quando gli oggetti vengono letti o scritti.  
  
- CardSpace.  
  
 È possibile configurare ogni origine di traccia per l'utilizzo dello stesso listener (condiviso), come indicato nell'esempio di configurazione seguente.  
  
```xml  
<configuration>  
    <system.diagnostics>  
        <sources>  
            <source name="System.ServiceModel"   
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="CardSpace">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.IO.Log">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.Runtime.Serialization">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.IdentityModel">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
        </sources>  
  
        <sharedListeners>  
            <add name="xml"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="c:\log\Traces.svclog" />  
        </sharedListeners>  
    </system.diagnostics>  
</configuration>  
```  
  
 È inoltre possibile aggiungere origini di traccia definite dall'utente, come dimostrato nell'esempio seguente, in modo che vengano create tracce di codice utente.  
  
```xml  
<system.diagnostics>  
   <sources>  
       <source name="UserTraceSource" switchValue="Warning, ActivityTracing" >  
          <listeners>  
              <add name="xml"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="C:\logs\UserTraces.svclog" />  
          </listeners>  
       </source>  
   </sources>  
   <trace autoflush="true" />   
</system.diagnostics>  
```  
  
 Per ulteriori informazioni sulla creazione di origini di traccia definite dall'utente, vedere [estensione della traccia](../../../../../docs/framework/wcf/samples/extending-tracing.md).  
  
## <a name="configuring-trace-listeners-to-consume-traces"></a>Configurazione dei listener di traccia per l'utilizzo di tracce  
 In fase di esecuzione, WCF inserisce i dati di traccia nei listener che elaborano i dati. WCF fornisce diversi listener predefiniti per <xref:System.Diagnostics>, che differiscono dal formato utilizzato per l'output. È inoltre possibile aggiungere tipi di listener personalizzati.  
  
 È possibile utilizzare l'istruzione `add` per specificare il nome e il tipo del listener di traccia che si desidera utilizzare. Nella configurazione di esempio, il listener viene denominato `traceListener` e viene aggiunto il listener di traccia standard di .NET Framework, ovvero `System.Diagnostics.XmlWriterTraceListener`, come tipo da utilizzare. Per ogni origine di traccia è possibile aggiungere il numero desiderato di listener. Se il listener di traccia genera la traccia in un file, nel file di configurazione è necessario specificare il percorso e il nome del file di output. A tal fine impostare `initializeData` sul nome del file per quel listener. Se non si specifica un nome file, viene generato un nome file a caso in base al tipo di listener utilizzato. Se viene utilizzato <xref:System.Diagnostics.XmlWriterTraceListener>, viene generato un nome file senza estensione. Se si implementa un listener personalizzato, è inoltre possibile utilizzare questo attributo per ricevere dati di inizializzazione diversi dal nome file. È ad esempio possibile specificare un identificatore di database per questo attributo.  
  
 È possibile configurare un listener di traccia personalizzato per l'invio di tracce in transito, ad esempio a un database remoto. I distributori di applicazioni devono applicare un apposito controllo di accesso nei log di traccia del computer remoto.  
  
 È inoltre possibile configurare un listener di traccia a livello di programmazione. Per altre informazioni, vedere [Procedura: Creare e inizializzare listener](https://go.microsoft.com/fwlink/?LinkId=94648) di traccia e [creare un TraceListener personalizzato](https://go.microsoft.com/fwlink/?LinkId=96239).  
  
> [!CAUTION]
> Poiché `System.Diagnostics.XmlWriterTraceListener` non è thread-safe, è possibile che l'origine di traccia blocchi le risorse in modo esclusivo durante la restituzione di tracce. Quando molti thread restituiscono tracce a un'origine configurata per l'utilizzo di questo listener, può verificarsi un conflitto di risorse con conseguente calo delle prestazioni. Per risolvere il problema, è necessario implementare un listener personalizzato di tipo thread-safe.  
  
## <a name="trace-level"></a>Livello di traccia  
 Il livello di traccia viene controllato in base all'impostazione `switchValue` dell'origine di traccia. Nella tabella seguente viene fornita una descrizione dei livelli di traccia disponibili.  
  
|Livello di traccia|Natura degli eventi registrati|Contenuto degli eventi registrati|Eventi registrati|Destinazione utente|  
|-----------------|----------------------------------|-----------------------------------|--------------------|-----------------|  
|Off|N/D|N/D|Non vengono create tracce.|N/D|  
|Critico|Eventi "negativi": eventi che indicano un'elaborazione imprevista o una condizione di errore.||Vengono registrate eccezioni non gestite comprese le seguenti:<br /><br /> -OutOfMemoryException<br />-ThreadAbortException (CLR richiama qualsiasi ThreadAbortExceptionHandler)<br />-StackOverflowException (non può essere intercettato)<br />-ConfigurationErrorsException<br />-SEHException<br />-Errori di avvio dell'applicazione<br />-Eventi FailFast<br />-Blocco del sistema<br />-Messaggi non elaborabili: tracce del messaggio che provocano un errore dell'applicazione.|Administrators<br /><br /> Sviluppatori di applicazioni|  
|Errore|Eventi "negativi": eventi che indicano un'elaborazione imprevista o una condizione di errore.|Si è verificata un'elaborazione imprevista. L'applicazione non è stata in grado di eseguire un'attività come previsto. L'applicazione, tuttavia, è ancora in esecuzione.|Vengono registrate tutte le eccezioni.|Administrators<br /><br /> Sviluppatori di applicazioni|  
|Avviso|Eventi "negativi": eventi che indicano un'elaborazione imprevista o una condizione di errore.|Un possibile problema si è verificato o potrebbe verificarsi, ma l'applicazione funziona ancora correttamente. Tuttavia, potrebbe smettere di farlo.|-L'applicazione riceve più richieste di quanto consentito dalle impostazioni di limitazione delle richieste.<br />-La coda di ricezione si avvicina alla capacità massima configurata.<br />-Il timeout è stato superato.<br />-Le credenziali vengono rifiutate.|Administrators<br /><br /> Sviluppatori di applicazioni|  
|Informazioni|Eventi "positivi": eventi che contrassegnano attività cardine riuscite|Attività cardine importanti e corrette di esecuzione dell'applicazione, indipendentemente dal funzionamento corretto o non corretto dell'applicazione.|In generale il sistema genera messaggi informativi utili per il monitoraggio e la diagnosi dello stato di sistema, la valutazione delle prestazioni o il profiling. È possibile utilizzare queste informazioni per la pianificazione della capacità e la gestione delle prestazioni:<br /><br /> -I canali vengono creati.<br />-Vengono creati i listener di endpoint.<br />-Il messaggio immette/lascia il trasporto.<br />-Il token di sicurezza viene recuperato.<br />-Viene letta l'impostazione di configurazione.|Administrators<br /><br /> Sviluppatori di applicazioni<br /><br /> Sviluppatori di prodotti|  
|Dettagliato|Eventi "positivi": eventi che contrassegnano le attività cardine riuscite.|Vengono generati eventi di basso livello per codice utente e manutenzione.|In genere è possibile utilizzare questo livello per il debug o l'ottimizzazione dell'applicazione.<br /><br /> -Intestazione del messaggio riconosciuta.|Administrators<br /><br /> Sviluppatori di applicazioni<br /><br /> Sviluppatori di prodotti|  
|ActivityTracing||Eventi di flusso tra attività di elaborazione e componenti.|Questo livello consente ad amministratori e sviluppatori di mettere in correlazione applicazioni nello stesso dominio applicazione:<br /><br /> : Tracce per i limiti delle attività, ad esempio Start/Stop.<br />: Tracce per i trasferimenti.|Tutti|  
|Tutti||L'applicazione può funzionare correttamente. Vengono generati tutti gli eventi.|Tutti gli eventi precedenti.|Tutti|  
  
 I livelli da Dettagliato a Critico sono inclusi l'uno dentro l'altro, ovvero ogni livello di traccia comprende tutti i livelli che lo precedono ad eccezione del livello Disattivo. Un listener in ascolto al livello Avviso, ad esempio, riceve le tracce Critico, Errore e Avviso. Il livello Tutto comprende gli eventi da Dettagliato a Critico ed eventi di Traccia attività.  
  
> [!CAUTION]
> I livelli Informazioni, Dettagliato e ActivityTracing generano molte tracce che possono influire negativamente sulla velocità effettiva dei messaggi se tutte le risorse disponibili nel computer sono esaurite.  
  
## <a name="configuring-activity-tracing-and-propagation-for-correlation"></a>Configurazione della traccia e della propagazione di attività a fini di correlazione  
 Il valore `activityTracing` specificato per l'attributo `switchValue` consente di attivare la traccia di attività, che genera tracce per limiti e trasferimenti di attività all'interno di endpoint.  
  
> [!NOTE]
> Quando si utilizzano determinate funzionalità di estendibilità in WCF, è possibile <xref:System.NullReferenceException> ottenere un oggetto quando la traccia attività è abilitata. Per risolvere questo problema, controllare il file di configurazione dell'applicazione e verificare che l'attributo `switchValue` per l'origine di traccia non sia impostato su `activityTracing`.  
  
 L'attributo `propagateActivity` indica se l'attività deve essere propagata ad altri endpoint che partecipano nello scambio di messaggi. Impostando questo valore su `true`, è possibile osservare file di traccia generati da due endpoint qualsiasi e notare come un set di tracce in un endpoint venga propagato a un set di tracce in un altro endpoint.  
  
 Per ulteriori informazioni sulla traccia e la propagazione delle attività, vedere [propagazione](../../../../../docs/framework/wcf/diagnostics/tracing/propagation.md).  
  
 Entrambi `propagateActivity` i `ActivityTracing` valori booleani e si applicano a System. ServiceModel TraceSource. Il `ActivityTracing` valore si applica anche a qualsiasi origine di traccia, inclusi WCF o quelli definiti dall'utente.  
  
 Non è possibile utilizzare l'attributo `propagateActivity` con le origini di traccia definite dall'utente. Per la propagazione di ID attività di codice utente, accertarsi di non impostare l'attributo `ActivityTracing` di ServiceModel, mantenendo l'attributo `propagateActivity` di ServiceModel impostato su `true`.  
  
## <a name="see-also"></a>Vedere anche

- [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)
- [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)
- [Procedura: Creare e inizializzare listener di traccia](https://go.microsoft.com/fwlink/?LinkId=94648)
- [Creazione di un oggetto TraceListener personalizzato](https://go.microsoft.com/fwlink/?LinkId=96239)
