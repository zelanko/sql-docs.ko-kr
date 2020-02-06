---
title: '예제: OPENXML 사용 | Microsoft 문서'
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- XML [SQL Server], mapping data
- OPENXML statement, about OPENXML statement
- overflow in XML document [SQL Server]
- mapping XML data [SQL Server]
- combining attribute-centric and element centric mapping
- unconsumed data
- attribute-centric mapping
- column patterns [XML in SQL Server]
- XML [SQL Server], overflow handling
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- flags parameter
- element-centric mapping [SQL Server]
- edge tables
ms.assetid: 689297f3-adb0-4d8d-bf62-cfda26210164
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ea3ad1c2f7cb482888f0cd4d31a91f9975745b7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67943381"
---
# <a name="examples-using-openxml"></a>예제: OPENXML 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 항목의 예제에서는 XML 문서의 행 집합 뷰를 만들 때 OPENXML을 사용하는 방법을 설명합니다. OPENXML 구문에 대한 자세한 내용은 [OPENXML&#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)을 참조하세요. 다음 예에서는 OPENXML의 메타 속성 지정을 제외한 OPENXML의 모든 측면을 보여 줍니다. OPENXML에서 메타 속성을 지정하는 방법은 [OPENXML에 메타 속성 지정](../../relational-databases/xml/specify-metaproperties-in-openxml.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 데이터를 검색할 때 XML 문서에서 행을 결정하는 노드를 식별하는 데 *rowpattern* 이 사용됩니다. 또한 MSXML XPath 구현에 사용된 XPath 패턴 언어에 *rowpattern* 이 표현됩니다. 예를 들어 패턴이 요소나 특성으로 끝나는 경우에는 *rowpattern*에 의해 지정된 각 요소 또는 특성 노드에 대해 한 개의 행이 생성됩니다.  
  
 *flags* 값은 기본 매핑을 제공합니다. *ColPattern* 이 *SchemaDeclaration*에 지정되지 않은 경우 *flags* 에 지정된 매핑이 간주됩니다. *ColPattern* 이 *SchemaDeclaration* 에 지정된 경우에는 *flags*값이 무시됩니다. 지정된 *ColPattern* 은 매핑(특성 중심 또는 요소 중심)은 물론, 오버플로와 소비되지 않은 데이터를 처리할 때의 동작도 결정합니다.  
  
### <a name="a-executing-a-simple-select-statement-with-openxml"></a>A. OPENXML에서 단순 SELECT 문 실행  
 이 예의 XML 문서는 <`Customer`>, <`Order`> 및 <`OrderDetail`> 요소로 이루어져 있습니다. OPENXML 문은 XML 문서로부터 두 열( **CustomerID** 및 **ContactName**)로 구성된 행 집합의 고객 정보를 검색합니다.  
  
 먼저 **sp_xml_preparedocument** 저장 프로시저가 문서 핸들을 얻기 위해 호출됩니다. 이 문서 핸들은 OPENXML에 전달됩니다.  
  
 OPENXML 문에서는 다음을 보여 줍니다.  
  
-   *rowpattern*(/ROOT/Customer)은 처리할 <`Customer`> 노드를 식별합니다.  
  
-   *flags* 매개 변수 값은 **1** 로 설정되어 특성 중심의 매핑을 나타냅니다. 결과적으로 XML 특성은 *SchemaDeclaration*에 정의된 행 집합의 열에 매핑됩니다.  
  
-   WITH 절의 *SchemaDeclaration*에서는 지정된 *ColName* 값이 해당 XML 특성 이름과 일치합니다. 따라서 *ColPattern* 매개 변수는 *SchemaDeclaration*에 지정되지 않습니다.  
  
 그런 다음 SELECT 문은 OPENXML이 제공하는 행 집합의 모든 열을 검색합니다.  
  
