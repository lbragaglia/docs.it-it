---
title: Raccolta di dati di telemetria dall'interfaccia della riga di comando di ML.NET
description: Informazioni sulle funzionalità di telemetria dell'interfaccia della riga di comando di ML.NET che raccolgono dati di utilizzo per l'analisi, su come disabilitare le funzionalità e sui dati raccolti. Sono inoltre disponibili collegamenti al contratto di licenza di .NET e informazioni sulla conformità a GDPR di Microsoft.
ms.topic: conceptual
ms.date: 05/05/2019
ms.custom: ''
ms.openlocfilehash: 94c66267dfeec4b70ba4dd1fc47518eb0e01509a
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053580"
---
# <a name="telemetry-collection-by-the-mlnet-cli"></a><span data-ttu-id="27327-104">Raccolta di dati di telemetria dall'interfaccia della riga di comando di ML.NET</span><span class="sxs-lookup"><span data-stu-id="27327-104">Telemetry collection by the ML.NET CLI</span></span>

<span data-ttu-id="27327-105">L'[interfaccia della riga di comando di ML.NET](http://aka.ms/mlnet-cli) include una funzionalità di telemetria che raccoglie dati di utilizzo anonimi che vengono aggregati per l'uso da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27327-105">The [ML.NET CLI](http://aka.ms/mlnet-cli) includes a telemetry feature that collects anonymous usage data that is aggregated for use by Microsoft.</span></span>

## <a name="how-microsoft-uses-the-data"></a><span data-ttu-id="27327-106">Come Microsoft usa i dati</span><span class="sxs-lookup"><span data-stu-id="27327-106">How Microsoft uses the data</span></span>

<span data-ttu-id="27327-107">Il team di prodotto usa i dati di telemetria dell'interfaccia della riga di comando di ML.NET per capire come migliorare gli strumenti che propone.</span><span class="sxs-lookup"><span data-stu-id="27327-107">The product team uses ML.NET CLI telemetry data to help understand how to improve the tools.</span></span> <span data-ttu-id="27327-108">Se i clienti utilizzano raramente una particolare attività di Machine Learning, ad esempio, il team di prodotto indaga sul motivo e usa i risultati per stabilire le priorità delle funzionalità da sviluppare in futuro.</span><span class="sxs-lookup"><span data-stu-id="27327-108">For example, if customers infrequently use a particular machine learning task, the product team investigates why and uses findings to prioritize feature development.</span></span> <span data-ttu-id="27327-109">I dati di telemetria dell'interfaccia della riga di comando di ML.NET sono utili anche per il debug dei problemi, ad esempio gli arresti anomali del sistema e le anomalie di codice.</span><span class="sxs-lookup"><span data-stu-id="27327-109">ML.NET CLI telemetry also helps with debugging of issues such as crashes and code anomalies.</span></span> 

