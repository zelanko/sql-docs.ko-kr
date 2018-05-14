---
title: query() 메서드(xml 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 82f56308ec18e2c3b8bde437e2d776f9daf05120
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="query-method-xml-data-type"></a>query() 메서드(xml 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **xml** 데이터 형식의 인스턴스에 대해 XQuery를 지정합니다. 결과는 **xml** 형식이 됩니다. 이 메서드는 형식화되지 않은 XML의 인스턴스를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
query ('XQuery')  
```  
  
## <a name="arguments"></a>인수  
 XQuery  
 문자열인 XQuery 식으로 XML 인스턴스에서 요소, 특성 같은 XML 노드를 쿼리합니다.  
  
## <a name="examples"></a>예  
 이 섹션에서는 **xml** 데이터 형식의 query() 메서드를 사용하는 예를 보여 줍니다.  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>1. xml 형식 변수에 대해 query() 메서드 사용  
 다음 예에서는 **xml** 형식의 **@myDoc** 변수를 선언하고 여기에 XML 인스턴스를 할당합니다. 그런 다음, **query()** 메서드를 사용하여 문서에 대해 XQuery를 지정합니다.  
  
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
 다음 예에서는 **query()** 메서드를 사용하여 **AdventureWorks** 데이터베이스에서 **xml** 형식의 **CatalogDescription** 열에 XQuery를 지정합니다.  
  
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
  
-   CatalogDescription 열은 형식화된 **xml** 열입니다. 즉, 이 열에 연결된 스키마 컬렉션이 있다는 의미입니다. [XQuery 프롤로그](../../xquery/modules-and-prologs-xquery-prolog.md)에서는 **namespace** 키워드를 사용하여 나중에 쿼리 본문에 사용될 접두사를 정의합니다.  
  
-   **query()** 메서드는 **ProductModelID** 특성이 있는 XML <`Product`> 요소를 생성하는데, 이 경우 **ProductModelID** 특성 값을 데이터베이스에서 검색합니다. XML 생성에 대한 자세한 내용은 [XML 생성&#40;XQuery&#41;](../../xquery/xml-construction-xquery.md)을 참조하세요.  
  
-   WHERE 절의 [exist() 메서드(XML 데이터 형식)](../../t-sql/xml/exist-method-xml-data-type.md)를 사용하여 XML에서 <`Warranty`> 요소를 포함하는 행만 찾습니다. 다시 **namespace** 키워드를 사용하여 두 개의 네임스페이스 접두사를 정의합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
 query() 메서드와 exist() 메서드는 모두 PD 접두사를 선언합니다. 이 경우 WITH XMLNAMESPACES를 사용하여 접두사를 먼저 정의하고 쿼리에서 이를 사용할 수 있습니다.  
  
```  
WITH XMLNAMESPACES 
(  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM
)  
SELECT CatalogDescription.query('<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />')
       AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/PD:ProductDescription/PD:Features/WM:Warranty ') = 1;

```  
  
## <a name="see-also"></a>참고 항목  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
