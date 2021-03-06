---
title: Utilizzo di controlli WPF
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms Designer [Windows Forms], interoperability with WPF
- interoperability [WPF]
ms.assetid: 03c85dce-26ad-44cd-bc1d-8e0cb56de096
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5ea92b24a2ca30c0ad137d83c8f521a952ad0c6b
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69658493"
---
# <a name="use-wpf-controls-in-windows-forms-apps"></a>Usare i controlli WPF nelle app Windows Forms

È possibile utilizzare i controlli Windows Presentation Foundation (WPF) nelle applicazioni basate su Windows Forms. Sebbene si tratta di due tecnologie di visualizzazione diverse, interagiscono senza problemi.

Il Progettazione Windows Form in Visual Studio fornisce un ambiente di progettazione visiva per l'hosting di controlli Windows Presentation Foundation. Un controllo WPF è ospitato da un particolare controllo Windows Forms denominato <xref:System.Windows.Forms.Integration.ElementHost>. Questo controllo consente al controllo WPF di partecipare al layout del form e di ricevere i messaggi della tastiera e del mouse. In fase di progettazione, è possibile disporre <xref:System.Windows.Forms.Integration.ElementHost> il controllo come qualsiasi Windows Forms controllo.

È inoltre possibile utilizzare Windows Forms controlli nelle applicazioni basate su WPF. Per altre informazioni, vedere [progettazione di XAML in Visual Studio](/visualstudio/designers/designing-xaml-in-visual-studio).

## <a name="see-also"></a>Vedere anche

- [Interoperatività di WPF e Windows Forms](/dotnet/framework/wpf/advanced/wpf-and-windows-forms-interoperation)
