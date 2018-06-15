---
title: 부모-자식 차원의 단항 연산자 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0b7f38bb378650fbd243441086df043295376581
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023130"
---
# <a name="parent-child-dimension-attributes---unary-operators"></a>부모-자식 차원 특성 단항 연산자
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 부모-자식 관계가 포함된 차원에서 부모 특성의 모든 계산되지 않은 멤버에 대한 사용자 지정 롤업을 결정하는 단항(또는 사용자 지정 롤업) 연산자 열을 지정하세요. 그러면 부모 멤버의 값이 계산될 때마다 멤버에 단항 연산자가 적용됩니다. 부모 특성( **Usage** =Parent)에서**UnaryOperatorColumn**은 데이터 원본 뷰에서 단항 연산자가 있는 테이블 열을 지정합니다. 이 열에 저장되어 있는 사용자 지정 롤업 연산자 값이 특성의 각 멤버에 적용됩니다.  
  
 데이터 원본 뷰의 차원 테이블에서 명명된 계산을 만들고 단항 연산자 열로 지정할 수 있습니다. '+'와 같은 단순한 식은 모든 멤버에 동일한 연산자를 반환합니다. 그러나 모든 멤버에 연산자를 반환하기만 하면 어떤 식도 사용할 수 있습니다.  
  
 부모 특성에서 **UnaryOperatorColumn** 속성 설정을 수동으로 변경하거나 비즈니스 인텔리전스 마법사의 사용자 지정 집계 정의 기능을 사용하여 차원의 멤버와 연결된 기본 집계를 바꿀 수 있습니다. 비즈니스 인텔리전스 마법사를 사용하여 이러한 구성을 설정하는 방법은 [차원에 사용자 지정 집계 추가](../../analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension.md)를 참조하세요.  
  
 부모 특성에서 **UnaryOperatorColumn** 속성의 기본 설정은 (none)이며 사용자 지정 롤업 연산자를 해제합니다. 다음 표에서는 단항 연산자를 나열하며 각 연산자가 수준에 적용될 때 어떻게 동작하는지 설명합니다.  
  
|단항 연산자|Description|  
|--------------------|-----------------|  
|+(더하기 기호)|멤버 값을 멤버 이전에 발생하는 형제 멤버의 집계 값에 추가합니다. 이 연산자는 특성에 단항 연산자 열이 정의되지 않은 경우의 기본 연산자입니다.|  
|-(빼기 기호)|멤버 값을 멤버 이전에 발생하는 형제 멤버의 집계 값에서 뺍니다.|  
|*(별표)|멤버 값을 멤버 이전에 발생하는 형제 멤버의 집계 값에 곱합니다.|  
|/(나누기 기호)|멤버 값을 멤버 이전에 발생하는 형제 멤버의 집계 값으로 나눕니다.|  
|~(물결표)|멤버 값을 무시합니다.|  
  
 빈 값과 표에 없는 값은 더하기 기호(+) 단항 연산자와 같은 것으로 처리됩니다. 연산자 선행 규칙이 없으므로 단항 연산자 열에 저장된 멤버 순서에 따라 계산 순서가 결정됩니다. 계산 순서를 변경하려면 새 특성을 만들고 해당 **Type** 속성을 **Sequence**로 설정한 다음 **Source Column** 속성의 계산 순서에 해당하는 시퀀스 번호를 할당합니다. 또한 해당 특성을 기준으로 특성의 멤버 순서를 지정해야 합니다. 비즈니스 인텔리전스 마법사를 사용하여 특성의 멤버 순서를 지정하는 방법은 [차원 순서 정의](../../analysis-services/multidimensional-models/bi-wizard-define-the-ordering-for-a-dimension.md)를 참조하세요.  
  
 **UnaryOperatorColumn** 속성을 사용하여 특성의 모든 멤버에 대해 리터럴 문자로 단항 연산자를 반환하도록 명명된 계산을 지정할 수 있습니다. 명명된 계산에 `'*'` 와 같은 리터럴 문자를 입력하기만 하면 됩니다. 이 경우 특성의 모든 멤버에 대해 기본 연산자인 더하기 기호(+)가 곱하기 연산자인 별표(*)로 변경됩니다. 자세한 내용은 [데이터 원본 뷰에서 명명된 계산 정의&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
 차원 디자이너의 **찾아보기** 탭에서 계층의 각 멤버 옆에 있는 단항 연산자를 볼 수 있습니다. 쓰기 가능 차원으로 작업할 때 단항 연산자를 변경할 수도 있습니다. 쓰기 가능한 차원이 아니면 도구를 사용하여 데이터 원본을 직접 수정해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [부모-자식 차원의 사용자 지정 롤업 연산자](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md)   
 [차원 디자이너에서 비즈니스 인텔리전스 마법사를 시작 합니다.](../../analysis-services/multidimensional-models/database-dimensions-bi-wizard-in-dimension-designer.md)  
  
  
