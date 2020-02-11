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
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65f6145f0cbfbd59fffb71e030f6427ea1f551c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036209"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 함수

**규칙**  
 소개 된 버전: ODBC 2.0 표준 준수: ODBC  
  
 **요약**  
 **SQLBindParameter** 는 SQL 문의 매개 변수 표식에 버퍼를 바인딩합니다. **SQLBindParameter** 는 기본 드라이버가 유니코드 데이터를 지원 하지 않는 경우에도 유니코드 C 데이터 형식에 대 한 바인딩을 지원 합니다.  
  
> [!NOTE]  
>  이 함수는 ODBC 1.0 함수 **SQLSetParam**을 대체 합니다. 자세한 내용은 "설명"을 참조 하십시오.  
  
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
 입력 문 핸들입니다.  
  
 *ParameterNumber*  
 입력 매개 변수를 순서 대로 오름차순으로 정렬 하 여 1에서 시작 하는 매개 변수 수입니다.  
  
 *InputOutputType*  
 입력 매개 변수의 형식입니다. 자세한 내용은 "설명"의 "*Inputoutputtype* 인수"를 참조 하십시오.  
  
 *ValueType*  
 입력 매개 변수의 C 데이터 형식입니다. 자세한 내용은 "설명"의 "*ValueType* 인수"를 참조 하십시오.  
  
 *ParameterType*  
 입력 매개 변수의 SQL 데이터 형식입니다. 자세한 내용은 "Comments"의 "*ParameterType* 인수"를 참조 하십시오.  
  
 *ColumnSize*  
 입력 해당 매개 변수 표식의 열 또는 식의 크기입니다. 자세한 내용은 "설명"의 "*Columnsize* 인수"를 참조 하십시오.  
  
 응용 프로그램이 64 비트 Windows 운영 체제에서 실행 되는 경우 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)를 참조 하세요.  
  
 *DecimalDigits*  
 입력 해당 매개 변수 표식의 열 또는 식의 10 진수입니다. 열 크기에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)를 참조 하십시오.  
  
 *ParameterValuePtr*  
 [지연 된 입력] 매개 변수 데이터의 버퍼에 대 한 포인터입니다. 자세한 내용은 "주석"의 "*Parametervalueptr* 인수"를 참조 하십시오.  
  
 *BufferLength*  
 [입/출력] *Parametervalueptr* 버퍼의 길이 (바이트)입니다. 자세한 내용은 "Comments"의 "*Bufferlength* 인수"를 참조 하십시오.  
  
 응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)를 참조 하세요.  
  
 *StrLen_or_IndPtr*  
 [지연 된 입력] 매개 변수의 길이에 대 한 버퍼에 대 한 포인터입니다. 자세한 내용은 "설명"의 "*StrLen_or_IndPtr* 인수"를 참조 하십시오.  
  
## <a name="returns"></a>반환

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단

 **SQLBindParameter** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLBindParameter** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  

