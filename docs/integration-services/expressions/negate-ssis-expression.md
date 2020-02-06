---
title: '- (부정)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 25f4ee4514e56bc581b2b7c9f7f843f7aaf32baf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297470"
---
# <a name="--negate-ssis-expression"></a>-(부정)(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  숫자 식을 부정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 숫자 데이터 형식의 유효한 식입니다. 부호 있는 숫자 데이터 형식만 지원합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 *numeric_expression*의 데이터 형식을 반환합니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 **Counter** 변수 값을 부정하고 숫자 리터럴 50을 더합니다.  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>참고 항목  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
