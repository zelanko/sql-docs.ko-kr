---
title: SQLPutData 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cfe33eb04b4948dcba85aa2d9549c301eb65c8a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlputdata-function"></a>SQLPutData 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLPutData** 문 실행 시 드라이버에는 매개 변수 또는 열에 대 한 데이터를 보내는 응용 프로그램을 허용 합니다. 이 함수는 문자, 이진, 또는 데이터 원본에 따른 특정 데이터 형식 (예를 들어 형식의 매개 변수는 SQL_LONGVARBINARY 또는 SQL_LONGVARCHAR)을 가진 열에 부분에 문자 또는 이진 데이터 값을 보내는 데 사용할 수 있습니다. **SQLPutData** 기본 드라이버 유니코드 데이터를 지원 하지 않을 경우에 유니코드 C 데이터 형식에 대 한 바인딩을 지원 합니다.  
  
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
 [입력] 매개 변수 또는 열에 대 한 실제 데이터를 포함 하는 버퍼에 대 한 포인터입니다. 데이터에 지정 된 C 데이터 형식에 있어야 합니다.는 *ValueType* 의 인수 **SQLBindParameter** (데이터용 매개 변수) 또는 *TargetType* 인수의  **SQLBindCol** (데이터용 열)입니다.  
  
 *StrLen_or_Ind*  
 [입력] 길이 \* *DataPtr*합니다. 에 대 한 호출에서 전송 되는 데이터의 양을 지정 **SQLPutData**합니다. 데이터의 양이 지정 된 매개 변수 또는 열에 대 한 각 호출에 달라질 수 있습니다. *StrLen_or_Ind* 다음 조건 중 하나가 충족 하지 않는 경우 무시 됩니다.  
  
-   *StrLen_or_Ind* SQL_NTS, SQL_NULL_DATA, 또는 SQL_DEFAULT_PARAM 합니다.  
  
-   C 데이터 형식에 지정 된 **SQLBindParameter** 또는 **SQLBindCol** SQL_C_CHAR 또는 SQL_C_BINARY 됩니다.  
  
-   C 데이터 형식을 SQL_C_DEFAULT를 이며 지정된 된 SQL 데이터 형식에 대 한 기본 C 데이터 형식은 SQL_C_CHAR 또는 SQL_C_BINARY입니다.  
  
 C 데이터의 다른 모든 형식의 경우 *StrLen_or_Ind* SQL_NULL_DATA 또는 SQL_DEFAULT_PARAM으로 아닙니다 드라이버 가정 하는의 크기는 \* *DataPtr* 버퍼는 지정 된 C 데이터 형식의 크기 와 *ValueType* 또는 *TargetType* 전체 데이터 값을 보냅니다. 자세한 내용은 참조 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 부록 d: 데이터 형식에서입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLPutData** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLPutData** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|문자열 또는 이진 데이터에 대 한 출력 매개 변수 반환 공백이 아닌 문자 또는 NULL이 아닌 이진 데이터 잘림이 발생 했습니다. 문자열 값 경우 오른쪽 잘림 없었습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성 위반|데이터 값으로 식별 된 *ValueType* 인수에 **SQLBindParameter** 바인딩된 매개 변수에서 식별 되는 데이터 형식 변환 하지 못했습니다에 대 한는 *ParameterType*인수 **SQLBindParameter**합니다.|  
