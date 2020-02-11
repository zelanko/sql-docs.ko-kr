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
ms.openlocfilehash: 6e744d3de177197923540fc3101c58dcbb4d3490
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990734"
---
# <a name="numeric-functions"></a>숫자 함수
다음 표에서는 ODBC 스칼라 함수 집합에 포함 된 숫자 함수에 대해 설명 합니다. 응용 프로그램에서는 *정보 형식이* SQL_NUMERIC_FUNCTIONS 인 **SQLGetInfo** 를 호출 하 여 드라이버에서 지원 되는 숫자 함수를 확인할 수 있습니다.  
  
 모든 숫자 함수는 입력 매개 변수와 동일한 데이터 형식의 값을 반환 하는 ABS, ROUND, TRUNCATE, SIGN, FLOOR 및 상한은 제외 하 고 SQL_FLOAT 데이터 형식의 값을 반환 합니다.  
  
 *Numeric_exp* 로 표시 되는 인수는 열 이름, 다른 스칼라 함수의 결과 또는 *숫자 litera*l (기본 데이터 형식이 SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL 또는 SQL_DOUBLE로 표시 될 수 있습니다.  
  
 *Float_exp* 로 표시 되는 인수는 열 이름, 다른 스칼라 함수의 결과 또는 *숫자 리터럴이*될 수 있으며,이 경우 기본 데이터 형식이 SQL_FLOAT으로 표시 될 수 있습니다.  
  
 *Integer_exp* 로 표시 되는 인수는 열 이름, 다른 스칼라 함수의 결과 또는 *숫자 리터럴이*될 수 있습니다. 여기서 기본 데이터 형식은 SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER 또는 SQL_BIGINT로 표시 될 수 있습니다.  
  
 CURRENT_DATE, CURRENT_TIME 및 CURRENT_TIMESTAMP 스칼라 함수는 SQL-92에 맞게 ODBC 3.0에 추가 되었습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**ABS (** _numeric_exp_ **)** (ODBC 1.0)|*Numeric_exp*의 절대값을 반환 합니다.|  
|**ACOS (** _float_exp_ **)** (ODBC 1.0)|각도 (라디안)로 표현 되는 *float_exp* 의 아크코사인을 반환 합니다.|  
|**ASIN (** _float_exp_ **)** (ODBC 1.0)|*Float_exp* 의 아크사인을 라디안으로 표현 된 각도로 반환 합니다.|  
|**ATAN (** _float_exp_ **)** (ODBC 1.0)|라디안으로 표시 된 각도 *float_exp* 의 아크탄젠트를 반환 합니다.|  
|**ATAN2 (** _float_exp1_, _float_exp2_**)** (ODBC 2.0)|각각 *float_exp1* 및 *float_exp2*에 의해 지정 된 *x* 및 *y* 좌표의 아크탄젠트를 라디안으로 표현 된 각도로 반환 합니다.|  
|**상한 (** _numeric_exp_ **)** (ODBC 1.0)|*Numeric_exp*보다 크거나 같은 최소 정수를 반환 합니다. 반환 값은 입력 매개 변수와 동일한 데이터 형식입니다.|  
|**COS (** _float_exp_ **)** (ODBC 1.0)|*Float_exp*코사인을 반환 합니다. 여기서 *float_exp* 는 라디안으로 표현 된 각도입니다.|  
|**COT (** _float_exp_ **)** (ODBC 1.0)|*Float_exp*의 코탄젠트를 반환 합니다. 여기서 *float_exp* 는 라디안으로 표현 된 각도입니다.|  
|**도 (** _numeric_exp_ **)** (ODBC 2.0)|*Numeric_exp* 라디안에서 변환 된 각도 수를 반환 합니다.|  
|**EXP (** _float_exp_ **)** (ODBC 1.0)|*Float_exp*의 지 수 값을 반환 합니다.|  
|**FLOOR (** _numeric_exp_ **)** (ODBC 1.0)|*Numeric_exp*보다 작거나 같은 최대 정수를 반환 합니다. 반환 값은 입력 매개 변수와 동일한 데이터 형식입니다.|  
|**로그 (** _float_exp_ **)** (ODBC 1.0)|*Float_exp*의 자연 로그를 반환 합니다.|  
|**LOG10 (** _float_exp_ **)** (ODBC 2.0)|*Float_exp*의 밑이 10 인 로그를 반환 합니다.|  
|**MOD (** _integer_exp1_, _integer_exp2_**)** (ODBC 1.0)|*Integer_exp2*으로 나눈 *integer_exp1* 나머지 (모듈러스)를 반환 합니다.|  
|**PI ()** (ODBC 1.0)|Pi의 상수 값을 부동 소수점 값으로 반환 합니다.|  
|**POWER (** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|*Numeric_exp* 의 값을 *integer_exp*의 거듭제곱으로 반환 합니다.|  
|**라디안 (** _numeric_exp_ **)** (ODBC 2.0)|*Numeric_exp* 도에서 변환 된 라디안 수를 반환 합니다.|  
|**RAND (**[*integer_exp*]**)** (ODBC 1.0)|선택적 초기값으로 *integer_exp* 를 사용 하 여 임의의 부동 소수점 값을 반환 합니다.|  
|**ROUND (** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|소수점 오른쪽 *integer_exp* 자릿수로 반올림 *numeric_exp* 를 반환 합니다. *Integer_exp* 음수 이면 *numeric_exp* 소수점 왼쪽에 &#124;*integer_exp*&#124;으로 반올림 됩니다.|  
|**SIGN (** _numeric_exp_ **)** (ODBC 1.0)|*Numeric_exp*의 부호 표시기를 반환 합니다. *Numeric_exp* 이 0 보다 작은 경우-1이 반환 됩니다. *Numeric_exp* 0 이면 0이 반환 됩니다. *Numeric_exp* 이 0 보다 크면 1이 반환 됩니다.|  
|**SIN (** _float_exp_ **)** (ODBC 1.0)|*Float_exp*의 사인을 반환 합니다. 여기서 *float_exp* 는 라디안으로 표시 된 각도입니다.|  
|**SQRT (** _float_exp_ **)** (ODBC 1.0)|*Float_exp*의 제곱근을 반환 합니다.|  
|**황갈색 (** _float_exp_ **)** (ODBC 1.0)|*Float_exp*의 탄젠트를 반환 합니다. 여기서 *float_exp* 는 라디안으로 표시 된 각도입니다.|  
|**TRUNCATE (** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|소수점이 하 *integer_exp* 위치로 잘린 *numeric_exp* 반환 합니다. *Integer_exp* 음수 이면 *numeric_exp* 소수점 왼쪽의&#124; *integer_exp* &#124;으로 잘립니다.|
