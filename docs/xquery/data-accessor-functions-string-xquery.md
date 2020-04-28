---
title: string 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cb30d81102c17f2c3ce04b31ac7ff2b9689343e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038946"
---
# <a name="data-accessor-functions---string-xquery"></a>데이터 접근자 함수 - string(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  문자열로 표현 된 *$arg* 의 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 노드 또는 원자 값입니다.  
  
## <a name="remarks"></a>설명  
  
-   *$Arg* 빈 시퀀스인 경우 길이가 0 인 문자열이 반환 됩니다.  
  
-   *$Arg* 노드인 경우 함수는 문자열-값 접근자를 사용 하 여 가져온 노드의 문자열 값을 반환 합니다. 이 내용은 W3C XQuery 1.0 및 XPath 2.0 데이터 모델 사양에 정의되어 있습니다.  
  
-   *$Arg* 원자 값인 경우 함수는 **xs: string**으로 캐스팅 된 식에서 반환 된 것과 동일한 문자열을 반환 합니다 .이 문자열은 그렇지 않은 경우를 제외 하 고는 *$arg*.  
  
-   *$Arg* 형식이 **xs: ANYURI**인 경우 URI는 특수 문자를 이스케이프 하지 않고 문자열로 변환 됩니다.  
  
-   인수가 없는 **fn: string ()** 구현은 컨텍스트 종속 조건자의 컨텍스트에서만 사용할 수 있습니다. 특히 사용 시 대괄호([])로 묶어야 합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-string-function"></a>A. 문자열 함수 사용  
 다음 쿼리는 <`Features` `ProductDescription`> 요소의 <> 자식 요소 노드를 검색 합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<PD:Features xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 **String ()** 함수를 지정 하면 지정 된 노드의 문자열 값이 표시 됩니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
### <a name="b-using-the-string-function-on-various-nodes"></a>B. 여러 노드에서 문자열 함수 사용  
 다음 예에서는 XML 인스턴스가 xml 유형의 변수에 할당됩니다. 쿼리는 다양 한 노드에 **문자열 ()** 을 적용 한 결과를 보여 주기 위해 지정 됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
