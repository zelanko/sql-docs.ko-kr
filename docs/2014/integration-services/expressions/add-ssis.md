---
title: + (추가)(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9341cb3647db9e8e7061b1418b169c4ac4d158d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769629"
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
 [연산자 우선 순위 및 계산 방향](operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](operators-ssis-expression.md)  
  
  
