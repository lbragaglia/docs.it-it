---
title: 'Procedura: Nascondere ToolStripMenuItems'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- ToolStripMenuItems [Windows Forms], hiding
- MenuStrip control [Windows Forms], hiding menu items
- menus [Windows Forms], hiding menu items
- menu items [Windows Forms], hiding
- hiding menu items
ms.assetid: 418a768f-808a-44cd-8cef-f4e161883621
ms.openlocfilehash: 64c0f093063357c1e8db5933c035cc8295ad4f1e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623045"
---
# <a name="how-to-hide-toolstripmenuitems"></a>Procedura: Nascondere ToolStripMenuItems
Se si nasconde le voci di menu è un modo per controllare l'interfaccia utente dell'applicazione e limitare i comandi dell'utente. Spesso, è consigliabile nascondere un intero menu quando tutte le voci di menu su di esso non sono disponibili. Evitare distrazioni per l'utente. Inoltre, si potrebbe voler nascondere e disabilitare il menu o la voce di menu, come nascondere da solo non impedisce all'utente di accesso a un comando di menu tramite un tasto di scelta rapida.  
  
### <a name="to-hide-any-menu-item-programmatically"></a>Per nascondere qualsiasi voce di menu a livello di codice  
  
- All'interno del metodo in cui si impostano le proprietà della voce di menu, aggiungere il codice per impostare il <xref:System.Windows.Forms.ToolStripItem.Visible%2A> proprietà `false`.  
  
    ```vb  
    MenuItem3.Visible = False  
    ```  
  
    ```csharp  
    menuItem3.Visible = false;  
    ```  
  
    ```cpp  
    menuItem3->Visible = false;  
    ```  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Forms.ToolStripItem.Visible%2A>
- <xref:System.Windows.Forms.MenuStrip>
- [Panoramica sul controllo MenuStrip](menustrip-control-overview-windows-forms.md)
- [Procedura: Disabilitare i ToolStripMenuItems](how-to-disable-toolstripmenuitems.md)
