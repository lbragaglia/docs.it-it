---
title: 'Procedura: Usare un moniker del servizio con i contratti di scambio di metadati'
ms.date: 03/30/2017
ms.assetid: c41a07e5-cb9d-45d6-9ea4-34511e227faf
ms.openlocfilehash: e114bc2c046ba7145a91121ce23c82912680a048
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/13/2019
ms.locfileid: "70968955"
---
# <a name="how-to-use-a-service-moniker-with-metadata-exchange-contracts"></a>Procedura: Usare un moniker del servizio con i contratti di scambio di metadati
Dopo aver sviluppato alcuni nuovi servizi WCF, è possibile decidere di poter chiamare questi servizi da uno script o da un'applicazione Visual Basic 6,0. Un metodo consiste nel generare un assembly client WCF, registrare l'assembly con COM, installare l'assembly nella GAC, quindi fare riferimento ai tipi COM dal codice Visual Basic. Quando si distribuisce l'applicazione, sarà necessario distribuire anche l'assembly client WCF. L'utente dovrà quindi registrare l'assembly client WCF con COM e posizionarlo nella cache di assembly globale. L'interoperabilità COM di WCF consente inoltre di effettuare le stesse chiamate al servizio senza basarsi su un assembly client WCF. Il moniker WCF consente di chiamare qualsiasi servizio WCF da qualsiasi linguaggio compatibile con COM (Visual Basic, VBScript, Visual Basic, Applications Edition (VBA) e così via) specificando un URI dell'endpoint MEX (Metadata Exchange) che il moniker del servizio utilizza per estrarre il tipo informazioni sul servizio. In questo argomento viene illustrato come chiamare l'esempio WCF Introduzione usando un moniker WCF che specifica un endpoint MEX.  
  
> [!NOTE]
> I tipi definiti dall'assembly client WCF non vengono mai creati in realtà. e l'assembly viene usato solo per i metadati.  
  
### <a name="using-the-service-moniker-with-a-mex-address"></a>Utilizzo del moniker del servizio con un indirizzo Mex  
  
1. Compilare l'esempio introduzione e utilizzare Internet Explorer per passare all'URL (http://localhost/ServiceModelSamples/Service.svc) per verificare che il servizio sia funzionante.  
  
2. Creare uno script di Visual Basic o un'applicazione Visual Basic che contiene il codice seguente:  
  
    ```vb
    monString = "service:mexaddress=http://localhost/ServiceModelSamples/Service.svc/MEX"  
    monString = monString + ", address=http://localhost/ServiceModelSamples/Service.svc"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
    Set calc = GetObject(monString)  
    MsgBox calc.Add(3, 4)  
    ```  
  
3. Eseguire l'applicazione o lo script Visual Basic.  
  
    > [!NOTE]
    > Il servizio che si sta chiamando deve esporre un endpoint Mex affinché il moniker sia in grado di leggere i metadati dal servizio. Per altre informazioni, vedere [Procedura: Pubblicare i metadati per un servizio usando un file](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)di configurazione.  
  
    > [!NOTE]
    > Se il formato del moniker non è valido o se il servizio non è disponibile, la chiamata a `GetObject` restituirà un errore di sintassi non valida.  Se si riceve questo errore, verificare che il moniker che si sta usando sia valido e che il servizio sia disponibile.  
  
## <a name="see-also"></a>Vedere anche

- [Procedura: Usare il moniker del servizio Windows Communication Foundation senza registrazione](../../../../docs/framework/wcf/feature-details/use-the-wcf-service-moniker-without-registration.md)
- [Procedura: Usare un moniker di servizio con contratti WSDL](../../../../docs/framework/wcf/feature-details/how-to-use-a-service-moniker-with-wsdl-contracts.md)
