---
title: "인터페이스 규칙에 따라 핵심 | Microsoft Docs"
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
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1df0215014eea87559e87aeb2f29e848e1473a66
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="core-interface-conformance"></a>핵심 인터페이스 규칙
모든 ODBC 드라이버 이상 핵심 수준 통해 인터페이스를 준수 합니다. 핵심 수준에서 기능 대부분의 제네릭 상호 운용 가능한 응용 프로그램에서 필요한 것 이므로, 드라이버는 이러한 응용 프로그램 작업할 수 있습니다. 핵심 수준에서 기능 ISO CLI 사양에 정의 된 기능 하 고 Open 그룹 CLI 사양에 정의 된 nonoptional 기능에도 해당 합니다. 핵심 수준 인터페이스 – 준수 ODBC 드라이버는 다음과 같은 작업을 수행 하는 응용 프로그램을 허용 합니다.  
  
-   할당 하 고 호출 하 여 모든 유형의 핸들을 해제 **SQLAllocHandle** 및 **SQLFreeHandle**합니다.  
  
-   모든 형태를 사용 하 여는 **SQLFreeStmt** 함수입니다.  
  
-   호출 하 여 결과 집합 열을 바인딩할 **SQLBindCol**합니다.  
  
-   동적 매개 변수를 호출 하 여 입력 방향 으로만, 매개 변수 배열을 포함 하 여 처리 **SQLBindParameter** 및 **SQLNumParams**합니다. (출력 방향에서 매개 변수에서 203 기능는 [수준 2 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   바인딩 오프셋을 지정 합니다.  
  
-   에 대 한 호출과 관련 된 실행 시 데이터 대화 상자에서 사용 하 여 **SQLParamData** 및 **SQLPutData**합니다.  
  
-   호출 하 여 커서 및 커서 이름 관리 **SQLCloseCursor**, **SQLGetCursorName**, 및 **SQLSetCursorName**합니다.  
  
-   호출 하 여 결과 집합의 설명 (메타 데이터)에 대 한 액세스를 위해 **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**, 및 **SQLRowCount** . (책갈피 메타 데이터를 검색할 열 번호는 0에서 이러한 기능을 사용 하는 기능을에서 204 [수준 2 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   카탈로그 함수를 호출 하 여 데이터 사전 쿼리 **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**, 및 **SQLTables**합니다.  
  
     드라이버 다중 부분 이름 데이터베이스 테이블 및 뷰를 지 원하는 데 필요 하지 않습니다. (자세한 내용은 101에 기능을 참조 하십시오. [수준 1 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-1-interface-conformance.md) 201의 기능 및 [수준 2 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) 그러나 열을 한정 및 인덱스의 이름과 같은 SQL 92 사양의 특정 기능을 구문상 유사 다중 부분 이름을 지정 합니다. S Q l 92의 이러한 정보를 새 옵션을 소개 하기 위한 ODBC 기능의 현재 목록을 적합 하지 않습니다.  
  
-   데이터 원본 및 연결을 호출 하 여 관리할 **SQLConnect**, **SQLDataSources**, **SQLDisconnect**, 및 **SQLDriverConnect**합니다. ODBC에 관계 없이 수준을 지 원하는 호출 하 여 드라이버에 대 한 자세한 내용을 **SQLDrivers**합니다.  
  
-   준비 및 호출 하 여 SQL 문을 실행 **SQLExecDirect**, **SQLExecute**, 및 **SQLPrepare**합니다.  
  
-   호출 하 여 결과 집합의 한 행 이나 앞 으로만에서 여러 행을 인출 **SQLFetch** 또는 호출 하 여 **SQLFetchScroll** 와 *FetchOrientation* 인수 SQL_FETCH_NEXT로 설정 합니다.  
  
-   호출 하 여 부분으로 바인딩되지 않은 열을 가져올 **SQLGetData**합니다.  
  
-   호출 하 여 모든 특성의 현재 값을 가져올 **SQLGetConnectAttr**, **SQLGetEnvAttr**, 및 **SQLGetStmtAttr**, 모든 특성을 해당 기본값으로 설정 하 고 특정 특성을 호출 하 여 기본이 아닌 값으로 설정 **SQLSetConnectAttr**, **SQLSetEnvAttr**, 및 **SQLSetStmtAttr**합니다.  
  
-   설명자의 특정 필드를 호출 하 여 조작 **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**, 및 **SQLSetDescRec**합니다.  
  
-   호출 하 여 진단 정보를 가져올 **SQLGetDiagField** 및 **SQLGetDiagRec**합니다.  
  
-   호출 하 여 드라이버 기능을 검색 **SQLGetFunctions** 및 **SQLGetInfo**합니다. 또한 호출 하 여 데이터 원본에 전송 하기 전에 SQL 문을 하려고 모든 텍스트를 대체의 결과 검색 **SQLNativeSql**합니다.  
  
-   구문을 사용 하 여 **SQLEndTran** 된 트랜잭션을 커밋합니다. 핵심 수준 드라이버 필요 true 트랜잭션을;를 지원 하지 않습니다. 따라서 응용 프로그램 연결 특성 SQL_ATTR_AUTOCOMMIT SQL_ROLLBACK 나 SQL_AUTOCOMMIT_OFF 지정할 수 없습니다. (자세한 내용은 참조 109 기능인 [수준 2 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   호출 **SQLCancel** 실행 시 데이터 대화 상자를 취소 하 고, 다른 스레드의 ODBC 함수가 실행을 취소 하려면 다중 스레드 환경에서 합니다. 핵심 수준 인터페이스 규칙의 사용 및 함수의 비동기 실행에 대 한 지원이 필요 하지 않습니다 **SQLCancel** ODBC 함수를 비동기적으로 실행 취소할 수 있습니다. 플랫폼도 아니고 ODBC 드라이버는 동시에 독립적인 작업을 수행 하 고 드라이버에 대 한 다중 스레드 수 있어야 합니다. 그러나 다중 스레드 환경에서 ODBC 드라이버에는 스레드로부터 안전 이어야 합니다. 응용 프로그램에서 보낸 요청의 serialization 심각한 성능 문제를 만들 수 있지만이 사양을 구현 수와 호환 되는.  
  
-   호출 하 여 테이블의 행 식별 열 SQL_BEST_ROWID 가져올 **SQLSpecialColumns**합니다. (SQL_ROWVER에 대 한 지원의 208 기능는 [수준 2 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  ODBC 드라이버는 핵심 인터페이스 규칙 수준에서 기능을 구현 해야 합니다.
