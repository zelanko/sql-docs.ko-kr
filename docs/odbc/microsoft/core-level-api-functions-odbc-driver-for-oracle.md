---
title: 코어 수준 API 함수 (Oracle 용 ODBC 드라이버) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281023"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>핵심 수준 API 함수(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 이 수준의 함수는 ODBC 드라이버에 대 한 인터페이스 규칙의 최소 수준을 구성 합니다.  
  
|API 함수|참고|  
|------------------|-----------|  
|**SQLAllocConnect**|*Henv*에 의해 식별 되는 환경 내에서 연결 핸들 *hdbc*의 메모리를 할당 합니다. 드라이버 관리자는이 호출을 처리 하 고 **SQLConnect**, **SQLBrowseConnect**또는 **SQLDriverConnect** 가 호출 될 때마다 드라이버의 **sqlallocconnect** 함수를 호출 합니다.|  
|**SQLAllocEnv**|Oracle 클라이언트 소프트웨어에 대 한 요구 사항을 지정 하는 대화 상자를 표시 한 다음 SQL_NULL_HANDLE을 반환 합니다. Oracle 클라이언트 소프트웨어가 설치 되지 않은 경우이 함수는 응용 프로그램에서 사용할 수 있도록 ODBC 호출 수준 인터페이스를 처리 하 고, *henv*하 고, 초기화 하는 환경에 대해 메모리를 할당 합니다.|  
|**SQLAllocStmt**|문 핸들에 대해 메모리를 할당 하 고 문 핸들을 hdbc에서 지정한 연결과 연결 합니다. 드라이버 관리자는이 호출을 드라이버에 전달 하 여 hstmt 구조에 대해 메모리를 할당 합니다.|  
|**SQLBindCol**|결과 열에 대 한 저장소 공간을 할당 하 고 결과 유형을 지정 합니다.|  
|**SQLCancel**|문 핸들 hstmt의 처리를 취소 합니다. 경우에 따라 Oracle은 실행 중인 문의 취소를 허용 하지 않습니다. 즉, Oracle이 프로세스를 완료할 때까지 실행 중인 문이 계속 되며, 이때 Oracle 용 ODBC 드라이버에서 문의 결과가 취소 됩니다.|  
|**SQLColAttributes**|결과 집합의 열에 대 한 설명자 정보를 반환 합니다. 설명자 정보는 문자열, 32 비트 설명자 종속 값 또는 정수 값으로 반환 됩니다.|  
|**SQLConnect**|데이터 원본에 연결 합니다. Oracle 운영 체제 인증을 사용 하려면 "/"를 *Szuid* 매개 변수로 지정 하 고 ""를 *szauthstr* 매개 변수로 지정 합니다.|  
|**SQLDescribeCol**|지정 된 결과 열의 이름, 형식, 전체 자릿수, 소수 자릿수 및 null 허용 여부를 반환 합니다. **참고: SQLDescribeCol** 는 SQL_VARCHAR으로 계산 열을 보고 합니다.|  
|**SQLDisconnect**|연결을 닫습니다. 공유 환경에 연결 풀링을 사용 하는 경우 응용 프로그램이 해당 환경에서 연결을 통해 **Sqldisconnect** 를 호출 하면 연결이 연결 풀로 반환 되 고 동일한 공유 환경을 사용 하는 다른 구성 요소에서 계속 사용할 수 있습니다.|  
|**SQLError**|마지막 오류에 대 한 오류 또는 상태 정보를 반환 합니다. 이 드라이버는 **SQLError** 를 호출 하는 방법에 따라 *hstmt*, *hdbc*및 *henv* 인수에 대해 반환 될 수 있는 오류 또는 스택 또는 목록을 유지 관리 합니다. 각 문 다음에 오류 큐가 플러시됩니다. 일반적으로 Oracle 오류 메시지를 검색 하며, 그렇지 않은 경우 비어 있습니다.|  
|**SQLExecDirect**|준비 되지 않은 새 SQL 문을 실행 합니다. 문에 매개 변수가 있는 경우 드라이버는 매개 변수 표식 변수의 현재 값을 사용 합니다. 테이블, 뷰 또는 필드 이름에 공백이 포함 된 경우에는 따옴표 안에 이름을 묶습니다. 예를 들어, 데이터베이스에 *내 테이블* 이라는 테이블과 *my field*필드가 있는 경우 식별자의 각 요소를 다음과 같이 묶습니다.<br /><br /> 내 \`테이블\`을 선택 합니다. \`내 Field1\`,; \`내 테이블\`. \`내 테이블\` 의 \`내 Field2\`|  
|**SQLExecute**|준비 된 SQL 문 ( **Sqlprepare**에서 이미 준비한 문)을 실행 합니다. 문에 매개 변수가 있는 경우 드라이버는 매개 변수 표식 변수의 현재 값을 사용 합니다.|  
|**SQLFetch**|결과 집합의 한 행을 **SQLBindCol**에 대 한 이전 호출에서 지정한 위치로 검색 합니다. 바인딩되지 않은 열에 대 한 **SQLGetData** 호출을 위한 드라이버를 준비 합니다.|  
|**SQLFreeConnect**|연결 핸들을 해제 하 고 핸들에 할당 된 모든 메모리를 해제 합니다.|  
|**SQLFreeEnv**|Oracle 용 ODBC 드라이버를 닫고 드라이버와 연결 된 모든 메모리를 해제 합니다.|  
|**SQLFreeStmt**|특정 hstmt와 연결 된 처리를 중지 하 고, hstmt와 연결 된 열려 있는 모든 커서를 닫고, 보류 중인 결과를 삭제 하 고, 필요에 따라 문 핸들과 연결 된 모든 리소스를 해제 합니다.|  
|**SQLGetCursorName**|지정 된 hstmt와 연결 된 커서의 이름을 반환 합니다.|  
|**SQLNumResultCols**|결과 집합 커서의 열 수를 반환 합니다.|  
|**SQLPrepare**|문을 최적화 하 고 실행 하는 방법을 계획 하 여 SQL 문을 준비 합니다. SQL 문은 **Sqlexecdirect**에 의해 실행 되도록 컴파일됩니다.<br /><br /> 테이블, 뷰 또는 필드 이름에 공백이 포함 된 경우에는 따옴표 안에 이름을 묶습니다. 예를 들어 데이터베이스에 *내 테이블* 이라는 테이블과 *my field*필드가 있는 경우 식별자의 각 요소를 다음과 같이 묶습니다.<br /><br /> 내 \`테이블\`을 선택 합니다. \`내 테이블\` 의 \`내 필드\`<br /><br /> 배열을 정식 매개 변수로 포함 하는 결과 집합을 사용 하는 방법에 대 한 자세한 내용은 [저장 프로시저에서 배열 매개 변수 반환](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)을 참조 하세요.|  
|**SQLRowCount**|Oracle에서는 마지막 행을 반입할 때까지 결과 집합의 행 수를 확인 하는 방법을 제공 하지 않으므로-1을 반환 합니다.|  
|**SQLSetCursorName**|커서 이름을 활성 문 핸들 *hstmt*와 연결 합니다.|  
|**SQLSetParam**|ODBC 2에서 SQLBindParameter로 대체 되었습니다. *x*.|  
|**SQLTransact**|연결과 관련 된 모든 문 핸들 (hstmts) 또는 환경 핸들과 연결 된 모든 연결에 대 한 모든 활성 작업 ( *henv*)에 대 한 커밋 또는 롤백 작업을 요청 합니다. 수동 모드에서 커밋이 실패할 경우 트랜잭션은 활성 상태로 유지 됩니다. 트랜잭션을 롤백하거나 커밋 작업을 다시 시도 하도록 선택할 수 있습니다. 자동 트랜잭션 모드에서 커밋 작업이 실패 하는 경우 트랜잭션은 자동으로 롤백됩니다. 트랜잭션을 비활성화할 수 없습니다.|
