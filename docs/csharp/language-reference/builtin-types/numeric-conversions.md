---
title: Conversioni numeriche predefinite- C# riferimento
ms.date: 10/22/2019
helpviewer_keywords:
- implicit numeric conversions [C#]
- explicit numeric conversion [C#]
- numeric conversions [C#], implicit
- numeric conversions [C#], explicit
- conversions [C#], implicit numeric
- conversions [C#], explicit numeric
ms.openlocfilehash: 5380e8480c39d1940df13b2ecb50a0f394367388
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72776033"
---
# <a name="built-in-numeric-conversions-c-reference"></a>Conversioni numeriche predefinite (C# riferimento)

C#fornisce un set di tipi numerici [integrali](integral-numeric-types.md) e a [virgola mobile](floating-point-numeric-types.md) . Esiste una conversione tra due tipi numerici, impliciti o espliciti. È necessario usare l' [operatore cast `()`](../operators/type-testing-and-cast.md#cast-operator-) per richiamare una conversione esplicita.

## <a name="implicit-numeric-conversions"></a>Conversioni numeriche implicite

Nella tabella seguente vengono illustrate le conversioni implicite predefinite tra i tipi numerici incorporati:

|Da|Per|
|----------|--------|
|[sbyte](integral-numeric-types.md)|`short`, `int`, `long`, `float`, `double` o `decimal`|
|[byte](integral-numeric-types.md)|`short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double` o `decimal`|
|[short](integral-numeric-types.md)|`int`, `long`, `float`, `double` o `decimal`|
|[ushort](integral-numeric-types.md)|`int`, `uint`, `long`, `ulong`, `float`, `double` o `decimal`|
|[int](integral-numeric-types.md)|`long`, `float`, `double` o `decimal`|
|[uint](integral-numeric-types.md)|`long`, `ulong`, `float`, `double` o `decimal`|
|[long](integral-numeric-types.md)|`float`, `double`o `decimal`|
|[ulong](integral-numeric-types.md)|`float`, `double`o `decimal`|
|[float](floating-point-numeric-types.md)|`double`|

> [!NOTE]
> Le conversioni implicite da `int`, `uint`, `long` o `ulong` a `float` e da `long` o `ulong` a `double` possono causare una perdita di precisione, ma mai una perdita di un ordine di grandezza. Le altre conversioni numeriche implicite non perdono mai le informazioni.

Si noti anche che

- Qualsiasi [tipo numerico integrale](integral-numeric-types.md) è implicitamente convertibile in qualsiasi [tipo numerico a virgola mobile](floating-point-numeric-types.md).

- Non esistono conversioni implicite per i tipi di `byte` e `sbyte`. Non esiste alcuna conversione implicita dai tipi `double` e `decimal`.

- Non esiste alcuna conversione implicita tra il tipo `decimal` e i tipi `float` o `double`.

- Il valore di un'espressione costante di tipo `int` (ad esempio, un valore rappresentato da un valore letterale integer) può essere convertito in modo implicito in `sbyte`, `byte`, `short`, `ushort`, `uint` o `ulong`, se è compreso nell'intervallo del tipo di destinazione :

  ```csharp
  byte a = 13;
  byte b = 300;  // CS0031: Constant value '300' cannot be converted to a 'byte'
  ```

  Come illustrato nell'esempio precedente, se il valore della costante non è compreso nell'intervallo del tipo di destinazione, si verifica un errore del compilatore [CS0031](../../misc/cs0031.md) .

## <a name="explicit-numeric-conversions"></a>Conversioni numeriche esplicite

Nella tabella seguente vengono illustrate le conversioni esplicite predefinite tra i tipi numerici incorporati per i quali non esiste alcuna [conversione implicita](#implicit-numeric-conversions):

|Da|Per|
|----------|--------|
|[sbyte](integral-numeric-types.md)|`byte`, `ushort`, `uint` o `ulong`|
|[byte](integral-numeric-types.md)|`sbyte`|
|[short](integral-numeric-types.md)|`sbyte`, `byte`, `ushort`, `uint` o `ulong`|
|[ushort](integral-numeric-types.md)|`sbyte`, `byte`o `short`|
|[int](integral-numeric-types.md)|`sbyte`, `byte`, `short`, `ushort`, `uint` o `ulong`|
|[uint](integral-numeric-types.md)|`sbyte`, `byte`, `short`, `ushort` o `int`|
|[long](integral-numeric-types.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint` o `ulong`|
|[ulong](integral-numeric-types.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint` o `long`|
|[float](floating-point-numeric-types.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong` o `decimal`|
|[double](floating-point-numeric-types.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float` o `decimal`|
|[decimal](floating-point-numeric-types.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float` o `double`|

> [!NOTE]
> Una conversione numerica esplicita potrebbe causare la perdita di dati o generare un'eccezione, in genere un <xref:System.OverflowException>.

Si noti anche che

- Quando si converte un valore di tipo integrale a un altro tipo integrale, il risultato dipende dal [contesto di controllo](../keywords/checked-and-unchecked.md) dell'overflow. In un contesto controllato, la conversione ha esito positivo se il valore di origine è compreso nell'intervallo del tipo di destinazione. In caso contrario, verrà generata un'eccezione <xref:System.OverflowException>. In un contesto non controllato, la conversione ha sempre esito positivo e procede nel modo seguente:

  - Se il tipo di origine è maggiore del tipo di destinazione, il valore di origine viene troncato rimuovendo i relativi "extra" bit più rilevanti. Il risultato viene quindi trattato come un valore del tipo di destinazione.

  - Se il tipo di origine è inferiore al tipo di destinazione, il valore di origine è con segno esteso o con estensione zero, in modo che sia della stessa dimensione del tipo di destinazione. L'estensione firma viene usata se il tipo di origine dispone della firma; l'estensione zero viene usata se il tipo di origine è privo di firma. Il risultato viene quindi trattato come un valore del tipo di destinazione.

  - Se il tipo di origine ha le stesse dimensioni del tipo di destinazione, il valore di origine viene considerato un valore del tipo di destinazione.

- Quando si esegue una conversione da un valore `decimal` a un tipo integrale, il valore viene arrotondato per difetto al valore integrale più vicino. Se il valore integrale risultante non rientra nell'intervallo del tipo di destinazione, viene generata un'eccezione <xref:System.OverflowException>.

- Quando si esegue una conversione da un valore `double` o `float` a un tipo integrale, il valore viene arrotondato per difetto al valore integrale più vicino. Se il valore integrale risultante non rientra nell'intervallo del tipo di destinazione, il risultato dipende dal [contesto di controllo](../keywords/checked-and-unchecked.md) dell'overflow. In un contesto controllato (checked) viene generata un'eccezione <xref:System.OverflowException>, mentre in un contesto non controllato (unckecked) il risultato è un valore non specificato del tipo di destinazione.

- Per una conversione da `double` a `float`, il valore `double` viene arrotondato al valore `float` più vicino. Se il valore `double` è troppo piccolo o troppo grande per adattarsi al tipo di `float`, il risultato sarà zero o infinito.

- Quando si esegue una conversione da `float` o `double` a `decimal`, il valore di origine viene convertito nella rappresentazione `decimal` e arrotondato al numero più vicino successivo alla ventottesima posizione decimale, se necessario. A seconda dell'entità del valore di origine, è possibile che si verifichi uno dei risultati seguenti:

  - Se il valore di origine è troppo piccolo per essere rappresentato come `decimal`, il risultato diventa zero.

  - Se il valore di origine è NaN (non un numero), infinito o troppo grande per essere rappresentato come `decimal`, viene generata un'eccezione <xref:System.OverflowException>.

- Quando si converte `decimal` in `float` o `double`, il valore di origine viene arrotondato rispettivamente al valore `float` o `double` più vicino.

## <a name="c-language-specification"></a>Specifiche del linguaggio C#

Per altre informazioni, vedere le sezioni seguenti delle [specifiche del linguaggio C#](~/_csharplang/spec/introduction.md):

- [Conversioni numeriche implicite](~/_csharplang/spec/conversions.md#implicit-numeric-conversions)
- [Conversioni numeriche esplicite](~/_csharplang/spec/conversions.md#explicit-numeric-conversions)

## <a name="see-also"></a>Vedere anche

- [Riferimenti per C#](../index.md)
- [Cast e conversioni di tipi](../../programming-guide/types/casting-and-type-conversions.md)
