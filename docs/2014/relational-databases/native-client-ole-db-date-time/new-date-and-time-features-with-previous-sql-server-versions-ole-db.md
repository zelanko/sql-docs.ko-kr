---
title: 이전 SQL Server 버전 (OLE DB)을 사용 하는 새로운 날짜 및 시간 기능 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], enhanced behavior with earlier SQL Server versions
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
author: rothja
ms.author: jroth
ms.openlocfilehash: 39f22fe37138fab22d79acc5bd667257f392737a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056300"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>이전 SQL Server 버전 관련 새로운 날짜 및 시간 기능(OLE DB)
  이 항목에서는 향상 된 날짜 및 시간 기능을 사용 하는 클라이언트 응용 프로그램이 이전 버전의와 통신할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , 그리고 이전 버전의 Native client를 사용 하 여 컴파일한 클라이언트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 향상 된 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 날짜 및 시간 기능을 지 원하는 서버에 명령을 보내는 경우 예상 되는 동작에 대해 설명 합니다.  
  
## <a name="down-level-client-behavior"></a>하위 수준 클라이언트 동작  
 이전 버전의 Native Client를 사용 하는 클라이언트 응용 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 새로운 날짜/시간 형식을 열로 표시 `nvarchar` 합니다. 열의 내용은 리터럴 표현입니다. 자세한 내용은 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](data-type-support-for-ole-db-date-and-time-improvements.md)의 "데이터 형식: 문자열 및 리터럴" 섹션을 참조 하세요. 열 크기는 열에 지정된 전체 자릿수에 대한 최대 리터럴 길이입니다.  
  
 카탈로그 API는 클라이언트에 반환된 하위 수준 데이터 형식 코드(예: `nvarchar`)와 일관된 메타데이터 및 관련된 하위 수준 표현(예: 적절한 리터럴 형식)을 반환합니다. 그러나 반환되는 데이터 형식의 이름은 실제 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 형식 이름입니다.  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]날짜/시간 형식에 대 한 스키마가 변경 된 (또는 이후) 서버에 대해 하위 수준 클라이언트 응용 프로그램이 실행 되는 경우 예상 되는 동작은 다음과 같습니다.  
  
|OLE DB 클라이언트 형식|SQL Server 2005 형식|SQL Server 2008(또는 이후 버전) 형식|결과 변환(서버에서 클라이언트로)|매개 변수 변환(클라이언트에서 서버로)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|DateTime|Date|정상|정상|  
|DBTYPE_DBTIMESTAMP|||시간 필드가 0으로 설정됩니다.|시간 필드가 0이 아닌 경우 문자열 잘림이 발생 하 여 IRowsetChange가 실패 합니다.|  
|DBTYPE_DBTIME||Time(0)|정상|정상|  
|DBTYPE_DBTIMESTAMP|||날짜 필드가 현재 날짜로 설정됩니다.|소수 자릿수 초가 0이 아닌 경우 문자열 잘림이 발생 하 여 IRowsetChange가 실패 합니다.<br /><br /> 날짜는 무시됩니다.|  
|DBTYPE_DBTIME||Time(7)|실패-시간 리터럴이 잘못 되었습니다.|정상|  
|DBTYPE_DBTIMESTAMP|||실패-시간 리터럴이 잘못 되었습니다.|정상|  
|DBTYPE_DBTIMESTAMP||Datetime2 (3)|정상|정상|  
|DBTYPE_DBTIMESTAMP||Datetime2 (7)|정상|정상|  
|DBTYPE_DBDATE|Smalldatetime|Date|정상|정상|  
|DBTYPE_DBTIMESTAMP|||시간 필드가 0으로 설정됩니다.|시간 필드가 0이 아닌 경우 문자열 잘림 때문에 IRowsetChange가 실패 합니다.|  
|DBTYPE_DBTIME||Time(0)|정상|정상|  
|DBTYPE_DBTIMESTAMP|||날짜 필드가 현재 날짜로 설정됩니다.|소수 자릿수 초가 0이 아닌 경우 문자열 잘림이 발생 하 여 IRowsetChange가 실패 합니다.<br /><br /> 날짜는 무시됩니다.|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|정상|정상|  
  
 표에서 정상은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 동작하는 경우 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)](또는 이후 버전)에서도 계속 동작함을 의미합니다.  
  
 다음과 같은 일반적인 스키마 변경 내용만 고려됩니다.  
  
-   논리적으로 애플리케이션에 날짜 또는 시간 값만 필요한 경우 새 형식을 사용합니다. 그러나 이전에는 개별 날짜 및 시간 형식을 사용할 수 없었으므로 애플리케이션에서 `datetime` 또는 `smalldatetime`을 사용해야 했습니다.  
  
-   초 소수 부분 자릿수를 늘리거나 정확도를 높이기 위해 새 형식을 사용합니다.  
  
