---
title: 유형 시스템 (XQuery) | Microsoft Docs
description: XML 스키마의 기본 제공 유형과 xpath 데이터 형식 네임 스페이스에 정의 된 유형을 포함 하는 XQuery 유형 시스템에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f82cfc060b021e28c5b5e73602285b1edc3fcf20
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84886554"
---
# <a name="type-system-xquery"></a>유형 시스템(XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery는 유형 지정이 엄격한 언어이며 형식화되지 않은 데이터에 대해서는 유형 지정이 엄격하지 않은 언어입니다. XQuery의 미리 정의된 유형에는 다음이 포함됩니다.  
  
-   네임 스페이스에 있는 XML 스키마의 기본 제공 형식 **http://www.w3.org/2001/XMLSchema** 입니다.  
  
-   네임 스페이스에 정의 된 형식 **http://www.w3.org/2004/07/xpath-datatypes** 입니다.  
  
 이 항목에서는 다음에 대해서도 설명합니다.  
  
-   형식화된 값과 노드의 문자열 값  
  
-   [데이터 함수는 xquery&#41;&#40;](../xquery/data-accessor-functions-data-xquery.md) 하 고 [문자열 함수는 xquery&#41;&#40;](../xquery/data-accessor-functions-string-xquery.md)합니다.  
  
-   식에 의해 반환된 시퀀스 유형 일치  
  
## <a name="built-in-types-of-xml-schema"></a>XML 스키마의 기본 제공 유형  
 XML 스키마의 기본 제공 유형에는 xs의 미리 정의된 네임스페이스 접두사가 있습니다. 이러한 형식 중 일부에는 **xs: integer** 및 **xs: string**이 포함 됩니다. 이러한 모든 기본 제공 유형이 지원됩니다. 이러한 유형은 XML 스키마 컬렉션을 만들 때 사용할 수 있습니다.  
  
 형식화된 XML을 쿼리할 때 노드의 정적 및 동적 유형은 쿼리 중인 열 또는 변수와 연결된 XML 스키마 컬렉션에 의해 결정됩니다. 정적 및 동적 형식에 대 한 자세한 내용은 [XQuery&#41;&#40;식 컨텍스트 및 쿼리 평가 ](../xquery/expression-context-and-query-evaluation-xquery.md)를 참조 하세요. 예를 들어 다음 쿼리는 형식화 된 **xml** 열에 대해 지정 됩니다 ( `Instructions` ). 이 식에서는 `instance of`를 사용하여 반환된 `LotSize` 특성의 형식화된 값이 `xs:decimal` 유형인지 확인합니다.  
  
```  
SELECT Instructions.query('  
   DECLARE namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   data(/AWMI:root[1]/AWMI:Location[@LocationID=10][1]/@LotSize)[1] instance of xs:decimal  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이 유형 지정 정보는 열과 연결된 XML 스키마 컬렉션에 의해 제공됩니다.  
  
## <a name="types-defined-in-xpath-data-types-namespace"></a>XPath 데이터 형식 네임스페이스에 정의된 유형  
 네임 스페이스에 정의 된 형식에는 **http://www.w3.org/2004/07/xpath-datatypes** 미리 정의 된 **xdt**접두사가 있습니다. 이러한 유형에는 다음이 적용됩니다.  
  
-   XML 스키마 컬렉션을 만들 때는 이러한 유형을 사용할 수 없습니다. 이러한 형식은 XQuery 형식 시스템에서 사용 되며 [xquery 및 정적 형식화](../xquery/xquery-and-static-typing.md)에 사용 됩니다. **Xdt** 네임 스페이스의 원자성 형식 (예 **: xdt: untypedAtomic**)으로 캐스팅할 수 있습니다.  
  
-   형식화 되지 않은 XML을 쿼리할 때 요소 노드의 정적 및 동적 형식은 **xdt: 형식화**되지 않으며 특성 값의 형식은 **xdt: untypedAtomic**입니다. **Query ()** 메서드의 결과는 형식화 되지 않은 XML을 생성 합니다. 즉, XML 노드는 각각 **xdt: 형식화 되지** 않은 및 **xdt: untypedAtomic**로 반환 됩니다.  
  
-   **Xdt: dayTimeDuration** 및 **xdt: yearMonthDuration** 형식은 지원 되지 않습니다.  
  
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
  
## <a name="typed-value-vs-string-value"></a>형식화된 값과 문자열 값  
 모든 노드에는 형식화된 값과 문자열 값이 있습니다. 형식화된 XML 데이터의 경우 형식화된 값의 유형은 쿼리 중인 열 또는 변수와 연결된 XML 스키마 컬렉션에 의해 제공됩니다. 형식화 되지 않은 XML 데이터의 경우 형식화 된 값의 형식은 **xdt: untypedAtomic**입니다.  
  
 **Data ()** 또는 **string ()** 함수를 사용 하 여 노드의 값을 검색할 수 있습니다.  
  
-   [데이터 함수 &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md) 는 노드의 형식화 된 값을 반환 합니다.  
  
-   [문자열 함수 &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md) 는 노드의 문자열 값을 반환 합니다.  
  
 다음 XML 스키마 컬렉션에서는 `root` 정수 형식의 <> 요소가 정의 됩니다.  
  
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
  
 다음 예에서는 `LaborHours` 특성의 합계를 계산합니다. `data()`함수는 `LaborHours` `Location` 제품 모델에 대 한 모든 <> 요소에서 특성의 형식화 된 값을 검색 합니다. 열과 연결 된 XML 스키마에 따라 `Instruction` `LaborHours` 은 **xs: decimal** 형식입니다.  
  
```  
SELECT Instructions.query('   
DECLARE namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
             sum(data(//AWMI:Location/@LaborHours))   
') AS Result   
FROM Production.ProductModel   
WHERE ProductModelID=7  
```  
  
 이 쿼리는 결과로 12.75를 반환합니다.  
  
> [!NOTE]  
>  이 예제에서 **data ()** 함수를 명시적으로 사용 하는 것은 설명을 위한 목적 으로만 사용 됩니다. 지정 되지 않은 경우 **sum ()** 함수는 **데이터 ()** 함수를 암시적으로 적용 하 여 노드의 형식화 된 값을 추출 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler 템플릿 및 권한](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [XQuery 기초](../xquery/xquery-basics.md)  
  
  
