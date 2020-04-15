---
title: SQL칼럼 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: abce98b64da8de6039f81025201cce25269763a6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302611"
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumns는** *카탈로그 이름,* *테이블 이름*또는 *ColumnName* 매개 변수에 대한 값이 있는지 여부를 SQL_SUCCESS 반환합니다. **SQLFetch는** 이러한 매개 변수에 잘못된 값이 사용되는 SQL_NO_DATA 반환합니다.  
  
> [!NOTE]  
>  큰 값 형식의 경우 모든 길이 매개 변수는 SQL_SS_LENGTH_UNLIMITED 값으로 반환됩니다.  
  
 **SQLColumns** 정적 서버 커서에서 실행할 수 있습니다. 업데이터(동적 또는 키 집합) 커서에서 **SQLColumns를** 실행하려고 하면 커서 유형이 변경되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 *CatalogName* 매개 변수의 두 부분으로 구성된 이름인 *Linked_Server_Name.Catalog_Name*을 사용하여 연결된 서버의 테이블에 대한 정보를 보고할 수 있도록 지원합니다.  
  
 ODBC 2. *x* 응용 프로그램 *테이블Name에서*와일드 카드를 사용 하지 않는 , **SQLColumns** 는 이름이 *TableName과* 일치 하 고 현재 사용자가 소유 하는 모든 테이블에 대 한 정보를 반환 합니다. 현재 사용자가 *TableName* 매개 변수와 일치하는 테이블을 소유하지 않는 경우 **SQLColumns는** 테이블 이름이 *TableName* 매개 변수와 일치하는 다른 사용자가 소유한 테이블에 대한 정보를 반환합니다. ODBC 2. *와일드카드를* 사용하는 x 응용 프로그램 **SQLColumns는** 이름이 *TableName*과 일치하는 모든 테이블을 반환합니다. ODBC 3. *x* 응용 프로그램 **SQLColumns** 는 소유자 또는 와일드카드 사용 여부에 관계없이 *이름이 TableName과* 일치하는 모든 테이블을 반환합니다.  
  
 다음 표에서는 결과 집합에서 반환되는 열을 나열합니다.  
  
|열 이름|설명|  
|-----------------|-----------------|  
|DATA_TYPE|**varchar(최대)** 데이터 형식에 대해 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR 반환합니다.|  
|TYPE_NAME|**varchar(최대)** 및 **nvarchar(최대)** 데이터 유형에 대해 "varchar", "varbinary" 또는 "nvarchar"를 반환합니다. **varbinary(max)**|  
|COLUMN_SIZE|열의 크기가 무제한임을 나타내는 **varchar(최대)** 데이터 형식에 대해 SQL_SS_LENGTH_UNLIMITED 반환합니다.|  
|BUFFER_LENGTH|버퍼 의 크기가 무제한임을 나타내는 **varchar(최대)** 데이터 형식에 대한 SQL_SS_LENGTH_UNLIMITED 반환합니다.|  
|SQL_DATA_TYPE|**varchar(최대)** 데이터 형식에 대해 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR 반환합니다.|  
|CHAR_OCTET_LENGTH|char 열 또는 binary 열의 최대 길이를 반환합니다. 크기가 무제한인 경우 0을 반환합니다.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름을 반환합니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|XML 스키마 컬렉션 이름이 정의된 스키마의 이름을 반환합니다. 스키마 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_XML_SCHEMACOLLECTION_NAME|XML 스키마 컬렉션의 이름을 반환합니다. 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_UDT_CATALOG_NAME|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_UDT_SCHEMA_NAME|UDT가 포함된 스키마의 이름입니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT의 어셈블리가 명시된 정식 이름입니다.|  
  
 UDT의 경우 기존 TYPE_NAME 열은 UDT의 이름을 나타내는 데 사용됩니다. 따라서 **SQLColumns 또는 SQLProcedureColumns의** 결과 집합에 [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)추가해야 합니다. UDT 열 또는 매개 변수의 DATA_TYPE은 SQL_SS_UDT입니다.  
  
 UDT 매개 변수의 경우 서버에서 이 정보를 반환하거나 요구하면 위에 정의된 새로운 드라이버별 설명자를 사용하여 UDT의 추가 메타데이터 속성을 얻거나 설정할 수 있습니다.  
  
 클라이언트가 SQLColumns에 연결하고 호출할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 때 카탈로그 입력 매개 변수에 NULL 또는 와일드카드 값을 사용하면 다른 카탈로그의 정보가 반환되지 않습니다. 현재 카탈로그에 대한 정보만 반환됩니다. 클라이언트는 먼저 SQLTable을 호출하여 원하는 테이블이 있는 카탈로그를 확인할 수 있습니다. 그런 다음 클라이언트는 SQLColumns 호출에서 카탈로그 입력 매개 변수에 대해 해당 카탈로그 값을 사용하여 해당 테이블의 열에 대한 정보를 검색할 수 있습니다.  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns 및 테이블 반환 매개 변수  
 SQLColumns에서 반환되는 결과 집합은 SQL_SOPT_SS_NAME_SCOPE 설정에 따라 다릅니다. 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오. 테이블 반환 매개 변수에 다음 열이 추가되었습니다.  
  
|열 이름|데이터 형식|콘텐츠|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|TABLE_TYPE의 열의 경우 열이 계산 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
|SS_IS_IDENTITY|Smallint|열이 ID 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
  
 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;[&#40;테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLColumns 지원  
 날짜/시간 형식에 대해 반환된 값에 대한 자세한 내용은 [카탈로그 메타데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)를 참조하십시오.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLColumns 지원  
 **SQLColumns는** 큰 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>스파스 열에 대한 SQLColumns 지원  
 SQLColumns에 대한 결과 집합에 두 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 특정 열이 추가되었습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|열이 스파스 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
|SS_IS_COLUMN_SET|**Smallint**|열이 **column_set** 열인 경우 이 열은 SQL_TRUE. 그렇지 않으면, SQL_FALSE.|  
  
 ODBC 사양에 따라 SS_IS_SPARSE 및 SS_IS_COLUMN_SET ODBC 자체에서 위임한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열보다 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]이전 버전에 추가된 모든 드라이버 별 열 앞에 나타납니다.  
  
 SQLColumns에서 반환되는 결과 집합은 SQL_SOPT_SS_NAME_SCOPE 설정에 따라 다릅니다. 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 ODBC의 스파스 열에 대한 자세한 내용은 [sparse 열 지원 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLColumns 함수](https://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