```  
DECLARE @DocHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @DocHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@DocHandle, '/ROOT/Customer',1)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @DocHandle  
```  
  
 다음은 결과입니다.  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 <`Customer`> 요소에는 하위 요소가 없기 때문에 *flags*가 **2**로 설정되어 요소 중심 매핑을 나타내도록 같은 SELECT 문이 실행되는 경우 두 고객에 대한 **CustomerID** 및 **ContactName**의 값은 NULL로 반환됩니다.  
  
 \@xmlDocument는 **xml** 형식 또는 **(n)varchar(max)** 형식일 수 있습니다.  
  
 XML 문서에서 <`CustomerID`>와 <`ContactName`>이 하위 요소인 경우에는 요소 중심의 매핑이 값을 검색합니다.  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer>  
   <CustomerID>VINET</CustomerID>  
   <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer>     
   <CustomerID>LILAS</CustomerID>  
   <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT    *  
FROM      OPENXML (@XmlDocumentHandle, '/ROOT/Customer',2)  
           WITH (CustomerID  varchar(10),  
                 ContactName varchar(20))  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 다음은 결과입니다.  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 **sp_xml_preparedocument** 에 의해 반환되는 문서 핸들은 세션이 아닌 일괄 처리 기간 동안 유효합니다.  
  
### <a name="b-specifying-colpattern-for-mapping-between-rowset-columns-and-the-xml-attributes-and-elements"></a>B. 행 집합 열과 XML 특성 및 요소 간의 매핑을 위해 ColPattern 지정  
 이 예제에서는 행 집합 열과 XML 특성 및 요소 간에 매핑을 제공하기 위해 선택 사항인 *ColPattern* 매개 변수에 XPath 패턴을 지정하는 방법을 보여 줍니다.  
  
 이 예의 XML 문서는 <`Customer`>, <`Order`> 및 <`OrderDetail`> 요소로 이루어져 있습니다. OPENXML 문은 고객과 주문 정보를 XML 문서로부터 행 집합(**CustomerID**, **OrderDate**, **ProdID**및 **Qty**)으로 검색합니다.  
  
 먼저 **sp_xml_preparedocument** 저장 프로시저가 문서 핸들을 얻기 위해 호출됩니다. 이 문서 핸들은 OPENXML에 전달됩니다.  
  
 OPENXML 문에서는 다음을 보여 줍니다.  
  
-   *rowpattern*(/ROOT/Customer/Order/OrderDetail)은 처리할 <`OrderDetail`> 노드를 식별합니다.  
  
 이해를 돕기 위해 *flags* 매개 변수 값은 **2** 로 설정되어 특성 중심의 매핑을 나타냅니다. 하지만 *ColPattern* 에 지정된 매핑은 이 매핑을 덮어 씁니다. 즉, *ColPattern* 에 지정된 XPath 패턴은 행 집합의 열을 특성으로 매핑합니다. 그러면 특성 중심 매핑이 됩니다.  
  
 WITH 절에 있는 *SchemaDeclaration*에서는 *ColPattern* 도 *ColName* 및 *ColType* 매개 변수로 지정됩니다. 선택 항목인 *ColPattern* 은 지정된 XPath 패턴이며 다음을 나타냅니다.  
  
-   행 집합의 **OrderID**, **CustomerID** 및 **OrderDate** 열은 *rowpattern*에 의해 식별되는 노드의 부모 노드 특성으로 매핑되고 *rowpattern*은 <`OrderDetail`> 노드를 식별합니다. 따라서 **CustomerID** 및 **OrderDate** 열은 < **> 요소의** CustomerID**및**OrderDate`Order` 특성으로 매핑됩니다.  
  
-   행 집합의 **ProdID** 및 **Qty** 열은 **rowpattern** 에서 식별된 노드의 **ProductID** 및 *Quantity*특성으로 매핑됩니다.  
  
 그런 다음 SELECT 문은 OPENXML이 제공하는 행 집합의 모든 열을 검색합니다.  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT stmt using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@XmlDocumentHandle, '/ROOT/Customer/Order/OrderDetail',2)  
WITH (OrderID     int         '../@OrderID',  
      CustomerID  varchar(10) '../@CustomerID',  
      OrderDate   datetime    '../@OrderDate',  
      ProdID      int         '@ProductID',  
      Qty         int         '@Quantity')  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 다음은 결과입니다.  
  
