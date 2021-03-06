---
title: Proprietà dell'interfaccia - Guida per programmatori C#
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], on interfaces
- interfaces [C#], properties
ms.assetid: 6503e9ed-33d7-44ec-b4c1-cc16c084b795
ms.openlocfilehash: fad674c6d56011afcccbe9ce2a88e7af411fe0a2
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2019
ms.locfileid: "72579148"
---
# <a name="interface-properties-c-programming-guide"></a>Proprietà dell'interfaccia (Guida per programmatori C#)

Le proprietà possono essere dichiarate su una [interfaccia](../../language-reference/keywords/interface.md). Nell'esempio seguente viene illustrata la funzione di accesso di una proprietà di interfaccia:

[!code-csharp[csProgGuideProperties#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#14)]

La funzione di accesso di una proprietà di interfaccia non ha un corpo. Lo scopo delle funzioni di accesso, pertanto, è quello di indicare se la proprietà è in lettura-scrittura, in sola lettura o in sola scrittura.

## <a name="example"></a>Esempio

Nell'esempio seguente l'interfaccia `IEmployee` include una proprietà in lettura-scrittura, `Name`, e una proprietà in sola lettura, `Counter`. La classe `Employee` implementa l'interfaccia `IEmployee` e usa le due proprietà. Il programma legge il nome di un nuovo dipendente e il numero corrente di dipendenti e quindi visualizza il nome del dipendente e il relativo numero calcolato.

È possibile usare il nome completo della proprietà, che fa riferimento all'interfaccia in cui il membro è dichiarato. Esempio:

[!code-csharp[csProgGuideProperties#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#16)]

Questo meccanismo è denominato [Implementazione esplicita dell'interfaccia](../interfaces/explicit-interface-implementation.md). Se la classe `Employee` implementa, ad esempio, due interfacce, `ICitizen` e `IEmployee`, ed entrambe le interfacce includono la proprietà `Name`, sarà necessaria l'implementazione esplicita del membro dell'interfaccia. In altre parole, la dichiarazione di proprietà seguente:

[!code-csharp[csProgGuideProperties#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#16)]

implementa la proprietà `Name` nell'interfaccia `IEmployee`, mentre la dichiarazione seguente:

[!code-csharp[csProgGuideProperties#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#17)]

implementa la proprietà `Name` nell'interfaccia `ICitizen`.

[!code-csharp[csProgGuideProperties#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#15)]

**`210 Hazem Abolrous`**

## <a name="sample-output"></a>Esempio di output

```console
Enter number of employees: 210
Enter the name of the new employee: Hazem Abolrous
The employee information:
Employee number: 211
Employee name: Hazem Abolrous
```

## <a name="see-also"></a>Vedere anche

- [Guida per programmatori C#](../index.md)
- [Proprietà](./properties.md)
- [Uso delle proprietà](./using-properties.md)
- [Confronto tra proprietà e indicizzatori](../indexers/comparison-between-properties-and-indexers.md)
- [Indicizzatori](../indexers/index.md)
- [Interfacce](../interfaces/index.md)
