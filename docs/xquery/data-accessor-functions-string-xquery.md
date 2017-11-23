---
title: "string 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9372f042d6d3f0268a87147fb251985c634576db
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="data-accessor-functions---string-xquery"></a>데이터 접근자 함수-문자열 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  값을 반환 *$arg* 문자열로 표시 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 노드 또는 원자 값입니다.  
  
## <a name="remarks"></a>주의  
  
-   경우 *$arg* 이 빈 시퀀스인 경우 길이가 0 인 문자열이 반환 됩니다.  
  
-   경우 *$arg* 노드인 경우 함수는 문자열 값 접근자를 사용 하 여 가져온 노드의 문자열 값을 반환 합니다. 이 내용은 W3C XQuery 1.0 및 XPath 2.0 데이터 모델 사양에 정의되어 있습니다.  
  
-   경우 *$arg* 원자성 값로 캐스팅 된 식에서 반환 되는 동일한 문자열이 반환 **xs: string**, *$arg*, 특별히 언급 된 경우를 제외 하 고 있습니다.  
  
-   경우 유형의 *$arg* 은 **xs: anyuri**, 특수 문자를 이스케이프 처리 하지 않고 URI를 문자열로 변환 됩니다.  
  
-   이 구현 **fn: string** 는 상황별 조건자의 컨텍스트에서 인수만 사용할 수 있습니다. 특히 사용 시 대괄호([])로 묶어야 합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-string-function"></a>1. 문자열 함수 사용  
 다음 쿼리는 <`ProductDescription`> 요소의 <`Features`> 자식 요소 노드를 검색합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<PD:Features xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 지정 하는 경우는 **string ()** 함수를 지정 된 노드의 문자열 값을 받을 수 있습니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 string(/PD:ProductDescription[1]/PD:Features[1])  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 다음은 결과의 일부입니다.  
  
```  
These are the product highlights.   
3 yearsparts and labor...    
```  
  
### <a name="b-using-the-string-function-on-various-nodes"></a>2. 여러 노드에서 문자열 함수 사용  
 다음 예에서는 XML 인스턴스가 xml 유형의 변수에 할당됩니다. 쿼리를 적용 한 결과 설명 하기 위해 지정 **string ()** 다양 한 노드를 합니다.  
  
```  
declare @x xml  
set @x = '<?xml version="1.0" encoding="UTF-8" ?>  
<!--  This is a comment -->  
<root>  
  <a>10</a>  
just text  
  <b attr="x">20</b>  
</root>  
'  
```  
  
 다음 쿼리는 문서 노드의 문자열 값을 검색합니다. 이 값은 모든 해당 하위 항목 텍스트 노드의 문자열 값을 연결하여 형성됩니다.  
  
```  
select @x.query('string(/)')  
```  
  
 다음은 결과입니다.  
  
```  
This is a comment 10  
just text  
 20  
```  
  
 다음 쿼리에서는 처리 지침 노드의 문자열 값을 검색합니다. 여기에는 텍스트 노드가 없기 때문에 빈 시퀀스가 결과로 반환됩니다.  
  
```  
select @x.query('string(/processing-instruction()[1])')  
```  
  
 다음 쿼리는 주석 노드의 문자열 값을 검색하고 텍스트 노드를 반환합니다.  
  
```  
select @x.query('string(/comment()[1])')  
```  
  
 다음은 결과입니다.  
  
```  
This is a comment   
```  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
