---
title: 테이블 값 매개 변수의 데이터 전송
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b7eecfdac3d42b7a3d8d66ffe1f8ac68652230f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304504"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>테이블 반환 매개 변수 및 열 값에 대한 바인딩 및 데이터 전송
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  테이블 반환 매개 변수는 다른 매개 변수처럼 서버에 전달되기 전에 바인딩되어야 합니다. 응용 프로그램은 SQLBindParameter 또는 SQLSetDescField 또는 SQLSetDescRec에 대한 동등한 호출을 사용하여 다른 매개 변수를 바인딩하는 것과 동일한 방식으로 테이블 값 매개 변수를 바인딩합니다. 테이블 반환 매개 변수의 서버 데이터 형식은 SQL_SS_TABLE입니다. C 형식은 SQL_C_DEFAULT 또는 SQL_C_BINARY로 지정할 수 있습니다.  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 입력 테이블 반환 매개 변수만 지원됩니다. 따라서 DESC_PARAMETER_TYPE을 SQL_PARAM_INPUT 이외의 값으로 설정하면 SQLSTATE=HY105 및 "매개 변수 유형이 잘못되었습니다"라는 메시지가 포함된 SQL_ERROR가 반환됩니다.  
  
 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 특성을 사용하여 전체 테이블 반환 매개 변수 열에 기본값을 할당할 수 있습니다. 그러나 개별 테이블 값 매개 변수 열 값은 SQLBindParameter를 사용하여 *StrLen_or_IndPtr* SQL_DEFAULT_PARAM 사용하여 기본 값을 할당할 수 없습니다. SQLBindParameter를 사용하여 *StrLen_or_IndPtr* SQL_DEFAULT_PARAM 사용하여 테이블 값 매개 변수를 전체적으로 기본값으로 설정할 수 없습니다. 이러한 규칙을 따르지 않으면 SQLExecute 또는 SQLExecDirect가 SQL_ERROR 반환합니다. 진단 레코드는 SQLSTATE=07S01 및 "매개 변수 \<p> 기본 매개 변수의 \<잘못된 사용"이라는 메시지와 함께 생성되며, 여기서 p> 쿼리 문에서 TVP의 서수입니다.  
  
 테이블 반환 매개 변수를 바인딩한 후에는 애플리케이션에서 각 테이블 반환 매개 변수 열을 바인딩해야 합니다. 이렇게 하려면 응용 프로그램이 먼저 SQLSetStmtAttr을 호출하여 테이블 값 매개 변수의 서수로 SQL_SOPT_SS_PARAM_FOCUS 설정합니다. 그런 다음 응용 프로그램은 SQLBindParameter, SQLSetDescRec 및 SQLSetDescField라는 다음 루틴을 호출하여 테이블 값 매개 변수의 열을 바인딩합니다. SQL_SOPT_SS_PARAM_FOCUS 0으로 설정하면 일반 최상위 매개 변수에서 작동하는 SQLBindParameter, SQLSetDescRec 및 SQLSetDescField의 일반적인 효과가 복원됩니다.
 
 참고 : unixODBC 2.3.1 ~ 2.3.4와 리눅스 및 맥 ODBC 드라이버의 경우, SQL_CA_SS_TYPE_NAME 설명자 필드와 SQLSetDescField를 통해 TVP 이름을 설정할 때, unixODBC는 자동으로 라는 정확한 기능에 따라 ANSI와 유니코드 문자열 사이에 변환되지 않습니다 (SQLSetDescFieldA / SQLSetDesDescFieldW). 항상 SQLBindParameter 또는 SQLSetDescFieldW 유니코드 (UTF-16) 문자열을 사용 하 여 TVP 이름을 설정 하는 데 필요한.
  
 테이블 반환 매개 변수 자체에 대해 실제로 보내거나 받는 데이터는 없지만 매개 변수의 각 구성 열에 대해서는 데이터를 보내고 받습니다. 테이블 값 매개 변수는 의사 열이므로 SQLBindParameter에 대한 매개 변수는 다음과 같이 다른 데이터 형식과 다른 특성을 참조하는 데 사용됩니다.  
  
