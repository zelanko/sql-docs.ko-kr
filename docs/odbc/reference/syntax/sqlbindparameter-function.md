---
title: "SQLBindParameter 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLBindParameter
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLBindParameter
helpviewer_keywords: SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
caps.latest.revision: "52"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 299e4ced3e6047f7d3e205d384d3191d43e70ef1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 함수
**규칙**  
 도입 된 버전: ODBC 2.0 표준 준수: ODBC  
  
 **요약**  
 **SQLBindParameter** 버퍼는 SQL 문의 매개 변수 표식에 바인딩합니다. **SQLBindParameter** 기본 드라이버 유니코드 데이터를 지원 하지 않을 경우에 유니코드 C 데이터 형식에 대 한 바인딩을 지원 합니다.  
  
> [!NOTE]  
>  이 함수는 ODBC 1.0 함수를 대체 **SQLSetParam**합니다. 자세한 내용은 "설명"을 참조 하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *ParameterNumber*  
 [입력] 매개 변수 번호 순서가 지정 된 순차적으로 증가 매개 변수 순서에 1부터 시작 합니다.  
  
 *InputOutputType*  
 [입력] 형식 매개 변수입니다. 자세한 내용은 참조 하십시오. "*InputOutputType* 인수"에서 "설명"입니다.  
  
 *ValueType*  
 [입력] C 데이터 형식 매개 변수입니다. 자세한 내용은 참조 하십시오. "*ValueType* 인수"에서 "설명"입니다.  
  
 *ParameterType*  
 [입력] SQL 데이터 형식 매개 변수입니다. 자세한 내용은 참조 하십시오. "*ParameterType* 인수"에서 "설명"입니다.  
  
 *ColumnSize*  
 [입력] 크기는 열 또는 식의 해당 매개 변수 표식입니다. 자세한 내용은 참조 하십시오. "*ColumnSize* 인수"에서 "설명"입니다.  
  
 를 64 비트 Windows 운영 체제에서 응용 프로그램를 실행 하는 경우 참조 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)합니다.  
  
 *DecimalDigits*  
 [입력] 열 또는 해당 매개 변수 표식의 식의 10 진수입니다. 열 크기에 대 한 자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.  
  
 *ParameterValuePtr*  
 [지연 된 입력] 매개 변수의 데이터에 대 한 버퍼에 대 한 포인터입니다. 자세한 내용은 참조 하십시오. "*ParameterValuePtr* 인수"에서 "설명"입니다.  
  
 *BufferLength*  
 [입력/출력] 길이 *ParameterValuePtr* 버퍼의 바이트입니다. 자세한 내용은 참조 하십시오. "*BufferLength* 인수"에서 "설명"입니다.  
  
 참조 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우.  
  
 *StrLen_or_IndPtr*  
 [지연 된 입력] 매개 변수의 길이 대 한 버퍼에 대 한 포인터입니다. 자세한 내용은 참조 하십시오. "*StrLen_or_IndPtr* 인수"에서 "설명"입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLBindParameter** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 여는 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLBindParameter** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성 위반|으로 식별 되는 데이터 형식에서 *ValueType* 인수에서 식별 되는 데이터 형식으로 변환할 수 없습니다는 *ParameterType* 인수입니다. 이 오류를 반환할 수 있습니다는 **SQLExecDirect**, **SQLExecute**, 또는 **SQLPutData** 순서가 아니라 실행 시 **SQLBindParameter**.|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 대해 지정 된 값 (DM) *ParameterNumber* 1 미만입니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 **MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|잘못 된 응용 프로그램 버퍼 형식|인수로 지정한 값 *ValueType* 유효한 C 데이터 형식 또는 SQL_C_DEFAULT 없습니다.|  
