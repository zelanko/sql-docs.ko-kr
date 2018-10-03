---
title: string-length 함수 (XQuery) | Microsoft Docs
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
- string-length function
- fn:string-length function
ms.assetid: 7cd69c8b-cf2c-478c-b9a3-e0e14e1aa8aa
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9871fb0f7f11a83506631ecb27d756bfaf8d036e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796271"
---
# <a name="functions-on-string-values---string-length"></a>문자열 값 함수 - string-length
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  문자의 문자열 길이를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:string-length() as xs:integer  
fn:string-length($arg as xs:string?) as xs:integer  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 길이를 계산할 원본 문자열입니다.  
  
## <a name="remarks"></a>Remarks  
 경우 값 *$arg* 가 빈 시퀀스에는 **xs: integer** 0 값이 반환 됩니다.  
  
 XQuery 함수에서 서로게이트 쌍의 동작은 데이터베이스 호환성 수준에 따라 달라집니다. 호환성 수준이 110 이상인 경우 각 서로게이트 쌍은 단일 문자로 계산됩니다. 호환성 수준이 110보다 낮으면 각 서로게이트 쌍을 두 문자로 간주합니다. 자세한 내용은 [ALTER DATABASE 호환성 수준 &#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 하 고 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
 값에 두 개의 서로게이트 문자로 표현된 4바이트 유니코드 문자가 포함된 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 서로게이트 문자 개수를 별개로 셉니다.  
  
 합니다 **string-length ()** 없이 매개 변수는 조건자 내 에서만 사용 될 수 있습니다. 예를 들어 다음 쿼리는 <`ROOT`> 요소를 반환합니다.  
  
```  
DECLARE @x xml;  
SET @x='<ROOT>Hello</ROOT>';  
SELECT @x.query('/ROOT[string-length()=5]');  
```  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 XQuery 함수에서 서로게이트 쌍의 동작은 데이터베이스 호환성 수준과 일부 경우 함수의 기본 네임스페이스 URI에 따라 달라집니다. 자세한 내용은 항목의 "XQuery 함수는 서로게이트 인식" 섹션을 참조 하세요 [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경 내용](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)합니다. 도 참조 하세요 [ALTER DATABASE 호환성 수준 &#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 하 고 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-string-length-xquery-function-to-retrieve-products-with-long-summary-descriptions"></a>1. string-length() XQuery 함수를 사용하여 긴 요약 설명이 포함된 제품 검색  
 요약 설명이 50자 이상인 제품에 대해 다음 쿼리는 제품 ID, 요약 설명 길이 및 요약 자체인 <`Summary`> 요소를 검색합니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT CatalogDescription.query('  
      <Prod ProductID= "{ /pd:ProductDescription[1]/@ProductModelID }" >  
       <LongSummary SummaryLength =   
           "{string-length(string( (/pd:ProductDescription/pd:Summary)[1] )) }" >  
           { string( (/pd:ProductDescription/pd:Summary)[1] ) }  
       </LongSummary>  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('string-length( string( (/pd:ProductDescription/pd:Summary)[1]))', 'decimal') > 200;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   WHERE 절의 조건은 XML 문서에 저장된 요약 설명이 200자 이상인 행만 검색합니다. 사용 된 [value () 메서드 (XML 데이터 형식)](../t-sql/xml/value-method-xml-data-type.md)합니다.  
  
-   SELECT 절은 사용자가 원하는 XML만을 생성합니다. 사용 된 [query () 메서드 (XML 데이터 형식)](../t-sql/xml/query-method-xml-data-type.md) XML을 생성 하 여 XML 문서에서 데이터를 검색 하는 데 필요한 XQuery 식을 지정 합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
Result  
-------------------  
<Prod ProductID="19">  
      <LongSummary SummaryLength="214">Our top-of-the-line competition   
             mountain bike. Performance-enhancing options include the  
             innovative HL Frame, super-smooth front suspension, and   
             traction for all terrain.  
      </LongSummary>  
</Prod>  
...  
```  
  
### <a name="b-using-the-string-length-xquery-function-to-retrieve-products-whose-warranty-descriptions-are-short"></a>2. string-length() XQuery 함수를 사용하여 보증 설명이 짧은 제품 검색  
 보증 설명이 20자 미만인 제품의 경우 다음 쿼리는 제품 ID, 길이, 보증 설명 및 <`Warranty`> 요소 자체가 포함된 XML을 검색합니다.  
  
 보증은 제품 기능 중 하나입니다. <`Features`> 요소 다음에는 선택 항목인 <`Warranty`> 자식 요소가 옵니다.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for   $ProdDesc in /pd:ProductDescription,  
            $pf in $ProdDesc/pd:Features/wm:Warranty  
      where string-length( string(($pf/wm:Description)[1]) ) < 20  
      return   
          <Prod >  
             { $ProdDesc/@ProductModelID }  
             <ShortFeature FeatureDescLength =   
                             "{string-length( string(($pf/wm:Description)[1]) ) }" >  
                 { $pf }  
             </ShortFeature>  
          </Prod>  
     ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription')=1;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **pd** 하 고 **wm** 은이 쿼리에 사용 되는 네임 스페이스 접두사입니다. 이 접두사는 쿼리 중인 문서에 사용되는 동일 네임스페이스를 식별합니다.  
  
-   XQuery는 중첩된 FOR 루프를 지정합니다. 바깥쪽 FOR 루프 이므로 필요한 경우 검색 하려는 합니다 **ProductModelID** 의 특성을 <`ProductDescription`> 요소입니다. 20자 미만의 보증 기능 설명이 포함된 제품만 필요하기 때문에 내부 FOR 루프도 필수입니다.  
  
 다음은 결과의 일부입니다.  
  
```  
Result  
-------------------------  
<Prod ProductModelID="19">  
  <ShortFeature FeatureDescLength="15">  
    <wm:Warranty   
       xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
      <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
      <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
   </ShortFeature>  
</Prod>  
...  
```  
  
## <a name="see-also"></a>관련 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
