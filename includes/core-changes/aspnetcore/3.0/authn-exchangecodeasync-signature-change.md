---
ms.openlocfilehash: a4e20e0468d861138ad801c9dbfa15340b3f388c
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394283"
---
### <a name="authentication-oauthhandler-exchangecodeasync-signature-changed"></a><span data-ttu-id="34bfc-101">Autenticazione: OAuthHandler ExchangeCodeAsync firma modificata</span><span class="sxs-lookup"><span data-stu-id="34bfc-101">Authentication: OAuthHandler ExchangeCodeAsync signature changed</span></span>

<span data-ttu-id="34bfc-102">Nella ASP.NET Core 3,0 la firma di `OAuthHandler.ExchangeCodeAsync` è stata modificata da:</span><span class="sxs-lookup"><span data-stu-id="34bfc-102">In ASP.NET Core 3.0, the signature of `OAuthHandler.ExchangeCodeAsync` was changed from:</span></span>

```csharp
protected virtual System.Threading.Tasks.Task<Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse> ExchangeCodeAsync(string code, string redirectUri) { throw null; }
```

<span data-ttu-id="34bfc-103">A:</span><span class="sxs-lookup"><span data-stu-id="34bfc-103">To:</span></span>

```csharp
protected virtual System.Threading.Tasks.Task<Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse> ExchangeCodeAsync(Microsoft.AspNetCore.Authentication.OAuth.OAuthCodeExchangeContext context) { throw null; }
```

#### <a name="version-introduced"></a><span data-ttu-id="34bfc-104">Versione introdotta</span><span class="sxs-lookup"><span data-stu-id="34bfc-104">Version introduced</span></span>

<span data-ttu-id="34bfc-105">3.0</span><span class="sxs-lookup"><span data-stu-id="34bfc-105">3.0</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="34bfc-106">Comportamento precedente</span><span class="sxs-lookup"><span data-stu-id="34bfc-106">Old behavior</span></span>

<span data-ttu-id="34bfc-107">Le stringhe `code` e `redirectUri` sono state passate come argomenti distinti.</span><span class="sxs-lookup"><span data-stu-id="34bfc-107">The `code` and `redirectUri` strings were passed as separate arguments.</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="34bfc-108">Nuovo comportamento</span><span class="sxs-lookup"><span data-stu-id="34bfc-108">New behavior</span></span>

<span data-ttu-id="34bfc-109">`Code` e `RedirectUri` sono proprietà in `OAuthCodeExchangeContext` che possono essere impostate tramite il costruttore `OAuthCodeExchangeContext`.</span><span class="sxs-lookup"><span data-stu-id="34bfc-109">`Code` and `RedirectUri` are properties on `OAuthCodeExchangeContext` that can be set via the `OAuthCodeExchangeContext` constructor.</span></span> <span data-ttu-id="34bfc-110">Il nuovo tipo `OAuthCodeExchangeContext` è l'unico argomento passato a `OAuthHandler.ExchangeCodeAsync`.</span><span class="sxs-lookup"><span data-stu-id="34bfc-110">The new `OAuthCodeExchangeContext` type is the only argument passed to `OAuthHandler.ExchangeCodeAsync`.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="34bfc-111">Motivo della modifica</span><span class="sxs-lookup"><span data-stu-id="34bfc-111">Reason for change</span></span>

<span data-ttu-id="34bfc-112">Questa modifica consente di fornire parametri aggiuntivi in modo non sostanziale.</span><span class="sxs-lookup"><span data-stu-id="34bfc-112">This change allows additional parameters to be provided in a non-breaking manner.</span></span> <span data-ttu-id="34bfc-113">Non è necessario creare nuovi overload `ExchangeCodeAsync`.</span><span class="sxs-lookup"><span data-stu-id="34bfc-113">There's no need to create new `ExchangeCodeAsync` overloads.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="34bfc-114">Azione consigliata</span><span class="sxs-lookup"><span data-stu-id="34bfc-114">Recommended action</span></span>

<span data-ttu-id="34bfc-115">Costruire un `OAuthCodeExchangeContext` con i valori `code` e `redirectUri` appropriati.</span><span class="sxs-lookup"><span data-stu-id="34bfc-115">Construct an `OAuthCodeExchangeContext` with the appropriate `code` and `redirectUri` values.</span></span> <span data-ttu-id="34bfc-116">È necessario fornire un'istanza <xref:Microsoft.AspNetCore.Authentication.AuthenticationProperties>.</span><span class="sxs-lookup"><span data-stu-id="34bfc-116">An <xref:Microsoft.AspNetCore.Authentication.AuthenticationProperties> instance must be provided.</span></span> <span data-ttu-id="34bfc-117">Questa singola istanza `OAuthCodeExchangeContext` può essere passata al `OAuthHandler.ExchangeCodeAsync` anziché a più argomenti.</span><span class="sxs-lookup"><span data-stu-id="34bfc-117">This single `OAuthCodeExchangeContext` instance can be passed to `OAuthHandler.ExchangeCodeAsync` instead of multiple arguments.</span></span>

#### <a name="category"></a><span data-ttu-id="34bfc-118">Category</span><span class="sxs-lookup"><span data-stu-id="34bfc-118">Category</span></span>

<span data-ttu-id="34bfc-119">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="34bfc-119">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="34bfc-120">API interessate</span><span class="sxs-lookup"><span data-stu-id="34bfc-120">Affected APIs</span></span>

<xref:Microsoft.AspNetCore.Authentication.OAuth.OAuthHandler%601.ExchangeCodeAsync(System.String,System.String)?displayProperty=nameWithType>

<!--

#### Affected APIs

`M:Microsoft.AspNetCore.Authentication.OAuth.OAuthHandler`1.ExchangeCodeAsync(System.String,System.String)`

-->