---
title: SQLPutData 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPutData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPutData
helpviewer_keywords:
- SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c4e704d96924942812904ea63d0e3d4fce8748e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300043"
---
# <a name="sqlputdata-function"></a>SQLPutData 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLPutData는** 응용 프로그램이 문 실행 시간에 드라이버에 매개 변수 또는 열에 대한 데이터를 보낼 수 있습니다. 이 함수는 문자, 이진 또는 데이터 원본별 데이터 형식(예: SQL_LONGVARBINARY 또는 SQL_LONGVARCHAR 형식의 매개 변수)가 있는 열에 부분적으로 문자 또는 이진 데이터 값을 보내는 데 사용할 수 있습니다. **SQLPutData는** 기본 드라이버가 유니코드 데이터를 지원하지 않는 경우에도 유니코드 C 데이터 형식에 대한 바인딩을 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *데이터 Ptr*  
 [입력] 매개 변수 또는 열에 대한 실제 데이터를 포함하는 버퍼에 대한 포인터입니다. 데이터는 **SQLBindParameter의** ValueType 인수(매개 변수 데이터)의 *값유형* 인수 또는 **SQLBindCol의** *TargetType* 인수(열 데이터의 경우)에 지정된 C 데이터 형식에 있어야 합니다.  
  
 *StrLen_or_Ind*  
 [입력] 데이터 \* *Ptr의*길이 . **SQLPutData**에 대한 호출에서 전송된 데이터의 양을 지정합니다. 데이터 양은 지정된 매개 변수 또는 열에 대한 호출마다 다를 수 있습니다. *StrLen_or_Ind* 다음 조건 중 하나를 충족하지 않는 한 무시됩니다.  
  
-   *StrLen_or_Ind* SQL_NTS, SQL_NULL_DATA 또는 SQL_DEFAULT_PARAM.  
  
-   **SQLBindParameter** 또는 **SQLBindCol에** 지정된 C 데이터 형식은 SQL_C_CHAR 또는 SQL_C_BINARY.  
  
