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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
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
 **Unorder** 함수 같은 다른 함수 또는 문에 의해 집합에 포함 되는 튜플에 적용 된 순서를 제거 합니다 [순서](../mdx/order-mdx.md) 함수입니다. 반환 된 집합의 튜플 순서는 **Unorder** 함수가 확정적이 지 않습니다.  
  
 합니다 **Unorder** 함수 집합 처리에 대 한 쿼리 최적화를 힌트로 사용 됩니다. 집합 내의 튜플 순서가 계산 이나 쿼리에 중요 한 경우 사용 하 여 **Unorder** 함수에는 이러한 경우의 성능 이점을 제공할 수 있습니다. 예를 들어 합니다 [NonEmpty (MDX)](../mdx/nonempty-mdx.md) 함수 성능이 더 뛰어나고 좀이 함수에 제공 된 집합은 보다 정렬 되지 않습니다 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 하지만 순서를 유지 해야 사용 하 여 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], 쿼리 프로세서를 수행 하려고 합니다. 등의 대부분에 대해 자동으로이 함수 함수가 **합계** 하 고 **집계**합니다. 성능 이점은 **Unorder** 은 수백만 개의 튜플로 구성 된 매우 큰 집합 뚜렷하게 나타날 수만 있습니다.  
  
## <a name="example"></a>예제  
 다음 의사 코드에서는 이 함수에 대한 구문을 보여 줍니다.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
