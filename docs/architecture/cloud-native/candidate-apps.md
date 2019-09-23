---
title: App candidate per cloud native
description: Informazioni sui tipi di applicazioni che traggono vantaggio da un approccio nativo per il cloud
author: robvet
ms.date: 08/20/2019
ms.openlocfilehash: 3ee13d4c636d08a58a7dcab6883725a55a08ae65
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2019
ms.locfileid: "71183525"
---
# <a name="candidate-apps-for-cloud-native"></a><span data-ttu-id="7095f-103">App candidate per cloud native</span><span class="sxs-lookup"><span data-stu-id="7095f-103">Candidate apps for cloud native</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="7095f-104">Esaminare le app nel portfolio.</span><span class="sxs-lookup"><span data-stu-id="7095f-104">Look at the apps in your portfolio.</span></span> <span data-ttu-id="7095f-105">Quanti di essi sono idonei per un'architettura nativa del cloud?</span><span class="sxs-lookup"><span data-stu-id="7095f-105">How many of them qualify for a cloud-native architecture?</span></span> <span data-ttu-id="7095f-106">Tutti questi elementi?</span><span class="sxs-lookup"><span data-stu-id="7095f-106">All of them?</span></span> <span data-ttu-id="7095f-107">Forse?</span><span class="sxs-lookup"><span data-stu-id="7095f-107">Perhaps some?</span></span>

<span data-ttu-id="7095f-108">Applicando un'analisi costi/vantaggi, è possibile che la maggior parte dei prezzi non supporti il pesante tag di prezzo necessario per il cloud nativo.</span><span class="sxs-lookup"><span data-stu-id="7095f-108">Applying a cost/benefit analysis, there's a good chance that most wouldn't support the hefty price tag required to be cloud native.</span></span> <span data-ttu-id="7095f-109">Il costo di un cloud nativo è di gran lunga superiore al valore aziendale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7095f-109">The cost of being cloud native would far exceed the business value of the application.</span></span>

<span data-ttu-id="7095f-110">Quale tipo di applicazione può essere un candidato per il cloud nativo?</span><span class="sxs-lookup"><span data-stu-id="7095f-110">What type of application might be a candidate for cloud native?</span></span>

- <span data-ttu-id="7095f-111">Un sistema aziendale strategico di grandi dimensioni che deve evolvere costantemente funzionalità/funzionalità aziendali</span><span class="sxs-lookup"><span data-stu-id="7095f-111">A large, strategic enterprise system that needs to constantly evolve business capabilities/features</span></span>

- <span data-ttu-id="7095f-112">Un'applicazione che richiede una velocità di rilascio elevata, con attendibilità elevata</span><span class="sxs-lookup"><span data-stu-id="7095f-112">An application that requires a high release velocity - with high confidence</span></span>

- <span data-ttu-id="7095f-113">Sistema con cui è necessario rilasciare le singole funzionalità *senza* una ridistribuzione completa dell'intero sistema</span><span class="sxs-lookup"><span data-stu-id="7095f-113">A system with where individual features must release *without* a full redeployment of the entire system</span></span>

- <span data-ttu-id="7095f-114">Un'applicazione sviluppata da team con competenze in diversi stack di tecnologie</span><span class="sxs-lookup"><span data-stu-id="7095f-114">An application developed by teams with expertise in different technology stacks</span></span>

- <span data-ttu-id="7095f-115">Applicazione con componenti che devono essere ridimensionati in modo indipendente</span><span class="sxs-lookup"><span data-stu-id="7095f-115">An application with components that must scale independently</span></span>

<span data-ttu-id="7095f-116">Sono quindi presenti sistemi legacy.</span><span class="sxs-lookup"><span data-stu-id="7095f-116">Then there are legacy systems.</span></span> <span data-ttu-id="7095f-117">Per quanto riguarda la creazione di nuove applicazioni, è spesso responsabile della modernizzazione dei carichi di lavoro legacy cruciali per l'azienda.</span><span class="sxs-lookup"><span data-stu-id="7095f-117">While we'd all like to build new applications, we're often responsible for modernizing legacy workloads that are critical to the business.</span></span> <span data-ttu-id="7095f-118">Nel corso del tempo, un'applicazione legacy potrebbe essere scomposta in microservizi, in contenitori e infine "ripiattaforma" in un'architettura nativa del cloud.</span><span class="sxs-lookup"><span data-stu-id="7095f-118">Over time, a legacy application could be decomposed into microservices, containerized, and ultimately "replatformed" into a cloud-native architecture.</span></span>  

### <a name="modernizing-legacy-apps"></a><span data-ttu-id="7095f-119">Modernizzazione di app legacy</span><span class="sxs-lookup"><span data-stu-id="7095f-119">Modernizing legacy apps</span></span>

