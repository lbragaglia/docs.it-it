---
title: 'Procedura: Chiamare un metodo di estensione (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- calling extension methods [Visual Basic]
- extension methods [Visual Basic]
ms.assetid: df07750f-40f4-4c07-a79e-1113a27cfbea
ms.openlocfilehash: f2058162ab939d2619d7255c884d88c35ee63715
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512668"
---
# <a name="how-to-call-an-extension-method-visual-basic"></a>Procedura: Chiamare un metodo di estensione (Visual Basic)

I metodi di estensione consentono di aggiungere metodi a una classe esistente. Dopo che un metodo di estensione è stato dichiarato e introdotto nell'ambito, è possibile chiamarlo come metodo di istanza del tipo che estende. Per ulteriori informazioni su come scrivere un metodo di estensione, vedere [procedura: Scrivere un metodo](./how-to-write-an-extension-method.md)di estensione.

 Nelle istruzioni seguenti si fa riferimento al `PrintAndPunctuate`metodo di estensione, che consente di visualizzare l'istanza di stringa che la richiama, seguito da qualsiasi valore inviato per il secondo `punc`parametro,.

```vb
Imports System.Runtime.CompilerServices

Module StringExtensions
    <Extension()>
    Public Sub PrintAndPunctuate(ByVal aString As String,
                                 ByVal punc As String)
        Console.WriteLine(aString & punc)
    End Sub

End Module
```

Il metodo deve essere nell'ambito quando viene chiamato.

### <a name="to-call-an-extension-method"></a>Per chiamare un metodo di estensione

1. Dichiarare una variabile con il tipo di dati del primo parametro del metodo di estensione. Per `PrintAndPunctuate`è necessaria una <xref:System.String> variabile:

    ```vb
    Dim example = "Ready"
    ```

2. Tale variabile richiamerà il metodo di estensione e il relativo valore verrà associato al primo parametro `aString`. Viene visualizzata `Ready?`la seguente istruzione chiamante.

    ```vb
    example.PrintAndPunctuate("?")
    ```

     Si noti che la chiamata a questo metodo di estensione è simile a una chiamata a uno dei <xref:System.String> metodi di istanza che richiedono un solo parametro:

    ```vb
    example.EndsWith("dy")
    example.IndexOf("R")
    ```

3. Dichiarare un'altra variabile di stringa e chiamare di nuovo il metodo per verificare che funzioni con qualsiasi stringa.

    ```vb
    Dim example2 = " or not"
    example2.PrintAndPunctuate("!!!")
    ```

     Il risultato è il seguente: `or not!!!`.

## <a name="example"></a>Esempio
 Il codice seguente è un esempio completo della creazione e dell'uso di un semplice metodo di estensione.

```vb
Imports System.Runtime.CompilerServices
Imports ConsoleApplication1.StringExtensions

Module Module1

    Sub Main()

        Dim example = "Hello"
        example.PrintAndPunctuate(".")
        example.PrintAndPunctuate("!!!!")

        Dim example2 = "Goodbye"
        example2.PrintAndPunctuate("?")
    End Sub

    <Extension()>
    Public Sub PrintAndPunctuate(ByVal aString As String,
                                 ByVal punc As String)
        Console.WriteLine(aString & punc)
    End Sub
End Module

' Output:
' Hello.
' Hello!!!!
' Goodbye?
```

## <a name="see-also"></a>Vedere anche

- [Procedura: Scrivere un metodo di estensione](./how-to-write-an-extension-method.md)
- [Metodi di estensione](./extension-methods.md)
- [Ambito in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
