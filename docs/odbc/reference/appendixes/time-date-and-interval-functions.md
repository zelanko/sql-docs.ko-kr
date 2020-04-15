---
title: 시간, 날짜 및 간격 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aec3d6b23383edcc9659ff884e8cd71b0595dae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302824"
---
# <a name="time-date-and-interval-functions"></a>시간, 날짜 및 간격 함수
다음 표에는 ODBC 스칼라 함수 집합에 포함된 시간 및 날짜 함수가 나열되어 있습니다. 응용 프로그램은 정보 *유형의* SQL_TIMEDATE_FUNCTIONS **SQLGetInfo를** 호출하여 드라이버가 지원하는 시간 및 날짜 함수를 결정할 수 있습니다.  
  
 *timestamp_exp* 표시되는 인수는 열의 이름, 다른 스칼라 함수의 결과 또는 *ODBC 시간 이스케이프,* *ODBC-date-escape*또는 *ODBC-timestamp-escape가*기본 데이터 형식을 SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE 또는 SQL_TYPE_TIMESTAMP 나타낼 수 있습니다.  
  
 *date_exp* 로 표시된 인수는 열의 이름, 다른 스칼라 함수의 결과 또는 기본 데이터 형식을 SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE 또는 SQL_TYPE_TIMESTAMP 나타낼 수 있는 *ODBC 날짜-이스케이프* 또는 *ODBC-timestamp-escape일*수 있습니다.  
  
 *time_exp* 것으로 표시된 인수는 열의 이름, 다른 스칼라 함수의 결과 또는 기본 데이터 형식을 SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP 나타낼 수 있는 *ODBC 시간 이스케이프* 또는 *ODBC-타임스탬프-이스케이프일*수 있습니다.  
  
 CURRENT_DATE, CURRENT_TIME 및 CURRENT_TIMESTAMP 시간 스칼라 함수는 SQL-92에 맞게 ODBC 3.0에 추가되었습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**CURRENT_DATE(ODBC** 3.0)|현재 날짜를 반환합니다.|  
