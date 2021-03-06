---
title: Vincoli e relazioni di XML Schema
ms.date: 03/30/2017
ms.assetid: 165bc2bc-60a1-40e0-9b89-7c68ef979079
ms.openlocfilehash: 76af1c2e9d85d18a68b8c0a947dfba3b3291326c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784195"
---
# <a name="xml-schema-constraints-and-relationships"></a>Vincoli e relazioni di XML Schema
In uno schema XSD (XML Schema Definition Language) è possibile specificare vincoli, ovvero vincoli UNIQUE, Key e keyref, e relazioni (tramite l'annotazione **msdata: Relationship** ). In questo argomento viene spiegato come vengono interpretati i vincoli e le relazioni specificati in XML Schema per generare il tipo <xref:System.Data.DataSet>.  
  
 In generale, in uno schema XML è possibile specificare l'annotazione **msdata: Relationship** se si desidera generare solo relazioni nel **set di dati**. Per ulteriori informazioni, vedere [generazione di relazioni tra DataSet da XML Schema (XSD)](generating-dataset-relations-from-xml-schema-xsd.md). Si specificano i vincoli (Unique, Key e keyref) se si desidera generare vincoli nel **set di dati**. Notare che i vincoli key e keyref vengono usati anche per generare relazioni, come spiegato successivamente in questo argomento.  
  
## <a name="generating-a-relationship-from-key-and-keyref-constraints"></a>Generazione di una relazione dai vincoli key e keyref  
 Anziché specificare l'annotazione **msdata: Relationship** , è possibile specificare i vincoli key e keyref, che vengono utilizzati durante il processo di mapping di XML Schema per generare non solo i vincoli ma anche la relazione nel **set di dati**. Tuttavia, se si specifica `msdata:ConstraintOnly="true"` nell'elemento **keyref** , nel **set di dati** vengono inclusi solo i vincoli e non sarà inclusa la relazione.  
  
 Nell'esempio seguente viene illustrato uno schema XML che include elementi **Order** e **OrderDetail** , che non sono annidati. Nello schema vengono specificati anche i vincoli key e keyref.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 Il **set di dati** generato durante il processo di mapping di XML Schema include le tabelle **Order** e **OrderDetail** . Il **set di dati** include inoltre relazioni e vincoli. Nell'esempio seguente vengono illustrati tali vincoli e relazioni. Si noti che lo schema non specifica l'annotazione **msdata: Relationship** ; al contrario, i vincoli key e keyref vengono usati per generare la relazione.  
  
```  
....ConstraintName: OrderNumberKey  
....Type: UniqueConstraint  
....Table: Order  
....Columns: OrderNumber  
....IsPrimaryKey: False  
  
....ConstraintName: OrderNoRef  
....Type: ForeignKeyConstraint  
....Table: OrderDetail  
....Columns: OrderNo  
....RelatedTable: Order  
....RelatedColumns: OrderNumber  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
```  
  
 Nell'esempio di schema precedente gli elementi **Order** e **OrderDetail** non sono annidati. Nell'esempio di schema seguente tali elementi sono annidati. Tuttavia, non è specificata alcuna annotazione **msdata: Relationship** ; viene pertanto presupposta una relazione implicita. Per altre informazioni, vedere [eseguire il mapping di relazioni implicite tra gli elementi dello schema annidato](map-implicit-relations-between-nested-schema-elements.md). Nello schema vengono specificati anche i vincoli key e keyref.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:integer" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 Il **set di dati** risultante dal processo di mapping di XML Schema include due tabelle:  
  
```  
Order(OrderNumber, EmpNumber, Order_Id)  
OrderDetail(OrderNumber, ItemNumber, Order_Id)  
```  
  
 Il **set di dati** include anche le due relazioni, una basata sull'annotazione **msdata: Relationship** e l'altra in base ai vincoli key e keyref, e vari vincoli. Nell'esempio seguente vengono illustrati i vincoli e le relazioni.  
  
```  
..RelationName: Order_OrderDetail  
..ParentTable: Order  
..ParentColumns: Order_Id  
..ChildTable: OrderDetail  
..ChildColumns: Order_Id  
..ParentKeyConstraint: Constraint1  
..ChildKeyConstraint: Order_OrderDetail  
..Nested: True  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
  
..ConstraintName: OrderNumberKey  
..Type: UniqueConstraint  
..Table: Order  
..Columns: OrderNumber  
..IsPrimaryKey: False  
  
..ConstraintName: Constraint1  
..Type: UniqueConstraint  
..Table: Order  
..Columns: Order_Id  
..IsPrimaryKey: True  
  
..ConstraintName: Order_OrderDetail  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: Order_Id  
..RelatedTable: Order  
..RelatedColumns: Order_Id  
  
..ConstraintName: OrderNoRef  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: OrderNo  
..RelatedTable: Order  
..RelatedColumns: OrderNumber  
```  
  
 Se un vincolo keyref che fa riferimento a una tabella nidificata contiene l'annotazione **msdata: nidificata = "true"** , il **set di dati** creerà una singola relazione annidata basata sul vincolo keyref e sul vincolo unique/key correlato.  
  
## <a name="see-also"></a>Vedere anche

- [Derivazione della struttura relazionale di DataSet da XML Schema (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [Panoramica di ADO.NET](../ado-net-overview.md)
