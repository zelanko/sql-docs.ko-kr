---
title: 날짜 및 시간과 스키마 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f44cb40d8f40427d0a18b1d3eee7dd084281985e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47677466"
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>메타데이터 - 날짜 및 시간과 스키마 행 집합
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  이 항목에서는 COLUMNS 및 PROCEDURE_PARAMETERS 행 집합에 대한 정보를 제공합니다. 이 정보는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에 새로 추가된 향상된 OLE DB 날짜 및 시간 기능과 관련이 있습니다.  
  
## <a name="columns-rowset"></a>COLUMNS 행 집합  
 날짜/시간 형식에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|날짜|DBTYPE_DBDATE|지우기|0|  
|Time|DBTYPE_DBTIME2|Set|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|지우기|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|지우기|3|  
|Datetime2|DBTYPE_DBTIMESTAMP|Set|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|Set|0..7|  
  
 COLUMN_FLAGS에서 날짜/시간 형식에 대해 DBCOLUMNFLAGS_ISFIXEDLENGTH는 항상 true이지만 다음과 같은 플래그는 항상 false입니다.  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 나머지 플래그(DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE 및 DBCOLUMNFLAGS_WRITEUNKNOWN)는 열이 정의되는 방법에 따라 설정될 수 있습니다.  
  
 새 플래그 DBCOLUMNFLAGS_SS_ISVARIABLESCALE은 응용 프로그램에서 DATA_TYPE이 DBTYPE_DBTIMESTAMP인 열의 서버 유형을 확인할 수 있도록 COLUMN_FLAGS에 제공됩니다. 서버 유형을 확인하려면 DATETIME_PRECISION도 사용해야 합니다.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 서버에 연결된 경우에만 유효합니다. 하위 수준 서버에 연결된 경우에는 DBCOLUMNFLAGS_SS_ISFIXEDSCALE이 정의되지 않습니다.  
  
## <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS 행 집합  
 DATA_TYPE에는 COLUMNS 스키마 행 집합과 동일한 값이 포함되고 TYPE_NAME에는 서버 유형이 포함됩니다.  
  
 새 열 SS_DATETIME_PRECISION은 COLUMNS 행 집합과 유사한 DATETIME_PRECISION에서처럼 형식의 전체 자릿수를 반환하기 위해 추가되었습니다.  
  
## <a name="providertypes-rowset"></a>PROVIDER_TYPES 행 집합  
 날짜/시간 형식에 대해 다음 행이 반환됩니다.  
  
|형식 -><br /><br /> Column|날짜|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|날짜|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|소수 자릿수|NULL|NULL|소수 자릿수|소수 자릿수|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|날짜|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE(다음 중 하나에 해당하지 않을 경우)<br /><br /> 하위 수준 서버에 연결된 클라이언트입니다.<br /><br /> 데이터 형식 호환성 연결 속성이 80과 동일한 호환성 수준을 지정합니다.|VARIANT_TRUE(다음 중 하나에 해당하지 않을 경우)<br /><br /> 하위 수준 서버에 연결된 클라이언트입니다.<br /><br /> 데이터 형식 호환성 연결 속성이 80과 동일한 호환성 수준을 지정합니다.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB는 numeric 및 decimal 형식의 MINIMUM_SCALE 및 MAXIMUM_SCALE만 정의하므로 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서는 time, datetime2 및 datetimeoffset에 이러한 열을 사용하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [메타 데이터 &#40;OLE DB&#41;](http://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
  
  
