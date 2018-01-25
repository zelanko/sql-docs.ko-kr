---
title: "nodes () 메서드 (xml 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- nodes() method
- nodes method
ms.assetid: 7267fe1b-2e34-4213-8bbf-1c953822446c
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: f75f08164b84e803a6a54d039a09cf481a1886e9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nodes-method-xml-data-type"></a>nodes() 메서드(xml 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **nodes ()** 메서드는 조각으로 나눌 때 유용 프로그램 **xml** 데이터 형식 인스턴스를 관계형 데이터입니다. 이 메서드를 사용하면 새로운 행으로 매핑되는 열을 식별할 수 있습니다.  
  
 모든 **xml** 데이터 형식 인스턴스에 암시적으로 제공 된 컨텍스트 노드. 열 또는 변수에 저장된 XML 인스턴스의 경우 이 노드는 문서 노드입니다. 문서 노드는 암시적 노드 맨 위에 있는 모든 **xml** 데이터 형식 인스턴스가 있습니다.  
  
 결과 **nodes ()** 메서드는 원래 XML 인스턴스의 논리적 복사본이 포함 된 행 집합입니다. 이러한 논리적 복사본에서 모든 행 인스턴스의 컨텍스트 노드는 쿼리 식으로 식별된 노드 중 하나로 설정되므로 이후의 쿼리에서는 이러한 컨텍스트 노드에 따라 상대적으로 탐색할 수 있습니다.  
  
 행 집합에서 여러 값을 검색할 수 있습니다. 예를 들어 적용할 수 있습니다는 **value ()** 메서드를 반환한 행 집합이 **nodes ()** 원래 XML 인스턴스에서 여러 값을 검색 합니다. **value ()** XML 인스턴스에 적용 될 경우이 메서드는 하나의 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
nodes (XQuery) as Table(Column)  
```  
  
## <a name="arguments"></a>인수  
 *XQuery*  
 문자열 리터럴인 XQuery 식입니다. 쿼리 식이 노드를 생성하는 경우 이렇게 생성된 노드는 결과 행 집합에 제공됩니다. 쿼리 식에 의해 빈 시퀀스가 생성되는 경우 빈 행 집합이 반환됩니다. 쿼리 식이 노드 대신 원자 값이 들어 있는 시퀀스를 정적으로 생성하는 경우 정적 오류가 발생합니다.  
  
 *테이블*(*열*)  
 결과 행 집합에 대한 테이블 이름 및 열 이름입니다.  
  
## <a name="remarks"></a>주의  
 예를 들어 다음과 같은 테이블을 가정해 보세요.  
  
```  
T (ProductModelID int, Instructions xml)  
```  
  
 다음 제조 지침 문서가 이 테이블에 저장되어 있고 한 조각만 표시되어 있습니다. 문서에는 3개의 제조 위치가 있습니다.  
  
```  
<root>  
  <Location LocationID="10"...>  
     <step>...</step>  
     <step>...</step>  
      ...  
  </Location>  
  <Location LocationID="20" ...>  
       ...  
  </Location>  
  <Location LocationID="30" ...>  
       ...  
  </Location>  
</root>  
```  
  
 쿼리 식 `nodes()`에서 `/root/Location` 메서드를 호출하면 각각 원래 XML 문서의 논리적 복사본이 들어 있고 컨텍스트 항목이 `<Location>` 노드 중 하나로 설정된 3개의 행이 포함된 행 집합이 반환됩니다.  
  
```  
Product  
ModelID      Instructions  
----------------------------------  
1       <root>  
             <Location LocationID="20" ... />  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
             <Location LocationID="20" ... />  
             </root>  
