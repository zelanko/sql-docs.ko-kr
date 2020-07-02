---
title: 문자열 길이 함수 (XQuery) | Microsoft Docs
description: XQuery 함수 문자열 길이 ()를 사용 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- string-length function
- fn:string-length function
ms.assetid: 7cd69c8b-cf2c-478c-b9a3-e0e14e1aa8aa
author: rothja
ms.author: jroth
ms.openlocfilehash: 2987001d2163340d9734a9cf606dfbe009901de3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720059"
---
# <a name="functions-on-string-values---string-length"></a>문자열 값 함수 - string-length
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  문자의 문자열 길이를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:string-length() as xs:integer  
fn:string-length($arg as xs:string?) as xs:integer  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 길이를 계산할 원본 문자열입니다.  
  
## <a name="remarks"></a>설명  
 *$Arg* 의 값이 빈 시퀀스인 경우 **xs: integer** 값 0이 반환 됩니다.  
  
 XQuery 함수에서 서로게이트 쌍의 동작은 데이터베이스 호환성 수준에 따라 달라집니다. 호환성 수준이 110 이상인 경우 각 서로게이트 쌍은 단일 문자로 계산됩니다. 호환성 수준이 110보다 낮으면 각 서로게이트 쌍을 두 문자로 간주합니다. 자세한 내용은 [ALTER Database Compatibility Level &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 및 [데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md)을 참조 하세요.  
  
 값에 두 개의 서로게이트 문자로 표현된 4바이트 유니코드 문자가 포함된 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 서로게이트 문자 개수를 별개로 셉니다.  
  
 매개 변수가 없는 **문자열 길이 ()** 는 조건자 내 에서만 사용할 수 있습니다. 예를 들어 다음 쿼리는 <> 요소를 반환 합니다 `ROOT` .  
  
```  
DECLARE @x xml;  
SET @x='<ROOT>Hello</ROOT>';  
SELECT @x.query('/ROOT[string-length()=5]');  
```  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 XQuery 함수에서 서로게이트 쌍의 동작은 데이터베이스 호환성 수준과 일부 경우 함수의 기본 네임스페이스 URI에 따라 달라집니다. 자세한 내용은 [SQL Server 2016의 데이터베이스 엔진 기능에 대 한 주요 변경 내용](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)항목의 "XQuery 함수는 서로게이트를 인식 합니다." 섹션을 참조 하세요. 또한 [ALTER Database Compatibility Level &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 및 [데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md)을 참조 하세요.  
  
## <a name="examples"></a>예제  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-string-length-xquery-function-to-retrieve-products-with-long-summary-descriptions"></a>A. string-length() XQuery 함수를 사용하여 긴 요약 설명이 포함된 제품 검색  
 요약 설명이 50 자를 초과 하는 제품의 경우 다음 쿼리는 제품 ID, 요약 설명의 길이 및 요약 자체도 <> 요소를 검색 합니다 `Summary` .  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
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
  
-   WHERE 절의 조건은 XML 문서에 저장된 요약 설명이 200자 이상인 행만 검색합니다. [Value () 메서드 (XML 데이터 형식)](../t-sql/xml/value-method-xml-data-type.md)를 사용 합니다.  
  
-   SELECT 절은 사용자가 원하는 XML만을 생성합니다. [Query () 메서드 (xml 데이터 형식)](../t-sql/xml/query-method-xml-data-type.md) 를 사용 하 여 xml을 생성 하 고 xml 문서에서 데이터를 검색 하는 데 필요한 XQuery 식을 지정 합니다.  
  
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
  
### <a name="b-using-the-string-length-xquery-function-to-retrieve-products-whose-warranty-descriptions-are-short"></a>B. string-length() XQuery 함수를 사용하여 보증 설명이 짧은 제품 검색  
 보증 설명이 20 자 미만인 제품의 경우 다음 쿼리는 제품 ID, 길이, 보증 설명 및 <> 요소 자체를 포함 하는 XML을 검색 합니다 `Warranty` .  
  
 보증은 제품 기능 중 하나입니다. 선택적 <`Warranty`> 자식 요소가 <> 요소 뒤에 옵니다 `Features` .  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
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
  
-   **pd** 및 **wm** 은이 쿼리에서 사용 되는 네임 스페이스 접두사입니다. 이 접두사는 쿼리 중인 문서에 사용되는 동일 네임스페이스를 식별합니다.  
  
-   XQuery는 중첩된 FOR 루프를 지정합니다. <> 요소의 **제품 Modelid** 특성을 검색 하려고 하기 때문에 외부 for 루프가 필요 합니다 `ProductDescription` . 20자 미만의 보증 기능 설명이 포함된 제품만 필요하기 때문에 내부 FOR 루프도 필수입니다.  
  
 다음은 결과의 일부입니다.  
  
```  
Result  
-------------------------  
<Prod ProductModelID="19">  
  <ShortFeature FeatureDescLength="15">  
    <wm:Warranty   
       xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
      <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
      <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
   </ShortFeature>  
</Prod>  
...  
```  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
