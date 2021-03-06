---
ms.openlocfilehash: 846a6bcd3c668e6ad505f745bcb830c3b9dce437
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859271"
---
### <a name="aescryptoserviceprovider-decryptor-provides-a-reusable-transform"></a>Il componente di decrittografia AesCryptoServiceProvider fornisce una trasformazione riutilizzabile

|   |   |
|---|---|
|Dettagli|A partire dalle app destinate a .NET Framework 4.6.2, il componente di decrittografia <xref:System.Security.Cryptography.AesCryptoServiceProvider> fornisce una trasformazione riutilizzabile. Dopo una chiamata a <xref:System.Security.Cryptography.CryptoAPITransform.TransformFinalBlock(System.Byte[],System.Int32,System.Int32)?displayProperty=name>, la trasformazione viene reinizializzata e può essere riutilizzata. Per le app destinate a versioni precedenti di .NET Framework, il tentativo di riusare il componente di decrittografia chiamando <xref:System.Security.Cryptography.CryptoAPITransform.TransformBlock(System.Byte[],System.Int32,System.Int32,System.Byte[],System.Int32)?displayProperty=name> dopo una chiamata a <xref:System.Security.Cryptography.CryptoAPITransform.TransformFinalBlock(System.Byte[],System.Int32,System.Int32)?displayProperty=name> genera un'eccezione <xref:System.Security.Cryptography.CryptographicException> o produce dati danneggiati.|
|Suggerimento|L'impatto di questa modifica dovrebbe essere minimo, dato che questo è il comportamento previsto. Le applicazioni che dipendono dal comportamento precedente lo possono rifiutare esplicitamente aggiungendo l'impostazione di configurazione seguente alla sezione <code>&lt;runtime&gt;</code> del file di configurazione dell'applicazione:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.AesCryptoServiceProvider.DontCorrectlyResetDecryptor=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>Le applicazioni destinate a versioni precedenti di .NET Framework ma in esecuzione su una versione uguale o successiva a .NET Framework .NET Framework 4.6.2 possono acconsentire esplicitamente a questo comportamento aggiungendo l'impostazione di configurazione seguente alla sezione <code>&lt;runtime&gt;</code> del file di configurazione dell'applicazione:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.AesCryptoServiceProvider.DontCorrectlyResetDecryptor=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|Ambito|Secondario|
|Versione|4.6.2|
|Tipo|Ridestinazione|
|API interessate|<ul><li><xref:System.Security.Cryptography.AesCryptoServiceProvider.CreateDecryptor?displayProperty=nameWithType></li></ul>|

