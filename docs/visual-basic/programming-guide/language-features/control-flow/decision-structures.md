---
title: Strutture decisionali (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- statements [Visual Basic], control flow
- If statement [Visual Basic], decision structures
- If statement [Visual Basic], If...Then...Else
- control flow [Visual Basic], decision structures
- decision structures [Visual Basic]
- conditional statements [Visual Basic], decision structures
ms.assetid: 2e2e0895-4483-442a-b17c-26aead751ec2
ms.openlocfilehash: f0df649c4be50e9cadd51258c89137b68b4ffe22
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963195"
---
# <a name="decision-structures-visual-basic"></a>Strutture decisionali (Visual Basic)
Visual Basic consente di verificare le condizioni ed eseguire diverse operazioni in base ai risultati del test. È possibile verificare se una condizione è true o false, per i diversi valori di un'espressione o per varie eccezioni generate quando si esegue una serie di istruzioni.  
  
 Nella figura seguente viene illustrata una struttura decisionale che verifica la presenza di una condizione true e che esegue azioni diverse a seconda che sia true o false.  
  
 ![Un diagramma di flusso di un If...Then...Else costruzione.](./media/decision-structures/if-then-else-construction.gif)  
  
## <a name="ifthenelse-construction"></a>If...Then...Else costruzione  
 `If...Then...Else`le costruzioni consentono di testare una o più condizioni ed eseguire una o più istruzioni a seconda di ogni condizione. È possibile verificare le condizioni e intraprendere azioni nei modi seguenti:  
  
- Eseguire una o più istruzioni se una condizione è`True`  
  
- Eseguire una o più istruzioni se una condizione è`False`  
  
- Eseguire alcune istruzioni se una condizione è `True` e altre se è`False`  
  
- Testare una condizione aggiuntiva se una condizione precedente è`False`  
  
 La struttura di controllo che offre tutte queste possibilità è il [If...Then...Else istruzione](../../../../visual-basic/language-reference/statements/if-then-else-statement.md). È possibile utilizzare una versione a riga singola se si dispone solo di un test e di un'istruzione da eseguire. Se si dispone di un set più complesso di condizioni e azioni, è possibile usare la versione a più righe.  
  
## <a name="selectcase-construction"></a>Select...Case costruzione  
 La `Select...Case` costruzione consente di valutare un'espressione una sola volta ed eseguire set di istruzioni diversi in base a valori possibili differenti. Per ulteriori informazioni, vedere [Istruzione Select...Case](../../../../visual-basic/language-reference/statements/select-case-statement.md).  
  
## <a name="trycatchfinally-construction"></a>Try...Catch...Finally Costruzione  
 `Try...Catch...Finally`le costruzioni consentono di eseguire un set di istruzioni in un ambiente che mantiene il controllo se una qualsiasi delle istruzioni causa un'eccezione. È possibile eseguire azioni diverse per le diverse eccezioni. Facoltativamente, è possibile specificare un blocco di codice che viene eseguito prima di uscire `Try...Catch...Finally` dall'intera costruzione, indipendentemente da ciò che si verifica. Per altre informazioni, vedere [Istruzione Try...Catch...Finally](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
> [!NOTE]
> Per molte strutture di controllo, quando si fa clic su una parola chiave, vengono evidenziate tutte le parole chiave nella struttura. Ad esempio, quando si fa `If` clic in `If...Then...Else` una costruzione, vengono evidenziate `Then`tutte `ElseIf`le `Else`istanze di `End If` `If`,,, e nella costruzione. Per passare alla parola chiave evidenziata successiva o precedente, premere CTRL + MAIUSC + freccia giù o CTRL + MAIUSC + freccia su.  
  
## <a name="see-also"></a>Vedere anche

- [Flusso di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)
- [Strutture di ciclo](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)
- [Altre strutture di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)
- [Strutture di controllo annidate](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)
- [Operatore If](../../../../visual-basic/language-reference/operators/if-operator.md)
