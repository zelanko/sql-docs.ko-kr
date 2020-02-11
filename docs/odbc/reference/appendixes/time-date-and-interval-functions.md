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
ms.openlocfilehash: ae10946be501adb16fdda5fa9f053e389eea4bed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070080"
---
# <a name="time-date-and-interval-functions"></a>시간, 날짜 및 간격 함수
다음 표에서는 ODBC 스칼라 함수 집합에 포함 된 시간 및 날짜 함수를 보여 줍니다. 응용 프로그램은 SQL_TIMEDATE_FUNCTIONS *정보 형식* 으로 **SQLGetInfo** 를 호출 하 여 드라이버에서 지원 되는 시간 및 날짜 함수를 확인할 수 있습니다.  
  
 *Timestamp_exp* 로 표시 되는 인수는 열 이름, 다른 스칼라 함수의 결과 또는 odbc *시간 이스케이프*, *odbc-날짜-이스케이프*또는 odbc *-타임 스탬프-* 이스케이프 (기본 데이터 형식이 SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE 또는 SQL_TYPE_TIMESTAMP로 표시 될 수 있습니다.  
  
 *Date_exp* 로 표시 되는 인수는 열 이름, 다른 스칼라 함수의 결과 또는 *odbc-날짜-이스케이프* 또는 *odbc-타임 스탬프-이스케이프*(기본 데이터 형식이 SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE 또는 SQL_TYPE_TIMESTAMP로 표시 될 수 있음) 일 수 있습니다.  
  
 *Time_exp* 로 표시 되는 인수는 열 이름, 다른 스칼라 함수의 결과 또는 *odbc 시간 이스케이프* 또는 *odbc-타임 스탬프-이스케이프*일 수 있습니다 .이 경우 기본 데이터 형식은 SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP로 표시 될 수 있습니다.  
  
 CURRENT_DATE, CURRENT_TIME 및 CURRENT_TIMESTAMP timedate.cpl 스칼라 함수는 SQL-92에 맞게 ODBC 3.0에 추가 되었습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**CURRENT_DATE ()** (ODBC 3.0)|현재 날짜를 반환합니다.|  
|**CURRENT_TIME [(** *시간-전체 자릿수* **)]** (ODBC 3.0)|현재 현지 시간을 반환합니다. *시간 전체 자릿수* 인수는 반환 된 값의 초 전체 자릿수를 결정 합니다.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *타임 스탬프-전체 자릿수* **)]** (ODBC 3.0)|현재 현지 날짜와 현지 시간을 타임 스탬프 값으로 반환 합니다. *Timestamp-precision* 인수는 반환 된 타임 스탬프의 초 전체 자릿수를 결정 합니다.|  
|**Curdate ()** (ODBC 1.0)|현재 날짜를 반환합니다.|  
|**Curtime ()** (ODBC 1.0)|현재 현지 시간을 반환합니다.|  
|**Dayname (** *date_exp* **)** (ODBC 2.0)|요일의 데이터 원본인 이름을 포함 하는 문자열을 반환 합니다 (예: 일요일-토요일 또는 Sun). Sunday에서 영어를 사용 하는 데이터 원본 또는 Saturday까지에서 독일어를 사용 하는 데이터 원본에 대해 Samstag를 사용 하는 경우 *date_exp*의 일 부분|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|*Date_exp* 의 월 필드를 기준으로 1-31 범위의 정수 값으로 월의 날짜를 반환 합니다.|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|*Date_exp* 의 주 필드를 기준으로 하는 요일을 1-7 범위의 정수 값으로 반환 합니다. 여기서 1은 일요일을 나타냅니다.|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|*Date_exp* 의 연도 필드를 기준으로 하는 날짜를 1-366 범위의 정수 값으로 반환 합니다.|  
|Extract **(** extract- *source* *에서 field* **)** (ODBC 3.0)|*추출 원본*에서 *추출 필드* 부분을 반환 합니다. *Extract 원본* 인수는 datetime 또는 interval 식입니다. *추출 필드* 인수는 다음 키워드 중 하나일 수 있습니다.<br /><br /> 년 월 일 시 분 초<br /><br /> 반환 된 값의 전체 자릿수는 구현에서 정의 됩니다. 소수 자릿수는 SECOND가 지정 되지 않은 경우 0입니다 .이 경우 소수 자릿수는 *추출 원본* 필드의 초 소수 부분 자릿수 보다 작지 않습니다.|  
|**시간 (** *time_exp* **)** (ODBC 1.0)|*Time_exp* 의 시간 필드를 기준으로 하는 시간을 0-23 범위의 정수 값으로 반환 합니다.|  
|**분 (** *time_exp* **)** (ODBC 1.0)|*Time_exp* 의 분 필드를 기준으로 0-59 범위의 정수 값으로 분을 반환 합니다.|  
|**월 (** *date_exp* **)** (ODBC 1.0)|*Date_exp* 의 월 필드를 기준으로 하는 월을 1-12 범위의 정수 값으로 반환 합니다.|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2.0)|월의 데이터 원본 이름을 포함 하는 문자열을 반환 합니다 (예: 1 월에서 12 월 또는 1 월-12 월까지). 영어를 사용 하는 데이터 원본의 경우 *date_exp*의 월 부분에 독일어를 사용 하는 데이터 원본에 대해 januar에서을 통해 Dezember을 반환 합니다.|  
|**NOW ()** (ODBC 1.0)|현재 날짜와 시간을 타임 스탬프 값으로 반환 합니다.|  
|**QUARTER (** *date_exp* **)** (ODBC 1.0)|*Date_exp* 의 분기를 1-4 범위의 정수 값으로 반환 합니다. 여기서 1은 1 월 1 일부 터 3 월 31 일까 지를 나타냅니다.|  
|**SECOND (** *time_exp* **)** (ODBC 1.0)|*Time_exp* 의 두 번째 필드를 기반으로 하는 두 번째 필드를 0-59 범위의 정수 값으로 반환 합니다.|
|**TIMESTAMPADD (** *interval*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|*Timestamp_exp* *간격* *integer_exp* 간격을 더하여 계산 된 타임 스탬프를 반환 합니다. *Interval* 의 유효한 값은 다음과 같은 키워드입니다.<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 여기서 소수 자릿수 초는 billionths로 표시 됩니다. 예를 들어 다음 SQL 문은 각 직원의 이름과 1 년의 1 년 기념일을 반환 합니다.<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> *Timestamp_exp* 가 시간 값이 고 *interval* 이 일, 주, 월, 분기 또는 연도를 지정 하는 경우 *timestamp_exp* 의 날짜 부분은 결과 타임 스탬프를 계산 하기 전에 현재 날짜로 설정 됩니다.<br /><br /> *Timestamp_exp* 날짜 값이 고 *interval* 이 소수 자릿수 초, 초, 분 또는 시간을 지정 하는 경우 *timestamp_exp* 의 시간 부분은 결과 타임 스탬프를 계산 하기 전에 0으로 설정 됩니다.<br /><br /> 응용 프로그램은 SQL_TIMEDATE_ADD_INTERVALS 옵션으로 **SQLGetInfo** 를 호출 하 여 데이터 소스에서 지 원하는 간격을 결정 합니다.|  
|**TIMESTAMPDIFF (** *interval*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|*Timestamp_exp2* *timestamp_exp1*보다 큰 정수 형식 *간격* 의 정수를 반환 합니다. *Interval* 의 유효한 값은 다음과 같은 키워드입니다.<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 여기서 소수 자릿수 초는 billionths로 표시 됩니다. 예를 들어 다음 SQL 문은 각 직원의 이름 및 사용 된 연도 수를 반환 합니다.<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 타임 스탬프 식이 시간 값이 고 *interval* 이 일, 주, 월, 분기 또는 연도를 지정 하는 경우 타임 스탬프의 차이를 계산 하기 전에 타임 스탬프의 날짜 부분이 현재 날짜로 설정 됩니다.<br /><br /> Timestamp 식이 날짜 값 이며 *interval* 초, 초, 분 또는 시간을 지정 하는 경우 타임 스탬프의 시간 부분은 0으로 설정 되어 타임 스탬프 간의 차이를 계산 합니다.<br /><br /> 응용 프로그램은 SQL_TIMEDATE_DIFF_INTERVALS 옵션으로 **SQLGetInfo** 를 호출 하 여 데이터 소스에서 지 원하는 간격을 결정 합니다.|  
|**주 (** *date_exp* **)** (ODBC 1.0)|*Date_exp* 의 주 필드를 기준으로 1-53 범위의 정수 값으로 연간 주를 반환 합니다.|  
|**YEAR (** *date_exp* **)** (ODBC 1.0)|*Date_exp* 의 연도 필드를 기준으로 하는 연도를 정수 값으로 반환 합니다. 범위는 데이터 원본에 따라 다릅니다.|
