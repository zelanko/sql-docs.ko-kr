---
title: SQLXMLOLEDB 공급자 사용 (SQLXML)
description: ADO 응용 프로그램에서 SQLXMLOLEDB 공급자별 속성을 사용 하는 방법에 대 한 정보를 봅니다.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sample applications [SQLXML]
- SQLXMLOLEDB Provider, samples
- ClientSideXML property
ms.assetid: fbcefac5-29c9-478b-b0e0-d510b593f446
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bbecbe6507754412ffd4a95fc60b077a92fc669e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415047"
---
# <a name="using-the-sqlxmloledb-provider-sqlxml-40"></a>SQLXMLOLEDB 공급자 사용(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  이 섹션의 항목에서는 SQLXMLOLEDB 공급자 고유 속성의 사용 방법을 보여 주는 ADO 예제 애플리케이션에 대해 설명합니다.  
  
## <a name="application-requirements-for-sqlxmloledb-40-provider"></a>SQLXMLOLEDB 4.0 공급자의 애플리케이션 요구 사항  
 SQLXMLOLEDB 4.0을 사용하는 작업 예제를 만들려면 다음을 수행해야 합니다.  
  
1.  Microsoft Visual Basic .exe 애플리케이션을 만들고 다음 참조 중 하나를 추가합니다.  
  
    -   Microsoft ADO(ActiveX Data Objects) 2.6 라이브러리  
  
    -   Microsoft ADO(ActiveX Data Objects) 2.7 라이브러리  
  
    -   Microsoft ActiveX Data Objects 2.8 라이브러리  
  
2.  SQLXML 4.0과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 배포 및 설치합니다.  

     자세한 내용은 [SQLXML 4.0 프로그래밍 개념](../../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md) 및 [SQL Server Native Client 설치](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SQLXMLOLEDB 공급자&#41;&#40;SQL 쿼리 실행 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md)  
 ClientSideXML 및 xml 루트 속성을 사용 하 여 SQL 쿼리를 실행 하는 방법을 보여 줍니다.  
  
 [SQLXMLOLEDB Provider &#40;SQL 쿼리를 포함 하는 템플릿 실행&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md)  
 ClientSideXML 속성을 사용 하는 방법을 보여 줍니다.  
  
 [SQLXMLOLEDB 공급자를 &#40;XPath 쿼리 실행&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md)  
 ClientSideXML, 기본 경로 및 매핑 스키마 속성을 사용 하는 방법을 보여 줍니다.  
  
 [SQLXMLOLEDB 공급자를 사용 하 &#40;네임 스페이스가 있는 XPath 쿼리 실행&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md)  
 네임스페이스로 한정된 스키마에 대해 쿼리하는 방법을 설명합니다.  
  
 [SQLXMLOLEDB Provider &#40;XPath 쿼리를 포함 하는 템플릿 실행&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-xpath-queries-sqlxmloledb-provider.md)  
 ClientSideXML, 기본 경로 및 매핑 스키마 속성을 사용 하 여 SQL 쿼리를 사용 하 여 템플릿을 실행 하는 방법을 보여 줍니다.  
  
 [SQLXMLOLEDB 공급자&#41;&#40;XSL 변환 적용 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/applying-an-xsl-transformation-sqlxmloledb-provider.md)  
 Xml 및 xsl 속성을 사용 하 여 XSL 변환을 적용 하는 방법을 보여 줍니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client의 시스템 요구 사항](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)  
  
  
