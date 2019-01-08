---
title: 숫자 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c92a2d943ecbe571bd87268a7096d2adf51a06c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52534291"
---
# <a name="numeric-functions"></a>숫자 함수
다음 표에서 ODBC 스칼라 함수 집합에 포함 된 숫자 함수에 설명 합니다. 호출 하 여 **SQLGetInfo** 사용 하 여는 *정보 유형* SQL_NUMERIC_FUNCTIONS의 응용 프로그램을 드라이버에서 지원 되는 숫자 함수 확인할 수 있습니다.  
  
 모든 숫자 함수 반환 값 데이터 형식을 SQL_FLOAT ABS 제외 하 고 ROUND, TRUNCATE, 로그인, 바닥 및 천장에 동일한 데이터의 값을 반환 하는 입력된 매개 변수로 입력 합니다.  
  
 로 표시 된 인수 *numeric_exp* 다른 스칼라 함수의 결과 열의 이름이 될 수 있습니다 또는 *숫자 litera*l, SQL_NUMERIC, SQL_로 기본 데이터 형식을 나타낼 수 있습니다 위치 10 진수 SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, 또는 SQL_DOUBLE 합니다.  
  
 로 표시 된 인수 *float_exp* 다른 스칼라 함수의 결과 열의 이름이 될 수 있습니다 또는 *숫자 리터럴*이면 기본 데이터 형식을 SQL_FLOAT로 표현할 수 있습니다 위치 합니다.  
  
 로 표시 된 인수 *integer_exp* 다른 스칼라 함수의 결과 열의 이름이 될 수 있습니다 또는 *숫자 리터럴*SQL_TINYINT, SQL_로 기본 데이터 형식을 나타낼 수 있는, SMALLINT, SQL_INTEGER, 또는 SQL_BIGINT 합니다.  
  
 SQL-92에 맞게 ODBC 3.0에서 CURRENT_DATE 고 CURRENT_TIME, CURRENT_TIMESTAMP 스칼라 함수가 추가 되었습니다.  
  
|기능|Description|  
|--------------|-----------------|  
|**ABS (** *numeric_exp* **)** (ODBC 1.0)|절대값을 반환 합니다 *numeric_exp*합니다.|  
|**ACOS (** *float_exp* **)** (ODBC 1.0)|아크코사인을 반환 합니다 *float_exp* 각도를 라디안 단위로 표현 됩니다.|  
|**ASIN (** *float_exp* **)** (ODBC 1.0)|아크사인 값을 반환 *float_exp* 각도를 라디안 단위로 표현 됩니다.|  
|**ATAN (** *float_exp* **)** (ODBC 1.0)|아크탄젠트를 반환 *float_exp* 각도를 라디안 단위로 표현 됩니다.|  
|**ATAN2 (** *float_exp1*하십시오 _float_exp2_**)** (ODBC 2.0)|아크탄젠트를 반환 합니다 *x* 하 고 *y* 으로 지정 된 좌표 *float_exp1* 및 *float_exp2*각각 각도 라디안 단위로 표현 됩니다.|  
|**CEILING (** *numeric_exp* **)** (ODBC 1.0)|보다 크거나 같은 최소 정수를 반환 *numeric_exp*합니다. 반환 값은 입력된 매개 변수로 동일한 데이터 형식입니다.|  
|**COS (** *float_exp* **)** (ODBC 1.0)|코사인을 반환 *float_exp*, 여기서 *float_exp* 라디안에서으로 표시 되는 각도입니다.|  
|**COT (** *float_exp* **)** (ODBC 1.0)|코탄젠트를 반환 합니다 *float_exp*, 여기서 *float_exp* 라디안에서으로 표시 되는 각도입니다.|  
|**도 (** *numeric_exp* **)** (ODBC 2.0)|변환 하는 각도 반환 *numeric_exp* 라디안입니다.|  
|**EXP (** *float_exp* **)** (ODBC 1.0)|지 수 값을 반환 *float_exp*합니다.|  
|**FLOOR (** *numeric_exp* **)** (ODBC 1.0)|보다 작거나 같은 최대 정수를 반환 *numeric_exp*합니다. 반환 값은 입력된 매개 변수로 동일한 데이터 형식입니다.|  
|**로그 (** *float_exp* **)** (ODBC 1.0)|자연 로그를 반환 *float_exp*합니다.|  
|**LOG10 (** *float_exp* **)** (ODBC 2.0)|반환을 밑수 10 로그 *float_exp*합니다.|  
|**MOD (** *integer_exp1*하십시오 _integer_exp2_**)** (ODBC 1.0)|나머지를 반환 합니다 (모듈러스) *integer_exp1* 나눈 *integer_exp2*합니다.|  
|**PI ()** (ODBC 1.0)|부동 소수점 값으로 pi의 상수 값을 반환합니다.|  
|**POWER (** *numeric_exp*하십시오 _integer_exp_**)** (ODBC 2.0)|값을 반환 *numeric_exp* 활용할 *integer_exp*합니다.|  
|**RADIANS (** *numeric_exp* **)** (ODBC 2.0)|변환 하는 라디안 수를 반환 *numeric_exp* 도 합니다.|  
|**RAND (**[*integer_exp*]**)** (ODBC 1.0)|사용 하 여 임의의 부동 소수점 값 반환 *integer_exp* 선택적 시드 값으로.|  
|**ROUND (** *numeric_exp*하십시오 _integer_exp_**)** (ODBC 2.0)|반환 *numeric_exp* 반올림 *integer_exp* 소수점이 하 자릿수를 배치 합니다. 하는 경우 *integer_exp* 가 음수 이면 *numeric_exp* 반올림 됩니다 &#124; *integer_exp* &#124; 소수점의 왼쪽에 배치 합니다.|  
|**기호 (** *numeric_exp* **)** (ODBC 1.0)|부호를 나타내는 표시기 반환 *numeric_exp*합니다. 하는 경우 *numeric_exp* 0-1 보다 작은 반환 됩니다. 하는 경우 *numeric_exp* 0, 0이 반환 됩니다. 하는 경우 *numeric_exp* 0 보다 크면 1이 반환 됩니다.|  
|**SIN (** *float_exp* **)** (ODBC 1.0)|사인을 반환 합니다 *float_exp*, 여기서 *float_exp* 라디안에서으로 표시 되는 각도입니다.|  
|**SQRT (** *float_exp* **)** (ODBC 1.0)|제곱근을 반환 합니다 *float_exp*합니다.|  
|**TAN (** *float_exp* **)** (ODBC 1.0)|탄젠트를 반환 *float_exp*, 여기서 *float_exp* 라디안에서으로 표시 되는 각도입니다.|  
|**TRUNCATE (** *numeric_exp*하십시오 _integer_exp_**)** (ODBC 2.0)|반환 *numeric_exp* 잘립니다 *integer_exp* 소수점이 하 자릿수를 배치 합니다. 하는 경우 *integer_exp* 가 음수 이면 *numeric_exp* 잘립니다 &#124; *integer_exp* &#124; 소수점의 왼쪽에 배치 합니다.|
