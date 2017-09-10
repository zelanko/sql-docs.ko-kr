---
title: "substring 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fbe33b349def61c3b093079554db626b56f2f09
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-string-values---substring"></a>문자열 값-substring 함수
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  값의 일부를 반환 *$sourceString*의 값이 지정 된 위치에서 시작, *$startingLoc,* 의 값이 지정 된 문자 수에 대 한 계속 *$ 길이*합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc  as as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>인수  
 *$sourceString*  
 원본 문자열입니다.  
  
 *$startingLoc*  
 원본 문자열에서 하위 문자열이 시작하는 시작 지점입니다. 이 값이 음수이거나 0이면 0보다 큰 위치에 있는 문자만 반환됩니다. 길이 보다 큰 경우는 *$sourceString*, 길이가 0 인 문자열이 반환 됩니다.  
  
 *$length*  
 검색할 문자 개수입니다(옵션). 에 지정 된 위치에서 모든 문자를 지정 하지 반환 *$startingLoc* 문자열의 끝까지 합니다.  
  
## <a name="remarks"></a>주의  
 함수에 3개의 인수를 지정하면 해당 위치 `$sourceString`이 따르는 `$p`의 문자가 반환됩니다.  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 값 *$length* 값에는 문자 수보다 클 수 *$sourceString* 은 시작 위치 이후의 합니다. 부분 문자열의 끝까지 있는 문자를 반환 하는 경우에 *$sourceString*합니다.  
  
 문자열의 첫 번째 문자는 위치 1에 있습니다.  
  
 하는 경우의 값 *$sourceString* 이 빈 시퀀스인 경우 길이가 0 인 문자열로 처리 됩니다. 그렇지 않은 경우 *$startingLoc* 또는 *$length* 이 빈 시퀀스인 경우 빈 시퀀스가 반환 됩니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 XQuery 함수에서 서로게이트 쌍의 동작은 데이터베이스 호환성 수준과 일부 경우 함수의 기본 네임스페이스 URI에 따라 달라집니다. 자세한 내용은 항목의 "XQuery 함수는 서로게이트 인식" 섹션을 참조 하십시오. [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경 내용](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)합니다. 또한 참조 [ALTER DATABASE 호환성 수준 &#40; Transact SQL &#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 및 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)합니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 SQL Server가 필요는 *$startingLoc* 및 *$length 매개 변수* 유형이 xs: double 대신 xs: decimal 이어야 합니다.  
  
 SQL Server에서는 *$startingLoc* 및 *$length* 빈 시퀀스 이면 빈 시퀀스가 ()로 매핑되는 동적 오류 결과로 가능한 값 이기 때문에 있습니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** 유형 열에는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>1. substring() XQuery 함수를 사용하여 부분 요약 제품 모델 설명 검색  
 다음 쿼리는 제품 모델에 대해 기술하는 텍스트(문서의 <`Summary`> 요소)에서 처음 50개 문자를 검색합니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **string ()** 의 문자열 값을 반환 하는 함수는 <`Summary`> 요소입니다. <`Summary`> 요소에 텍스트와 하위 요소(html 서식 지정 요소)가 모두 들어 있고, 이러한 요소를 건너뛰고 모든 텍스트를 검색할 것이기 때문에 이 함수가 사용됩니다.  
  
-   **substring ()** 으로 검색 하는 문자열 값에서 처음 50 개 문자를 검색 하는 함수는 **string ()**합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
