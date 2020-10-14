---
title: 'sql: variable () 함수 (XQuery) | Microsoft Docs'
description: 'Xquery 확장 함수 sql: variable ()을 사용 하 여 XQuery 식 내에 SQL 관계형 값이 포함 된 변수를 노출 하는 방법을 알아봅니다.'
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
ms.openlocfilehash: 6ed7dd109906b4cace6ed185b1842f9e9e7dedde
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037041"
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery 확장 함수 - sql:variable()
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery 식 내의 SQL 관계형 값을 포함하는 변수를 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>설명  
 [Xml 내 관계형 데이터 바인딩](../t-sql/xml/binding-relational-data-inside-xml-data.md)항목에 설명 된 것 처럼 [xml 데이터 형식 메서드](../t-sql/xml/xml-data-type-methods.md) 를 사용 하 여 XQuery 내에 관계형 값을 노출할 때이 함수를 사용할 수 있습니다.  
  
 예를 들어 [query () 메서드](../t-sql/xml/query-method-xml-data-type.md) 는 **xml** 데이터 형식 변수 또는 열에 저장 된 xml 인스턴스에 대 한 쿼리를 지정 하는 데 사용 됩니다. 일부 경우에는 쿼리에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 변수 또는 매개 변수로부터 값을 사용하거나 관계형 및 XML 데이터를 함께 사용할 수 있습니다. 이렇게 하려면 **sql: variable** 함수를 사용 합니다.  
  
 SQL 값은 해당 XQuery 값에 매핑되고 해당 형식은 해당 SQL 형식에 해당 하는 XQuery 기본 형식이 됩니다.  
  
 Xml DML insert 문의 원본 식 컨텍스트에서만 **xml** 인스턴스를 참조할 수 있습니다. 그렇지 않으면 **xml** 형식의 값 또는 CLR (공용 언어 런타임) 사용자 정의 형식을 참조할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. sql:variable() 함수를 사용하여 Transact-SQL 변수 값을 XML로 가져오기  
 다음 예에서는 다음으로 구성된 XML 인스턴스를 생성합니다.  
  
-   비-XML 열의 값(`ProductID`). [Sql: column () 함수](../xquery/xquery-extension-functions-sql-column.md) 는이 값을 XML에 바인딩하는 데 사용 됩니다.  
  
-   다른 테이블에 있는 비-XML 열의 값(`ListPrice`). 여기에서도 XML에서 이 값을 바인딩하는 데 `sql:column()`이 사용됩니다.  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] 변수의 값(`DiscountPrice`). XML로 이 값을 바인딩하는 데 `sql:variable()` 메서드가 사용됩니다.  
  
-   `ProductModelName`보다 흥미로운 쿼리를 만들기 위해 **xml** 유형 열의 값 ()입니다.  
  
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
  
-   `namespace`키워드는 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md)에서 네임 스페이스 접두사를 정의 하는 데 사용 됩니다. 이러한 작업은 스키마가 연결되어 있는 `ProductModelName` 유형의 열에서 `CatalogDescription xml` 특성 값이 검색되기 때문에 수행됩니다.  
  
 다음은 결과입니다.  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server XQuery 확장 함수](./xquery-extension-functions-sql-column.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML 데이터 인스턴스 만들기](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
