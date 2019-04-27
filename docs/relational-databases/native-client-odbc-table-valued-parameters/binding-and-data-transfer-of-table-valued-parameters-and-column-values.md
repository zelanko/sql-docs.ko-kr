---
title: 바인딩 및 데이터 전송 테이블 반환 매개 변수 및 열 값 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f8b291344939bcbafa7f91080837d2302efb1d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62738559"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>테이블 반환 매개 변수 및 열 값에 대한 바인딩 및 데이터 전송
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  테이블 반환 매개 변수는 다른 매개 변수처럼 서버에 전달되기 전에 바인딩되어야 합니다. 응용 프로그램에서는 테이블 반환 매개 변수는 다른 매개 변수를 바인딩합니다: SQLBindParameter 또는 SQLSetDescField SQLSetDescRec에 해당 하는 호출을 사용 하 여 합니다. 테이블 반환 매개 변수의 서버 데이터 형식은 SQL_SS_TABLE입니다. C 형식은 SQL_C_DEFAULT 또는 SQL_C_BINARY로 지정할 수 있습니다.  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 입력 테이블 반환 매개 변수만 지원됩니다. 따라서 DESC_PARAMETER_TYPE을 SQL_PARAM_INPUT 이외의 값으로 설정하면 SQLSTATE=HY105 및 "매개 변수 유형이 잘못되었습니다"라는 메시지가 포함된 SQL_ERROR가 반환됩니다.  
  
 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 특성을 사용하여 전체 테이블 반환 매개 변수 열에 기본값을 할당할 수 있습니다. 개별 테이블 반환 매개 변수 열 값을 단, 할당할 수 없습니다 기본값에는 SQL_DEFAULT_PARAM을 사용 하 여 *StrLen_or_IndPtr* SQLBindParameter와 합니다. 에 SQL_DEFAULT_PARAM을 사용 하 여 테이블 반환 매개 변수를 전체적으로 기본값으로 설정할 수 없습니다 *StrLen_or_IndPtr* SQLBindParameter와 합니다. 이러한 규칙을 따르지 SQLExecute 또는 SQLExecDirect SQL_ERROR를 반환 합니다. Sqlstate 진단 레코드가 생성 됩니다 07S01 및 메시지 = "매개 변수에 대 한 기본 매개 변수 사용이 잘못 되었습니다 \<p >" 여기서 \<p > 쿼리 문에서 TVP의 서 수입니다.  
  
 테이블 반환 매개 변수를 바인딩한 후에는 응용 프로그램에서 각 테이블 반환 매개 변수 열을 바인딩해야 합니다. 이렇게 하려면 응용 프로그램 SQLSetStmtAttr 테이블 반환 매개 변수의 서 수에 SQL_SOPT_SS_PARAM_FOCUS를 설정 하려면 먼저 호출 합니다. 그런 다음 응용 프로그램이 다음 루틴을 호출 하 여 테이블 반환 매개 변수의 열에 바인딩합니다. SQLBindParameter SQLSetDescRec, 하며 SQLSetDescField 합니다. SQL_SOPT_SS_PARAM_FOCUS로 설정 0 복원 SQLBindParameter와 SQLSetDescRec, SQLSetDescField의 일반 효과가 일반적인 최상위 매개 변수에 대해 작동 합니다.
 
 참고: unixODBC 2.3.1을 2.3.4, SQL_CA_SS_TYPE_NAME 설명자 필드를 사용 하 여 SQLSetDescField 통해 TVP 이름을 설정할 때 사용 하 여 Linux 및 Mac ODBC 드라이버에 대 한 unixODBC 변환 하지 않습니다 자동으로 ANSI와 유니코드 간의 정확한에 따라 문자열 함수 호출 (SQLSetDescFieldA / SQLSetDescFieldW). 항상 사용 하도록 SQLBindParameter 또는 SQLSetDescFieldW 유니코드 (utf-16) 문자열을 사용 하 여 TVP 이름을 설정 하는 것이 반드시 합니다.
  
 테이블 반환 매개 변수 자체에 대해 실제로 보내거나 받는 데이터는 없지만 매개 변수의 각 구성 열에 대해서는 데이터를 보내고 받습니다. 테이블 반환 매개 변수는 의사 열 이므로 SQLBindParameter 매개 변수는 다음과 같이 다른 데이터 형식에는 다른 특성을 참조 하는 데 사용 됩니다.  
  
