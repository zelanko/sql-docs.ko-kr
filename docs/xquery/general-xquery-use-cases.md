---
title: 일반 XQuery 사용 사례 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e844425f0c512cfe7c15354bf1aeb100d6104e2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68004527"
---
# <a name="general-xquery-use-cases"></a>일반 XQuery 사용 사례
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 XQuery에 대한 일반적인 사용 예를 보여 줍니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. 제품 및 중량 검색을 위한 카탈로그 설명 쿼리  
 다음 쿼리는 제품 카탈로그 설명에서 제품 모델 ID와 중량(있는 경우)을 반환합니다. 쿼리는 다음 형식의 XML을 생성합니다.  
  
```  
<Product ProductModelID="...">  
  <Weight>...</Weight>  
</Product>  
```  
  
 다음은 쿼리입니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
-   XQuery 프롤로그의 **namespace** 키워드는 쿼리 본문에 사용 되는 네임 스페이스 접두사를 정의 합니다.  
  
-   쿼리 본문은 필요한 XML을 생성합니다.  
  
-   WHERE 절에서는 **exist ()** 메서드를 사용 하 여 제품 카탈로그 설명이 포함 된 행만 찾습니다. 즉, <`ProductDescription`> 요소를 포함 하는 XML입니다.  
  
 다음은 결과입니다.  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 다음 쿼리는 동일한 정보를 검색 하지만 카탈로그 설명이 포함 된 해당 제품 모델에 대해서만 <`Weight` `Specifications`> 요소에 가중치, <> 요소를 포함 합니다. 이 예에서는 WITH XMLNAMESPACES를 사용하여 pd 접두사와 해당 네임스페이스 바인딩을 선언합니다. 이러한 방식으로 **query ()** 메서드와 **exist ()** 메서드에서 바인딩이 설명 되지 않습니다.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
 이전 쿼리에서 WHERE 절에 있는 **xml** 데이터 형식의 `Weight` **exist ()** 메서드는 <`Specifications`> 요소에 <> 요소가 있는지 확인 합니다.  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>B. 카탈로그 설명에 소형 전면 사진이 포함된 제품 모델의 제품 모델 ID 검색  
 XML 제품 카탈로그 설명에는 제품 그림, <`Picture`> 요소가 포함 됩니다. 각 사진은 몇 가지 속성을 갖고 있습니다. 여기에는 그림 각도, <`Angle`> 요소 및 크기 <`Size`> 요소가 포함 됩니다.  
  
 카탈로그 설명에 소형 전면 사진이 포함된 제품 모델에 대해 이 쿼리는 다음과 같은 형식의 XML을 생성합니다.  
  
