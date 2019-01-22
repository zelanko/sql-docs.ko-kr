---
title: SQLBindParameter 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79f340d95cf1cd15b176069458347b2bea97055c
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420218"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 함수

**규칙**  
 도입 된 버전: ODBC 2.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLBindParameter** 버퍼 SQL 문에서 매개 변수 표식에 바인딩합니다. **SQLBindParameter** 기본 드라이버 유니코드 데이터를 지원 하지 않는 경우에 유니코드 C 데이터 형식으로 바인딩을 지원 합니다.  
  
> [!NOTE]  
>  이 함수는 ODBC 1.0 함수를 대체 **SQLSetParam**합니다. 자세한 내용은 "설명입니다."을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
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
 [입력] 매개 변수 번호 순서가 지정 된 순차적으로 증가 매개 변수 순서에 1에서 시작 합니다.  
  
 *InputOutputType*  
 [입력] 형식 매개 변수입니다. 자세한 내용은 참조 하세요. "*InputOutputType* 인수"에서 "설명"입니다.  
  
 *ValueType*  
 [입력] 매개 변수의 C 데이터 형식입니다. 자세한 내용은 참조 하세요. "*ValueType* 인수"에서 "설명"입니다.  
  
 *ParameterType*  
 [입력] 매개 변수의 SQL 데이터 형식입니다. 자세한 내용은 참조 하세요. "*ParameterType* 인수"에서 "설명"입니다.  
  
 *ColumnSize*  
 [입력] 열 또는 식의 해당 매개 변수 표식 크기입니다. 자세한 내용은 참조 하세요. "*ColumnSize* 인수"에서 "설명"입니다.  
  
 를 64 비트 Windows 운영 체제에서 응용 프로그램를 실행 하는 경우 참조 [ODBC 64-Bit 정보](../../../odbc/reference/odbc-64-bit-information.md)합니다.  
  
 *DecimalDigits*  
 [입력] 열 또는 해당 매개 변수 표식의 식의 10 진수입니다. 열 크기에 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.  
  
 *ParameterValuePtr*  
 [지연된 입력] 매개 변수의 데이터에 대 한 버퍼에 대 한 포인터입니다. 자세한 내용은 참조 하세요. "*ParameterValuePtr* 인수"에서 "설명"입니다.  
  
 *BufferLength*  
 [입력/출력] 길이 *ParameterValuePtr* 바이트 버퍼입니다. 자세한 내용은 참조 하세요. "*BufferLength* 인수"에서 "설명"입니다.  
  
 참조 [ODBC 64-Bit 정보](../../../odbc/reference/odbc-64-bit-information.md)이면 응용 프로그램을 64 비트 운영 체제에서 실행 됩니다.  
  
 *StrLen_or_IndPtr*  
 [지연된 입력] 매개 변수의 길이 대 한 버퍼에 대 한 포인터입니다. 자세한 내용은 참조 하세요. "*StrLen_or_IndPtr* 인수"에서 "설명"입니다.  
  
## <a name="returns"></a>반환 값

 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단

 때 **SQLBindParameter** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLBindParameter** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  

|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|으로 식별 되는 데이터 형식 합니다 *ValueType* 인수에서 식별 되는 데이터 형식으로 변환할 수 없습니다는 *ParameterType* 인수입니다. 이 오류를 반환할 수 있습니다는 **SQLExecDirect**, **SQLExecute**, 또는 **SQLPutData** 여는 대신 실행 시 **SQLBindParameter**.|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 지정 된 값 (DM) *상태로* 1 미만입니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 **MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|잘못 된 응용 프로그램 버퍼 형식|인수에 의해 지정 된 값 *ValueType* 유효한 C 데이터 형식 또는 SQL_C_DEFAULT 없습니다.|  
|HY004|잘못 된 SQL 데이터 형식|인수에 지정 된 값 *ParameterType* 유효한 ODBC SQL 데이터 형식 식별자도 아니고 드라이버별 SQL 데이터 형식 식별자를 드라이버에서 지원 되었습니다.|  
|HY009|잘못 된 인수 값|(DM) 인수 *ParameterValuePtr* 가 null 포인터 인수 *StrLen_or_IndPtr* 가 null 포인터와 인수의 *InputOutputType* SQL_PARAM_ 없습니다. 출력입니다.<br /><br /> (DM) SQL_PARAM_OUTPUT 위치 인수 *ParameterValuePtr* 가 null 포인터 C 형식 문자 또는 이진 및는 BufferLength 되었습니다 (*cbValueMax*) 0 보다 큽니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 계속 실행 될 때 **SQLBindParameter** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY021|일관성이 없는 설명자 정보|일관성 확인 중 선택 설명자 정보를 일관 되지 않았습니다. ("일관성 확인" 섹션을 참조 하세요 **SQLSetDescField**.)<br /><br /> 인수에 지정 된 값 *DecimalDigits* 로 지정 된 SQL 데이터 형식의 열에 대 한 데이터 원본에서 지원 되는 값의 범위를 벗어났습니다 합니다 *ParameterType* 인수입니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 값 *BufferLength* 0 보다 작습니다. (SQL_DESC_DATA_PTR 필드에 대 한 설명을 참조 하세요 **SQLSetDescField**.)|  
|HY104|잘못 된 정밀도 또는 배율 값|인수에 지정 된 값 *ColumnSize* 하거나 *DecimalDigits* 으로 지정 된 SQL 데이터 형식의 열에 대 한 데이터 원본에서 지원 되는 값의 범위를 벗어났습니다는  *ParameterType* 인수입니다.|  
|HY105|잘못 된 매개 변수 형식|인수에 지정 된 값 (DM) *InputOutputType* 올바르지 않습니다. ("주석입니다." 참조)|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본과 인수에 지정 된 값의 조합에 의해 지정 된 변환을 지원 하지 않습니다 *ValueType* 인수에 지정 된 드라이버 관련 값 *ParameterType*.<br /><br /> 인수에 지정 된 값 *ParameterType* ODBC의 버전 드라이버에서 지원 되지만 드라이버나 데이터 원본에서 지원 되지에 대 한 유효한 ODBC SQL 데이터 형식 식별자가 있습니다.<br /><br /> 드라이버는 ODBC 2에만 지원합니다. *x* 고 인수가 *ValueType* 다음 중 하나 였습니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 에 나열 된 모든 C 간격 데이터 형식 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식입니다.<br /><br /> 드라이버 3.50, 및 인수 이전 ODBC 버전 지원 *ValueType* SQL_C_GUID 되었습니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석

 응용 프로그램 호출 **SQLBindParameter** SQL 문에서 각 매개 변수 표식을 바인딩합니다. 바인딩에 응용 프로그램이 호출 될 때까지 계속 적용 됩니다 **SQLBindParameter** 다시 호출 **SQLFreeStmt** SQL_RESET_PARAMS 옵션 또는 호출 **SQLSetDescField** 를 APD의 SQL_DESC_COUNT 헤더 필드를 0으로 설정 합니다.  
  
 매개 변수에 대 한 자세한 내용은 참조 하십시오 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다. 매개 변수 데이터 형식 및 매개 변수 표식에 대 한 자세한 내용은 참조 하세요. [매개 변수 데이터 형식](../../../odbc/reference/appendixes/parameter-data-types.md) 하 고 [매개 변수 표식을](../../../odbc/reference/appendixes/parameter-markers.md) 부록 c: SQL 문법입니다.  
  
## <a name="parameternumber-argument"></a>상태로 인수  
 하는 경우 *상태로* 호출에 **SQLBindParameter** SQL_DESC_COUNT의 값 보다 크면 **SQLSetDescField** SQL_DESC_의 가치를 높일 라고 계산 *상태로*입니다.  
  
## <a name="inputoutputtype-argument"></a>InputOutputType 인수  
 합니다 *InputOutputType* 인수 매개 변수의 형식을 지정 합니다. 이 인수는 IPD의으로 필드를 설정 합니다. 와 같은 프로시저를 호출 하지 않는 SQL 문의 모든 매개 변수에 **삽입** 문의 *입력 * * 매개 변수*합니다. 프로시저 호출에서 매개 변수 입력 될 수 있습니다, 입/출력 또는 출력 매개 변수입니다. (응용 프로그램 호출 **SQLProcedureColumns** ; 프로시저 호출에서 매개 변수의 형식을 확인 하려면 해당 형식을 확인할 수 없는 매개 변수는 입력된 매개 변수 것으로 가정 합니다.)  
  
 합니다 *InputOutputType* 인수는 다음 값 중 하나:  
  
