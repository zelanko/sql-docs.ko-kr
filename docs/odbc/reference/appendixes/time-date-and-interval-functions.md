---
title: 시간, 날짜 및 간격 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1303ca724ef6790ae7bcf218ab8ed0e5da4ed38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735089"
---
# <a name="time-date-and-interval-functions"></a>시간, 날짜 및 간격 함수
다음 표에서 ODBC 스칼라 함수 집합에 포함 된 날짜 및 시간 함수를 나열 합니다. 응용 프로그램에서 호출 하 여 드라이버에서 지원 되는 날짜 및 시간 함수를 확인할 수 있습니다 **SQLGetInfo** 사용 하 여는 *정보 유형* SQL_TIMEDATE_FUNCTIONS입니다.  
  
 로 표시 된 인수 *timestamp_exp* 다른 스칼라 함수의 결과 열의 이름이 될 수 있습니다 또는 *ODBC 시간 이스케이프*합니다 *ODBC 날짜-이스케이프*, 또는 *ODBC 타임 스탬프 이스케이프*, SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE, 또는 SQL_TYPE_TIMESTAMP로 기본 데이터 형식이 표시 될 수 있습니다 위치 합니다.  
  
 로 표시 된 인수 *date_exp* 다른 스칼라 함수의 결과 열의 이름이 될 수 있습니다 또는 *ODBC 날짜-이스케이프* 하거나 *ODBC 타임 스탬프 이스케이프*여기서는 내부 데이터 형식이 SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE, 또는 SQL_TYPE_TIMESTAMP로 나타낼 수 있습니다.  
  
 로 표시 된 인수 *time_exp* 다른 스칼라 함수의 결과 열의 이름이 될 수 있습니다 또는 *ODBC 시간 이스케이프* 하거나 *ODBC 타임 스탬프 이스케이프*여기서는 내부 데이터 형식이 SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP로 나타낼 수 있습니다.  
  
 CURRENT_DATE 고 CURRENT_TIME, CURRENT_TIMESTAMP timedate 스칼라 함수 SQL-92에 맞게 ODBC 3.0에서 추가 되었습니다.  
  