-   `datetime2`날짜 및 시간에 대 한 기본 데이터 형식 이므로로 전환 합니다.  
  
 ICommandWithParameters:: GetParameterInfo 또는 스키마 행 집합을 통해 얻은 서버 메타 데이터를 사용 하 여 ICommandWithParameters:: SetParameterInfo를 통해 매개 변수 형식 정보를 설정 하는 응용 프로그램은 원본 형식의 문자열 표현이 대상 형식의 문자열 표현 보다 큰 클라이언트를 변환 하는 동안 실패 합니다. 예를 들어 클라이언트 바인딩에서 DBTYPE_DBTIMESTAMP를 사용 하 고 서버 열이 날짜인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client는 값을 "yyyy-mm-dd-mm hh: mm: ss"로 변환 하지만 서버 메타 데이터는로 반환 됩니다 `nvarchar(10)` . 결과 오버플로는 DBSTATUS_E_CATCONVERTVALUE를 유발합니다. 행 집합 메타 데이터는 결과 집합 메타 데이터에서 설정 되므로 IRowsetChange으로 데이터를 변환 하는 경우에도 유사한 문제가 발생 합니다.  
  
### <a name="parameter-and-rowset-metadata"></a>매개 변수 및 행 집합 메타데이터  
 이 섹션에서는 이전 버전의 Native Client를 사용 하 여 컴파일된 클라이언트의 매개 변수, 결과 열 및 스키마 행 집합에 대 한 메타 데이터에 대해 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 합니다.  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 DBPARAMINFO 구조는 *Prgparaminfo* 매개 변수를 통해 다음 정보를 반환 합니다.  
  
|매개 변수 유형|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19, 21.27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26, 28.34|~0|~0|  
  
 이러한 값 범위 중 일부는 연속되지 않습니다. 예를 들어 8, 10..16에서는 9가 누락되어 있습니다. 이러한 경우는 소수 부분 자릿수가 0보다 커서 소수점을 추가했을 때 발생합니다.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 다음 열이 반환됩니다.  
  
|열 유형|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|date|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19, 21.27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26, 28.34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 구조는 다음 정보를 반환합니다.  
  
|매개 변수 유형|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19, 21.27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26, 28.34|~0|~0|  
  
### <a name="schema-rowsets"></a>스키마 행 집합  
 이 섹션에서는 새 데이터 형식의 매개 변수, 결과 열 및 스키마 행 집합에 대한 메타데이터에 대해 설명합니다. 이 정보는 클라이언트 공급자가 Native Client 이전의 도구를 사용 하 여 개발 된 경우에 유용 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
#### <a name="columns-rowset"></a>COLUMNS 행 집합  
 날짜/시간 형식에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|date|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16, 20.32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|Datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19, 21.27|38, 42.54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26, 28.34|52, 56.68|NULL|  
  
#### <a name="procedure_parameters-rowset"></a>PROCEDURE_PARAMETERS 행 집합  
 날짜/시간 형식에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|date|DBTYPE_WSTR|10|20|date|  
|time|DBTYPE_WSTR|8, 10..16|16, 20.32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|Datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|Datetime|  
|datetime2|DBTYPE_WSTR|19, 21.27|38, 42.54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26, 28.34|52, 56.68|datetimeoffset|  
  
#### <a name="provider_types-rowset"></a>PROVIDER_TYPES 행 집합  
 날짜/시간 형식에 대해 다음 행이 반환됩니다.  
  
|형식 -><br /><br /> 열|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>하위 수준 서버 동작  
 이전 버전의 서버에 연결 된 경우에는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 새 서버 유형 이름 (예: ICommandWithParameters:: SetParameterInfo 또는 ITableDefinition:: CreateTable)을 사용 하려고 하면 DB_E_BADTYPENAME 발생 합니다.  
  
 새 형식이 형식 이름을 사용하지 않고 매개 변수 또는 결과에 바인딩되고, 새 형식을 사용하여 서버 유형을 암시적으로 지정하거나 서버 유형에서 클라이언트 유형으로의 유효한 변환이 없는 경우 DB_E_ERRORSOCCURRED가 반환되고 DBBINDSTATUS_UNSUPPORTED_CONVERSION이 Execute에 사용된 접근자에 대한 바인딩 상태로 설정됩니다.  
  
 버퍼 유형에서 연결의 서버 버전의 서버 유형으로 지원되는 클라이언트 변환이 있는 경우 모든 클라이언트 버퍼 유형을 사용할 수 있습니다. 이 컨텍스트에서 *서버 형식은* ICommandWithParameters:: SetParameterInfo로 지정 된 형식이 나 ICommandWithParameters:: SetParameterInfo가 호출 되지 않은 경우 버퍼 형식에 의해 암시 된 형식을 의미 합니다. 이는 하위 수준 서버에서, 또는 DataTypeCompatibility=80일 때 지원되는 서버 유형에 대한 클라이언트 변환이 성공할 경우 DBTYPE_DBTIME2 및 DBTYPE_DBTIMESTAMPOFFSET을 사용할 수 있음을 의미합니다. 물론 서버 유형이 잘못된 경우 서버는 실제 서버 유형으로 암시적 변환을 수행하지 못하면 여전히 오류를 보고할 수 있습니다.  
  
## <a name="ssprop_init_datatypecompatibility-behavior"></a>SSPROP_INIT_DATATYPECOMPATIBILITY 동작  
 SSPROP_INIT_DATATYPECOMPATIBILITY을 SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000로 설정 하면 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 내용 ](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)에 설명 된 대로 새로운 날짜/시간 형식 및 관련 메타 데이터가 클라이언트에 표시 됩니다 OLE DB 및 ODBC&#41;&#40;.  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind 비교  
 새 날짜/시간 형식은 날짜/시간 형식이 아니라 문자열 형식으로 표시되기 때문에 이러한 형식에 대해서는 모든 비교 연산자를 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
