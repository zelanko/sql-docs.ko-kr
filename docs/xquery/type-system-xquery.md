---
title: "형식 시스템 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- sequence [XQuery]
- type system [XQuery]
- typed values [XQuery]
- XQuery, sequence
- string values [XQuery]
- XQuery, XPath data type namespace
- xdt prefix [XML in SQL Server]
- XQuery, type system
- built-in XML schema types [SQL Server]
- xs prefix [XML in SQL Server]
ms.assetid: 22d6f861-d058-47ee-b550-cbe9092dcb12
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c0c11fc81be9e8a5b34548e22a7f2feb43a441b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="type-system-xquery"></a>유형 시스템(XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery는 유형 지정이 엄격한 언어이며 형식화되지 않은 데이터에 대해서는 유형 지정이 엄격하지 않은 언어입니다. XQuery의 미리 정의된 유형에는 다음이 포함됩니다.  
  
-   기본 제공 형식에 XML 스키마의는 **http://www.w3.org/2001/XMLSchema** 네임 스페이스입니다.  
  
-   에 정의 된 유형에 **http://www.w3.org/2004/07/xpath-datatypes** 네임 스페이스입니다.  
  
 이 항목에서는 다음에 대해서도 설명합니다.  
  
-   형식화된 값과 노드의 문자열 값  
  
-   [데이터 함수 &#40; XQuery &#41; ](../xquery/data-accessor-functions-data-xquery.md) 및 [함수 &#40; 문자열 XQuery &#41; ](../xquery/data-accessor-functions-string-xquery.md).  
  
-   식에 의해 반환된 시퀀스 유형 일치  
  
## <a name="built-in-types-of-xml-schema"></a>XML 스키마의 기본 제공 유형  
 XML 스키마의 기본 제공 유형에는 xs의 미리 정의된 네임스페이스 접두사가 있습니다. 이러한 형식 중 일부는 같습니다. **xs: integer** 및 **xs: string**합니다. 이러한 모든 기본 제공 유형이 지원됩니다. 이러한 유형은 XML 스키마 컬렉션을 만들 때 사용할 수 있습니다.  
  
 형식화된 XML을 쿼리할 때 노드의 정적 및 동적 유형은 쿼리 중인 열 또는 변수와 연결된 XML 스키마 컬렉션에 의해 결정됩니다. 정적 및 동적 유형에 대 한 자세한 내용은 참조 하십시오. [식 컨텍스트 및 쿼리 평가 &#40; XQuery &#41; ](../xquery/expression-context-and-query-evaluation-xquery.md). 다음 쿼리를 지정 하는 예를 들어 형식화 된에 대해 **xml** 열 (`Instructions`). 이 식에서는 `instance of`를 사용하여 반환된 `LotSize` 특성의 형식화된 값이 `xs:decimal` 유형인지 확인합니다.  
  
```  
SELECT Instructions.query('  
   DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   data(/AWMI:root[1]/AWMI:Location[@LocationID=10][1]/@LotSize)[1] instance of xs:decimal  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이 유형 지정 정보는 열과 연결된 XML 스키마 컬렉션에 의해 제공됩니다.  
  
## <a name="types-defined-in-xpath-data-types-namespace"></a>XPath 데이터 형식 네임스페이스에 정의된 유형  
 에 정의 된 형식에서 **http://www.w3.org/2004/07/xpath-datatypes** 네임 스페이스의 미리 정의 된 접두사가 **xdt**합니다. 이러한 유형에는 다음이 적용됩니다.  
  
-   XML 스키마 컬렉션을 만들 때는 이러한 유형을 사용할 수 없습니다. 이러한 형식은 XQuery 유형 시스템에 사용 되 고에 사용 되 [XQuery 및 정적 형식 지정](../xquery/xquery-and-static-typing.md)합니다. 예를 들어 원자성 유형으로 캐스팅할 수 **xdt: untypedatomic**에 **xdt** 네임 스페이스입니다.  
  
-   형식화 되지 않은 XML을 쿼리할 때 요소 노드의 정적 및 동적 유형은 **xdt: 형식화 되지 않은**, 특성 값의 형식이 고 **xdt: untypedatomic**합니다. 결과 **query ()** 메서드는 형식화 되지 않은 XML을 생성 합니다. 즉, XML 노드가으로 반환 됩니다 **xdt: 형식화 되지 않은** 및 **xdt: untypedatomic**각각.  
  
-   **xdt: daytimeduration** 및 **xdt: yearmonthduration** 형식은 지원 되지 않습니다.  
  
 다음 예에서는 형식화되지 않은 XML 변수에 대해 쿼리가 지정됩니다. `data(/a[1]`) 식은 원자 값의 시퀀스를 반환합니다. `data()` 함수는 `<a>` 요소의 형식화된 값을 반환합니다. 쿼리 중인 XML이 형식화되지 않았기 때문에 반환된 값의 유형은 `xdt:untypedAtomic`입니다. 따라서 `instance of`는 True를 반환합니다.  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
SELECT @x.query( 'data(/a[1]) instance of xdt:untypedAtomic' )  
```  
  
 형식화된 값을 검색하는 대신 다음 예의 식(`/a[1]`)은 `<a>` 요소의 시퀀스를 반환합니다. `instance of` 식은 요소 테스트를 사용하여 식에 의해 반환된 값이 `xdt:untyped type`의 요소 노드인지 확인합니다.  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
-- Is this an element node whose name is "a" and type is xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(a, xdt:untyped?)')  
-- Is this an element node of type xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(*, xdt:untyped?)')  
-- Is this an element node?  
SELECT @x.query( '/a[1] instance of element()')  
```  
  
> [!NOTE]  
>  형식화된 XML 인스턴스를 쿼리 중이고 쿼리 식에 부모 축이 포함된 경우 결과 노드의 정적 유형 정보는 더 이상 사용할 수 없습니다. 하지만 동적 유형은 노드와 계속 연결되어 있습니다.  
  
## <a name="typed-value-vs-string-value"></a>형식화된 값과 문자열 값 비교  
 모든 노드에는 형식화된 값과 문자열 값이 있습니다. 형식화된 XML 데이터의 경우 형식화된 값의 유형은 쿼리 중인 열 또는 변수와 연결된 XML 스키마 컬렉션에 의해 제공됩니다. 형식화 되지 않은 XML 데이터에 대 한 형식화 된 값의 형식이 **xdt: untypedatomic**합니다.  
  
 사용할 수는 **data ()** 또는 **string ()** 노드의 값을 검색 하는 함수:  
  
-   [데이터 함수 &#40; XQuery &#41; ](../xquery/data-accessor-functions-data-xquery.md) 노드의 형식화 된 값을 반환 합니다.  
  
-   [함수 &#40; 문자열 XQuery &#41; ](../xquery/data-accessor-functions-string-xquery.md) 노드의 문자열 값을 반환 합니다.  
  
 다음 XML 스키마 컬렉션에서는 정수 유형의 <`root`> 요소가 정의됩니다.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="integer"/>  
</schema>'  
GO  
```  
  
 다음 예에서는 식이 먼저 `/root[1]`의 형식화된 값을 검색한 다음 여기에 `3`을 더합니다.  
  
```  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('data(/root[1]) + 3')  
```  
  
 다음 예에서는 식에 있는 `string(/root[1])`이 문자열 유형의 값을 반환하기 때문에 식이 실패합니다. 그런 다음 피연산자로 숫자 유형의 값만 사용하는 산술 연산자로 이 값이 전달됩니다.  
  
```  
-- Fails because the argument is string type (must be numeric primitive type).  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('string(/root[1]) + 3')  
```  
  
 다음 예에서는 `LaborHours` 특성의 합계를 계산합니다. `data()` 의 형식화 된 값을 검색 하는 함수 `LaborHours` 모든 특성의 <`Location`> 제품 모델에 대 한 요소입니다. 와 연결 된 XML 스키마에 따라는 `Instruction` 열 `LaborHours` 의 **xs: decimal** 유형입니다.  
  
```  
SELECT Instructions.query('   
DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
             sum(data(//AWMI:Location/@LaborHours))   
') AS Result   
FROM Production.ProductModel   
WHERE ProductModelID=7  
```  
  
 이 쿼리는 결과로 12.75를 반환합니다.  
  
> [!NOTE]  
>  명시적으로 사용 된 **data ()** 이 예제는 함수는 예시용 으로만 합니다. 지정 하지 않으면 **sum ()** 암시적으로 적용 된 **data ()** 노드의 형식화 된 값을 추출 하는 함수입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Profiler 템플릿 및 권한](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [XQuery 기초](../xquery/xquery-basics.md)  
  
  
