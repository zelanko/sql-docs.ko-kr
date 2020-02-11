---
title: SQLColumns | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 58209d617d7978ff4ed6da486bd5c89c076c05af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787417"
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **Sqlcolumns** 는 *CatalogName*, *TableName*또는 *ColumnName* 매개 변수에 대 한 값이 있는지 여부를 SQL_SUCCESS을 반환 합니다. 이러한 매개 변수에 잘못 된 값이 사용 되는 경우 **Sqlfetch** SQL_NO_DATA 반환 합니다.  
  
> [!NOTE]  
>  큰 값 형식의 경우 모든 길이 매개 변수는 SQL_SS_LENGTH_UNLIMITED 값으로 반환됩니다.  
  
 **Sqlcolumns** 는 정적 서버 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 (동적 또는 키 집합) 커서에 대해 **Sqlcolumns** 를 실행 하려고 하면 커서 유형이 변경 되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환 됩니다.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 *CatalogName* 매개 변수의 두 부분으로 구성된 이름인 *Linked_Server_Name.Catalog_Name*을 사용하여 연결된 서버의 테이블에 대한 정보를 보고할 수 있도록 지원합니다.  
  
 ODBC 2의 경우. *x* 응용 프로그램 *tablename*에서 와일드 카드를 사용 하지 않습니다. **sqlcolumns** 는 이름이 *tablename* 과 일치 하 고 현재 사용자가 소유 하 고 있는 모든 테이블에 대 한 정보를 반환 합니다. 현재 사용자가 이름이 *tablename* 매개 변수와 일치 하는 테이블을 소유 하지 않는 경우 **sqlcolumns** 는 다른 사용자가 소유 하 고 있는 테이블에 대 한 정보를 반환 합니다 .이는 테이블 이름이 *tablename* 매개 변수와 일치 합니다. ODBC 2의 경우. 와일드 카드를 사용 하는 *x* 응용 프로그램 **sqlcolumns** 는 이름이 *TableName*과 일치 하는 모든 테이블을 반환 합니다. ODBC 3의 경우. *x* 응용 프로그램 **sqlcolumns** 는 소유자 또는 와일드 카드 사용 여부에 관계 없이 이름이 *TableName* 과 일치 하는 모든 테이블을 반환 합니다.  
  
 다음 표에서는 결과 집합에서 반환되는 열을 나열합니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|DATA_TYPE|**VARCHAR (max)** 데이터 형식에 대 한 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR를 반환 합니다.|  
|TYPE_NAME|**Varchar (max)**, **varbinary (max)** 및 **nvarchar (max)** 데이터 형식에 대해 "varchar", "varbinary" 또는 "nvarchar"를 반환 합니다.|  
|COLUMN_SIZE|**Varchar (max)** 데이터 형식에 대해 열 크기에 제한이 없음을 나타내는 SQL_SS_LENGTH_UNLIMITED를 반환 합니다.|  
|BUFFER_LENGTH|**Varchar (max)** 데이터 형식에 대 한 SQL_SS_LENGTH_UNLIMITED를 반환 합니다 .이는 버퍼의 크기가 무제한 임을 나타냅니다.|  
|SQL_DATA_TYPE|**VARCHAR (max)** 데이터 형식에 대 한 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR를 반환 합니다.|  
|CHAR_OCTET_LENGTH|char 열 또는 binary 열의 최대 길이를 반환합니다. 크기가 무제한인 경우 0을 반환합니다.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름을 반환합니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|XML 스키마 컬렉션 이름이 정의된 스키마의 이름을 반환합니다. 스키마 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_XML_SCHEMACOLLECTION_NAME|XML 스키마 컬렉션의 이름을 반환합니다. 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_UDT_CATALOG_NAME|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_UDT_SCHEMA_NAME|UDT가 포함된 스키마의 이름입니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT의 어셈블리가 명시된 정식 이름입니다.|  
  
 Udt의 경우 기존 TYPE_NAME 열은 UDT의 이름을 나타내는 데 사용 됩니다. 따라서 **Sqlcolumns** 또는 [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)의 결과 집합에 추가 열을 추가 하지 않아야 합니다. UDT 열 또는 매개 변수의 DATA_TYPE은 SQL_SS_UDT입니다.  
  
 UDT 매개 변수의 경우 서버에서 이 정보를 반환하거나 요구하면 위에 정의된 새로운 드라이버별 설명자를 사용하여 UDT의 추가 메타데이터 속성을 얻거나 설정할 수 있습니다.  
  
 클라이언트가 SQLColumns에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 하 고이를 호출 하는 경우 카탈로그 입력 매개 변수에 NULL 또는 와일드 카드 값을 사용 하면 다른 카탈로그의 정보가 반환 되지 않습니다. 현재 카탈로그에 대한 정보만 반환됩니다. 클라이언트는 먼저 SQLTables를 호출 하 여 원하는 테이블이 있는 카탈로그를 확인할 수 있습니다. 그런 다음 클라이언트는 SQLColumns 호출에서 카탈로그 입력 매개 변수에 해당 카탈로그 값을 사용 하 여 해당 테이블의 열에 대 한 정보를 검색할 수 있습니다.  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns 및 테이블 반환 매개 변수  
 SQLColumns에서 반환 하는 결과 집합은 SQL_SOPT_SS_NAME_SCOPE 설정에 따라 달라 집니다. 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 참조 하세요. 테이블 반환 매개 변수에 다음 열이 추가되었습니다.  
  
|열 이름|데이터 형식|콘텐츠|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|TABLE_TYPE의 열의 경우 열이 계산 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
|SS_IS_IDENTITY|Smallint|열이 ID 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLColumns 지원  
 날짜/시간 형식에 대해 반환 되는 값에 대 한 자세한 내용은 [카탈로그 메타 데이터](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)를 참조 하세요.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLColumns 지원  
 **Sqlcolumns** 는 크기가 높은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC&#41;&#40;LARGE CLR 사용자 정의 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>스파스 열에 대한 SQLColumns 지원  
 SQLColumns의 결과 집합에는 두 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 특정 열이 추가 되었습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|열이 스파스 열이면 SQL_TRUE이며 그렇지 않으면 SQL_FALSE입니다.|  
|SS_IS_COLUMN_SET|**Smallint**|열이 **column_set** 열인 경우 SQL_TRUE입니다. 그렇지 않으면 SQL_FALSE 합니다.|  
  
 ODBC 사양에 따라 SS_IS_SPARSE 및 SS_IS_COLUMN_SET는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]버전에 추가 된 모든 드라이버 특정 열 앞에, 그리고 odbc 자체에 의해 지정 된 모든 열 뒤에 나타납니다.  
  
 SQLColumns에서 반환 하는 결과 집합은 SQL_SOPT_SS_NAME_SCOPE 설정에 따라 달라 집니다. 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 참조 하세요.  
  
 ODBC의 스파스 열에 대 한 자세한 내용은 [스파스 열 지원 &#40;odbc&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLColumns 함수](https://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
