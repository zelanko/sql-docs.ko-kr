---
title: 새로운 날짜 및 시간 기능과 이전 SQL Server 버전 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f5e7bdd599222eb0c37f851901a59f663cc2658
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>새로운 날짜 및 시간 기능과 이전 SQL Server 버전 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  이 항목에서는 향상 된 날짜 및 시간 기능을 사용 하는 클라이언트 응용 프로그램의 버전으로 통신 하는 경우 예상 되는 동작을 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], 시점과 버전을 사용 하 여 컴파일한 클라이언트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 이전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 날짜 및 시간 기능 향상 된 원하는 서버에 명령을 보냅니다.  
  
## <a name="down-level-client-behavior"></a>하위 수준 클라이언트 동작  
 버전을 사용 하는 클라이언트 응용 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 보다 이전 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 으로 새 날짜/시간 형식을 **nvarchar** 열입니다. 열의 내용은 리터럴 표현입니다. 자세한 내용은의 "데이터 형식:: 문자열 및 리터럴" 섹션을 참조 하십시오. [OLE DB 날짜 및 시간 기능 향상에 대 한 데이터 형식 지원](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)합니다. 열 크기는 열에 지정된 전체 자릿수에 대한 최대 리터럴 길이입니다.  
  
 카탈로그 Api 클라이언트에 반환 된 하위 수준 데이터 형식 코드와 일치 메타 데이터를 반환 합니다 (예를 들어 **nvarchar**)와 관련 된 하위 수준 표현 (예를 들어 적절 한 리터럴 형식). 그러나 반환되는 데이터 형식의 이름은 실제 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 형식 이름입니다.  
  
 하위 수준 클라이언트 응용 프로그램에 대해 실행 되는 경우는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (또는 이상) 날짜/시간에는 스키마 변경 내용에 형식을 적용 된 서버에 예상 되는 동작은 다음과 같습니다.  
  
|OLE DB 클라이언트 형식|SQL Server 2005 형식|SQL Server 2008(또는 이후 버전) 형식|결과 변환(서버에서 클라이언트로)|매개 변수 변환(클라이언트에서 서버로)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|날짜/시간|날짜|확인|확인|  
|DBTYPE_DBTIMESTAMP|||시간 필드가 0으로 설정됩니다.|시간 필드가 0이 아닌 경우 IRowsetChange 문자열 잘림으로 인해 실패 합니다.|  
|DBTYPE_DBTIME||Time(0)|확인|확인|  
|DBTYPE_DBTIMESTAMP|||날짜 필드가 현재 날짜로 설정됩니다.|IRowsetChange 소수 자릿수 초는 0이 아닌 경우 문자열 잘림으로 인해 실패 합니다.<br /><br /> 날짜는 무시됩니다.|  
|DBTYPE_DBTIME||Time(7)|실패 - 시간 리터럴이 잘못되었습니다.|확인|  
|DBTYPE_DBTIMESTAMP|||실패 - 시간 리터럴이 잘못되었습니다.|확인|  
|DBTYPE_DBTIMESTAMP||Datetime2(3)|확인|확인|  
|DBTYPE_DBTIMESTAMP||Datetime2 (7)|확인|확인|  
|DBTYPE_DBDATE|Smalldatetime|날짜|확인|확인|  
|DBTYPE_DBTIMESTAMP|||시간 필드가 0으로 설정됩니다.|시간 필드가 0이 아닌 경우 IRowsetChange 문자열 잘림으로 인해 실패 합니다.|  
|DBTYPE_DBTIME||Time(0)|확인|확인|  
|DBTYPE_DBTIMESTAMP|||날짜 필드가 현재 날짜로 설정됩니다.|IRowsetChange 소수 자릿수 초는 0이 아닌 경우 문자열 잘림으로 인해 실패 합니다.<br /><br /> 날짜는 무시됩니다.|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|확인|확인|  
  
 표에서 정상은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 동작하는 경우 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)](또는 이후 버전)에서도 계속 동작함을 의미합니다.  
  
 다음과 같은 일반적인 스키마 변경 내용만 고려됩니다.  
  
-   논리적으로 응용 프로그램에 날짜 또는 시간 값만 필요한 경우 새 형식을 사용합니다. 그러나 응용 프로그램이 사용 하도록 강제 적용 **datetime** 또는 **smalldatetime** 때문에 별도 날짜 및 시간 형식을 사용할 수 없었습니다.  
  
-   초 소수 부분 자릿수를 늘리거나 정확도를 높이기 위해 새 형식을 사용합니다.  
  
