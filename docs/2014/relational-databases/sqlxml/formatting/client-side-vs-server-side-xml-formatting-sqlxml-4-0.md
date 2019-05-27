---
title: 클라이언트 쪽 vs. 서버 쪽 XML 서식 지정 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 4eaa4667db1e8b6ed789e2adb90bc8d72c1b02e6
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012346"
---
# <a name="client-side-vs-server-side-xml-formatting-sqlxml-40"></a>클라이언트 쪽 vs. 서버 쪽 XML 서식 지정(SQLXML 4.0)
  이 항목에서는 SQL XML의 클라이언트 쪽 XML 서식과 서버 쪽 XML 서식의 일반적인 차이점에 대해 설명합니다.  
  
## <a name="multiple-rowset-queries-not-supported-in-client-side-formatting"></a>클라이언트 쪽 서식에서 지원되지 않는 여러 행 집합 쿼리  
 클라이언트 쪽 XML 서식을 사용하는 경우 여러 행 집합을 생성하는 쿼리는 지원되지 않습니다. 예를 들어 가상 디렉터리에 클라이언트 쪽 서식을 지정했다고 가정합니다. SELECT 문이 두 개는이 예제 템플릿에서 것이 좋습니다에  **\<sql:query >** 블록:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
     SELECT FirstName FROM Person.Contact FOR XML Nested;   
     SELECT LastName FROM Person.Contact FOR XML Nested    
  </sql:query>  
</ROOT>  
```  
  
 응용 프로그램 코드에서 이 템플릿을 실행할 수 있지만 클라이언트 쪽 XML 서식에서 여러 행 집합의 서식 설정을 지원하지 않기 때문에 오류가 반환됩니다. 두 쿼리를 지정 하는 경우 분리  **\<sql:query >** 블록, 원하는 결과 얻게 됩니다.  
  
## <a name="timestamp-maps-differently-in-client--vs-server-side-formatting"></a>타임 스탬프 클라이언트 vs에 다르게 지도입니다. 서버 쪽 서식  
 서버 쪽 XML 서식에서 `timestamp` 형식의 데이터베이스 열은 쿼리에 XMLDATA 옵션이 지정된 경우 i8 XDR 형식에 매핑됩니다.  
  
 클라이언트 쪽 XML 서식에서 `timestamp` 형식의 데이터베이스 열은 쿼리에 이진 Base64 옵션이 지정되어 있는지 여부에 따라 `uri` 또는 `bin.base64` XDR 형식에 매핑됩니다. 합니다 `bin.base64` XDR 형식 되므로 updategram 및 bulkload 기능을 사용 하는 경우 유용한이 형식이 변환 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `timestamp` 형식입니다. 이러한 변환 작업을 통해 삽입, 업데이트 또는 삭제 작업이 성공합니다.  
  
## <a name="deep-variants-are-used-in-server-side-formatting"></a>서버 쪽 서식에는 중첩이 많은 VARIANT가 사용됨  
 서버 쪽 XML 서식에는 중첩이 많은 VARIANT 형식이 사용됩니다. 클라이언트 쪽 XML 서식을 사용하는 경우 변형은 유니코드 문자열로 변환되고 VARIANT의 하위 유형은 사용되지 않습니다.  
  
## <a name="nested-mode-vs-auto-mode"></a>중첩된 모드 vs입니다. AUTO 모드  
 클라이언트 쪽 FOR XML의 NESTED 모드는 서버 쪽 FOR XML의 AUTO 모드와 비슷합니다. 단, 다음 사항은 예외입니다.  
  
### <a name="when-you-query-views-using-auto-mode-on-the-server-side-the-view-name-is-returned-as-the-element-name-in-the-resulting-xml"></a>서버 쪽에서 AUTO 모드를 사용하여 뷰를 쿼리하면 뷰 이름이 결과 XML에 요소 이름으로 반환됩니다.  
 예를 들어를 AdventureWorksdatabase의 Person.Contact 테이블에 다음 뷰를 만들었다고 가정 합니다.  
  
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
  
 템플릿을 실행하면 다음 XML이 반환됩니다. (일부 결과만 표시 됩니다.) 참고 요소 이름은 쿼리가 실행 되는 뷰의 이름이 지.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ContactView CID="1" FName="Gustavo" LName="Achong" />   
  <ContactView CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
 해당 NESTED 모드를 사용하여 클라이언트 쪽 XML 서식을 지정하면 기본 테이블 이름이 결과 XML에 요소 이름으로 반환됩니다. 예를 들어, 다음 수정 된 템플릿은 동일한 SELECT 문을 실행 하지만 XML 서식이 클라이언트 쪽에서 수행 됩니다 (즉, **클라이언트 쪽 xml** 로 설정 된 템플릿에서 true).  
  
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
  
 클라이언트 쪽 FOR XML의 NESTED 모드를 사용하는 경우 테이블 이름이 결과 XML에 요소 이름으로 반환되고 (쿼리에 지정 된 테이블 별칭은 사용 되지 않습니다.) 예를 들어 다음 템플릿을 참조하십시오.  
  
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
  
 XML 서식이 서버에서 수행 되는 경우 (**클라이언트 쪽 xml = "0"**), dbobject 쿼리는 실제 테이블 및 열 이름이 반환 됩니다 (있는 경우에 지정 된 별칭)을 반환 하는 열에 대 한 별칭을 사용할 수 있습니다. 예를 들어 다음 템플릿은 쿼리를 실행 하 고 XML 서식이 서버에서 수행 됩니다 (합니다 **클라이언트 쪽 xml** 옵션을 지정 하지 하며 **Run On Client** 에 대 한 옵션을 선택 하지 않으면 합니다 가상 루트)입니다. 또한 이 쿼리는 클라이언트 쪽 NESTED 모드가 아니라 AUTO 모드를 지정합니다.  
  
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
  
### <a name="client-side-vs-server-side-xpath"></a>클라이언트 쪽 vs. 서버 쪽 XPath  
 클라이언트 쪽 XPath와 서버 쪽 XPath는 다음을 제외하고는 동일하게 작동합니다.  
  
-   클라이언트 쪽 XPath 쿼리를 사용할 때 적용되는 데이터 변환은 서버 쪽 XPath 쿼리를 사용할 때 적용되는 데이터 변환과 다릅니다. 클라이언트 쪽 XPath에는 CONVERT 모드 126 대신 CAST가 사용됩니다.  
  
-   지정 하는 경우 **클라이언트 쪽 xml = "0"** (false) 템플릿에서 하면 서버 쪽 XML 서식이 요청 됩니다. 따라서 서버에서는 NESTED 옵션이 인식되지 않으므로 FOR XML NESTED를 지정할 수 없습니다. 이렇게 하면 오류가 발생합니다. 서버에서 인식되는 AUTO, RAW 또는 EXPLICIT 모드를 사용해야 합니다.  
  
-   지정 하는 경우 **클라이언트 쪽 xml = "1"** (true) 템플릿에서 하면 클라이언트 쪽 XML 서식이 요청 됩니다. 이 경우 FOR XML NESTED를 지정할 수 있습니다. 하지만 FOR XML AUTO를 지정 하는 경우 서버 쪽에서 발생 XML 서식을 **클라이언트 쪽 xml = "1"** 템플릿에 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 보안 고려 사항에 대 한 &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [클라이언트 쪽 XML 서식 지정 &#40;SQLXML 4.0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [서버 쪽 XML 서식 지정 &#40;SQLXML 4.0&#41;](server-side-xml-formatting-sqlxml-4-0.md)  
  
  
