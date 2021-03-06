---
title: Cenni preliminari sul componente PrintDialog (Windows Form)
ms.date: 03/30/2017
f1_keywords:
- PrintDialog
helpviewer_keywords:
- Print dialog box [Windows Forms], displaying
- PrintDialog component [Windows Forms], about PrintDialog component
ms.assetid: 8327b8ac-1017-4b5e-a88b-fea9dd56999c
ms.openlocfilehash: 2478990e3cec00df9a748dbd9875485e5f060ed7
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211749"
---
# <a name="printdialog-component-overview-windows-forms"></a>Cenni preliminari sul componente PrintDialog (Windows Form)

I moduli di Windows [PrintDialog](printdialog-component-windows-forms.md) componente è una finestra di dialogo preconfigurata che consente di selezionare una stampante, scegliere le pagine da stampare e indicare altre impostazioni relative alla stampa nelle applicazioni basate su Windows. Questo componente può essere usato come semplice soluzione per la selezione della stampante e delle impostazioni relative alla stampa anziché configurare una propria finestra di dialogo. È possibile abilitare gli utenti di stampare diverse parti dei documenti: stampare tutte, stampare un intervallo di pagine selezionato o una selezione. Basandosi sulle finestre di dialogo standard di Windows è quindi possibile creare applicazioni le cui funzionalità di base sono immediatamente familiari agli utenti. Il <xref:System.Windows.Forms.PrintDialog> componente eredita dal <xref:System.Windows.Forms.CommonDialog> classe.

## <a name="working-with-the-component"></a>Utilizzo del componente

Usare il <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> metodo per visualizzare la finestra di dialogo in fase di esecuzione. Il componente include proprietà relative a un singolo processo di stampa (<xref:System.Drawing.Printing.PrintDocument> classe) o le impostazioni di una singola stampante (<xref:System.Drawing.Printing.PrinterSettings> classe). Uno di questi elementi, a sua volta, potrebbe essere condivisa da più stampanti.

Quando viene aggiunto a un modulo, il <xref:System.Windows.Forms.PrintDialog> componente è visualizzato nella barra delle applicazioni nella parte inferiore della finestra di progettazione Windows Form in Visual Studio.

## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Forms.PrintDialog>
- [Componente PrintDialog](printdialog-component-windows-forms.md)
