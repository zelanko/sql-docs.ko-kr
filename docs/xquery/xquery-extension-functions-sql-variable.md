---
title: sql:변수() 함수 (XQuery) | 마이크로 소프트 문서
description: XQuery Extension 함수 sql:variable()를 사용하여 XQuery 식 내에 SQL 관계값이 포함된 변수를 노출하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 8241e15643eb4aa25912451ddfed94699954797f
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388601"
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery 확장 함수 - sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 식 내의 SQL 관계형 값을 포함하는 변수를 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>설명  
 [XML 내부의 관계형 데이터 바인딩](../t-sql/xml/binding-relational-data-inside-xml-data.md)항목에서 설명한 대로 [XML 데이터 형식 메서드를](../t-sql/xml/xml-data-type-methods.md) 사용하여 XQuery 내부에 관계형 값을 노출할 때 이 함수를 사용할 수 있습니다.  
  
 예를 들어 [query() 메서드는](../t-sql/xml/query-method-xml-data-type.md) **xml** 데이터 형식 변수 또는 열에 저장 되는 XML 인스턴스에 대 한 쿼리를 지정 하는 데 사용 됩니다. 일부 경우에는 쿼리에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 변수 또는 매개 변수로부터 값을 사용하거나 관계형 및 XML 데이터를 함께 사용할 수 있습니다. 이렇게 하려면 **sql:변수** 함수를 사용합니다.  
  
 SQL 값은 해당 XQuery 값에 매핑되고 해당 형식은 해당 SQL 형식과 동일한 XQuery 기본 형식입니다.  
  
 **XML-DML** 삽입 문의 소스 식 컨텍스트에서만 xml 인스턴스를 참조할 수 있습니다. 그렇지 않으면 **xml** 형식또는 CLR(공통 언어 런타임) 사용자 정의 형식의 값을 참조할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. sql:variable() 함수를 사용하여 Transact-SQL 변수 값을 XML로 가져오기  
 다음 예에서는 다음으로 구성된 XML 인스턴스를 생성합니다.  
  
-   비-XML 열의 값(`ProductID`). [sql:column() 함수는](../xquery/xquery-extension-functions-sql-column.md) XML에서 이 값을 바인딩하는 데 사용됩니다.  
  
-   다른 테이블에 있는 비-XML 열의 값(`ListPrice`). 여기에서도 XML에서 이 값을 바인딩하는 데 `sql:column()`이 사용됩니다.  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] 변수의 값(`DiscountPrice`). XML로 이 값을 바인딩하는 데 `sql:variable()` 메서드가 사용됩니다.  
  
-   **xml** `ProductModelName`형식 열의 값 () 을 사용하여 쿼리를 더 흥미롭게 만듭니다.  
  
 다음은 쿼리입니다.  
  
```sql
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
       <Product   
           ProductID="{ sql:column("Production.Product.ProductID") }"  
           ProductModelID= "{ sql:column("Production.Product.ProductModelID") }"  
           ProductModelName="{/pd:ProductDescription[1]/@ProductModelName }"  
           ListPrice="{ sql:column("Production.Product.ListPrice") }"  
           DiscountPrice="{ sql:variable("@price") }"  
        />')   
FROM Production.Product   
JOIN Production.ProductModel  
ON Production.Product.ProductModelID = Production.ProductModel.ProductModelID  
WHERE ProductID=771  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `query()` 메서드 내부의 XQuery는 XML을 생성합니다.  
  
-   키워드는 `namespace` [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md)에서 네임스페이스 접두사를 정의하는 데 사용됩니다. 이러한 작업은 스키마가 연결되어 있는 `ProductModelName` 유형의 열에서 `CatalogDescription xml` 특성 값이 검색되기 때문에 수행됩니다.  
  
 다음은 결과입니다.  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL 서버 XQuery 확장 함수](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [형식XML과 형식이 없는 XML 비교](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [SQL 서버&#41;&#40;XML 데이터](../relational-databases/xml/xml-data-sql-server.md)   
 [XML 데이터의 인스턴스 생성](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 방법](../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
