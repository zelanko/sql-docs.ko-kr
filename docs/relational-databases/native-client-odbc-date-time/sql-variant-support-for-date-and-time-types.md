---
title: 날짜 및 시간 형식에 대 한 sql_variant 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 442e6d486ed85a7f5d9d35a4ff347f84166aaec9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719735"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>날짜 및 시간 형식에 대한 sql_variant 지원
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  이 항목에서는 **sql_variant** 데이터 형식에서 향상된 날짜 및 시간 기능을 지원하는 방법에 대해 설명합니다.  
  
 열 특성 SQL_CA_SS_VARIANT_TYPE은 C 형식의 variant 결과 열을 반환하는 데 사용됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]IRD (구현 행 설명자)에서 변형 결과 열의 SQL 형식을 설정 하는 추가 특성인 SQL_CA_SS_VARIANT_SQL_TYPE를 소개 합니다. IPD(구현 매개 변수 설명자)에서 SQL_SS_VARIANT 형식으로 바인딩된 SQL_C_BINARY C 형식을 갖는 SQL 형식의 SQL_SS_TIME2 또는 SQL_SS_TIMESTAMPOFFSET 매개 변수를 지정하는 데에도 SQL_CA_SS_VARIANT_SQL_TYPE을 사용할 수 있습니다.  
  
 새 형식 SQL_SS_TIME2 및 SQL_SS_TIMESTAMPOFFSET는 SQLColAttribute로 설정할 수 있습니다. SQL_CA_SS_VARIANT_SQL_TYPE는 SQLGetDescField에서 반환 될 수 있습니다.  
  
 결과 열의 경우 드라이버에서는 variant를 날짜/시간 형식으로 변환합니다. 자세한 내용은 [SQL에서 C로 변환](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)을 참조 하세요. SQL_C_BINARY에 바인딩할 때 버퍼 길이는 SQL 형식에 해당 하는 구조체를 받을 수 있을 만큼 커야 합니다.  
  
 SQL_SS_TIME2 및 SQL_SS_TIMESTAMPOFFSET 매개 변수의 경우 드라이버에서는 아래 표에 설명된 대로 C 값을 **sql_variant** 값으로 변환합니다. 매개 변수가 SQL_C_BINARY로 바인딩되어 있고 서버 형식이 SQL_SS_VARIANT인 경우에는 애플리케이션에서 SQL_CA_SS_VARIANT_SQL_TYPE을 다른 SQL 형식으로 설정한 경우 외에는 이진 값으로 처리됩니다. 이 경우 SQL_CA_SS_VARIANT_SQL_TYPE이 우선 순위가 높습니다. 즉, SQL_CA_SS_VARIANT_SQL_TYPE이 설정된 경우 C 형식에서 variant SQL 형식을 추론하는 기본 동작이 무시됩니다.  
  
|C 형식|서버 유형|의견|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_TINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_STINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_SHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_SSHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_USHORT|int|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_LONG|int|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_SLONG|int|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_ULONG|bigint|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_SBIGINT|bigint|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_FLOAT|real|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_DOUBLE|float|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_UTINYINT|tinyint|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_BINARY|varbinary|SQL_CA_SS_VARIANT_SQL_TYPE이 설정되지 않습니다.|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> 소수 자릿수가 SQL_DESC_PRECISION( *DecimalDigits* 의 **SQLBindParameter**매개 변수)으로 설정됩니다.|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE= SQL_SS_TIMESTAMPOFFSET<br /><br /> 소수 자릿수가 SQL_DESC_PRECISION( *DecimalDigits* 의 **SQLBindParameter**매개 변수)으로 설정됩니다.|  
|SQL_C_TYPE_DATE|date|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|소수 자릿수가 SQL_DESC_PRECISION( *DecimalDigits* 의 **SQLBindParameter**매개 변수)으로 설정됩니다.|  
|SQL_C_NUMERIC|decimal|전체 자릿수가 SQL_DESC_PRECISION( *ColumnSize* 의 **SQLBindParameter**매개 변수)으로 설정됩니다.<br /><br /> 소수 자릿수가 SQL_DESC_SCALE(SQLBindParameter의 *DecimalDigits* 매개 변수)로 설정됩니다.|  
|SQL_C_SS_TIME2|time|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE이 무시됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;날짜 및 시간 기능 향상](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
