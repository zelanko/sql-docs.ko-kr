---
title: 클라이언트 쪽 및 서버 쪽 XML 서식 지정 (SQLXML)
description: SQLXML 4.0에서 클라이언트 쪽 및 서버 쪽 XML 서식의 일반적인 차이점에 대해 알아봅니다.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- FOR XML clause, formatting
- client-side XML formatting
- server-side XPath
- server-side XML formatting
- AUTO mode
- client-side XPath
ms.assetid: f807ab7a-c5f8-4e61-9b00-23aebfabc47e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 34eb3a31a9b2affc473338cb730dddeee2f87904
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84882898"
---
# <a name="client-side-vs-server-side-xml-formatting-sqlxml-40"></a>클라이언트 쪽 vs. 서버 쪽 XML 서식 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 SQL XML의 클라이언트 쪽 XML 서식과 서버 쪽 XML 서식의 일반적인 차이점에 대해 설명합니다.  
  
## <a name="multiple-rowset-queries-not-supported-in-client-side-formatting"></a>클라이언트 쪽 서식에서 지원되지 않는 여러 행 집합 쿼리  
 클라이언트 쪽 XML 서식을 사용하는 경우 여러 행 집합을 생성하는 쿼리는 지원되지 않습니다. 예를 들어 가상 디렉터리에 클라이언트 쪽 서식을 지정했다고 가정합니다. 블록에 SELECT 문이 두 개 있는이 샘플 템플릿을 살펴보겠습니다 **\<sql:query>** .  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
     SELECT FirstName FROM Person.Contact FOR XML Nested;   
     SELECT LastName FROM Person.Contact FOR XML Nested    
  </sql:query>  
</ROOT>  
```  
  
 애플리케이션 코드에서 이 템플릿을 실행할 수 있지만 클라이언트 쪽 XML 서식에서 여러 행 집합의 서식 설정을 지원하지 않기 때문에 오류가 반환됩니다. 별도의 두 블록에 쿼리를 지정 하는 경우 **\<sql:query>** 원하는 결과를 얻을 수 있습니다.  
  
## <a name="timestamp-maps-differently-in-client--vs-server-side-formatting"></a>클라이언트 쪽 서식과 서버 쪽 서식에서 서로 다르게 매핑되는 타임스탬프  
 서버 쪽 XML 서식에서 **timestamp** 형식의 데이터베이스 열은 i8 XDR 형식 (쿼리에서 XMLDATA 옵션이 지정 된 경우)에 매핑됩니다.  
  
 클라이언트 쪽 XML 서식에서 **timestamp** 형식의 데이터베이스 열은 **uri** 또는 **bin. base64** XDR 형식에 매핑됩니다 (binary base64 옵션이 쿼리에 지정 되어 있는지 여부에 따라 다름). Updategram **bin.base64** 및 bulkload 기능을 사용 하는 경우이 형식이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **타임 스탬프** 형식으로 변환 되기 때문에 bin을 사용 하면 유용 합니다. 이러한 변환 작업을 통해 삽입, 업데이트 또는 삭제 작업이 성공합니다.  
  
## <a name="deep-variants-are-used-in-server-side-formatting"></a>서버 쪽 서식에는 중첩이 많은 VARIANT가 사용됨  
 서버 쪽 XML 서식에는 중첩이 많은 VARIANT 형식이 사용됩니다. 클라이언트 쪽 XML 서식을 사용하는 경우 변형은 유니코드 문자열로 변환되고 VARIANT의 하위 유형은 사용되지 않습니다.  
  
## <a name="nested-mode-vs-auto-mode"></a>NESTED 모드와 AUTO 모드  
 클라이언트 쪽 FOR XML의 NESTED 모드는 서버 쪽 FOR XML의 AUTO 모드와 비슷합니다. 단, 다음 사항은 예외입니다.  
  
### <a name="when-you-query-views-using-auto-mode-on-the-server-side-the-view-name-is-returned-as-the-element-name-in-the-resulting-xml"></a>서버 쪽에서 AUTO 모드를 사용하여 뷰를 쿼리하면 뷰 이름이 결과 XML에 요소 이름으로 반환됩니다.  
 예를 들어 AdventureWorksdatabase의 Person 테이블에 다음 뷰가 생성 되어 있다고 가정 합니다.  
  
```  
CREATE VIEW ContactView AS (SELECT ContactID as CID,  
                               FirstName  as FName,  
                               LastName  as LName  
                        FROM Person.Contact)  