<span data-ttu-id="7095f-120">L'e-book gratuito Microsoft [modernizza le applicazioni .NET esistenti con il cloud di Azure e i contenitori di Windows](https://dotnet.microsoft.com/download/thank-you/modernizing-existing-net-apps-ebook) fornisce indicazioni per la migrazione dei carichi di lavoro locali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="7095f-120">The free Microsoft e-book [Modernize existing .NET applications with Azure cloud and Windows Containers](https://dotnet.microsoft.com/download/thank-you/modernizing-existing-net-apps-ebook) provides guidance for migrating on-premises workloads into cloud.</span></span> <span data-ttu-id="7095f-121">La figura 1-8 Mostra che non è disponibile una singola strategia unica, unica per la modernizzazione delle applicazioni legacy.</span><span class="sxs-lookup"><span data-stu-id="7095f-121">Figure 1-8 shows that there isn't a single, one-size-fits-all strategy for modernizing legacy applications.</span></span>

<span data-ttu-id="7095f-122">![Strategie per la migrazione dei carichi](./media/strategies-for-migrating-legacy-workloads.png)
di lavoro legacy**Figura 1-8**.</span><span class="sxs-lookup"><span data-stu-id="7095f-122">![Strategies for migrating legacy workloads](./media/strategies-for-migrating-legacy-workloads.png)
**Figure 1-8**.</span></span> <span data-ttu-id="7095f-123">Strategie per la migrazione di carichi di lavoro legacy</span><span class="sxs-lookup"><span data-stu-id="7095f-123">Strategies for migrating legacy workloads</span></span>

