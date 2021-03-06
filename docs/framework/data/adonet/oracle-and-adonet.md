---
title: Oracle e ADO.NET
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ee8e389-53cf-45cf-80bd-1df63ef34f2e
ms.openlocfilehash: ccfe40f218e3f09de53d6cb596a31b2520d9ff9b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783480"
---
# <a name="oracle-and-adonet"></a>Oracle e ADO.NET
> [!NOTE]
> I tipi in <xref:System.Data.OracleClient> sono deprecati. I tipi restano supportati nella versione corrente di .NET Framework, ma saranno rimossi in una versione futura. Microsoft consiglia di usare un provider Oracle di terze parti.  
  
 In questa sezione vengono descritte le caratteristiche e i comportamenti specifici del provider di dati .NET Framework per Oracle.  
  
 Il .NET Framework provider di dati per Oracle consente di accedere a un database Oracle utilizzando l'interfaccia OCI (Oracle Call Interface) fornita dal software client Oracle. La funzionalità del provider di dati è progettata per essere simile a quella dei provider di dati .NET Framework per SQL Server, OLE DB e ODBC.  
  
 Per utilizzare la .NET Framework provider di dati per Oracle, un'applicazione deve fare riferimento <xref:System.Data.OracleClient> allo spazio dei nomi come indicato di seguito:  
  
```vb  
Imports System.Data.OracleClient  
```  
  
```csharp  
using System.Data.OracleClient;  
```  
  
 Quando si compila il codice, inoltre, è necessario includere un riferimento alla DLL. Ad esempio, se si compila un programma C#, la riga di comando deve includere:  
  
```  
csc /r:System.Data.OracleClient.dll  
```  
  
## <a name="in-this-section"></a>In questa sezione  
 [Requisiti di sistema](system-requirements-for-the-dotnet-data-provider-for-oracle.md)  
 Vengono descritti i requisiti per l'utilizzo di .NET Framework provider di dati per Oracle e vengono descritti alcuni problemi che è necessario tenere presente quando si utilizza.  
  
 [Oggetti BFILE Oracle](oracle-bfiles.md)  
 Viene descritta la classe <xref:System.Data.OracleClient.OracleBFile> usata per il tipo di dati BFILE Oracle.  
  
 [Oggetti LOB Oracle](oracle-lobs.md)  
 Viene descritta la classe <xref:System.Data.OracleClient.OracleLob> usata per il tipo di dati LOB Oracle.  
  
 [Oggetti REF CURSOR Oracle](oracle-ref-cursors.md)  
 Viene descritto il supporto del tipo di dati REF CURSOR Oracle.  
  
 [OracleTypes](oracletypes.md)  
 Vengono descritte le strutture utilizzabili con i tipi di dati Oracle, inclusi tipi <xref:System.Data.OracleClient.OracleNumber> e <xref:System.Data.OracleClient.OracleString>.  
  
 [Sequenze Oracle](oracle-sequences.md)  
 Viene descritto il supporto per il recupero dei valori chiave di sequenze di Oracle generati dal server.  
  
 [Mapping dei tipi di dati Oracle](oracle-data-type-mappings.md)  
 Vengono presentati i tipi di dati Oracle e i relativi mapping alla classe <xref:System.Data.OracleClient.OracleDataReader>.  
  
 [Transazioni distribuite Oracle](oracle-distributed-transactions.md)  
 Viene descritto come l'oggetto <xref:System.Data.OracleClient.OracleConnection>, in presenza di una transazione attiva, esegue l'inserimento automatico nella transazione distribuita.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Protezione delle applicazioni ADO.NET](securing-ado-net-applications.md)  
 Vengono descritte le tecniche che consentono di scrivere codice sicuro quando si usa ADO.NET.  
  
 [Oggetti DataSet, DataTable e DataView](./dataset-datatable-dataview/index.md)  
 Viene descritto come creare e usare `DataSets`, `DataSets` tipizzati, `DataTables` e `DataViews`.  
  
 [Recupero e modifica di dati in ADO.NET](retrieving-and-modifying-data.md)  
 Viene descritto come usare i dati in ADO.NET.  
  
 [SQL Server e ADO.NET](./sql/index.md)  
 Viene descritto come usare le funzionalità e le caratteristiche specifiche di SQL Server.  
  
 [DbProviderFactories](dbproviderfactories.md)  
 Vengono descritte le classi generiche che consentono di scrivere codice indipendente dal provider in ADO.NET.  
  
## <a name="see-also"></a>Vedere anche

- [ADO.NET](index.md)
- [Panoramica di ADO.NET](ado-net-overview.md)
