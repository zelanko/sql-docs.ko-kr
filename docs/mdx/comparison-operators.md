---
title: 비교 연산자 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e3aa00334d98af02521005679174feb3b28c55f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001518"
---
# <a name="comparison-operators"></a>비교 연산자


  스칼라 데이터와 함께 비교 연산자를 사용합니다. 어떤 MDX 식에서든 비교 연산자를 사용할 수 있습니다.  
  
 MDX 문 및 MDX와 같은 함수에서 비교 연산자를 이용할 수 조건을 검사할 [IIf](../mdx/iif-mdx.md) 함수입니다. 하지만 어떤 조건을 확인하려고 비교 연산자를 사용하는 경우 그 조건을 기준으로 데이터를 변경하려 하기 전에 적절한 권한을 가져야 합니다. 실제 데이터에 대한 액세스 권한을 가지고 그 데이터를 쿼리할 수 있는 사용자는 추가 쿼리에 비교 연산자를 사용할 수 있습니다. 하지만 이러한 액세스 권한을 가지고 있다고 해서 모든 사용자가 데이터를 변경할 수 있는 적절한 권한을 가지고 있다든가 가지고 있어야 한다는 의미는 아닙니다. 또한 데이터 무결성을 유지하기 위해 데이터를 쿼리하고 변경할 수 있는 사람의 수를 제한합니다.  
  
 비교 연산자는 부울 데이터 형식으로 계산되어 테스트 조건의 결과에 따라 TRUE 또는 FALSE를 반환합니다.  
  
 MDX는 다음 테이블에 나열된 비교 연산자를 지원합니다.  
  
|연산자|설명|  
|--------------|-----------------|  
|[=(같음)](../mdx/equal-to-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수와 같으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 부울에 TRUE가 포함되는 `0=null` 비교가 수행되지 않으면 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 비교 연산자는 Null 값을 반환합니다.|  
|[<>(같지 않음)](../mdx/not-equal-to-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수와 같지 않으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
|[>(보다 큼)](../mdx/greater-than-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수보다 더 큰 값을 가지고 있으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
|[>=(크거나 같음)](../mdx/greater-than-or-equal-to-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수보다 더 크거나 같은 값을 가지고 있으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
|[<(보다 작음)](../mdx/less-than-mdx.md)|왼쪽된 인수가 오른쪽 인수; 보다 작은 값이 있으면 null이 아닌 인수의 경우 TRUE를 반환 그렇지 않으면 FALSE입니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
|[<=(작거나 같음)](../mdx/less-than-or-equal-to-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수보다 더 작거나 같은 값을 가지고 있으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40;MDX 구문&#41;](../mdx/operators-mdx-syntax.md)  
  
  
