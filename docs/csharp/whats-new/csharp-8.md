---
title: Novità di C# 8.0 - Guida a C#
description: Panoramica delle nuove funzionalità disponibili in C# 8.0. Questo articolo è aggiornato alla versione di anteprima 2.
ms.date: 02/12/2019
ms.openlocfilehash: 874420775215502ebdacb8420b3fe0e027d6660f
ms.sourcegitcommit: 8f95d3a37e591963ebbb9af6e90686fd5f3b8707
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56747622"
---
# <a name="whats-new-in-c-80"></a><span data-ttu-id="9b53f-104">Novità di C# 8.0</span><span class="sxs-lookup"><span data-stu-id="9b53f-104">What's new in C# 8.0</span></span>

<span data-ttu-id="9b53f-105">Sono disponibili numerosi miglioramenti per il linguaggio C# che è già possibile provare con l'anteprima 2.</span><span class="sxs-lookup"><span data-stu-id="9b53f-105">There are many enhancements to the C# language that you can try out already with preview 2.</span></span> <span data-ttu-id="9b53f-106">Le nuove funzionalità aggiunte nell'anteprima 2 sono:</span><span class="sxs-lookup"><span data-stu-id="9b53f-106">The new features added in preview 2 are:</span></span>

- <span data-ttu-id="9b53f-107">[Miglioramenti dei criteri di ricerca](#more-patterns-in-more-places):</span><span class="sxs-lookup"><span data-stu-id="9b53f-107">[Pattern matching enhancements](#more-patterns-in-more-places):</span></span>
  * [<span data-ttu-id="9b53f-108">Espressioni switch</span><span class="sxs-lookup"><span data-stu-id="9b53f-108">Switch expressions</span></span>](#switch-expressions)
  * [<span data-ttu-id="9b53f-109">Criteri per le proprietà</span><span class="sxs-lookup"><span data-stu-id="9b53f-109">Property patterns</span></span>](#property-patterns)
  * [<span data-ttu-id="9b53f-110">Criteri per le tuple</span><span class="sxs-lookup"><span data-stu-id="9b53f-110">Tuple patterns</span></span>](#tuple-patterns)
  * [<span data-ttu-id="9b53f-111">Criteri per la posizione</span><span class="sxs-lookup"><span data-stu-id="9b53f-111">Positional patterns</span></span>](#positional-patterns)
- [<span data-ttu-id="9b53f-112">Dichiarazioni using</span><span class="sxs-lookup"><span data-stu-id="9b53f-112">Using declarations</span></span>](#using-declarations)
- [<span data-ttu-id="9b53f-113">Funzioni locali statiche</span><span class="sxs-lookup"><span data-stu-id="9b53f-113">Static local functions</span></span>](#static-local-functions)
- [<span data-ttu-id="9b53f-114">Struct ref Disposable</span><span class="sxs-lookup"><span data-stu-id="9b53f-114">Disposable ref structs</span></span>](#disposable-ref-structs)

<span data-ttu-id="9b53f-115">Le funzionalità del linguaggio seguenti sono state introdotte nell'anteprima 1 di C# 8.0:</span><span class="sxs-lookup"><span data-stu-id="9b53f-115">The following language features first appeared in C# 8.0 preview 1:</span></span>

- [<span data-ttu-id="9b53f-116">Tipi riferimento nullable</span><span class="sxs-lookup"><span data-stu-id="9b53f-116">Nullable reference types</span></span>](#nullable-reference-types)
- [<span data-ttu-id="9b53f-117">Flussi asincroni</span><span class="sxs-lookup"><span data-stu-id="9b53f-117">Asynchronous streams</span></span>](#asynchronous-streams)
- [<span data-ttu-id="9b53f-118">Indici e intervalli</span><span class="sxs-lookup"><span data-stu-id="9b53f-118">Indices and ranges</span></span>](#indices-and-ranges)

> [!NOTE]
> <span data-ttu-id="9b53f-119">Questo articolo è stato aggiornato per l'ultima volta per l'anteprima 2 di C# 8.0.</span><span class="sxs-lookup"><span data-stu-id="9b53f-119">This article was last updated for C# 8.0 preview 2.</span></span>

<span data-ttu-id="9b53f-120">Il resto di questo articolo descrive brevemente queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9b53f-120">The remainder of this article briefly describes these features.</span></span> <span data-ttu-id="9b53f-121">Se sono disponibili articoli approfonditi, vengono forniti collegamenti a queste panoramiche ed esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="9b53f-121">Where in-depth articles are available, links to those tutorials and overviews are provided.</span></span>

## <a name="more-patterns-in-more-places"></a><span data-ttu-id="9b53f-122">Più criteri in più posizioni</span><span class="sxs-lookup"><span data-stu-id="9b53f-122">More patterns in more places</span></span>

<span data-ttu-id="9b53f-123">I **criteri di ricerca** offrono strumenti per fornire funzionalità dipendenti dalla forma su tipi di dati correlati ma diversi.</span><span class="sxs-lookup"><span data-stu-id="9b53f-123">**Pattern matching** gives tools to provide shape-dependent functionality across related but different kinds of data.</span></span> <span data-ttu-id="9b53f-124">In C# 7.0 è stata introdotta la sintassi per i criteri di tipi e i criteri di costanti, tramite l'espressione [`is`](../language-reference/keywords/is.md) e l'istruzione [`switch`](../language-reference/keywords/switch.md).</span><span class="sxs-lookup"><span data-stu-id="9b53f-124">C# 7.0 introduced syntax for type patterns and constant patterns by using the [`is`](../language-reference/keywords/is.md) expression and the [`switch`](../language-reference/keywords/switch.md) statement.</span></span> <span data-ttu-id="9b53f-125">Queste funzionalità rappresentano il primo passo per il supporto dei paradigmi di programmazione in cui i dati e la funzionalità sono separati.</span><span class="sxs-lookup"><span data-stu-id="9b53f-125">These features represented the first tentative steps toward supporting programming paradigms where data and functionality live apart.</span></span> <span data-ttu-id="9b53f-126">Man mano che il settore effettua la transizione verso più microservizi e altre architetture basate sul cloud, diventano necessari altri strumenti del linguaggio.</span><span class="sxs-lookup"><span data-stu-id="9b53f-126">As the industry moves toward more microservices and other cloud-based architectures, other language tools are needed.</span></span>

<span data-ttu-id="9b53f-127">C# 8.0 espande questo vocabolario, in modo da poter usare più espressioni di criteri in più posizioni nel codice.</span><span class="sxs-lookup"><span data-stu-id="9b53f-127">C# 8.0 expands this vocabulary so you can use more pattern expressions in more places in your code.</span></span> <span data-ttu-id="9b53f-128">Prendere in considerazione queste funzionalità quando i dati e le funzionalità sono separati.</span><span class="sxs-lookup"><span data-stu-id="9b53f-128">Consider these features when your data and functionality are separate.</span></span> <span data-ttu-id="9b53f-129">Prendere in considerazione i criteri di ricerca quando gli algoritmi dipendono da un fatto diverso dal tipo di runtime di un oggetto.</span><span class="sxs-lookup"><span data-stu-id="9b53f-129">Consider pattern matching when your algorithms depend on a fact other than the runtime type of an object.</span></span> <span data-ttu-id="9b53f-130">Queste tecniche offrono un altro modo per esprimere le progettazioni.</span><span class="sxs-lookup"><span data-stu-id="9b53f-130">These techniques provide another way to express designs.</span></span>

<span data-ttu-id="9b53f-131">Oltre ai nuovi criteri disponibili in nuove posizioni, C# 8.0 introduce i **criteri ricorsivi**.</span><span class="sxs-lookup"><span data-stu-id="9b53f-131">In addition to new patterns in new places, C# 8.0 adds **recursive patterns**.</span></span> <span data-ttu-id="9b53f-132">Il risultato di qualsiasi espressione di criteri è un'espressione.</span><span class="sxs-lookup"><span data-stu-id="9b53f-132">The result of any pattern expression is an expression.</span></span> <span data-ttu-id="9b53f-133">Un criterio ricorsivo è semplicemente un'espressione di criteri applicata all'output di un'altra espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="9b53f-133">A recursive pattern is simply a pattern expression applied to the output of another pattern expression.</span></span>

### <a name="switch-expressions"></a><span data-ttu-id="9b53f-134">Espressioni switch</span><span class="sxs-lookup"><span data-stu-id="9b53f-134">switch expressions</span></span>

<span data-ttu-id="9b53f-135">Spesso, un'istruzione [`switch`](../language-reference/keywords/switch.md) produce un valore in ognuno dei relativi blocchi `case`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-135">Often, a [`switch`](../language-reference/keywords/switch.md) statement produces a value in each of its `case` blocks.</span></span> <span data-ttu-id="9b53f-136">Le **espressioni switch** consentono di usare una sintassi più concisa per le espressioni</span><span class="sxs-lookup"><span data-stu-id="9b53f-136">**Switch expressions** enable you to use more concise expression syntax.</span></span> <span data-ttu-id="9b53f-137">con meno parole chiave `case` e `break` ripetitive e un numero inferiore di parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="9b53f-137">There are fewer repetitive `case` and `break` keywords, and fewer curly braces.</span></span>  <span data-ttu-id="9b53f-138">Ad esempio, si consideri l'enumerazione seguente che elenca i colori dell'arcobaleno:</span><span class="sxs-lookup"><span data-stu-id="9b53f-138">As an example, consider the following enum that lists the colors of the rainbow:</span></span>

```csharp
public enum Rainbow
{
    Red,
    Orange,
    Yellow,
    Blue,
    Indigo,
    Violet
}
```

<span data-ttu-id="9b53f-139">È possibile convertire un valore `Rainbow` nei relativi valori RGB usando il metodo seguente che contiene un'espressione switch:</span><span class="sxs-lookup"><span data-stu-id="9b53f-139">You could convert a `Rainbow` value to its RGB values using the following method containing a switch expression:</span></span>

```csharp
public static RGBColor FromRainbow(Rainbow colorBand) =>
    colorBand switch
    {
        Rainbow.Red    => new RGBColor(0xFF, 0x00, 0x00),
        Rainbow.Orange => new RGBColor(0xFF, 0x7F, 0x00),
        Rainbow.Yellow => new RGBColor(0xFF, 0xFF, 0x00),
        Rainbow.Blue   => new RGBColor(0x00, 0x00, 0xFF),
        Rainbow.Indigo => new RGBColor(0x4B, 0x00, 0x82),
        Rainbow.Violet => new RGBColor(0x94, 0x00, 0xD3),
        _              => throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand)),
    };
```

<span data-ttu-id="9b53f-140">Questo esempio include numerosi miglioramenti della sintassi:</span><span class="sxs-lookup"><span data-stu-id="9b53f-140">There are several syntax improvements here:</span></span>

- <span data-ttu-id="9b53f-141">La variabile precede la parola chiave `switch`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-141">The variable comes before the `switch` keyword.</span></span> <span data-ttu-id="9b53f-142">L'ordine diverso rende più semplice distinguere visivamente l'espressione switch dall'istruzione switch.</span><span class="sxs-lookup"><span data-stu-id="9b53f-142">The different order makes it visually easy to distinguish the switch expression from the switch statement.</span></span>
- <span data-ttu-id="9b53f-143">Gli elementi `case` e `:` vengono sostituiti con `=>`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-143">The `case` and `:` elements are replaced with `=>`.</span></span> <span data-ttu-id="9b53f-144">È più conciso e intuitivo.</span><span class="sxs-lookup"><span data-stu-id="9b53f-144">It's more concise and intuitive.</span></span>
- <span data-ttu-id="9b53f-145">Il caso `default` è sostituito con un discard `_`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-145">The `default` case is replaced with a `_` discard.</span></span>
- <span data-ttu-id="9b53f-146">I corpi sono espressioni e non istruzioni.</span><span class="sxs-lookup"><span data-stu-id="9b53f-146">The bodies are expressions, not statements.</span></span>

<span data-ttu-id="9b53f-147">Confrontare questo codice con quello equivalente che usa l'istruzione `switch` classica:</span><span class="sxs-lookup"><span data-stu-id="9b53f-147">Contrast that with the equivalent code using the classic `switch` statement:</span></span>

```csharp
public static RGBColor fromRainbowClassic(Rainbow colorBand)
{
    switch (colorBand)
    {
        case Rainbow.Red:
            return new RGBColor(0xFF, 0x00, 0x00);
        case Rainbow.Orange:
            return new RGBColor(0xFF, 0x7F, 0x00);
        case Rainbow.Yellow:
            return new RGBColor(0xFF, 0xFF, 0x00);
        case Rainbow.Blue:
            return new RGBColor(0x00, 0x00, 0xFF);
        case Rainbow.Indigo:
            return new RGBColor(0x4B, 0x00, 0x82);
        case Rainbow.Violet:
            return new RGBColor(0x94, 0x00, 0xD3);
        default:
            throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand));
    };
}
```

### <a name="property-patterns"></a><span data-ttu-id="9b53f-148">Criteri per le proprietà</span><span class="sxs-lookup"><span data-stu-id="9b53f-148">Property patterns</span></span>

<span data-ttu-id="9b53f-149">I **criteri per le proprietà** consentono di individuare corrispondenze in base alle proprietà dell'oggetto esaminato.</span><span class="sxs-lookup"><span data-stu-id="9b53f-149">The **property pattern** enables you to match on properties of the object examined.</span></span> <span data-ttu-id="9b53f-150">Si consideri un sito di e-commerce che deve calcolare le imposte sulle vendite in base all'indirizzo dell'acquirente.</span><span class="sxs-lookup"><span data-stu-id="9b53f-150">Consider an eCommerce site that must compute sales tax based on the buyer's address.</span></span> <span data-ttu-id="9b53f-151">Questo calcolo non è una delle responsabilità principali di una classe `Address`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-151">That computation is not a core responsibility of an `Address` class.</span></span> <span data-ttu-id="9b53f-152">È soggetto a variazioni nel tempo, probabilmente più spesso rispetto a eventuali modifiche del formato dell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="9b53f-152">It will change over time, likely more often than address format changes.</span></span> <span data-ttu-id="9b53f-153">L'importo delle imposte sulle vendite dipende dalla proprietà `State` dell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="9b53f-153">The amount of sales tax depends on the `State` property of the address.</span></span> <span data-ttu-id="9b53f-154">Il metodo seguente usa i criteri per le proprietà per calcolare l'imposta sulle vendite dall'indirizzo e dal prezzo:</span><span class="sxs-lookup"><span data-stu-id="9b53f-154">The following method uses the property pattern to compute the sales tax from the address and the price:</span></span>

```csharp
public static decimal ComputeSalesTax(Address location, decimal salePrice) =>
    location switch
    {
        { State: "WA" } => salePrice * 0.06M,
        { State: "MN" } => salePrice * 0.75M,
        { State: "MI" } => salePrice * 0.05M,
        // other cases removed for brevity...
        _ => 0M
    };
    ```

Pattern matching creates a concise syntax for expressing this algorithm.

### Tuple patterns

Some algorithms depend on multiple inputs. **Tuple patterns** allow you to switch based on multiple values expressed as a [tuple](../tuples.md).  The following code shows a switch expression for the game *rock, paper, scissors*:

```csharp
public static string RockPaperScissors(string first, string second)
    => (first, second) switch
    {
        ("rock", "paper") => "rock is covered by paper. Paper wins.",
        ("rock", "scissors") => "rock breaks scissors. Rock wins.",
        ("paper", "rock") => "paper covers rock. Paper wins.",
        ("paper", "scissors") => "paper is cut by scissors. Scissors wins.",
        ("scissors", "rock") => "scissors is broken by rock. Rock wins.",
        ("scissors", "paper") => "scissors cuts paper. Scissors wins.",
        (_, _) => "tie"
    };
    ```

The messages indicate the winner. The discard case represents the three combinations for ties, or other text inputs.

### Positional patterns

Some types include a `Deconstruct` method that deconstructs its properties into discrete variables. When a `Deconstruct` method is accessible, you can use **positional patterns** to inspect properties of the object and use those properties for a pattern.  Consider the following `Point` class that includes a `Deconstruct` method to create discrete variables for `X` and `Y`:

```csharp
public class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) => (X, Y) = (x, y);

    public void Deconstruct(out int x, out int y) =>
        (x, y) = (X, Y);
}
```

<span data-ttu-id="9b53f-155">Il metodo seguente usa i **criteri per la posizione** per estrarre i valori di `x` e `y`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-155">The following method uses the **positional pattern** to extract the values of `x` and `y`.</span></span> <span data-ttu-id="9b53f-156">Usa quindi una clausola `when` per determinare il quadrante del punto:</span><span class="sxs-lookup"><span data-stu-id="9b53f-156">Then, it uses a `when` clause to determine the quadrant of the point:</span></span>

```csharp
static string Quadrant(Point p) => p switch
{
    (0, 0) => "origin",
    (var x, var y) when x > 0 && y > 0 => "Quadrant 1",
    (var x, var y) when x < 0 && y > 0 => "Quadrant 2",
    (var x, var y) when x < 0 && y < 0 => "Quadrant 3",
    (var x, var y) when x > 0 && y < 0 => "Quadrant 4",
    (var x, var y) => "on a border",
    _ => "unknown"
};
```

<span data-ttu-id="9b53f-157">I criteri discard nell'espressione switch precedente individuano una corrispondenza quando `x` o `y` è 0, ma non entrambi.</span><span class="sxs-lookup"><span data-stu-id="9b53f-157">The discard pattern in the preceding switch matches when either `x` or `y`, but not both, is 0.</span></span> <span data-ttu-id="9b53f-158">Un'espressione switch deve produrre un valore o generare un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="9b53f-158">A switch expression must either produce a value or throw an exception.</span></span> <span data-ttu-id="9b53f-159">Se nessuno dei casi corrisponde, l'espressione switch genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="9b53f-159">If none of the cases match, the switch expression throws an exception.</span></span> <span data-ttu-id="9b53f-160">Il compilatore genera un avviso per l'utente se non è possibile includere tutti i casi possibili nell'espressione switch.</span><span class="sxs-lookup"><span data-stu-id="9b53f-160">The compiler generates a warning for you if you do not cover all possible cases in your switch expression.</span></span>

## <a name="using-declarations"></a><span data-ttu-id="9b53f-161">Dichiarazioni using</span><span class="sxs-lookup"><span data-stu-id="9b53f-161">using declarations</span></span>

<span data-ttu-id="9b53f-162">Una **dichiarazione using** è una dichiarazione di variabile preceduta dalla parola chiave `using`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-162">A **using declaration** is a variable declaration preceded by the `using` keyword.</span></span> <span data-ttu-id="9b53f-163">Indica al compilatore che la variabile dichiarata deve essere eliminata alla fine dell'ambito di inclusione.</span><span class="sxs-lookup"><span data-stu-id="9b53f-163">It tells the compiler that the variable being declared should be disposed at the end of the enclosing scope.</span></span> <span data-ttu-id="9b53f-164">Ad esempio, si consideri il codice seguente che consente di scrivere un file di testo:</span><span class="sxs-lookup"><span data-stu-id="9b53f-164">For example, consider the following code that writes a text file:</span></span>

```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using var file = new System.IO.StreamWriter("WriteLines2.txt");
    foreach (string line in lines)
    {
        // If the line doesn't contain the word 'Second', write the line to the file.
        if (!line.Contains("Second"))
        {
            file.WriteLine(line);
        }
    }
// file is disposed here
}
```

<span data-ttu-id="9b53f-165">Nell'esempio precedente il file viene eliminato quando viene raggiunta la parentesi graffa di chiusura per il metodo.</span><span class="sxs-lookup"><span data-stu-id="9b53f-165">In the preceding example, the file is disposed when the closing brace for the method is reached.</span></span> <span data-ttu-id="9b53f-166">Questa è la fine dell'ambito in cui viene dichiarato `file`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-166">That's the end of the scope in which `file` is declared.</span></span> <span data-ttu-id="9b53f-167">Il codice precedente è equivalente al codice seguente con l'[istruzione using](../language-reference/keywords/using-statement.md) classica:</span><span class="sxs-lookup"><span data-stu-id="9b53f-167">The preceding code is equivalent to the following code using the classic [using statements](../language-reference/keywords/using-statement.md) statement:</span></span>


```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using (var file = new System.IO.StreamWriter("WriteLines2.txt"))
    {
        foreach (string line in lines)
        {
            // If the line doesn't contain the word 'Second', write the line to the file.
            if (!line.Contains("Second"))
            {
                file.WriteLine(line);
            }
        }
    } // file is disposed here
}
```

<span data-ttu-id="9b53f-168">Nell'esempio precedente il file viene eliminato quando viene raggiunta la parentesi graffa di chiusura associata all'istruzione `using`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-168">In the preceding example, the file is disposed when the closing brace associated with the `using` statement is reached.</span></span>

<span data-ttu-id="9b53f-169">In entrambi i casi, il compilatore genera la chiamata a `Dispose()`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-169">In both cases, the compiler generates the call to `Dispose()`.</span></span> <span data-ttu-id="9b53f-170">Il compilatore genera un errore se l'espressione nell'istruzione using non è eliminabile.</span><span class="sxs-lookup"><span data-stu-id="9b53f-170">The compiler generates an error if the expression in the using statement is not disposable.</span></span>

## <a name="static-local-functions"></a><span data-ttu-id="9b53f-171">Funzioni locali statiche</span><span class="sxs-lookup"><span data-stu-id="9b53f-171">Static local functions</span></span>

<span data-ttu-id="9b53f-172">È ora possibile aggiungere il modificatore `static` alle funzioni locali per assicurarsi che tale funzione locale non acquisisca (faccia riferimento a) variabili dall'ambito di inclusione.</span><span class="sxs-lookup"><span data-stu-id="9b53f-172">You can now add the `static` modifier to local functions to ensure that local function doesn't capture (reference) any variables from the enclosing scope.</span></span> <span data-ttu-id="9b53f-173">In questo modo viene generato l'errore `CS8421`, "A static local function can't contain a reference to <variable>." (Una funzione locale statica non può fare riferimento a 'variabile')</span><span class="sxs-lookup"><span data-stu-id="9b53f-173">Doing so generates `CS8421`, "A static local function can't contain a reference to <variable>."</span></span> 

<span data-ttu-id="9b53f-174">Si consideri il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="9b53f-174">Consider the following code.</span></span> <span data-ttu-id="9b53f-175">La funzione locale `LocalFunction` accede alla variabile `y`, dichiarata nell'ambito di inclusione (il metodo `M`).</span><span class="sxs-lookup"><span data-stu-id="9b53f-175">The local function `LocalFunction` accesses the variable `y`, declared in the enclosing scope (the method `M`).</span></span> <span data-ttu-id="9b53f-176">Pertanto, non è possibile dichiarare `LocalFunction` con il modificatore `static`:</span><span class="sxs-lookup"><span data-stu-id="9b53f-176">Therefore, `LocalFunction` can't be declared with the `static` modifier:</span></span>

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

<span data-ttu-id="9b53f-177">Il codice seguente contiene una funzione locale statica.</span><span class="sxs-lookup"><span data-stu-id="9b53f-177">The following code contains a static local function.</span></span> <span data-ttu-id="9b53f-178">Può essere statica perché non accede ad alcuna variabile nell'ambito di inclusione:</span><span class="sxs-lookup"><span data-stu-id="9b53f-178">It can be static because it doesn't access any variables in the enclosing scope:</span></span>

```csharp
int M()
{
    int y = 5;
    int x = 7;
    return Add(x, y);

    static int Add(int left, int right) => left + right;
}
```

## <a name="disposable-ref-structs"></a><span data-ttu-id="9b53f-179">Struct ref Disposable</span><span class="sxs-lookup"><span data-stu-id="9b53f-179">Disposable ref structs</span></span>

<span data-ttu-id="9b53f-180">Un oggetto `struct` dichiarato con il modificatore `ref` potrebbe non implementare alcuna interfaccia e quindi non può implementare <xref:System.IDisposable>.</span><span class="sxs-lookup"><span data-stu-id="9b53f-180">A `struct` declared with the `ref` modifier may not implement any interfaces and so cannot implement <xref:System.IDisposable>.</span></span> <span data-ttu-id="9b53f-181">Pertanto, per abilitare un `ref struct` per l'eliminazione, deve avere un metodo `void Dispose()` accessibile.</span><span class="sxs-lookup"><span data-stu-id="9b53f-181">Therefore, to enable a `ref struct` to be disposed, it must have an accessible `void Dispose()` method.</span></span> <span data-ttu-id="9b53f-182">Questo vale anche per le dichiarazioni `readonly ref struct`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-182">This also applies to `readonly ref struct` declarations.</span></span>

## <a name="nullable-reference-types"></a><span data-ttu-id="9b53f-183">Tipi riferimento nullable</span><span class="sxs-lookup"><span data-stu-id="9b53f-183">Nullable reference types</span></span>

<span data-ttu-id="9b53f-184">All'interno di un contesto delle annotazioni nullable, qualsiasi variabile di un tipo riferimento viene considerata come un **tipo riferimento non nullable**.</span><span class="sxs-lookup"><span data-stu-id="9b53f-184">Inside a nullable annotation context, any variable of a reference type is considered to be a **nonnullable reference type**.</span></span> <span data-ttu-id="9b53f-185">Se si vuole indicare che una variabile può essere Null, è necessario aggiungere `?` al nome del tipo per dichiarare la variabile come un **tipo riferimento nullable**.</span><span class="sxs-lookup"><span data-stu-id="9b53f-185">If you want to indicate that a variable may be null, you must append the type name with the `?` to declare the variable as a **nullable reference type**.</span></span>

<span data-ttu-id="9b53f-186">Per i tipi riferimento non nullable, il compilatore usa l'analisi di flusso per garantire che le variabili locali vengano inizializzate su un valore diverso da Null al momento della dichiarazione.</span><span class="sxs-lookup"><span data-stu-id="9b53f-186">For nonnullable reference types, the compiler uses flow analysis to ensure that local variables are initialized to a non-null value when declared.</span></span> <span data-ttu-id="9b53f-187">I campi devono essere inizializzati durante la costruzione.</span><span class="sxs-lookup"><span data-stu-id="9b53f-187">Fields must be initialized during construction.</span></span> <span data-ttu-id="9b53f-188">Il compilatore genera un avviso se la variabile non è impostata da una chiamata a uno qualsiasi dei costruttori disponibili o da un inizializzatore.</span><span class="sxs-lookup"><span data-stu-id="9b53f-188">The compiler generates a warning if the variable is not set by a call to any of the available constructors or by an initializer.</span></span> <span data-ttu-id="9b53f-189">Inoltre, non è possibile assegnare ai tipi riferimento non nullable un valore che potrebbe essere Null.</span><span class="sxs-lookup"><span data-stu-id="9b53f-189">Furthermore, nonnullable reference types can't be assigned a value that could be null.</span></span>

<span data-ttu-id="9b53f-190">I tipi riferimento nullable non vengono controllati per verificare che non vengano assegnati o inizializzati su Null.</span><span class="sxs-lookup"><span data-stu-id="9b53f-190">Nullable reference types aren't checked to ensure they aren't assigned or initialized to null.</span></span> <span data-ttu-id="9b53f-191">Tuttavia, il compilatore usa l'analisi di flusso per garantire che qualsiasi variabile di un tipo riferimento nullable venga controllata per i valori Null prima dell'accesso o prima che venga assegnata a un tipo riferimento non nullable.</span><span class="sxs-lookup"><span data-stu-id="9b53f-191">However, the compiler uses flow analysis to ensure that any variable of a nullable reference type is checked against null before it's accessed or assigned to a nonnullable reference type.</span></span>

<span data-ttu-id="9b53f-192">Altre informazioni su questa funzionalità sono disponibili nella panoramica dei [tipi riferimento nullable](../nullable-references.md).</span><span class="sxs-lookup"><span data-stu-id="9b53f-192">You can learn more about the feature in the overview of [nullable reference types](../nullable-references.md).</span></span> <span data-ttu-id="9b53f-193">È possibile provare in autonomia in una nuova applicazione in questa [esercitazione sui tipi riferimento nullable](../tutorials/nullable-reference-types.md).</span><span class="sxs-lookup"><span data-stu-id="9b53f-193">Try it yourself in a new application in this [nullable reference types tutorial](../tutorials/nullable-reference-types.md).</span></span> <span data-ttu-id="9b53f-194">Per informazioni sulla procedura per eseguire la migrazione di una base di codice esistente per l'uso dei tipi riferimento nullable, vedere l'[esercitazione sulla migrazione di un'applicazione per l'uso dei tipi riferimento nullable](../tutorials/upgrade-to-nullable-references.md).</span><span class="sxs-lookup"><span data-stu-id="9b53f-194">Learn about the steps to migrate an existing codebase to make use of nullable reference types in the [migrating an application to use nullable reference types tutorial](../tutorials/upgrade-to-nullable-references.md).</span></span>

## <a name="asynchronous-streams"></a><span data-ttu-id="9b53f-195">Flussi asincroni</span><span class="sxs-lookup"><span data-stu-id="9b53f-195">Asynchronous streams</span></span>

<span data-ttu-id="9b53f-196">A partire da C# 8.0, è possibile creare e utilizzare i flussi in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="9b53f-196">Starting with C# 8.0, you can create and consume streams asynchronously.</span></span> <span data-ttu-id="9b53f-197">Un metodo che restituisce un flusso asincrono ha tre proprietà:</span><span class="sxs-lookup"><span data-stu-id="9b53f-197">A method that returns an asynchronous stream has three properties:</span></span>

1. <span data-ttu-id="9b53f-198">È stato dichiarato con il modificatore `async`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-198">It was declared with the `async` modifier.</span></span>
1. <span data-ttu-id="9b53f-199">Restituisce <xref:System.Collections.Generic.IAsyncEnumerable%601>.</span><span class="sxs-lookup"><span data-stu-id="9b53f-199">It returns an <xref:System.Collections.Generic.IAsyncEnumerable%601>.</span></span>
1. <span data-ttu-id="9b53f-200">Il metodo contiene istruzioni `yield return` per restituire gli elementi successivi nel flusso asincrono.</span><span class="sxs-lookup"><span data-stu-id="9b53f-200">The method contains `yield return` statements to return successive elements in the asynchronous stream.</span></span>

<span data-ttu-id="9b53f-201">Per utilizzare un flusso asincrono, è necessario aggiungere la parola chiave `await` prima della parola chiave `foreach` quando si enumerano gli elementi del flusso.</span><span class="sxs-lookup"><span data-stu-id="9b53f-201">Consuming an asynchronous stream requires you to add the `await` keyword before the `foreach` keyword when you enumerate the elements of the stream.</span></span> <span data-ttu-id="9b53f-202">Per l'aggiunta della parola chiave `await`, il metodo che enumera il flusso asincrono deve essere dichiarato con il modificatore `async` e restituire un tipo consentito per un metodo `async`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-202">Adding the `await` keyword requires the method that enumerates the asynchronous stream to be declared with the `async` modifier and to return a type allowed for an `async` method.</span></span> <span data-ttu-id="9b53f-203">In genere ciò significa restituire <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>.</span><span class="sxs-lookup"><span data-stu-id="9b53f-203">Typically that means returning a <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="9b53f-204">Può anche essere <xref:System.Threading.Tasks.ValueTask> o <xref:System.Threading.Tasks.ValueTask%601>.</span><span class="sxs-lookup"><span data-stu-id="9b53f-204">It can also be a <xref:System.Threading.Tasks.ValueTask> or <xref:System.Threading.Tasks.ValueTask%601>.</span></span> <span data-ttu-id="9b53f-205">Un metodo può sia utilizzare che produrre un flusso asincrono, il che significa che restituirebbe <xref:System.Collections.Generic.IAsyncEnumerable%601>.</span><span class="sxs-lookup"><span data-stu-id="9b53f-205">A method can both consume and produce an asynchronous stream, which means it would return an <xref:System.Collections.Generic.IAsyncEnumerable%601>.</span></span> <span data-ttu-id="9b53f-206">Il codice seguente genera una sequenza da 1 a 20, con un'attesa di 100 ms tra la generazione di ogni numero:</span><span class="sxs-lookup"><span data-stu-id="9b53f-206">The following code generates a sequence from 1 to 20, waiting 100 ms between generating each number:</span></span>

```csharp
public static async System.Collections.Generic.IAsyncEnumerable<int> GenerateSequence()
{
    for (int i = 0; i < 20; i++)
    {
        await Task.Delay(100);
        yield return i;
    }
}
```

<span data-ttu-id="9b53f-207">La sequenza viene enumerata usando l'istruzione `await foreach`:</span><span class="sxs-lookup"><span data-stu-id="9b53f-207">You would enumerate the sequence using the `await foreach` statement:</span></span>

```csharp
await foreach (var number in GenerateSequence())
{
    Console.WriteLine(number);
}
```

<span data-ttu-id="9b53f-208">È possibile provare i flussi asincroni in autonomia nell'esercitazione dedicata alla [creazione e all'utilizzo di flussi asincroni](../tutorials/generate-consume-asynchronous-stream.md).</span><span class="sxs-lookup"><span data-stu-id="9b53f-208">You can try asynchronous streams yourself in our tutorial on [creating and consuming async streams](../tutorials/generate-consume-asynchronous-stream.md).</span></span>

## <a name="indices-and-ranges"></a><span data-ttu-id="9b53f-209">Indici e intervalli</span><span class="sxs-lookup"><span data-stu-id="9b53f-209">Indices and ranges</span></span>

<span data-ttu-id="9b53f-210">Gli intervalli e gli indici offrono una sintassi concisa per la specifica di intervalli secondari in una matrice, <xref:System.Span%601> o <xref:System.ReadOnlySpan%601>.</span><span class="sxs-lookup"><span data-stu-id="9b53f-210">Ranges and indices provide a succinct syntax for specifying subranges in an array, <xref:System.Span%601>, or <xref:System.ReadOnlySpan%601>.</span></span>

<span data-ttu-id="9b53f-211">È possibile specificare un indice **dalla fine**.</span><span class="sxs-lookup"><span data-stu-id="9b53f-211">You can specify an index **from the end**.</span></span> <span data-ttu-id="9b53f-212">Per specificarlo **dalla fine** si usa l'operatore `^`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-212">You specify **from the end** using the `^` operator.</span></span> <span data-ttu-id="9b53f-213">Si ha familiarità con `array[2]`, che indica l'elemento "2 dall'inizio".</span><span class="sxs-lookup"><span data-stu-id="9b53f-213">You are familiar with `array[2]` meaning the element "2 from the start".</span></span> <span data-ttu-id="9b53f-214">`array[^2]` significa l'elemento "2 dalla fine".</span><span class="sxs-lookup"><span data-stu-id="9b53f-214">Now, `array[^2]` means the element "2 from the end".</span></span> <span data-ttu-id="9b53f-215">L'indice `^0` significa "la fine" o l'indice che segue l'ultimo elemento.</span><span class="sxs-lookup"><span data-stu-id="9b53f-215">The index `^0` means "the end", or the index that follows the last element.</span></span>

<span data-ttu-id="9b53f-216">È possibile specificare un **intervallo** con l'**operatore range**: `..`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-216">You can specify a **range** with the **range operator**: `..`.</span></span> <span data-ttu-id="9b53f-217">Ad esempio, `0..^0` specifica l'intero intervallo della matrice: 0 dall'inizio fino a 0 dalla fine, escluso.</span><span class="sxs-lookup"><span data-stu-id="9b53f-217">For example, `0..^0` specifies the entire range of the array: 0 from the start up to, but not including 0 from the end.</span></span> <span data-ttu-id="9b53f-218">Per entrambi gli operandi è possibile usare "dall'inizio" o "dalla fine".</span><span class="sxs-lookup"><span data-stu-id="9b53f-218">Either operand may use "from the start" or "from the end".</span></span> <span data-ttu-id="9b53f-219">Inoltre, uno degli operandi può essere omesso.</span><span class="sxs-lookup"><span data-stu-id="9b53f-219">Furthermore, either operand may be omitted.</span></span> <span data-ttu-id="9b53f-220">I valori predefiniti sono `0` per l'indice iniziale e `^0` per l'indice finale.</span><span class="sxs-lookup"><span data-stu-id="9b53f-220">The defaults are `0` for the start index, and `^0` for the end index.</span></span>

<span data-ttu-id="9b53f-221">Di seguito verranno esaminati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="9b53f-221">Let's look at a few examples.</span></span> <span data-ttu-id="9b53f-222">Si consideri la matrice seguente, annotata con il relativo indice dall'inizio e dalla fine:</span><span class="sxs-lookup"><span data-stu-id="9b53f-222">Consider the following array, annotated with its index from the start and from the end:</span></span>

```csharp
var words = new string[]
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
};
```

<span data-ttu-id="9b53f-223">L'indice di ogni elemento consolida il concetto di "dall'inizio" e "dalla fine" e che gli intervalli escludono la fine dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="9b53f-223">The index of each element reinforces the concept of "from the start", and "from the end", and that ranges are exclusive of the end of the range.</span></span> <span data-ttu-id="9b53f-224">L'intera matrice "inizia" con il primo elemento.</span><span class="sxs-lookup"><span data-stu-id="9b53f-224">The "start" of the entire array is the first element.</span></span> <span data-ttu-id="9b53f-225">La "fine" dell'intera matrice è *dopo* l'ultimo elemento.</span><span class="sxs-lookup"><span data-stu-id="9b53f-225">The "end" of the entire array is *past* the last element.</span></span>

<span data-ttu-id="9b53f-226">È possibile recuperare l'ultima parola con l'indice `^1`:</span><span class="sxs-lookup"><span data-stu-id="9b53f-226">You can retrieve the last word with the `^1` index:</span></span>

```csharp
Console.WriteLine($"The last word is {words[^1]}");
// writes "dog"
```

<span data-ttu-id="9b53f-227">Il codice seguente crea un intervallo secondario con le parole "quick", "brown" e "fox".</span><span class="sxs-lookup"><span data-stu-id="9b53f-227">The following code creates a subrange with the words "quick", "brown", and "fox".</span></span> <span data-ttu-id="9b53f-228">Include da `words[1]` a `words[3]`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-228">It includes `words[1]` through `words[3]`.</span></span> <span data-ttu-id="9b53f-229">L'elemento `words[4]` non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="9b53f-229">The element `words[4]` is not in the range.</span></span>

```csharp
var brownFox = words[1..4];
```

<span data-ttu-id="9b53f-230">Il codice seguente crea un intervallo secondario con "lazy" e "dog".</span><span class="sxs-lookup"><span data-stu-id="9b53f-230">The following code creates a subrange with "lazy" and "dog".</span></span> <span data-ttu-id="9b53f-231">Include `words[^2]` e `words[^1]`.</span><span class="sxs-lookup"><span data-stu-id="9b53f-231">It includes `words[^2]` and `words[^1]`.</span></span> <span data-ttu-id="9b53f-232">L'indice finale `words[^0]` non viene incluso:</span><span class="sxs-lookup"><span data-stu-id="9b53f-232">The end index `words[^0]` is not included:</span></span>

```csharp
var lazyDog = words[^2..^0];
```

<span data-ttu-id="9b53f-233">Gli esempi seguenti creano intervalli aperti alle estremità, per l'inizio, la fine o entrambe:</span><span class="sxs-lookup"><span data-stu-id="9b53f-233">The following examples create ranges that are open ended for the start, end, or both:</span></span>

```csharp
var allWords = words[..]; // contains "The" through "dog".
var firstPhrase = words[..4]; // contains "The" through "fox"
var lastPhrase = words[6..]; // contains "the, "lazy" and "dog"
```

<span data-ttu-id="9b53f-234">È anche possibile dichiarare gli intervalli come variabili:</span><span class="sxs-lookup"><span data-stu-id="9b53f-234">You can also declare ranges as variables:</span></span>

```csharp
Range phrase = 1..4;
```

<span data-ttu-id="9b53f-235">L'intervallo può quindi essere usato all'interno dei caratteri `[` e `]`:</span><span class="sxs-lookup"><span data-stu-id="9b53f-235">The range can then be used inside the `[` and `]` characters:</span></span>

```csharp
var text = words[phrase];
```