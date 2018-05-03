---
title: 부모-자식 차원의 사용자 지정 롤업 연산자 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ced2c7f2fabb5c73364527b19423478e67d2894
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="parent-child-dimension-attributes---custom-rollup-operators"></a>부모-자식 차원 특성 사용자 지정 롤업 연산자
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  사용자 지정 롤업 연산자는 부모-자식 계층에서 멤버 값이 부모 값으로 롤업되는 방식을 제어할 수 있는 간단한 방법을 제공합니다. 부모-자식 관계를 포함하는 차원에서 부모 특성의 모든 계산되지 않는 멤버에 대한 롤업을 지정하는 단항 연산자가 있는 열을 지정합니다. 그러면 부모 멤버의 값이 계산될 때마다 멤버에 단항 연산자가 적용됩니다.  
  
 단항 연산자는 부모 특성의 **UnaryOperatorColumn** 속성으로 정의되는 열에 저장되며 특성의 각 멤버에 적용됩니다. 이 속성으로 지정한 열은 차원 테이블에 있거나 차원 테이블의 외부 키로 차원 테이블과 관련된 테이블에 있을 수 있습니다.  
  
 사용자 지정 롤업 연산자는 사용자 지정 멤버 수식과 비슷하지만 훨씬 단순한 기능을 제공합니다. 사용자 지정 멤버 수식은 MDX(Multidimensional Expressions) 식을 사용하여 멤버 롤업 방식을 결정합니다. 반면에 사용자 지정 롤업 연산자는 간단한 단항 연산자를 사용하여 멤버 값이 부모에 미치는 영향을 결정합니다. 차원에서 상위 수준의 사용자 지정 멤버 수식은 현재 수준의 사용자 지정 롤업 연산자를 재정의합니다.  
  
## <a name="custom-rollup-precedence"></a>사용자 지정 롤업 선행 규칙  
 선행 규칙에 따라, 계층 구조에서 현재 수준의 원본 특성에 대한 사용자 지정 롤업 연산자는 상위 수준의 사용자 지정 멤버 수식을 재정의합니다. 그러나 현재 수준의 사용자 지정 롤업 연산자는 상위 수준의 사용자 지정 멤버 수식에 의해 재정의됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 멤버 수식 정의](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md)   
 [부모-자식 차원의 단항 연산자](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-unary-operators.md)  
  
  
