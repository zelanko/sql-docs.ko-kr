---
title: 숫자 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 03da5b6644e0f7df3dc4e5e16a211cb503023bad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299873"
---
# <a name="numeric-functions"></a>숫자 함수
다음 표에서는 ODBC 스칼라 함수 집합에 포함된 숫자 함수에 대해 설명합니다. SQL_NUMERIC_FUNCTIONS *정보 형식을* 사용하여 **SQLGetInfo를** 호출하여 응용 프로그램은 드라이버에서 지원하는 숫자 함수를 결정할 수 있습니다.  
  
 모든 숫자 함수는 입력 매개 변수와 동일한 데이터 형식의 값을 반환하는 ABS, ROUND, TRUNCATE, SIGN, FLOOR 및 천장을 제외한 SQL_FLOAT 데이터 형식의 값을 반환합니다.  
  
 *numeric_exp* 표시된 인수는 열의 이름, 다른 스칼라 함수의 결과 또는 기본 데이터 형식이 SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL 또는 SQL_DOUBLE 나타낼 수 있는 *숫자-리터라*l일 수 있습니다.  
  
 *float_exp* 것으로 표시된 인수는 열의 이름, 다른 스칼라 함수의 결과 또는 기본 데이터 형식을 SQL_FLOAT 나타낼 수 있는 *숫자 리터럴일*수 있습니다.  
  
 *integer_exp* 표시된 인수는 열의 이름, 다른 스칼라 함수의 결과 또는 기본 데이터 형식을 SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER 또는 SQL_BIGINT 나타낼 수 있는 *숫자 리터럴일*수 있습니다.  
  
 CURRENT_DATE, CURRENT_TIME 및 CURRENT_TIMESTAMP 스칼라 함수는 SQL-92에 맞게 ODBC 3.0에 추가되었습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**ABS** _(numeric_exp)_ **)** (ODBC 1.0)|*numeric_exp*의 절대 값을 반환합니다.|  
|**아코스(float_exp)** _float_exp_ **)** (ODBC 1.0)|라디안으로 표현된 *float_exp* 아크코신을 각도로 반환합니다.|  
|**아신** _(float_exp)_ **)** (ODBC 1.0)|radians로 표현된 *float_exp* 호신을 각도로 반환합니다.|  
|**아탄** _(float_exp)_ **)** (ODBC 1.0)|radians로 표현된 *float_exp* 아크탄젠트를 각도로 반환합니다.|  
|**ATAN2** _(float_exp1,_ _float_exp2)_**)** (ODBC 2.0)|*float_exp1* 및 *float_exp2*각각 라디안에서 표현된 각도로 지정된 *x* 및 *y* 좌표의 아크탄젠트를 반환합니다.|  
|**천장(numeric_exp)** _numeric_exp_ **)** (ODBC 1.0)|numeric_exp 보다 크거나 *같을*가장 작은 정수입니다. 반환 값은 입력 매개 변수와 동일한 데이터 형식입니다.|  
|**COS(float_exp)** _float_exp_ **)** (ODBC 1.0)|*float_exp* 라디안에서 표현된 각도인 *float_exp*코사인을 반환합니다.|  
|**COT** _(float_exp)_ **)** (ODBC 1.0)|*float_exp* radians로 표현된 각도인 *float_exp*코탄젠트를 반환합니다.|  
|**도(numeric_exp)** _numeric_exp_ **)** (ODBC 2.0)|*numeric_exp* 라디안에서 변환된 도 수를 반환합니다.|  
|**익스포(float_exp)** _float_exp_ **)** (ODBC 1.0)|*float_exp*.|  
|**바닥(numeric_exp)** _numeric_exp_ **)** (ODBC 1.0)|numeric_exp 이하 또는 *같음의*가장 큰 정수를 반환합니다. 반환 값은 입력 매개 변수와 동일한 데이터 형식입니다.|  
|**로그(float_exp)** _float_exp_ **)** (ODBC 1.0)|*float_exp*자연의 로그가 반환됩니다.|  
|**LOG10(float_exp)** _float_exp_ **)** (ODBC 2.0)|*float_exp*기본 10 로그백을 반환합니다.|  
|**MOD** _(integer_exp1,_ _integer_exp2)_**)** (ODBC 1.0)|*integer_exp1* 나머지(계수)를 *integer_exp2*으로 나눈 값을 반환합니다.|  
|**PI(ODBC** 1.0)|pi의 상수 값을 부동 점 값으로 반환합니다.|  
|**전원(numeric_exp,** _numeric_exp_ _integer_exp)_**)** (ODBC 2.0)|*numeric_exp* 값을 *integer_exp.*|  
|**라디안** _(numeric_exp)_ **)** (ODBC 2.0)|*numeric_exp* 도에서 변환된 라디안 수를 반환합니다.|  
|**RAND***([integer_exp]***(ODBC** 1.0)|선택적 시드 값으로 *integer_exp* 사용하여 임의부동점 값을 반환합니다.|  
|**라운드(numeric_exp,** _numeric_exp_ _integer_exp)_**)** (ODBC 2.0)|numeric_exp *numeric_exp* 반품은 소수점 *오른쪽의 integer_exp* 위치에 반올림됩니다. *integer_exp* 음수인 경우 *numeric_exp* 소수점 왼쪽에 *integer_exp*&#124; &#124;배치합니다.|  
|**기호(numeric_exp)** _numeric_exp_ **)** (ODBC 1.0)|*numeric_exp*기호의 표시기를 반환합니다. *numeric_exp* 0보다 낮으면 -1이 반환됩니다. *numeric_exp* 0이면 0이 반환됩니다. *numeric_exp* 0보다 크면 1이 반환됩니다.|  
|**SIN(float_exp)** _float_exp_ **)** (ODBC 1.0)|*float_exp* radians로 표현 된 각도인 *float_exp*사인을 반환합니다.|  
|**SQRT(float_exp)** _float_exp_ **)** (ODBC 1.0)|*float_exp*의 제곱근을 반환합니다.|  
|**TAN(float_exp)** _float_exp_ **)** (ODBC 1.0)|*float_exp* radians로 표현된 각도인 *float_exp*접선을 반환합니다.|  
|**트렁킨** _(numeric_exp,_ _integer_exp)_**)** (ODBC 2.0)|소수점 오른쪽의 *integer_exp* 위치에 잘린 *numeric_exp* 반환합니다. *integer_exp* 음수인 경우 *numeric_exp* 소수점 왼쪽에 *integer_exp*&#124; &#124;잘립니다.|