-   전환 **datetime2** 날짜 및 시간에 대 한이 기본 설정된 된 데이터 형식입니다.  
  
 Icommandwithparameters:: Getparameterinfo 또는 스키마 행 집합을 통해 가져온 서버 메타 데이터를 사용 하 여 icommandwithparameters:: Setparameterinfo 통해 매개 변수 형식 정보를 설정 하는 응용 프로그램은 클라이언트 변환 도중 실패 있는 문자열 소스 형식으로 나타낸 대상 유형의 문자열 표현 보다 큽니다. 예를 들어 클라이언트 바인딩 DBTYPE_DBTIMESTAMP를 사용 하 고 서버 열은 날짜, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 "yyyy dd 밀리미터 hh:mm:ss.fff"에 값을 변환 하지만 서버 메타 데이터를로 반환 됩니다 **nvarchar (10)**합니다. 결과 오버플로는 DBSTATUS_E_CATCONVERTVALUE를 유발합니다. 비슷한 문제가 발생 하는 데이터 변환 IRowsetChange, 하 여 행 집합 메타 데이터는 결과 집합 메타 데이터에서 설정 되어 있기 때문입니다.  
  
### <a name="parameter-and-rowset-metadata"></a>매개 변수 및 행 집합 메타데이터  
 이 섹션의 버전으로 컴파일된 클라이언트에 대 한 매개 변수, 결과 열 및 스키마 행 집합에 대 한 메타 데이터를 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 보다 이전 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]합니다.  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 DBPARAMINFO 구조를 통해 다음 정보를 반환 합니다.는 *prgParamInfo* 매개 변수:  
  
|매개 변수 유형|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 이러한 값 범위 중 일부는 연속되지 않습니다. 예를 들어 8, 10..16에서는 9가 누락되어 있습니다. 이러한 경우는 소수 부분 자릿수가 0보다 커서 소수점을 추가했을 때 발생합니다.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 다음 열이 반환됩니다.  
  
|열 유형|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|date|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 구조는 다음 정보를 반환합니다.  
  
|매개 변수 유형|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>스키마 행 집합  
 이 섹션에서는 새 데이터 형식의 매개 변수, 결과 열 및 스키마 행 집합에 대한 메타데이터에 대해 설명합니다. 이 정보는 유용 도구를 사용 하 여 개발 하는 클라이언트 공급자는 것 보다 이전 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client입니다.  
  
#### <a name="columns-rowset"></a>COLUMNS 행 집합  
 날짜/시간 형식에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|date|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS 행 집합  
 날짜/시간 형식에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|date|DBTYPE_WSTR|10|20|date|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|datetime|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>PROVIDER_TYPES 행 집합  
 날짜/시간 형식에 대해 다음 행이 반환됩니다.  
  
|형식 -><br /><br /> 열|date|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>하위 수준 서버 동작  
 보다 이전 버전의 서버에 연결 된 경우 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], (예를 들어 icommandwithparameters:: Setparameterinfo itabledefinition:: Createtable)와 새 서버 유형 이름을 사용 하려는 모든 시도가 DB_E_BADTYPENAME로 발생 합니다.  
  
 새 형식이 형식 이름을 사용하지 않고 매개 변수 또는 결과에 바인딩되고, 새 형식을 사용하여 서버 유형을 암시적으로 지정하거나 서버 유형에서 클라이언트 유형으로의 유효한 변환이 없는 경우 DB_E_ERRORSOCCURRED가 반환되고 DBBINDSTATUS_UNSUPPORTED_CONVERSION이 Execute에 사용된 접근자에 대한 바인딩 상태로 설정됩니다.  
  
 버퍼 유형에서 연결의 서버 버전의 서버 유형으로 지원되는 클라이언트 변환이 있는 경우 모든 클라이언트 버퍼 유형을 사용할 수 있습니다. 이 컨텍스트에서 *서버 유형* icommandwithparameters:: Setparameterinfo를로 지정 된 사용 권한에 포함 된 버퍼 유형 icommandwithparameters:: Setparameterinfo 호출 되지 않은 경우 또는 유형을 의미 합니다. 이는 하위 수준 서버에서, 또는 DataTypeCompatibility=80일 때 지원되는 서버 유형에 대한 클라이언트 변환이 성공할 경우 DBTYPE_DBTIME2 및 DBTYPE_DBTIMESTAMPOFFSET을 사용할 수 있음을 의미합니다. 물론 서버 유형이 잘못된 경우 서버는 실제 서버 유형으로 암시적 변환을 수행하지 못하면 여전히 오류를 보고할 수 있습니다.  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>SSPROP_INIT_DATATYPECOMPATIBILITY 동작  
 SSPROP_INIT_DATATYPECOMPATIBILITY SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000로 설정 되 면 새로운 날짜/시간 형식 및 관련된 메타 데이터 표시를 클라이언트 하위 수준 클라이언트에 대 한 표시 된 대로에 설명 된 대로 [에 대 한 대량 복사 변경 사항 향상 된 날짜 및 시간 형식 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다.  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind 비교  
 새 날짜/시간 형식은 날짜/시간 형식이 아니라 문자열 형식으로 표시되기 때문에 이러한 형식에 대해서는 모든 비교 연산자를 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [날짜 및 시간 기능 향상 & #40; OLE db& #41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
