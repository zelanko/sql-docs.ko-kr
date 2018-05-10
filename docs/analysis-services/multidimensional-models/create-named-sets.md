---
title: 명명 된 집합 만들기 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 52248437e6de4039fd0b2d7d3cc7bec42686a312
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-named-sets"></a>명명된 집합 만들기
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  명명된 집합은 MDX(Multidimensional Expressions) 쿼리 등에서 다시 사용할 수 있도록 생성되는 집합 식이나 차원 멤버 집합입니다. 큐브 데이터, 산술 연산자, 숫자 및 함수를 조합하여 명명된 집합을 만들 수 있습니다. 예를 들어 Production 측정값에 대한 최상위 값을 갖는 Factories 차원의 10개 멤버가 포함된 명명된 집합을 Top Ten Factories라는 이름으로 만들 수 있습니다. 이 Top Ten Factories를 최종 사용자가 쿼리에서 사용할 수 있습니다. 예를 들어 최종 사용자는 Top Ten Factories를 한 축에 배치하고 다른 축에는 Production을 포함하여 Measures 차원을 배치할 수 있습니다. 자세한 내용은 [다차원 모델의 계산](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md) 및 [명명된 집합을 MDX로 작성&#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)을 참조하세요.  
  
 명명된 집합을 만들려면 큐브 디자이너의 **계산** 탭에 있는 **새 명명된 집합** 명령을 사용합니다. **계산** 탭 도구 모음의 **큐브** 메뉴에서 이 명령을 호출할 수 있습니다. 이 명령은 명명된 집합에 대해 다음과 같은 옵션을 지정할 수 있는 폼을 표시합니다.  
  
 **이름**  
 명명된 집합의 이름을 선택합니다. 이 이름은 큐브를 찾아볼 때 최종 사용자에게 표시됩니다.  
  
 **식**  
 명명된 집합을 만드는 식을 지정합니다. MDX로 이 식을 작성할 수 있습니다. 식에 포함할 수 있는 항목들은 다음과 같습니다.  
  
-   차원, 수준, 측정값 등 큐브 구성 요소를 나타내는 데이터 식  
  
-   산술 연산자  
  
-   숫자  
  
-   함수  
  
 **계산 도구** 창의 **메타데이터** 탭에서 큐브 구성 요소를 복사하거나 **명명된 집합 폼 편집기** 창의 **식** 상자로 끌 수 있습니다. **계산 도구** 창의 **함수** 탭에서 함수를 복사하거나 **명명된 집합 폼 편집기** 창의 **식** 상자로 끌 수 있습니다.  
  
> [!IMPORTANT]  
>  명시적으로 해당 집합의 멤버 이름을 지정 하 여 집합 식을 만드는 경우 중괄호 쌍에 멤버 목록을 묶습니다 ({}).  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 계산](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
