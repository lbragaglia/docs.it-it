---
title: 'Procedura: convertire un oggetto in un altro tipo in Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- objects [Visual Basic], converting
ms.assetid: 60cb5fc7-7ba4-4ab5-9c24-480fa12ddcdc
ms.openlocfilehash: 39083fc55d30e24c357ec162a15466f81655f4c8
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582335"
---
# <a name="how-to-convert-an-object-to-another-type-in-visual-basic"></a>Procedura: convertire un oggetto in un altro tipo in Visual Basic
Per convertire una variabile di `Object` in un altro tipo di dati, è possibile usare una parola chiave di conversione come la [funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene convertita una variabile `Object` in un `Integer` e in un `String`.  
  
```vb  
Public Sub objectConversion(ByVal anObject As Object)  
    Dim anInteger As Integer  
    Dim aString As String  
    anInteger = CType(anObject, Integer)  
    aString = CType(anObject, String)  
End Sub  
```  
  
 Se si è certi che il contenuto di una variabile `Object` è di un determinato tipo di dati, è preferibile convertire la variabile in quel tipo di dati. Se si continua a usare la variabile di `Object`, è necessario eseguire la *conversione boxing* e unboxing (per un tipo di valore) o l' *associazione tardiva* *(per* un tipo di riferimento). Queste operazioni consentono di ottenere tempo di esecuzione aggiuntivo e rallentare le prestazioni.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
- Un riferimento allo spazio dei nomi <xref:System?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Object>
- [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [Conversioni di ampliamento e restrizione](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [Conversioni implicite ed esplicite](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [Conversioni fra stringhe e altri tipi](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)
- [Conversioni di matrice](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)
- [Strutture](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [Tipi di dati](../../../../visual-basic/language-reference/data-types/index.md)
- [Funzioni di conversione del tipo](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
