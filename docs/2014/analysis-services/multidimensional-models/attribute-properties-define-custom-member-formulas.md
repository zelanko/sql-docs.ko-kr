---
title: 사용자 지정 멤버 수식 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- members [Analysis Services], custom
- custom rollup formulas [Analysis Services]
- MDX [Analysis Services], custom rollup formulas
- custom member formulas [Analysis Services]
ms.assetid: 258304e2-d900-4013-97e3-871f51dfdce2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 969a8f11926957ae19512e92b68e02d12011dd03
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077277"
---
# <a name="define-custom-member-formulas"></a>사용자 지정 멤버 수식 정의
  사용자 지정 멤버 수식이라고 하는 MDX(Multidimensional Expression) 식을 정의하여 지정된 특성의 멤버에 값을 제공할 수 있습니다. 데이터 원본 뷰의 테이블 열은 특성의 각 멤버에 값을 지정하는 데 사용되는 식을 제공합니다.  
  
 사용자 지정 멤버 수식은 멤버에 연결되는 셀 값을 결정하고 측정값의 집계 함수를 무시합니다. 사용자 지정 멤버 수식은 MDX로 작성됩니다. 각각의 사용자 지정 멤버 수식은 단일 멤버에 적용됩니다. 사용자 지정 멤버 수식은 차원 테이블이나 해당 차원 테이블과 외래 키 관계에 있는 다른 테이블에 저장됩니다.  
  
 특성에서 `CustomRollupColumn` 속성은 특성의 멤버에 대한 사용자 지정 멤버 수식을 포함하는 열을 지정합니다. 열의 행이 비어 있으면 멤버의 셀 값이 정상적으로 반환됩니다. 열의 수식이 유효하지 않으면 멤버를 사용하는 셀 값이 검색될 때마다 런타임 오류가 발생합니다.  
  
 특성을 포함하는 차원 테이블이나 직접 관련된 테이블에 사용자 지정 멤버 수식을 저장할 문자열 열이 있어야만 특성에 대한 사용자 지정 멤버 수식을 지정할 수 있습니다. 하거나 설정할 수 있습니다이 경우는 `CustomRollupColumn` 속성 특성을 수동으로 하거나 비즈니스 인텔리전스 마법사의 사용자 지정 멤버 수식 설정 향상 기능을 사용 하 여 특성에 대 한 사용자 지정 멤버 수식을 사용 합니다. 이 향상 기능을 사용하는 방법에 대한 자세한 내용은 [차원에 특성의 사용자 지정 멤버 수식 설정](bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)을 참조하세요.  
  
## <a name="evaluating-custom-member-formulas"></a>사용자 지정 멤버 수식 평가  
 사용자 지정 멤버 수식은 계산 멤버와 다릅니다. 사용자 지정 멤버 수식은 차원 테이블에 있는 멤버에 적용되며 멤버의 값만 제공합니다. 이와 달리 계산 멤버는 차원 테이블에 저장되지 않으며 계산 멤버 식은 차원이나 계층에 포함된 추가 멤버에 대해 데이터와 메타데이터를 모두 정의합니다.  
  
 사용자 지정 멤버 수식은 측정값에 연결된 집계 함수를 무시합니다. 예를 들어 사용자 지정 멤버 수식을 지정하기 전에 `Sum` 집계 함수를 사용하는 측정값에는 Time 차원의 아래 멤버들에 대한 다음과 같은 값이 있습니다.  
  
-   2003: 2100  
  
    -   분기 1: 700  
  
    -   분기 2: 500  
  
    -   3 분기: 100  
  
    -   분기 4: 800  
  
-   2004: 1500  
  
    -   분기 1: 600  
  
    -   분기 2: 200  
  
    -   3 분기: 300  
  
    -   분기 4: 400  
  
 사용자 지정 멤버 수식을 사용할 경우 사용자 지정 롤업 수식에서 멤버의 값을 대신 제공합니다. 예를 들어 다음과 같은 사용자 지정 멤버 수식을 사용하여 Time 차원에 있는 2004 멤버의 Quarter 4 자식 멤버에 대한 값을 450으로 제공할 수 있습니다.  
  
```  
Time.[Quarter 3] * 1.5  
```  
  
 사용자 지정 멤버 수식은 차원 테이블의 열에 저장됩니다. 특성에 `CustomRollupColumn` 속성을 설정하여 사용자 지정 롤업 수식을 사용할 수 있습니다.  
  
 특성의 모든 멤버에 단일 MDX 식을 적용하려면 MDX 식을 리터럴 문자열로 반환하는 차원 테이블에 명명된 계산을 만듭니다. 그런 다음 구성할 특성에 `CustomRollupColumn` 속성 설정을 사용하여 명명된 계산을 지정합니다. 명명된 계산은 SQL 식으로 정의된 행 값을 반환하는 데이터 원본 뷰 테이블의 열입니다. 명명된 계산을 만드는 방법에 대한 자세한 내용은 [데이터 원본 뷰에서 명명된 계산 정의&#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
> [!NOTE]  
>  특정 특성을 기반으로 모든 수준의 멤버 대신 특정 수준의 멤버에 MDX 식을 적용하려면 수준에 식을 MDX 스크립트로 정의합니다. 자세한 내용은 [MDX 스크립팅 기본 사항&#40;Analysis Services&#41;](mdx/mdx-scripting-fundamentals-analysis-services.md)을 참조하세요.  
  
 특성의 멤버에 대해 계산 멤버와 사용자 지정 롤업 수식을 모두 사용하려면 평가 순서를 알고 있어야 합니다. 계산 멤버가 사용자 지정 롤업 수식보다 먼저 확인됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [특성 및 특성 계층](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [차원에 특성의 사용자 지정 멤버 수식 설정](bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)  
  
  
