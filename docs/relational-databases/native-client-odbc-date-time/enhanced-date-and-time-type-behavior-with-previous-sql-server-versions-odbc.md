---
title: 향상 된 날짜 및 시간 형식을 이전 버전 SQL Server (ODBC)에 대 한 동작 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], enhanced behavior with earlier SQL Server versions
ms.assetid: cd4e137f-dc5e-4df7-bc95-51fe18c587e0
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2b3831355e3b3fa7dff3ab3a36a8d58da4ab35dc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc"></a>이전 버전 SQL Server에 대한 향상된 날짜 및 시간 형식 동작(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  이 항목에서는 향상된 날짜 및 시간 기능을 사용하는 클라이언트 응용 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]보다 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]와 통신할 경우 및 Microsoft Data Access Components, Windows Data Access Components 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]보다 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Native Client를 사용하는 클라이언트 응용 프로그램이 향상된 날짜 및 시간 기능을 지원하는 서버에 명령을 보낼 경우 예상되는 동작에 대해 설명합니다.  
  
## <a name="down-level-client-behavior"></a>하위 수준 클라이언트 동작  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]보다 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Native Client를 사용하여 컴파일된 클라이언트 응용 프로그램에서는 새로운 날짜/시간 형식을 nvarchar 열로 인식합니다. "데이터 형식:: 문자열 및 리터럴" 섹션에 설명 된 대로 열의 내용은 리터럴 표현을는 [ODBC 날짜 및 시간 기능 향상에 대 한 데이터 형식 지원](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)합니다. 열 크기는 열에 지정된 초 소수 부분 자릿수에 대한 최대 리터럴 길이입니다.  
  
 카탈로그 API는 클라이언트에 반환된 하위 수준 데이터 형식 코드(예: nvarchar)와 일관된 메타데이터 및 관련된 하위 수준 표현(예: 적절한 리터럴 형식)을 반환합니다. 그러나 반환되는 데이터 형식의 이름은 실제 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 형식 이름입니다.  
  
 SQLDescribeCol, SQLDescribeParam, SQGetDescField, 및 SQLColAttribute에서 반환 된 문 메타 데이터는 하위 수준 형식과 모든 측면을 형식 이름을 포함 하 여에서 일치 하는 메타 데이터를 반환 합니다. 이러한 하위 형식의 예로 **nvarchar**합니다.  
  
 하위 수준 클라이언트 응용 프로그램에 대해 실행 되는 경우는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (또는 이상) 날짜/시간에는 스키마 변경 내용에 형식을 적용 된 서버에 예상 되는 동작은 다음과 같습니다.  
  
|SQL Server 2005 형식|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (이상) 형식|ODBC 클라이언트 형식|결과 변환(SQL에서 C로 변환)|매개 변수 변환(C에서 SQL로 변환)|  
|--------------------------|----------------------------------------------|----------------------|------------------------------------|---------------------------------------|  
|날짜/시간|날짜|SQL_C_TYPE_DATE|확인|확인 (1)|  
|||SQL_C_TYPE_TIMESTAMP|시간 필드가 0으로 설정됩니다.|정상(2)<br /><br /> 시간 필드가 0 이외의 값이면 실패합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 작동합니다.|  
||Time(0)|SQL_C_TYPE_TIME|확인|확인 (1)|  
|||SQL_C_TYPE_TIMESTAMP|날짜 필드가 현재 날짜로 설정됩니다.|정상(2)<br /><br /> 날짜가 무시됩니다. 초 소수 부분이 0 이외의 값이면 실패합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 작동합니다.|  
||Time(7)|SQL_C_TIME|실패 - 시간 리터럴이 잘못되었습니다.|확인 (1)|  
|||SQL_C_TYPE_TIMESTAMP|실패 - 시간 리터럴이 잘못되었습니다.|확인 (1)|  
||Datetime2(3)|SQL_C_TYPE_TIMESTAMP|확인|확인 (1)|  
||Datetime2 (7)|SQL_C_TYPE_TIMESTAMP|확인|클라이언트 변환 시 값이 1/300초로 반올림됩니다.|  
|Smalldatetime|날짜|SQL_C_TYPE_DATE|확인|확인|  
|||SQL_C_TYPE_TIMESTAMP|시간 필드가 0으로 설정됩니다.|정상(2)<br /><br /> 시간 필드가 0 이외의 값이면 실패합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 작동합니다.|  
||Time(0)|SQL_C_TYPE_TIME|확인|확인|  
|||SQL_C_TYPE_TIMESTAMP|날짜 필드가 현재 날짜로 설정됩니다.|정상(2)<br /><br /> 날짜가 무시됩니다. 초 소수 부분이 0 이외의 값이면 실패합니다.<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 작동합니다.|  
||Datetime2(0)|SQL_C_TYPE_TIMESTAMP|확인|확인|  
  
## <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|1.|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 동작하는 경우 그보다 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서도 계속 동작합니다.|  
|2|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 작동한 응용 프로그램이 그보다 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 작동하지 않을 수 있습니다.|  
  
 여기서는 다음과 같이 일반적인 스키마 변경 사항만 고려되었습니다.  
  
-   논리적으로 응용 프로그램에 날짜 또는 시간 값만 필요한 경우 새 형식을 사용합니다. 그러나 이전에는 개별 날짜 및 시간 형식이 없었으므로 응용 프로그램에서 datetime 또는 smaledatetime을 사용해야 했습니다.  
  
-   초 소수 부분 자릿수를 늘리거나 정확도를 높이기 위해 새 형식을 사용합니다.  
  
-   datetime2가 선호하는 날짜 및 시간 데이터 형식이기 때문에 datetime2로 전환합니다.  
  
### <a name="column-metadata-returned-by-sqlcolumns-sqlprocedurecolumns-and-sqlspecialcolumns"></a>SQLColumns, SQLProcedureColumns 및 SQLSpecialColumns가 반환하는 열 메타데이터  
 날짜/시간 형식에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|date|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|TYPE_NAME|date|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|20|16, 20..32|16|16|38, 42..54|52, 56..68|  
|DECIMAL_DIGITS|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|CHAR_OCTET_LENGTH|NULL|NULL|NULL|NULL|NULL|NULL|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
  
 SQLSpecialColumns는 SQL_DATA_TYPE, SQL_DATETIME_SUB, CHAR_OCTET_LENGTH 또는 SS_DATA_TYPE을 반환하지 않습니다.  
  
### <a name="data-type-metadata-returned-by-sqlgettypeinfo"></a>SQLGetTypeInfo가 반환하는 데이터 형식 메타데이터  
 날짜/시간 형식에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|date|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULL|NULL|NULL|NULL|NULL|NULL|  
|LOCAL_TYPE_NAME|date|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|NUM_PREC_RADIX|NULL|NULL|NULL|NULL|NULL|NULL|  
|INTERVAL_PRECISION|NULL|NULL|NULL|NULL|NULL|NULL|  
|USERTYPE|0|0|12|22|0|0|  
  
## <a name="down-level-server-behavior"></a>하위 수준 서버 동작  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]보다 이전 버전의 서버 인스턴스에 연결되어 있는 경우 새로운 서버 형식 또는 관련된 메타데이터 코드 및 설명자 필드를 사용하려고 하면 SQL_ERROR가 반환됩니다. SQLSTATE HY004 및 "연결에서 서버 버전의 SQL 데이터 형식이 잘못되었습니다."라는 메시지가 포함된 진단 레코드 또는 07006 및 "제한된 데이터 형식 특성을 위반했습니다."라는 메시지가 포함된 진단 레코드가 생성됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [날짜 및 시간 기능 향상 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
