---
title: SQLBind매개 변수 함수 | 마이크로 소프트 문서
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
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02f50862bcfb0295c7f098afc6856c91e0249f66
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301363"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 함수

**규칙**  
 버전 출시: ODBC 2.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLBindParameter** 는 SQL 문의 매개 변수 마커에 버퍼를 바인딩합니다. **SQLBindParameter는** 기본 드라이버가 유니코드 데이터를 지원하지 않는 경우에도 유니코드 C 데이터 형식에 대한 바인딩을 지원합니다.  
  
> [!NOTE]  
>  이 함수는 ODBC 1.0 함수 **SQLSetParam을**대체합니다. 자세한 내용은 '댓글'을 참조하세요.  
  
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

 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *매개 변수 번호*  
 [입력] 매개 변수 번호는 1부터 시작하여 증가하는 매개 변수 순서로 순차적으로 정렬됩니다.  
  
 *InputOutputType*  
 [입력] 매개 변수의 형식입니다. 자세한 내용은 *"주석"의 "입력 출력 유형* 인수"를 참조하십시오.  
  
 *Valuetype*  
 [입력] 매개 변수의 C 데이터 형식입니다. 자세한 내용은 "주석"의 *"ValueType* 인수"를 참조하십시오.  
  
 *매개 변수 유형*  
 [입력] 매개 변수의 SQL 데이터 형식입니다. 자세한 내용은 "주석"의 *"매개 변수 유형* 인수"를 참조하십시오.  
  
 *ColumnSize*  
 [입력] 해당 매개 변수 마커의 열 크기 또는 식입니다. 자세한 내용은 "주석"의 *"열 크기* 인수"를 참조하십시오.  
  
 응용 프로그램이 64비트 Windows 운영 체제에서 실행되는 경우 [ODBC 64비트 정보를](../../../odbc/reference/odbc-64-bit-information.md)참조하십시오.  
  
 *DecimalDigits*  
 [입력] 해당 매개 변수 마커의 열 또는 식의 소수 자릿수입니다. 열 크기에 대한 자세한 내용은 [열 크기, 소수 자릿수, 옥텟 전사 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.  
  
 *매개 변수 값 Ptr*  
 [지연 된 입력] 매개 변수의 데이터에 대 한 버퍼에 대 한 포인터입니다. 자세한 내용은 "주석"의 *"매개 변수값 Ptr* 인수"를 참조하십시오.  
  
 *버퍼 길이*  
 [입력/출력] *바이트내의 ParameterValuePtr* 버퍼의 길이입니다. 자세한 내용은 "주석"의 *"버퍼길이* 인수"를 참조하십시오.  
  
 [64비트](../../../odbc/reference/odbc-64-bit-information.md)운영 체제에서 응용 프로그램이 실행되는 경우 ODBC 64비트 정보를 참조하십시오.  
  
 *StrLen_or_IndPtr*  
 [지연 된 입력] 매개 변수의 길이에 대 한 버퍼에 대 한 포인터입니다. 자세한 내용은 "댓글"의 *"StrLen_or_IndPtr* 인수"를 참조하십시오.  
  
## <a name="returns"></a>반환

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단

 **SQLBindParameter** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_STMT *핸들 SQL_HANDLE_STMT* 및 문 *핸들* *핸들을* 사용 하 여 **SQLGetDiagRec를** 호출 하 여 가져올 수 있습니다. 다음 표에서는 **SQLBindParameter에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  

|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|*ValueType* 인수로 식별된 데이터 형식은 *ParameterType* 인수로 식별된 데이터 유형으로 변환할 수 없습니다. 이 오류는 **SQLExecute** **SQLPutData** **SQLBindParameter**. **SQLExecDirect**|  
|07009|잘못된 설명자 인덱스|(DM) 인수 *ParameterNumber에* 대해 지정된 값이 1보다 적습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. **MessageText* 버퍼에서 **SQLGetDiagRec에서** 반환된 오류 메시지는 오류와 그 원인을 설명합니다.|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|잘못된 응용 프로그램 버퍼 유형|인수 *ValueType에* 의해 지정 된 값 유효한 C 데이터 형식 또는 SQL_C_DEFAULT 아닙니다.|  
|HY004|잘못된 SQL 데이터 형식|ParameterType 인수에 *ParameterType* 대해 지정된 값은 유효한 ODBC SQL 데이터 형식 식별자도 아니고 드라이버에서 지원하는 드라이버 별 SQL 데이터 형식 식별자도 아닙니다.|  
|HY09|잘못된 인수 값|(DM) 인수 *ParameterValuePtr은* null 포인터이고 인수 *StrLen_or_IndPtr* null 포인터이고 *인수 InputOutputType은* SQL_PARAM_OUTPUT 않았습니다.<br /><br /> (DM) SQL_PARAM_OUTPUT 인수 *ParameterValuePtr이* null 포인터인 경우 C 형식은 char 또는 이진이고*버퍼길이(cbValueMax)는*0보다 큽니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLBindParameter가** 호출될 때 이 비동기 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 *함수는 StatementHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY021|일관되지 않은 설명자 정보|일관성 검사 중에 확인된 설명자 정보가 일치하지 않았습니다. **(SQLSetDescField의**"일관성 검사" 섹션을 참조하십시오.)<br /><br /> 인수 *DecimalDigits에* 대해 지정된 값은 *ParameterType* 인수에서 지정한 SQL 데이터 형식의 열에 대해 데이터 원본에서 지원하는 값 범위를 벗어났습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *버퍼길이의* 값이 0보다 적었습니다. **(SQLSetDescField에서**SQL_DESC_DATA_PTR 필드에 대한 설명을 참조하십시오.)|  
|HY104|잘못된 정밀도 또는 축척 값|*ColumnSize* 또는 *DecimalDigits* 인수에 대해 지정된 값은 *ParameterType* 인수에서 지정한 SQL 데이터 형식의 열에 대해 데이터 원본에서 지원하는 값 범위를 벗어났습니다.|  
|HY105|잘못된 매개 변수 유형|(DM) 인수 *InputOutputType에* 대해 지정된 값이 잘못되었습니다. ("댓글"참조))|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본인수 *ValueType에* 대해 지정된 값과 인수 *ParameterType에*대해 지정된 드라이버 별 값의 조합으로 지정된 변환을 지원하지 않습니다.<br /><br /> ParameterType 인수에 *ParameterType* 대해 지정된 값은 드라이버에서 지원하는 ODBC 버전에 대한 유효한 ODBC SQL 데이터 형식 식별자이지만 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> 드라이버는 ODBC 2만 지원합니다. *x* 및 인수 *ValueType은* 다음 중 하나입니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 부록 D: 데이터 형식의 [C 데이터 형식에](../../../odbc/reference/appendixes/c-data-types.md) 나열된 모든 간격 C 데이터 형식입니다.<br /><br /> 드라이버는 3.50 이전의 ODBC 버전만 지원하며 *ValueType* 인수가 SQL_C_GUID.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
  
