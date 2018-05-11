---
title: 사용자 정의 계층 추가 또는 삭제 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00f65e2ed6b0633e1e76ea428ea671b392371ca0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="user-defined-hierarchies---add-or-delete-a-user-defined-hierarchy"></a>사용자 정의 계층-추가 또는 사용자 정의 계층을 삭제
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  **의 차원 디자이너에 있는** 차원 구조 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭의 차원에서 사용자 정의 계층을 추가하거나 제거할 수 있습니다.  
  
 사용자 정의 계층을 추가하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 계층이 인스턴스화되고 해당 차원이 처리되어야만 사용자가 계층을 사용할 수 있습니다. 자세한 내용은 참조 [다차원 모델 데이터베이스 ](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) 및 [다차원 모델 처리 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)합니다.  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>차원에 사용자 정의 계층을 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 해당 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 연 다음 작업할 차원을 엽니다.  
  
     차원은 차원 디자이너의 **차원 구조** 탭에서 열립니다.  
  
2.  **특성** 창에서 사용자 정의 계층에 사용할 특성을 **계층** 창으로 끕니다.  
  
3.  사용자 정의 계층에서 수준을 형성할 추가 특성을 끕니다.  
  
     계층에서 특성이 나열되는 순서는 중요합니다. 예를 들어 시간 계층의 연도는 계층 목록에서 일보다 상위에 표시되어야 합니다.  
  
4.  필요에 따라 사용자 정의 계층에서 수준을 올바른 위치로 끌어 수준을 다시 정렬합니다.  
  
5.  필요에 따라 사용자 정의 계층이나 해당 수준의 속성을 수정합니다.  
  
     예를 들어 일반적으로 사용자 정의 계층의 이름을 지정하고 해당 수준의 이름을 하나 이상 바꾸며 All 수준의 사용자 지정 이름을 정의할 수 있습니다. 자세한 내용은 [사용자 계층 속성](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)및 [수준 속성 - 사용자 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)을 참조하세요.  
  
    > [!NOTE]  
    >  기본적으로 사용자 정의 계층은 단순히 사용자가 정보를 보기 위해 드릴다운할 수 있는 경로입니다. 그러나 수준 간에 관계가 있으면 수준 간의 특성 관계를 구성하여 쿼리 성능을 높일 수 있습니다. 자세한 내용은 [특성 관계](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) 및 [특성 관계 정의](../../analysis-services/multidimensional-models/attribute-relationships-define.md)를 참조하세요.  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>차원에서 사용자 정의 계층을 제거하려면  
  
-   **차원 구조** 탭의 **계층** 창에서 제거할 사용자 정의 계층을 클릭합니다. 도구 모음에서 **삭제**를 클릭합니다.  
  
     — 또는 —  
  
-   **계층** 창에서 제거할 사용자 정의 계층을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
     — 또는 —  
  
-   사용자 정의 계층을 디자인 화면 밖으로 끕니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [사용자 정의 계층 만들기](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
  
  
