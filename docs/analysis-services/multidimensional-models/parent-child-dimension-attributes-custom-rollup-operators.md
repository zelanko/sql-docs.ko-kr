---
title: "부모-자식 차원의 사용자 지정 롤업 연산자 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84ed7fd34e017fe0ea076822d1931ea1143b5849
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
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
  
  
