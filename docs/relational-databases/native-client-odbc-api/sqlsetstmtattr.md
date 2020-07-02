---
title: SQLSetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6c18c4106c5fab5f6f1c75276db8c211f9873c8b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751834"
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 혼합(키 집합/동적) 커서 모델을 지원하지 않습니다. SQL_ATTR_KEYSET_SIZE를 사용하여 키 집합 크기를 0이 아닌 값으로 설정하려고 하면 오류가 발생합니다.  
  
 응용 프로그램은 모든 문에 SQL_ATTR_ROW_ARRAY_SIZE을 설정 하 여 **Sqlfetch** 또는 [sqlfetchscroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) 함수 호출에서 반환 되는 행 수를 선언 합니다. 드라이버는 서버 커서를 지정하는 문에서 커서의 인출 요청을 충족하기 위해 SQL_ATTR_ROW_ARRAY_SIZE를 사용하여 서버가 생성하는 행 블록의 크기를 결정합니다. 트랜잭션 격리 수준이 커밋된 트랜잭션의 반복 읽기를 보장하는 데 충분하다면 행 멤버 자격 및 정렬이 동적 커서의 블록 크기 내에서 고정됩니다. 이 값으로 지정된 블록 밖에서는 커서가 완전히 동적입니다. 서버 커서 블록 크기는 완전히 동적이며 인출 처리 중 임의 시점에 변경될 수 있습니다.  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>SQLSetStmtAttr 및 테이블 반환 매개 변수  
 SQLSetStmtAttr는 테이블 반환 매개 변수 열의 설명자 필드에 액세스 하기 전에 APD (응용 프로그램 매개 변수 설명자)에서 SQL_SOPT_SS_PARAM_FOCUS를 설정 하는 데 사용할 수 있습니다.  
  
 SQL_SOPT_SS_PARAM_FOCUS를 테이블 반환 매개 변수가 아닌 매개 변수의 서 수로 설정 하려고 하면 SQLSetStmtAttr가 SQL_ERROR를 반환 하 고 SQLSTATE = HY024 및 "잘못 된 특성 값입니다." 라는 메시지가 포함 된 진단 레코드가 생성 됩니다. SQL_SOPT_SS_PARAM_FOCUS는 SQL_ERROR가 반환될 때 변경되지 않습니다.  
  
 SQL_SOPT_SS_PARAM_FOCUS를 0으로 설정하면 매개 변수의 설명자 레코드에 대한 액세스가 복원됩니다.  
  
 SQLSetStmtAttr를 사용 하 여 SQL_SOPT_SS_NAME_SCOPE를 설정할 수도 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 SQL_SOPT_SS_NAME_SCOPE 섹션을 참조하십시오.  
  
 자세한 내용은 [준비 된 문의 테이블 반환 매개 변수 메타 데이터](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)를 참조 하세요.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>스파스 열에 대한 SQLSetStmtAttr 지원  
 SQLSetStmtAttr를 사용 하 여 SQL_SOPT_SS_NAME_SCOPE를 설정할 수 있습니다. 자세한 내용은이 항목의 뒷부분에 나오는 SQL_SOPT_SS_NAME_SCOPE 섹션을 참조 하세요. 스파스 열에 대 한 자세한 내용은 [스파스 열 지원 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)를 참조 하세요.  
  
## <a name="statement-attributes"></a>문 특성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 다음과 같은 드라이버별 문 특성도 지원합니다.  
  
