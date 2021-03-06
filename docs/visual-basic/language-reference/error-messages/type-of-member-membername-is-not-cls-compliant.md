---
title: Il tipo di membro '<membername>' non è conforme a CLS
ms.date: 07/20/2015
f1_keywords:
- bc40025
- vbc40025
helpviewer_keywords:
- BC40025
ms.assetid: adbd34bb-43d2-4266-90e7-cd1afaf49b4e
ms.openlocfilehash: f6f66617774dccff4450cce42904126acf5c3769
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590679"
---
# <a name="type-of-member-membername-is-not-cls-compliant"></a>Tipo di membro '\<nomeMembro >' non è conforme a CLS
Il tipo di dati specificato per questo membro non è in parte i [Language Independence and Language-Independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS). Ciò non è un errore all'interno del componente, perché .NET Framework e Visual Basic supporta questo tipo di dati. Tuttavia, un altro componente scritto in codice strettamente conforme a CLS potrebbe non supportare questo tipo di dati. Un componente di questo tipo potrebbe non essere in grado di interagire correttamente con il componente.  
  
 I seguenti tipi di dati di Visual Basic non sono conformi a CLS:  
  
- [Tipo di dati SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
- [Tipo di dati UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
- [Tipo di dati ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
- [Tipo di dati UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per altre informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40025  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
- Se il componente interagisce solo con altri componenti di .NET Framework o non si interfaccia con altri componenti, non occorre apportare alcuna modifica.  
  
- Se si prevede l'interazione con un componente non scritto per .NET Framework, potrebbe essere in grado di determinare, tramite la reflection o nella documentazione, se supporta questo tipo di dati. In caso affermativo, non occorre apportare alcuna modifica.  
  
- Se si prevede l'interazione con un componente che non supporta questo tipo di dati, è necessario sostituirlo con il tipo compatibile con CLS più vicino. Al posto di `UInteger` ad esempio può essere possibile usare `Integer` se non è necessario l'intervallo di valore al di sopra di 2.147.483.647. Se è necessario l'intervallo esteso, è possibile sostituire `UInteger` con `Long`.  
  
- Se si prevede l'interazione con oggetti COM o di automazione, tenere presente che alcuni tipi hanno un'ampiezza di dati diversi in .NET Framework. Ad esempio, `uint` è spesso a 16 bit in altri ambienti. Se si passa un argomento a 16 bit a un componente, dichiararlo come `UShort` invece di `UInteger` nel codice gestito di Visual Basic.  
  
## <a name="see-also"></a>Vedere anche

- [Reflection](../../../framework/reflection-and-codedom/reflection.md)
