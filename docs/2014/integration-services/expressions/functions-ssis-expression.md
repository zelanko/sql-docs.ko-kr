---
title: 함수(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- expressions [Integration Services], functions
- string functions
- SQL Server Integration Services, functions
- SSIS, functions
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4e721c7dfddb953dd82952aa51c20550e5e60eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061253"
---
# <a name="functions-ssis-expression"></a>함수(SSIS 식)
  식 언어에는 식에 사용할 함수 집합이 포함되어 있습니다. 식은 단일 함수를 사용할 수도 있지만 일반적으로 연산자와 함수를 결합하여 여러 개의 함수를 사용합니다.  
  
 함수는 다음 그룹으로 분류될 수 있습니다.  
  
-   수치 연산 함수는 매개 변수로 함수에 제공된 숫자 입력 값을 기반으로 계산을 수행하고 숫자 값을 반환합니다.  
  
-   문자열 함수는 문자열 또는 16진수 입력 값에 대해 작업을 수행하고 문자열 또는 숫자 값을 반환합니다.  
  
-   날짜 및 시간 함수는 날짜 및 시간 값에 대해 작업을 수행하고 문자열, 숫자 또는 날짜 및 시간 값을 반환합니다.  
  
-   시스템 함수는 식에 대한 정보를 반환합니다.  
  
 식 언어는 다음 수치 연산 함수를 제공합니다.  
  
|기능|Description|  
|--------------|-----------------|  
|[ABS &#40;SSIS 식&#41;](abs-ssis-expression.md)|숫자 식의 절대값을 양수로 반환합니다.|  
|[EXP &#40;SSIS 식&#41;](exp-ssis-expression.md)|밑이 e인 지정한 식의 지수를 반환합니다.|  
|[CEILING &#40;SSIS 식&#41;](ceiling-ssis-expression.md)|숫자 식보다 크거나 같은 최소 정수를 반환합니다.|  
|[FLOOR &#40;SSIS 식&#41;](floor-ssis-expression.md)|숫자 식보다 작거나 같은 최대 정수를 반환합니다.|  
|[LN &#40;SSIS 식&#41;](ln-ssis-expression.md)|숫자 식의 자연 로그를 반환합니다.|  
|[로그 &#40;SSIS 식&#41;](log-ssis-expression.md)|숫자 식의 상용 로그를 반환합니다.|  
|[POWER &#40;SSIS 식&#41;](power-ssis-expression.md)|숫자 식의 거듭제곱을 반환합니다.|  
|[ROUND &#40;SSIS 식&#41;](round-ssis-expression.md)|특정 길이나 전체 자릿수로 반올림한 숫자 식을 반환합니다. .|  
|[로그인 &#40;SSIS 식&#41;](sign-ssis-expression.md)|숫자 식의 양수(+), 음수(-) 또는 영(0) 부호를 반환합니다.|  
|[사각형 &#40;SSIS 식&#41;](square-ssis-expression.md)|숫자 식의 제곱을 반환합니다.|  
|[SQRT &#40;SSIS 식&#41;](sqrt-ssis-expression.md)|숫자 식의 제곱근을 반환합니다.|  
  
 식 계산기는 다음 문자열 함수를 제공합니다.  
  
|기능|Description|  
|--------------|-----------------|  
|[코드 포인트 &#40;SSIS 식&#41;](codepoint-ssis-expression.md)|문자 식에서 가장 왼쪽 문자의 유니코드 코드 값을 반환합니다.|  
|[FINDSTRING &#40;SSIS 식&#41;](findstring-ssis-expression.md)|식에서 지정한 문자열 항목의 인덱스(1부터 시작)를 반환합니다.|  
|[16 진수 &#40;SSIS 식&#41;](hex-ssis-expression.md)|정수의 16진수 값을 나타내는 문자열을 반환합니다.|  
|[LEN &#40;SSIS 식&#41;](len-ssis-expression.md)|문자 식에 포함된 문자의 수를 반환합니다.|  
|[왼쪽 &#40;SSIS 식&#41;](left-ssis-expression.md)|지정한 문자 식의 왼쪽부터 지정한 개수의 문자를 반환합니다.|  
|[낮은 &#40;SSIS 식&#41;](lower-ssis-expression.md)|대문자를 소문자로 변환한 후에 문자 식을 반환합니다.|  
|[LTRIM &#40;SSIS 식&#41;](trim-ssis-expression.md)|선행 공백을 제거하고 문자 식을 반환합니다.|  
|[대체 &#40;SSIS 식&#41;](replace-ssis-expression.md)|식 내의 문자열을 다른 문자열이나 빈 문자열로 바꾼 후 문자 식을 반환합니다.|  
|[복제 &#40;SSIS 식&#41;](replicate-ssis-expression.md)|지정한 횟수만큼 복제된 문자 식을 반환합니다.|  
|[역방향 &#40;SSIS 식&#41;](reverse-ssis-expression.md)|문자 식을 역 순서로 반환합니다.|  
|[오른쪽 &#40;SSIS 식&#41;](right-ssis-expression.md)|지정한 문자 식의 오른쪽에서부터 지정한 개수의 문자를 반환합니다.|  
|[RTRIM &#40;SSIS 식&#41;](rtrim-ssis-expression.md)|후행 공백을 제거하고 문자 식을 반환합니다.|  
|[부분 문자열이 &#40;SSIS 식&#41;](substring-ssis-expression.md)|문자 식의 일부를 반환합니다.|  
|[TRIM &#40;SSIS 식&#41;](trim-ssis-expression.md)|선행 및 후행 공백을 제거하고 문자 식을 반환합니다.|  
|[위 &#40;SSIS 식&#41;](upper-ssis-expression.md)|소문자를 대문자로 변환한 후에 문자 식을 반환합니다.|  
  
 식 계산기는 다음 날짜 및 시간 함수를 제공합니다.  
  
|함수|Description|  
|--------------|-----------------|  
|[DATEADD &#40;SSIS 식&#41;](dateadd-ssis-expression.md)|지정한 날짜에 날짜 또는 시간 간격을 더하여 새로운 DT_DBTIMESTAMP 값을 반환합니다.|  
|[DATEDIFF &#40;SSIS 식&#41;](datediff-ssis-expression.md)|지정한 두 날짜 간에 교차되는 날짜와 시간 경계값을 반환합니다.|  
|[DATEPART &#40;SSIS 식&#41;](datepart-ssis-expression.md)|날짜의 특정 부분을 나타내는 정수를 반환합니다.|  
|[일 &#40;SSIS 식&#41;](day-ssis-expression.md)|지정한 날짜의 일을 나타내는 정수를 반환합니다.|  
|[GETDATE &#40;SSIS 식&#41;](getdate-ssis-expression.md)|시스템의 현재 날짜를 반환합니다.|  
|[GETUTCDATE &#40;SSIS 식&#41;](getutcdate-ssis-expression.md)|시스템의 현재 날짜를 UTC 시간(국제 표준시 또는 그리니치 표준시)으로 반환합니다.|  
|[월 &#40;SSIS 식&#41;](month-ssis-expression.md)|지정한 날짜의 월을 나타내는 정수를 반환합니다.|  
|[YEAR &#40;SSIS 식&#41;](year-ssis-expression.md)|지정한 날짜의 연도를 나타내는 정수를 반환합니다.|  
  
 식 계산기는 다음 Null 함수를 제공합니다.  
  
|기능|Description|  
|--------------|-----------------|  
|[ISNULL &#40;SSIS 식&#41;](null-ssis-expression.md)|식이 Null인지 여부에 따라 부울 결과를 반환합니다.|  
|[NULL &#40;SSIS 식&#41;](null-ssis-expression.md)|요청한 데이터 형식의 Null 값을 반환합니다.|  
  
 식 이름은 대문자로 표시되지만 대/소문자를 구분하지 않습니다. 예를 들어 "null"은 "NULL"과 동일한 기능을 수행합니다.  
  
## <a name="see-also"></a>관련 항목  
 [연산자 &#40;SSIS 식&#41;](operators-ssis-expression.md)   
 [고급 Integration Services 식의 예](examples-of-advanced-integration-services-expressions.md)   
 [Integration Services&#40;SSIS&#41; 식](integration-services-ssis-expressions.md)  
  
  
