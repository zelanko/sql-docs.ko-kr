---
title: 간격 리터럴 구문 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6352a5ae894adb09f714a78386bfecfa3ce1df77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041626"
---
# <a name="interval-literal-syntax"></a>간격 리터럴 구문
ODBC의 간격 리터럴에 대 한 구문을 사용 됩니다.  
  
 *간격 리터럴:: 간격 =* [+ *&#124;* -] *간격 문자열 간격-한정자*  
  
 *간격-문자열* :: = *견적* {0} *연도-월-리터럴* &#124; *하루 시간 리터럴* } *견적*  
  
 *year-month-literal* ::= *years-value* &#124; [*years-value* -] *months-value*  
  
 *날짜-시간-리터럴이* :: = *날짜-시간 간격* &#124; *시간 간격*  
  
 *day-time-interval* ::= *days-value* [*hours-value* [:*minutes-value*[:*seconds-value*]]]  
  
 *time-interval* ::= *hours-value* [:*minutes-value* [:*seconds-value* ] ]  
  
 &#124;*분 값* [:*초 값* ]  
  
 &#124; *seconds-value*  
  
 *years-value* ::= *datetime-value*  
  
 *months-value* ::= *datetime-value*  
  
 *days-value* ::= *datetime-value*  
  
 *hours-value* ::= *datetime-value*  
  
 *minutes-value* ::= *datetime-value*  
  
 *초 값* :: = *정수값 초* [. [ *초의 소수*]]  
  
 *seconds-integer-value* ::= *unsigned-integer*  
  
 *seconds-fraction* ::= *unsigned-integer*  
  
 *datetime-value* ::= *unsigned-integer*  
  
 *간격 한정자* :: = *시작 필드* TO *끝 필드* &#124; *단일 날짜/시간 필드*  
  
 *start-field* ::= *non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *끝 필드* :: = *비-두 번째-날짜/시간-필드* &#124; 두 번째 [(*간격 소수-시간 (초)-정밀도*)]  
  
 *단일 날짜/시간 필드* :: = *비-두 번째-날짜/시간-필드* [(*간격 최고의-필드 정밀도*)] &#124; 두 번째 [(*최고의 필드 정밀도 간격*  [, (*간격 소수-시간 (초)-정밀도*)]  
  
 *날짜/시간 필드* :: = *비-두 번째-날짜/시간-필드* &#124; 두 번째  
  
 *두 번째-날짜/시간-필드가 아닌* :: = 연도 &#124; 월 &#124; 일 &#124; 시간 &#124; 분  
  
 *interval-fractional-seconds-precision* ::= *unsigned-integer*  
  
 *간격 최고의-필드 정밀도* :: = *부호 없는 정수*  
  
 *quote* ::= '  
  
 *unsigned-integer* ::= *digit...*
