---
title: 핵심 수준 API 함수 (ODBC Driver for Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4135e192a2a97944ff455c72c76c136faaac4652
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>핵심 수준 API 함수 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 이 수준에서 기능 ODBC 드라이버에 대 한 인터페이스 규칙의 최소 수준으로 구성 됩니다.  
  
|API 함수|참고|  
|------------------|-----------|  
|**SQLAllocConnect**|연결 핸들에 대 한 메모리를 할당 *hdbc*로 식별 되는 환경 내에서 *henv*합니다. 드라이버 관리자는이 호출을 처리 하 고 드라이버의 호출 **SQLAllocConnect** 때마다 함수 **SQLConnect**, **SQLBrowseConnect**, 또는  **SQLDriverConnect** 호출 됩니다.|  
|**SQLAllocEnv**|Oracle 클라이언트 소프트웨어에 대 한 요구 사항을 지정 하는 대화 상자를 표시 하 고 SQL_NULL_HANDLE를 반환 합니다. 이 함수는 환경 핸들에 대 한 메모리를 할당 Oracle 클라이언트 소프트웨어가 설치 되지 않은 경우 *henv*, 응용 프로그램에서 사용 하기 위해 ODBC 호출 수준 인터페이스를 초기화 합니다.|  
|**SQLAllocStmt**|문 핸들에 대 한 메모리를 할당 하 고 hdbc로 지정 된 연결 된 문 핸들을 연결 합니다. 드라이버 관리자는이 호출 hstmt 구조에 대 한 메모리를 할당 하는 드라이버에 전달 합니다.|  
|**SQLBindCol**|결과 열에 대 한 저장 공간을 할당 하 고 결과의 유형을 지정 합니다.|  
|**SQLCancel**|문 핸들을 hstmt에서 처리를 취소합니다. 경우에 따라 Oracle의 실행 중인 문 취소를 허용 하지 않습니다. 즉, Oracle ODBC Driver for Oracle에 의해 취소 될 문에서 결과 될 때 프로세스를 완료 될 때까지 실행 중인 문을 계속 됩니다.|  
|**SQLColAttributes**|결과 집합의 열에 대 한 설명자 정보를 반환합니다. 설명자 정보 문자열, 32 비트 설명자 종속 값 또는 정수 값으로 반환 됩니다.|  
|**SQLConnect**|데이터 원본에 연결합니다. Oracle 운영 체제 인증을 사용 하려면 지정 "/"로 *szUID* 매개 변수 및 ""로 *szAuthStr* 매개 변수입니다.|  
|**SQLDescribeCol**|이름, 형식, 정밀도, 배율 및 지정 된 결과 열의 null 허용 여부를 반환합니다. **참고:****SQLDescribeCol** SQL_VARCHAR로 계산 된 열을 보고 합니다.|  
|**SQLDisconnect**|연결을 닫습니다. 공유 환경에 대 한 연결 풀링이 사용 되 고 응용 프로그램이 호출 **SQLDisconnect** 해당 환경에서 해당 연결에서 연결이 연결 풀으로 반환 되 고 계속 사용 하 여 다른 구성 요소에 사용할 수 동일한 공유 환경입니다.|  
|**SQLError**|마지막 오류에 대 한 오류 또는 상태 정보를 반환합니다. 스택 또는 오류에 대 한 반환 될 수 있는 목록을 유지 관리 하는 드라이버는 *hstmt*, *hdbc*, 및 *henv* 방법에 따라 인수에 대 한 호출 **SQLError**  이루어집니다. 오류 큐는 각 문 뒤에 플러시됩니다. 일반적으로 Oracle 오류 메시지를 검색 있으며 그렇지 않은 경우 비어 있습니다.|  
|**SQLExecDirect**|새, 준비 되지 않은 SQL 문을 실행합니다. 드라이버 문에 매개 변수가 있는 경우 매개 변수 표식 변수의 현재 값을 사용 합니다. 테이블, 뷰 또는 필드 이름에 공백이 있으면 이름을 따옴표 뒤에 기호를 묶습니다. 예를 들어, 테이블이 있는 데이터베이스에 있으면 *My Table* 및 필드 *My Field*, 식별자의 각 요소를 묶습니다 같이:<br /><br /> 선택 \`표\`합니다. \`내 Field1\`, \`표\`.\` 내 Field2\` FROM \`표 '|  
|**SQLExecute**|준비 된 SQL 문을 실행 (여 이미 준비 된 문을 **SQLPrepare**). 드라이버 문에 매개 변수가 있는 경우 매개 변수 표식 변수의 현재 값을 사용 합니다.|  
|**SQLFetch**|결과 집합에 대 한 이전 호출에서 지정한 위치에서에서 한 행을 검색 **SQLBindCol**합니다. 드라이버에 대 한 호출에 대 한 준비 **SQLGetData** 바인딩되지 않은 열에 대 한 합니다.|  
|**SQLFreeConnect**|연결 핸들을 해제 하 고 핸들에 대해 할당 된 모든 메모리를 해제 합니다.|  
|**SQLFreeEnv**|ODBC Driver for Oracle 닫고 드라이버와 관련 된 모든 메모리를 해제 합니다.|  
|**SQLFreeStmt**|특정 hstmt와 연결 된 처리를 중지는 hstmt와 관련 된 열려 있는 모든 커서를 닫고, 보류 중인 결과가 삭제 및 필요에 따라 문 핸들에 연결 된 모든 리소스를 해제 합니다.|  
|**SQLGetCursorName**|주어진된 hstmt 연관 된 커서의 이름을 반환 합니다.|  
|**SQLNumResultCols**|결과 집합 커서의 열 수를 반환합니다.|  
|**SQLPrepare**|최적화 하 고 문을 실행 하는 방법을 계획 하 여 SQL 문을 준비 합니다. 실행 SQL 문이 컴파일된 **SQLExecDirect**합니다.<br /><br /> 테이블, 뷰 또는 필드 이름에 공백이 있으면 이름을 따옴표 뒤에 기호를 묶습니다. 예를 들어, 데이터베이스 라는 테이블을 포함 하는 경우 *My Table* 및 필드 *My Field*, 식별자의 각 요소를 다음과 같이 묶습니다.<br /><br /> 선택 \`표\`.\` My Field\` FROM \`표 '<br /><br /> 정식 매개 변수로 서 배열을 포함 하는 결과 집합을 사용 하는 방법에 대 한 정보를 참조 하십시오. [저장 프로시저에서 배열 매개 변수 반환](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)합니다.|  
|**SQLRowCount**|Oracle에는 결과 집합 후 마지막 행을 인출 있으므로 반환 될 때까지-1의에서 행 수를 결정 하는 방법을 제공 하지 않습니다.|  
|**SQLSetCursorName**|활성 문 핸들에는 커서 이름을 연결 *hstmt*합니다.|  
|**SQLSetParam**|ODBC 2의에서 SQLBindParameter로 바뀝니다. *x*합니다.|  
|**SQLTransact**|연결을 통해 연결 된 모든 문 핸들 (hstmts)의 모든 활성 작업에 대해 또는 환경 핸들에 연결 된 모든 연결에 대 한 커밋 또는 롤백 작업을 요청 *henv*합니다. 수동 모드에 있을 때 커밋 실패 하면 트랜잭션이 활성 상태로 유지 되; 트랜잭션을 롤백 또는 커밋 작업을 다시 시도를 선택할 수 있습니다. 자동 트랜잭션 모드에 있을 때 커밋 작업이 실패 하면 트랜잭션이 롤백됩니다 트랜잭션이 비활성화할 수 없습니다.|
