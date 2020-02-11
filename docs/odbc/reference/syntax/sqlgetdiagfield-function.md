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
ms.openlocfilehash: 620ccce9a035139482b2d9b4630bb2242f720af8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103773"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 함수(SQLGetDiagField Function)

**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetDiagField** 는 오류, 경고 및 상태 정보를 포함 하는 진단 데이터 구조 (지정 된 핸들과 연결 된) 레코드의 필드에 대 한 현재 값을 반환 합니다.  
  
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
 입력 진단이 필요한 핸들의 유형을 설명 하는 핸들 유형 식별자입니다. 다음 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 핸들은 드라이버 관리자 및 드라이버 에서만 사용 됩니다. 응용 프로그램은이 핸들 형식을 사용 하면 안 됩니다. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)을 참조 하세요.  
  
 *처리*  
 입력 *HandleType*로 표시 되는 형식의 진단 데이터 구조에 대 한 핸들입니다. *HandleType* 가 SQL_HANDLE_ENV 경우 *handle* 은 공유 또는 공유 되지 않는 환경 핸들 일 수 있습니다.  
  
 *개수*  
 입력 응용 프로그램에서 정보를 검색 하는 상태 레코드를 나타냅니다. 상태 레코드의 번호는 1입니다. *DiagIdentifier* 인수는 진단 헤더의 *필드를 나타내는 경우에는* 무시 됩니다. 그렇지 않은 경우에는 0 보다 커야 합니다.  
  
 *DiagIdentifier*  
 입력 값을 반환할 진단 필드를 나타냅니다. 자세한 내용은 "Comments"의 "*DiagIdentifier* 인수" 섹션을 참조 하세요.  
  
 *DiagInfoPtr*  
 출력 진단 정보를 반환할 버퍼에 대 한 포인터입니다. 데이터 형식은 *DiagIdentifier*의 값에 따라 달라 집니다. *DiagInfoPtr* 이 정수 형식이 면 응용 프로그램은이 함수를 호출 하기 전에 SQLULEN의 버퍼를 사용 하 고 값을 0으로 초기화 해야 합니다. 일부 드라이버는 버퍼의 하위 32 비트 또는 16 비트만 쓸 수 있고 고차 비트는 변경 되지 않은 상태로 둘 수 있습니다.  
  
 *DiagInfoPtr* 가 NULL 인 경우 *StringLengthPtr* 는 *DiagInfoPtr*가 가리키는 버퍼에서 반환 될 수 있는 총 바이트 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 합니다.  
  
 *BufferLength*  
 입력 *DiagIdentifier* 이 ODBC에 정의 된 진단이 고 *DiagInfoPtr* 가 문자열 또는 이진 버퍼를 가리키는 경우이 인수는 \* *DiagInfoPtr*의 길이 여야 합니다. *DiagIdentifier* 가 ODBC 정의 필드이 고 \* *DiagInfoPtr* 가 정수인 경우 *bufferlength* 는 무시 됩니다. * \*DiagInfoPtr* 의 값이 유니코드 문자열이 면 ( **SQLGetDiagFieldW**호출 시) *bufferlength* 인수는 짝수 여야 합니다.  
  
 *DiagIdentifier* 가 드라이버 정의 필드인 경우 응용 프로그램은 *bufferlength* 인수를 설정 하 여 필드의 특성을 드라이버 관리자에 게 표시 합니다. *Bufferlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   *DiagInfoPtr* 이 문자열에 대 한 포인터인 경우 *bufferlength* 는 문자열 또는 SQL_NTS의 길이입니다.  
  
-   *DiagInfoPtr* 가 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*길이*) 매크로의 결과를 *bufferlength*로 배치 합니다. 그러면 음수 값이 *Bufferlength*에 배치 됩니다.  
  