-   C 데이터 형식은 SQL_C_DEFAULT 지정된 SQL 데이터 형식의 기본 C 데이터 형식은 SQL_C_CHAR 또는 SQL_C_BINARY.  
  
 다른 모든 C 데이터의 경우 *StrLen_or_Ind* SQL_NULL_DATA SQL_DEFAULT_PARAM 않은 경우 드라이버는 \* *DataPtr* 버퍼의 크기가 *ValueType* 또는 *TargetType으로* 지정된 C 데이터 형식의 크기라고 가정하고 전체 데이터 값을 보냅니다. 자세한 내용은 부록 D: 데이터 [형식의 C에서 SQL 데이터 유형으로 데이터 변환을](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 참조하십시오.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLPutData** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우, SQL_HANDLE_STMT *핸들 유형* 및 *문 핸들* *핸들을* 사용하여 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLPutData에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|출력 매개 변수에 대해 반환된 문자열 또는 이진 데이터는 비공백 문자 또는 NULL이 아닌 이진 데이터의 잘림을 초래했습니다. 문자열 값인 경우 오른쪽 잘린 값입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|바인딩된 매개 변수에 대 한 **SQLBindParameter의** *ValueType* 인수로 식별 된 데이터 **값은 SQLBindParameter**에서 *ParameterType* 인수에 의해 식별 된 데이터 유형으로 변환할 수 없습니다.|  
|07S01|기본 매개 변수의 잘못된 사용|**SQLBindParameter로**설정된 매개 변수 값이 SQL_DEFAULT_PARAM 해당 매개 변수에 기본값이 없습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|22001|문자열 데이터, 오른쪽 잘림|문자 또는 이진 값을 열에 할당하면 비공백(character) 또는 비널(binary) 문자 또는 바이트가 잘리게 됩니다.<br /><br /> **SQLGetInfo의** SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"이고 **SQLBindParameter에서** *StrLen_or_IndPtr* 인수로 지정된 것보다 긴 매개 변수(데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 별 데이터 형식)에 대해 더 많은 데이터가 전송되었습니다.<br /><br /> **SQLGetInfo의** SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"이고 **SQLBulkOperations로** 추가또는 업데이트된 데이터 행의 열에 해당하는 길이 버퍼에 지정된 것보다 긴 열(데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 **SQLSetPos**별 데이터 형식)에 대해 더 많은 데이터가 전송되었습니다.|  
|22003|범위를 벗어난 숫자 값|바인딩된 숫자 매개 변수 또는 열에 대해 전송된 데이터로 인해 연결된 테이블 열에 할당될 때 숫자의 전체(분수와 반대)가 잘립니다.<br /><br /> 하나 이상의 입력/출력 또는 출력 매개 변수에 대해 숫자 값(숫자 또는 문자열)을 반환하면 숫자의 전체(분수와 반대)가 잘릴 수 있습니다.|  
|22007|잘못된 날짜 시간 형식|날짜, 시간 또는 타임스탬프 구조에 바인딩된 매개 변수 또는 열에 대해 전송된 데이터는 각각 잘못된 날짜, 시간 또는 타임스탬프였습니다.<br /><br /> 입력/출력 또는 출력 매개 변수는 날짜, 시간 또는 타임스탬프 C 구조에 바인딩되었으며 반환된 매개 변수의 값은 각각 잘못된 날짜, 시간 또는 타임스탬프였습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|22008|일시 필드 오버플로|입력/출력 또는 출력 매개 변수에 대해 계산된 datetime 식으로 인해 날짜, 시간 또는 타임스탬프 C 구조가 잘못되었습니다.|  
|22012|0으로 나누기|입력/출력 또는 출력 매개 변수에 대해 계산된 산술 식은 0으로 분할됩니다.|  
|22015|간격 필드 오버플로|정확한 숫자 또는 간격 열 또는 매개 변수에 대해 인터벌 SQL 데이터 형식에 대해 전송된 데이터로 인해 상당한 자릿수가 손실되었습니다.<br /><br /> 필드가 두 개 이상 인 간격 열 또는 매개 변수에 대해 데이터가 전송되고 숫자 데이터 유형으로 변환되었으며 숫자 데이터 형식에 표현이 없습니다.<br /><br /> 열 또는 매개 변수 데이터에 대해 전송된 데이터는 INTERVAL SQL 형식에 할당되었으며 INTERVAL SQL 형식에서 C 형식의 값을 나타내지 않았습니다.<br /><br /> 간격 C 유형으로 정확한 숫자 또는 간격 C 열 또는 매개 변수에 대해 전송된 데이터는 상당한 자릿수의 손실을 일으켰습니다.<br /><br /> 열 또는 매개 변수 데이터에 대해 전송된 데이터는 간격 C 구조에 할당되었으며 간격 데이터 구조에 데이터의 표현이 없었습니다.|  
|22018|캐스트 사양에 대해 잘못된 문자 값|C 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식이었습니다. 열의 SQL 형식은 문자 데이터 형식입니다. 및 열 또는 매개 변수의 값이 바인딩된 C 형식의 유효한 리터럴이 아닙니다.<br /><br /> SQL 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식입니다. C 형은 SQL_C_CHAR. 열 또는 매개 변수의 값이 바인딩된 SQL 형식의 유효한 리터럴이 아닙니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) *인수 DataPtr은* null 포인터이고 *StrLen_or_Ind* 인수는 0, SQL_DEFAULT_PARAM 또는 SQL_NULL_DATA 않았습니다.|  
|HY010|함수 시퀀스 오류|(DM) 이전 함수 호출은 **SQLPutData** 또는 **SQLParamData**에 대한 호출이 아닙니다.<br /><br /> (DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 SQLPutData 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY019|조각으로 전송되는 비문자 및 비이진 데이터|**SQLPutData** 매개 변수 또는 열에 대해 두 번 이상 호출되었으며 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열에 문자 C 데이터를 보내거나 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열에 이진 C 데이터를 보내는 데 사용되지 않았습니다.|  
|HY020|null 값을 연결하려고 시도|**SQLPutData는** SQL_NEED_DATA 반환된 호출 이후 두 번 이상 호출되었으며, 이러한 호출 중 하나에서 *StrLen_or_Ind* 인수에는 SQL_NULL_DATA 또는 SQL_DEFAULT_PARAM 포함되어 있습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|*DataPtr* 인수는 null 포인터가 아니며 *StrLen_or_Ind* 인수는 0보다 작지만 SQL_NTS 또는 SQL_NULL_DATA 같지 않았습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
 **SQLPutData는 SQL** 문에서 매개 변수에 대 한 데이터를 보내는 동안 호출 하는 경우 문을 실행 하기 위해 호출 된 함수에 의해 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다 **(SQLExecute** 또는 **SQLExecDirect).** **SQLBulkOperations로** 업데이트되거나 추가되는 열에 대한 데이터를 보내거나 **SQLSetPos로**업데이트하는 동안 호출되는 경우 **SQLBulkOperations** 또는 **SQLSetPos에서**반환할 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 **SQLPutData는** 두 가지 용도에 대한 실행 시 데이터 데이터를 제공하도록 호출할 수 있습니다: **SQLExecute** 또는 **SQLExecDirect**에 대한 호출에서 사용할 매개 변수 데이터 또는 **SQLBulkOperations** 에 대한 호출에 의해 행이 업데이트되거나 추가되거나 **SQLSetPos**에 대한 호출에 의해 업데이트될 때 사용할 열 데이터  
  
 응용 프로그램이 **SQLParamData를** 호출하여 보낼 데이터를 결정하면 드라이버는 응용 프로그램이 보낼 매개 변수 데이터 또는 열 데이터를 찾을 수 있는 위치를 결정하는 데 사용할 수 있는 표시기를 반환합니다. 또한 데이터를 보내기 위해 **SQLPutData를** 호출해야 하는 응용 프로그램의 표시기인 SQL_NEED_DATA 반환합니다. **SQLPutData에** *DataPtr* 인수에서 응용 프로그램은 매개 변수 또는 열에 대한 실제 데이터를 포함하는 버퍼에 포인터를 전달합니다.  
  
 드라이버가 **SQLPutData에**대한 SQL_SUCCESS 반환하면 응용 프로그램이 **SQLParamData를** 다시 호출합니다. **SQLParamData** 는 더 많은 데이터를 보내야 하는 경우 SQL_NEED_DATA 반환하며, 이 경우 응용 프로그램에서 **SQLPutData를** 다시 호출합니다. 실행 시 모든 데이터가 전송된 경우 SQL_SUCCESS 반환합니다. 그런 다음 응용 프로그램이 **SQLParamData를** 다시 호출합니다. 드라이버가 * \*SQL_NEED_DATA 값PtrPtr의*다른 표시기를 반환하는 경우 다른 매개 변수 또는 열에 대한 데이터가 필요하고 **SQLPutData가** 다시 호출됩니다. 드라이버가 SQL_SUCCESS 반환하면 실행 시 모든 데이터가 전송되고 SQL 문을 실행하거나 **SQLBulkOperations** 또는 **SQLSetPos** 호출을 처리할 수 있습니다.  
  
 명령문 실행 시간에 데이터 실행 매개 변수 데이터가 전달되는 방법에 대한 자세한 내용은 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 및 [긴 데이터 전송의](../../../odbc/reference/develop-app/sending-long-data.md)"매개 변수 값 전달"을 참조하십시오. 실행 시 데이터 열 데이터를 업데이트하거나 추가하는 방법에 대한 자세한 내용은 [SQLSetPos의](../../../odbc/reference/syntax/sqlsetpos-function.md)"SQLSetPos 사용" 섹션, [SQLBulkOperations의](../../../odbc/reference/syntax/sqlbulkoperations-function.md)"책갈피를 사용하여 대량 업데이트 수행" 및 [긴 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)를 참조하십시오.  
  
> [!NOTE]  
>  응용 프로그램은 **SQLPutData를** 사용하여 문자, 바이너리 또는 데이터 원본별 데이터 형식이 있는 열로 문자 C 데이터를 보내거나 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열로 이진 C 데이터를 보낼 때만 부분적으로 데이터를 보낼 수 있습니다. **SQLPutData는** 다른 조건에서 두 번 이상 호출되는 경우 SQL_ERROR 및 SQLSTATE HY019(비문자 및 비이진 데이터로 전송)를 반환합니다.  
  
## <a name="example"></a>예제  
 다음 샘플에서는 Test라는 데이터 원본 이름을 가정합니다. 연결된 데이터베이스에는 다음과 같이 만들 수 있는 테이블이 있어야 합니다.  
  
```sql  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```cpp  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|버퍼를 매개 변수에 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|다음 매개 변수를 반환하여 데이터를|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