|매개 변수|열이 포함 되지 않은 테이블 반환 매개 변수 형식에 대 한 관련된 특성|테이블 반환 매개 변수에 대한 관련 특성|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|IPD의 SQL_DESC_PARAMETER_TYPE<br /><br /> 테이블 반환 매개 변수 열의 경우 이 값은 테이블 반환 매개 변수 자체에 대한 설정과 같습니다.|IPD의 SQL_DESC_PARAMETER_TYPE<br /><br /> SQL_PARAM_INPUT이여야 합니다.|  
|*ValueType*|APD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE|APD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE<br /><br /> SQL_C_DEFAULT 또는 SQL_C_BINARY여야 합니다.|  
|*ParameterType*|IPD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE|IPD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE<br /><br /> SQL_SS_TABLE이여야 합니다.|  
|*ColumnSize*|IPD의 SQL_DESC_LENGTH 또는 SQL_DESC_PRECISION<br /><br /> 이 값에 따라 달라 집니다 *ParameterType*합니다.|SQL_DESC_ARRAY_SIZE<br /><br /> 매개 변수 포커스를 테이블 반환 매개 변수로 설정할 때 SQL_ATTR_PARAM_SET_SIZE를 사용하여 설정할 수도 있습니다.<br /><br /> 테이블 반환 매개 변수의 경우 이 값은 테이블 반환 매개 변수 열 버퍼의 행 수입니다.|  
|*DecimalDigits*|IPD의 SQL_DESC_PRECISION 또는 SQL_DESC_SCALE|사용되지 않습니다. 0이어야 합니다.<br /><br /> 이 매개 변수는 없습니다 0, SQLBindParameter은 sqlstate 반환 SQL_ERROR와 진단 레코드가 생성 될 경우 = HY104 및 "잘못 된 정밀도 또는 배율" 메시지입니다.|  
|*ParameterValuePtr*|APD의 SQL_DESC_DATA_PTR|SQL_CA_SS_TYPE_NAME<br /><br /> 저장 프로시저 호출의 경우 선택 사항이며 필요하지 않은 경우 NULL을 지정할 수 있습니다. 프로시저 호출이 아닌 SQL 문에는 지정해야 합니다.<br /><br /> 또한 이 매개 변수는 변수 행 바인딩을 사용할 때 응용 프로그램에서 이 테이블 반환 매개 변수를 식별하는 데 사용할 수 있는 고유 값으로도 사용됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "가변 테이블 반환 매개 변수 행 바인딩" 섹션을 참조하십시오.<br /><br /> 테이블 반환 매개 변수 형식 이름을 지정 하는 SQLBindParameter 대 한 호출을 하는 경우 ANSI 응용 프로그램으로 작성 된 응용 프로그램에도 유니코드 값으로 지정 해야 합니다. 매개 변수에 사용 된 값 *StrLen_or_IndPtr* SQL_NTS 또는 문자열 길이의 sizeof(WCHAR) 곱한 이름 이어야 합니다.|  
|*BufferLength*|APD의 SQL_DESC_OCTET_LENGTH|테이블 반환 매개 변수 형식 이름의 길이(바이트)입니다.<br /><br /> 형식 이름이 null로 끝나는 경우 SQL_NTS이고 테이블 반환 매개 변수 형식 이름이 필요하지 않은 경우 0입니다.|  
|*StrLen_or_IndPtr*|APD의 SQL_DESC_OCTET_LENGTH_PTR|APD의 SQL_DESC_OCTET_LENGTH_PTR<br /><br /> 테이블 반환 매개 변수의 경우 데이터 길이가 아닌 행 수입니다.|  
  
 테이블 반환 매개 변수에 대해서는 고정 행 바인딩과 가변 행 바인딩의 두 가지 데이터 전송 모드가 지원됩니다.  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>고정 테이블 반환 매개 변수 행 바인딩  
 고정 행 바인딩에서는 응용 프로그램이 가능한 모든 입력 열 값을 수용할 수 있는 크기의 버퍼 또는 버퍼 배열을 할당합니다. 이 응용 프로그램에서는 다음 작업을 수행합니다.  
  
