---
ms.openlocfilehash: 9c72bc686e014a0bffdf272e3813358d1b29cc66
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65199149"
---
### <a name="net-com-successfully-marshals-byref-safearray-parameters-on-events"></a><span data-ttu-id="a30f3-101">.NET COM esegue correttamente il marshalling dei parametri ByRef SafeArray negli eventi</span><span class="sxs-lookup"><span data-stu-id="a30f3-101">.NET COM successfully marshals ByRef SafeArray parameters on events</span></span>

|   |   |
|---|---|
|<span data-ttu-id="a30f3-102">Dettagli</span><span class="sxs-lookup"><span data-stu-id="a30f3-102">Details</span></span>|<span data-ttu-id="a30f3-103">In .NET Framework 4.7.2 e versioni precedenti, un parametro ByRef [SafeArray](https://docs.microsoft.com/en-us/windows/desktop/api/oaidl/ns-oaidl-safearray) su un evento COM non sarebbe in grado di eseguire di nuovo il marshalling al codice nativo.</span><span class="sxs-lookup"><span data-stu-id="a30f3-103">In the .NET Framework 4.7.2 and earlier versions, a ByRef [SafeArray](https://docs.microsoft.com/en-us/windows/desktop/api/oaidl/ns-oaidl-safearray) parameter on a COM event would fail to marshal back to native code.</span></span>  <span data-ttu-id="a30f3-104">Con questa modifica il marshalling di [SafeArray](https://docs.microsoft.com/en-us/windows/desktop/api/oaidl/ns-oaidl-safearray) viene ora eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="a30f3-104">With this change the [SafeArray](https://docs.microsoft.com/en-us/windows/desktop/api/oaidl/ns-oaidl-safearray) is now marshaled successfully.</span></span><ul><li><span data-ttu-id="a30f3-105">[ x ] Anomalo</span><span class="sxs-lookup"><span data-stu-id="a30f3-105">[ x ] Quirked</span></span></li></ul>|
|<span data-ttu-id="a30f3-106">Suggerimento</span><span class="sxs-lookup"><span data-stu-id="a30f3-106">Suggestion</span></span>|<span data-ttu-id="a30f3-107">Se la corretta esecuzione del marshalling dei parametri ByRef SafeArray negli eventi COM interrompe l'esecuzione, è possibile disabilitare questo codice aggiungendo l'opzione di configurazione seguente alla configurazione dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="a30f3-107">If properly marshaling ByRef SafeArray parameters on COM Events breaks execution, you can disable this code by adding the following configuration switch to your application config:</span></span><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;Switch.System.Runtime.InteropServices.DoNotMarshalOutByrefSafeArrayOnInvoke&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>|
|<span data-ttu-id="a30f3-108">Ambito</span><span class="sxs-lookup"><span data-stu-id="a30f3-108">Scope</span></span>|<span data-ttu-id="a30f3-109">Secondario</span><span class="sxs-lookup"><span data-stu-id="a30f3-109">Minor</span></span>|
|<span data-ttu-id="a30f3-110">Versione</span><span class="sxs-lookup"><span data-stu-id="a30f3-110">Version</span></span>|<span data-ttu-id="a30f3-111">4.8</span><span class="sxs-lookup"><span data-stu-id="a30f3-111">4.8</span></span>|
|<span data-ttu-id="a30f3-112">Tipo</span><span class="sxs-lookup"><span data-stu-id="a30f3-112">Type</span></span>|<span data-ttu-id="a30f3-113">Runtime</span><span class="sxs-lookup"><span data-stu-id="a30f3-113">Runtime</span></span>|