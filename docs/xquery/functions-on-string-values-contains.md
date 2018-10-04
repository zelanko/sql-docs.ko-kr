---
title: contains 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 595d5fb7d98d85120fca3b96eedc5a83694dc1a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753921"
---
# <a name="functions-on-string-values---contains"></a>문자열 값 함수 - contains
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  형식을 나타내는 xs: boolean 값을 반환 하는지 여부를 값 *$arg1* 로 지정 된 문자열 값을 포함 *$arg2*.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>인수  
 *$arg1*  
 테스트할 문자열 값입니다.  
  
 *$arg2*  
 검색할 하위 문자열입니다.  
  
## <a name="remarks"></a>Remarks  
 경우 값 *$arg2* 는 길이가 0 인 문자열 반환 **True**합니다. 경우 값 *$arg1* 길이가 0 인 문자열 및 값은 *$arg2* 길이가 0 인 문자열이 아닙니다, 함수 반환 **False**합니다.  
  
 경우 값 *$arg1* 하거나 *$arg2* 이 빈 시퀀스인 경우 인수는 길이가 0 인 문자열로 취급 됩니다.  
  
 contains() 함수는 문자열 비교를 위해 XQuery의 기본 유니코드 코드 포인트 데이터 정렬을 사용합니다.  
  
 지정 된 부분 문자열 값 *$arg2* 4,000 자 보다 작을 수에 합니다. 지정 된 값이 4000 자 보다 큰 경우 동적 오류 조건이 발생 하 고 contains () 함수는 부울 값 대신 빈 시퀀스를 반환 **True** 하거나 **False**합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 XQuery 식에서 동적 오류를 발생시키지 않습니다.  
  
 대/소문자 구분 비교를 가져오려면 합니다 [대문자](../xquery/functions-on-string-values-upper-case.md) 또는 lower-case 함수를 사용할 수 있습니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 XQuery 함수에서 서로게이트 쌍의 동작은 데이터베이스 호환성 수준과 일부 경우 함수의 기본 네임스페이스 URI에 따라 달라집니다. 자세한 내용은 항목의 "XQuery 함수는 서로게이트 인식" 섹션을 참조 하세요 [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경 내용](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)합니다. 도 참조 하세요 [ALTER DATABASE 호환성 수준 &#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 하 고 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 xml 형식 열에 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-contains-xquery-function-to-search-for-a-specific-character-string"></a>1. contains() XQuery 함수를 사용하여 특정 문자열 검색  
 다음 쿼리는 요약 설명에 Aerodynamic이라는 단어가 포함된 제품을 검색합니다. 이 쿼리는 이러한 제품에 대한 ProductID와 <`Summary`> 요소를 반환합니다.  
  
```  
--The product model description document uses  
--namespaces. The WHERE clause uses the exit()  
--method of the xml data type. Inside the exit method,  
--the XQuery contains()function is used to  
--determine whether the <Summary> text contains the word  
--Aerodynamic.   
  
USE AdventureWorks  
GO  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
   /pd:ProductDescription/pd:Summary//text()  
    [contains(., "Aerodynamic")]') = 1  
```  
  
 결과  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `28     <Prod ProductModelID="28">`  
  
 `<pd:Summary xmlns:pd=`  
  
 `"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>관련 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
