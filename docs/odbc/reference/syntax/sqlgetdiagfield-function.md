---
title: SQLGetDiag필드 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a26319868a4b94b895da73d39b284f612fe35889
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285433"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 함수(SQLGetDiagField Function)

**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetDiagField오류,** 경고 및 상태 정보를 포함하는 진단 데이터 구조(지정된 핸들와 연관된) 레코드 필드의 현재 값을 반환합니다.  
  
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
 [입력] 진단이 필요한 핸들 유형을 설명하는 핸들 형식 식별자입니다. 다음 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 핸들은 드라이버 관리자와 드라이버에서만 사용됩니다. 응용 프로그램에서는 이 핸들 형식을 사용해서는 안 됩니다. SQL_HANDLE_DBC_INFO_TOKEN 대한 자세한 내용은 [ODBC 드라이버에서 연결-풀 인식 개발을](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)참조하십시오.  
  
 *Handle*  
 [입력] *핸들 Type으로*표시된 형식의 진단 데이터 구조에 대한 핸들입니다. *핸들유형이* SQL_HANDLE_ENV 경우 *핸들은* 공유 또는 공유되지 않은 환경 핸들일 수 있습니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램에서 정보를 검색하는 상태 레코드를 나타냅니다. 상태 레코드는 1에서 번호가 매겨져 있습니다. *DiagIdentifier* 인수진단 헤더의 필드를 나타내는 경우 *RecNumber는* 무시됩니다. 그렇지 않은 경우 0보다 높아야 합니다.  
  
 *디아그식별서*  
 [입력] 값을 반환할 진단 의 필드를 나타냅니다. 자세한 내용은 "주석" 섹션의 *"DiagIdentifier* 인수" 섹션을 참조하십시오.  
  
 *디아그포페프르*  
 [출력] 진단 정보를 반환할 버퍼에 대한 포인터입니다. 데이터 형식은 *DiagIdentifier*의 값에 따라 달라집니다. *DiagInfoPtr이* 정수 형식인 경우 일부 드라이버는 32비트 또는 16비트 버퍼만 작성하고 상위 순서의 비트를 변경하지 않고 그대로 둘 수 있기 때문에 응용 프로그램은 SQLULEN 버퍼를 사용하고 이 함수를 호출하기 전에 값을 0으로 초기화해야 합니다.  
  
 *DiagInfoPtr이* NULL인 경우 *StringLengthPtr은* *DiagInfoPtr에서*가리키는 버퍼에서 반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] *DiagIdentifier가* ODBC 정의 진단이고 *DiagInfoPtr이* 문자 문자열 또는 이진 버퍼를 가리키는 \*경우 이 인수는 *DiagInfoPtr*의 길이여야 합니다. *DiagIdentifier가* ODBC 정의 필드이고 \* *DiagInfoPtr이* 정수인 경우 *버퍼길이는* 무시됩니다. DiagInfoPtr의 값이 유니코드 문자열인 **경우(SQLGetDiagFieldW를**호출할 때) *버퍼길이* 인수는 짝수여야 합니다. * \**  
  
 *DiagIdentifier가* 드라이버 정의 필드인 경우 응용 프로그램은 *BufferLength* 인수를 설정하여 드라이버 관리자에 필드의 특성을 나타냅니다. *BufferLength에는* 다음 값이 있을 수 있습니다.  
  
-   *DiagInfoPtr이* 문자 문자열에 대한 포인터인 경우 *BufferLength는* 문자열 또는 SQL_NTS 길이입니다.  
  
-   *DiagInfoPtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은 *버퍼길이*에*SQL_LEN_BINARY_ATTR(길이)* 매크로의 결과를 배치합니다. 이렇게 하면 *버퍼길이에*음수 값이 배치됩니다.  
  
-   *DiagInfoPtr이* 문자열 문자열 이나 이진 문자열 이외의 값에 대 한 포인터 인 경우 *BufferLength* 값 SQL_IS_POINTER 있어야 합니다.  
  