```  
  
 사용 하 여이 행 집합을 쿼리 한 다음 **xml** 데이터 형식 메서드. 다음 쿼리는 생성된 각 행에 대한 컨텍스트 항목의 하위 트리를 추출합니다.  
  
```  
SELECT T2.Loc.query('.')  
FROM   T  
CROSS APPLY Instructions.nodes('/root/Location') as T2(Loc)   
```  
  
 다음은 결과입니다.  
  
```  
ProductModelID  Instructions  
----------------------------------  
1        <Location LocationID="10" ... />  
1        <Location LocationID="20" ... />  
1        <Location LocationID="30" .../>  
```  
  
 반환된 행 집합에는 유형 정보가 유지 관리됩니다. 적용할 수 있습니다 **xml** 와 같은 데이터 형식 메서드의 **query ()**, **value ()**, **exist ()**, 및 **nodes ()** 결과에 대 한 **nodes ()** 메서드. 그러나 적용할 수 없습니다는 **modify ()** XML 인스턴스를 수정 하는 메서드.  
  
 또한 행 집합의 컨텍스트 노드는 구체화할 수 없습니다. 즉, 이 노드를 SELECT 문에서 사용할 수 없습니다. 하지만 IS NULL 및 COUNT(*)에서는 사용할 수 있습니다.  
  
 사용 하는 시나리오는 **nodes ()** 사용 하는 방법과 동일 [OPENXML &#40; Transact SQL &#41; ](../../t-sql/functions/openxml-transact-sql.md). 이 메서드는 XML에 대한 행 집합 뷰를 제공합니다. 그러나 사용 하는 경우 커서를 사용할 필요가 없습니다는 **nodes ()** 메서드 XML 문서의 여러 행을 포함 하는 테이블입니다.  
  
 행 집합에서 반환 하는 **nodes ()** 방법은 명명 되지 않은 행 집합입니다. 따라서 별칭을 사용하여 명시적으로 이름을 지정해야 합니다.  
  
 **nodes ()** 함수는 사용자 정의 함수의 결과에 직접 적용할 수 없습니다. 사용 하는 **nodes ()** 함수는 스칼라 사용자 정의 함수의 결과 함께 사용자 정의 함수의 결과 변수에 할당 하거나 파생된 테이블을 사용 하 여 사용자 정의 함수에 열 별칭을 할당 하려면 값을 반환 하 고 별칭에서 선택 하려면 CROSS APPLY를 사용 합니다.  
  
 다음 예에서는 `CROSS APPLY`를 사용하여 사용자 정의 함수의 결과에서 선택하는 한 가지 방법을 보여 줍니다.  
  
```  
USE AdventureWorks;  
GO  
  
CREATE FUNCTION XTest()  
RETURNS xml  
AS  
BEGIN  
RETURN '<document/>';  
END;  
GO  
  
SELECT A2.B.query('.')  
FROM  
(SELECT dbo.XTest()) AS A1(X)   
CROSS APPLY X.nodes('.') A2(B);  
GO  
  
