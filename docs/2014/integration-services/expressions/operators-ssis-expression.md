---
title: 연산자(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cbceb75a036343b0d116481c5e36e3da3aa63a85
ms.sourcegitcommit: 87fec38a515a7c524b7c99f99bc6f4d338e09846
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2018
ms.locfileid: "51272591"
---
# <a name="operators-ssis-expression"></a>연산자(SSIS 식)
  이 섹션에서는 식 언어가 제공하는 연산자 및 식 계산기에 사용되는 연산자 우선 순위 및 계산 방향에 대해 설명합니다.  
  
 다음 표에서는 이 섹션의 연산자에 대한 항목을 나열합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[캐스트&#40;SSIS 식&#41;](cast-ssis-expression.md)|식의 데이터 형식을 다른 데이터 형식으로 변환합니다.|  
|[&#40;&#41;&#40;괄호&#41;&#40;SSIS 식&#41;](parentheses-ssis-expression.md)|식의 계산 순서를 식별합니다.|  
|[+&#40;더하기&#41;&#40;SSIS&#41;](add-ssis.md)|두 숫자 식을 더합니다.|  
|[+&#40;연결&#41; &#40;SSIS 식&#41;](concatenate-ssis-expression.md)|두 식을 연결합니다.|  
|[-&#40;빼기&#41;&#40;SSIS 식&#41;](subtract-ssis-expression.md)|첫 번째 숫자 식에서 두 번째 식을 뺍니다.|  
|[-&#40;부정&#41; &#40;SSIS 식&#41;](negate-ssis-expression.md)|숫자 식을 부정합니다.|  
|[&#42;&#40;곱하기&#41;&#40;SSIS 식&#41;](multiply-ssis-expression.md)|두 숫자 식을 곱합니다.|  
|[나누기&#40;SSIS 식&#41;](divide-ssis-expression.md)|첫 번째 숫자 식을 두 번째 숫자 식으로 나눕니다.|  
|[&#40;모듈로&#41; &#40;SSIS 식&#41;](modulo-ssis-expression.md)|첫 번째 숫자 식을 두 번째 식으로 나눈 다음 나머지의 정수 부분을 제공합니다.|  
|[&#124;&#124;&#40;논리적 OR&#41;&#40;SSIS 식&#41;](logical-or-ssis-expression.md)|논리적 OR 연산을 수행합니다.|  
|[&&&#40;논리적 AND&#41;&#40;SSIS 식&#41;](logical-and-ssis-expression.md)|논리적 AND 연산을 수행합니다.|  
|[\! &#40;논리적 NOT&#41; &#40;SSIS 식&#41;](logical-not-ssis-expression.md)|부울 피연산자를 부정합니다.|  
|[&#124;&#40;포괄적 비트 OR&#41;&#40;SSIS 식&#41;](bitwise-inclusive-or-ssis-expression.md)|두 정수 값의 비트 OR 연산을 수행합니다.|  
|[^&#40;배타적 비트 OR&#41;&#40;SSIS 식&#41;](bitwise-exclusive-or-ssis-expression.md)|두 정수 값의 배타적 비트 OR 연산을 수행합니다.|  
|[&&#40;비트 AND&#41;&#40;SSIS 식&#41;](bitwise-and-ssis-expression.md)|두 정수 값의 비트 AND 연산을 수행합니다.|  
|[~&#40;비트 Not&#41;&#40;SSIS 식&#41;](bitwise-not-ssis-expression.md)|정수의 비트 부정을 수행합니다.|  
|[== &#40;같음&#41;&#40;SSIS 식&#41;](equal-ssis-expression.md)|두 식이 같은지 비교합니다.|  
|[!= &#40;같지 않음&#41;&#40;SSIS 식&#41;](unequal-ssis-expression.md)|두 식이 같지 않은지 비교합니다.|  
|[&#62;&#40;보다 큼&#41;&#40;SSIS 식&#41;](greater-than-ssis-expression.md)|비교를 수행하여 첫 번째 식이 두 번째 식보다 큰지 확인합니다.|  
|[&#60;&#40;보다 작음&#41;&#40;SSIS 식&#41;](less-than-ssis-expression.md)|첫 번째 식이 두 번째 식보다 작은지 비교합니다.|  
|[&#62;=&#40;크거나 같음&#41;&#40;SSIS 식&#41;](greater-than-or-equal-to-ssis-expression.md)|첫 번째 식이 두 번째 식보다 크거나 같은지 비교합니다.|  
|[&#60;=&#40;작거나 같음&#41;&#40;SSIS 식&#41;](less-than-or-equal-to-ssis-expression.md)|첫 번째 식이 두 번째 식보다 작거나 같은지 비교합니다.|  
|[?:&#40;조건&#41;&#40;SSIS 식&#41;](conditional-ssis-expression.md)|부울 식의 계산에 따라 두 식 중 하나를 반환합니다.|  
  
 우선 순위 계층에서 각 연산자의 배치에 대한 자세한 내용은 [Operator Precedence and Associativity](operator-precedence-and-associativity.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)   
 [고급 Integration Services 식의 예](examples-of-advanced-integration-services-expressions.md)   
 [Integration Services&#40;SSIS&#41; 식](integration-services-ssis-expressions.md)  
  
  