```  
OrderID CustomerID        OrderDate          ProdID    Qty  
-------------------------------------------------------------  
10248    VINET     1996-07-04 00:00:00.000     11       12  
10248    VINET     1996-07-04 00:00:00.000     42       10  
10283    LILAS     1996-08-16 00:00:00.000     72        3  
```  
  
 *ColPattern* 으로 지정된 XPath 패턴은 또한 행 집합 열로 XML 요소를 매핑하도록 지정될 수 있습니다. 그러면 요소 중심 매핑이 됩니다. 다음 예에서 XML 문서 <`CustomerID`> 및 <`OrderDate`>는 <`Orders`> 요소의 하위 요소입니다. *ColPattern* 은 *flags* 매개 변수에 지정된 매핑을 덮어쓰므로 OPENXML에는 *flags* 매개 변수가 지정되지 않습니다.  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order EmployeeID="5" >  
      <OrderID>10248</OrderID>  
      <CustomerID>VINET</CustomerID>  
      <OrderDate>1996-07-04T00:00:00</OrderDate>  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order  EmployeeID="3" >  
      <OrderID>10283</OrderID>  
      <CustomerID>LILAS</CustomerID>  
      <OrderDate>1996-08-16T00:00:00</OrderDate>  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail')  
WITH (CustomerID  varchar(10)   '../CustomerID',  
      OrderDate   datetime      '../OrderDate',  
      ProdID      int           '@ProductID',  
      Qty         int           '@Quantity')  
EXEC sp_xml_removedocument @docHandle  
```  
  
### <a name="c-combining-attribute-centric-and-element-centric-mapping"></a>C. 특성 중심 및 요소 중심의 매핑 결합  
 이 예에서 *flags* 매개 변수는 **3** 으로 설정되며 특성 중심 및 요소 중심 매핑이 적용됨을 나타냅니다. 이 경우, 특성 중심의 매핑이 먼저 적용된 다음 아직 처리되지 않은 모든 열에 대해 요소 중심의 매핑이 적용됩니다.  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument =N'<ROOT>  
<Customer CustomerID="VINET"  >  
     <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" >   
     <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer',3)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @docHandle  
```  
  
 다음은 결과입니다.  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 특성 중심의 매핑은 **CustomerID**에 대해 적용됩니다. < **> 요소에는** ContactName`Customer` 특성이 없습니다. 따라서 요소 중심 매핑이 적용됩니다.  
  
### <a name="d-specifying-the-text-xpath-function-as-colpattern"></a>D. text() XPath 함수를 ColPattern으로 지정  
 이 예의 XML 문서는 <`Customer`> 및 <`Order`> 요소로 이루어져 있습니다. OPENXML 문은 < **> 요소의** oid`Order` 특성, *rowpattern*으로 식별된 노드에 대한 부모 노드의 ID 및 요소 콘텐츠의 리프 값 문자열로 구성된 행 집합을 검색합니다.  
  
 먼저 **sp_xml_preparedocument** 저장 프로시저가 문서 핸들을 얻기 위해 호출됩니다. 이 문서 핸들은 OPENXML에 전달됩니다.  
  
 OPENXML 문에서는 다음을 보여 줍니다.  
  
-   *rowpattern*(/root/Customer/Order)은 처리할 <`Order`> 노드를 식별합니다.  
  
-   *flags* 매개 변수 값은 **1** 로 설정되어 특성 중심의 매핑을 나타냅니다. 결과적으로 XML 특성은 *SchemaDeclaration*에 정의된 행 집합 열에 매핑됩니다.  
  
-   WITH 절에 있는 *SchemaDeclaration* 에서는 행 집합 열 이름 **oid** 와 **amount** 가 해당 XML 특성 이름과 일치합니다. 따라서 *ColPattern* 매개 변수는 지정되지 않습니다. 행 집합의 **comment** 열에 대해서는 XPath 함수 **text()** 가 *ColPattern*으로 지정됩니다. 이것은 *flags*에 지정된 특성 중심의 매핑을 덮어쓰며 열에는 요소 내용의 리프 값 문자열이 포함됩니다.  
  
 그런 다음 SELECT 문은 OPENXML이 제공하는 행 집합의 모든 열을 검색합니다.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied  
      </Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
            <Urgency>Important</Urgency>  
            Happy Customer.  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH (oid     char(5),   
           amount  float,   
           comment ntext 'text()')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 다음은 결과입니다.  
  
