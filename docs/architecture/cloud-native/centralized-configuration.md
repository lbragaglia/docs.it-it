---
title: Configurazione centralizzata
description: La configurazione centralizzata con Azure Key Vault può semplificare la gestione delle app native del cloud.
ms.date: 06/30/2019
ms.openlocfilehash: f4f495591550abccf2c64ef24cbe7620b039d8ca
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2019
ms.locfileid: "71183518"
---
# <a name="centralized-configuration"></a><span data-ttu-id="59d43-103">Configurazione centralizzata</span><span class="sxs-lookup"><span data-stu-id="59d43-103">Centralized configuration</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="59d43-104">Le applicazioni native del cloud coinvolgono molti altri servizi in esecuzione rispetto alle tradizionali app monolitiche a istanza singola.</span><span class="sxs-lookup"><span data-stu-id="59d43-104">Cloud-native applications involve many more running services than traditional single-instance monolithic apps.</span></span> <span data-ttu-id="59d43-105">La gestione delle impostazioni di configurazione per decine di servizi interdipendenti può essere complessa, motivo per cui gli archivi di configurazione centralizzati vengono spesso implementati per le applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="59d43-105">Managing configuration settings for dozens of interdependent services can be challenging, which is why centralized configuration stores are often implemented for distributed applications.</span></span>

<span data-ttu-id="59d43-106">Come illustrato nel [capitolo 1](introduction.md), le raccomandazioni per le app a dodici fattori richiedono una separazione rigorosa tra il codice e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="59d43-106">As discussed in [Chapter 1](introduction.md), the Twelve-Factor App recommendations require strict separation between code and configuration.</span></span> <span data-ttu-id="59d43-107">Questo significa che l'archiviazione delle impostazioni di configurazione come costanti o valori letterali nel codice è una violazione.</span><span class="sxs-lookup"><span data-stu-id="59d43-107">This means storing configuration settings as constants or literal values in code is a violation.</span></span> <span data-ttu-id="59d43-108">Questa raccomandazione esiste perché lo stesso codice deve essere utilizzato in più ambienti, tra cui sviluppo, test, gestione temporanea e produzione.</span><span class="sxs-lookup"><span data-stu-id="59d43-108">This recommendation exists because the same code should be used across multiple environments, including development, testing, staging, and production.</span></span> <span data-ttu-id="59d43-109">Tuttavia, è probabile che i valori di configurazione variano a seconda di ognuno di questi ambienti.</span><span class="sxs-lookup"><span data-stu-id="59d43-109">However, configuration values are likely to vary between each of these environments.</span></span> <span data-ttu-id="59d43-110">I valori di configurazione devono quindi essere archiviati nell'ambiente stesso oppure l'ambiente deve archiviare le credenziali in un archivio di configurazione centralizzato.</span><span class="sxs-lookup"><span data-stu-id="59d43-110">So, configuration values should be stored in the environment itself, or the environment should store the credentials to a centralized configuration store.</span></span>

<span data-ttu-id="59d43-111">L'applicazione eShopOnContainers include i file di impostazioni dell'applicazione locale con ogni microservizio.</span><span class="sxs-lookup"><span data-stu-id="59d43-111">The eShopOnContainers application includes local application settings files with each microservice.</span></span> <span data-ttu-id="59d43-112">Questi file vengono archiviati nel controllo del codice sorgente, ma non includono i segreti di produzione, ad esempio le stringhe di connessione o le chiavi API.</span><span class="sxs-lookup"><span data-stu-id="59d43-112">These files are checked into source control but don't include production secrets such as connection strings or API keys.</span></span> <span data-ttu-id="59d43-113">In produzione, le singole impostazioni possono essere sovrascritte con le variabili di ambiente per servizio.</span><span class="sxs-lookup"><span data-stu-id="59d43-113">In production, individual settings may be overwritten with per-service environment variables.</span></span> <span data-ttu-id="59d43-114">Si tratta di una pratica comune per le applicazioni ospitate, ma non fornisce un archivio di configurazione centrale.</span><span class="sxs-lookup"><span data-stu-id="59d43-114">This is a common practice for hosted applications, but doesn't provide a central configuration store.</span></span> <span data-ttu-id="59d43-115">Per supportare la gestione centralizzata delle impostazioni di configurazione, ogni microservizio include un'impostazione che consente di alternare l'uso di impostazioni locali o Azure Key Vault impostazioni.</span><span class="sxs-lookup"><span data-stu-id="59d43-115">To support centralized management of configuration settings, each microservice includes a setting to toggle between its use of local settings or Azure Key Vault settings.</span></span>

## <a name="azure-key-vault"></a><span data-ttu-id="59d43-116">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="59d43-116">Azure Key Vault</span></span>

<span data-ttu-id="59d43-117">Azure Key Vault offre archiviazione sicura di token, password, certificati, chiavi API e altri segreti riservati.</span><span class="sxs-lookup"><span data-stu-id="59d43-117">Azure Key Vault provides secure storage of tokens, passwords, certificates, API keys, and other sensitive secrets.</span></span> <span data-ttu-id="59d43-118">L'accesso a Key Vault richiede l'autenticazione e l'autorizzazione del chiamante appropriate, che nel caso dei microservizi eShopOnContainers indica l'uso di una combinazione ClientID/ClientSecret.</span><span class="sxs-lookup"><span data-stu-id="59d43-118">Access to Key Vault requires proper caller authentication and authorization, which in the case of the eShopOnContainers microservices means the use of a ClientId/ClientSecret combination.</span></span> <span data-ttu-id="59d43-119">Non archiviare le credenziali nel controllo del codice sorgente, ma impostate nell'ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="59d43-119">Don't check in these credentials into source control, but instead set in the application's environment.</span></span> <span data-ttu-id="59d43-120">L'accesso diretto a Key Vault da AKS può essere eseguito usando [Key Vault FlexVolume](https://github.com/Azure/kubernetes-keyvault-flexvol).</span><span class="sxs-lookup"><span data-stu-id="59d43-120">Direct access to Key Vault from AKS can be achieved using [Key Vault FlexVolume](https://github.com/Azure/kubernetes-keyvault-flexvol).</span></span>

<span data-ttu-id="59d43-121">Con la configurazione centralizzata, le impostazioni che si applicano all'intera applicazione, ad esempio l'endpoint di registrazione centralizzato, possono essere impostate una sola volta e utilizzate da ogni parte dell'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="59d43-121">With centralized configuration, settings that apply to the entire application, such as the centralized logging endpoint, can be set once and used by every part of the distributed application.</span></span> <span data-ttu-id="59d43-122">Sebbene i microservizi siano indipendenti l'uno dall'altro, in genere saranno presenti alcune dipendenze condivise i cui dettagli di configurazione possono trarre vantaggio da un archivio di configurazione centralizzato.</span><span class="sxs-lookup"><span data-stu-id="59d43-122">Although microservices should be independent of one another, there will typically still be some shared dependencies whose configuration details can benefit from a centralized configuration store.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="59d43-123">[Precedente](deploy-eshoponcontainers-azure.md)
>[Successivo](scale-applications.md)</span><span class="sxs-lookup"><span data-stu-id="59d43-123">[Previous](deploy-eshoponcontainers-azure.md)
[Next](scale-applications.md)</span></span> <!-- Next Chapter -->