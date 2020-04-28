---
title: 열 크기 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07b6151c723cb5e05189791100338e9e343c28aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306584"
---
# <a name="column-size"></a>열 크기
숫자 데이터 형식의 열 또는 매개 변수 크기는 열 또는 매개 변수의 데이터 형식에 사용 되는 최대 자릿수 또는 데이터의 전체 자릿수로 정의 됩니다. 문자 형식의 경우 데이터 문자 길이입니다. binary 데이터 형식의 경우 열 크기는 데이터의 길이 (바이트)로 정의 됩니다. Time, timestamp 및 all interval 데이터 형식의 경우이 데이터의 문자 표현에 있는 문자 수입니다. 각 간결한 SQL 데이터 형식에 대해 정의 된 열 크기는 다음 표에 나와 있습니다.  
  
|SQL 유형 식별자|열 크기|  
|-------------------------|-----------------|  
|모든 문자 형식 [a], [b]|SQL_DESC_LENGTH 설명자 필드에 포함 된 열 또는 매개 변수의 문자에서 정의 된 또는 최대 열 크기입니다. 예를 들어 CHAR (10)로 정의 된 싱글바이트 문자 열의 열 크기는 10입니다.|  
|SQL_DECIMAL SQL_NUMERIC|정의 된 자릿수입니다. 예를 들어 숫자 (10, 3)로 정의 된 열의 전체 자릿수는 10입니다.|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19 (부호 있는 경우) 또는 20 (unsigned 인 경우)|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|모든 이진 형식 [a], [b]|열 또는 매개 변수의 정의 또는 최대 길이 (바이트)입니다. 예를 들어 BINARY (10)로 정의 된 열의 길이는 10입니다.|  
|SQL_TYPE_DATE [c]|10 ( *yyyy-mm-dd* 형식의 문자 수)|  
|SQL_TYPE_TIME [c]|8 ( *hh-mm-ss* 형식의 문자 수) 또는 9 + *s* ( *hh: mm: ss*[. fff ...] 형식의 문자 수)입니다. 여기서 *s* 는 초 전체 자릿수입니다.|  
|SQL_TYPE_TIMESTAMP|16 ( *yyyy-mm-dd hh: mm* 형식의 문자 수)<br /><br /> 19 ( *yyyy-mm-dd* *hh: mm: ss* 형식의 문자 수)<br /><br /> 또는<br /><br /> 20 + *s* ( *yyyy-mm-dd hh: mm: ss*[. fff ...] 형식의 문자 수)입니다. 여기서 *s* 는 초 전체 자릿수입니다.|  
|SQL_INTERVAL_SECOND|여기서 *p* 는 간격의 선행 전체 자릿수이 고 *s* 는 초 전체 자릿수, *p* ( *s*= 0) 또는 *p*+*s*+ 1 ( *s*>0)입니다. 2|  
|SQL_INTERVAL_DAY_TO_SECOND|여기서 *p* 는 간격 선행 전체 자릿수이 고,은 초 전체 자릿수, 9 *+ p* ( *s*= 0) 또는 10 +*p*+*s* ( *s*>0) 인 *경우입니다.* 2|  
|SQL_INTERVAL_HOUR_TO_SECOND|여기서 *p* 는 간격 선행 전체 자릿수이 *고은* 초 전체 자릿수, 6 +*p* ( *s*= 0) 또는 7 +*p*+*s* ( *s*>0)입니다. 2|  
|SQL_INTERVAL_MINUTE_TO_SECOND|여기서 *p* 는 간격 선행 전체 자릿수이 *고은* 초 전체 자릿수, 3 +*p* ( *s*= 0) 또는 4 +*p*+*s* ( *s*>0)입니다. 2|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*. 여기서 *p* 는 간격의 선행 전체 자릿수입니다. 2|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*, 여기서 *p* 는 간격 선행 전체 자릿수입니다. 2|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*. 여기서 *p* 는 간격 선행 전체 자릿수입니다. 2|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*, 여기서 *p* 는 간격 선행 전체 자릿수입니다. 2|  
|SQL_GUID|36 ( *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* 형식의 문자 수)|  
  
 [a] odbc 2.0 드라이버에서 **SQLSetParam** 를 호출 하는 odbc 1.0 응용 프로그램의 경우, odbc 1.0 드라이버에서 **SQLBindParameter** 를 호출 하는 odbc 2.0 응용 \*프로그램의 경우, *StrLen_or_IndPtr* 가 SQL_LONGVARCHAR 또는 SQL_LONGVARBINARY 유형에 대해 SQL_DATA_AT_EXEC 되는 경우 *columnsize* 는이 표에 정의 된 전체 자릿수가 아니라 전송할 데이터의 전체 길이로 설정 해야 합니다.  
  
 [b] 드라이버에서 변수 형식의 열 또는 매개 변수 길이를 확인할 수 없는 경우 SQL_NO_TOTAL 반환 합니다.  
  
 [c]이 데이터 형식에 대해 **SQLBindParameter** 의 *columnsize* 인수는 무시 됩니다.  
  
 [d] 간격 데이터 형식의 열 길이에 대 한 일반 규칙은이 부록 앞부분의 [Interval 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md)를 참조 하세요.  
  
 열 (또는 매개 변수) 크기에 대해 반환 되는 값은 하나의 설명자 필드에 있는 값과 일치 하지 않습니다. 다음 표와 같이 데이터 유형에 따라 SQL_DESC_PRECISION 또는 SQL_DESC_LENGTH 필드에서 값을 가져올 수 있습니다.  
  
|SQL 유형|에 해당 하는 설명자 필드<br /><br /> 열 또는 매개 변수 크기|  
|--------------|--------------------------------------------------------------------|  
|모든 문자 및 이진 형식|LENGTH|  
|모든 숫자 형식|PRECISION|  
|모든 날짜/시간 및 간격 형식|LENGTH|  
|SQL_BIT|LENGTH|
