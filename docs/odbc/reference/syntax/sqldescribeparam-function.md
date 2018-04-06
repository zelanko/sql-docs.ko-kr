---
title: SQLDescribeParam 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df8d1653e158f19abf92eb1a650425213cbe393d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 함수(SQLDescribeParam Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLDescribeParam** 준비 된 SQL 문에 연결 된 매개 변수 표식에 대 한 설명을 반환 합니다. 이 정보는 IPD 필드에서 제공 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 매개 변수 표식 번호에서에서 정렬 된 순차적으로 증가 매개 변수 순서 1부터 시작 합니다.  
  
 *DataTypePtr*  
 [출력] 매개 변수의 SQL 데이터 형식을 반환 하는 버퍼에 대 한 포인터입니다. IPD의 SQL_DESC_CONCISE_TYPE 레코드 필드에서이 값을 읽습니다. 값 중 하나가이 됩니다는 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식 또는 드라이버별 SQL 데이터 형식과의 섹션입니다.  
  
 Odbc 3. *x*, SQL_TYPE_DATE SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP에서 반환할  *\*DataTypePtr* 날짜, 시간 또는 타임 스탬프 데이터에 대 한 ODBC 2에서 각각;. *x*, SQL_DATE, SQL_TIME, 또는 SQL_TIMESTAMP 반환 됩니다. 드라이버 관리자 때 ODBC 2 필요한 매핑을 수행 합니다. *x* 응용 프로그램이 작동 ODBC 3. *x* 드라이버 때나 ODBC 3. *x* 응용 프로그램이 작동 ODBC 2. *x* 드라이버입니다.  
  
 때 *ColumnNumber* 같은지 SQL_BINARY에 반환 됩니다 (책갈피 열)에 대해 0으로  *\*DataTypePtr* 가변 길이 책갈피에 대 한 합니다. (SQL_INTEGER는 책갈피가 ODBC 3에서 사용 되는 경우에 반환 됩니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 또는 ODBC 2. *x* 응용 프로그램을 사용 하는 ODBC 3. *x* 드라이버입니다.)  
  
 자세한 내용은 참조 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식에서입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.  
  
 *ParameterSizePtr*  
 [출력] 데이터 원본에 정의 된 대로 크기, 열 또는 해당 매개 변수 표식의 식의 문자를 반환 하는 버퍼에 대 한 포인터입니다. 열 크기에 대 한 자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.  
  
 *DecimalDigitsPtr*  
 [출력] 데이터 원본에 정의 된 대로 열의 소수 자릿수 또는 해당 매개 변수는 식의 수를 반환 하는 버퍼에 대 한 포인터입니다. 10 진수 숫자에 대 한 자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.  
  
 *NullablePtr*  
 [출력] 매개 변수가 NULL 값을 허용 하는지 여부를 나타내는 값을 반환 하는 버퍼에 대 한 포인터입니다. IPD의 SQL_DESC_NULLABLE 필드에서이 값을 읽습니다. 다음 중 하나일 수 있습니다.  
  
-   SQL_NO_NULLS: 매개 변수는 NULL 값 (기본값)를 허용 하지 않습니다.  
  
-   SQL_NULLABLE: 매개 변수는 NULL 값을 허용 합니다.  
  
-   SQL_NULLABLE_UNKNOWN: 드라이버 매개 변수가 NULL 값을 허용 하는지 여부를 확인할 수 없습니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDescribeParam** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 여는 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLDescribeParam** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 대해 지정 된 값 (DM) *ParameterNumber* 1 보다 작으면 합니다.<br /><br /> 인수에 대해 지정 된 값 *ParameterNumber* 연결 된 SQL 문의 매개 변수 개수 보다 큽니다.<br /><br /> 매개 변수 표식이 아닌 DML 문의 일부입니다.<br /><br /> 매개 변수 표식의 일부 였던는 **선택** 목록입니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치 하지 않습니다.|매개 변수 개수는 **삽입** 문을 문에 라는 테이블의 열 수가 일치 하지 않습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) 함수가 호출 하기 전에 호출 된 **SQLPrepare** 또는 **SQLExecDirect** 에 대 한는 *StatementHandle*합니다.<br /><br /> DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLDescribeParam** 함수를 호출 했습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 매개 변수 표식은 SQL 문의 순서 대로 1부터 시작 증가 매개 변수 순서에 번호가 지정 됩니다.  
  
 **SQLDescribeParam** SQL 문에서 매개 변수 유형 (입력, 입/출력 또는 출력)를 반환 하지 않습니다. 제외에 대 한 호출 프로시저에서 SQL 문의 모든 매개 변수에 입력된 매개 변수입니다. 를 프로시저에 대 한 호출에서 각 매개 변수의 형식을 확인 하려면 응용 프로그램이 호출 **SQLProcedureColumns**합니다.  
  
 자세한 내용은 참조 [매개 변수를 설명 하는](../../../odbc/reference/develop-app/describing-parameters.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 SQL 문에 대 한 사용자를 한 다음 해당 문을 준비 합니다. 호출 다음에 **SQLNumParams** 를 문에 매개 변수가 포함 되어 있는지 확인 합니다. 호출 문에 매개 변수가 있으면 **SQLDescribeParam** 이러한 매개 변수를 설명 하 고 **SQLBindParameter** 바인드할 수입니다. 마지막으로 매개 변수 값에 대 한 사용자 요청 하 고 문을 실행 합니다.  
  
```  
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
|버퍼는 매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
