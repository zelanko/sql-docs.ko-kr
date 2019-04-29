---
title: 핵심 인터페이스 적합성 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e41d71cd3651e1db5d1a533159012b645b8c7764
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043764"
---
# <a name="core-interface-conformance"></a>핵심 인터페이스 적합성
모든 ODBC 드라이버를 갖추고 있어야 합니다. 최소한 핵심 인터페이스 적합성 합니다. 코어 수준에서 기능 가장 일반적인 상호 운용 가능한 응용 프로그램에 필요한 것 이기 때문에 이러한 응용 프로그램은 드라이버를 사용할 수 있습니다. 코어 수준에서 기능에도 nonoptional 기능 열기 그룹 CLI 사양에서 정의 하는 ISO CLI 사양에 정의 된 기능에 해당 합니다. 핵심 수준 인터페이스와 호환 되는 ODBC 드라이버는 다음과 같은 작업을 수행 하는 응용 프로그램을 허용 합니다.  
  
-   할당 하 고 호출 하 여 모든 유형의 핸들을 해제 **SQLAllocHandle** 하 고 **SQLFreeHandle**합니다.  
  
-   모든 형태를 사용 합니다 **SQLFreeStmt** 함수입니다.  
  
-   호출 하 여 결과 집합 열을 바인딩할 **SQLBindCol**합니다.  
  
-   동적 매개 변수를 호출 하 여 배열을 입력 방향의, 매개 변수를 포함 하 여 처리할 **SQLBindParameter** 하 고 **SQLNumParams**합니다. (출력 방향에서 매개 변수는 기능을에 203 [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   바인딩 오프셋을 지정 합니다.  
  
-   에 대 한 호출과 관련 된 실행 시 데이터 대화 상자에서 사용 하 여 **SQLParamData** 하 고 **SQLPutData**합니다.  
  
-   커서 및 커서 이름은 호출 하 여 관리할 **SQLCloseCursor**를 **SQLGetCursorName**, 및 **SQLSetCursorName**합니다.  
  
-   호출 하 여 결과 집합에 대 한 설명 (메타 데이터)에 대 한 액세스를 얻을 **SQLColAttribute**를 **SQLDescribeCol**합니다 **SQLNumResultCols**, 및 **SQLRowCount** . (책갈피 메타 데이터를 검색할 열 번호는 0에서 이러한 기능을 사용 하는 기능을에서 204 [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   카탈로그 함수를 호출 하 여 데이터 사전 쿼리 **SQLColumns**, **SQLGetTypeInfo**합니다 **SQLStatistics**, 및 **SQLTables**합니다.  
  
     드라이버 다중 부분 이름 데이터베이스 테이블 및 뷰를 지 원하는 데 필요 하지 않습니다. (자세한 내용은 101의 기능을 참조 하세요. [수준 1 인터페이스 적합성](../../../odbc/reference/develop-app/level-1-interface-conformance.md) 및 기능에서 201 [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) 그러나 SQL-92 사양에 열을 한정 인덱스의 이름 등의 특정 기능은 다중 부분 이름을 지정 하 구문적으로 비교할 수 있습니다. SQL-92의 이러한 측면에 대 한 새 옵션을 소개 하기 위해 ODBC 기능 목록이 있는 아닙니다.  
  
-   호출 하 여 데이터 원본 및 연결 관리 **SQLConnect**, **SQLDataSources**합니다 **SQLDisconnect**, 및 **SQLDriverConnect**합니다. ODBC에 관계 없이 수준을 지를 호출 하 여 드라이버에 대 한 정보를 가져올 **SQLDrivers**합니다.  
  
-   준비 하 고 호출 하 여 SQL 문을 실행할 **SQLExecDirect**를 **SQLExecute**, 및 **SQLPrepare**합니다.  
  
-   호출 하 여 결과 집합의 한 행 또는 정방향 전용의 여러 행을 인출 **SQLFetch** 또는 전화 800-659-3579 **SQLFetchScroll** 사용 하 여 합니다 *FetchOrientation* 인수 SQL_FETCH_NEXT로 설정 합니다.  
  
-   호출 하 여 부분으로 바인딩되지 않은 열을 얻을 **SQLGetData**합니다.  
  
-   호출 하 여 모든 특성의 현재 값을 얻을 **SQLGetConnectAttr**, **SQLGetEnvAttr**, 및 **SQLGetStmtAttr**, 모든 특성을 기본값으로 설정 하 고 특정 특성을 호출 하 여 기본이 아닌 값을 설정 **SQLSetConnectAttr**를 **SQLSetEnvAttr**, 및 **SQLSetStmtAttr**합니다.  
  
-   설명자의 특정 필드를 호출 하 여 조작 **SQLCopyDesc**를 **SQLGetDescField**를 **SQLGetDescRec**를 **SQLSetDescField**, 및 **SQLSetDescRec**합니다.  
  
-   호출 하 여 진단 정보를 얻는 **SQLGetDiagField** 하 고 **SQLGetDiagRec**합니다.  
  
-   드라이버 기능을 호출 하 여 감지 **SQLGetFunctions** 하 고 **SQLGetInfo**합니다. 또한 호출 하 여 데이터 원본에 전송 되기 전에 SQL 문에 대 한 모든 텍스트를 대체의 결과 검색할 **SQLNativeSql**합니다.  
  
-   구문을 사용 하 여 **SQLEndTran** 된 트랜잭션을 커밋합니다. 핵심 수준 드라이버 true 트랜잭션이; 지원할 필요가 따라서 응용 프로그램 연결 특성 SQL_ATTR_AUTOCOMMIT SQL_ROLLBACK 나 SQL_AUTOCOMMIT_OFF 지정할 수 없습니다. (자세한 내용은 참조에서 기능 109 [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   호출 **SQLCancel** 실행 시 데이터 대화 상자를 취소 하 고, 다른 스레드의 ODBC 함수 실행을 취소 하려면 다중 스레드 환경입니다. 핵심 수준 인터페이스 적합성은의 사용 및 함수의 비동기 실행에 대 한 지원을 요구 하지 않습니다 **SQLCancel** ODBC 함수를 비동기적으로 실행을 취소 합니다. 플랫폼도 아니고 ODBC 드라이버는 드라이버를 동시에 독립적인 작업을 수행 하려면 다중 스레드 있어야 합니다. 그러나 다중 스레드 환경에서 ODBC 드라이버에는 스레드로부터 안전한 이어야 합니다. 응용 프로그램에서 요청의 serialization은 심각한 성능 문제를 만들 수 있지만이 사양을 구현 방법와 호환 되는입니다.  
  
-   호출 하 여 테이블의 SQL_BEST_ROWID 행 식별 열을 가져올 **SQLSpecialColumns**합니다. (SQL_ROWVER 지원에서 208 기능 됩니다 [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  ODBC 드라이버는 핵심 인터페이스 적합성 수준에서 함수를 구현 해야 합니다.
