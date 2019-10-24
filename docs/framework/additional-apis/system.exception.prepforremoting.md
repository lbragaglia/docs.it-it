---
title: Metodo Exception. PrepForRemoting (System)
author: mairaw
ms.author: mairaw
ms.date: 10/08/2019
topic_type:
- apiref
api_name:
- System.Exception.PrepForRemoting
api_location:
- mscorlib.dll
api_type:
- Assembly
ms.openlocfilehash: 057390d64f70d3cb8eba7d4b29b94570fdca77e3
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72405032"
---
# <a name="exceptionprepforremoting-method"></a><span data-ttu-id="0e773-102">Metodo Exception.PrepForRemoting</span><span class="sxs-lookup"><span data-stu-id="0e773-102">Exception.PrepForRemoting Method</span></span>

<span data-ttu-id="0e773-103">Conserva la traccia dello stack sul lato server aggiungendola al messaggio prima che l'eccezione venga rigenerata nel sito di chiamata del client.</span><span class="sxs-lookup"><span data-stu-id="0e773-103">Preserves the server-side stack trace by appending it to the message before the exception is rethrown at the client call site.</span></span>

```csharp
internal Exception PrepForRemoting();
```

## <a name="returns"></a><span data-ttu-id="0e773-104">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="0e773-104">Returns</span></span>

<xref:System.Exception>  
<span data-ttu-id="0e773-105">Istanza corrente di <xref:System.Exception>.</span><span class="sxs-lookup"><span data-stu-id="0e773-105">This <xref:System.Exception> instance.</span></span>

## <a name="remarks"></a><span data-ttu-id="0e773-106">Note</span><span class="sxs-lookup"><span data-stu-id="0e773-106">Remarks</span></span>

> [!WARNING]
> <span data-ttu-id="0e773-107">Il metodo `Exception.PrepForRemoting` è interno e non è destinato a essere utilizzato direttamente nel codice.</span><span class="sxs-lookup"><span data-stu-id="0e773-107">The `Exception.PrepForRemoting` method is internal and is not meant to be used directly in your code.</span></span>
>
> <span data-ttu-id="0e773-108">Microsoft non supporta l'utilizzo di questo metodo in un'applicazione di produzione in qualsiasi circostanza.</span><span class="sxs-lookup"><span data-stu-id="0e773-108">Microsoft does not support the use of this method in a production application under any circumstance.</span></span>

## <a name="requirements"></a><span data-ttu-id="0e773-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="0e773-109">Requirements</span></span>

<span data-ttu-id="0e773-110">**Spazio dei nomi:** <xref:System></span><span class="sxs-lookup"><span data-stu-id="0e773-110">**Namespace:** <xref:System></span></span>

<span data-ttu-id="0e773-111">**Assembly:** mscorlib. dll (in mscorlib. dll)</span><span class="sxs-lookup"><span data-stu-id="0e773-111">**Assembly:** mscorlib.dll (in mscorlib.dll)</span></span>

<span data-ttu-id="0e773-112">**Versioni .NET Framework:** Disponibile a partire da 1,0.</span><span class="sxs-lookup"><span data-stu-id="0e773-112">**.NET Framework versions:** Available since 1.0.</span></span>