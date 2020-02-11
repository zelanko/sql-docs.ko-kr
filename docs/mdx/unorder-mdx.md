---
title: Unorder (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097265"
---
# <a name="unorder-mdx"></a>Unorder(MDX)


  지정한 집합에서 강제 적용된 순서를 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Unorder** 함수는 [order](../mdx/order-mdx.md) 함수와 같은 다른 함수 또는 문에 의해 집합에 포함 된 튜플에 적용 되는 모든 순서를 제거 합니다. **Unorder** 함수에서 반환 된 집합의 튜플 순서는 결정 되지 않습니다.  
  
 **Unorder** 함수는 설정 처리에 대 한 쿼리 최적화에 대 한 힌트로 사용 됩니다. 집합 내의 튜플 순서가 계산 또는 쿼리에 중요 하지 않은 경우 **Unorder** 함수를 사용 하면 이러한 경우에 성능상의 이점을 제공할 수 있습니다. 예를 들어,이 함수에 제공 된 집합이 순서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 를 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]유지 해야 하는 경우 보다는 [이 함수에](../mdx/nonempty-mdx.md) 제공 된 집합이 정렬 되지 않을 때 더 나은 성능을 제공할 수 있습니다. 그러나에서는 쿼리 프로세서가 **Sum** 및 **Aggregate**와 같은 여러 함수에 대해이 함수를 자동으로 수행 하려고 합니다. **Unorder** 를 사용 하는 경우에는 수백만 개의 튜플로 구성 된 매우 큰 집합에 대해서만 성능을 향상 시킬 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 의사 코드에서는 이 함수에 대한 구문을 보여 줍니다.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
