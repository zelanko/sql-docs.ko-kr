---
title: "인라인 XSD 스키마 생성 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XSD schemas [SQL Server]
- XMLSCHEMA option
- schemas [SQL Server], XML
- XDR schemas
- FOR XML clause, inline XSD schema generation
- inline XSD schema generation [SQL Server]
- XMLDATA option
ms.assetid: 04b35145-1cca-45f4-9eb7-990abf2e647d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2b651f16b3bf5c43755aafa1c6b67cbef06fc1cd
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="generate-an-inline-xsd-schema"></a>인라인 XSD 스키마 생성
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
FOR XML 절에서는 쿼리가 쿼리 결과와 함께 인라인 스키마를 반환하도록 요청할 수 있습니다. XDR 스키마가 필요한 경우 FOR XML 절에 XMLDATA 키워드를 사용합니다. XSD 스키마가 필요한 경우 XMLSCHEMA 키워드를 사용합니다.  
  
 이 항목에서는 XMLSCHEMA 키워드에 대해 설명하고 결과 인라인 XSD 스키마의 구조를 설명합니다. 인라인 스키마를 요청하는 경우 다음과 같은 제한 사항이 있습니다.  
  
-   XMLSCHEMA는 RAW 및 AUTO 모드에서만 지정할 수 있으며 EXPLICIT 모드에서는 지정할 수 없습니다.  
  
-   중첩 FOR XML 쿼리에 TYPE 지시어를 지정하는 경우 쿼리 결과는 **xml** 형식이 되며 형식화되지 않은 XML 데이터의 인스턴스로 취급됩니다. 자세한 내용은 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)를 참조하세요.  
  
 FOR XML 쿼리에 XMLSCHEMA를 지정하는 경우 스키마와 XML 데이터를 모두 쿼리 결과로 수신합니다. 데이터의 각 최상위 요소는 기본 네임스페이스 선언을 사용하여 이전 스키마를 참조하며, 이 선언은 인라인 스키마의 대상 네임스페이스를 참조합니다.  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks2012].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<Production.ProductModel xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="1" Name="Classic Vest" />  
```  
  
 결과에는 XML 스키마와 XML 결과가 포함됩니다. 결과에서 <`ProductModel`> 최상위 요소는 기본 네임스페이스 선언 xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1"을 사용하여 스키마를 참조합니다.  
  
 결과의 스키마 부분에는 여러 네임스페이스를 기술하는 여러 스키마 문서가 포함될 수 있습니다. 최소한 다음 두 스키마 문서가 반환됩니다.  
  
-   한 스키마 문서는 **Sqltypes** 네임스페이스에 대한 문서이며 기본 SQL 유형이 반환되는 문서입니다.  
  
-   다른 스키마 문서는 FOR XML 쿼리 결과의 셰이프를 기술합니다.  
  
 또한 형식화된 **xml** 데이터 형식이 쿼리 결과에 포함된 경우 형식화된 해당 **xml** 데이터 형식과 연결된 스키마가 포함됩니다.  
  
 FOR XML 결과의 셰이프를 기술하는 스키마 문서의 대상 네임스페이스에는 고정 부분과 자동으로 증가하는 숫자 부분이 포함됩니다. 이 네임스페이스의 형식은 다음과 같으며 여기서 *n* 은 양의 정수입니다. 예를 들어 이전 쿼리에서 urn:schemas-microsoft-com:sql:SqlRowSet1은 대상 네임스페이스입니다.  
  
```  
urn:schemas-microsoft-com:sql:SqlRowSetn  
```  
  
 결과의 대상 네임스페이스는 실행될 때마다 내용이 변경되지 않는 것이 좋습니다. 예를 들어 결과 XML을 쿼리하는 경우 대상 네임스페이스에 변경된 내용이 있으면 해당 쿼리를 업데이트해야 합니다. FOR XML 절에 XMLSCHEMA 옵션을 추가할 때 선택적으로 대상 네임스페이스를 지정할 수 있습니다. 결과 XML에는 제공한 네임스페이스가 포함되며 쿼리 실행 회수에 관계없이 동일하게 유지됩니다.  
  
```  
SELECT ProductModelID, Name  
FROM   Production.ProductModel  
WHERE ProductModelID=1  
FOR XML AUTO, XMLSCHEMA ('MyURI')  
```  
  
## <a name="entity-elements"></a>엔터티 요소  
 쿼리 결과에 대해 생성된 XSD 스키마 구조의 세부 내용을 다루기 전에 엔터티 요소에 대해 먼저 이해해야 합니다.  
  
 FOR XML 쿼리에 의해 반환된 XML 데이터에 있는 엔터티 요소는 열이 아닌 테이블로부터 생성된 요소입니다. 예를 들어 다음 FOR XML 쿼리는 `Person` 데이터베이스에 있는 `AdventureWorks2012` 테이블의 연락처 정보를 반환합니다.  
  
```  
SELECT BusinessEntityID, FirstName  
FROM Person.Person  
WHERE BusinessEntityID = 1  
FOR XML AUTO, ELEMENTS  
```  
  
 다음은 결과입니다.  
  
 `<Person>`  
  
 `<BusinessEntityID>1</BusinessEntityID>`  
  
 `<FirstName>Ken</FirstName>`  
  
 `</Person>`  
  
 이 결과에서 <`Person`>은 엔터티 요소입니다. XML 결과에는 여러 엔터티 요소가 포함될 수 있으며 이러한 각 요소에는 인라인 XSD 스키마의 전역 선언이 포함됩니다. 예를 들어 다음 쿼리는 판매 주문 제목과 특정 주문에 대한 세부 정보를 검색합니다.  
  
```  
SELECT  SalesOrderHeader.SalesOrderID, ProductID, OrderQty  
FROM    Sales.SalesOrderHeader, Sales.SalesOrderDetail  
WHERE   SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
AND     SalesOrderHeader.SalesOrderID=5001  
FOR XML AUTO, ELEMENTS, XMLSCHEMA  
```  
  
 이 쿼리는 ELEMENTS 지시어를 지정하기 때문에 결과 XML은 요소 중심입니다. 이 쿼리는 또한 XMLSCHEMA 지시어를 지정합니다. 따라서 인라인 XSD 스키마가 반환됩니다. 다음은 결과입니다.  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="Sales.SalesOrderHeader">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="SalesOrderID" type="sqltypes:int" />`  
  
 `<xsd:element ref="schema:Sales.SalesOrderDetail" minOccurs="0" maxOccurs="unbounded" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `<xsd:element name="Sales.SalesOrderDetail">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="OrderQty" type="sqltypes:smallint" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   결과에서 <`SalesOrderHeader`> 및 <`SalesOrderDetail`>은 엔터티 요소입니다. 따라서 이러한 요소는 스키마에서 전역으로 선언됩니다. 즉, 선언이 <`Schema`> 요소 내부의 최상위에 표시됩니다.  
  
