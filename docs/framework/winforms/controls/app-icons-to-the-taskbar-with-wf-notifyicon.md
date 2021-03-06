---
title: 'Procedura: Aggiungere icone delle applicazioni alla barra delle applicazioni con il componente NotifyIcon di Windows Forms'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- TrayIcon
helpviewer_keywords:
- status area icons
- icons [Windows Forms], adding to taskbar
- NotifyIcon component
- taskbar [Windows Forms], adding icons
ms.assetid: d28c0fe6-aaf2-4df7-ad74-928d861a8510
ms.openlocfilehash: 05b6f300afea4671c1a847b116b378514ecb8b56
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959512"
---
# <a name="how-to-add-application-icons-to-the-taskbar-with-the-windows-forms-notifyicon-component"></a>Procedura: Aggiungere icone delle applicazioni alla barra delle applicazioni con il componente NotifyIcon di Windows Forms

I moduli di Windows <xref:System.Windows.Forms.NotifyIcon> componente consente di visualizzare una singola icona nell'area di notifica dello stato della barra delle applicazioni. Per visualizzare le icone più nell'area di stato, è necessario disporre di più <xref:System.Windows.Forms.NotifyIcon> componenti nel form. Per impostare l'icona visualizzata per un controllo, usare il <xref:System.Windows.Forms.NotifyIcon.Icon%2A> proprietà. È anche possibile scrivere codice <xref:System.Windows.Forms.NotifyIcon.DoubleClick> gestore dell'evento in modo che si verifica un evento quando l'utente fa doppio clic sull'icona. Ad esempio, si è stato possibile visualizzare una finestra di dialogo per l'utente debba configurare il processo in background rappresentato dall'icona.

> [!NOTE]
> Il <xref:System.Windows.Forms.NotifyIcon> componente viene usato solo a fini di notifica per avvertire gli utenti che si è verificato un evento o azione o si è verificato un cambiamento dello stato di qualche tipo. Utilizzare i menu, barre degli strumenti e altri elementi dell'interfaccia utente per l'interazione standard con le applicazioni.

### <a name="to-set-the-icon"></a>Per impostare l'icona

1. Assegnare un valore per il <xref:System.Windows.Forms.NotifyIcon.Icon%2A> proprietà. Il valore deve essere di tipo `System.Drawing.Icon` e possono essere caricati da un file con estensione ico. È possibile specificare il file dell'icona nel codice o facendo clic sul pulsante con puntini di sospensione (![The puntini di sospensione nella finestra proprietà di Visual Studio.](./media/visual-studio-ellipsis-button.png)) accanto al <xref:System.Windows.Forms.NotifyIcon.Icon%2A> proprietà nel **proprietà** finestra e quindi selezionare il file nei **aperto** finestra di dialogo visualizzata.

2. Impostare la proprietà <xref:System.Windows.Forms.NotifyIcon.Visible%2A> su `true`.

3. Impostare il <xref:System.Windows.Forms.NotifyIcon.Text%2A> proprietà da una stringa di descrizione appropriata.

     Nell'esempio di codice seguente, il percorso impostato per il percorso dell'icona è il **documenti** cartella. Poiché si può presupporre che la maggior parte dei computer che eseguono il sistema operativo Windows sarà inclusa in questa cartella, viene usato questo percorso. Anche questa scelta consente agli utenti con livelli di accesso di sistema minimi eseguire in modo sicuro l'applicazione. Nell'esempio seguente richiede un modulo con un <xref:System.Windows.Forms.NotifyIcon> controllo già aggiunto. È inoltre necessario un file di icona denominato `Icon.ico`.

    ```vb
    ' You should replace the bold icon in the sample below
    ' with an icon of your own choosing.
    NotifyIcon1.Icon = New _
       System.Drawing.Icon(System.Environment.GetFolderPath _
       (System.Environment.SpecialFolder.Personal) _
       & "\Icon.ico")
    NotifyIcon1.Visible = True
    NotifyIcon1.Text = "Antivirus program"
    ```

    ```csharp
    // You should replace the bold icon in the sample below
    // with an icon of your own choosing.
    // Note the escape character used (@) when specifying the path.
    notifyIcon1.Icon =
       new System.Drawing.Icon (System.Environment.GetFolderPath
       (System.Environment.SpecialFolder.Personal)
       + @"\Icon.ico");
    notifyIcon1.Visible = true;
    notifyIcon1.Text = "Antivirus program";
    ```

    ```cpp
    // You should replace the bold icon in the sample below
    // with an icon of your own choosing.
    notifyIcon1->Icon = gcnew
       System::Drawing::Icon(String::Concat
       (System::Environment::GetFolderPath
       (System::Environment::SpecialFolder::Personal),
       "\\Icon.ico"));
    notifyIcon1->Visible = true;
    notifyIcon1->Text = "Antivirus program";
    ```

## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Forms.NotifyIcon>
- <xref:System.Windows.Forms.NotifyIcon.Icon%2A>
- [Procedura: Associare un Menu di scelta rapida a un componente NotifyIcon di Windows Form](how-to-associate-a-shortcut-menu-with-a-windows-forms-notifyicon-component.md)
- [Componente NotifyIcon](notifyicon-component-windows-forms.md)
- [Panoramica sul componente NotifyIcon](notifyicon-component-overview-windows-forms.md)
