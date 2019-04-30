---
title: 상호 운용 가능한 SQL 문 생성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc8072a6d7291a546f0f12256aa4b336da037a83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281086"
---
# <a name="constructing-interoperable-sql-statements"></a>상호 운용 가능한 SQL 문 생성
이전 섹션에서 설명 했 듯이 상호 운용 가능한 응용 프로그램에서 ODBC SQL 문법을 사용 해야 합니다. 하지만이 문법을 사용 하 여, 초과 다양 한 추가 문제 상호 운용 가능한 응용 프로그램이 직면 합니다. 예를 들어, 응용 프로그램 무엇입니까 모든 데이터 원본에서 지원 되지 않는 외부 조인과 같은 한 기능을 사용 하려는 경우?  
  
 이 시점에서 응용 프로그램 작성자는 언어 기능은 필수 및 선택적에 대 한 몇 가지 결정 해야 합니다. 대부분의 경우에서 특정 드라이버 응용 프로그램에 필요한 기능을 지원 하지 않는 경우 응용 프로그램이 단순히 거부 해당 드라이버를 사용 하 여 실행 합니다. 그러나이 기능은 선택 사항, 하는 경우 응용 프로그램이 기능을 해결할 수 있습니다. 예를 들어, 사용자가 기능을 사용 하도록 허용 하는 인터페이스의 해당 부분을 비활성화할 수 있습니다 것입니다.  
  
 지원 되는 기능을 확인 하려면 호출 하 여 응용 프로그램 시작 **SQLGetInfo** SQL_SQL_CONFORMANCE 옵션을 사용 합니다. SQL 적합성 수준 응용 프로그램의 SQL 지원 되는 광범위 한 보기를 제공 합니다. 이 보기에서는 응용 프로그램이 호출 구체화할 **SQLGetInfo** 다양 한 다른 옵션 중 하나를 사용 하 여 합니다. 이러한 옵션의 전체 목록은 참조 하세요. 합니다 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다. 마지막으로, **SQLGetTypeInfo** 데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 다음 섹션에서는 다양 한 상호 운용 가능한 SQL 문을 생성할 때 응용 프로그램에 대 한 감시 해야 할 가능한 요소를 나열 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 및 스키마 사용](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [카탈로그 위치](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [식별자 사례](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [프로시저 호출의 매개 변수 표식](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 문](../../../odbc/reference/develop-app/ddl-statements.md)
