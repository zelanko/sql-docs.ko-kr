---
description: 메타 데이터-SQL Server Native Client의 날짜 및 시간 및 스키마 행 집합
title: 날짜 및 시간 및 스키마 행 집합
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 360b3ea7b6fe4957ba66044ec540fe050f43abfb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97433633"
---
# <a name="metadata---date-and-time-and-schema-rowsets-in-sql-server-native-client"></a>메타 데이터-SQL Server Native Client의 날짜 및 시간 및 스키마 행 집합
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  이 항목에서는 COLUMNS 및 PROCEDURE_PARAMETERS 행 집합에 대한 정보를 제공합니다. 이 정보는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에 새로 추가된 향상된 OLE DB 날짜 및 시간 기능과 관련이 있습니다.  
  
## <a name="columns-rowset"></a>COLUMNS 행 집합  
 날짜/시간 형식에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|date|DBTYPE_DBDATE|지우기|0|  
|time|DBTYPE_DBTIME2|설정|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|지우기|0|  
|Datetime|DBTYPE_DBTIMESTAMP|지우기|3|  
|datetime2|DBTYPE_DBTIMESTAMP|설정|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|설정|0..7|  
  
 COLUMN_FLAGS에서 날짜/시간 형식에 대해 DBCOLUMNFLAGS_ISFIXEDLENGTH는 항상 true이지만 다음과 같은 플래그는 항상 false입니다.  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 나머지 플래그(DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE 및 DBCOLUMNFLAGS_WRITEUNKNOWN)는 열이 정의되는 방법에 따라 설정될 수 있습니다.  
  
 새 플래그 DBCOLUMNFLAGS_SS_ISVARIABLESCALE은 애플리케이션에서 DATA_TYPE이 DBTYPE_DBTIMESTAMP인 열의 서버 유형을 확인할 수 있도록 COLUMN_FLAGS에 제공됩니다. 서버 유형을 확인하려면 DATETIME_PRECISION도 사용해야 합니다.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 서버에 연결된 경우에만 유효합니다. 하위 수준 서버에 연결된 경우에는 DBCOLUMNFLAGS_SS_ISFIXEDSCALE이 정의되지 않습니다.  
  
## <a name="procedure_parameters-rowset"></a>PROCEDURE_PARAMETERS 행 집합  
 DATA_TYPE에는 COLUMNS 스키마 행 집합과 동일한 값이 포함되고 TYPE_NAME에는 서버 유형이 포함됩니다.  
  
 새 열 SS_DATETIME_PRECISION은 COLUMNS 행 집합과 유사한 DATETIME_PRECISION에서처럼 형식의 전체 자릿수를 반환하기 위해 추가되었습니다.  
  
## <a name="provider_types-rowset"></a>PROVIDER_TYPES 행 집합  
 날짜/시간 형식에 대해 다음 행이 반환됩니다.  
  
|형식 -><br /><br /> 열|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|소수 자릿수|NULL|NULL|소수 자릿수|소수 자릿수|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE(다음 중 하나에 해당하지 않을 경우)<br /><br /> 하위 수준 서버에 연결된 클라이언트입니다.<br /><br /> 데이터 형식 호환성 연결 속성이 80과 동일한 호환성 수준을 지정합니다.|VARIANT_TRUE(다음 중 하나에 해당하지 않을 경우)<br /><br /> 하위 수준 서버에 연결된 클라이언트입니다.<br /><br /> 데이터 형식 호환성 연결 속성이 80과 동일한 호환성 수준을 지정합니다.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB는 numeric 및 decimal 형식의 MINIMUM_SCALE 및 MAXIMUM_SCALE만 정의하므로 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서는 time, datetime2 및 datetimeoffset에 이러한 열을 사용하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [메타데이터&#40;OLE DB&#41;](./data-type-support-for-ole-db-date-and-time-improvements.md)  
  