-   *DiagInfoPtr* 가 문자열 또는 이진 문자열이 아닌 값에 대 한 포인터인 경우 *bufferlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   * \*DiagInfoPtr* 에 고정 길이 데이터 형식이 포함 된 경우 *bufferlength* 는 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT 또는 SQL_IS_USMALLINT입니다.  
  
 *StringLengthPtr*  
 출력 문자 데이터에 대해 \* *DiagInfoPtr*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (null 종결 문자에 필요한 바이트 수 제외)를 반환할 버퍼에 대 한 포인터입니다. 반환할 수 있는 바이트 수가 *bufferlength*보다 크거나 같은 경우 \* *DiagInfoPtr* 의 텍스트는 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_NO_DATA입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDiagField** 는 자체에 대 한 진단 레코드를 게시 하지 않습니다. 다음 반환 값을 사용 하 여 자체 실행의 결과를 보고 합니다.  
  
-   SQL_SUCCESS: 함수가 진단 정보를 성공적으로 반환 했습니다.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* 이 너무 작아서 요청 된 진단 필드를 보유할 수 없습니다. 따라서 진단 필드의 데이터가 잘렸습니다. 잘림이 발생 했는지 확인 하기 위해 응용 프로그램은 *Bufferlength* 를 사용 가능한 실제 바이트 수와 비교 하 여 **StringLengthPtr*에 기록 합니다.  
  
-   SQL_INVALID_HANDLE: *HandleType* 및 *handle* 이 나타내는 핸들이 유효한 핸들이 아닙니다.  
  
-   SQL_ERROR: 다음 중 하나가 발생 했습니다.  
  
    -   *DiagIdentifier* 인수가 유효한 값 중 하나가 아닙니다.  
  
    -   *DiagIdentifier* 인수가 SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE 또는 SQL_DIAG_ROW_COUNT 되었지만 *핸들이* 문 핸들이 아닙니다. (드라이버 관리자는이 진단을 반환 합니다.)  
  
    -   *DiagIdentifier* 가 진단 레코드에서 필드를 나타내는 경우 *에는 값* 이 음수 이거나 0입니다. 헤더 필드의 경우에는 *번호가* 무시 됩니다.  
  
    -   요청 된 값이 문자열이 고 *Bufferlength* 가 0 보다 작은 경우  
  
    -   비동기 알림을 사용 하는 경우 핸들에 대 한 비동기 작업이 완료 되지 않았습니다.  
  
-   SQL_NO_DATA: *값* 이 *핸들* 에 지정 된 핸들에 대해 존재 하는 진단 레코드 수보다 큽니다. 또한 함수는 *핸들*에 대 한 진단 레코드가 없는 경우 양수 *값* 에 대 한 SQL_NO_DATA를 반환 합니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램은 일반적으로 **SQLGetDiagField** 를 호출 하 여 다음 세 가지 목표 중 하나를 수행 합니다.  
  
1.  함수 호출이 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO (또는 **SQLBrowseConnect** 함수의 경우 SQL_NEED_DATA)를 반환 했을 때 특정 오류 또는 경고 정보를 가져오려면  
  
2.  SQL_DIAG_ROW_COUNT 헤더 필드에서 **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 를 호출 하 여 삽입, 삭제 또는 업데이트 작업을 수행 했을 때 영향을 받는 데이터 원본의 행 수를 확인 하거나 드라이버가 SQL_DIAG_CURSOR_ROW_COUNT 헤더 필드에서이 정보를 제공할 수 있는 경우 현재 열린 커서에 있는 행 수를 확인 합니다.  
  
