---
title: SQLColumns | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
caps.latest.revision: "62"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f539f5202717a5eb58929a9be9ea7945687cbb4e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumns** 에 대 한 값이 존재 하는지 여부에 관계 없이 SQL_SUCCESS를 반환 된 *CatalogName*, *TableName*, 또는 *ColumnName* 매개 변수입니다. **SQLFetch** 이러한 매개 변수에서 잘못 된 값을 사용할 경우 SQL_NO_DATA를 반환 합니다.  
  
> [!NOTE]  
>  큰 값 형식의 경우 모든 길이 매개 변수는 SQL_SS_LENGTH_UNLIMITED 값으로 반환됩니다.  
  
 **SQLColumns** 는 정적 서버 커서에 대해 실행할 수 있습니다. 실행 하려고 **SQLColumns** 업데이트할 수 있는 (동적 또는 키 집합) 커서에서 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 사용 하 여 연결 된 서버의 테이블에 대 한 정보 보고를 지원는 *CatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
 Odbc 2. *x* 응용 프로그램에서 와일드 카드를 사용 하지 *TableName*, **SQLColumns** 정보에 대 한 테이블 이름이 일치를 반환 *TableName*현재 사용자가 소유 하 고 있습니다. 현재 사용자와 이름이 없는 테이블을 소유 하는 경우는 *TableName* 매개 변수를 **SQLColumns** 일치 하는 테이블 이름이 다른 사용자가 소유한 모든 테이블에 대 한 정보를 반환 된  *TableName* 매개 변수입니다. Odbc 2. *x* 와일드 카드를 사용 하 여 응용 프로그램 **SQLColumns** 이름을 일치 하는 모든 테이블을 반환 *TableName*합니다. Odbc 3. *x* 응용 프로그램 **SQLColumns** 이름을 일치 하는 모든 테이블을 반환 *TableName* 소유자 또는 와일드 카드 사용 여부에 관계 없이 합니다.  
  
 다음 표에서는 결과 집합에서 반환되는 열을 나열합니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|DATA_TYPE|반환 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR입니다는 **varchar (max)** 데이터 형식입니다.|  
|TYPE_NAME|에 대 한 "varchar", "varbinary" 또는 "nvarchar"를 반환 된 **varchar (max)**, **varbinary (max)**, 및 **nvarchar (max)** 데이터 형식입니다.|  
|COLUMN_SIZE|에 대해 SQL_SS_LENGTH_UNLIMITED를 반환 **varchar (max)** 데이터 형식 열의 크기를 제한 아님을 나타내는입니다.|  
|BUFFER_LENGTH|에 대해 SQL_SS_LENGTH_UNLIMITED를 반환 **varchar (max)** 데이터 형식을 나타내는 버퍼의 크기는 제한 되지 않습니다.|  
|SQL_DATA_TYPE|반환 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR입니다는 **varchar (max)** 데이터 형식입니다.|  
|CHAR_OCTET_LENGTH|char 열 또는 binary 열의 최대 길이를 반환합니다. 크기가 무제한인 경우 0을 반환합니다.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름을 반환합니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|XML 스키마 컬렉션 이름이 정의된 스키마의 이름을 반환합니다. 스키마 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_XML_SCHEMACOLLECTION_NAME|XML 스키마 컬렉션의 이름을 반환합니다. 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_UDT_CATALOG_NAME|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_UDT_SCHEMA_NAME|UDT가 포함된 스키마의 이름입니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT의 어셈블리가 명시된 정식 이름입니다.|  
  
 Udt에 대 한 기존의 TYPE_NAME 열 UDT;의 이름을 나타내는 데 사용 되는 결과 집합에 없는 다른 열을 추가할 수는 따라서 **SQLColumns** 또는 [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)합니다. UDT 열 또는 매개 변수의 DATA_TYPE은 SQL_SS_UDT입니다.  
  
 UDT 매개 변수의 경우 서버에서 이 정보를 반환하거나 요구하면 위에 정의된 새로운 드라이버별 설명자를 사용하여 UDT의 추가 메타데이터 속성을 얻거나 설정할 수 있습니다.  
  
 클라이언트가 연결 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카탈로그 입력된 매개 변수에 다른 카탈로그에서 정보를 반환 하지 것입니다에 대 한 NULL 또는 와일드 카드 값을 사용 하 여 SQLColumns를 호출 합니다. 현재 카탈로그에 대한 정보만 반환됩니다. 먼저 클라이언트를 확인 하려면 카탈로그에서 원하는 테이블 SQLTables를 호출 합니다. 클라이언트를 사용할 수 해당 카탈로그 값 SQLColumns에 대 한 호출에서 카탈로그 입력된 매개 변수의 해당 테이블의 열에 대 한 정보를 검색 합니다.  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns 및 테이블 반환 매개 변수  
 SQLColumns에서 반환 된 결과 집합은 SQL_SOPT_SS_NAME_SCOPE의 설정에 따라 달라 집니다. 자세한 내용은 참조 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다. 테이블 반환 매개 변수에 다음 열이 추가되었습니다.  
  
|열 이름|데이터 형식|내용|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|TABLE_TYPE의 열의 경우 열이 계산 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
|SS_IS_IDENTITY|Smallint|열이 ID 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 [테이블 반환 매개 변수 사용 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLColumns 지원  
 날짜/시간 형식에 대해 반환 되는 값에 대 한 정보를 참조 하십시오. [카탈로그 메타 데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)합니다.  
  
 자세한 내용은 참조 [날짜 및 시간 기능 향상 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLColumns 지원  
 **SQLColumns** 큰 CLR 사용자 정의 형식 (Udt)을 지원 합니다. 자세한 내용은 참조 [Large CLR User-Defined 형식 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>스파스 열에 대한 SQLColumns 지원  
 두 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLColumns 한 결과 집합에 특정 열이 추가 되었습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|열이 스파스 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
|SS_IS_COLUMN_SET|**Smallint**|열이는 **column_set** 열 이면 SQL_TRUE, 그렇지 않으면 SQL_FALSE입니다.|  
  
 ODBC 사양, SS_IS_SPARSE 및 SS_IS_COLUMN_SET 표시에 추가 된 모든 드라이버별 열 앞 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 보다 이전 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], 그리고 ODBC 자체에서 지정한 모든 열 뒤 합니다.  
  
 SQLColumns에서 반환 된 결과 집합은 SQL_SOPT_SS_NAME_SCOPE의 설정에 따라 달라 집니다. 자세한 내용은 참조 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다.  
  
 ODBC의 스파스 열에 대 한 자세한 내용은 참조 [Sparse Columns Support &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLColumns 함수](http://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