|**CURRENT_TIME[(시간** **정밀도)]** (ODBC 3.0) *time-precision*|현재 현지 시간을 반환합니다. *시간 정밀도* 인수는 반환된 값의 초 정밀도를 결정합니다.|  
|**CURRENT_TIMESTAMP**<br /> **[(타임스탬프** **정밀도)](ODBC** 3.0) *timestamp-precision*|현재 로컬 날짜와 현지 시간을 타임스탬프 값으로 반환합니다. *타임스탬프 정밀도* 인수는 반환된 타임스탬프의 초 정밀도를 결정합니다.|  
|**커데이트 (ODBC** 1.0)|현재 날짜를 반환합니다.|  
|**커타임(ODBC** 1.0)|현재 현지 시간을 반환합니다.|  
|**데이네임(date_exp)** *date_exp* **)** (ODBC 2.0)|오늘의 데이터 원본별 이름이 포함된 문자열을 반환합니다(예: 일요일부터 토요일 또는 일요일까지). Sunday에서 *date_exp*일 부분에 대해 Samstag를 통해 Samstag를 사용하는 데이터 원본에 대해 독일어)를 사용하는 데이터 원본에 대해 .|  
|**데이오브월(date_exp)** *date_exp* **)** (ODBC 1.0)|*date_exp* 월 필드를 기준으로 월의 일을 1-31 범위의 정수 값으로 반환합니다.|  
|**데이오브위크** *(date_exp)* **)** (ODBC 1.0)|*date_exp* 주 필드를 기준으로 요일을 1-7 범위의 정수 값으로 반환하며, 여기서 1은 일요일을 나타냅니다.|  
|**데이오브이어(date_exp)** *date_exp* **)** (ODBC 1.0)|*date_exp* 연도 필드를 기준으로 연도의 일을 1-366 범위의 정수 값으로 반환합니다.|  
|**EXTRACT(** *추출(추출-소스에서 추출* *extract-source* **필드)** (ODBC 3.0)|추출 소스의 *추출 필드* 부분을 *반환합니다.* *추출 소스* 인수는 datetime 또는 간격 식입니다. *추출 필드* 인수는 다음 키워드 중 하나가 될 수 있습니다.<br /><br /> 연도 월 요일 시간 분 초<br /><br /> 반환된 값의 정밀도는 구현 정의입니다. SECOND를 지정하지 않는 한 축척은 0이며, 이 경우 배율은 *추출 소스* 필드의 분수 초 정밀도보다 큽입니다.|  
|**시간(time_exp)** *time_exp* **)** (ODBC 1.0)|*time_exp* 시간 필드를 기준으로 시간을 0-23 범위의 정수 값으로 반환합니다.|  
|**분(time_exp)** *time_exp* **)** (ODBC 1.0)|*time_exp* 분 필드를 0-59 범위의 정수 값으로 반환합니다.|  
|**월(date_exp)** *date_exp* **)** (ODBC 1.0)|*date_exp* 월 필드를 기준으로 월을 1-12 범위의 정수 값으로 반환합니다.|  
|**월 명(date_exp)** *date_exp* **)** (ODBC 2.0)|*date_exp*월 부분에 대해 영어를 사용하는 데이터 원본의 경우 1월부터 12월까지 또는 12월까지의 데이터 원본또는 Dezember를 통해 Januar를 포함하는 문자 문자열을 반환합니다.|  
|**지금()** (ODBC 1.0)|현재 날짜와 시간을 타임스탬프 값으로 반환합니다.|  
|**분기(date_exp)** *date_exp* **)** (ODBC 1.0)|*date_exp* 분기를 1-4 범위의 정수 값으로 반환하며, 여기서 1은 1월 1일부터 3월 31일까지입니다.|  
|**초(time_exp)** *time_exp* **)** (ODBC 1.0)|*time_exp* 두 번째 필드를 기준으로 두 번째 필드를 0-59 범위의 정수 값으로 반환합니다.|
|**타임스탬프(간격,** *interval* *integer_exp,* *timestamp_exp)* **)** (ODBC 2.0)|*timestamp_exp*형식 *간격의* *integer_exp* 간격을 추가하여 계산된 타임스탬프를 반환합니다. *간격의* 유효한 값은 다음 키워드입니다.<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 분수 초가 수십억 초로 표현되는 경우. 예를 들어 다음 SQL 문은 각 직원의 이름과 1년 기념일을 반환합니다.<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> *timestamp_exp* 시간 값이며 *간격이* 일, 주, 월, 분기 또는 연도를 지정하는 경우 *timestamp_exp* 날짜 부분은 결과 타임스탬프를 계산하기 전에 현재 날짜로 설정됩니다.<br /><br /> *timestamp_exp* 날짜 값이고 *간격이* 분수 초, 초, 분 또는 시간을 지정하는 경우 결과 타임스탬프를 계산하기 전에 *timestamp_exp* 시간 부분이 0으로 설정됩니다.<br /><br /> 응용 프로그램은 SQL_TIMEDATE_ADD_INTERVALS 옵션으로 **SQLGetInfo를** 호출하여 데이터 원본이 지원하는 간격을 결정합니다.|  
|**타임스탬프DIFF(간격,** *interval* *timestamp_exp1,* *timestamp_exp2)* **)** (ODBC 2.0)|*timestamp_exp2* *timestamp_exp1*보다 큰 형식 *간격의* 정수 수를 반환합니다. *간격의* 유효한 값은 다음 키워드입니다.<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 분수 초가 수십억 초로 표현되는 경우. 예를 들어 다음 SQL 문은 각 직원의 이름과 그 직원또는 고용된 연도를 반환합니다.<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 타임스탬프 표현식이 시간 값이고 *간격이* 일, 주, 월, 분기 또는 연도를 지정하는 경우 해당 타임스탬프의 날짜 부분은 타임스탬프 간의 차이를 계산하기 전에 현재 날짜로 설정됩니다.<br /><br /> 타임스탬프 표현식이 날짜 값이고 *간격이* 분수 초, 초, 분 또는 시간을 지정하는 경우 해당 타임스탬프의 시간 부분은 타임스탬프 간의 차이를 계산하기 전에 0으로 설정됩니다.<br /><br /> 응용 프로그램은 SQL_TIMEDATE_DIFF_INTERVALS 옵션으로 **SQLGetInfo를** 호출하여 데이터 원본이 지원하는 간격을 결정합니다.|  
|**주(date_exp)** *date_exp* **)** (ODBC 1.0)|*date_exp* 주 필드를 기준으로 연도의 주를 1-53 범위의 정수 값으로 반환합니다.|  
|**연도(date_exp)** *date_exp* **)** (ODBC 1.0)|date_exp 연도 필드를 기준으로 연도를 정수 *값으로* 반환합니다. 범위는 데이터 원본에 따라 다릅니다.|