|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|*ValueType* 인수로 식별 되는 데이터 형식은 *ParameterType* 인수로 식별 되는 데이터 형식으로 변환할 수 없습니다. 이 오류는 **SQLBindParameter**대신 실행 시 **sqlexecdirect**, **Sqlexecute**또는 **sqlexecdirect** 에서 반환 될 수 있습니다.|  
|07009|잘못 된 설명자 인덱스|(DM) 인수 *Parameternumber* 에 지정 된 값이 1 보다 작은 경우|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. **MessageText* Buffer의 **SQLGetDiagRec** 에서 반환 된 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|응용 프로그램 버퍼 유형이 잘못 되었습니다.|인수 *ValueType* 에 지정 된 값이 유효한 C 데이터 형식이 아니거나 SQL_C_DEFAULT.|  
|HY004|잘못 된 SQL 데이터 형식|*ParameterType* 인수에 지정 된 값이 올바른 ODBC sql 데이터 형식 식별자 또는 드라이버에서 지 원하는 드라이버 특정 SQL 데이터 형식 식별자가 아닙니다.|  
|HY009|인수 값이 잘못 되었습니다.|(DM *) 인수가 null 포인터이 고* , *StrLen_or_IndPtr* 인수가 null 포인터이 고, *inputoutputtype* 인수가 SQL_PARAM_OUTPUT 되지 않았습니다.<br /><br /> (DM) SQL_PARAM_OUTPUT은 인수 *Parametervalueptr* 이 null 포인터이 고, C 형식이 char 또는 binary이 고, bufferlength (*cbValueMax*)가 0 보다 큽니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLBindParameter** 가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY021|일관 되지 않은 설명자 정보|일관성 확인 중에 확인 된 설명자 정보가 일치 하지 않습니다. **SQLSetDescField**의 "일관성 검사" 섹션을 참조 하세요.<br /><br /> *DecimalDigits* 인수에 지정 된 값이 *ParameterType* 인수로 지정 된 SQL 데이터 형식의 열에 대 한 데이터 원본에서 지 원하는 값 범위를 벗어났습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) *Bufferlength* 의 값이 0 보다 작은 경우 **SQLSetDescField**의 SQL_DESC_DATA_PTR 필드에 대 한 설명을 참조 하세요.|  
|HY104|전체 자릿수 또는 소수 자릿수 값이 잘못 되었습니다.|*Columnsize* 또는 *DecimalDigits* 인수에 지정 된 값이 *ParameterType* 인수로 지정 된 SQL 데이터 형식의 열에 대 한 데이터 원본에서 지 원하는 값 범위를 벗어났습니다.|  
|HY105|매개 변수 형식이 잘못 되었습니다.|(DM) *Inputoutputtype* 인수에 지정 된 값이 잘못 되었습니다. "설명"을 참조 하십시오.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본은 인수 *ValueType* 에 지정 된 값과 인수 *ParameterType*에 지정 된 드라이버별 값의 조합으로 지정 된 변환을 지원 하지 않습니다.<br /><br /> *ParameterType* 인수에 지정 된 값이 드라이버에서 지원 되는 odbc 버전에 대 한 올바른 odbc SQL 데이터 형식 식별자 이지만 드라이버 또는 데이터 원본에서 지원 하지 않습니다.<br /><br /> 드라이버는 ODBC 2만 지원 합니다. *x* 와 인수 *ValueType* 은 다음 중 하나입니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 그리고 부록 D: 데이터 형식의 [c 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 에 나열 된 모든 interval c 데이터 형식입니다.<br /><br /> 드라이버는 3.50 이전의 ODBC 버전만 지원 하 고 인수 *ValueType* 은 SQL_C_GUID 되었습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석

 응용 프로그램은 **SQLBindParameter** 를 호출 하 여 SQL 문의 각 매개 변수 표식을 바인딩합니다. 바인딩은 응용 프로그램이 **SQLBindParameter** 를 다시 호출 하거나, SQL_RESET_PARAMS 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하거나, **SQLSetDescField** 를 호출 하 여 apd의 SQL_DESC_COUNT 헤더 필드를 0으로 설정할 때까지 적용 된 상태로 유지 됩니다.  
  
 매개 변수에 대 한 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요. 매개 변수 데이터 형식 및 매개 변수 표식에 대 한 자세한 내용은 [매개 변수 데이터 형식](../../../odbc/reference/appendixes/parameter-data-types.md) 및 매개 변수 [표식](../../../odbc/reference/appendixes/parameter-markers.md) (부록 C: SQL 문법)을 참조 하세요.  
  
## <a name="parameternumber-argument"></a>ParameterNumber 인수  
 **SQLBindParameter** 에 대 한 호출의 *parameternumber* 가 SQL_DESC_COUNT 값 보다 크면 **SQLSetDescField** 가 호출 되어 SQL_DESC_COUNT 값을 *parameternumber*로 늘립니다.  
  
## <a name="inputoutputtype-argument"></a>InputOutputType 인수  
 *Inputoutputtype* 인수는 매개 변수의 유형을 지정 합니다. 이 인수는 IPD의 SQL_DESC_PARAMETER_TYPE 필드를 설정 합니다. **INSERT** 문과 같이 프로시저를 호출 하지 않는 SQL 문의 모든 매개 변수는 *입력 * * 매개 변수*입니다. 프로시저 호출의 매개 변수는 입력, 입/출력 또는 출력 매개 변수가 될 수 있습니다. 응용 프로그램은 프로시저 호출에서 매개 변수의 형식을 확인 하기 위해 **SQLProcedureColumns** 를 호출 합니다. 형식을 확인할 수 없는 매개 변수는 입력 매개 변수로 간주 됩니다.  
  
 *Inputoutputtype* 인수는 다음 값 중 하나입니다.  
  
-   SQL_PARAM_INPUT. 매개 변수는 **INSERT** 문과 같은 프로시저를 호출 하지 않는 SQL 문에서 매개 변수를 표시 하거나 프로시저에서 입력 매개 변수를 표시 합니다. 예를 들어 **직원 값으로 삽입 (?,?,?)** 의 매개 변수는 입력 매개 변수 이지만 **{call AddEmp (?,?,?)}** 의 매개 변수는 입력 매개 변수가 될 수 있지만 반드시 그럴 필요는 없습니다.  
  
     문이 실행 되 면 드라이버는 매개 변수의 데이터를 데이터 원본으로 보냅니다. \* *parametervalueptr* 버퍼에는 유효한 입력 값이 포함 되어야 합니다. 또는 **StrLen_or_IndPtr* 버퍼에는 SQL_LEN_DATA_AT_EXEC 매크로의 SQL_NULL_DATA, SQL_DATA_AT_EXEC 또는 결과가 포함 되어야 합니다.  
  
     응용 프로그램이 프로시저 호출에서 매개 변수의 형식을 확인할 수 없는 경우 *Inputoutputtype* 을 SQL_PARAM_INPUT로 설정 합니다. 데이터 원본에서 매개 변수에 대 한 값을 반환 하는 경우 드라이버에서 해당 값을 삭제 합니다.  
  
-   SQL_PARAM_INPUT_OUTPUT. 매개 변수는 프로시저에서 입/출력 매개 변수를 표시 합니다. 예를 들어 **{Call GetEmpDept (?)}** 의 매개 변수는 직원의 이름을 받아 직원의 부서 이름을 반환 하는 입력/출력 매개 변수입니다.  
  
     문이 실행 되 면 드라이버는 매개 변수의 데이터를 데이터 원본으로 보냅니다. \* *parametervalueptr* 버퍼에는 유효한 입력 값이 포함 되어 있거나, \* *StrLen_or_IndPtr* 버퍼에 SQL_NULL_DATA, SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과가 포함 되어야 합니다. 문이 실행 된 후 드라이버는 매개 변수에 대 한 데이터를 응용 프로그램에 반환 합니다. 데이터 원본에서 입력/출력 매개 변수의 값을 반환 하지 않는 경우 드라이버는 **StrLen_or_IndPtr* 버퍼를 SQL_NULL_DATA으로 설정 합니다.  
  
    > [!NOTE]  
    >  Odbc 1.0 응용 프로그램이 ODBC 2.0 드라이버에서 **SQLSetParam** 를 호출 하면 드라이버 관리자는이를 *inputoutputtype* 인수가 SQL_PARAM_INPUT_OUTPUT로 설정 된 **SQLBindParameter** 에 대 한 호출로 변환 합니다.  
  
-   SQL_PARAM_OUTPUT. 매개 변수는 프로시저의 반환 값 또는 프로시저의 출력 매개 변수를 표시 합니다. 두 경우 모두 *출력 매개 변수*라고 합니다. 예를 들어 **{? = Call GetNextEmpID}** 의 매개 변수는 다음 직원 ID를 반환 하는 출력 매개 변수입니다.  
  
     문이 실행 된 후에는 매개 변수에 대 한 데이터를 반환 합니다 .이 경우 *Parametervalueptr* 및 *StrLen_or_IndPtr* 인수가 모두 null 포인터 이면 드라이버는 출력 값을 삭제 합니다. 데이터 원본에서 출력 매개 변수의 값을 반환 하지 않는 경우 드라이버는 **StrLen_or_IndPtr* 버퍼를 SQL_NULL_DATA으로 설정 합니다.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. 입력/출력 매개 변수를 스트리밍되는지를 나타냅니다. **SQLGetData** 는 파트의 매개 변수 값을 읽을 수 있습니다. 버퍼 길이가 **SQLGetData**호출 시 결정 되기 때문에 *bufferlength* 는 무시 됩니다. *StrLen_or_IndPtr* 버퍼의 값은 SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과를 포함 해야 합니다. 매개 변수는 출력 시 스트리밍되는 경우 입력 시 DAE (데이터 실행 시) 매개 변수로 바인딩되어야 합니다. *Parametervalueptr* 은 입력 및 출력 모두에 대해 값이 *parametervalueptr* 과 함께 전달 된 사용자 정의 토큰으로 **sqlparamdata** 에서 반환 되는 null이 아닌 모든 포인터 값일 수 있습니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요.  
  
-   SQL_PARAM_OUTPUT_STREAM. 출력 매개 변수의 경우 SQL_PARAM_INPUT_OUTPUT_STREAM와 동일 합니다. **StrLen_or_IndPtr* 은 입력에서 무시 됩니다.  
  
 다음 표에서는 *Inputoutputtype* 과 **StrLen_or_IndPtr*의 다양 한 조합을 보여 줍니다.  
  
|*InputOutputType*|**StrLen_or_IndPtr*|결과|ParameterValuePtr에 대 한 주석|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*LEN*) 또는 SQL_DATA_AT_EXEC|파트의 입력|*Parametervalueptr* 은 해당 값이 *parametervalueptr*으로 전달 된 사용자 정의 토큰으로 **sqlparamdata** 에서 반환 되는 포인터 값일 수 있습니다.|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*LEN*) 또는 SQL_DATA_AT_EXEC|입력 바인딩 버퍼|*Parametervalueptr* 은 입력 버퍼의 주소입니다.|  
|SQL_PARAM_OUTPUT|입력 시 무시 됩니다.|출력 바인딩 버퍼|*Parametervalueptr* 은 출력 버퍼의 주소입니다.|  
|SQL_PARAM_OUTPUT_STREAM|입력 시 무시 됩니다.|스트리밍된 출력|*Parametervalueptr* 은 값이 *parametervalueptr*으로 전달 된 사용자 정의 토큰으로 **sqlparamdata** 에서 반환 되는 모든 포인터 값일 수 있습니다.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*LEN*) 또는 SQL_DATA_AT_EXEC|파트 및 출력 바인딩 버퍼의 입력|*Parametervalueptr* 은 값이 *parametervalueptr*으로 전달 된 사용자 정의 토큰으로 **sqlparamdata** 에 의해 반환 되는 출력 버퍼의 주소입니다.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*LEN*) 또는 SQL_DATA_AT_EXEC|입력 바인딩 버퍼 및 출력 바인딩 버퍼|*Parametervalueptr* 은 공유 된 입력/출력 버퍼의 주소입니다.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*LEN*) 또는 SQL_DATA_AT_EXEC|파트 및 스트리밍된 출력의 입력|*Parametervalueptr* 은 null이 아닌 모든 포인터 값이 될 수 있으며,이 값은 값이 입력 및 출력 모두에 대해 *Parametervalueptr* 으로 전달 된 사용자 정의 토큰으로 **sqlparamdata** 에서 반환 됩니다.|  
  
> [!NOTE]  
>  드라이버는 응용 프로그램에서 출력 또는 입력 출력 매개 변수를 스트리밍된로 바인딩할 때 허용 되는 SQL 유형을 결정 해야 합니다. 드라이버 관리자는 잘못 된 SQL 형식에 대해 오류를 생성 하지 않습니다.  
  
