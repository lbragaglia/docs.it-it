---
title: -bugreport
ms.date: 03/08/2018
helpviewer_keywords:
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
ms.openlocfilehash: 46d726332806f7d1f6e80dd7df31867051276b45
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002355"
---
# <a name="-bugreport"></a>-bugreport
Consente di creare un file che è possibile utilizzare per il file di un report sui bug.  
  
## <a name="syntax"></a>Sintassi  
  
```  
-bugreport:file  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Nome|Definizione|  
|---|---|  
|`file`|Obbligatorio. Nome del file che conterrà il report sui bug. Racchiudere il nome file tra virgolette ("") se il nome contiene uno spazio.|  
  
## <a name="remarks"></a>Note  
 Le informazioni seguenti sono state aggiunte a `file`:  
  
- Copia di tutti i file del codice sorgente nella compilazione.  
  
- Elenco delle opzioni del compilatore utilizzate nella compilazione.  
  
- Informazioni sulla versione del compilatore, della Common Language Runtime e del sistema operativo.  
  
- L'eventuale output del compilatore.  
  
- Una descrizione del problema, per cui viene richiesto.  
  
- Una descrizione del modo in cui si ritiene che il problema venga risolto, per cui viene richiesto.  
  
 Poiché una copia di tutti i file di codice sorgente è inclusa in `file`, potrebbe essere necessario riprodurre l'errore del codice (sospetto) nel programma più breve possibile.  
  
> [!IMPORTANT]
> L'opzione `-bugreport` produce un file che contiene informazioni potenzialmente riservate. Sono inclusi l'ora corrente, la versione del compilatore, la versione .NET Framework, la versione del sistema operativo, il nome utente, gli argomenti della riga di comando con cui è stato eseguito il compilatore, tutto il codice sorgente e il formato binario di qualsiasi assembly a cui si fa riferimento. Per accedere a questa opzione, è possibile specificare le opzioni della riga di comando nel file Web. config per una compilazione lato server di un'applicazione ASP.NET. Per evitare questo problema, modificare il file Machine. config per non consentire agli utenti di eseguire la compilazione nel server.  
  
 Se questa opzione viene usata con `-errorreport:prompt`, `-errorreport:queue` o `-errorreport:send` e l'applicazione rileva un errore interno del compilatore, le informazioni contenute in `file` vengono inviate a Microsoft Corporation. Tali informazioni consentiranno ai tecnici Microsoft di identificare la ragione dell'errore e contribuire a migliorare la prossima versione di Visual Basic. Per impostazione predefinita, nessuna informazione viene inviata a Microsoft. Tuttavia, quando si compila un'applicazione utilizzando `-errorreport:queue`, che è abilitata per impostazione predefinita, l'applicazione raccoglie i report degli errori. Quindi, quando l'amministratore del computer accede, il sistema di segnalazione degli errori Visualizza una finestra popup che consente all'amministratore di trasmettere a Microsoft eventuali segnalazioni di errore che si sono verificate dopo l'accesso.  
  
> [!NOTE]
> L'opzione `/bugreport` non è disponibile nell'ambiente di sviluppo di Visual Studio. è disponibile solo quando si esegue la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene compilato `T2.vb` e tutte le informazioni di segnalazione dei bug vengono inserite nel file `Problem.txt`.  
  
```console  
vbc -bugreport:problem.txt t2.vb  
```  
  
## <a name="see-also"></a>Vedere anche

- [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [-debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)
- [-errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)
- [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Elemento trustLevel per securityPolicy (schema delle impostazioni ASP.NET)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as399f0x(v=vs.100))
