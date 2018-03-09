---
title: "구조적 쿼리 언어 (SQL) | Microsoft Docs"
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
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f51c5b639649a3d21ce515a1d4082e84be4f7329
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="structured-query-language-sql"></a>SQL(구조적 쿼리 언어)(Structured Query Language)
일반적인 DBMS를 사용 하면 저장, 액세스 및를 구성 하 고 효율적인 방식으로 데이터를 수정할 수 있습니다. 원래, Dbms의 사용자에 게 프로그래머 했습니다. 저장 된 데이터에 액세스 하는 프로그램 COBOL와 같은 프로그래밍 언어로 작성 필요 합니다. 이러한 프로그램 배경이 사용자에 게 친숙 한 인터페이스를 보여 쓴 종종를 잘 알고 있는 프로그래머의 서비스 필요한 데이터 자체에 대 한 액세스. 데이터에 대 한 임시 액세스는 큰 의미가 없습니다.  
  
 사용자가 이러한 상황을 완전히 만족 되지 않았습니다. 데이터를 액세스 하는 동안에 자주 특별 한 소프트웨어를 작성 하는 DBMS 프로그래머가 유도 필요 합니다. 예를 들어 영업부 각각 해당 하는 영업 사원 총 판매액을 본 이전 달에 회사의 서비스의 각 판매 직원의 길이에서 따라 순위가이 정보를 원하는 경우 이전의 두 가지 선택 사항: 중 하나는 프로그램에 있는 항목을 이미 존재 이러한 프로그램을 작성 하는 프로그래머에 게 문의 해야 할 부서 또는 정보에 액세스 하 여이 방식으로 허용 됩니다. 대부분의 경우가 요소는 가치를 확인할 수 있고가 항상 일회성, 또는 임시, 조회에 대 한는 고가의 솔루션 보다 더 많은 작업이 이었습니다. 점점 더 많은 사용자가 쉽게 액세스할 수 있도록를 원하는 대로이 문제는 큰 증가 합니다.  
  
 사용자 데이터에 임시로 액세스할 수 있도록 허용 해당 요청을 표현 하는 언어를 지정 해야 합니다. 데이터베이스에 단일 요청 쿼리;로 이루어집니다. 이러한 언어는 쿼리 언어를 라고 합니다. 많은 쿼리 언어는이 목적을 위해 개발 된 있지만 가장 인기 있는 상태가 된 다음 중 하나:는 1970 년대에 IBM에서 고안 된 구조적 쿼리 언어입니다. 일반적으로 머리 글자어 SQL, 알려진 하 고 "ess 큐 ell"와 "게임의 속 편"; 모두 듭니다. 이 설명서에서는 이전 발음을 사용합니다. SQL standard 1986를 ANSI 및 ISO 표준 1987; 있게 되었습니다. 오늘날 많은 유용한 데이터베이스 관리 시스템에서 사용 됩니다.  
  
 SQL 사용자의 임시 요구 사항을 해결 되지만 컴퓨터 프로그램에서 데이터 액세스에 대 한 필요성 자리를 비울 않을 하지 않았습니다. 실제로 대부분의 데이터베이스 액세스 여전히 (였으며)에 사용 되는 주문 입력 및 데이터 조작 프로그램 계정 조정에 사용 되는 같은 프로그래밍 방식의 정기적으로 예약 된 보고서 및 통계 분석의 형태로, 데이터 입력 프로그램 및 작업 순서를 생성 합니다.  
  
 이러한 프로그램에는 또한 다음과 같은 세 가지 방법 중 하나를 사용 하 여 SQL 사용:  
  
-   **SQL 포함**, SQL 문은 C 또는 COBOL 등의 호스트 언어로 포함 됩니다.  
  
-   **SQL 모듈**, 어떤 SQL 문 DBMS에서 컴파일된 및 호스트 언어에서 호출 됩니다.  
  
-   **호출 수준 인터페이스**, 또는 CLI는 DBMS에 SQL 문을 전달 하 고 결과를 검색 하는 DBMS에서 호출 된 함수의 구성 됩니다.  
  
> [!NOTE]  
>  호출 수준 인터페이스 응용 프로그램 프로그래밍 하는 대신 사용 하는 용어 (API) 상호 연결 되는 기록 사건은 동일한 작업에 대 한 다른 용어입니다. 데이터베이스 세계에서 API 자체 SQL에 설명 하는 데 사용: SQL는 DBMS에 API입니다.  
  
 이러한 선택 항목의 포함 된 SQL은 가장 일반적으로 사용 되는 대부분 주 Dbms 소유 Cli를 지원 하지만입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL 문 처리](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [Embedded SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 모듈](../../odbc/reference/sql-modules.md)  
  
-   [호출 수준 인터페이스](../../odbc/reference/call-level-interfaces.md)
