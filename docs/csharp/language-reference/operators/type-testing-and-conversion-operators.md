---
title: Operatori di conversione e di test del tipo - Riferimenti per C#
description: Informazioni sugli operatori C# che è possibile usare per controllare il tipo del risultato di un'espressione e, se necessario, convertirlo in un altro tipo.
ms.date: 06/21/2019
author: pkulikov
f1_keywords:
- is_CSharpKeyword
- as_CSharpKeyword
- ()_CSharpKeyword
- typeof_CSharpKeyword
helpviewer_keywords:
- type-testing operators [C#]
- conversion operators [C#]
- type conversion [C#]
- is operator [C#]
- as operator [C#]
- cast operator [C#]
- cast expression [C#]
- () operator [C#]
- typeof operator [C#]
ms.openlocfilehash: 4468bc86634ad97f2dfbdb5f842eb5206f957a79
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/21/2019
ms.locfileid: "67307531"
---
# <a name="type-testing-and-conversion-operators-c-reference"></a><span data-ttu-id="54644-103">Operatori di conversione e di test del tipo (Riferimenti per C#)</span><span class="sxs-lookup"><span data-stu-id="54644-103">Type-testing and conversion operators (C# reference)</span></span>

<span data-ttu-id="54644-104">È possibile usare gli operatori seguenti per eseguire il controllo o la conversione di tipi:</span><span class="sxs-lookup"><span data-stu-id="54644-104">You can use the following operators to perform type checking or type conversion:</span></span>

- <span data-ttu-id="54644-105">[operatore is](#is-operator): per controllare se il tipo di runtime di un'espressione è compatibile con un determinato tipo</span><span class="sxs-lookup"><span data-stu-id="54644-105">[is operator](#is-operator): to check if the runtime type of an expression is compatible with a given type</span></span>
- <span data-ttu-id="54644-106">[operatore as](#as-operator): per convertire in modo esplicito un'espressione in un tipo specificato se il tipo di runtime è compatibile con esso</span><span class="sxs-lookup"><span data-stu-id="54644-106">[as operator](#as-operator): to explicitly convert an expression to a given type if its runtime type is compatible with that type</span></span>
- <span data-ttu-id="54644-107">[operatore cast ()](#cast-operator-): per eseguire una conversione esplicita</span><span class="sxs-lookup"><span data-stu-id="54644-107">[cast operator ()](#cast-operator-): to perform an explicit conversion</span></span>
- <span data-ttu-id="54644-108">[operatore typeof](#typeof-operator): per ottenere l'istanza <xref:System.Type?displayProperty=nameWithType> per un tipo</span><span class="sxs-lookup"><span data-stu-id="54644-108">[typeof operator](#typeof-operator): to obtain the <xref:System.Type?displayProperty=nameWithType> instance for a type</span></span>

## <a name="is-operator"></a><span data-ttu-id="54644-109">Operatore is</span><span class="sxs-lookup"><span data-stu-id="54644-109">is operator</span></span>

<span data-ttu-id="54644-110">L' operatore `is` controlla se il tipo di runtime del risultato di un'espressione è compatibile con un determinato tipo.</span><span class="sxs-lookup"><span data-stu-id="54644-110">The `is` operator checks if the runtime type of an expression result is compatible with a given type.</span></span> <span data-ttu-id="54644-111">A partire da C# 7.0, l'operatore `is` verifica il risultato di un'espressione anche rispetto a un criterio.</span><span class="sxs-lookup"><span data-stu-id="54644-111">Starting with C# 7.0, the `is` operator also tests an expression result against a pattern.</span></span>

<span data-ttu-id="54644-112">L'espressione con l'operatore di test del tipo `is` ha il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="54644-112">The expression with the type-testing `is` operator has the following form</span></span>

```csharp
E is T
```

<span data-ttu-id="54644-113">in cui `E` è un'espressione che restituisce un valore e `T` è il nome di un tipo o un parametro di tipo.</span><span class="sxs-lookup"><span data-stu-id="54644-113">where `E` is an expression that returns a value and `T` is the name of a type or a type parameter.</span></span> <span data-ttu-id="54644-114">`E` non può essere un metodo anonimo o un'espressione lambda.</span><span class="sxs-lookup"><span data-stu-id="54644-114">`E` cannot be an anonymous method or a lambda expression.</span></span>

<span data-ttu-id="54644-115">L'espressione `E is T` restituisce `true` se il risultato di `E` è diverso da null e può essere convertito nel tipo `T` da una conversione di riferimento, una conversione boxing o una conversione unboxing; in caso contrario, restituisce `false`.</span><span class="sxs-lookup"><span data-stu-id="54644-115">The `E is T` expression returns `true` if the result of `E` is non-null and can be converted to type `T` by a reference conversion, a boxing conversion, or an unboxing conversion; otherwise, it returns `false`.</span></span> <span data-ttu-id="54644-116">L'operatore `is` non considera le conversioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="54644-116">The `is` operator doesn't consider user-defined conversions.</span></span>

<span data-ttu-id="54644-117">L'esempio seguente dimostra che l'operatore `is` restituisce `true` se il tipo di runtime del risultato di un'espressione deriva da un determinato tipo, ovvero se esiste una conversione di riferimento tra i tipi:</span><span class="sxs-lookup"><span data-stu-id="54644-117">The following example demonstrates that the `is` operator returns `true` if the runtime type of an expression result derives from a given type, that is, there exists a reference conversion between types:</span></span>

[!code-csharp[is with reference conversion](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#IsWithReferenceConversion)]

<span data-ttu-id="54644-118">L'esempio successivo mostra che l'operatore `is` prende in considerazione le conversioni boxing e unboxing ma non le conversioni numeriche:</span><span class="sxs-lookup"><span data-stu-id="54644-118">The next example shows that the `is` operator takes into account boxing and unboxing conversions but doesn't consider numeric conversions:</span></span>

[!code-csharp-interactive[is with int](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#IsWithInt)]

<span data-ttu-id="54644-119">Per informazioni sulle conversioni C#, vedere il capito [Conversioni](~/_csharplang/spec/conversions.md) della [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54644-119">For information about C# conversions, see the [Conversions](~/_csharplang/spec/conversions.md) chapter of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

### <a name="type-testing-with-pattern-matching"></a><span data-ttu-id="54644-120">Test del tipo con criteri di ricerca</span><span class="sxs-lookup"><span data-stu-id="54644-120">Type testing with pattern matching</span></span>

<span data-ttu-id="54644-121">A partire da C# 7.0, l'operatore `is` verifica il risultato di un'espressione anche rispetto a un criterio.</span><span class="sxs-lookup"><span data-stu-id="54644-121">Starting with C# 7.0, the `is` operator also tests an expression result against a pattern.</span></span> <span data-ttu-id="54644-122">In particolare, supporta il criterio del tipo nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="54644-122">In particular, it supports the type pattern in the following form:</span></span>

```csharp
E is T v
```

<span data-ttu-id="54644-123">in cui `E` è un'espressione che restituisce un valore, `T` è il nome di un tipo o un parametro di tipo e `v` è una nuova variabile locale di tipo `T`.</span><span class="sxs-lookup"><span data-stu-id="54644-123">where `E` is an expression that returns a value, `T` is the name of a type or a type parameter, and `v` is a new local variable of type `T`.</span></span> <span data-ttu-id="54644-124">Se il risultato di `E` è diverso da null e può essere convertito in `T` con una conversione di riferimento, boxing o unboxing, l'espressione `E is T v` restituisce `true` e il valore convertito del risultato di `E` viene assegnato alla variabile `v`.</span><span class="sxs-lookup"><span data-stu-id="54644-124">If the result of `E` is non-null and can be converted to `T` by a reference, boxing, or unboxing conversion, the `E is T v` expression returns `true` and the converted value of the result of `E` is assigned to variable `v`.</span></span>

<span data-ttu-id="54644-125">L'esempio seguente illustra l'uso dell'operatore `is` con un criterio del tipo:</span><span class="sxs-lookup"><span data-stu-id="54644-125">The following example demonstrates the usage of the `is` operator with the type pattern:</span></span>

[!code-csharp-interactive[is with type pattern](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#IsTypePattern)]

<span data-ttu-id="54644-126">Per altre informazioni sul criterio del tipo e sugli altri criteri supportati, vedere [Criteri di ricerca con is](../keywords/is.md#pattern-matching-with-is).</span><span class="sxs-lookup"><span data-stu-id="54644-126">For more information about the type pattern and other supported patterns, see [Pattern matching with is](../keywords/is.md#pattern-matching-with-is).</span></span>

## <a name="as-operator"></a><span data-ttu-id="54644-127">operatore as</span><span class="sxs-lookup"><span data-stu-id="54644-127">as operator</span></span>

<span data-ttu-id="54644-128">L'operatore `as` converte in modo esplicito il risultato di un'espressione in un tipo di valore nullable o di riferimento specificato.</span><span class="sxs-lookup"><span data-stu-id="54644-128">The `as` operator explicitly converts the result of an expression to a given reference or nullable value type.</span></span> <span data-ttu-id="54644-129">Se la conversione non è possibile, l'operatore `as` restituisce `null`.</span><span class="sxs-lookup"><span data-stu-id="54644-129">If the conversion is not possible, the `as` operator returns `null`.</span></span> <span data-ttu-id="54644-130">A differenza dell'[operatore cast ()](#cast-operator-), l'operatore `as` non genera mai un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="54644-130">Unlike the [cast operator ()](#cast-operator-), the `as` operator never throws an exception.</span></span>

<span data-ttu-id="54644-131">Un'espressione nel formato</span><span class="sxs-lookup"><span data-stu-id="54644-131">The expression of the form</span></span>

```csharp
E as T
```

<span data-ttu-id="54644-132">in cui `E` è un'espressione che restituisce un valore e `T` è il nome di un tipo o un parametro di tipo, produce lo stesso risultato di</span><span class="sxs-lookup"><span data-stu-id="54644-132">where `E` is an expression that returns a value and `T` is the name of a type or a type parameter, produces the same result as</span></span>

```csharp
E is T ? (T)(E) : (T)null
```

<span data-ttu-id="54644-133">con la differenza che `E` viene valutato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="54644-133">except that `E` is only evaluated once.</span></span>

<span data-ttu-id="54644-134">L'operatore `as` considera solo conversioni di riferimenti, nullable, boxing e unboxing.</span><span class="sxs-lookup"><span data-stu-id="54644-134">The `as` operator considers only reference, nullable, boxing, and unboxing conversions.</span></span> <span data-ttu-id="54644-135">Non è possibile usare l'operatore `as` per eseguire una conversione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="54644-135">You cannot use the `as` operator to perform a user-defined conversion.</span></span> <span data-ttu-id="54644-136">A questo scopo, usare l'[operatore cast()](#cast-operator-).</span><span class="sxs-lookup"><span data-stu-id="54644-136">To do that, use the [cast operator ()](#cast-operator-).</span></span>

<span data-ttu-id="54644-137">Nell'esempio seguente viene illustrato l'uso dell'operatore `as`:</span><span class="sxs-lookup"><span data-stu-id="54644-137">The following example demonstrates the usage of the `as` operator:</span></span>

[!code-csharp-interactive[as operator](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#AsOperator)]

> [!NOTE]
> <span data-ttu-id="54644-138">Come mostrato nell'esempio precedente, è necessario confrontare il risultato dell'espressione `as` con `null` per verificare se la conversione riesce.</span><span class="sxs-lookup"><span data-stu-id="54644-138">As the preceding example shows, you need to compare the result of the `as` expression with `null` to check if the conversion is successful.</span></span> <span data-ttu-id="54644-139">A partire da C# 7.0, è possibile usare l'[operatore is](#type-testing-with-pattern-matching) sia per verificare se la conversione riesce sia, in caso di esito positivo, per assegnare il risultato a una nuova variabile.</span><span class="sxs-lookup"><span data-stu-id="54644-139">Starting with C# 7.0, you can use the [is operator](#type-testing-with-pattern-matching) both to test if the conversion succeeds and, if it succeeds, assign its result to a new variable.</span></span>

## <a name="cast-operator-"></a><span data-ttu-id="54644-140">Operatore cast ()</span><span class="sxs-lookup"><span data-stu-id="54644-140">Cast operator ()</span></span>

<span data-ttu-id="54644-141">Un'espressione cast nel formato `(T)E` esegue una conversione esplicita del risultato dell'espressione `E` nel tipo `T`.</span><span class="sxs-lookup"><span data-stu-id="54644-141">A cast expression of the form `(T)E` performs an explicit conversion of the result of expression `E` to type `T`.</span></span> <span data-ttu-id="54644-142">Se non esiste alcuna conversione esplicita dal tipo `E` al tipo `T`, si verifica un errore in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="54644-142">If no explicit conversion exists from the type of `E` to type `T`, a compile-time error occurs.</span></span> <span data-ttu-id="54644-143">In fase di esecuzione, è possibile che una conversione esplicita non riesca e che un'espressione cast generi un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="54644-143">At run time, an explicit conversion might not succeed and a cast expression might throw an exception.</span></span>

<span data-ttu-id="54644-144">L'esempio seguente illustra conversioni esplicite numeriche e di riferimento:</span><span class="sxs-lookup"><span data-stu-id="54644-144">The following example demonstrates explicit numeric and reference conversions:</span></span>

[!code-csharp-interactive[cast expression](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#Cast)]

<span data-ttu-id="54644-145">Per informazioni sulle conversioni esplicite supportate, vedere la sezione [Conversioni esplicite](~/_csharplang/spec/conversions.md#explicit-conversions) della [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54644-145">For information about supported explicit conversions, see the [Explicit conversions](~/_csharplang/spec/conversions.md#explicit-conversions) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span> <span data-ttu-id="54644-146">Per informazioni su come definire una conversione personalizzata di tipo esplicito o implicito, vedere gli articoli sulle parole chiave [explicit](../keywords/explicit.md) e [implicit](../keywords/implicit.md).</span><span class="sxs-lookup"><span data-stu-id="54644-146">For information about how to define a custom explicit or implicit type conversion, see the [explicit](../keywords/explicit.md) or [implicit](../keywords/implicit.md) keyword article, respectively.</span></span>

### <a name="other-usages-of-"></a><span data-ttu-id="54644-147">Altri utilizzi di ()</span><span class="sxs-lookup"><span data-stu-id="54644-147">Other usages of ()</span></span>

<span data-ttu-id="54644-148">È possibile usare le parentesi anche per [chiamare un metodo oppure richiamare un delegato](member-access-operators.md#invocation-operator-).</span><span class="sxs-lookup"><span data-stu-id="54644-148">You also use parentheses to [call a method or invoke a delegate](member-access-operators.md#invocation-operator-).</span></span>

<span data-ttu-id="54644-149">Le parentesi possono essere usate anche per specificare l'ordine in cui valutare le operazioni in un'espressione.</span><span class="sxs-lookup"><span data-stu-id="54644-149">Other use of parentheses is to specify the order in which to evaluate operations in an expression.</span></span> <span data-ttu-id="54644-150">Per altre informazioni, vedere la sezione [Aggiunta di parentesi](../../programming-guide/statements-expressions-operators/operators.md#adding-parentheses) dell'articolo [Operatori](../../programming-guide/statements-expressions-operators/operators.md).</span><span class="sxs-lookup"><span data-stu-id="54644-150">For more information, see the [Adding parentheses](../../programming-guide/statements-expressions-operators/operators.md#adding-parentheses) section of the [Operators](../../programming-guide/statements-expressions-operators/operators.md) article.</span></span> <span data-ttu-id="54644-151">Per l'elenco degli operatori ordinati in base al livello di precedenza, vedere [ Operatori C#](index.md).</span><span class="sxs-lookup"><span data-stu-id="54644-151">For the list of operators ordered by precedence level, see [C# operators](index.md).</span></span>

## <a name="typeof-operator"></a><span data-ttu-id="54644-152">Operatore typeof</span><span class="sxs-lookup"><span data-stu-id="54644-152">typeof operator</span></span>

<span data-ttu-id="54644-153">L'operatore `typeof` ottiene l'istanza <xref:System.Type?displayProperty=nameWithType> per un tipo.</span><span class="sxs-lookup"><span data-stu-id="54644-153">The `typeof` operator obtains the <xref:System.Type?displayProperty=nameWithType> instance for a type.</span></span> <span data-ttu-id="54644-154">Un argomento dell'operatore `typeof` deve essere il nome o il parametro di un tipo, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="54644-154">An argument of the `typeof` operator must be the name of a type or a type parameter, as the following example shows:</span></span>

[!code-csharp-interactive[typeof operator](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#TypeOf)]

<span data-ttu-id="54644-155">È possibile usare l'operatore `typeof` anche con tipi generici non associati.</span><span class="sxs-lookup"><span data-stu-id="54644-155">You also can use the `typeof` operator with unbound generic types.</span></span> <span data-ttu-id="54644-156">Il nome di un tipo generico non associato deve contenere il numero appropriato di virgole, ovvero una in meno rispetto al numero di parametri del tipo.</span><span class="sxs-lookup"><span data-stu-id="54644-156">The name of an unbound generic type must contain the appropriate number of commas, which is one less than the number of type parameters.</span></span> <span data-ttu-id="54644-157">L'esempio seguente illustra l'uso dell'operatore `typeof` con un tipo generico non associato:</span><span class="sxs-lookup"><span data-stu-id="54644-157">The following example shows the usage of the `typeof` operator with an unbound generic type:</span></span>

[!code-csharp-interactive[typeof unbound generic](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#TypeOfUnboundGeneric)]

<span data-ttu-id="54644-158">Un'espressione non può essere un argomento dell'operatore `typeof`.</span><span class="sxs-lookup"><span data-stu-id="54644-158">An expression cannot be an argument of the `typeof` operator.</span></span> <span data-ttu-id="54644-159">Per ottenere l'istanza <xref:System.Type?displayProperty=nameWithType> per il tipo di runtime del risultato dell'espressione, usare il metodo <xref:System.Object.GetType%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="54644-159">To get the <xref:System.Type?displayProperty=nameWithType> instance for the runtime type of the expression result, use the <xref:System.Object.GetType%2A?displayProperty=nameWithType> method.</span></span>

### <a name="type-testing-with-the-typeof-operator"></a><span data-ttu-id="54644-160">Test del tipo con l'operatore `typeof`</span><span class="sxs-lookup"><span data-stu-id="54644-160">Type testing with the `typeof` operator</span></span>

<span data-ttu-id="54644-161">Usare l'operatore `typeof` per controllare se il tipo di runtime del risultato dell'espressione corrisponde esattamente a un determinato tipo.</span><span class="sxs-lookup"><span data-stu-id="54644-161">Use the `typeof` operator to check if the runtime type of the expression result exactly matches a given type.</span></span> <span data-ttu-id="54644-162">L'esempio seguente illustra la differenza tra il controllo del tipo eseguito con l'operatore `typeof` e il controllo del tipo con l'[operatore is](#is-operator):</span><span class="sxs-lookup"><span data-stu-id="54644-162">The following example demonstrates the difference between type checking performed with the `typeof` operator and the [is operator](#is-operator):</span></span>

[!code-csharp[typeof vs is](~/samples/csharp/language-reference/operators/TypeTestingAndConversionOperators.cs#TypeCheckWithTypeOf)]

## <a name="operator-overloadability"></a><span data-ttu-id="54644-163">Overload degli operatori</span><span class="sxs-lookup"><span data-stu-id="54644-163">Operator overloadability</span></span>

<span data-ttu-id="54644-164">Gli operatori `is`, `as` e `typeof` non supportano l'overload.</span><span class="sxs-lookup"><span data-stu-id="54644-164">The `is`, `as`, and `typeof` operators are not overloadable.</span></span>

<span data-ttu-id="54644-165">Un tipo definito dall'utente non può eseguire l'overload dell'operatore `()`, ma può definire conversioni di tipi personalizzate che possano essere eseguite da un'espressione cast.</span><span class="sxs-lookup"><span data-stu-id="54644-165">A user-defined type cannot overload the `()` operator, but can define custom type conversions that can be performed by a cast expression.</span></span> <span data-ttu-id="54644-166">Per altre informazioni, vedere gli articoli sulle parole chiave [explicit](../keywords/explicit.md) e [implicit](../keywords/implicit.md).</span><span class="sxs-lookup"><span data-stu-id="54644-166">For more information, see the [explicit](../keywords/explicit.md) and [implicit](../keywords/implicit.md) keyword articles.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="54644-167">Specifiche del linguaggio C#</span><span class="sxs-lookup"><span data-stu-id="54644-167">C# language specification</span></span>

<span data-ttu-id="54644-168">Per altre informazioni, vedere le sezioni seguenti delle [specifiche del linguaggio C#](~/_csharplang/spec/introduction.md):</span><span class="sxs-lookup"><span data-stu-id="54644-168">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="54644-169">Operatore is</span><span class="sxs-lookup"><span data-stu-id="54644-169">The is operator</span></span>](~/_csharplang/spec/expressions.md#the-is-operator)
- [<span data-ttu-id="54644-170">Operatore as</span><span class="sxs-lookup"><span data-stu-id="54644-170">The as operator</span></span>](~/_csharplang/spec/expressions.md#the-as-operator)
- [<span data-ttu-id="54644-171">Espressioni cast</span><span class="sxs-lookup"><span data-stu-id="54644-171">Cast expressions</span></span>](~/_csharplang/spec/expressions.md#cast-expressions)
- [<span data-ttu-id="54644-172">Operatore typeof</span><span class="sxs-lookup"><span data-stu-id="54644-172">The typeof operator</span></span>](~/_csharplang/spec/expressions.md#the-typeof-operator)

## <a name="see-also"></a><span data-ttu-id="54644-173">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="54644-173">See also</span></span>

- [<span data-ttu-id="54644-174">Riferimenti per C#</span><span class="sxs-lookup"><span data-stu-id="54644-174">C# reference</span></span>](../index.md)
- [<span data-ttu-id="54644-175">Operatori C#</span><span class="sxs-lookup"><span data-stu-id="54644-175">C# operators</span></span>](index.md)
- [<span data-ttu-id="54644-176">Procedura: eseguire il cast sicuro con i criteri di ricerca e gli operatori is e as</span><span class="sxs-lookup"><span data-stu-id="54644-176">How to: safely cast by using pattern matching and the is and as operators</span></span>](../../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md)