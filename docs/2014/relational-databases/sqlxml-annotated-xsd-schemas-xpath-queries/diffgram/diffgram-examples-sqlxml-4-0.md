---
title: DiffGram 예제 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 975fd3a984418c20ae0e142b447aea6645284cbc
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703195"
---
# <a name="diffgram-examples-sqlxml-40"></a>DiffGram 예(SQLXML 4.0)
  이 항목에서 설명하는 예는 데이터베이스에 대한 삽입, 업데이트 및 삭제 작업을 수행하는 DiffGram으로 구성되어 있습니다. 예를 사용하기 전에 다음 사항을 확인하십시오.  
  
-   DiffGram 예를 테스트하려면 예에 사용되는 두 개의 테이블(Cust 및 Ord)을 만들어야 합니다.  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   이 항목의 예 중 대부분에는 다음 XSD 스키마가 사용됩니다.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
    <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
    <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
    </xsd:element>  
  
    </xsd:schema>     
    ```  
  
     이 스키마를 예에 사용되는 다른 파일을 저장한 폴더와 같은 폴더에 DiffGramSchema.xml로 저장합니다.  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. DiffGram을 사용하여 레코드 삭제  
 이 예의 DiffGram은 Cust 테이블에서 CustomerID가 ALFKI인 고객 레코드를 삭제하고 Ord 테이블에서 OrderID가 1인 해당 주문 레코드를 삭제합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 ** \< Before>** 블록에는 ** \< Order>** 요소 (**diffgr: id = "Order1"**)와 ** \< Customer>** 요소 (**diffgr: id = "Customer1"**)가 있습니다. 이러한 요소는 데이터베이스의 기존 레코드를 나타냅니다. ** \< Datainstance>** 요소에 해당 하는 레코드 ( **diffgr: id**가 같음)가 없습니다. 이는 삭제 작업임을 나타냅니다.  
  
#### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  이러한 테이블을 **tempdb** 데이터베이스에 만듭니다.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  다음 예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  위 DiffGram을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 이전 단계에 사용된 폴더와 같은 폴더에 MyDiffGram.xml로 저장합니다.  
  
4.  이 항목의 앞에서 제공된 DiffGramSchema를 복사하여 텍스트 파일로 붙여넣습니다. 파일을 DiffGramSchema.xml로 저장합니다.  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 DiffGram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>B. DiffGram을 사용하여 레코드 삽입  
 이 예에서 DiffGram은 Cust 테이블과 Ord 테이블에 레코드를 하나씩 삽입합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 이 DiffGram에서 ** \< 이전>** 블록을 지정 하지 않았습니다 (기존 데이터베이스 레코드는 확인 되지 않음). 각각 Cust 및 Ord 테이블에 매핑되는 ** \< 고객>** 및 ** \< datainstance>** 블록의 요소 ** \<>** 요소에 의해 식별 되는 두 개의 레코드 인스턴스가 있습니다. 이러한 두 요소는 모두 **diffgr: haschanges** 특성을 지정 합니다 (**haschanges = "inserted"**). 이는 삽입 작업임을 나타냅니다. 이 DiffGram에서 **Haschanges = "modified"** 를 지정 하는 경우 존재 하지 않는 레코드를 수정 하 고 오류가 발생 함을 나타냅니다.  
  
#### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  이러한 테이블을 **tempdb** 데이터베이스에 만듭니다.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  다음 예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  위 DiffGram을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 이전 단계에 사용된 폴더와 같은 폴더에 MyDiffGram.xml로 저장합니다.  
  
4.  이 항목의 앞에서 제공된 DiffGramSchema를 복사하여 텍스트 파일로 붙여넣습니다. 파일을 DiffGramSchema.xml로 저장합니다.  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 DiffGram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. DiffGram을 사용하여 기존 레코드 업데이트  
 이 예에서 DiffGram은 고객 ALFKI의 고객 정보(CompanyName 및 ContactName)를 업데이트합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 ** \< Before>** 블록은 ** \< Customer>** 요소 (**diffgr: id = "Customer1"**)를 포함 합니다. ** \< Datainstance>** 블록에는 동일한 **id**를 가진 해당 ** \< Customer>** 요소가 포함 됩니다. ** \< Newdataset>** 의 ** \< customer>** 요소는 **diffgr: haschanges = "modified"** 도 지정 합니다. 이는 업데이트 작업을 나타내며,이에 따라 **Cust** 테이블의 고객 레코드가 업데이트 됩니다. **Diffgr: hasChanges** 특성이 지정 되지 않은 경우 DiffGram 처리 논리는이 요소를 무시 하 고 업데이트를 수행 하지 않습니다.  
  
#### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  이러한 테이블을 **tempdb** 데이터베이스에 만듭니다.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  다음 예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  위 DiffGram을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 이전 단계에 사용된 폴더와 같은 폴더에 MyDiffGram.xml로 저장합니다.  
  
4.  이 항목의 앞에서 제공된 DiffGramSchema를 복사하여 텍스트 파일로 붙여넣습니다. 파일을 DiffGramSchema.xml로 저장합니다.  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 DiffGram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. DiffGram을 사용하여 레코드 삽입, 업데이트 및 삭제  
 이 예에서는 비교적 복잡한 DiffGram을 사용하여 삽입, 업데이트 및 삭제 작업을 수행합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 DiffGram 논리는 이 DiffGram을 다음과 같이 처리합니다.  
  
-   DiffGram 처리 논리에 따라 매핑 스키마에 설명 된 것 처럼 ** \< 이전>** 블록의 모든 최상위 요소가 해당 테이블에 매핑됩니다.  
  
-   ** \< Before>** 블록에는 ** \< Order>** 요소 (**Dffgr: id = "Order1"**) 및 ** \< Customer>** 요소 (**diffgr: id = "Customer1"**)가 있습니다 .이 요소에는 ** \< datainstance>** 블록에 해당 하는 요소가 없습니다 (동일한 id로). 이는 삭제 작업임을 나타내며 Cust 테이블과 Ord 테이블에서 레코드가 삭제됩니다.  
  
-   ** \< Before>** 블록에는 동일한 id를 가진 ** \< datainstance>** 블록에 해당 ** \< customer>** 요소가 있는 ** \< customer>** 요소 (**diffgr: id = "Customer2"**)가 있습니다. ** \< Datainstance>** 블록의 요소는 **Diffgr: haschanges = "modified"** 를 지정 합니다. 이는 customer ANATR의 경우 ** \< datainstance>** 블록에 지정 된 값을 사용 하 여 Cust 테이블에서 CompanyName 및 ContactName 정보가 업데이트 되는 업데이트 작업입니다.  
  
-   ** \< Datainstance>** 블록에는 ** \< Customer>** 요소 (**diffgr: id = "예제의 customer3"**) 및 ** \< Order>** 요소 (**diffgr: id = "Order3"**)가 있습니다. 이러한 요소는 모두 **diffgr: hasChanges** 특성을 지정 하지 않습니다. 따라서 DiffGram 처리 논리에서 이러한 요소는 무시됩니다.  
  
-   ** \< Datainstance>** 블록에는 before> 블록에 해당 요소가 없는 ** \< Customer>** 요소 (**diffgr: id = "Customer4"**) 및 ** \< Order>** 요소 (**diffgr: id = "Order4"**)가 있습니다 \< . ** \< Datainstance>** 블록의 이러한 요소는 **Diffgr: haschanges = "inserted"** 를 지정 합니다. 따라서 Cust 테이블과 Ord 테이블에 새 레코드가 추가됩니다.  
  
#### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  **Tempdb** 데이터베이스에 다음 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  다음 예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  위 DiffGram을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 이전 단계에 사용된 폴더와 같은 폴더에 MyDiffGram.xml로 저장합니다.  
  
4.  이 항목의 앞에서 제공된 DiffGramSchema를 복사하여 텍스트 파일로 붙여넣습니다. 파일을 DiffGramSchema.xml로 저장합니다.  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 DiffGram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. diffgr:parentID 주석이 지정된 DiffGram을 사용하여 업데이트 적용  
 이 예에서는 DiffGram의 ** \< before>** 블록에 지정 된 **parentID** 주석을 업데이트를 적용 하는 데 사용 하는 방법을 보여 줍니다.  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 ** \< 이전>** 블록만 있으므로이 DiffGram은 삭제 작업을 지정 합니다. DiffGram에서 **parentID** 주석은 주문 및 주문 세부 정보 간에 부모-자식 관계를 지정 하는 데 사용 됩니다. SQLXML에서 레코드를 삭제할 때 이 관계를 통해 식별된 자식 테이블에서 레코드가 삭제되고 해당 부모 테이블에서도 레코드가 삭제됩니다.  
  
  
