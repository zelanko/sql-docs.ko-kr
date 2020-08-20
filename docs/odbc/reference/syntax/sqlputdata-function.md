---
description: SQLPutData 함수
title: SQLPutData 함수 | Microsoft Docs
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
ms.openlocfilehash: 8adda30141a99c1a575d8cc66511f1606e77dcf5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487136"
---
# <a name="sqlputdata-function"></a>SQLPutData 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlputdata** 를 사용 하면 응용 프로그램에서 문 실행 시 매개 변수 또는 열에 대 한 데이터를 드라이버에 보낼 수 있습니다. 이 함수를 사용 하 여 문자, 이진 또는 데이터 원본 관련 데이터 형식 (예: SQL_LONGVARBINARY 또는 SQL_LONGVARCHAR 형식의 매개 변수)이 있는 열에 문자 또는 이진 데이터 값을 보낼 수 있습니다. **Sqlputdata** 는 기본 드라이버가 유니코드 데이터를 지원 하지 않는 경우에도 유니코드 C 데이터 형식에 대 한 바인딩을 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *DataPtr*  
 입력 매개 변수 또는 열에 대 한 실제 데이터를 포함 하는 버퍼에 대 한 포인터입니다. 데이터는 **SQLBindParameter** 의 *ValueType* 인수 (매개 변수 데이터의 경우) 또는 **SQLBindCol** 의 *TargetType* 인수 (열 데이터)에 지정 된 C 데이터 형식에 있어야 합니다.  
  
 *StrLen_or_Ind*  
 입력 \* *Dataptr*의 길이입니다. **Sqlputdata**에 대 한 호출에서 전송 되는 데이터의 양을 지정 합니다. 데이터의 양은 지정 된 매개 변수 또는 열에 대 한 각 호출에 따라 달라질 수 있습니다. *StrLen_or_Ind* 는 다음 조건 중 하나를 충족 하지 않는 경우 무시 됩니다.  
  
-   *StrLen_or_Ind* SQL_NTS, SQL_NULL_DATA 또는 SQL_DEFAULT_PARAM입니다.  
  
-   **SQLBindParameter** 또는 **SQLBindCol** 에 지정 된 C 데이터 형식은 SQL_C_CHAR 또는 SQL_C_BINARY입니다.  
  
