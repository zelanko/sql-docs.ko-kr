---
title: + (추가)(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2b7b971521991be68d69efd2519b423958ef4fbf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248863"
---
# <a name="-add-ssis"></a>+(더하기)(SSIS)
  두 숫자 식을 더합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression1, numeric_ expression2*  
 숫자 데이터 형식의 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 두 인수의 데이터 형식에 따라 결정됩니다. 자세한 내용은 [Integration Services Data Types](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 두 피연산자 중 하나가 Null이면 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 리터럴을 추가합니다.  
  
```  
5 + 6.09 + 7.0  
```  
  
 이 예에서는 **VacationHours** 열과 **SickLeaveHours** 열의 값을 더합니다.  
  
```  
VacationHours + SickLeaveHours  
```  
  
 이 예에서는 **StandardCost** 열에 계산된 값을 추가합니다. 변수 **Profit%** 은 이름에 % 문자가 포함되어 있으므로 대괄호로 묶어야 합니다. 자세한 내용은 [식별자&#40;SSIS&#41;](identifiers-ssis.md)를 참조하세요.  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>관련 항목  
 [연산자 우선순위 및 결합성](operator-precedence-and-associativity.md)   
 [연산자 &#40;SSIS 식&#41;](operators-ssis-expression.md)  
  
  