<span data-ttu-id="27327-110">Nonostante il team di prodotto gradisca disporre di questo tipo di informazioni, Microsoft è consapevole che non tutti gli utenti sono disposti a inviare i dati.</span><span class="sxs-lookup"><span data-stu-id="27327-110">While the product team appreciates this insight, we also know that not everyone wants to send this data.</span></span> [<span data-ttu-id="27327-111">Informazioni su come disabilitare i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="27327-111">Find out how to disable telemetry.</span></span>](#opt-out-of-data-collection)

## <a name="scope"></a><span data-ttu-id="27327-112">Ambito</span><span class="sxs-lookup"><span data-stu-id="27327-112">Scope</span></span>

<span data-ttu-id="27327-113">Il comando `mlnet` avvia l'interfaccia della riga di comando di ML.NET, ma non raccoglie i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="27327-113">The `mlnet` command launches the ML.NET CLI, but the command itself doesn't collect telemetry.</span></span>

<span data-ttu-id="27327-114">La funzionalità di telemetria *non è abilitata* quando si esegue il comando `mlnet` con nessun altro comando collegato.</span><span class="sxs-lookup"><span data-stu-id="27327-114">Telemetry *isn't enabled* when you run the `mlnet` command with no other command attached.</span></span> <span data-ttu-id="27327-115">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="27327-115">For example:</span></span>

- `mlnet`
- `mlnet --help`

<span data-ttu-id="27327-116">La funzionalità di telemetria *è abilitata* quando si esegue un [comando dell'interfaccia della riga di comando di ML.NET](../reference/ml-net-cli-reference.md), ad esempio `mlnet auto-train`.</span><span class="sxs-lookup"><span data-stu-id="27327-116">Telemetry *is enabled* when you run an [ML.NET CLI command](../reference/ml-net-cli-reference.md), such as `mlnet auto-train`.</span></span>

## <a name="opt-out-of-data-collection"></a><span data-ttu-id="27327-117">Rifiutare esplicitamente la raccolta dei dati</span><span class="sxs-lookup"><span data-stu-id="27327-117">Opt out of data collection</span></span>

<span data-ttu-id="27327-118">La funzionalità di telemetria dell'interfaccia della riga di comando di ML.NET è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="27327-118">The ML.NET CLI telemetry feature is enabled by default.</span></span>

<span data-ttu-id="27327-119">Rifiutare esplicitamente la funzionalità di telemetria impostando la variabile di ambiente `DOTNET_CLI_TELEMETRY_OPTOUT` su `1` o `true`.</span><span class="sxs-lookup"><span data-stu-id="27327-119">Opt out of the telemetry feature by setting the `DOTNET_CLI_TELEMETRY_OPTOUT` environment variable to `1` or `true`.</span></span> <span data-ttu-id="27327-120">Questa variabile di ambiente viene applicata a livello globale allo strumento dell'interfaccia della riga di comando di .NET.</span><span class="sxs-lookup"><span data-stu-id="27327-120">This environment variable applies globally to the .NET CLI tool.</span></span>

## <a name="data-points-collected"></a><span data-ttu-id="27327-121">Punti dati raccolti</span><span class="sxs-lookup"><span data-stu-id="27327-121">Data points collected</span></span>

<span data-ttu-id="27327-122">La funzionalità raccoglie i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="27327-122">The feature collects the following data:</span></span>

- <span data-ttu-id="27327-123">Il comando che è stato richiamato, ad esempio `auto-train`</span><span class="sxs-lookup"><span data-stu-id="27327-123">What command was invoked, such as `auto-train`</span></span>
- <span data-ttu-id="27327-124">I nomi dei parametri della riga di comando usati (ad esempio "dataset-name, label-column-name, ml-task, output-path, max-exploration-time, verbosity")</span><span class="sxs-lookup"><span data-stu-id="27327-124">Command-line parameter names used (i.e. "dataset-name, label-column-name, ml-task, output-path, max-exploration-time, verbosity")</span></span>
- <span data-ttu-id="27327-125">Indirizzo MAC con hash: ID univoco e anonimo dal punto di vista crittografico (SHA256) per un computer</span><span class="sxs-lookup"><span data-stu-id="27327-125">Hashed MAC address: a cryptographically (SHA256) anonymous and unique ID for a machine</span></span>
- <span data-ttu-id="27327-126">Il timestamp di una chiamata</span><span class="sxs-lookup"><span data-stu-id="27327-126">Timestamp of an invocation</span></span>
- <span data-ttu-id="27327-127">Indirizzo IP a tre ottetti (non l'indirizzo IP completo) usato solo per determinare la posizione geografica</span><span class="sxs-lookup"><span data-stu-id="27327-127">Three octet IP address (not full IP address) used only to determine geographical location</span></span>
- <span data-ttu-id="27327-128">Nome di tutti gli argomenti e dei parametri usati.</span><span class="sxs-lookup"><span data-stu-id="27327-128">Name of all arguments/parameters used.</span></span> <span data-ttu-id="27327-129">Non i valori del cliente, ad esempio le stringhe</span><span class="sxs-lookup"><span data-stu-id="27327-129">Not the customer's values, such as strings</span></span>
- <span data-ttu-id="27327-130">Nome di file del set di dati con hash</span><span class="sxs-lookup"><span data-stu-id="27327-130">Hashed dataset filename</span></span>
- <span data-ttu-id="27327-131">Bucket delle dimensioni di file del set di dati</span><span class="sxs-lookup"><span data-stu-id="27327-131">Dataset file-size bucket</span></span>
- <span data-ttu-id="27327-132">Sistema operativo e versione</span><span class="sxs-lookup"><span data-stu-id="27327-132">Operating system and version</span></span>
- <span data-ttu-id="27327-133">Valore del parametro --task: Valori di categorie, ad esempio `regression`, `binary-classification` e `multiclass-classification`</span><span class="sxs-lookup"><span data-stu-id="27327-133">Value of --task parameter: Categorical values, such as `regression`, `binary-classification`, and `multiclass-classification`</span></span>
- <span data-ttu-id="27327-134">Versione dell'interfaccia della rigaa di comando ML.NET (vale a dire 0.3.27703.4)</span><span class="sxs-lookup"><span data-stu-id="27327-134">ML.NET CLI version (i.e. 0.3.27703.4)</span></span>

<span data-ttu-id="27327-135">I dati vengono inviati ai server Microsoft in modalità protetta grazie alla tecnologia [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), conservati con accesso limitato e usati in base a severi controlli di sicurezza da parte di sistemi di [archiviazione di Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="27327-135">The data is sent securely to Microsoft servers using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) technology, held under restricted access, and used under strict security controls from secure [Azure Storage](https://azure.microsoft.com/services/storage/) systems.</span></span>

### <a name="data-points-not-collected"></a><span data-ttu-id="27327-136">Punti dati non raccolti</span><span class="sxs-lookup"><span data-stu-id="27327-136">Data points not collected</span></span>
<span data-ttu-id="27327-137">La funzionalità di telemetria *non* raccoglie:</span><span class="sxs-lookup"><span data-stu-id="27327-137">The telemetry feature *doesn't* collect:</span></span>
- <span data-ttu-id="27327-138">dati personali, ad esempio i nomi utente</span><span class="sxs-lookup"><span data-stu-id="27327-138">personal data, such as usernames</span></span>
- <span data-ttu-id="27327-139">nomi dei set di dati</span><span class="sxs-lookup"><span data-stu-id="27327-139">dataset filenames</span></span>
- <span data-ttu-id="27327-140">dati dei set di dati</span><span class="sxs-lookup"><span data-stu-id="27327-140">data from dataset files</span></span>

<span data-ttu-id="27327-141">Se si sospetta che la funzionalità di telemetria dell'interfaccia della riga di comando di ML.NET raccolga dati sensibili o che i dati raccolti siano gestiti in modo inappropriato o non sicuro, segnalare un problema nel repository di [ML.NET](https://github.com/dotnet/machinelearning).</span><span class="sxs-lookup"><span data-stu-id="27327-141">If you suspect that the ML.NET CLI telemetry is collecting sensitive data or that the data is being insecurely or inappropriately handled, file an issue in the [ML.NET](https://github.com/dotnet/machinelearning) repository for investigation.</span></span>

## <a name="license"></a><span data-ttu-id="27327-142">Licenza</span><span class="sxs-lookup"><span data-stu-id="27327-142">License</span></span>

<span data-ttu-id="27327-143">La distribuzione dell'interfaccia della riga di comando di ML.NET da parte di Microsoft è concessa secondo le [Condizioni di licenza software Microsoft: Microsoft .NET Library](https://aka.ms/dotnet-core-eula).</span><span class="sxs-lookup"><span data-stu-id="27327-143">The Microsoft distribution of ML.NET CLI is licensed with the [Microsoft Software License Terms: Microsoft .NET Library](https://aka.ms/dotnet-core-eula).</span></span> <span data-ttu-id="27327-144">Per informazioni dettagliate sulla raccolta e l'elaborazione dei dati, vedere la sezione intitolata "DATA".</span><span class="sxs-lookup"><span data-stu-id="27327-144">For details on data collection and processing, see the section entitled "Data."</span></span>

## <a name="disclosure"></a><span data-ttu-id="27327-145">Divulgazione</span><span class="sxs-lookup"><span data-stu-id="27327-145">Disclosure</span></span>

<span data-ttu-id="27327-146">Quando si esegue un [comando dell'interfaccia della riga di comando di ML.NET](../reference/ml-net-cli-reference.md) per la prima volta, ad esempio `mlnet auto-train`, lo strumento dell'interfaccia della riga di comando di ML.NET visualizza un avviso sulla divulgazione di informazioni che spiega come rifiutare esplicitamente la funzionalità di telemetria.</span><span class="sxs-lookup"><span data-stu-id="27327-146">When you first run a [ML.NET CLI command](../reference/ml-net-cli-reference.md) such as `mlnet auto-train`, the ML.NET CLI tool displays disclosure text that tells you how to opt out of telemetry.</span></span> <span data-ttu-id="27327-147">Il testo potrebbe variare lievemente in funzione della versione dell'interfaccia della riga di comando in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="27327-147">Text may vary slightly depending on the version of the CLI you're running.</span></span>

## <a name="see-also"></a><span data-ttu-id="27327-148">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="27327-148">See also</span></span>
- [<span data-ttu-id="27327-149">Riferimento interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="27327-149">ML.NET CLI reference</span></span>](../reference/ml-net-cli-reference.md)
- [<span data-ttu-id="27327-150">Condizioni di licenza software Microsoft: Microsoft .NET Library</span><span class="sxs-lookup"><span data-stu-id="27327-150">Microsoft Software License Terms: Microsoft .NET Library</span></span>](https://aka.ms/dotnet-core-eula)
- <span data-ttu-id="27327-151">[Privacy at Microsoft](https://www.microsoft.com/trustcenter/privacy/) (La privacy in Microsoft)</span><span class="sxs-lookup"><span data-stu-id="27327-151">[Privacy at Microsoft](https://www.microsoft.com/trustcenter/privacy/)</span></span>
- [<span data-ttu-id="27327-152">Informativa sulla privacy di Microsoft</span><span class="sxs-lookup"><span data-stu-id="27327-152">Microsoft Privacy Statement</span></span>](https://privacy.microsoft.com/privacystatement)