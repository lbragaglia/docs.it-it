---
title: 'Procedura: Ridurre lo sfarfallio nella grafica con il doppio buffering per form e controlli'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flicker [Windows Forms], reducing in Windows Forms
- graphics [Windows Forms], reducing double-buffered flicker
ms.assetid: 91083d3a-653f-4f15-a467-0f37b2aa39d6
ms.openlocfilehash: d143d7ec87a214a900264e069b329ea28a92c3e9
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590390"
---
# <a name="how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls"></a>Procedura: Ridurre lo sfarfallio nella grafica con il doppio buffering per form e controlli
Il doppio buffer usa un buffer di memoria per risolvere i problemi di sfarfallio associati a più operazioni di disegno. Quando il doppio buffer è abilitato, tutte le operazioni di disegno vengono prima sottoposte a rendering in un buffer di memoria invece che nella superficie di disegno visualizzata. Dopo che tutte le operazioni di disegno sono state completate, il buffer di memoria viene copiato direttamente nella superficie di disegno associata. Poiché sullo schermo viene eseguita una sola operazione, lo sfarfallio dell'immagine associata a operazioni di disegno complesse viene eliminato. Per la maggior parte delle applicazioni, il doppio buffer predefinito fornito da .NET Framework fornirà risultati ottimali. I controlli standard Windows Forms sono a doppio buffering per impostazione predefinita. È possibile abilitare il doppio buffering nei tuoi moduli predefinito e creati i controlli in due modi. È possibile impostare il <xref:System.Windows.Forms.Control.DoubleBuffered%2A> proprietà `true`, oppure è possibile chiamare il <xref:System.Windows.Forms.Control.SetStyle%2A> per impostare il <xref:System.Windows.Forms.ControlStyles.OptimizedDoubleBuffer> flag `true`. Entrambi i metodi verranno attivato predefinito doppio buffering per il form o il controllo e fornire rendering della grafica di sfarfallio. La chiamata di <xref:System.Windows.Forms.Control.SetStyle%2A> metodo è consigliato solo per i controlli personalizzati per cui è stato scritto tutto il codice per il rendering.  
  
 Per scenari di memorizzazione nel buffer più avanzati, ad esempio l'animazione o gestione avanzata della memoria, è possibile implementare la propria logica di buffering doppio. Per altre informazioni, vedere [Procedura: Gestire manualmente le immagini memorizzate nel buffer](how-to-manually-manage-buffered-graphics.md).  
  
### <a name="to-reduce-flicker"></a>Per ridurre lo sfarfallio  
  
- Impostare la proprietà <xref:System.Windows.Forms.Control.DoubleBuffered%2A> su `true`.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#31)]  
  
 \- oppure -  
  
- Chiamare il <xref:System.Windows.Forms.Control.SetStyle%2A> per impostare il <xref:System.Windows.Forms.ControlStyles.OptimizedDoubleBuffer> flag `true`.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#32](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#32)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#32](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#32)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Forms.Control.DoubleBuffered%2A>
- <xref:System.Windows.Forms.Control.SetStyle%2A>
- [Grafica a doppio buffer](double-buffered-graphics.md)
- [Grafica e disegno in Windows Form](graphics-and-drawing-in-windows-forms.md)
