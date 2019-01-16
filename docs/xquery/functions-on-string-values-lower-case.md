---
title: lower-case 함수 (XQuery) | Microsoft Docs
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
- lower-case Function (XQuery)
- lower-case
ms.assetid: 5222c4ff-890c-4d57-8506-c065a5ebfd3e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d265f405bdebac9a44461ca3b262935eaaba25bd
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254478"
---
# <a name="functions-on-string-values---lower-case"></a>문자열 값 함수 - lower-case
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Lower-case 함수에서 각 문자를 변환 *$arg* 를 해당 소문자로 동일 합니다. 유니코드 코드 포인트에 대한 Microsoft Windows 이진 대/소문자 변환은 문자를 소문자로 변환하는 방법을 지정합니다. 이 표준은 유니코드 코드 포인트 표준에 대한 매핑과 같지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:lower-case($arg as xs:string?) as xs:string  
```  
  
## <a name="arguments"></a>인수  
  
|||  
|-|-|  
|용어|정의|  
|*$arg*|소문자로 변환할 문자열 값입니다.|  
  
## <a name="remarks"></a>Remarks  
 경우 값 *$arg* 는 비어 있는 경우 길이가 0 인 문자열 반환 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-a-string-to-upper-case"></a>1. 문자열을 대문자로 변경  
 다음 예제에서는 입력된 문자열을 변경 ' abcDEF! @4' 소문자로 합니다.  
  
```  
DECLARE @x xml = N'abcDEF!@4';  
SELECT @x.value('fn:lower-case(/text()[1])', 'nvarchar(10)');  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `abcdef!@4`  
  
### <a name="b-search-for-a-specific-character-string"></a>2. 특정 문자열 검색  
 다음 예에서는 lower-case 함수를 사용하여 대/소문자를 구분하지 않는 검색을 수행하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks  
GO  
--WITH XMLNAMESPACES clause specifies the namespace prefix  
--to use.   
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
--The XQuery contains() function is used to determine whether  
--any of the text nodes below the <Summary> element contain  
--the word 'frame'. The lower-case() function makes the   
--case insensitive.  
  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
/pd:ProductDescription/pd:Summary//text()[  
          contains(lower-case(.), "FRAME")]')  = 1  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `19     <Prod ProductModelID="19">`  
  
 `<pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike.`  
  
 `Performance-enhancing options include the innovative HL Frame,`  
  
 `super-smooth front suspension, and traction for all terrain.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
 `25     <Prod ProductModelID="25">`  
  
 `<pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">This bike is ridden by race winners. Developed with the`  
  
 `Adventure Works Cycles professional race team, it has a extremely light`  
  
 `heat-treated aluminum frame, and steering that allows precision control.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>관련 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
