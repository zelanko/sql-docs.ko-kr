---
title: OPENXML (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ff4578d88cdb76468d261843c36043ef4696d92c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="openxml-transact-sql"></a>OPENXML(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OPENXML은 XML 문서에 대한 행 집합 뷰를 제공합니다. OPENXML이 행 집합 공급자이므로 테이블, 뷰 또는 OPENROWSET 함수 등의 행 집합 공급자가 있을 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 OPENXML을 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
## <a name="arguments"></a>인수  
 *idoc*  
 XML 문서의 내부 표시 문서 핸들입니다. 호출 하 여 만든 XML 문서의 내부 표현을 **sp_xml_preparedocument**합니다.  
  
 *rowpattern*  
 노드를 식별 하는 데 사용 하는 XPath 패턴은 (해당 핸들을 전달 하는 XML 문서에는 *idoc* 매개 변수) 행으로 처리 합니다.  
  
 *플래그*  
 XML 데이터와 관계형 행 집합 사이에 사용해야 하는 매핑과 남는 열을 채우는 방법을 나타냅니다. *플래그* 선택적 입력된 매개 변수 이며 다음 값 중 하나일 수 있습니다.  
  
|바이트 값|Description|  
|----------------|-----------------|  
|**0**|기본적으로 **특성 중심** 매핑.|  
|**1**|사용 하 여는 **특성 중심** 매핑. XML_ELEMENTS와 결합할 수 있습니다. 이 경우 **특성 중심** 매핑이 먼저 적용 한 다음 **요소 중심** 와 아직 처리 되지 않은 모든 열에 대 한 매핑이 적용 됩니다.|  
|**2**|사용 하 여 **요소 중심** 매핑. XML_ATTRIBUTES와 결합할 수 있습니다. 이 경우 **특성 중심** 매핑이 먼저 적용 한 다음 **요소 중심** 처리 하지 않은 모든 열에 대 한 매핑이 적용 됩니다.|  
|**8**|XML_ATTRIBUTES 또는 XML_ELEMENTS와 결합(논리적 OR 연산을 수행)할 수 있습니다. 검색 상황에서이 플래그 오버플로 속성에 소비 된 데이터를 복사 하지 해야 함을 나타냅니다  **@mp:xmltext** 합니다.|  
  
 *SchemaDeclaration*  
 폼의 스키마 정의: *ColName**ColType* [*ColPattern* | *메타 속성*] [**** *ColNameColType* [*ColPattern* | *메타 속성*]...]  
  
 *ColName*  
 행 집합의 열 이름입니다.  
  
 *ColType*  
 행 집합에 있는 열의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다. 기본 열 형식이 다른 경우 **xml** 형식 강제 변환이 특성의 데이터 형식 발생 합니다.  
  
 *ColPattern*  
 선택 사항이며 XML 노드를 열에 매핑하는 방법을 설명하는 일반 XPath 패턴입니다. 경우 *ColPattern* 를 지정 하지 않으면 기본 매핑이 (**특성 중심** 또는 **요소 중심** 에 지정 된 대로 매핑 *플래그* ) 수행 합니다.  
  
 으로 지정 된 XPath 패턴 *ColPattern* 매핑 특성을 지정 하는 데 사용 됩니다 (의 경우 **특성 중심** 및 **요소 중심** 매핑)는 로 표시 된 기본 매핑을 개선 하거나 덮어쓰도록 *플래그*합니다.  
  
 으로 지정 된 일반 XPath 패턴 *ColPattern* 은 메타 속성도 지원 합니다.  
  
 *메타 속성*  
 OPENXML이 제공하는 메타 속성 중 하나입니다. 경우 *메타 속성* 지정, 열에 메타 속성이 제공 하는 정보를 포함 합니다. 메타 속성을 통해 상대적 위치 및 네임스페이스 정보 등 XML 노드에 대한 정보를 추출할 수 있습니다. 텍스트 형태로 표시되는 것보다 많은 정보를 제공합니다.  
  
 *테이블 이름*  
 제공할 수 있는 테이블 이름입니다 (대신 *SchemaDeclaration*) 하는 경우 원하는 스키마가 있는 테이블이 이미 존재 하 고 열 패턴은 필수입니다.  
  
## <a name="remarks"></a>주의  
 WITH 절 중 하나를 사용 하 여 행 집합 서식이 (및 필요에 따라 추가 매핑 정보)을 제공 *SchemaDeclaration* 기존를 지정 하거나 *TableName*합니다. 선택적인 WITH 절을 지정 하지 않으면 결과에서 반환 됩니다는 **가장자리** 테이블 형식입니다. edge 테이블은 세부 수준의 XML 문서 구조(예: 요소/특성 이름, 문서 계층 구조, 네임스페이스, PI 등)를 단일 테이블로 표시합니다.  
  
 다음 표에서 설명의 구조는 **가장자리** 테이블입니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|문서 노드의 고유 ID입니다.<br /><br /> 루트 요소의 ID 값은 0입니다. 음수 ID 값은 예약된 값입니다.|  
|**parentid**|**bigint**|노드의 부모를 나타냅니다. 이 ID가 나타내는 부모가 반드시 부모 요소일 필요는 없지만 해당 노드는 이 ID가 나타내는 부모 노드의 NodeType에 종속됩니다. 예를 들어 노드가 텍스트 노드인 경우 해당 부모는 특성 노드일 수 있습니다.<br /><br /> 노드가 XML 문서의 최상위 수준에 있으면 해당 **ParentID** 는 NULL입니다.|  
|**nodetype**|**int**|노드 유형을 나타냅니다. XML DOM 노드 유형 번호에 해당하는 정수입니다.<br /><br /> 노드 유형은 다음과 같습니다.<br /><br /> 1 = 요소 노드<br /><br /> 2 = 특성 노드<br /><br /> 3 = 텍스트 노드|  
|**localname**|**nvarchar**|요소 또는 특성의 로컬 이름을 지정합니다. DOM 개체에 이름이 없는 경우에는 NULL입니다.|  
|**prefix**|**nvarchar**|노드 이름의 네임스페이스 접두사입니다.|  
|**namespaceuri**|**nvarchar**|노드의 네임스페이스 URI입니다. 값이 NULL이면 네임스페이스가 없는 것입니다.|  
|**datatype**|**nvarchar**|요소 또는 특성 행의 실제 데이터 형식이며 데이터 형식이 아닐 경우에는 NULL입니다. 데이터 형식은 인라인 DTD 또는 인라인 스키마로부터 추정할 수 있습니다.|  
|**prev**|**bigint**|이전의 형제 요소에 대한 XML ID입니다. 바로 이전의 형제가 없으면 NULL입니다.|  
|**text**|**ntext**|특성 값 또는 텍스트 형식의 요소 내용이 포함 (경우 NULL이 고 **가장자리** 테이블 항목 값이 필요 하지 않습니다).|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>1. 단순 SELECT 문에 OPENXML 사용  
 다음 예는 `sp_xml_preparedocument`를 사용하여 XML 이미지의 내부 표현을 만듭니다. `SELECT` 행 집합 공급자를 사용하는 `OPENXML` 문은 XML 문서의 내부 표현에 대해 실행됩니다.  
  
 *플래그* 값으로 설정 되어 `1`합니다. 이 나타냅니다 **특성 중심** 매핑. 따라서 XML 특성이 행 집합의 열에 매핑됩니다. *rowpattern* 로 지정 된 `/ROOT/Customer` 식별 된 `<Customers>` 처리 될 노드를 합니다.  
  
 선택적 *ColPattern* XML 특성 이름과 일치 하는 열 이름이 없으므로 (열 패턴) 매개 변수를 지정 하지 않으면 합니다.  
  
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
  
 하는 경우 동일한 `SELECT` 문이 실행 되는 *플래그* 로 설정 `2`한다는 표시 이므로 **요소 중심** 의 값을 매핑할 `CustomerID` 및 `ContactName` 둘 다에 대해는 명명 된 요소가 있기 때문에 XML 문서에는 고객 NULL로 반환 됩니다 `CustomerID` 또는 `ContactName` XML 문서에 있습니다.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>2. 열과 XML 특성 간의 매핑을 위해 ColPattern 지정  
 다음 쿼리는 XML 문서에서 고객 ID, 주문 날짜, 제품 ID, 수량 특성을 반환합니다. *rowpattern* 식별 된 `<OrderDetails>` 요소입니다. `ProductID` 및 `Quantity`는 `<OrderDetails>` 요소의 특성입니다. 그러나 `OrderID`, `CustomerID` 및 `OrderDate`는 부모 요소 `<Orders>`의 특성입니다.  
  
 선택적 *ColPattern* 지정 됩니다. 이에 따라 다음과 같은 결과가 나타납니다.  
  
-   `OrderID`, `CustomerID`, 및 `OrderDate` 의해 식별 된 노드는 부모 특성에 대 한 행 집합 맵에서 *rowpattern* XML 문서에 있습니다.  
  
-   `ProdID` 행 집합의 열에 매핑되는 `ProductID` 특성을 및 `Qty` 행 집합의 열에 매핑되는 `Quantity` 에서 식별 된 노드는 특성 *rowpattern*합니다.  
  
 하지만 **요소 중심** 의해 매핑이 지정는 *플래그* 매개 변수에서 지정 된 매핑은 *ColPattern* 이 매핑을 덮어 씁니다.  
  
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
  
### <a name="c-obtaining-results-in-an-edge-table-format"></a>3. edge 테이블 형식으로 결과 얻기  
 다음 예의 예제 XML 문서는 `<Customers>`, `<Orders>`, `<Order_0020_Details>` 요소로 구성됩니다. 첫째, **sp_xml_preparedocument** 문서 핸들을 얻기 위해 호출 됩니다. 이 문서 핸들은 `OPENXML`에 전달됩니다.  
  
 에 `OPENXML` 문는 *rowpattern* (`/ROOT/Customers`) 식별는 `<Customers>` 노드를 처리 합니다. WITH 절은 제공 되지 않았으므로 `OPENXML` 에서 행 집합을 반환 된 **가장자리** 테이블 형식입니다.  
  
 마지막으로 `SELECT` 문은 검색의 모든 열은 **가장자리** 테이블입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [예제: OPENXML 사용](../../relational-databases/xml/examples-using-openxml.md)  
  
  

