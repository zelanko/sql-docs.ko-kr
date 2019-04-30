---
title: SQLSetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31493eb8c685fbb31fa21691794740eb2b61219c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188690"
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 혼합(키 집합/동적) 커서 모델을 지원하지 않습니다. SQL_ATTR_KEYSET_SIZE를 사용하여 키 집합 크기를 0이 아닌 값으로 설정하려고 하면 오류가 발생합니다.  
  
 반환 된 행 수를 선언 하는 모든 문에서 SQL_ATTR_ROW_ARRAY_SIZE를 설정 하는 응용 프로그램을 **SQLFetch** 하거나 [SQLFetchScroll](sqlfetchscroll.md) 함수 호출 합니다. 드라이버는 서버 커서를 지정하는 문에서 커서의 인출 요청을 충족하기 위해 SQL_ATTR_ROW_ARRAY_SIZE를 사용하여 서버가 생성하는 행 블록의 크기를 결정합니다. 트랜잭션 격리 수준이 커밋된 트랜잭션의 반복 읽기를 보장하는 데 충분하다면 행 멤버 자격 및 정렬이 동적 커서의 블록 크기 내에서 고정됩니다. 이 값으로 지정된 블록 밖에서는 커서가 완전히 동적입니다. 서버 커서 블록 크기는 완전히 동적이며 인출 처리 중 임의 시점에 변경될 수 있습니다.  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>SQLSetStmtAttr 및 테이블 반환 매개 변수  
 SQLSetStmtAttr은 SQL_SOPT_SS_PARAM_FOCUS를 테이블 반환 매개 변수 열의 설명자 필드에 액세스 하기 전에 응용 프로그램 매개 변수 설명자 (APD) 설정에 사용할 수 있습니다.  
  
 즉 하지 테이블 반환 매개 변수, SQLSetStmtAttr 반환 SQL_ERROR 진단 레코드가 만들어집니다 sqlstate 매개 변수의 서 수에 SQL_SOPT_SS_PARAM_FOCUS를 설정 하려고 시도 하는 경우 = HY024 및 "잘못 된 특성 값이"입니다. SQL_SOPT_SS_PARAM_FOCUS는 SQL_ERROR가 반환될 때 변경되지 않습니다.  
  
 SQL_SOPT_SS_PARAM_FOCUS를 0으로 설정하면 매개 변수의 설명자 레코드에 대한 액세스가 복원됩니다.  
  
 SQLSetStmtAttr는 SQL_SOPT_SS_NAME_SCOPE를 설정 하려면 데도 사용할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 SQL_SOPT_SS_NAME_SCOPE 섹션을 참조하십시오.  
  
 자세한 내용은 [Prepared 문 테이블 반환 매개 변수 메타 데이터](../native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)입니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>스파스 열에 대한 SQLSetStmtAttr 지원  
 SQLSetStmtAttr은 SQL_SOPT_SS_NAME_SCOPE를 설정 하려면 사용할 수 있습니다. 자세한 내용은이 항목의 뒷부분에 나오는 SQL_SOPT_SS_NAME_SCOPE 섹션을 참조 하세요. 스파스 열에 대 한 자세한 내용은 참조 하십시오 [Sparse Columns Support &#40;ODBC&#41;](../native-client/odbc/sparse-columns-support-odbc.md)합니다.  
  
## <a name="statement-attributes"></a>문 특성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 다음과 같은 드라이버별 문 특성도 지원합니다.  
  
### <a name="sqlsoptsscursoroptions"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 SQL_SOPT_SS_CURSOR 특성은 드라이버가 커서에 드라이버별 성능 옵션을 사용할지 여부를 지정합니다. [SQLGetData](sqlgetdata.md) 이러한 옵션에 설정 된 경우 허용 되지 않습니다. 기본 설정은 SQL_CO_OFF입니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*ValuePtr* 값|Description|  
|----------------------|-----------------|  
|SQL_CO_OFF|기본. 빠른 정방향 전용, 읽기 전용 커서 및 자동 인출 사용 하지 않도록 설정, 사용 하도록 설정 **SQLGetData** 읽기 전용, 정방향 전용 커서에 있습니다. SQL_SOPT_SS_CURSOR_OPTIONS가 SQL_CO_OFF로 설정되면 커서 유형이 변경되지 않습니다. 즉, 빠른 정방향 전용 커서는 빠른 정방향 전용 커서로 유지됩니다. 커서 유형을 변경 하려면 응용 프로그램이 이제 설정 해야 사용 하 여 다른 커서 유형을 `SQLSetStmtAttr`/SQL_ATTR_CURSOR_TYPE 합니다.|  
|SQL_CO_FFO|빠른 정방향 전용, 읽기 전용 커서를 사용 하지 않도록 설정 수 있도록 **SQLGetData** 읽기 전용, 정방향 전용 커서에 있습니다.|  
|SQL_CO_AF|임의의 커서 유형에 대해 자동 인출 옵션을 설정합니다. 문 핸들에 대해이 옵션을 설정 하면 **SQLExecute** 하거나 **SQLExecDirect** 암시적 생성 **SQLFetchScroll** (SQL_FIRST). 커서가 열리고 서버에 대한 단일 왕복에서 행의 첫 번째 일괄 처리가 반환됩니다.|  
|SQL_CO_FFO_AF|빠른 정방향 전용 커서에 대해 자동 인출 옵션을 설정합니다. 이는 SQL_CO_AF 및 SQL_CO_FFO를 모두 지정한 것과 같습니다.|  
  
 이러한 옵션이 설정된 경우 서버는 마지막 행이 인출되면 자동으로 커서를 닫습니다. 응용 프로그램 호출 해야 합니다 [SQLFreeStmt](sqlfreestmt.md) (SQL_CLOSE) 또는 [SQLCloseCursor](sqlclosecursor.md), 하지만 드라이버는 서버에 닫기 알림을 보낼 필요가 없습니다.  
  
 Select 목록에 포함 하는 경우는 **텍스트**를 **ntext**, 또는 **이미지** 열에서 빠른 정방향 전용 커서는 동적 커서로 변환 됩니다 및 **SQLGetData** 허용 됩니다.  
  
### <a name="sqlsoptssdeferprepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 SQL_SOPT_SS_DEFER_PREPARE 특성 문이 될 때까지 지연 즉시 준비 여부를 결정 **SQLExecute**하십시오 [SQLDescribeCol](sqldescribecol.md) 또는 [SQLDescribeParam](sqldescribeparam.md) 실행 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 및 이전 버전에서는 이 속성이 무시됩니다(준비 지연이 지원되지 않음). *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*ValuePtr* 값|Description|  
|----------------------|-----------------|  
|SQL_DP_ON|기본. 호출한 후 [SQLPrepare 함수](https://go.microsoft.com/fwlink/?LinkId=59360)를 때까지 문 준비가 지연 됩니다 **SQLExecute** 가 호출 되거나 메타 속성 작업 (**SQLDescribeCol** 또는**SQLDescribeParam**) 실행 됩니다.|  
|SQL_DP_OFF|문을 준비할 즉시 **SQLPrepare** 실행 됩니다.|  
  
### <a name="sqlsoptssregionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 SQL_SOPT_SS_REGIONALIZE 특성은 명령 수준에서 데이터 변환을 결정하는 데 사용됩니다. 이 특성은 드라이버가 날짜, 시간 및 통화 값을 문자열로 변환할 때 클라이언트 로캘 설정을 준수하도록 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 데이터 형식에서 문자열로의 변환만 해당됩니다.  
  
 *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*ValuePtr* 값|Description|  
|----------------------|-----------------|  
|SQL_RE_OFF|기본. 드라이버가 날짜, 시간 및 통화 데이터를 문자열 데이터로 변환할 때 클라이언트 로캘 설정을 사용하지 않습니다.|  
|SQL_RE_ON|드라이버가 날짜, 시간 및 통화 데이터를 문자열 데이터로 변환할 때 클라이언트 로캘 설정을 사용합니다.|  
  
 국가별 변환 설정이 통화, 숫자, 날짜 및 시간 데이터 형식에 적용됩니다. 변환 설정은 통화, 숫자, 날짜 또는 시간 값을 문자열로 변환한 경우 출력 변환에만 적용할 수 있습니다.  
  
> [!NOTE]  
>  문 옵션 SQL_SOPT_SS_REGIONALIZE가 사용되면 드라이버는 현재 사용자의 로캘 레지스트리 설정을 사용합니다. 드라이버 응용 프로그램 설정에서 예를 들어, 호출 하는 경우 현재 스레드의 로캘을 인식 하지 않습니다 **SetThreadLocale**합니다.  
  
 데이터 원본의 국가별 동작을 변경하면 응용 프로그램에서 오류가 발생할 수 있습니다. 날짜 문자열을 구문 분석하며 날짜 문자열이 ODBC에 정의된 대로 표시될 것으로 예상하는 응용 프로그램에서 이 값을 변경하면 부정적인 영향을 줄 수 있습니다.  
  
### <a name="sqlsoptsstextptrlogging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 SQL_SOPT_SS_TEXTPTR_LOGGING 특성은 포함 된 열에 대 한 작업 로깅을 설정/해제 **텍스트** 하거나 **이미지** 데이터입니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*ValuePtr* 값|Description|  
|----------------------|-----------------|  
|SQL_TL_OFF|수행 된 작업의 로깅을 사용 하지 않도록 설정 **텍스트** 하 고 **이미지** 데이터입니다.|  
|SQL_TL_ON|기본. 수행 된 작업의 로깅을 사용 하도록 설정 **텍스트** 하 고 **이미지** 데이터입니다.|  
  
### <a name="sqlsoptsshiddencolumns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 SQL_SOPT_SS_HIDDEN_COLUMNS 특성은 결과 집합에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT FOR BROWSE 문의 숨겨진 열을 노출합니다. 드라이버는 기본적으로 이러한 열을 노출하지 않습니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*ValuePtr* 값|Description|  
|----------------------|-----------------|  
|SQL_HC_OFF|기본. 결과 집합에서 FOR BROWSE 열을 숨깁니다.|  
|SQL_HC_ON|FOR BROWSE 열을 공개합니다.|  
  
### <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 특성은 쿼리 알림 요청에 대한 메시지 텍스트를 반환합니다.  
  
### <a name="sqlsoptssquerynotificationoptions"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS 특성은 쿼리 알림 요청에 사용되는 옵션을 지정합니다. 이러한 옵션은 아래에 지정된 것처럼 `name=value` 구문이 포함된 문자열로 지정됩니다. 응용 프로그램은 서비스를 만들고 큐에서 알림을 읽어야 합니다.  
  
 쿼리 알림 옵션 문자열의 구문은 다음과 같습니다.  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sqlsoptssquerynotificationtimeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT 특성은 쿼리 알림을 활성 상태로 유지할 초를 지정합니다. 기본값은 432000초(5일)입니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
### <a name="sqlsoptssparamfocus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 SQL_SOPT_SS_PARAM_FOCUS 특성은 후속 SQLBindParameter, SQLGetDescField, SQLSetDescField SQLGetDescRec, 포커스를 지정 하 고 SQLSetDescRec 호출 합니다.  
  
 SQL_SOPT_SS_PARAM_FOCUS의 형식은 SQLULEN입니다.  
  
 기본값은 0이며 이는 이러한 호출이 SQL 문의 매개 변수 표식에 해당하는 매개 변수의 주소를 지정한다는 의미입니다. 테이블 반환 매개 변수의 매개 변수 번호로 설정하면 이러한 호출이 해당 테이블 반환 매개 변수 열의 주소를 지정합니다. 테이블 반환 매개 변수의 매개 변수 번호가 아닌 값으로 설정 하면 이러한 호출이 오류 IM020를 반환 합니다. "매개 변수 포커스가 테이블 반환 매개 변수는 참조 하지 않습니다".  
  
### <a name="sqlsoptssnamescope"></a>SQL_SOPT_SS_NAME_SCOPE  
 SQL_SOPT_SS_NAME_SCOPE 특성은 후속 카탈로그 함수 호출의 이름 범위를 지정합니다. SQLColumns 반환한 결과 집합은 SQL_SOPT_SS_NAME_SCOPE의 설정에 따라 달라 집니다.  
  
 SQL_SOPT_SS_NAME_SCOPE의 형식은 SQLULEN입니다.  
  
|*ValuePtr* 값|Description|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|기본.<br /><br /> 테이블 반환 매개 변수를 사용할 때 실제 테이블의 메타데이터가 반환되도록 지정합니다.<br /><br /> SQLColumns 스파스의 멤버가 아닌 열만 반환 됩니다 스파스 열 기능을 사용 하는 경우 `column_set`합니다.|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|응용 프로그램이 실제 테이블이 아니라 테이블 형식의 메타데이터를 요구한다는 것을 나타냅니다. 카탈로그 함수가 테이블 형식의 메타데이터를 반환해야 합니다. 그런 다음 응용 프로그램으로 테이블 반환 매개 변수의 TYPE_NAME을 전달 합니다 *TableName* 매개 변수입니다.|  
|SQL_SS_NAME_SCOPE_EXTENDED|SQLColumns에 관계 없이 모든 열을 스파스 열 기능을 사용 하는 경우 반환 하도록 `column_set` 멤버 자격.|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|SQLColumns 스파스의 멤버인 열만 반환 스파스 열 기능을 사용 하는 경우 `column_set`합니다.|  
|SQL_SS_NAME_SCOPE_DEFAULT|SQL_SS_NAME_SCOPE_TABLE과 같습니다.|  
  
 SS_TYPE_CATALOG_NAME 및 ss_type_schema_name은 사용 되는 *CatalogName* 하 고 *SchemaName* 매개 변수 각각 카탈로그 및 테이블 반환 매개 변수에 대 한 스키마를 식별 하 합니다. 응용 프로그램이 테이블 반환 매개 변수의 메타데이터 검색을 마치면 SQL_SOPT_SS_NAME_SCOPE가 기본값인 SQL_SS_NAME_SCOPE_TABLE로 다시 설정됩니다.  
  
 SQL_SOPT_SS_NAME_SCOPE가 SQL_SS_NAME_SCOPE_TABLE로 설정되면 연결된 서버에 대한 쿼리가 실패합니다. 서버 구성 요소를 포함 하는 카탈로그를 사용 하 여 SQLPrimaryKeys SQLColumns를 호출 하지 못합니다.  
  
 SQL_SOPT_SS_NAME_SCOPE를 잘못된 값으로 설정하려고 하면 SQL_ERROR가 반환되고 SQLSTATE HY024 및 "잘못된 특성 값입니다" 메시지가 표시되며 진단 레코드가 생성됩니다.  
  
 SQL_SOPT_SS_NAME_SCOPE의 이외의 값이 호출 됩니다 SQLTables, SQLColumns, 또는 SQLPrimaryKeys 카탈로그 함수가 다른 경우 SQL_SS_NAME_SCOPE_TABLE 면 SQL_ERROR가 반환 됩니다. SQLSTATE HY010 및 "함수 시퀀스 오류입니다(SQL_SOPT_SS_NAME_SCOPE가 SQL_SS_NAME_SCOPE_TABLE로 설정되지 않았습니다)" 메시지가 표시되고 진단 레코드가 생성됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLGetStmtAttr 함수](https://go.microsoft.com/fwlink/?LinkId=59355)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
