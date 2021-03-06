---
title: Espressioni incorporate in XML (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlEmbeddedExpression
helpviewer_keywords:
- embedded expressions [Visual Basic]
- LINQ to XML [Visual Basic], embedded expressions
- XML literals [Visual Basic], embedded expressions
ms.assetid: bf2eb779-b751-4b7c-854f-9f2161482352
ms.openlocfilehash: 525fa04db86a299d88e1612aac76d014f35124eb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922626"
---
# <a name="embedded-expressions-in-xml-visual-basic"></a>Espressioni incorporate in XML (Visual Basic)
Le espressioni incorporate consentono di creare valori letterali XML contenenti espressioni che vengono valutate in fase di esecuzione. La sintassi per un'espressione incorporata `<%=` è `expression` `%>`, che corrisponde alla sintassi utilizzata in ASP.NET.  
  
 È ad esempio possibile creare un valore letterale elemento XML, combinando espressioni incorporate con contenuto di testo letterale.  
  
 [!code-vb[VbXMLSamples#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#27)]  
  
 Se `isbnNumber` contiene l'intero 12345 e `modifiedDate` contiene la data 3/5/2006, quando viene eseguito questo codice, il valore di `book` è:  
  
```xml  
<book category="fiction" isbn="12345">  
  <modifiedDate>3/5/2006</modifiedDate>  
</book>  
```  
  
## <a name="embedded-expression-location-and-validation"></a>Posizione e convalida dell'espressione incorporata  
 Le espressioni incorporate possono essere visualizzate solo in determinate posizioni all'interno di espressioni letterali XML. Il percorso dell'espressione controlla i tipi che l'espressione può restituire `Nothing` e il modo in cui viene gestito. Nella tabella seguente vengono descritti i percorsi e i tipi di espressioni incorporate consentiti.  
  
|Posizione nel valore letterale|Tipo di espressione|Gestione di`Nothing`|  
|---|---|---|  
|Nome elemento XML|<xref:System.Xml.Linq.XName>|Errore|  
|Contenuto elemento XML|`Object`o matrice di`Object`|Ignorato|  
|Nome attributo elemento XML|<xref:System.Xml.Linq.XName>|Errore, a meno che anche il valore dell'attributo non sia`Nothing`|  
|Valore dell'attributo dell'elemento XML|`Object`|Dichiarazione di attributo ignorata|  
|Attributo elemento XML|<xref:System.Xml.Linq.XAttribute>o una raccolta di<xref:System.Xml.Linq.XAttribute>|Ignorato|  
|Elemento radice del documento XML|<xref:System.Xml.Linq.XElement>o una raccolta di <xref:System.Xml.Linq.XElement> un oggetto e un numero arbitrario di <xref:System.Xml.Linq.XProcessingInstruction> oggetti e <xref:System.Xml.Linq.XComment>|Ignorato|  
  
- Esempio di espressione incorporata in un nome di elemento XML:  
  
     [!code-vb[VbXMLSamples#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#32)]  
  
- Esempio di espressione incorporata nel contenuto di un elemento XML:  
  
     [!code-vb[VbXMLSamples#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#33)]  
  
- Esempio di espressione incorporata in un nome di attributo dell'elemento XML:  
  
     [!code-vb[VbXMLSamples#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#34)]  
  
- Esempio di espressione incorporata in un valore di attributo dell'elemento XML:  
  
     [!code-vb[VbXMLSamples#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#35)]  
  
- Esempio di espressione incorporata in un attributo dell'elemento XML:  
  
     [!code-vb[VbXMLSamples#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#36)]  
  
- Esempio di espressione incorporata in un elemento radice di un documento XML:  
  
     [!code-vb[VbXMLSamples#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#37)]  
  
 Se si abilita `Option Strict`, il compilatore verifica che il tipo di ogni espressione incorporata venga ampliato al tipo richiesto. L'unica eccezione riguarda l'elemento radice di un documento XML, che viene verificato quando viene eseguito il codice. Se si compila senza `Option Strict`, è possibile incorporare espressioni di `Object` tipo e il relativo tipo viene verificato in fase di esecuzione.  
  
 Nelle posizioni in cui il contenuto è facoltativo, le espressioni `Nothing` incorporate che contengono vengono ignorate. Ciò significa che non è necessario verificare che il contenuto dell'elemento, i valori di attributo e gli elementi `Nothing` della matrice non siano prima di usare un valore letterale XML. I valori obbligatori, ad esempio i nomi degli elementi e `Nothing`degli attributi, non possono essere.  
  
 Per ulteriori informazioni sull'utilizzo di un'espressione incorporata in un particolare tipo di valore letterale, vedere valore letterale [documento XML](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md), [valore letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).  
  
## <a name="scoping-rules"></a>Regole di ambito  
 Il compilatore converte ogni valore letterale XML in una chiamata del costruttore per il tipo di valore letterale appropriato. Il contenuto letterale e le espressioni incorporate in un valore letterale XML vengono passati come argomenti al costruttore. Ciò significa che tutte le Visual Basic gli elementi di programmazione disponibili per un valore letterale XML sono disponibili anche per le espressioni incorporate.  
  
 All'interno di un valore letterale XML è possibile accedere ai prefissi degli spazi `Imports` dei nomi XML dichiarati con l'istruzione. È possibile dichiarare un nuovo prefisso dello spazio dei nomi XML o ombreggiare un prefisso dello spazio dei nomi XML esistente in `xmlns` un elemento usando l'attributo. Il nuovo spazio dei nomi è disponibile per i nodi figlio dell'elemento, ma non per i valori letterali XML nelle espressioni incorporate.  
  
> [!NOTE]
> Quando si dichiara un prefisso dello spazio dei nomi XML `xmlns` usando l'attributo Namespace, il valore dell'attributo deve essere una stringa costante. In questo senso, l'utilizzo `xmlns` dell'attributo è simile all' `Imports` utilizzo dell'istruzione per dichiarare uno spazio dei nomi XML. Non è possibile usare un'espressione incorporata per specificare il valore dello spazio dei nomi XML.  
  
## <a name="see-also"></a>Vedere anche

- [Creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Valore letterale di documento XML](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)
- [Valore letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
- [Istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [Cenni preliminari sui valori letterali XML](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md)
