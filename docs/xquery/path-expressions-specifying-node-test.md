---
title: "경로 식 단계에서 노드 테스트 지정 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- axis step [XQuery]
- node test [XQuery]
ms.assetid: ffe27a4c-fdf3-4c66-94f1-7e955a36cadd
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87ad8f138eee79e84b9cc1056959ebf93a2c3aaa
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="path-expressions---specifying-node-test"></a>경로 식에서 노드 테스트 지정
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  경로 식의 축 단계는 다음 구성 요소를 포함합니다.  
  
-   [축](../xquery/path-expressions-specifying-axis.md)  
  
-   노드 테스트  
  
-   [(선택 사항) 0 개 이상의 단계 한정자](../xquery/path-expressions-specifying-predicates.md)  
  
 자세한 내용은 참조 [경로 식 &#40; XQuery &#41; ](../xquery/path-expressions-xquery.md).  
  
 노드 테스트는 경로 식에서 축 단계의 두 번째 구성 요소이자 조건입니다. 단계에서 선택한 모든 노드는 이 조건을 충족시켜야 합니다. 경로 식 `/child::ProductDescription`의 경우 노드 테스트는 `ProductDescription`입니다. 이 단계에서는 이름이 ProductDescription인 요소 노드 자식만 검색합니다.  
  
 노드 테스트 조건은 다음을 포함할 수 있습니다.  
  
-   노드 이름 -  지정된 이름이 있는 주 노드 종류의 노드만 반환됩니다.  
  
-   노드 유형 -  지정된 유형의 노드만 반환됩니다.  
  
> [!NOTE]  
>  XQuery 경로 식에 지정된 노드 이름은 Transact-SQL 쿼리와 같은 데이터 정렬 구분 규칙이 적용되지 않고 항상 대/소문자를 구분합니다.  
  
## <a name="node-name-as-node-test"></a>노드 테스트로서의 노드 이름  
 경로 식 단계에서 노드 테스트로 노드 이름을 지정할 때는 주 노드 종류의 개념을 이해해야 합니다. 모든 축(child, parent 또는 attribute)에는 주 노드 종류가 있습니다. 예를 들어  
  
-   attribute 축은 특성만 포함할 수 있습니다. 따라서 특성 노드는 attribute 축의 주 노드 종류입니다.  
  
-   기타 축의 경우 축에서 선택한 노드에 요소 노드를 포함할 수 있는 경우 요소는 해당 축의 주 노드 종류입니다.  
  
 노드 테스트로 노드 이름을 지정할 때는 해당 단계에서 다음 유형의 노드를 반환합니다.  
  
-   축의 주 노드 종류인 노드  
  
-   노드 테스트에 지정된 것과 같은 이름이 있는 노드  
  
 예를 들어 다음 경로 식을 참조하십시오.  
  
```  
child::ProductDescription   
```  
  
 이 1단계 식은 `child` 축을 지정하고 노드 테스트로 `ProductDescription`이라는 노드 이름을 지정합니다. 식은 주 노드 종류가 child 축인 노드, 요소 노드 및 노드 이름이 ProductDescription인 노드만 반환합니다.  
  
 경로 식 `/child::PD:ProductDescription/child::PD:Features/descendant::*,`에는 세 가지 단계가 있습니다. 이러한 단계는 child 축과 descendant 축을 지정합니다. 각 단계에서 노드 이름은 노드 테스트로 지정됩니다. 세 번째 단계의 와일드카드 문자(`*`)는 주 노드 종류가 descendant 축인 모든 노드를 나타냅니다. 축의 주 노드 종류는 선택된 노드의 유형 및 노드에서 선택한 노드 이름 필터를 확인합니다.  
  
 이 식의 제품 카탈로그 XML 문서에 대해 실행 되는 시기에 결과적으로 **ProductModel** 테이블의 모든 요소 노드 자식을 검색는 \<기능 > 요소 노드 자식을 \< ProductDescription > 요소입니다.  
  
 경로 식 `/child::PD:ProductDescription/attribute::ProductModelID`, 두 단계로 구성 됩니다. 이 두 단계는 노드 테스트로 노드 이름을 지정합니다. 또한 두 번째 단계에서는 attribute 축을 사용합니다. 그러므로 각 단계는 노드 테스트로 이름이 지정된 축의 주 노드 종류인 노드를 선택합니다. 따라서이 식은 반환 **ProductModelID** 특성 노드는 \<ProductDescription > 요소 노드.  
  
 노드 테스트에 대해 노드의 이름을 지정할 때 다음 예에서처럼 와일드카드 문자(*)를 사용하여 노드의 로컬 이름 또는 그 네임스페이스 접두사를 지정할 수 있습니다.  
  
```  
declare @x xml  
set @x = '  
<greeting xmlns="ns1">  
   <salutation>hello</salutation>  
</greeting>  
<greeting xmlns="ns2">  
   <salutation>welcome</salutation>  
</greeting>  
<farewell xmlns="ns1" />'  
select @x.query('//*:greeting')  
select @x.query('declare namespace ns="ns1"; /ns:*')  
```  
  
## <a name="node-type-as-node-test"></a>노드 테스트로서의 노드 유형  
 요소 노드가 아닌 노드 유형을 쿼리하려면 노드 유형 테스트를 사용합니다. 다음 표에 표시된 것처럼 사용 가능한 노드 유형 테스트는 네 가지입니다.  
  
|노드 유형|반환 값|예제|  
|---------------|-------------|-------------|  
|`comment()`|주석 노드에 대해 True|`following::comment()`는 컨텍스트 노드 다음에 나타나는 모든 주석 노드를 선택합니다.|  
|`node()`|모든 종류의 노드에 대해 True|`preceding::node()`는 컨텍스트 노드 이전에 나타나는 모든 노드를 선택합니다.|  
|`processing-instruction()`|처리 명령 노드에 대해 True|`self::processing instruction()`은 컨텍스트 노드 내의 모든 처리 명령 노드를 선택합니다.|  
|`text()`|텍스트 노드에 대해 True|`child::text()`는 컨텍스트 노드의 자식인 텍스트 노드를 선택합니다.|  
  
 text() 또는 comment()와 같은 노드 유형이 노드 테스트로 지정되어 있는 경우 이 단계에서는 축의 주 노드 종류에 관계없이 지정된 종류의 노드만 반환합니다. 예를 들어 다음 경로 식은 컨텍스트 노드의 주석 노드 자식만 반환합니다.  
  
```  
child::comment()  
```  
  
 마찬가지로, `/child::ProductDescription/child::Features/child::comment()` 주석 노드 자식을 검색은 \<기능 > 요소 노드 자식을 \<ProductDescription > 요소 노드.  
  
## <a name="examples"></a>예  
 다음 예에서는 노드 이름과 노드 종류를 비교합니다.  
  
### <a name="a-results-of-specifying-the-node-name-and-the-node-type-as-node-tests-in-a-path-expression"></a>1. 경로 식에서 노드 테스트로 노드 이름과 노드 유형을 지정한 결과  
 다음 예제에서는 간단한 XML 문서에 할당 됩니다는 **xml** 유형 변수입니다. 문서는 다른 경로 식을 사용하여 쿼리됩니다. 그런 다음 결과가 비교됩니다.  
  
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
select @x.query('  
/child::a/child::b/descendant::*  
')  
```  
  
 이 식에서는 `<b>` 요소 노드의 하위 항목 요소 노드를 묻습니다.  
  
 노드 테스트의 별표(`*`)는 노드 이름에 대한 와일드카드 문자를 나타냅니다. descendant 축에는 주 노드 종류로 요소 노드가 있습니다. 따라서 식은 `<b>` 요소 노드의 모든 하위 항목 요소 노드를 반환합니다. 즉, 다음 결과에서처럼 `<c>` 및 `<d>` 요소 노드가 반환됩니다.  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 descendant 축을 지정하는 대신 descendent-or-self 축을 지정하면 컨텍스트 노드가 반환되고 그 하위 항목도 반환됩니다.  
  
```  
/child::a/child::b/descendant-or-self::*  
```  
  
 이 식은 `<b>` 요소 노드 및 그 하위 항목 요소 노드를 반환합니다. 하위 항목 노드를 반환할 때 descendant-or-self 축의 주 노드 종류인 요소 노드 유형에 따라 반환되는 노드의 종류가 결정됩니다.  
  
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
  
 이전 식에서는 노드 이름으로 와일드카드 문자를 사용했습니다. 그 대신 이 식에 표시된 대로 `node()` 함수를 사용할 수 있습니다.  
  
```  
/child::a/child::b/descendant::node()  
```  
  
 때문에 `node()` 노드 형식이 descendant 축의 모든 노드를 받게 됩니다. 다음은 결과입니다.  
  
```  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
 또한 descendant-or-self 축 및 `node()`를 노드 테스트로 지정하는 경우 모든 하위 항목, 요소 및 텍스트 노드를 받고 컨텍스트 노드인 `<b>` 요소도 받게 됩니다.  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
### <a name="b-specifying-a-node-name-in-the-node-test"></a>2. 노드 테스트에서 노드 이름 지정  
 다음 예에서는 모든 경로 식에서 노드 테스트로 노드 이름을 지정합니다. 그 결과 모든 식에서 노드 테스트에 지정된 노드 이름이 있는 축에 대한 주 노드 종류의 노드를 반환합니다.  
  
 다음 쿼리 식은 `Production.ProductModel` 테이블에 저장된 제품 카탈로그 XML 문서에서 <`Warranty`> 요소를 반환합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:Warranty  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   XQuery 프롤로그의 `namespace` 키워드는 쿼리 본문에 사용되는 접두사를 정의합니다. XQuery 프롤로그에 대 한 자세한 내용은 참조 하십시오. [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 합니다.  
  
-   경로 식의 세 단계 모두 child 축 및 노드 이름을 노드 테스트로 지정합니다.  
  
-   축 단계의 선택적 단계 한정자 부분은 식의 어느 단계에서도 지정되지 않습니다.  
  
 쿼리는 <`ProductDescription`> 요소의 <`Features`> 요소 자식 중 <`Warranty`> 요소 자식을 반환합니다.  
  
 다음은 결과입니다.  
  
```  
<wm:Warranty xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
  <wm:Description>parts and labor</wm:Description>  
</wm:Warranty>     
```  
  
 다음 쿼리에서 경로 식은 노드 테스트에 와일드카드 문자(`*`)를 지정합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 와일드카드 문자는 노드 이름에 대해 지정됩니다. 따라서 쿼리는 <`ProductDescription`> 요소 노드의 <`Features`> 요소 노드 자식 중 모든 요소 노드 자식을 반환합니다.  
  
 다음 쿼리는 이전 쿼리와 비슷하지만 와일드카드 문자와 함께 네임스페이스가 지정되어 있다는 점이 다릅니다. 그 결과 해당 네이스페이스의 모든 요소 노드 자식이 반환됩니다. <`Features`> 요소에는 다른 네임스페이스의 요소가 포함될 수 있습니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 이 쿼리에 표시된 대로 네임스페이스 접두사로 와일드카드 문자를 사용할 수 있습니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*:Maintenance  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 이 쿼리는 제품 카탈로그 XML 문서에서 모든 네임스페이스의 <`Maintenance`> 요소 노드 자식을 반환합니다.  
  
### <a name="c-specifying-node-kind-in-the-node-test"></a>3. 노드 테스트에서 노드 종류 지정  
 다음 예에서는 모든 경로 식에서 노드 테스트로 노드 종류를 지정합니다. 그 결과 모든 식은 노드 테스트에 지정된 종류의 노드를 반환합니다.  
  
 다음 쿼리의 경우 경로 식이 세 번째 단계에서 노드 종류를 지정합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::text()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 다음 쿼리에서는 다음과 같이 지정됩니다.  
  
-   경로 식에는 슬래시 표시(`/`)로 구분되는 세 가지 단계가 있습니다.  
  
-   각 단계마다 child 축을 지정합니다.  
  
-   처음 두 단계는 노드 테스트로 노드 이름을 지정하고 세 번째 단계는 노드 테스트로 노드 종류를 지정합니다.  
  
-   식은 <`ProductDescription`> 요소 노드의 <`Features`> 요소 자식 중 텍스트 노드 자식을 반환합니다.  
  
 텍스트 노드 하나만 반환됩니다. 다음은 결과입니다.  
  
```  
These are the product highlights.   
```  
  
 다음 쿼리는 <`ProductDescription`> 요소의 주석 노드 자식을 반환합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::comment()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   두 번째 단계는 노드 테스트로 노드 종류를 지정합니다.  
  
-   그 결과 식은 <`ProductDescription`> 요소 노드의 주석 노드 자식을 반환합니다.  
  
 다음은 결과입니다.  
  
```  
<!-- add one or more of these elements... one for each specific product in this product model -->  
<!-- add any tags in <specifications> -->      
```  
  
 다음 쿼리는 최상위의 처리 명령 노드를 검색합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 다음은 결과입니다.  
  
```  
<?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>   
```  
  
 문자열 리터럴 매개 변수를 `processing-instruction()` 노드 테스트에 전달할 수 있습니다. 이 경우 쿼리에서는 그 이름 특성 값이 인수에 지정된 문자열 리터럴인 처리 명령을 반환합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction("xml-stylesheet")  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 특정 제한 사항은 다음과 같습니다.  
  
-   확장 SequenceType 노드 테스트는 지원되지 않습니다.  
  
-   처리 명령(이름)이 지원되지 않습니다. 대신 이름을 따옴표 안에 넣습니다.  
  
  
