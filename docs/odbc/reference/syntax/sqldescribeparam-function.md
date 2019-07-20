---
title: SQLDescribeParam 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9c1ba115766b820cdcc4f671eeacf9eeec90a894
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345452"
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 함수(SQLDescribeParam Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLDescribeParam** 는 준비 된 SQL 문과 연결 된 매개 변수 표식에 대 한 설명을 반환 합니다. 이 정보는 IPD의 필드 에서도 사용할 수 있습니다.  
  
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
 입력 문 핸들입니다.  
  
 *ParameterNumber*  
 입력 매개 변수 표식 번호는 1부터 시작 하 여 매개 변수 순서에 따라 순차적으로 정렬 됩니다.  
  
 *DataTypePtr*  
 출력 매개 변수의 SQL 데이터 형식을 반환할 버퍼에 대 한 포인터입니다. 이 값은 IPD의 SQL_DESC_CONCISE_TYPE 레코드 필드에서 읽습니다. 이 값은 부록 D의 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 섹션에 있는 값 중 하나입니다. 데이터 형식 또는 드라이버별 SQL 데이터 형식입니다.  
  
 ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP는 각각 DATE, TIME 또는 TIMESTAMP 데이터에 대해  *\*DataTypePtr* 에서 반환 됩니다 (ODBC 2 *의 경우). x*, SQL_DATE, SQL_TIME 또는 SQL_TIMESTAMP이 반환 됩니다. 드라이버 관리자는 ODBC 2를 사용할 때 필요한 매핑을 수행 합니다. *x* 응용 프로그램이 ODBC 3에서 작동 하 고 있습니다. *x* 드라이버 또는 ODBC 3 인 경우 *x* 응용 프로그램에서 ODBC 2를 사용 하 고 있습니다. *x* 드라이버.  
  
 *Columnnumber* 가 0과 같을 때 (책갈피 열) SQL_BINARY는 가변 길이 책갈피에 대 한  *\*DataTypePtr* 으로 반환 됩니다. ODBC 3에서 책갈피를 사용 하는 경우 SQL_INTEGER이 반환 됩니다. ODBC 2를 사용 하 여 작동 하는 *x* 응용 프로그램 *x* 드라이버 또는 ODBC 2. ODBC 3에서 작동 하는 *x* 응용 프로그램입니다. *x* 드라이버)  
  
 자세한 내용은 부록 D의 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) : 데이터 형식. 드라이버별 SQL 데이터 형식에 대 한 자세한 내용은 드라이버 설명서를 참조 하십시오.  
  
 *ParameterSizePtr*  
 출력 데이터 원본에 정의 된 대로 해당 매개 변수 표식의 열 또는 식의 크기 (문자 수)를 반환할 버퍼에 대 한 포인터입니다. 열 크기에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)를 참조 하십시오.  
  
 *DecimalDigitsPtr*  
 출력 데이터 원본에 정의 된 대로 해당 매개 변수의 열 또는 식에 대 한 10 진수 자릿수를 반환할 버퍼에 대 한 포인터입니다. 10 진수에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)를 참조 하십시오.  
  
 *NullablePtr*  
 출력 매개 변수가 NULL 값을 허용 하는지 여부를 나타내는 값을 반환할 버퍼에 대 한 포인터입니다. 이 값은 IPD의 SQL_DESC_NULLABLE 필드에서 읽습니다. 다음 중 하나일 수 있습니다.  
  
-   SQL_NO_NULLS: 매개 변수는 NULL 값을 허용 하지 않습니다 (기본값).  
  
-   SQL_NULLABLE: 매개 변수는 NULL 값을 허용 합니다.  
  
-   SQL_NULLABLE_UNKNOWN: 드라이버에서 매개 변수가 NULL 값을 허용 하는지 여부를 확인할 수 없습니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLDescribeParam** 에서 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType의 SQL_HANDLE_STMT* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLDescribeParam** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR입니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07009|잘못 된 설명자 인덱스|(DM) 인수 *Parameternumber* 에 지정 된 값이 1 보다 작은 경우<br /><br /> 인수 *Parameternumber* 에 지정 된 값이 연결 된 SQL 문의 매개 변수 개수 보다 큽니다.<br /><br /> 매개 변수 표식은 비 DML 문에 속합니다.<br /><br /> 매개 변수 표식은 **SELECT** 목록의 일부입니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치 하지 않습니다.|**INSERT** 문의 매개 변수 수가 문에서 이름이 지정 된 테이블의 열 수와 일치 하지 않습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec에** 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.  *\**|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소 됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*에 대해 **Sqlprepare** 또는 **sqlexecdirect** 를 호출 하기 전에 함수가 호출 되었습니다.<br /><br /> (DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLDescribeParam** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA이 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출에서 SQL_STILL_EXECUTING를 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 매개 변수 표식은 SQL 문에 표시 되는 순서 대로 1부터 시작 하는 매개 변수 순서에 따라 번호가 매겨집니다.  
  
 **SQLDescribeParam** 는 SQL 문에서 매개 변수의 유형 (입력, 입/출력 또는 출력)을 반환 하지 않습니다. 프로시저에 대 한 호출을 제외 하 고 SQL 문의 모든 매개 변수는 입력 매개 변수입니다. 프로시저 호출에서 각 매개 변수의 형식을 확인 하기 위해 응용 프로그램은 **SQLProcedureColumns**를 호출 합니다.  
  
 자세한 내용은 [매개 변수 설명](../../../odbc/reference/develop-app/describing-parameters.md)을 참조 하세요.  
  
## <a name="code-example"></a>코드 예  
 다음 예에서는 사용자에 게 SQL 문을 입력 하 라는 메시지를 표시 한 다음 해당 문을 준비 합니다. 그런 다음 **Sqlnumparams** 를 호출 하 여 문에 매개 변수가 포함 되어 있는지 여부를 확인 합니다. 문에 매개 변수가 포함 되어 있는 경우 **SQLDescribeParam** 를 호출 하 여 이러한 매개 변수를 설명 하 고 **SQLBindParameter** 를 바인딩합니다. 마지막으로 사용자에 게 매개 변수 값을 묻는 메시지를 표시 한 다음 문을 실행 합니다.  
  
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
|매개 변수에 버퍼 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행을 위한 문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
