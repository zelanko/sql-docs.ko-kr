---
title: "WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가 | Microsoft 문서"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ELEMENTS XSINIL directive
- adding namespaces
- XSINIL directive
- default namespaces
- queries [XML in SQL Server], WITH XMLNAMESPACES clause
- predefined namespaces [XML in SQL Server]
- FOR XML clause, WITH XMLNAMESPACES clause
- namespaces [XML in SQL Server]
- xml data type [SQL Server], WITH XMLNAMESPACES clause
- WITH XMLNAMESPACES clause
ms.assetid: 2189cb5e-4460-46c5-a254-20c833ebbfec
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6730eac672d4803c3f50a200e83acb214b2986da
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="add-namespaces-to-queries-with-with-xmlnamespaces"></a>WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] [WITH XMLNAMESPACES(Transact-SQL)](../../t-sql/xml/with-xmlnamespaces.md)는 다음과 같은 방식으로 네임스페이스 URI를 지원합니다.  
  
-   [FOR XML을 사용하는 XML 생성](../../relational-databases/xml/for-xml-sql-server.md) 쿼리 시 URI 매핑에 대한 네임스페이스 접두사를 사용할 수 있도록 만듭니다.  
  
-   [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)의 정적 네임스페이스 컨텍스트에 URI 매핑에 대한 네임스페이스를 사용할 수 있도록 만듭니다.  
  
## <a name="using-with-xmlnamespaces-in-the-for-xml-queries"></a>FOR XML 쿼리에서 WITH XMLNAMESPACES 사용  
 WITH XMLNAMESPACES를 사용하면 FOR XML 쿼리에 XML 네임스페이스를 포함시킬 수 있습니다. 예를 들어 다음 FOR XML 쿼리를 참조하십시오.  
  
```  
SELECT ProductID, Name, Color  
FROM   Production.Product  
WHERE  ProductID=316 or ProductID=317  
FOR XML RAW  
```  
  
 다음은 결과입니다.  
  
```  
<row ProductID="316" Name="Blade" />  
<row ProductID="317" Name="LL Crankarm" Color="Black" />  
  
```  
  
 FOR XML 쿼리에 의해 생성된 XML에 네임스페이스를 추가하려면 먼저 WITH NAMESPACES 절을 사용하여 URI 매핑에 네임스페이스 접두사를 지정합니다. 그런 다음 수정된 다음 쿼리에 표시된 것과 같이 쿼리에 네임스페이스를 지정할 때 네임스페이스 접두사를 사용합니다. WITH XMLNAMESPACES 절은 URI(`ns1`) 매핑에 대해 네임스페이스 접두사(`uri`)를 지정합니다. `ns1` 접두사는 FOR XML 쿼리에 의해 생성되는 요소 및 특성 이름을 지정하는 데 사용됩니다.  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Prod'), ELEMENTS  
  
```  
  
 XML 결과에는 네임스페이스 접두사가 포함됩니다.  
  
```  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
</ns1:Prod>  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>317</ns1:ProductID>  
  <ns1:Name>LL Crankarm</ns1:Name>  
  <ns1:Color>Black</ns1:Color>  
</ns1:Prod>  
  
```  
  
 다음은 WITH XMLNAMESPACES 절에 적용됩니다.  
  
-   FOR XML 쿼리의 RAW, AUTO 및 PATH 모드에서만 지원됩니다. EXPLICIT 모드는 지원되지 않습니다.  
  
-   FOR XML 쿼리의 네임스페이스 접두사와 **xml** 데이터 형식 메서드에만 영향을 주고 XML 파서에는 영향을 주지 않습니다. 예를 들어 다음 쿼리는 XML 문서에 myNS 접두사에 대한 네임스페이스 선언이 없기 때문에 오류를 반환합니다.  
  
-   WITH XMLNAMESPACES 절을 사용하는 경우 FOR XML 지시어, XMLSCHEMA 및 XMLDATA는 사용할 수 없습니다.  
  
    ```  
    CREATE TABLE T (x xml)  
    go  
    WITH XMLNAMESPACES ('http://abc' as myNS )  
    INSERT INTO T VALUES('<myNS:root/>')  
    ```  
  
## <a name="using-the-xsinil-directive"></a>XSINIL 지시어 사용  
 ELEMENTS XSINIL 지시어를 사용할 때는 WITH XMLNAMESPACES 절에서 xsi 접두사를 정의할 수 없습니다. 대신 ELEMENTS XSINIL을 사용할 때 자동으로 추가됩니다. 다음 쿼리에서는 **xsi:nil** 특성이 True로 설정된 요소에 Null 값이 매핑되는 요소 중심 XML을 생성하는 ELEMENTS XSINIL을 사용합니다.  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316   
FOR XML RAW, ELEMENTS XSINIL  
```  
  
 다음은 결과입니다.  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
  <ns1:Color xsi:nil="true" />  
