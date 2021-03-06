---
title: Tag consigliati per i commenti della documentazione - Guida per programmatori C#
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- XML [C#], tags
- XML documentation [C#], tags
ms.assetid: 6e98f7a9-38f4-4d74-b644-1ff1b23320fd
ms.openlocfilehash: d17ff0b78d8ae40916447e8e12da7948a21e5717
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2019
ms.locfileid: "72523362"
---
# <a name="recommended-tags-for-documentation-comments-c-programming-guide"></a>Tag consigliati per i commenti relativi alla documentazione (Guida per programmatori C#)
Il compilatore C# elabora i commenti alla documentazione nel codice e li formatta come XML in un file il cui nome è stato specificato nell'opzione della riga di comando **/doc**. Per creare la documentazione finale basata sul file generato dal compilatore, è possibile creare uno strumento personalizzato o usare uno strumento come [DocFX](https://dotnet.github.io/docfx/) o [Sandcastle](https://github.com/EWSoftware/SHFB).  
  
 I tag vengono elaborati in costrutti di codice come tipi e membri dei tipi.  
  
> [!NOTE]
> Non è possibile applicare a uno spazio dei nomi i commenti relativi alla documentazione.  
  
 Il compilatore elabora tutti i tag validi per XML. I tag seguenti forniscono le funzionalità comunemente usate nella documentazione dell'utente.  
  
## <a name="tags"></a>Tag  
  
||||  
|---|---|---|  
|[\<c>](./code-inline.md)|[\<para>](./para.md)|[\<see>](./see.md)*|  
|[\<code>](./code.md)|[\<param>](./param.md)*|[\<seealso>](./seealso.md)*|  
|[\<example>](./example.md)|[\<paramref>](./paramref.md)|[\<summary>](./summary.md)|  
|[\<exception>](./exception.md)*|[\<permission>](./permission.md)*|[\<typeparam>](./typeparam.md)*|  
|[\<include>](./include.md)*|[\<remarks>](./remarks.md)|[\<typeparamref>](./typeparamref.md)|  
|[\<list>](./list.md)|[\<returns>](./returns.md)|[\<value>](./value.md)|  
  
 \* indica che il compilatore esegue la verifica della sintassi.  
  
 Se si vuole che nel testo di un commento alla documentazione vengano visualizzate parentesi angolari, usare la codifica HTML di `<` e `>`, ovvero rispettivamente `&lt;` e `&gt;`. Questa codifica viene mostrata nell'esempio seguente:
  
```csharp  
/// <summary>
/// This property always returns a value &lt; 1.
/// </summary>
```
  
## <a name="see-also"></a>Vedere anche

- [Guida per programmatori C#](../index.md)
- [-doc (opzioni del compilatore C#)](../../language-reference/compiler-options/doc-compiler-option.md)
- [Commenti relativi alla documentazione XML](./index.md)
