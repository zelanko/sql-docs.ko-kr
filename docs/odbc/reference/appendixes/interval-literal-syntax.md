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
manager: craigg
ms.openlocfilehash: d477dbc6b54d7ebd82b7e2ef8611f5f6dd807e83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188820"
---
# <a name="interval-literal-syntax"></a>간격 리터럴 구문
ODBC의 간격 리터럴에 대 한 구문을 사용 됩니다.  
  
 *interval-literal ::= INTERVAL* [+ *&#124;* -] *interval-string interval-qualifier*  
  
 *interval-string* ::= *quote* { *year-month-literal* &#124; *day-time-literal* } *quote*  
  
 *year-month-literal* ::= *years-value* &#124; [*years-value* -] *months-value*  
  
 *day-time-literal* ::= *day-time-interval* &#124; *time-interval*  
  
 *day-time-interval* ::= *days-value* [*hours-value* [:*minutes-value*[:*seconds-value*]]]  
  
 *time-interval* ::= *hours-value* [:*minutes-value* [:*seconds-value* ] ]  
  
 &#124; *minutes-value* [:*seconds-value* ]  
  
 &#124; *seconds-value*  
  
 *years-value* ::= *datetime-value*  
  
 *months-value* ::= *datetime-value*  
  
 *days-value* ::= *datetime-value*  
  
 *hours-value* ::= *datetime-value*  
  
 *minutes-value* ::= *datetime-value*  
  
 *seconds-value* ::= *seconds-integer-value* [.[*seconds-fraction*] ]  
  
 *seconds-integer-value* ::= *unsigned-integer*  
  
 *seconds-fraction* ::= *unsigned-integer*  
  
 *datetime-value* ::= *unsigned-integer*  
  
 *interval-qualifier* ::= *start-field* TO *end-field* &#124; *single-datetime-field*  
  
 *start-field* ::= *non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *end-field* ::= *non-second-datetime-field* &#124; SECOND[(*interval-fractional-seconds-precision*)]  
  
 *단일 날짜/시간 필드* :: = *비-두 번째-날짜/시간-필드* [(*간격 최고의-필드 정밀도*)] &#124; 두 번째 [(*최고의 필드 정밀도 간격*  [, (*간격 소수-시간 (초)-정밀도*)]  
  
 *날짜/시간 필드* :: = *비-두 번째-날짜/시간-필드* &#124; 두 번째  
  
 *두 번째-날짜/시간-필드가 아닌* :: = 연도 &#124; 월 &#124; 일 &#124; 시간 &#124; 분  
  
 *interval-fractional-seconds-precision* ::= *unsigned-integer*  
  
 *interval-leading-field-precision* ::= *unsigned-integer*  
  
 *quote* ::= '  
  
 *unsigned-integer* ::= *digit...*