## <a name="comments"></a>주석

 응용 프로그램은 **SQLBindParameter를** 호출하여 SQL 문의 각 매개 변수 마커를 바인딩합니다. 바인딩은 응용 프로그램이 **SQLBindParameter를** 다시 호출하거나, SQL_RESET_PARAMS 옵션으로 **SQLFreeStmt를** 호출하거나, **SQLSetDescField를** 호출하여 APD의 SQL_DESC_COUNT 헤더 필드를 0으로 설정할 때까지 적용됩니다.  
  
 매개 변수에 대한 자세한 내용은 [문 매개 변수 를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오. 매개 변수 데이터 형식 및 매개 변수 마커에 대한 자세한 내용은 부록 C: SQL 문법의 [매개 변수 데이터 유형](../../../odbc/reference/appendixes/parameter-data-types.md) 및 매개 변수 [마커를](../../../odbc/reference/appendixes/parameter-markers.md) 참조하십시오.  
  
## <a name="parameternumber-argument"></a>매개 변수 번호 인수  
 *매개 변수번호* **SQLBindParameter** 호출에서 SQL_DESC_COUNT 값보다 큰 **경우, SQLSetDescField는** SQL_DESC_COUNT 값을 증가하기 위해 호출됩니다. *ParameterNumber*  
  
## <a name="inputoutputtype-argument"></a>입력출력타입 인수  
 *입력출력유형* 인수는 매개변수의 형식을 지정합니다. 이 인수는 IPD의 SQL_DESC_PARAMETER_TYPE 필드를 설정합니다. **INSERT** 문과 같은 프로시저를 호출하지 않는 SQL 문의 모든 매개 변수는 *input**매개 변수입니다.* 프로시저 호출의 매개 변수는 입력, 입력/출력 또는 출력 매개 변수일 수 있습니다. 응용 프로그램은 **SQLProcedureColumns를** 호출하여 프로시저 호출에서 매개 변수의 형식을 결정합니다. 형식을 결정할 수 없는 매개 변수는 입력 매개 변수로 가정합니다.  
  
 *InputOutputType* 인수는 다음 값 중 하나입니다.  
  
-   SQL_PARAM_INPUT. 매개 변수는 **INSERT** 문과 같은 프로시저를 호출하지 않는 SQL 문의 매개 변수를 표시하거나 프로시저의 입력 매개 변수를 표시합니다. 예를 들어 **직원 값에 삽입(?, ?, ?)의** 매개 변수는 입력 매개 변수인 반면 **{call AddEmp(?, ?, ?)}의** 매개 변수는 입력 매개 변수일 수 있지만 반드시 입력 매개 변수는 아닐 수 있습니다.  
  
     문이 실행되면 드라이버는 매개 변수에 대한 데이터를 데이터 원본으로 보냅니다. \* *ParameterValuePtr* 버퍼에는 유효한 입력 값이 포함되어야 SQL_LEN_DATA_AT_EXEC SQL_DATA_AT_EXEC SQL_NULL_DATA*StrLen_or_IndPtr* 합니다.  
  
     응용 프로그램이 프로시저 호출에서 매개 변수의 형식을 확인할 수 없는 경우 *InputOutputType을* SQL_PARAM_INPUT 설정합니다. 데이터 원본이 매개 변수에 대한 값을 반환하면 드라이버는 매개 변수를 삭제합니다.  
  
-   SQL_PARAM_INPUT_OUTPUT. 매개 변수는 프로시저의 입력/출력 매개변수를 표시합니다. 예를 들어 **{call GetEmpDept(?)}의** 매개 변수는 직원의 이름을 수락하고 직원 부서의 이름을 반환하는 입력/출력 매개 변수입니다.  
  
     문이 실행되면 드라이버는 매개 변수에 대한 데이터를 데이터 원본으로 보냅니다. \* *ParameterValuePtr* 버퍼에는 유효한 입력 값이 포함되어야 합니다 SQL_LEN_DATA_AT_EXEC SQL_DATA_AT_EXEC SQL_NULL_DATA \* *StrLen_or_IndPtr.* 문이 실행된 후 드라이버는 매개 변수에 대한 데이터를 응용 프로그램에 반환합니다. 데이터 원본이 입력/출력 매개 변수에 대한 값을 반환하지 않는 경우 드라이버는*StrLen_or_IndPtr* 버퍼를 설정 SQL_NULL_DATA합니다.  
  
    > [!NOTE]  
    >  ODBC 1.0 응용 프로그램이 ODBC 2.0 드라이버에서 **SQLSetParam을** 호출하면 드라이버 관리자는 이를 **SQLBindParameter** 호출로 변환하여 *입력출력 유형* 인수가 SQL_PARAM_INPUT_OUTPUT 설정됩니다.  
  
-   SQL_PARAM_OUTPUT. 매개 변수는 프로시저의 프로시저 또는 출력 매개 변수의 반환 값을 표시합니다. 두 경우 모두 출력 *매개 변수라고 합니다.* 예를 들어 **{?=call GetNextEmpID}의** 매개 변수는 다음 직원 ID를 반환하는 출력 매개 변수입니다.  
  
     문이 실행된 후 Driver는 *ParameterValuePtr* 및 *StrLen_or_IndPtr* 인수가 모두 null 포인터가 아니라면 매개 변수에 대한 데이터를 응용 프로그램에 반환합니다. 데이터 원본이 출력 매개 변수에 대한 값을 반환하지 않는 경우 드라이버는 SQL_NULL_DATA **StrLen_or_IndPtr* 버퍼를 설정합니다.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. 입력/출력 매개 변수를 스트리밍해야 했음을 나타냅니다. **SQLGetData** 부분에서 매개 변수 값을 읽을 수 있습니다. *버퍼 길이는* **SQLGetData**의 호출에서 결정되므로 버퍼 길이는 무시됩니다. *StrLen_or_IndPtr* 버퍼의 값에는 SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과가 포함되어야 합니다. 매개 변수는 출력시 스트리밍되는 경우 입력 시 DAE(데이터 실행 시) 매개 변수로 바인딩되어야 합니다. *ParameterValuePtr* 은 **SQLParamData에서** 입력 및 출력 모두에 대해 *ParameterValuePtr로* 값이 전달된 사용자 정의 토큰으로 반환되는 비널 포인터 값일 수 있습니다. 자세한 내용은 [SQLGetData를 사용하여 출력 매개 변수 검색을](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)참조하십시오.  
  
-   SQL_PARAM_OUTPUT_STREAM. SQL_PARAM_INPUT_OUTPUT_STREAM 출력 매개 변수에 대해 동일합니다. **StrLen_or_IndPtr* 입력시 무시됩니다.  
  
 다음 표에는 *InputOutputType* 및 **StrLen_or_IndPtr*다른 조합이 나열되어 있습니다.  
  
|*InputOutputType*|**StrLen_or_IndPtr*|결과|매개 변수값Ptr에 대한 비고|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|*SQL_LEN_DATA_AT_EXEC(렌)* 또는 SQL_DATA_AT_EXEC|부품 입력|*ParameterValuePtr* 은 **SQLParamData에서** 해당 값이 *ParameterValuePtr*로 전달된 사용자 정의 토큰으로 반환되는 모든 포인터 값일 수 있습니다.|  
|SQL_PARAM_INPUT|*SQL_LEN_DATA_AT_EXEC(렌)* 또는 SQL_DATA_AT_EXEC|입력 바운드 버퍼|*매개 변수값 Ptr은* 입력 버퍼의 주소입니다.|  
|SQL_PARAM_OUTPUT|입력 시 무시됩니다.|출력 바운드 버퍼|*매개 변수값 Ptr은* 출력 버퍼의 주소입니다.|  
|SQL_PARAM_OUTPUT_STREAM|입력 시 무시됩니다.|스트리밍된 출력|*ParameterValuePtr은* 모든 포인터 값이 될 수 있으며, **이는 SQLParamData에서** 해당 값이 *ParameterValuePtr*로 전달된 사용자 정의 토큰으로 반환됩니다.|  
|SQL_PARAM_INPUT_OUTPUT|*SQL_LEN_DATA_AT_EXEC(렌)* 또는 SQL_DATA_AT_EXEC|부품 및 출력 바운드 버퍼의 입력|*ParameterValuePtr은* 출력 버퍼의 **주소이며, SQLParamData에서** 해당 값이 *ParameterValuePtr*로 전달된 사용자 정의 토큰으로 반환됩니다.|  
|SQL_PARAM_INPUT_OUTPUT|*SQL_LEN_DATA_AT_EXEC(렌)* 또는 SQL_DATA_AT_EXEC|입력 바운드 버퍼 및 출력 바인딩 버퍼|*ParameterValuePtr은* 공유 입력/출력 버퍼의 주소입니다.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|*SQL_LEN_DATA_AT_EXEC(렌)* 또는 SQL_DATA_AT_EXEC|부품 입력 및 스트리밍 출력|*ParameterValuePtr은* **SQLParamData에서** 입력 및 출력 모두에 대해 *ParameterValuePtr로* 값이 전달된 사용자 정의 토큰으로 반환되는 비널 포인터 값이 될 수 있습니다.|  
  
> [!NOTE]  
>  드라이버는 응용 프로그램이 스트림된 출력 또는 입력 출력 매개 변수를 바인딩할 때 허용되는 SQL 형식을 결정해야 합니다. 드라이버 관리자는 잘못된 SQL 형식에 대한 오류를 생성하지 않습니다.  
  
## <a name="valuetype-argument"></a>값 유형 인수

 *ValueType* 인수는 매개 변수의 C 데이터 형식을 지정합니다. 이 인수는 APD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정합니다. 부록 D: 데이터 [형식의 C 데이터 유형](../../../odbc/reference/appendixes/c-data-types.md) 섹션의 값 중 하나여야 합니다.  
  
 *DataType* 인수가 간격 데이터 형식 중 하나인 경우 APD의 *ParameterNumber* 레코드의 SQL_DESC_TYPE 필드가 SQL_INTERVAL 설정되고 APD의 SQL_DESC_CONCISE_TYPE 필드가 간결한 간격 데이터 유형으로 설정되고 *ParameterNumber* 레코드의 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 특정 간격 데이터 형식의 하위 코드로 설정됩니다. [(부록 D: 데이터 유형](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조)) APD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 SQL_DESC_PRECISION 필드에 설정된 기본 간격 정밀도(2)와 기본 간격 초 정밀도(6)가 각각 데이터에 사용됩니다. 기본 정밀도 중 하나가 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec**에 대한 호출로 설명자 필드를 명시적으로 설정해야 합니다.  
  
 *DataType* 인수가 날짜 시간 데이터 형식 중 하나인 경우 *APD의 ParameterNumber* 레코드의 SQL_DESC_TYPE 필드가 SQL_DATETIME 설정되고, *APD의 parameterNumber* 레코드의 SQL_DESC_CONCISE_TYPE 필드가 간결한 datetime C 데이터 유형으로 설정되고, *ParameterNumber* 레코드의 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 특정 날짜 시간 데이터 형식의 하위 코드로 설정됩니다. [(부록 D: 데이터 유형](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조))  
  
 *ValueType* 인수가 SQL_C_NUMERIC 데이터 형식인 경우 기본 정밀도(드라이버 정의) 및 기본 축척(0)이 APD의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정된 대로 데이터에 사용됩니다. 기본 정밀도 또는 배율이 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec**에 대한 호출로 설명자 필드를 명시적으로 설정해야 합니다.  
  
 SQL_C_DEFAULT ParameterType으로 지정된 SQL 데이터 형식에 대한 기본 C 데이터 형식에서 매개 변수 값을 전송되도록 *지정합니다.*  
  
 확장 된 C 데이터 형식을 지정할 수도 있습니다. 자세한 내용은 [ODBC의 C 데이터 유형을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)참조하십시오.  
  
 자세한 내용은 [기본 C 데이터 유형,](../../../odbc/reference/appendixes/default-c-data-types.md) [C에서 SQL 데이터 유형으로 의 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)및 부록 D: 데이터 [형식의 SQL에서 C 데이터 유형으로 데이터를 변환하는 것을](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 참조하십시오.  
  
## <a name="parametertype-argument"></a>매개 변수 유형 인수

 이 값은 부록 D: 데이터 [형식의 SQL 데이터 유형](../../../odbc/reference/appendixes/sql-data-types.md) 섹션에 나열된 값 중 하나여야 하며 드라이버별 값이어야 합니다. 이 인수는 IPD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정합니다.  
  
 *ParameterType* 인수가 datetime 식별자 중 하나인 경우 IPD의 SQL_DESC_TYPE 필드가 SQL_DATETIME 설정되고 IPD의 SQL_DESC_CONCISE_TYPE 필드가 간결한 datetime SQL 데이터 유형으로 설정되고 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 적절한 datetime 하위 코드 값으로 설정됩니다.  
  
 *ParameterType이* 간격 식별자 중 하나인 경우 IPD의 SQL_DESC_TYPE 필드가 SQL_INTERVAL 설정되고, IPD의 SQL_DESC_CONCISE_TYPE 필드가 간결한 SQL 간격 데이터 유형으로 설정되고 IPD의 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 적절한 간격 서브코드로 설정됩니다. IPD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 정밀도를 선도하는 간격으로 설정되고 SQL_DESC_PRECISION 필드는 해당되는 경우 간격 초 정밀도로 설정됩니다. SQL_DESC_DATETIME_INTERVAL_PRECISION 또는 SQL_DESC_PRECISION 기본값이 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField**을 호출하여 명시적으로 설정해야 합니다. 이러한 필드에 대한 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)을 참조하십시오.  
  
 *ValueType* 인수가 SQL_NUMERIC 데이터 형식인 경우 IPD의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정된 기본 정밀도(드라이버 정의) 및 기본 축척(0)이 데이터에 사용됩니다. 기본 정밀도 또는 배율이 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec**에 대한 호출로 설명자 필드를 명시적으로 설정해야 합니다.  
  
 데이터를 변환하는 방법에 대한 자세한 내용은 [C에서 SQL 데이터 유형으로 데이터를 변환하고](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 부록 D: 데이터 [형식의 SQL 데이터 유형에서 C 데이터 유형으로 데이터를 변환하는 것을](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 참조하십시오.  
  
## <a name="columnsize-argument"></a>열 크기 인수

 *ColumnSize* 인수는 매개 변수 마커, 해당 데이터의 길이 또는 둘 다에 해당하는 열 또는 식의 크기를 지정합니다. 이 인수는 SQL 데이터 *형식(ParameterType* 인수)에 따라 IPD의 다른 필드를 설정합니다. 다음 규칙은 이 매핑에 적용됩니다.  
  
-   *ParameterType이* SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY 또는 간결한 SQL datetime 또는 간격 데이터 형식 중 하나인 경우 IPD의 SQL_DESC_LENGTH 필드는 *ColumnSize*의 값으로 설정됩니다. 자세한 내용은 부록 D: 데이터 유형의 [열 크기, 소수 자릿수, 전송 옥텟 길이 및 디스플레이 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 섹션을 참조하십시오.  
  
-   *ParameterType이* SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL 또는 SQL_DOUBLE 경우 IPD의 SQL_DESC_PRECISION 필드는 *ColumnSize*의 값으로 설정됩니다.  
  
-   다른 데이터 형식의 경우 *ColumnSize* 인수는 무시됩니다.  
  
 자세한 내용은 "매개 변수 값 전달" 및 *"StrLen_or_IndPtr* 인수"에서 SQL_DATA_AT_EXEC 참조하세요.  
  
## <a name="decimaldigits-argument"></a>소수 자릿수 인수

 *parameterType이* SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND 또는 SQL_INTERVAL_MINUTE_TO_SECOND 경우 IPD의 SQL_DESC_PRECISION 필드가 *decimalDigits로*설정됩니다. *ParameterType이* SQL_NUMERIC 또는 SQL_DECIMAL 경우 IPD의 SQL_DESC_SCALE 필드가 *DecimalDigits로*설정됩니다. 다른 모든 데이터 형식의 경우 *DecimalDigits* 인수는 무시됩니다.  
  
## <a name="parametervalueptr-argument"></a>매개 변수 값 Ptr 인수

 *ParameterValuePtr* 인수는 **SQLExecute** 또는 **SQLExecDirect가** 호출될 때 매개 변수에 대한 실제 데이터를 포함하는 버퍼를 가리킵니다. 데이터는 *ValueType* 인수에서 지정한 양식에 있어야 합니다. 이 인수는 APD의 SQL_DESC_DATA_PTR 필드를 설정합니다. 응용 프로그램은 * \*StrLen_or_IndPtr* SQL_NULL_DATA 또는 SQL_DATA_AT_EXEC 한, null 포인터에 *parameterValuePtr* 인수를 설정할 수 있습니다. (이것은 입력 또는 입력 /출력 매개 변수에만 적용됩니다.)  
  
 \* *StrLen_or_IndPtr* *SQL_LEN_DATA_AT_EXEC(길이)* 매크로 또는 SQL_DATA_AT_EXEC 결과인 경우 *ParameterValuePtr은* 매개 변수와 연결된 응용 프로그램 정의 포인터 값입니다. **SQLParamData를**통해 응용 프로그램에 반환됩니다. 예를 들어 *ParameterValuePtr은* 매개 변수 번호, 데이터에 대한 포인터 또는 응용 프로그램이 입력 매개 변수를 바인딩하는 데 사용되는 구조에 대한 포인터와 같은 0이 아닌 토큰일 수 있습니다. 그러나 매개 변수가 입력/출력 매개 변수인 경우 *ParameterValuePtr은* 출력 값이 저장되는 버퍼에 대한 포인터여야 합니다. SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1보다 큰 경우 응용 프로그램은 *parameterValuePtr* 인수와 함께 SQL_ATTR_PARAMS_PROCESSED_PTR 문 특성이 가리키는 값을 사용할 수 있습니다. 예를 들어 *ParameterValuePtr값의* 배열을 가리킬 수 있으며 응용 프로그램은 SQL_ATTR_PARAMS_PROCESSED_PTR 가리키는 값을 사용하여 배열에서 올바른 값을 검색할 수 있습니다. 자세한 내용은 이 섹션의 "매개 변수 값 전달"을 참조하십시오.  
  
 *InputOutputType* 인수가 SQL_PARAM_INPUT_OUTPUT SQL_PARAM_OUTPUT 경우 *ParameterValuePtr은* 드라이버가 출력 값을 반환하는 버퍼를 가리킵니다. 프로시저가 하나 이상의 결과 집합을 \*반환하는 경우 모든 결과 집합/행 수가 처리될 때까지 *ParameterValuePtr* 버퍼가 설정되지 않습니다. 처리가 완료될 때까지 버퍼가 설정되지 않으면 **SQLMoreResults가** SQL_NO_DATA 반환할 때까지 출력 매개 변수 및 반환 값을 사용할 수 없습니다. SQL_CLOSE 옵션으로 **SQLCloseCursor** 또는 **SQLFreeStmt를** 호출하면 이러한 값이 삭제됩니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1보다 큰 경우 *ParameterValuePtr은* 배열을 가리킵니다. 단일 SQL 문은 입력 또는 입력/출력 매개 변수에 대한 입력 값의 전체 배열을 처리하고 입력/출력 또는 출력 매개 변수에 대한 출력 값 배열을 반환합니다.  
  
## <a name="bufferlength-argument"></a>버퍼길이 인수

 문자 및 이진 C 데이터의 경우 *BufferLength* 인수는 \* *ParameterValuePtr* 버퍼의 길이(단일 요소인 경우) 또는 \* *ParameterValuePtr* 배열의 요소 길이(SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1보다 큰 경우)를 지정합니다. 이 인수는 APD의 SQL_DESC_OCTET_LENGTH 레코드 필드를 설정합니다. 응용 프로그램이 여러 값을 지정하는 경우 *BufferLength는* 입력 및 출력시 **ParameterValuePtr* 배열의 값 위치를 결정하는 데 사용됩니다. 입력/출력 및 출력 매개 변수의 경우 출력에서 문자 및 이진 C 데이터를 트런케이트할지 여부를 결정하는 데 사용됩니다.  
  
-   문자 C 데이터의 경우 반환할 수 있는 바이트 수가 *BufferLength보다*크거나 \*같으면 *ParameterValuePtr의* 데이터는 *bufferLength에* 잘리며 null 종료 문자의 길이가 적고 드라이버가 null-종료합니다.  
  
-   이진 C 데이터의 경우 반환할 수 있는 바이트 수가 *BufferLength보다*큰 경우 \* *ParameterValuePtr의* 데이터가 *BufferLength* 바이트로 잘립니다.  
  
 다른 모든 유형의 C 데이터에 대해 *BufferLength* 인수는 무시됩니다. \* *ParameterValuePtr* 버퍼의 길이(단일 요소인 경우) 또는 \* *ParameterValuePtr* 배열의 요소 길이(응용 프로그램이 각 매개 변수에 대해 여러 값을 지정하기 위해 SQL_ATTR_PARAMSET_SIZE *특성* 인수를 사용하여 **SQLSetStmtAttr을** 호출하는 경우) C 데이터 형식의 길이로 가정됩니다.  
  
 스트리밍된 출력 또는 스트리밍된 입력/출력 매개 변수의 경우 버퍼 길이가 **SQLGetData**에 지정되어 있으므로 *BufferLength* 인수는 무시됩니다.  
  
> [!NOTE]  
>  ODBC 1.0 응용 프로그램이 ODBC 3에서 **SQLSetParam을** 호출하는 경우. *x* 드라이버, 드라이버 관리자는 *이를 BUFFERLength* 인수가 항상 SQL_SETPARAM_VALUE_MAX **SQLBindParameter** 호출로 변환합니다. 드라이버 관리자가 ODBC 3인 경우 오류를 반환하기 때문입니다. *x* 응용 프로그램은 *버퍼길이를* odBC 3인 SQL_SETPARAM_VALUE_MAX 설정합니다. *x* 드라이버는 이 것을 사용하여 ODBC 1.0 응용 프로그램에서 호출되는 시기를 결정할 수 있습니다.  
  
> [!NOTE]  
>  **SQLSetParam에서**응용 프로그램이 **ParameterValuePtr* 버퍼의 길이를 지정하여 드라이버가 문자 또는 이진 데이터를 반환할 수 있도록 하는 방법과 응용 프로그램이 문자 또는 이진 매개 변수 값의 배열을 드라이버에 보내는 방법은 드라이버 정의됩니다.  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr 인수

 *StrLen_or_IndPtr* 인수는 **SQLExecute** 또는 **SQLExecDirect가** 호출될 때 다음 중 하나가 포함된 버퍼를 가리킵니다. 이 인수는 응용 프로그램 매개 변수 포인터의 SQL_DESC_OCTET_LENGTH_PTR 및 SQL_DESC_INDICATOR_PTR 레코드 필드를 설정합니다.  
  
-   * 매개 변수*값Ptr에*저장된 매개 변수 값의 길이입니다. 문자 또는 이진 C 데이터를 제외하면 무시됩니다.  
  
-   SQL_NTS. 매개 변수 값은 null-종료된 문자열입니다.  
  
-   SQL_NULL_DATA. 매개 변수 값은 NULL입니다.  
  
-   SQL_DEFAULT_PARAM. 프로시저는 응용 프로그램에서 검색된 값 대신 매개 변수의 기본값을 사용하는 것입니다. 이 값은 ODBC 표준 구문에서 호출된 프로시저에서만 유효하며 *InputOutputType* 인수가 SQL_PARAM_INPUT, SQL_PARAM_INPUT_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT_STREAM 경우에만 유효합니다. \* *StrLen_or_IndPtr* SQL_DEFAULT_PARAM 때 *ValueType*, *ParameterType*, *columnSize,* *DecimalDigits,* *BufferLength및* *ParameterValuePtr* 인수는 입력 매개 변수에 대해 무시되고 입력/출력 매개 변수에 대한 출력 매개 변수 값을 정의하는 데만 사용됩니다.  
  
-   *SQL_LEN_DATA_AT_EXEC(길이)* 매크로의 결과입니다. 매개 변수에 대한 데이터는 **SQLPutData**. *ParameterType* 인수가 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 긴 데이터 원본별 데이터 형식이고 드라이버가 **SQLGetInfo의**SQL_NEED_LONG_DATA_LEN 정보 형식에 대해 "Y"를 반환하는 경우 *길이는* 매개 변수에 대해 보낼 데이터의 바이트 수입니다. 그렇지 않으면 *길이는* 음수값이 어야 하며 무시됩니다. 자세한 내용은 이 섹션의 후반부 "매개 변수 값 전달"을 참조하십시오.  
  
     예를 들어, SQL_LONGVARCHAR 매개 변수에 대해 하나 이상의 호출에서 10,000바이트의 데이터가 **SQLPutData와** 함께 전송되도록 지정하려면 응용 프로그램이 **StrLen_or_IndPtr* SQL_LEN_DATA_AT_EXEC(10000)로 설정합니다.  
  
-   SQL_DATA_AT_EXEC. 매개 변수에 대한 데이터는 **SQLPutData**. 이 값은 ODBC 3을 호출할 때 ODBC 1.0 응용 프로그램에서 사용됩니다. *x* 드라이버. 자세한 내용은 이 섹션의 후반부 "매개 변수 값 전달"을 참조하십시오.  
  
 *StrLen_or_IndPtr* null 포인터인 경우 드라이버는 모든 입력 매개 변수 값이 NULL이 아닌 것으로 가정하고 해당 문자 및 이진 데이터가 null-종료된다고 가정합니다. *InputOutputType이* SQL_PARAM_OUTPUT 또는 SQL_PARAM_OUTPUT_STREAM 및 *ParameterValuePtr* 및 *StrLen_or_IndPtr* 모두 null 포인터인 경우 드라이버는 출력 값을 삭제합니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자는 매개 변수의 데이터 형식이 SQL_C_BINARY *때 StrLen_or_IndPtr* null 포인터를 지정하지 않는 것이 좋습니다. 드라이버가 SQL_C_BINARY 데이터를 예기치 않게 잘리지 않도록 하려면 *StrLen_or_IndPtr* 유효한 길이 값에 대한 포인터를 포함해야 합니다.  
  
 *InputOutputType* 인수가 SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM *StrLen_or_IndPtr 경우* 드라이버가 SQL_NULL_DATA 반환하는 버퍼, \* *ParameterValuePtr에서* 반환할 수 있는 바이트 수(문자 데이터의 null-termination 바이트 제외) 또는 SQL_NO_TOTAL(반환할 수 있는 바이트 수를 확인할 수 없는 경우)을 가리킵니다. 프로시저가 하나 이상의 결과 집합을 반환하는 경우 모든 결과를 가져올 때까지 **StrLen_or_IndPtr* 버퍼가 설정되지 않습니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1보다 크면 *StrLen_or_IndPtr* SQLLEN 값의 배열을 가리킵니다. 이 섹션의 앞에 나열된 값 중 하나일 수 있으며 단일 SQL 문으로 처리됩니다.  
  
## <a name="passing-parameter-values"></a>매개 변수 값 전달

 응용 프로그램은 \* *ParameterValuePtr* 버퍼또는 하나 이상의 **SQLPutData**에 대한 호출을 사용하여 매개 변수에 대한 값을 전달할 수 있습니다. **데이터가 SQLPutData로** 전달되는 매개 변수를 *실행 시 데이터* 매개 변수라고 합니다. 일반적으로 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 매개 변수에 대한 데이터를 전송하는 데 사용되며 다른 매개 변수와 혼합할 수 있습니다.  
  
 매개 변수 값을 전달하기 위해 응용 프로그램은 다음 단계 순서를 수행합니다.  
  
1.  각 매개 변수에 대 한 **SQLBindParameter** 호출 매개 변수값 *(ParameterValuePtr* 인수) 및 길이/표시기 *(StrLen_or_IndPtr* 인수)에 대 한 버퍼를 바인딩합니다. 실행 시 데이터 매개 변수의 경우 *ParameterValuePtr은* 매개 변수 번호 또는 데이터에 대한 포인터와 같은 응용 프로그램 정의 포인터 값입니다. 값은 나중에 반환되며 매개 변수를 식별하는 데 사용할 수 있습니다.  
  
2.  \* *ParameterValuePtr* 및 **StrLen_or_IndPtr* 버퍼에 입력 및 입력/출력 매개 변수에 대한 값을 배치합니다.  
  
    -   일반 매개 변수의 경우 응용 프로그램은 \* *ParameterValuePtr* 버퍼에 매개 변수 값을 배치하고 해당 값의 길이를 **StrLen_or_IndPtr* 버퍼에 배치합니다. 자세한 내용은 [매개변수 값 설정](../../../odbc/reference/develop-app/setting-parameter-values.md)을 참조하십시오.  
  
    -   실행 시 데이터 매개 변수의 경우 응용 프로그램은*SQL_LEN_DATA_AT_EXEC(길이)* 매크로(ODBC 2.0 드라이버를 호출할 때)의 결과를 **StrLen_or_IndPtr* 버퍼에 넣습니다.  
  
3.  **SQLExecute** 또는 **SQLExecDirect를** 호출하여 SQL 문을 실행합니다.  
  
    -   실행 시 데이터 매개 변수가 없는 경우 프로세스가 완료됩니다.  
  
    -   실행 시 데이터 매개 변수가 있으면 함수가 SQL_NEED_DATA 반환합니다.  
  
4.  **SQLParamData를** 호출하여 처리될 첫 번째 데이터 실행 매개 변수에 대해 **SQLBindParameter의** *ParameterValuePtr* 인수에 지정된 응용 프로그램 정의 값을 검색합니다. **SQLParamData는** SQL_NEED_DATA 반환합니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수는 실행 시 데이터 열과 유사하지만 **SQLParamData에서** 반환하는 값은 각각 다릅니다. 실행 시 데이터 매개 변수는 SQL 문의 매개 변수로 SQLPutData 로 데이터가 **SQLExecDirect** 또는 **SQLExecute**로 실행될 때 데이터가 **SQLPutData로** 전송됩니다. **SQLBindParameter**. **SQLParamData에** 의해 반환 되는 값은 매개 변수 *값 Ptr* 인수에서 **SQLBindParameter에** 전달 되는 포인터 값입니다. 실행 시 데이터 열은 행이 **SQLBulkOperations로** 업데이트되거나 **SQLSetPos로**업데이트될 때 **데이터가 SQLPutData로** 전송되는 행 집합의 열입니다. **SQLBindCol.** **SQLParamData에서** 반환되는 값은 처리 중인 **TargetValuePtr* 버퍼(SQLBindCol **SQLBindCol**호출로 설정됨)의 행 의 주소입니다.  
  
5.  매개 변수에 대 한 데이터를 보낼 **SQLPutData** 를 하나 이상 호출 합니다. 데이터 값이 \* **SQLPutData에**지정된 *ParameterValuePtr* 버퍼보다 큰 경우 두 개 이상의 호출이 필요합니다. 동일한 매개 변수에 대한 **SQLPutData에** 대한 여러 호출은 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열로 문자 C 데이터를 보내거나 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열로 이진 C 데이터를 보낼 때만 허용됩니다.  
  
6.  매개 변수에 대해 모든 데이터가 전송되었음을 알리기 위해 **SQLParamData를** 다시 호출합니다.  
  
    -   실행 시 데이터 매개 변수가 더 많은 경우 **SQLParamData는** SQL_NEED_DATA 반환하고 처리할 다음 실행 시 데이터 매개 변수에 대한 응용 프로그램 정의 값을 반환합니다. 응용 프로그램은 4 단계와 5단계를 반복합니다.  
  
    -   실행 시 데이터 매개 변수가 더 이상 없는 경우 프로세스가 완료됩니다. 명령문이 성공적으로 실행된 경우 **SQLParamData는** SQL_SUCCESS 반환하거나 SQL_SUCCESS_WITH_INFO. 실행이 실패하면 SQL_ERROR 반환합니다. 이 시점에서 **SQLParamData** 문을 실행 하는 데 사용 되는 함수에 의해 반환될 수 있는 모든 SQLSTATE를 반환할 수 있습니다 **(SQLExecDirect** 또는 **SQLExecute).**  
  
         모든 입력/출력 또는 출력 매개 변수에 \*대한 출력 값은 *ParameterValuePtr및* **StrLen_or_IndPtr* 버퍼에서 사용할 수 있으며 응용 프로그램이 문에서 생성된 모든 결과 집합을 검색한 후.  
  
 **SQLExecute** 또는 **SQLExecDirect를** 호출하면 명령문이 SQL_NEED_DATA 상태로 됩니다. 이 시점에서 응용 프로그램은 **SQLCancel,** **SQLGetDiagField,** **SQLGetDiagRec,** **SQLGetFunctions,** **SQLParamData**또는 **SQLPutData** 문과 연결된 명령문 또는 *연결 핸들만* 호출할 수 있습니다. 명령문 또는 문과 연결된 연결이 있는 다른 함수를 호출하는 경우 함수는 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. 이 문은 **SQLParamData** 또는 **SQLPutData** 가 오류를 반환하거나 **SQLParamData가** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환하거나 명령문이 취소될 때 SQL_NEED_DATA 상태를 남깁니다.  
  
 응용 프로그램에서 **SQLCancel을** 호출하는 동안 드라이버는 여전히 실행 시 데이터 매개 변수에 대한 데이터가 필요하면 드라이버는 문 실행을 취소합니다. 그런 다음 응용 프로그램이 **SQLExecute** 또는 **SQLExecDirect를** 다시 호출할 수 있습니다.  
  
## <a name="retrieving-streamed-output-parameters"></a>스트리밍된 출력 매개 변수 검색

 응용 프로그램이 *InputOutputType을* SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM 설정하면 **SQLGetData**에 대한 하나 이상의 호출로 출력 매개 변수 값을 검색해야 합니다. 드라이버에 응용 프로그램으로 돌아가는 스트리밍된 출력 매개 변수 값이 있으면 **SQLMoreResults,** **SQLExecute**및 **SQLExecDirect**의 다음 함수에 대한 호출에 대한 응답으로 SQL_PARAM_DATA_AVAILABLE 반환합니다. 응용 프로그램은 **SQLParamData를** 호출하여 사용 가능한 매개 변수 값을 결정합니다.  
  
 SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대한 자세한 내용은 [SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)를 사용하여 출력 매개 변수 검색을 참조하십시오.  
  
## <a name="using-arrays-of-parameters"></a>매개 변수 배열 사용

 응용 프로그램이 매개 변수 마커가 있는 문을 준비하고 매개 변수 배열을 전달하는 경우 이 방법을 실행할 수 있는 두 가지 방법이 있습니다. 한 가지 방법은 드라이버가 백 엔드의 배열 처리 기능에 의존하는 것입니다. 오라클은 어레이 처리 기능을 지원하는 데이터 원본의 예입니다. 이 기능을 구현하는 또 다른 방법은 드라이버가 매개 변수 배열의 각 매개 변수 집합에 대해 SQL 문 일괄 처리를 생성하고 일괄 처리를 실행하는 것입니다. 매개 변수의 배열은 UPDATE **WHERE CURRENT OF** 문과 함께 사용할 수 없습니다.  
  
 매개 변수 의 배열이 처리될 때 개별 결과 집합/행 개수(각 매개 변수 집합에 대해 하나씩)를 사용할 수 있거나 결과 집합/행 수를 하나로 롤업할 수 있습니다. **SQLGetInfo의** SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 각 매개 변수 집합(SQL_PARC_BATCH)에 대해 행 수를 사용할 수 있는지 또는 하나의 행 개수만 사용할 수 있는지 여부를 나타냅니다(SQL_PARC_NO_BATCH).  
  
 **SQLGetInfo의** SQL_PARAM_ARRAY_SELECTS 옵션은 각 매개 변수 집합(SQL_PAS_BATCH)에 대해 결과 집합을 사용할 수 있는지 또는 하나의 결과 집합만 사용할 수 있는지(SQL_PAS_NO_BATCH)를 나타냅니다. 드라이버가 매개 변수 배열로 결과 집합 생성 문을 실행하도록 허용하지 않는 경우 SQL_PARAM_ARRAY_SELECTS SQL_PAS_NO_SELECT 반환합니다.  
  
 자세한 내용은 [SQLGetInfo 함수를](../../../odbc/reference/syntax/sqlgetinfo-function.md)참조하십시오.  
  
 매개 변수의 배열을 지원 하기 위해 SQL_ATTR_PARAMSET_SIZE 문 특성 각 매개 변수에 대 한 값 수를 지정 하도록 설정 됩니다. 필드가 1보다 큰 경우 APD의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드는 배열을 가리커해야 합니다. 각 배열의 카디널리티는 SQL_ATTR_PARAMSET_SIZE 값과 같습니다.  
  
 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드는 오류 집합을 포함하여 처리된 매개 변수 집합 수를 포함하는 버퍼를 가리킵니다. 각 매개 변수 집합이 처리되면 드라이버는 버퍼에 새 값을 저장합니다. null 포인터인 경우 번호가 반환되지 않습니다. 매개 변수 배열을 사용하는 경우 설정 함수에서 SQL_ERROR 반환되는 경우에도 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드가 가리키는 값이 채워집니다. SQL_NEED_DATA 반환되면 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드가 가리키는 값은 처리 중인 매개 변수 집합으로 설정됩니다.  
  
 매개 변수의 배열이 바인딩되고 현재 OF 문이 실행되는 **UPDATE가** 드라이버 정의일 때 발생하는 내용입니다.  
  
## <a name="column-wise-parameter-binding"></a>열 별 매개 변수 바인딩

 열 별 바인딩에서 응용 프로그램은 각 매개 변수에 별도의 매개 변수 및 길이/표시기 배열을 바인딩합니다.  
  
 열 별 바인딩을 사용 하려면 응용 프로그램은 먼저 SQL_PARAM_BIND_BY_COLUMN SQL_ATTR_PARAM_BIND_TYPE 문 특성을 설정 합니다. 기본값입니다. 바인딩할 각 열을 위해 응용 프로그램은 다음 단계를 수행합니다.  
  
1.  매개 변수 버퍼 배열을 할당합니다.  
  
2.  길이/표시기 버퍼의 배열을 할당합니다.  
  
    > [!NOTE]  
    >  열 별 바인딩을 사용할 때 응용 프로그램이 설명자에게 직접 쓰는 경우 길이 및 표시기 데이터에 별도의 배열을 사용할 수 있습니다.  
  
3.  다음 인수를 사용 하 고 **SQLBind매개** 변수를 호출합니다.  
  
    -   *ValueType은* 매개 변수 버퍼 배열의 단일 요소의 C 형식입니다.  
  
    -   *ParameterType은* 매개 변수의 SQL 유형입니다.  
  
    -   *매개 변수값 Ptr은* 매개 변수 버퍼 배열의 주소입니다.  
  
    -   *BufferLength는* 매개 변수 버퍼 배열의 단일 요소의 크기입니다. 데이터가 고정 길이 데이터인 경우 *BufferLength* 인수는 무시됩니다.  
  
    -   *StrLen_or_IndPtr* 길이/표시기 배열의 주소입니다.  
  
 이 정보가 사용되는 방법에 대한 자세한 내용은 이 섹션의 "주석"의 "ParameterValuePtr 인수"를 참조하십시오. 매개 변수의 열 별 바인딩에 대한 자세한 내용은 [매개 변수의 바인딩 배열을](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)참조하십시오.  
  
## <a name="row-wise-parameter-binding"></a>행 별 매개 변수 바인딩

 행 별 바인딩에서 응용 프로그램은 바인딩할 각 매개 변수에 대한 매개 변수 및 길이/표시기 버퍼를 포함하는 구조를 정의합니다.  
  
 행 별 바인딩을 사용 하려면 응용 프로그램은 다음 단계를 수행 합니다.  
  
1.  단일 매개변수 집합(매개변수 및 길이/표시기 버퍼 포함)을 보유하는 구조를 정의하고 이러한 구조의 배열을 할당합니다.  
  
    > [!NOTE]  
    >  행 별 바인딩을 사용할 때 응용 프로그램이 설명자에 직접 쓰는 경우 길이 및 표시기 데이터에 대해 별도의 필드를 사용할 수 있습니다.  
  
2.  SQL_ATTR_PARAM_BIND_TYPE 문 특성을 단일 매개 변수 집합을 포함하는 구조의 크기 또는 매개 변수가 바인딩될 버퍼 인스턴스의 크기로 설정합니다. 길이에는 바인딩된 매개 변수의 주소가 지정된 길이로 증분될 때 결과가 다음 행에서 동일한 매개변수의 시작을 가리키도록 하기 위해 모든 바인딩된 매개변수및 구조또는 버퍼의 패딩에 대한 공간이 포함되어야 합니다. ANSI C에서 *sizeof* 연산자사용 시 이 동작이 보장됩니다.  
  
3.  바인딩할 각 매개 변수에 대 한 다음 인수와 **SQLBindParameter를** 호출 합니다.  
  
    -   *ValueType은* 열에 바인딩할 매개 변수 버퍼 멤버의 형식입니다.  
  
    -   *ParameterType은* 매개 변수의 SQL 유형입니다.  
  
    -   *ParameterValuePtr은* 첫 번째 배열 요소의 매개 변수 버퍼 멤버의 주소입니다.  
  
    -   *버퍼길이는* 매개 변수 버퍼 멤버의 크기입니다.  
  
    -   *StrLen_or_IndPtr* 바인딩할 길이/표시기 멤버의 주소입니다.  
  
 이 정보가 사용되는 방법에 대한 자세한 내용은 이 섹션의 후반부 *"ParameterValuePtr* 인수"를 참조하십시오. 매개 변수의 행 별 바인딩에 대한 자세한 내용은 [매개 변수의 바인딩 배열을](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)참조하십시오.  
  
## <a name="error-information"></a>오류 정보

 드라이버가 매개 변수 배열을 일괄 처리로 구현하지 않는 경우(SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 SQL_PARC_NO_BATCH 같음) 오류 상황은 하나의 문이 실행된 것처럼 처리됩니다. 드라이버가 매개 변수 배열을 일괄 처리로 구현하는 경우 응용 프로그램은 IPD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 사용하여 SQL 문의 매개 변수 또는 매개 변수 배열의 매개 변수를 결정하여 **SQLExecDirect** 또는 **SQLExecute가** 오류를 반환하도록 할 수 있습니다. 이 필드에는 매개 변수 값의 각 행에 대한 상태 정보가 포함되어 있습니다. 필드에 오류가 발생했음을 나타내는 경우 진단 데이터 구조의 필드는 실패한 매개 변수의 행 및 매개 변수 번호를 나타냅니다. 배열의 요소 수는 apD의 SQL_DESC_ARRAY_SIZE 헤더 필드에 의해 정의되며, SQL_ATTR_PARAMSET_SIZE 문 특성으로 설정할 수 있습니다.  
  
> [!NOTE]  
>  APD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드는 매개 변수를 무시하는 데 사용됩니다. 매개 변수 무시에 대한 자세한 내용은 다음 섹션인 "매개 변수 집합 무시"를 참조하십시오.  
  
 **SQLExecute** 또는 **SQLExecDirect가** SQL_ERROR 반환하는 경우 IPD의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 배열의 요소에는 SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED 또는 SQL_PARAM_DIAG_UNAVAILABLE 포함됩니다.  
  
 이 배열의 각 요소에 대해 진단 데이터 구조에는 하나 이상의 상태 레코드가 포함됩니다. 구조의 SQL_DIAG_ROW_NUMBER 필드는 오류를 일으킨 매개 변수 값의 행 번호를 나타냅니다. 오류를 일으킨 매개 변수 행에서 특정 매개 변수를 확인할 수 있는 경우 매개 변수 번호가 SQL_DIAG_COLUMN_NUMBER 필드에 입력됩니다.  
  
 SQL_PARAM_UNUSED 매개 변수가 사용되지 않은 경우 **SQLExecute** 또는 **SQLExecDirect를** 강제로 중단하는 이전 매개 변수에서 오류가 발생했기 때문에 입력됩니다. 예를 들어 **SQLExecute** 또는 **SQLExecDirect를** 중단시키는 40번째 매개 변수 집합을 실행하는 동안 50개의 매개 변수와 오류가 발생한 경우 41~50매개 변수의 상태 배열에 SQL_PARAM_UNUSED 입력됩니다.  
  
 SQL_PARAM_DIAG_UNAVAILABLE 드라이버가 매개 변수 배열을 모놀리식 단위로 처리하면 입력되므로 이 개별 매개 변수 수준의 오류 정보를 생성하지 않습니다.  
  
 단일 매개 변수 집합 처리에 일부 오류로 인해 배열의 후속 매개 변수 집합이 중지됩니다. 다른 오류는 후속 매개 변수의 처리에 영향을 주지 않습니다. 처리를 중지하는 오류는 드라이버 정의입니다. 처리가 중지되지 않으면 배열의 모든 매개 변수가 처리되고 오류로 인해 SQL_SUCCESS_WITH_INFO 반환되며 SQL_ATTR_PARAMS_PROCESSED_PTR 정의된 버퍼는 오류 집합을 포함하는 처리된 총 매개 변수 집합(SQL_ATTR_PARAMSET_SIZE 문 특성에 의해 정의된 대로)으로 설정됩니다.  
  
> [!CAUTION]  
>  매개 변수 배열의 처리에서 오류가 발생하는 경우 ODBC 동작은 ODBC 3에서 다릅니다. *ODBC* 2보다 x. *x*. ODBC 2. *x,* 함수가 반환된 SQL_ERROR 및 처리가 중단되었습니다. **SQLParamOptions의** *pirow* 인수로 가리키는 버퍼에는 오류 행 수가 포함되어 있습니다. ODBC 3. *x*, 함수는 SQL_SUCCESS_WITH_INFO 반환하고 처리는 중지되거나 계속될 수 있습니다. 계속하면 SQL_ATTR_PARAMS_PROCESSED_PTR 지정한 버퍼가 오류를 초래한 매개 변수를 포함하여 처리된 모든 매개 변수의 값으로 설정됩니다. 이러한 동작 변경으로 인해 기존 응용 프로그램에 문제가 발생할 수 있습니다.  
  
 **SQLExecute** 또는 **SQLExecDirect가** SQL_ERROR 또는 SQL_NEED_DATA 반환되는 경우와 같이 매개 변수 배열의 모든 매개 변수 집합 처리를 완료하기 전에 반환되면 상태 배열에는 이미 처리된 해당 매개 변수에 대한 상태가 포함됩니다. IPD의 SQL_DESC_ROWS_PROCESSED_PTR 필드가 가리키는 위치에는 SQL_ERROR 또는 SQL_NEED_DATA 오류 코드를 발생시킨 매개 변수 배열의 행 번호가 포함되어 있습니다. 매개 변수배열이 SELECT 문으로 전송되면 상태 배열 값의 가용성은 드라이버 정의입니다. 명령문이 실행된 후 또는 결과 집합을 가져온 후에 사용할 수 있습니다.  
  
## <a name="ignoring-a-set-of-parameters"></a>매개 변수 집합 무시

 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드(SQL_ATTR_PARAM_STATUS_PTR 문 특성에 의해 설정된 대로)를 사용하여 SQL 문에 바인딩된 매개 변수 집합을 무시해야 함을 나타낼 수 있습니다. 실행 중에 하나 이상의 매개 변수 집합을 무시하도록 드라이버를 지시하려면 응용 프로그램은 다음 단계를 수행해야 합니다.  
  
1.  **SQLSetDescField를** 호출하여 상태 정보를 포함하는 SQLUSMALLINT 값의 배열을 가리키도록 APD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 설정합니다. 이 필드는 응용 프로그램이 설명자 핸들을 가져오지 않고 필드를 설정할 수 있는 SQL_ATTR_PARAM_OPERATION_PTR *특성을* 사용하여 **SQLSetStmtAttr을** 호출하여 설정할 수도 있습니다.  
  
2.  APD의 SQL_DESC_ARRAY_STATUS_PTR 필드에 의해 정의된 배열의 각 요소를 다음 두 값 중 하나로 설정합니다.  
  
    -   SQL_PARAM_IGNORE 행이 문 실행에서 제외됨을 나타냅니다.  
  
    -   SQL_PARAM_PROCEED 행이 문 실행에 포함되어 있음을 나타냅니다.  
  
3.  준비된 문을 실행 하려면 **SQLExecDirect** 또는 **SQLExecute를** 호출 합니다.  
  
 다음 규칙은 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드에 의해 정의된 배열에 적용됩니다.  
  
-   포인터는 기본적으로 null로 설정됩니다.  
  
-   포인터가 null이면 모든 요소가 SQL_ROW_PROCEED 설정된 것처럼 모든 매개 변수 집합이 사용됩니다.  
  
-   요소를 SQL_PARAM_PROCEED 설정한다고 해서 작업이 특정 매개 변수 집합을 사용하도록 보장하지는 않습니다.  
  
-   SQL_PARAM_PROCEED 헤더 파일에서 0으로 정의됩니다.  
  
 응용 프로그램은 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드를 IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 것과 동일한 배열을 가리키도록 설정할 수 있습니다. 이 기능은 매개 변수를 행 데이터에 바인딩할 때 유용합니다. 그런 다음 행 데이터의 상태에 따라 매개 변수를 무시할 수 있습니다. 다음 코드는 SQL_PARAM_IGNORE 외에도 SQL 문의 매개 변수인 SQL_ROW_DELETED, SQL_ROW_UPDATED 및 SQL_ROW_ERROR 무시합니다. SQL_PARAM_PROCEED 외에도 다음 코드로 인해 SQL 문이 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO 및 SQL_ROW_ADDED 진행됩니다.  
  
## <a name="rebinding-parameters"></a>매개 변수 다시 바인딩

 응용 프로그램은 바인딩을 변경하기 위해 두 작업 중 하나를 수행할 수 있습니다.  
  
-   **SQLBindParameter를** 호출하여 이미 바인딩된 열에 대한 새 바인딩을 지정합니다. 드라이버는 이전 바인딩을 새 바인딩으로 덮어씁니다.  
  
-   **SQLBindParameter**에 대한 바인딩 호출에 의해 지정된 버퍼 주소에 추가할 오프셋을 지정합니다. 자세한 내용은 다음 섹션인 "간격띄우기로 다시 바인딩"을 참조하십시오.  
  
## <a name="rebinding-with-offsets"></a>간격띄우기로 다시 바인딩

 매개 변수를 다시 바인딩하는 것은 응용 프로그램에 많은 매개 변수를 포함할 수 있는 버퍼 영역 설정이 있지만 **SQLExecDirect** 또는 **SQLExecute** 호출은 몇 가지 매개 변수만 사용하는 경우에 특히 유용합니다. 버퍼 영역의 나머지 공간은 오프셋에 의해 기존 바인딩을 수정하여 다음 매개 변수 집합에 사용할 수 있습니다.  
  
 APD의 SQL_DESC_BIND_OFFSET_PTR 헤더 필드는 바인딩 오프셋을 가리킵니다. 필드가 null이 아닌 경우 드라이버는 포인터를 참조하고 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값이 null 포인터인 경우 실행 시 설명자 레코드의 해당 필드에 역참조 값을 추가합니다. SQL 문이 실행될 때 새 포인터 값이 사용됩니다. 오프셋은 다시 바인딩한 후에도 유효합니다. SQL_DESC_BIND_OFFSET_PTR 오프셋 자체가 아닌 오프셋에 대한 포인터이므로 응용 프로그램은 설명자 필드를 변경하기 위해 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 또는 [SQLSetDescRec를](../../../odbc/reference/syntax/sqlsetdescrec-function.md) 호출하지 않고도 오프셋을 직접 변경할 수 있습니다. 포인터는 기본적으로 null로 설정됩니다. ARD의 SQL_DESC_BIND_OFFSET_PTR 필드는 [SQLSetDescField에](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 대한 호출 또는 SQL_ATTR_PARAM_BIND_OFFSET_PTR *fAttribute를* 사용하여 [SQLSetStmtAttr에](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)대한 호출로 설정할 수 있습니다.  
  
 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값에 직접 추가됩니다. 오프셋이 다른 값으로 변경된 경우에도 새 값은 각 설명자 필드의 값에 직접 추가됩니다. 새 오프셋은 필드 값과 이전 오프셋의 합계에 추가되지 않습니다.  
  
## <a name="descriptors"></a>설명자

 매개 변수가 바인딩되는 방법은 APD 및 IPD의 필드에 의해 결정됩니다. **SQLBindParameter의** 인수는 이러한 설명자 필드를 설정하는 데 사용됩니다. **SQLBindParameter는** 응용 프로그램이 **SQLBindParameter를**호출하는 설명자 핸들을 얻을 필요가 없기 때문에 사용하기가 더 효율적이지만 **SQLSetDescField** 함수에 의해 필드를 설정할 수도 있습니다.  
  
> [!CAUTION]  
>  한 문에 **대해 SQLBindParameter를** 호출하면 다른 문에 영향을 줄 수 있습니다. 이 문제는 명령문과 연결된 ARD가 명시적으로 할당되고 다른 명령문과도 연결될 때 발생합니다. **SQLBindParameterAPD의** 필드를 수정 하기 때문에 수정 프로그램은이 설명자가 연결 된 모든 문에 적용 됩니다. 필수 동작이 아닌 경우 응용 프로그램은 **SQLBindParameter**를 호출하기 전에 다른 명령문에서 이 설명자와 분리해야 합니다.  
  
 개념적으로 **SQLBindParameter는** 다음 단계를 순서대로 수행합니다.  
  
1.  APD 핸들을 가져오려면 [SQLGetStmtAttr을](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) 호출합니다.  
  
2.  APD의 SQL_DESC_COUNT 필드를 얻기 위해 [SQLGetDescField를](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 호출하고 *ColumnNumber* 인수의 값이 SQL_DESC_COUNT 값을 초과하는 경우 **SQLSetDescField를** 호출하여 SQL_DESC_COUNT 값을 *ColumnNumber*에 증가시다.  
  
3.  [SQLSetDescField를](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 여러 번 호출하여 APD의 다음 필드에 값을 할당합니다.  
  
    -   값 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE *값으로*설정합니다.valueType이 datetime 또는 interval 하위 유형의 간결한 식별자 중 하나인 경우 SQL_DESC_TYPE SQL_DATETIME 또는 SQL_INTERVAL 설정하고 간결한 식별자로 SQL_DESC_CONCISE_TYPE 설정하고 해당 날짜 시간 또는 간격 하위 코드로 SQL_DESC_DATETIME_INTERVAL_CODE 설정합니다. *ValueType*  
  
    -   SQL_DESC_OCTET_LENGTH 필드를 *BufferLength*값으로 설정합니다.  
  
    -   SQL_DESC_DATA_PTR 필드를 *ParameterValue*의 값으로 설정합니다.  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 필드를 *StrLen_or_Ind*값으로 설정합니다.  
  
    -   SQL_DESC_INDICATOR_PTR 필드도 *StrLen_or_Ind*값으로 설정합니다.  
  
     *StrLen_or_Ind* 매개 변수는 표시기 정보와 매개 변수 값의 길이를 모두 지정합니다.  
  
4.  IPD 핸들을 얻기 위해 [SQLGetStmtAttr을](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) 호출합니다.  
  
5.  IPD의 SQL_DESC_COUNT 필드를 얻기 위해 [SQLGetDescField를](../../../odbc/reference/syntax/sqlgetdescfield-function.md) *호출하고, columnNumber* 인수의 값이 SQL_DESC_COUNT 값을 초과하는 **경우, SQLSetDescField를** 호출하여 SQL_DESC_COUNT 값을 *ColumnNumber*에 증가시다 .  
  
6.  IPD의 다음 필드에 값을 할당하려면 [SQLSetDescField를](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 여러 번 호출합니다.  
  
    -   *ParameterType이*datetime 또는 interval 하위 유형의 간결한 식별자 중 하나인 경우를 제외하고 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE *변수를* SQL_DATETIME 또는 SQL_INTERVAL SQL_DESC_TYPE 설정하고, 간결한 식별자로 SQL_DESC_CONCISE_TYPE 설정하고, 해당 날짜 시간 또는 간격 하위 코드에 SQL_DESC_DATETIME_INTERVAL_CODE 설정합니다.  
  
    -   *매개 변수 유형에*적합한 SQL_DESC_LENGTH SQL_DESC_PRECISION 및 SQL_DESC_DATETIME_INTERVAL_PRECISION 중 하나 이상을 설정합니다.  
  
    -   *SQL_DESC_SCALE DecimalDigits*값으로 설정합니다.  
  
 **SQLBindParameter** 에 대한 호출이 실패하면 APD에서 설정한 설명자 필드의 내용은 정의되지 않으며 APD의 SQL_DESC_COUNT 필드는 변경되지 않습니다. 또한 IPD에 적절한 레코드의 SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_TYPE 필드는 정의되지 않고 IPD의 SQL_DESC_COUNT 필드는 변경되지 않습니다.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>SQLSetParam에서 호출 변환

 ODBC 1.0 응용 프로그램이 ODBC 3에서 **SQLSetParam을** 호출하는 경우. *x* 드라이버, ODBC 3. *x* 드라이버 관리자는 다음 표와 같이 호출을 매핑합니다.  
  
|ODBC 1.0 애플리케이션으로 전화 걸기|ODBC 3로 전화하십시오. *x* 드라이버|  
|----------------------------------|-------------------------------|  
|SQLSetParam(문핸들, 매개변수번호, 값유형, 파라미터타입, 길이정밀도, 파라미터스케일, 파라미터밸등, StrLen_or_IndPtr);|SQLBindParameter (문핸들, 매개 변수 번호, SQL_PARAM_INPUT_OUTPUT, 값 유형, 매개 변수 유형, *열크기*, *소수점자리*, 매개 변수 값 Ptr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 ORDERS 테이블에 데이터를 삽입하는 SQL 문을 준비합니다. 명령문의 각 매개 변수에 대해 응용 프로그램은 **SQLBindParameter를** 호출하여 ODBC C 데이터 형식과 매개 변수의 SQL 데이터 형식을 지정하고 각 매개 변수에 버퍼를 바인딩합니다. 각 데이터 행에 대해 응용 프로그램은 각 매개 변수에 데이터 값을 할당하고 **SQLExecute를** 호출하여 문을 실행합니다.  
  
 다음 샘플에서는 컴퓨터에 Northwind 데이터베이스와 연결된 ODBC 데이터 원본이 있다고 가정합니다.  
  
 자세한 코드 예제는 [SQLBulkOperations 함수,](../../../odbc/reference/syntax/sqlbulkoperations-function.md) [SQLProcedures 함수,](../../../odbc/reference/syntax/sqlprocedures-function.md) [SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)및 [SQLSetPos 함수를](../../../odbc/reference/syntax/sqlsetpos-function.md)참조하십시오.  
  
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

 다음 예제에서 응용 프로그램은 명명된 매개 변수를 사용하여 SQL Server 저장 프로시저를 실행합니다.  
  
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
  
|원하는 정보|참조|  
|---------------------------|---------|  
|명령문에서 매개 변수에 대한 정보 반환|[SQLDescribeParam 함수(SQLDescribeParam Function)](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|명령문에 매개 변수 버퍼 해제|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|문 매개 변수 수 반환|[SQLNumParams 함수](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|다음 매개 변수를 반환하여 데이터를|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|여러 매개변수 값 지정|[SQLParamOptions 함수](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>참고 항목

 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