### <a name="sql_sopt_ss_cursor_options"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 SQL_SOPT_SS_CURSOR 특성은 드라이버가 커서에 드라이버별 성능 옵션을 사용할지 여부를 지정합니다. 이러한 옵션을 설정 하면 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 를 사용할 수 없습니다. 기본 설정은 SQL_CO_OFF입니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*값*|설명|  
|----------------------|-----------------|  
|SQL_CO_OFF|기본값 빠른 앞 으로만 이동 가능한 읽기 전용 커서 및 자동 인출 사용 하지 않도록 설정 하 여 앞 으로만 이동 가능한 읽기 전용 커서에서 **SQLGetData** 를 사용 하도록 설정 합니다. SQL_SOPT_SS_CURSOR_OPTIONS가 SQL_CO_OFF로 설정되면 커서 유형이 변경되지 않습니다. 즉, 빠른 정방향 전용 커서는 빠른 정방향 전용 커서로 유지됩니다. 커서 유형을 변경 하려면 응용 프로그램이 **SQLSetStmtAttr**/SQL_ATTR_CURSOR_TYPE를 사용 하 여 다른 커서 유형을 설정 해야 합니다.|  
|SQL_CO_FFO|빠른 전진 전용, 읽기 전용 커서를 사용 하도록 설정 하 고 앞 으로만 이동 가능한 읽기 전용 커서에서 **SQLGetData** 를 사용 하지 않도록 설정 합니다.|  
|SQL_CO_AF|임의의 커서 유형에 대해 자동 인출 옵션을 설정합니다. 문 핸들에 대해이 옵션을 설정 하면 **Sqlexecute** 또는 **sqlexecdirect** 가 암시적 **sqlfetchscroll** (SQL_FIRST)을 생성 합니다. 커서가 열리고 서버에 대한 단일 왕복에서 행의 첫 번째 일괄 처리가 반환됩니다.|  
|SQL_CO_FFO_AF|빠른 정방향 전용 커서에 대해 자동 인출 옵션을 설정합니다. 이는 SQL_CO_AF 및 SQL_CO_FFO를 모두 지정한 것과 같습니다.|  
  
 이러한 옵션이 설정된 경우 서버는 마지막 행이 인출되면 자동으로 커서를 닫습니다. 응용 프로그램은 여전히 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) (SQL_CLOSE) 또는 [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)를 호출 해야 하지만 드라이버에서 서버에 CLOSE 알림을 보낼 필요가 없습니다.  
  
 Select 목록에 **text**, **ntext**또는 **image** 열이 포함 된 경우에는 빠른 전진 전용 커서가 동적 커서로 변환 되 고 **SQLGetData** 가 허용 됩니다.  
  