```  
oid   amount        comment  
----- -----------   -----------------------------  
O1    3.5           NULL  
O2    13.4          Customer was very satisfied  
O3    100.0         Happy Customer.  
O4    10000.0       NULL  
```  
  
### <a name="e-specifying-tablename-in-the-with-clause"></a>E. WITH 절에 TableName 지정  
 이 예에서는 WITH 절에서 *SchemaDeclaration* 대신 *TableName*을 지정합니다. 이것은 원하는 구조를 가지고 있고 열 패턴 *ColPattern* 매개 변수는 필요하지 않은 테이블을 사용하는 경우에 유용합니다.  
  
 이 예의 XML 문서는 <`Customer`> 및 <`Order`> 요소로 이루어져 있습니다. OPENXML 문은 XML 문서로부터 세 열로 구성된 행 집합(**oid**, **date**및 **amount**)의 주문 정보를 검색합니다.  
  
 먼저 **sp_xml_preparedocument** 저장 프로시저가 문서 핸들을 얻기 위해 호출됩니다. 이 문서 핸들은 OPENXML에 전달됩니다.  
  
 OPENXML 문에서는 다음을 보여 줍니다.  
  
-   *rowpattern*(/root/Customer/Order)은 처리할 <`Order`> 노드를 식별합니다.  
  
-   WITH 절에는 *SchemaDeclaration* 이 없습니다. 그 대신 테이블 이름이 지정됩니다. 따라서 테이블 스키마가 행 집합 스키마로 사용됩니다.  
  
-   *flags* 매개 변수 값은 **1** 로 설정되어 특성 중심의 매핑을 나타냅니다. 따라서 *rowpattern*으로 식별되는 요소의 특성은 동일한 이름의 행 집합 열에 매핑됩니다.  
  
 그런 다음 SELECT 문은 OPENXML이 제공하는 행 집합의 모든 열을 검색합니다.  
  
```  
-- Create a test table. This table schema is used by OPENXML as the  
-- rowset schema.  
CREATE TABLE T1(oid char(5), date datetime, amount float)  
GO  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
-- Sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH T1  
EXEC sp_xml_removedocument @docHandle  
```  
  
 다음은 결과입니다.  
  
```  
oid   date                        amount  
----- --------------------------- ----------  
O1    1996-01-20 00:00:00.000     3.5  
O2    1997-04-30 00:00:00.000     13.4  
O3    1999-07-14 00:00:00.000     100.0  
O4    1996-01-20 00:00:00.000     10000.0  
```  
  
### <a name="f-obtaining-the-result-in-an-edge-table-format"></a>F. Edge 테이블 형식으로 결과 얻기  
 이 예제에서는 OPENXML 문에서 WITH 절이 지정되지 않습니다. 따라서 OPENXML이 생성하는 행 집합은 Edge 테이블 형식이 됩니다. SELECT 문은 Edge 테이블의 열을 모두 반환합니다.  
  
 이 예의 예제 XML 문서는 <`Customer`>, <`Order`> 및 <`OrderDetail`> 요소로 이루어져 있습니다.  
  
 먼저 **sp_xml_preparedocument** 저장 프로시저가 문서 핸들을 얻기 위해 호출됩니다. 이 문서 핸들은 OPENXML에 전달됩니다.  
  
 OPENXML 문에서는 다음을 보여 줍니다.  
  
-   *rowpattern*(/ROOT/Customer)은 처리할 <`Customer`> 노드를 식별합니다.  
  
-   WITH 절은 제공되지 않습니다. 따라서 OPENXML은 행 집합을 Edge 테이블 형식으로 반환합니다.  
  
 그런 다음 SELECT 문은 Edge 테이블의 모든 열을 검색합니다.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
SET @xmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer')  
  