|07S01|기본 매개 변수를 잘못 사용 했습니다.|매개 변수 값을 사용 하 여 설정 **SQLBindParameter**SQL_DEFAULT_PARAM으로 되어 해당 매개 변수에 기본값이 없는 합니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|22001|문자열 데이터, 오른쪽이 잘렸습니다.|문자 또는 이진 열 값을 할당 비어 있지 않은 값 (문자) 또는 null이 아닌 (이진) 문자 또는 바이트 잘림이 발생 했습니다.<br /><br /> SQL_NEED_LONG_DATA_LEN 정보 유형을 **SQLGetInfo** "Y"가 되 고 지정한 것 (데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY, 또는 긴 데이터 원본에 따른 특정 데이터 형식) 긴 매개 변수에 대 한 더 많은 데이터가 전송 되었습니다 와 *StrLen_or_IndPtr* 인수 **SQLBindParameter**합니다.<br /><br /> SQL_NEED_LONG_DATA_LEN 정보 유형을 **SQLGetInfo** "Y"가 되 고에 지정 된 것 보다 긴 열 (데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY, 또는 긴 데이터 원본에 따른 특정 데이터 형식)에 대 한 더 많은 데이터가 전송 되었습니다는 추가 되었거나 업데이트 된 데이터의 행에 열에 해당 하는 길이 버퍼 **SQLBulkOperations** 또는와 업데이트 된 **SQLSetPos**합니다.|  
|22003|숫자 값 범위를 벗어났습니다.|데이터 전송에 바인딩된 숫자 매개 변수 또는 열 (소수) 대비 전체 연결 된 테이블 열에 할당 된 경우 잘릴 숫자 부분과 발생 합니다.<br /><br /> 하나 이상의 입/출력 또는 출력 매개 변수 (숫자 또는 문자열)으로 숫자 값을 반환는 발생할 (소수) 대비 전체 부분의 잘릴 수 있습니다.|  
|22007|잘못 된 날짜/시간 형식|매개 변수 또는 날짜, 시간 또는 타임 스탬프 구조에 바인딩된 열에 대 한 전송 되는 데이터를 각각는 잘못 된 날짜, 시간 또는 타임 스탬프입니다.<br /><br /> 날짜, 시간 또는 타임 스탬프 C 구조에는 입/출력 또는 출력 매개 변수가 바인딩된 되었으며 반환 된 매개 변수 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22008|Datetime 필드 오버플로|입력/출력에 대해 계산 된 datetime 식 또는 출력 매개 변수는 날짜, 시간 또는 유효 하지 않는 C 타임 스탬프 구조에서 발생 했습니다.|  
|22012|0으로 나누기|산술 식 입력/출력에 대 한 계산 또는 0으로 나누기에서 발생 한 출력 매개 변수입니다.|  
|22015|간격 필드 오버플로|정확한 숫자 또는 간격 열에 대 한 데이터는 전송 또는 간격 SQL 데이터 형식에 매개 변수 했기 때문에 유효 자릿수의 손실입니다.<br /><br /> 데이터 간격 열 또는 매개 변수를 둘 이상의 필드에 대 한 전송, 숫자 데이터 형식으로 변환 및 숫자 데이터 형식에 나타나지 발생 했습니다.<br /><br /> 열에 대 한 전송 되는 데이터 또는 매개 변수 데이터 간격 SQL 형식에 할당 된 되었으며 간격 SQL 형식에에서 나타나지 C 형식의 값입니다.<br /><br /> 정확한 수치 또는 간격 C 열 또는 매개 변수를 C 간격 유형 전송 되는 데이터 했기 때문에 유효 자릿수의 손실입니다.<br /><br /> 열에 대 한 전송 되는 데이터 또는 매개 변수 데이터는 간격 C 구조에 할당 된 되었으며 간격 데이터 구조에 있는 데이터의 표현을 없습니다.|  
|22018|캐스트 사양의 문자 값|정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식;가 C 유형은 열의 SQL 형식을 문자 데이터 형식. 및 열 또는 매개 변수에서 값 바인딩된 C 형식의 올바른 리터럴 올바르지 않습니다.<br /><br /> SQL 형식 된 정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식입니다. 가 SQL_C_CHAR; C 유형은 및 열 또는 매개 변수에서 값 바인딩된 SQL 형식의 올바른 리터럴 올바르지 않습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) 인수 *DataPtr* null 포인터를 인수 *StrLen_or_Ind* 없습니다 0, SQL_DEFAULT_PARAM으로 또는 SQL_NULL_DATA 합니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) 함수 호출 없습니다에 대 한 호출 **SQLPutData** 또는 **SQLParamData**합니다.<br /><br /> DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. SQLPutData 함수를 호출할 때이 비동기 함수 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY019|문자 및 이진이 아닌 데이터를 나누어 보냈습니다|**SQLPutData** 호출 두 번 이상 매개 변수 또는 열에 대 한 했으며 데이터를 보내는 C 문자는 문자, 이진, 또는 데이터 원본에 따른 특정 데이터 형식이 있는 열 또는 문자 열에 이진 C 데이터를 보내도록 사용 되지 않았습니다 binary 또는 데이터 원본에 따른 특정 데이터 형식입니다.|  
|HY020|Null 값을 연결 하려고 합니다.|**SQLPutData** sql_need_data가 반환 되는 호출 후 및 이러한 호출 중 하나에 두 번 이상 호출한는 *StrLen_or_Ind* 인수 SQL_NULL_DATA 또는 SQL_DEFAULT_PARAM을 포함 합니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수 *DataPtr* 는 null 포인터가 되 고 인수가 없습니다 *StrLen_or_Ind* 가 0 보다 작지만 SQL_NTS 또는 SQL_NULL_DATA 같지 않습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
 경우 **SQLPutData** 호출 되는 SQL 문의 매개 변수에 대 한 데이터를 전송 하는 동안 문을 실행 하는 호출 되는 함수에서 반환 될 수 있는 모든 SQLSTATE 반환할 수 있습니다 (**SQLExecute** 또는 **SQLExecDirect**). 열에 대 한 데이터를 전송 하는 동안 호출 되 면 업데이트 되거나 추가 된 **SQLBulkOperations** 로 업데이트 또는 **SQLSetPos**, 반환할 수 있지만에서 반환 될 수 있는 모든 SQLSTATE  **SQLBulkOperations** 또는 **SQLSetPos**합니다.  
  
