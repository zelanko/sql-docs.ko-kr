---
title: DiffGram 예 (SQLXML 4.0) | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed354e6b72f66908c12e1254738df75008659f8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127728"
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
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>1. DiffGram을 사용하여 레코드 삭제  
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
  
 에  **\<하기 전에 >** 블록, 즉는  **\<순서 >** 요소 (**diffgr: id = "(diffgr:id="order1"**) 및  **\< 고객 >** 요소 (**diffgr: id = "Customer1"**). 이러한 요소는 데이터베이스의 기존 레코드를 나타냅니다. 합니다  **\<DataInstance >** 요소에 해당 레코드가 없는 (동일한 **diffgr: id**). 이는 삭제 작업임을 나타냅니다.  
  
#### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  이러한 테이블을 만들 합니다 **tempdb** 데이터베이스입니다.  
  
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
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>2. DiffGram을 사용하여 레코드 삽입  
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
  
 이 DiffGram에는  **\<하기 전에 >** 블록을 지정 하지 않으면 (없습니다 기존 데이터베이스 레코드가 식별) 합니다. 레코드 인스턴스 두 개가 (로 식별 되는  **\<고객 >** 하 고  **\<순서 >** 요소에는  **\<DataInstance >** 블록) 각각 Cust 테이블과 Ord 테이블에 매핑하는 합니다. 이러한 요소 중 둘 다 지정 된 **diffgr: haschanges** 특성 (**hasChanges = "inserted"**). 이는 삽입 작업임을 나타냅니다. 지정 하는 경우이 DiffGram **hasChanges = "modified"**, 오류가 발생 하는 존재 하지 않는 레코드를 수정 하려는 있음을 나타냅니다.  
  
#### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  이러한 테이블을 만들 합니다 **tempdb** 데이터베이스입니다.  
  
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
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>3. DiffGram을 사용하여 기존 레코드 업데이트  
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
  
 합니다  **\<하기 전에 >** 블록 포함을  **\<고객 >** 요소 (**diffgr: id = "Customer1"**). 합니다  **\<DataInstance >** 해당 블록 포함  **\<고객 >** 동일한 요소 **id**합니다. 합니다  **\<고객 >** 요소에는  **\<NewDataSet >** 도 지정 **diffgr: haschanges = "modified"** 합니다. 고객 레코드가 업데이트 작업을 의미 합니다 **Cust** 테이블이 적절 하 게 업데이트 됩니다. 경우는 **diffgr: haschanges** 특성이 지정 되지 않은 DiffGram 처리 논리는이 요소를 무시 하 고 업데이트가 수행 되지 않습니다.  
  
#### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  이러한 테이블을 만들 합니다 **tempdb** 데이터베이스입니다.  
  
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
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>4. DiffGram을 사용하여 레코드 삽입, 업데이트 및 삭제  
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
  
-   최상위 요소를 모두 포함 하는 DiffGram 처리 논리에 따라 합니다  **\<하기 전에 >** 매핑 스키마에 설명 된 대로 해당 테이블에는 지도 차단 합니다.  
  
-   합니다  **\<하기 전에 >** 블록에는  **\<순서 >** 요소 (**dffgr:id "(diffgr:id="order1"=**) 및  **\<고객 >** 요소 (**diffgr: id = "Customer1"**)에 해당 요소가 없습니다 합니다  **\<DataInstance >** 블록 (ID가 같은). 이는 삭제 작업임을 나타내며 Cust 테이블과 Ord 테이블에서 레코드가 삭제됩니다.  
  
-   합니다  **\<하기 전에 >** 블록에는  **\<고객 >** 요소 (**diffgr: id = "Customer2"**)에 해당  **\<고객 >** 요소에는  **\<DataInstance >** 블록 (ID가 같은). 요소를  **\<DataInstance >** 지정 하는 블록이 **diffgr: haschanges = "modified"** 합니다. 이 작업은 업데이트 작업에 지정 된 값을 사용 하 여 Cust 테이블에서 CompanyName 및 ContactName 정보가 업데이트 됩니다는 anatr 이라는 고객에 대 한 합니다  **\<DataInstance >** 블록입니다.  
  
-   합니다  **\<DataInstance >** 블록에는  **\<고객 >** 요소 (**diffgr: id = "customer3 이라는"**) 및  **\<순서 >** 요소 (**diffgr: id = "Order3"**). 이러한 요소를 모두 지정 합니다 **diffgr: haschanges** 특성입니다. 따라서 DiffGram 처리 논리에서 이러한 요소는 무시됩니다.  
  
-   합니다  **\<DataInstance >** 블록에는  **\<고객 >** 요소 (**diffgr: id = "(diffgr:id="customer4"**) 및  **\<순서 >** 요소 (**diffgr: id = "Order4"**)에서 해당 요소가 없을에 대 한는 \<전에 > 블록입니다. 이러한 요소는  **\<DataInstance >** 블록 지정 **diffgr: haschanges = "inserted"** 합니다. 따라서 Cust 테이블과 Ord 테이블에 새 레코드가 추가됩니다.  
  
#### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  다음 테이블을 만듭니다는 **tempdb** 데이터베이스입니다.  
  
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
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>5. diffgr:parentID 주석이 지정된 DiffGram을 사용하여 업데이트 적용  
 이 예제 하는 방법을 **parentID** 에 지정 된 주석 합니다  **\<하기 전에 >** 업데이트 적용에 DiffGram의 블록을 사용 합니다.  
  
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
  
 이 DiffGram만 있기 때문에 삭제 작업을 지정 된  **\<하기 전에 >** 블록입니다. DiffGram에서 합니다 **parentID** 주석은 주문 및 주문 세부 정보 간의 부모-자식 관계를 지정 하는 데 사용 됩니다. SQLXML에서 레코드를 삭제할 때 이 관계를 통해 식별된 자식 테이블에서 레코드가 삭제되고 해당 부모 테이블에서도 레코드가 삭제됩니다.  
  
  
