---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f91799e5d484a763c23fcc132232a8a35fc6152c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52517407"
---
# <a name="sqlputdata-function"></a>SQLPutData 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLPutData** 드라이버 문 실행 시 매개 변수 또는 열에 대 한 데이터를 보내도록 응용 프로그램을 허용 합니다. 이 함수는 문자, 이진 또는 데이터 소스 특정 데이터 형식 (예를 들어, 형식의 매개 변수는 SQL_LONGVARBINARY 또는 SQL_LONGVARCHAR)를 사용 하 여 열에 부분에 문자 또는 이진 데이터 값을 보내는 데 사용할 수 있습니다. **SQLPutData** 기본 드라이버 유니코드 데이터를 지원 하지 않는 경우에 유니코드 C 데이터 형식으로 바인딩을 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *DataPtr*  
 [입력] 매개 변수 또는 열에 대 한 실제 데이터를 포함 하는 버퍼에 대 한 포인터입니다. 데이터에 지정 된 C 데이터 형식에서 이어야 합니다는 *ValueType* 인수의 **SQLBindParameter** (데이터용 매개 변수) 또는 *TargetType* 인수의  **SQLBindCol** (데이터용 열).  
  
 *StrLen_or_Ind*  
 [입력] 길이가 \* *DataPtr*합니다. 에 대 한 호출에서 전송 되는 데이터 양을 지정 **SQLPutData**합니다. 지정 된 매개 변수 또는 열에 대 한 각 호출을 사용 하 여 데이터의 양이 달라질 수 있습니다. *StrLen_or_Ind* 다음 조건 중 하나가 충족 하지 않으면 무시 됩니다.  
  
-   *StrLen_or_Ind* SQL_NTS, SQL_NULL_DATA, 또는 SQL_DEFAULT_PARAM 합니다.  
  
-   지정 된 C 데이터 형식과 **SQLBindParameter** 또는 **SQLBindCol** SQL_C_CHAR 또는 SQL_C_BINARY 합니다.  
  
-   C 데이터 형식은 SQL_C_DEFAULT를 이며 지정된 된 SQL 데이터 형식에 대 한 기본 C 데이터 형식 SQL_C_CHAR 또는 SQL_C_BINARY 합니다.  
  
 C 데이터의 다른 모든 형식의 경우 *StrLen_or_Ind* 없거나 SQL_NULL_DATA SQL_DEFAULT_PARAM으로 드라이버 가정의 크기를 \* *DataPtr* 버퍼 크기가 지정 된 C 데이터 형식 사용 하 여 *ValueType* 하거나 *TargetType* 전체 데이터 값을 보냅니다. 자세한 내용은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 부록 d: 데이터 형식입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLPutData** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLPutData** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|공백이 아닌 문자 또는 NULL이 아닌 이진 데이터의 잘림 문자열 또는 이진 데이터는 출력 매개 변수를 반환 했습니다. 문자열 값이 오른쪽 잘림 이었습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|로 식별 된 데이터 값을 *ValueType* 에서 인수 **SQLBindParameter** 바인딩된 매개 변수에서 식별 되는 데이터 형식 변환 하지 못했습니다에 대 한는 *ParameterType*에 인수 **SQLBindParameter**합니다.|  
