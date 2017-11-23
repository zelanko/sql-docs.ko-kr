---
title: "일반 XQuery 사용 경우까지 이렇게 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords: XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4bef0c77a25ac81adb5a758ecb96e1d02a1177ea
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="general-xquery-use-cases"></a>일반 XQuery 사용 사례
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 XQuery에 대한 일반적인 사용 예를 보여 줍니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>1. 제품 및 중량 검색을 위한 카탈로그 설명 쿼리  
 다음 쿼리는 제품 카탈로그 설명에서 제품 모델 ID와 중량(있는 경우)을 반환합니다. 쿼리는 다음 형식의 XML을 생성합니다.  
  
```  
<Product ProductModelID="…">  
  <Weight>…</Weight>  
</Product>  
```  
  
 다음은 쿼리입니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **네임 스페이스** 키워드 XQuery 프롤로그에 쿼리 본문에 사용 되는 네임 스페이스 접두사를 정의 합니다.  
  
-   쿼리 본문은 필요한 XML을 생성합니다.  
  
-   WHERE 절에는 **exist ()** 메서드는 제품 카탈로그 설명이 포함 된 행만 검색 하는 데 사용 됩니다. 즉, <`ProductDescription`> 요소가 포함된 XML을 검색합니다.  
  
 다음은 결과입니다.  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 다음 쿼리는 카탈로그 설명에서 사양을 나타내는 <`Specifications`> 요소에 있는 중량을 나타내는 <`Weight`> 요소가 포함된 제품 모델에 대해서만 같은 정보를 검색합니다. 이 예에서는 WITH XMLNAMESPACES를 사용하여 pd 접두사와 해당 네임스페이스 바인딩을 선언합니다. 이러한 방식으로 바인딩 둘 다에 설명 되지 않은 **query ()** 메서드 및는 **exist ()** 메서드.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 이전 쿼리에서 **exist ()** 의 메서드는 **xml** 데이터 형식 확인 있는지 확인 하는 WHERE 절에는 <`Weight`> 요소에는 <`Specifications`> 요소입니다.  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>2. 카탈로그 설명에 소형 전면 사진이 포함된 제품 모델의 제품 모델 ID 검색  
 XML 제품 카탈로그 설명에는 <`Picture`> 요소에 제품 사진이 포함됩니다. 각 사진은 몇 가지 속성을 갖고 있습니다. 여기에는 사진 각도를 나타내는 <`Angle`> 요소와 크기를 나타내는 <`Size`> 요소가 포함됩니다.  
  
 카탈로그 설명에 소형 전면 사진이 포함된 제품 모델에 대해 이 쿼리는 다음과 같은 형식의 XML을 생성합니다.  
  
