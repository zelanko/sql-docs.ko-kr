---
title: "상호 운용할 수 있는 SQL 문을 구성 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34636d9ead963cf9548d8ff1345424f4283fd1fb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="constructing-interoperable-sql-statements"></a>상호 운용할 수 있는 SQL 문 구성
이전 섹션에서 설명 했 듯이 상호 운용 가능한 응용 프로그램에서 ODBC SQL 문법을 사용 해야 합니다. 그러나이 문법을 사용 하 여 다음 다양 한 추가 문제 상호 운용 가능한 응용 프로그램에서 직면 됩니다. 예를 들어 응용 프로그램이 수행 하는 모든 데이터 원본에서 지원 되지 않는 외부 조인과 같은 기능을 사용 하려는 경우  
  
 이 시점에서 응용 프로그램 작성기에 있는 언어 기능 필수 및 선택적에 대 한 몇 가지 결정 해야 합니다. 대부분의 경우에서 특정 드라이버는 응용 프로그램에서 필요한 기능을 지원 하지 않는 경우 응용 프로그램 단순히 거부 해당 드라이버와 함께 실행 합니다. 그러나 선택적 기능이 있으면 응용 프로그램이 기능이 해결할 수 있습니다. 예를 들어 것 사용자 기능을 사용 하도록 허용 하는 인터페이스의 일부를 비활성화할 수 있습니다.  
  
 지원 되는 기능을 확인 하려면 호출 하 여 응용 프로그램 시작 **SQLGetInfo** SQL_SQL_CONFORMANCE 옵션을 사용 합니다. SQL 지원 되는 광범위 한 뷰는 SQL 규칙 수준 응용 프로그램에 제공 합니다. 응용 프로그램 호출 하 여이 뷰를 구체화 하려면 **SQLGetInfo** 다양 한 다른 옵션 중 하나를 사용 합니다. 이러한 옵션의 전체 목록은 참조 하십시오.는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다. 마지막으로, **SQLGetTypeInfo** 데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 다음 섹션에서는 여러 가지 상호 운용할 수 있는 SQL 문을 구성 하는 경우 응용 프로그램에 대 한 감시 해야 할 가능한 요소를 나열 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 및 스키마 사용](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [카탈로그 위치](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [식별자 사례](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [프로시저 호출의 매개 변수 표식](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 문](../../../odbc/reference/develop-app/ddl-statements.md)
