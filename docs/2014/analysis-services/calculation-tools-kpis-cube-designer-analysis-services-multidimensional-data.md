---
title: 계산 도구 (Kpi 탭, 큐브 디자이너) (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpisview.calculationtoolspane.f1
ms.assetid: c030c725-7763-4c23-9988-4b274a88fc31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd16965c81ccb091d70320bd91c56112d3c15a0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088267"
---
# <a name="calculation-tools-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>계산 도구(KPI 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **KPI** 탭에 있는 **계산 도구** 창을 사용하여 KPI(핵심 성과 지표)에 사용할 수 있는 메타데이터, 함수 및 템플릿을 탐색할 수 있습니다.  
  
> [!NOTE]  
>  이 창은 폼 보기에만 표시됩니다.  
  
## <a name="options"></a>옵션  
 **메타데이터**  
 선택한 큐브의 메타데이터를 표시합니다.  
  
 해당 요소에 대한 MDX(Multidimensional Expression) 구문을 창에서 선택한 위치에 포함시키려면 선택한 요소를 **KPI 폼 편집기** 창으로 끕니다.  
  
 **함수**  
 식과 조건에 사용 가능한 함수를 표시합니다.  
  
 선택한 요소를 **KPI 폼 편집기** 창으로 끌어 창에서 선택한 위치에 해당 요소에 대한 MDX 구문을 포함시킬 수 있습니다.  
  
> [!NOTE]  
>  프로젝트 모드에서 **계산 도구** 대화 상자는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 포함된 MDXFunctions.xml이라는 XML 파일에서 이 옵션에 대한 정보를 읽습니다. 온라인 모드에서 이 옵션에 대한 정보를 해당 인스턴스의 MDSCHEMA_FUNCTIONS 스키마 행 집합에서 읽습니다.  
  
 **템플릿**  
 KPI에 사용할 수 있는 미리 정의된 템플릿을 표시합니다.  
  
 선택한 요소를 **KPI 폼 편집기** 창으로 끌어 창에서 선택한 위치에 해당 요소에 대한 MDX 구문을 포함시킬 수 있습니다.  
  
## <a name="context-menu"></a>상황에 맞는 메뉴  
 다음 옵션은 **계산 도구** 창에서 요소를 마우스 오른쪽 단추로 클릭하면 표시되는 상황에 맞는 메뉴를 통해 사용할 수 있습니다.  
  
 **복사**  
 **메타데이터** 또는 **함수** 에서 선택한 요소를 클립보드로 복사하려면 선택합니다.  
  
> [!NOTE]  
>   이 옵션은 **템플릿** 을 선택하면 표시되지 않습니다.  
  
> [!NOTE]  
>  **메타데이터** 에 표시된 차원의 **집합** 폴더 또는 **함수**에 표시된 함수의 함수 그룹 폴더와 같이 선택한 멤버를 복사할 수 없는 경우에는 이 옵션을 사용할 수 없습니다.  
  
 **멤버 필터**  
 **멤버 필터** 대화 상자를 표시하고 **메타데이터**에서 선택한 요소에 대해 표시된 멤버를 필터링하려면 선택합니다. **멤버 필터** 대화 상자에 대한 자세한 내용은 [멤버 필터 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
> [!NOTE]  
>   이 옵션은 **메타데이터** 를 선택한 경우에만 표시됩니다.  
  
> [!NOTE]  
>   이 옵션은 **메타데이터**에서 특성의 수준을 선택한 경우에만 사용할 수 있습니다.  
  
 **템플릿 추가**  
 선택한 템플릿을 기반으로 새 계산 멤버, 명명된 집합 또는 스크립트 명령을 큐브 스크립트에 추가하고 폼 보기에서 **KPI 폼 편집기** 를 표시하려면 선택합니다.  
  
> [!NOTE]  
>   이 옵션은 **메타데이터** 를 선택한 경우에만 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [큐브 디자이너 &#40;Analysis Services 다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [큐브 디자이너 &#40;Kpi&#41; &#40;Analysis Services-다차원 데이터&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)   
 [도구 모음 &#40;Kpi 탭, 큐브 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](toolbar-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI 구성 도우미 &#40;Kpi 탭, 큐브 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](kpi-organizer-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI 폼 편집기 &#40;Kpi 탭, 큐브 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](kpi-form-editor-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI 브라우저 &#40;Kpi 탭, 큐브 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](kpi-browser-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