|매개 변수|열을 포함하여 테이블 값이 아닌 매개 변수 형식에 대한 관련 특성|테이블 반환 매개 변수에 대한 관련 특성|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|IPD의 SQL_DESC_PARAMETER_TYPE<br /><br /> 테이블 반환 매개 변수 열의 경우 이 값은 테이블 반환 매개 변수 자체에 대한 설정과 같습니다.|IPD의 SQL_DESC_PARAMETER_TYPE<br /><br /> SQL_PARAM_INPUT이여야 합니다.|  
|*Valuetype*|APD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE|APD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE<br /><br /> SQL_C_DEFAULT 또는 SQL_C_BINARY여야 합니다.|  
|*매개 변수 유형*|IPD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE|IPD의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE<br /><br /> SQL_SS_TABLE이여야 합니다.|  
|*ColumnSize*|IPD의 SQL_DESC_LENGTH 또는 SQL_DESC_PRECISION<br /><br /> 이는 *ParameterType*의 값에 따라 달라집니다.|SQL_DESC_ARRAY_SIZE<br /><br /> 매개 변수 포커스를 테이블 반환 매개 변수로 설정할 때 SQL_ATTR_PARAM_SET_SIZE를 사용하여 설정할 수도 있습니다.<br /><br /> 테이블 반환 매개 변수의 경우 이 값은 테이블 반환 매개 변수 열 버퍼의 행 수입니다.|  
|*DecimalDigits*|IPD의 SQL_DESC_PRECISION 또는 SQL_DESC_SCALE|사용되지 않습니다. 0이어야 합니다.<br /><br /> 이 매개 변수가 0이 아닌 경우 SQLBindParameterSQL_ERROR 반환 하고 SQLSTATE = HY104 및 메시지 "잘못 된 정밀도 또는 축척"으로 진단 레코드가 생성 됩니다.|  
|*매개 변수 값 Ptr*|APD의 SQL_DESC_DATA_PTR|SQL_CA_SS_TYPE_NAME<br /><br /> 저장 프로시저 호출의 경우 선택 사항이며 필요하지 않은 경우 NULL을 지정할 수 있습니다. 프로시저 호출이 아닌 SQL 문에는 지정해야 합니다.<br /><br /> 또한 이 매개 변수는 변수 행 바인딩을 사용할 때 애플리케이션에서 이 테이블 반환 매개 변수를 식별하는 데 사용할 수 있는 고유 값으로도 사용됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "가변 테이블 반환 매개 변수 행 바인딩" 섹션을 참조하십시오.<br /><br /> SQLBindParameter 호출에서 테이블 값 매개 변수 형식 이름을 지정하는 경우 ANSI 응용 프로그램으로 빌드된 응용 프로그램에서도 유니코드 값으로 지정해야 합니다. 매개 변수 *StrLen_or_IndPtr* 사용되는 값은 SQL_NTS 또는 이름의 문자열 길이에 sizeof(WCHAR)를 곱한 값이어야 합니다.|  
|*버퍼 길이*|APD의 SQL_DESC_OCTET_LENGTH|테이블 반환 매개 변수 형식 이름의 길이(바이트)입니다.<br /><br /> 형식 이름이 null로 끝나는 경우 SQL_NTS이고 테이블 반환 매개 변수 형식 이름이 필요하지 않은 경우 0입니다.|  
|*StrLen_or_IndPtr*|APD의 SQL_DESC_OCTET_LENGTH_PTR|APD의 SQL_DESC_OCTET_LENGTH_PTR<br /><br /> 테이블 반환 매개 변수의 경우 데이터 길이가 아닌 행 수입니다.|  
||||

 테이블 반환 매개 변수에 대해서는 고정 행 바인딩과 가변 행 바인딩의 두 가지 데이터 전송 모드가 지원됩니다.  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>고정 테이블 반환 매개 변수 행 바인딩  
 고정 행 바인딩에서는 애플리케이션이 가능한 모든 입력 열 값을 수용할 수 있는 크기의 버퍼 또는 버퍼 배열을 할당합니다. 이 애플리케이션에서는 다음 작업을 수행합니다.  
  
