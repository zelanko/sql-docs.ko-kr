---
title: 카탈로그 메타 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- metadata [ODBC]
- catalog metadata [ODBC]
ms.assetid: b82665be-8cb1-4ad3-ac15-2e590bdc1815
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 783843e9bc25b0f6f1771fe7459de85b8cb56431
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705450"
---
# <a name="catalog-metadata"></a>카탈로그 메타데이터
  이 항목에서는 `SQLColumns` 및 `SQLProcedureColumns`에서 반환하는 열 메타데이터와 `SQLGetTypeInfo`에서 반환하는 데이터 형식 메타데이터에 대해 설명합니다.  
  
## <a name="remarks"></a>설명  
 날짜/시간 형식에 대해 `SQLColumns` 및 `SQLProcedureColumns`에서 다음 열 값이 반환됩니다.  
  
|매개 변수 유형|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8, 10 ... 16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|6|10|16|16|16|20|  
|DECIMAL_DIGITS|0|0..7|0|3|1.7|1.7|  
|SQL_DATA_TYPE|SQL_DATETIME|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TYPE_TIMESTAMPOFFSET|  
|SQL_DATETIME_SUB|SQL_CODE_DATE|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|  
|CHAR_OCTET_LENGTH|NULL|NULL|NULL|NULL|NULL|NULL|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
  
 날짜/시간 형식에 대해 `SQLGetTypeInfo`에서 다음 열 값이 반환됩니다.  
  
|매개 변수 유형|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|소수 자릿수|NULL|NULL|소수 자릿수|소수 자릿수|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULL|NULL|NULL|NULL|NULL|NULL|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|0|0|0|3|0|0|  
|MAXIMUM_SCALE|0|7|0|3|7|7|  
|SQL_DATA_TYPE|SQL_DATETIME|SQL_SS_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TYPE_TIMESTAMPOFFSET|  
|SQL_DATETIME_SUB|SQL_CODE_DATE|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|  
|NUM_PREC_RADIX|NULL|NULL|NULL|NULL|NULL|NULL|  
|INTERVAL_PRECISION|NULL|NULL|NULL|NULL|NULL|NULL|  
|USERTYPE|0|0|12|22|0|0|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;메타 데이터](../../database-engine/dev-guide/metadata-odbc.md)  
  
  
