---
title: 간격 리터럴 구문을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 016a4fa307e9bda697dde5eec81ce606ad07a19b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907348"
---
# <a name="interval-literal-syntax"></a>간격 리터럴 구문
ODBC의 간격 리터럴에 다음 구문을 사용 됩니다.  
  
 *간격 리터럴:: 간격 =* [+*&#124;*-] *간격 문자열 간격 한정자*  
  
 *간격 문자열* :: = *견적* { *연도-월-리터럴* &#124; *일 시간 리터럴* } *따옴표*  
  
 *연도-월-리터럴* :: = *연도 값* &#124; [*연도 값* -] *달 값*  
  
 *날짜 시간 리터럴* :: = *일 간격* &#124; *시간 간격*  
  
 *일 간격* :: = *일 값* [*시간 값* [:*분 값*[:*초 값*]]]  
  
 *시간 간격* :: = *시간 값* [:*분 값* [:*초 값* ]]  
  
 &#124;*분 값* [:*초 값* ]  
  
 &#124;*초 값*  
  
 *연도 값* :: = *날짜/시간 값*  
  
 *달 값* :: = *날짜/시간 값*  
  
 *일 값* :: = *날짜/시간 값*  
  
 *시간 값* :: = *날짜/시간 값*  
  
 *분 값* :: = *날짜/시간 값*  
  
 *초 값* :: = *정수값 초* [. [ *초의 소수 부분*]]  
  
 *시간 (초)-정수 값* :: = *부호 없는 정수*  
  
 *초의 소수 부분* :: = *부호 없는 정수*  
  
 *날짜/시간 값* :: = *부호 없는 정수*  
  
 *간격 한정자* :: = *시작 필드* TO *끝 필드* &#124; *단일 날짜/시간 필드*  
  
 *시작 필드* :: = *두 번째-날짜/시간-필드가 아닌* [(*앞에 오는 필드 정밀도 간격* )]  
  
 *끝 필드* :: = *두 번째-날짜/시간-필드가 아닌* &#124; 두 번째 [(*간격 소수-초-정밀도*)]  
  
 *단일 날짜/시간 필드* :: = *두 번째-날짜/시간-필드가 아닌* [(*앞에 오는 필드 정밀도 간격*)] &#124; 두 번째 [(*앞에 오는 필드 정밀도 간격*  [, (*간격 소수-초-정밀도*)]  
  
 *날짜/시간 필드* :: = *두 번째-날짜/시간-필드가 아닌* &#124; 두 번째  
  
 *두 번째-날짜/시간-필드가 아닌* :: = 연도 &#124; 월 &#124; 일 &#124; 시간 &#124; 분  
  
 *간격 소수-초-정밀도* :: = *부호 없는 정수*  
  
 *앞에 오는 필드 정밀도 간격* :: = *부호 없는 정수*  
  
 *견적* :: = '  
  
 *부호 없는 정수* :: = *자리...*
