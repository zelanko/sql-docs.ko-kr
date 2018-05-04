---
title: SQLGetDiagField 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39ae1a58454a7ce70f5ae2a33d951a769223fdd1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 함수(SQLGetDiagField Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetDiagField** 의 오류, 경고 및 상태 정보를 포함 하는 진단 데이터 구조 (지정된 된 핸들 연관 된) 레코드의 필드의 현재 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 진단이 필요한 핸들의 형식을 설명 하는 핸들 형식 식별자입니다. 다음 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC 라는  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   여  
  
 드라이버 관리자와 드라이버는 경우에 SQL_HANDLE_DBC_INFO_TOKEN 핸들이 사용 됩니다. 응용 프로그램에는이 핸들 형식은 사용 하지 않아야 합니다. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
 *Handle*  
 [입력] 표시 된 형식의 진단 데이터 구조에 대 한 핸들 *HandleType*합니다. 경우 *HandleType* SQL_HANDLE_ENV은 *처리* 공유 또는 비공유 환경 핸들 일 수 있습니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램 정보를 찾고 상태 레코드를 나타냅니다. 상태 레코드는 1에서 번호가 지정 됩니다. 경우는 *DiagIdentifier* 인수 진단 헤더의 모든 필드를 나타냅니다. *RecNumber* 는 무시 됩니다. 그렇지 않으면 0 이상 이어야 합니다.  
  
 *DiagIdentifier*  
 [입력] 값을 반환 하는 진단 필드를 나타냅니다. 자세한 내용은 참조는 "*DiagIdentifier* 인수" 섹션의 "설명"입니다.  
  
 *DiagInfoPtr*  
 [출력] 진단 정보를 반환 하는 버퍼에 대 한 포인터입니다. 데이터 형식 값에 따라 달라 집니다 *DiagIdentifier*합니다. 경우 *DiagInfoPtr* 는 정수 형식, 응용 프로그램 SQLULEN의 버퍼를 사용 해야 및 초기화 값을 일부 드라이버도이 함수를 호출 하기 전에 0만 있습니다 하위 32 비트 또는 16 비트는 버퍼의 작성 및 더 높은 순서를 그대로 둡니다. 비트 변경 되지 않습니다.  
  
 경우 *DiagInfoPtr* 이 NULL 이면 *StringLengthPtr* 바이트 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 여전히 가리키는버퍼에서반환할수 *DiagInfoPtr*합니다.  
  
 *BufferLength*  
 [입력] 경우 *DiagIdentifier* 은 ODBC 정의 진단 및 *DiagInfoPtr* 문자열 또는 이진 버퍼를 가리키거나,이 인수 길이 여야 \* *DiagInfoPtr* . 경우 *DiagIdentifier* 은 ODBC 정의 된 필드 및 \* *DiagInfoPtr* 정수 이면 *BufferLength* 는 무시 됩니다. 경우에 값  *\*DiagInfoPtr* 는 유니코드 문자열 (호출할 때 **SQLGetDiagFieldW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 경우 *DiagIdentifier* 드라이버에서 정의 된 필드는 응용 프로그램을 설정 하 여 드라이버 관리자에 필드의 특성을 나타내는 *BufferLength* 인수입니다. *BufferLength* 다음 값을 가질 수 있습니다.  
  
-   경우 *DiagInfoPtr* 문자 문자열에 대 한 포인터 *BufferLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   경우 *DiagInfoPtr* 이진 버퍼를 교차 하는 응용 프로그램 위치에 대 한 포인터는 SQL_LEN_BINARY_ATTR의 결과입니다 (*길이*) 매크로에서 *BufferLength*합니다. 이렇게 하면 배치에 음수 값 *BufferLength*합니다.  
  
-   경우 *DiagInfoPtr* 문자열이 나 이진 문자열 이외의 값에 대 한 포인터 *BufferLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   경우  *\*DiagInfoPtr* 고정 길이 데이터 형식이 들어 *BufferLength* SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT, 또는 SQL_IS_USMALLINT, 적절 하 게 됩니다.  
  
 *StringLengthPtr*  
 [출력] 바이트 (null 종결 문자에 필요한 바이트 수가 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *DiagInfoPtr*, 문자 데이터에 대 한 합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *BufferLength*에 있는 텍스트 \* *DiagInfoPtr* 잘립니다 *BufferLength* 빼기 null 종료 문자 길이입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_NO_DATA 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDiagField** 자체에 대 한 진단 레코드를 게시 하지 않습니다. 다음과 같은 반환 값의 자체 실행 결과 보고 하기 위해 사용 됩니다.  
  
-   SQL_SUCCESS: 함수가 진단 정보를 성공적으로 반환 했습니다.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* 너무 작아서 요청한 진단 필드를 저장할 수 있습니다. 따라서 진단 필드에 데이터가 잘렸습니다. 잘림이 발생 한, 비교 해야 응용 프로그램을 확인 하려면 *BufferLength* 에 기록 되는 데 사용할 수 있는, 바이트의 실제 수 **StringLengthPtr*합니다.  
  
-   SQL_INVALID_HANDLE: 핸들이 표시 *HandleType* 및 *처리* 유효한 핸들 없습니다.  
  
-   SQL_ERROR 다음 중 하나가 발생 했습니다.:  
  
    -   *DiagIdentifier* 인수가 유효한 값 중 하나 였습니다.  
  
    -   *DiagIdentifier* SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE, 또는 SQL_DIAG_ROW_COUNT에 인수가 있지만 *처리* 문 핸들 없습니다. (드라이버 관리자 반환이 진단 합니다.)  
  
    -   *RecNumber* 인수를 음수 또는 0 경우 *DiagIdentifier* 진단 레코드에서 필드를 표시 합니다. *RecNumber* 헤더 필드에 대해 무시 됩니다.  
  
    -   요청 된 값은 문자열 및 *BufferLength* 0 보다 작은 합니다.  
  
    -   비동기 알림을 사용 하 여, 핸들에서 비동기 작업 완료 되지 않았습니다.  
  
-   SQL_NO_DATA: *RecNumber* 에 지정 된 핸들에 대 한 존재 하는 진단 레코드 개수 보다 큰 *처리 합니다.* 함수에 대 한 임의의 양수도 SQL_NO_DATA를 반환할 *RecNumber* 에 대 한 진단 레코드가 없는 경우 *처리*합니다.  
  
## <a name="comments"></a>설명  
 응용 프로그램에서 일반적으로 호출 **SQLGetDiagField** 세 개의 목표 중 하나를 수행 하려면:  
  
1.  함수 호출 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 했습니다 때 특정 오류 또는 경고 정보를 얻으려면 (또는 대 한 SQL_NEED_DATA는 **SQLBrowseConnect** 함수).  
  
2.  데이터 원본에 삽입, 삭제 또는 업데이트 작업에 대 한 호출을 사용 하 여 수행 하는 경우 영향을 받는 행의 수를 확인 하려면 **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, 또는 **SQLSetPos** (SQL_DIAG_ROW_COUNT 헤더 필드에서), 드라이버는이 정보를 제공할 수 있는 경우 현재 열린 커서에 존재 하는 행 수를 확인 하려면 (에서 SQL_DIAG_CURSOR_ROW_COUNT 헤더 필드)입니다.  
  
3.  함수를 호출 하 여 실행을 확인 하려면 **SQLExecDirect** 또는 **SQLExecute** (에서 SQL_DIAG_DYNAMIC_FUNCTION 및 SQL_DIAG_DYNAMIC_FUNCTION_CODE 헤더 필드).  
  
 모든 ODBC 함수 게시할 수 0 개 이상의 진단 레코드 한다는 호출 될 때마다 응용 프로그램를 호출할 수 있도록 **SQLGetDiagField** ODBC 함수 호출 합니다. 한 번에 저장할 수 있는 진단 레코드의 수 제한은 없습니다. **SQLGetDiagField** 가장 최근에 구조에 연결 된 진단 데이터에 지정 된 진단 정보를 검색 된 *처리* 인수입니다. 응용 프로그램이 아닌 다른 ODBC 함수를 호출 하는 경우 **SQLGetDiagField** 또는 **SQLGetDiagRec**, 동일한 핸들을 포함 한 이전 호출에서 모든 진단 정보는 손실 됩니다.  
  
 응용 프로그램 증가 하 여 모든 진단 레코드를 검색할 수 *RecNumber*로 **SQLGetDiagField** 관계 없이 SQL_SUCCESS를 반환 합니다. 상태 레코드 수가 SQL_DIAG_NUMBER 헤더 필드에 표시 됩니다. 에 대 한 호출이 **SQLGetDiagField** 는 헤더 및 레코드 필드에 비파괴적 합니다. 응용 프로그램에서 호출할 수 **SQLGetDiagField** 진단 함수를 제외한 함수 동일한 핸들에서 레코드를 게시할 수 있는 중간에 호출 되지 않았습니다으로 레코드에서 필드를 검색 하려면 나중에 다시 합니다.  
  
 응용 프로그램에서 호출할 수 **SQLGetDiagField** 언제 든 지 SQL_DIAG_CURSOR_ROW_COUNT 또는 SQL_DIAG_ROW_COUNT 경우 SQL_ERROR를 반환 하는 제외 하 고 모든 진단 필드를 반환할 *처리* 않습니다는 문 핸들입니다. 다른 진단 필드 정의 되지 않은 경우에 대 한 호출 **SQLGetDiagField** (제공 발생 다른 진단 하지 않음)와 관계 없이 SQL_SUCCESS를 반환 합니다 필드에 대해 정의 되지 않은 값이 반환 됩니다.  
  
 자세한 내용은 참조 [를 사용 하 여 SQLGetDiagRec 및 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 및 [SQLGetDiagRec 구현 및 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)합니다.  
  
 비동기적으로 실행 되는 것과 다른 API를 호출 하면 HY010 생성 됩니다 "함수 시퀀스 오류입니다."입니다. 그러나 비동기 작업이 완료 되기 전에 오류 레코드를 검색할 수 없습니다.  
  
## <a name="handletype-argument"></a>HandleType 인수  
 각 핸들 유형에 관련 된 진단 정보를 가질 수 있습니다. *HandleType* 인수의 핸들 형식을 나타냅니다 *처리*합니다.  
  
 일부 헤더 및 레코드 필드는 핸들 환경, 연결, 문 및 설명자에 대 한 반환 수 없습니다. 다음 "헤더 필드" 및 "레코드 필드" 섹션에서 필드 적용 되지 않는 이러한 핸들이 표시 됩니다.  
  
 경우 *HandleType* SQL_HANDLE_ENV은 *처리* 공유 또는 비공유 환경 핸들 일 수 있습니다.  
  
 헤더 드라이버별 진단 필드가 없는 환경 핸들에 연결 해야 합니다.  
  
 설명자 핸들에 대해 정의 된만 진단 헤더 필드는 SQL_DIAG_NUMBER 및 SQL_DIAG_RETURNCODE입니다.  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier 인수  
 이 인수는 진단 데이터 구조에서 필요한 필드의 식별자를 나타냅니다. 경우 *RecNumber* 보다 크면 또는 1 이상이 면 필드의 데이터는 함수에서 반환 된 진단 정보를 설명 합니다. 경우 *RecNumber* 가 0 이면 필드가 헤더의 진단 데이터 구조 이며 따라서 하지 특정 정보에 진단 정보를 반환 하는 함수 호출에 관련 된 데이터를 포함 합니다.  
  
 드라이버는 진단 데이터 구조에 드라이버별 헤더 및 레코드 필드를 정의할 수 있습니다.  
  
 ODBC 3 *.x* 작업 하는 ODBC 2 응용 프로그램 *.x* 드라이버를 호출할 수 **SQLGetDiagField** 에서만 *DiagIdentifier* SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME, 또는 SQL_DIAG_SQLSTATE의 인수입니다. 다른 모든 진단 필드는 SQL_ERROR를 반환 합니다.  
  
## <a name="header-fields"></a>헤더 필드  
 다음 표에 나열 된 헤더 필드에 포함 될 수는 *DiagIdentifier* 인수입니다.  
  
|DiagIdentifier|반환 형식|반환 값|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|이 필드는 커서의 행 수를 포함 합니다. 해당 의미에 따라 달라 집니다는 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2, 및 SQL_STATIC_CURSOR_ATTRIBUTES2를 나타내는 정보 유형 행 개수는 각 커서 유형 (SQL_CA2_CRC_EXACT 및 SQL_CA2_CRC_APPROXIMATE 비트) 수 있습니다.<br /><br /> 이 필드의 내용을 정의 되므로 문 핸들에 대 한 후에 **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 가 호출 합니다. 호출 **SQLGetDiagField** 와 *DiagIdentifier* 핸들에는 문 이외의 SQL_DIAG_CURSOR_ROW_COUNT의 SQL_ERROR를 반환 합니다.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|이것이 기본 함수를 실행 하는 SQL 문을 설명 하는 문자열입니다. (특정 값에 대 한이 섹션의 뒷부분에 나오는 "동적 함수 필드의 값"을 참조 합니다.) 이 필드의 내용에 대 한 호출 후에 문 핸들에 대 한 정의 되므로 **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults**합니다. 호출 **SQLGetDiagField** 와 *DiagIdentifier* 핸들에는 문 이외의 SQL_DIAG_DYNAMIC_FUNCTION의 SQL_ERROR를 반환 합니다. 이 필드의 값에 대 한 호출 하기 전에 정의 되지 않은 **SQLExecute** 또는 **SQLExecDirect**합니다.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|이것이 기본 함수에 의해 실행 된 SQL 문에 대해 설명 하는 숫자 코드입니다. (특정 값에 대 한 값의 the 동적 함수, 필드 ""이이 섹션의 뒷부분에 나오는 참조 합니다.) 이 필드의 내용에 대 한 호출 후에 문 핸들에 대 한 정의 되므로 **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults**합니다. 호출 **SQLGetDiagField** 와 *DiagIdentifier* 핸들에는 문 이외의 SQL_DIAG_DYNAMIC_FUNCTION_CODE의 SQL_ERROR를 반환 합니다. 이 필드의 값에 대 한 호출 하기 전에 정의 되지 않은 **SQLExecute** 또는 **SQLExecDirect**합니다.|  
|SQL_DIAG_NUMBER|SQLINTEGER|지정된 된 핸들에 사용할 수 있는 상태 레코드의 수입니다.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|함수에서 반환 된 코드를 반환 합니다. 반환 코드 목록은 참조 [반환 코드](../../../odbc/reference/develop-app/return-codes-odbc.md)합니다. 드라이버는 SQL_DIAG_RETURNCODE; 구현 하지 않아도 항상 드라이버 관리자에서 구현 됩니다. 함수에 아직 호출 하는 경우는 *처리*, SQL_DIAG_RETURNCODE에 관계 없이 SQL_SUCCESS를 반환 됩니다.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|삽입, 삭제 또는 업데이트 수행의 영향을 받는 행 수가 **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos**. 드라이버에서 정의한 후에 한 *커서 사양* 실행 된 합니다. 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다. 호출 **SQLGetDiagField** 와 *DiagIdentifier* 핸들에는 문 이외의 SQL_DIAG_ROW_COUNT의 SQL_ERROR를 반환 합니다. 이 필드의 데이터에도 반환 됩니다는 *RowCountPtr* 의 인수 **SQLRowCount**합니다. 반환 된 행 수는 있지만이 필드의 데이터를 모든 nondiagnostic 함수 호출 후 다시 설정 **SQLRowCount** 문이 준비 또는 할당 된 상태로 다시 설정 될 때까지 동일 하 게 유지 합니다.|  
  
## <a name="record-fields"></a>레코드 필드  
 다음 표에 나열 된 레코드 필드에 포함 될 수는 *DiagIdentifier* 인수입니다.  
  
|DiagIdentifier|반환 형식|반환 값|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|이 레코드의 SQLSTATE 값의 클래스 부분을 정의 하는 문서를 나타내는 문자열입니다. 해당 값은 "ISO 9075"를 Open Group 및 ISO 호출 수준 인터페이스에 의해 정의 되는 모든 Sqlstate입니다. (모든 하는 것 인 SQLSTATE 클래스는 "IM")는 ODBC 관련 SQLSTATEs, 해당 값은 "ODBC 3.0" 입니다.|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|SQL_DIAG_ROW_NUMBER 필드가 행 집합 또는 매개 변수 집합에서 유효한 행 수 인 경우이 필드는 매개 변수 집합에 있는 매개 변수 번호 또는 결과 집합의 열 번호를 나타내는 값을 포함 합니다. 결과 집합 열 번호는 항상 1;에서 시작 이 상태 레코드와 관련 된 책갈피 열을 경우 필드에는 0 일 수 있습니다. 매개 변수 번호는 1부터 시작 합니다. 상태 레코드 열 번호 또는 매개 변수 번호와 연결 되지 않은 경우에 SQL_NO_COLUMN_NUMBER 값을 갖습니다. 드라이버는 열 번호 또는이 레코드와 연결 된 매개 변수 번호를 확인할 수 없는 경우이 필드는 SQL_COLUMN_NUMBER_UNKNOWN 값을 갖습니다.<br /><br /> 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|진단 레코드와 관련 된 연결의 이름을 나타내는 문자열입니다. 이 필드는 드라이버 정의입니다. 환경 핸들에 연결 된 진단 데이터 구조에 대 한 모든 연결 하는 진단에 대 한이 필드는 길이가 0 인 문자열입니다.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|오류 또는 경고에 정보 메시지입니다. 이 필드는에 설명 된 대로 서식이 지정 [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)합니다. 진단 메시지 텍스트에 최대 길이가 없음이 있습니다.|  
|SQL_DIAG_NATIVE|SQLINTEGER|드라이버/데이터 원본에 따른 특정 원시 오류 코드입니다. 원시 오류 코드가 없는 경우 드라이버는 0을 반환 합니다.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|이 필드는 행 집합의 행 번호 또는 상태 레코드와 관련 된 매개 변수 집합에 매개 변수 번호를 포함 합니다. 행 번호 및 매개 변수 번호는 1부터 시작 합니다. 이 상태 레코드 행 번호 또는 매개 변수 번호와 연결 되지 않은 경우이 필드에 SQL_NO_ROW_NUMBER 값으로 지정 합니다. 드라이버는 행 번호 또는이 레코드와 연결 된 매개 변수 번호를 확인할 수 없는 경우이 필드는 SQL_ROW_NUMBER_UNKNOWN 값을 갖습니다.<br /><br /> 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|진단 레코드와 관련 된 서버 이름을 나타내는 문자열입니다. 에 대 한 호출에 대 한 반환 값과 동일 **SQLGetInfo** SQL_DATA_SOURCE_NAME 옵션을 사용 합니다. 환경 핸들에 연결 된 진단 데이터 구조 및 모든 서버에 관련 되지 않아 진단에 대 한이 필드는 길이가 0 인 문자열입니다.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|5 자의 SQLSTATE 진단 코드입니다. 자세한 내용은 참조 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)합니다.|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|SQLSTATE 코드의 하위 클래스 부분 정의 부분을 식별 하는 SQL_DIAG_CLASS_ORIGIN으로 같은 형식 및 유효한 값을 가진 문자열입니다. "ODBC 3.0" 반환 되는 관련 ODBC SQLSTATE는 다음과 같습니다.<br /><br /> 01S00, 01S01, 01 S 02, 01S06, 01S07, 07S01, 08 S 01 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012 합니다.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>동적 함수 필드의 값  
 다음 표에서 설명를 호출 하 여 실행 하는 SQL 문의 각 형식에 적용 되는 값 SQL_DIAG_DYNAMIC_FUNCTION 및 SQL_DIAG_DYNAMIC_FUNCTION_CODE **SQLExecute** 또는 **SQLExecDirect**. 드라이버에 나열 된 드라이버에서 정의 된 값을 추가할 수 있습니다.  
  
|SQL 문<br /><br /> 실행|값<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|값<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter 도메인-문*|"ALTER 도메인"|SQL_DIAG_ALTER_DOMAIN|  
|*변경 테이블-문*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*어설션이 정의*|"어설션 만들기"|SQL_DIAG_CREATE_ASSERTION|  
|*문자 집합 정의*|"문자 집합 만들기"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*데이터 정렬 정의*|"데이터 정렬 만들기"|SQL_DIAG_CREATE_COLLATION|  
|*인덱스 생성-문*|"CREATE INDEX"|SQL_DIAG_CREATE_INDEX|  
|*테이블 생성-문*|"테이블 만들기"|SQL_DIAG_CREATE_TABLE|  
|*뷰 생성-문*|"뷰 만들기"|SQL_DIAG_CREATE_VIEW|  
|*커서 사양이*|"커서 선택"|SQL_DIAG_SELECT_CURSOR|  
|*delete 문을 배치*|"동적 삭제 커서"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete 문은 검색*|"삭제 위치"|SQL_DIAG_DELETE_WHERE|  
n-정의 *|"도메인 만들기"|SQL_DIAG_CREATE_DOMAIN|  
|*drop 어설션 문*|"DROP ASSERTION"|SQL_DIAG_DROP_ASSERTION|  
|*문자 집합 stmt 놓기*|"DROP 문자 집합"|SQL_DIAG_DROP_CHARACTER_SET|  
|*드롭-데이터 정렬-문*|"DROP 데이터 정렬"|SQL_DIAG_DROP_COLLATION|  
|*drop 도메인 문*|"DROP 도메인"|SQL_DIAG_DROP_DOMAIN|  
|*drop index 문*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop 스키마 문*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*drop 테이블 문*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*drop 번역 문*|"DROP 번역"|SQL_DIAG_DROP_TRANSLATION|  
|*drop view 문*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
-문을 *|"GRANT"|SQL_DIAG_GRANT|  
|*insert 문*|"삽입"|SQL_DIAG_INSERT|  
|*ODBC 프로시저 확장*|"호출"|SQL_DIAG_ 호출|  
|*revoke 문*|"REVOKE"|SQL_DIAG_REVOKE|  
|*스키마 정의*|"스키마 만들기"|SQL_DIAG_CREATE_SCHEMA|  
|*번역 정의*|"번역을 작성 합니다."|SQL_DIAG_CREATE_TRANSLATION|  
|*update 문을 배치*|"동적 업데이트 커서"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update 문을 검색*|"업데이트" WHERE "|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*빈 문자열*|SQL_DIAG_UNKNOWN_STATEMENT|  
  
## <a name="sequence-of-status-records"></a>상태 레코드의 시퀀스  
 행 번호 및 진단의 종류에 따라 시퀀스의 상태 레코드에 배치 됩니다. 드라이버 관리자를 생성 하는 상태 레코드를 반환 하는 최종 순서를 결정 합니다. 드라이버를 생성 하는 상태 레코드를 반환 하는 최종 순서를 결정 합니다.  
  
 드라이버 관리자와 드라이버 진단 레코드는 게시 하는 경우 드라이버 관리자는 순서를 지정 하는 일을 담당 합니다.  
  
 상태 레코드 두 개 이상의 인 레코드의 시퀀스 행 번호에 의해 먼저 결정 됩니다. 행으로 진단 레코드의 시퀀스를 결정 하는 데 다음 규칙이 적용 됩니다.  
  
-   모든 행에 해당 하지 않는 레코드를 – 1 SQL_NO_ROW_NUMBER 정의 되었기 때문에 특정 행에 해당 하는 레코드 앞에 나타납니다.  
  
-   레코드는에 대 한 행 번호는 알려진 SQL_ROW_NUMBER_UNKNOWN – 2 되도록 정의 되어 있으므로 다른 모든 레코드 앞에 나타납니다.  
  
-   특정 행에 관련 된 모든 레코드에 대 한 레코드가 SQL_DIAG_ROW_NUMBER 필드에 값으로 정렬 됩니다. 모든 오류 및 영향을 받는 첫 번째 행의 경고 나열 되 고 모든 오류 및 경고는 다음의 행이 영향을 받는, 고 까지입니다.  
  
> [!NOTE]  
>  ODBC 3 *.x* 드라이버 관리자 정렬 되지 않은 상태 레코드 진단 큐에 있는 경우 SQLSTATE 01S01 (행에서 오류)는 ODBC 2가 반환한 *.x* 드라이버 경우 SQLSTATE 01S01는 ODBC에서 반환 (행에서 오류) 3 *.x* 드라이버 때 **SQLExtendedFetch** 라고 또는 **SQLSetPos** 으로 배치 된 하는 커서에 라고 **SQLExtendedFetch** .  
  
 각 행 내에서 또는 또는 행에 있는 행 번호 알 수 없는, 해당 하지 않는 모든 레코드에 대 한 SQL_NO_ROW_NUMBER 같은 행 번호를 가진 이러한 모든 레코드를 나열 된 첫 번째 레코드 집합 정렬 규칙을 사용 하 여 결정 됩니다. 첫 번째 레코드를 다음 행에 영향을 주는 다른 레코드의 순서 정의 되지 않습니다. 응용 프로그램 오류 경고를 앞에 첫 번째 레코드 후 가정할 수 없습니다. 응용 프로그램 완전 한 진단 데이터 구조는 함수에 대 한 실패 한 호출에 대 한 전체 정보를 검색 해야 합니다.  
  
 다음 규칙은 행 내에서 첫 번째 레코드를 결정 하는 데 사용 됩니다. 가장 높은 순위 인 레코드는 첫 번째 레코드입니다. 레코드 (드라이버 관리자, 드라이버, 게이트웨이 및 등)의 소스 간주 되지 않습니다 레코드의 순위를 지정 합니다.  
  
-   **오류** 오류를 설명 하는 상태 레코드 가장 높은 순위를 가져야 합니다. 오류를 정렬 하는 다음 규칙이 적용 됩니다.  
  
    -   트랜잭션 오류 또는 가능한 트랜잭션 오류를 나타내는 레코드 outrank 다른 모든 레코드입니다.  
  
    -   둘 이상의 레코드가 동일한 오류 조건을 설명 하는 경우 Open 그룹 CLI 사양 (03 HZ 통해 클래스)에 정의 된 Sqlstate outrank SQLSTATEs ODBC 및 드라이버 정의 합니다.  
  
-   **구현에서 정의 된 데이터 값을 No** 드라이버 정의 된 데이터 없음 값 (클래스 02)를 설명 하는 상태 레코드에는 두 번째는 높은 순위입니다.  
  
-   **경고** 상태 레코드 (클래스 01) 경고를 설명 하는 가장 낮은 순위입니다. 둘 이상의 레코드가 동일한 경고 조건을 SQLSTATEs Open 그룹 CLI 사양에 정의 된 경고에 대해 설명 하는 경우에 ODBC 정의 하 고 드라이버에서 정의 된 Sqlstate outrank 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|진단 데이터 구조의 여러 필드 가져오기|[SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