EXEC sp_xml_removedocument @docHandle  
```  
  
 결과는 Edge 테이블로 반환됩니다. Edge 테이블에 대해 쿼리를 작성하여 다음과 같은 정보를 얻을 수 있습니다. 다음은 그 예입니다.  
  
-   다음은 문서의 **Customer** 노드 수를 반환하는 쿼리입니다. WITH 절이 지정되지 않았으므로 OPENXML은 Edge 테이블을 반환합니다. SELECT 문은 Edge 테이블을 쿼리합니다.  
  
    ```  
    SELECT count(*)  
    FROM OPENXML(@docHandle, '/')  
    WHERE localname = 'Customer'  
    ```  
  
-   다음 쿼리는 요소 유형의 XML 노드에 대한 로컬 이름을 반환합니다.  
  
    ```  
    SELECT distinct localname   
    FROM OPENXML(@docHandle, '/')   
    WHERE nodetype = 1   
    ORDER BY localname  
    ```  
  
### <a name="g-specifying-rowpattern-ending-with-an-attribute"></a>G. 특성으로 끝나는 rowpattern 지정  
 이 예의 XML 문서는 <`Customer`>, <`Order`> 및 <`OrderDetail`> 요소로 이루어져 있습니다. OPENXML 문은 XML 문서로부터 세 열로 구성된 행 집합(**ProductID**, **Quantity**및 **OrderID**)의 주문 정보를 검색합니다.  
  
 먼저 **sp_xml_preparedocument** 가 문서 핸들을 얻기 위해 호출됩니다. 이 문서 핸들은 OPENXML에 전달됩니다.  
  
 OPENXML 문에서는 다음을 보여 줍니다.  
  
-   *rowpattern*(/ROOT/Customer/Order/OrderDetail/\@ProductID)은 XML 특성 **ProductID**로 끝납니다. 결과 행 집합에서는 XML 문서에서 선택된 각 특성 노드에 대해 행이 만들어집니다.  
  
-   이 예제에는 *flags* 매개 변수가 지정되지 않습니다. 그 대신 *ColPattern* 매개 변수에 의해 매핑이 지정됩니다.  
  
 WITH 절에 있는 *SchemaDeclaration* 에서는 *ColPattern* 도 *ColName* 및 *ColType* 매개 변수로 지정됩니다. 선택 사항인 *ColPattern* 은 다음을 나타내기 위해 지정된 XPath 패턴입니다.  
  
-   행 집합의**ProdID**열에 대해 *ColPattern* 으로 지정된 XPath 패턴( **.** )은 컨텍스트 노드인 현재 노드를 식별합니다. 지정된 *rowpattern*에 따른 < **> 요소의** ProductID`OrderDetail` 특성입니다.  
  
-   행 집합에 있는 *Qty* 열에 대해 지정된 **ColPattern\@,** ../**Quantity**는 컨텍스트 노드 **ProductID>의 노드인 부모 <** >의 `OrderDetail`Quantity\< 특성을 식별합니다.  
  
-   이와 비슷하게 행 집합에 있는 *OID* 열에 지정된 **ColPattern\@,** ../../**OrderID**는 컨텍스트 노드에 대한 부모 노드의 부모 < **>의** OrderID`Order` 특성을 식별합니다. 부모 노드는 <`OrderDetail`>이고 컨텍스트 노드는 <`ProductID`>입니다.  
  
 그런 다음 SELECT 문은 OPENXML이 제공하는 행 집합의 모든 열을 검색합니다.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--Sample XML document  
SET @xmlDocument =N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail/@ProductID')  
       WITH ( ProdID  int '.',  
              Qty     int '../@Quantity',  
              OID     int '../../@OrderID')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 다음은 결과입니다.  
  
```  
ProdID      Qty         OID  
----------- ----------- -------   
11          12          10248  
42          10          10248  
72          3           10283  
```  
  
### <a name="h-specifying-an-xml-document-that-has-multiple-text-nodes"></a>H. 여러 개의 텍스트 노드가 있는 XML 문서 지정  
 XML 문서에 텍스트 노드가 여러 개 있는 경우 *text()* **ColPattern**을 포함한 SELECT 문은 전체가 아닌 첫 번째 텍스트 노드만 반환합니다. 다음은 그 예입니다.  
  
```  
DECLARE @h int  
EXEC sp_xml_preparedocument @h OUTPUT,  
         N'<root xmlns:a="urn:1">  
           <a:Elem abar="asdf">  
             T<a>a</a>U  
           </a:Elem>  
         </root>',  
         '<ns xmlns:b="urn:1" />'  
  
SELECT * FROM openxml(@h, '/root/b:Elem')  
      WITH (Col1 varchar(20) 'text()')  