<span data-ttu-id="7095f-124">Le app monolitiche che non sono in gran parte critiche traggono vantaggio da una rapida migrazione (pronta per l'[infrastruttura cloud](https://docs.microsoft.com/dotnet/standard/modernize-with-azure-and-containers/lift-and-shift-existing-apps-azure-iaas)).</span><span class="sxs-lookup"><span data-stu-id="7095f-124">Monolithic apps that are non-critical largely benefit from a quick lift-and-shift ([Cloud Infrastructure-Ready](https://docs.microsoft.com/dotnet/standard/modernize-with-azure-and-containers/lift-and-shift-existing-apps-azure-iaas)) migration.</span></span> <span data-ttu-id="7095f-125">In questo caso, il carico di lavoro locale viene riallocato a una macchina virtuale basata sul cloud, senza modifiche.</span><span class="sxs-lookup"><span data-stu-id="7095f-125">Here, the on-premises workload is rehosted to a cloud-based VM, without changes.</span></span> <span data-ttu-id="7095f-126">Questo approccio usa il [modello IaaS (infrastruttura distribuita come servizio)](https://azure.microsoft.com/overview/what-is-iaas/).</span><span class="sxs-lookup"><span data-stu-id="7095f-126">This approach uses the [IaaS (Infrastructure as a Service) model](https://azure.microsoft.com/overview/what-is-iaas/).</span></span> <span data-ttu-id="7095f-127">Azure include diversi strumenti, ad esempio[Azure migrate](https://aka.ms/azuremigrate), [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)e il [servizio migrazione del database di Azure](https://azure.microsoft.com/campaigns/database-migration/), per semplificare il passaggio.</span><span class="sxs-lookup"><span data-stu-id="7095f-127">Azure includes several tools such as ([Azure Migrate](https://aka.ms/azuremigrate), [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/), and [Azure Database Migration Service](https://azure.microsoft.com/campaigns/database-migration/)) to make such a move easier.</span></span> <span data-ttu-id="7095f-128">Sebbene questa strategia possa produrre risparmi in termini di costi, tali applicazioni in genere non sono state progettate per sbloccare e sfruttare i vantaggi di cloud computing.</span><span class="sxs-lookup"><span data-stu-id="7095f-128">While this strategy can yield some cost savings, such applications typically weren't architected to unlock and leverage the benefits of cloud computing.</span></span> 

<span data-ttu-id="7095f-129">Le app monolitiche cruciali per l'azienda traggono spesso vantaggio da una migrazione migliorata (*ottimizzata*per il cloud).</span><span class="sxs-lookup"><span data-stu-id="7095f-129">Monolithic apps that are critical to the business oftentimes benefit from an enhanced lift-and-shift (*Cloud Optimized*) migration.</span></span> <span data-ttu-id="7095f-130">Questo approccio include le ottimizzazioni di distribuzione che abilitano i servizi cloud principali, senza modificare l'architettura di base dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7095f-130">This approach includes deployment optimizations that enable key cloud services - without changing the core architecture of the application.</span></span> <span data-ttu-id="7095f-131">Ad esempio, è possibile [distribuire](https://docs.microsoft.com/virtualization/windowscontainers/about/) l'applicazione e distribuirla in un agente di orchestrazione del contenitore, come i [Servizi Kubernetes di Azure](https://azure.microsoft.com/services/kubernetes-service/), illustrati più avanti in questo libro.</span><span class="sxs-lookup"><span data-stu-id="7095f-131">For example, you might [containerize](https://docs.microsoft.com/virtualization/windowscontainers/about/) the application and deploy it to a container orchestrator, like [Azure Kubernetes Services](https://azure.microsoft.com/services/kubernetes-service/), discussed later in this book.</span></span> <span data-ttu-id="7095f-132">Una volta nel cloud, l'applicazione può utilizzare altri servizi cloud, ad esempio database, code di messaggi, monitoraggio e Caching distribuito.</span><span class="sxs-lookup"><span data-stu-id="7095f-132">Once in the cloud, the application could consume other cloud services such as databases, message queues, monitoring, and distributed caching.</span></span>

<span data-ttu-id="7095f-133">Infine, le app monolitiche che eseguono funzioni aziendali strategiche possono trarre il massimo vantaggio da un approccio *nativo del cloud* , l'oggetto di questo libro.</span><span class="sxs-lookup"><span data-stu-id="7095f-133">Finally, monolithic apps that perform strategic enterprise functions might best benefit from a *Cloud-Native* approach, the subject of this book.</span></span> <span data-ttu-id="7095f-134">Questo approccio offre agilità e velocità.</span><span class="sxs-lookup"><span data-stu-id="7095f-134">This approach provides agility and velocity.</span></span> <span data-ttu-id="7095f-135">Ma comporta un costo per la ricreazione, la riprogettazione e la riscrittura del codice.</span><span class="sxs-lookup"><span data-stu-id="7095f-135">But, it comes at a cost of replatforming, rearchitecting, and rewriting code.</span></span>

<span data-ttu-id="7095f-136">Se l'utente e il team ritengono che un approccio nativo per il cloud sia appropriato, è necessario razionalizzare la decisione con l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7095f-136">If you and your team believe a cloud-native approach is appropriate, it behooves you to rationalize the decision with your organization.</span></span> <span data-ttu-id="7095f-137">Qual è esattamente il problema aziendale che verrà risolto da un approccio nativo per il cloud?</span><span class="sxs-lookup"><span data-stu-id="7095f-137">What exactly is the business problem that a cloud- native approach will solve?</span></span> <span data-ttu-id="7095f-138">In che modo si allineano alle esigenze aziendali?</span><span class="sxs-lookup"><span data-stu-id="7095f-138">How would it align with business needs?</span></span>

- <span data-ttu-id="7095f-139">Versioni rapide delle funzionalità con maggiore fiducia?</span><span class="sxs-lookup"><span data-stu-id="7095f-139">Rapid releases of features with increased confidence?</span></span>

- <span data-ttu-id="7095f-140">Scalabilità con granularità fine: uso più efficiente delle risorse?</span><span class="sxs-lookup"><span data-stu-id="7095f-140">Fine-grained scalability - more efficient usage of resources?</span></span>

- <span data-ttu-id="7095f-141">Maggiore resilienza del sistema?</span><span class="sxs-lookup"><span data-stu-id="7095f-141">Improved system resiliency?</span></span>

- <span data-ttu-id="7095f-142">Miglioramento delle prestazioni del sistema</span><span class="sxs-lookup"><span data-stu-id="7095f-142">Improved system performance?</span></span>

- <span data-ttu-id="7095f-143">Maggiore visibilità sulle operazioni?</span><span class="sxs-lookup"><span data-stu-id="7095f-143">More visibility into operations?</span></span>

- <span data-ttu-id="7095f-144">Piattaforme di sviluppo e archivi dati di Blend per arrivare allo strumento migliore per il processo?</span><span class="sxs-lookup"><span data-stu-id="7095f-144">Blend development platforms and data stores to arrive at the best tool for the job?</span></span>

- <span data-ttu-id="7095f-145">Investimento per applicazioni future?</span><span class="sxs-lookup"><span data-stu-id="7095f-145">Future-proof application investment?</span></span>

<span data-ttu-id="7095f-146">La strategia di migrazione corretta dipende dalle priorità dell'organizzazione e dai sistemi di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7095f-146">The right migration strategy depends on organizational priorities and the systems you're targeting.</span></span> <span data-ttu-id="7095f-147">Per molti, può essere più conveniente ottimizzare il cloud di un'applicazione monolitica o aggiungere servizi con granularità grossolana a un'app a più livelli.</span><span class="sxs-lookup"><span data-stu-id="7095f-147">For many, it may be more cost effective to cloud-optimize a monolithic application or add coarse-grained services to an N-Tier app.</span></span> <span data-ttu-id="7095f-148">In questi casi, è comunque possibile sfruttare appieno le funzionalità di PaaS cloud come quelle offerte dal servizio app Azure.</span><span class="sxs-lookup"><span data-stu-id="7095f-148">In these cases, you can still make full use of cloud PaaS capabilities like the ones offered by Azure App Service.</span></span>

## <a name="summary"></a><span data-ttu-id="7095f-149">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7095f-149">Summary</span></span>

<span data-ttu-id="7095f-150">In questo capitolo è stato introdotto il cloud native computing.</span><span class="sxs-lookup"><span data-stu-id="7095f-150">In this chapter, we introduced cloud-native computing.</span></span> <span data-ttu-id="7095f-151">È stata fornita una definizione insieme alle funzionalità principali che guidano un'applicazione nativa del cloud.</span><span class="sxs-lookup"><span data-stu-id="7095f-151">We provided a definition along with the key capabilities that drive a cloud-native application.</span></span> <span data-ttu-id="7095f-152">Sono stati esaminati i tipi di applicazioni che potrebbero giustificare questo investimento e impegno.</span><span class="sxs-lookup"><span data-stu-id="7095f-152">We looked the types of applications that might justify this investment and effort.</span></span>

<span data-ttu-id="7095f-153">Con l'introduzione, viene ora analizzato in modo molto più dettagliato il cloud nativo.</span><span class="sxs-lookup"><span data-stu-id="7095f-153">With the introduction behind, we now dive into a much more detailed look at cloud native.</span></span>

### <a name="references"></a><span data-ttu-id="7095f-154">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="7095f-154">References</span></span>

- [<span data-ttu-id="7095f-155">Cloud native Computing Foundation</span><span class="sxs-lookup"><span data-stu-id="7095f-155">Cloud Native Computing Foundation</span></span>](https://www.cncf.io/)

- [<span data-ttu-id="7095f-156">Microservizi .NET.: Architettura per le applicazioni .NET in contenitori</span><span class="sxs-lookup"><span data-stu-id="7095f-156">.NET Microservices: Architecture for Containerized .NET applications</span></span>](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook)

- [<span data-ttu-id="7095f-157">Modernizza le applicazioni .NET esistenti con il cloud di Azure e i contenitori di Windows</span><span class="sxs-lookup"><span data-stu-id="7095f-157">Modernize existing .NET applications with Azure cloud and Windows Containers</span></span>](https://dotnet.microsoft.com/download/thank-you/modernizing-existing-net-apps-ebook)

- [<span data-ttu-id="7095f-158">Modelli nativi del cloud di Cornelia Davis</span><span class="sxs-lookup"><span data-stu-id="7095f-158">Cloud Native Patterns by Cornelia Davis</span></span>](https://www.manning.com/books/cloud-native-patterns)

- [<span data-ttu-id="7095f-159">Oltre l'applicazione a dodici fattori</span><span class="sxs-lookup"><span data-stu-id="7095f-159">Beyond the Twelve-Factor Application</span></span>](https://content.pivotal.io/blog/beyond-the-twelve-factor-app)

- [<span data-ttu-id="7095f-160">Che cos'è l'infrastruttura come codice</span><span class="sxs-lookup"><span data-stu-id="7095f-160">What is Infrastructure as Code</span></span>](https://docs.microsoft.com/azure/devops/learn/what-is-infrastructure-as-code)

- [<span data-ttu-id="7095f-161">Micro deploy di uber Engineering: Distribuzione giornaliera con sicurezza</span><span class="sxs-lookup"><span data-stu-id="7095f-161">Uber Engineering’s Micro Deploy: Deploying Daily with Confidence</span></span>](https://eng.uber.com/micro-deploy/)

- [<span data-ttu-id="7095f-162">Come Netflix distribuisce il codice</span><span class="sxs-lookup"><span data-stu-id="7095f-162">How Netflix Deploys Code</span></span>](https://www.infoq.com/news/2013/06/netflix/)

- [<span data-ttu-id="7095f-163">Controllo dell'overload per la scalabilità di microservizi WeChat</span><span class="sxs-lookup"><span data-stu-id="7095f-163">Overload Control for Scaling WeChat Microservices</span></span>](https://www.cs.columbia.edu/~ruigu/papers/socc18-final100.pdf)

- [<span data-ttu-id="7095f-164">RayGun-Case Study</span><span class="sxs-lookup"><span data-stu-id="7095f-164">RayGun - Case Study</span></span>](https://raygun.com/case-study/ovation)

>[!div class="step-by-step"]
><span data-ttu-id="7095f-165">[Precedente](definition.md)
>[Successivo](introduce-eshoponcontainers-reference-app.md)</span><span class="sxs-lookup"><span data-stu-id="7095f-165">[Previous](definition.md)
[Next](introduce-eshoponcontainers-reference-app.md)</span></span> <!-- Next Chapter -->