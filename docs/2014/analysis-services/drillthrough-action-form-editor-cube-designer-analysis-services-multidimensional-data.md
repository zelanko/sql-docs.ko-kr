---
title: 드릴스루 동작 폼 편집기 (동작 탭, 큐브 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.drillthroughaction.f1
ms.assetid: 225fd818-b5ea-494f-b67b-66e09798274a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8589c743e926b6654cfba123ef7a47a85c0e95d3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213233"
---
# <a name="drillthrough-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>드릴스루 동작 폼 편집기(동작 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **작업** 탭에 있는 **드릴스루 동작 폼 편집기** 창을 사용하여 **작업 구성 도우미** 창에서 선택한 드릴스루 작업을 수정할 수 있습니다. 드릴스루 동작에 대한 자세한 내용은 [작업&#40;Analysis Services - 다차원 데이터&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
> [!NOTE]  
>  드릴스루 동작은 더 이상 기본 데이터 저장소로 드릴다운하지 않습니다. 드릴스루 동작에서 액세스하는 정보는 차원 또는 계층 멤버를 사용하여 큐브 내에서 모델링해야 합니다.  
  
## <a name="options"></a>변수  
 **name**  
 동작의 이름을 입력합니다.  
  
 **동작 대상**  
 확장하면 **측정값 그룹 멤버** 옵션이 표시됩니다.  
  
 **측정값 그룹 멤버**  
 드릴스루 동작을 연결할 측정값 그룹을 선택합니다.  
  
 **조건(옵션)**  
 선택적 조건을 기술하는 MDX(Multidimensional Expression) 식을 입력합니다. 이 옵션은 **측정값 그룹 멤버**와 함께 사용되어 동작의 가용성을 추가로 제한합니다. 식은 부울 값을 반환해야 합니다. True인 경우 동작을 사용할 수 있습니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 **드릴스루 열**  
 확장하면 사용자가 이 동작을 실행할 때 반환되는 특성을 나타내는 표가 표시됩니다.  
  
> [!NOTE]  
>  둘 이상의 차원을 선택할 수 있지만 드릴스루 동작에서 한 차원을 두 번 이상 사용할 수는 없습니다.  
  
 표에는 다음 열이 있습니다.  
  
|Column|Description|  
|------------|-----------------|  
|**Dimensions**|반환 특성이 파생되는 차원을 선택합니다. 측정값을 드릴스루하려면 MEASURES를 선택합니다.|  
|**반환 열**|선택한 차원에서 동작 실행 시 반환할 특성 또는 측정값을 선택합니다.|  
  
 **추가 속성**  
 확장하면 **기본값**, **최대 행 수**, **호출**, **애플리케이션**, **설명**, **캡션**및 **MDX 캡션** 옵션이 표시됩니다.  
  
 **Default**  
 이 드릴스루 동작을 기본 드릴스루 동작으로 포함하려면 **True** 를 선택합니다. 포함하지 않으려면 **False**를 선택합니다.  
  
 클라이언트 응용 프로그램이 실행한 MDX `RETURN` 문에서 `DRILLTHROUGH` 절을 생략하면 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스는 모든 기본 드릴스루 동작을 계산하여 비어 있지 않은 집합을 반환하는 첫 번째 기본 드릴스루 작업을 실행합니다. MDX에 대 한 자세한 내용은 `DRILLTHROUGH` 문에서 참조 [DRILLTHROUGH 문 &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-drillthrough)합니다.  
  
> [!NOTE]  
>  이 옵션은 이전 버전과의 호환성을 위해 사용됩니다.  
  
 **최대 행 수**  
 드릴스루 동작에서 반환할 최대 행 수를 입력합니다. 이 옵션을 0 또는 빈 값으로 설정하면 드릴스루 동작은 검색된 모든 행을 클라이언트 애플리케이션으로 반환합니다.  
  
 **호출**  
 동작 실행 시기를 나타내는 설정을 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 클라이언트 애플리케이션에 동작 실행 시기에 대한 권장 사항만 제공할 뿐 직접 작업 호출을 제어하지는 않습니다.  
  
 다음 표에서는 사용 가능한 설정에 대해 설명합니다.  
  
|값|Description|  
|-----------|-----------------|  
|일괄 처리|동작이 일괄 처리 작업이나 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 태스크의 일부로 실행됩니다.|  
|대화형|사용자가 작업을 호출할 때 동작이 실행됩니다.|  
|열 때|큐브를 처음으로 열 때 동작이 실행됩니다.|  
  
 **응용 프로그램**  
 드릴스루 동작을 실행할 수 있는 애플리케이션 이름을 입력합니다.  
  
 이 옵션을 사용하여 이 동작을 가장 많이 사용하는 클라이언트 애플리케이션을 식별하고 팝업 메뉴에서 해당 작업 옆에 적절한 아이콘을 표시할 수도 있습니다.  
  
> [!NOTE]  
>  이 옵션은 클라이언트 애플리케이션에 동작을 실행해야 하는 클라이언트 애플리케이션에 대한 권장 사항만 제공할 뿐 직접 작업에 대한 액세스를 제어하지는 않습니다. 클라이언트 애플리케이션은 다른 클라이언트 애플리케이션에 연결된 모든 동작을 숨겨야 합니다.  
  
 **설명**  
 동작에 대한 선택적 설명을 입력합니다.  
  
 **캡션**  
 **MDX 캡션** 이 **False**로 설정된 경우 클라이언트 응용 프로그램에서 동작에 대해 표시할 캡션을 입력합니다.  
  
 **MDX 캡션** 이 **True**로 설정된 경우 캡션 문자열을 반환하는 MDX(Multidimensional Expression) 식을 입력합니다.  
  
 **캡션이 MDX 인지**  
 클라이언트 애플리케이션에서 동작에 대해 표시할 캡션을 나타내는 리터럴 문자열이 **캡션** 에 포함되어 있음을 나타내려면 **False** 를 선택합니다.  
  
 클라이언트 애플리케이션에서 동작에 대해 표시할 캡션을 나타내는 문자열을 반환하는 MDX 식이 **캡션** 에 포함되어 있음을 나타내려면 **True** 를 선택합니다. 클라이언트 애플리케이션으로 동작을 반환하기 전에 MDX 식을 확인해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Multidimensional Expression &#40;MDX&#41; 참조](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [작업 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [도구 모음 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [동작 구성 도우미 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [계산 도구 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [동작 폼 편집기 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [보고 동작 폼 편집기 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
