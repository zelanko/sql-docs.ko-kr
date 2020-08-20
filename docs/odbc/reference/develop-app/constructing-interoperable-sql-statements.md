---
description: 상호 운용 가능한 SQL 문 생성
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acdb0f360242c4c9953804cb768214b0a78251dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465885"
---
# <a name="constructing-interoperable-sql-statements"></a>상호 운용 가능한 SQL 문 생성
이전 섹션에서 설명한 것 처럼 상호 운용 가능한 응용 프로그램은 ODBC SQL 문법을 사용 해야 합니다. 그러나이 문법을 사용 하는 것 외에도 상호 운용 가능한 응용 프로그램에서 많은 추가 문제가 발생 합니다. 예를 들어 외부 조인과 같이 모든 데이터 원본에서 지원 하지 않는 기능을 사용 하려는 경우 응용 프로그램에서 수행 하는 작업은 무엇 인가요?  
  
 이 시점에서 응용 프로그램 작성자는 필요한 언어 기능 및 선택적 요소에 대 한 몇 가지 결정을 내려야 합니다. 대부분의 경우 특정 드라이버가 응용 프로그램에 필요한 기능을 지원 하지 않는 경우 응용 프로그램은 단순히 해당 드라이버를 사용 하 여 실행을 거부 합니다. 그러나이 기능이 선택 사항인 경우 응용 프로그램은 기능을 해결할 수 있습니다. 예를 들어 사용자가 기능을 사용할 수 있도록 하는 인터페이스의 해당 부분을 사용 하지 않도록 설정할 수 있습니다.  
  
 지원 되는 기능을 확인 하기 위해 응용 프로그램은 SQL_SQL_CONFORMANCE 옵션으로 **SQLGetInfo** 를 호출 하 여 시작 합니다. SQL 규칙 수준은 응용 프로그램에 지원 되는 SQL의 광범위 한 뷰를 제공 합니다. 이 뷰를 구체화 하기 위해 응용 프로그램은 여러 다른 옵션을 사용 하 여 **SQLGetInfo** 를 호출 합니다. 이러한 옵션의 전체 목록은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조 하세요. 마지막으로 **SQLGetTypeInfo** 는 데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 다음 섹션에는 상호 운용할 수 있는 SQL 문을 생성할 때 응용 프로그램이 감시 해야 하는 여러 가지 요소가 나와 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 및 스키마 사용](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [카탈로그 위치](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [식별자 사례](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [프로시저 호출의 매개 변수 표식](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 문](../../../odbc/reference/develop-app/ddl-statements.md)
