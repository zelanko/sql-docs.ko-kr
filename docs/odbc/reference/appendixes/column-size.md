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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5639828c90141079ab66f6cceb466328ddb3f56d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019228"
---
# <a name="column-size"></a>열 크기
숫자 데이터 형식의 열 (또는 매개 변수) 크기는 데이터 형식의 열 또는 매개 변수 또는 데이터의 전체 자릿수에 사용 되는 숫자의 최대 수로 정의 됩니다. 이 데이터의 문자에서 길이 문자 형식에 대 한 이진 데이터 형식에 대 한 열 크기는 데이터의 길이 (바이트)에서으로 정의 됩니다. 시간, 타임 스탬프 및 모든 간격 데이터 형식의 경우이 데이터의 문자 표현에 있는 문자의 수입니다. 각 간결한 SQL 데이터 형식에 대해 정의 된 열 크기는 다음 표에 표시 됩니다.  
  
|SQL 유형 식별자|열 크기|  
|-------------------------|-----------------|  
|모든 문자 형식 [a], [b]입니다.|문자 열 또는 매개 변수의 (SQL_DESC_LENGTH 설명자 필드에 포함)의 정의 또는 최대 열 크기입니다. 예를 들어, char (10)로 정의 된 싱글바이트 문자 열의 열 크기는 10입니다.|  
|SQL_DECIMAL SQL_NUMERIC|정의 된 자릿수입니다. 예를 들어 NUMERIC(10,3)로 정의 된 열 전체 자릿수는 10입니다.|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 (부호 있음) 하는 경우 또는 20 (부호 없음) 하는 경우|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|모든 이진 형식 [a], [b]입니다.|정의 또는 최대 길이 (바이트)에서의 열 또는 매개 변수입니다. 예를 들어 binary(10)로 표현으로 정의 된 열의 길이 10입니다.|  
|SQL_TYPE_DATE[c]|10 (문자 수를 *yyyy-월-일* 형식).|  
|SQL_TYPE_TIME[c]|8 (에 있는 문자의 수를 *hh-mm-ss* 형식), 또는 9 + *s* (의 문자 수가 합니다 *hh: mm:* [.fff...] 형식으로 여기서 *의*초 전체 자릿수)입니다.|  
|SQL_TYPE_TIMESTAMP|16 (문자 수를 *mm: yyyy hh: mm* 형식)<br /><br /> 19 (문자 수를 *yyyy-월-일* *hh: mm:* 형식)<br /><br /> 로 구분하거나 여러<br /><br /> 20 + *s* (의 문자 수가 합니다 *h:mm: ss yyyy-월-일*[.fff...] 형식으로 여기서 *s* 초 전체 자릿수)입니다.|  
|SQL_INTERVAL_SECOND|여기서 *p* 선행 정밀도 간격 및 *s* 초 전체 자릿수 *p* (경우 *s*= 0) 또는 *p* + *s*+ 1 (경우 *s*> 0). [ d]|  
|SQL_INTERVAL_DAY_TO_SECOND|여기서 *p* 선행 정밀도 간격 및 *s* 초 전체 자릿수, 9 +*p* (경우 *s*= 0) 또는 10 +*p* + *s* (경우 *s*> 0). [ d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|여기서 *p* 선행 정밀도 간격 및 *s* 초 전체 자릿수, 6 +*p* (경우 *s*= 0) 또는 7 +*p* + *s* (경우 *s*> 0). [ d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|여기서 *p* 선행 정밀도 간격 및 *s* 초 전체 자릿수를 3 +*p* (경우 *s*= 0) 또는 4 +*p* + *s* (경우 *s*> 0). [ d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*, 여기서 *p* 전체 자릿수를 유도 하는 간격입니다. [ d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*, 여기서 *p* 전체 자릿수를 유도 하는 간격입니다. [ d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*, 여기서 *p* 전체 자릿수를 유도 하는 간격입니다. [ d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*, 여기서 *p* 전체 자릿수를 유도 하는 간격입니다. [ d]|  
|SQL_GUID|36 (문자 수를 *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* 형식)|  
  
 [a] an ODBC 1.0에 대 한 응용 프로그램 호출 **SQLSetParam** 는 ODBC 2.0 드라이버에는 ODBC 2.0 응용 프로그램 호출 **SQLBindParameter** 1.0 ODBC 드라이버에서 사용 하는 경우 \*  *StrLen_or_IndPtr* SQL_LONGVARCHAR 또는 SQL_LONGVARBINARY 형식 SQL_DATA_AT_EXEC입니다 *ColumnSize* 전송할 전체 자릿수 없습니다이 테이블에 정의 된 대로 데이터의 총 길이를 설정 해야 합니다.  
  
 [b] 드라이버 변수 형식에 대 한 열 또는 매개 변수 길이 확인할 수 없는, 하는 경우 SQL_NO_TOTAL을 반환 합니다.  
  
 [c]를 *ColumnSize* 인수의 **SQLBindParameter** 이 데이터 형식에 대해 무시 됩니다.  
  
 [간격 데이터 형식에서 열 길이 대 한 일반 규칙 d]을 참조 하세요 [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md)이 부록 앞부분입니다.  
  
 열 (또는 매개 변수) 크기에 대 한 반환 값 한 설명자 필드의 값에 일치 하지 않습니다. 다음 표에 나와 있는 것 처럼의 SQL_DESC_PRECISION 또는 데이터의 유형에 따라 SQL_DESC_LENGTH 필드에서 값을 가져올 수 있습니다.  
  
|SQL 유형|해당 하는 설명자 필드<br /><br /> 열 또는 매개 변수 크기|  
|--------------|--------------------------------------------------------------------|  
|모든 문자 및 이진 유형|LENGTH|  
|모든 숫자 형식|PRECISION|  
|모든 날짜/시간 형식과 간격|LENGTH|  
|SQL_BIT|LENGTH|
