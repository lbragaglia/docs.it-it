---
title: 'Procedura: Definire un modello GroupBox'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], GroupBox
- GroupBox control [WPF], creating templates
ms.assetid: 85a4d1a7-4753-4f4a-b26d-14fa10c1ddb5
ms.openlocfilehash: dd53af87ec2d12b2ed0dcf2b23374d76e8f631a9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910520"
---
# <a name="how-to-define-a-groupbox-template"></a>Procedura: Definire un modello GroupBox
Questo esempio viene illustrato come creare un modello per un <xref:System.Windows.Controls.GroupBox> controllo.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente definisce una <xref:System.Windows.Controls.GroupBox> modello di controllo utilizzando un <xref:System.Windows.Controls.Grid> controllo per il layout. Il modello Usa un <xref:System.Windows.Controls.BorderGapMaskConverter> per definire il bordo del <xref:System.Windows.Controls.GroupBox> in modo che non nasconda la <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> contenuto.  
  
 [!code-xaml[GroupBoxSnippet#GroupBoxTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#groupboxtemplate)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Controls.GroupBox>
- [Procedura: Creare un controllo GroupBox](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms748321(v=vs.90))
