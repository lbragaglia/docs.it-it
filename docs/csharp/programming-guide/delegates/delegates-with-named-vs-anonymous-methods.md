---
title: Delegati con metodi denominati Metodi anonimi - Guida per programmatori C#
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- delegates [C#], with named vs. anonymous methods
- methods [C#], in delegates
ms.assetid: 98fa8c61-66b6-4146-986c-3236c4045733
ms.openlocfilehash: 9df143fb183ef2fc7e951b2cee47d18ce4b11942
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590657"
---
# <a name="delegates-with-named-vs-anonymous-methods-c-programming-guide"></a>Delegati con metodi denominati Metodi anonimi (Guida per programmatori C#)
È possibile associare un [delegato](../../language-reference/keywords/delegate.md) a un metodo denominato. Quando si crea un'istanza di un delegato usando un metodo denominato, il metodo viene passato come parametro, ad esempio:  
  
 [!code-csharp[csProgGuideDelegates#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#1)]  
  
 La chiamata viene eseguita usando un metodo denominato. I delegati costruiti con un metodo denominato possono incapsulare un metodo [statico](../../language-reference/keywords/static.md) o un metodo di istanza. I metodi denominati rappresentano l'unico modo per creare un'istanza di un delegato nelle versioni precedenti di C#. In una situazione in cui la creazione di un nuovo metodo rappresenta un sovraccarico inutile, tuttavia, C# consente di creare un'istanza di un delegato e di specificare immediatamente un blocco di codice che verrà elaborato dal delegato al momento della chiamata. Il blocco può contenere un'espressione lambda oppure un metodo anonimo. Per altre informazioni, vedere [Funzioni anonime](../statements-expressions-operators/anonymous-functions.md).  
  
## <a name="remarks"></a>Osservazioni  
 La firma del metodo che viene passato come parametro del delegato deve essere uguale a quella della dichiarazione del delegato.  
  
 Un'istanza di delegato può incapsulare un metodo statico o un metodo di istanza.  
  
 Anche se il delegato può usare un parametro [out](../../language-reference/keywords/out-parameter-modifier.md), è consigliabile non usarlo con delegati di eventi multicast perché non è possibile sapere quale delegato verrà chiamato.  
  
## <a name="example-1"></a>Esempio 1  
 Di seguito è illustrato un semplice esempio di dichiarazione e uso di un delegato. Si noti che sia il delegato, `Del`, che il metodo associato, `MultiplyNumbers`, hanno la stessa firma  
  
 [!code-csharp[csProgGuideDelegates#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#2)]  
  
## <a name="example-2"></a>Esempio 2  
 Nell'esempio che segue un delegato viene mappato sia al metodo statico che al metodo di istanza e restituisce informazioni specifiche da ciascuno di essi.  
  
 [!code-csharp[csProgGuideDelegates#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#3)]  
  
## <a name="see-also"></a>Vedere anche

- [Guida per programmatori C#](../index.md)
- [Delegati](./index.md)
- [Procedura: Combinare delegati multicast](./how-to-combine-delegates-multicast-delegates.md)
- [Eventi](../events/index.md)
