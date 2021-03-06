---
title: Filtro di dati (C#)
ms.date: 07/20/2015
ms.assetid: fbaece0d-0f23-47f7-89c5-f3ea8db692b6
ms.openlocfilehash: 17d3a65b6042c9679a263eff0048f5360c4aa546
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2019
ms.locfileid: "69594389"
---
# <a name="filtering-data-c"></a>Filtro di dati (C#)
Il filtro si riferisce all'operazione in base alla quale il set di risultati viene limitato in modo da contenere solo gli elementi che corrispondono a una condizione specificata. È anche noto come selezione.  
  
 Nella figura seguente vengono illustrati i risultati del filtro di una sequenza di caratteri. Il predicato per l'operazione di filtro specifica che il carattere deve essere 'A'.  
  
 ![Diagramma che illustra un'operazione di filtro LINQ](./media/filtering-data/linq-filter-operation.png)  
  
 La sezione seguente elenca i metodi dell'operatore query standard che esegue la selezione.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|DESCRIZIONE|Sintassi di espressione della query C#|Altre informazioni|  
|-----------------|-----------------|---------------------------------|----------------------|  
|OfType|Seleziona i valori, a seconda della loro capacità di eseguire il cast a un tipo specificato.|Non applicabile.|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=nameWithType>|  
|Dove|Seleziona i valori che si basano su una funzione di predicato.|`where`|<xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>Esempio di sintassi delle espressioni di query  
 Nell'esempio seguente viene usata la clausola `where` per filtrare da una matrice le stringhe con una lunghezza specifica.  
  
```csharp  
string[] words = { "the", "quick", "brown", "fox", "jumps" };  
  
IEnumerable<string> query = from word in words  
                            where word.Length == 3  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
*/  
```  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Linq>
- [Panoramica degli operatori di query standard (C#)](./standard-query-operators-overview.md)
- [Clausola where](../../../language-reference/keywords/where-clause.md)
- [Procedura: Specificare dinamicamente i filtri dei predicati in fase di esecuzione](../../linq-query-expressions/how-to-dynamically-specify-predicate-filters-at-runtime.md)
- [Procedura: Eseguire una query sui metadati di un assembly tramite reflection (LINQ) (C#)](./how-to-query-an-assembly-s-metadata-with-reflection-linq.md)
- [Procedura: Eseguire una query per trovare i file con un attributo o un nome specifico (C#)](./how-to-query-for-files-with-a-specified-attribute-or-name.md)
- [Procedura: Ordinare o filtrare i dati di testo in base a qualsiasi parola o campo (LINQ) (C#)](./how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