|기능|Description|  
|--------------|-----------------|  
|**CURRENT_DATE ()** (ODBC 3.0)|현재 날짜를 반환합니다.|  
|**CURRENT_TIME[(** *time-precision* **)]** (ODBC 3.0)|현재 현지 시간을 반환합니다. 합니다 *시간 정밀도* 인수에 반환된 된 값의 초 전체 자릿수를 결정 합니다.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *타임 스탬프 정밀도* **)]** (ODBC 3.0)|타임 스탬프 값으로 현재 현지 날짜와 현지 시간을 반환합니다. 합니다 *타임 스탬프 정밀도* 인수는 반환 된 타임 스탬프의 초 전체 자릿수를 결정 합니다.|  
|**CURDATE ()** (ODBC 1.0)|현재 날짜를 반환합니다.|  
|**CURTIME ()** (ODBC 1.0)|현재 현지 시간을 반환합니다.|  
|**DAYNAME(** *date_exp* **)** (ODBC 2.0)|요일 (예: 일요일부터 토요일 이나 일요일 데이터 소스 관련 이름을 포함 하는 문자열을 반환 합니다. Sunday에서 독일어를 사용 하는 데이터 원본에 대 한 영어 또는 Sonntag Samstag 통해을 사용 하 여 데이터 원본)의 일 부분 *date_exp*합니다.|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|월 필드를 기준으로 월의 일을 반환 *date_exp* 1-31 범위의 정수 값으로.|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|주 필드를 기반으로 요일을 반환 *date_exp* 범위의 정수 값으로 1-7, 여기서 1은 일요일을 나타냅니다.|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|연도 필드를 기반으로 연간 일자를 반환 *date_exp* 1-366 사이의 정수 값으로.|  
|**추출 (** *필드 추출 FROM* *추출 원본* **)** (ODBC 3.0)|반환 된 *필드 추출* 부분을 *추출 원본*. 합니다 *추출 원본* 인수는 datetime 또는 간격 식입니다. 합니다 *필드 추출* 인수는 다음 키워드 중 하나일 수 있습니다.<br /><br /> 년 월 일 분 초<br /><br /> 반환된 된 값의 전체 자릿수는 구현 시 정의 됩니다. 소수 자릿수가 0 초를 지정 하지 않으면 경우 소수 자릿수 보다 작지 않습니다 소수 자릿수 초의 전체 자릿수는 *추출 원본* 필드입니다.|  
|**HOUR(** *time_exp* **)** (ODBC 1.0)|시간 필드를 기반으로 시간을 반환 *time_exp* 0 ~ 23 사이의 정수 값으로.|  
|**MINUTE(** *time_exp* **)** (ODBC 1.0)|분 필드를 기준으로 분을 반환 *time_exp* 0-59 사이의 정수 값으로.|  
|**월 (** *date_exp* **)** (ODBC 1.0)|월 필드를 기준으로 월을 반환 합니다 *date_exp* 1-12 범위의 정수 값으로.|  
|**MONTHNAME(** *date_exp* **)** (ODBC 2.0)|월 부분 (예: 12 까지의 월 또는 12 월 영어를 사용 하는 데이터 원본에 대 한 통해 독일어를 사용 하는 데이터 원본의 Dezember까지) 달의 데이터 소스 관련 이름을 포함 하는 문자열을 반환 합니다. *date_exp*합니다.|  
|**이제 ()** (ODBC 1.0)|현재 날짜 및 시간을 타임 스탬프 값으로 반환합니다.|  
|**QUARTER(** *date_exp* **)** (ODBC 1.0)|분기를 반환 *date_exp* 범위의 정수 값으로 1-4, 1 년 1 월 1 년 3 월 31 일까 지 나타냅니다.|  
|**SECOND(** *time_exp* **)** (ODBC 1.0)|두 번째 필드를 기반으로 두 번째 반환 *time_exp* 0-59 사이의 정수 값으로.|
|**TIMESTAMPADD(** *interval*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|추가 하 여 계산 된 타임 스탬프를 반환 *integer_exp* 형식의 간격 *간격* 하 *timestamp_exp*합니다. 유효한 값은 *간격* 다음 키워드는:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 여기서 소수 자릿수 초는 10억 분의 두 번째 1에서 표현 됩니다. 예를 들어, 다음 SQL 문은 자신의 1 년 연주기 각 직원의 이름과 반환합니다.<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 하는 경우 *timestamp_exp* 는 시간 값 및 *간격* 일, 주, 월, 분기 또는 년의 날짜 부분을 지정 합니다 *timestamp_exp* 하기 전에 현재 날짜로 설정 됩니다 결과 타임 스탬프를 계산 합니다.<br /><br /> 하는 경우 *timestamp_exp* 날짜 값이 고 *간격* 소수 자릿수를 지정 초, 초, 분 또는 시간, 시간 부분 *timestamp_exp* 전에 0으로 설정 됩니다 결과 타임 스탬프를 계산 합니다.<br /><br /> 응용 프로그램 호출 하 여 데이터 원본 지원 되는 간격을 결정 **SQLGetInfo** SQL_TIMEDATE_ADD_INTERVALS 옵션을 사용 합니다.|  
|**TIMESTAMPDIFF(** *interval*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|정수 형식의 간격 수를 반환 합니다 *간격* 되 *timestamp_exp2* 보다 크면 *timestamp_exp1*합니다. 유효한 값은 *간격* 다음 키워드는:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 여기서 소수 자릿수 초는 10억 분의 두 번째 1에서 표현 됩니다. 예를 들어, 다음 SQL 문은 자신이 채택 되었습니다 년 수와 각 직원의 이름을 반환 합니다.<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 두 식 중 하나가 타임 스탬프에 시간 값 이면 하 고 *간격* 타임 스탬프 간의 차이 계산 하기 전에 현재 날짜로 설정 일, 주, 월, 분기 또는 연도, 해당 타임 스탬프의 날짜 부분을 지정 합니다.<br /><br /> 타임 스탬프 식 중 하나가 날짜 값 이면 및 *간격* 소수 지정 타임 스탬프 간의 차이 계산 하기 전에 해당 타임 스탬프의 시간 부분은 0으로 설정 시간 (초), 초, 분 또는 시간입니다.<br /><br /> 응용 프로그램 호출 하 여 데이터 원본 지원 되는 간격을 결정 **SQLGetInfo** SQL_TIMEDATE_DIFF_INTERVALS 옵션을 사용 합니다.|  
|**WEEK(** *date_exp* **)** (ODBC 1.0)|주 필드를 기반으로 해당 연도의 주를 반환 *date_exp* 1-53 범위의 정수 값으로.|  
|**YEAR(** *date_exp* **)** (ODBC 1.0)|연도 필드를 기반으로 연도 반환 합니다 *date_exp* 정수 값으로. 범위는 데이터 원본에 따라 다릅니다.|
