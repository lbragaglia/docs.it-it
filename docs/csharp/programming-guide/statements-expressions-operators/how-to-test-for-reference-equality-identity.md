---
title: "Procedura: Testare l'uguaglianza di riferimenti (identità) - Guida per programmatori C#"
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- object identity [C#]
- reference equality [C#]
ms.assetid: 91307fda-267b-4fd2-a338-2aada39ee791
ms.openlocfilehash: 2b4b7b7bdd03077a78aa2a6375764fa86a885ef5
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588635"
---
# <a name="how-to-test-for-reference-equality-identity-c-programming-guide"></a>Procedura: Testare l'uguaglianza di riferimenti (identità) (Guida per programmatori C#)
Non è necessario implementare alcuna logica personalizzata per supportare i confronti di uguaglianza dei riferimenti nei tipi. Questa funzionalità viene fornita per tutti i tipi dal metodo statico <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType>.  
  
 L'esempio seguente mostra come determinare se due variabili presentano *uguaglianza dei riferimenti*, ovvero se fanno riferimento allo stesso oggetto in memoria.  
  
 Nell'esempio viene inoltre illustrato perché <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> restituisce sempre `false` per i tipi di valore e perché non è consigliabile utilizzare <xref:System.Object.ReferenceEquals%2A> per determinare l'uguaglianza di stringhe.  
  
## <a name="example"></a>Esempio  
 [!code-csharp[csProgGuideObjects#90](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#90)]  
  
 L'implementazione di `Equals` nella classe di base universale <xref:System.Object?displayProperty=nameWithType> esegue anche un controllo dell'uguaglianza dei riferimenti, ma è meglio non servirsene perché, se una classe esegue l'override del metodo, i risultati potrebbero non essere quelli previsti. Lo stesso vale per gli operatori `==` e `!=`. Quando si opera sui tipi di riferimento, il comportamento predefinito di `==` e `!=` prevede l'esecuzione di un controllo dell'uguaglianza dei riferimenti. Le classi derivate possono tuttavia eseguire l'overload dell'operatore per eseguire un controllo dell'uguaglianza dei valori. Per ridurre al minimo la possibilità di errori, è preferibile usare sempre <xref:System.Object.ReferenceEquals%2A> quando è necessario determinare se due oggetti presentano uguaglianza dei riferimenti.  
  
 Stringhe costanti all'interno dello stesso assembly vengono sempre archiviate dal runtime. Ciò significa che viene mantenuta una sola istanza di ogni stringa letterale univoca. Il runtime tuttavia non garantisce che le stringhe create in fase di esecuzione vengano archiviate né garantisce che due stringhe costanti uguali in assembly diversi vengano centralizzate.  
  
## <a name="see-also"></a>Vedere anche

- [Confronti di uguaglianza](./equality-comparisons.md)