```  
< Product ProductModelID="…">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   WHERE 절에는 **exist ()** 메서드는 제품 카탈로그 설명이 있는 행만 검색 하는 데 사용 되는 <`Picture`> 요소입니다.  
  
-   WHERE 절이 사용 하는 **value ()** 메서드를 두 번의 값을 비교 하는 <`Size`> 및 <`Angle`> 요소입니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<p1:Product   
  xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>3. 기본 목록 만들기의 제품 모델 이름 및 기능, 각에 쌍으로 포함 된 \<기능 > 요소  
 제품 모델 카탈로그 설명에서 XML에는 몇 가지 제품 기능이 포함됩니다. 이러한 모든 기능은 <`Features`> 요소에 포함됩니다. 쿼리에서 사용 하 여 [XML 생성 (XQuery)](../xquery/xml-construction-xquery.md) 필요한 XML을 생성 합니다. 중괄호에 있는 식은 결과로 대체됩니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   $pd/p1:Features/*는 <`Features`>의 요소 노드 자식만 반환하지만 $pd/p1:Features/node()는 모든 노드를 반환합니다. 여기에는 요소 노드, 텍스트 노드, 처리 명령 및 주석이 포함됩니다.  
  
-   두 개의 FOR 루프는 제품 이름 및 개별 기능이 반환되는 카티션 곱을 생성합니다.  
  
-   **ProductName** 는 특성입니다. 이 쿼리의 XML 생성은 해당 항목을 요소로 반환합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>4. 제품 모델 카탈로그 설명에서 목록의 제품 모델 이름, 모델 ID 및 기능 내에 그룹화 된는 \<제품 > 요소  
 다음 쿼리는 제품 모델 이름, 모델 ID를 나열 하 고 기능 내에 그룹화 된 제품 모델 카탈로그 설명에 저장 된 정보를 사용 하는 \<제품 > 요소입니다.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="http://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="http://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="http://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>5. 제품 모델 기능 설명 검색  
 다음 쿼리는 포함 된 XML을 생성 한 <`Product`> 있는 요소로 **ProducModelID**, **ProductModelName** 특성 및 처음 두 개의 제품 기능입니다. 특히 처음 두 개의 제품 기능은 <`Features`> 요소에 대한 처음 두 개의 자식 요소입니다. 기능이 더 많은 경우 빈 <`There-is-more/`> 요소를 반환합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   FOR ... RETURN 루프 구조는 처음 두 개의 제품 기능을 검색합니다. **position ()** 함수는 시퀀스에서 요소의 위치를 찾아야 하는 데 사용 됩니다.  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>6. 제품 카탈로그 설명에서 "ons"로 끝나는 요소 이름 찾기  
 다음 쿼리는 카탈로그 설명을 검색하고 이름이 "ons"로 끝나는 <`ProductDescription`> 요소에 있는 모든 요소를 반환합니다.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 다음은 결과의 일부입니다.  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>7. "Aerodynamic"이라는 단어가 포함된 요약 설명 찾기  
 다음 쿼리는 제품 카탈로그의 요약 설명에 "Aerodynamic"이라는 단어가 포함된 제품 모델을 검색합니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 SELECT 쿼리를 지정 하는 참고 **query ()** 및 **value ()** 의 메서드는 **xml** 데이터 형식입니다. 따라서 두 개의 서로 다른 쿼리 프롤로그에 있는 네임스페이스 선언을 두 번 반복하는 대신 pd 접두사가 쿼리에서 사용되고 WITH XMLNAMESPACES를 사용하여 한 번만 정의됩니다.  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   WHERE 절을 사용하여 카탈로그 설명에서 <`Summary`> 요소에 "Aerodynamic"이라는 단어가 들어 있는 행만 검색합니다.  
  
-   **contains ()** 함수를 사용 하는 경우 단어가 텍스트에 포함 되어 있는지 확인 합니다.  
  
-   **value ()** 의 메서드는 **xml** 데이터 형식에서 반환 된 값과 비교 **contains ()** 1입니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>8. 카탈로그 설명에 제품 모델 사진이 포함되지 않은 제품 모델 찾기  
 다음 쿼리는 카탈로그 설명에 <`Picture`> 요소가 포함되지 않은 제품 모델에 대한 ProductModelID를 검색합니다.  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   경우는 **exist ()** False (0)를 반환 하는 WHERE 절에서 메서드를 제품 모델 ID가 반환 됩니다. 그렇지 않으면 제품 모델 ID가 반환되지 않습니다.  
  
-   모든 제품 설명에는 <`Picture`> 요소가 포함되기 때문에 이 경우 결과 집합이 비어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [계층 구조와 관련 된 XQueries](../xquery/xqueries-involving-hierarchy.md)   
 [XQueries 정렬 포함](../xquery/xqueries-involving-order.md)   
 [XQueries 처리 관계형 데이터](../xquery/xqueries-handling-relational-data.md)   
 [XQuery에서 문자열 검색](../xquery/string-search-in-xquery.md)   
 [XQuery의 네임 스페이스 처리](../xquery/handling-namespaces-in-xquery.md)   
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
