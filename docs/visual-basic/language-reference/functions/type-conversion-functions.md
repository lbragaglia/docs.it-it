---
title: Funzioni di conversione del tipo (Visual Basic)
ms.date: 10/24/2018
f1_keywords:
- vb.CUShort
- vb.csng
- vb.CDate
- CByte
- CSng
- vb.CDec
- CBool
- CStr
- vb.CULng
- CDec
- CVErr
- CDbl
- CShort
- vb.CObj
- vb.CVErr
- CULng
- vb.cdbl
- vb.cbool
- CObj
- CDate
- CLng
- vb.cstr
- vb.cbyte
- vb.clng
- vb.CChar
- CUShort
- vb.CUInt
- vb.cint
- vb.CShort
- CInt
- CUInt
- CChar
helpviewer_keywords:
- CDate function
- CByte function
- Integer data type [Visual Basic], converting
- string conversion [Visual Basic], conversion functions
- fractions
- data types [Visual Basic], converting
- text, converting
- CDec function
- Char data type [Visual Basic], converting
- type conversion [Visual Basic], functions for
- Single data type [Visual Basic], converting
- numbers [Visual Basic], rounding
- rounding numbers [Visual Basic], type conversion
- CUShort function
- Long data type [Visual Basic], converting
- return values [Visual Basic], data types
- single-precision numbers [Visual Basic], converting
- data type conversion [Visual Basic], functions for
- CStr function
- times [Visual Basic], converting
- CSng function
- conversions [Visual Basic], type conversion functions
- CBool function
- CDbl function
- CUInt function
- Currency data type [Visual Basic], conversion functions
- numbers [Visual Basic], converting
- Double data type [Visual Basic], converting
- CLng function
- CSByte function
- double-precision numbers
- Decimal data type [Visual Basic], converting
- Boolean data type [Visual Basic], converting
- integers [Visual Basic], type conversion functions
- dates [Visual Basic], converting
- CULng function
- CInt function
- Date data type [Visual Basic], converting
- Byte data type [Visual Basic], converting
- String data type [Visual Basic], converting
- CChar function
- banker's rounding
- Short data type [Visual Basic], converting
- rounding numbers [Visual Basic], banker's rounding
- type conversion [Visual Basic], Visual Basic vs. .NET Framework
ms.assetid: d9d8d165-f967-44ff-a6cd-598e4740a99e
ms.openlocfilehash: 0516a579c1ad9944284d25f2f057f2f03619bbab
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582982"
---
# <a name="type-conversion-functions-visual-basic"></a>Funzioni di conversione del tipo (Visual Basic)

Queste funzioni vengono compilate inline, ovvero il codice di conversione fa parte del codice che valuta l'espressione. A volte non viene eseguita alcuna chiamata a una procedura per eseguire la conversione, migliorando le prestazioni. Ogni funzione assegna un'espressione a un tipo di dati specifico.

## <a name="syntax"></a>Sintassi

```vb
CBool(expression)
CByte(expression)
CChar(expression)
CDate(expression)
CDbl(expression)
CDec(expression)
CInt(expression)
CLng(expression)
CObj(expression)
CSByte(expression)
CShort(expression)
CSng(expression)
CStr(expression)
CUInt(expression)
CULng(expression)
CUShort(expression)
```

## <a name="part"></a>Parte

`expression`  
Obbligatorio. Qualsiasi espressione del tipo di dati di origine.

## <a name="return-value-data-type"></a>Tipo di dati del valore restituito

Il nome della funzione determina il tipo di dati del valore restituito, come illustrato nella tabella seguente.

