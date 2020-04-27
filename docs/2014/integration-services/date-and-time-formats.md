---
title: 날짜 및 시간 형식 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- time data types [Integration Services]
- fast parse [Integration Services]
- date data types
- date and time formats for fast parse
ms.assetid: bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26bd117cb63ccc623ee54f3370e1d07237de9c52
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059652"
---
# <a name="date-and-time-formats"></a>날짜 및 시간 형식
  빠른 구문 분석에서는 데이터 구문 분석을 위한 신속하고 간단한 루틴을 제공합니다. 빠른 구문 분석에서는 날짜 및 시간 데이터 형식에 대해 다음과 같은 형식이 지원됩니다.  
  
## <a name="date-data-types"></a>날짜 데이터 형식  
 빠른 구문 분석에서는 날짜 데이터에 대해 다음과 같은 문자열 형식이 지원됩니다.  
  
-   선행 공백을 포함하는 날짜 형식. 예를 들어 " 2004-02-03"은 유효한 값입니다.  
  
-   다음 표에 나열된 ISO 8601 형식  
  
    |형식|Description|  
    |------------|-----------------|  
    |YYYYMMDD<br /><br /> YYYY-MM-DD|네 자리 연도, 두 자리 월 및 두 자리 일이 포함된 기본 및 하이픈으로 연결된 형식입니다. 하이픈으로 연결된 형식에서 날짜 부분은 하이픈(-)으로 구분됩니다.|  
    |YYYY-MM|네 자리 연도와 두 자리 연도의 기본 및 하이픈으로 연결된 축약 형식입니다. 하이픈으로 연결된 형식에서 날짜 부분은 하이픈(-)으로 구분됩니다.|  
    |YYYY|네 자리 연도의 축약 형식입니다.|  
  
 빠른 구문 분석에서는 날짜 데이터에 대해 다음과 같은 형식이 지원되지 않습니다.  
  
-   영문자 월 값. 예를 들어 Oct-31-2003 날짜 형식은 유효하지 않습니다.  
  
-   DD-MM-YYYY 및 MM-DD-YYYY와 같은 모호한 형식. 예를 들어 03-04-1995 및 04-03-1995는 유효하지 않습니다.  
  
-   네 자리 역년과 일 년 내의 세 자리 일의 기본 및 확장 잘림 형식(YYYYDDD 및 YYYY-DDD)입니다.  
  
-   네 자리 연도, 해당 연도의 주를 나타내는 두 자리 숫자 및 해당 주의 일을 나타내는 한 자리 숫자의 기본 및 확장 형식(YYYYWwwD 및 YYYY-Www-D)입니다.  
  
-   연도와 주 날짜에 대한 기본 및 확장 잘림 형식(YYYWww 및 YYYY-Www)은 네 자리 연도와 주를 나타내는 두 자리 숫자입니다.  
  
 빠른 구문 분석에서는 날짜가 DT_DBDATE로 출력됩니다. 잘림 형식의 날짜 값은 채워집니다. 예를 들어 YYYY는 YYYY0101이 됩니다.  
  
 자세한 내용은 [Integration Services 데이터 형식](data-flow/integration-services-data-types.md)을 참조 하세요.  
  
## <a name="time-data-type"></a>시간 데이터 형식  
 빠른 구문 분석에서는 시간 데이터에 대해 다음과 같은 문자열 형식이 지원됩니다.  
  
-   선행 공백을 포함하는 시간 형식. 예를 들어 " 10:24"는 유효한 값입니다.  
  
-   24시간 형식. 빠른 구문 분석에서는 AM 및 PM 표기가 지원되지 않습니다.  
  
-   다음 표에 나열된 ISO 8601 시간 형식  
  
    |형식|Description|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|두 자리 시간, 두 자리 분 및 두 자리 초의 기본 및 확장 형식입니다. 확장 형식에서 시간 부분은 콜론(:)으로 구분됩니다.|  
    |HHMI<br /><br /> HH:MI|두 자리 시간과 두 자리 분의 기본 및 확장 잘림 형식입니다. 확장 형식에서 시간 부분은 콜론(:)으로 구분됩니다.|  
    |HH|두 자리 시간의 잘림 형식입니다.|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|자정 형식입니다.|  
  
