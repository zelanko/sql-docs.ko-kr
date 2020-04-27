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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3387b07a8e769206a6a495addff4287000691fec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290573"
---
# <a name="interval-literal-syntax"></a>간격 리터럴 구문
다음 구문은 ODBC의 간격 리터럴에 사용 됩니다.  
  
 *interval-literal:: = interval* [+*&#124;*-] *interval-문자열 interval-한정자*  
  
 *간격-문자열* :: = *따옴표* { *년-월-리터럴* &#124; *일-시간-리터럴* } *따옴표*  
  
 *년-월-리터럴* :: = *년-값* &#124; [*년-값* -] *월-값*  
  
 *일-시간-리터럴* :: = *일-시간 간격* &#124; *시간-간격*  
  
 *일-시간-간격* :: = *일-값* [*시간-값* [:*분 값*[:*초-값*]]]  
  
 *시간 간격* :: = *시간-값* [:*분-값* [:*초-값* ]]  
  
 &#124; *분-값* [:*seconds-값* ]  
  
 &#124; *초-값*  
  
 *연도-값* :: = *datetime-값*  
  
 *months-value* :: = *datetime-value*  
  
 *days-value* :: = *datetime-value*  
  
 *시간-value* :: = *datetime-value*  
  
 *분-값* :: = *datetime-값*  
  
 *초-값* :: = *초-정수 값* [. [ *초-분수*] ]  
  
 *초-정수-값* :: = *unsigned-정수*  
  
 *초-분수* :: = *부호 없는 정수*  
  
 *datetime-value* :: = *unsigned-integer*  
  
 *interval-한정자* :: = *시작 필드* 에서 *끝 필드* &#124; *단일 날짜/시간 필드*  
  
 *시작-field* :: = *second가 아닌-datetime-field* [(*interval-선행-필드-전체 자릿수* )]  
  
 *끝 필드* :: = *초 이외의 날짜/시간 필드* &#124; 초 [(*간격-초-전체 자릿수*)]  
  
 *단일 날짜/시간 필드* :: = *두 번째-날짜/시간 필드* [(*간격-필드-전체 자릿수*)] &#124; second [(간격-*선행-필드-* 전체 자릿수 [, (*간격-초-전체 자릿수*)]  
  
 *datetime-field* :: = *second가 아닌-datetime-field* &#124; second  
  
 *second-datetime-field* :: = YEAR &#124; MONTH &#124; DAY &#124; HOUR &#124; MINUTE  
  
 *간격-초-초-전체 자릿수* :: = *부호 없는 정수*  
  
 *간격-선행 필드-전체 자릿수* :: = *부호 없는 정수*  
  
 *quote* :: = '  
  
 *unsigned-integer* :: = *digit* ...