-   SQL_PARAM_INPUT. 매개 변수 표시와 같은 프로시저를 호출 하지 않는 SQL 문에서 매개 변수를 **삽입** 문 또는 프로시저에서 입력된 매개 변수를 표시 합니다. 예를 들어, 매개 변수 **직원 값에 삽입 (?,?,?)**  입력된 매개 변수는 매개 변수 **{AddEmp 호출 (?,?,?)}**  일 수 있지만 입력된 매개 변수가 필요 합니다.  
  
     드라이버; 데이터 원본에는 매개 변수에 대 한 데이터를 보냅니다 문이 실행 될 때 합니다 \* *ParameterValuePtr* 버퍼에 유효한 입력된 값이 있어야 합니다. 또는 **StrLen_or_IndPtr* 버퍼 SQL_NULL_DATA, SQL_DATA_AT_EXEC를 또는 SQL_LEN_DATA_AT 결과가 있어야 합니다. _EXEC 매크로입니다.  
  
     응용 프로그램에는 프로시저 호출에서 매개 변수의 형식을 확인할 수 없습니다, 경우에 설정 *InputOutputType* SQL_PARAM_INPUT;에 데이터 소스 매개 변수의 값을 반환 하는 경우 드라이버 삭제 합니다.  
  
-   SQL_PARAM_INPUT_OUTPUT. 매개 변수는 프로시저에서는 입/출력 매개 변수를 표시합니다. 예를 들어, 매개 변수 **{GetEmpDept(?) 호출}**  직원의 이름을 허용 하 고 직원의 부서 이름을 반환 하는 입/출력 매개 변수입니다.  
  
     드라이버; 데이터 원본에는 매개 변수에 대 한 데이터를 보냅니다 문이 실행 될 때 합니다 \* *ParameterValuePtr* 버퍼에 유효한 입력된 값이 있어야 합니다. 또는 \* *StrLen_or_IndPtr* 버퍼 SQL_NULL_DATA, SQL_DATA_AT_EXEC 또는 결과가 있어야 합니다. SQL_LEN_DATA_AT_EXEC 매크로입니다. 드라이버 응용 프로그램에 매개 변수는 데이터를 반환 문이 실행 된 후 드라이버를 설정 하는 데이터 소스는 입/출력 매개 변수 값을 반환 하지 않으면는 **StrLen_or_IndPtr* 버퍼를 sql_null_data로 합니다.  
  
    > [!NOTE]  
    >  ODBC 1.0 응용 프로그램을 호출할 때 **SQLSetParam** 에서 ODBC 2.0 드라이버를 드라이버 관리자는이를 변환에 대 한 호출 **SQLBindParameter** 나타나는 합니다 *InputOutputType* 인수는 SQL_PARAM_INPUT_OUTPUT로 설정 됩니다.  
  
-   SQL_PARAM_OUTPUT. 매개 변수는 프로시저 또는 출력 매개 변수는 프로시저의 반환 값을 표시 두 경우 모두이 라고 *출력 매개 변수*합니다. 예를 들어, 매개 변수 **{? = GetNextEmpID 호출}** 다음 직원 ID를 반환 하는 출력 매개 변수  
  
     하지 않는 한 드라이버의 응용 프로그램에 데이터 매개 변수를 반환 문이 실행 된 후의 *ParameterValuePtr* 및 *StrLen_or_IndPtr* 가 모두 null 포인터인 경우 인수는 드라이버는 출력 값을 삭제합니다. 드라이버를 설정 하는 데이터 원본에서 출력 매개 변수 값을 반환 하지 않으면는 **StrLen_or_IndPtr* 버퍼를 sql_null_data로 합니다.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. 입력/출력 매개 변수를 스트리밍할 수 해야 나타냅니다. **SQLGetData** 파트의 매개 변수 값을 읽을 수 있습니다. *BufferLength* 호출에서 버퍼 길이 확인할 수는 무시 됩니다 **SQLGetData**합니다. 값을 *StrLen_or_IndPtr* 버퍼 SQL_NULL_DATA, SQL_DEFAULT_PARAM을 SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과 포함 해야 합니다. 출력에서 스트리밍됩니다 경우 입력에서 데이터 실행 시 (DAE) 매개 변수로 매개 변수를 바인딩해야 합니다. *ParameterValuePtr* 에서 반환 되는 null이 아닌 포인터 값이 될 수 있습니다 **SQLParamData** 사용 하 여 사용자 정의 값을 토큰으로 전달한 *ParameterValuePtr* 두 입력 및 출력입니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
-   SQL_PARAM_OUTPUT_STREAM. 출력 매개 변수의 SQL_PARAM_INPUT_OUTPUT_STREAM와 동일 합니다. **StrLen_or_IndPtr* 입력에서 무시 됩니다.  
  
 다음 표에서 다양 한 조합을 *InputOutputType* 및 **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|결과|ParameterValuePtr에 주석 표시|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|입력된 부분|*ParameterValuePtr* 포인터 값에서 반환 될 수 있지만 **SQLParamData** 사용 하 여 사용자 정의 값을 토큰으로 전달한 *ParameterValuePtr*합니다.|  
|SQL_PARAM_INPUT|하지 SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|입력 버퍼를 바인딩된|*ParameterValuePtr* 입력된 버퍼의 주소입니다.|  
|SQL_PARAM_OUTPUT|입력에서 무시 됩니다.|바인딩된 출력 버퍼|*ParameterValuePtr* 출력 버퍼의 주소입니다.|  
|SQL_PARAM_OUTPUT_STREAM|입력에서 무시 됩니다.|스트리밍된 출력|*ParameterValuePtr* 하 여 반환할 포인터 값이 될 수 있습니다 **SQLParamData** 사용 하 여 사용자 정의 값을 토큰으로 전달한 *ParameterValuePtr*합니다.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|파트에서 입력된 및 출력 바인딩된 버퍼|*ParameterValuePtr* 에서 반환 될 수도 있는 출력 버퍼의 주소 **SQLParamData** 사용 하 여 사용자 정의 값을 토큰으로 전달한 *ParameterValuePtr*합니다.|  
|SQL_PARAM_INPUT_OUTPUT|하지 SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|바인딩된 버퍼와 출력 바인딩된 버퍼를 입력 합니다.|*ParameterValuePtr* 공유 입/출력 버퍼의 주소입니다.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) 또는 SQL_DATA_AT_EXEC|입력된에 파트 및 스트리밍된 출력|*ParameterValuePtr* 반환한는 null이 아닌 포인터 값이 될 수 있습니다 **SQLParamData** 사용 하 여 사용자 정의 값을 토큰으로 전달한 *ParameterValuePtr* 두 입력에 대 한 및 출력을 추가 합니다.|  
  
> [!NOTE]  
>  드라이버 스트리밍되므로 응용 프로그램 출력 또는 입력 / 출력 매개 변수를 바인딩할 때 허용 되는 SQL 형식을 결정 해야 합니다. 드라이버 관리자는 잘못 된 SQL 형식에 대 한 오류를 생성 하지 않습니다.  
  
