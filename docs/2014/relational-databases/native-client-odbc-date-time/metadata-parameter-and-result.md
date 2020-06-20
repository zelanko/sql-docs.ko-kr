---
title: 매개 변수 및 결과 메타 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- metadata [ODBC]
ms.assetid: 1518e6e5-a6a8-4489-b779-064c5624df53
author: rothja
ms.author: jroth
ms.openlocfilehash: 94cce7c3debc467d2c06f97d9a390455245f5606
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020148"
---
# <a name="parameter-and-result-metadata"></a>매개 변수 및 결과 메타데이터
  이 항목에서는 날짜 및 시간 데이터 형식에 대해 IPD(구현 매개 변수 설명자) 및 IRD(구현 행 설명자) 필드에서 반환되는 내용에 대해 설명합니다.  
  
## <a name="information-returned-in-ipd-fields"></a>IPD 필드에서 반환되는 정보  
 다음은 IPD 필드에서 반환되는 정보입니다.  
  
|매개 변수 유형|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8, 10 ... 16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8, 10 ... 16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_TYPE|SQL_TYPE_DATE|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|`date`|`time`|IRD의 `smalldatetime`, IPD의 `datetime2`|IRD의 `datetime`, IPD의 `datetime2`|`datetime2`|datetimeoffset|  
|SQL_CA_SS_VARIANT_TYPE|SQL_C_TYPE_DATE|SQL_C_TYPE_BINARY|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_BINARY|  
|SQL_CA_SS_VARIANT_SQL_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_CA_SS_SERVER_TYPE|해당 없음|해당 없음|SQL_SS_TYPE_SMALLDATETIME|SQL_SS_TYPE_DATETIME|SQL_SS_TYPE_DEFAULT|해당 없음|  
  
 값 범위가 연속되지 않을 수도 있습니다. 예를 들어 8,10..16에서는 9가 누락되어 있습니다. 이러한 경우는 소수 부분 자릿수가 0보다 커서 소수점을 추가했을 때 발생합니다.  
  
 `datetime2`는 드라이버에서 모든 `smalldatetime` 값을 서버에 전달하기 위한 일반 형식으로 사용되므로 `datetime` 및 `SQL_TYPE_TIMESTAMP`의 typename으로 반환됩니다.  
  
 SQL_CA_SS_VARIANT_SQL_TYPE은 새 설명자 필드입니다. 이 필드는 애플리케이션에서 `sqlvariant`(SQL_SSVARIANT) 열 및 매개 변수와 연관된 값 형식을 지정하는 데 사용하기 위해 IRD 및 IPD에 추가되었습니다.  
  
 SQL_CA_SS_SERVER_TYPE은 새로운 IPD 전용 필드로, 애플리케이션에서 SQL_TYPE_TYPETIMESTAMP나 C 형식의 SQL_C_TYPE_TIMESTAMP를 갖는 SQL_SS_VARIANT로 바인딩된 매개 변수 값을 서버로 전송하는 방법을 제어하는 데 사용할 수 있습니다. SQLExecute 또는 SQLExecDirect가 호출 될 때 SQL_DESC_CONCISE_TYPE가 SQL_TYPE_TIMESTAMP SQL_SS_VARIANT 이거나 C 형식이 SQL_C_TYPE_TIMESTAMP 인 경우 SQL_CA_SS_SERVER_TYPE 값은 다음과 같이 매개 변수 값의 TDS (tabular data stream) 형식을 결정 합니다.  
  
|SQL_CA_SS_SERVER_TYPE 값|SQL_DESC_PRECISION에 대한 유효한 값|SQL_DESC_LENGTH에 대한 유효한 값|TDS 유형|  
|----------------------------------------|-------------------------------------------|----------------------------------------|--------------|  
|SQL_SS_TYPE_DEFAULT|0..7|19, 21..27|`datetime2`|  
|SQL_SS_TYPE_SMALLDATETIME|0|19|`smalldatetime`|  
|SQL_SS_TYPE_DATETIME|3|23|`datetime`|  
  
 SQL_CA_SS_SERVER_TYPE의 기본 설정은 SQL_SS_TYPE_DEFAULT입니다. SQL_DESC_PRECISION 및 SQL_DESC_LENGTH 설정의 유효성은 위 표에 설명된 대로 SQL_CA_SS_SERVER_TYPE 설정으로 검사됩니다. 이 유효성 검사에 실패하면 SQL_ERROR가 반환되고 SQLState 07006 및 "제한된 데이터 형식 특성을 위반했습니다"라는 메시지가 포함된 진단 레코드가 기록됩니다. SQL_CA_SS_SERVER_TYPE이 SQL_SS_TYPE DEFAULT 이외의 값으로 설정되고 DESC_CONCISE_TYPE이 SQL_TYPE_TIMESTAMP가 아닌 경우에도 이 오류가 반환됩니다. 다음과 같이 설명자 일관성 검사가 발생할 때 이러한 유효성 검사가 수행됩니다.  
  
-   SQL_DESC_DATA_PTR이 변경된 경우  
  
-   준비 또는 실행 시간에 SQLExecute, SQLExecDirect, SQLSetPos 또는 SQLBulkOperations를 호출하는 경우  
  
-   지연 된 준비를 사용 하지 않도록 설정 하 여 SQLPrepare를 호출 하거나 준비 되었지만 실행 되지 않은 문에 대해 SQLNumResultCols, SQLDescribeCol 또는 SQLDescribeParam를 호출 하 여 응용 프로그램에서 지연 되지 않은 준비를 강제로 실행 하는 경우  
  
 SQLSetDescField를 호출 하 여 SQL_CA_SS_SERVER_TYPE를 설정 하는 경우 해당 값은 SQL_SS_TYPE_DEFAULT, SQL_SS_TYPE_SMALLDATETIME 또는 SQL_SS_TYPE_DATETIME 이어야 합니다. 그렇지 않으면 SQL_ERROR가 반환되고 SQLState HY092 및 "잘못된 특성/옵션 식별자입니다"라는 메시지가 포함된 진단 레코드가 기록됩니다.  
  
 SQL_CA_SS_SERVER_TYPE 특성은 `datetime` 및 `smalldatetime`에서 지원되지만 `datetime2`에서는 지원되지 않는 기능에 종속된 애플리케이션에서 사용할 수 있습니다. 예를 들어, 및 `datetime2` `dateadd` **datediif** 함수를 사용 해야 하는 반면 `datetime` 및는 `smalldatetime` 산술 연산자를 허용 합니다. 이 속성은 대부분의 애플리케이션에서 사용할 필요가 없으며 사용해서는 안 됩니다.  
  
## <a name="information-returned-in-ird-fields"></a>IRD 필드에서 반환되는 정보  
 다음은 IRD 필드에서 반환되는 정보입니다.  
  
|열 유형|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8, 10 ... 16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_DISPLAY_SIZE|10|8, 10 ... 16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8, 10 ... 16|16|2|19, 21..27|26, 28..34|  
|SQL_DESC_LITERAL_PREFIX|'|'|'|'|'|'|  
|SQL_DESC_LITERAL_SUFFIX|'|'|'|'|'|'|  
|SQL_DESC_LOCAL_TYPE_NAME|`date`|`time`|`smalldatetime`|`datetime`|`datetime2`|datetimeoffset|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|SQL_DESC_TYPE|SQL_DATETIME|SQL_SS_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|`date`|`time`|`smalldatetime`|`datetime`|`datetime2`|datetimeoffset|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;메타 데이터](../../database-engine/dev-guide/metadata-odbc.md)  
  
  
