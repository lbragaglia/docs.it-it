---
title: <oneWay>
ms.date: 03/30/2017
ms.assetid: 00e67e0e-77c0-4695-9138-c0997b0e5f3c
ms.openlocfilehash: f12969d8b752e54916b45c3d0e64f114971b8944
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2019
ms.locfileid: "70397658"
---
# <a name="oneway"></a>\<oneWay>
Abilita il routing dei pacchetti e l'uso di metodi unidirezionali per un'associazione personalizzata.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> System. serviceModel**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Binding >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<CustomBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<Binding >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> oneWay**  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<oneWay packetRoutable="Boolean">
  <channelPoolSettings idleTimeout="TimeSpan"
                       leaseTimeout="TimeSpan"
                       maxOutboundConnectionsPerEndpoint="Integer" />
</oneWay>
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|DESCRIZIONE|  
|---------------|-----------------|  
|`packetRoutable`|Valore booleano che specifica se è attivato il routing dei pacchetti. Il valore predefinito è `false`.|  
|`MaxAcceptedChannels`|Numero intero che specifica il numero massimo di canali che possono essere accettati.|  
  
### <a name="child-elements"></a>Elementi figlio  
  
|Elemento|DESCRIZIONE|  
|-------------|-----------------|  
|[\<channelPoolSettings>](channelpoolsettings.md)|Oggetto <xref:System.ServiceModel.Configuration.ChannelPoolSettingsElement> che contiene le proprietà del pool di canali per il canale corrente.|  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|DESCRIZIONE|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## <a name="remarks"></a>Note  
 Per abilitare il routing dei pacchetti, è necessario un livello di conversione unidirezionale, fornito da questo elemento. Un utente può creare un'associazione personalizzata che sovrapponga questa associazione su un trasporto in grado di riconoscere la sessione o un trasporto Request/Reply affinché supporti il routing dei pacchetti. Questa elemento può essere inoltre usato quando si desidera esporre metodi unidirezionali in modo più nativo. Su questo livello possono essere applicate più trasformazioni, ad esempio duplex composito e messaggistica attendibile.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.ServiceModel.Channels.OneWayBindingElement>
- <xref:System.ServiceModel.Configuration.OneWayElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Associazioni](../../../wcf/bindings.md)
- [Estensione delle associazioni](../../../wcf/extending/extending-bindings.md)
- [Associazioni personalizzate](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
