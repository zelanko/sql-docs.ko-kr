---
title: SQLDescribeParam 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e810d2e7ff3f69faea5fdcbccbb7f7ba276df48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537620"
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 함수(SQLDescribeParam Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLDescribeParam** 준비 된 SQL 문과 사용 하 여 연결 하는 매개 변수 표식에 대 한 설명을 반환 합니다. 이 정보는 IPD 필드에도 사용할 수 있습니다.  
  
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
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *ParameterNumber*  
 [입력] 매개 변수 표식 번호 정렬 순차적으로 증가 매개 변수 순서에 1에서 시작 합니다.  
  
 *DataTypePtr*  
 [출력] 매개 변수의 SQL 데이터 형식을 반환 하는 버퍼에 대 한 포인터입니다. IPD의 SQL_DESC_CONCISE_TYPE 레코드 필드에서이 값을 읽습니다. 에 있는 값 중 하나일 수는이 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 섹션의 부록 d: 데이터 형식 또는 드라이버별 SQL 데이터 형식입니다.  
  
 Odbc 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP에서 반환될지  *\*DataTypePtr* 날짜, 시간 또는 타임 스탬프 데이터에 대 한 ODBC 2에서 각각;. *x*, SQL_DATE, SQL_TIME, 또는 SQL_TIMESTAMP 반환 됩니다. 드라이버 관리자는 ODBC 2 때 필요한 매핑을 수행 합니다. *x* 응용 프로그램이 작동을 ODBC 3. *x* 드라이버 때나는 ODBC 3. *x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 합니다. *x* 드라이버입니다.  
  
 때 *ColumnNumber* 같은지 SQL_BINARY 반환 됩니다 (책갈피 열)에 대해 0으로  *\*DataTypePtr* 가변 길이 책갈피에 대 한 합니다. (SQL_INTEGER는 책갈피가 ODBC 3에서 사용 되는 경우에 반환 됩니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 또는 ODBC 2. *x* 응용 프로그램을 사용 하는 ODBC 3. *x* 드라이버입니다.)  
  
 자세한 내용은 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.  
  
 *ParameterSizePtr*  
 [출력] 데이터 원본에 의해 정의 된 대로 열 또는 식의 해당 매개 변수 표식 문자 크기를 반환 하는 버퍼에 대 한 포인터입니다. 열 크기에 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.  
  
 *DecimalDigitsPtr*  
 [출력] 데이터 원본에 의해 정의 된 대로 해당 매개 변수의 식이나 열의 10 진수의 수를 반환 하는 버퍼에 대 한 포인터입니다. 소수 자릿수에 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.  
  
 *NullablePtr*  
 [출력] 매개 변수에 NULL 값을 허용 하는지 여부를 나타내는 값을 반환 하는 버퍼에 대 한 포인터입니다. IPD의 SQL_DESC_NULLABLE 필드에서이 값을 읽습니다. 다음 중 하나일 수 있습니다.  
  
-   SQL_NO_NULLS: 매개 변수는 NULL 값 (이 값은 기본값)를 허용 하지 않습니다.  
  
-   SQL_NULLABLE: 매개 변수는 NULL 값을 허용 합니다.  
  
-   SQL_NULLABLE_UNKNOWN: 드라이버는 매개 변수에 NULL 값을 허용 하는지 여부를 확인할 수 없습니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDescribeParam** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLDescribeParam** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 지정 된 값 (DM) *상태로* 가 1 미만입니다.<br /><br /> 인수에 지정 된 값 *상태로* 연결된 된 SQL 문 매개 변수 개수 보다 큽니다.<br /><br /> 매개 변수 표식에서 비 DML 문의 일부입니다.<br /><br /> 매개 변수 표식 된 부분을 **선택** 목록입니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치 하지 않습니다.|매개 변수 개수는 **삽입** 문을 문에서 지정 된 테이블의 열 수가 일치 하지 않습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) 함수를 호출한 호출 하기 전에 **SQLPrepare** 하거나 **SQLExecDirect** 에 대 한 합니다 *StatementHandle*합니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLDescribeParam** 함수를 호출 했습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 매개 변수 표식은 SQL 문에 표시 되는 순서 대로 1부터 증가 매개 변수 순서 대로 번호가 지정 됩니다.  
  
 **SQLDescribeParam** SQL 문에서 매개 변수 형식 (입력, 입/출력 또는 출력)를 반환 하지 않습니다. 제외 하 고 프로시저에 대 한 호출 SQL 문의 모든 매개 변수에 입력된 매개 변수입니다. 응용 프로그램이 호출 된 프로시저 호출에서 각 매개 변수의 형식을 결정할 **SQLProcedureColumns**합니다.  
  
 자세한 내용은 [매개 변수를 설명 하는](../../../odbc/reference/develop-app/describing-parameters.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 SQL 문에 대 한 사용자를 다음 해당 문을 준비 합니다. 다음으로 호출 **SQLNumParams** 문에 매개 변수를 포함 하는지 여부를 확인 하려면. 호출 문에 매개 변수가 있으면 **SQLDescribeParam** 이러한 매개 변수를 설명 하 고 **SQLBindParameter** 에 바인딩해야 합니다. 마지막으로 모든 매개 변수 값에 대 한 라는 메시지를 하 고 문을 실행 합니다.  
  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼 매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
