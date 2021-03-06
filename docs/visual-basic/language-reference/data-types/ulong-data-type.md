---
title: Tipo di dati ULong (Visual Basic)
ms.date: 01/31/2018
f1_keywords:
- vb.ulong
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- literal type characters [Visual Basic], UL
- ULong data type
- UL literal type characters [Visual Basic]
ms.assetid: 017e0702-774e-44ae-bedc-786b424ca84e
ms.openlocfilehash: 19a75f056436b858a22588d7ac5f37df5dd326f2
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2019
ms.locfileid: "72583122"
---
# <a name="ulong-data-type-visual-basic"></a>Tipo di dati ULong (Visual Basic)

Include interi senza segno a 64 bit (8 byte) compresi tra 0 e 18.446.744.073.709.551.615 (più di 1,84 volte 10 ^ 19).

## <a name="remarks"></a>Note

Utilizzare il tipo di dati `ULong` per contenere dati binari troppo grandi per `UInteger` o i valori Unsigned Integer più grandi possibili.

Il valore predefinito di `ULong` è 0.

## <a name="literal-assignments"></a>Assegnazioni di valori letterali

È possibile dichiarare e inizializzare una variabile di `ULong` assegnando un valore letterale decimale, un valore letterale esadecimale, un valore letterale ottale o (a partire da Visual Basic 2017) un valore letterale binario. Se il valore letterale integer è esterno all'intervallo di `ULong`, vale a dire se è minore di <xref:System.UInt64.MinValue?displayProperty=nameWithType> o maggiore di <xref:System.UInt64.MaxValue?displayProperty=nameWithType>, si verifica un errore di compilazione.

Nell'esempio seguente, i valori interi uguali a 7.934.076.125 rappresentati come valori letterali decimali, esadecimali o binari vengono assegnati a valori `ULong`.

[!code-vb[ULong](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ULong)]

> [!NOTE]
> Usare il prefisso `&h` o `&H` per indicare un valore letterale esadecimale, il prefisso `&b` o `&B` per indicare un valore letterale binario e il prefisso `&o` o `&O` per indicare un valore letterale ottale. I valori letterali decimali non hanno prefissi.

A partire da Visual Basic 2017, è anche possibile usare il carattere di sottolineatura, `_`, come separatore di cifre per migliorare la leggibilità, come illustrato nell'esempio seguente.

[!code-vb[ULong](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

A partire da Visual Basic 15,5, è anche possibile usare il carattere di sottolineatura (`_`) come separatore iniziale tra il prefisso e le cifre esadecimali, binarie o ottali. Esempio:

```vb
Dim number As ULong = &H_F9AC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

I valori letterali numerici possono includere anche il [carattere di tipo](../../programming-guide/language-features/data-types/type-characters.md) `UL` o `ul` per indicare il tipo di dati `ULong`, come illustrato nell'esempio seguente.

```vb
Dim number = &H_00_00_0A_96_2F_AC_14_D7ul
```

## <a name="programming-tips"></a>Suggerimenti per la programmazione

- **Numeri negativi.** Poiché `ULong` è un tipo senza segno, non può rappresentare un numero negativo. Se si usa l'operatore meno unario (`-`) su un'espressione che restituisce il tipo `ULong`, Visual Basic converte prima l'espressione in `Decimal`.

- **Conformità a CLS.** Il tipo di dati `ULong` non fa parte della [Common Language Specification](https://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS), pertanto il codice conforme a CLS non può utilizzare un componente che lo utilizza.

- **Considerazioni sull'interoperabilità.** Se si interagisce con componenti non scritti per il .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che i tipi come `ulong` possono avere una larghezza dati diversa (32 bit) in altri ambienti. Se si passa un argomento a 32 bit a tale componente, dichiararlo come `UInteger` anziché `ULong` nel codice di Visual Basic gestito.

  Inoltre, l'automazione non supporta interi a 64 bit in Windows 95, Windows 98, Windows ME o Windows 2000. Non è possibile passare un Visual Basic `ULong` argomento a un componente di automazione su queste piattaforme.

- **Conversioni.** Il tipo di dati `ULong` viene ampliato in `Decimal`, `Single` e `Double`. Ciò significa che è possibile convertire `ULong` in uno di questi tipi senza riscontrare un errore <xref:System.OverflowException?displayProperty=nameWithType>.

- **Digitare i caratteri.** L'aggiunta di caratteri di tipo letterale `UL` a un valore letterale forza il tipo di dati `ULong`. `ULong` non dispone di alcun carattere di tipo identificatore.

- **Tipo di Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.UInt64?displayProperty=nameWithType>.

## <a name="see-also"></a>Vedere anche

- <xref:System.UInt64>
- [Tipi di dati](../../../visual-basic/language-reference/data-types/index.md)
- [Funzioni di conversione del tipo](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [Procedura: Chiamare una funzione Windows che accetta tipi senza segno](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [Uso efficiente dei tipi di dati](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