-   <`SalesOrderID`>, <`ProductID`> 및 <`OrderQty`>는 열로 매핑되므로 엔터티 요소가 아닙니다. 열 데이터는 ELEMENTS 지시어로 인해 XML의 요소로 반환됩니다. 이러한 데이터는 엔터티 요소의 복합 유형에 대한 로컬 요소로 매핑됩니다. ELEMENTS 지시어를 지정하지 않으면 `SalesOrderID`, `ProductID` 및 `OrderQty` 값이 해당 엔터티 요소의 복합 유형에 대한 로컬 특성으로 매핑됩니다.  
  
## <a name="attribute-name-clashes"></a>특성 이름 충돌  
 다음 설명에서는 `CustOrder` 및 `CustOrderDetail` 테이블을 기준으로 설명합니다. 다음 예제를 테스트하려면 아래와 같이 테이블을 만들고 자신의 예제 데이터를 추가합니다.  
  
```  
CREATE TABLE CustOrder (OrderID int primary key, CustomerID int)  
GO  
CREATE TABLE CustOrderDetail (OrderID int, ProductID int, Qty int)  
GO  
```  
  
 FOR XML에서 일부 경우에는 동일 이름을 사용하여 서로 다른 속성과 특성을 나타냅니다. 예를 들어 다음 특성 중심 RAW 모드 쿼리는 이름이 OrderID로 같은 두 개의 특성을 생성합니다. 이렇게 하면 오류가 발생합니다.  
  
```  
SELECT CustOrder.OrderID,   
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
FROM   dbo.CustOrder, dbo.CustOrderDetail  
WHERE  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA  
```  
  
 하지만 같은 이름의 두 요소를 사용할 수 있기 때문에 ELEMENTS 지시어를 추가하여 문제를 해결할 수 있습니다.  
  
```  
SELECT CustOrder.OrderID,  
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
from   dbo.CustOrder, dbo.CustOrderDetail  
where  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA, ELEMENTS  
```  
  
 다음은 결과입니다. 인라인 XSD 스키마에서 OrderID 요소는 두 번 정의됩니다. 선언 중 하나에서는 CustOrderDetail 테이블의 OrderID에 따라 minOccurs가 0으로 설정되어 있으며 다른 하나는 minOccurs가 기본적으로 1인 `CustOrder` 테이블의 OrderID 기본 키 열로 매핑됩니다.  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" />`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" minOccurs="0" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
## <a name="element-name-clashes"></a>요소 이름 충돌  
 FOR XML에서는 동일한 이름을 사용하여 두 개의 하위 요소를 나타낼 수 있습니다. 예를 들어 다음 쿼리는 제품의 ListPrice 및 DealerPrice 값을 검색하지만 두 열에 대해 Price라는 동일한 별칭을 지정합니다. 따라서 결과 행 집합에는 이름이 같은 두 열이 포함됩니다.  
  
### <a name="case-1-both-subelements-are-nonkey-columns-of-the-same-type-and-can-be-null"></a>사례 1: 두 하위 요소 모두 같은 유형의 키가 아닌 열이며 NULL일 수 있습니다.  
 다음 쿼리에서 두 하위 요소는 모두 같은 유형의 키가 아닌 열이며 NULL일 수 있습니다.  
  
