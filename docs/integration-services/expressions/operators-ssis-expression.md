---
title: 연산자(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b625b23dc45a3a5ed9abc00f0068ed3e7fbfeb58
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297447"
---
# <a name="operators-ssis-expression"></a>연산자(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  이 섹션에서는 식 언어가 제공하는 연산자 및 식 계산기에 사용되는 연산자 우선 순위 및 계산 방향에 대해 설명합니다.  
  
 다음 표에서는 이 섹션의 연산자에 대한 항목을 나열합니다.  
  
|연산자|설명|  
|--------------|-----------------|  
|[캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)|식의 데이터 형식을 다른 데이터 형식으로 변환합니다.|  
|[&#40;&#41;&#40;괄호&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/parentheses-ssis-expression.md)|식의 계산 순서를 식별합니다.|  
|[+&#40;더하기&#41;&#40;SSIS&#41;](../../integration-services/expressions/add-ssis.md)|두 숫자 식을 더합니다.|  
|[+&#40;연결&#41; &#40;SSIS 식&#41;](../../integration-services/expressions/concatenate-ssis-expression.md)|두 식을 연결합니다.|  
|[-&#40;빼기&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/subtract-ssis-expression.md)|첫 번째 숫자 식에서 두 번째 식을 뺍니다.|  
|[-&#40;부정&#41; &#40;SSIS 식&#41;](../../integration-services/expressions/negate-ssis-expression.md)|숫자 식을 부정합니다.|  
|[&#42;&#40;곱하기&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/multiply-ssis-expression.md)|두 숫자 식을 곱합니다.|  
|[나누기&#40;SSIS 식&#41;](../../integration-services/expressions/divide-ssis-expression.md)|첫 번째 숫자 식을 두 번째 숫자 식으로 나눕니다.|  
|[%&#40;모듈로&#41; &#40;SSIS 식&#41;](../../integration-services/expressions/modulo-ssis-expression.md)|첫 번째 숫자 식을 두 번째 식으로 나눈 다음 나머지의 정수 부분을 제공합니다.|  
|[&#124;&#124;&#40;논리적 OR&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)|논리적 OR 연산을 수행합니다.|  
|[&&&#40;논리적 AND&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)|논리적 AND 연산을 수행합니다.|  
|[\! &#40;논리적 NOT&#41; &#40;SSIS 식&#41;](../../integration-services/expressions/logical-not-ssis-expression.md)|부울 피연산자를 부정합니다.|  
|[&#124;&#40;포괄적 비트 OR&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)|두 정수 값의 비트 OR 연산을 수행합니다.|  
|[^&#40;배타적 비트 OR&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)|두 정수 값의 배타적 비트 OR 연산을 수행합니다.|  
|[&&#40;비트 AND&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)|두 정수 값의 비트 AND 연산을 수행합니다.|  
|[~ &#40;비트 NOT&#41; &#40;SSIS 식&#41;](../../integration-services/expressions/bitwise-not-ssis-expression.md)|정수의 비트 부정을 수행합니다.|  
|[== &#40;같음&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/equal-ssis-expression.md)|두 식이 같은지 비교합니다.|  
|[\!=&#40;같지 않음&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/unequal-ssis-expression.md)|두 식이 같지 않은지 비교합니다.|  
|[&#62;&#40;보다 큼&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/greater-than-ssis-expression.md)|비교를 수행하여 첫 번째 식이 두 번째 식보다 큰지 확인합니다.|  
|[&#60;&#40;보다 작음&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/less-than-ssis-expression.md)|첫 번째 식이 두 번째 식보다 작은지 비교합니다.|  
|[&#62;=&#40;크거나 같음&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)|첫 번째 식이 두 번째 식보다 크거나 같은지 비교합니다.|  
|[&#60;=&#40;작거나 같음&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)|첫 번째 식이 두 번째 식보다 작거나 같은지 비교합니다.|  
|[?:&#40;조건&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/conditional-ssis-expression.md)|부울 식의 계산에 따라 두 식 중 하나를 반환합니다.|  
  
 우선 순위 계층에서 각 연산자의 배치에 대한 자세한 내용은 [Operator Precedence and Associativity](../../integration-services/expressions/operator-precedence-and-associativity.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [고급 Integration Services 식의 예](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
