---
ms.openlocfilehash: fc17efbad63ee43ddcdfd14e2fbd1557d2b3d31c
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72424780"
---
### <a name="tls-1x-by-default-passes-the-sch_send_aux_record-flag-to-the-underlying-schannel-api"></a>TLS 1.x passa per impostazione predefinita il flag SCH_SEND_AUX_RECORD all'API SCHANNEL sottostante

|   |   |
|---|---|
|Dettagli|Quando si usa TLS 1.x, .NET Framework si basa sull'API SCHANNEL di Windows sottostante. A partire da .NET Framework 4.6, il flag [SCH_SEND_AUX_RECORD](https://docs.microsoft.com/windows/win32/api/schannel/ns-schannel-schannel_cred) viene passato per impostazione predefinita a SCHANNEL. SCHANNEL suddivide di conseguenza i dati da crittografare in due record separati, il primo come un singolo byte e il secondo come <em>n</em>-1 byte. In rari casi, ciò interrompe la comunicazione tra i client e i server esistenti che si basano sul presupposto che i dati risiedano in un singolo record.|
|Suggerimento|Se questa modifica interrompe la comunicazione con un server esistente, è possibile disabilitare l'invio del flag [SCH_SEND_AUX_RECORD](https://docs.microsoft.com/windows/win32/api/schannel/ns-schannel-schannel_cred) e ripristinare il comportamento precedente, che non prevede la suddivisione dei dati in record separati, aggiungendo l'opzione seguente all'elemento [<](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) nella sezione [<](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'app:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.Net.DontEnableSchSendAuxRecord=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre> <blockquote> [!IMPORTANT] Questa impostazione è disponibile solo per la compatibilità con le versioni precedenti. Il suo uso non è altrimenti consigliato.</blockquote> |
|Scope|Marginale|
|Versione|4.6|
|Digitare|Ridestinazione|
|API interessate|<ul><li><xref:System.Net.Security.SslStream?displayProperty=nameWithType></li><li><xref:System.Net.ServicePointManager?displayProperty=nameWithType></li><li><xref:System.Net.Http.HttpClient?displayProperty=nameWithType></li><li><xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType></li><li><xref:System.Net.HttpWebRequest?displayProperty=nameWithType></li><li><xref:System.Net.FtpWebRequest?displayProperty=nameWithType></li></ul>|