```  
DROP TABLE T  
go  
CREATE TABLE T (ProductID int primary key, ListPrice money, DealerPrice money)  
go  
INSERT INTO T values (1, 1.25, null)  
go  
  
SELECT ProductID, ListPrice Price, DealerPrice Price  
FROM   T  
for    XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 이것은 생성된 해당 XML입니다. 인라인 XSD의 일부만 표시됩니다.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" minOccurs="0" maxOccurs="2" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `</row>`  
  
 인라인 XSD 스키마에서 다음을 유의하십시오.  
  
-   ListPrice 및 DealerPrice 모두 같은 `money` 유형이며 두 요소 모두 테이블에서 NULL일 수 있습니다. 따라서 두 요소는 결과 XML에 반환되지 않을 수도 있기 때문에 minOccurs=0 및 maxOccurs=2로 지정된 <`row`> 요소의 복합 유형 선언에는 <`Price`> 자식 요소가 하나만 있습니다.  
  
-   결과에서는 `DealerPrice` 값이 테이블에서 NULL이기 때문에 `ListPrice`만 <`Price`> 요소로 반환됩니다. `XSINIL` 매개 변수를 ELEMENTS 지시어로 추가하는 경우 DealerPrice에 해당하는 <`Price`> 요소에 대해 `xsi:nil` 값이 TRUE로 설정된 두 요소가 모두 수신됩니다. 또한 `nillable` 특성이 모두 TRUE로 설정된 인라인 XSD 스키마에서 <`row`> 복합 유형 정의에 있는 두 개의 <`Price`> 자식 요소가 수신됩니다. 다음은 결과의 일부입니다.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `<Price xsi:nil="true" />`  
  
 `</row>`  
  
### <a name="case-2-one-key-and-one-nonkey-column-of-the-same-type"></a>사례 2: 유형이 같은 하나의 키 열과 하나의 키가 아닌 열  
 다음 쿼리는 유형이 같은 하나의 키 열과 하나의 키가 아닌 열을 보여 줍니다.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 int, Col3 nvarchar(20))  
go  
INSERT INTO T VALUES (1, 1, 'test')  
go   
```  
  
 테이블 **T** 에 대한 다음 쿼리는 Col1 및 Col2에 대해 같은 별칭을 지정하며, 여기서 Col1은 기본 키이며 Null일 수 없고 Col2는 Null일 수 있습니다. 이 쿼리는 <`row`> 요소의 자식인 두 개의 형제 요소를 생성합니다.  
  
```  
SELECT Col1 as Col, Col2 as Col, Col3  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 다음은 결과입니다. 인라인 XSD 스키마의 조각만 표시됩니다.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="Col3" minOccurs="0">`  
  
 `<xsd:simpleType>`  
  
 `<xsd:restriction base="sqltypes:nvarchar"`  
  
 `sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth"`  
  
 `sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `</xsd:element>`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col>1</Col>`  
  
 `<Col>1</Col>`  
  
 `<Col3>test</Col3>`  
  
 `</row>`  
  
 인라인 XSD 스키마에서 Col2에 해당하는 <`Col`> 요소는 minOccurs가 0으로 설정됩니다.  
  
### <a name="case-3-both-elements-of-different-types-and-corresponding-columns-can-be-null"></a>사례 3: 유형이 다른 요소와 해당 열은 모두 NULL일 수 있습니다.  
 다음 쿼리는 사례 2에 표시된 예제 테이블에 대해 지정됩니다.  
  
```  
SELECT Col1, Col2 as Col, Col3 as Col  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 다음 쿼리에서 Col2 및 Col3에는 같은 별칭이 지정됩니다. 이 쿼리는 이름이 같고 결과에서 모두 <`raw`> 요소의 자식인 두 개의 형제 요소를 생성합니다. 이 열은 모두 유형이 다르며 모두 NULL일 수 있습니다. 다음은 결과입니다. 인라인 XSD 스키마의 일부만 표시됩니다.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:simpleType name="Col1">`  
  
 `<xsd:restriction base="sqltypes:int" />`  
  
 `</xsd:simpleType>`  
  
 `<xsd:simpleType name="Col2">`  
  
 `<xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col1" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" minOccurs="0" maxOccurs="2" type="xsd:anySimpleType" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col1>1</Col1>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col1">1</Col>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col2">test</Col>`  
  
 `</row>`  
  
 인라인 XSD 스키마에서 다음을 유의하십시오.  
  
-   Col2 및 Col3이 모두 NULL일 수 있기 때문에 <`Col`> 요소 선언은 minOccurs를 0으로 설정하고 maxOccurs를 2로 설정합니다.  
  
-   두 <`Col`> 요소가 모두 형제이기 때문에 스키마에는 하나의 요소 선언이 있습니다. 두 요소 모두 간단한 유형이지만 또한 두 요소의 유형이 모두 다르기 때문에 스키마의 요소 유형은 `xsd:anySimpleType`입니다. 결과에서 각 인스턴스 유형은 `xsi:type` 특성에 의해 식별됩니다.  
  
-   결과에서 <`Col`> 요소의 각 인스턴스는 `xsi:type` 특성을 사용하여 해당 인스턴스 유형을 참조합니다.  
  
  
