---
title: 'Procedura: Serializzare un oggetto come flusso XML con codifica SOAP'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
ms.assetid: af406e0a-fa3a-46dd-a7ba-c80731eba3a0
ms.openlocfilehash: bfbdda0861a6f2867a2e7003dd7054129fd343b8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62018021"
---
# <a name="how-to-serialize-an-object-as-a-soap-encoded-xml-stream"></a>Procedura: Serializzare un oggetto come flusso XML con codifica SOAP
  
 Dato che un messaggio SOAP viene creato con XML, è possibile usare <xref:System.Xml.Serialization.XmlSerializer> per serializzare le classi e generare messaggi SOAP codificati. L'elemento XML ottenuto risulta conforme alla [sezione 5 del documento "Simple Object Access Protocol (SOAP) 1.1" del World Wide Web Consortium](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/#_Toc478383512). Quando si crea un servizio Web XML che comunica tramite messaggi SOAP, è possibile personalizzare il flusso XML applicando un set di attributi SOAP speciali a classi e membri di classi. Per un elenco di attributi, vedere [Attributi per il controllo della serializzazione SOAP codificata](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md).  
  
### <a name="to-serialize-an-object-as-a-soap-encoded-xml-stream"></a>Per serializzare un oggetto come flusso XML con codifica SOAP  
  
1. Creare la classe con lo [strumento XML Schema Definition (Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md).  
  
2. Applicare uno o più degli attributi speciali disponibili in `System.Xml.Serialization`. Consultare l'elenco "Attributi per il controllo della serializzazione SOAP codificata".  
  
3. Creare un `XmlTypeMapping` creando un nuovo `SoapReflectionImporter` e richiamando il metodo `ImportTypeMapping` con il tipo della classe serializzata.  
  
     L'esempio di codice seguente chiama il metodo `ImportTypeMapping` della classe `SoapReflectionImporter` per creare un `XmlTypeMapping`.  
  
    ```vb  
    ' Serializes a class named Group as a SOAP message.  
    Dim myTypeMapping As XmlTypeMapping =
        New SoapReflectionImporter().ImportTypeMapping(GetType(Group))  
    ```  
  
    ```csharp  
    // Serializes a class named Group as a SOAP message.  
    XmlTypeMapping myTypeMapping =
        new SoapReflectionImporter().ImportTypeMapping(typeof(Group));
    ```  
  
4. Creare un'istanza della classe `XmlSerializer` passando `XmlTypeMapping` al costruttore <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Xml.Serialization.XmlTypeMapping%29>.  
  
    ```vb  
    Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
    ```  
  
    ```csharp  
    XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
    ```  
  
5. Chiamare il metodo `Serialize` o `Deserialize`.  
  
## <a name="example"></a>Esempio  
  
```vb  
' Serializes a class named Group as a SOAP message.  
Dim myTypeMapping As XmlTypeMapping =
    New SoapReflectionImporter().ImportTypeMapping(GetType(Group))
Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
```  
  
```csharp  
// Serializes a class named Group as a SOAP message.  
XmlTypeMapping myTypeMapping =
    new SoapReflectionImporter().ImportTypeMapping(typeof(Group));
XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
```  
  
## <a name="see-also"></a>Vedere anche

- [Serializzazione SOAP e XML](../../../docs/standard/serialization/xml-and-soap-serialization.md)
- [Attributi per il controllo della serializzazione SOAP codificata](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md)
- [Serializzazione XML con Servizi Web XML](../../../docs/standard/serialization/xml-serialization-with-xml-web-services.md)
- [Procedura: Serializzare un oggetto](../../../docs/standard/serialization/how-to-serialize-an-object.md)
- [Procedura: Deserializzare un oggetto](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
- [Procedura: Eseguire l'override della serializzazione XML con codifica SOAP](../../../docs/standard/serialization/how-to-override-encoded-soap-xml-serialization.md)
