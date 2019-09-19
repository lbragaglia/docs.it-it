---
title: 'Esercitazione: Analizzare i sentimenti-classificazione binaria'
description: Questa esercitazione illustra come creare un'applicazione Razor Pages che classifica i sentimenti dai commenti del sito Web ed esegue l'azione appropriata. Il classificatore dei sentimenti binari usa il generatore di modelli in Visual Studio.
ms.date: 09/13/2019
author: luisquintanilla
ms.author: luquinta
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: c6184e097daf4604173db9e2a34606e68eb0fdc8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054321"
---
# <a name="tutorial-analyze-sentiment-of-website-comments-in-a-web-application-using-mlnet-model-builder"></a>Esercitazione: Analizzare i sentimenti dei commenti del sito Web in un'applicazione Web usando il generatore di modelli ML.NET

Informazioni su come analizzare i sentimenti dai commenti in tempo reale all'interno di un'applicazione Web.

Questa esercitazione illustra come creare un ASP.NET Core Razor Pages applicazione che classifica i sentimenti dai commenti del sito Web in tempo reale.

In questa esercitazione si imparerà a:

> [!div class="checklist"]
> * Creare un'applicazione Razor Pages ASP.NET Core
> * Preparare e identificare i dati
> * Scegliere uno scenario
> * Caricare i dati
> * Eseguire il training del modello
> * Valutare il modello
> * Usare il modello per le stime

> [!NOTE]
> Il generatore di modelli è attualmente in anteprima.

