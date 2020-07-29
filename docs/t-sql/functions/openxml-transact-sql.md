---
title: OPENXML(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENXML_TSQL
- OPENXML
dev_langs:
- TSQL
helpviewer_keywords:
- OPENXML statement
- rowsets [SQL Server], XML documents
- XML [SQL Server], rowset views
ms.assetid: 8088b114-7d01-435a-8e0d-b81abacc86d6
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: ca8ececca1e40762aa386ba05a53bdf8a1932090
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112396"
---
# <a name="openxml-transact-sql"></a>OPENXML(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  OPENXML은 XML 문서에 대한 행 집합 뷰를 제공합니다. OPENXML이 행 집합 공급자이므로 테이블, 뷰 또는 OPENROWSET 함수 등의 행 집합 공급자가 있을 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 OPENXML을 사용할 수 있습니다.  
  
 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *idoc*  
 XML 문서의 내부 표시 문서 핸들입니다. XML 문서의 내부 표현은 **sp_xml_preparedocument**를 호출하여 만듭니다.  
  
 *rowpattern*  
 행으로 처리될 노드를 식별하는 데 사용되는 XPath 패턴입니다. 이 노드는 *idoc* 매개 변수로 핸들이 전달되는 XML 문서에서 가져옵니다.
  
 *flags*  
 XML 데이터와 관계형 행 집합 사이에 사용되는 매핑과 남는 열을 채우는 방법을 나타냅니다. *flags*는 선택적 입력 매개 변수이며 다음 값 중 하나일 수 있습니다.  
  
|바이트 값|Description|  
|----------------|-----------------|  
|**0**|기본적으로 **특성 중심** 매핑을 사용합니다.|  
|**1**|**특성 중심** 매핑을 사용합니다. XML_ELEMENTS와 결합할 수 있습니다. 이 경우 **특성 중심** 매핑이 먼저 적용됩니다. 그런 다음, **요소 중심** 매핑이 나머지 열에 적용됩니다.|  
|**2**|**요소 중심** 매핑을 사용합니다. XML_ATTRIBUTES와 결합할 수 있습니다. 이 경우 **특성 중심** 매핑이 먼저 적용됩니다. 그런 다음, **요소 중심** 매핑이 나머지 열에 적용됩니다.|  
|**8**|XML_ATTRIBUTES 또는 XML_ELEMENTS와 결합(논리적 OR 연산을 수행)할 수 있습니다. 검색 상황에서 이 플래그는 소비된 데이터를 오버플로 속성인 **\@mp:xmltext**로 복사할 수 없음을 나타냅니다.|  
  
 _SchemaDeclaration_  
 _ColName_*ColType* [_ColPattern_ | _MetaProperty_] [ **,** _ColNameColType_ [_ColPattern_ | _MetaProperty_]...] 형식의 스키마 정의입니다.  
  
 _ColName_  
 행 집합의 열 이름입니다.  
  
 *ColType*  
 행 집합에 있는 열의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다. 열 형식이 특성의 기본 **xml** 데이터 형식과 다른 경우 형식 강제 변환이 발생합니다.  
  
 *ColPattern*  
 선택 사항이며 XML 노드를 열에 매핑하는 방법을 설명하는 일반 XPath 패턴입니다. *ColPattern*을 지정하지 않으면 기본 매핑(**flags**에 지정된 대로 **특성 중심** 또는 *요소 중심* 매핑)이 수행됩니다.  
  
 *ColPattern*으로 지정된 XPath 패턴은 **flags**로 표시된 기본 매핑을 덮어쓰거나 향상시키도록 매핑의 특수한 특성(**특성 중심** 및 *요소 중심* 매핑의 경우)을 지정하는 데 사용합니다.  
  
 *ColPattern*으로 지정된 일반 XPath 패턴은 메타 속성도 지원합니다.  
  
 *MetaProperty*  
 OPENXML이 제공하는 메타 속성 중 하나입니다. *MetaProperty*가 지정되면 메타 속성이 제공하는 정보가 열에 포함됩니다. 메타 속성을 통해 상대적 위치 및 네임스페이스 정보 등 XML 노드에 대한 정보를 추출할 수 있습니다. 이 메타 속성은 텍스트로 표시되는 것보다 더 많은 정보를 제공합니다.  
  
 *TableName*  
 원하는 스키마가 있는 테이블이 이미 있고 열 패턴이 필요하지 않은 경우 *SchemaDeclaration* 대신 지정할 수 있는 테이블 이름입니다.  
  
## <a name="remarks"></a>설명  
 WITH 절은 *SchemaDeclaration*을 사용하거나 기존 *TableName*을 지정하여 행 집합 형식(및 필요한 경우 추가 매핑 정보)을 제공합니다. 선택적 WITH 절을 지정하지 않으면 결과가 **edge** 테이블 형식으로 반환됩니다. edge 테이블은 세부 수준의 XML 문서 구조(예: 요소/특성 이름, 문서 계층 구조, 네임스페이스, PI 등)를 단일 테이블로 표시합니다.  
  
 다음 표에서는 **edge** 테이블의 구조에 대해 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|문서 노드의 고유 ID입니다.<br /><br /> 루트 요소의 ID 값은 0입니다. 음수 ID 값은 예약된 값입니다.|  
|**parentid**|**bigint**|노드의 부모를 나타냅니다. 이 ID가 나타내는 부모가 반드시 부모 요소일 필요는 없지만 해당 노드는 이 ID가 나타내는 부모 노드의 NodeType에 종속됩니다. 예를 들어 노드가 텍스트 노드인 경우 해당 부모는 특성 노드일 수 있습니다.<br /><br /> 노드가 XML 문서의 최상위 수준에 있으면 해당 **ParentID** 는 NULL입니다.|  
|**nodetype**|**int**|노드 유형을 나타냅니다. XML DOM 노드 유형 번호에 해당하는 정수입니다.<br /><br /> 노드 유형은 다음과 같습니다.<br /><br /> 1 = 요소 노드<br /><br /> 2 = 특성 노드<br /><br /> 3 = 텍스트 노드|  
|**localname**|**nvarchar**|요소 또는 특성의 로컬 이름을 지정합니다. DOM 개체에 이름이 없는 경우에는 NULL입니다.|  
|**prefix**|**nvarchar**|노드 이름의 네임스페이스 접두사입니다.|  
|**namespaceuri**|**nvarchar**|노드의 네임스페이스 URI입니다. 값이 NULL이면 네임스페이스가 없는 것입니다.|  
|**datatype**|**nvarchar**|요소 또는 특성 행의 실제 데이터 형식이며 데이터 형식이 아닐 경우에는 NULL입니다. 데이터 형식은 인라인 DTD 또는 인라인 스키마로부터 추정할 수 있습니다.|  
|**prev**|**bigint**|이전의 형제 요소에 대한 XML ID입니다. 바로 이전의 형제가 없으면 NULL입니다.|  
|**text**|**ntext**|텍스트 형식의 특성 값 또는 요소 내용을 포함합니다. **edge** 테이블 항목에 값이 필요하지 않은 경우에는 NULL입니다.|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. 단순 SELECT 문에 OPENXML 사용  
 다음 예는 `sp_xml_preparedocument`를 사용하여 XML 이미지의 내부 표현을 만듭니다. `SELECT` 행 집합 공급자를 사용하는 `OPENXML` 문은 XML 문서의 내부 표현에 대해 실행됩니다.  
  
 *flag* 값이 `1`로 설정됩니다. 이 값은 **특성 중심** 매핑을 나타냅니다. 따라서 XML 특성이 행 집합의 열에 매핑됩니다. *로 지정된* rowpattern`/ROOT/Customer`은 처리할 `<Customers>` 노드를 식별합니다.  
  
 열 이름이 XML 특성 이름과 일치하므로 선택적인 *ColPattern*(열 패턴) 매개 변수는 지정되지 않습니다.  
  
 `OPENXML` 행 집합 공급자는 `CustomerID` 문이 필수 열(이 경우에는 모든 열)을 검색하는 두 열(`ContactName`와 `SELECT`)로 된 행 집합을 만듭니다.  
  
```  
DECLARE @idoc int, @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;  
-- Execute a SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customer',1)  
            WITH (CustomerID  varchar(10),  
                  ContactName varchar(20));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 `SELECT`flags*가* 로 설정되고 `2`요소 중심**매핑을 나타내는 동일한** 문이 실행되면, XML 문서에 `CustomerID` 또는 `ContactName` 이름의 요소가 없으므로 XML 문서의 두 고객 모두에 대한 `CustomerID` 및 `ContactName`의 값이 NULL로 반환됩니다.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. 열과 XML 특성 간의 매핑을 위해 ColPattern 지정  
 다음 쿼리는 XML 문서에서 고객 ID, 주문 날짜, 제품 ID, 수량 특성을 반환합니다. *rowpattern*은 `<OrderDetails>` 요소를 식별합니다. `ProductID` 및 `Quantity`는 `<OrderDetails>` 요소의 특성입니다. 그러나 `OrderID`, `CustomerID` 및 `OrderDate`는 부모 요소 `<Orders>`의 특성입니다.  
  
 선택적 *ColPattern*이 지정되는 매핑은 다음과 같습니다.  
  
-   행 집합의 `OrderID`, `CustomerID` 및 `OrderDate`는 XML 문서에서 *rowpattern*으로 식별된 노드의 부모 특성에 매핑됩니다.  
  
-   행 집합의 `ProdID` 열은 `ProductID` 특성에 매핑되며, 행 집합의 `Qty` 열은 `Quantity`rowpattern*으로 식별된 노드의*  특성에 매핑됩니다.  
  
 **요소 중심** 매핑이 *flags* 매개 변수에 지정되더라도 *ColPattern*에 지정된 매핑이 이 매핑을 덮어씁니다.  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">v  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';   
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT stmt using OPENXML rowset provider  
SELECT *  
FROM   OPENXML (@idoc, '/ROOT/Customer/Order/OrderDetail',2)   
         WITH (OrderID       int         '../@OrderID',
               CustomerID  varchar(10) '../@CustomerID',
               OrderDate   datetime    '../@OrderDate',
               ProdID      int         '@ProductID',
               Qty         int         '@Quantity');
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
OrderID CustomerID           OrderDate                 ProdID    Qty  
------------------------------------------------------------------------  
10248      VINET       1996-07-04 00:00:00.000   11      12  
10248      VINET       1996-07-04 00:00:00.000   42      10  
10283      LILAS       1996-08-16 00:00:00.000   72      3  
```  
  
### <a name="c-obtaining-results-in-an-edge-table-format"></a>C. edge 테이블 형식으로 결과 얻기  
 다음 예의 예제 XML 문서는 `<Customers>`, `<Orders>`, `<Order_0020_Details>` 요소로 구성됩니다. 먼저 문서 핸들을 얻기 위해 **sp_xml_preparedocument**를 호출합니다. 이 문서 핸들은 `OPENXML`에 전달됩니다.  
  
 `OPENXML` 문에서 *rowpattern*(`/ROOT/Customers`)은 처리할 `<Customers>` 노드를 식별합니다. WITH 절이 제공되지 않았으므로 `OPENXML`에서 **edge** 테이블 형식의 행 집합을 반환합니다.  
  
 마지막으로 `SELECT` 문은 **edge** 테이블의 모든 열을 검색합니다.  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customers CustomerID="VINET" ContactName="Paul Henriot">  
   <Orders CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <Order_x0020_Details OrderID="10248" ProductID="11" Quantity="12"/>  
      <Order_x0020_Details OrderID="10248" ProductID="42" Quantity="10"/>  
   </Orders>  
</Customers>  
<Customers CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Orders CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <Order_x0020_Details OrderID="10283" ProductID="72" Quantity="3"/>  
   </Orders>  
</Customers>  
</ROOT>';  
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customers')   
EXEC sp_xml_removedocument @idoc;  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [예제: OPENXML 사용](../../relational-databases/xml/examples-using-openxml.md)  
  