1.  SQLBindParameter, SQLSetDescRec, 또는 SQLSetDescField 호출을 사용 하 여 모든 매개 변수를 바인딩합니다.  
  
    1.  SQL_DESC_ARRAY_SIZE를 각 테이블 반환 매개 변수에 대해 전송될 수 있는 최대 행 수로 설정합니다. 이렇게 하려면 SQLBindParameter 호출에서 합니다.  
  
2.  각 테이블 반환 매개 변수의 서 수에 SQL_SOPT_SS_PARAM_FOCUS를 설정 하려면 SQLSetStmtAttr를 호출 합니다.  
  
    1.  각 테이블 반환 매개 변수에 대 한 SQLBindParameter, SQLSetDescRec, 또는 SQLSetDescField 호출을 사용 하 여 테이블 반환 매개 변수 열에 바인딩합니다.  
  
    2.  기본값이 있는 각 테이블 반환 매개 변수 열에 대 한 SQLSetDescField SQL_CA_SS_COL_HAS_DEFAULT_VALUE를 1로 설정 하 여 호출 합니다.  
  
3.  SQL_SOPT_SS_PARAM_FOCUS를 0으로 설정 하는 SQLSetStmtAttr를 호출 합니다. SQLExecute 하기 전에 수행 해야 하거나 SQLExecDirect 라고 합니다. 그렇지 않으면 SQL_ERROR가 반환되고 SQLSTATE=HY024 및 "특성 값 SQL_SOPT_SS_PARAM_FOCUS가 잘못되었습니다. 실행 시 0이어야 합니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.  
  
4.  집합 *StrLen_or_IndPtr* 또는 SQL_DESC_OCTET_LENGTH_PTR 없습니다 행 또는 행 개수를 사용 하 여 테이블 반환 매개 변수에 대해서는 sql_default_param으로 때 SQLExecute SQLExecDirect의 다음 호출에서 전송 되는 테이블 반환 매개 변수 행이 있습니다. *StrLen_or_IndPtr* 또는 SQL_DESC_OCTET_LENGTH_PTR에 설정할 수 없습니다를 sql_null_data로 테이블 반환 매개 변수에 대 한 테이블 반환 매개 변수는 null을 허용 (없지만 테이블 반환 매개 변수 구성 열의 nullable 일 수 있음). 잘못 된 값으로 설정 됩니다 SQLExecute SQLExecDirect SQL_ERROR를 반환 하 고 진단 레코드가 생성 됩니다 = HY090 및 메시지 "매개 변수에 대 한 잘못 된 문자열 또는 버퍼 길이 \<p >", 여기서 p는 매개 변수 번호입니다.  
  
5.  SQLExecute 또는 SQLExecDirect를 호출합니다.  
  
 입력 경우 부분에 테이블 반환 매개 변수 열 값을 전달할 수 있습니다 *StrLen_or_IndPtr* SQL_LEN_DATA_AT_EXEC로 설정 됩니다 (*길이*) 또는 SQL_DATA_AT_EXEC 열에 대 한 합니다. 이는 매개 변수 배열을 사용할 때 값을 개별적으로 전달하는 것과 유사합니다. 드라이버;에 대 한 데이터를 요청 하 고 대로 SQLParamData은 모든 실행 시 데이터 매개 변수를 사용 하 여 배열의 행을 표시 하지 않습니다. 응용 프로그램은이 주의 해야 합니다. 응용 프로그램은 드라이버에서 값을 요청하는 순서에 대해 어떠한 가정도 할 수 없습니다.  
  
## <a name="variable-table-valued-parameter-row-binding"></a>가변 테이블 반환 매개 변수 행 바인딩  
 가변 행 바인딩에서는 행이 실행 시 일괄 처리로 전송되며 요청 시 응용 프로그램에서 행을 드라이버에 전달합니다. 이는 개별 매개 변수 값의 실행 시 데이터와 유사합니다. 가변 행 바인딩에서 응용 프로그램은 다음을 수행합니다.  
  