|Nome funzione|Tipo di dati restituito|Intervallo per argomento `expression`|
|-------------------|----------------------|-------------------------------------|
|`CBool`|[Tipo di dati Boolean](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|Qualsiasi espressione `Char` o `String` o numeric valida.|
|`CByte`|[Tipo di dati Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md)|<xref:System.Byte.MinValue?displayProperty=nameWithType> (0) tramite <xref:System.Byte.MaxValue?displayProperty=nameWithType> (255) (senza segno); le parti frazionarie sono arrotondate. <sup>1</sup><br/><br/>A partire da Visual Basic 15,8, Visual Basic ottimizza le prestazioni della conversione da virgola mobile a byte con la funzione `CByte`; Per ulteriori informazioni, vedere la sezione [osservazioni](#remarks) . Per un esempio, vedere la sezione di [esempio CInt](#cint-example) .|
|`CChar`|[Tipo di dati Char](../../../visual-basic/language-reference/data-types/char-data-type.md)|Qualsiasi espressione `Char` o `String` valida; viene convertito solo il primo carattere di un `String`; il valore può essere compreso tra 0 e 65535 (senza segno).|
|`CDate`|[Tipo di dati Date](../../../visual-basic/language-reference/data-types/date-data-type.md)|Qualsiasi rappresentazione valida di data e ora.|
|`CDbl`|[Tipo di dati Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|-1.79769313486231570 e + 308 a-4.94065645841246544 E-324 per i valori negativi; 4.94065645841246544 e-324 tramite 1.79769313486231570 E + 308 per i valori positivi.|
|`CDec`|[Tipo di dati Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|+/-79.228.162.514.264.337.593.543.950.335 per numeri con scala zero, ovvero numeri senza posizioni decimali. Per i numeri con 28 cifre decimali, l'intervallo è +/-7.9228162514264337593543950335. Il numero più piccolo possibile diverso da zero è 0,0000000000000000000000000001 (+/-1E-28).|
|`CInt`|[Tipo di dati Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)|<xref:System.Int32.MinValue?displayProperty=nameWithType> (-2.147.483.648) tramite <xref:System.Int32.MaxValue?displayProperty=nameWithType> (2.147.483.647); le parti frazionarie sono arrotondate. <sup>1</sup> <br/><br/>A partire da Visual Basic 15,8, Visual Basic ottimizza le prestazioni della conversione da virgola mobile a integer con la funzione `CInt`; Per ulteriori informazioni, vedere la sezione [osservazioni](#remarks) . Per un esempio, vedere la sezione di [esempio CInt](#cint-example) . |
|`CLng`|[Tipo di dati Long](../../../visual-basic/language-reference/data-types/long-data-type.md)|<xref:System.Int64.MinValue?displayProperty=nameWithType> (-9.223.372.036.854.775.808) tramite <xref:System.Int64.MaxValue?displayProperty=nameWithType> (9.223.372.036.854.775.807); le parti frazionarie sono arrotondate. <sup>1</sup><br/><br/>A partire da Visual Basic 15,8, Visual Basic ottimizza le prestazioni della conversione di interi a virgola mobile a 64 bit con la funzione `CLng`; Per ulteriori informazioni, vedere la sezione [osservazioni](#remarks) . Per un esempio, vedere la sezione di [esempio CInt](#cint-example) .|
|`CObj`|[Tipo di dati Object](../../../visual-basic/language-reference/data-types/object-data-type.md)|Qualsiasi espressione valida.|
|`CSByte`|[Tipo di dati SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|<xref:System.SByte.MinValue?displayProperty=nameWithType> (-128) tramite <xref:System.SByte.MaxValue?displayProperty=nameWithType> (127); le parti frazionarie sono arrotondate. <sup>1</sup><br/><br/>A partire da Visual Basic 15,8, Visual Basic ottimizza le prestazioni della conversione in byte a virgola mobile e con firma con la funzione `CSByte`; Per ulteriori informazioni, vedere la sezione [osservazioni](#remarks) . Per un esempio, vedere la sezione di [esempio CInt](#cint-example) .|
|`CShort`|[Tipo di dati Short](../../../visual-basic/language-reference/data-types/short-data-type.md)|<xref:System.Int16.MinValue?displayProperty=nameWithType> (-32.768) tramite <xref:System.Int16.MaxValue?displayProperty=nameWithType> (32.767); le parti frazionarie sono arrotondate. <sup>1</sup><br/><br/>A partire da Visual Basic 15,8, Visual Basic ottimizza le prestazioni della conversione da virgola mobile a a 16 bit con la funzione `CShort`; Per ulteriori informazioni, vedere la sezione [osservazioni](#remarks) . Per un esempio, vedere la sezione di [esempio CInt](#cint-example) .|
|`CSng`|[Tipo di dati Single](../../../visual-basic/language-reference/data-types/single-data-type.md)|-3 402823e38 e + 38 fino a-401298E E-45 per i valori negativi; 401298E e-45 tramite 3 402823e38 E + 38 per i valori positivi.|
|`CStr`|[Tipo di dati String](../../../visual-basic/language-reference/data-types/string-data-type.md)|Restituisce per `CStr` dipendono dall'argomento `expression`. Vedere [valori restituiti per la funzione CStr](../../../visual-basic/language-reference/functions/return-values-for-the-cstr-function.md).|
|`CUInt`|[Tipo di dati UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|<xref:System.UInt32.MinValue?displayProperty=nameWithType> (0) tramite <xref:System.UInt32.MaxValue?displayProperty=nameWithType> (4.294.967.295) (senza segno); le parti frazionarie sono arrotondate. <sup>1</sup><br/><br/>A partire da Visual Basic 15,8, Visual Basic ottimizza le prestazioni della conversione a virgola mobile e Unsigned Integer con la funzione `CUInt`; Per ulteriori informazioni, vedere la sezione [osservazioni](#remarks) . Per un esempio, vedere la sezione di [esempio CInt](#cint-example) .|
|`CULng`|[Tipo di dati ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)|<xref:System.UInt64.MinValue?displayProperty=nameWithType> (0) tramite <xref:System.UInt64.MaxValue?displayProperty=nameWithType> (18.446.744.073.709.551.615) (senza segno); le parti frazionarie sono arrotondate. <sup>1</sup><br/><br/>A partire da Visual Basic 15,8, Visual Basic ottimizza le prestazioni della conversione a virgola mobile e long integer senza segno con la funzione `CULng`; Per ulteriori informazioni, vedere la sezione [osservazioni](#remarks) . Per un esempio, vedere la sezione di [esempio CInt](#cint-example) .|
|`CUShort`|[Tipo di dati UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)|<xref:System.UInt16.MinValue?displayProperty=nameWithType> (0) tramite <xref:System.UInt16.MaxValue?displayProperty=nameWithType> (65.535) (senza segno); le parti frazionarie sono arrotondate. <sup>1</sup><br/><br/>A partire da Visual Basic 15,8, Visual Basic ottimizza le prestazioni della conversione di interi a 16 bit senza segno a virgola mobile con la funzione `CUShort`; Per ulteriori informazioni, vedere la sezione [osservazioni](#remarks) . Per un esempio, vedere la sezione di [esempio CInt](#cint-example) .|

<sup>1</sup> le parti frazionarie possono essere soggette a un tipo speciale di arrotondamento denominato *arrotondamento del banco*. Per ulteriori informazioni, vedere la sezione "osservazioni".

## <a name="remarks"></a>Note

Come regola, è consigliabile usare le funzioni di conversione dei tipi di Visual Basic in preferenza ai metodi di .NET Framework, ad esempio `ToString()`, nella classe <xref:System.Convert> o in una singola struttura o classe del tipo. Le funzioni Visual Basic sono progettate per un'interazione ottimale con il codice Visual Basic e rendono anche il codice sorgente più breve e più facile da leggere. Inoltre, i metodi di conversione .NET Framework non producono sempre gli stessi risultati delle funzioni di Visual Basic, ad esempio quando si converte `Boolean` in `Integer`. Per ulteriori informazioni, vedere [risoluzione dei problemi](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)relativi ai tipi di dati.

A partire da Visual Basic 15,8, le prestazioni della conversione da virgola mobile a integer sono ottimizzate quando si passa il valore <xref:System.Single> o <xref:System.Double> restituito dai metodi seguenti a una delle funzioni di conversione integer (`CByte`, `CShort`, `CInt` @no__ t_5, `CSByte`, `CUShort`, `CUInt`, `CULng`):

- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Single)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Single)?displayProperty=nameWithType>
- <xref:System.Math.Ceiling(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Floor(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Round(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Truncate(System.Double)?displayProperty=nameWithType>

Questa ottimizzazione consente di eseguire il codice che esegue un numero elevato di conversioni di valori integer fino a due volte più velocemente. Nell'esempio seguente vengono illustrate le conversioni a virgola mobile ottimizzate:

```vb
Dim s As Single = 173.7619
Dim d As Double = s

Dim i1 As Integer = CInt(Fix(s))               ' Result: 173
Dim b1 As Byte = CByte(Int(d))                 ' Result: 173
Dim s1 AS Short = CShort(Math.Truncate(s))     ' Result: 173
Dim i2 As Integer = CInt(Math.Ceiling(d))      ' Result: 174
Dim i3 As Integer = CInt(Math.Round(s))        ' Result: 174
```

## <a name="behavior"></a>Comportamento

- **Coercizione.** In generale, è possibile utilizzare le funzioni di conversione del tipo di dati per assegnare il risultato di un'operazione a un tipo di dati specifico anziché al tipo di dati predefinito. Usare, ad esempio, `CDec` per forzare l'aritmetica decimale nei casi in cui in genere si verificano operazioni aritmetiche a precisione singola, a precisione doppia o Integer.

- **Conversioni non riuscite.** Se il `expression` passato alla funzione non è compreso nell'intervallo del tipo di dati in cui deve essere convertito, viene eseguita una <xref:System.OverflowException>.

- **Parti frazionarie.** Quando si converte un valore non integrale in un tipo integrale, le funzioni di conversione integer (`CByte`, `CInt`, `CLng`, `CSByte`, `CShort`, `CUInt`, `CULng` e `CUShort`) rimuovono la parte frazionaria e arrotondano il valore all'intero più vicino.

     Se la parte frazionaria è esattamente 0,5, le funzioni di conversione integer arrotondano al numero intero pari più vicino. 0,5, ad esempio, viene arrotondato a 0, 1,5 e 2,5 entrambi arrotondati a 2. Questa operazione viene talvolta denominata *arrotondamento del banco*e il suo scopo consiste nel compensare la distorsione che potrebbe accumularsi durante l'aggiunta di molti di questi numeri.

     `CInt` e `CLng` differiscono dalle funzioni <xref:Microsoft.VisualBasic.Conversion.Int%2A> e <xref:Microsoft.VisualBasic.Conversion.Fix%2A>, che troncano, anziché arrotondare, la parte frazionaria di un numero. Inoltre, `Fix` e `Int` restituiscono sempre un valore dello stesso tipo di dati passato.

- **Conversioni di data e ora.** Utilizzare la funzione <xref:Microsoft.VisualBasic.Information.IsDate%2A> per determinare se un valore può essere convertito in una data e ora. `CDate` riconosce i valori letterali di data e ora, ma non i valori numerici. Per convertire un valore di `Date` Visual Basic 6,0 in un valore `Date` in Visual Basic 2005 o versioni successive, è possibile usare il metodo <xref:System.DateTime.FromOADate%2A?displayProperty=nameWithType>.

- **Valori di data/ora neutri.** Il [tipo di dati date](../../../visual-basic/language-reference/data-types/date-data-type.md) contiene sempre le informazioni di data e ora. Ai fini della conversione del tipo, Visual Basic considera 1/1/0001 (1 gennaio dell'anno 1) come *valore neutro* per la data e 00:00:00 (mezzanotte) come valore neutro per l'ora. Se si converte un valore `Date` in una stringa, `CStr` non include valori neutri nella stringa risultante. Se ad esempio si converte `#January 1, 0001 9:30:00#` in una stringa, il risultato sarà "9:30:00 AM"; le informazioni sulla data vengono omesse. Tuttavia, le informazioni sulla data sono ancora presenti nel valore di `Date` originale e possono essere ripristinate con funzioni come <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> funzione.

- **Sensibilità delle impostazioni cultura.** Le funzioni di conversione dei tipi che coinvolgono stringhe eseguono conversioni in base alle impostazioni cultura correnti dell'applicazione. @No__t_0, ad esempio, riconosce i formati di data in base alle impostazioni locali del sistema. È necessario specificare il giorno, il mese e l'anno nell'ordine corretto per le impostazioni locali o la data potrebbe non essere interpretata correttamente. Un formato di data estesa non viene riconosciuto se contiene una stringa del giorno della settimana, ad esempio "mercoledì".

     Se è necessario eseguire la conversione da o verso una rappresentazione di stringa di un valore in un formato diverso da quello specificato dalle impostazioni locali, non è possibile usare le funzioni di conversione del tipo di Visual Basic. A tale scopo, usare i metodi `ToString(IFormatProvider)` e `Parse(String, IFormatProvider)` del tipo di tale valore. Usare, ad esempio, <xref:System.Double.Parse%2A?displayProperty=nameWithType> durante la conversione di una stringa in una `Double` e usare <xref:System.Double.ToString%2A?displayProperty=nameWithType> quando si converte un valore di tipo `Double` in una stringa.

## <a name="ctype-function"></a>CType Function

La [funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md) accetta un secondo argomento, `typename` e assegna `expression` a `typename`, dove `typename` può essere qualsiasi tipo di dati, struttura, classe o interfaccia a cui esiste una conversione valida.

Per un confronto tra `CType` con le altre parole chiave di conversione dei tipi, vedere [Operatore DirectCast](../../../visual-basic/language-reference/operators/directcast-operator.md) e [operatore TryCast](../../../visual-basic/language-reference/operators/trycast-operator.md).

## <a name="cbool-example"></a>Esempio di CBool

Nell'esempio seguente viene utilizzata la funzione `CBool` per convertire espressioni in valori `Boolean`. Se un'espressione restituisce un valore diverso da zero, `CBool` restituisce `True`; in caso contrario, restituisce `False`.

[!code-vb[VbVbalrFunctions#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#1)]

## <a name="cbyte-example"></a>Esempio di CByte

Nell'esempio seguente viene utilizzata la funzione `CByte` per convertire un'espressione in un `Byte`.

[!code-vb[VbVbalrFunctions#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#2)]

## <a name="cchar-example"></a>Esempio di CChar

Nell'esempio seguente viene utilizzata la funzione `CChar` per convertire il primo carattere di un'espressione `String` in un tipo di `Char`.

[!code-vb[VbVbalrFunctions#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#3)]

Il tipo di dati dell'argomento di input `CChar` deve essere `Char` o `String`. Non è possibile usare `CChar` per convertire un numero in un carattere, perché `CChar` non può accettare un tipo di dati numerico. Nell'esempio seguente viene ottenuto un numero che rappresenta un punto di codice (codice carattere) e lo converte nel carattere corrispondente. Usa la funzione <xref:Microsoft.VisualBasic.Interaction.InputBox%2A> per ottenere la stringa di cifre, `CInt` per convertire la stringa nel tipo `Integer` e `ChrW` per convertire il numero nel tipo `Char`.

[!code-vb[VbVbalrFunctions#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#4)]

## <a name="cdate-example"></a>Esempio di CDate

Nell'esempio seguente viene usata la funzione `CDate` per convertire le stringhe in valori `Date`. In generale, le date e le ore di codifica hardcoded come stringhe, come illustrato in questo esempio, non sono consigliate. Usare i valori letterali di data e ora, ad esempio #Feb 12, 1969 # e #4:45:23 PM #, in alternativa.

[!code-vb[VbVbalrFunctions#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#5)]

## <a name="cdbl-example"></a>Esempio di CDbl

[!code-vb[VbVbalrFunctions#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#6)]

## <a name="cdec-example"></a>Esempio di CDec

Nell'esempio seguente viene utilizzata la funzione `CDec` per convertire un valore numerico in `Decimal`.

[!code-vb[VbVbalrFunctions#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#7)]

## <a name="cint-example"></a>Esempio di CInt

Nell'esempio seguente viene utilizzata la funzione `CInt` per convertire un valore in `Integer`.

[!code-vb[VbVbalrFunctions#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#8)]

## <a name="clng-example"></a>Esempio di CLng

Nell'esempio seguente viene utilizzata la funzione `CLng` per convertire i valori `Long`.

[!code-vb[VbVbalrFunctions#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#9)]

## <a name="cobj-example"></a>Esempio di CObj

Nell'esempio seguente viene utilizzata la funzione `CObj` per convertire un valore numerico in `Object`. La variabile `Object` contiene solo un puntatore a quattro byte, che punta al valore `Double` assegnato.

[!code-vb[VbVbalrFunctions#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#10)]

## <a name="csbyte-example"></a>Esempio di CSByte

Nell'esempio seguente viene utilizzata la funzione `CSByte` per convertire un valore numerico in `SByte`.

[!code-vb[VbVbalrFunctions#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#11)]

## <a name="cshort-example"></a>Esempio di CShort

Nell'esempio seguente viene utilizzata la funzione `CShort` per convertire un valore numerico in `Short`.

[!code-vb[VbVbalrFunctions#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#12)]

## <a name="csng-example"></a>Esempio di CSng

Nell'esempio seguente viene utilizzata la funzione `CSng` per convertire i valori `Single`.

[!code-vb[VbVbalrFunctions#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#13)]

## <a name="cstr-example"></a>Esempio di CStr

Nell'esempio seguente viene utilizzata la funzione `CStr` per convertire un valore numerico in `String`.

[!code-vb[VbVbalrFunctions#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#14)]

Nell'esempio seguente viene utilizzata la funzione `CStr` per convertire i valori di `Date` in `String` valori.

[!code-vb[VbVbalrFunctions#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#15)]

`CStr` esegue sempre il rendering di un valore `Date` nel formato breve standard per le impostazioni locali correnti, ad esempio, "6/15/2003 4:35:47 PM". Tuttavia, `CStr` non vengono eliminati i *valori neutri* 1/1/0001 per la data e 00:00:00 per l'ora.

Per informazioni più dettagliate sui valori restituiti da `CStr`, vedere [valori restituiti per la funzione CStr](../../../visual-basic/language-reference/functions/return-values-for-the-cstr-function.md).

## <a name="cuint-example"></a>Esempio di CUInt

Nell'esempio seguente viene utilizzata la funzione `CUInt` per convertire un valore numerico in `UInteger`.

[!code-vb[VbVbalrFunctions#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#16)]

## <a name="culng-example"></a>Esempio di CULng

Nell'esempio seguente viene utilizzata la funzione `CULng` per convertire un valore numerico in `ULong`.

[!code-vb[VbVbalrFunctions#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#17)]

## <a name="cushort-example"></a>Esempio di CUShort

Nell'esempio seguente viene utilizzata la funzione `CUShort` per convertire un valore numerico in `UShort`.

[!code-vb[VbVbalrFunctions#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#18)]

## <a name="see-also"></a>Vedere anche

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- <xref:Microsoft.VisualBasic.Conversion.Int%2A>
- <xref:Microsoft.VisualBasic.Conversion.Fix%2A>
- <xref:Microsoft.VisualBasic.Strings.Format%2A>
- <xref:Microsoft.VisualBasic.Conversion.Hex%2A>
- <xref:Microsoft.VisualBasic.Conversion.Oct%2A>
- <xref:Microsoft.VisualBasic.Conversion.Str%2A>
- <xref:Microsoft.VisualBasic.Conversion.Val%2A>
- [Funzioni di conversione](../../../visual-basic/language-reference/functions/conversion-functions.md)
- [Conversioni di tipi in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