|07S01|기본 매개 변수를 잘못 사용 했습니다.|매개 변수 값을 사용 하 여 설정할 **SQLBindParameter**SQL_DEFAULT_PARAM으로 되었으며 해당 매개 변수에 기본값이 없습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|22001|문자열 데이터, 오른쪽이 잘렸습니다.|비어 있지 않은 값 (문자) 또는 null이 아닌 (이진) 문자 또는 바이트 잘리는 문자 또는 이진 값 열에 할당이 했습니다.<br /><br /> SQL_NEED_LONG_DATA_LEN 정보 유형을 **SQLGetInfo** "Y" 되었으며 지정 된 것 보다 긴 매개 변수 (데이터 형식이 SQL_LONGVARBINARY, SQL_LONGVARCHAR, 긴 데이터 소스 특정 데이터 형식)에 대 한 자세한 데이터를 전송 사용 하 여 합니다 *StrLen_or_IndPtr* 에서 인수 **SQLBindParameter**합니다.<br /><br /> SQL_NEED_LONG_DATA_LEN 정보 유형을 **SQLGetInfo** "Y" 되었으며에서 지정 된 것 보다 긴 열 (데이터 형식이 SQL_LONGVARBINARY, SQL_LONGVARCHAR, 긴 데이터 소스 특정 데이터 형식)에 대 한 자세한 데이터를 전송 합니다 열 추가 또는 업데이트 된 데이터 행에 해당 하는 길이 버퍼 **SQLBulkOperations** 으로 업데이트 하거나 **SQLSetPos**합니다.|  
|22003|숫자 값 범위를 벗어났습니다.|데이터 바인딩된 숫자 매개 변수에 대 한 전송 또는 열 (소수) 대신 전체 부분을 잘릴 숫자를 연결 된 테이블 열에 할당 된 경우 발생 합니다.<br /><br /> 하나 이상의 입/출력 또는 출력 매개 변수의 숫자 값 (숫자 또는 문자열)으로 반환 되 었어야 하지만 (소수) 대신 전체 부분 숫자를 자를 수입니다.|  
|22007|잘못 된 날짜/시간 형식|매개 변수 또는 날짜, 시간 또는 타임 스탬프 구조에 바인딩된 열에 대 한 전송 된 데이터를 각각는 잘못 된 날짜, 시간 또는 타임 스탬프입니다.<br /><br /> 입/출력 또는 출력 매개 변수를 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩 되었습니다 및 반환된 매개 변수 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22008|Datetime 필드 오버플로|입/출력에 대해 계산 된 datetime 식 또는 출력 매개 변수는 날짜, 시간 또는 타임 스탬프 C 구조에 잘못 된 발생 합니다.|  
|22012|0으로 나누기|입/출력에 대 한 계산 된 산술 식 또는 출력 매개 변수가 0으로 나누기 했습니다.|  
|22015|간격 필드 오버플로|정확한 숫자 또는 간격 열의 데이터가 전송 또는 간격 SQL 데이터 형식에 매개 변수 했기 때문에 유효 자릿수 손실입니다.<br /><br /> 데이터는 간격 열 이나 매개 변수에 둘 이상의 필드를 사용 하 여 전송 된, 숫자 데이터 형식으로 변환 된 및 숫자 데이터 형식에서으로 표시 되지 했습니다.<br /><br /> 열에 대 한 전송 된 데이터 나 매개 변수 데이터를 간격 SQL 형식에 할당 된 이며 간격 SQL 형식 표현 방식이 없기 C 형식의 값입니다.<br /><br /> 정확한 수치 또는 간격 C 열 또는 매개 변수는 간격 C 형식으로 전송 되는 데이터 유효 자릿수 손실이 발생 합니다.<br /><br /> 열에 대 한 전송 된 데이터 나 매개 변수 데이터를 C 간격 구조에 할당 된 및 간격 데이터 구조의 데이터를에서 표현 방식이 없기 했습니다.|  
|22018|캐스트 사양의 문자 값|C 형식이는 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식 열의 SQL 형식이 된 문자 데이터 형식입니다. 및 열 또는 매개 변수에서 값이 바인딩된 C 형식의 유효한 리터럴입니다.<br /><br /> SQL 형식이는 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식 C 형식을 SQL_C_CHAR; 하는 열 또는 매개 변수에서 값을 바인딩된 SQL 형식의 올바른 리터럴 없습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) 인수 *DataPtr* 가 null 포인터와 인수의 *StrLen_or_Ind* 없습니다 SQL_DEFAULT_PARAM으로 또는 SQL_NULL_DATA, 0입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)는 이전 함수 호출이 실패 했음을에 대 한 호출 **SQLPutData** 하거나 **SQLParamData**합니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수 SQLPutData 함수가 호출 되었을 때 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY019|문자 및 이진이 아닌 데이터를 나누어 보냈습니다|**SQLPutData** 라는 두 번 이상 매개 변수 또는 열에 대 한 되었으며 문자, 이진 또는 데이터 소스 특정 데이터 형식의 열에 문자 데이터를 보내도록 또는 문자를 사용 하 여 열에 이진 C 데이터를 보내도록 사용 하지 않았습니다 이진 또는 데이터 소스 특정 데이터 형식입니다.|  
|HY020|Null 값을 연결 하려고 합니다.|**SQLPutData** SQL_NEED_DATA를 반환 하는 호출 후 및 이러한 호출 중 하나에서 두 번 이상 호출한 합니다 *StrLen_or_Ind* SQL_NULL_DATA 또는 SQL_DEFAULT_PARAM 인수 포함 합니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수 *DataPtr* null 포인터와 인수의 없습니다 *StrLen_or_Ind* 0 보다 작지만 같지 SQL_NTS 또는 SQL_NULL_DATA 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
 경우 **SQLPutData** 호출 되는 SQL 문의 매개 변수에 대해 데이터를 전송 하는 동안 문을 실행 하기 위해 호출 함수에서 반환 될 수 있는 모든 SQLSTATE 반환할 수 있습니다 (**SQLExecute** 또는**SQLExecDirect**). 열에 대 한 데이터를 전송 하는 동안 호출 되 면 업데이트 되거나 추가 된 **SQLBulkOperations** 으로 업데이트 하거나 **SQLSetPos**에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다  **SQLBulkOperations** 나 **SQLSetPos**합니다.  
  
