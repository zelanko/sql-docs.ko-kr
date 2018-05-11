---
title: ABS(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b4f95753f01cf2aec515c9badcd80fc214c98db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="abs-ssis-expression"></a>ABS(SSIS 식)
  숫자 식의 절대값을 양수로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ABS(numeric_expression)  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 부호 있는 숫자 식이거나 부호 없는 숫자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 함수에 전달된 숫자 식의 데이터 형식입니다.  
  
## <a name="remarks"></a>Remarks  
 인수가 Null이면 ABS 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 ABS 함수를 양수와 음수에 적용합니다. 둘 다 1.23을 반환합니다.  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 이 예에서는 변수 **HighTemperature** 와 **LowTempature**의 값을 빼는 식에 ABS 함수를 적용합니다.  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
