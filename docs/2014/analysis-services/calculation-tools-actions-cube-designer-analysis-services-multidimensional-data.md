---
title: 계산 도구 (동작 탭, 큐브 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.cubeeditor.actionsview.calculationtoolspane.f1
ms.assetid: a3370370-43cd-4cc2-bb9f-c0d988b96f05
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2a0fe659397a801fa69c2bb4ce2e26d7e087f9b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182929"
---
# <a name="calculation-tools-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>계산 도구(동작 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **동작** 탭에 있는 **계산 도구** 창을 사용하여 작업, 드릴스루 작업 및 보고 작업에 사용할 수 있는 메타데이터, 함수 및 템플릿을 탐색할 수 있습니다.  
  
## <a name="options"></a>변수  
 **메타데이터**  
 선택한 큐브의 메타데이터를 표시합니다.  
  
 선택한 요소를 **동작 폼 편집기**, **드릴스루 동작 폼 편집기**또는 **보고서 동작 폼 편집기** 창으로 끌어 선택한 위치에 해당 요소에 대한 MDX(Multidimensional Expressions) 구문을 포함할 수 있습니다.  
  
 **함수**  
 식과 조건에 사용 가능한 함수를 표시합니다.  
  
 선택한 요소를 **동작 폼 편집기**, **드릴스루 작업 폼 편집기**또는 **보고 작업 폼 편집기** 창으로 끌어 그 위치에 해당 요소에 대한 MDX 구문을 포함할 수 있습니다.  
  
> [!NOTE]  
>  프로젝트 모드에서 **계산 도구** 대화 상자는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 포함된 MDXFunctions.xml이라는 XML 파일에서 이 옵션에 대한 정보를 읽습니다. 온라인 모드에서 이 옵션에 대한 정보를 해당 인스턴스의 MDSCHEMA_FUNCTIONS 스키마 행 집합에서 읽습니다.  
  
 **템플릿**  
 동작에 사용 가능한 미리 정의된 템플릿을 표시합니다.  
  
 선택한 요소를 **동작 폼 편집기**, **드릴스루 작업 폼 편집기**또는 **보고 작업 폼 편집기** 창으로 끌어 그 위치에 해당 요소에 대한 MDX 구문을 포함할 수 있습니다.  
  
## <a name="context-menu"></a>상황에 맞는 메뉴  
 다음 옵션은 **계산 도구** 창에서 요소를 마우스 오른쪽 단추로 클릭하면 표시되는 상황에 맞는 메뉴를 통해 사용할 수 있습니다.  
  
|옵션|정의|  
|------------|----------------|  
|**복사**|**메타데이터** 또는 **함수** 에서 선택한 요소를 클립보드로 복사하려면 선택합니다.<br /><br /> 확인 하는 경우이 옵션이 표시 되지 않습니다 **템플릿** 을 선택 합니다. 또한 선택한 멤버 복사할 수 없습니다와 같은 경우이 옵션을 사용할 참고는 **집합** 폴더에 표시 된 차원의 **메타 데이터** 또는 에표시된함수의함수그룹폴더 **함수**합니다.|  
|**멤버 필터**|**멤버 필터** 대화 상자를 표시하고 **메타데이터**에서 선택한 요소에 대해 표시된 멤버를 필터링하려면 선택합니다. **멤버 필터** 대화 상자에 대한 자세한 내용은 [멤버 필터 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.<br /><br /> 경우에이 옵션은 표시 **메타 데이터** 을 선택 합니다. 또한에서 특성의 수준을 선택한 경우에이 옵션은 사용할 수에 유의 **메타 데이터**합니다.|  
|**템플릿 추가**|큐브 및 화면 표시에 대해 선택한 템플릿을 기반으로 새 동작, 드릴스루 작업 또는 보고 작업을 각각 **작업 폼 편집기**, **드릴스루 작업 폼 편집기**또는 **보고 작업 폼 편집기**에 추가하려면 선택합니다.<br /><br /> 참고: 경우에이 옵션이 표시 됩니다 **메타 데이터** 을 선택 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [MDX 스크립팅 기본 사항 &#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [작업 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [도구 모음 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [동작 구성 도우미 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [동작 폼 편집기 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [드릴스루 동작 폼 편집기 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [보고 동작 폼 편집기 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  