### <a name="sql_sopt_ss_defer_prepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 SQL_SOPT_SS_DEFER_PREPARE 특성은 **Sqlexecute**, [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 또는 [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md) 가 실행 될 때까지 문이 즉시 준비 되거나 지연 되는지 여부를 결정 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 및 이전 버전에서는 이 속성이 무시됩니다(준비 지연이 지원되지 않음). *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*값*|설명|  
|----------------------|-----------------|  
|SQL_DP_ON|기본값 [Sqlprepare 함수](https://go.microsoft.com/fwlink/?LinkId=59360)를 호출한 후에는 **sqlprepare** 가 호출 되거나 메타 속성 작업 (**SQLDescribeCol** 또는 **SQLDescribeParam**)이 실행 될 때까지 문 준비가 지연 됩니다.|  
|SQL_DP_OFF|**Sqlprepare** 를 실행 하는 즉시 문이 준비 됩니다.|  
  
### <a name="sql_sopt_ss_regionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 SQL_SOPT_SS_REGIONALIZE 특성은 명령 수준에서 데이터 변환을 결정하는 데 사용됩니다. 이 특성은 드라이버가 날짜, 시간 및 통화 값을 문자열로 변환할 때 클라이언트 로캘 설정을 준수하도록 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 데이터 형식에서 문자열로의 변환만 해당됩니다.  
  
 *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*값*|설명|  
|----------------------|-----------------|  
|SQL_RE_OFF|기본값 드라이버가 날짜, 시간 및 통화 데이터를 문자열 데이터로 변환할 때 클라이언트 로캘 설정을 사용하지 않습니다.|  
|SQL_RE_ON|드라이버가 날짜, 시간 및 통화 데이터를 문자열 데이터로 변환할 때 클라이언트 로캘 설정을 사용합니다.|  
  
 국가별 변환 설정이 통화, 숫자, 날짜 및 시간 데이터 형식에 적용됩니다. 변환 설정은 통화, 숫자, 날짜 또는 시간 값을 문자열로 변환한 경우 출력 변환에만 적용할 수 있습니다.  
  
> [!NOTE]  
>  문 옵션 SQL_SOPT_SS_REGIONALIZE가 사용되면 드라이버는 현재 사용자의 로캘 레지스트리 설정을 사용합니다. 응용 프로그램에서 **SetThreadLocale**를 호출 하는 등을 통해이를 설정 하는 경우 드라이버는 현재 스레드의 로캘을 인식 하지 못합니다.  
  
 데이터 원본의 국가별 동작을 변경하면 애플리케이션에서 오류가 발생할 수 있습니다. 날짜 문자열을 구문 분석하며 날짜 문자열이 ODBC에 정의된 대로 표시될 것으로 예상하는 애플리케이션에서 이 값을 변경하면 부정적인 영향을 줄 수 있습니다.  
  
### <a name="sql_sopt_ss_textptr_logging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 SQL_SOPT_SS_TEXTPTR_LOGGING 특성은 **텍스트** 또는 **이미지** 데이터를 포함 하는 열에 대 한 작업 로깅을 설정/해제 합니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*값*|설명|  
|----------------------|-----------------|  
|SQL_TL_OFF|**Text** 및 **image** 데이터에 대해 수행 되는 작업의 로깅을 사용 하지 않도록 설정 합니다.|  
|SQL_TL_ON|기본값 **Text** 및 **image** 데이터에 대해 수행 되는 작업의 로깅을 사용 하도록 설정 합니다.|  
  
### <a name="sql_sopt_ss_hidden_columns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 SQL_SOPT_SS_HIDDEN_COLUMNS 특성은 결과 집합에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT FOR BROWSE 문의 숨겨진 열을 노출합니다. 드라이버는 기본적으로 이러한 열을 노출하지 않습니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
|*값*|설명|  
|----------------------|-----------------|  
|SQL_HC_OFF|기본값 결과 집합에서 FOR BROWSE 열을 숨깁니다.|  
|SQL_HC_ON|FOR BROWSE 열을 공개합니다.|  
  
### <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 특성은 쿼리 알림 요청에 대한 메시지 텍스트를 반환합니다.  
  
### <a name="sql_sopt_ss_querynotification_options"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS 특성은 쿼리 알림 요청에 사용되는 옵션을 지정합니다. 이러한 옵션은 아래에 지정된 것처럼 `name=value` 구문이 포함된 문자열로 지정됩니다. 애플리케이션은 서비스를 만들고 큐에서 알림을 읽어야 합니다.  
  
 쿼리 알림 옵션 문자열의 구문은 다음과 같습니다.  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 예를 들면 다음과 같습니다.  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sql_sopt_ss_querynotification_timeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT 특성은 쿼리 알림을 활성 상태로 유지할 초를 지정합니다. 기본값은 432000초(5일)입니다. *ValuePtr* 값은 SQLLEN 유형입니다.  
  
### <a name="sql_sopt_ss_param_focus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 SQL_SOPT_SS_PARAM_FOCUS 특성은 후속 SQLBindParameter, SQLGetDescField, SQLSetDescField, SQLGetDescRec 및 SQLSetDescRec 호출에 대 한 포커스를 지정 합니다.  
  
 SQL_SOPT_SS_PARAM_FOCUS의 형식은 SQLULEN입니다.  
  
 기본값은 0이며 이는 이러한 호출이 SQL 문의 매개 변수 표식에 해당하는 매개 변수의 주소를 지정한다는 의미입니다. 테이블 반환 매개 변수의 매개 변수 번호로 설정하면 이러한 호출이 해당 테이블 반환 매개 변수 열의 주소를 지정합니다. 테이블 반환 매개 변수의 매개 변수 번호가 아닌 값으로 설정하면 이러한 호출이 오류 IM020: "매개 변수 포커스가 테이블 반환 매개 변수를 참조하지 않습니다"를 반환합니다.  
  
### <a name="sql_sopt_ss_name_scope"></a>SQL_SOPT_SS_NAME_SCOPE  
 SQL_SOPT_SS_NAME_SCOPE 특성은 후속 카탈로그 함수 호출의 이름 범위를 지정합니다. SQLColumns에서 반환 하는 결과 집합은 SQL_SOPT_SS_NAME_SCOPE 설정에 따라 달라 집니다.  
  
 SQL_SOPT_SS_NAME_SCOPE의 형식은 SQLULEN입니다.  
  
|*값*|설명|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|기본값<br /><br /> 테이블 반환 매개 변수를 사용할 때 실제 테이블의 메타데이터가 반환되도록 지정합니다.<br /><br /> 스파스 열 기능을 사용 하는 경우 SQLColumns는 스파스 **column_set**의 멤버가 아닌 열만 반환 합니다.|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|애플리케이션이 실제 테이블이 아니라 테이블 형식의 메타데이터를 요구한다는 것을 나타냅니다. 카탈로그 함수가 테이블 형식의 메타데이터를 반환해야 합니다. 그런 다음 응용 프로그램은 테이블 반환 매개 변수의 TYPE_NAME를 *TableName* 매개 변수로 전달 합니다.|  
|SQL_SS_NAME_SCOPE_EXTENDED|스파스 열 기능을 사용 하는 경우 SQLColumns는 **column_set** 멤버 자격에 관계 없이 모든 열을 반환 합니다.|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|스파스 열 기능을 사용 하는 경우 SQLColumns는 스파스 **column_set**의 멤버인 열만 반환 합니다.|  
|SQL_SS_NAME_SCOPE_DEFAULT|SQL_SS_NAME_SCOPE_TABLE과 같습니다.|  
  
 SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMA_NAME는 각각 *CatalogName* 및 *SchemaName* 매개 변수와 함께 사용 되어 테이블 반환 매개 변수의 카탈로그와 스키마를 식별 합니다. 애플리케이션이 테이블 반환 매개 변수의 메타데이터 검색을 마치면 SQL_SOPT_SS_NAME_SCOPE가 기본값인 SQL_SS_NAME_SCOPE_TABLE로 다시 설정됩니다.  
  
 SQL_SOPT_SS_NAME_SCOPE가 SQL_SS_NAME_SCOPE_TABLE로 설정되면 연결된 서버에 대한 쿼리가 실패합니다. 서버 구성 요소를 포함 하는 카탈로그를 사용 하 여 SQLColumns 또는 Sqlprimarykey를 호출 하면 실패 합니다.  
  
 SQL_SOPT_SS_NAME_SCOPE를 잘못된 값으로 설정하려고 하면 SQL_ERROR가 반환되고 SQLSTATE HY024 및 "잘못된 특성 값입니다" 메시지가 표시되며 진단 레코드가 생성됩니다.  
  
 SQL_SOPT_SS_NAME_SCOPE에 SQL_SS_NAME_SCOPE_TABLE 이외의 값이 있는 경우 SQLTables, Sqltables 또는 SQLPrimaryKeys의 다른 카탈로그 함수를 호출 하면 SQL_ERROR 반환 됩니다. SQLSTATE HY010 및 "함수 시퀀스 오류입니다(SQL_SOPT_SS_NAME_SCOPE가 SQL_SS_NAME_SCOPE_TABLE로 설정되지 않았습니다)" 메시지가 표시되고 진단 레코드가 생성됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLGetStmtAttr 함수](https://go.microsoft.com/fwlink/?LinkId=59355)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