## <a name="comments"></a>주석  
 **SQLPutData** 두 가지 사용에 대 한 데이터 실행 시 데이터를 제공 하기 위해 호출할 수:에 대 한 호출에 사용할 매개 변수 데이터 **SQLExecute** 하거나 **SQLExecDirect**, 또는 행이 업데이트 될 때 사용할 데이터 열 호출 하 여 추가 하거나 **SQLBulkOperations** 에 대 한 호출에 의해 업데이트 될 **SQLSetPos**합니다.  
  
 응용 프로그램을 호출할 때 **SQLParamData** 데이터를 결정 보내야, 드라이버 응용 프로그램 매개 변수 데이터를 보내는 결정 하는 데 사용할 수 있는 또는 열 데이터를 찾을 수 있는 표시기를 반환 합니다. 또한 호출 해야 하는 응용 프로그램에서 표시기는 SQL_NEED_DATA를 반환 합니다 **SQLPutData** 데이터를 보냅니다. 에 *DataPtr* 인수 **SQLPutData**, 응용 프로그램 매개 변수 또는 열에 대 한 실제 데이터를 포함 하는 버퍼에 대 한 포인터를 전달 합니다.  
  
 드라이버에 대 한 관계 없이 SQL_SUCCESS를 반환 하는 경우 **SQLPutData**를 호출 하 여 응용 프로그램 **SQLParamData** 다시 합니다. **SQLParamData** sql_need_data가 더 많은 데이터를 전송 해야 하는 경우는 경우 응용 프로그램이 호출 반환 **SQLPutData** 다시 합니다. 모든 실행 시 데이터 데이터가 전송 된 경우와 관계 없이 SQL_SUCCESS를 반환 합니다. 그런 다음 응용 프로그램 호출 **SQLParamData** 다시 합니다. 드라이버 SQL_NEED_DATA 및 다른 표시기를 반환 하는 경우  *\*ValuePtrPtr*, 다른 매개 변수 또는 열에 대 한 데이터를 필요 하 고 **SQLPutData** 가 다시 호출 합니다. 드라이버가 SQL_SUCCESS, 그런 다음 모든 데이터 실행 시를 반환 하는 경우 데이터 전송 되어 하 고 SQL 문을 실행할 수 있습니다 또는 **SQLBulkOperations** 하거나 **SQLSetPos** 호출을 처리할 수 있습니다.  
  
 문 실행 시이 방법은 어떻게 데이터 실행 시 매개 변수 데이터 전달 된에 대 한에서 "매개 변수 값 전달"을 참조 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 하 고 [긴 데이터를 보내는](../../../odbc/reference/develop-app/sending-long-data.md)합니다. 어떻게 데이터 실행 시 열 데이터에 대 한 자세한 내용은 업데이트 하거나 추가 "를 사용 하 여 SQLSetPos" 섹션의 참조 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "수행 대량 업데이트를 사용 하 여"에서 책갈피 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), 및 [Long 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)합니다.  
  
> [!NOTE]  
>  응용 프로그램에서 사용할 수 있습니다 **SQLPutData** 부분이 나 문자를 이진 열에 이진 C 데이터를 보낼 때 문자, 이진 또는 데이터 소스 특정 데이터 형식의 열에 문자 데이터를 전송 하는 경우에 데이터 또는 데이터를 보내려면 원본 관련 데이터 형식입니다. 하는 경우 **SQLPutData** 라고 두 번 이상 기타 조건에서 SQL_ERROR 및 반환 SQLSTATE HY019 (문자 및 이진이 아닌 데이터를 나누어 보냈습니다).  
  
## <a name="example"></a>예제  
 다음 샘플에서는 Test 라는 데이터 원본 이름을 가정 합니다. 연결된 된 데이터베이스 테이블을 다음과 같이 만들 수 있어야 합니다.  
  
```  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼 매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|에 대 한 데이터를 보내도록 다음 매개 변수를 반환 합니다.|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
