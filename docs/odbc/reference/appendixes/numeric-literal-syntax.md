---
title: 숫자 리터럴 구문을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0863af2ae1fef38107a33ea99de330d547d7d2f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="numeric-literal-syntax"></a>숫자 리터럴 구문
Odbc에서 숫자 리터럴을에 다음 구문이 사용 됩니다.  
  
 *숫자 리터럴* :: = *서명 숫자-리터럴 &#124; 부호 없는 숫자-리터럴*  
  
 *부호 있는 숫자-리터럴* :: = [*기호*] *부호 없는 숫자-리터럴*  
  
 *부호 없는 숫자-리터럴* :: = *정확한 숫자-리터럴 &#124; 대략적인 숫자-리터럴*  
  
 *정확한 숫자-리터럴* :: = *부호 없는 정수* [*기간*[*부호 없는 정수*]]  *&#124;기간 부호 없는 정수*  
  
 *sign* :: = *더하기 기호 &#124; 빼기 기호*  
  
 *대략적인 숫자-리터럴* :: = *E가 수의 지 수*  
  
 *가 수* :: = *정확한 숫자-리터럴*  
  
 *지 수* :: = *부호 있는 정수*  
  
 *부호 있는 정수* :: = [*기호*] *부호 없는 정수*  
  
 *부호 없는 정수* :: = *자리...*  
  
 *더하기 기호* :: = *+*  
  
 *빼기 기호* :: =-  
  
 *자리* :: 1 = &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *기간* :: = 합니다.