## <a name="comments"></a>설명  
 **SQLPutData** 두 가지 용도 대 한 데이터 실행 시 데이터를 제공 하기 위해 호출할 수:에 대 한 호출에 사용할 매개 변수 데이터 **SQLExecute** 또는 **SQLExecDirect**, 또는 행이 업데이트 될 때 사용할 데이터 열 호출 하 여 추가 또는 **SQLBulkOperations** 에 대 한 호출에 의해 업데이트 될 **SQLSetPos**합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLParamData** 데이터 결정을 보내야, 드라이버는 응용 프로그램 매개 변수 데이터를 보낼 결정 하는 데 사용할 수 있는 또는 열 데이터를 찾을 수 있는 표시를 반환 합니다. 또한 호출 해야 하는 응용 프로그램을 나타내는 sql_need_data가 반환 **SQLPutData** 데이터를 보내려고 합니다. 에 *DataPtr* 인수를 **SQLPutData**, 응용 프로그램 매개 변수 또는 열에 대 한 실제 데이터를 포함 하는 버퍼에 대 한 포인터를 전달 합니다.  
  
 드라이버에 대 한 관계 없이 SQL_SUCCESS를 반환 하는 경우 **SQLPutData**, 응용 프로그램 호출 **SQLParamData** 다시 합니다. **SQLParamData** SQL_NEED_DATA 더 많은 데이터를 전송 하는 경우이 경우 응용 프로그램 호출 반환 **SQLPutData** 다시 합니다. 모든 실행 시 데이터 데이터가 플러시된 경우 SQL_SUCCESS를 반환 합니다. 그런 다음 응용 프로그램 호출 **SQLParamData** 다시 합니다. 드라이버 SQL_NEED_DATA 및 다른 표시기를 반환 하는 경우  *\*ValuePtrPtr*, 다른 매개 변수 또는 열에 대 한 데이터를 필요 하 고 **SQLPutData** 를 다시 호출 합니다. 드라이버가 SQL_SUCCESS, 다음 모든 데이터 실행 시를 반환 하는 경우 데이터 전송 되어 하 고 SQL 문을 실행할 수 있습니다 또는 **SQLBulkOperations** 또는 **SQLSetPos** 호출을 처리할 수 있습니다.  
  
 문 실행 시 전달 된 방법 데이터 실행 시 매개 변수 데이터에 대 한 자세한 내용은에서 "매개 변수 값 전달" 참조 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 및 [긴 데이터를 보내는](../../../odbc/reference/develop-app/sending-long-data.md)합니다. 어떻게 데이터 실행 시 열 데이터에 대 한 자세한 내용은 업데이트 되거나 추가 된 섹션을 참조 "를 사용 하 여 SQLSetPos"에서 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "수행 대량 업데이트를 사용 하 여"에서 책갈피 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), 및 [긴 데이터와 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)합니다.  
  
> [!NOTE]  
>  응용 프로그램 צ ְ ײ **SQLPutData** 부분에는 문자, 이진, 또는 데이터 원본에 따른 특정 데이터 형식과 열 C 문자 데이터를 보내는 경우에 또는 문자, 이진 열에 이진 C 데이터를 보낼 때의 데이터 또는 데이터를 전송 원본에 따른 특정 데이터 형식입니다. 경우 **SQLPutData** 라고 두 번 이상 다른 조건에서 반환 하 고 SQLSTATE HY019 SQL_ERROR (아닌 문자 및 이진이 아닌 데이터를 나누어 보냈습니다).  
  
## <a name="example"></a>예제  
 다음 샘플에서는 Test 라는 데이터 원본 이름입니다. 연결된 된 데이터베이스 테이블을 다음과 같이 만들 수 있어야 합니다.  
  
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
|버퍼는 매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|에 대 한 데이터를 보내는 다음 매개 변수를 반환 합니다.|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
