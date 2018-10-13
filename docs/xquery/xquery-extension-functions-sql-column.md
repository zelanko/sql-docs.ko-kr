---
title: 1!s!sql:column () 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:column function
- sql:column() function
ms.assetid: e8f67bdf-b489-49a9-9d0f-2069c1750467
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 17703c8a4c4839b977da9f4583a90ea3c3583b52
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49119890"
---
# <a name="xquery-extension-functions---sqlcolumn"></a>XQuery 확장 함수 - sql:column()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  항목에 설명 된 대로 [관계형 데이터 내에서 XML 데이터 바인딩](../t-sql/xml/binding-relational-data-inside-xml-data.md)를 사용할 수는 **sql:column(()** 사용 하는 경우 함수 [XML 데이터 형식 메서드](../t-sql/xml/xml-data-type-methods.md) 관계형 값을 제공할 XQuery 내입니다.  
  
 예를 들어 합니다 [query () 메서드 (XML 데이터 형식)](../t-sql/xml/query-method-xml-data-type.md) 변수 또는 열에 저장 된 XML 인스턴스에 대해 쿼리를 지정 하는 데 사용 됩니다 **xml** 형식입니다. 쿼리에 다른 비-XML 열의 값을 사용하여 관계형 및 XML 데이터를 함께 가져올 수도 있습니다. 이 작업을 수행 하려면 사용 합니다 **1!s!sql:column ()** 함수입니다.  
  
 SQL 값은 해당 XQuery 값으로 매핑되고 이 값의 유형은 해당 SQL 유형과 같은 XQuery 기본 유형이 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sql:column("columnName")  
```  
  
## <a name="remarks"></a>Remarks  
 에 지정 된 열 참조를 **1!s!sql:column ()** XQuery 내의 함수는 처리 중인 행의 열을 참조 합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 참조할 수 있습니다는 **xml** XML-DML 원본 식의 컨텍스트에서 인스턴스 insert 문 형식의 열을 참조할 수 없습니다이 고, 그렇지 않으면 **xml** 또는 CLR 사용자 정의 형식입니다.  
  
 합니다 **1!s!sql:column ()** 함수가 조인 연산에 지원 되지 않습니다. 대신 APPLY 연산을 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-sqlcolumn-to-retrieve-the-relational-value-inside-xml"></a>1. sql:column()을 사용하여 XML 내의 관계형 값 검색  
 XML을 생성할 때 다음 예는 비-XML 관계형 열의 값을 검색하여 XML 및 관계형 데이터에 바인딩하는 방법을 보여 줍니다.  
  
 쿼리는 다음 형식의 XML을 생성합니다.  
  
```xml
<Product ProductID="771" ProductName="Mountain-100 Silver, 38" ProductPrice="3399.99" ProductModelID="19"   
  ProductModelName="Mountain 100" />  
```  
  
 생성된 XML에서 다음을 유의하십시오.  
  
-   합니다 **ProductID**, **ProductName**, 및 **ProductPrice** 특성 값에서 가져온 합니다 **제품** 테이블입니다.  
  
-   합니다 **ProductModelID** 에서 특성 값을 검색 합니다 **ProductModel** 테이블입니다.  
  
-   쿼리를 보다 유용 하 게 하도록 합니다 **ProductModelName** 특성 값에서 가져온 합니다 **CatalogDescription** 열의 **xml 형식**합니다. 모든 제품 모델에 대해 XML 제품 모델 카탈로그 정보가 저장되지는 않으므로 `if` 문을 사용하여 값이 있는 경우에만 해당 값을 검색합니다.  
  
    ```sql
    SELECT P.ProductID, CatalogDescription.query('  
    declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           <Product   
               ProductID=       "{ sql:column("P.ProductID") }"  
               ProductName=     "{ sql:column("P.Name") }"  
               ProductPrice=    "{ sql:column("P.ListPrice") }"  
               ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
               { if (not(empty(/pd:ProductDescription))) then  
                 attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
                else   
                   ()  
    }  
            </Product>  
    ') as Result  
    FROM Production.ProductModel PM, Production.Product P  
    WHERE PM.ProductModelID = P.ProductModelID  
    AND   CatalogDescription is not NULL  
    ORDER By PM.ProductModelID  
    ```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   값은 서로 다른 두 테이블에서 검색되므로 FROM 절은 두 개의 테이블을 지정합니다. WHERE 절의 조건은 결과를 필터링하고 제품 모델에 카탈로그 설명이 있는 제품만 검색합니다.  
  
-   합니다 **네임 스페이스** 키워드는 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) "pd" 쿼리 본문에 사용 되는 XML 네임 스페이스 접두사를 정의 합니다. 테이블 별칭 "P" 및 "PM"은 쿼리 자체의 FROM 절에 정의됩니다.  
  
-   합니다 **1!s!sql:column ()** 함수는 XML 내 비-XML 값을 사용 됩니다.  
  
 다음은 결과의 일부입니다.  
  
```  
ProductID               Result  
-----------------------------------------------------------------  
771         <Product ProductID="771"                   ProductName="Mountain-100 Silver, 38"   
                  ProductPrice="3399.99" ProductModelID="19"   
                  ProductModelName="Mountain 100" />  
...  
```  
  
 다음 쿼리는 제품의 특정 정보가 포함된 XML을 생성합니다. 이 정보에는 ProductID, ProductName, ProductPrice와 가능한 경우 특정 제품 모델 ProductModelID=19에 해당하는 모든 제품의 ProductModelName이 포함됩니다. XML에 할당 됩니다 합니다 @x 변수 **xml** 형식입니다.  
  
```sql
declare @x xml  
SELECT @x = CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <Product   
           ProductID=       "{ sql:column("P.ProductID") }"  
           ProductName=     "{ sql:column("P.Name") }"  
           ProductPrice=    "{ sql:column("P.ListPrice") }"  
           ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
           { if (not(empty(/pd:ProductDescription))) then  
             attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
            else   
               ()  
}  
        </Product>  
')   
FROM Production.ProductModel PM, Production.Product P  
WHERE PM.ProductModelID = P.ProductModelID  
And P.ProductModelID = 19  
select @x  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server XQuery 확장 함수](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML 데이터 인스턴스 만들기](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
