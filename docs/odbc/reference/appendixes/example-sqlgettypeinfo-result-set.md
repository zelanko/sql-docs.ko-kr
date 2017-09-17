---
title: "SQLGetTypeInfo 결과 예 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b43138efe4c6540b12bbfeeb0185f61ad0e65861
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="example-sqlgettypeinfo-result-set"></a>SQLGetTypeInfo 결과 집합 예제
응용 프로그램이 호출 **SQLGetTypeInfo** 데이터 원본과 해당 데이터 형식 특성에서 지원 되는 데이터 유형을 확인 하려면. 다음 표에서에서 반환 된 결과 집합 예를 보여 줍니다. **SQLGetTypeInfo** SQL_CHAR, SQL_LONGVARCHAR, SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR, 및 SQL_INTERVAL_DAY_TO_SECOND 지 원하는 데이터 원본에 대 한 합니다.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"char"|SQL_CHAR|255|"'"|"'"|"길이"|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<Null >|SQL_TRUE|  
|"십진수"|SQL_DECIMAL|28|\<Null >|\<Null >|"precision,<br />scale "|SQL_TRUE|  
|"실제"|SQL_REAL|7|\<Null >|\<Null >|\<Null >|SQL_TRUE|  
|"datetime"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<Null >|SQL_TRUE|  
|"연도를 간격 YEAR()"|SQL_INTERVAL_YEAR|9|"'"|"'"|"precision"|SQL_TRUE|  
|"FRACTION(5) 간격 DAY()"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|"precision"|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<Null >|SQL_FALSE|\<Null >|"char"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<Null >|SQL_FALSE|\<Null >|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"십진수"|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"실제"|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<Null >|SQL_FALSE|\<Null >|"datetime"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<Null >|SQL_FALSE|\<Null >|"연도를 간격 YEAR()"|  
TERVAL_DAY_TO_SECOND * *|SQL_FALSE|SQL_PRED_BASIC|\<Null >|SQL_FALSE|\<Null >|"FRACTION(5) 간격 DAY()"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<Null >|\<Null >|SQL_CHAR|\<Null >|\<Null >|\<Null >|  
|**SQL_LONGVARCHAR**|\<Null >|\<Null >|SQL_LONGVARCHAR|\<Null >|\<Null >|\<Null >|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<Null >|10|\<Null >|  
|**SQL_REAL**|\<Null >|\<Null >|SQL_REAL|\<Null >|10|\<Null >|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<Null >|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<Null >|9|  
ERVAL_DAY_TO_SECOND * *|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<Null >|9|
