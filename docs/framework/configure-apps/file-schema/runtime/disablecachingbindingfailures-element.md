---
title: <disableCachingBindingFailures> Elemento
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCachingBindingFailures
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCachingBindingFailures
helpviewer_keywords:
- assemblies [.NET Framework],caching binding failures
- caching assembly binding failures
- <disableCachingBindingFailures> element
- disableCachingBindingFailures element
ms.assetid: bf598873-83b7-48de-8955-00b0504fbad0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d5b45ea4b30677d17e72685b16c19f9192c8c144
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252685"
---
# <a name="disablecachingbindingfailures-element"></a>\<Elemento > disableCachingBindingFailures
Specifica se disabilitare la memorizzazione nella cache degli errori di associazione che si verificano perché l'assembly non è stato trovato da Probe.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> di runtime**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<disableCachingBindingFailures>**  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<disableCachingBindingFailures enabled="0|1"/>  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|enabled|Attributo obbligatorio.<br /><br /> Specifica se disabilitare la memorizzazione nella cache degli errori di associazione che si verificano perché l'assembly non è stato trovato da Probe.|  
  
## <a name="enabled-attribute"></a>Attributo enabled  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|0|Non disabilitare la memorizzazione nella cache degli errori di associazione che si verificano perché l'assembly non è stato trovato da Probe. Questo è il comportamento di binding predefinito a partire dalla versione .NET Framework 2,0.|  
|1|Disabilitare la memorizzazione nella cache degli errori di associazione che si verificano perché l'assembly non è stato trovato da Probe. Questa impostazione ripristina il comportamento di associazione della .NET Framework versione 1,1.|  
  
### <a name="child-elements"></a>Elementi figlio  
 Nessuno.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione usato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## <a name="remarks"></a>Note  
 A partire dalla versione di .NET Framework 2,0, il comportamento predefinito per il caricamento degli assembly consiste nel memorizzare nella cache tutti gli errori di binding e caricamento. Ovvero, se il tentativo di caricamento di un assembly ha esito negativo, le successive richieste di caricamento dello stesso assembly hanno esito negativo, senza alcun tentativo di individuazione dell'assembly. Questo elemento Disabilita il comportamento predefinito per gli errori di associazione che si verificano perché l'assembly non è stato trovato nel percorso di probe. Questi errori generano <xref:System.IO.FileNotFoundException>.  
  
 Alcuni errori di binding e caricamento non sono interessati da questo elemento e vengono sempre memorizzati nella cache. Questi errori si verificano perché l'assembly è stato trovato ma non è stato possibile caricarlo. Generano <xref:System.BadImageFormatException> o <xref:System.IO.FileLoadException>. Nell'elenco seguente sono inclusi alcuni esempi di tali errori.  
  
- Se si tenta di caricare un file non è un assembly valido, i tentativi successivi di caricamento dell'assembly avranno esito negativo anche se il file danneggiato viene sostituito con l'assembly corretto.  
  
- Se si tenta di caricare un assembly bloccato dal file system, i tentativi successivi di caricamento dell'assembly avranno esito negativo anche dopo che l'assembly verrà rilasciato dal file system.  
  
- Se una o più versioni dell'assembly che si sta tentando di caricare si trovano nel percorso di sondaggio, ma la versione specifica richiesta non è tra di esse, i successivi tentativi di caricamento della versione avranno esito negativo anche se la versione corretta viene spostata nel percorso di sondaggio.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come disabilitare la memorizzazione nella cache degli errori di associazione degli assembly che si verificano perché l'assembly non è stato trovato da Probe.  
  
```xml  
<configuration>  
   <runtime>  
      <disableCachingBindingFailures enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Vedere anche

- [Schema delle impostazioni di runtime](index.md)
- [Schema dei file di configurazione](../index.md)
- [Come il runtime individua gli assembly](../../../deployment/how-the-runtime-locates-assemblies.md)
