---
title: "비교 연산자 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: comparison operators [MDX]
ms.assetid: 4a4bbc76-c6a2-4b19-ae75-6ac3ac14df01
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 02a4f85a2e2f0ca4589ed385900a7bd87f6f934f
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="comparison-operators"></a>비교 연산자
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  스칼라 데이터와 함께 비교 연산자를 사용합니다. 어떤 MDX 식에서든 비교 연산자를 사용할 수 있습니다.  
  
 조건을를 확인 하려면를 사용할 수도 있습니다 MDX 문과 같은 MDX 함수에서 비교 연산자 [IIf](../mdx/iif-mdx.md) 함수입니다. 하지만 어떤 조건을 확인하려고 비교 연산자를 사용하는 경우 그 조건을 기준으로 데이터를 변경하려 하기 전에 적절한 권한을 가져야 합니다. 실제 데이터에 대한 액세스 권한을 가지고 그 데이터를 쿼리할 수 있는 사용자는 추가 쿼리에 비교 연산자를 사용할 수 있습니다. 하지만 이러한 액세스 권한을 가지고 있다고 해서 모든 사용자가 데이터를 변경할 수 있는 적절한 권한을 가지고 있다든가 가지고 있어야 한다는 의미는 아닙니다. 또한 데이터 무결성을 유지하기 위해 데이터를 쿼리하고 변경할 수 있는 사람의 수를 제한합니다.  
  
 비교 연산자는 부울 데이터 형식으로 계산되어 테스트 조건의 결과에 따라 TRUE 또는 FALSE를 반환합니다.  
  
 MDX는 다음 테이블에 나열된 비교 연산자를 지원합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[=(같음)](../mdx/equal-to-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수와 같으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 부울에 TRUE가 포함되는 `0=null` 비교가 수행되지 않으면 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 비교 연산자는 Null 값을 반환합니다.|  
|[<>(같지 않음)](../mdx/not-equal-to-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수와 같지 않으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
|[>(보다 큼)](../mdx/greater-than-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수보다 더 큰 값을 가지고 있으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
|[>=(크거나 같음)](../mdx/greater-than-or-equal-to-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수보다 더 크거나 같은 값을 가지고 있으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
|[<(보다 작음)](../mdx/less-than-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수보다 더 작은 값을 가지고 있으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
|[<=(작거나 같음)](../mdx/less-than-or-equal-to-mdx.md)|Null이 아닌 인수의 경우 왼쪽 인수가 오른쪽 인수보다 더 작거나 같은 값을 가지고 있으면 TRUE를 반환하고 그렇지 않으면 FALSE를 반환합니다.<br /><br /> 인수 중 하나 또는 모두가 Null 값으로 계산되는 경우 이 연산자는 Null 값을 반환합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [연산자 &#40; MDX 구문 &#41;](../mdx/operators-mdx-syntax.md)  
  
  