3.  **Sqlexecdirect** 또는 **sqlexecute** 를 호출 하 여 실행 된 함수를 확인 하려면 (SQL_DIAG_DYNAMIC_FUNCTION 및 SQL_DIAG_DYNAMIC_FUNCTION_CODE 헤더 필드에서)  
  
 모든 ODBC 함수는 호출 될 때마다 0 개 이상의 진단 레코드를 게시할 수 있으므로 응용 프로그램은 ODBC 함수 호출 후 **SQLGetDiagField** 를 호출할 수 있습니다. 한 번에 저장할 수 있는 진단 레코드 수에는 제한이 없습니다. **SQLGetDiagField** 는 *핸들* 인수에 지정 된 진단 데이터 구조와 가장 최근에 연결 된 진단 정보만 검색 합니다. 응용 프로그램에서 **SQLGetDiagField** 또는 **SQLGetDiagRec**이외의 ODBC 함수를 호출 하는 경우 동일한 핸들이 있는 이전 호출의 진단 정보는 모두 손실 됩니다.  
  
 **SQLGetDiagField** 가 SQL_SUCCESS을 반환 하는 한 응용 프로그램은 *개수*를 증가 시켜 모든 진단 레코드를 검색할 수 있습니다. 상태 레코드의 수는 SQL_DIAG_NUMBER 헤더 필드에 표시 됩니다. **SQLGetDiagField** 에 대 한 호출은 헤더 및 레코드 필드에 대 한 비파괴입니다. 응용 프로그램은 나중에 **SQLGetDiagField** 를 다시 호출 하 여 진단 함수 이외의 함수가 중간에 호출 되지 않은 경우 동일한 핸들에 레코드를 게시할 수 있습니다.  
  
 응용 프로그램은 SQL_DIAG_CURSOR_ROW_COUNT 또는 SQL_DIAG_ROW_COUNT를 제외 하 고 언제 든 지 **SQLGetDiagField** 를 호출 하 여 진단 필드를 반환할 수 있습니다 .이는 *핸들이* 문 핸들이 아닌 경우 SQL_ERROR를 반환 합니다. 다른 진단 필드가 정의 되어 있지 않으면 **SQLGetDiagField** 에 대 한 호출에서 다른 진단이 발생 하지 않은 경우에는 SQL_SUCCESS을 반환 하 고 필드에 대해 정의 되지 않은 값이 반환 됩니다.  
  
 자세한 내용은 [SQLGetDiagRec 및 SQLGetDiagField 사용](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 및 [SQLGetDiagRec 및 SQLGetDiagField 구현](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)을 참조 하세요.  
  
 비동기적으로 실행 되는 API 이외의 API를 호출 하면 "함수 시퀀스 오류" HY010 생성 됩니다. 그러나 비동기 작업이 완료 되기 전에는 오류 레코드를 검색할 수 없습니다.  
  
## <a name="handletype-argument"></a>HandleType 인수  
 각 핸들 유형에는 연결 된 진단 정보가 있을 수 있습니다. *HandleType* 인수 *는 핸들의*핸들 형식을 나타냅니다.  
  
 환경, 연결, 문 및 설명자 핸들에 대해 일부 헤더 및 레코드 필드를 반환할 수 없습니다. 필드가 적용 되지 않는 핸들은 다음에 나오는 "헤더 필드" 및 "레코드 필드" 섹션에 나와 있습니다.  
  
 *HandleType* 가 SQL_HANDLE_ENV 경우 *handle* 은 공유 또는 공유 되지 않는 환경 핸들 일 수 있습니다.  
  
 드라이버 관련 헤더 진단 필드는 환경 핸들과 연결 되지 않아야 합니다.  
  
 설명자 핸들에 대해 정의 된 진단 헤더 필드는 SQL_DIAG_NUMBER SQL_DIAG_RETURNCODE 됩니다.  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier 인수  
 이 인수는 진단 데이터 구조에서 필요한 필드의 식별자를 나타냅니다. *값* 이 1 보다 크거나 같으면 필드의 데이터는 함수에서 반환 된 진단 정보를 설명 합니다. *값* 이 0 이면 필드는 진단 데이터 구조의 헤더에 있으므로 특정 정보가 아닌 진단 정보를 반환 하는 함수 호출과 관련 된 데이터를 포함 합니다.  
  
 드라이버는 드라이버 관련 헤더 및 레코드 필드를 진단 데이터 구조로 정의할 수 있습니다.  
  
 Odbc*2.x 드라이버를* 사용 하 여 작업 하는*odbc 3(sp3) 응용* 프로그램은 SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME 또는 SQL_DIAG_SQLSTATE의 *DiagIdentifier* 인수를 사용 하 여 **SQLGetDiagField** 를 호출할 수 있습니다. 다른 모든 진단 필드는 SQL_ERROR을 반환 합니다.  
  
## <a name="header-fields"></a>헤더 필드  
 다음 표에 나열 된 헤더 필드는 *DiagIdentifier* 인수에 포함 될 수 있습니다.  
  
|DiagIdentifier|반환 형식|반환|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|이 필드는 커서의 행 수를 포함 합니다. 이러한 의미 체계는 각 커서 유형에 사용할 수 있는 행 개수 (SQL_CA2_CRC_EXACT 및 SQL_CA2_CRC_APPROXIMATE 비트)를 나타내는 **SQLGetInfo** 정보 형식 SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 및 SQL_STATIC_CURSOR_ATTRIBUTES2에 따라 다릅니다.<br /><br /> 이 필드의 내용은 문 핸들에 대해서만 정의 되 고 **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 호출 된 후에만 정의 됩니다. 문 핸들이 아닌 SQL_DIAG_CURSOR_ROW_COUNT *DiagIdentifier* 를 사용 하 여 **SQLGetDiagField** 를 호출 하면 SQL_ERROR 반환 됩니다.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR|이는 기본 함수가 실행 한 SQL 문을 설명 하는 문자열입니다. 특정 값에 대해서는이 섹션의 뒷부분에 나오는 "동적 함수 필드 값"을 참조 하세요. 이 필드의 내용은 **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults**를 호출한 후에만 문 핸들에 대해 정의 됩니다. 문 핸들이 아닌 SQL_DIAG_DYNAMIC_FUNCTION *DiagIdentifier* 를 사용 하 여 **SQLGetDiagField** 를 호출 하면 SQL_ERROR 반환 됩니다. **Sqlexecute** 또는 **sqlexecdirect**를 호출 하기 전에이 필드의 값이 정의 되지 않았습니다.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|기본 함수에 의해 실행 된 SQL 문을 설명 하는 숫자 코드입니다. 특정 값에 대해서는이 섹션의 뒷부분에 나오는 "동적 함수 필드 값"을 참조 하세요. 이 필드의 내용은 **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults**를 호출한 후에만 문 핸들에 대해 정의 됩니다. 문 핸들이 아닌 SQL_DIAG_DYNAMIC_FUNCTION_CODE *DiagIdentifier* 를 사용 하 여 **SQLGetDiagField** 를 호출 하면 SQL_ERROR 반환 됩니다. **Sqlexecute** 또는 **sqlexecdirect**를 호출 하기 전에이 필드의 값이 정의 되지 않았습니다.|  
|SQL_DIAG_NUMBER|SQLINTEGER|지정 된 핸들에 사용할 수 있는 상태 레코드의 수입니다.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|함수에서 반환 하는 코드를 반환 합니다. 반환 코드 목록은 [반환 코드](../../../odbc/reference/develop-app/return-codes-odbc.md)를 참조 하세요. 드라이버는 SQL_DIAG_RETURNCODE를 구현할 필요가 없습니다. 항상 드라이버 관리자에 의해 구현 됩니다. *핸들*에 대해 아직 함수가 호출 되지 않은 경우에는 SQL_DIAG_RETURNCODE에 대해 SQL_SUCCESS 반환 됩니다.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|**Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos**에서 수행 하는 insert, delete 또는 update의 영향을 받는 행 수입니다. *커서 사양이* 실행 된 후 드라이버에서 정의 됩니다. 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다. 문 핸들이 아닌 SQL_DIAG_ROW_COUNT *DiagIdentifier* 를 사용 하 여 **SQLGetDiagField** 를 호출 하면 SQL_ERROR 반환 됩니다. 이 필드의 데이터는 **Sqlrowcount**의 *rowcountptr* 인수에도 반환 됩니다. 이 필드의 데이터는 진단이 아닌 함수를 호출할 때마다 다시 설정 되지만 **Sqlrowcount** 에서 반환 되는 행 수는 문이 준비 됨 또는 할당 됨 상태로 다시 설정 될 때까지 동일 하 게 유지 됩니다.|  
  
## <a name="record-fields"></a>레코드 필드  
 다음 표에 나열 된 레코드 필드는 *DiagIdentifier* 인수에 포함 될 수 있습니다.  
  
|DiagIdentifier|반환 형식|반환|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR|이 레코드에서 SQLSTATE 값의 클래스 부분을 정의 하는 문서를 나타내는 문자열입니다. Open Group 및 ISO 호출 수준 인터페이스에 의해 정의 된 모든 SQLSTATEs의 값은 "ISO 9075"입니다. ODBC 관련 SQLSTATEs (SQLSTATE 클래스가 "IM" 인 모든 해당)의 경우 해당 값은 "ODBC 3.0"입니다.|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|SQL_DIAG_ROW_NUMBER 필드가 행 집합 또는 매개 변수 집합의 올바른 행 번호가 면이 필드는 결과 집합의 열 번호 또는 매개 변수 집합의 매개 변수 번호를 나타내는 값을 포함 합니다. 결과 집합 열 번호는 항상 1부터 시작 합니다. 이 상태 레코드가 책갈피 열과 관련 된 경우이 필드는 0이 될 수 있습니다. 매개 변수 번호는 1부터 시작 합니다. 상태 레코드가 열 번호 또는 매개 변수 번호와 연결 되지 않은 경우 SQL_NO_COLUMN_NUMBER 값이 있습니다. 드라이버가이 레코드와 연결 된 열 번호 또는 매개 변수 번호를 확인할 수 없는 경우이 필드의 값은 SQL_COLUMN_NUMBER_UNKNOWN입니다.<br /><br /> 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR|진단 레코드와 관련 된 연결의 이름을 나타내는 문자열입니다. 이 필드는 드라이버에 정의 되어 있습니다. 환경 핸들과 연결 된 진단 데이터 구조 및 연결과 관련이 없는 진단의 경우이 필드는 길이가 0 인 문자열입니다.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR|오류 또는 경고에 대 한 정보 메시지입니다. 이 필드는 [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)에 설명 된 대로 형식이 지정 됩니다. 진단 메시지 텍스트에 대 한 최대 길이는 없습니다.|  
|SQL_DIAG_NATIVE|SQLINTEGER|드라이버/데이터 소스 관련 네이티브 오류 코드입니다. 네이티브 오류 코드가 없으면 드라이버는 0을 반환 합니다.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|이 필드에는 행 집합의 행 번호 또는 상태 레코드와 연결 된 매개 변수 집합의 매개 변수 번호가 포함 됩니다. 행 번호와 매개 변수 번호는 1로 시작 합니다. 이 필드에는이 상태 레코드가 행 번호 또는 매개 변수 번호와 연결 되지 않은 경우 SQL_NO_ROW_NUMBER 값이 있습니다. 드라이버가이 레코드와 연결 된 행 번호 또는 매개 변수 번호를 확인할 수 없는 경우이 필드의 값은 SQL_ROW_NUMBER_UNKNOWN입니다.<br /><br /> 이 필드의 내용은 문 핸들에 대해서만 정의 됩니다.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR|진단 레코드와 관련 된 서버 이름을 나타내는 문자열입니다. SQL_DATA_SOURCE_NAME 옵션을 사용 하 여 **SQLGetInfo** 호출에 대해 반환 되는 값과 같습니다. 환경 핸들과 연결 된 진단 데이터 구조와 서버와 관련이 없는 진단의 경우이 필드는 길이가 0 인 문자열입니다.|  
|SQL_DIAG_SQLSTATE|SQLCHAR|5 자로 된 SQLSTATE 진단 코드입니다. 자세한 내용은 [Sqlstates](../../../odbc/reference/develop-app/sqlstates.md)을 참조 하세요.|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR|SQLSTATE 코드에서 하위 클래스 부분의 정의 부분을 식별 하는 SQL_DIAG_CLASS_ORIGIN와 동일한 형식 및 유효한 값을 가진 문자열입니다. "ODBC 3.0"이 반환 되는 ODBC 관련 SQLSTATES는 다음과 같습니다.<br /><br /> 01S00, 01S01, 01 S 02, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S01, 42S01, 42S01, 42S01, 42S01, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006 IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>동적 함수 필드의 값  
 다음 표에서는 **Sqlexecute** 또는 **sqlexecdirect**를 호출 하 여 실행 되는 각 SQL 문의 유형에 적용 되는 SQL_DIAG_DYNAMIC_FUNCTION 및 SQL_DIAG_DYNAMIC_FUNCTION_CODE 값에 대해 설명 합니다. 드라이버는 나열 된 값에 드라이버 정의 값을 추가할 수 있습니다.  
  
|SQL 문<br /><br /> 될|의 값<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|의 값<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain 문*|"도메인 변경"|SQL_DIAG_ALTER_DOMAIN|  
|*alter table 문*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*어설션 정의*|"어설션 만들기"|SQL_DIAG_CREATE_ASSERTION|  
|*문자 집합-정의*|"문자 집합 만들기"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*데이터 정렬-정의*|"데이터 정렬 만들기"|SQL_DIAG_CREATE_COLLATION|  
|*domainn-정의*|"도메인 만들기"|SQL_DIAG_CREATE_DOMAIN|
|*create-index 문*|"인덱스 만들기"|SQL_DIAG_CREATE_INDEX|  
|*create-table 문*|"CREATE TABLE"|SQL_DIAG_CREATE_TABLE|  
|*create-view-문*|"뷰 만들기"|SQL_DIAG_CREATE_VIEW|  
|*커서 사양*|"커서 선택"|SQL_DIAG_SELECT_CURSOR|  
|*delete-문 배치*|"동적 커서 삭제"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete-문-검색*|"DELETE WHERE"|SQL_DIAG_DELETE_WHERE|  
|*drop assertion 문*|"DROP ASSERTION"|SQL_DIAG_DROP_ASSERTION|  
|*드롭 문자 집합-stmt*|"문자 집합 삭제"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop collation-문*|"데이터 정렬 삭제"|SQL_DIAG_DROP_COLLATION|  
|*drop 도메인 문*|"도메인 삭제"|SQL_DIAG_DROP_DOMAIN|  
|*drop index 문*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop schema 문*|"스키마 삭제"|SQL_DIAG_DROP_SCHEMA|  
|*drop table 문*|"테이블 삭제"|SQL_DIAG_DROP_TABLE|  
|*drop translation 문*|"변환 삭제"|SQL_DIAG_DROP_TRANSLATION|  
|*드롭 뷰-문*|"뷰 삭제"|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|부여|SQL_DIAG_GRANT|
|*insert 문*|넣거나|SQL_DIAG_INSERT|  
|*ODBC-프로시저 확장*|전화할|SQL_DIAG_ 호출|  
|*revoke 문*|해지|SQL_DIAG_REVOKE|  
|*스키마 정의*|"스키마 만들기"|SQL_DIAG_CREATE_SCHEMA|  
|*번역-정의*|"번역 만들기"|SQL_DIAG_CREATE_TRANSLATION|  
|*업데이트-문 배치*|"동적 업데이트 커서"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*업데이트-문-검색*|"업데이트 위치"|SQL_DIAG_UPDATE_WHERE|  
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

 상태 레코드는 행 번호 및 진단 유형에 따라 시퀀스에 배치 됩니다. 드라이버 관리자는 생성 된 상태 레코드를 반환 하는 마지막 순서를 결정 합니다. 드라이버는 생성 하는 상태 레코드를 반환 하는 마지막 순서를 결정 합니다.  
  
 드라이버 관리자와 드라이버에서 진단 레코드를 게시 하는 경우 드라이버 관리자는 순서를 지정 해야 합니다.  
  
 두 개 이상의 상태 레코드가 있는 경우 레코드의 순서는 먼저 행 번호로 결정 됩니다. 다음 규칙은 진단 레코드의 시퀀스를 행별로 확인 하는 데 적용 됩니다.  
  
-   SQL_NO_ROW_NUMBER가-1로 정의 되어 있으므로 행에 해당 하지 않는 레코드는 특정 행에 해당 하는 레코드 앞에 표시 됩니다.  
  
-   SQL_ROW_NUMBER_UNKNOWN가-2로 정의 되어 있으므로 행 번호가 unknown 인 레코드는 다른 모든 레코드 앞에 표시 됩니다.  
  
-   특정 행과 관련 된 모든 레코드에 대해 레코드는 SQL_DIAG_ROW_NUMBER 필드의 값을 기준으로 정렬 됩니다. 영향을 받은 첫 번째 행에 대 한 모든 오류 및 경고가 나열 된 다음 영향을 받는 다음 행의 모든 오류 및 경고가 표시 됩니다.  
  
> [!NOTE]
>  Odbc*3.X 드라이버 관리자* 는 sqlstate 01S01 (행 오류)가 odbc 2.x 드라이버에 의해 반환 되거나, sqlextendedfetch가 호출 되거나 **sqlextendedfetch**를 사용 하 여 배치 된 커서에 대해 **SQLSETPOS** 가 호출 되 면 odbc*2.X 드라이버에서* sqlstate** 01S01 (행 오류 **** )가 반환 되는 경우 진단 큐에서 상태 레코드를 정렬 하지 않습니다.  
  
 각 행 이나 행에 해당 하지 않는 모든 레코드 또는 행 번호를 알 수 없는 모든 레코드의 경우 또는 행 번호가 SQL_NO_ROW_NUMBER와 같은 모든 레코드에 대해 나열 된 첫 번째 레코드는 정렬 규칙 집합을 사용 하 여 결정 됩니다. 첫 번째 레코드 이후 행에 영향을 주는 다른 레코드의 순서는 정의 되지 않습니다. 응용 프로그램은 첫 번째 레코드 뒤에서 오류가 경고 앞에 오는 것으로 간주할 수 없습니다. 응용 프로그램은 전체 진단 데이터 구조를 검색 하 여 함수에 대 한 실패 한 호출에 대 한 전체 정보를 가져와야 합니다.  
  
 다음 규칙은 행 내의 첫 번째 레코드를 확인 하는 데 사용 됩니다. 순위가 가장 높은 레코드는 첫 번째 레코드입니다. 레코드의 원본 (드라이버 관리자, 드라이버, 게이트웨이 등)은 레코드를 순위를 지정 하는 경우 고려 되지 않습니다.  
  
-   **오류** 오류를 설명 하는 상태 레코드의 순위가 가장 높습니다. 정렬 오류에 적용 되는 규칙은 다음과 같습니다.  
  
    -   트랜잭션 실패 또는 가능한 트랜잭션 오류를 나타내는 레코드입니다. 다른 모든 레코드를 표시 합니다.  
  
    -   두 개 이상의 레코드가 동일한 오류 조건을 설명 하는 경우 Open Group CLI 사양 (클래스 03 ~ HZ)에서 정의 된 SQLSTATEs와 드라이버에서 정의한 SQLSTATEs입니다.  
  
-   **구현에서 정의 된 데이터 값 없음** 드라이버 정의 데이터 값 없음 (클래스 02)을 설명 하는 상태 레코드에는 두 번째 최고 순위가 있습니다.  
  
-   **경고** 경고 (클래스 01)를 설명 하는 상태 레코드의 순위가 가장 낮습니다. 두 개 이상의 레코드가 동일한 경고 조건을 설명 하는 경우 Open Group CLI 사양 outrank ODBC 정의 및 드라이버 정의 SQLSTATEs에서 정의 되는 경고 SQLSTATEs입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|진단 데이터 구조의 여러 필드 가져오기|[SQLGetDiagRec 함수](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