-   C 데이터 형식은 SQL_C_DEFAULT 되며 지정 된 SQL 데이터 형식에 대 한 기본 C 데이터 형식은 SQL_C_CHAR 또는 SQL_C_BINARY입니다.  
  
 다른 모든 유형의 C 데이터에 대해 *StrLen_or_Ind* SQL_NULL_DATA 또는 SQL_DEFAULT_PARAM 되지 않은 경우 드라이버는 \* *Dataptr* 버퍼의 크기가 *ValueType* 또는 *TargetType* 으로 지정 된 C 데이터 형식의 크기인 것으로 가정 하 고 전체 데이터 값을 보냅니다. 자세한 내용은 부록 D: 데이터 형식에서 데이터 [를 C에서 SQL 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 을 참조 하세요.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlputdata** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType* SQL_HANDLE_STMT의 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **Sqlputdata** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|출력 매개 변수에 대해 반환 된 문자열 또는 이진 데이터 때문에 비어 있지 않은 문자 또는 NULL이 아닌 이진 데이터가 잘렸습니다. 문자열 값인 경우 오른쪽이 잘렸습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|바인딩된 매개 변수에 대 한 **SQLBindParameter** 의 *ValueType* 인수에 의해 식별 되는 데이터 값을 **SQLBindParameter**의 *ParameterType* 인수로 식별 된 데이터 형식으로 변환할 수 없습니다.|  
|07S01|기본 매개 변수 사용이 잘못 되었습니다.|**SQLBindParameter**로 설정 된 매개 변수 값이 SQL_DEFAULT_PARAM 되었으며 해당 매개 변수에 기본값이 없습니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|22001|문자열 데이터, 오른쪽 잘림|열에 문자 또는 이진 값을 할당 하 여 비어 있지 않은 (문자) 또는 null이 아닌 (이진) 문자 또는 바이트가 잘렸습니다.<br /><br /> **SQLGetInfo** 의 SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"이 고, 긴 매개 변수에 대 한 추가 데이터 (데이터 형식 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 관련 데이터 형식)가 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수로 지정 된 것 보다 많은 데이터를 보냈습니다.<br /><br /> **SQLGetInfo** 의 SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"이 고, 긴 열 (데이터 형식은 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 관련 데이터 형식)에 대해 **추가 또는 업데이트** 된 데이터 행의 열에 **해당 하는**길이 버퍼에 지정 된 것 보다 많은 데이터를 전송 했습니다.|  
|22003|숫자 값이 범위를 벗어났습니다.|바인딩된 숫자 매개 변수 또는 열에 대해 전송 된 데이터는 연결 된 테이블 열에 할당 될 때 잘린 숫자의 전체 (소수 부분)를 초래 합니다.<br /><br /> 하나 이상의 입력/출력 또는 출력 매개 변수에 대해 숫자 값 (숫자 또는 문자열)을 반환 하면 잘린 숫자의 전체 부분이 소수 부분으로 표시 되지 않습니다.|  
|22007|날짜/시간 형식이 잘못 되었습니다.|날짜, 시간 또는 타임 스탬프 구조에 바인딩된 매개 변수 또는 열에 대해 전송 된 데이터는 각각 잘못 된 날짜, 시간 또는 타임 스탬프입니다.<br /><br /> Input/output 또는 output 매개 변수는 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩되고 반환 된 매개 변수의 값은 각각 잘못 된 날짜, 시간 또는 타임 스탬프입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|22008|Datetime 필드 오버플로|입/출력 또는 출력 매개 변수에 대해 계산 된 datetime 식이 잘못 된 날짜, 시간 또는 타임 스탬프 C 구조를 가져왔습니다.|  
|22012|0으로 나누었습니다.|입/출력 또는 출력 매개 변수에 대해 계산 된 산술 식의 결과로 0으로 나누었습니다.|  
|22015|간격 필드 오버플로입니다.|정확한 숫자 또는 간격 열 이나 매개 변수에 대해 interval SQL 데이터 형식으로 전송 된 데이터를 통해 유효 자릿수가 손실 됩니다.<br /><br /> 데이터가 두 개 이상의 필드를 포함 하는 간격 열 또는 매개 변수에 대해 전송 되었으며 숫자 데이터 형식으로 변환 되었으며 숫자 데이터 형식에는 표시 되지 않았습니다.<br /><br /> 열 또는 매개 변수 데이터에 대해 전송 되는 데이터가 interval SQL 형식에 할당 되었으며 interval SQL 형식에 C 형식의 값이 표시 되지 않았습니다.<br /><br /> 정확한 숫자 또는 간격 C 열 또는 매개 변수에 대해 interval C 형식으로 전송 된 데이터는 유효 자릿수가 손실 되는 원인이 됩니다.<br /><br /> 열 또는 매개 변수 데이터에 대해 전송 된 데이터는 interval C 구조에 할당 되 고 interval 데이터 구조에는 데이터가 표시 되지 않습니다.|  
|22018|캐스트 사양에 대 한 문자 값이 잘못 되었습니다.|C 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. 열의 SQL 형식이 문자 데이터 형식입니다. 열 또는 매개 변수의 값이 바인딩된 C 형식의 올바른 리터럴이 아닙니다.<br /><br /> SQL 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. C 형식이 SQL_C_CHAR 되었습니다. 열 또는 매개 변수의 값이 바인딩된 SQL 형식의 올바른 리터럴이 아닙니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|(DM) 인수가 *Dataptr* 은 null 포인터이 고 *StrLen_or_Ind* 인수가 0, SQL_DEFAULT_PARAM 또는 SQL_NULL_DATA이 아닙니다.|  
|HY010|함수 시퀀스 오류|(DM) 이전 함수 호출은 **Sqlputdata** 또는 **sqlputdata**에 대 한 호출이 아닙니다.<br /><br /> (DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. SQLPutData 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY019|문자 및 이진이 아닌 데이터를 나누어 보냈습니다.|**Sqlputdata** 가 매개 변수 또는 열에 대해 두 번 이상 호출 되었으며 문자, 이진 또는 데이터 원본 관련 데이터 형식이 포함 된 열에 문자 C 데이터를 보내거나 문자, 이진 또는 데이터 원본 관련 데이터 형식의 열로 이진 c 데이터를 전송 하는 데 사용 되지 않았습니다.|  
|HY020|Null 값 연결 시도|**Sqlputdata** 가 SQL_NEED_DATA를 반환 하는 호출에서 두 번 이상 호출 되었으며, 이러한 호출 중 하나에서 *StrLen_or_Ind* 인수에 SQL_NULL_DATA 또는 SQL_DEFAULT_PARAM 포함 되어 있습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|*Dataptr* 인수가 null 포인터가 아닙니다. *StrLen_or_Ind* 인수는 0 보다 작지만 SQL_NTS 또는 SQL_NULL_DATA와 같지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
 SQL 문의 매개 변수에 대 한 데이터를 전송 하는 동안 **Sqlputdata** 를 호출 하는 경우 문 (**Sqlexecute** 또는 **sqlputdata**)을 실행 하기 위해 호출 된 함수에 의해 반환 될 수 있는 SQLSTATE를 반환할 수 있습니다. 업데이트 되거나 **SQLBulkOperations** 를 사용 하 여 추가 되거나 **sqlsetpos**로 업데이트 되는 열에 대 한 데이터를 전송 하는 동안 호출 되는 경우 **SQLBulkOperations** 또는 **sqlsetpos**에서 반환 될 수 있는 SQLSTATE를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 **Sqlputdata** 를 호출 하면 **Sqlexecute** 또는 **sqlputdata**호출에 사용 되는 매개 변수 데이터 또는 **SQLBulkOperations** 를 호출 하 여 행을 업데이트 하거나 추가 하거나 **SQLSetPos**를 호출 하 여 행을 업데이트 하거나 추가할 때 사용할 열 데이터를 실행할 때 데이터를 실행할 수 있습니다.  
  
 응용 프로그램에서 **Sqlparamdata** 를 호출 하 여 보내야 하는 데이터를 결정 하는 경우 드라이버는 응용 프로그램에서 보낼 매개 변수 데이터 또는 열 데이터를 찾을 수 있는 위치를 결정 하는 데 사용할 수 있는 표시기를 반환 합니다. 또한 데이터를 보내기 위해 **Sqlputdata** 를 호출 해야 하는 응용 프로그램에 대 한 지표로 SQL_NEED_DATA 반환 합니다. **Sqlputdata**에 대 한 *dataptr* 인수에서 응용 프로그램은 매개 변수 또는 열에 대 한 실제 데이터를 포함 하는 버퍼에 대 한 포인터를 전달 합니다.  
  
 드라이버가 **Sqlputdata**에 대 한 SQL_SUCCESS를 반환 하는 경우 응용 프로그램은 **sqlputdata** 를 다시 호출 합니다. **Sqlparamdata** 는 추가 데이터를 전송 해야 하는 경우에 SQL_NEED_DATA를 반환 합니다 .이 경우 응용 프로그램은 **sqlparamdata** 를 다시 호출 합니다. 모든 실행 데이터 데이터를 보낸 경우에 SQL_SUCCESS를 반환 합니다. 그러면 응용 프로그램에서 **Sqlparamdata** 를 다시 호출 합니다. 드라이버가 SQL_NEED_DATA을 반환 하 고 다른 표시기를 * \* 이상 값으로 반환*하는 경우 다른 매개 변수 또는 열에 대 한 데이터가 필요 하 고 **sqlputdata** 가 다시 호출 됩니다. 드라이버가 SQL_SUCCESS 반환 하는 경우 모든 실행 시 데이터 데이터가 전송 되 고 SQL 문을 실행 하거나 **SQLBulkOperations** 또는 **SQLSetPos** 호출을 처리할 수 있습니다.  
  
 실행 시 데이터 매개 변수 데이터가 문 실행 시 전달 되는 방법에 대 한 자세한 내용은 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 의 "매개 변수 값 전달" 및 [긴 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)을 참조 하세요. 실행 시 데이터 열 데이터를 업데이트 하거나 추가 하는 방법에 대 한 자세한 내용은 [sqlsetpos](../../../odbc/reference/syntax/sqlsetpos-function.md)의 "sqlsetpos 사용" 및 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)의 "책갈피를 사용 하 여 대량 업데이트 수행" 및 [Long data 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)섹션을 참조 하세요.  
  
> [!NOTE]  
>  문자 C 데이터를 문자, 이진 또는 데이터 원본 관련 데이터 형식이 있는 열로 보내거나 문자, 이진 또는 데이터 원본 관련 데이터 형식이 있는 열에 이진 C 데이터를 보내는 경우에만 응용 프로그램에서 **Sqlputdata** 를 사용 하 여 부분으로 데이터를 보낼 수 있습니다. **Sqlputdata** 가 다른 조건에서 두 번 이상 호출 되는 경우에는 SQL_ERROR 및 SQLSTATE HY019를 반환 합니다. 문자 및 이진이 아닌 데이터는 조각으로 전송 됩니다.  
  
## <a name="example"></a>예제  
 다음 샘플에서는 테스트 라는 데이터 원본 이름을 가정 합니다. 연결 된 데이터베이스에는 다음과 같이 만들 수 있는 테이블이 있어야 합니다.  
  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|매개 변수에 버퍼 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|다음 매개 변수를 반환 하 여 데이터 보내기|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
