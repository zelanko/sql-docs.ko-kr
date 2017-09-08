---
title: "경로 식 단계에서 축 지정 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
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
- attribute axis [SQL Server]
- axis step [XQuery]
- descendant axis
- self axis
- path expressions [XQuery]
- child axis
- descendant-or-self axis
- parent axis
ms.assetid: c44fb843-0626-4496-bde0-52ca0bac0a9e
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c34c230f6df65610466e087da5707622c3911e42
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="path-expressions---specifying-axis"></a>경로 식에서 축 지정
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  경로 식의 축 단계는 다음 구성 요소를 포함합니다.  
  
-   축  
  
-   A [노드 테스트](../xquery/path-expressions-specifying-node-test.md)  
  
-   [(선택 사항) 0 개 이상의 단계 한정자](../xquery/path-expressions-specifying-predicates.md)  
  
 자세한 내용은 참조 [경로 식 &#40; XQuery &#41; ](../xquery/path-expressions-xquery.md).  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 XQuery 구현은 다음 축 단계를 지원합니다.  
  
|축|Description|  
|----------|-----------------|  
|**자식**|컨텍스트 노드의 자식을 반환합니다.|  
|**하위 항목**|컨텍스트 노드의 모든 하위 노드를 반환합니다.|  
|**부모**|컨텍스트 노드의 부모를 반환합니다.|  
|**특성**|컨텍스트 노드의 특성을 반환합니다.|  
|**자체**|컨텍스트 노드 자신을 반환합니다.|  
|**하위 또는 자체**|컨텍스트 노드와 해당 컨텍스트 노드의 모든 하위 노드를 반환합니다.|  
  
 이러한 모든 축을 제외 하 고는 **부모** 축 정방향 축입니다. **부모** 축 문서 계층 구조에서 거꾸로 검색 하므로 역방향 축입니다가 있습니다. 예를 들어 상대 경로 식 `child::ProductDescription/child::Summary`에는 두 단계가 있는데 각 단계는 하나의 `child` 축을 지정합니다. 검색 하는 첫 번째 단계는 \<ProductDescription > 컨텍스트 노드의 요소 자식이 있습니다. 각 \<ProductDescription > 요소 노드를 두 번째 단계 검색는 \<요약 > 요소 노드 자식을 합니다.  
  
 상대 경로 식 `child::root/child::Location/attribute::LocationID`에는 세 단계가 있습니다. 처음 두 단계는 각각 `child` 축을 지정하고 세 번째 단계는 `attribute` 축을 지정합니다. 제조 지침 XML 문서에서 실행 될 때는 **Production.ProductModel** 테이블 식에서 반환 된 `LocationID` 특성의는 \<위치 >는 요소노드자식을\<루트 > 요소입니다.  
  
## <a name="examples"></a>예  
 이 항목의 쿼리 예제에 대해 지정 된 **xml** 유형 열에는 **AdventureWorks** 데이터베이스입니다.  
  
### <a name="a-specifying-a-child-axis"></a>1. child 축 지정  
 특정 제품 모델에 대해 다음 쿼리는 검색은 \<기능 > 요소 노드 자식을 \<ProductDescription >에 저장 된 제품 카탈로그 설명에서 요소 노드는 `Production.ProductModel` 테이블입니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `query()` 의 메서드는 **xml** 데이터 형식에는 경로 식을 지정 합니다.  
  
-   경로 식의 단계는 모두 `child` 축과 노드 이름, `ProductDescription`과 `Features`를 노드 테스트로서 지정합니다. 노드 테스트에 대 한 정보를 참조 하십시오. [경로 식 단계에서 노드 테스트 지정](../xquery/path-expressions-specifying-node-test.md)합니다.  
  
### <a name="b-specifying-descendant-and-descendant-or-self-axes"></a>2. descendant 및 descendant-or-self 축 지정  
 다음 예에서는 descendant 및 descendant-or-self 축을 사용합니다. 이 예의 쿼리에 대해 지정 됩니다는 **xml** 유형 변수입니다. 생성되는 결과의 차이점을 쉽게 설명하기 위해 XML 인스턴스를 단순화하였습니다.  
  
```  
declare @x xml  
set @x='  
<a>  
 <b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
 </b>  
</a>'  
declare @y xml  
set @y = @x.query('  
  /child::a/child::b  
')  
select @y  
```  
  
 아래 결과에서 식은 `<b>` 요소 노드의 `<a>` 요소 노드 자식을 반환합니다.  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
```  
  
 이 식에서 경로 식  
  
 `/child::a/child::b/descendant::*`에 대해 descendant 축을 지정하면 <`b`> 요소 노드의 모든 하위 노드를 검색합니다.  
  
 노드 테스트에서 별표(*)는 노드 테스트로서 노드 이름을 나타냅니다. 따라서 descendant 축의 기본 노드 유형인 요소 노드에 따라 반환되는 노드 유형이 결정됩니다. 즉, 식이 모든 요소 노드를 반환합니다. 텍스트 노드는 반환되지 않습니다. 주 노드 유형과 노드 테스트와의 관계에 대 한 자세한 내용은 참조 [경로 식 단계에서 노드 테스트 지정](../xquery/path-expressions-specifying-node-test.md) 항목입니다.  
  
 아래 결과에서 볼 수 있듯이 <`c`> 및 <`d`> 요소 노드가 반환됩니다.  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 descendant 축 대신 descendant-or-self 축을 지정하면 `/child::a/child::b/descendant-or-self::*`가 컨텍스트 노드, <`b`> 요소 및 그 하위 노드를 반환합니다.  
  
 다음은 결과입니다.  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
  
<c>text2  
     <d>text3</d>  
</c>  
  
<d>text3</d>   
```  
  
 에 대해 다음 예제 쿼리는 **AdventureWorks** 데이터베이스 검색의 모든 하위 항목 요소 노드는 <`Features`>의 자식 요소는 <`ProductDescription`> 요소:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features/descendant::*  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
### <a name="c-specifying-a-parent-axis"></a>3. parent 축 지정  
 다음 쿼리는 `Production.ProductModel` 테이블에 저장되어 있는 제품 카탈로그 XML 문서에서 <`ProductDescription`> 요소의 <`Summary`> 요소 자식을 반환합니다.  
  
 이 예에서는 parent 축을 사용하여 <`Feature`> 요소의 부모로 돌아가 <`ProductDescription`> 요소의 <`Summary`> 요소 자식을 검색합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
/child::PD:ProductDescription/child::PD:Features/parent::PD:ProductDescription/child::PD:Summary  
')  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
  
```  
  
 이 쿼리 예에서 경로 식은 `parent` 축을 사용합니다. 아래와 같이 parent 축을 사용하지 않도록 식을 다시 작성할 수 있습니다.  
  
```  
/child::PD:ProductDescription[child::PD:Features]/child::PD:Summary  
```  
  
 parent 축에 대한 보다 적절한 예는 아래와 같습니다.  
  
 에 저장 된 각 제품 모델 카탈로그 설명에서 **CatalogDescription** 의 열은 **ProductModel** 테이블에는 `<ProductDescription>` 된 요소는 `ProductModelID` 특성과 `<Features>`다음 조각에 나와 있는 것 처럼 자식 요소:  
  
```  
<ProductDescription ProductModelID="..." >  
  ...  
  <Features>  
    <Feature1>...</Feature1>  
    <Feature2>...</Feature2>  
   ...  
</ProductDescription>  
```  
  
 쿼리는 FLWOR 문에서 반복기 변수 `$f`를 설정하여 `<Features>` 요소의 요소 자식을 반환합니다. 자세한 내용은 참조 [FLWOR 문 및 반복 &#40; XQuery &#41; ](../xquery/flwor-statement-and-iteration-xquery.md). `return` 절은 각 기능에 대해 다음 형식으로 XML을 작성합니다.  
  
```  
<Feature ProductModelID="...">...</Feature>  
<Feature ProductModelID="...">...</Feature>  
```  
  
 각 `ProductModelID`> 요소에 대해 `<Feature`를 추가하기 위해 `parent` 축이 지정됩니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  for $f in /child::PD:ProductDescription/child::PD:Features/child::*  
  return  
   <Feature  
     ProductModelID="{ ($f/parent::PD:Features/parent::PD:ProductDescription/attribute::ProductModelID)[1]}" >  
          { $f }  
   </Feature>  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<Feature ProductModelID="19">  
  <wm:Warranty   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
    <wm:Description>parts and labor</wm:Description>  
  </wm:Warranty>  
</Feature>  
<Feature ProductModelID="19">  
  <wm:Maintenance   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:NoOfYears>10 years</wm:NoOfYears>  
    <wm:Description>maintenance contract available through your dealer   
                  or any AdventureWorks retail store.</wm:Description>  
  </wm:Maintenance>  
</Feature>  
<Feature ProductModelID="19">  
  <p1:wheel   
   xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">  
      High performance wheels.  
  </p1:wheel>  
</Feature>  
```  
  
 단일 값이 반환되도록 경로 식에서 `[1]` 조건자가 추가되었습니다.  
  
  
