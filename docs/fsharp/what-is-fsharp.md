---
title: Cos'è F#
description: Informazioni sul linguaggio di programmazione F# e sulla programmazione di questo tipo. Informazioni sui tipi di dati avanzati, sulle funzioni e sul modo in cui si integrano.
ms.date: 08/03/2018
ms.openlocfilehash: 3cba509f59a8e81e1a0264de7451e9d80304d768
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332727"
---
# <a name="what-is-f"></a>Che cos'è F#

F# è un linguaggio di programmazione funzionale che semplifica la scrittura di codice corretto e mantenibile.

La programmazione in F# comporta principalmente la definizione di tipi e funzioni che vengono automaticamente inferiti e generalizzati. Ciò consente di rimanere concentrati sul dominio del problema e sulla manipolazione dei dati, anziché sui dettagli della programmazione.

```fsharp
open System // Gets access to functionality in System namespace.

// Defines a function that takes a name and produces a greeting.
let getGreeting name =
    sprintf "Hello, %s! Isn't F# great?" name

[<EntryPoint>]
let main args =
    // Defines a list of names
    let names = [ "Don"; "Julia"; "Xi" ]

    // Prints a greeting for each name!
    names
    |> List.map getGreeting
    |> List.iter (fun greeting -> printfn "%s" greeting)

    0
```

F# dispone di numerose funzionalità, tra cui:

* Sintassi leggera
* Immutabile per impostazione predefinita
* Inferenza dei tipi e generalizzazione automatica
* Funzioni di prima classe
* Tipi di dati avanzati
* Pattern matching
* Programmazione asincrona

L'insieme completo delle funzionalità è documentato nella [Guida di riferimento del linguaggio F#](./language-reference/index.md).

## <a name="rich-data-types"></a>Tipi di dati avanzati

I tipi di dati, ad esempio i [record](./language-reference/records.md) e le [unioni discriminate](./language-reference/discriminated-unions.md), consentono di rappresentare dati e domini complessi.

```fsharp
// Group data with Records
type SuccessfulWithdrawal = {
    Amount: decimal
    Balance: decimal
}

type FailedWithdrawal = {
    Amount: decimal
    Balance: decimal
    IsOverdraft: bool
}

// Use discriminated unions to represent data of 1 or more forms
type WithdrawalResult =
    | Success of SuccessfulWithdrawal
    | InsufficientFunds of FailedWithdrawal
    | CardExpired of System.DateTime
    | UndisclosedFailure
```

I record F# e le unioni discriminate sono non null, non modificabili e confrontabili per impostazione predefinita, rendendoli molto facili da utilizzare.

## <a name="enforced-correctness-with-functions-and-pattern-matching"></a>Ottenere la correttezza tramite le funzioni e il pattern matching

Le funzioni F# sono facili da dichiarare e potenti nella pratica. In combinazione con i [criteri di ricerca](./language-reference/pattern-matching.md), consentono di definire un comportamento la cui correttezza viene verificata dal compilatore.

```fsharp
// Returns a WithdrawalResult
let withdrawMoney amount = // Implementation elided

let handleWithdrawal amount =
    let w = withdrawMoney amount

    // The F# compiler enforces accounting for each case!
    match w with
    | Success s -> printfn "Successfully withdrew %f" s.Amount
    | InsufficientFunds f -> printfn "Failed: balance is %f" f.Balance
    | CardExpired d -> printfn "Failed: card expired on %O" d
    | UndisclosedFailure -> printfn "Failed: unknown :("
```

Anche le funzioni F# sono di prima classe, ovvero possono essere passate come parametri e restituite da altre funzioni.

## <a name="functions-to-define-operations-on-objects"></a>Funzioni per definire operazioni sugli oggetti

F# dispone del supporto completo per gli oggetti, che sono tipi di dati utili quando è necessario combinare dati e funzionalità. Le funzioni F# vengono usate per modificare gli oggetti.

```fsharp
type Set<'T when 'T: comparison>(elements: seq<'T>) =
    member s.IsEmpty = // Implementation elided
    member s.Contains (value) =// Implementation elided
    member s.Add (value) = // Implementation elided
    // ...
    // Further Implementation elided
    // ...
    interface IEnumerable<‘T>
    interface IReadOnlyCollection<‘T>

module Set =
    let isEmpty (set: Set<'T>) = set.IsEmpty

    let contains element (set: Set<'T>) = set.Contains(element)

    let add value (set: Set<'T>) = set.Add(value)
```

Anziché scrivere codice orientato a oggetti, in F# spesso si scrive codice che considera gli oggetti semplicemente come un altro tipo di dati modificabili dalle funzioni. Funzionalità come le [interfacce generiche](./language-reference/interfaces.md), le [espressioni di oggetti](./language-reference/object-expressions.md) e l'utilizzo oculato dei [membri](./language-reference/members/index.md) sono comuni nei programmi F# più grandi.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su un insieme più ampio di funzionalità, vedere la [Panoramica di F#](tour.md).