1.  SQLBindParameter, SQLSetDescRec 또는 SQLSetDescField 호출을 사용 하 여 모든 매개 변수를 바인딩합니다.  
  
    1.  SQL_DESC_ARRAY_SIZE를 각 테이블 반환 매개 변수에 대해 전송될 수 있는 최대 행 수로 설정합니다. 이 작업은 SQLBindParameter 호출에서 수행할 수 있습니다.  
  
2.  SQLSetStmtAttr을 호출하여 각 테이블 값 매개 변수의 서수에 SQL_SOPT_SS_PARAM_FOCUS 설정합니다.  
  
    1.  각 테이블 값 매개 변수에 대해 SQLBindParameter, SQLSetDescRec 또는 SQLSetDescField 호출을 사용하여 테이블 값 매개 변수 열을 바인딩합니다.  
  
    2.  기본값을 갖도록 하는 각 테이블 값 매개 변수 열에 대해 SQLSetDescField를 호출하여 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 1로 설정합니다.  
  
3.  SQLSetStmtAttr을 호출하여 SQL_SOPT_SS_PARAM_FOCUS 0으로 설정합니다. 이 작업은 SQLExecute 또는 SQLExecDirect가 호출되기 전에 수행해야 합니다. 그렇지 않으면 SQL_ERROR가 반환되고 SQLSTATE=HY024 및 "특성 값 SQL_SOPT_SS_PARAM_FOCUS가 잘못되었습니다. 실행 시 0이어야 합니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.  
  
4.  *StrLen_or_IndPtr* 또는 SQL_DESC_OCTET_LENGTH_PTR SQL_DEFAULT_PARAM 행이 없는 테이블 값 매개 변수에 대 한 SQL_DEFAULT_PARAM 또는 SQLExecute 또는 SQLExecDirect 테이블 값 매개 변수에 행이 있는 경우 다음 호출에서 전송할 행 수를 설정 합니다. *StrLen_or_IndPtr 테이블* 값 매개 변수는 null 수 없으므로 테이블 값 매개 변수에 대해 테이블 값 매개 변수에 대해 SQL_NULL_DATA 설정할 수 SQL_DESC_OCTET_LENGTH_PTR(테이블 값 매개 변수 구성 열은 null일 수 있음). 잘못된 값으로 설정된 경우 SQLExecute 또는 SQLExecDirect는 SQL_ERROR 반환하고 진단 레코드는 SQLSTATE=HY090 및 p가 매개 변수 \<번호인 "매개 변수 p> 대한 잘못된 문자열 또는 버퍼 길이"라는 메시지로 생성됩니다.  
  
5.  SQLExecute 또는 SQLExecDirect를 호출합니다.  
  
 StrLen_or_IndPtr*SQL_LEN_DATA_AT_EXEC(길이)* 또는 SQL_DATA_AT_EXEC 열로 설정된 *경우* 입력 테이블 값 매개 변수 열 값을 조각으로 전달할 수 있습니다. 이는 매개 변수 배열을 사용할 때 값을 개별적으로 전달하는 것과 유사합니다. 모든 실행 시 데이터 매개 변수와 마찬가지로 SQLParamData는 드라이버가 데이터를 요청하는 배열의 행을 나타내지 않습니다. 응용 프로그램이 처리해야합니다. 애플리케이션은 드라이버에서 값을 요청하는 순서에 대해 어떠한 가정도 할 수 없습니다.  
  
## <a name="variable-table-valued-parameter-row-binding"></a>가변 테이블 반환 매개 변수 행 바인딩  
 가변 행 바인딩에서는 행이 실행 시 일괄 처리로 전송되며 요청 시 애플리케이션에서 행을 드라이버에 전달합니다. 이는 개별 매개 변수 값의 실행 시 데이터와 유사합니다. 가변 행 바인딩에서 애플리케이션은 다음을 수행합니다.  
  
1.  이전 섹션 "고정 테이블 반환 매개 변수 행 바인딩"의 1~3단계에서 설명한 대로 매개 변수 및 테이블 반환 매개 변수 열을 바인딩합니다.  
  