|HY004|잘못 된 SQL 데이터 형식|인수에 대해 지정 된 값 *ParameterType* 유효한 ODBC SQL 데이터 형식 식별자도 아니고 드라이버에서 지 원하는 드라이버별 SQL 데이터 형식 식별자가 있습니다.|  
|HY009|잘못 된 인수 값|(DM) 인수 *ParameterValuePtr* 인수는 null 포인터 *StrLen_or_IndPtr* null 포인터를 인수 *InputOutputType* SQL_PARAM_ 없습니다 출력입니다.<br /><br /> (DM) SQL_PARAM_OUTPUT 여기서 인수 *ParameterValuePtr* 는 null 포인터 char 또는 binary, 및는 BufferLength가 C 유형은 (*cbValueMax*) 0 보다 큽니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때 **SQLBindParameter** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY021|일관성 없는 설명자 정보|일관성 확인을 하는 동안 체크 설명자 정보 일관 되지 않았습니다. ("일관성 검사" 섹션을 참조 **SQLSetDescField**.)<br /><br /> 인수에 대해 지정 된 값 *DecimalDigits* 로 지정 된 SQL 데이터 형식의 열에 대 한 데이터 원본에 의해 지원 되는 값의 범위 밖에 *ParameterType* 인수입니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM)에 있는 값 *BufferLength* 0 보다 작습니다. (에 SQL_DESC_DATA_PTR 필드의 설명을 참조 **SQLSetDescField**.)|  
|HY104|잘못 된 정밀도 또는 배율 값|인수에 대해 지정 된 값 *ColumnSize* 또는 *DecimalDigits* 로 지정 된 SQL 데이터 형식의 열에 대 한 데이터 원본에 의해 지원 되는 값의 범위 밖에  *ParameterType* 인수입니다.|  
|HY105|잘못 된 매개 변수 형식|인수에 대해 지정 된 값 (DM) *InputOutputType* 올바르지 않습니다. ("주석" 참조)|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 지원 하지 않는 인수에 대해 지정 된 값의 조합에 의해 지정 된 변환을 *ValueType* 및 인수에 대해 지정 된 드라이버 관련 값 *ParameterType*.<br /><br /> 인수에 대해 지정 된 값 *ParameterType* ODBC의 버전 드라이버에서 지원 되지만 드라이버 또는 데이터 원본에서 지원 하지 않아 유효한 ODBC SQL 데이터 형식 식별자가 있습니다.<br /><br /> 드라이버는 ODBC 2만 지원합니다. *x* 인수 *ValueType* 다음 중 하나 였습니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 에 나열 된 모든 간격 C 데이터 형식 및 [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식에서입니다.<br /><br /> 드라이버 지원 3.50, 및 인수는 이전 ODBC 버전 *ValueType* SQL_C_GUID 되었습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램이 호출 **SQLBindParameter** 하는 SQL 문의 각 매개 변수 표식을 바인딩합니다. 바인딩은 응용 프로그램 호출할 때까지 적용 되지 않고 **SQLBindParameter** 다시 호출 **SQLFreeStmt** SQL_RESET_PARAMS 옵션 또는 호출 **SQLSetDescField** 를 APD의 SQL_DESC_COUNT 헤더 필드를 0으로 설정 합니다.  
  
 매개 변수에 대 한 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다. 매개 변수 데이터 형식 및 매개 변수 표식에 대 한 자세한 내용은 참조 [매개 변수 데이터 형식](../../../odbc/reference/appendixes/parameter-data-types.md) 및 [매개 변수 표식을](../../../odbc/reference/appendixes/parameter-markers.md) 부록 c: SQL 문법에 있습니다.  
  
## <a name="parameternumber-argument"></a>ParameterNumber 인수  
 경우 *ParameterNumber* 에 대 한 호출에서 **SQLBindParameter** SQL_DESC_COUNT의 값 보다 크면 **SQLSetDescField** SQL_DESC_의 값 늘리기 위해 호출 됩니다 카운트를 *ParameterNumber*합니다.  
  
## <a name="inputoutputtype-argument"></a>InputOutputType 인수  
 *InputOutputType* 매개 변수 형식의 인수를 지정 합니다. 이 인수는 IPD의 DESC_PARAMETER_TYPE 필드를 설정 합니다. 와 같은 프로시저를 호출 하지 않는 SQL 문의 모든 매개 변수에 **삽입** 문의 *입력**매개 변수*합니다. 프로시저 호출에서 매개 변수 입력 될 수, 입/출력 또는 출력 매개 변수입니다. (응용 프로그램이 호출 **SQLProcedureColumns** ; 프로시저 호출에서 매개 변수의 형식을 확인 하려면 해당 유형을 확인할 수 없는 매개 변수 입력된 매개 변수를 것으로 간주 됩니다.)  
  
 *InputOutputType* 인수는 다음 값 중 하나입니다.  
  
-   SQL_PARAM_INPUT 합니다. 매개 변수 표시와 같은 프로시저를 호출 하지 않는 SQL 문에서 매개 변수는 **삽입** 문 또는 그 프로시저에서 입력된 매개 변수를 표시 합니다. 예를 들어, 매개 변수 **직원 값으로 삽입 (?,?,?)**  입력된 매개 변수는 매개 변수 **{AddEmp 호출 (?,?,?)을 (를)**  될 수 있지만 입력된 매개 변수가 필요 합니다.  
  
     드라이버; 데이터 원본에는 매개 변수에 대 한 데이터를 보냅니다는 문이 실행 될 때 \* *ParameterValuePtr* 버퍼에 유효한 입력된 값이 있어야 합니다. 또는 **StrLen_or_IndPtr* 버퍼 SQL_NULL_DATA, SQL_DATA_AT_EXEC로 또는 SQL_LEN_DATA_AT 결과 있어야 합니다. _EXEC 매크로입니다.  
  
     응용 프로그램에서 프로시저 호출에서 매개 변수 형식의 확인할 수 없는 경우 설정 *InputOutputType* SQL_PARAM_INPUT;에 데이터 원본이 매개 변수에 값을 반환 하는 경우 드라이버를 무시 합니다.  
  
-   SQL_PARAM_INPUT_OUTPUT 합니다. 매개 변수는 프로시저에서는 입/출력 매개 변수를 표시합니다. 예를 들어, 매개 변수 **{GetEmpDept(?) 호출}**  직원의 이름을 허용 하 고 직원의 부서 이름을 반환 하는 입/출력 매개 변수입니다.  
  
     드라이버; 데이터 원본에는 매개 변수에 대 한 데이터를 보냅니다는 문이 실행 될 때 \* *ParameterValuePtr* 버퍼에 유효한 입력된 값이 있어야 합니다. 또는 \* *StrLen_or_IndPtr* 버퍼 SQL_NULL_DATA, SQL_DATA_AT_EXEC로 또는 결과를 포함 해야 합니다 SQL_LEN_DATA_AT_EXEC 매크로입니다. 드라이버; 응용 프로그램에는 매개 변수에 대 한 데이터를 반환 문이 실행 된 후 드라이버를 설정 하는 데이터 원본에서 입/출력 매개 변수의 값을 반환 하지 않으면는 **StrLen_or_IndPtr* SQL_NULL_DATA로 버퍼입니다.  
  
    > [!NOTE]  
    >  ODBC 1.0 응용 프로그램 호출 하는 경우 **SQLSetParam** ODBC 2.0 드라이버를 드라이버 관리자는이를 변환에 대 한 호출 **SQLBindParameter** 는 *InputOutputType* 인수는 SQL_PARAM_INPUT_OUTPUT로 설정 됩니다.  
  
-   SQL_PARAM_OUTPUT 합니다. 매개 변수는 프로시저 또는 출력 매개 변수는 프로시저의 반환 값 표시 두 경우 모두 라고 *출력 매개 변수*합니다. 예를 들어, 매개 변수 **{? = GetNextEmpID 호출}** 다음 직원 ID를 반환 하는 출력 매개 변수  
  
     하지 않는 한 드라이버의 응용 프로그램에 데이터 매개 변수를 반환 후 문이 실행 되는 *ParameterValuePtr* 및 *StrLen_or_IndPtr* 인수는 모두 null 포인터인 경우는 드라이버는 출력 값을 삭제 합니다. 드라이버를 설정 하는 데이터 원본에 대 한 출력 매개 변수 값을 반환 하지 않으면는 **StrLen_or_IndPtr* SQL_NULL_DATA로 버퍼입니다.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM 합니다. 입력/출력 매개 변수를 스트리밍할 수 있는지를 나타냅니다. **SQLGetData** 부분에 매개 변수 값을 읽을 수 있습니다. *BufferLength* 는 버퍼 길이의 함수가 호출 될 때 결정 됩니다 때문에 무시 됩니다. **SQLGetData**합니다. 값은 *StrLen_or_IndPtr* 버퍼 SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC로 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과 포함 해야 합니다. 출력에서 스트리밍되는 경우 입력 데이터 실행 시 (디지털 오디오) 매개 변수로 매개 변수를 바인딩해야 합니다. *ParameterValuePtr* null이 아닌 포인터 값으로 반환 될 수 있지만 **SQLParamData** 와 함께 전달 된 사용자 정의 값을 토큰으로 *ParameterValuePtr* 두 입력에 대 한 및 출력을 추가 합니다. 자세한 내용은 참조 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
-   SQL_PARAM_OUTPUT_STREAM 합니다. 출력 매개 변수에 대해 SQL_PARAM_INPUT_OUTPUT_STREAM와 동일 합니다. **StrLen_or_IndPtr* 입력에서 무시 됩니다.  
  
 다음 표에서 다양 한 조합을 *InputOutputType* 및 **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|결과|ParameterValuePtr에 주석 표시|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|입력된에 부분|*ParameterValuePtr* 포인터 값으로 반환 될 수 있지만 **SQLParamData** 와 함께 전달 된 사용자 정의 값을 토큰으로 *ParameterValuePtr*합니다.|  
|SQL_PARAM_INPUT|하지 SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|입력 버퍼를 바인딩했습니다|*ParameterValuePtr* 입력된 버퍼의 주소입니다.|  
|SQL_PARAM_OUTPUT|입력에는 무시 됩니다.|바인딩된 출력 버퍼|*ParameterValuePtr* 출력 버퍼의 주소입니다.|  
|SQL_PARAM_OUTPUT_STREAM|입력에는 무시 됩니다.|스트리밍된 출력|*ParameterValuePtr* 반환할는 포인터 값이 될 수 **SQLParamData** 와 함께 전달 된 사용자 정의 값을 토큰으로 *ParameterValuePtr*합니다.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|입력된에 파트 및 바인딩된 출력 버퍼|*ParameterValuePtr* 는 출력 버퍼에서 반환할 수도 주소 **SQLParamData** 와 함께 전달 된 사용자 정의 값을 토큰으로 *ParameterValuePtr*합니다.|  
|SQL_PARAM_INPUT_OUTPUT|하지 SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|입력 버퍼와 출력 바인딩된 버퍼 바인딩했습니다|*ParameterValuePtr* 공유 입/출력 버퍼의 주소입니다.|  
L_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|입력된에 파트 및 스트리밍된 출력|*ParameterValuePtr* 반환할는 null이 아닌 포인터 값이 될 수 **SQLParamData** 와 함께 전달 된 사용자 정의 값을 토큰으로 *ParameterValuePtr* 모두에 대 한 입력 및 출력 합니다.|  
  
> [!NOTE]  
>  드라이버는 응용 프로그램 바인딩할 출력 또는 입력-출력 매개 변수 처럼 스트리밍할 때 허용 되는 SQL 형식을 결정 해야 합니다. 드라이버 관리자에서 잘못 된 SQL 형식에 대 한 오류를 생성 하지 않습니다.  
  
## <a name="valuetype-argument"></a>ValueType 인수  
 *ValueType* 인수 매개 변수의 C 데이터 형식을 지정 합니다. 이 인수는 APD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE, 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정합니다. 값 중 하나 이어야 합니다는 [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md) 섹션 부록 d: 데이터 형식입니다.  
  
 경우는 *ValueType* 인수는 interval 데이터 형식을의 SQL_DESC_TYPE 필드 중 하나는 *ParameterNumber* APD 레코드가 SQL_INTERVAL로 설정 되 면 APD의 SQL_DESC_CONCISE_TYPE 필드 설정 되어 간결한 간격 데이터 형식 및의 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 *ParameterNumber* 레코드 특정 간격 데이터 형식에 대 한 하위 코드로 설정 됩니다. (참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).) 전체 자릿수 (2)와 기본 간격 초 자릿수 (6)는 APD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 SQL_DESC_PRECISION 필드에 설정 된 대로 각각 유도 하는 기본 간격 데이터에 사용 됩니다. 중 하나가 기본 전체 자릿수를 적절 한 없으면 응용 프로그램이 명시적으로 설정 해야 설명자 필드를 호출 하 여 **SQLSetDescField** 또는 **SQLSetDescRec**합니다.  
  
 경우는 *ValueType* 인수는의 SQL_DESC_TYPE 필드는 datetime 데이터 형식 중 하나는 *ParameterNumber* APD 레코드가 SQL_DATETIME, SQL_DESC_CONCISE_TYPE 필드는 의로설정된*ParameterNumber* APD 레코드가 간결한 datetime C 데이터 형식으로의 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드로 설정 되는 *ParameterNumber* 레코드 특정 날짜/시간에 대 한 하위 코드로 설정 되어 데이터 형식입니다. (참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 경우는 *ValueType* 인수가 SQL_C_NUMERIC 데이터 형식 (드라이버 정의 된) 기본 전체 자릿수가 고 기본 소수 자릿수 (0)는 APD의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정 된 대로 사용 되는 데이터입니다. 기본 전체 자릿수 또는 소수 적합 하지 않은 경우 응용 프로그램이 명시적으로 설정 해야 설명자 필드를 호출 하 여 **SQLSetDescField** 또는 **SQLSetDescRec**합니다.  
  
 SQL_C_DEFAULT 지정 매개 변수 값으로 지정 된 SQL 데이터 형식에 대해 기본 C 데이터 형식에서 전송할 수 *ParameterType*합니다.  
  
 또한 확장된 C 데이터 형식을 지정할 수 있습니다. 자세한 내용은 참조 [odbc에서 C 데이터 형식을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.  
  
 자세한 내용은 참조 [기본 C 데이터 형식](../../../odbc/reference/appendixes/default-c-data-types.md), [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md), 및 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 부록 d: 데이터 형식에서입니다.  
  
## <a name="parametertype-argument"></a>ParameterType 인수  
 에 나열 된 값 중 하나 이어야 합니다는 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식 또는 섹션에는 드라이버 관련 값 이어야 합니다. 이 인수는 IPD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE, 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정합니다.  
  
 경우는 *ParameterType* 인수는 datetime 식별자 중 하나는 IPD의 SQL_DESC_TYPE 필드 SQL_DATETIME로 설정 됩니다, SQL_DESC_CONCISE_TYPE 필드는 IPD의 간결 datetime SQL 데이터 형식 및는 SQL_DESC_로 설정 됩니다 DATETIME_INTERVAL_CODE 필드는 datetime 적절 한 하위 코드 값으로 설정 됩니다.  
  
 경우 *ParameterType* 하나 간격 식별자는 IPD의 SQL_DESC_TYPE 필드 SQL_INTERVAL로 설정, SQL_DESC_CONCISE_TYPE 필드는 IPD의 간결 SQL 간격 데이터 형식 및는 SQL_DESC_DATETIME_로 설정 됩니다 INTERVAL_CODE 필드는 IPD의 적절 한 간격 하위 코드로 설정 됩니다. IPD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드 간격 선행 정밀도로 설정 되어 및 SQL_DESC_PRECISION 필드를 해당 하는 경우 간격 (초) 정밀도로 설정 합니다. SQL_DESC_DATETIME_INTERVAL_PRECISION 또는 SQL_DESC_PRECISION의 기본값을 적절 한 없으면 응용 프로그램이 명시적으로 설정 해야를 호출 하 여 **SQLSetDescField**합니다. 이러한 필드에 대 한 자세한 내용은 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.  
  
 경우는 *ValueType* 인수가 SQL_NUMERIC 데이터 형식 (드라이버 정의 된) 기본 전체 자릿수가 고 기본 소수 자릿수 (0)는 IPD의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정 된 대로 사용 되는 데이터입니다. 기본 전체 자릿수 또는 소수 적합 하지 않은 경우 응용 프로그램이 명시적으로 설정 해야 설명자 필드를 호출 하 여 **SQLSetDescField** 또는 **SQLSetDescRec**합니다.  
  
 데이터를 변환 하는 방법에 대 한 정보를 참조 하십시오. [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 및 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 부록 d: 데이터 형식에서입니다.  
  
## <a name="columnsize-argument"></a>ColumnSize 인수  
 *ColumnSize* 인수는 열 또는 매개 변수 표식에 해당 데이터 또는 둘 다의 길이에 해당 하는 식의 크기를 지정 합니다. SQL 데이터 형식에 따라 IPD의 다른 필드를 설정 하는이 인수 (의 *ParameterType* 인수). 이 매핑은 다음 규칙이 적용 됩니다.  
  
-   경우 *ParameterType* SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY, 되었거나 간결한 SQL 날짜/시간 또는 간격 데이터 형식의는 IPD의 SQL_DESC_LENGTH 필드 하나 의값으로설정된 *ColumnSize*합니다. (자세한 내용은 참조는 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에는 섹션입니다.)  
  
-   경우 *ParameterType* SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL, 또는 SQL_DOUBLE는 IPD의 SQL_DESC_PRECISION 필드의 값으로 설정 되어 *ColumnSize*합니다.  
  
-   다른 데이터 형식에 대해서는 *ColumnSize* 인수는 무시 됩니다.  
  
 자세한 내용은 "매개 변수 값 전달"과에서 SQL_DATA_AT_EXEC를 참조 하십시오. "*StrLen_or_IndPtr* 인수입니다."  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 인수  
 경우 *ParameterType* SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND, 또는 SQL_INTERVAL_MINUTE_TO_SECOND는 IPD의 SQL_DESC_PRECISION 필드 설정 되어 *DecimalDigits*합니다. 경우 *ParameterType* SQL_NUMERIC 또는 SQL_DECIMAL는 IPD의 자릿수가 SQL_DESC_SCALE 필드 설정 되어 *DecimalDigits*합니다. 다른 모든 데이터 형식에 대 한는 *DecimalDigits* 인수는 무시 됩니다.  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 인수  
 *ParameterValuePtr* 인수는 버퍼를 가리키는 하는 경우, **SQLExecute** 또는 **SQLExecDirect** 호출 되 면 매개 변수에 대해 실제 데이터를 포함 합니다. 데이터는 지정 된 형식에서 이어야 합니다는 *ValueType* 인수입니다. 이 인수는 APD의 SQL_DESC_DATA_PTR 필드가 설정합니다. 응용 프로그램을 설정할 수는 *ParameterValuePtr* 인수는 null 포인터를  *\*StrLen_or_IndPtr* SQL_NULL_DATA 또는 SQL_DATA_AT_EXEC입니다. (만 입력 또는 입/출력 매개 변수 적용 됨)  
  
 경우 \* *StrLen_or_IndPtr* 는 SQL_LEN_DATA_AT_EXEC의 결과입니다 (*길이*) 매크로 또는 SQL_DATA_AT_EXEC로 다음 *ParameterValuePtr* 되는 매개 변수 연관 된 응용 프로그램 정의 포인터 값입니다. 통해 응용 프로그램에 반환 되기 **SQLParamData**합니다. 예를 들어 *ParameterValuePtr* 매개 변수 번호, 데이터에 대 한 포인터 또는 응용 프로그램 입력된 매개 변수를 바인딩하는 데 사용 하는 구조에 대 한 포인터와 같은 0이 아닌 토큰 수 있습니다. 그러나 경우에 유의 매개 변수는 입/출력 매개 변수는 *ParameterValuePtr* 출력 값을 저장할 버퍼에 대 한 포인터 여야 합니다. SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1 보다 크면 응용 프로그램와 함께 문 특성 SQL_ATTR_PARAMS_PROCESSED_PTR가 가리키는 값을 사용할 수는 *ParameterValuePtr* 인수입니다. 예를 들어 *ParameterValuePtr* 값 배열을 가리키는 있으며 응용 프로그램 배열에서 올바른 값을 검색 하려면 SQL_ATTR_PARAMS_PROCESSED_PTR 가리키는 값을 사용할 수도 있습니다. 자세한 내용은이 섹션의 뒷부분에 나오는 "매개 변수 값 전달"을 참조 하십시오.  
  
 경우는 *InputOutputType* 인수가, SQL_PARAM_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT *ParameterValuePtr* 드라이버가 출력 값을 반환 하는 버퍼를 가리킵니다. 프로시저는 하나 이상의 결과 집합을 반환 하는 경우는 \* *ParameterValuePtr* 버퍼 보장 되지 않는 모든 결과 집합/행 개수 처리 될 때까지 설정할 수 있습니다. 처리가 완료 될 때까지 버퍼를 설정 하지 않으면, 출력 매개 변수 및 반환 값 사용할 수 없는까지 **SQLMoreResults** SQL_NO_DATA를 반환 합니다. 호출 **SQLCloseCursor** 또는 **SQLFreeStmt** 옵션의 SQL_CLOSE와 이러한 값을 무시 하면 됩니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성에 값이 1 보다 큰 경우 *ParameterValuePtr* 배열을 가리킵니다. 단일 SQL 문 처리 하는 입력 또는 입/출력 매개 변수에 대 한 입력된 값의 전체 배열 및 출력 매개 변수 또는 입력/출력에 대 한 출력 값의 배열을 반환 합니다.  
  
## <a name="bufferlength-argument"></a>BufferLength 인수  
 문자 및 이진 C 데이터에 대 한는 *BufferLength* 의 길이 지정 하는 인수는 \* *ParameterValuePtr* 버퍼 (단일 요소 경우) 또는 요소에는 길이\* *ParameterValuePtr* 배열 (SQL_ATTR_PARAMSET_SIZE 문 특성의 값은 1 보다 큰). 이 인수는 APD의 SQL_DESC_OCTET_LENGTH 레코드 필드를 설정합니다. 응용 프로그램에 여러 값을 지정 하는 경우 *BufferLength* 에 있는 값의 위치를 확인 하는 데 사용 되는 **ParameterValuePtr* 입력 및 출력에서 모두 배열입니다. 입/출력 및 출력 매개 변수에 대 한 문자 및 이진 C 데이터 출력에 truncate 것인지 결정 사용 됩니다.  
  
-   C 문자 데이터를 반환할 수 있는 바이트 수 보다 크거나 같은 경우에 대 한 *BufferLength*, 데이터에 \* *ParameterValuePtr* 잘립니다  *BufferLength* null 종결 문자 길이 여백을 제외 하 고 드라이버에 의해 null 종료 합니다.  
  
-   이진 C 데이터를 반환할 수 있는 바이트 수 이상인 경우에 대 한 *BufferLength*, 데이터에 \* *ParameterValuePtr* 잘립니다 *BufferLength*바이트입니다.  
  
 다른 모든 유형의 C 데이터는 *BufferLength* 인수는 무시 됩니다. 길이 \* *ParameterValuePtr* 버퍼 (단일 요소 경우) 또는 요소 길이 \* *ParameterValuePtr* (응용 프로그램 를호출하는경우배열 **SQLSetStmtAttr** 와 *특성* 의 각 매개 변수에 대해 여러 값을 지정 SQL_ATTR_PARAMSET_SIZE 인수) C 데이터 형식의 길이 것으로 간주 됩니다.  
  
 스트리밍된 출력 또는 스트리밍된 입/출력 매개 변수는 *BufferLength* 인수는 버퍼 길이에 지정 되어 있으므로 무시 됩니다 **SQLGetData**합니다.  
  
> [!NOTE]  
>  ODBC 1.0 응용 프로그램 호출 하는 경우 **SQLSetParam** ODBC 3에서. *x* 드라이버를 드라이버 관리자는이를 변환에 대 한 호출 **SQLBindParameter** 는 *BufferLength* 인수는 항상 SQL_SETPARAM_VALUE_MAX 합니다. 드라이버 관리자에서 오류가 반환 ODBC 3 때문에. *x* 응용 프로그램 집합 *BufferLength* 를 SQL_SETPARAM_VALUE_MAX, ODBC 3. *x* 드라이버는 ODBC 1.0 응용 프로그램에서 호출 될 때 결정 하는 데 사용할 수 있습니다.  
  
> [!NOTE]  
>  **SQLSetParam**, 응용 프로그램의 길이 지정 하는 방식으로 **ParameterValuePtr* 드라이버는 문자 또는 이진 데이터 및 응용 프로그램에서 보내는 방식으로 반환 될 수 있도록 버퍼는 배열 문자 또는 이진 매개 변수 값이 드라이버는 드라이버 별로 정의 됩니다.  
  
## <a name="strlenorindptr-argument"></a>StrLen_or_IndPtr 인수  
 *StrLen_or_IndPtr* 인수는 버퍼를 가리키는 하는 경우, **SQLExecute** 또는 **SQLExecDirect** 호출 되 면 다음 중 하나를 포함 합니다. (이 인수는 응용 프로그램 매개 변수 포인터의 SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 레코드 필드를 설정합니다.)  
  
-   에 저장 된 매개 변수 값의 길이 **ParameterValuePtr*합니다. 이 문자 또는 이진 C 데이터를 제외 하 고 무시 됩니다.  
  
-   SQL_NTS 합니다. 매개 변수 값은 null로 끝나는 문자열입니다.  
  
-   SQL_NULL_DATA 합니다. 매개 변수 값은 NULL입니다.  
  
-   SQL_DEFAULT_PARAM 합니다. 프로시저는 응용 프로그램에서 검색 하는 값 대신 매개 변수의 기본값을 사용 하는 것입니다. 이 값은 ODBC 정식 구문을에서 호출 하는 프로시저에만 유효 하 고 다음 경우에만 *InputOutputType* SQL_PARAM_INPUT 또는 SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM 인수는 합니다. 때 \* *StrLen_or_IndPtr* SQL_DEFAULT_PARAM으로가 *ValueType*, *ParameterType*, *ColumnSize*,  *DecimalDigits*, *BufferLength*, 및 *ParameterValuePtr* 인수에 대 한 입력된 매개 변수가 무시 되 고 입력에 대 한 출력 매개 변수 값을 정의 하는 데에 사용 됩니다 / 출력 매개 변수입니다.  
  
-   결과 SQL_LEN_DATA_AT_EXEC (*길이*) 매크로입니다. 매개 변수에 대 한 데이터 전송 **SQLPutData**합니다. 경우는 *ParameterType* 인수는 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 long, 데이터 원본에 따른 특정 데이터 형식, 및 드라이버 반환 "Y" SQL_NEED_LONG_DATA_LEN 정보 유형에 대해에서 **SQLGetInfo**, *길이* ; 매개 변수에 대해 전달할 데이터의 바이트 수는 그렇지 않은 경우 *길이* 음수가 아닌 값 이어야 하며 무시 됩니다. 자세한 내용은 "전달 매개 변수 값"이이 섹션의 뒷부분에 나오는 참조 하십시오.  
  
     예를 들어, 10, 000 바이트의 데이터를 함께 보내집니다 지정 하려면 **SQLPutData** 는 SQL_LONGVARCHAR 매개 변수에 대 한 여러 호출에서 응용 프로그램 설정 **StrLen_or_IndPtr* SQL_LEN_DATA_AT_EXEC ( 10000)입니다.  
  
-   SQL_DATA_AT_EXEC입니다. 매개 변수에 대 한 데이터 전송 **SQLPutData**합니다. ODBC 3를 호출할 때이 값은 ODBC 1.0 응용 프로그램에서 사용 됩니다. *x* 드라이버입니다. 자세한 내용은 "전달 매개 변수 값"이이 섹션의 뒷부분에 나오는 참조 하십시오.  
  
 경우 *StrLen_or_IndPtr* 가 null 포인터 이면 드라이버는 모든 입력된 매개 변수 값이 NULL이 아닌 지 않으며 문자와 이진 데이터를 null로 끝나는 가정 합니다. 경우 *InputOutputType* SQL_PARAM_OUTPUT 또는 SQL_PARAM_OUTPUT_STREAM 및 *ParameterValuePtr* 및 *StrLen_or_IndPtr* 모두 null 포인터인 드라이버 삭제 출력 값입니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자에 대 한 null 포인터를 지정 해서는 안 됩니다. *StrLen_or_IndPtr* 매개 변수의 데이터 형식 SQL_C_BINARY 경우. 드라이버가 예기치 않게 잘라내지 않습니다 SQL_C_BINARY 데이터 되도록 *StrLen_or_IndPtr* 유효한 길이 값에 대 한 포인터를 포함 해야 합니다.  
  
 경우는 *InputOutputType* 인수가 SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM, 또는 SQL_PARAM_OUTPUT_STREAM, *StrLen_or_IndPtr* 버퍼를 가리키는 드라이버가 SQL_NULL_DATA에 반환할 수 있는 바이트 수를 반환 합니다. \* *ParameterValuePtr* (null 종료 바이트의 문자 데이터 제외) 또는 SQL_NO_TOTAL (경우에 사용 가능한 바이트 수 반환 확인할 수 없습니다). 프로시저는 하나 이상의 결과 집합을 반환 하는 경우는 **StrLen_or_IndPtr* 버퍼를 인출 된 모든 결과 될 때까지 설정할 보장 되지 않습니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성에 값이 1 보다 큰 경우 *StrLen_or_IndPtr* SQLLEN 값의 배열을 가리킵니다. 이러한 반환이 섹션의 앞부분에 나열 된 값 중 하나일 수 있습니다 및 단일 SQL 문으로 처리 합니다.  
  
## <a name="passing-parameter-values"></a>매개 변수 값 전달  
 응용 프로그램 중 하나는 매개 변수의 값을 전달할 수에 \* *ParameterValuePtr* 버퍼 또는 하나 이상의 호출을 통해 **SQLPutData**합니다. 데이터와 함께 전달 되는 매개 변수 **SQLPutData** 라고 *실행 시 데이터* 매개 변수입니다. 이러한 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 매개 변수에 대 한 데이터를 보내는 데 일반적으로 사용 하 고 다른 매개 변수와 함께 사용할 수 있습니다.  
  
 매개 변수 값을 전달 하려면 응용 프로그램에서는 다음과 같은 일련의 단계를 수행 합니다.  
  
1.  호출 **SQLBindParameter** 매개 변수의 값에 대 한 버퍼를 바인딩할 각 매개 변수에 대해 (*ParameterValuePtr* 인수) 및 길이/표시기 (*StrLen_or_IndPtr* 인수)입니다. 실행 시 데이터 매개 변수에 대 한 *ParameterValuePtr* 매개 변수 번호 또는 데이터에 대 한 포인터와 같은 응용 프로그램 정의 포인터 값입니다. 값이 나중에 반환 하 고는 매개 변수를 식별 하는 데 사용할 수 있습니다.  
  
2.  배치에서 입력 및 입/출력 매개 변수 값은 \* *ParameterValuePtr* 및 **StrLen_or_IndPtr* 버퍼:  
  
    -   일반 매개 변수에 대 한 응용 프로그램에서 매개 변수 값이 배치는 \* *ParameterValuePtr* 버퍼와 해당 값의 길이 **StrLen_or_IndPtr* 버퍼입니다. 자세한 내용은 참조 [매개 변수 값 설정](../../../odbc/reference/develop-app/setting-parameter-values.md)합니다.  
  
    -   응용 프로그램 실행 시 데이터 매개 변수에 대해 SQL_LEN_DATA_AT_EXEC는 결과 넣습니다 (*길이*) 매크로 (ODBC 2.0 드라이버 호출) 하는 경우에 **StrLen_or_IndPtr* 버퍼입니다.  
  
3.  호출 **SQLExecute** 또는 **SQLExecDirect** SQL 문을 실행할 수 있습니다.  
  
    -   실행 시 데이터 매개 변수가 없는 경우 프로세스 완료 되었습니다.  
  
    -   모든 실행 시 데이터 매개 변수가 있는 경우 sql_need_data가 반환 됩니다.  
  
4.  호출 **SQLParamData** 에 지정 된 응용 프로그램 정의 값을 검색 하는 *ParameterValuePtr* 의 인수 **SQLBindParameter** 첫 번째에 대 한 처리 해야 하는 실행 시 데이터 매개 변수입니다. **SQLParamData** SQL_NEED_DATA를 반환 합니다.  
  
    > [!NOTE]  
    >  반환 된 값 실행 시 데이터 매개 변수가 실행 시 데이터 열과 비슷한 있지만 **SQLParamData** 을에 따라 다릅니다. 실행 시 데이터 매개 변수를 데이터 전송 하는 SQL 문의 매개 변수에 **SQLPutData** 와 문이 실행 되는 경우 **SQLExecDirect** 또는 **SQLExecute**. 연결 된 **SQLBindParameter**합니다. 반환한 값 **SQLParamData** 에 전달 하는 포인터 값 **SQLBindParameter** 에 *ParameterValuePtr* 인수입니다. 실행 시 데이터 열을 데이터 전송 하는 행 집합의 열은 **SQLPutData** 행이 업데이트 되거나 추가 된이 **SQLBulkOperations** 또는와 업데이트 된 **SQLSetPos**. 연결 된 **SQLBindCol**합니다. 반환한 값 **SQLParamData** 는에 있는 행의 주소는 **TargetValuePtr* 버퍼 (를 호출 하 여 설정 **SQLBindCol**) 처리가 진행 중입니다.  
  
5.  호출 **SQLPutData** 한 번 이상 매개 변수에 대 한 데이터를 보내려고 합니다. 하나 이상의 호출 하는 경우 데이터 값 보다 크면는 \* *ParameterValuePtr* 에 지정 된 버퍼 **SQLPutData**;를 여러 번 호출 **SQLPutData**데이터 원본에 따른 특정 데이터 형식 또는 동일한 매개 변수는 문자, 이진 열에 이진 C 데이터를 보낼 때 또는는 문자, 이진, 또는 데이터 원본에 따른 특정 데이터 형식과 열에 문자 데이터를 보낼 때만 허용 됩니다.  
  
6.  호출 **SQLParamData** 는 매개 변수에 대 한 모든 데이터가 보냈음을 알리는 돌아갑니다.  
  
    -   더 많은 실행 시 데이터 매개 변수가 **SQLParamData** 처리할 SQL_NEED_DATA 및 다음 실행 시 데이터 매개 변수에 대 한 응용 프로그램 정의 값을 반환 합니다. 응용 프로그램 4, 5 단계를 반복합니다.  
  
    -   더 이상 실행 시 데이터 매개 변수가 있는 경우에 프로세스가 완료 됩니다. 문이 성공적으로 실행 하는 경우 **SQLParamData** SQL_SUCCESS 또는; SQL_SUCCESS_WITH_INFO를 반환 합니다. 실행이 실패 SQL_ERROR를 반환 합니다. 이 시점에서 **SQLParamData** 문을 실행 하는 데 사용 되는 함수에 의해 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다 (**SQLExecDirect** 또는 **SQLExecute**).  
  
         사용할 수 있는 모든 입/출력 또는 출력 매개 변수에 대 한 출력 값은 \* *ParameterValuePtr* 및 **StrLen_or_IndPtr* 버퍼링 하는 응용 프로그램은 모든 결과 집합을 검색 한 후 문으로 생성 합니다.  
  
 호출 **SQLExecute** 또는 **SQLExecDirect** 문을 SQL_NEED_DATA 상태에 넣습니다. 이 시점에서 응용 프로그램 에서만 호출할 수 **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**, 또는 **SQLPutData** 문을 사용 하 여 또는 *연결 핸들* 문과 연결 된입니다. 함수 반환 SQLSTATE HY010 문이나 문과 연결 된 연결 된 다른 함수를 호출 하는 경우 (함수 시퀀스 오류). SQL_NEED_DATA 상태의 문 leaves **SQLParamData** 또는 **SQLPutData** 에서 오류를 반환 **SQLParamData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 또는 문을 취소 됩니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLCancel** 드라이버 문 실행을 취소 하는 동안 드라이버 실행 시 데이터 매개 변수에 대 한 데이터를 여전히 필요 합니다; 응용 프로그램이 호출할 수 **SQLExecute** 또는  **SQLExecDirect** 다시 합니다.  
  
## <a name="retrieving-streamed-output-parameters"></a>스트리밍된 출력 매개 변수 검색  
 응용 프로그램 설정 하는 경우 *InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM 출력 매개 변수 값은 하나 이상의 호출을 통해 검색 해야 **SQLGetData**합니다. 드라이버는 응용 프로그램에 반환할 스트리밍된 출력 매개 변수 값이 0이 반환 됩니다 SQL_PARAM_DATA_AVAILABLE 다음과 같은 기능에 대 한 호출에 대 한 응답에서: **SQLMoreResults**, **SQLExecute**, 및 **SQLExecDirect**합니다. 응용 프로그램이 호출 **SQLParamData** 사용할 수 있는 매개 변수 값을 확인 하려면.  
  
 SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 참조 하십시오. [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
## <a name="using-arrays-of-parameters"></a>매개 변수 배열을 사용 하 여  
 응용 프로그램 매개 변수 표식 및 매개 변수 배열 패스를 사용 하 여 문을 준비를 하는 경우에 두 가지가이 실행 될 수 있습니다. 한 가지 방법은 드라이버가 있는 경우에는 매개 변수 배열 전체 문이 처리에 원자 단위로 백 엔드의 배열 처리 기능에 의존 하는 것입니다. Oracle은 배열 처리 기능을 지 원하는 데이터 원본의 예. 이 기능을 구현 하는 다른 방법은 드라이버가 SQL 문 각 매개 변수 배열에 있는 매개 변수 집합에 대 한 SQL 문 일괄 처리를 생성 하 고 일괄 처리를 실행 하는 합니다. 배열 매개 변수는 함께 사용할 수 없습니다는 **업데이트 WHERE CURRENT OF** 문.  
  
 매개 변수 배열을 처리 될 때 개별 결과 집합/행 개수 (각 매개 변수 집합에 대해 각각 하나씩)를 사용할 수 있습니다 또는 결과 집합/행 개수를 하나의 롤업 될 수 있습니다. 옵션에 SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo** 행 개수 매개 변수 (SQL_PARC_BATCH)의 각 집합에 사용할 수 있는 하나의 행 개수는 사용할 수 있는 (SQL_PARC_NO_BATCH) 여부를 나타냅니다.  
  
 옵션에 SQL_PARAM_ARRAY_SELECTS **SQLGetInfo** 결과 집합은 각 매개 변수 (SQL_PAS_BATCH) 집합에 사용할 수 있는 하나의 결과 집합을 사용할 수 있는 (SQL_PAS_NO_BATCH) 여부를 나타냅니다. 드라이버에서 결과 집합 – 생성 문을 매개 변수 배열을 사용 하 여 실행 하도록 허용 하지 않으면, SQL_PARAM_ARRAY_SELECTS SQL_PAS_NO_SELECT를 반환 합니다.  
  
 자세한 내용은 참조 [SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)합니다.  
  
 배열 매개 변수를 지원 하려면 각 매개 변수에 대 한 값의 수를 지정 하려면 SQL_ATTR_PARAMSET_SIZE 문 특성 설정 됩니다. 필드는 1 보다 큰 경우 APD의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드 배열을 가리켜야 합니다. 각 배열의 카디널리티 SQL_ATTR_PARAMSET_SIZE의 값과 같습니다.  
  
 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드 처리 되 면 오류 집합을 포함 하 여 매개 변수 집합의 수를 포함 하는 버퍼를 가리킵니다. 각 매개 변수 집합이 처리 되 면 드라이버는 새 값을 버퍼에 저장 합니다. 이 null 포인터 이면 번호가 없으면 반환 됩니다. 매개 변수 배열을 사용 되는 경우 설정 함수에서 SQL_ERROR가 반환 되는 경우에 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드에서 가리키는 값이 채워집니다. SQL_NEED_DATA가 반환 하는 경우 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드에서 가리키는 값이 처리 되는 매개 변수 집합에 설정 됩니다.  
  
 매개 변수 배열이 바인딩되어 있을 때와 발생 하는 상황 **업데이트 WHERE CURRENT OF** 문이 실행 되는 드라이버 정의입니다.  
  
## <a name="column-wise-parameter-binding"></a>열 단위 매개 변수 바인딩  
 열 단위 바인딩을 응용 프로그램을 각 매개 변수에 별도 매개 변수 및 배열 길이/표시기를 바인딩합니다.  
  
 에 열 단위 바인딩을 사용 하려면 응용 프로그램을 SQL_PARAM_BIND_BY_COLUMN SQL_ATTR_PARAM_BIND_TYPE 문 특성 먼저 설정 합니다. (기본값입니다.) 바인딩할 각 열에 대 한 응용 프로그램에서 다음 단계를 수행 합니다.  
  
1.  매개 변수 버퍼 배열을 할당합니다.  
  
2.  길이/표시기 버퍼의 배열을 할당합니다.  
  
    > [!NOTE]  
    >  응용 프로그램은 열 단위 바인딩을 사용 하는 경우 설명자에 직접 쓰는, 별도 배열 길이 및 표시기 데이터에 대 한 사용할 수 있습니다.  
  
3.  호출 **SQLBindParameter** 다음 인수:  
  
    -   *ValueType* C 유형 매개 변수 버퍼 배열의 단일 요소입니다.  
  
    -   *ParameterType* SQL 유형 매개 변수입니다.  
  
    -   *ParameterValuePtr* 매개 변수 버퍼 배열의 주소입니다.  
  
    -   *BufferLength* 크기 매개 변수 버퍼 배열의 단일 요소입니다. *BufferLength* 데이터는 고정 길이 데이터 인수는 무시 됩니다.  
  
    -   *StrLen_or_IndPtr* 주소 길이/표시기 배열입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "주석,"에서 "ParameterValuePtr 인수"를 참조 합니다. 매개 변수 열 단위 바인딩에 대 한 자세한 내용은 참조 [바인딩 배열의 매개 변수](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)합니다.  
  
## <a name="row-wise-parameter-binding"></a>행 단위 매개 변수 바인딩  
 행 단위 바인딩을 응용 프로그램에 각 매개 변수에 대해 매개 변수 및 길이/표시기 버퍼를 포함 하는 구조를 정의 합니다.  
  
 응용 프로그램을 행 단위 바인딩을 사용 하려면 다음 단계를 수행 합니다.  
  
1.  단일 집합 매개 변수 (모두 매개 변수 및 길이/표시기 버퍼 포함)을 유지 하기 위한 구조를 정의 하 고 이러한 구조 배열을 할당 합니다.  
  
    > [!NOTE]  
    >  응용 프로그램은 행 단위 바인딩을 사용 하는 경우 설명자에 직접 쓰는, 길이 및 표시기 데이터에 대 한 별도 필드를 사용할 수 있습니다.  
  
2.  매개 변수가 바인딩될 버퍼의 인스턴스 크기 또는 단일 매개 변수 집합이 포함 된 구조체의 크기에 SQL_ATTR_PARAM_BIND_TYPE 문 특성을 설정 합니다. 길이 바인딩된 매개 변수를 모두 및 구조 또는 바인딩된 매개 변수 주소는 지정 된 길이로 증가, 결과 시작에서 동일한 매개 변수 부분을 가리키도록는 버퍼의 패딩에 대 한 공간을 포함 해야 합니다는 다음 행입니다. 사용 하는 경우는 *sizeof* ANSI c에서 연산자를이 동작이 유지 됩니다.  
  
3.  호출 **SQLBindParameter** 바인딩할 각 매개 변수에 대해 다음 인수:  
  
    -   *ValueType* 열에 바인딩된 매개 변수 버퍼 멤버의 형식입니다.  
  
    -   *ParameterType* SQL 유형 매개 변수입니다.  
  
    -   *ParameterValuePtr* 첫 번째 배열 요소에 포함 된 매개 변수 버퍼 멤버의 주소입니다.  
  
    -   *BufferLength* 매개 변수 버퍼 멤버의 크기입니다.  
  
    -   *StrLen_or_IndPtr* 바인딩되어야 길이/표시기 멤버의 주소입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. "*ParameterValuePtr* 인수"이이 섹션의 뒷부분에 나오는 합니다. 매개 변수의 행 단위 바인딩에 대 한 자세한 내용은 참조는 [바인딩 배열의 매개 변수](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)합니다.  
  
## <a name="error-information"></a>오류 정보  
 드라이버 (SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 SQL_PARC_NO_BATCH 같음) 일괄 처리로 매개 변수 배열 구현 하지 않으면, 오류 상황이 하나의 문이 실행 된 경우 처럼 처리 됩니다. 드라이버가 일괄 처리로 매개 변수 배열을 구현 하는 경우 응용 프로그램의 SQL 문 또는 매개 변수 배열에 있는 매개 변수 발생 되는 매개 변수를 확인 하는 IPD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 사용할 수  **SQLExecDirect** 또는 **SQLExecute** 오류를 반환 합니다. 이 필드는 매개 변수 값의 각 행에 대 한 상태 정보를 포함합니다. 필드 나타나면 오류가 발생 했습니다 진단 데이터 구조의 필드에 실패 한 매개 변수 행 및 매개 변수 수가 표시 됩니다. 배열의 요소 수가 SQL_ATTR_PARAMSET_SIZE 문 특성에 의해 설정 될 수 있는 APD의 SQL_DESC_ARRAY_SIZE 헤더 필드에 따라 정의 됩니다.  
  
> [!NOTE]  
>  APD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드 매개 변수를 무시 하도록 사용 됩니다. 매개 변수는 무시 하는 방법에 대 한 자세한 내용은 다음 섹션인 "매개 변수 집합을 무시 합니다."를 참조 하십시오.  
  
 때 **SQLExecute** 또는 **SQLExecDirect** SQL_ERROR를 반환 SQL_DESC_ARRAY_STATUS_PTR 필드는 IPD의가 가리키는 배열의 요소가 SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_ 포함 됩니다 PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED, 또는 SQL_PARAM_DIAG_UNAVAILABLE 합니다.  
  
 이 배열의 각 요소에 대 한 진단 데이터 구조는 하나 이상의 상태 레코드를 포함합니다. 구조체의 SQL_DIAG_ROW_NUMBER 필드 오류가 발생 하는 매개 변수 값의 행 수를 나타냅니다. 오류가 발생 하는 매개 변수의 행에서 특정 매개 변수를 확인할 수 있으면 매개 변수 번호 SQL_DIAG_COLUMN_NUMBER 필드에 입력 됩니다.  
  
 강제 적용 하는 이전 매개 변수에서 오류가 발생 하 여 매개 변수가 사용 되지 않은 경우 SQL_PARAM_UNUSED 입력 **SQLExecute** 또는 **SQLExecDirect** 를 중단 합니다. 매개 변수를 발생 시킨 40 집합을 실행 하는 동안 오류가 발생 했습니다 50 매개 변수는 고 예를 들어 **SQLExecute** 또는 **SQLExecDirect** SQL_PARAM_UNUSED에 입력 한 다음 중단 하 고 부터 50 41 매개 변수에 대 한 상태 배열입니다.  
  
 SQL_PARAM_DIAG_UNAVAILABLE는 드라이버 하므로이 개별 매개 변수 수준의 오류 정보를 생성 하지 않습니다 매개 변수 배열을 단일 단위로 취급 하는 경우 시작 됩니다.  
  
 일부 단일 매개 변수 집합이 처리 발생할 후속 매개 변수 집합이의 처리를 중지 배열에. 다른 오류 후속 매개 변수 처리는 영향을 주지 않습니다. 기록할 오류 처리가 중지는 드라이버 정의입니다. 처리 중지 되지 않은 배열에 있는 모든 매개 변수 처리, SQL_SUCCESS_WITH_INFO가 반환 하는 오류의 결과로 하 고 SQL_ATTR_PARAMS_PROCESSED_PTR 정의한 버퍼 처리 하는 매개 변수 집합의 총 수로 설정 되어 (에 정의 된 대로 SQL_ATTR_PARAMSET_SIZE 문 특성), 오류 집합을 포함 하 합니다.  
  
> [!CAUTION]  
>  ODBC의 매개 변수 배열 처리에서 오류가 발생 하는 경우은 다른 ODBC 3에서입니다. *x* 보다 ODBC 2. *x*합니다. Odbc 2. *x*, 함수 반환 상태가 중단 SQL_ERROR 및 처리 합니다. 가 가리키는 버퍼는 *pirow* 의 인수 **SQLParamOptions** 오류 행의 번호를 포함 합니다. Odbc 3. *x*, SQL_SUCCESS_WITH_INFO를 반환 하는 함수 및 중지 하거나 계속 하거나 년 5 월을 처리 합니다. 계속 해 서을 SQL_ATTR_PARAMS_PROCESSED_PTR로 지정 된 버퍼의 모든 매개 변수 처리를 수행 하면 오류가 발생 하는 것을 비롯 하 값으로 설정 됩니다. 동작의이 변경에는 기존 응용 프로그램에 문제가 발생할 수 있습니다.  
  
 때 **SQLExecute** 또는 **SQLExecDirect** 상태 배열에 포함 된 SQL_ERROR 또는 SQL_NEED_DATA가 반환 되는 경우와 같은 매개 변수 배열에서 모든 매개 변수 집합의 처리를 완료 하기 전에 반환 이미 처리 된 해당 매개 변수에 대 한 상태입니다. SQL_DESC_ROWS_PROCESSED_PTR 필드는 IPD의 가리키는 위치 SQL_ERROR 또는 SQL_NEED_DATA 오류 코드가 발생 하는 매개 변수 배열에서 행 번호를 포함 합니다. 상태 배열 값의 가용성은 드라이버 정의; SELECT 문에 매개 변수 배열의 보내면 결과 집합이 인출 또는 문이 실행 된 후 찾아볼 수 있습니다.  
  
## <a name="ignoring-a-set-of-parameters"></a>매개 변수 집합을 무시합니다.  
 APD (SQL_ATTR_PARAM_STATUS_PTR 문 특성에 의해 설정)로 SQL_DESC_ARRAY_STATUS_PTR 필드 SQL 문에 바인딩된 매개 변수 집합을 무시 해야 함을 나타내기 위해 사용할 수 있습니다. 실행 하는 동안 하나 이상의 매개 변수 집합을 무시 하도록 드라이버를 지시 하는 경우, 다음이 단계는 응용 프로그램을 따라야 합니다.  
  
1.  호출 **SQLSetDescField** SQLUSMALLINT 상태 정보를 포함 하는 값의 배열을를 가리키도록 APD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 설정할 수 있습니다. 이 필드를 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** 와 *특성* SQL_ATTR_PARAM_OPERATION_PTR 설명자 핸들을 가져오지 않고 필드를 설정 하려면 응용 프로그램 수입니다.  
  
2.  두 값 중 하나로 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드 정의 된 배열의 각 요소를 설정 합니다.  
  
    -   SQL_PARAM_IGNORE 행 문 실행에서 제외 되었음을 나타냅니다.  
  
    -   SQL_PARAM_PROCEED 행 문 실행에 포함 되어 있는지를 나타냅니다.  
  
3.  호출 **SQLExecDirect** 또는 **SQLExecute** 준비 된 문을 실행할 수 있습니다.  
  
 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드에서 정의 된 배열에는 다음 규칙이 적용 됩니다.  
  
-   포인터가 설정 되어 기본적으로 null로 합니다.  
  
-   포인터가 null 이면 모든 요소가 SQL_ROW_PROCEED 하도록 설정 된 경우에 따라 모든 매개 변수 집합이 사용 됩니다.  
  
-   SQL_PARAM_PROCEED에 요소를 설정 하는 해당 특정 매개 변수 집합을 사용 합니다 보장 하지 않습니다.  
  
-   SQL_PARAM_PROCEED 헤더 파일에는 0으로 정의 됩니다.  
  
 응용 프로그램 IRD에서 SQL_DESC_ARRAY_STATUS_PTR 필드와 동일한 배열을 가리키도록 APD의 가리키는 SQL_DESC_ARRAY_STATUS_PTR 필드에 따라을 설정할 수 있습니다. 매개 변수 행 데이터에 바인딩하는 경우에 유용 합니다. 매개 변수 행 데이터의 상태에 따라 다음 무시할 수 있습니다. SQL_PARAM_IGNORE, 다음과 같은 코드가 발생 매개 변수가 무시 되도록 SQL 문에서: SQL_ROW_UPDATED은 SQL_ROW_DELETED, SQL_ROW_ERROR 합니다. SQL_PARAM_PROCEED, 다음과 같은 코드가 발생 진행 하는 SQL 문: SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, 및 SQL_ROW_ADDED 합니다.  
  
## <a name="rebinding-parameters"></a>다시 바인딩 매개 변수  
 응용 프로그램 바인딩을 변경 하려면 두 작업 중 하나라도 수행해 보십시오.  
  
-   호출 **SQLBindParameter** 지정 이미 바인딩된 열에 대 한 새 바인딩을 지정 합니다. 드라이버를 새 항목으로 기존 바인딩을 덮어씁니다.  
  
-   에 대 한 바인딩 호출에서 지정 된 버퍼 주소에 추가할 수에 대 한 오프셋을 지정 **SQLBindParameter**합니다. 자세한 내용은 다음 섹션을 참조 하십시오. "오프셋으로 다시 바인딩해야 합니다."  
  
## <a name="rebinding-with-offsets"></a>오프셋으로 다시 바인딩  
 매개 변수 다시 바인딩하는 응용 프로그램에 대 한 호출 하지만 많은 매개 변수를 포함할 수 있는 버퍼 영역 설치 프로그램은 때 특히 유용 **SQLExecDirect** 또는 **SQLExecute** 매개 변수 중 일부만 사용 합니다. 버퍼 영역에서 남은 공간 오프셋 기존 바인딩을 수정 하 여 다음 매개 변수 집합에 사용할 수 있습니다.  
  
 APD의 SQL_DESC_BIND_OFFSET_PTR 헤더 필드 바인딩 오프셋을 가리킵니다. 필드가 null이 아닌 경우 드라이버는 포인터를 역참조 하 고, 없는 경우에 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR 필드에 있는 값의 null 포인터 이면 설명자의 해당 필드에 역참조 된 값을 추가 실행 시간에 기록 합니다. 새로운 포인터 값에는 SQL 문이 실행 될 때 사용 됩니다. 다시 바인딩 후 오프셋 유효합니다. SQL_DESC_BIND_OFFSET_PTR 자체 오프셋 보다는 오프셋에 대 한 포인터 이기 때문에 응용 프로그램 변경할 수 오프셋을 직접 호출 하지 않고도 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 또는 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) 를 설명자 필드를 변경 합니다. 포인터가 설정 되어 기본적으로 null로 합니다. 카드가의 SQL_DESC_BIND_OFFSET_PTR 필드를 호출 하 여 설정할 수 있습니다 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 또는 호출 하 여 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)와 *fAttribute* SQL_ATTR_PARAM_BIND_의 OFFSET_PTR 합니다.  
  
 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값에 직접 추가 됩니다. 오프셋을 다른 값으로 변경 되 면 새 값은 여전히 각 설명자 필드의 값에 직접 추가 됩니다. 새 오프셋 필드 값 및 모든 이전 오프셋의 합계에 추가 되지 않습니다.  
  
## <a name="descriptors"></a>설명자  
 매개 변수에 바인딩되는 방식을 Apd 및 Ipd 필드에 의해 결정 됩니다. 인수에 **SQLBindParameter** 설명자 필드를 설정 하는 데 사용 됩니다. 필드 여도 설정할 수 있습니다는 **SQLSetDescField** 작동 하지만 **SQLBindParameter** 를호출하는설명자핸들을얻기위해응용프로그램에없기때문에사용하여이더효율적**SQLBindParameter**합니다.  
  
> [!CAUTION]  
>  호출 **SQLBindParameter** 하나의 문으로 다른 문의 영향을 줄 수에 대 한 합니다. 문과 연결 된를 명시적으로 할당 되 고 있을 때 다른 문의 연관 발생 합니다. 때문에 **SQLBindParameter** 수정 필드는 APD의 수정이이 설명자와 관련 된 모든 문에 적용 합니다. 필요한 동작 없는 경우 호출 하기 전에 응용 프로그램에서 다른 문이이 설명자를 분리 해야 **SQLBindParameter**합니다.  
  
 개념적으로 **SQLBindParameter** 시퀀스의 다음 단계를 수행 합니다.  
  
1.  호출 [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) APD 핸들을 가져올 수 있습니다.  
  
2.  호출 [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) APD의 SQL_DESC_COUNT 필드를 가져오지 경우의 값은 *ColumnNumber* SQL_DESC_COUNT, 호출의 값을 초과 하는 인수 **SQLSetDescField**SQL_DESC_COUNT에 값을 늘리려면 다음 *ColumnNumber*합니다.  
  
3.  호출 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 여러 번 APD의 다음 필드에 값을 할당 합니다.  
  
    -   SQL_DESC_TYPE과 SQL_DESC_CONCISE_TYPE의 값을 설정 *ValueType*한다는 점을 제외 하는 경우 *ValueType* 하나는 날짜/시간 또는 간격 하위 간결한 식별자 중 SQL_를 SQL_DESC_TYPE 설정 날짜/시간 또는 sql_interval 인, 각각 SQL_DESC_CONCISE_TYPE 간결한 식별자를 설정 하 고 해당 날짜/시간 또는 간격 하위 코드 값을 SQL_DESC_DATETIME_INTERVAL_CODE 설정 합니다.  
  
    -   SQL_DESC_OCTET_LENGTH 필드의 값으로 설정 *BufferLength*합니다.  
  
    -   값에 SQL_DESC_DATA_PTR 필드가 설정 *ParameterValue*합니다.  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 필드의 값으로 설정 *StrLen_or_Ind*합니다.  
  
    -   SQL_DESC_INDICATOR_PTR 필드의 값도 설정 *StrLen_or_Ind*합니다.  
  
     *StrLen_or_Ind* 표시기 정보와 매개 변수 값에 대 한 길이 모두 매개 변수를 지정 합니다.  
  
4.  호출 [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) IPD 핸들을 가져올 수 있습니다.  
  
5.  호출 [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) IPD의 SQL_DESC_COUNT 필드를 가져오지 경우의 값은 *ColumnNumber* SQL_DESC_COUNT, 호출의 값을 초과 하는 인수 **SQLSetDescField**SQL_DESC_COUNT에 값을 늘리려면 다음 *ColumnNumber*합니다.  
  
6.  호출 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 여러 번는 IPD의 다음 필드에 값을 할당 합니다.  
  
    -   SQL_DESC_TYPE과 SQL_DESC_CONCISE_TYPE의 값을 설정 *ParameterType*한다는 점을 제외 하는 경우 *ParameterType* 하나 날짜/시간 또는 간격 하위 간결한 식별자의 SQL_DESC_TYPE 설정 SQL_DATETIME 또는 sql_interval 인을 간결 하 게 식별자 및 해당 날짜/시간 또는 간격 하위 코드에 사용할 값을 SQL_DESC_DATETIME_INTERVAL_CODE 세트에 각각 SQL_DESC_CONCISE_TYPE을 설정합니다.  
  
    -   적합 한 SQL_DESC_LENGTH, SQL_DESC_PRECISION, 및 SQL_DESC_DATETIME_INTERVAL_PRECISION, 중 하나 이상을 설정 *ParameterType*합니다.  
  
    -   값으로 설정 하는 자릿수가 SQL_DESC_SCALE *DecimalDigits*합니다.  
  
 경우에 대 한 호출 **SQLBindParameter** 실패 APD의 설정한 것과 설명자 필드의 내용이 정의 하 고 APD의 SQL_DESC_COUNT 필드는 변경 되지 않습니다. 그리고 SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE, 및 SQL_DESC_TYPE 필드는 IPD의 적절 한 레코드의 정의 되지 않습니다.는 IPD의 SQL_DESC_COUNT 필드는 변경 되지 않습니다.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>SQLSetParam 간에서 호출의 변환  
 ODBC 1.0 응용 프로그램 호출 하는 경우 **SQLSetParam** ODBC 3에서. *x* 드라이버에서 ODBC 3. *x* 드라이버 관리자는 다음 표에 나와 있는 것 처럼 호출을 매핑합니다.  
  
|ODBC 1.0 응용 프로그램에 의해 호출|ODBC 3 호출 합니다. *x* 드라이버|  
|----------------------------------|-------------------------------|  
|SQLSetParam (StatementHandle, ParameterNumber, ValueType, ParameterType, LengthPrecision, ParameterScale, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, *ColumnSize*, *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX,      StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램에 ORDERS 테이블에 데이터를 삽입 하는 SQL 문을 준비 합니다. 응용 프로그램 호출 문의 각 매개 변수에 대해 **SQLBindParameter** ODBC C 데이터 형식 및 매개 변수의 SQL 데이터 형식을 지정 하 고 버퍼를 각 매개 변수에 바인딩할 수 있습니다. 데이터 값을 각 매개 변수 및 호출 응용 프로그램 데이터의 각 행에 대 한 할당 **SQLExecute** 문을 실행할 수 있습니다.  
  
 다음 샘플 Northwind Northwind 데이터베이스와 연결 된 사용자의 컴퓨터에서 ODBC 데이터 원본이 있다고 가정 합니다.  
  
 더 많은 코드 예제를 참조 하십시오. [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLProcedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md), [SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md), 및 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램 명명된 된 매개 변수를 사용 하 여 SQL Server 저장 프로시저를 실행 합니다.  
  
```  
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|문의 매개 변수에 대 한 정보 반환|[SQLDescribeParam 함수](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|문에서 매개 변수 버퍼를 해제합니다.|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|문 매개 변수 개수 반환|[SQLNumParams 함수](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|에 대 한 데이터를 보내는 다음 매개 변수를 반환 합니다.|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|여러 매개 변수 값 지정|[SQLParamOptions 함수](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
