---
title: "수준 2 인터페이스 규칙에 따라 | Microsoft Docs"
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
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4002a7b376a752d4c5d3a2ddd2506bc9357842fa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="level-2-interface-conformance"></a>수준 2 인터페이스 규칙
수준 2 인터페이스 규칙 수준은 Level 1 인터페이스 규칙 – 수준 기능 및 다음 기능에 포함 되어 있습니다.  
  
|||  
|-|-|  
|201|데이터베이스 테이블 및 뷰 세 부분으로 이루어진 이름을 사용 합니다. (자세한 내용은 참조는 두 부분으로 이루어진 명명 지원 기능 101에 [수준 1 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|동적 매개 변수를 호출 하 여 설명 **SQLDescribeParam**합니다.|  
|203|뿐만 아니라 입력된 매개 변수가 있지만 출력 및 입/출력 매개 변수 및 저장된 프로시저의 결과 값을 사용 합니다.|  
|204|책갈피를 호출 하 여 검색을 포함 하 여 책갈피를 사용 하 여 **SQLDescribeCol** 및 **SQLColAttribute** 열 번호는 0, 호출 하 여 책갈피에 기반을 인출 **SQLFetchScroll** 와 *FetchOrientation* 인수 SQL_FETCH_BOOKMARK; 및 update를 설정 합니다. 삭제 하 고 호출 하 여 책갈피 작업에 의해 인출 **SQLBulkOperations** 는 와*작업* 인수 SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK, 또는 SQL_FETCH_BY_BOOKMARK로 설정 합니다.|  
|205|호출 하 여 고급 데이터 사전에 대 한 정보 검색 **SQLColumnPrivileges**, **SQLForeignKeys**, 및 **SQLTablePrivileges**합니다.|  
|206|SQL 문 대신 ODBC 함수를 사용 하 여 호출 하 여 추가 데이터베이스 작업을 수행 하려면 **SQLBulkOperations** SQL_ADD와 또는 **SQLSetPos** SQL_DELETE 또는 SQL_UPDATE 합니다. (지원에 대 한 호출 **SQLSetPos** 와 *LockType* SQL_LOCK_EXCLUSIVE 또는 SQL_LOCK_UNLOCK로 설정 하는 인수 받는 규칙 수준의 일부 이지만 선택적 기능입니다.)|  
|207|지정 된 개별 문에 대 한 ODBC 함수의 비동기 실행을 사용 하도록 설정 합니다.|  
|208|호출 하 여 테이블의 행 식별 열 SQL_ROWVER 가져올 **SQLSpecialColumns**합니다. (자세한 내용은 참조에 대 한 지원 **SQLSpecialColumns** 와 *IdentifierType* 인수 SQL_BEST_ROWID에 20을 기능으로로 설정 [핵심 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/core-interface-conformance.md) .)|  
|209|문 특성 SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY 이외의 값이 하나 이상 설정.|  
|210|로그인 요청 시간 초과 및 SQL 쿼리 (SQL_ATTR_LOGIN_TIMEOUT 및 SQL_ATTR_QUERY_TIMEOUT) 수 있습니다.|  
|211|기본 격리 수준 변경 하는 기능 "직렬화" 수준의 격리를 사용 하 여 트랜잭션을 실행 하는 기능입니다.|
