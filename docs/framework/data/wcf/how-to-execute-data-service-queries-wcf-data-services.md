---
title: 'Procedura: Esecuzione di query sul servizio dati (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- querying the data service [WCF Data Services]
- WCF Data Services, querying
- WCF Data Services, accessing data
ms.assetid: 62997821-e0c6-4c4d-9fb7-1273fb5e5d18
ms.openlocfilehash: 984bba9f31ddaee68c6997ba6da09a511e42b4ce
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780071"
---
# <a name="how-to-execute-data-service-queries-wcf-data-services"></a>Procedura: Esecuzione di query sul servizio dati (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente di eseguire query su un servizio dati da un'applicazione client basata su .NET Framework usando le classi del servizio dati client generate. È possibile eseguire query usando uno dei metodi seguenti:  
  
- Mediante l'esecuzione di una query LINQ sull'oggetto <xref:System.Data.Services.Client.DataServiceQuery%601> denominato ottenuto dall'oggetto <xref:System.Data.Services.Client.DataServiceContext> generato dallo strumento `Add Data Service Reference`  
  
- In modo implicito, mediante enumerazione dell'oggetto <xref:System.Data.Services.Client.DataServiceQuery%601> denominato ottenuto dall'oggetto <xref:System.Data.Services.Client.DataServiceContext> generato dallo strumento `Add Data Service Reference`  
  
- In modo esplicito, chiamando il metodo <xref:System.Data.Services.Client.DataServiceContext.Execute%2A> su <xref:System.Data.Services.Client.DataServiceQuery%601> o il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> per l'esecuzione asincrona.  
  
 Per ulteriori informazioni, vedere [esecuzione di query sul servizio dati](querying-the-data-service-wcf-data-services.md).  
  
 Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente. Questo servizio e le classi di dati client vengono creati al completamento della [WCF Data Services avvio rapido](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come definire ed eseguire una query LINQ sul servizio dati Northwind per la restituzione di tutti le entità `Customers`.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomersLinq](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getallcustomerslinq)]
 [!code-vb[Astoria Northwind Client#GetAllCustomersLinq](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getallcustomerslinq)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come usare il contesto generato dallo strumento `Add Data Service Reference` per eseguire in modo implicito una query sul servizio dati Northwind per la restituzione di tutte le entità `Customers`. L'URI del set di entità `Customers` richiesto viene determinato automaticamente dal contesto. La query viene eseguita in modo implicito quando si verifica l'enumerazione.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomers](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getallcustomers)]
 [!code-vb[Astoria Northwind Client#GetAllCustomers](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getallcustomers)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come usare l'oggetto <xref:System.Data.Services.Client.DataServiceContext> per eseguire in modo esplicito una query sul servizio dati Northwind per la restituzione di tutte le entità `Customers`.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomersExplicit](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getallcustomersexplicit)]
 [!code-vb[Astoria Northwind Client#GetAllCustomersExplicit](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getallcustomersexplicit)]  
  
## <a name="see-also"></a>Vedere anche

- [Procedura: Aggiungere opzioni di query a una query del servizio dati](how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)
