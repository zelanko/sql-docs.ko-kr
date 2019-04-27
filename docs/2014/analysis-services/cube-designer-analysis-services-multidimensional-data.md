---
title: 큐브 디자이너 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Cube Designer
ms.assetid: a6692467-da88-4312-8b03-d812f2ae5a96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a4333b9d2c15097b1954144738543250bb591621
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679629"
---
# <a name="cube-designer-analysis-services---multidimensional-data"></a>큐브 디자이너(Analysis Services - 다차원 데이터)
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 **큐브 디자이너**를 사용하여 큐브에 포함된 데이터를 찾아볼 수 있을 뿐만 아니라 큐브에 포함된 측정값 그룹 및 측정값, 큐브 차원 및 차원 관계, 계산, KPI(핵심 성과 지표), 동작, 파티션, 큐브 뷰 및 번역을 포함하여 기존 큐브의 다양한 속성을 편집할 수 있습니다. 다음 방법으로 **큐브 디자이너** 대화 상자를 표시할 수 있습니다.  
  
-   **솔루션 탐색기** 에서 큐브를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **열기** 또는 **디자이너 보기** 를 선택합니다.  
  
-   **솔루션 탐색기**에서 큐브를 두 번 클릭합니다.  
  
 **큐브 디자이너** 에는 다음 탭이 있습니다.  
  
## <a name="tabs"></a>탭  
  
|탭|정의|  
|---------|----------------|  
|**큐브 구조**|이 탭을 사용하여 측정값 그룹 및 측정값을 생성 및 수정하고, 큐브 차원을 추가하고, 연결된 데이터 원본 뷰에서 큐브에 포함된 개체를 표시할 수 있습니다. 이 탭에 대한 자세한 내용은 [큐브 구조&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](cube-structure-cube-designer-analysis-services-multidimensional-data.md)를 참조하세요.|  
|**차원 용도**|이 탭을 사용하여 큐브에 포함된 큐브 차원과 측정값 그룹 간에 관계를 생성 및 수정할 수 있습니다. 이 탭에 대한 자세한 내용은 [차원 용도&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)를 참조하세요.|  
|**새 명명된 집합**|이 탭을 사용하여 계산 멤버, 명명된 집합 및 MDX(Multidimensional Expressions) 스크립트를 비롯하여 큐브에 포함될 계산을 생성 및 수정할 수 있습니다. 이 탭에 대한 자세한 내용은 [계산&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)을 참조하세요.|  
|**KPI**|이 탭을 사용하여 큐브에 포함될 KPI를 생성 및 수정할 수 있습니다. 이 탭에 대한 자세한 내용은 [KPI&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)를 참조하세요.|  
|**동작**|이 탭을 사용하여 드릴스루 작업 및 보고 작업을 비롯하여 큐브에 포함될 동작을 생성 및 수정할 수 있습니다. 이 탭에 대한 자세한 내용은 [작업&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)을 참조하세요.|  
|**파티션**|이 탭을 사용하여 측정값 그룹 및 파티션에 대한 자동 관리 캐싱 설정을 비롯하여 큐브에 포함될 파티션을 생성 및 수정할 수 있습니다. 이 탭에 대한 자세한 내용은 [파티션&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](partitions-cube-designer-analysis-services-multidimensional-data.md)을 참조하세요.|  
|**큐브 뷰**|이 탭을 사용하여 큐브에 포함될 큐브 뷰를 생성 및 수정할 수 있습니다. 이 탭에 대한 자세한 내용은 [큐브 뷰&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](perspectives-cube-designer-analysis-services-multidimensional-data.md)를 참조하세요.|  
|**번역**|이 탭을 사용하여 큐브에 포함될 측정값 그룹, 측정값, 큐브 차원, 큐브 뷰, KPI, 동작, 명명된 집합 및 계산 멤버에 대한 번역을 생성 및 수정할 수 있습니다. 이 탭에 대한 자세한 내용은 [번역&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](translations-cube-designer-analysis-services-multidimensional-data.md)을 참조하세요.|  
|**브라우저**|이 탭을 사용하여 큐브에 대한 데이터 및 메타데이터를 찾아볼 수 있습니다. 이 탭에 대한 자세한 내용은 [브라우저&#40;큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)를 참조하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [큐브 개체 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [다차원 모델의 큐브](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
