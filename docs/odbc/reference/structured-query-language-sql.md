---
title: 구조적 쿼리 언어 (SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86f9dd843171c02654302694c669f40b6b51ab78
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769671"
---
# <a name="structured-query-language-sql"></a>SQL(구조적 쿼리 언어)(Structured Query Language)
일반적인 DBMS를 사용 하면 저장, 액세스 및 구성 하 고 효율적인 방식으로 데이터를 수정할 수 있습니다. 원래 Dbms의 사용자는 프로그래머에 게 되었습니다. 저장된 된 데이터에 액세스 COBOL 같은 프로그래밍 언어에서 프로그램을 작성 해야 합니다. 이러한 프로그램 비기술적 사용자에 게 친숙 한 인터페이스를 보여 쓴 종종를 잘 알고 있는 프로그래머의 서비스 필요한 데이터 자체에 대 한 액세스. 데이터에 대 한 일반 액세스 실용적인 없습니다.  
  
 사용자가이 상황에 완전히 만족 되지 않았습니다. 데이터에 액세스 하는 동안에 자주 특별 한 소프트웨어를 작성 하는 DBMS 프로그래머 유도 필요 합니다. 예를 들어, 영업 부서 해당 하는 영업 사원 각각 사용 하 여 이전 달의 총 판매액을 확인 하려고 하 고 회사의 서비스의 각 판매 직원의 길이에서 따라 순위가이 정보를 원하는 경우 되었을 두 가지 선택 사항:는 프로그램 중 하나에 있는 항목을 이미 존재 이 방식으로 액세스할 수 있는 정보를 허용 또는 부서에서는 이러한 프로그램을 작성 하는 프로그래머에 게 문의 해야 합니다. 이 대부분의 경우에서 가치를 한 번, 또는 임시 질문에 대 한 비용이 많이 듭니다 있었습니다 보다 더 많은 작업 이었습니다. 점점 더 많은 사용자가 쉽게 액세스할 수 있도록 원하는,이 문제에 더 큰 증가 합니다.  
  
 임시로 데이터에 액세스할 수 있도록 해당 요청을 표현 하는 언어를 제공 해야 합니다. 데이터베이스에 대 한 단일 요청; 쿼리로 정의 됩니다. 이러한 언어는 쿼리 언어를 라고 합니다. 다양 한 쿼리 언어는이 목적을 위해 개발 된 있지만 중 가장 많이 사용 되었습니다: 년대에서 IBM에서 개발 하는 구조적 쿼리 언어입니다. 일반적으로 머리 글자어 SQL 라고 하 고 "ess-큐-ell" 및 "sequel"로 발음 합니다. SQL이 1986에서 표준 ANSI 및 ISO 표준 1987; 유용한 많은 데이터베이스 관리 시스템에서 현재 사용 됩니다.  
  
 SQL 사용자의 임시 요구 해결 하지만 컴퓨터 프로그램에서 데이터 액세스에 대 한 필요성 떨어진 이동 하지 않았습니다. 사실 대부분의 데이터베이스 액세스 여전히 (였으며)에 사용 되는 주문 항목 및 데이터 조작 프로그램과 같은 프로그램을 계정 조정 하는 데 같은 프로그래밍 방식의 정기적으로 예약 된 보고서 및 통계 분석의 형태로, 데이터 입력 프로그램 및 작업 순서를 생성 합니다.  
  
 또한 이러한 프로그램 다음 세 가지 방법 중 하나를 사용 하 여 SQL을 사용 합니다.  
  
-   **SQL 포함**에 sql에서 문을 호스트 등의 언어로 C 또는 COBOL 포함 됩니다.  
  
-   **SQL 모듈**는 SQL 문을 DBMS 컴파일 및 호스트 언어에서 호출 됩니다.  
  
-   **호출 수준 인터페이스**, 또는 dbms SQL 문을 전달 하 고 DBMS에서 결과 검색할 호출 된 함수의 구성 된 CLI입니다.  
  
> [!NOTE]  
>  응용 프로그램 프로그래밍 하는 대신 호출 수준 인터페이스를 사용 하는 용어 인터페이스 (API)는 기록 실수로 동일한 작업에 대 한 또 다른 용어입니다. 데이터베이스 환경에서는 자체 SQL 설명 하기 위해 API를 사용 합니다: SQL은 DBMS에 API.  
  
 이러한 선택 항목의 포함 된 SQL은 가장 일반적으로 사용 되는 대부분의 주요 Dbms 전용 Cli를 지원 하지만입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL 문 처리](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [Embedded SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 모듈](../../odbc/reference/sql-modules.md)  
  
-   [호출 수준 인터페이스](../../odbc/reference/call-level-interfaces.md)
