---
title: 클라이언트 쪽 XML 서식 지정 (SQLXML)
description: FOR XML 절을 사용 하 여 SQLXML 4.0의 클라이언트 쪽 XML 서식에 대해 알아봅니다.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- middle tier XML formatting [SQLXML]
- client-side XML formatting
- client-side-xml attribute
ms.assetid: 9630a21d-a93b-4d3b-8a25-c4b32399f993
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1b03c1cb91c17e330d73f192bbd364c95591c721
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84530017"
---
# <a name="client-side-xml-formatting-sqlxml-40"></a>클라이언트 쪽 XML 서식 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 클라이언트 쪽 XML 서식 지정에 대한 정보를 제공합니다. 클라이언트 쪽 서식 지정은 중간 계층의 XML 서식 지정을 의미합니다.  
  
> [!NOTE]  
>  이 항목에서는 이미 FOR XML 절에 익숙한 사용자를 대상으로 클라이언트 쪽의 FOR XML 절 사용에 대한 추가 정보를 제공합니다. FOR xml에 대 한 자세한 내용은 [FOR xml을 사용 하 여 Xml 생성](../../../relational-databases/xml/for-xml-sql-server.md)을 참조 하세요.  
  
 **중요** 클라이언트 쪽 FOR XML 기능을 새 **xml** 데이터 형식과 함께 사용 하려면 클라이언트는 항상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLOLEDB 공급자 대신 NATIVE client (SQLNCLI11) 데이터 공급자를 사용 해야 합니다. SQLNCLI11은 최신 버전의 SQL Server 공급자이며 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 데이터 형식을 완전히 이해합니다. SQLOLEDB 공급자를 사용 하는 클라이언트 쪽 FOR XML의 동작은 **xml** 데이터 형식을 문자열로 처리 합니다.  
  
## <a name="formatting-xml-documents-on-the-client-side"></a>클라이언트 쪽에서 XML 문서 서식 지정  
 클라이언트 애플리케이션에서 다음 쿼리를 실행하는 경우를 살펴보겠습니다.  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML RAW  
```  
  
 다음 쿼리 부분만 서버로 전송됩니다.  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 서버에서 쿼리를 실행 하 고 클라이언트에 행 집합 (FirstName 및 LastNamecolumns 포함)을 반환 합니다. 그러면 중간 계층에서 행 집합에 FOR XML 변환을 적용하고 XML 서식을 클라이언트에 반환합니다.  
  
 마찬가지로, XPath 쿼리를 실행하면 서버는 클라이언트에 행 집합을 반환하고 FOR XML EXPLICIT 변환이 클라이언트의 행 집합에 적용되어 필요한 XML 서식을 생성합니다.  
  
 다음 표에서는 클라이언트 쪽 FOR XML에서 지정할 수 있는 모드를 보여 줍니다.  
  
|클라이언트 쪽 FOR XML 모드|주석|  
|-------------------------------|-------------|  
|RAW|클라이언트 쪽 또는 서버 쪽 FOR XML에 지정될 경우 동일한 결과를 생성합니다.|  
|NESTED|서버 쪽의 FOR XML AUTO 모드와 비슷합니다.|  
|EXPLICIT|서버 쪽 FOR XML EXPLICIT 모드와 비슷합니다.|  
  
> [!NOTE]  
>  AUTO 모드를 지정하고 클라이언트 쪽 XML 서식 지정을 요청하는 경우 전체 쿼리가 서버로 전송됩니다. 즉, XML 서식 지정이 서버에서 실행됩니다. 이는 편의상 수행되는 기능이지만 NESTED 모드는 생성되는 XML 문서의 요소 이름으로 기본 테이블 이름을 반환합니다. 일부 애플리케이션에는 기본 테이블을 이름이 필요할 수 있습니다. 예를 들어 저장 프로시저를 실행하고 결과 데이터를 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework의 데이터 세트에 로드한 후 나중에 DiffGram을 생성하여 테이블의 데이터를 업데이트할 수 있습니다. 이러한 경우 기본 테이블 정보가 필요할 수 있으므로 NESTED 모드를 사용해야 합니다.  
  
## <a name="benefits-of-client-side-xml-formatting"></a>클라이언트 쪽 XML 서식 지정의 이점  
 다음은 클라이언트에서 XML 서식 지정을 할 때의 이점입니다.  
  
### <a name="if-you-have-stored-procedures-on-the-server-that-return-a-single-rowset-you-can-request-client-side-for-xml-transformation-to-generate-an-xml"></a>서버에 단일 행 집합을 반환하는 저장 프로시저가 있는 경우 클라이언트 쪽 FOR XML 변환을 요청하여 XML을 생성할 수 있습니다.  
 예를 들어 다음과 같은 저장 프로시저가 있다고 가정해 보십시오. 이 프로시저는 AdventureWorks 데이터베이스의 Person.Contact 테이블에서 직원의 이름과 성을 반환합니다.  
  
```  
IF EXISTS (SELECT name FROM sysobjects  
   WHERE name = 'GetContacts' AND type = 'P')  
   DROP PROCEDURE GetContacts  