DROP FUNCTION XTest;  
GO  
```  
  
## <a name="examples"></a>예  
  
### <a name="using-nodes-method-against-a-variable-of-xml-type"></a>1. xml 형식의 변수에 대해 nodes() 메서드 사용  
 다음 예에는 <`Root`> 최상위 요소 하나와 <`row`> 자식 요소 3개가 있는 XML 문서가 있습니다. 이 쿼리는 `nodes()` 메서드를 사용하여 각 <`row`> 요소에 대해 하나의 개별 컨텍스트 노드를 설정합니다. `nodes()` 메서드는 3개의 행이 포함된 행 집합을 반환합니다. 각 행에는 원래 문서에서 서로 다른 <`row`> 요소를 식별하는 각 컨텍스트 노드와 함께 원래 XML의 논리적 복사본이 들어 있습니다.  
  
 그런 다음 쿼리는 각 행에서 컨텍스트 노드를 반환합니다.  
  
```  
DECLARE @x xml   
SET @x='<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>'  
SELECT T.c.query('.') AS result  
FROM   @x.nodes('/Root/row') T(c)  
GO  
```  
  
 다음은 결과입니다. 이 예에서 쿼리 메서드는 컨텍스트 항목과 해당 내용을 반환합니다.  
  
```  
<row id="1"><name>Larry</name><oflw>some text</oflw></row>  
<row id="2"><name>moe</name></row>  
<row id="3"/>  
```  
  
 컨텍스트 노드에 부모 접근자를 적용하면 3개 모두에 대한 <`Root`> 요소를 반환합니다.  
  
```  
SELECT T.c.query('..') AS result  
FROM   @x.nodes('/Root/row') T(c)  
go  
```  
  
 다음은 결과입니다.  
  
```  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
```  
  
### <a name="specifying-the-nodes-method-against-a-column-of-xml-type"></a>2. xml 형식의 열에 대해 nodes() 메서드 지정  
 자전거 제조 지침이이 예제에서 사용 하 고 지침에 저장 된 **xml** 의 유형 열은 **ProductModel** 테이블입니다.  
  
 다음 예제에서는 `nodes()` 에 대해 지정 된 메서드는 `Instructions` 의 열 **xml** 에 입력는 `ProductModel` 테이블 합니다.  
  
 `nodes()` 메서드는 `/MI:root/MI:Location` 경로를 지정하여 <`Location`> 요소를 컨텍스트 노드로 설정합니다. 결과 행 집합에는 <`Location`> 요소로 설정된 컨텍스트 노드와 함께 문서에 있는 각 <`Location`> 노드에 대해 원래 문서의 논리적 복사본이 하나씩 들어 있습니다. 따라서 `nodes()` 함수는 일련의 <`Location`> 컨텍스트 노드를 제공합니다.  
  
 이 행 집합에 대한 `query()` 메서드는 `self::node`를 요청하므로 각 행에 `<Location>` 요소를 반환합니다.  
  
 이 예에서 쿼리는 특정 제품 모델의 제조 지침 문서에 각 <`Location`> 요소를 컨텍스트 노드로 설정합니다. 이러한 컨텍스트 노드를 사용하여 다음과 같은 값을 검색할 수 있습니다.  
  
-   각 위치 Id 찾기 <`Location`>  
  
-   제조 단계 검색 (<`step`> 자식 요소) 각 <`Location`>  
  
 이 쿼리는 `'.'` 메서드에서 `self::node()`에 대한 축약형 구문 `query()`이 지정된 컨텍스트 항목을 반환합니다.  
  
 다음에 유의하세요.  
  
-   `nodes()` 메서드는 Instructions 열에 적용되며 `T (C)` 행 집합을 반환합니다. 이 행 집합에는 컨텍스트 항목으로 `/root/Location`이 포함된 원래 제조 지침 문서의 논리적 복사본이 포함됩니다.  
  
-   CROSS APPLY는 `nodes()` 테이블의 각 행에 `Instructions`를 적용하고 결과 집합을 생성하는 행만 반환합니다.  
  
    ```  
    SELECT C.query('.') as result  
    FROM Production.ProductModel  
    CROSS APPLY Instructions.nodes('  
    declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /MI:root/MI:Location') as T(C)  
    WHERE ProductModelID=7  
    ```  
  
     다음은 결과의 일부입니다.  
  
    ```  
    <MI:Location LocationID="10"  ...>  
       <MI:step ... />  
          ...  
    </MI:Location>  
    <MI:Location LocationID="20"  ... >  
        <MI:step ... />  
          ...  
    </MI:Location>  
    ...  
    ```  
  
### <a name="applying-nodes-to-the-rowset-returned-by-another-nodes-method"></a>3. 다른 nodes() 메서드에서 반환된 행 집합에 nodes() 적용  
 다음 코드는 XML 문서에서 `Instructions` 테이블의 `ProductModel` 열에 있는 제조 지침을 쿼리합니다. 이 쿼리는 제품 모델 ID, 제조 위치 및 제조 단계가 포함된 행 집합을 반환합니다.  
  
 다음에 유의하세요.  
  
-   `nodes()` 메서드는 `Instructions` 열에 적용되며 `T1 (Locations)` 행 집합을 반환합니다. 이 행 집합에는 항목 컨텍스트로 `/root/Location` 요소가 포함된 원래 제조 지침 문서의 논리적 복사본이 포함됩니다.  
  
-   `nodes()`는 `T1 (Locations)` 행 집합에 적용되며 `T2 (steps)` 행 집합을 반환합니다. 이 행 집합에는 항목 컨텍스트로 `/root/Location/step` 요소가 포함된 원래 제조 지침 문서의 논리적 복사본이 포함됩니다.  
  
```  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO         
```  
  
 다음은 결과입니다.  
  
```  
ProductModelID LocID Step         
----------------------------         
7      10   <step ... />         
7      10   <step ... />         
...         
7      20   <step ... />         
7      20   <step ... />         
7      20   <step ... />         
...         
```  
  
 이 쿼리는 `MI` 접두사를 두 번 선언합니다. 대신 `WITH XMLNAMESPACES`를 사용하여 접두사를 한 번만 선언하고 쿼리에서 사용할 수 있습니다.  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions'  AS MI)  
  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO    
```  
  
## <a name="see-also"></a>관련 항목:  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)  
  
  