1.  이전 섹션 "고정 테이블 반환 매개 변수 행 바인딩"의 1~3단계에서 설명한 대로 매개 변수 및 테이블 반환 매개 변수 열을 바인딩합니다.  
  
2.  집합 *StrLen_or_IndPtr* 또는 SQL_DESC_OCTET_LENGTH_PTR SQL_DATA_AT_EXEC로 실행 시 전달할 수 있는 모든 테이블 반환 매개 변수에 대 한 합니다. 이 중 하나라도 설정하지 않으면 매개 변수가 이전 섹션에 설명된 대로 처리됩니다.  
  
3.  SQLExecute 또는 SQLExecDirect를 호출합니다. 이렇게 하면 실행 시 데이터 매개 변수로 처리할 SQL_PARAM_INPUT 또는 SQL_PARAM_INPUT_OUTPUT 매개 변수가 있는 경우 SQL_NEED_DATA가 반환됩니다. 이 경우 응용 프로그램을 다음을 수행합니다.  
  
    -   Calls SQLParamData. 이 반환 합니다 *ParameterValuePtr* SQL_NEED_DATA의 반환 코드 및 실행 시 데이터 매개 변수 값. 드라이버에 모든 매개 변수 데이터 전달 되었는지, SQLParamData SQL_SUCCESS, SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR를 반환 합니다. 실행 시 데이터 매개 변수에 대 한 *ParameterValuePtr*, 동일한 설명자 필드 SQL_DESC_DATA_PTR과 값은 필수 매개 변수를 고유 하 게 식별 하는 토큰으로 간주 될 수 있습니다. 이 "토큰"은 바인딩 시 응용 프로그램에서 드라이버로 전달된 다음 실행 시 응용 프로그램으로 다시 전달됩니다.  
  
4.  Null 테이블 반환 매개 변수의 테이블 반환 매개 변수 행 데이터를 보내려면 테이블 반환 매개 변수 행이 없는 경우 응용 프로그램이 호출 된 SQLPutData *StrLen_or_Ind* SQL_DEFAULT_PARAM으로 설정 합니다.  
  
     NULL이 아닌 TVP의 경우 응용 프로그램은 다음을 수행합니다.  
  
    -   집합 *Str_Len_or_Ind* 적절 한 값으로 모든 테이블 반환 매개 변수 열에 대해 실행 시 데이터 매개 변수로 지정할 필요가 있는 테이블 반환 매개 변수 열에 대 한 데이터 버퍼를 채웁니다. 일반 매개 변수를 드라이버에 개별적으로 전달할 수 있는 방법과 유사하게 테이블 반환 매개 변수 열에 실행 시 데이터를 사용할 수 있습니다.  
  
    -   사용 하 여 SQLPutData 호출 *Str_Len_or_Ind* 서버에 전송할 행 수로 설정 합니다. 값이 0에서 SQL_DESC_ARRAY_SIZE 또는 SQL_DEFAULT_PARAM 사이의 범위를 벗어나면 오류가 발생하고 "문자열 또는 버퍼 길이가 잘못되었습니다"라는 메시지와 함께 SQLSTATE=HY090이 반환됩니다. 0은 이 목록의 두 번째 글머리 항목에 설명된 대로 모든 행을 보냈으며 테이블 반환 매개 변수의 데이터가 더 이상 없음을 나타냅니다. SQL_DEFAULT_PARAM은 이 목록의 첫 번째 글머리 항목에 설명된 대로 드라이버에서 테이블 반환 매개 변수의 데이터를 처음으로 요청할 때에만 사용할 수 있습니다.  
  
5.  모든 행을 보낸 SQLPutData를 사용 하 여 테이블 반환 매개 변수에 대 한 호출을 *Str_Len_or_Ind* 값 0, 다음 위에 3a 단계로 진행 됩니다.  
  
6.  SQLParamData를 다시 호출합니다. 테이블 반환 매개 변수 열 사이의 모든 실행 시 데이터 매개 변수가 있는 경우 이러한 것으로 식별 값 *ValuePtrPtr* SQLParamData에서 반환 합니다. 모든 열 값을 사용할 수 있는 SQLParamData가 다시 반환 합니다 *ParameterValuePtr* 테이블 반환 매개 변수 및 응용 프로그램에 대 한 값이 다시 시작 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
