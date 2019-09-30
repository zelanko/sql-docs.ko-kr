---
title: '! (논리적 Not)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ce0a8e44a89dbac275b8c2df320a20e7bc14f14
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297493"
---
# <a name="-logical-not-ssis-expression"></a>! (논리적 Not)(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  부울 피연산자를 부정합니다.  
  
> [!NOTE]  
>  ! 연산자는 다른 연산자와 함께 사용할 수 없습니다. 예를 들어 ! 연산자와 > 연산자를 !> 연산자로 결합할 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>인수  
 *boolean_expression*  
 부울로 계산되는 유효한 식입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 DT_BOOL  
  
## <a name="remarks"></a>Remarks  
 다음 표에서는 ! 연산의 결과를 지정합니다.  
  
|원래 부울 식|! 연산자를 적용한 후|  
|---------------------------------|------------------------------------|  
|TRUE|FALSE|  
|NULL|NULL|  
|FALSE|TRUE|  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 **Color** 열의 값이 "red"이면 FALSE가 됩니다.  
  
```  
!(Color == "red")  
```  
  
 이 예에서는 **MonthNumber** 변수 값이 현재 월을 나타내는 정수와 같으면 TRUE가 됩니다. 자세한 내용은 [MONTH&#40;SSIS 식&#41;](../../integration-services/expressions/month-ssis-expression.md) 및 [GETDATE&#40;SSIS 식&#41;](../../integration-services/expressions/getdate-ssis-expression.md)를 참조하세요.  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>참고 항목  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
