---
title: DotNet-Trace-.NET Core
description: Installazione e utilizzo dello strumento da riga di comando DotNet-Trace.
author: sdmaclea
ms.author: stmaclea
ms.date: 10/14/2019
ms.openlocfilehash: 6513cf63070bc1984006da75313e9912d76a6c95
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/15/2019
ms.locfileid: "72321582"
---
# <a name="trace-for-performance-analysis-utility-dotnet-trace"></a><span data-ttu-id="746f9-103">Trace for Performance Analysis Utility (`dotnet-trace`)</span><span class="sxs-lookup"><span data-stu-id="746f9-103">Trace for performance analysis utility (`dotnet-trace`)</span></span>

<span data-ttu-id="746f9-104">**Questo articolo si applica a:** .net core 3,0 SDK e versioni successive</span><span class="sxs-lookup"><span data-stu-id="746f9-104">**This article applies to:** .NET Core 3.0 SDK and later versions</span></span>

## <a name="installing-dotnet-trace"></a><span data-ttu-id="746f9-105">Installazione di `dotnet-trace`</span><span class="sxs-lookup"><span data-stu-id="746f9-105">Installing `dotnet-trace`</span></span>

<span data-ttu-id="746f9-106">Per installare la versione di rilascio più recente del [pacchetto NuGet](https://www.nuget.org/packages/dotnet-trace)di `dotnet-trace`, usare il comando [DotNet tool install](../tools/dotnet-tool-install.md) :</span><span class="sxs-lookup"><span data-stu-id="746f9-106">To install the latest release version of the `dotnet-trace` [NuGet package](https://www.nuget.org/packages/dotnet-trace), use the [dotnet tool install](../tools/dotnet-tool-install.md) command:</span></span>

```dotnetcli
dotnet tool install --global dotnet-trace
```

## <a name="synopsis"></a><span data-ttu-id="746f9-107">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="746f9-107">Synopsis</span></span>

```console
dotnet-trace [-h, --help] [--version] <command>
```

## <a name="description"></a><span data-ttu-id="746f9-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="746f9-108">Description</span></span>

<span data-ttu-id="746f9-109">Lo strumento `dotnet-trace` è uno strumento globale dell'interfaccia della riga di comando multipiattaforma che consente di raccogliere le tracce di .NET Core di un processo in esecuzione senza alcun profiler nativo.</span><span class="sxs-lookup"><span data-stu-id="746f9-109">The `dotnet-trace` tool is a cross-platform CLI global tool that enables the collection of .NET Core traces of a running process without any native profiler involved.</span></span> <span data-ttu-id="746f9-110">È basato sulla tecnologia di `EventPipe` multipiattaforma del runtime di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="746f9-110">It's built around the cross-platform `EventPipe` technology of the .NET Core runtime.</span></span> <span data-ttu-id="746f9-111">`dotnet-trace` offre la stessa esperienza in Windows, Linux o macOS.</span><span class="sxs-lookup"><span data-stu-id="746f9-111">`dotnet-trace` delivers the same experience on Windows, Linux, or macOS.</span></span>

## <a name="options"></a><span data-ttu-id="746f9-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="746f9-112">Options</span></span>

- **`--version`**

<span data-ttu-id="746f9-113">Visualizzare la versione dell'utilità DotNet-Counters.</span><span class="sxs-lookup"><span data-stu-id="746f9-113">Display the version of the dotnet-counters utility.</span></span>

- **`-h|--help`**

<span data-ttu-id="746f9-114">Mostra la guida della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="746f9-114">Show command-line help.</span></span>

## <a name="commands"></a><span data-ttu-id="746f9-115">Comandi</span><span class="sxs-lookup"><span data-stu-id="746f9-115">Commands</span></span>

| <span data-ttu-id="746f9-116">Comando</span><span class="sxs-lookup"><span data-stu-id="746f9-116">Command</span></span>                                                     |
| ----------------------------------------------------------- |
| [<span data-ttu-id="746f9-117">raccolta traccia DotNet</span><span class="sxs-lookup"><span data-stu-id="746f9-117">dotnet-trace collect</span></span>](#dotnet-trace-collect)               |
| [<span data-ttu-id="746f9-118">conversione DotNet-Trace</span><span class="sxs-lookup"><span data-stu-id="746f9-118">dotnet-trace convert</span></span>](#dotnet-trace-convert)               |
| [<span data-ttu-id="746f9-119">elenco DotNet-Trace-processi</span><span class="sxs-lookup"><span data-stu-id="746f9-119">dotnet-trace list-processes</span></span>](#dotnet-trace-list-processes) |
| [<span data-ttu-id="746f9-120">elenco DotNet-Trace-profili</span><span class="sxs-lookup"><span data-stu-id="746f9-120">dotnet-trace list-profiles</span></span>](#dotnet-trace-list-profiles)   |

## <a name="dotnet-trace-collect"></a><span data-ttu-id="746f9-121">raccolta traccia DotNet</span><span class="sxs-lookup"><span data-stu-id="746f9-121">dotnet-trace collect</span></span>

<span data-ttu-id="746f9-122">Raccoglie una traccia di diagnostica da un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="746f9-122">Collects a diagnostic trace from a running process.</span></span>

### <a name="synopsis"></a><span data-ttu-id="746f9-123">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="746f9-123">Synopsis</span></span>

```console
dotnet-trace collect [-h|--help] [-p|--process-id] [--buffersize <size>] [-o|--output]
    [--providers] [--profile <profile-name>] [--format]
```

### <a name="options"></a><span data-ttu-id="746f9-124">Opzioni</span><span class="sxs-lookup"><span data-stu-id="746f9-124">Options</span></span>

- **`-p|--process-id <PID>`**

  <span data-ttu-id="746f9-125">Processo da cui raccogliere la traccia.</span><span class="sxs-lookup"><span data-stu-id="746f9-125">The process to collect the trace from.</span></span>

- **`--buffersize <size>`**

  <span data-ttu-id="746f9-126">Imposta la dimensione del buffer circolare in memoria in megabyte.</span><span class="sxs-lookup"><span data-stu-id="746f9-126">Sets the size of the in-memory circular buffer in megabytes.</span></span> <span data-ttu-id="746f9-127">Valore predefinito di 256 MB.</span><span class="sxs-lookup"><span data-stu-id="746f9-127">Default 256 MB.</span></span>

- **`-o|--output <trace-file-path>`**

  <span data-ttu-id="746f9-128">Percorso di output per i dati di traccia raccolti.</span><span class="sxs-lookup"><span data-stu-id="746f9-128">The output path for the collected trace data.</span></span> <span data-ttu-id="746f9-129">Se non viene specificato, il valore predefinito è `trace.nettrace`.</span><span class="sxs-lookup"><span data-stu-id="746f9-129">If not specified it defaults to `trace.nettrace`.</span></span>

- **`--providers <list-of-comma-separated-providers>`**

  <span data-ttu-id="746f9-130">Elenco delimitato da virgole di provider di `EventPipe` da abilitare.</span><span class="sxs-lookup"><span data-stu-id="746f9-130">A comma-separated list of `EventPipe` providers to be enabled.</span></span> <span data-ttu-id="746f9-131">Questi provider integrano tutti i provider impliciti dal `--profile <profile-name>`.</span><span class="sxs-lookup"><span data-stu-id="746f9-131">These providers supplement any providers implied by `--profile <profile-name>`.</span></span> <span data-ttu-id="746f9-132">Se è presente un'incoerenza per un determinato provider, la configurazione ha la precedenza sulla configurazione implicita del profilo.</span><span class="sxs-lookup"><span data-stu-id="746f9-132">If there's any inconsistency for a particular provider, the configuration here takes precedence over the implicit configuration from the profile.</span></span>

  <span data-ttu-id="746f9-133">Questo elenco di provider ha il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="746f9-133">This list of providers is in the form:</span></span>

  - `Provider[,Provider]`
  - <span data-ttu-id="746f9-134">il formato del `Provider` è: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]`.</span><span class="sxs-lookup"><span data-stu-id="746f9-134">`Provider` is in the form: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]`.</span></span>
  - <span data-ttu-id="746f9-135">il formato del `KeyValueArgs` è: `[key1=value1][;key2=value2]`.</span><span class="sxs-lookup"><span data-stu-id="746f9-135">`KeyValueArgs` is in the form: `[key1=value1][;key2=value2]`.</span></span>

- **`--profile <profile-name>`**

  <span data-ttu-id="746f9-136">Set predefinito di configurazioni del provider che consente di specificare brevemente gli scenari di traccia comuni.</span><span class="sxs-lookup"><span data-stu-id="746f9-136">A named pre-defined set of provider configurations that allows common tracing scenarios to be specified succinctly.</span></span>

- **`--format <NetTrace|Speedscope>`**

  <span data-ttu-id="746f9-137">Imposta il formato di output per la conversione del file di traccia.</span><span class="sxs-lookup"><span data-stu-id="746f9-137">Sets the output format for the trace file conversion.</span></span>

## <a name="dotnet-trace-convert"></a><span data-ttu-id="746f9-138">conversione DotNet-Trace</span><span class="sxs-lookup"><span data-stu-id="746f9-138">dotnet-trace convert</span></span>

<span data-ttu-id="746f9-139">Converte `nettrace` tracce in formati alternativi per l'utilizzo con strumenti di analisi di traccia alternativi.</span><span class="sxs-lookup"><span data-stu-id="746f9-139">Converts `nettrace` traces to alternate formats for use with alternate trace analysis tools.</span></span>

### <a name="synopsis"></a><span data-ttu-id="746f9-140">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="746f9-140">Synopsis</span></span>

```console
dotnet-trace convert [<input-filename>] [-h|--help] [--format] [-o|--output]
```

### <a name="arguments"></a><span data-ttu-id="746f9-141">argomenti</span><span class="sxs-lookup"><span data-stu-id="746f9-141">Arguments</span></span>

- **`<input-filename>`**

  <span data-ttu-id="746f9-142">File di traccia di input da convertire.</span><span class="sxs-lookup"><span data-stu-id="746f9-142">Input trace file to be converted.</span></span> <span data-ttu-id="746f9-143">Il valore predefinito è *Trace. NetTrace*.</span><span class="sxs-lookup"><span data-stu-id="746f9-143">Defaults to *trace.nettrace*.</span></span>

### <a name="options"></a><span data-ttu-id="746f9-144">Opzioni</span><span class="sxs-lookup"><span data-stu-id="746f9-144">Options</span></span>

- **`--format <NetTrace|Speedscope>`**

  <span data-ttu-id="746f9-145">Imposta il formato di output per la conversione del file di traccia.</span><span class="sxs-lookup"><span data-stu-id="746f9-145">Sets the output format for the trace file conversion.</span></span>

- **`-o|--output <output-filename>`**

  <span data-ttu-id="746f9-146">Nome file di output.</span><span class="sxs-lookup"><span data-stu-id="746f9-146">Output filename.</span></span> <span data-ttu-id="746f9-147">Verrà aggiunta l'estensione del formato di destinazione.</span><span class="sxs-lookup"><span data-stu-id="746f9-147">Extension of target format will be added.</span></span>

## <a name="dotnet-trace-list-processes"></a><span data-ttu-id="746f9-148">elenco DotNet-Trace-processi</span><span class="sxs-lookup"><span data-stu-id="746f9-148">dotnet-trace list-processes</span></span>

<span data-ttu-id="746f9-149">Elenca i processi DotNet che è possibile tracciare.</span><span class="sxs-lookup"><span data-stu-id="746f9-149">Lists dotnet processes that can be traced.</span></span>

### <a name="synopsis"></a><span data-ttu-id="746f9-150">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="746f9-150">Synopsis</span></span>

```console
dotnet-trace list-processes [-h|--help]
```

## <a name="dotnet-trace-list-profiles"></a><span data-ttu-id="746f9-151">elenco DotNet-Trace-profili</span><span class="sxs-lookup"><span data-stu-id="746f9-151">dotnet-trace list-profiles</span></span>

<span data-ttu-id="746f9-152">Elenca i profili di traccia predefiniti con una descrizione dei provider e dei filtri presenti in ciascun profilo.</span><span class="sxs-lookup"><span data-stu-id="746f9-152">Lists pre-built tracing profiles with a description of what providers and filters are in each profile.</span></span>

### <a name="synopsis"></a><span data-ttu-id="746f9-153">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="746f9-153">Synopsis</span></span>

```console
dotnet-trace list-profiles [-h|--help]
```

## <a name="collect-a-trace-with-dotnet-trace"></a><span data-ttu-id="746f9-154">Raccogliere una traccia con `dotnet-trace`</span><span class="sxs-lookup"><span data-stu-id="746f9-154">Collect a trace with `dotnet-trace`</span></span>

- <span data-ttu-id="746f9-155">Per raccogliere le tracce con `dotnet-trace`, è necessario innanzitutto individuare l'identificatore di processo (PID) dell'applicazione .NET Core da cui raccogliere le tracce.</span><span class="sxs-lookup"><span data-stu-id="746f9-155">To collect traces using `dotnet-trace`, you'll need to first, find out the process identifier (PID) of the .NET Core application to collect traces from.</span></span>

  - <span data-ttu-id="746f9-156">In Windows sono disponibili opzioni come l'utilizzo di gestione attività o del comando `tasklist`.</span><span class="sxs-lookup"><span data-stu-id="746f9-156">On Windows, there are options such as using the task manager or the `tasklist` command.</span></span>
  - <span data-ttu-id="746f9-157">In Linux l'opzione Trivial potrebbe usare `ps` comando.</span><span class="sxs-lookup"><span data-stu-id="746f9-157">On Linux, the trivial option could be using `ps` command.</span></span>

<span data-ttu-id="746f9-158">È anche possibile usare il comando [DotNet-Trace list-processes](#dotnet-trace-list-processes) per scoprire quali processi di .NET Core sono in esecuzione, insieme ai relativi PID.</span><span class="sxs-lookup"><span data-stu-id="746f9-158">You may also use the [dotnet-trace list-processes](#dotnet-trace-list-processes) command to find out what .NET Core processes are running, along with their PIDs.</span></span>

- <span data-ttu-id="746f9-159">Eseguire quindi il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="746f9-159">Then, run the following command:</span></span>

```console
> dotnet-trace collect --process-id <PID>

Press <Enter> to exit...
Connecting to process: <Full-Path-To-Process-Being-Profiled>/dotnet.exe
Collecting to file: <Full-Path-To-Trace>/trace.nettrace
  Session Id: <SessionId>
  Recording trace 721.025 (KB)
```

- <span data-ttu-id="746f9-160">Infine, arrestare la raccolta premendo il tasto `<Enter>` e `dotnet-trace` terminerà la registrazione degli eventi nel file `trace.nettrace`.</span><span class="sxs-lookup"><span data-stu-id="746f9-160">Finally, stop collection by pressing the `<Enter>` key, and `dotnet-trace` will finish logging events to `trace.nettrace` file.</span></span>

## <a name="viewing-the-trace-captured-from-dotnet-trace"></a><span data-ttu-id="746f9-161">Visualizzazione della traccia acquisita da `dotnet-trace`</span><span class="sxs-lookup"><span data-stu-id="746f9-161">Viewing the trace captured from `dotnet-trace`</span></span>

<span data-ttu-id="746f9-162">In Windows è possibile visualizzare i file di `.nettrace` in [PerfView](https://github.com/microsoft/perfview) per l'analisi, esattamente come le tracce raccolte con ETW o LTTng.</span><span class="sxs-lookup"><span data-stu-id="746f9-162">On Windows, `.nettrace` files can be viewed on [PerfView](https://github.com/microsoft/perfview) for analysis, just like traces collected with ETW or LTTng.</span></span> <span data-ttu-id="746f9-163">Per le tracce raccolte in Linux, è possibile spostare la traccia in un computer Windows per la visualizzazione in PerfView.</span><span class="sxs-lookup"><span data-stu-id="746f9-163">For traces collected on Linux, you can move the trace to a Windows machine to be viewed on PerfView.</span></span>

<span data-ttu-id="746f9-164">È anche possibile visualizzare la traccia in un computer Linux cambiando il formato di output di `dotnet-trace` in `speedscope`.</span><span class="sxs-lookup"><span data-stu-id="746f9-164">You may also view the trace on a Linux machine by changing the output format of `dotnet-trace` to `speedscope`.</span></span> <span data-ttu-id="746f9-165">È possibile modificare il formato del file di output utilizzando l'opzione `-f|--format`-`-f speedscope` renderà `dotnet-trace` produrre un file `speedscope`.</span><span class="sxs-lookup"><span data-stu-id="746f9-165">You can change the output file format using the `-f|--format` option - `-f speedscope` will make `dotnet-trace` to produce a `speedscope` file.</span></span> <span data-ttu-id="746f9-166">Attualmente è possibile scegliere tra `nettrace` (opzione predefinita) e `speedscope`.</span><span class="sxs-lookup"><span data-stu-id="746f9-166">You can currently choose between `nettrace` (the default option) and `speedscope`.</span></span> <span data-ttu-id="746f9-167">è possibile aprire i file di `Speedscope` in <https://www.speedscope.app>.</span><span class="sxs-lookup"><span data-stu-id="746f9-167">`Speedscope` files can be opened at <https://www.speedscope.app>.</span></span>

> [!NOTE]
> <span data-ttu-id="746f9-168">Il runtime di .NET Core genera tracce nel formato `nettrace` e viene convertito in speedscope (se specificato) dopo il completamento della traccia.</span><span class="sxs-lookup"><span data-stu-id="746f9-168">The .NET Core runtime generates traces in the `nettrace` format, and they're converted to speedscope (if specified) after the trace is completed.</span></span> <span data-ttu-id="746f9-169">Poiché alcune conversioni possono comportare la perdita di dati, il file di `nettrace` originale viene mantenuto accanto al file convertito.</span><span class="sxs-lookup"><span data-stu-id="746f9-169">Since some conversions may result in loss of data, the original `nettrace` file is preserved next to the converted file.</span></span>

## <a name="using-dotnet-trace-to-collect-counter-values-over-time"></a><span data-ttu-id="746f9-170">Utilizzo di `dotnet-trace` per raccogliere i valori dei contatori nel tempo</span><span class="sxs-lookup"><span data-stu-id="746f9-170">Using `dotnet-trace` to collect counter values over time</span></span>

<span data-ttu-id="746f9-171">Se si sta provando a usare `EventCounter` per il monitoraggio dello stato di base in impostazioni sensibili alle prestazioni, ad esempio gli ambienti di produzione e si desidera raccogliere tracce invece di controllarle in tempo reale, è possibile eseguire questa operazione anche con `dotnet-trace`.</span><span class="sxs-lookup"><span data-stu-id="746f9-171">If you're trying to use `EventCounter` for basic health monitoring in  performance-sensitive settings like production environments and you want to collect traces instead of watching them in real time, you can do that with `dotnet-trace` as well.</span></span>

<span data-ttu-id="746f9-172">Se ad esempio si desidera raccogliere i valori dei contatori delle prestazioni in fase di esecuzione, è possibile utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="746f9-172">For example, if you want to collect runtime performance counter values, you can use the following command:</span></span>

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1
```

<span data-ttu-id="746f9-173">Questo comando indica ai contatori di runtime di essere segnalati una volta al secondo per il monitoraggio dell'integrità leggero.</span><span class="sxs-lookup"><span data-stu-id="746f9-173">This command tells the runtime counters to be reported once every second for lightweight health monitoring.</span></span> <span data-ttu-id="746f9-174">La sostituzione di `EventCounterIntervalSec=1` con un valore superiore (ad esempio 60) consente di raccogliere una traccia più piccola con una minore granularità nei dati del contatore.</span><span class="sxs-lookup"><span data-stu-id="746f9-174">Replacing `EventCounterIntervalSec=1` with a higher value (for example, 60) allows you to collect a smaller trace with less granularity in the counter data.</span></span>

<span data-ttu-id="746f9-175">Se si vuole disabilitare gli eventi di runtime per ridurre ulteriormente l'overhead (e le dimensioni della traccia), è possibile usare il comando seguente per disabilitare gli eventi di runtime e il profiler dello stack gestito.</span><span class="sxs-lookup"><span data-stu-id="746f9-175">If you want to disable runtime events to reduce the overhead (and trace size) even further, you can use the following command to disable runtime events and managed stack profiler.</span></span>

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1,Microsoft-Windows-DotNETRuntime:0:1,Microsoft-DotNETCore-SampleProfiler:0:1
```

## <a name="net-providers"></a><span data-ttu-id="746f9-176">Provider .NET</span><span class="sxs-lookup"><span data-stu-id="746f9-176">.NET Providers</span></span>

<span data-ttu-id="746f9-177">Il runtime di .NET Core supporta i provider .NET seguenti.</span><span class="sxs-lookup"><span data-stu-id="746f9-177">The .NET Core runtime supports the following .NET providers.</span></span> <span data-ttu-id="746f9-178">.NET Core usa le stesse parole chiave per abilitare sia `Event Tracing for Windows (ETW)` che `EventPipe` tracce.</span><span class="sxs-lookup"><span data-stu-id="746f9-178">.NET Core uses the same keywords to enable both `Event Tracing for Windows (ETW)` and `EventPipe` traces.</span></span>

| <span data-ttu-id="746f9-179">Nome provider</span><span class="sxs-lookup"><span data-stu-id="746f9-179">Provider name</span></span>                            | <span data-ttu-id="746f9-180">Informazioni</span><span class="sxs-lookup"><span data-stu-id="746f9-180">Information</span></span> |
|------------------------------------------|-------------|
| `Microsoft-Windows-DotNETRuntime`        | [<span data-ttu-id="746f9-181">Il provider di runtime</span><span class="sxs-lookup"><span data-stu-id="746f9-181">The Runtime Provider</span></span>](../../framework/performance/clr-etw-providers.md#the-runtime-provider)<br>[<span data-ttu-id="746f9-182">Parole chiave di runtime CLR</span><span class="sxs-lookup"><span data-stu-id="746f9-182">CLR Runtime Keywords</span></span>](../../framework/performance/clr-etw-keywords-and-levels.md#runtime) |
| `Microsoft-Windows-DotNETRuntimeRundown` | [<span data-ttu-id="746f9-183">Il provider di rundown</span><span class="sxs-lookup"><span data-stu-id="746f9-183">The Rundown Provider</span></span>](../../framework/performance/clr-etw-providers.md#the-rundown-provider)<br>[<span data-ttu-id="746f9-184">Parole chiave di rundown CLR</span><span class="sxs-lookup"><span data-stu-id="746f9-184">CLR Rundown Keywords</span></span>](../../framework/performance/clr-etw-keywords-and-levels.md#rundown) |
| `Microsoft-DotNETCore-SampleProfiler`    | <span data-ttu-id="746f9-185">Abilita il profiler di esempio.</span><span class="sxs-lookup"><span data-stu-id="746f9-185">Enables the sample profiler.</span></span> |