---
title: 'Procedura: Accedere agli elementi figlio XML (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- XML axis [Visual Basic], child
- child axis property [Visual Basic]
- XML child axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: 6689eb36-c471-469f-a82d-099ab8197b25
ms.openlocfilehash: 3c00166e471b7c6d69bd7f6fc3bda87b651d7d46
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64598674"
---
# <a name="how-to-access-xml-child-elements-visual-basic"></a>Procedura: Accedere agli elementi figlio XML (Visual Basic)
In questo esempio viene illustrato come utilizzare un elemento figlio proprietà asse a cui accedere tutti gli elementi figlio XML con un nome specificato in un elemento XML. In particolare, viene utilizzata la <xref:System.Xml.Linq.XElement.Value%2A> proprietà da ottenere il valore del primo elemento nella raccolta che il `name` restituisce proprietà di asse figlio. Il `name` proprietà child axis Ottiene tutti gli elementi figlio denominati `phone` nel `contact` oggetto. Questo esempio Usa anche il `phone` proprietà child axis per accedere a tutti gli elementi figlio denominati `phone` contenuti nel `contact` oggetto.  
  
## <a name="example"></a>Esempio  
 [!code-vb[VbXMLSamples#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples4.vb#10)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
- Un riferimento allo spazio dei nomi <xref:System.Xml.Linq>.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>
- [Proprietà Child Axis XML](../../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)
- [Proprietà Value XML](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)
- [Accesso a XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)
- [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
