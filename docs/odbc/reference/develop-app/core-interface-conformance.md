---
title: 코어 인터페이스 적합성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886ded1cd79b35488c0d47df3dbd8055dc6a8016
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302135"
---
# <a name="core-interface-conformance"></a>핵심 인터페이스 적합성
모든 ODBC 드라이버는 최소한 코어 레벨 인터페이스 적합성을 나타내야 합니다. 코어 수준의 기능은 대부분의 일반적인 상호 운용 가능한 응용 프로그램에 필요한 기능이므로 드라이버는 이러한 응용 프로그램에서 작업할 수 있습니다. 코어 레벨의 기능은 ISO CLI 사양에 정의된 기능및 오픈 그룹 CLI 사양에 정의된 선택사양이 아닌 기능에도 해당합니다. 코어 레벨 인터페이스 를 준수하는 ODBC 드라이버를 사용하면 응용 프로그램에서 다음 을 모두 수행할 수 있습니다.  
  
-   **SQLAllocHandle** 및 **SQLFreeHandle**을 호출하여 모든 유형의 핸들을 할당하고 해제합니다.  
  
-   **SQLFreeStmt** 함수의 모든 형태를 사용합니다.  
  
-   **SQLBindCol**을 호출하여 결과 집합 열을 바인딩합니다.  
  
-   **SQLBindParameter** 및 **SQLNumParams을**호출하여 입력 방향으로만 매개 변수 배열을 포함한 동적 매개 변수를 처리합니다. (출력 방향의 매개 변수는 레벨 [2 인터페이스 적합성의](../../../odbc/reference/develop-app/level-2-interface-conformance.md)기능 203입니다.)  
  
-   바인드 오프셋을 지정합니다.  
  
-   **SQLParamData** 및 **SQLPutData에**대한 호출과 관련된 실행 시 데이터 대화 상자를 사용합니다.  
  
-   **SQLCloseCursor,** **SQLGetCursorName**및 **SQLSetCursorName을**호출하여 커서 및 커서 이름을 관리합니다.  
  
-   **SQLColAttribute,** **SQLDescribeCol,** **SQLNumResultCols**및 **SQLRowCount를**호출하여 결과 집합의 설명(메타데이터)에 액세스할 수 있습니다. (책갈피 메타데이터를 검색하기 위해 열 번호 0에서 이러한 함수를 사용하는 것은 [수준 2 인터페이스 적합성의](../../../odbc/reference/develop-app/level-2-interface-conformance.md)기능 204입니다.)  
  
-   카탈로그 함수 **SQLColumns,** **SQLGetTypeInfo,** **SQLStatistics**및 **SQLTable을**호출하여 데이터 사전을 쿼리합니다.  
  
     드라이버는 데이터베이스 테이블 및 뷰의 다중 부분 이름을 지원할 필요가 없습니다. (자세한 내용은 레벨 1 인터페이스 [적합성의](../../../odbc/reference/develop-app/level-1-interface-conformance.md) 기능 101 및 [레벨 2 인터페이스 적합성의](../../../odbc/reference/develop-app/level-2-interface-conformance.md)기능 201을 참조하십시오.) 그러나 열 자격 및 인덱스 이름과 같은 SQL-92 사양의 특정 기능은 구문적으로 다중 부분 이름과 비교할 수 있습니다. ODBC 기능의 현재 목록은 SQL-92의 이러한 측면에 새로운 옵션을 소개하기 위한 것이 아닙니다.  
  
-   **SQLConnect,** **SQLDataSource,** **SQLDisconnect**및 **SQLDriverConnect를**호출하여 데이터 원본 및 연결을 관리합니다. **SQLDriver를**호출하여 지원되는 ODBC 수준에 관계없이 드라이버에 대한 정보를 얻을 수 있습니다.  
  
-   **SQLExecDirect**, **SQLExecute**및 **SQLPrepare를**호출하여 SQL 문을 준비하고 실행합니다.  
  
-   **SQLFetch를** 호출하거나 *fetchOrientation* 인수를 SQL_FETCH_NEXT 설정된 **SQLFetchScroll를** 호출하여 결과 집합 또는 여러 행의 한 행을 앞으로 방향으로만 가져옵니다.  
  
-   **SQLGetData**를 호출하여 부분에서 언바운드 열을 가져옵니다.  
  
-   **SQLGetConnectAttr,** **SQLGetEnvAttr**및 **SQLGetStmtAttr을**호출하여 모든 특성의 현재 값을 얻고 모든 특성을 기본값으로 설정하고 **SQLSetConnectAttr,** **SQLSetEnvAttr**및 **SQLSetStmtAttr을**호출하여 기본값이 아닌 값으로 특정 특성을 설정합니다.  
  
-   **SQLCopyDesc,** **SQLGetDescField,** **SQLGetDescRec,** **SQLSetDescField**및 **SQLSetDescCRec를**호출하여 설명자의 특정 필드를 조작합니다.  
  
-   **SQLGetDiagField** 및 **SQLGetDiagRec을**호출하여 진단 정보를 가져옵니다.  
  
-   **SQLGetFunctions** 및 **SQLGetInfo를**호출하여 드라이버 기능을 검색합니다. 또한 **SQLNativeSql**을 호출하여 데이터 원본으로 전송되기 전에 SQL 문에 대한 텍스트 대체 의 결과를 검색합니다.  
  
-   **SQLEndTran의** 구문을 사용하여 트랜잭션을 커밋합니다. 코어 수준 드라이버는 실제 트랜잭션을 지원할 필요가 없습니다. 따라서 응용 프로그램은 SQL_ATTR_AUTOCOMMIT 연결 특성에 대한 SQL_ROLLBACK 지정하거나 SQL_AUTOCOMMIT_OFF 수 없습니다. (자세한 내용은 레벨 2 인터페이스 [적합성의](../../../odbc/reference/develop-app/level-2-interface-conformance.md)기능 109를 참조하십시오.)  
  
-   **SQLCancel을** 호출하여 실행 시 데이터 대화 상자를 취소하고 다중 스레드 환경에서 다른 스레드에서 실행되는 ODBC 함수를 취소합니다. 코어 수준 인터페이스 준수는 함수의 비동기 실행에 대한 지원을 요구하지 않으며 **SQLCancel을** 사용하여 비동기적으로 실행되는 ODBC 함수를 취소하도록 명령하지 않습니다. 플랫폼이나 ODBC 드라이버가 동시에 독립적인 활동을 수행하기 위해 다중 스레드일 필요는 없습니다. 그러나 다중 스레드 환경에서는 ODBC 드라이버가 스레드에 안전해야 합니다. 응용 프로그램에서 요청을 직렬화하는 것은 심각한 성능 문제를 일으킬 수 있더라도 이 사양을 구현하는 준수한 방법입니다.  
  
-   **SQLSpecialColumns를**호출하여 테이블의 행 식별 열을 SQL_BEST_ROWID 가져옵니다. (SQL_ROWVER 대한 지원은 레벨 [2 인터페이스 적합성의](../../../odbc/reference/develop-app/level-2-interface-conformance.md)기능 208입니다.)  
  
    > [!IMPORTANT]  
    >  ODBC 드라이버는 코어 인터페이스 적합성 수준에서 함수를 구현해야 합니다.
