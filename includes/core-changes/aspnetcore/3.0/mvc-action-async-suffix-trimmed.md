---
ms.openlocfilehash: dc9f37ae0cd6eef2c67e62421571290bba1c2233
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394386"
---
### <a name="mvc-async-suffix-trimmed-from-controller-action-names"></a>MVC: suffisso asincrono rimosso dai nomi delle azioni del controller

Nell'ambito dell'indirizzamento di [ASPNET/AspNetCore # 4849](https://github.com/aspnet/AspNetCore/issues/4849), ASP.NET Core MVC taglia il suffisso `Async` dai nomi delle azioni per impostazione predefinita. A partire da ASP.NET Core 3,0, questa modifica interessa sia il routing che la generazione del collegamento.

#### <a name="version-introduced"></a>Versione introdotta

3.0

#### <a name="old-behavior"></a>Comportamento precedente

Si consideri il seguente ASP.NET Core controller MVC:

```csharp
public class ProductController : Controller
{
    public async IActionResult ListAsync()
    {
        var model = await DbContext.Products.ToListAsync();
        return View(model);
    }
}
```

L'azione è instradabile tramite `Product/ListAsync`. Per la generazione di collegamenti è necessario specificare il suffisso `Async`. Esempio:

```cshtml
<a asp-controller="Product" asp-action="ListAsync">List</a>
```

#### <a name="new-behavior"></a>Nuovo comportamento

In ASP.NET Core 3,0, l'azione è instradabile tramite `Product/List`. Il codice di generazione del collegamento deve omettere il suffisso `Async`. Esempio:

```cshtml
<a asp-controller="Product" asp-action="List">List</a>
```

Questa modifica non influisce sui nomi specificati usando l'attributo `[ActionName]`. Il nuovo comportamento può essere disabilitato impostando `MvcOptions.SuppressAsyncSuffixInActionNames` su `false` in `Startup.ConfigureServices`:

```csharp
services.AddMvc(options =>
{
   options.SuppressAsyncSuffixInActionNames = false; 
});
```

#### <a name="reason-for-change"></a>Motivo della modifica

Per convenzione, i metodi .NET asincroni sono con suffisso `Async`. Tuttavia, quando un metodo definisce un'azione MVC, è indesiderabile usare il suffisso `Async`.

#### <a name="recommended-action"></a>Azione consigliata

Se l'app dipende da azioni MVC che conservano il suffisso `Async` del nome, scegliere una delle seguenti attenuazioni:

- Utilizzare l'attributo `[ActionName]` per mantenere il nome originale.
- Disabilitare la ridenominazione completamente impostando `MvcOptions.SuppressAsyncSuffixInActionNames` su `false` in `Startup.ConfigureServices`:

```csharp
services.AddMvc(options =>
{
   options.SuppressAsyncSuffixInActionNames = false; 
});
```

#### <a name="category"></a>Category

ASP.NET Core

#### <a name="affected-apis"></a>API interessate

Nessuno

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