EXEC sp_xml_removedocument @h  
```  
  
 SELECT 문은 **TaU** 가 아닌 **T**를 결과로 반환합니다.  
  
### <a name="i-specifying-the-xml-data-type-in-the-with-clause"></a>9\. WITH 절에서 xml 데이터 형식 지정  
 WITH 절에서 형식화된 열 및 형식화되지 않은 열을 모두 포함하여 **xml** 데이터 형식 열로 매핑된 열 패턴은 빈 시퀀스나 요소 시퀀스, 처리 명령, 텍스트 노드 및 주석을 반환해야 합니다. 데이터는 **xml** 데이터 형식으로 캐스팅됩니다.  
  
 다음 예에서 WITH 절에 있는 테이블 스키마 선언에는 **xml** 유형의 열이 포함됩니다.  
  
```  
DECLARE @h int  
DECLARE @x xml  
set @x = '<Root>  
  <row id="1"><lname>Duffy</lname>  
   <Address>  
            <Street>111 Maple</Street>  
            <City>Seattle</City>  
   </Address>  
  </row>  
  <row id="2"><lname>Wang</lname>  
   <Address>  
            <Street>222 Pine</Street>  
            <City>Bothell</City>  
   </Address>  
  </row>  
</Root>'  
  
EXEC sp_xml_preparedocument @h output, @x  
SELECT *  
FROM   OPENXML (@h, '/Root/row', 10)  
      WITH (id int '@id',  
  
            lname    varchar(30),  
            xmlname  xml 'lname',  
            OverFlow xml '@mp:xmltext')  
EXEC sp_xml_removedocument @h  
```  
  
 특히 **xml** 형식의 변수(\@x)를 **sp_xml_preparedocument()** 함수로 전달합니다.  
  
 다음은 결과입니다.  
  
```  
id  lname   xmlname                   OverFlow  
--- ------- ------------------------------ -------------------------------  
1   Duffy   <lname>Duffy</lname>  <row><Address>  
                                   <Street>111 Maple</Street>  
                                   <City>Seattle</City>  
                                  </Address></row>  
2   Wang    <lname>Wang</lname>   <row><Address>  
                                    <Street>222 Pine</Street>  
                                    <City>Bothell</City>  
                                   </Address></row>  
```  
  
 결과에서 다음을 확인하십시오.  
  
-   **varchar(30)** 유형의 **lname** 열에 대해 값이 해당 <`lname`> 요소로부터 검색됩니다.  
  
-   **xml** 유형의 **xmlname** 열에 대해 같은 이름의 요소가 해당 값으로 반환됩니다.  
  
-   플래그는 10으로 설정되어 있습니다. 10은 2 + 8을 의미하며, 여기서 2는 요소 중심 매핑이고 8은 사용되지 않은 XML 데이터만 WITH 절에 정의된 OverFlow 열에 추가되어야 함을 나타냅니다. 플래그를 2로 설정한 경우 전체 XML 문서가 WITH 절에 지정된 OverFlow 열에 복사됩니다.  
  
-   WITH 절에 있는 열이 형식화된 XML 열이고 XML 인스턴스가 스키마에 맞지 않는 경우 오류가 반환됩니다.  
  
### <a name="j-retrieving-individual-values-from-multivalued-attributes"></a>J. 다중 값 특성에서 개별 값 검색  
 XML 문서는 다중 값 특성을 가질 수 있습니다. 예를 들어 **IDREFS** 특성은 다중 값일 수 있습니다. XML 문서에서 다중 값 특성 값은 공간으로 값이 구별되는 문자열로 지정됩니다. 다음 XML 문서에서 **Student> 요소의** attends\< 특성과 **Class>의** attendedBy\< 특성은 다중 값을 갖고 있습니다. 다중 값 XML 특성에서 개별 값을 검색하고 데이터베이스의 독립된 행에서 각각의 값을 저장하려면 추가 작업이 필요합니다. 다음 예제에서는 처리 과정을 보여 줍니다.  
  
 이 예제 XML 문서는 다음 요소로 구성됩니다.  
  
-   \<Student>  
  
     **id** (학생 ID), **name**및 **attends** 특성입니다. **attends** 특성은 다중 값 특성입니다.  
  
-   \<Class>  
  
     **id** (학생 ID), **name**및 **attendedBy** 특성입니다. **attendedBy** 특성은 다중 값 특성입니다.  
  
 **Student>에 있는** attends\< 특성과 **Class>에 있는** attendedBy\< 특성은 Student 및 Class 테이블 간의 **m:n** 관계를 나타냅니다. 학생은 여러 개의 수업을 받을 수 있고 한 수업에는 여러 학생이 있을 수 있습니다.  
  
 이 문서를 조각으로 나눈 후 다음과 같이 데이터베이스에 저장한다고 가정하십시오.  
  
-   Students 테이블에 \<Student> 데이터를 저장합니다.  
  
-   Courses 테이블에 \<Class> 데이터를 저장합니다.  
  
-   CourseAttendence 테이블에 학생과 수업 간의 **m:n** 관계 데이터를 저장합니다. 값을 추출하려면 추가 작업이 필요합니다. 이 정보를 검색하고 테이블에 저장하려면 다음 저장 프로시저를 사용하십시오.  
  
    -   **Insert_Idrefs_Values**  
  
         CourseAttendence 테이블에 학과 ID와 학생 ID를 삽입합니다.  
  
    -   **Extract_idrefs_values**  
  
         \<Course> 요소에서 각각의 학생 ID를 추출합니다. Edge 테이블을 사용하여 이 값을 검색합니다.  
  
 다음 단계를 참조하십시오.  
  
```  
-- Create these tables:  
DROP TABLE CourseAttendance  
DROP TABLE Students  
DROP TABLE Courses  
GO  
CREATE TABLE Students(  
                id   varchar(5) primary key,  
                name varchar(30)  
                )  
