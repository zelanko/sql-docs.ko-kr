---
title: SQLXML 4.0 프로그래밍 개념 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
- SQLXML
ms.assetid: 5a11cda2-b8a3-4453-848f-641afdaa7024
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2ab9bd2ff6cfddcf96e4844eb9ea14eea414b650
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093264"
---
# <a name="sqlxml-40-programming-concepts"></a>SQLXML 4.0 프로그래밍 개념
  SQLXML 3.0은 웹 릴리스로 제공되어 추가 클라이언트 쪽 XML 기능과 주석이 추가된 XSD 스키마, XML 대량 로드, 웹 서비스(SOAP) 지원, Updategram 등 기존 기능에 대한 향상된 기능을 제공했습니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 SQLXML 3.0과 동일한 기능뿐 아니라 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 새로운 기능을 수용하기 위해 제공된 추가 업데이트를 제공하는 SQLXML 4.0을 소개했습니다.  
  
 이 섹션에서는 SQLXML 4.0에 대한 정보를 제공합니다.  
  
 [SQLXML이 SQL Server에 설치되지 않음](sqlxml-is-not-installed-in-sql-server.md)  
 이 항목에서는 SQLXML 4.0을 설치하는 방법에 대해 설명합니다.  
  
 [SQLXML 4.0 SP1의 새로운 기능](what-s-new-in-sqlxml-4-0-sp1.md)  
 SQLXML 4.0의 업데이트 및 향상된 기능을 설명하고 이 설명서의 관련 항목에 대한 링크를 제공합니다.  
  
 [ADO를 사용하여 SQLXML 4.0 쿼리 실행](using-ado-to-execute-sqlxml-4-0-queries.md)  
 SQLXML 쿼리에 ADO를 사용하는 방법에 대해 설명합니다. 이전 버전보다 SQLXML 4.0에서 ADO가 더욱 강화되었습니다.  
  
 [SQLXML 4.0의 xml 데이터 형식 지원](xml-data-type-support-in-sqlxml-4-0.md)  
 SQLXML 4.0에서 추가된 xml 데이터 형식 지원에 대해 설명합니다.  
  
 [SQLXML 예 실행을 위한 요구 사항](requirements-for-running-sqlxml-examples.md)  
 제공된 SQLXML 예에서 작업 예제를 만들기 위한 요구 사항에 대해 설명합니다.  
  
 [클라이언트 쪽 및 서버 쪽 서식 지정 &#40;SQLXML 4.0&#41;](formatting/client-side-and-server-side-formatting-sqlxml-4-0.md)  
 XML 문서 구성을 위한 FOR XML 명령을 비롯하여 클라이언트 쪽 및 서버 쪽 형식 지정을 비교하고 정보를 제공합니다.  
  
 [SQLXML 4.0의 주석이 추가된 XSD 스키마](annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
 SQLXML 4.0에서 주석이 추가된 XSD 스키마를 사용하는 방법에 대한 정보를 제공합니다. 또한 레거시 응용 프로그램에서 사용하기 위한 주석이 추가된 XDR 스키마에 대한 정보를 제공합니다.  
  
 [SQLXML 4.0의 XPath 쿼리 사용](../sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
 XPath 언어의 하위 집합을 사용하여 주석이 추가된 XSD 스키마로 만든 XML 뷰를 쿼리하는 방법에 대해 설명하고 예를 제공합니다.  
  
 [SQLXML 4.0에서 updategram을 사용하여 데이터 수정](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
 주석이 추가된 XSD(또는 XDR) 스키마가 제공하는 XML 뷰에서 작업하여 데이터베이스의 데이터를 수정하는 Updategram에 대한 정보를 제공합니다.  
  
 [XML 데이터 대량 로드 수행 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
 SQLXML 4.0에서 XML을 대량 로드하는 방법에 대해 설명합니다.  
  
 [SQLXML 4.0 데이터 액세스 구성 요소](../sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/sqlxml-4-0-data-access-components-sqlxmloledb-provider.md)  
 SQLXMLOLEDB 공급자를 문서화하고 다른 SQLXML 4.0 데이터 액세스 구성 요소에 대한 링크를 제공합니다.  
  
 [SQLXML 4.0 .NET Framework 지원](../../database-engine/dev-guide/sqlxml-4-0-net-framework-support.md)  
 .NET Framework에 대한 SQLXML 4.0 지원을 설명합니다.  
  
 [템플릿, XSL 및 스키마 캐싱 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/caching-templates-xsl-and-schemas-sqlxml-4-0.md)  
 성능 향상을 위해 SQLXML에서 제공되는 캐싱 기능에 대해 설명합니다.  
  
 [SQLXML 4.0 보안 고려 사항](../sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
 SQLXML 4.0과 관련된 보안 문제에 대해 설명합니다.  
  
 [SQLXML 4.0에 대한 지침 및 제한 사항](../sqlxml-annotated-xsd-schemas-xpath-queries/guidelines-and-limitations-of-sqlxml-4-0.md)  
 SQLXML 4.0에서 작업할 때 주의할 문제를 표시합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터&#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  