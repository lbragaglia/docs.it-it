---
title: Esplorare intervalli di dati con indici e intervalli
description: Questa esercitazione avanzata descrive come esplorare i dati usando indici e intervalli per esaminare le sezioni di un set di dati sequenziale.
ms.date: 09/20/2019
ms.custom: mvc
ms.openlocfilehash: 1be144560d2b20bafc66cd68de0735e6dc7f0124
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699930"
---
# <a name="indices-and-ranges"></a>Indici e intervalli

Gli intervalli e gli indici forniscono una sintassi concisa per l'accesso a singoli elementi o intervalli in una sequenza.

In questa esercitazione si imparerà a:

> [!div class="checklist"]
>
> - Usare la sintassi per gli intervalli in una sequenza.
> - Comprendere le decisioni a livello di progettazione per l'inizio e la fine di ogni sequenza.
> - Analizzare gli scenari per i tipi <xref:System.Index> e <xref:System.Range>.

## <a name="language-support-for-indices-and-ranges"></a>Supporto del linguaggio per indici e intervalli

Questo supporto per il linguaggio si basa su due nuovi tipi e due nuovi operatori:

- <xref:System.Index?displayProperty=nameWithType> rappresenta un indice in una sequenza.
- Indice dell'operatore `^`end, che specifica che un indice è relativo alla fine di una sequenza.
- <xref:System.Range?displayProperty=nameWithType> rappresenta un intervallo secondario di una sequenza.
- Operatore `..`Range, che specifica l'inizio e la fine di un intervallo come operandi.

Per iniziare, ecco come funzionano le regole per gli indici. Prendere in considerazione una matrice `sequence`. L'indice `0` è uguale a `sequence[0]`. L'indice `^0` è uguale a `sequence[sequence.Length]`. Si noti che `sequence[^0]` genera un'eccezione, proprio come `sequence[sequence.Length]`. Per qualsiasi numero `n`, l'indice `^n` è uguale a `sequence[sequence.Length - n]`.

```csharp
string[] words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0
```

È possibile recuperare l'ultima parola con l'indice `^1`. Aggiungere il codice seguente sotto l'inizializzazione:

[!code-csharp[LastIndex](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastIndex)]

Un intervallo specifica *inizio* e *fine* di un intervallo. Gli intervalli sono esclusivi, vale a dire che la *fine* non è inclusa nell'intervallo. L'intervallo `[0..^0]` rappresenta l'intero intervallo, proprio come `[0..sequence.Length]` rappresenta l'intero intervallo. 

Il codice seguente crea un intervallo secondario con le parole "quick", "brown" e "fox". Include da `words[1]` a `words[3]`. L'elemento `words[4]` non è compreso nell'intervallo. Aggiungere il codice seguente allo stesso metodo. Copiarlo e incollarlo nella parte inferiore della finestra interattiva.

[!code-csharp[Range](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Range)]

Il codice seguente crea un intervallo secondario con "lazy" e "dog". Include `words[^2]` e `words[^1]`. L'indice finale `words[^0]` non viene incluso. Aggiungere anche il codice seguente:

[!code-csharp[LastRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastRange)]

Gli esempi seguenti creano intervalli aperti alle estremità, per l'inizio, la fine o entrambe:

[!code-csharp[PartialRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_PartialRanges)]

È anche possibile dichiarare gli intervalli o gli indici come variabili. In seguito la variabile può essere usata all'interno dei caratteri `[` e `]`:

[!code-csharp[IndexRangeTypes](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_RangeIndexTypes)]

L'esempio seguente illustra molti dei motivi per cui sono state fatte tali scelte. Modificare `x`, `y`, e `z` per provare combinazioni diverse. Durante le varie prove, usare valori per cui `x` è minore di `y` e `y` è minore di `z` per le combinazioni valide. Aggiungere il codice seguente in un nuovo metodo. Provare combinazioni diverse:

[!code-csharp[SemanticsExamples](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Semantics)]

## <a name="type-support-for-indices-and-ranges"></a>Supporto dei tipi per gli indici e gli intervalli

Se un tipo fornisce un [indicizzatore](../programming-guide/indexers/index.md) con un parametro <xref:System.Index> o <xref:System.Range>, supporta in modo esplicito gli indici o gli intervalli rispettivamente.

Un tipo può essere **conteggiato** se dispone di una proprietà denominata `Length` o `Count` con un getter accessibile e un tipo restituito `int`. Un tipo conteggiabile che non supporta in modo esplicito gli indici o gli intervalli può fornire un supporto implicito. Per ulteriori informazioni, vedere le sezioni supporto implicito degli [indici](~/_csharplang/proposals/csharp-8.0/ranges.md#implicit-index-support) e [supporto per intervalli impliciti](~/_csharplang/proposals/csharp-8.0/ranges.md#implicit-range-support) della [Nota relativa alla proposta di funzionalità](~/_csharplang/proposals/csharp-8.0/ranges.md).

I tipi .NET seguenti, ad esempio, supportano sia gli indici che gli intervalli: <xref:System.Array>, <xref:System.String>, <xref:System.Span%601> e <xref:System.ReadOnlySpan%601>. Il <xref:System.Collections.Generic.List%601> supporta gli indici, ma non supporta gli intervalli.

## <a name="scenarios-for-indices-and-ranges"></a>Scenari per gli indici e gli intervalli

Quando si vuole analizzare un intervallo secondario di un'intera sequenza, si usano spesso intervalli e indici. La nuova sintassi è più chiara e consente di capire meglio la funzione dell'intervallo secondario. La funzione locale `MovingAverage` accetta un <xref:System.Range> come argomento. In seguito il metodo enumera solo quell'intervallo durante il calcolo dei valori minimo e massimo e della media. Provare a includere il codice seguente nel progetto:

[!code-csharp[MovingAverages](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_MovingAverage)]

È possibile scaricare il codice completo dal repository [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/RangesIndexes).
