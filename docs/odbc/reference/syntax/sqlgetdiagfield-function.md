---
title: SQLGetDiagField 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f975b15d07bf837c0f5fe5d2649cc78b341d23c6
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420168"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 함수(SQLGetDiagField Function)

**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetDiagField** 오류, 경고 및 상태 정보가 포함 된 진단 데이터 구조 (지정된 된 핸들을 사용 하 여 연결 된) 레코드의 필드의 현재 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
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
 [입력] 진단이 필요 하는 핸들의 형식을 설명 하는 핸들 형식 식별자입니다. 다음 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 드라이버 관리자 및 드라이버에 의해서만 SQL_HANDLE_DBC_INFO_TOKEN 핸들을 사용 합니다. 응용 프로그램에는이 핸들 형식은 사용 하지 마십시오. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 하세요. [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
 *Handle*  
 [입력] 지정 된 형식의 진단 데이터 구조에 대 한 핸들 *HandleType*합니다. 하는 경우 *HandleType* SQL_HANDLE_ENV, 됩니다 *처리* 공유 또는 비공유 환경 핸들 일 수 있습니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램 정보를 검색 하는 상태 레코드를 나타냅니다. 상태 레코드는 1부터 번호가 지정 됩니다. 경우는 *DiagIdentifier* 인수는 진단 헤더의 모든 필드를 나타냅니다 *RecNumber* 무시 됩니다. 그렇지 않은 경우 0 보다 여야 합니다.  
  
 *DiagIdentifier*  
 [입력] 반환 되는 값인 진단 필드를 나타냅니다. 자세한 내용은 참조는 "*DiagIdentifier* 인수" 섹션에서 "설명"입니다.  
  
 *DiagInfoPtr*  
 [출력] 진단 정보를 반환 하는 버퍼에 대 한 포인터입니다. 데이터 형식 값에 따라 달라 집니다 *DiagIdentifier*합니다. 하는 경우 *DiagInfoPtr* 정수 형식이, SQLULEN 버퍼를 사용 하는 응용 프로그램 및 초기화를 일부 드라이버를이 함수를 호출 하기 전에 0 값만 될 수 있습니다 하위 32 비트 또는 16 비트는 버퍼의 쓰기 더 높은 순서 유지 비트 변경 되지 않습니다.  
  
 하는 경우 *DiagInfoPtr* 가 null 인 경우 *StringLengthPtr* 총 바이트 (문자 데이터에 대 한 null 종료 문자 제외)도 돌아갑니다 가리키는버퍼에서반환할사용가능한 *DiagInfoPtr*합니다.  
  
 *BufferLength*  
 [입력] 경우 *DiagIdentifier* 은 ODBC 정의 진단 하 고 *DiagInfoPtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 \* *DiagInfoPtr* . 경우 *DiagIdentifier* 은 ODBC 정의 된 필드와 \* *DiagInfoPtr* 정수 이면 *BufferLength* 무시 됩니다. 경우 값  *\*DiagInfoPtr* 는 유니코드 문자열 (호출할 때 **SQLGetDiagFieldW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 하는 경우 *DiagIdentifier* 드라이버에서 정의 된 필드는 응용 프로그램을 설정 하 여 드라이버 관리자에 필드의 특성을 나타내는 합니다 *BufferLength* 인수. *BufferLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우 *DiagInfoPtr* 문자열로 포인터가 *BufferLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   하는 경우 *DiagInfoPtr* 결과인 이진 버퍼는 응용 프로그램 위치에 대 한 포인터를 SQL_LEN_BINARY_ATTR (*길이*)에서 매크로 *BufferLength*합니다. 에 음수 값이 배치 *BufferLength*합니다.  
  
-   하는 경우 *DiagInfoPtr* 문자열 또는 이진 문자열 이외의 값에 대 한 포인터 *BufferLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우  *\*DiagInfoPtr* 고정 길이 데이터 형식을 포함 *BufferLength* 인지 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT, SQL_IS_USMALLINT를 적절 하 게 합니다.  
  
 *StringLengthPtr*  
 [출력] 바이트 (null 종료 문자에 필요한 바이트 수가 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *DiagInfoPtr*, 문자 데이터에 대 한 합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *BufferLength*에 있는 텍스트 \* *DiagInfoPtr* 잘립니다 *BufferLength* 빼기 null 종료 문자 길이입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_NO_DATA 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDiagField** 자체에 대 한 진단 레코드를 게시 하지 않습니다. 자체 실행의 결과 보고 하는 다음 반환 값을 사용 합니다.  
  
-   SQL_SUCCESS: 함수는 진단 정보를 반환 했습니다.  
  
-   SQL_SUCCESS_WITH_INFO: \**DiagInfoPtr* 가 너무 작아서 요청 된 진단 필드를 저장할 수 있습니다. 따라서 진단 필드에 데이터가 잘렸습니다. 잘림이 발생을 응용 프로그램을 비교 해야 결정할 *BufferLength* 에 기록 되는 사용 가능한 바이트의 실제 수 **StringLengthPtr*합니다.  
  
-   SQL_INVALID_HANDLE: 핸들에 나타난 *HandleType* 하 고 *처리* 는 유효한 핸들이 없습니다.  
  
-   SQL_ERROR: 다음 중 하나에 다음이 발생 했습니다.  
  
    -   *DiagIdentifier* 인수가 유효한 값 중 하나 였습니다.  
  
    -   *DiagIdentifier* 인수가 SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE, 또는 SQL_DIAG_ROW_COUNT, 하지만 *처리* 문 핸들 없습니다. (드라이버 관리자 반환이 진단 합니다.)  
  
    -   *RecNumber* 인수가 음수 또는 0 인 경우 *DiagIdentifier* 진단 레코드에서 필드를 표시 합니다. *RecNumber* 헤더 필드에 대해 무시 됩니다.  
  
    -   요청 된 값이 문자열 및 *BufferLength* 가 0 보다 작습니다.  
  
    -   비동기 알림을 사용 하는 경우 핸들에 대해 비동기 작업이 완료 되지 않았습니다.  
  
-   SQL_NO_DATA: *RecNumber* 에 지정 된 핸들에 대해 존재 하는 진단 레코드 개수 보다 *처리 합니다.* 또한 함수 모든 양수 SQL_NO_DATA를 반환할 *RecNumber* 에 대 한 진단 레코드가 없는 경우 *처리*합니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 일반적으로 호출 **SQLGetDiagField** 세 가지 목표 중 하나를 수행 하려면:  
  
1.  SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 함수 호출에 반환 될 때 특정 오류 또는 경고 정보를 가져오려면 (에 대 한 SQL_NEED_DATA 또는 합니다 **SQLBrowseConnect** 함수).  
  
2.  데이터 소스에서 삽입, 삭제 또는 업데이트 작업에 대 한 호출을 사용 하 여 수행 하는 경우 영향을 받는 행의 수를 확인 하려면 **SQLExecute**하십시오 **SQLExecDirect**,  **SQLBulkOperations**, 또는 **SQLSetPos** (SQL_DIAG_ROW_COUNT 헤더 필드에서), 또는 드라이버는이 정보를 제공할 수 있으면 현재 열린 커서에 존재 하는 행의 수를 확인 하려면 (에서 SQL_DIAG_CURSOR_ROW_COUNT 헤더 필드)입니다.  
  
3.  함수를 호출 하 여 실행 된 결정할 **SQLExecDirect** 또는 **SQLExecute** (에서 SQL_DIAG_DYNAMIC_FUNCTION 및 SQL_DIAG_DYNAMIC_FUNCTION_CODE 헤더 필드).  
  
 모든 ODBC 함수를 게시할 수 0 개 이상의 진단 레코드는 호출 될 때마다 응용 프로그램에서 호출할 수 있도록 **SQLGetDiagField** ODBC 함수를 호출 합니다. 한 번에 저장할 수 있는 진단 레코드의 수 제한은 없습니다. **SQLGetDiagField** 에 지정 된 진단 데이터 구조를 사용 하 여 가장 최근에 연결 된 진단 정보를 검색 합니다 *처리* 인수입니다. 응용 프로그램이 아닌 다른 ODBC 함수를 호출 하는 경우 **SQLGetDiagField** 하거나 **SQLGetDiagRec**, 동일한 핸들을 포함 한 이전 호출에서 모든 진단 정보는 손실 됩니다.  
  
 응용 프로그램 증가 시켜 모든 진단 레코드를 검색할 수 있습니다 *RecNumber*으로 **SQLGetDiagField** 관계 없이 SQL_SUCCESS를 반환 합니다. 상태 레코드 수가 SQL_DIAG_NUMBER 헤더 필드에 표시 됩니다. 에 대 한 호출 **SQLGetDiagField** 헤더 및 레코드 필드에 비 소멸 됩니다. 응용 프로그램에서 호출할 수 있습니다 **SQLGetDiagField** 동일한 핸들에 대해 레코드 게시는 그동안에서 진단 함수 이외의 함수 호출 되지 않았습니다으로 a 레코드에서 필드를 검색 하려면 나중에 다시 합니다.  
  
 응용 프로그램에서 호출할 수 있습니다 **SQLGetDiagField** 언제 든 지 SQL_DIAG_CURSOR_ROW_COUNT 또는 SQL_DIAG_ROW_COUNT 경우 SQL_ERROR를 반환 하는 제외 하 고 모든 진단 필드를 반환할 *처리* 아닙니다를 문 핸들입니다. 다른 진단 필드에 정의 된 경우에 대 한 호출 **SQLGetDiagField** (제공 없는 다른 진단 발생)와 관계 없이 SQL_SUCCESS를 반환 합니다 정의 되지 않은 값을 필드에 대해 반환 됩니다.  
  
 자세한 내용은 [를 사용 하 여 SQLGetDiagRec 및 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 하 고 [구현 SQLGetDiagRec 및 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)합니다.  
  
 비동기적으로 실행 되는 것과 다른 API를 호출할 HY010 생성 "함수 시퀀스 오류입니다."입니다. 그러나 비동기 작업이 완료 되기 전에 오류 레코드를 검색할 수 없습니다.  
  
## <a name="handletype-argument"></a>HandleType 인수  
 각 핸들 형식은 연결 된 진단 정보를 가질 수 있습니다. *HandleType* 인수는 핸들 형식의 나타냅니다 *처리*합니다.  
  
 일부 헤더 및 레코드 필드는 핸들 환경, 연결, 문 및 설명자에 대 한 반환 수 없습니다. 다음 섹션에서는 "헤더 필드" 및 "레코드 필드" 필드를 적용 하지는 이러한 핸들이 표시 됩니다.  
  
 하는 경우 *HandleType* SQL_HANDLE_ENV, 됩니다 *처리* 공유 또는 비공유 환경 핸들 일 수 있습니다.  
  
 드라이버별 헤더 진단 필드가 없는 환경 핸들을 사용 하 여 연결 해야 합니다.  
  
 설명자 핸들에 대해 정의 된만 진단 헤더 필드는 SQL_DIAG_NUMBER 및 SQL_DIAG_RETURNCODE입니다.  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier 인수  
 이 인수는 진단 데이터 구조에서 필요한 필드의 식별자를 나타냅니다. 하는 경우 *RecNumber* 보다 크면 또는 1과 같으면 필드의 데이터 함수에서 반환 하는 진단 정보를 설명 합니다. 하는 경우 *RecNumber* 가 0 이면 필드 헤더의 진단 데이터 구조 이며 따라서 진단 정보를 특정 정보를 반환 하는 함수 호출에 관련 된 데이터를 포함 합니다.  
  
 드라이버는 진단 데이터 구조의 드라이버별 헤더 및 레코드 필드를 정의할 수 있습니다.  
  
 ODBC 3 *.x* 는 ODBC 2를 사용 하는 응용 프로그램 *.x* 드라이버를 호출할 수 있게 됩니다 **SQLGetDiagField** 만 *DiagIdentifier* SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME, 또는 SQL_DIAG_SQLSTATE 인수입니다. 다른 모든 진단 필드에서 SQL_ERROR를 반환 합니다.  
  
## <a name="header-fields"></a>헤더 필드  
 다음 표에 나열 된 헤더 필드에 포함할 수는 *DiagIdentifier* 인수입니다.  
  
|DiagIdentifier|반환 형식|반환 값|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|이 필드에는 커서의 행 수가 포함 되어 있습니다. 해당 의미 체계에 따라 달라 집니다 합니다 **SQLGetInfo** 정보 형식이 SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2, 및 SQL_STATIC_CURSOR_ATTRIBUTES2는 나타내는 행 개수 (SQL_CA2_CRC_EXACT 및 SQL_CA2_CRC_APPROXIMATE 비트)에 각 커서 유형에 대해 사용할 수 있습니다.<br /><br /> 문 핸들에 대해서만 및 설정한 후에이 필드의 내용을 정의 된 **SQLExecute**를 **SQLExecDirect**, 또는 **SQLMoreResults** 가 호출 되었습니다. 호출 **SQLGetDiagField** 사용 하 여를 *DiagIdentifier* 문 외에 SQL_DIAG_CURSOR_ROW_COUNT의 핸들에서 SQL_ERROR를 반환 합니다.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|기본 함수를 실행 하는 SQL 문을 설명 하는 문자열입니다. (특정 값에 대 한이 섹션의 뒷부분에 나오는 "동적 함수 필드의 값"을 참조 하세요.) 이 필드의 콘텐츠를 호출한 후에 문 핸들에 대해서만 정의 되므로 **SQLExecute**를 **SQLExecDirect**, 또는 **SQLMoreResults**합니다. 호출 **SQLGetDiagField** 사용 하 여를 *DiagIdentifier* 문 외에 SQL_DIAG_DYNAMIC_FUNCTION의 핸들에서 SQL_ERROR를 반환 합니다. 이 필드의 값을 호출 하기 전에 정의 되지 않은 **SQLExecute** 하거나 **SQLExecDirect**합니다.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|기본 함수에 의해 실행 된 SQL 문에 대해 설명 하는 숫자 코드입니다. (참조 "값은 동적 함수 필드의,"이이 섹션의 뒷부분에 특정 값에 대 한). 이 필드의 콘텐츠를 호출한 후에 문 핸들에 대해서만 정의 되므로 **SQLExecute**를 **SQLExecDirect**, 또는 **SQLMoreResults**합니다. 호출 **SQLGetDiagField** 사용 하 여를 *DiagIdentifier* 문 외에 SQL_DIAG_DYNAMIC_FUNCTION_CODE의 핸들에서 SQL_ERROR를 반환 합니다. 이 필드의 값을 호출 하기 전에 정의 되지 않은 **SQLExecute** 하거나 **SQLExecDirect**합니다.|  
|SQL_DIAG_NUMBER|SQLINTEGER|지정된 된 핸들에 사용할 수 있는 상태 레코드의 수입니다.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|함수에서 반환 하는 코드를 반환 합니다. 반환 코드의 목록에 대해서 [반환 코드](../../../odbc/reference/develop-app/return-codes-odbc.md)합니다. 드라이버는 SQL_DIAG_RETURNCODE; 구현할 필요가 없습니다. 항상 드라이버 관리자에 의해 구현 됩니다. 함수가 아직에서 호출한 경우는 *처리*, SQL_DIAG_RETURNCODE에 대 한 관계 없이 SQL_SUCCESS를 반환 됩니다.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|Insert, delete 또는 update 수행한 영향을 받는 행 수가 **SQLExecute**, **SQLExecDirect**하십시오 **SQLBulkOperations**, 또는 **SQLSetPos**. 후 드라이버에서 정의 된 것을 *커서 사양이* 실행 되었습니다. 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다. 호출 **SQLGetDiagField** 사용 하 여를 *DiagIdentifier* 문 외에 SQL_DIAG_ROW_COUNT의 핸들에서 SQL_ERROR를 반환 합니다. 이 필드의 데이터에도 반환 되는 *RowCountPtr* 인수의 **SQLRowCount**합니다. 행 개수를 반환 하는 반면 모든 nondiagnostic 함수 호출 후이 필드의에서 데이터를 다시 설정 됩니다 **SQLRowCount** 문을 준비 또는 할당 된 상태로 다시 설정 될 때까지 동일 하 게 유지 합니다.|  
  
## <a name="record-fields"></a>레코드 필드  
 다음 표에 나열 된 레코드 필드에 포함할 수는 *DiagIdentifier* 인수입니다.  
  
|DiagIdentifier|반환 형식|반환 값|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|이 레코드의 SQLSTATE 값 클래스 부분을 정의 하는 문서를 나타내는 문자열입니다. 해당 값은 Open Group 및 ISO 호출 수준 인터페이스를 정의한 모든 SQLSTATEs "ISO 9075"입니다. (모든 원하는 언어로 된 SQLSTATE 클래스 "IM") ODBC 별 SQLSTATEs, 해당 값은 "ODBC 3.0" 입니다.|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|SQL_DIAG_ROW_NUMBER 필드를 행 집합 또는 매개 변수 집합이 유효한 행 숫자 이면이 필드는 매개 변수 집합에 있는 매개 변수 번호 또는 결과 집합의 열 번호를 나타내는 값을 포함 합니다. 결과 집합 열 번호는 항상 1부터 시작 이 상태 레코드 책갈피 열에 포함 하는 경우 필드는 0 일 수 있습니다. 매개 변수 번호는 1부터 시작 합니다. 상태 레코드 열 번호 또는 매개 변수 번호를 사용 하 여 연결 되지 않은 경우 값 SQL_NO_COLUMN_NUMBER이 있습니다. 드라이버는 열 개수나이 레코드와 연결 된 매개 변수 번호를 확인할 수 없는 경우이 필드 SQL_COLUMN_NUMBER_UNKNOWN 값이 있습니다.<br /><br /> 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|진단 레코드에 연결 하는 연결의 이름을 나타내는 문자열입니다. 이 필드는 드라이버 정의 됩니다. 환경 핸들에 연결 된 진단 데이터 구조 및 모든 연결에 관련 되지 않아 진단이이 필드는 길이가 0 인 문자열입니다.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|오류 또는 경고에 사용 되는 정보 메시지입니다. 이 필드에 설명 된 대로 형식이 [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)합니다. 진단 메시지 텍스트에 최대 길이가 없습니다.|  
|SQL_DIAG_NATIVE|SQLINTEGER|드라이버/데이터 소스 관련 원시 오류 코드입니다. 원시 오류 코드가 없는 경우 드라이버는 0을 반환 합니다.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|이 필드는 상태 레코드와 연관 된 매개 변수 집합에 있는 매개 변수 번호 또는 행 집합의 행 번호를 포함 합니다. 행 번호 및 매개 변수 번호는 1부터 시작 합니다. 이 상태 레코드 매개 변수 개수나 행 번호를 사용 하 여 연결 되지 않은 경우이 필드 SQL_NO_ROW_NUMBER 값이 있습니다. 드라이버는 행 수 또는이 레코드와 연결 된 매개 변수 번호를 확인할 수 없는 경우이 필드 SQL_ROW_NUMBER_UNKNOWN 값이 있습니다.<br /><br /> 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|진단 레코드에 연결 하는 서버 이름을 나타내는 문자열입니다. 에 대 한 호출에 대 한 반환 값으로 동일 **SQLGetInfo** SQL_DATA_SOURCE_NAME 옵션을 사용 합니다. 환경 핸들에 연결 된 진단 데이터 구조 및 모든 서버에 관련 되지 않아 진단이이 필드는 길이가 0 인 문자열입니다.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|5 자의 SQLSTATE 진단 코드입니다. 자세한 내용은 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)합니다.|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|SQLSTATE 코드의 하위 클래스 부분 정의 부분을 식별 하는 SQL_DIAG_CLASS_ORIGIN으로 동일한 형식 및 유효한 값을 사용 하 여 문자열입니다. "ODBC 3.0" 반환 되는 특정 ODBC SQLSTATE는 다음과 같습니다.<br /><br /> 01S00, 01S01, 01S02, 01S06, 01S07, 07S01, 08S01 21S01, 21S02, 25S01 잘림, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007 IM008, IM010, IM011, IM012 합니다.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>동적 함수 필드 값  
 다음 표에서를 호출 하 여 실행 된 SQL 문의 각 형식에 적용 되는 값을 SQL_DIAG_DYNAMIC_FUNCTION 및 SQL_DIAG_DYNAMIC_FUNCTION_CODE **SQLExecute** 또는 **SQLExecDirect**. 드라이버에 나오는 드라이버에서 정의 된 값을 추가할 수 있습니다.  
  
|SQL 문<br /><br /> 실행|값<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|값<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain-statement*|"ALTER 도메인"|SQL_DIAG_ALTER_DOMAIN|  
|*alter-table-statement*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*assertion-definition*|"어설션을 만들지"|SQL_DIAG_CREATE_ASSERTION|  
|*character-set-definition*|"문자 집합 만들기"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*collation-definition*|"데이터 정렬 만들기"|SQL_DIAG_CREATE_COLLATION|  
|*domainn-definition*|"도메인 만들기"|SQL_DIAG_CREATE_DOMAIN|
|*create-index-statement*|"인덱스 만들기"|SQL_DIAG_CREATE_INDEX|  
|*create-table-statement*|"테이블 만들기"|SQL_DIAG_CREATE_TABLE|  
|*create-view-statement*|"뷰 만들기"|SQL_DIAG_CREATE_VIEW|  
|*cursor-specification*|"커서 선택"|SQL_DIAG_SELECT_CURSOR|  
|*delete-statement-positioned*|"동적 삭제 커서"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete-statement-searched*|"WHERE 삭제"|SQL_DIAG_DELETE_WHERE|  
|*drop-assertion-statement*|"DROP 어설션"|SQL_DIAG_DROP_ASSERTION|  
|*drop-character-set-stmt*|"DROP 문자 집합"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-collation-statement*|"DROP 데이터 정렬"|SQL_DIAG_DROP_COLLATION|  
|*drop-domain-statement*|"DROP 도메인"|SQL_DIAG_DROP_DOMAIN|  
|*drop-index-statement*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop-schema-statement*|"삭제 스키마"|SQL_DIAG_DROP_SCHEMA|  
|*drop-table-statement*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*drop-translation-statement*|"DROP 변환"|SQL_DIAG_DROP_TRANSLATION|  
|*drop-view-statement*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|"권한 부여"|SQL_DIAG_GRANT|
|*insert-statement*|"INSERT"|SQL_DIAG_INSERT|  
|*ODBC-procedure-extension*|"CALL"|SQL_DIAG_ CALL|  
|*revoke-statement*|"REVOKE"|SQL_DIAG_REVOKE|  
|*schema-definition*|"스키마 만들기"|SQL_DIAG_CREATE_SCHEMA|  
|*translation-definition*|"번역을 작성 합니다."|SQL_DIAG_CREATE_TRANSLATION|  
|*update-statement-positioned*|"동적 업데이트 커서"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update-statement-searched*|"WHERE 업데이트"|SQL_DIAG_UPDATE_WHERE|  
|알 수 없음|*빈 문자열*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  
|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  
|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|
-->

## <a name="sequence-of-status-records"></a>상태 레코드의 시퀀스

 상태 레코드에 행 번호 및 진단의 형식을 기반으로 하는 순서로 배치 됩니다. 드라이버 관리자를 생성 하는 상태 레코드를 반환 하는 최종 순서를 결정 합니다. 드라이버 생성 하는 상태 레코드를 반환 하는 최종 순서를 결정 합니다.  
  
 진단 레코드 드라이버 관리자와 드라이버에서 게시 되는 경우 드라이버 관리자는 순서를 지정 하는 일을 담당 합니다.  
  
 두 개 이상의 상태 레코드의 경우이 레코드의 시퀀스는 먼저 행 번호로 결정 됩니다. 행으로 진단 레코드의 시퀀스를 결정 하는 다음 규칙이 적용 됩니다.  
  
-   모든 행에 해당 하지 않는 레코드 SQL_NO_ROW_NUMBER-1로 정의 되어 있으므로 특정 행에 해당 하는 레코드 앞에 표시 합니다.  
  
-   에 대 한 행 번호를 알 수 없는 레코드 SQL_ROW_NUMBER_UNKNOWN-2 되도록 정의 되어 있으므로 다른 모든 레코드를 앞에 표시 합니다.  
  
-   특정 행에 관련 된 모든 레코드에 대 한 레코드 SQL_DIAG_ROW_NUMBER 필드의 값으로 정렬 됩니다. 나열 된 모든 오류 및 경고의 영향을 받는 첫 번째 행과 모든 오류 및 경고는 다음의 영향을 받지 등에 행 하는 다음.  
  
> [!NOTE]
>  ODBC 3 *.x* 드라이버 관리자 정렬 되지 않은 상태 레코드 진단 큐의 경우 SQLSTATE 01S01는 ODBC 2 (행의 오류)가 반환한 *.x* 드라이버 경우 SQLSTATE 01S01 ODBC 반환한 (행의 오류) 3 *.x* 드라이버 때 **SQLExtendedFetch** 라고 하거나 **SQLSetPos** 사용 하 여 배치 하는 커서에 라고 **SQLExtendedFetch** .  
  
 각 행 내에서 또는 해당 하는 행 번호를 알 수 없는, 또는 행에 해당 하지 않는 모든 레코드에 대 한 SQL_NO_ROW_NUMBER 같음 행 번호를 포함 하는 모든 레코드에 대 한, 나열 된 첫 번째 레코드 집합을 정렬 규칙을 사용 하 여 결정 됩니다. 첫 번째 레코드를 다음 행에 영향을 주는 다른 레코드의 순서가 정의 되지 않습니다. 응용 프로그램 오류 경고를 앞에 첫 번째 레코드 후 한다는 가정할 수 없습니다. 응용 프로그램에는 전체 진단 데이터 구조 함수에 대 한 실패 한 호출에 대 한 전체 정보를 검색 해야 합니다.  
  
 다음 규칙은 한 행 내에서 첫 번째 레코드를 결정 하는 데 사용 됩니다. 가장 높은 순위를 사용 하 여 레코드는 첫 번째 레코드입니다. 원본 레코드 (드라이버 관리자, 드라이버, 게이트웨이 및 등)의 간주 되지 않습니다 레코드 순위를 지정 합니다.  
  
-   **오류** 오류를 설명 하는 상태 레코드 가장 높은 순위를 가집니다. 오류를 정렬 하려면 다음과 같은 규칙이 적용 됩니다.  
  
    -   트랜잭션 오류 또는 가능한 트랜잭션 오류를 나타내는 레코드 outrank 다른 모든 레코드입니다.  
  
    -   둘 이상의 레코드가 동일한 오류 조건이 설명 하는 경우 (HZ 클래스 03) 열기 그룹 CLI 사양에 정의 된 Sqlstate outrank ODBC 및 드라이버에서 정의 된 Sqlstate입니다.  
  
-   **구현 시 정의 된 데이터 값 없음** 드라이버에서 정의 된 데이터가 없는 값 (클래스 02)을 설명 하는 상태 레코드에는 두 번째가 가장 높은 순위입니다.  
  
-   **경고** (클래스 01) 경고를 설명 하는 상태 레코드 가장 낮은 순위를 가집니다. 둘 이상의 레코드 SQLSTATEs 열기 그룹 CLI 사양에 정의 된 경고를 동일한 경고 조건에 설명 하는 경우 ODBC 정의 및 드라이버에서 정의 된 Sqlstate outrank 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|진단 데이터 구조체의 여러 필드 가져오기|[SQLGetDiagRec 함수](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