```  
  
 다음 템플릿에서는 ContactView 뷰에 대해 쿼리를 지정하고 서버 쪽 XML 서식도 지정합니다.  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT *  
    FROM   ContactView  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 템플릿을 실행하면 다음 XML이 반환됩니다. (일부 결과만 표시 됩니다.) 요소 이름은 쿼리가 실행 되는 뷰의 이름입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ContactView CID="1" FName="Gustavo" LName="Achong" />   
  <ContactView CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
 해당 NESTED 모드를 사용하여 클라이언트 쪽 XML 서식을 지정하면 기본 테이블 이름이 결과 XML에 요소 이름으로 반환됩니다. 예를 들어 다음 수정 된 템플릿은 동일한 SELECT 문을 실행 하지만 XML 서식 지정은 클라이언트 쪽에서 수행 됩니다. 즉, **클라이언트 쪽 xml** 은 템플릿에서 true로 설정 됩니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT *  
    FROM   ContactView  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 이 템플릿을 실행하면 다음과 같은 XML이 생성됩니다. 이 경우 요소 이름은 기본 테이블 이름입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact CID="1" FName="Gustavo" LName="Achong" />   
  <Person.Contact CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
### <a name="when-you-use-auto-mode-of-the-server-side-for-xml-the-table-aliases-specified-in-the-query-are-returned-as-element-names-in-the-resulting-xml"></a>서버 쪽 FOR XML의 AUTO 모드를 사용하는 경우 쿼리에 지정된 테이블 별칭이 결과 XML에 요소 이름으로 반환됩니다.  
 예를 들어 다음 템플릿을 참조하십시오.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 이 템플릿을 실행하면 다음과 같은 XML이 생성됩니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <C fname="Gustavo" lname="Achong" />   
  <C fname="Catherine" lname="Abel" />   
...  
</ROOT>   
```  
  
 클라이언트 쪽 FOR XML의 NESTED 모드를 사용하는 경우 테이블 이름이 결과 XML에 요소 이름으로 반환되고 쿼리에 지정 된 테이블 별칭은 사용 되지 않습니다. 예를 들어 다음 템플릿을 살펴보세요.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 이 템플릿을 실행하면 다음과 같은 XML이 생성됩니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact fname="Gustavo" lname="Achong" />   
  <Person.Contact fname="Catherine" lname="Abel" />   
...  
</ROOT>  
```  
  
### <a name="if-you-have-a-query-that-returns-columns-as-dbobject-queries-you-cannot-use-aliases-for-these-columns"></a>쿼리에서 열을 dbobject 쿼리로 반환하는 경우 해당 열의 별칭을 사용할 수 없습니다.  
 예를 들어 다음 템플릿을 살펴보겠습니다. 이 템플릿에서는 직원 ID와 사진을 반환하는 쿼리를 실행합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query client-side-xml="1">  
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML NESTED, elements  
</sql:query>  
</ROOT>  
```  
  
 이 템플릿을 실행하면 Photo 열이 dbobject 쿼리로 반환됩니다. 이 dbobject 쿼리에서 `@P`는 존재하지 않는 열 이름을 나타냅니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@P</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
 XML 형식이 서버 (**클라이언트 쪽 xml = "0"**)에서 수행 되는 경우에는 별칭을 사용 하 여 실제 테이블 및 열 이름이 반환 되는 dbobject 쿼리를 반환 하는 열에 별칭을 사용할 수 있습니다 (별칭을 지정한 경우에도). 예를 들어 다음 템플릿은 쿼리를 실행 하 고 XML 서식 지정은 서버에서 수행 됩니다. 즉, **클라이언트 쪽 xml** 옵션이 지정 되지 않고 **클라이언트에서 실행** 옵션이 가상 루트에 대해 선택 되지 않습니다. 또한 이 쿼리는 클라이언트 쪽 NESTED 모드가 아니라 AUTO 모드를 지정합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query   
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML AUTO, elements  
</sql:query>  
</ROOT>  
```  
  
 이 템플릿을 실행하면 다음 XML 문서가 반환됩니다. 이 경우 LargePhoto 열에 대한 dbobject 쿼리에 별칭이 사용되지 않습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@LargePhoto</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
### <a name="client-side-vs-server-side-xpath"></a>클라이언트 쪽 XPath와 서버 쪽 XPath  
 클라이언트 쪽 XPath와 서버 쪽 XPath는 다음을 제외하고는 동일하게 작동합니다.  
  
-   클라이언트 쪽 XPath 쿼리를 사용할 때 적용되는 데이터 변환은 서버 쪽 XPath 쿼리를 사용할 때 적용되는 데이터 변환과 다릅니다. 클라이언트 쪽 XPath에는 CONVERT 모드 126 대신 CAST가 사용됩니다.  
  
-   템플릿에서 **클라이언트-xml = "0"** (false)을 지정 하면 서버 쪽 xml 서식 지정을 요청 하는 것입니다. 따라서 서버에서는 NESTED 옵션이 인식되지 않으므로 FOR XML NESTED를 지정할 수 없습니다. 이렇게 하면 오류가 발생합니다. 서버에서 인식되는 AUTO, RAW 또는 EXPLICIT 모드를 사용해야 합니다.  
  
-   템플릿에서 **클라이언트-xml = "1"** (true)을 지정 하면 클라이언트 쪽 xml 서식 지정을 요청 하는 것입니다. 이 경우 FOR XML NESTED를 지정할 수 있습니다. FOR XML AUTO를 지정 하면 **클라이언트 쪽 xml = "1"** 이 템플릿에 지정 된 경우에도 서버 쪽에서 xml 서식 지정이 수행 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 보안 고려 사항은 SQLXML 4.0을 &#40;&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [클라이언트 쪽 XML 서식 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [서버 쪽 XML 서식 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/server-side-xml-formatting-sqlxml-4-0.md)  
  
  