Il codice sorgente per questa esercitazione è reperibile nel repository [DotNet/machinelearning-Samples](https://github.com/dotnet/machinelearning-samples) .

## <a name="pre-requisites"></a>Prerequisiti

Per un elenco di prerequisiti e istruzioni di installazione, vedere la [Guida all'installazione del generatore di modelli](../how-to-guides/install-model-builder.md).

## <a name="create-a-razor-pages-application"></a>Creare un'applicazione Razor Pages

1. Creare un' **applicazione ASP.NET Core Razor Pages**.

    1. Aprire Visual Studio e selezionare **File > nuovo progetto >** dalla barra dei menu. 
    1. Nella finestra di dialogo Nuovo progetto selezionare il nodo **Visual C#** seguito dal nodo **Web**. 
    1. Selezionare quindi il modello di progetto **Applicazione Web ASP.NET Core**. 
    1. Nella casella di testo **nome** Digitare "SentimentRazor".
    1. Per impostazione predefinita, è necessario selezionare la casella di controllo **Crea una directory per soluzione** . In caso contrario, controllarlo. 
    1. Selezionare il pulsante **OK** .
    1. Scegliere **applicazione Web** nella finestra che consente di visualizzare i diversi tipi di progetti di ASP.NET Core, quindi selezionare il pulsante **OK** .

## <a name="prepare-and-understand-the-data"></a>Preparare e identificare i dati

Scaricare il [set di dati di Wikipedia Detox](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv). Quando si apre la pagina Web, fare clic con il pulsante destro del mouse sulla pagina, scegliere **Salva con nome** e salvare il file in un punto qualsiasi del computer. 

Ogni riga nel set di dati *Wikipedia-Detox-250-line-data. TSV* rappresenta una revisione diversa lasciata da un utente in Wikipedia. La prima colonna rappresenta il sentimento del testo (0 è non tossico, 1 è tossico) e la seconda colonna rappresenta il commento lasciato dall'utente. Le colonne sono separate da tabulazioni. I dati hanno un aspetto simile al seguente:

| Valutazione | SentimentText |
| :---: | :---: |
1 | = = RUDE = = Dude, l'utente non è in grado di caricare nuovamente l'immagine di Carl, altrimenti.
1 | = = OK! = = IM PASSERÀ A VANDALIZZARE WILD A UN WIKI, QUINDI!!!
0 | Spero che questo possa essere utile.

## <a name="choose-a-scenario"></a>Scegliere uno scenario

![](./media/sentiment-analysis-model-builder/model-builder-screen.png)

Per eseguire il training del modello, è necessario scegliere uno scenario di Machine Learning disponibile nell'elenco del generatore di modelli. 

1. In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul progetto *SentimentRazor* e scegliere **Aggiungi** > **Machine Learning**.
1. Per questo esempio, lo scenario è analisi dei sentimenti. Nel passaggio dello *scenario* dello strumento generatore di modelli selezionare lo scenario **analisi del sentiment** .

## <a name="load-the-data"></a>Caricare i dati

Il generatore di modelli accetta dati da due origini, un database SQL Server o un file `csv` locale `tsv` in formato o.

1. Nel passaggio relativo ai dati dello strumento generatore di modelli selezionare **File** dall'elenco a discesa delle origini dati.
1. Selezionare il pulsante accanto alla casella di testo **selezionare un file** e usare Esplora file per cercare e selezionare il file *Wikipedia-Detox-250-line-data. TSV* .
1. Scegliere **la valutazione dell'elenco** **a discesa stima nell'etichetta o nella colonna**
1. Selezionare il collegamento **Train (Train** ) per passare al passaggio successivo nello strumento generatore di modelli.

## <a name="train-the-model"></a>Eseguire il training del modello

L'attività di Machine Learning utilizzata per eseguire il training del modello di stima dei prezzi in questa esercitazione è la classificazione binaria. Durante il processo di training del modello, generatore di modelli esegue il training di modelli distinti usando algoritmi di classificazione binari e impostazioni differenti per trovare il modello di prestazioni migliori per il set di dati.

Il tempo necessario per l'esecuzione del training di ogni modello è proporzionato alla quantità di dati. Generatore di modelli seleziona automaticamente un valore predefinito per il **tempo di training (secondi)** in base alle dimensioni dell'origine dati. 

1. Sebbene generatore di modelli imposti il valore di **tempo per il training (secondi)** su 10 secondi, aumentarlo a 30 secondi. Il training per un periodo di tempo più lungo consente a Generatore di modelli di esplorare un numero maggiore di algoritmi e una combinazione di parametri nella ricerca del modello migliore.
1. Selezionare **Start Training** (Avvia training).

    Durante il processo di training i dati dell'avanzamento vengono visualizzati nella sezione `Progress` del passaggio relativo al training.

    - Stato visualizza lo stato di completamento del processo di training.
    - Precisione migliore visualizza la precisione del modello con le prestazioni migliori individuato dal generatore di modelli. Precisione maggiore indica il modello stimato più correttamente con i dati di test.
    - Algoritmo migliore visualizza il nome dell'algoritmo con le prestazioni migliori individuato dal generatore di modelli.
    - Ultimo algoritmo visualizza il nome dell'algoritmo usato più di recente dal generatore di modelli per eseguire il training del modello.

1. Al termine del training, selezionare il collegamento **Evaluate (valuta** ) per passare al passaggio successivo.

## <a name="evaluate-the-model"></a>Valutare il modello

Il risultato del passaggio relativo al training è rappresentato dal modello con le prestazioni migliori. Nel passaggio di valutazione dello strumento generatore di modelli la sezione di output conterrà l'algoritmo usato dal modello con le prestazioni migliori nella voce **Best model** (Modello migliore), insieme con le metriche in **Best Model Quality (RSquared)** (Qualità modello migliore). Viene visualizzata anche una tabella di riepilogo con i cinque modelli migliori e le metriche relative.

Se non si è soddisfatti della precisione delle metriche,un modo semplice per migliorarla consiste nell'aumentare la durata del training del modello o nell'usare più dati. In caso contrario, selezionare il collegamento al **codice** per passare al passaggio finale nello strumento generatore di modelli.

## <a name="add-the-code-to-make-predictions"></a>Aggiungere il codice per eseguire stime

Il risultato del processo di training sarà la creazione di due progetti.

### <a name="reference-the-trained-model"></a>Riferimento al modello sottoposto a training

1. Nel passaggio del *codice* dello strumento generatore di modelli selezionare **Aggiungi progetti** per aggiungere i progetti generati automaticamente alla soluzione.

    I progetti seguenti dovrebbero essere visualizzati nella **Esplora soluzioni**:

    - *SentimentRazorML. ConsoleApp*: Applicazione console .NET Core che contiene il codice di training e di stima del modello.
    - *SentimentRazorML. Model*: una libreria di classi .NET Standard che contiene i modelli di dati che definiscono lo schema di input e output dei dati del modello, nonché la versione persistente del modello che ha avuto le prestazioni migliori durante il training.

    Per questa esercitazione viene usato solo il progetto *SentimentRazorML. Model* , perché le stime verranno effettuate nell'applicazione Web *SentimentRazor* anziché nella console. Sebbene *SentimentRazorML. ConsoleApp* non venga usato per l'assegnazione dei punteggi, può essere usato per ripetere il training del modello usando nuovi dati in un secondo momento. Tuttavia, la ripetizione del training esula dall'ambito di questa esercitazione.

1. Per usare il modello sottoposto a training all'interno dell'applicazione Razor Pages, aggiungere un riferimento al progetto *SentimentRazorML. Model* .

    1. Fare clic con il pulsante destro del mouse su progetto **SentimentRazor** . 
    1. Selezionare **Aggiungi riferimento >** . 
    1. Selezionare il nodo **progetti > soluzione** e nell'elenco selezionare il progetto **SentimentRazorML. Model** .
    1. Selezionare **OK**.

### <a name="configure-the-predictionengine-pool"></a>Configurare il pool di PredictionEngine

Per effettuare una singola previsione, usare [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602). Per poter usare [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) nell'applicazione, è necessario crearlo quando necessario. In tal caso, una procedura consigliata da prendere in considerazione è l'inserimento delle dipendenze.

> [!WARNING]
> [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) non è thread-safe. Per migliorare le prestazioni e le capacità di thread safety, usare il servizio `PredictionEnginePool` che crea una classe [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) di oggetti `PredictionEngine` per l'uso da parte dell'applicazione. Leggere il post di blog seguente per altre informazioni su come [creare e usare pool di oggetti `PredictionEngine` in ASP.NET Core](https://devblogs.microsoft.com/cesardelatorre/how-to-optimize-and-run-ml-net-models-on-scalable-asp-net-core-webapis-or-web-apps/). 

1. Installare il pacchetto NuGet *Microsoft.Extensions.ml* :

    1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**. 
    1. Scegliere "nuget.org" come origine del pacchetto. 
    1. Selezionare la scheda **Sfoglia** e cercare **Microsoft.Extensions.ml**. 
    1. Selezionare il pacchetto nell'elenco e fare clic sul pulsante **Installa** . 
    1. Selezionare il pulsante **OK** nella finestra di dialogo **Anteprima modifiche**
    1. Selezionare il pulsante **Accetto** nella finestra di dialogo **accettazione della licenza** se si accettano le condizioni di licenza per i pacchetti elencati. 

1. Aprire il file *Startup.cs* nel progetto *SentimentRazor* .
1. Aggiungere le istruzioni using seguenti per fare riferimento al pacchetto NuGet *Microsoft.Extensions.ml* e al progetto *SentimentRazorML. Model* :

    [!code-csharp [StartupUsings](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L12-L14)]        

1. Creare una variabile globale per archiviare il percorso del file di modello sottoposto a training.

    [!code-csharp [ModelPath](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L20)]

1. Il file del modello viene archiviato nella directory di compilazione insieme ai file di assembly dell'applicazione. Per semplificare l'accesso, creare un metodo helper chiamato `GetAbsolutePath` dopo il `Configure` metodo.

    [!code-csharp [GetAbsolutePathMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L66-L73)]

1. Usare il `GetAbsolutePath` metodo `Startup` nel costruttore della `_modelPath`classe per impostare.

    [!code-csharp [InitModelPath](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L25)]

1. Configurare per l'applicazione `ConfigureServices` nel metodo: `PredictionEnginePool`

    [!code-csharp [InitPredEnginePool](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L42)]

### <a name="create-sentiment-analysis-handler"></a>Crea gestore analisi dei sentimenti

Le stime verranno effettuate nella pagina principale dell'applicazione. Pertanto, un metodo che accetta l'input dell'utente e utilizza `PredictionEnginePool` per restituire una stima deve essere aggiunta.

1. Aprire il file *index.cshtml.cs* che si trova nella directory *pages* e aggiungere le istruzioni using seguenti:

    [!code-csharp [IndexUsings](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L7-L8)]

    Per utilizzare l'oggetto `PredictionEnginePool` configurato `Startup` nella classe, è necessario inserirlo nel costruttore del modello in cui si desidera utilizzarlo. 

1. Aggiungere una variabile per fare riferimento `PredictionEnginePool` all'oggetto `IndexModel` all'interno della classe.

    [!code-csharp [PredEnginePool](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L14)]

1. Creare un costruttore nella `IndexModel` classe e inserire il `PredictionEnginePool` servizio al suo interno.

    [!code-csharp [IndexConstructor](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L16-L19)]

1. Creare un gestore metodo che usi `PredictionEnginePool` per eseguire stime dall'input dell'utente ricevuto dalla pagina Web.

    1. Sotto il `OnGet` metodo, creare un nuovo metodo denominato`OnGetAnalyzeSentiment`

        ```csharp
        public IActionResult OnGetAnalyzeSentiment([FromQuery] string text)
        {

        }
        ```

    1. All'interno `OnGetAnalyzeSentiment` del metodo, restituisce un sentimento *neutro* se l'input dell'utente è vuoto o null.

        [!code-csharp [InitInput](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L28)] 
    
    1. Dato un input valido, creare una nuova istanza di `ModelInput`. 

        [!code-csharp [InitInput](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L29)] 

    1. Usare per `PredictionEnginePool` stimare i sentimenti.

        [!code-csharp [MakePrediction](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L30)] 

    1. Convertire il `bool` valore stimato in tossico o non tossico con il codice seguente.

        [!code-csharp [ConvertPrediction](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L31)]

    1. Infine, restituire le opinioni alla pagina Web.

        [!code-csharp [ReturnSentiment](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L32)]

### <a name="configure-the-web-page"></a>Configurare la pagina Web

I risultati restituiti da `OnGetAnalyzeSentiment` verranno visualizzati dinamicamente `Index` nella pagina Web.

1. Aprire il file *index. cshtml* nella directory *pages* e sostituirne il contenuto con il codice seguente: 

    [!code-cshtml [IndexPage](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml)]

1. Aggiungere quindi il codice di stile CSS alla fine della pagina *site. CSS* nella directory *wwwroot\css* :

    [!code-css [CssStyling](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/css/site.css#L61-L105)]

1. Successivamente, aggiungere il `OnGetAnalyzeSentiment` codice per inviare input dalla pagina Web al gestore.

    1. Nel file *site. js* che si trova nella directory *wwwroot\js* creare una funzione chiamata `getSentiment` per effettuare una richiesta GET HTTP `OnGetAnalyzeSentiment` con l'input dell'utente al gestore.

        [!code-javascript [GetSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L5-L10)]

    1. Di seguito, aggiungere un'altra funzione `updateMarker` chiamata per aggiornare dinamicamente la posizione del marcatore nella pagina Web in modo che il sentimento venga stimato.

        [!code-javascript [UpdateMarkerMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L12-L15)]

    1. Creare una funzione del gestore eventi `updateSentiment` chiamata per ottenere l'input dall'utente, inviarlo `OnGetAnalyzeSentiment` alla funzione utilizzando la `getSentiment` funzione e aggiornare il marcatore con la `updateMarker` funzione.

        [!code-javascript [UpdateSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L17-L34)]

    1. Infine, registrare il gestore eventi e associarlo all' `textarea` elemento con l' `id=Message` attributo.

        [!code-javascript [UpdateSentimentEvtHandler](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L36)]

## <a name="run-the-application"></a>Esecuzione dell'applicazione

Ora che l'applicazione è configurata, eseguire l'applicazione che dovrebbe essere avviata nel browser.

Quando l'applicazione viene avviata, immettere *Generatore di modelli è interessante.* nell'area di testo. Il sentimento stimato visualizzato non deve essere *tossico*.

![](./media/sentiment-analysis-model-builder/web-app.png)

Se è necessario fare riferimento ai progetti generati dal generatore di modelli in un secondo momento all'interno di un'altra soluzione, è possibile `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` trovarli nella directory.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:
> [!div class="checklist"]
> * Creare un'applicazione Razor Pages ASP.NET Core
> * Preparare e identificare i dati
> * Scegliere uno scenario
> * Caricare i dati
> * Eseguire il training del modello
> * Valutare il modello
> * Usare il modello per le stime

### <a name="additional-resources"></a>Risorse aggiuntive

Per altre informazioni sugli argomenti presentati in questa esercitazione, vedere le risorse seguenti:

- [Scenari del generatore di modelli](../automate-training-with-model-builder.md#scenarios)
- [Classificazione binaria](../resources/glossary.md#binary-classification)
- [Metriche del modello di classificazione binaria](../resources/metrics.md#metrics-for-binary-classification)