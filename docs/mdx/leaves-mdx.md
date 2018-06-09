---
title: Leaves (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b18f283dce1ed5d0d3099dbdc26e27e8aff39ffc
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741252"
---
# <a name="leaves-mdx"></a>Leaves(MDX)


  모든 특성 또는 특정 차원에만 속하는 특성으로 구성된 집합을 반환합니다. 반환된 집합의 각 x 특성의 경우, x가 세분성 특성이거나 세분성 특성에 직접 또는 간접적으로 관련되어 있으면 해당 세분성은 조각에 영향을 주지 않고 x 특성에 대해 설정됩니다. **둡니다** 함수는 SCOPE 문 내에 또는 대입의 왼쪽에 사용 하기 위해 설계 되었습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Dimension_Expression*  
 차원을 반환하는 유효한 MDX(Multidimensional Expressions) 식입니다.  
  
## <a name="remarks"></a>Remarks  
 리프 멤버는 모든 특성 계층에 대한 가장 낮은 수준의 크로스 조인으로 형성된 튜플입니다. 계산 멤버는 제외됩니다.  
  
-   차원 이름이 지정 되는 **둡니다** 함수는 지정 된 차원에 대 한 키 특성의 리프 멤버를 포함 하는 집합을 반환 합니다.  
  
-   차원이 여러 측정값 그룹과 연결된 경우 현재 범위의 측정값 차원이 사용됩니다.  
  
-   차원 이름이 지정되지 않은 경우 이 함수는 전체 큐브의 리프 멤버가 포함된 집합을 반환합니다.  
  
    > [!NOTE]  
    >  차원 식이 계층으로 확인되고 계층 고유 이름이 차원 고유 이름과 같은 경우, 즉 큐브 차원 속성 HierarchyUniqueNameStyle이 ExcludeDimensionName이고 계층 이름이 차원 이름과 같으면 해당 차원이 사용됩니다.  
  
    > [!IMPORTANT]  
    >  현재 범위의 측정값 그룹에서 일부 특성의 세분성이 같지 않으면 오류가 생성됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
