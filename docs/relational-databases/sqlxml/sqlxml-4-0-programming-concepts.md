---
title: SQLXML 4.0 프로그래밍 개념
description: SQLXML 4.0에서 사용 되는 프로그래밍 개념에 대 한 정보를 봅니다.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
- SQLXML
ms.assetid: 5a11cda2-b8a3-4453-848f-641afdaa7024
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2699c938d13750e954a4171da610c6a40b74f141
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97429651"
---
# <a name="sqlxml-40-programming-concepts"></a>SQLXML 4.0 프로그래밍 개념
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  SQLXML 3.0은 웹 릴리스로 제공되어 추가 클라이언트 쪽 XML 기능과 주석이 추가된 XSD 스키마, XML 대량 로드, 웹 서비스(SOAP) 지원, Updategram 등 기존 기능에 대한 향상된 기능을 제공했습니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 SQLXML 3.0과 동일한 기능뿐 아니라 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 새로운 기능을 수용하기 위해 제공된 추가 업데이트를 제공하는 SQLXML 4.0을 소개했습니다.  
  
 이 섹션에서는 SQLXML 4.0에 대한 정보를 제공합니다.  
  
 [SQLXML이 SQL Server에 설치되지 않음](../../relational-databases/sqlxml/sqlxml-is-not-installed-in-sql-server.md)  
 이 항목에서는 SQLXML 4.0을 설치하는 방법에 대해 설명합니다.  
  
 [SQLXML 4.0 SP1의 새로운 기능](../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md)  
 SQLXML 4.0의 업데이트 및 향상된 기능을 설명하고 이 설명서의 관련 항목에 대한 링크를 제공합니다.  
  
 [ADO를 사용하여 SQLXML 4.0 쿼리 실행](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)  
 SQLXML 쿼리에 ADO를 사용하는 방법에 대해 설명합니다. 이전 버전보다 SQLXML 4.0에서 ADO가 더욱 강화되었습니다.  
  
 [SQLXML 4.0의 xml 데이터 형식 지원](../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)  
 SQLXML 4.0에서 추가된 xml 데이터 형식 지원에 대해 설명합니다.  
  
 [SQLXML 예 실행을 위한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)  
 제공된 SQLXML 예에서 작업 예제를 만들기 위한 요구 사항에 대해 설명합니다.  
  
 [클라이언트 쪽 및 서버 쪽 서식 지정 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/formatting/client-side-and-server-side-formatting-sqlxml-4-0.md)  
 XML 문서 구성을 위한 FOR XML 명령을 비롯하여 클라이언트 쪽 및 서버 쪽 형식 지정을 비교하고 정보를 제공합니다.  
  
 [SQLXML 4.0의 주석이 추가된 XSD 스키마](../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
 SQLXML 4.0에서 주석이 추가된 XSD 스키마를 사용하는 방법에 대한 정보를 제공합니다. 또한 레거시 애플리케이션에서 사용하기 위한 주석이 추가된 XDR 스키마에 대한 정보를 제공합니다.  
  
 [SQLXML 4.0의 XPath 쿼리 사용](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
 XPath 언어의 하위 집합을 사용하여 주석이 추가된 XSD 스키마로 만든 XML 뷰를 쿼리하는 방법에 대해 설명하고 예를 제공합니다.  
  
 [SQLXML 4.0에서 updategram을 사용하여 데이터 수정](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
 주석이 추가된 XSD(또는 XDR) 스키마가 제공하는 XML 뷰에서 작업하여 데이터베이스의 데이터를 수정하는 Updategram에 대한 정보를 제공합니다.  
  
 [XML 데이터 대량 로드 수행&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
 SQLXML 4.0에서 XML을 대량 로드하는 방법에 대해 설명합니다.  
  
 [SQLXML 4.0 데이터 액세스 구성 요소](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/sqlxml-4-0-data-access-components-sqlxmloledb-provider.md)  
 SQLXMLOLEDB 공급자를 문서화하고 다른 SQLXML 4.0 데이터 액세스 구성 요소에 대한 링크를 제공합니다.  
  
 [SQLXML 4.0 .NET Framework 지원](../sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md)  
 .NET Framework에 대한 SQLXML 4.0 지원을 설명합니다.  
  
 [SQLXML 4.0 &#40;템플릿, XSL 및 스키마 캐싱&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/caching-templates-xsl-and-schemas-sqlxml-4-0.md)  
 성능 향상을 위해 SQLXML에서 제공되는 캐싱 기능에 대해 설명합니다.  
  
 [SQLXML 4.0 보안 고려 사항](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
 SQLXML 4.0과 관련된 보안 문제에 대해 설명합니다.  
  
 [SQLXML 4.0에 대한 지침 및 제한 사항](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/guidelines-and-limitations-of-sqlxml-4-0.md)  
 SQLXML 4.0에서 작업할 때 주의할 문제를 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