## <a name="valuetype-argument"></a>ValueType 인수

 *ValueType* 인수는 매개 변수의 C 데이터 형식을 지정 합니다. 이 인수는 APD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정 합니다. 부록 D: 데이터 형식의 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션에 있는 값 중 하나 여야 합니다.  
  
 *ValueType* 인수가 interval 데이터 형식 중 하나인 경우 Apd의 *parameternumber* 레코드 SQL_DESC_TYPE 필드가 SQL_INTERVAL로 설정 되 고, apd의 SQL_DESC_CONCISE_TYPE 필드가 간결한 간격 데이터 형식으로 설정 되 고, *parameternumber* 레코드의 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 특정 interval 데이터 형식에 대 한 하위 코드로 설정 됩니다. [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요. APD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 SQL_DESC_PRECISION 필드에 설정 된 기본 간격 선행 전체 자릿수 (2) 및 기본 간격 (6)은 각각 데이터에 사용 됩니다. 기본 전체 자릿수가 적절 하지 않은 경우에는 응용 프로그램에서 **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 설명자 필드를 명시적으로 설정 해야 합니다.  
  
 *ValueType* 인수가 datetime 데이터 형식 중 하나인 경우 Apd의 *parameternumber* 레코드의 SQL_DESC_TYPE 필드가 SQL_DATETIME로 설정 되 고, Apd의 *parameternumber* 레코드의 SQL_DESC_CONCISE_TYPE 필드가 간결한 datetime C 데이터 형식으로 설정 되 고, *parameternumber* 레코드의 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 특정 datetime 데이터 형식에 대 한 하위 코드로 설정 됩니다. [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.  
  
 *ValueType* 인수가 SQL_C_NUMERIC 데이터 형식이 면 apd의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정 된 기본 전체 자릿수 (드라이버 정의)와 기본 소수 자릿수 (0)가 데이터에 사용 됩니다. 기본 전체 자릿수 또는 소수 자릿수가 적절 하지 않은 경우 응용 프로그램에서 **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 설명자 필드를 명시적으로 설정 해야 합니다.  
  
 SQL_C_DEFAULT *ParameterType*를 사용 하 여 지정 된 SQL 데이터 형식에 대 한 기본 C 데이터 형식에서 매개 변수 값을 전송 하도록 지정 합니다.  
  
 확장 된 C 데이터 형식을 지정할 수도 있습니다. 자세한 내용은 [ODBC의 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)을 참조 하세요.  
  
 자세한 내용은 [기본 c 데이터 형식](../../../odbc/reference/appendixes/default-c-data-types.md), [c에서 sql 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)및 부록 D: 데이터 형식에서 데이터 [를 sql에서 c 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 을 참조 하세요.  
  
## <a name="parametertype-argument"></a>ParameterType 인수

 이 값은 부록 D: 데이터 형식의 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 섹션에 나열 된 값 중 하나 여야 합니다. 또는 드라이버 관련 값 이어야 합니다. 이 인수는 IPD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정 합니다.  
  
 *ParameterType* 인수가 datetime 식별자 중 하나인 경우 IPD의 SQL_DESC_TYPE 필드가 SQL_DATETIME로 설정 되 고, IPD의 SQL_DESC_CONCISE_TYPE 필드가 간결한 datetime SQL 데이터 형식으로 설정 되 고, SQL_DESC_DATETIME_INTERVAL_CODE 필드가 적절 한 날짜/시간 하위 코드 값으로 설정 됩니다.  
  
 *ParameterType* 가 간격 식별자 중 하나 이면 IPD의 SQL_DESC_TYPE 필드가 SQL_INTERVAL로 설정 되 고, IPD의 SQL_DESC_CONCISE_TYPE 필드가 간결한 SQL interval 데이터 형식으로 설정 되 고, IPD의 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 적절 한 간격 하위 코드 집합으로 설정 됩니다. IPD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 간격 선행 정밀도로 설정 되 고, SQL_DESC_PRECISION 필드는 간격 (초)의 전체 자릿수로 설정 됩니다 (해당 되는 경우). SQL_DESC_DATETIME_INTERVAL_PRECISION 또는 SQL_DESC_PRECISION의 기본값이 적절 하지 않은 경우 응용 프로그램은 **SQLSetDescField**를 호출 하 여 명시적으로이 값을 설정 해야 합니다. 이러한 필드에 대 한 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)를 참조 하세요.  
  
 *ValueType* 인수가 SQL_NUMERIC 데이터 형식이 면 기본 전체 자릿수 (드라이버 정의) 및 기본 소수 자릿수 (0)가 IPD의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정 된 대로 데이터에 사용 됩니다. 기본 전체 자릿수 또는 소수 자릿수가 적절 하지 않은 경우 응용 프로그램에서 **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 설명자 필드를 명시적으로 설정 해야 합니다.  
  
 데이터를 변환 하는 방법에 대 한 자세한 내용은 데이터 형식에서 데이터를 [c에서 Sql 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 형식으로 변환 및 [Sql에서 c 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 을 참조 하세요.  
  
## <a name="columnsize-argument"></a>ColumnSize 인수

 *Columnsize* 인수는 매개 변수 표식, 해당 데이터의 길이 또는 둘 다에 해당 하는 열 또는 식의 크기를 지정 합니다. 이 인수는 SQL 데이터 형식 ( *ParameterType* 인수)에 따라 IPD의 다른 필드를 설정 합니다. 이 매핑에 적용 되는 규칙은 다음과 같습니다.  
  
-   *ParameterType* 가 SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY 또는 간결한 SQL datetime 또는 interval 데이터 형식 중 하나인 경우에는 IPD의 SQL_DESC_LENGTH 필드가 *columnsize*의 값으로 설정 됩니다. 자세한 내용은 부록 D: 데이터 형식의 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 섹션을 참조 하십시오.  
  
-   *ParameterType* 가 SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL 또는 SQL_DOUBLE 이면 IPD의 SQL_DESC_PRECISION 필드가 *columnsize*의 값으로 설정 됩니다.  
  
-   다른 데이터 형식의 경우 *Columnsize* 인수는 무시 됩니다.  
  
 자세한 내용은 "매개 변수 값 전달" 및 SQL_DATA_AT_EXEC "*StrLen_or_IndPtr* 인수"를 참조 하세요.  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 인수

 *ParameterType* 가 SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND 또는 SQL_INTERVAL_MINUTE_TO_SECOND 이면 IPD의 SQL_DESC_PRECISION 필드가 *DecimalDigits*로 설정 됩니다. *ParameterType* 가 SQL_NUMERIC 또는 SQL_DECIMAL 이면 IPD의 SQL_DESC_SCALE 필드가 *DecimalDigits*로 설정 됩니다. 다른 모든 데이터 형식의 경우 *DecimalDigits* 인수는 무시 됩니다.  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 인수

 *Parameter인수* 는 **Sqlexecute** 또는 **sqlexecdirect** 가 호출 될 때 매개 변수에 대 한 실제 데이터를 포함 하는 버퍼를 가리킵니다. 데이터는 *ValueType* 인수로 지정 된 형식 이어야 합니다. 이 인수는 APD의 SQL_DESC_DATA_PTR 필드를 설정 합니다. StrLen_or_IndPtr SQL_NULL_DATA 또는 SQL_DATA_AT_EXEC 경우 응용 프로그램 *은 매개 변수를 null* 포인터로 설정할 수 있습니다. * \** 이는 입력 또는 입/출력 매개 변수에만 적용 됩니다.  
  
 \* *StrLen_or_IndPtr* SQL_LEN_DATA_AT_EXEC (*길이*) 매크로 또는 SQL_DATA_AT_EXEC의 결과인 경우 *parametervalueptr* 은 매개 변수와 연결 된 응용 프로그램 정의 포인터 값입니다. **Sqlparamdata**를 통해 응용 프로그램에 반환 됩니다. 예를 들어 매개 변수 번호, 데이터에 대 한 포인터 또는 응용 프로그램에서 입력 매개 변수를 바인딩하는 데 사용 하는 구조에 대 한 포인터와 같은 0이 아닌 토큰을 *Parametervalueptr* 으로 사용할 수 있습니다. 그러나 매개 변수가 입/출력 매개 변수인 경우 *Parametervalueptr* 은 출력 값이 저장 되는 버퍼에 대 한 포인터 여야 합니다. SQL_ATTR_PARAMSET_SIZE statement 특성의 값이 1 보다 크면 응용 프로그램은 SQL_ATTR_PARAMS_PROCESSED_PTR statement 특성에 의해 가리키는 값을 *Parametervalueptr* 인수와 함께 사용할 수 있습니다. 예를 들어 *Parametervalueptr* 은 값의 배열을 가리키면 응용 프로그램은 SQL_ATTR_PARAMS_PROCESSED_PTR에서 가리키는 값을 사용 하 여 배열에서 올바른 값을 검색할 수 있습니다. 자세한 내용은이 섹션의 뒷부분에 나오는 "매개 변수 값 전달"을 참조 하십시오.  
  
 *Inputoutputtype* 인수가 SQL_PARAM_INPUT_OUTPUT 또는 SQL_PARAM_OUTPUT 인 경우 *Parametervalueptr* 은 드라이버가 출력 값을 반환 하는 버퍼를 가리킵니다. 프로시저에서 하나 이상의 결과 집합을 반환 하 \*는 경우에는 모든 결과 집합/행 개수가 처리 될 때까지 *parametervalueptr* 버퍼가 설정 되지 않을 수 있습니다. 처리가 완료 될 때까지 버퍼를 설정 하지 않으면 **SQLMoreResults** 가 SQL_NO_DATA를 반환할 때까지 출력 매개 변수와 반환 값을 사용할 수 없습니다. SQL_CLOSE 옵션을 사용 하 여 **SQLCloseCursor** 또는 **SQLFreeStmt** 를 호출 하면 이러한 값이 삭제 됩니다.  
  
 SQL_ATTR_PARAMSET_SIZE statement 특성의 값이 1 보다 크면 *Parametervalueptr* 이 배열을 가리킵니다. 단일 SQL 문은 입력 또는 입/출력 매개 변수에 대 한 입력 값의 전체 배열을 처리 하 고 입력/출력 또는 출력 매개 변수에 대 한 출력 값의 배열을 반환 합니다.  
  
## <a name="bufferlength-argument"></a>BufferLength 인수

 문자 및 이진 C 데이터의 경우 *bufferlength* 인수는 \* *parametervalueptr* 버퍼의 길이 (단일 요소인 경우) 또는 \* *parametervalueptr* 배열의 요소 길이 (SQL_ATTR_PARAMSET_SIZE statement 특성의 값이 1 보다 큰 경우)를 지정 합니다. 이 인수는 APD의 SQL_DESC_OCTET_LENGTH 레코드 필드를 설정 합니다. 응용 프로그램에서 여러 값을 지정 하는 경우 *Bufferlength* 를 사용 하 여 입력 및 출력 모두에서 **Parametervalueptr* 배열의 값 위치를 확인 합니다. 입/출력 및 출력 매개 변수의 경우 출력에서 문자 및 이진 C 데이터를 잘라낼 지 여부를 결정 하는 데 사용 됩니다.  
  
-   문자 C 데이터의 경우 반환할 수 있는 바이트 수가 *bufferlength*보다 크거나 같은 경우 \* *parametervalueptr* 의 데이터는 null 종료 문자의 길이 보다 작은 *bufferlength* 로 잘리고 드라이버에 의해 null로 종료 됩니다.  
  
-   이진 C 데이터의 경우 반환할 수 있는 바이트 수가 *bufferlength*보다 크면 \* *parametervalueptr* 의 데이터가 *bufferlength* 바이트로 잘립니다.  
  
 다른 모든 형식의 C 데이터에 대해 *Bufferlength* 인수는 무시 됩니다. \* *Parametervalueptr* 버퍼의 길이 (단일 요소에 해당 하는 경우) 또는 \* *parametervalueptr* 배열의 요소 길이 (응용 프로그램에서 각 매개 변수에 대해 여러 값을 지정 하는 SQL_ATTR_PARAMSET_SIZE의 *특성* 인수를 사용 하 여 **SQLSetStmtAttr** 를 호출 하는 경우)는 C 데이터 형식의 길이로 가정 됩니다.  
  
 스트리밍된 출력 또는 스트리밍된 입력/출력 매개 변수의 경우 버퍼 길이가 **SQLGetData**에서 지정 되므로 *bufferlength* 인수가 무시 됩니다.  
  
> [!NOTE]  
>  Odbc 1.0 응용 프로그램이 ODBC 3에서 **SQLSetParam** 를 호출 하는 경우 *x* 드라이버, 드라이버 관리자는이를 *bufferlength* 인수가 항상 SQL_SETPARAM_VALUE_MAX **SQLBindParameter** 호출로 변환 합니다. ODBC 3 인 경우 드라이버 관리자에서 오류를 반환 합니다. *x* 응용 프로그램은 *BUFFERLENGTH* 를 ODBC 3 인 SQL_SETPARAM_VALUE_MAX로 설정 합니다. *x* 드라이버는이를 사용 하 여 ODBC 1.0 응용 프로그램에서 호출 되는 시기를 확인할 수 있습니다.  
  
> [!NOTE]  
>  **SQLSetParam**에서 응용 프로그램이 문자 또는 이진 데이터를 반환할 수 있도록 **Parametervalueptr* 버퍼의 길이를 지정 하는 방법과 응용 프로그램에서 문자 또는 이진 매개 변수 값 배열을 드라이버에 전송 하는 방법이 드라이버에 정의 되어 있습니다.  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr 인수

 *StrLen_or_IndPtr* 인수는 **Sqlexecute** 또는 **sqlexecdirect** 가 호출 될 때 다음 중 하나를 포함 하는 버퍼를 가리킵니다. 이 인수는 응용 프로그램 매개 변수 포인터의 SQL_DESC_OCTET_LENGTH_PTR 및 SQL_DESC_INDICATOR_PTR 레코드 필드를 설정 합니다.  
  
-   **Parametervalueptr*에 저장 된 매개 변수 값의 길이입니다. 문자 또는 이진 C 데이터를 제외 하 고는 무시 됩니다.  
  
-   SQL_NTS. 매개 변수 값이 null로 끝나는 문자열입니다.  
  
-   SQL_NULL_DATA. 매개 변수 값이 NULL입니다.  
  
-   SQL_DEFAULT_PARAM. 프로시저는 응용 프로그램에서 검색 된 값 대신 매개 변수의 기본값을 사용 하는 것입니다. 이 값은 ODBC 정식 구문에서 호출 된 프로시저 에서만 유효 하며,이 경우 *Inputoutputtype* 인수가 SQL_PARAM_INPUT, SQL_PARAM_INPUT_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT_STREAM 인 경우에만 유효 합니다. \* *StrLen_or_IndPtr* SQL_DEFAULT_PARAM 되는 경우 *ValueType*, *ParameterType*, *columnsize*, *DecimalDigits*, *bufferlength*및 *parametervalueptr* 인수는 입력 매개 변수에 대해 무시 되 고 입력/출력 매개 변수의 출력 매개 변수 값을 정의 하는 데만 사용 됩니다.  
  
-   SQL_LEN_DATA_AT_EXEC (*길이*) 매크로의 결과입니다. 매개 변수에 대 한 데이터는 **Sqlputdata**를 사용 하 여 전송 됩니다. *ParameterType* 인수가 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 길고 데이터 원본 관련 데이터 형식이 고 드라이버에서 **SQLGetInfo**의 SQL_NEED_LONG_DATA_LEN 정보 형식에 대해 "Y"를 반환 하는 경우 *길이* 는 매개 변수에 대해 전송 되는 데이터 바이트 수입니다. 그렇지 않으면 *길이* 는 음수가 아닌 값 이어야 하며 무시 됩니다. 자세한 내용은이 섹션의 뒷부분에 나오는 "매개 변수 값 전달"을 참조 하십시오.  
  
     예를 들어 하나 이상의 호출에서 **Sqlputdata** 를 사용 하 여 1만 바이트의 데이터를 전송 하도록 지정 하려면 SQL_LONGVARCHAR 매개 변수의 경우 응용 프로그램에서 **StrLen_or_IndPtr* 를 SQL_LEN_DATA_AT_EXEC (10000)로 설정 합니다.  
  
-   SQL_DATA_AT_EXEC. 매개 변수에 대 한 데이터는 **Sqlputdata**를 사용 하 여 전송 됩니다. 이 값은 odbc 1.0 응용 프로그램에서 ODBC 3을 호출할 때 사용 됩니다. *x* 드라이버. 자세한 내용은이 섹션의 뒷부분에 나오는 "매개 변수 값 전달"을 참조 하십시오.  
  
 *StrLen_or_IndPtr* null 포인터인 경우 드라이버는 모든 입력 매개 변수 값이 null이 아니고 해당 문자 및 이진 데이터가 null로 종료 된다고 가정 합니다. *Inputoutputtype* 이 SQL_PARAM_OUTPUT 또는 SQL_PARAM_OUTPUT_STREAM이 고 *Parametervalueptr* 및 *StrLen_or_IndPtr* 모두 null 포인터인 경우 드라이버는 출력 값을 삭제 합니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자는 매개 변수의 데이터 형식이 SQL_C_BINARY 될 때 *StrLen_or_IndPtr* 에 대해 null 포인터를 지정 하지 않는 것이 좋습니다. 드라이버가 예기치 않게 SQL_C_BINARY 데이터를 잘라내는 것이 아닌지 확인 하려면 *StrLen_or_IndPtr* 올바른 길이 값에 대 한 포인터를 포함 해야 합니다.  
  
 *Inputoutputtype* 인수가 SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM 인 경우, *StrLen_or_IndPtr* 가 반환 하는 데 사용할 수 있는 바이트 수 (문자 데이터의 NULL 종결 바이트 제외) 또는 SQL_NULL_DATA \* *(반환* 에 사용할 수 있는 바이트 수를 확인할 수 없는 경우)가 SQL_NO_TOTAL 반환 하는 버퍼를 가리킵니다. 프로시저에서 하나 이상의 결과 집합을 반환 하는 경우 모든 결과가 인출 될 때까지 **StrLen_or_IndPtr* 버퍼가 설정 되지 않을 수 있습니다.  
  
 SQL_ATTR_PARAMSET_SIZE statement 특성의 값이 1 보다 크면 *StrLen_or_IndPtr* 는 sqllen 값의 배열을 가리킵니다. 이러한 값은이 섹션의 앞부분에 나열 된 값 중 하나일 수 있으며 단일 SQL 문을 사용 하 여 처리 됩니다.  
  
## <a name="passing-parameter-values"></a>매개 변수 값 전달

 응용 프로그램은 매개 변수 \*값을 *parametervalueptr* 버퍼 또는 **sqlputdata**에 대 한 하나 이상의 호출로 전달할 수 있습니다. **Sqlputdata** 를 사용 하 여 해당 데이터를 전달 하는 매개 변수는 *실행 시 데이터* 매개 변수 라고 합니다. 이러한 매개 변수는 일반적으로 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 매개 변수에 대 한 데이터를 전송 하는 데 사용 되며 다른 매개 변수와 혼합할 수 있습니다.  
  
 매개 변수 값을 전달 하기 위해 응용 프로그램은 다음과 같은 일련의 단계를 수행 합니다.  
  
1.  는 각 매개 변수에 대해 **SQLBindParameter** 를 호출 하 여 매개 변수 값 (*Parametervalueptr* 인수) 및 길이/표시기 (*StrLen_or_IndPtr* 인수)에 대 한 버퍼를 바인딩합니다. 실행 시 데이터 매개 변수의 경우 *Parametervalueptr* 은 매개 변수 번호 또는 데이터에 대 한 포인터와 같은 응용 프로그램 정의 포인터 값입니다. 나중에 값이 반환 되 고 매개 변수를 식별 하는 데 사용할 수 있습니다.  
  
2.  \* *Parametervalueptr* 및 **StrLen_or_IndPtr* 버퍼에 입력 및 입/출력 매개 변수의 값을 배치 합니다.  
  
    -   일반 매개 변수의 경우 응용 프로그램은 매개 변수 값을 \* *parametervalueptr* 버퍼에 배치 하 고 해당 값의 길이를 **StrLen_or_IndPtr* 버퍼에 배치 합니다. 자세한 내용은 [매개 변수 값 설정](../../../odbc/reference/develop-app/setting-parameter-values.md)을 참조 하세요.  
  
    -   실행 시 데이터 매개 변수의 경우 응용 프로그램은 **StrLen_or_IndPtr* 버퍼에 SQL_LEN_DATA_AT_EXEC (*길이*) 매크로 (ODBC 2.0 드라이버를 호출할 때)의 결과를 저장 합니다.  
  
3.  **Sqlexecute** 또는 **sqlexecdirect** 를 호출 하 여 SQL 문을 실행 합니다.  
  
    -   실행 시 데이터 매개 변수가 없으면 프로세스가 완료 된 것입니다.  
  
    -   실행 시 데이터 매개 변수가 있는 경우 함수는 SQL_NEED_DATA을 반환 합니다.  
  
4.  처리할 첫 번째 실행 시 데이터 매개 변수에 대해 **SQLBindParameter** 의 *Parametervalueptr* 인수에 지정 된 응용 프로그램 정의 값을 검색 하기 위해 **sqlparamdata** 를 호출 합니다. **Sqlparamdata** 는 SQL_NEED_DATA를 반환 합니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수는 실행 시 데이터 열과 비슷하지만 **Sqlparamdata** 에서 반환 되는 값은 서로 다릅니다. 실행 시 데이터 매개 변수는 문이 **Sqlputdata** 또는 **sqlexecute**를 사용 하 여 실행 될 때 **sqlputdata** 를 사용 하 여 데이터를 전송 하는 SQL 문의 매개 변수입니다. **SQLBindParameter**와 바인딩됩니다. **Sqlparamdata** 에서 반환 되는 값은 *Parametervalueptr* 인수에서 **SQLBindParameter** 로 전달 되는 포인터 값입니다. 실행 시 데이터 열은 행이 업데이트 되거나 **SQLBulkOperations** 로 추가 되거나 **SQLSetPos**로 업데이트 될 때 **sqlputdata** 를 사용 하 여 데이터를 전송 하는 행 집합의 열입니다. **SQLBindCol**와 바인딩됩니다. **Sqlparamdata** 에서 반환 되는 값은 처리 중인 **Targetvalueptr* 버퍼 ( **SQLBindCol**에 대 한 호출에 의해 설정 됨)의 행 주소입니다.  
  
5.  **Sqlputdata** 를 한 번 이상 호출 하 여 매개 변수에 대 한 데이터를 보냅니다. 데이터 값이 **sqlputdata**에 지정 된 *parametervalueptr* 버퍼 \*보다 클 경우 둘 이상의 호출이 필요 합니다. 동일한 매개 변수에 대 한 **Sqlputdata** 에 대 한 여러 호출은 문자, 이진 또는 데이터 원본 관련 데이터 형식이 있는 열에 문자 c 데이터를 보내거나 문자, 이진 또는 데이터 원본 관련 데이터 형식이 있는 열에 이진 c 데이터를 보내는 경우에만 허용 됩니다.  
  
6.  **Sqlparamdata** 를 다시 호출 하 여 매개 변수에 대 한 모든 데이터가 전송 되었음을 알립니다.  
  
    -   실행 시 데이터 매개 변수가 더 있는 경우 **Sqlparamdata** 는 SQL_NEED_DATA을 반환 하 고 다음 실행 시 데이터 매개 변수에 대해 처리할 응용 프로그램 정의 값을 반환 합니다. 응용 프로그램은 4 단계와 5 단계를 반복 합니다.  
  
    -   실행 시 데이터 매개 변수가 더 이상 없으면 프로세스가 완료 된 것입니다. 문이 성공적으로 실행 된 경우 **Sqlparamdata** 는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 합니다. 실행에 실패 하면 SQL_ERROR 반환 됩니다. 이 시점에서 **Sqlparamdata** 는 문 (**sqlparamdata** 또는 **sqlexecute**)을 실행 하는 데 사용 되는 함수에 의해 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
         입력/출력 또는 출력 매개 변수의 출력 값은 응용 프로그램이 문에서 생성 \*된 모든 결과 집합을 검색 한 후 *parametervalueptr* 및 **StrLen_or_IndPtr* 버퍼에서 사용할 수 있습니다.  
  
 **Sqlexecute** 또는 **sqlexecdirect** 를 호출 하면 문이 SQL_NEED_DATA 상태로 전환 됩니다. 이 시점에서 응용 프로그램은 문과 연결 된 문 또는 *연결 핸들* 을 사용 하 여 **sqlcancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **sqlparamdata**또는 **sqlputdata** 만 호출할 수 있습니다. 문 또는 문과 연결 된 연결을 사용 하 여 다른 함수를 호출 하는 경우이 함수는 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. **Sqlparamdata** 또는 **sqlparamdata** 에서 오류를 반환 하거나 **sqlparamdata** 가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 하거나 문이 취소 되는 경우 문은 SQL_NEED_DATA 상태를 유지 합니다.  
  
 응용 프로그램이 실행 시 데이터 매개 변수에 대 한 데이터를 필요로 하는 동안 **Sqlcancel** 을 호출 하는 경우 드라이버는 문 실행을 취소 합니다. 그러면 응용 프로그램에서 **Sqlexecute** 또는 **sqlexecdirect** 를 다시 호출할 수 있습니다.  
  
## <a name="retrieving-streamed-output-parameters"></a>스트리밍된 출력 매개 변수 검색

 응용 프로그램에서 *Inputoutputtype* 을 SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM로 설정 하는 경우 **SQLGetData**에 대 한 호출 하나 이상에서 출력 매개 변수 값을 검색 해야 합니다. 응용 프로그램에 반환할 스트리밍된 출력 매개 변수 값이 드라이버에 있으면 **SQLMoreResults**, **Sqlexecute**및 **sqlexecdirect**함수 호출에 대 한 응답으로 SQL_PARAM_DATA_AVAILABLE 반환 됩니다. 응용 프로그램은 **Sqlparamdata** 를 호출 하 여 사용할 수 있는 매개 변수 값을 확인 합니다.  
  
 SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요.  
  
## <a name="using-arrays-of-parameters"></a>매개 변수 배열 사용

 응용 프로그램에서 매개 변수 표식을 사용 하 여 문을 준비 하 고 매개 변수 배열에 전달 하는 경우이를 실행할 수 있는 두 가지 방법이 있습니다. 한 가지 방법은 드라이버가 백 엔드의 배열 처리 기능을 사용 하는 것입니다 .이 경우 매개 변수 배열을 사용 하는 전체 문이 하나의 원자 단위로 처리 됩니다. Oracle은 배열 처리 기능을 지 원하는 데이터 원본의 예입니다. 이 기능을 구현 하는 또 다른 방법은 드라이버에서 SQL 문 일괄 처리를 생성 하 고, 매개 변수 배열의 각 매개 변수 집합에 대해 SQL 문을 하나씩 실행 하 고, 일괄 처리를 실행 하는 것입니다. 매개 변수 배열은 **WHERE CURRENT of** 문과 함께 사용할 수 없습니다.  
  
 매개 변수 배열을 처리할 때 개별 결과 집합/행 개수 (각 매개 변수 집합에 대해 하나씩)를 사용 하거나 결과 집합/행 수를 하나로 롤업할 수 있습니다. **SQLGetInfo** 의 SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 각 매개 변수 집합에 대해 행 개수를 사용할 수 있는지 (SQL_PARC_BATCH) 또는 하나의 행 개수만 사용할 수 있는지 (SQL_PARC_NO_BATCH)를 나타냅니다.  
  
 **SQLGetInfo** 의 SQL_PARAM_ARRAY_SELECTS 옵션은 각 매개 변수 집합에 대해 결과 집합을 사용할 수 있는지 (SQL_PAS_BATCH) 또는 하나의 결과 집합만 사용할 수 있는지 (SQL_PAS_NO_BATCH)를 나타냅니다. 드라이버에서 매개 변수 배열을 사용 하 여 결과 집합 생성 문을 실행 하는 것을 허용 하지 않는 경우 SQL_PARAM_ARRAY_SELECTS는 SQL_PAS_NO_SELECT 반환 합니다.  
  
 자세한 내용은 [SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)를 참조 하세요.  
  
 매개 변수 배열을 지원 하기 위해 SQL_ATTR_PARAMSET_SIZE statement 특성을 설정 하 여 각 매개 변수에 대 한 값의 수를 지정 합니다. 필드가 1 보다 크면 APD의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드가 배열을 가리켜야 합니다. 각 배열의 카디널리티는 SQL_ATTR_PARAMSET_SIZE의 값과 같습니다.  
  
 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드는 오류 집합을 포함 하 여 처리 된 매개 변수 집합의 수를 포함 하는 버퍼를 가리킵니다. 각 매개 변수 집합이 처리 될 때 드라이버는 버퍼에 새 값을 저장 합니다. Null 포인터인 경우에는 숫자가 반환 되지 않습니다. 매개 변수 배열을 사용 하는 경우 설정 함수에서 SQL_ERROR을 반환 하더라도 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드가 가리키는 값이 채워집니다. SQL_NEED_DATA 반환 되 면 APD의 SQL_DESC_ROWS_PROCESSED_PTR 필드가 가리키는 값이 처리 되는 매개 변수 집합으로 설정 됩니다.  
  
 매개 변수 배열이 바인딩되고 **CURRENT of** 문이 실행 되는 업데이트는 드라이버에 정의 된 경우에 발생 합니다.  
  
## <a name="column-wise-parameter-binding"></a>열 단위 매개 변수 바인딩

 열 단위 바인딩에서 응용 프로그램은 각 매개 변수에 개별 매개 변수 및 길이/표시기 배열을 바인딩합니다.  
  
 열 단위 바인딩을 사용 하기 위해 응용 프로그램은 먼저 SQL_ATTR_PARAM_BIND_TYPE statement 특성을 SQL_PARAM_BIND_BY_COLUMN로 설정 합니다. 이것이 기본값입니다. 바인딩할 각 열에 대해 응용 프로그램은 다음 단계를 수행 합니다.  
  
1.  매개 변수 버퍼 배열을 할당 합니다.  
  
2.  길이/표시기 버퍼의 배열을 할당 합니다.  
  
    > [!NOTE]  
    >  열 단위 바인딩을 사용할 때 응용 프로그램이 설명자에 직접 쓰면 길이 및 표시기 데이터에 대해 별도의 배열을 사용할 수 있습니다.  
  
3.  다음 인수를 사용 하 여 **SQLBindParameter** 를 호출 합니다.  
  
    -   *ValueType* 은 매개 변수 버퍼 배열에서 단일 요소의 C 형식입니다.  
  
    -   *ParameterType* 는 매개 변수의 SQL 형식입니다.  
  
    -   *Parametervalueptr* 은 매개 변수 버퍼 배열의 주소입니다.  
  
    -   *Bufferlength* 는 매개 변수 버퍼 배열의 단일 요소 크기입니다. 데이터가 고정 길이 데이터 이면 *Bufferlength* 인수가 무시 됩니다.  
  
    -   *StrLen_or_IndPtr* 는 길이/지표 배열의 주소입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "주석"의 "ParameterValuePtr 인수"를 참조 하세요. 매개 변수의 열 단위 바인딩에 대 한 자세한 내용은 [매개 변수 배열 바인딩](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)을 참조 하세요.  
  
## <a name="row-wise-parameter-binding"></a>행 단위 매개 변수 바인딩

 행 단위 바인딩에서 응용 프로그램은 바인딩할 각 매개 변수의 길이/표시기 버퍼를 포함 하는 구조체를 정의 합니다.  
  
 행 단위 바인딩을 사용 하기 위해 응용 프로그램에서는 다음 단계를 수행 합니다.  
  
1.  단일 매개 변수 집합을 포함 하는 구조체를 정의 하 고 (매개 변수 및 길이/표시기 버퍼 모두 포함) 이러한 구조체의 배열을 할당 합니다.  
  
    > [!NOTE]  
    >  행 단위 바인딩을 사용할 때 응용 프로그램이 설명자에 직접 쓰면 길이 및 표시기 데이터에 대해 별도의 필드를 사용할 수 있습니다.  
  
2.  SQL_ATTR_PARAM_BIND_TYPE statement 특성을 단일 매개 변수 집합이 포함 된 구조체의 크기나 매개 변수가 바인딩되는 버퍼의 인스턴스 크기로 설정 합니다. 길이에는 모든 바인딩된 매개 변수의 공간을 포함 해야 하 고, 구조체 또는 버퍼의 안쪽 여백을 포함 하 여 바인딩된 매개 변수의 주소가 지정 된 길이로 증가 하는 경우 결과는 다음 행. ANSI C에서 *sizeof* 연산자를 사용 하는 경우이 동작이 보장 됩니다.  
  
3.  바인딩할 각 매개 변수에 대해 다음 인수를 사용 하 여 **SQLBindParameter** 를 호출 합니다.  
  
    -   *ValueType* 은 열에 바인딩할 매개 변수 버퍼 멤버의 형식입니다.  
  
    -   *ParameterType* 는 매개 변수의 SQL 형식입니다.  
  
    -   *Parametervalueptr* 은 첫 번째 배열 요소에서 매개 변수 버퍼 멤버의 주소입니다.  
  
    -   *Bufferlength* 는 매개 변수 버퍼 멤버의 크기입니다.  
  
    -   *StrLen_or_IndPtr* 은 바인딩할 길이/표시기 멤버의 주소입니다.  
  
 이 정보를 사용 하는 방법에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "*Parametervalueptr* 인수"를 참조 하십시오. 매개 변수의 행 단위 바인딩에 대 한 자세한 내용은 [매개 변수의 바인딩 배열](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)을 참조 하세요.  
  
## <a name="error-information"></a>오류 정보

 드라이버에서 매개 변수 배열을 일괄 처리로 구현 하지 않는 경우 (SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 SQL_PARC_NO_BATCH와 같음) 한 문이 실행 된 것 처럼 오류 상황이 처리 됩니다. 드라이버에서 매개 변수 배열을 일괄 처리로 구현 하는 경우 응용 프로그램은 IPD의 헤더 필드를 SQL_DESC_ARRAY_STATUS_PTR 사용 하 여 **Sqlexecdirect** 또는 **sqlexecute** 에서 오류를 반환 하는 SQL 문 또는 매개 변수 배열에 있는 매개 변수를 확인할 수 있습니다. 이 필드에는 매개 변수 값의 각 행에 대 한 상태 정보가 포함 됩니다. 필드가 오류가 발생 했음을 나타내는 경우 진단 데이터 구조의 필드는 실패 한 매개 변수의 행 및 매개 변수 번호를 나타냅니다. 배열의 요소 수는 SQL_ATTR_PARAMSET_SIZE statement 특성에 의해 설정 될 수 있는 APD의 SQL_DESC_ARRAY_SIZE 헤더 필드에 의해 정의 됩니다.  
  
> [!NOTE]  
>  APD의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드는 매개 변수를 무시 하는 데 사용 됩니다. 매개 변수를 무시 하는 방법에 대 한 자세한 내용은 다음 섹션인 "매개 변수 집합 무시"를 참조 하십시오.  
  
 **Sqlexecute** 또는 **sqlexecdirect** 가 SQL_ERROR 반환 하는 경우 IPD의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 배열의 요소는 SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED 또는 SQL_PARAM_DIAG_UNAVAILABLE를 포함 합니다.  
  
 이 배열의 각 요소에 대해 진단 데이터 구조는 하나 이상의 상태 레코드를 포함 합니다. 구조체의 SQL_DIAG_ROW_NUMBER 필드는 오류를 발생 시킨 매개 변수 값의 행 번호를 나타냅니다. 오류를 발생 시킨 매개 변수의 행에서 특정 매개 변수를 확인할 수 있는 경우 매개 변수 번호는 SQL_DIAG_COLUMN_NUMBER 필드에 입력 됩니다.  
  
 강제 **Sqlexecute** 또는 **sqlexecdirect** 를 중단 하는 이전 매개 변수에서 오류가 발생 하 여 매개 변수가 사용 되지 않은 경우 SQL_PARAM_UNUSED가 입력 됩니다. 예를 들어 매개 변수가 50 fortieth **Sqlexecute** 또는 **sqlexecdirect** 를 중단 시킨 매개 변수 집합을 실행 하는 동안 오류가 발생 한 경우 41 ~ 50 매개 변수의 상태 배열에 SQL_PARAM_UNUSED을 입력 합니다.  
  
 드라이버에서 매개 변수 배열을 모놀리식 단위로 처리 하는 경우에는 SQL_PARAM_DIAG_UNAVAILABLE가 입력 되므로 오류 정보의 개별 매개 변수 수준을 생성 하지 않습니다.  
  
 단일 매개 변수 집합을 처리 하는 동안 일부 오류가 발생 하면 배열의 후속 매개 변수 집합을 처리할 수 없습니다. 다른 오류는 후속 매개 변수의 처리에 영향을 주지 않습니다. 처리를 중지 하는 오류는 드라이버에 정의 되어 있습니다. 처리가 중지 되지 않은 경우 배열의 모든 매개 변수가 처리 되 고, SQL_SUCCESS_WITH_INFO 오류가 발생 하 여 반환 되며, SQL_ATTR_PARAMS_PROCESSED_PTR에 의해 정의 된 버퍼가 처리 된 총 매개 변수 집합 수로 설정 됩니다. 오류 집합을 포함 하는 SQL_ATTR_PARAMSET_SIZE statement 특성).  
  
> [!CAUTION]  
>  Odbc의 매개 변수 배열을 처리할 때 오류가 발생 하는 경우 odbc 동작은 ODBC 3에서 다릅니다. *x* 는 ODBC 2 보다입니다. *x*. ODBC 2. *x*에서 함수 SQL_ERROR 반환 되 고 처리가 더 이상 수행 되지 않았습니다. **Sqlparamoptions** 의 *pirow* 인수에 의해 가리키는 버퍼에는 오류 행 번호가 포함 됩니다. ODBC 3. *x*함수는 SQL_SUCCESS_WITH_INFO을 반환 하 고 처리는 중지 또는 계속할 수 있습니다. 계속 되 면 SQL_ATTR_PARAMS_PROCESSED_PTR에 의해 지정 된 버퍼가 오류가 발생 한 모든 매개 변수 값을 포함 하 여 처리 된 모든 매개 변수 값으로 설정 됩니다. 이러한 동작이 변경 되 면 기존 응용 프로그램에 문제가 발생할 수 있습니다.  
  
 SQL_ERROR 또는 SQL_NEED_DATA 반환 된 경우와 같이 매개 변수 배열의 모든 매개 변수 집합에 대 한 처리를 완료 하기 전에 **Sqlexecute** 또는 **sqlexecdirect** 가 반환 되는 경우 상태 배열에는 이미 처리 된 매개 변수에 대 한 상태가 포함 됩니다. IPD의 SQL_DESC_ROWS_PROCESSED_PTR 필드가 가리키는 위치에는 SQL_ERROR 또는 SQL_NEED_DATA 오류 코드를 발생 시킨 매개 변수 배열의 행 번호가 포함 됩니다. 매개 변수 배열을 SELECT 문으로 보내면 상태 배열 값의 가용성은 드라이버에 정의 됩니다. 문을 실행 하거나 결과 집합을 인출 한 후에 사용할 수 있습니다.  
  
## <a name="ignoring-a-set-of-parameters"></a>매개 변수 집합 무시

 SQL_ATTR_PARAM_STATUS_PTR statement 특성에 의해 설정 된 대로 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드를 사용 하 여 SQL 문의 바인딩된 매개 변수 집합을 무시 해야 함을 나타낼 수 있습니다. 실행 중에 하나 이상의 매개 변수 집합을 무시 하도록 드라이버에 지시 하려면 응용 프로그램에서 다음 단계를 수행 해야 합니다.  
  
1.  **SQLSetDescField** 를 호출 하 여 상태 정보를 포함 하는 SQLUSMALLINT 값의 배열을 가리키도록 apd의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 설정 합니다. **SQLSetStmtAttr** 를 호출 하 여이 필드를 설정할 수도 있습니다 .이 SQL_ATTR_PARAM_OPERATION_PTR *특성* 을 사용 하면 응용 프로그램에서 설명자 핸들을 가져오지 않고 필드를 설정할 수 있습니다.  
  
2.  APD의 SQL_DESC_ARRAY_STATUS_PTR 필드로 정의 된 배열의 각 요소를 두 값 중 하나로 설정 합니다.  
  
    -   SQL_PARAM_IGNORE-행이 문 실행에서 제외 됨을 표시 합니다.  
  
    -   SQL_PARAM_PROCEED-행이 문 실행에 포함 됨을 표시 합니다.  
  
3.  **Sqlexecdirect** 또는 **sqlexecute** 를 호출 하 여 준비 된 문을 실행 합니다.  
  
 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드로 정의 된 배열에는 다음 규칙이 적용 됩니다.  
  
-   포인터는 기본적으로 null로 설정 됩니다.  
  
-   포인터가 null 이면 모든 요소가 SQL_ROW_PROCEED로 설정 된 것 처럼 모든 매개 변수 집합이 사용 됩니다.  
  
-   요소를 SQL_PARAM_PROCEED 설정 해도 작업에서 특정 매개 변수 집합을 사용 하는 것은 보장 되지 않습니다.  
  
-   SQL_PARAM_PROCEED 헤더 파일에서 0으로 정의 됩니다.  
  
 응용 프로그램은 IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 것과 동일한 배열을 가리키도록 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드를 설정할 수 있습니다. 이는 매개 변수를 행 데이터에 바인딩하는 경우에 유용 합니다. 그런 다음 행 데이터의 상태에 따라 매개 변수를 무시할 수 있습니다. SQL_PARAM_IGNORE 외에도, 다음 코드는 SQL 문의 매개 변수가 무시 되도록 합니다. SQL_ROW_DELETED, SQL_ROW_UPDATED 및 SQL_ROW_ERROR. SQL_PARAM_PROCEED 외에도, 다음 코드는 SQL 문을 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO 및 SQL_ROW_ADDED으로 진행 합니다.  
  
## <a name="rebinding-parameters"></a>리바인딩 매개 변수

 응용 프로그램은 다음 두 작업 중 하나를 수행 하 여 바인딩을 변경할 수 있습니다.  
  
-   이미 바인딩된 열에 대해 새 바인딩을 지정 하려면 **SQLBindParameter** 를 호출 합니다. 드라이버가 기존 바인딩을 새 바인딩으로 덮어씁니다.  
  
-   **SQLBindParameter**에 대 한 바인딩 호출로 지정 된 버퍼 주소에 추가할 오프셋을 지정 합니다. 자세한 내용은 다음 섹션인 "오프셋을 사용한 리바인딩"을 참조 하세요.  
  
## <a name="rebinding-with-offsets"></a>오프셋을 사용한 리바인딩

 매개 변수의 리바인딩은 응용 프로그램에 많은 매개 변수를 포함할 수 있는 버퍼 영역 설정이 있지만 **Sqlexecdirect** 또는 **sqlexecute** 를 호출 하는 경우 몇 가지 매개 변수만 사용 하는 경우 특히 유용 합니다. 버퍼 영역의 나머지 공간은 오프셋으로 기존 바인딩을 수정 하 여 다음 매개 변수 집합에 사용할 수 있습니다.  
  
 APD의 SQL_DESC_BIND_OFFSET_PTR 헤더 필드는 바인딩 오프셋을 가리킵니다. 필드가 null이 아닌 경우 드라이버는 포인터를 역참조 하 고 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값이 모두 null 포인터인 경우 설명자의 해당 필드에 역참조 된 값을 추가 합니다. 실행 시간에 기록 합니다. SQL 문이 실행 될 때 새 포인터 값이 사용 됩니다. 리바인딩 후에는 오프셋이 유효한 상태로 유지 됩니다. SQL_DESC_BIND_OFFSET_PTR는 오프셋 자체가 아니라 오프셋에 대 한 포인터 이기 때문에 응용 프로그램은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 또는 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) 를 호출 하 여 설명자 필드를 변경 하지 않고도 오프셋을 직접 변경할 수 있습니다. 포인터는 기본적으로 null로 설정 됩니다. SQLSetDescField에 대 한 호출 또는 SQL_ATTR_PARAM_BIND_OFFSET_PTR의 *Fattribute* 를 사용 하 여 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)에 대 한 호출로 [](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 의 SQL_DESC_BIND_OFFSET_PTR 필드를 설정할 수 있습니다.  
  
 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값에 직접 추가 됩니다. 오프셋이 다른 값으로 변경 되는 경우에도 새 값이 각 설명자 필드의 값에 직접 추가 됩니다. 새 오프셋은 필드 값 및 모든 이전 오프셋의 합계에 추가 되지 않습니다.  
  
## <a name="descriptors"></a>설명자

 매개 변수가 바인딩되는 방법은 APDs 및 IPDs의 필드에 의해 결정 됩니다. **SQLBindParameter** 의 인수는 해당 설명자 필드를 설정 하는 데 사용 됩니다. **SQLSetDescField** 함수를 사용 하 여 필드를 설정할 수도 있지만 **SQLBindParameter** 는 응용 프로그램에서 **SQLBindParameter**를 호출 하기 위한 설명자 핸들을 가져올 필요가 없기 때문에 사용 하는 것이 더 효율적입니다.  
  
> [!CAUTION]  
>  한 문에 대해 **SQLBindParameter** 를 호출 하면 다른 문에 영향을 줄 수 있습니다. 이는 문과 연결 된가 명시적으로 할당 되 고 다른 문과도 연결 된 경우에 발생 합니다. **SQLBindParameter** 는 apd의 필드를 수정 하기 때문에이 설명자가 연결 된 모든 문에 수정 내용이 적용 됩니다. 이 동작이 필요한 동작이 아닌 경우 응용 프로그램은 **SQLBindParameter**를 호출 하기 전에 다른 문에서이 설명자를 분리 해야 합니다.  
  
 개념적으로 **SQLBindParameter** 는 다음 단계를 순서 대로 수행 합니다.  
  
1.  [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) 를 호출 하 여 apd 핸들을 가져옵니다.  
  
2.  [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 를 호출 하 여 apd의 SQL_DESC_COUNT 필드를 가져오고 *columnnumber* 인수의 값이 SQL_DESC_COUNT의 값을 초과 하는 경우 **SQLSetDescField** 를 호출 하 여 SQL_DESC_COUNT 값을 *columnnumber*로 늘립니다.  
  
3.  [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 을 여러 번 호출 하 여 apd의 다음 필드에 값을 할당 합니다.  
  
    -   Valuetype이 datetime 또는 interval 하위 형식의 간결한 식별자 중 하나인 경우에는 SQL_DESC_TYPE를 *valuetype*의 값으로 설정 합니다. 단, *valuetype* 이 datetime 또는 interval 하위 형식의 간결한 식별자 중 하나인 경우 SQL_DESC_TYPE를 각각 SQL_DATETIME 또는 SQL_INTERVAL로 설정 하 고 SQL_DESC_CONCISE_TYPE를 간결한 식별자로 설정 하 고 SQL_DESC_DATETIME_INTERVAL_CODE를 해당 날짜/시간 또는 간격 하위 코드 SQL_DESC_CONCISE_TYPE 설정 한다는 점만 다릅니다.  
  
    -   SQL_DESC_OCTET_LENGTH 필드를 *Bufferlength*의 값으로 설정 합니다.  
  
    -   SQL_DESC_DATA_PTR 필드를 *Parametervalue*값으로 설정 합니다.  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 필드를 *StrLen_or_Ind*값으로 설정 합니다.  
  
    -   SQL_DESC_INDICATOR_PTR 필드도 *StrLen_or_Ind*값으로 설정 합니다.  
  
     *StrLen_or_Ind* 매개 변수는 매개 변수 값에 대 한 표시기 정보와 길이를 모두 지정 합니다.  
  
4.  [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) 를 호출 하 여 IPD 핸들을 가져옵니다.  
  
5.  [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 를 호출 하 여 IPD의 SQL_DESC_COUNT 필드를 가져오고 *columnnumber* 인수의 값이 SQL_DESC_COUNT 값을 초과 하는 경우 **SQLSetDescField** 를 호출 하 여 SQL_DESC_COUNT 값을 *columnnumber*로 늘립니다.  
  
6.  [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 을 여러 번 호출 하 여 IPD의 다음 필드에 값을 할당 합니다.  
  
    -   는 SQL_DESC_CONCISE_TYPE SQL_DESC_TYPE를 *ParameterType*값으로 설정 합니다. 단, *ParameterType* 가 datetime 또는 interval 하위 형식의 간결한 식별자 중 하나인 경우에는 각각 SQL_DATETIME 또는 SQL_INTERVAL로 설정 하 고 SQL_DESC_CONCISE_TYPE를 간결한 식별자로 설정 하 고 SQL_DESC_DATETIME_INTERVAL_CODE를 해당 날짜/시간 또는 간격 SQL_DESC_TYPE 하위 코드에 설정 합니다.  
  
    -   *ParameterType*에 적절 한 SQL_DESC_LENGTH, SQL_DESC_PRECISION 및 SQL_DESC_DATETIME_INTERVAL_PRECISION를 하나 이상 설정 합니다.  
  
    -   SQL_DESC_SCALE를 *DecimalDigits*값으로 설정 합니다.  
  
 **SQLBindParameter** 에 대 한 호출이 실패 하면 apd에 설정 된 설명자 필드의 내용이 정의 되지 않고 apd의 SQL_DESC_COUNT 필드가 변경 되지 않습니다. 또한 IPD의 적절 한 레코드에 대 한 SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_TYPE 필드가 정의 되지 않으며 IPD의 SQL_DESC_COUNT 필드가 변경 되지 않습니다.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>SQLSetParam에서 호출 변환

 Odbc 1.0 응용 프로그램이 ODBC 3에서 **SQLSetParam** 를 호출 하는 경우 *x* DRIVER, ODBC 3. *x* 드라이버 관리자는 다음 표와 같이 호출을 매핑합니다.  
  
|ODBC 1.0 응용 프로그램에서 호출|ODBC 3을 호출 합니다. *x* 드라이버|  
|----------------------------------|-------------------------------|  
|SQLSetParam (StatementHandle, ParameterNumber, ValueType, ParameterType, LengthPrecision, Parameternumber, Parametervalueeptr, StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, *Columnsize*, *DecimalDigits*, parametervalueeptr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>코드 예  
 다음 예에서는 응용 프로그램이 ORDERS 테이블에 데이터를 삽입 하는 SQL 문을 준비 합니다. 문의 각 매개 변수에 대해 응용 프로그램은 **SQLBindParameter** 를 호출 하 여 ODBC C 데이터 형식 및 매개 변수의 SQL 데이터 형식을 지정 하 고 버퍼를 각 매개 변수에 바인딩합니다. 응용 프로그램은 각 데이터 행에 대해 데이터 값을 각 매개 변수에 할당 하 고 **Sqlexecute** 를 호출 하 여 문을 실행 합니다.  
  
 다음 샘플에서는 northwind 데이터베이스와 연결 된 Northwind 라는 컴퓨터에 ODBC 데이터 원본이 있다고 가정 합니다.  
  
 더 많은 코드 예제는 [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [sqlprocedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md), [Sqlputdata 함수](../../../odbc/reference/syntax/sqlputdata-function.md)및 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조 하세요.  
  
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

 다음 예에서는 응용 프로그램에서 명명 된 매개 변수를 사용 하 여 SQL Server 저장 프로시저를 실행 합니다.  
  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|문의 매개 변수에 대 한 정보 반환|[SQLDescribeParam 함수(SQLDescribeParam Function)](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|문에서 매개 변수 버퍼 해제|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|문 매개 변수 수 반환|[SQLNumParams 함수](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|다음 매개 변수를 반환 하 여 데이터 보내기|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|여러 매개 변수 값 지정|[SQLParamOptions 함수](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>참고 항목

 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
