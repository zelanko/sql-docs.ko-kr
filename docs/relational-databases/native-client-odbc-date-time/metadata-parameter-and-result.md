---
title: 매개 변수 및 결과 메타데이터 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- metadata [ODBC]
ms.assetid: 1518e6e5-a6a8-4489-b779-064c5624df53
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ba66c950f25663dabc3c0c46f83a7589df300ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304094"
---
# <a name="metadata---parameter-and-result"></a>메타데이터 - 매개 변수 및 결과
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 날짜 및 시간 데이터 형식에 대해 IPD(구현 매개 변수 설명자) 및 IRD(구현 행 설명자) 필드에서 반환되는 내용에 대해 설명합니다.  
  
## <a name="information-returned-in-ipd-fields"></a>IPD 필드에서 반환되는 정보  
 다음은 IPD 필드에서 반환되는 정보입니다.  
  
|매개 변수 형식|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_TYPE|SQL_TYPE_DATE|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|**date**|**time**|IRD의 **작은 날짜 시간,** IPD에서 **날짜 시간2**|IRD의 **날짜 시간,** IPD의 **날짜 시간2**|**datetime2**|datetimeoffset|  
|SQL_CA_SS_VARIANT_TYPE|SQL_C_TYPE_DATE|SQL_C_TYPE_BINARY|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_BINARY|  
|SQL_CA_SS_VARIANT_SQL_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_CA_SS_SERVER_TYPE|해당 없음|해당 없음|SQL_SS_TYPE_SMALLDATETIME|SQL_SS_TYPE_DATETIME|SQL_SS_TYPE_DEFAULT|해당 없음|  
  
 값 범위가 연속되지 않을 수도 있습니다. 예를 들어 8,10..16에서는 9가 누락되어 있습니다. 이러한 경우는 소수 부분 자릿수가 0보다 커서 소수점을 추가했을 때 발생합니다.  
  
 **datetime2는** 드라이버가 서버에 모든 **SQL_TYPE_TIMESTAMP** 값을 전송하기 위한 공통 유형으로 사용하기 때문에 **smalldatetime** 및 **datetime의** 형식 이름으로 반환됩니다.  
  
 SQL_CA_SS_VARIANT_SQL_TYPE은 새 설명자 필드입니다. 이 필드는 응용 프로그램이 **sqlvariant(SQL_SSVARIANT)** 열 및 매개 변수와 관련된 값 형식을 지정할 수 있도록 IRD 및 IPD에 추가되었습니다.  
  
 SQL_CA_SS_SERVER_TYPE은 새로운 IPD 전용 필드로, 애플리케이션에서 SQL_TYPE_TYPETIMESTAMP나 C 형식의 SQL_C_TYPE_TIMESTAMP를 갖는 SQL_SS_VARIANT로 바인딩된 매개 변수 값을 서버로 전송하는 방법을 제어하는 데 사용할 수 있습니다. SQL_DESC_CONCISE_TYPE SQL_TYPE_TIMESTAMP(또는 SQL_SS_VARIANT C 형식이 SQL_C_TYPE_TIMESTAMP)인 경우, SQL_CA_SS_SERVER_TYPE 값은 다음과 같이 매개 변수 값의 테이블 형식 데이터 스트림(TDS) 형식을 결정합니다.  
  
|SQL_CA_SS_SERVER_TYPE 값|SQL_DESC_PRECISION에 대한 유효한 값|SQL_DESC_LENGTH에 대한 유효한 값|TDS 유형|  
|----------------------------------------|-------------------------------------------|----------------------------------------|--------------|  
|SQL_SS_TYPE_DEFAULT|0..7|19, 21..27|**datetime2**|  
|SQL_SS_TYPE_SMALLDATETIME|0|19|**smalldatetime**|  
|SQL_SS_TYPE_DATETIME|3|23|**datetime**|  
  
 SQL_CA_SS_SERVER_TYPE의 기본 설정은 SQL_SS_TYPE_DEFAULT입니다. SQL_DESC_PRECISION 및 SQL_DESC_LENGTH 설정의 유효성은 위 표에 설명된 대로 SQL_CA_SS_SERVER_TYPE 설정으로 검사됩니다. 이 유효성 검사에 실패하면 SQL_ERROR가 반환되고 SQLState 07006 및 "제한된 데이터 형식 특성을 위반했습니다"라는 메시지가 포함된 진단 레코드가 기록됩니다. SQL_CA_SS_SERVER_TYPE이 SQL_SS_TYPE DEFAULT 이외의 값으로 설정되고 DESC_CONCISE_TYPE이 SQL_TYPE_TIMESTAMP가 아닌 경우에도 이 오류가 반환됩니다. 다음과 같이 설명자 일관성 검사가 발생할 때 이러한 유효성 검사가 수행됩니다.  
  
-   SQL_DESC_DATA_PTR이 변경된 경우  
  
-   준비 또는 실행 시간에 SQLExecute, SQLExecDirect, SQLSetPos 또는 SQLBulkOperations를 호출하는 경우  
  
-   응용 프로그램이 지연된 준비를 사용하지 않도록 설정하거나 SQLNumResultCols, SQLDescribeCol 또는 SQLDescribeParam을 호출하여 준비되었지만 실행되지 않은 문을 호출하여 지연되지 않은 준비를 강제하는 경우.  
  
 sqlSetDescField에 대한 호출로 SQL_CA_SS_SERVER_TYPE 설정하면 해당 값은 SQL_SS_TYPE_DEFAULT, SQL_SS_TYPE_SMALLDATETIME 또는 SQL_SS_TYPE_DATETIME 값이어야 합니다. 그렇지 않으면 SQL_ERROR가 반환되고 SQLState HY092 및 "잘못된 특성/옵션 식별자입니다"라는 메시지가 포함된 진단 레코드가 기록됩니다.  
  
 SQL_CA_SS_SERVER_TYPE 특성은 **datetime** 및 **smalldatetime에서**지원하는 기능에 종속된 응용 프로그램에서 사용할 수 있지만 **datetime2는**사용할 수 없습니다. 예를 들어 **datetime2에는** **dateadd** 함수와 **날짜함수함수를** 사용해야 하는 반면 **날짜 시간과** 작은 **datetime은** 산술 연산자도 허용합니다. 이 속성은 대부분의 애플리케이션에서 사용할 필요가 없으며 사용해서는 안 됩니다.  
  
## <a name="information-returned-in-ird-fields"></a>IRD 필드에서 반환되는 정보  
 다음은 IRD 필드에서 반환되는 정보입니다.  
  
|열 유형|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_DISPLAY_SIZE|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8,10..16|16|2|19, 21..27|26, 28..34|  
|SQL_DESC_LITERAL_PREFIX|'|'|'|'|'|'|  
|SQL_DESC_LITERAL_SUFFIX|'|'|'|'|'|'|  
|SQL_DESC_LOCAL_TYPE_NAME|**date**|**time**|**smalldatetime**|**datetime**|**datetime2**|datetimeoffset|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|SQL_DESC_TYPE|SQL_DATETIME|SQL_SS_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|**date**|**time**|**smalldatetime**|**datetime**|**datetime2**|datetimeoffset|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;메타데이터](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
  
  
