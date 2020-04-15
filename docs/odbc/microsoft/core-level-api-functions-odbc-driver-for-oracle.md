---
title: 코어 레벨 API 기능(오라클용 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19751bb6d0556b117d0a73967d4db00c408733ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281023"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>핵심 수준 API 함수(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 이 수준의 함수는 ODBC 드라이버에 대한 최소 인터페이스 적합성 수준으로 구성됩니다.  
  
|API 기능|메모|  
|------------------|-----------|  
|**SQLAllocConnect**|*henv에*의해 식별 된 환경 내에서 연결 핸들, *hdbc에*대한 메모리를 할당합니다. 드라이버 관리자는 이 호출을 처리하고 **SQLConnect,** **SQLBrowseConnect**또는 **SQLDriverConnect가** 호출될 때마다 드라이버의 **SQLAllocConnect** 함수를 호출합니다.|  
|**SQLAllocEnv**|Oracle Client 소프트웨어에 대한 요구 사항을 지정하는 대화 상자를 표시한 다음 SQL_NULL_HANDLE 반환합니다. Oracle Client 소프트웨어가 설치되어 있지 않은 경우 이 함수는 환경 핸들, *henv에*메모리를 할당하고 응용 프로그램에서 사용할 ODBC 호출 수준 인터페이스를 초기화합니다.|  
|**SQLAllocStmt**|명령문 핸들에 메모리를 할당하고 명령문 핸들을 hdbc에서 지정한 연결과 연결합니다. 드라이버 관리자는 hstmt 구조에 대 한 메모리를 할당 하는 드라이버에 이 호출을 전달 합니다.|  
|**SQLBindCol**|결과 열에 대한 저장소 공간을 할당하고 결과 유형을 지정합니다.|  
|**SQLCancel**|명령문 핸들 hstmt에서 처리를 취소합니다. 경우에 따라 오라클은 실행 중인 명령문의 취소를 허용하지 않습니다. 즉, 오라클이 프로세스를 완료할 때까지 실행 중인 문이 계속되며, 이 때 오라클의 ODBC 드라이버에 의해 명령문의 결과가 취소됩니다.|  
|**SQLCol속성**|결과 집합의 열에 대한 설명자 정보를 반환합니다. 설명자 정보는 문자 문자열, 32비트 설명자 종속 값 또는 정수 값으로 반환됩니다.|  
|**SQLConnect**|데이터 원본에 연결합니다. Oracle 운영 체제 인증을 사용하려면 *szUID* 매개 변수로 "/"를 지정하고 *szAuthStr* 매개 변수로 ""를 지정합니다.|  
|**SQLDescribeCol**|지정된 결과 열의 이름, 유형, 정밀도, 배율 및 무효화가능성을 반환합니다. **참고: SQLDescribeCol은** 계산된 열을 SQL_VARCHAR 계산합니다.|  
|**SQL분리**|연결을 닫습니다. 공유 환경에 대해 연결 풀링을 사용하도록 설정하고 응용 프로그램이 해당 환경의 연결에서 **SQLDisconnect를** 호출하는 경우 연결은 연결 풀로 반환되고 동일한 공유 환경을 사용하는 다른 구성 요소에서 계속 사용할 수 있습니다.|  
|**SQL오류**|마지막 오류에 대한 오류 또는 상태 정보를 반환합니다. 드라이버는 **SQLError** 에 대한 호출이 이루어지는 방법에 따라 *hstmt,* *hdbc*및 *henv* 인수에 대해 반환할 수 있는 스택 또는 오류 목록을 유지 관리합니다. 각 문 후에 오류 큐가 플러시됩니다. 일반적으로 Oracle 오류 메시지를 검색하고 비어 있습니다.|  
|**SQLExecDirect**|준비되지 않은 새 SQL 문을 실행합니다. 드라이버는 문안에 매개 변수가 있는 경우 매개 변수 마커 변수의 현재 값을 사용합니다. 테이블, 뷰 또는 필드 이름에 공백이 포함된 경우 이름을 따옴표로 둘러싸십시오. 예를 들어 데이터베이스에 *내 테이블이라는* 테이블과 *내 필드필드가*포함된 경우 식별자의 각 요소를 다음과 같이 둘러싸십시오.<br /><br /> 내 \`테이블을\`선택합니다. \`내 필드1,;\` \`내\`테이블 . 내 테이블에서 내 필드2\` \` \`\`|  
|**SQLExecute**|준비된 SQL **문(SQLPrepare에서**이미 준비한 명령문)을 실행합니다. 드라이버는 문안에 매개 변수가 있는 경우 매개 변수 마커 변수의 현재 값을 사용합니다.|  
|**SQLFetch**|**SQLBindCol**에 대한 이전 호출에서 지정한 위치로 설정된 결과에서 한 행을 검색합니다. 언바운드 열에 대해 **SQLGetData** 호출에 대한 드라이버를 준비합니다.|  
|**SQLFreeConnect**|연결 핸들을 해제하고 핸들에 할당된 모든 메모리를 해제합니다.|  
|**SQL프리엔프**|오라클의 ODBC 드라이버를 닫고 드라이버와 관련된 모든 메모리를 해제합니다.|  
|**SQLFreeStmt**|특정 hstmt와 관련된 처리를 중지하고, hstmt와 연결된 열린 커서를 닫고, 보류 중인 결과를 버리고, 선택적으로 문 핸들과 관련된 모든 리소스를 해제합니다.|  
|**SQLGetCursorName**|지정된 hstmt와 연결된 커서의 이름을 반환합니다.|  
|**SQLNumResultCols**|결과 집합 커서의 열 수를 반환합니다.|  
|**SQLPrepare**|문을 최적화하고 실행하는 방법을 계획하여 SQL 문을 준비합니다. SQL 문은 **SQLExecDirect에**의해 실행을 위해 컴파일됩니다.<br /><br /> 테이블, 뷰 또는 필드 이름에 공백이 포함된 경우 이름을 따옴표로 둘러싸십시오. 예를 들어 데이터베이스에 *내 테이블이라는* 테이블과 *내 필드필드가*포함된 경우 식별자의 각 요소를 다음과 같이 둘러싸십시오.<br /><br /> 내 \`테이블을\`선택합니다. \`내\` 테이블에서 \`내 필드\`<br /><br /> 배열을 포함하는 결과 집합을 형식 매개 변수로 사용하는 자세한 내용은 [저장 프로시저의 배열 매개 변수 반환을](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)참조하십시오.|  
|**SQLRowCount**|Oracle은 마지막 행을 가져올 때까지 결과 집합의 행 수를 결정하는 방법을 제공하지 않으므로 -1을 반환합니다.|  
|**SQLSetCursorName**|활성 문 핸들 *hstmt와*커서 이름을 연결합니다.|  
|**SQLSetParam**|ODBC 2에서 SQLBind매개 변수로 대체되었습니다. *x*.|  
|**SQLTransact**|연결과 연결된 모든 명령문 핸들(hstmts)의 모든 활성 작업에 대해 커밋 또는 롤백 작업을 요청하거나 환경 핸들과 연결된 모든 연결에 대해 *henv*를 요청합니다. 수동 모드에서 커밋이 실패하면 트랜잭션은 활성 상태로 유지됩니다. 트랜잭션을 롤백하거나 커밋 작업을 다시 시도할 수 있습니다. 자동 트랜잭션 모드에서 커밋 작업이 실패하면 트랜잭션이 자동으로 롤백됩니다. 트랜잭션이 비활성 상태일 수 없습니다.|