GO  
CREATE PROCEDURE GetContacts  
AS  
    SELECT   FirstName, LastName  
    FROM     Person.Contact  
```  
  
 다음 예제 XML 템플릿은 저장 프로시저를 실행합니다. FOR XML 절은 저장 프로시저 이름 뒤에 지정됩니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    EXEC GetContacts FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 템플릿에서 **클라이언트-xml** 특성이 1 (true)로 설정 되어 있기 때문에 저장 프로시저는 서버에서 실행 되 고 서버에서 반환 되는 2 열 행 집합은 중간 계층에서 xml로 변환 된 후 클라이언트에 반환 됩니다. 이 문서에는 결과의 일부분만 나와 있습니다.  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact FirstName="Catherine" LastName="Abel" />  
</ROOT>  
```  
  
> [!NOTE]  
>  SQLXMLOLEDB Provider 또는 SQLXML 관리 되는 클래스를 사용 하는 경우 **clientside xml** 속성을 사용 하 여 클라이언트 쪽 xml 서식 지정을 요청할 수 있습니다.  
  
### <a name="the-workload-is-more-balanced"></a>작업의 균형이 더 잘 이루어집니다.  
 클라이언트에서 XML 서식 지정을 수행하므로 서버와 클라이언트 간에 작업 균형이 이루어지고 서버에서 다른 작업을 할 수 있는 여유가 확보됩니다.  
  
## <a name="supporting-client-side-xml-formatting"></a>클라이언트 쪽 XML 서식 지정 지원  
 클라이언트 쪽 XML 서식 지정 기능을 지원하기 위해 SQLXML은 다음을 제공합니다.  
  
-   SQLXMLOLEDB 공급자  
  
-   SQLXML 관리되는 클래스  
  
-   향상된 XML 템플릿 지원  
  
-   SqlXmlCommand. ClientSideXml 속성  
  
     SQLXML 관리되는 클래스의 이 속성을 true로 설정하여 클라이언트 쪽 서식 지정을 지정할 수 있습니다.  
  
## <a name="enhanced-xml-template-support"></a>향상된 XML 템플릿 지원  
 부터 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 의 xml 템플릿은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **클라이언트 쪽 xml** 특성을 추가 하 여 향상 되었습니다. 이 특성을 true로 설정하면 XML 서식이 클라이언트에서 지정됩니다. 이 템플릿 특성은 SQLXMLOLEDB 공급자별 Clientside-by-side Xml 속성의 기능과 동일 합니다.  
  
> [!NOTE]  
>  SQLXMLOLEDB 공급자를 사용 하는 ADO 응용 프로그램에서 XML 템플릿을 실행 하 고 템플릿에서 **클라이언트 쪽 xml** 특성과 공급자 clientside xml 속성을 둘 다 지정 하는 경우 템플릿에 지정 된 값이 우선 적용 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 쪽 및 서버 쪽 XML 서식 &#40;SQLXML 4.0&#41;의 아키텍처](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)   
 [XML 보안 고려 사항은 SQLXML 4.0을 &#40;&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [SQLXML 4.0의 xml 데이터 형식 지원](../../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)   
 [SQLXML 관리 되는 클래스](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md)   
 [클라이언트 쪽 및 서버 쪽 XML 서식 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-vs-server-side-xml-formatting-sqlxml-4-0.md)   
 [SqlXmlCommand 개체 &#40;SQLXML 관리 되는 클래스&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [XML 데이터&#40;SQL Server&#41;](../../../relational-databases/xml/xml-data-sql-server.md)  
  
  