</row>  
```  
  
## <a name="specifying-default-namespaces"></a>기본 네임스페이스 지정  
 네임스페이스 접두사를 선언하는 대신 DEFAULT 키워드를 사용하여 기본 네임스페이스를 선언할 수 있습니다. FOR XML 쿼리에서 기본 네임스페이스를 결과 XML의 XML 노드에 바인딩합니다. 다음 예에서 WITH XMLNAMESPACES는 기본 네임스페이스와 함께 정의된 두 개의 네임스페이스 접두사를 정의합니다.  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,   
                    'uri2' as ns2,  
                    DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product   
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Product'), ROOT('ns2:root'), ELEMENTS  
```  
  
 FOR XML 쿼리는 요소 중심 XML을 생성합니다. 쿼리는 노드 이름 지정 시에 두 네임스페이스 접두사를 모두 사용합니다. SELECT 절에서 ProductID, Name 및 Color는 접두사가 포함된 이름을 지정하지 않습니다. 따라서 결과 XML의 해당 요소는 기본 네임스페이스에 속합니다.  
  
```  
<ns2:root xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">  
  <ns1:Product>  
    <ProductID>316</ProductID>  
    <Name>Blade</Name>  
  </ns1:Product>  
  <ns1:Product>  
    <ProductID>317</ProductID>  
    <Name>LL Crankarm</Name>  
    <Color>Black</Color>  
  </ns1:Product>  
</ns2:root>  
```  
  
 다음 쿼리는 이전 쿼리와 비슷하지만 FOR XML AUTO 모드가 지정되어 있습니다.  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,  'uri2' as ns2,DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product as "ns1:Product"  
WHERE ProductID=316 or ProductID=317  
FOR XML AUTO, ROOT('ns2:root'), ELEMENTS  
```  
  
## <a name="using-predefined-namespaces"></a>미리 정의된 네임스페이스 사용  
 ELEMENTS XSINIL이 사용되는 경우의 xml 네임스페이스 및 xsi 네임스페이스를 제외한 미리 정의된 네임스페이스를 사용하는 경우 WITH XMLNAMESPACES를 사용하여 네임스페이스 바인딩을 명시적으로 지정해야 합니다. 다음 쿼리는 미리 정의된 네임스페이스에 대해 URI 바인딩에 대한 네임스페이스 접두사를 명시적으로 정의합니다(`urn:schemas-microsoft-com:xml-sql`).  
  
```  
WITH XMLNAMESPACES ('urn:schemas-microsoft-com:xml-sql' as sql)  
SELECT 'SELECT * FROM Customers FOR XML AUTO, ROOT("a")' AS "sql:query"  
FOR XML PATH('sql:root')  
```  
  
 다음은 결과입니다. SQLXML 사용자는 이러한 XML 템플릿에 익숙합니다. 자세한 내용은 [SQLXML 4.0 프로그래밍 개념](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)을 참조하세요.  
  
```  
<sql:root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>SELECT * FROM Customers FOR XML AUTO, ROOT("a")</sql:query>  
</sql:root>  
```  
  
 다음 PATH 모드 쿼리에 표시된 것과 같이 WITH XMLNAMESPACES에 명시적으로 정의할 필요 없이 xml 네임스페이스 접두사만 사용할 수 있습니다. 또한 접두사가 선언된 경우 네임스페이스 http://www.w3.org/XML/1998/namespace에 바인딩되어야 합니다. SELECT 절에 지정된 이름은 WITH XMLNAMESPACES를 사용하여 명시적으로 정의되지 않은 xml 네임스페이스 접두사를 참조합니다.  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
go  
```  
  
 @xml:lang 특성은 미리 정의된 xml 네임스페이스를 사용합니다. XML 버전 1.0에는 xml 네임스페이스 바인딩에 대한 명시적 선언이 필요하지 않기 때문에 결과에는 네임스페이스 바인딩의 명시적 선언이 포함되지 않습니다.  
  
 다음은 결과입니다.  
  
```  
<Translation>  
  <English xml:lang="en">food</English>  
  <German xml:lang="ger">Essen</German>  
</Translation>  
```  
  
## <a name="using-with-xmlnamespaces-with-the-xml-data-type-methods"></a>xml 데이터 형식 메서드에서 WITH XMLNAMESPACES 사용  
 [modify()](../../t-sql/xml/xml-data-type-methods.md) 메서드인 경우 SELECT 쿼리 또는 UPDATE에 지정된 **xml 데이터 형식 메서드** 는 모두 해당 프롤로그에서 네임스페이스 선언을 반복해야 합니다. 이 작업은 시간이 많이 걸리는 작업입니다 예를 들어 다음 쿼리는 카탈로그 설명에 사양이 포함되지 않는 제품 모델 ID를 검색합니다. 즉, <`Specifications`> 요소가 있습니다.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
```  
  
 이전 쿼리에서 **query()** 및 **exist()** 메서드는 모두 해당 프롤로그에서 같은 네임스페이스를 선언합니다. 예를 들어  
  
```  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
```  
  
 또는 WITH XMLNAMESPACES를 먼저 선언하고 쿼리에 있는 네임스페이스 접두사를 사용할 수 있습니다. 이 경우 **query()** 및 **exist()** 메서드는 해당 프롤로그에 네임스페이스 선언을 포함시킬 필요가 없습니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
Go  
```  
  
 XQuery 프롤로그에 있는 명시적 선언은 네임스페이스 접두사와 WITH 절에 정의된 기본 요소 네임스페이스를 무시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)   
 [WITH XMLNAMESPACES&#40;Transact-SQL&#41;](../../t-sql/xml/with-xmlnamespaces.md)   
 [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
