---
title: SQLDescribeParam 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be6d076ca121923a4b6769c7dad5269c3fd642ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301163"
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 함수(SQLDescribeParam Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLDescribeParam** 준비된 SQL 문과 관련 된 매개 변수 마커에 대 한 설명을 반환 합니다. 이 정보는 IPD 의 필드에서도 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *매개 변수 번호*  
 [입력] 매개 변수 마커 번호는 1부터 시작하여 증가하는 매개 변수 순서로 순차적으로 정렬됩니다.  
  
 *데이터 타이핑 Ptr*  
 [출력] 매개 변수의 SQL 데이터 형식을 반환할 버퍼에 대한 포인터입니다. 이 값은 IPD의 SQL_DESC_CONCISE_TYPE 레코드 필드에서 읽습니다. 이 값은 부록 D: 데이터 형식 또는 드라이버 별 SQL 데이터 형식의 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 섹션의 값 중 하나입니다.  
  
 ODBC 3. *x,* SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP 날짜, 시간 또는 타임스탬프 데이터에 대해 * \*DataTypePtr에서* 각각 반환됩니다. ODBC 2에서. *x,* SQL_DATE, SQL_TIME 또는 SQL_TIMESTAMP 반환됩니다. 드라이버 관리자는 ODBC 2때 필요한 매핑을 수행합니다. *x* 응용 프로그램이 ODBC 3로 작동합니다. *x* 드라이버 또는 ODBC 3. *x* 응용 프로그램이 ODBC 2로 작동합니다. *x* 드라이버.  
  
 *ColumnNumber가* 책갈피 열의 경우 0이면 SQL_BINARY 가변 길이 책갈피의 * \*경우 DataTypePtr에서* 반환됩니다. (odBC 3에서 책갈피를 사용하는 경우 SQL_INTEGER 반환됩니다. *x* 응용 프로그램은 ODBC 2로 작업합니다. *x* 드라이버 또는 ODBC 2에 의해. *x* 응용 프로그램은 ODBC 3로 작업합니다. *x* 드라이버.)  
  
 자세한 내용은 부록 D: 데이터 [형식의 SQL 데이터](../../../odbc/reference/appendixes/sql-data-types.md) 유형을 참조하십시오. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오.  
  
 *매개 변수크기Ptr*  
 [출력] 데이터 원본에 의해 정의된 해당 매개 변수 마커의 열 또는 식의 크기( 문자) 또는 식을 반환할 버퍼에 대한 포인터입니다. 열 크기에 대한 자세한 내용은 [열 크기, 소수 자릿수, 옥텟 전사 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.  
  
 *소수 자릿수Ptr*  
 [출력] 데이터 원본에 의해 정의된 해당 매개 변수의 열 또는 식의 소수 자릿수 또는 식을 반환하는 버퍼에 대한 포인터입니다. 소수 자릿수에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.  
  
 *널러블 Ptr*  
 [출력] 매개 변수가 NULL 값을 허용하는지 여부를 나타내는 값을 반환하는 버퍼에 대한 포인터입니다. 이 값은 IPD의 SQL_DESC_NULLABLE 필드에서 읽습니다. 다음 중 하나  
  
-   SQL_NO_NULLS: 매개 변수는 NULL 값을 허용하지 않습니다(기본값입니다).  
  
-   SQL_NULLABLE: 매개 변수는 NULL 값을 허용합니다.  
  
-   SQL_NULLABLE_UNKNOWN: 드라이버는 매개 변수가 NULL 값을 허용하는지 여부를 확인할 수 없습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLDescribeParam** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *문 핸들*핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. *Handle* 다음 표에서는 **SQLDescribeParam에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07009|잘못된 설명자 인덱스|(DM) 인수 *ParameterNumber에* 대해 지정된 값은 1보다 적습니다.<br /><br /> ParameterNumber 인수에 *ParameterNumber* 대해 지정된 값은 연결된 SQL 문의 매개 변수 수보다 큽합니다.<br /><br /> 매개 변수 마커는 DML이 아닌 문의 일부였습니다.<br /><br /> 매개 변수 마커가 **SELECT** 목록의 일부였습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치하지 않음|**INSERT** 문의 매개 변수 수가 명령문에 지정된 테이블의 열 수와 일치하지 않습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 함수는 **SQLPrepare** 또는 **SQLExecDirect** *를 호출하기*전에 호출되었습니다.<br /><br /> (DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLDescribeParam** 함수가 호출될 때 이 비동기 함수가 계속 실행중이었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 매개 변수 마커는 SQL 문에 나타나는 순서대로 1부터 증가하는 매개 변수 순서로 번호가 매겨져 있습니다.  
  
 **SQLDescribeParam은** SQL 문에서 매개 변수의 형식(입력, 입력/출력 또는 출력)을 반환하지 않습니다. 프로시저 호출을 제외하고 SQL 문의 모든 매개 변수는 입력 매개 변수입니다. 프로시저 호출에서 각 매개 변수의 형식을 확인하려면 응용 프로그램에서 **SQLProcedureColumns 를 호출합니다.**  
  
 자세한 내용은 [매개 변수 설명을](../../../odbc/reference/develop-app/describing-parameters.md)참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 다음 예제는 SQL 문을 사용자에게 묻는 메시지를 표시한 다음 해당 문을 준비합니다. 그런 다음 **SQLNumParams을** 호출하여 명령문에 매개 변수가 포함되어 있는지 여부를 확인합니다. 문에 매개 변수가 포함되어 있는 경우 **SQLDescribeParam을** 호출하여 해당 매개 변수와 **SQLBindParameter를** 바인딩합니다. 마지막으로 매개 변수의 값을 사용자에게 묻는 메시지를 표시한 다음 문을 실행합니다.  
  
```cpp  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|버퍼를 매개 변수에 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행을 위한 명령문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
