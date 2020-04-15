---
title: 예제 SQLGetTypeInfo 결과 집합 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5cf62f8a95f4c91095c21a6d603317fe1f73500
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307014"
---
# <a name="example-sqlgettypeinfo-result-set"></a>SQLGetTypeInfo 결과 집합의 예제
응용 프로그램은 **SQLGetTypeInfo를** 호출하여 데이터 원본에서 지원되는 데이터 형식과 해당 데이터 형식의 특성을 결정합니다. 다음 표에서는 SQL_CHAR, SQL_LONGVARCHAR, SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR 및 SQL_INTERVAL_DAY_TO_SECOND 지원하는 데이터 원본에 대해 **SQLGetTypeInfo에서** 반환한 샘플 결과 집합을 보여 준다.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"차"|SQL_CHAR|255|"'"|"'"|"길이"|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<널>|SQL_TRUE|  
|"소수점"|SQL_DECIMAL|28|\<널>|\<널>|"정밀도,<br />"라고 말했다.|SQL_TRUE|  
|"진짜"|SQL_REAL|7|\<널>|\<널>|\<널>|SQL_TRUE|  
|"날짜 시간"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<널>|SQL_TRUE|  
|"인터벌 연도() 년"|SQL_INTERVAL_YEAR|9|"'"|"'"|"정밀도"|SQL_TRUE|  
|"간격 일() ~ 분수(5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|"정밀도"|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<널>|SQL_FALSE|\<널>|"차"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<널>|SQL_FALSE|\<널>|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"소수점"|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"진짜"|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<널>|SQL_FALSE|\<널>|"날짜 시간"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<널>|SQL_FALSE|\<널>|"인터벌 연도() 년"|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<널>|SQL_FALSE|\<널>|"간격 일() ~ 분수(5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<널>|\<널>|SQL_CHAR|\<널>|\<널>|\<널>|  
|**SQL_LONGVARCHAR**|\<널>|\<널>|SQL_LONGVARCHAR|\<널>|\<널>|\<널>|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<널>|10|\<널>|  
|**SQL_REAL**|\<널>|\<널>|SQL_REAL|\<널>|10|\<널>|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<널>|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<널>|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<널>|9|