-   다음 표에 나열된 표준 시간대를 지정하는 시간 형식  
  
    |형식|Description|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|현지 시간을 얻기 위해 UTC(Coordinated Universal Time)에 더한 시간과 분을 나타내는 기본 및 확장 형식입니다.|  
    |-HH:MI<br /><br /> -HHMI|현지 시간을 얻기 위해 UTC에서 뺀 시간과 분을 나타내는 기본 및 확장 형식입니다.|  
    |+HH|현지 시간을 얻기 위해 UTC에 더한 시간을 나타내는 잘림 형식입니다.|  
    |-HH|현지 시간을 얻기 위해 UTC에서 뺀 시간을 나타내는 잘림 형식입니다.|  
    |Z|값 0은 시간이 UTC 시간임을 나타냅니다.|  
  
     모든 시간 및 날짜/시간 데이터의 형식은 표준 시간대 요소를 포함할 수 있습니다. 그러나 데이터가 DT_DBTIMESTAMPOFFSET 유형인 경우를 제외하고 시스템에서는 표준 시간대 값이 무시됩니다. 자세한 내용은 [Integration Services 데이터 형식](data-flow/integration-services-data-types.md)을 참조 하세요.  
  
     표준 시간대 요소를 포함하는 형식에서는 다음 예와 같이 시간 요소와 표준 시간대 요소 사이에 공백이 없습니다.  
  
     HH:MI:SS[+HH:MI]  
  
     앞의 예에서 대괄호는 표준 시간대 값이 선택 사항임을 나타냅니다.  
  
-   다음 표에 나열된 소수 부분을 포함하는 시간 형식  
  
    |형식|Description|  
    |------------|-----------------|  
    |HH[.nnnnnnn]|n은 시간의 소수 부분을 나타내는 0에서 9999999 사이의 값입니다. 대괄호는 이 값이 선택 사항임을 나타냅니다.<br /><br /> 예를 들어 값 12.750은 12:45를 나타냅니다.|  
    |HHMI[.nnnnnnn]<br /><br /> HH:MI[.nnnnnnn]|n은 분의 소수 부분을 나타내는 0에서 9999999 사이의 값입니다. 대괄호는 이 값이 선택 사항임을 나타냅니다.<br /><br /> 예를 들어 값 1220.500은 12:20:30을 나타냅니다.|  
    |HHMISS[.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n은 초의 소수 부분을 나타내는 0에서 9999999 사이의 값입니다. 대괄호는 이 값이 선택 사항임을 나타냅니다.<br /><br /> 예를 들어 값 122040.250은 12:20:40.15를 나타냅니다.|  
  
    > [!NOTE]  
    >  앞의 표에서 시간 형식의 소수 구분 기호는 소수점이나 쉼표일 수 있습니다.  
  
-   다음 예와 같이 윤초를 포함하는 시간 값  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 빠른 구문 분석에서는 문자열이 DT_DBTIME 및 DT_DBTIME2로 출력됩니다. 잘림 형식의 시간 값은 채워집니다. 예를 들어 HH:MI는 HH:MM:00.000이 됩니다.  
  
 자세한 내용은 [Integration Services 데이터 형식](data-flow/integration-services-data-types.md)을 참조 하세요.  
  
## <a name="datetime-data-type"></a>날짜/시간 데이터 형식  
 빠른 구문 분석에서는 날짜/시간 데이터에 대해 다음과 같은 문자열 형식이 지원됩니다.  
  
-   선행 공백을 포함하는 형식. 예를 들어 "  2003-01-10T203910"은 유효한 값입니다.  
  
-   대문자 T로 구분된 유효한 날짜 형식과 유효한 시간 형식의 조합(예: YYYYMMDDT[HHMISS][+HH:MI]). 시간 및 표준 시간대 값은 필요하지 않습니다. 예를 들어 "2003-10-14"는 유효합니다.  
  
 빠른 구문 분석에서는 시간 간격이 지원되지 않습니다. 예를 들어 YYYYMMDDThhmmss/YYYYMMDDThhmmss 형식에서 시작 및 종료 날짜/시간으로 구분된 시간 간격은 구문 분석할 수 없습니다.  
  
 빠른 구문 분석에서는 문자열이 DT_DATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 및 DT_DBTIMESTAMPOFFSET으로 출력됩니다. 잘림 형식의 날짜/시간 값은 채워집니다. 다음 표에서는 누락된 날짜 및 시간 부분에 대해 추가되는 값을 나열합니다.  
  
|날짜/시간 부분|안쪽 여백|  
|---------------------|-------------|  
|초|00을 추가합니다.|  
|분|00:00을 추가합니다.|  
|Hour|00:00:00을 추가합니다.|  
|일|해당 월의 일에 대해 01을 추가합니다.|  
|월|해당 연도의 월에 대해 01을 추가합니다.|  
  
 자세한 내용은 [Integration Services 데이터 형식](data-flow/integration-services-data-types.md)을 참조 하세요.  
  
  
