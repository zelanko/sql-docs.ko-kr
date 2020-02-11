---
title: 핵심 인터페이스 규칙 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02e8aabf808ebf11f2e241fc7d330f794dbb0112
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002111"
---
# <a name="core-interface-conformance"></a>핵심 인터페이스 적합성
모든 ODBC 드라이버는 최소한 코어 수준 인터페이스 규칙을 준수 해야 합니다. 핵심 수준의 기능은 대부분의 상호 운용성이 높은 응용 프로그램에 필요한 기능 이므로 이러한 응용 프로그램에서 드라이버를 사용할 수 있습니다. 핵심 수준의 기능은 ISO CLI 사양에 정의 된 기능과 오픈 그룹 CLI 사양에 정의 된 선택적 기능에도 해당 합니다. 코어 수준 인터페이스와 호환 되는 ODBC 드라이버를 사용 하면 응용 프로그램에서 다음 작업을 모두 수행할 수 있습니다.  
  
-   **SQLAllocHandle** 및 **sqlfreehandle**을 호출 하 여 모든 유형의 핸들을 할당 하 고 해제 합니다.  
  
-   모든 형태의 **SQLFreeStmt** 함수를 사용 합니다.  
  
-   **SQLBindCol**를 호출 하 여 결과 집합 열을 바인딩합니다.  
  
-   **SQLBindParameter** 및 **sqlnumparams**를 호출 하 여 입력 방향 에서만 매개 변수 배열을 포함 하는 동적 매개 변수를 처리 합니다. 출력 방향의 매개 변수는 [수준 2 인터페이스 규칙](../../../odbc/reference/develop-app/level-2-interface-conformance.md)의 기능 203입니다.  
  
-   바인딩 오프셋을 지정 합니다.  
  
-   **Sqlparamdata** 및 **sqlparamdata**에 대 한 호출을 포함 하는 실행 시 데이터 대화 상자를 사용 합니다.  
  
-   **SQLCloseCursor**, **SQLGetCursorName**및 **SQLSetCursorName**를 호출 하 여 커서 및 커서 이름을 관리 합니다.  
  
-   **Sqlcolattribute**, **SQLDescribeCol**, **Sqlnumresultcols**및 **sqlrowcount**를 호출 하 여 결과 집합의 설명 (메타 데이터)에 대 한 액세스 권한을 얻습니다. 책갈피 메타 데이터를 검색 하는 데 사용 되는 열 번호 0에 이러한 함수를 사용 하는 것은 [수준 2 인터페이스 규칙](../../../odbc/reference/develop-app/level-2-interface-conformance.md)의 기능 204입니다.  
  
-   **Sqlcolumns**, **SQLGetTypeInfo**, **SQLStatistics**및 **sqlcolumns**카탈로그 함수를 호출 하 여 데이터 사전을 쿼리 합니다.  
  
     드라이버는 데이터베이스 테이블 및 뷰의 여러 부분으로 된 이름을 지 원하는 데 필요 하지 않습니다. 자세한 내용은 [수준 1 인터페이스 규칙](../../../odbc/reference/develop-app/level-1-interface-conformance.md) 의 기능 101 및 [수준 2 인터페이스 규칙](../../../odbc/reference/develop-app/level-2-interface-conformance.md)의 기능 201을 참조 하세요. 그러나 열 한정 및 인덱스 이름과 같은 SQL-92 사양의 특정 기능은 multipart 명명과 구문적으로 비교 됩니다. 현재 ODBC 기능 목록은 SQL-92의 이러한 측면에 대 한 새로운 옵션을 소개 하기 위한 것이 아닙니다.  
  
-   **SQLConnect**, **sqldatasources**, **sqldatasources**및 **SQLDriverConnect**를 호출 하 여 데이터 원본 및 연결을 관리 합니다. **Sqldrivers**를 호출 하 여 지원 되는 ODBC 수준에 관계 없이 드라이버에 대 한 정보를 얻습니다.  
  
-   **Sqlexecdirect**, **Sqlexecute**및 **SQLPREPARE**를 호출 하 여 SQL 문을 준비 하 고 실행 합니다.  
  
-   **Sqlfetch** 를 호출 하거나 *fetchorientation* 인수가 SQL_FETCH_NEXT로 설정 된 **sqlfetchscroll** 을 호출 하 여 결과 집합의 한 행 또는 여러 행을 정방향 방향 으로만 인출 합니다.  
  
-   **SQLGetData**를 호출 하 여 파트에서 바인딩되지 않은 열을 가져옵니다.  
  
-   **SQLGetConnectAttr**, **SQLGetEnvAttr**및 **SQLGetStmtAttr**를 호출 하 여 모든 특성의 현재 값을 가져오고, 모든 특성을 기본값으로 설정 하 고, **SQLSetConnectAttr**, **SQLSetEnvAttr**및 **SQLSetStmtAttr**를 호출 하 여 특정 특성을 기본값이 아닌 값으로 설정 합니다.  
  
-   **Sqlcopydesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**및 **SQLSetDescRec**를 호출 하 여 설명자의 특정 필드를 조작 합니다.  
  
-   **SQLGetDiagField** 및 **SQLGetDiagRec**를 호출 하 여 진단 정보를 가져옵니다.  
  
-   **SQLGetFunctions** 및 **SQLGetInfo**를 호출 하 여 드라이버 기능을 검색 합니다. 또한 **SQLNativeSql**를 호출 하 여 데이터 원본으로 전송 되기 전에 SQL 문에 대 한 텍스트 대체의 결과를 검색 합니다.  
  
-   **Sqlendtran** 구문을 사용 하 여 트랜잭션을 커밋합니다. 핵심 수준 드라이버는 진정한 트랜잭션을 지원 하지 않아도 됩니다. 따라서 응용 프로그램은 SQL_ATTR_AUTOCOMMIT 연결 특성에 대해 SQL_ROLLBACK 또는 SQL_AUTOCOMMIT_OFF를 지정할 수 없습니다. 자세한 내용은 [수준 2 인터페이스 규칙](../../../odbc/reference/develop-app/level-2-interface-conformance.md)의 기능 109을 참조 하세요.  
  
-   **Sqlcancel** 을 호출 하 여 실행 시 데이터 대화 상자를 취소 하 고 다중 스레드 환경에서 다른 스레드에서 실행 중인 ODBC 함수를 취소 합니다. 핵심 수준 인터페이스 규칙은 비동기적으로 실행 되는 ODBC 함수를 **취소 하는** 함수 또는 비동기 실행을 지원 하지 않습니다. 드라이버가 독립 작업을 동시에 수행 하기 위해 플랫폼과 ODBC 드라이버 모두 다중 스레드를 필요로 하는 것은 아닙니다. 그러나 다중 스레드 환경에서는 ODBC 드라이버를 스레드로부터 안전 하 게 보호 해야 합니다. 응용 프로그램에서 요청을 직렬화 하는 것은 심각한 성능 문제를 만들 수 있지만이 사양을 구현 하는 것과 같은 규칙입니다.  
  
-   **SQLSpecialColumns**를 호출 하 여 테이블의 SQL_BEST_ROWID 행 식별 열을 가져옵니다. SQL_ROWVER에 대 한 지원은 [수준 2 인터페이스 규칙](../../../odbc/reference/develop-app/level-2-interface-conformance.md)의 기능 208입니다.  
  
    > [!IMPORTANT]  
    >  ODBC 드라이버는 핵심 인터페이스 규칙 수준에서 함수를 구현 해야 합니다.