GO  
CREATE TABLE Courses(  
               id       varchar(5) primary key,  
               name     varchar(30),  
               taughtBy varchar(5)  
)  
GO  
CREATE TABLE CourseAttendance(  
             id         varchar(5) references Courses(id),  
             attendedBy varchar(5) references Students(id),  
             constraint CourseAttendance_PK primary key (id, attendedBy)  
)  
go  
-- Create these stored procedures:  
DROP PROCEDURE f_idrefs  
GO  
CREATE PROCEDURE f_idrefs  
    @t      varchar(500),  
    @idtab  varchar(50),  
    @id     varchar(5)  
AS  
DECLARE @sp int  
DECLARE @att varchar(5)  
SET @sp = 0  
WHILE (LEN(@t) > 0)  
BEGIN   
    SET @sp = CHARINDEX(' ', @t+ ' ')  
    SET @att = LEFT(@t, @sp-1)  
    EXEC('INSERT INTO '+@idtab+' VALUES ('''+@id+''', '''+@att+''')')  
    SET @t = SUBSTRING(@t+ ' ', @sp+1, LEN(@t)+1-@sp)  
END  
Go  
  
DROP PROCEDURE fill_idrefs  
GO  
CREATE PROCEDURE fill_idrefs   
    @xmldoc     int,  
    @xpath      varchar(100),  
    @from       varchar(50),  
    @to         varchar(50),  
    @idtable    varchar(100)  
AS  
DECLARE @t varchar(500)  
DECLARE @id varchar(5)  
  
/* Temporary Edge table */  
SELECT *   
INTO #TempEdge   
FROM OPENXML(@xmldoc, @xpath)  
  
DECLARE fillidrefs_cursor CURSOR FOR  
    SELECT CAST(iv.text AS nvarchar(200)) AS id,  
           CAST(av.text AS nvarchar(4000)) AS refs  
    FROM   #TempEdge c, #TempEdge i,  
           #TempEdge iv, #TempEdge a, #TempEdge av  
    WHERE  c.id = i.parentid  
    AND    UPPER(i.localname) = UPPER(@from)  
    AND    i.id = iv.parentid  
    AND    c.id = a.parentid  
    AND    UPPER(a.localname) = UPPER(@to)  
    AND    a.id = av.parentid  
  
OPEN fillidrefs_cursor  
FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    IF (@@FETCH_STATUS <> -2)  
    BEGIN  
        execute f_idrefs @t, @idtable, @id  
    END  
    FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
END  
CLOSE fillidrefs_cursor  
DEALLOCATE fillidrefs_cursor  
Go  
-- This is the sample document that is shredded and the data is stored in the preceding tables.  
DECLARE @h int  
EXECUTE sp_xml_preparedocument @h OUTPUT, N'<Data>  
  <Student id = "s1" name = "Student1"  attends = "c1 c3 c6"  />  
  <Student id = "s2" name = "Student2"  attends = "c2 c4" />  
  <Student id = "s3" name = "Student3"  attends = "c2 c4 c6" />  
  <Student id = "s4" name = "Student4"  attends = "c1 c3 c5" />  
  <Student id = "s5" name = "Student5"  attends = "c1 c3 c5 c6" />  
  <Student id = "s6" name = "Student6" />  
  
  <Class id = "c1" name = "Intro to Programming"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c2" name = "Databases"   
         attendedBy = "s2 s3" />  
  <Class id = "c3" name = "Operating Systems"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c4" name = "Networks" attendedBy = "s2 s3" />  
  <Class id = "c5" name = "Algorithms and Graphs"   
         attendedBy =  "s4 s5"/>  
  <Class id = "c6" name = "Power and Pragmatism"   
         attendedBy = "s1 s3 s5" />  
</Data>'  
  
INSERT INTO Students SELECT * FROM OPENXML(@h, '//Student') WITH Students  
  
INSERT INTO Courses SELECT * FROM OPENXML(@h, '//Class') WITH Courses  
/* Using the edge table */  
EXECUTE fill_idrefs @h, '//Class', 'id', 'attendedby', 'CourseAttendance'  
  
SELECT * FROM Students  
SELECT * FROM Courses  
SELECT * FROM CourseAttendance  
  
EXECUTE sp_xml_removedocument @h  
```  
  
### <a name="k-retrieving-binary-from-base64-encoded-data-in-xml"></a>11. XML의 base64로 인코딩된 데이터에서 이진 검색  
 이진 데이터는 주로 base64 인코딩을 사용하여 XML에 포함됩니다. OPENXML을 사용하여 이 XML을 조각으로 나누면 base64로 인코딩된 데이터를 얻습니다. 이 예에서는 base64로 인코딩된 데이터를 다시 이진으로 변환하는 방법에 대해 설명합니다.  
  
-   예제 이진 데이터가 포함된 테이블을 만듭니다.  
  
-   FOR XML 쿼리 및 BINARY BASE64 옵션을 사용하여 이진 데이터가 base64로 인코딩된 XML을 생성합니다.  
  
-   OPENXML을 사용하여 XML을 조각으로 나눕니다. OPENXML에 의해 반환된 데이터는 base64 인코딩 데이터가 됩니다. 그런 다음 .value 함수를 호출하여 이를 다시 이진으로 변환합니다.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 varbinary(100))  
go  
-- Insert sample binary data  
INSERT T VALUES(1, 0x1234567890)   
go  
 -- Create test XML document that has base64 encoded binary data (use FOR XML query and specify BINARY BASE64 option)  
SELECT * FROM T  
FOR XML AUTO, BINARY BASE64  
go  
-- result  
-- <T Col1="1" Col2="EjRWeJA="/>  
  
-- Now shredd the sample XML using OPENXML.   
-- Call the .value function to convert   
-- the base64 encoded data returned by OPENXML to binary.  
DECLARE @h int ;  
EXEC sp_xml_preparedocument @h OUTPUT, '<T Col1="1" Col2="EjRWeJA="/>' ;  
SELECT Col1,   
CAST('<binary>' + Col2 + '</binary>' AS XML).value('.', 'varbinary(max)') AS BinaryCol   
FROM openxml(@h, '/T')   
WITH (Col1 integer, Col2 varchar(max)) ;  
EXEC sp_xml_removedocument @h ;  
GO  
```  
  
 다음은 결과입니다. 반환된 이진 데이터는 테이블 T에 있는 원래 이진 데이터입니다.  
  
```  
Col1        BinaryCol  
----------- ---------------------  
1           0x1234567890  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_xml_preparedocument&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)   
 [sp_xml_removedocument&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)   
 [OPENXML&#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML&#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
