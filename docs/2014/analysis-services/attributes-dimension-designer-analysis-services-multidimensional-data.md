---
title: 특성 (차원 구조 탭, 차원 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.attributespane.f1
ms.assetid: 627eaa08-7638-4edd-bdfa-0d8175a7cde5
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 693eb878c4e16e2b25dc959ce54a1e908c0d50d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161624"
---
# <a name="attributes-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>특성(차원 구조 탭, 차원 디자이너)(Analysis Services - 다차원 데이터)
  이 창을 사용하여 선택한 차원과 연결된 특성을 관리할 수 있습니다. 이 창에서 **계층** 창으로 특성을 끌어서 계층 및 수준을 만들 수 있습니다. 자세한 내용은 [계층 &#40;차원 구조 탭, 차원 디자이너&#41; &#40;Analysis Services-Multidimensional Data&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)합니다.  
  
 특성을 만들려면 목록, 트리 또는 표 모드에 있는 동안 **데이터 원본 뷰** 창에서 **특성** 창으로 열을 끕니다. 특성을 제거하려면 바로 가기 메뉴에서 **삭제** 를 선택합니다.  
  
 **특성 창을 표시 하려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 연 다음 원하는 차원을 엽니다.  
  
2.  차원이 선택되지 않은 경우에는 **차원 구조** 탭을 클릭합니다.  
  
## <a name="options"></a>변수  
 **특성**  
 선택한 차원에 사용할 수 있는 특성을 표시합니다. 이 옵션은 다음 모드에서 볼 수 있습니다.  
  
-   목록 모드  
  
     계층을 생성 및 수정하려면 이 모드를 사용합니다. 목록 모드에서 특성을 보려면 바로 가기 메뉴에서 **특성 표시 위치** 를 선택한 다음 **목록**을 클릭합니다.  
  
-   트리 모드  
  
     계층을 생성 및 수정하려면 이 모드를 사용합니다. 트리 모드에서 특성을 보려면 바로 가기 메뉴에서 **특성 표시 위치** 를 선택한 다음 **트리**를 클릭합니다.  
  
-   표 모드  
  
     차원을 수동으로 만들거나 특성 속성을 수정하려면 이 모드를 사용합니다. 표 모드에서 특성을 보려면 바로 가기 메뉴에서 **특성 표시 위치** 를 선택한 다음 **표**를 클릭합니다.  
  
## <a name="grid-mode-options"></a>표 모드 옵션  
 표 모드에서 특성을 볼 때는 다음 표에 나열된 열에 액세스할 수 있습니다.  
  
 **이름**  
 특성 이름을 표시합니다.  
  
 **Usage**  
 선택한 특성의 사용법을 설정합니다. 아래쪽 화살표를 클릭하여 다음 선택 항목 중에서 선택합니다.  
  
|값|Description|  
|-----------|-----------------|  
|Regular|일반 특성을 식별합니다.|  
|Key|차원의 키 특성을 식별합니다. 이는 차원의 리프 멤버에 해당합니다. 차원 하나에 키 특성이 하나씩만 있을 수 있습니다. 수정하려면**속성**창의 **KeyColumns** 속성 옆에 있는 줄임표 단추( **...** )를 클릭합니다.|  
|Parent|부모-자식 관계의 부모 특성을 나타냅니다. 이 관계에서 자식 특성은 항상 키 특성이어야 합니다.|  
|AccountType|계정 유형 특성을 나타냅니다. 이 값은 측정값에 대한 집계 함수를 "by account"로 설정한 경우 서버 또는 엔진에 사용됩니다.|  
  
 **형식**  
 특성 유형을 설정합니다. 아래쪽 화살표를 클릭하여 사용 가능한 선택 항목 중에서 선택합니다.  
  
 **키 열**  
 기본 열의 데이터 형식을 표시합니다. 새 특성을 만들 때는 아래쪽 화살표를 클릭하여 사용 가능한 선택 항목 중에서 선택합니다.  
  
 **이름 열**  
 기본 열의 위치를 표시합니다. 새 특성을 만들 때는 아래쪽 화살표를 클릭하여 **키와 같음** 또는 **개별 열**중 하나를 선택합니다. **개별 열** 을 선택하면 **속성** 창의 **NameColumn** 속성이 특성에 사용할 이름을 저장하는 열을 설정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [차원 구조 &#40;차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [계층 &#40;차원 구조 탭, 차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)   
 [도구 모음 &#40;차원 구조 탭, 차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)  
  
  
