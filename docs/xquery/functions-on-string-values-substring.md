---
title: substring 함수 (XQuery) | Microsoft Docs
description: 소스 문자열의 지정 된 부분을 반환 하는 XQuery 함수 substring ()에 대해 알아봅니다.
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
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a4881fc4710ba56439eb98b5b196af93247c11f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768160"
---
# <a name="functions-on-string-values---substring"></a>문자열 값 함수 - substring
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$StartingLoc* 값이 나타내는 위치에서 시작 하 여 *$sourceString*값의 일부를 반환 하 고 *$length*값이 나타내는 문자 수를 계속 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>인수  
 *$sourceString*  
 원본 문자열입니다.  
  
 *$startingLoc*  
 원본 문자열에서 하위 문자열이 시작하는 시작 지점입니다. 이 값이 음수이거나 0이면 0보다 큰 위치에 있는 문자만 반환됩니다. *$SourceString*길이 보다 크면 길이가 0 인 문자열이 반환 됩니다.  
  
 *$length*  
 검색할 문자 개수입니다(옵션). 지정 하지 않으면 *$startingLoc* 에 지정 된 위치에서 문자열의 끝까지 모든 문자를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 함수에 3개의 인수를 지정하면 해당 위치 `$sourceString`이 따르는 `$p`의 문자가 반환됩니다.  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 *$Length* 값은 시작 위치 다음 *$sourceString* 값의 문자 수보다 클 수 있습니다. 이 경우 부분 문자열은 *$sourceString*끝 까지의 문자를 반환 합니다.  
  
 문자열의 첫 번째 문자는 위치 1에 있습니다.  
  
 *$SourceString* 의 값이 빈 시퀀스인 경우 길이가 0 인 문자열로 처리 됩니다. 그렇지 않고 *$startingLoc* 또는 *$length* 빈 시퀀스인 경우 빈 시퀀스가 반환 됩니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 XQuery 함수에서 서로게이트 쌍의 동작은 데이터베이스 호환성 수준과 일부 경우 함수의 기본 네임스페이스 URI에 따라 달라집니다. 자세한 내용은 [SQL Server 2016의 데이터베이스 엔진 기능에 대 한 주요 변경 내용](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)항목의 "XQuery 함수는 서로게이트를 인식 합니다." 섹션을 참조 하세요. 또한 [ALTER Database Compatibility Level &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 및 [데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md)을 참조 하세요.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 SQL Server에는 *$startingLoc* 및 *$length 매개 변수가* xs: double이 아니라 xs: decimal 형식 이어야 합니다.  
  
 SQL Server는 ()에 매핑되는 동적 오류의 결과로 빈 시퀀스가 가능한 값 이기 때문에 *$startingLoc* 및 *$length* 빈 시퀀스가 될 수 있습니다.  
  
## <a name="examples"></a>예제  
 이 항목에서는 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 합니다.  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. substring() XQuery 함수를 사용하여 부분 요약 제품 모델 설명 검색  
 이 쿼리는 제품 모델을 설명 하는 텍스트의 처음 50 문자를 검색 하 고 `Summary` 문서의 <> 요소를 검색 합니다.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **String ()** 함수는<> 요소의 문자열 값을 반환 합니다 `Summary` . 이 함수는 <`Summary`> 요소에 텍스트와 하위 요소 (html 서식 요소)가 모두 포함 되어 있고, 이러한 요소를 건너뛰고 모든 텍스트를 검색 하기 때문에 사용 됩니다.  
  
-   **Substring ()** 함수는 **문자열 ()** 에 의해 검색 된 문자열 값에서 처음 50 문자를 검색 합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