## <a name="valuetype-argument"></a>ValueType 인수

 합니다 *ValueType* 인수 매개 변수의 C 데이터 형식을 지정 합니다. 이 인수는 APD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE, 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정합니다. 값 중 하나 이어야 합니다는 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션의 부록 d: 데이터 형식입니다.  
  
 경우는 *ValueType* 인수는 interval 데이터 형식을의 SQL_DESC_TYPE 필드 중 하나는 *상태로* SQL_INTERVAL APD의 레코드를로, APD의 SQL_DESC_CONCISE_TYPE 필드를로 설정 간결한 간격 데이터 형식 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 *상태로* 레코드 특정 간격 데이터 형식에 대 한 하위 코드가로 설정 됩니다. (참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).) 선행 정밀도 (2) 및 기본 간격 초 전체 자릿수 (6)는 APD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 자릿수가 SQL_DESC_PRECISION 필드에 설정 된 대로 각각 기본 간격은 데이터에 사용 됩니다. 두 기본 전체 자릿수 적합 하지 않은 경우 응용 프로그램이 명시적으로 설정 해야 설명자 필드를 호출한 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다.  
  
 경우는 *ValueType* 인수는 datetime 데이터 형식의 경우의 SQL_DESC_TYPE 필드 중 하나는 *상태로* SQL_DATETIME, SQL_DESC_CONCISE_TYPE 필드를 APD의레코드를로*상태로* APD의 레코드를 간결한 datetime C 데이터 형식 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드로 합니다 *상태로* 레코드를 특정 날짜/시간에 대 한 하위 코드가 데이터 형식입니다. (참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 경우는 *ValueType* 인수가 경우 SQL_C_NUMERIC 데이터 형식의 기본 전체 자릿수 (드라이버에서 정의 된를 임)이 고 기본 소수 자릿수 (0)는 APD의 SQL_DESC_PRECISION 및 자릿수가 SQL_DESC_SCALE 필드에 설정 된 대로 사용 되는 데이터입니다. 기본 전체 자릿수 또는 소수 적합 하지 않은 경우 응용 프로그램이 명시적으로 설정 해야 설명자 필드를 호출한 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다.  
  
 SQL_C_DEFAULT를 지정 된 매개 변수 값을 사용 하 여 지정 된 SQL 데이터 형식에 대 한 기본 C 데이터 형식에서 전송할 수 *ParameterType*합니다.  
  
 또한 확장된 C 데이터 유형을 지정할 수 있습니다. 자세한 내용은 [odbc에서 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.  
  
 자세한 내용은 [기본 C 데이터 형식](../../../odbc/reference/appendixes/default-c-data-types.md)를 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md), 및 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 부록 d: 데이터 형식입니다.  
  
## <a name="parametertype-argument"></a>ParameterType 인수

 에 나열 된 값 중 하나 이어야 합니다는 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 섹션의 부록 d: 데이터 형식 또는 드라이버 관련 값 이어야 합니다. 이 인수는 IPD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE, 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정합니다.  
  
 경우는 *ParameterType* 인수가 datetime 식별자 중 하나, IPD의 SQL_DESC_TYPE 필드 SQL_DATETIME로 설정 됩니다, IPD의 SQL_DESC_CONCISE_TYPE 필드를 간결 하 게 datetime SQL 데이터 형식 및는 SQL_DESC_로 설정 DATETIME_INTERVAL_CODE 필드는 적절 한 날짜/시간 하위 코드 값으로 설정 됩니다.  
  
 하는 경우 *ParameterType* 하나인 간격 식별자 IPD의 SQL_DESC_TYPE 필드 SQL_INTERVAL로 설정 되어, IPD의 SQL_DESC_CONCISE_TYPE 필드를 간결 하 게 SQL 간격 데이터 형식 및는 SQL_DESC_DATETIME_로 설정 IPD의 INTERVAL_CODE 필드 하위 코드를 적절 한 간격으로 설정 됩니다. IPD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드를 선행 간격 정밀도로 설정 하 고 SQL_DESC_PRECISION 필드는 해당 하는 경우 간격 시간 (초) 정밀도로 설정 됩니다. SQL_DESC_DATETIME_INTERVAL_PRECISION 또는 SQL_DESC_PRECISION의 기본 값을 적절 한 없으면 응용 프로그램이 명시적으로 설정 해야 호출 하 여 **SQLSetDescField**합니다. 이러한 필드에 대 한 자세한 내용은 참조 하세요. [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.  
  
 경우는 *ValueType* 인수가 SQL_NUMERIC 데이터 형식 (드라이버에서 정의 된를 임) 기본 전체 자릿수가 고 기본 소수 자릿수 (0), IPD의 SQL_DESC_PRECISION 및 자릿수가 SQL_DESC_SCALE 필드에 설정 된 대로 사용 되는 데이터입니다. 기본 전체 자릿수 또는 소수 적합 하지 않은 경우 응용 프로그램이 명시적으로 설정 해야 설명자 필드를 호출한 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다.  
  
 데이터를 변환 하는 방법에 대 한 자세한 내용은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 하 고 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 부록 d: 데이터 형식입니다.  
  
## <a name="columnsize-argument"></a>ColumnSize 인수

 합니다 *ColumnSize* 인수는 열 또는 매개 변수 표식에 해당 데이터 또는 둘 다의 길이에 해당 하는 식의 크기를 지정 합니다. SQL 데이터 형식에 따라 IPD의 다른 필드를 설정 하는이 인수 (합니다 *ParameterType* 인수). 이 매핑에 다음 규칙이 적용 됩니다.  
  
-   하는 경우 *ParameterType* SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY,이 아니거나 의값으로설정되어간결한SQLdatetime또는간격데이터형식,IPD의SQL_DESC_LENGTH필드중하나 *ColumnSize*합니다. (자세한 내용은 참조는 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 섹션의 부록 d: 데이터 형식입니다.)  
  
-   하는 경우 *ParameterType* SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL, 또는 SQL_DOUBLE, IPD의 SQL_DESC_PRECISION 필드의 값으로 설정 됩니다 *ColumnSize*합니다.  
  
-   다른 데이터 형식에 대 한 합니다 *ColumnSize* 인수는 무시 됩니다.  
  
 자세한 내용은 "매개 변수 값 전달"과에서 SQL_DATA_AT_EXEC를 참조 하세요. "*StrLen_or_IndPtr* 인수입니다."  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 인수

 하는 경우 *ParameterType* SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND, 또는 SQL_INTERVAL_MINUTE_TO_SECOND, IPD의 SQL_DESC_PRECISION 필드 설정 되어 하 *DecimalDigits*합니다. 하는 경우 *ParameterType* SQL_NUMERIC 인지 SQL_DECIMAL, IPD의 자릿수가 SQL_DESC_SCALE 필드로 설정 됩니다 *DecimalDigits*합니다. 다른 모든 데이터 형식에 대 한 합니다 *DecimalDigits* 인수는 무시 됩니다.  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 인수

 *ParameterValuePtr* 인수는 버퍼를 가리키는 하는 경우 **SQLExecute** 또는 **SQLExecDirect** 라고, 실제 데이터 매개 변수를 포함 합니다. 데이터를 지정한 형식에 있어야 합니다 *ValueType* 인수입니다. 이 인수는 APD의 SQL_DESC_DATA_PTR 필드가 설정합니다. 응용 프로그램을 설정할 수는 *ParameterValuePtr* 있다면 null 포인터에 대 한 인수  *\*StrLen_or_IndPtr* SQL_NULL_DATA 또는 SQL_DATA_AT_EXEC입니다. (이 적용 됩니다만 입력 또는 입/출력 매개 변수.)  
  
 경우 \* *StrLen_or_IndPtr* 결과 SQL_LEN_DATA_AT_EXEC입니다 (*길이*) 매크로 또는 SQL_DATA_AT_EXEC, 한 다음 *ParameterValuePtr* 는 매개 변수를 사용 하 여 연결 된 응용 프로그램 정의 포인터 값입니다. 통해 응용 프로그램에 반환 되기 **SQLParamData**합니다. 예를 들어 *ParameterValuePtr* 매개 변수 번호, 데이터에 대 한 포인터 또는 응용 프로그램 입력된 매개 변수를 바인딩하는 데 사용 된 구조에 대 한 포인터와 같은 0이 아닌 토큰을 수 있습니다. 그러나 경우에는 매개 변수는 입/출력 매개 변수를 *ParameterValuePtr* 출력 값을 저장할 버퍼에 대 한 포인터 여야 합니다. SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1 보다 크면 응용 프로그램 함께 문 특성 sql_attr_params_processed_ptr은 가리키는 값을 사용할 수는 *ParameterValuePtr* 인수입니다. 예를 들어 *ParameterValuePtr* 값의 배열을 가리키는 및 응용 프로그램에서는 SQL_ATTR_PARAMS_PROCESSED_PTR 가리키는 값을 사용 하 여 배열에서 올바른 값을 검색할 수 있습니다. 자세한 내용은이 섹션의 뒷부분에 나오는 "매개 변수 값 전달"을 참조 하세요.  
  
 경우는 *InputOutputType* 인수가, SQL_PARAM_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT *ParameterValuePtr* 드라이버가 출력 값을 반환 하는 버퍼를 가리킵니다. 프로시저는 하나 이상의 결과 집합을 반환 하는 경우는 \* *ParameterValuePtr* 버퍼 모든 결과 집합/행 개수 처리 될 때까지 설정할 보장 되지 않습니다. 버퍼 처리가 완료 될 때까지 설정 되지 않은 출력 매개 변수 및 반환 값을 사용할 수 없는 경우 될 때까지 **SQLMoreResults** SQL_NO_DATA를 반환 합니다. 호출 **SQLCloseCursor** 하거나 **SQLFreeStmt** 를 SQL_CLOSE 옵션을 사용 하 여 이러한 값을 삭제 하면 됩니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성에 값이 1 보다 크면 *ParameterValuePtr* 배열을 가리킵니다. 단일 SQL 문으로 입력 또는 입/출력 매개 변수의 입력된 값의 완전 한 배열을 처리 하 고 출력 매개 변수를 입/출력에 대 한 출력 값의 배열을 반환 합니다.  
  
## <a name="bufferlength-argument"></a>BufferLength 인수

 문자 및 이진 C 데이터에 대 한 합니다 *BufferLength* 의 길이 지정 하는 인수를 \* *ParameterValuePtr* 버퍼 (있으면 단일 요소) 또는 합니다 요소의길이\* *ParameterValuePtr* (SQL_ATTR_PARAMSET_SIZE 문 특성의 값을 1 보다 큰 경우) 배열입니다. 이 인수는 APD의 SQL_DESC_OCTET_LENGTH 레코드 필드를 설정합니다. 응용 프로그램에 여러 값을 지정 하는 경우 *BufferLength* 에 있는 값의 위치를 결정 하는 데 사용 되는 **ParameterValuePtr* 입력 및 출력 모두 배열입니다. 입/출력 및 출력 매개 변수에 대 한 문자 및 이진 C 데이터 출력 자를 결정 하기 위해 사용 됩니다.  
  
-   C 문자 데이터를 반환할 수 있는 바이트 수가 보다 크거나 같은 경우에 대 한 *BufferLength*, 데이터가 \* *ParameterValuePtr* 잘립니다  *BufferLength* null 종결 문자 길이의 덜 및 드라이버에 의해 null로 종결 됩니다.  
  
-   이진 C 데이터 반환에 사용할 수 있는 바이트 수가 보다 크면 *BufferLength*의 데이터를 \* *ParameterValuePtr* 잘립니다 *BufferLength*바이트입니다.  
  
 다른 모든 유형의 C 데이터에 대 한 합니다 *BufferLength* 인수는 무시 됩니다. 길이 \* *ParameterValuePtr* 버퍼 (있으면 단일 요소) 또는 요소 길이 \* *ParameterValuePtr* (응용 프로그램 를호출하는경우배열 **SQLSetStmtAttr** 사용 하 여는 *특성* SQL_ATTR_PARAMSET_SIZE 각 매개 변수에 대해 여러 값을 지정 하려면 인수의) C 데이터 형식의 길이 것으로 간주 됩니다.  
  
 스트리밍된 출력 또는 스트리밍된 입/출력 매개 변수를 *BufferLength* 인수는 버퍼 길이 지정 되어 있으므로 무시 됩니다 **SQLGetData**합니다.  
  
> [!NOTE]  
>  ODBC 1.0 응용 프로그램을 호출할 때 **SQLSetParam** 는 ODBC 3. *x* 드라이버를 드라이버 관리자를이를 변환에 대 한 호출 **SQLBindParameter** 는 합니다 *BufferLength* 인수는 항상 SQL_SETPARAM_VALUE_MAX 합니다. 드라이버 관리자 오류를 반환을 ODBC 3 때문에. *x* 응용 프로그램 집합 *BufferLength* 에 SQL_SETPARAM_VALUE_MAX는 ODBC 3. *x* 드라이버는 ODBC 1.0 응용 프로그램에서 호출 되는 경우를 결정 하는 데 사용할 수 있습니다.  
  
> [!NOTE]  
>  **SQLSetParam**응용 프로그램의 길이 지정 하는 방식으로 **ParameterValuePtr* 드라이버 문자 또는 이진 데이터 및 응용 프로그램 전송 하는 방식으로 반환할 수 있도록 버퍼를 배열 문자 또는 이진 매개 변수 값이 드라이버는 드라이버 정의 합니다.  
  
## <a name="strlenorindptr-argument"></a>StrLen_or_IndPtr Argument

 합니다 *StrLen_or_IndPtr* 인수는 버퍼를 가리키는 하는 경우 **SQLExecute** 또는 **SQLExecDirect** 호출 되 면 다음 중 하나를 포함 합니다. (이 인수는 응용 프로그램 매개 변수에 대 한 포인터의 SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 레코드 필드를 설정합니다.)  
  
-   에 저장 된 매개 변수 값의 길이 **ParameterValuePtr*합니다. 문자 또는 이진 C 데이터를 제외 하 고는 무시 됩니다.  
  
-   SQL_NTS. 매개 변수 값은 null로 끝나는 문자열.  
  
-   SQL_NULL_DATA. 매개 변수 값은 NULL입니다.  
  
-   SQL_DEFAULT_PARAM. 프로시저를 응용 프로그램에서 검색 된 값 대신 매개 변수의 기본값을 사용 하는 것입니다. 이 값은 ODBC 정식 구문을 호출 하는 프로시저에만 유효 고 경우에만 합니다 *InputOutputType* 인수가 SQL_PARAM_INPUT 또는 SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM 합니다. 때 \* *StrLen_or_IndPtr* SQL_DEFAULT_PARAM으로가 *ValueType*를 *ParameterType*를 *ColumnSize*,  *DecimalDigits*하십시오 *BufferLength*, 및 *ParameterValuePtr* 인수 입력된 매개 변수에 대 한 무시 되 고 입력에 대 한 출력 매개 변수 값을 정의 하는 데에 사용 됩니다 / 출력 매개 변수입니다.  
  
-   결과 SQL_LEN_DATA_AT_EXEC (*길이*) 매크로입니다. 데이터 매개 변수를 사용 하 여 발송 **SQLPutData**합니다. 경우는 *ParameterType* 인수는 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 long 이면 데이터 소스 관련 데이터 형식이 며 드라이버 "Y" SQL_NEED_LONG_DATA_LEN 정보 유형에 대해에서 반환 **SQLGetInfo**, *길이* ; 매개 변수에 대해 보낼 데이터의 바이트 수이 고, 그렇지 *길이* 음수가 아닌 값 이어야 하며 무시 됩니다. 자세한 내용은 "전달 매개 변수 값을이 섹션의 뒷부분에 나오는 참조 하세요.  
  
     예를 들어, 10, 000 바이트의 데이터를 사용 하 여 전송 되지 않는다는 지정할 **SQLPutData** SQL_LONGVARCHAR 매개 변수를 하나 이상의 호출을 응용 프로그램 설정 **StrLen_or_IndPtr* SQL_LEN_DATA_AT_EXEC ( 10000)입니다.  
  
-   SQL_DATA_AT_EXEC. 데이터 매개 변수를 사용 하 여 발송 **SQLPutData**합니다. ODBC 3를 호출할 때이 값은 ODBC 1.0 응용 프로그램에서 사용 됩니다. *x* 드라이버입니다. 자세한 내용은 "전달 매개 변수 값을이 섹션의 뒷부분에 나오는 참조 하세요.  
  
 하는 경우 *StrLen_or_IndPtr* 가 null 포인터인 경우 모든 입력된 매개 변수 값이 NULL이 아닌 지 고 문자 및 이진 데이터를 null로 끝나는 드라이버 가정 합니다. 하는 경우 *InputOutputType* SQL_PARAM_OUTPUT 또는 SQL_PARAM_OUTPUT_STREAM 및 *ParameterValuePtr* 하 고 *StrLen_or_IndPtr* 가 모두 null 포인터인 드라이버 삭제 출력 값입니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자에 대 한 null 포인터를 지정 해서는 안 됩니다 *StrLen_or_IndPtr* 매개 변수의 데이터 형식 SQL_C_BINARY 경우. 드라이버는 예기치 않게 잘리지 않았음을 SQL_C_BINARY 데이터, 되도록 *StrLen_or_IndPtr* 유효한 길이 값에 대 한 포인터를 포함 해야 합니다.  
  
 경우는 *InputOutputType* 인수가 SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM, 또는 SQL_PARAM_OUTPUT_STREAM 합니다 *StrLen_or_IndPtr* 버퍼를 가리키는 드라이버가 SQL_NULL_DATA에에서 반환할 사용 가능한 바이트의 수를 반환 합니다. \* *ParameterValuePtr* (null 종료 바이트의 문자 데이터 제외) 또는 SQL_NO_TOTAL (경우에 사용할 수 있는 바이트 수 반환 확인할 수 없습니다). 프로시저는 하나 이상의 결과 집합을 반환 하는 경우는 **StrLen_or_IndPtr* 버퍼를 인출 된 모든 결과 설정할 보장 되지 않습니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성에 값이 1 보다 크면 *StrLen_or_IndPtr* SQLLEN 값의 배열을 가리킵니다. 이이 섹션의 앞부분에 나열 된 값 중 하나일 수 있습니다 하 고 단일 SQL 문을 사용 하 여 처리 됩니다.  
  
## <a name="passing-parameter-values"></a>매개 변수 값 전달

 응용 프로그램 매개 변수 값을 하거나 전달할 수에 합니다 \* *ParameterValuePtr* 버퍼 또는 하나 이상의 호출을 사용 하 여 **SQLPutData**합니다. 데이터는 사용 하 여 전달 된 매개 변수 **SQLPutData** 이라고 *실행 시 데이터* 매개 변수입니다. 이러한 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 매개 변수에 대 한 데이터를 보내는 데 일반적으로 사용 되 고 다른 매개 변수와 함께 사용할 수 있습니다.  
  
 매개 변수 값을 전달 하려면 응용 프로그램에는 다음 일련의 단계를 수행 합니다.  
  
1.  호출 **SQLBindParameter** 매개 변수의 값에 대 한 버퍼를 바인딩할 각 매개 변수에 대해 (*ParameterValuePtr* 인수) 및 길이/표시기 (*StrLen_or_IndPtr* 인수)입니다. 실행 시 데이터 매개 변수에 대 한 *ParameterValuePtr* 매개 변수 개수 또는 데이터에 대 한 포인터와 같은 응용 프로그램 정의 포인터 값입니다. 값을 나중에 반환할 및 매개 변수 식별을 사용할 수 있습니다.  
  
2.  입력 및 입/출력 매개 변수의 값을 배치 합니다 \* *ParameterValuePtr* 및 **StrLen_or_IndPtr* 버퍼:  
  
    -   일반 매개 변수에 대 한 응용 프로그램에서 매개 변수 값을 배치 합니다 \* *ParameterValuePtr* 버퍼와 해당 값의 길이 **StrLen_or_IndPtr* 버퍼입니다. 자세한 내용은 [매개 변수 값 설정](../../../odbc/reference/develop-app/setting-parameter-values.md)합니다.  
  
    -   응용 프로그램 실행 시 데이터 매개 변수에 대해 SQL_LEN_DATA_AT_EXEC 결과 배치 (*길이*) 매크로 (ODBC 2.0 드라이버를 호출) 하는 경우에 **StrLen_or_IndPtr* 버퍼입니다.  
  
3.  호출 **SQLExecute** 하거나 **SQLExecDirect** SQL 문을 실행 합니다.  
  
    -   실행 시 데이터 매개 변수가 없는 경우에 프로세스가 완료 되었습니다.  
  
    -   모든 실행 시 데이터 매개 변수가 있는 경우 sql_need_data가 반환 됩니다.  
  
4.  호출 **SQLParamData** 에 지정 된 응용 프로그램 정의 값을 검색 하는 *ParameterValuePtr* 인수의 **SQLBindParameter** 첫 번째 처리할 실행 시 데이터 매개 변수입니다. **SQLParamData** returns SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  반환 되는 값 이지만 실행 시 데이터 매개 변수가 실행 시 데이터 열과 비슷한 **SQLParamData** 마다 다릅니다. 실행 시 데이터 매개 변수는 매개 변수는 데이터를 보낼 사용 하 여 SQL 문에서 **SQLPutData** 문을 사용 하 여 실행 될 때 **SQLExecDirect** 또는 **SQLExecute**. 사용 하 여 바인딩된 **SQLBindParameter**합니다. 반환 된 값 **SQLParamData** 에 전달 하는 포인터 값 **SQLBindParameter** 에 *ParameterValuePtr* 인수입니다. 실행 시 데이터 열이 있는 데이터를 보낼 사용 하 여 행 집합의 열 **SQLPutData** 행이 업데이트 되거나 추가 된 경우 **SQLBulkOperations** 사용 하 여 업데이트 또는 **SQLSetPos**. 사용 하 여 바인딩된 **SQLBindCol**합니다. 반환 된 값 **SQLParamData** 에 있는 행의 주소는 **TargetValuePtr* 버퍼 (를 호출 하 여 설정 **SQLBindCol**) 처리 되는 합니다.  
  
5.  호출 **SQLPutData** 한 번 이상 매개 변수에 대해 데이터를 보내도록 합니다. 데이터 값 보다 큰 경우 둘 이상의 호출이 필요 합니다 \* *ParameterValuePtr* 에 지정 된 버퍼 **SQLPutData**;를 여러 번 호출 **SQLPutData**동일한 매개 변수는 문자, 이진 또는 데이터 소스 특정 데이터 형식의 열에 문자 데이터를 전송 하는 경우에 또는 문자를 이진 열에 이진 C 데이터를 보낼 때 수 또는 데이터 소스 특정 데이터 형식에 대 한 합니다.  
  
6.  호출 **SQLParamData** 매개 변수의 모든 데이터가 전송 된는 신호를 다시 합니다.  
  
    -   자세한 실행 시 데이터 매개 변수가 **SQLParamData** 처리할 SQL_NEED_DATA 및 다음 실행 시 데이터 매개 변수에 대 한 응용 프로그램 정의 값을 반환 합니다. 응용 프로그램 4, 5 단계를 반복합니다.  
  
    -   더 이상 실행 시 데이터 매개 변수가 있는 경우에 프로세스가 완료 되었습니다. 문이 성공적으로 실행 하는 경우 **SQLParamData** SQL_SUCCESS 또는; SQL_SUCCESS_WITH_INFO를 반환 합니다. 실행 하지 못했습니다 SQL_ERROR를 반환 합니다. 이때 **SQLParamData** 문을 실행 하는 데 사용 되는 함수에 의해 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다 (**SQLExecDirect** 하거나 **SQLExecute**).  
  
         입/출력 또는 출력 매개 변수의 출력 값에 사용할 수는 \* *ParameterValuePtr* 및 **StrLen_or_IndPtr* 응용 프로그램은 모든 결과 집합을 검색 한 후 버퍼링 문에 의해 생성 됩니다.  
  
 호출 **SQLExecute** 하거나 **SQLExecDirect** SQL_NEED_DATA 상태의 문을 배치 합니다. 이 시점에서 응용 프로그램 에서만 호출할 수 있습니다 **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**하십시오 **SQLGetFunctions**, **SQLParamData**, 또는 **SQLPutData** 문을 사용 하 여 또는 *연결 핸들* 문과 사용 하 여 연결 합니다. SQLSTATE HY010 반환 문 또는 문과 사용 하 여 관련 연결을 사용 하 여 다른 함수를 호출 하는 경우 (함수 시퀀스 오류). SQL_NEED_DATA 상태의 문 리프 **SQLParamData** 하거나 **SQLPutData** 오류를 반환 **SQLParamData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 또는 문을 취소 됩니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLCancel** 드라이버 문 실행 취소 드라이버 실행 시 데이터 매개 변수에 대 한 데이터를 필요로 하, 동안; 응용 프로그램을 호출할 수 있습니다 **SQLExecute** 또는 **SQLExecDirect** 다시 합니다.  
  
## <a name="retrieving-streamed-output-parameters"></a>스트리밍된 출력 매개 변수 검색

 응용 프로그램 설정 하는 경우 *InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM 출력 매개 변수 값을 하나 이상 호출 하 여 검색 해야 **SQLGetData**합니다. 드라이버 응용 프로그램에 반환할 스트리밍된 출력 매개 변수 값에 있는 경우 SQL_PARAM_DATA_AVAILABLE 다음 함수에 대 한 호출에 대 한 응답에서 반환 됩니다. **SQLMoreResults**하십시오 **SQLExecute**, 및 **SQLExecDirect**합니다. 응용 프로그램 호출 **SQLParamData** 사용할 수 있는 매개 변수 값을 확인 하려면.  
  
 SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 참조 하세요. [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
## <a name="using-arrays-of-parameters"></a>매개 변수 배열 사용

 응용 프로그램 매개 변수 표식과 매개 변수 배열 전달을 사용 하 여 문을 준비를 하는 경우에 두 가지가이 실행 될 수 있습니다. 한 가지 방법은 원자 단위로 처리 됩니다 하는 경우 매개 변수 배열 사용 하 여 전체 문이 백 엔드의 배열 처리 기능을 사용 하려면 드라이버입니다. Oracle은 배열 처리 기능을 지 원하는 데이터 원본의 예입니다. 이 기능을 구현 하는 또 다른 방법은 각 매개 변수 배열에 매개 변수 집합에 대 한 하나 이상의 SQL 문이 SQL 문 일괄 처리를 생성 하 고 일괄 처리 실행 드라이버입니다. 매개 변수 배열을 사용 하 여 사용할 수 없습니다는 **업데이트 WHERE CURRENT OF** 문입니다.  
  
 매개 변수 배열을 처리 될 때 개별 결과 집합/행 개수 (각 매개 변수 집합에 대해 하나)를 사용할 수 있습니다 또는 결과 집합/행 개수는 하나로 롤업 될 수 있습니다. 옵션은 SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo** 행 개수 매개 변수 (SQL_PARC_BATCH)의 각 집합에 사용할 수 있는 하나의 행 개수는 사용할 수 있습니다 (SQL_PARC_NO_BATCH) 여부를 나타냅니다.  
  
 옵션은 SQL_PARAM_ARRAY_SELECTS **SQLGetInfo** 결과 집합은 각 매개 변수 (SQL_PAS_BATCH) 집합에 사용할 수 있는 하나의 결과 집합을 사용할 수 있습니다 (SQL_PAS_NO_BATCH) 여부를 나타냅니다. 드라이버는 결과 집합 생성 문을 매개 변수 배열을 사용 하 여 실행을 허용 하지 않으면 SQL_PARAM_ARRAY_SELECTS SQL_PAS_NO_SELECT를 반환 합니다.  
  
 자세한 내용은 [SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)합니다.  
  
 배열 매개 변수를 지원 하려면 각 매개 변수에 대해 값의 수를 지정 하려면 SQL_ATTR_PARAMSET_SIZE 문 특성 설정 됩니다. 필드 1 보다 큰 경우 APD의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR 필드 배열을 가리켜야 합니다. 각 배열의 카디널리티 SQL_ATTR_PARAMSET_SIZE 값과 동일합니다.  
  
 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드에는 처리 된 경우 오류 집합을 포함 하 여 매개 변수 집합 수를 포함 하는 버퍼를 가리킵니다. 각 매개 변수 집합을 처리 하면 드라이버는 새 값을 버퍼에 저장 합니다. 이 null 포인터인 경우 번호가 없으면 반환 됩니다. 매개 변수 배열을 사용 하는 경우에 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드에서 가리키는 값 설정 함수에서 sql_error가 반환 하는 경우에 채워집니다. Sql_need_data가 반환 되 면 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드에서 가리키는 값이 처리 되는 매개 변수 집합에 설정 됩니다.  
  
 매개 변수 배열이 바인딩되어 있을 때와 어떤 일이 발생 하는지 **업데이트 WHERE CURRENT OF** 문이 실행 되는 드라이버 정의 합니다.  
  
## <a name="column-wise-parameter-binding"></a>열 단위 매개 변수 바인딩

 열 단위 바인딩을 응용 프로그램 각 매개 변수를 별도 매개 변수 및 배열 길이/표시기를 바인딩합니다.  
  
 열 단위 바인딩을 사용 하려면 응용 프로그램을 SQL_PARAM_BIND_BY_COLUMN SQL_ATTR_PARAM_BIND_TYPE 문 특성 먼저 설정 합니다. (이것이 기본값입니다.) 응용 프로그램을 바인딩할 각 열에 대해 다음 단계를 수행 합니다.  
  
1.  매개 변수 버퍼 배열을 할당합니다.  
  
2.  길이/표시기 버퍼 배열을 할당합니다.  
  
    > [!NOTE]  
    >  응용 프로그램은 열 단위 바인딩을 사용 하는 경우 설명자에 직접 쓰는, 별도 배열 길이 및 표시기 데이터에 대해 사용할 수 있습니다.  
  
3.  호출 **SQLBindParameter** 다음 인수를 사용 합니다.  
  
    -   *ValueType* C 유형 매개 변수 버퍼 배열의 단일 요소입니다.  
  
    -   *ParameterType* SQL 유형 매개 변수입니다.  
  
    -   *ParameterValuePtr* 매개 변수 버퍼 배열의 주소입니다.  
  
    -   *BufferLength* 크기 매개 변수 버퍼 배열의 단일 요소입니다. 합니다 *BufferLength* 데이터는 고정 길이 데이터 인수는 무시 됩니다.  
  
    -   *StrLen_or_IndPtr* 주소 길이/표시기 배열입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "주석,"에서 "ParameterValuePtr 인수"를 참조 하세요. 매개 변수의 열 단위 바인딩에 대 한 자세한 내용은 참조 하세요 [매개 변수의 배열 바인딩](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)합니다.  
  
## <a name="row-wise-parameter-binding"></a>행 단위 매개 변수 바인딩

 행 단위 바인딩은 응용 프로그램 바인딩할 각 매개 변수에 대해 매개 변수 및 길이/표시기 버퍼를 포함 하는 구조체를 정의 합니다.  
  
 행 단위 바인딩을 사용 하려면 응용 프로그램에는 다음 단계를 수행 합니다.  
  
1.  단일 매개 변수 (매개 변수 및 길이/표시기 버퍼 포함) 집합을 보유 하는 구조체를 정의 하 고 이러한 구조 배열을 할당 합니다.  
  
    > [!NOTE]  
    >  응용 프로그램은 행 단위 바인딩을 사용 하는 경우 설명자에 직접 쓰는, 별도 필드 길이 및 표시기 데이터에 대해 사용할 수 있습니다.  
  
2.  매개 변수를 바인딩해야 하는 버퍼의 인스턴스 크기 또는 단일 매개 변수 집합을 포함 하는 구조체의 크기를 SQL_ATTR_PARAM_BIND_TYPE 문 특성을 설정 합니다. 길이 바인딩된 매개 변수를 모두 및 구조 또는 주소는 바인딩된 매개 변수를 지정된 된 길이 사용 하 여 증가 하는 경우 결과에서 동일한 매개 변수 부분을 가리키게 됩니다 있도록 버퍼의 패딩에 대 한 공간을 포함 해야 합니다 다음 행입니다. 사용 하는 경우는 *sizeof* ANSI c에서 연산자를이 동작이 유지 됩니다.  
  
3.  호출 **SQLBindParameter** 바인딩할 각 매개 변수에 대해 다음 인수를 사용 합니다.  
  
    -   *ValueType* 열에 바인딩할 매개 변수 버퍼 멤버의 형식입니다.  
  
    -   *ParameterType* SQL 유형 매개 변수입니다.  
  
    -   *ParameterValuePtr* 첫 번째 배열 요소에서 매개 변수 버퍼 멤버의 주소입니다.  
  
    -   *BufferLength* 매개 변수 버퍼 멤버의 크기입니다.  
  
    -   *StrLen_or_IndPtr* 바인딩할 길이/표시기 멤버의 주소입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. "*ParameterValuePtr* 인수"이이 섹션의 뒷부분에 나오는. 매개 변수의 행 단위 바인딩은 대 한 자세한 내용은 참조는 [매개 변수의 배열 바인딩](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)합니다.  
  
## <a name="error-information"></a>오류 정보

 드라이버 (SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 SQL_PARC_NO_BATCH 같음) 일괄 처리로 매개 변수 배열 구현 하지 않으면, 오류 상황 한 문이 실행 된 것 처럼 처리 됩니다. 응용 프로그램의 SQL 문 또는 매개 변수 배열에는 매개 변수는 매개 변수를 확인 하려면 IPD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 사용할 수 드라이버가 일괄 처리로 배열 매개 변수를 구현 하는 경우  **SQLExecDirect** 나 **SQLExecute** 오류를 반환 합니다. 이 필드는 매개 변수 값의 각 행에 대 한 상태 정보를 포함합니다. 필드는 오류가 발생 했음을 나타냅니다, 진단 데이터 구조의 필드 못한 매개 변수의 행 및 매개 변수 번호를 표시 합니다. 배열의 요소 수가 SQL_ATTR_PARAMSET_SIZE 문 특성으로 설정할 수 있는 APD의 SQL_DESC_ARRAY_SIZE 헤더 필드로 정의 됩니다.  
  
> [!NOTE]  
>  APD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드 매개 변수를 무시 됩니다. 매개 변수는 무시 하는 방법에 대 한 자세한 내용은 다음 섹션에서는 "매개 변수 집합을 무시 합니다."을 참조 하세요.  
  
 때 **SQLExecute** 하거나 **SQLExecDirect** SQL_ERROR를 반환 SQL_DESC_ARRAY_STATUS_PTR IPD 필드에서 가리키는 배열의 요소가 SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_ 포함 됩니다 PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED, 또는 SQL_PARAM_DIAG_UNAVAILABLE 합니다.  
  
 이 배열의 각 요소에 대해 진단 데이터 구조는 하나 이상의 상태 레코드를 포함합니다. 구조의 SQL_DIAG_ROW_NUMBER 필드는 오류를 발생 시키는 매개 변수 값의 행 수를 나타냅니다. 오류를 발생 시킨 매개 변수의 행에서 특정 매개 변수를 확인할 수 있으면 매개 변수 번호 SQL_DIAG_COLUMN_NUMBER 필드에 입력 됩니다.  
  
 강제 적용 하는 이전 매개 변수에서 오류가 발생 하기 때문에 매개 변수가 사용 되지 않은 경우 입력 SQL_PARAM_UNUSED **SQLExecute** 또는 **SQLExecDirect** 중단 합니다. 매개 변수를 발생 시킨 40 집합을 실행 하는 동안 오류가 발생 했습니다 경우 50 개의 매개 변수 및 예를 들어 **SQLExecute** 또는 **SQLExecDirect** SQL_PARAM_UNUSED에 입력 한 다음 중단 된 상태 배열 매개 변수부터 50 41입니다.  
  
 SQL_PARAM_DIAG_UNAVAILABLE는 드라이버가 개별 매개 변수 수준의 오류 정보를 생성 하지 않도록 매개 변수 배열 모놀리식 단위로 처리 하는 경우 시작 됩니다.  
  
 단일 매개 변수 집합을 처리 하는 일부 오류 때문에 중지 된 배열의 후속 매개 변수 집합이 처리. 다른 오류 후속 매개 변수를 처리 하는 영향을 주지 않습니다. 오류 처리가 중지 되는 드라이버 정의 됩니다. 처리 중지 되지 않은, 배열에 있는 모든 매개 변수 처리, SQL_SUCCESS_WITH_INFO 오류를 결과로 반환 되 고 sql_attr_params_processed_ptr은 정의한 버퍼를 처리 하는 매개 변수 집합의 총 수로 (정의 된 대로 합니다 SQL_ATTR_PARAMSET_SIZE 문 특성), 오류 집합을 포함 하는 합니다.  
  
> [!CAUTION]  
>  ODBC 동작 매개 변수 배열 처리에서 오류가 발생 하면 ODBC 3에서 다릅니다. *x* ODBC 2에 비해. *x*합니다. Odbc 2. *x*, 함수 반환 SQL_ERROR 및 처리를 활성화 합니다. 가리키는 버퍼를 *pirow* 인수의 **SQLParamOptions** 오류 행의 수를 포함 합니다. Odbc 3. *x*, SQL_SUCCESS_WITH_INFO를 반환 하는 함수 및 월을 하거나 처리를 중지 또는 계속 합니다. 계속 해 서을 sql_attr_params_processed_ptr은 지정한 버퍼 오류가 발생 하는 포함 하 여 처리 하 고, 모든 매개 변수의 값으로 설정 됩니다. 이 동작 변경이 기존 응용 프로그램에 대 한 문제를 발생할 수 있습니다.  
  
 때 **SQLExecute** 하거나 **SQLExecDirect** 에서는 상태 배열을 포함 하는 SQL_ERROR 또는 sql_need_data가 반환 될 때와 같은 매개 변수 배열의 모든 매개 변수 집합의 처리를 완료 하기 전에 반환 이미 처리 된 이러한 매개 변수에 대 한 상태입니다. IPD의 SQL_DESC_ROWS_PROCESSED_PTR 필드에서 가리키는 위치 SQL_ERROR 또는 SQL_NEED_DATA 오류 코드를 발생 시킨 매개 변수 배열의 행 수를 포함 합니다. 상태 배열 값의 가용성에 드라이버에서 정의 된;은 SELECT 문에 매개 변수 배열의 보내면 문이 실행 된 또는 집합 인출로 인해 후 찾아볼 수 있습니다.  
  
## <a name="ignoring-a-set-of-parameters"></a>매개 변수 집합을 무시합니다.

 SQL 문에 바인딩된 매개 변수 집합을를 무시 해야 함을 나타내려면 (SQL_ATTR_PARAM_STATUS_PTR 문 특성 설정) 된 대로 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드를 사용할 수 있습니다. 실행 하는 동안 하나 이상의 매개 변수 집합을 무시 하려면 드라이버에서 직접 응용 프로그램이 단계 따라야 합니다.  
  
1.  호출 **SQLSetDescField** SQLUSMALLINT 상태 정보를 포함 하는 값 배열을를 가리키도록 APD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 설정할 수 있습니다. 이 필드를 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** 사용 하 여는 *특성* SQL_ATTR_PARAM_OPERATION_PTR 설명자 핸들을 가져오지 않고도 필드를 설정 하려면 응용 프로그램을 허용 하는 중입니다.  
  
2.  두 값 중 하나로 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드에 의해 정의 된 배열의 각 요소를 설정 합니다.  
  
    -   SQL_PARAM_IGNORE 문 실행에서 행이 제외 되었음을 나타냅니다.  
  
    -   SQL_PARAM_PROCEED 행 문 실행에 포함 되어 있는지를 나타냅니다.  
  
3.  호출 **SQLExecDirect** 하거나 **SQLExecute** 준비 된 문을 실행 합니다.  
  
 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드에 의해 정의 된 배열에 다음과 같은 규칙이 적용 됩니다.  
  
-   포인터가 설정 되어 기본적으로 null로 합니다.  
  
-   포인터가 null 인 경우 모든 요소가 SQL_ROW_PROCEED로 설정 된 경우 모든 매개 변수 집합이 사용 됩니다.  
  
-   SQL_PARAM_PROCEED에 요소를 설정 합니다. 작업 매개 변수는 특정 집합을 사용할지는 보장 하지 않습니다.  
  
-   SQL_PARAM_PROCEED 헤더 파일에는 0으로 정의 됩니다.  
  
 응용 프로그램 IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드와 동일한 배열 가리키도록 APD의 가리키는 SQL_DESC_ARRAY_STATUS_PTR 필드로 설정할 수 있습니다. 이 매개 변수 행 데이터에 바인딩하는 경우에 유용 합니다. 매개 변수 행 데이터의 상태에 따라 다음 무시할 수 있습니다. SQL_PARAM_IGNORE, 외에도 다음 코드는 매개 변수를 무시 되도록 SQL 문에서 발생 합니다. SQL_ROW_DELETED, SQL_ROW_UPDATED, 및 SQL_ROW_ERROR SQL_PARAM_PROCEED, 외에도 다음 코드를 계속 하려면 SQL 문을 발생 합니다. SQL_ROW_SUCCESS SQL_ROW_SUCCESS_WITH_INFO, 하며 SQL_ROW_ADDED 합니다.  
  
## <a name="rebinding-parameters"></a>다시 바인딩 매개 변수

 응용 프로그램 바인딩을 변경 하려면 두 가지 작업 중 하나를 수행할 수 있습니다.  
  
-   호출 **SQLBindParameter** 이미 바인딩되어 있는 열에 대 한 새 바인딩을 지정 합니다. 드라이버를 새 인덱스로 이전 바인딩을 덮어씁니다.  
  
-   바인딩 호출에 의해 지정 된 버퍼 주소를 추가할 수에 대 한 오프셋을 지정 **SQLBindParameter**합니다. 자세한 내용은 다음 섹션을 참조 하세요. "오프셋을 사용 하 여 다시 바인딩해야 합니다."  
  
## <a name="rebinding-with-offsets"></a>오프셋을 사용 하 여 다시 바인딩

 매개 변수 다시 바인딩하는 응용 프로그램에 대 한 호출 하지만 많은 매개 변수를 포함할 수 있는 버퍼 영역 설치 프로그램은 때 특히 유용 **SQLExecDirect** 하거나 **SQLExecute** 매개 변수 중 일부만 사용 합니다. 오프셋으로 기존 바인딩을 수정 하 여 다음 매개 변수 집합에 대 한 버퍼 영역의 남은 공간을 사용할 수 있습니다.  
  
 APD의 SQL_DESC_BIND_OFFSET_PTR 헤더 필드 바인딩 오프셋을 가리킵니다. 필드가 null이 아닌 경우 드라이버는 포인터를 역참조 하 고, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR 필드에 값 null 포인터인 경우 설명자에 해당 필드에 역참조 된 값을 추가 실행 시간에 기록 합니다. 새로운 포인터 값에는 SQL 문이 실행 될 때 사용 됩니다. 오프셋 다시 바인딩 후 유효한 상태로 유지 합니다. SQL_DESC_BIND_OFFSET_PTR 자체의 오프셋 보다는 오프셋에 대 한 포인터 이기 때문에 응용 프로그램 변경할 수 오프셋을 직접 호출 하지 않고도 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 하거나 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) 를 설명자 필드를 변경 합니다. 포인터가 설정 되어 기본적으로 null로 합니다. 카드가 SQL_DESC_BIND_OFFSET_PTR 분야를 호출 하 여 설정할 수 있습니다 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 또는 호출 하 여 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)사용 하 여는 *fAttribute* SQL_ATTR_PARAM_BIND_의 OFFSET_PTR 합니다.  
  
 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값에 직접 추가 됩니다. 오프셋을 다른 값으로 변경 되 면 각 설명자 필드의 값에 직접 새 값 추가 계속 됩니다. 새 오프셋 필드 값 및 모든 이전 오프셋의 합에 추가 되지 않습니다.  
  
## <a name="descriptors"></a>설명자

 매개 변수가 바인딩된 어떻게 IPDs 고 Apd의 필드에 의해 결정 됩니다. 인수 **SQLBindParameter** 설명자 필드를 설정 하는 데 사용 됩니다. 필드 설정할 수도 있습니다는 **SQLSetDescField** 함수를 **SQLBindParameter** 호출설명자핸들을얻기위해응용프로그램에없기때문에사용하여이더효율적**SQLBindParameter**합니다.  
  
> [!CAUTION]  
>  호출 **SQLBindParameter** 하나의 문으로 다른 문의 영향을 줄 수에 대 한 합니다. 이 발생 된 문과 연결 된 카드가 명시적으로 할당 되 고 있을 때 다른 문과 사용 하 여 연결 합니다. 때문에 **SQLBindParameter** 필드를 수정 합니다 APD의 수정이이 설명자와 연결 된 모든 문이에 적용 합니다. 이 없는 경우 필요한 동작을 호출 하기 전에 응용 프로그램이 다른 문에서이 설명자를 분리 해야 **SQLBindParameter**합니다.  
  
 개념상 **SQLBindParameter** 시퀀스에서 다음 단계를 수행 합니다.  
  
1.  호출 [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) APD 핸들을 가져올 수 있습니다.  
  
2.  호출 [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) APD의 SQL_DESC_COUNT 필드를 가져오려는 경우의 값을 *ColumnNumber* SQL_DESC_COUNT, 호출의 값을 초과 하는 인수 **SQLSetDescField**SQL_DESC_COUNT 하의 값을 늘리려면 *ColumnNumber*합니다.  
  
3.  호출 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 여러 번 APD의 다음 필드에 값을 할당 합니다.  
  
    -   SQL_DESC_TYPE과 SQL_DESC_CONCISE_TYPE의 값을 설정 *ValueType*점을 제외 하 고, 경우 *ValueType* 하나인 datetime 또는 간격 하위 형식의 간결한 식별자, SQL_에 SQL_DESC_TYPE 설정 날짜/시간 또는 sql_interval 인, 간결한 식별자 SQL_DESC_CONCISE_TYPE를 설정 하 고 해당 날짜/시간 또는 간격 하위 코드 값을 SQL_DESC_DATETIME_INTERVAL_CODE 설정 각각.  
  
    -   SQL_DESC_OCTET_LENGTH 필드의 값으로 설정 *BufferLength*합니다.  
  
    -   값에 SQL_DESC_DATA_PTR 필드가 설정 *ParameterValue*합니다.  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 필드의 값으로 설정 *StrLen_or_Ind*합니다.  
  
    -   값도 SQL_DESC_INDICATOR_PTR 필드를 설정 *StrLen_or_Ind*합니다.  
  
     합니다 *StrLen_or_Ind* 표시기 정보와 매개 변수 값의 길이 매개 변수를 지정 합니다.  
  
4.  호출 [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) IPD 핸들을 가져올 수 있습니다.  
  
5.  호출 [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) IPD의 SQL_DESC_COUNT 필드를 가져오려는 경우의 값을 *ColumnNumber* SQL_DESC_COUNT, 호출의 값을 초과 하는 인수 **SQLSetDescField**SQL_DESC_COUNT 하의 값을 늘리려면 *ColumnNumber*합니다.  
  
6.  호출 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 여러 번 IPD의 다음 필드에 값을 할당 합니다.  
  
    -   SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE 값으로 설정 하는 *ParameterType*점을 제외 하 고 있으면 *ParameterType* 하나인 SQL_DESC_TYPE datetime 또는 간격 하위 형식의 간결한 식별자를 설정 SQL_DATETIME 또는 sql_interval 인에 각각 간결한 식별자를 해당 날짜/시간 또는 간격 하위 코드 값을 SQL_DESC_DATETIME_INTERVAL_CODE 집합 SQL_DESC_CONCISE_TYPE를 설정합니다.  
  
    -   SQL_DESC_LENGTH, 자릿수가 SQL_DESC_PRECISION, 및 SQL_DESC_DATETIME_INTERVAL_PRECISION, 하나 이상의 적합 한 설정 *ParameterType*합니다.  
  
    -   값으로 설정 하는 자릿수가 SQL_DESC_SCALE *DecimalDigits*합니다.  
  
 경우에 대 한 호출 **SQLBindParameter** 실패 APD의 설정한 것과 설명자 필드의 내용이 정의 및 APD의 SQL_DESC_COUNT 필드에는 변경 되지 않습니다. 또한 적절 한 레코드 IPD의 SQL_DESC_LENGTH, 자릿수가 SQL_DESC_PRECISION, 자릿수가 SQL_DESC_SCALE, 및 SQL_DESC_TYPE 필드를 정의 되지 않습니다 및 IPD의 SQL_DESC_COUNT 필드는 변경 되지 않습니다.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>SQLSetParam 간의 호출을 변환

 ODBC 1.0 응용 프로그램을 호출할 때 **SQLSetParam** 는 ODBC 3. *x* 드라이버는 ODBC 3. *x* 드라이버 관리자는 다음 표에 나와 있는 것 처럼 호출을 매핑합니다.  
  
|ODBC 1.0 응용 프로그램에서 호출|ODBC 3 호출 합니다. *x* 드라이버|  
|----------------------------------|-------------------------------|  
|SQLSetParam(      StatementHandle,      ParameterNumber,      ValueType,      ParameterType,      LengthPrecision,      ParameterScale,      ParameterValuePtr,      StrLen_or_IndPtr);|SQLBindParameter (StatementHandle 상태로, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType 합니다 *ColumnSize*를 *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX,      StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램에는 ORDERS 테이블에 데이터를 삽입 하는 SQL 문을 준비 합니다. 문의 각 매개 변수에 대해 응용 프로그램 호출 **SQLBindParameter** ODBC C 데이터 형식과 SQL 데이터 형식의 매개 변수를 지정 하 고 버퍼에 각 매개 변수에 바인딩할 수 있습니다. 데이터의 각 행에 대해 응용 프로그램 매개 변수 및 호출 각 데이터 값을 할당 **SQLExecute** 문을 실행 합니다.  
  
 다음 샘플에서는 northwind는 Northwind 데이터베이스에 연결 된 컴퓨터에서 ODBC 데이터 원본이 있다고 가정 합니다.  
  
 더 많은 코드 예제를 참조 하세요. [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLProcedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md)하십시오 [SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md), 및 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp
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

 다음 예제에서는 응용 프로그램에는 명명된 된 매개 변수를 사용 하 여 SQL Server 저장 프로시저를 실행 합니다.  
  
```cpp
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
|문에서 매개 변수에 대 한 정보를 반환합니다.|[SQLDescribeParam 함수](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|문에서 매개 변수 버퍼를 해제합니다.|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|문 매개 변수 개수를 반환합니다.|[SQLNumParams 함수](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|에 대 한 데이터를 보내도록 다음 매개 변수를 반환 합니다.|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|여러 매개 변수 값 지정|[SQLParamOptions 함수](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>관련 항목

 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
