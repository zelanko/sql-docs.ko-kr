---
title: 상호 운용 가능한 SQL 문 생성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eccdef63b7d06a456a07f5f1a9ccad987d2de29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282522"
---
# <a name="constructing-interoperable-sql-statements"></a>상호 운용 가능한 SQL 문 생성
이전 섹션에서 설명한 것처럼 상호 운용 가능한 응용 프로그램은 ODBC SQL 문법을 사용해야 합니다. 그러나 이 문법을 사용하는 것 외에도 상호 운용 가능한 응용 프로그램에서 여러 가지 추가 문제에 직면할 수 있습니다. 예를 들어, 모든 데이터 원본에서 지원되지 않는 외부 조인과 같은 기능을 사용하려는 경우 응용 프로그램이 수행하는 작업을 수행합니까?  
  
 이 시점에서 응용 프로그램 작성기는 필요한 언어 기능과 선택 사항인 언어에 대해 몇 가지 결정을 내려야 합니다. 대부분의 경우 특정 드라이버가 응용 프로그램에 필요한 기능을 지원하지 않는 경우 응용 프로그램은 해당 드라이버로 실행을 거부합니다. 그러나 이 기능이 선택 사항인 경우 응용 프로그램이 기능을 해결할 수 있습니다. 예를 들어 사용자가 이 기능을 사용할 수 있도록 하는 인터페이스의 해당 부분을 비활성화할 수 있습니다.  
  
 지원되는 기능을 확인하려면 응용 프로그램이 SQL_SQL_CONFORMANCE 옵션으로 **SQLGetInfo를** 호출하여 시작합니다. SQL 준수 수준은 응용 프로그램에 지원되는 SQL에 대한 광범위한 보기를 제공합니다. 이 보기를 구체화하기 위해 응용 프로그램은 다른 여러 옵션중 어느 과도 한 **SQLGetInfo를** 호출합니다. 이러한 옵션의 전체 목록은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조하십시오. 마지막으로 **SQLGetTypeInfo** 데이터 원본에서 지원 되는 데이터 형식에 대 한 정보를 반환 합니다. 다음 섹션에서는 상호 운용 가능한 SQL 문을 작성할 때 응용 프로그램에서 주의해야 하는 여러 가지 요소를 나열합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 및 스키마 사용](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [카탈로그 위치](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [식별자 사례](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [프로시저 호출의 매개 변수 표식](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 문](../../../odbc/reference/develop-app/ddl-statements.md)
