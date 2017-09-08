---
title: "query () 메서드 (xml 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query method
- query() method
ms.assetid: f48f6f7b-219f-463a-bf36-bc10f21afaeb
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: db0f9b1ffc4c6ca13084942144e13d64765d7019
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="query-method-xml-data-type"></a>query() 메서드(xml 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  인스턴스에 대해 XQuery를 지정 된 **xml** 데이터 형식입니다. 결과 **xml** 유형입니다. 이 메서드는 형식화되지 않은 XML의 인스턴스를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
query ('XQuery')  
```  
  
## <a name="arguments"></a>인수  
 XQuery  
 문자열인 XQuery 식으로 XML 인스턴스에서 요소, 특성 같은 XML 노드를 쿼리합니다.  
  
## <a name="examples"></a>예  
 이 섹션에서는의 query () 메서드를 사용 하는 예제는 **xml** 데이터 형식입니다.  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>1. xml 형식 변수에 대해 query() 메서드 사용  
 다음 예제에서는 변수를 선언  **@myDoc**  의 **xml** 입력 하 고 XML 인스턴스를 할당 합니다. **query ()** 메서드는 다음 문서에 대해 XQuery를 지정 하는 데 사용 됩니다.  
  
 쿼리에서는 <`ProductDescription`> 요소의 <`Features`> 자식 요소를 검색합니다.  
  
```  
declare @myDoc xml  
set @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc.query('/Root/ProductDescription/Features')  
```  
  
 다음은 결과입니다.  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### <a name="b-using-the-query-method-against-an-xml-type-column"></a>2. XML 형식 열에 대해 query() 메서드 사용  
 다음 예제에서는 **query ()** 메서드 지정에 대해 XQuery를 사용 하는 **CatalogDescription** 열 **xml** 에 입력의  **AdventureWorks** 데이터베이스:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   CatalogDescription 열은 형식화 된 **xml** 열입니다. 즉, 이 열에 연결된 스키마 컬렉션이 있다는 의미입니다. 에 [XQuery 프롤로그](../../xquery/modules-and-prologs-xquery-prolog.md), **네임 스페이스** 키워드는 쿼리 본문에 나중에 사용 되는 접두사를 정의 하는 데 사용 됩니다.  
  
-   **query ()** 메서드는 XML을 생성 한 <`Product`> 된 요소는 **ProductModelID** 있는 특성은 **ProductModelID** 특성 값이 데이터베이스에서 검색 합니다. XML 생성에 대 한 자세한 내용은 참조 하십시오. [XML 생성 &#40; XQuery &#41; ](../../xquery/xml-construction-xquery.md).  
  
-   [exist () 메서드 (XML 데이터 형식)](../../t-sql/xml/exist-method-xml-data-type.md) 포함 된 행만을 찾기 위해 WHERE 절 사용에 <`Warranty`> xml에서 요소입니다. 다시,는 **네임 스페이스** 키워드는 두 개의 네임 스페이스 접두사를 정의 하는 데 사용 됩니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
 query() 메서드와 exist() 메서드는 모두 PD 접두사를 선언합니다. 이 경우 WITH XMLNAMESPACES를 사용하여 접두사를 먼저 정의하고 쿼리에서 이를 사용할 수 있습니다.  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
## <a name="see-also"></a>관련 항목:  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 데이터 수정 언어 &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

