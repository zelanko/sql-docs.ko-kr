---
title: 메타 데이터 (브라우저 탭, 큐브 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.metadatapane.f1
ms.assetid: a1ace545-488d-4645-8330-56408a5e8abd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e4aade575cdcb8260865d4a1fe9ab6f4b7941fe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077852"
---
# <a name="metadata-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>메타데이터(브라우저 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **브라우저** 탭에 있는 **메타데이터** 창을 사용하여 큐브 구조를 찾아보고, 관련 측정값을 확인하고, 차원을 보거나 만들 수 있습니다. 계층을 드릴다운하고, 사용 가능한 측정값 및 KPI 목록을 보고, 개체의 정규화된 이름을 복사할 수 있습니다.  
  
 **메타데이터** 창에서 개체 및 계층을 쿼리 작성 영역으로 끌어 새 쿼리를 만들거나 Excel에서 찾아보도록 데이터를 내보낼 수 있습니다.  
  
## <a name="options"></a>변수  
 **메타데이터**  
 현재 뷰에 사용 가능한 메타데이터가 표시됩니다. 큐브 아이콘을 클릭하여 뷰(현재 선택된 큐브 뷰 또는 큐브)를 변경한 다음 **큐브 선택** 대화 상자를 사용하여 새 큐브 또는 큐브 뷰를 선택할 수 있습니다. **측정값 그룹**을 클릭하고 드롭다운 목록에서 새 측정값 그룹을 선택하여 **메타데이터** 창에서 사용할 수 있는 개체를 필터링할 수도 있습니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 보고서 **창에서** Office 11.0 피벗 테이블 컨트롤의 필터, 데이터, 행 또는 열 영역으로 선택한 항목을 끌어서 선택한 항목에 대한 데이터를 표시합니다.  
  
 **함수**  
 **브라우저**에서 쿼리 또는 데이터 뷰를 만드는 데 사용할 수 있는 모든 함수, 연산자 및 상수 목록을 표시합니다. 함수를 사용하려면 원하는 함수를 찾아 쿼리 영역으로 끌어서 놓습니다. 구문 정의가 텍스트에 추가됩니다.  
  
> [!WARNING]  
>  그래픽 디자인 뷰에서 작업할 때는 **함수** 목록을 사용할 수 없습니다.  
  
 테이블 형식 모델을 사용할 경우 함수 목록에 MDX 함수와 DAX 함수가 모두 포함됩니다. 그 외의 경우에는 MDX만 목록에 포함됩니다. 다차원 모델은 DAX 식을 개체 정의의 일부로 포함할 수는 있지만 DAX 함수를 직접 사용할 수는 없습니다.  
  
 팁:  DAX 함수가 포함 된 폴더는 모든 대문자에 나열 됩니다. 다른 모든 폴더에는 MDX 함수가 포함됩니다. 예를 들어 통계 함수를 위한 폴더가 두 가지. **통계** 는 관련된 DAX 함수가 포함 되어 있습니다.  
  
## <a name="context-menu"></a>상황에 맞는 메뉴  
 다음 옵션은 **메타데이터** 창에서 요소를 마우스 오른쪽 단추로 클릭하면 표시되는 상황에 맞는 메뉴를 통해 사용할 수 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**쿼리에 추가**|쿼리 작성 영역의 아래쪽 창에 선택한 개체를 추가하려면 클릭합니다.|  
|**필터에 추가**|선택한 차원, 특성, 계층 또는 수준을 **브라우저**의 필터 영역에 추가하려면 클릭합니다.<br /><br /> 참고: 이 옵션은 차원, 특성, 계층, 경우에 또는 수준을 선택 합니다.|  
|**복사**|선택한 항목을 클립보드에 추가하려면 클릭합니다.<br /><br /> 참고: 이 옵션은 개체의 정규화 된 이름을 복사 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [도구 모음 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Excel에서 분석 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [쿼리 및 필터 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [브라우저 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