```  
< Product ProductModelID="...">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
-   WHERE 절에서는 **exist ()** 메서드를 사용 하 여 <`Picture`> 요소가 포함 된 제품 카탈로그 설명이 있는 행만 검색 합니다.  
  
-   WHERE 절은 **value ()** 메서드를 두 번 사용 하 여 <`Size`> 및 <`Angle`> 요소의 값을 비교 합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<p1:Product   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. 각 쌍이 \<기능> 요소에 포함 된 제품 모델 이름 및 기능 쌍의 단순 목록을 만듭니다.  
 제품 모델 카탈로그 설명에서 XML에는 몇 가지 제품 기능이 포함됩니다. 이러한 모든 기능은 <`Features`> 요소에 포함 됩니다. 쿼리에서 [Xml 생성 (XQuery)](../xquery/xml-construction-xquery.md) 을 사용 하 여 필요한 xml을 생성 합니다. 중괄호에 있는 식은 결과로 대체됩니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
-   $pd/p1: Features/*는 <`Features`>의 요소 노드 자식만 반환 하지만 $pd/P1: features/node ()는 모든 노드를 반환 합니다. 여기에는 요소 노드, 텍스트 노드, 처리 명령 및 주석이 포함됩니다.  
  
-   두 개의 FOR 루프는 제품 이름 및 개별 기능이 반환되는 카티션 곱을 생성합니다.  
  
-   **ProductName** 은 특성입니다. 이 쿼리의 XML 생성은 해당 항목을 요소로 반환합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. 제품 모델의 카탈로그 설명에서 product> 요소 내에 \<그룹화 된 제품 모델 이름, 모델 ID 및 기능을 나열 합니다.  
 다음 쿼리는 제품 모델의 카탈로그 설명에 저장 된 정보를 사용 하 여 product> 요소 내 \<에 그룹화 된 제품 모델 이름, 모델 ID 및 기능을 나열 합니다.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  <p3:wheel xmlns:p3="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. 제품 모델 기능 설명 검색  
 다음 쿼리는 **ProducModelID**, 제품 **modelname** 특성 및 `Product` 처음 두 제품 기능을 포함 하는 <> 요소를 포함 하는 XML을 생성 합니다. 특히 처음 두 제품 기능은 <`Features`> 요소의 처음 두 자식 요소입니다. 더 많은 기능이 있는 경우 빈 <`There-is-more/`> 요소를 반환 합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
-   ... RETURN 루프 구조는 처음 두 제품 기능을 검색 합니다. **Position ()** 함수는 시퀀스에서 요소의 위치를 찾는 데 사용 됩니다.  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. 제품 카탈로그 설명에서 "ons"로 끝나는 요소 이름 찾기  
 다음 쿼리는 카탈로그 설명을 검색 하 고 이름이 "기능"으로 끝나는 <`ProductDescription`> 요소의 모든 요소를 반환 합니다.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
                     <p1:Specifications xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. "Aerodynamic"이라는 단어가 포함된 요약 설명 찾기  
 다음 쿼리는 제품 카탈로그의 요약 설명에 "Aerodynamic"이라는 단어가 포함된 제품 모델을 검색합니다.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
 SELECT 쿼리는 **xml** 데이터 형식의 **query ()** 및 **value ()** 메서드를 지정 합니다. 따라서 두 개의 서로 다른 쿼리 프롤로그에 있는 네임스페이스 선언을 두 번 반복하는 대신 pd 접두사가 쿼리에서 사용되고 WITH XMLNAMESPACES를 사용하여 한 번만 정의됩니다.  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   WHERE 절은 카탈로그 설명이 <`Summary`> 요소에서 "Aerodynamic" 이라는 단어를 포함 하는 행만 검색 하는 데 사용 됩니다.  
  
-   **Contains ()** 함수는 단어가 텍스트에 포함 되는지 여부를 확인 하는 데 사용 됩니다.  
  
-   **Xml** 데이터 형식의 **value ()** 메서드는 **contains ()** 에 의해 반환 된 값을 1로 비교 합니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. 카탈로그 설명에 제품 모델 사진이 포함되지 않은 제품 모델 찾기  
 다음 쿼리는 카탈로그 설명에 <`Picture`> 요소가 포함 되지 않은 제품 모델에 대 한 제품 모드 뚜껑을 검색 합니다.  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   WHERE 절의 **exist ()** 메서드가 False (0)를 반환 하는 경우 제품 모델 ID가 반환 됩니다. 그렇지 않으면 제품 모델 ID가 반환되지 않습니다.  
  
-   모든 제품 설명에는 <`Picture`> 요소가 포함 되어 있으므로이 경우 결과 집합이 비어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [계층 구조와 관련 된 XQueries](../xquery/xqueries-involving-hierarchy.md)   
 [순서와 관련 된 XQueries](../xquery/xqueries-involving-order.md)   
 [관계형 데이터를 처리 하는 XQueries](../xquery/xqueries-handling-relational-data.md)   
 [XQuery에서 문자열 검색](../xquery/string-search-in-xquery.md)   
 [XQuery의 네임 스페이스 처리](../xquery/handling-namespaces-in-xquery.md)   
 [WITH XMLNAMESPACES를 사용 하 여 쿼리에 네임 스페이스 추가](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML 데이터 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