2.  SQL_DATA_AT_EXEC 위해 실행 시 전달될 테이블 값 매개 변수에 대해 *StrLen_or_IndPtr* 또는 SQL_DESC_OCTET_LENGTH_PTR 설정합니다. 이 중 하나라도 설정하지 않으면 매개 변수가 이전 섹션에 설명된 대로 처리됩니다.  
  
3.  SQLExecute 또는 SQLExecDirect를 호출합니다. 이렇게 하면 실행 시 데이터 매개 변수로 처리할 SQL_PARAM_INPUT 또는 SQL_PARAM_INPUT_OUTPUT 매개 변수가 있는 경우 SQL_NEED_DATA가 반환됩니다. 이 경우 애플리케이션을 다음을 수행합니다.  
  
    -   SQLParamData를 호출합니다. 이렇게 하면 실행 시 데이터 매개 변수에 대한 *ParameterValuePtr* 값과 SQL_NEED_DATA 반환 코드가 반환됩니다. 모든 매개 변수 데이터가 드라이버에 전달되면 SQLParamData는 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR 반환합니다. 실행 시 데이터 매개 변수의 경우 설명자 필드 SQL_DESC_DATA_PTR 동일한 *ParameterValuePtr은*값이 필요한 매개 변수를 고유하게 식별하는 토큰으로 간주할 수 있습니다. 이 &quot;토큰&quot;은 바인딩 시 애플리케이션에서 드라이버로 전달된 다음 실행 시 애플리케이션으로 다시 전달됩니다.  
  
4.  null 테이블 값 매개 변수에 대 한 테이블 값 매개 변수 행 데이터를 보내려면 테이블 값 매개 변수행이 없는 경우 응용 프로그램은 SQL_DEFAULT_PARAM 설정 *StrLen_or_Ind* SQLPutData를 호출 합니다.  
  
     NULL이 아닌 TVP의 경우 애플리케이션은 다음을 수행합니다.  
  
    -   모든 테이블 값 매개 변수 열에 대한 *Str_Len_or_Ind* 적절한 값으로 설정하고 실행 시 데이터 매개 변수가 아닌 테이블 값 매개 변수 열에 대한 데이터 버퍼를 채웁니다. 일반 매개 변수를 드라이버에 개별적으로 전달할 수 있는 방법과 유사하게 테이블 반환 매개 변수 열에 실행 시 데이터를 사용할 수 있습니다.  
  
    -   서버로 전송할 행 수로 설정된 *Str_Len_or_Ind* 사용하여 SQLPutData를 호출합니다. 값이 0에서 SQL_DESC_ARRAY_SIZE 또는 SQL_DEFAULT_PARAM 사이의 범위를 벗어나면 오류가 발생하고 "문자열 또는 버퍼 길이가 잘못되었습니다"라는 메시지와 함께 SQLSTATE=HY090이 반환됩니다. 0은 이 목록의 두 번째 글머리 항목에 설명된 대로 모든 행을 보냈으며 테이블 반환 매개 변수의 데이터가 더 이상 없음을 나타냅니다. SQL_DEFAULT_PARAM은 이 목록의 첫 번째 글머리 항목에 설명된 대로 드라이버에서 테이블 반환 매개 변수의 데이터를 처음으로 요청할 때에만 사용할 수 있습니다.  
  
5.  모든 행이 전송되면 sqlPutData를 호출하여 *Str_Len_or_Ind* 값이 0인 테이블 값 매개 변수에 대해 호출한 다음 위의 3a 단계로 진행됩니다.  
  
6.  SQLParamData를 다시 호출합니다. 테이블 값 매개 변수 열 사이에 실행 시 데이터 매개 변수가 있는 경우 SQLParamData에서 반환하는 *ValuePtrPtr* 값으로 식별됩니다. 모든 열 값을 사용할 수 있는 경우 SQLParamData 테이블 값 매개 변수에 대 한 *ParameterValuePtr* 값을 다시 반환 하 고 응용 프로그램이 다시 시작 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 값 매개 변수](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