-   * \*DiagInfoPtr* 고정 길이 데이터 형식이 포함 된 경우 *BufferLength는* 적절 하 게 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT 또는 SQL_IS_USMALLINT.  
  
 *문자열길이Ptr*  
 [출력] 문자 데이터에 대한 \* *DiagInfoPtr에서*반환할 수 있는 총 바이트 수(null-termination 문자에 필요한 바이트 수 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 바이트 수가 *BufferLength보다*크거나 같으면 \* *DiagInfoPtr의* 텍스트는 *BufferLength에* 잘려null 종료 문자의 길이를 뺀 값입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_NO_DATA.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDiagField는** 자체적으로 진단 레코드를 게시하지 않습니다. 다음 반환 값을 사용하여 자체 실행 결과를 보고합니다.  
  
-   SQL_SUCCESS: 함수가 진단 정보를 반환했습니다.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr가* 너무 작아서 요청된 진단 필드를 보유할 수 없습니다. 따라서 진단 필드의 데이터가 잘렸습니다. 잘림이 발생했는지 확인하려면 응용 프로그램에서 *BufferLength를* **StringLengthPtr에*기록된 사용 가능한 실제 바이트 수와 비교해야 합니다.  
  
-   SQL_INVALID_HANDLE: HandleType *및* *Handle으로* 표시된 핸들이 올바른 핸들이 아닙니다.  
  
-   SQL_ERROR: 다음 중 하나가 발생했습니다.  
  
    -   *DiagIdentifier 인수는* 유효한 값 중 하나가 아닙니다.  
  
    -   *DiagIdentifier 인수는* SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE 또는 SQL_DIAG_ROW_COUNT 했지만 *핸들은* 문 핸들이 아닙니다. (드라이버 관리자가 이 진단을 반환합니다.)  
  
    -   *DiagIdentifier가* 진단 레코드의 필드를 나타낼 때 *RecNumber* 인수는 음수 또는 0입니다. *RecNumber는* 헤더 필드에 대해 무시됩니다.  
  
    -   요청된 값은 문자 문자열이고 *BufferLength는* 0보다 적습니다.  
  
    -   비동기 알림을 사용하는 경우 핸들의 비동기 작업이 완료되지 않았습니다.  
  
-   SQL_NO_DATA: *RecNumber핸들에* 지정된 핸들에 대해 존재했던 진단 레코드 수보다 *큽입니다.* 또한 이 함수는 *handle*에 대한 진단 레코드가 없는 경우 양수 *RecNumber에* 대해 SQL_NO_DATA 반환합니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램은 일반적으로 **SQLGetDiagField를** 호출하여 다음 세 가지 목표 중 하나를 수행합니다.  
  
1.  함수 호출이 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO(또는 **SQLBrowseConnect** 함수에 대한 SQL_NEED_DATA)를 반환할 때 특정 오류 또는 경고 정보를 얻으려면  
  
2.  삽입, 삭제 또는 업데이트 작업 때 영향을 받은 데이터 원본의 행 수를 확인 하려면 **SQLExecute,** **SQLExEcDirect**, **SQLBulkOperations**또는 **SQLSetPos(SQL_DIAG_ROW_COUNT** 헤더 필드)에 대 한 호출을 사용 하 여 수행 하거나 현재 열려 있는 커서에 있는 행 수를 확인 하려면 드라이버 (SQL_DIAG_CURSOR_ROW_COUNT 헤더 필드에서)에서이 정보를 제공할 수 있습니다.  
  
3.  **SQLExecDirect** 또는 **SQLExecute(SQL_DIAG_DYNAMIC_FUNCTION** 및 SQL_DIAG_DYNAMIC_FUNCTION_CODE 헤더 필드)에 대한 호출에 의해 실행된 함수를 확인합니다.  
  
 모든 ODBC 함수는 호출될 때마다 0 개 이상의 진단 레코드를 게시할 수 있으므로 응용 프로그램은 ODBC 함수 호출 후 **SQLGetDiagField를** 호출할 수 있습니다. 한 번에 저장할 수 있는 진단 레코드 의 수에는 제한이 없습니다. **SQLGetDiagField는** *핸들* 인수에 지정된 진단 데이터 구조와 가장 최근에 연관된 진단 정보만 검색합니다. 응용 프로그램이 **SQLGetDiagField** 또는 **SQLGetDiagRec**이외의 ODBC 함수를 호출하는 경우 동일한 핸들을 가진 이전 호출의 진단 정보가 손실됩니다.  
  
 응용 프로그램은 **SQLGetDiagField가** SQL_SUCCESS 반환하는 한 *RecNumber를*증가시켜 모든 진단 레코드를 검색할 수 있습니다. 상태 레코드 수는 SQL_DIAG_NUMBER 헤더 필드에 표시됩니다. **SQLGetDiagField에** 대한 호출은 헤더 및 레코드 필드에 비파괴적입니다. 응용 프로그램은 나중에 **SQLGetDiagField를** 호출하여 진단 함수 이외의 함수가 중간에 호출되지 않은 한 레코드에서 필드를 검색하여 동일한 핸들에 레코드를 게시할 수 있습니다.  
  
 응용 프로그램은 **SQLGetDiagField를** 호출하여 SQL_DIAG_CURSOR_ROW_COUNT 또는 SQL_DIAG_ROW_COUNT 제외하고 언제든지 진단 필드를 반환할 수 있으며 핸들이 문 핸들이 아닌 *경우* SQL_ERROR 반환합니다. 다른 진단 필드가 정의되지 않은 경우 **SQLGetDiagField** 호출은 SQL_SUCCESS 반환되며(다른 진단이 발생하지 않는 경우) 필드에 대해 정의되지 않은 값이 반환됩니다.  
  
 자세한 내용은 [SQLGetDiagRec 및 SQLGetDiagField 사용](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 및 [SQLGetDiagRec 및 SQLGetDiagField 구현을](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)참조하십시오.  
  
 비동기적으로 실행되는 API 이외의 API를 호출하면 HY010 "함수 시퀀스 오류"가 생성됩니다. 그러나 비동기 작업이 완료되기 전에는 오류 레코드를 검색할 수 없습니다.  
  
## <a name="handletype-argument"></a>핸들 타입 인수  
 각 핸들 유형에는 연결된 진단 정보가 있을 수 있습니다. *핸들 Type* 인수는 *핸들*의 핸들 형식을 나타냅니다.  
  
 환경, 연결, 명령문 및 설명자 핸들에 대해 일부 헤더 및 레코드 필드를 반환할 수 없습니다. 필드가 적용되지 않는 핸들은 다음의 "헤더 필드" 및 "레코드 필드" 섹션에 표시됩니다.  
  
 *핸들 유형이* SQL_HANDLE_ENV 경우 *핸들은* 공유 환경 핸들이거나 공유되지 않은 환경 핸들일 수 있습니다.  
  
 드라이버 관련 헤더 진단 필드를 환경 핸들과 연결해서는 안 됩니다.  
  
 설명자 핸들에 대해 정의된 진단 헤더 필드는 SQL_DIAG_NUMBER SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier 인수  
 이 인수는 진단 데이터 구조에서 필요한 필드의 식별자를 나타냅니다. *RecNumber가* 1보다 크거나 같으면 필드의 데이터는 함수에서 반환되는 진단 정보를 설명합니다. *RecNumber가* 0이면 필드가 진단 데이터 구조의 헤더에 있으므로 특정 정보가 아닌 진단 정보를 반환한 함수 호출과 관련된 데이터가 포함됩니다.  
  
 드라이버는 진단 데이터 구조에서 드라이버 별 헤더 및 레코드 필드를 정의할 수 있습니다.  
  
 ODBC 2 *.x* 드라이버로 작업하는 ODBC 3 *.x* 응용 프로그램은 SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME 또는 SQL_DIAG_SQLSTATE *대한 DiagIdentifier* 인수를 통해서만 **SQLGetDiagField를** 호출할 수 있습니다. 다른 모든 진단 필드는 SQL_ERROR 반환합니다.  
  
## <a name="header-fields"></a>헤더 필드  
 다음 표에 나열된 헤더 필드는 *DiagIdentifier* 인수에 포함될 수 있습니다.  
  
|디아그식별서|반환 형식|반환|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|이 필드에는 커서의 행 수가 포함됩니다. 시맨틱은 **SQLGetInfo** 정보 유형 SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 및 SQL_STATIC_CURSOR_ATTRIBUTES2 따라 달라지며, 이는 각 커서 유형(SQL_CA2_CRC_EXACT 및 SQL_CA2_CRC_APPROXIMATE 비트)에 사용할 수 있는 행 수를 나타냅니다.<br /><br /> 이 필드의 내용은 명령문 핸들에 대해서만 정의되며 **SQLExecute,** **SQLExecDirect**또는 **SQLMoreResults가** 호출된 후에만 정의됩니다. **SQLGetDiagField를** 문 핸들 이 외의 SQL_DIAG_CURSOR_ROW_COUNT *DiagIdentifier로* 호출하면 SQL_ERROR 반환됩니다.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|기본 함수가 실행한 SQL 문을 설명하는 문자열입니다. (특정 값은 이 섹션의 후반부 "동적 함수 필드의 값"을 참조하십시오.) 이 필드의 내용은 **SQLExecute,** **SQLExecDirect**또는 **SQLMoreResults**에 대한 호출 후에만 문 핸들에 대해서만 정의됩니다. **SQLGetDiagField를** 문 핸들 이 외의 *SQL_DIAG_DYNAMIC_FUNCTION DiagIdentifier로* 호출하면 SQL_ERROR 반환됩니다. 이 필드의 값은 **SQLExecute** 또는 **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|기본 함수에 의해 실행된 SQL 문을 설명하는 숫자 코드입니다. (특정 값은 이 섹션의 후반부 "동적 함수 필드의 값"을 참조하십시오.) 이 필드의 내용은 **SQLExecute,** **SQLExecDirect**또는 **SQLMoreResults**에 대한 호출 후에만 문 핸들에 대해서만 정의됩니다. **SQLGetDiagField를** 문 핸들 이외 다른 SQL_DIAG_DYNAMIC_FUNCTION_CODE *DiagIdentifier를* 호출하면 SQL_ERROR 반환됩니다. 이 필드의 값은 **SQLExecute** 또는 **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|지정된 핸들에 사용할 수 있는 상태 레코드 의 수입니다.|  
|SQL_DIAG_RETURNCODE|SQL리턴|함수에서 반환되는 코드를 반환합니다. 반환 코드 목록은 반환 [코드](../../../odbc/reference/develop-app/return-codes-odbc.md)를 참조하십시오. 드라이버는 SQL_DIAG_RETURNCODE 구현할 필요가 없습니다. 항상 드라이버 관리자에 의해 구현됩니다. *핸들에*아직 호출된 함수가 없는 경우 SQL_SUCCESS SQL_DIAG_RETURNCODE 동안 반환됩니다.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|**SQLExecute,** **SQLExecDirect**, **SQLBulkOperations**또는 **SQLSetPos에**의해 수행되는 삽입, 삭제 또는 업데이트의 영향을 받는 행 수입니다. *커서 사양이* 실행된 후 드라이버 정의됩니다. 이 필드의 내용은 명령문 핸들에 대해서만 정의됩니다. **SQLGetDiagField를** 문 핸들 이외 SQL_DIAG_ROW_COUNT *DiagIdentifier로* 호출하면 SQL_ERROR 반환됩니다. 이 필드의 데이터는 **SQLRowCount**의 *RowCount Ptr* 인수에서도 반환됩니다. 이 필드의 데이터는 모든 비진단 함수 호출 후에 재설정되지만 **SQLRowCount에서** 반환되는 행 수는 명령문이 준비되거나 할당된 상태로 다시 설정될 때까지 동일하게 유지됩니다.|  
  
## <a name="record-fields"></a>레코드 필드  
 다음 표에 나열된 레코드 필드는 *DiagIdentifier* 인수에 포함될 수 있습니다.  
  
|디아그식별서|반환 형식|반환|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|이 레코드에서 SQLSTATE 값의 클래스 부분을 정의하는 문서를 나타내는 문자열입니다. 해당 값은 오픈 그룹 및 ISO 호출 수준 인터페이스에 의해 정의된 모든 SQLSTATEs에 대해 "ISO 9075"입니다. ODBC 관련 SQLSTATEs(SQLSTATE 클래스가 "IM"인 모든 SQLSTAT)의 경우 해당 값은 "ODBC 3.0"입니다.|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|SQL_DIAG_ROW_NUMBER 필드가 행 집합의 유효한 행 번호이거나 매개 변수 집합인 경우 이 필드에는 결과 집합의 열 번호 또는 매개 변수 집합의 매개 변수 번호를 나타내는 값이 포함됩니다. 결과 집합 열 번호는 항상 1부터 시작됩니다. 이 상태 레코드가 책갈피 열과 관련된 경우 필드는 0이 될 수 있습니다. 매개 변수 번호는 1부터 시작합니다. 상태 레코드가 열 번호 또는 매개 변수 번호와 연결되지 않은 경우 SQL_NO_COLUMN_NUMBER 값이 있습니다. 드라이버가 이 레코드와 연결된 열 번호 또는 매개 변수 번호를 확인할 수 없는 경우 이 필드에는 SQL_COLUMN_NUMBER_UNKNOWN 값이 있습니다.<br /><br /> 이 필드의 내용은 명령문 핸들에 대해서만 정의됩니다.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|진단 레코드와 관련된 연결 이름을 나타내는 문자열입니다. 이 필드는 드라이버 정의입니다. 환경 핸들과 관련된 진단 데이터 구조와 연결과 관련이 없는 진단의 경우 이 필드는 길이가 0인 문자열입니다.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|오류 또는 경고에 대한 정보 메시지입니다. 이 필드는 진단 메시지에 설명된 대로 서식이 [지정됩니다.](../../../odbc/reference/develop-app/diagnostic-messages.md) 진단 메시지 텍스트의 최대 길이가 없습니다.|  
|SQL_DIAG_NATIVE|SQLINTEGER|드라이버/데이터 원본별 네이티브 오류 코드입니다. 기본 오류 코드가 없는 경우 드라이버는 0을 반환합니다.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|이 필드에는 행 집합의 행 번호 또는 상태 레코드가 연결된 매개 변수 집합의 매개 변수 번호가 포함됩니다. 행 번호와 매개 변수 번호는 1로 시작합니다. 이 필드에는 이 상태 레코드가 행 번호 또는 매개 변수 번호와 연결되지 않은 경우 SQL_NO_ROW_NUMBER 값이 있습니다. 드라이버가 이 레코드와 연결된 행 번호 또는 매개 변수 번호를 확인할 수 없는 경우 이 필드에는 SQL_ROW_NUMBER_UNKNOWN 값이 있습니다.<br /><br /> 이 필드의 내용은 명령문 핸들에 대해서만 정의됩니다.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|진단 레코드와 관련된 서버 이름을 나타내는 문자열입니다. SQL_DATA_SOURCE_NAME 옵션을 사용하여 **SQLGetInfo** 호출에 대해 반환된 값과 동일합니다. 환경 핸들과 관련된 진단 데이터 구조와 서버와 관련이 없는 진단의 경우 이 필드는 길이가 0인 문자열입니다.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|5자 SQLSTATE 진단 코드입니다. 자세한 내용은 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)를 참조하십시오.|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|SQLSTATE 코드의 하위 클래스 부분의 정의 부분을 식별하는 SQL_DIAG_CLASS_ORIGIN 동일한 형식과 유효한 값을 가진 문자열입니다. "ODBC 3.0"이 반환되는 ODBC 관련 SQLSTATES는 다음과 같습니다.<br /><br /> 01S00, 01S01, 01S02, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S11, 42S12, 42S21, 42S22, HY095, HY099, HY099, HY099, HY099, HY099, HY099, HY099, HY099 HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM0110, IM0110, IM0110.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>동적 함수 필드의 값  
 다음 표는 **SQLExecute** 또는 **SQLExecDirect**에 대한 호출에 의해 실행되는 각 SQL 문 유형에 적용되는 SQL_DIAG_DYNAMIC_FUNCTION 및 SQL_DIAG_DYNAMIC_FUNCTION_CODE 값에 대해 설명합니다. 드라이버는 나열된 값에 드라이버 정의 값을 추가할 수 있습니다.  
  
|SQL 문<br /><br /> 실행|의 값<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|의 값<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*도메인 문 변경*|"도메인 변경"|SQL_DIAG_ALTER_DOMAIN|  
|*테이블 문 변경*|"테이블 변경"|SQL_DIAG_ALTER_TABLE|  
|*어설션 정의*|"어설션 만들기"|SQL_DIAG_CREATE_ASSERTION|  
|*문자 집합 정의*|"캐릭터 세트 만들기"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*데이터 정렬 정의*|"데이터 정렬 만들기"|SQL_DIAG_CREATE_COLLATION|  
|*도메인 정의*|"도메인 만들기"|SQL_DIAG_CREATE_DOMAIN|
|*생성 인덱스 문*|"인덱스 만들기"|SQL_DIAG_CREATE_INDEX|  
|*테이블 문 만들기*|"테이블 만들기"|SQL_DIAG_CREATE_TABLE|  
|*뷰-문 만들기*|"뷰 만들기"|SQL_DIAG_CREATE_VIEW|  
|*커서 사양*|"커서 선택"|SQL_DIAG_SELECT_CURSOR|  
|*삭제 문 위치*|"동적 커서 삭제"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*문 삭제 검색*|"삭제 위치"|SQL_DIAG_DELETE_WHERE|  
|*드롭 어설션-문*|"drop 어설션"|SQL_DIAG_DROP_ASSERTION|  
|*드롭 문자 세트 - stmt*|"드롭 문자 세트"|SQL_DIAG_DROP_CHARACTER_SET|  
|*드롭 데이터 정렬-문*|"드롭 데이터 정렬"|SQL_DIAG_DROP_COLLATION|  
|*드롭 도메인 문*|"드롭 도메인"|SQL_DIAG_DROP_DOMAIN|  
|*드롭 인덱스 문*|"드롭 인덱스"|SQL_DIAG_DROP_INDEX|  
|*드롭 스키마 문*|"드롭 스키마"|SQL_DIAG_DROP_SCHEMA|  
|*드롭 테이블 문*|"드롭 테이블"|SQL_DIAG_DROP_TABLE|  
|*드롭 번역 문*|"드롭 번역"|SQL_DIAG_DROP_TRANSLATION|  
|*드롭 뷰-문*|"드롭 뷰"|SQL_DIAG_DROP_VIEW|  
|*교부금*|"그랜트"|SQL_DIAG_GRANT|
|*삽입 문*|"삽입"|SQL_DIAG_INSERT|  
|*ODBC 절차 확장*|"전화"|SQL_DIAG_ 통화|  
|*취소 문*|"해지"|SQL_DIAG_REVOKE|  
|*스키마 정의*|"스키마 만들기"|SQL_DIAG_CREATE_SCHEMA|  
|*번역 정의*|"번역 만들기"|SQL_DIAG_CREATE_TRANSLATION|  
|*업데이트 문 위치*|"동적 업데이트 커서"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*업데이트 문 검색*|"어디에 업데이트"|SQL_DIAG_UPDATE_WHERE|  
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

 상태 레코드는 행 번호와 진단 유형에 따라 시퀀스에 배치됩니다. 드라이버 관리자는 생성되는 상태 레코드를 반환할 최종 순서를 결정합니다. 드라이버는 생성되는 상태 레코드를 반환할 최종 순서를 결정합니다.  
  
 드라이버 관리자와 드라이버 모두에 의해 진단 레코드가 게시되는 경우 드라이버 관리자는 진단 레코드를 주문할 책임이 있습니다.  
  
 둘 이상의 상태 레코드가 있는 경우 레코드 의 시퀀스는 행 번호로 먼저 결정됩니다. 다음 규칙은 행별 진단 레코드의 순서를 결정하는 데 적용됩니다.  
  
-   SQL_NO_ROW_NUMBER -1로 정의되기 때문에 행에 일치하지 않는 레코드는 특정 행에 해당하는 레코드 앞에 나타납니다.  
  
-   행 번호를 알 수 없는 레코드는 SQL_ROW_NUMBER_UNKNOWN -2로 정의되므로 다른 모든 레코드 앞에 나타납니다.  
  
-   특정 행과 관련된 모든 레코드의 경우 레코드는 SQL_DIAG_ROW_NUMBER 필드의 값으로 정렬됩니다. 영향을 받는 첫 번째 행의 모든 오류 및 경고가 나열되고 다음 행의 모든 오류 및 경고 등이 표시됩니다.  
  
> [!NOTE]
>  SQLSTATE 01S01 (행의 오류)가 ODBC 2 *.x* 드라이버에 의해 반환되거나 SQLSTATE 01S01 (행의 오류)이 ODBC 3 *.x* 드라이버에 의해 반환되거나 **SQLSetPos가 SQLSetPos가 SQL로** 배치 된 커서에 호출 될 때 ODBC 3 *.x* 드라이버가 반환되는 경우 ODBC 3 .x 드라이버 관리자는 진단 큐에서 상태 레코드를 정렬하지 **않습니다.** **SQLExtendedFetch**  
  
 각 행 내에서 또는 행 번호와 일치하지 않거나 행 번호를 알 수 없는 모든 레코드또는 SQL_NO_ROW_NUMBER 동일한 행 번호를 가진 모든 레코드에 대해 나열된 첫 번째 레코드는 정렬 규칙 집합을 사용하여 결정됩니다. 첫 번째 레코드 후 행에 영향을 미치는 다른 레코드의 순서는 정의되지 않습니다. 응용 프로그램은 첫 번째 레코드 다음의 경고 앞에 오류가 있다고 가정할 수 없습니다. 응용 프로그램은 함수에 대한 실패한 호출에 대한 완전한 정보를 얻기 위해 전체 진단 데이터 구조를 검사해야 합니다.  
  
 다음 규칙은 행 내의 첫 번째 레코드를 결정하는 데 사용됩니다. 순위가 가장 높은 레코드는 첫 번째 레코드입니다. 레코드의 소스(드라이버 관리자, 드라이버, 게이트웨이 등)는 레코드의 순위를 매를 정할 때 고려되지 않습니다.  
  
-   **오류** 오류를 설명하는 상태 레코드의 순위가 가장 높습니다. 정렬 오류에는 다음 규칙이 적용됩니다.  
  
    -   트랜잭션 실패 또는 가능한 트랜잭션 실패를 나타내는 레코드가 다른 모든 레코드보다 우선합니다.  
  
    -   둘 이상의 레코드가 동일한 오류 조건을 설명하는 경우 Open 그룹 CLI 사양(클래스 03 ~ HZ)에 의해 정의된 SQLSTAT는 ODBC 및 드라이버 정의 SQLSTATEs보다 훨씬 높습니다.  
  
-   **구현 정의 데이터 값 없음** 드라이버 정의 데이터 없음 값(클래스 02)을 설명하는 상태 레코드의 순위가 두 번째로 높습니다.  
  
-   **경고 메시지** 경고(클래스 01)를 설명하는 상태 레코드의 순위가 가장 낮습니다. 둘 이상의 레코드가 동일한 경고 조건을 설명하는 경우 Open 그룹 CLI 사양에 정의된 SQLSTATEs경고가 ODBC 정의 및 드라이버 정의 SQLSTATEs보다 앞선다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|진단 데이터 구조의 여러 필드 구하기|[SQLGetDiagRec 함수](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
