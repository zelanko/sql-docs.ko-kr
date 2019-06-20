---
title: 브라우저 (Cube Designer) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.view.f1
ms.assetid: efb5ee1c-de50-4bfc-83ff-08a4f03c3ece
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4415fedb492eb32c2929c50999cad1542b41ca78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064615"
---
# <a name="browser-cube-designer-analysis-services---multidimensional-data"></a>브라우저(큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **브라우저** 탭을 사용하여 큐브의 차원, 측정값 및 KPI를 탐색할 수 있습니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 큐브 브라우저는 MDX 쿼리 디자이너에 통합되어 MDX 쿼리를 만들고, 큐브를 필터링하거나 조각화하고, 계층을 드릴다운하는 데 도움이 되는 그래픽 사용자 인터페이스를 제공합니다.  
  
 합니다 **브라우저** 탭에는 두 가지 모드가 있습니다. **디자인 모드** 하 고 **쿼리 모드**합니다. 이 두 모드에서는 **메타데이터** 창의 개체를 사용하여 큐브를 탐색하거나 **메타데이터** 창에서 쿼리 영역으로 멤버를 끌어서 놓아 사용할 데이터를 검색하는 MDX 쿼리를 작성할 수 있습니다.  
  
 **찾아보기 및 그래픽 디자인 모드를 사용 하 여 쿼리**  
  
 다음 그림은 그래픽 **디자인 모드** 의 **브라우저**인터페이스를 보여 줍니다.  
  
 ![Analysis Services MDX 쿼리 디자이너, 디자인 뷰](media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX 쿼리 디자이너, 디자인 뷰")  
  
 경우 그래픽 디자인 모드에서 작업할 때 합니다 **자동** (![쿼리 자동 실행](media/rsqdicon-autoexecute.gif "쿼리 자동 실행")) 도구 모음에서 토글 단추를 선택 합니다 **브라우저** 는 메타 데이터 개체를 데이터 창에 놓을 때마다 쿼리를 실행 합니다. 사용 하 여 쿼리를 수동으로 실행할 수 있습니다 합니다 **쿼리 실행** (![쿼리를 실행](media/rsqdicon-run.gif "쿼리를 실행")) 도구 모음의 단추입니다.  
  
 그래픽 쿼리 디자이너를 **쿼리** 모드로 변경하고 MDX 문의 텍스트를 사용하려면 도구 모음에서 **디자인 모드** 단추를 클릭합니다.  
  
 **찾아보기 및 MDX 텍스트 모드를 사용 하 여 쿼리**  
  
 MDX 테스트 디자인 모드에 있는 동안에는 직접 MDX를 사용할 수 있습니다. **메타데이터** 창도 계속 사용할 수 있으므로 개체를 쿼리 디자인 영역에 추가하고 **함수** 창의 목록에서 MDX 함수 및 연산자를 끌어서 놓을 수 있습니다.  
  
 다음 그림은 쿼리 모드의 **브라우저** 인터페이스를 보여 줍니다.  
  
 ![Analysis Services MDX 쿼리 디자이너, 쿼리 뷰](media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX 쿼리 디자이너, 쿼리 뷰")  
  
 그래픽 디자인 모드에서 작업을 시작하여 필요한 개체를 추가하고 큐브를 조각화할 필터를 추가한 다음 텍스트 모드로 전환하여 생성된 기본 MDX 쿼리를 확장하고 추가 멤버 속성 및 셀 속성을 포함할 수 있습니다.  
  
 **메타데이터** 창에는 **메타데이터** 및 **함수**탭이 표시됩니다. **메타데이터** 탭에서는 차원, 계층, KPI 및 측정값을 쿼리 디자인 영역으로 끌 수 있습니다. **함수** 탭에서 함수를 쿼리 디자인 영역으로 끌 수 있습니다. 쿼리를 실행하면 MDX 쿼리의 결과가 쿼리 디자인 영역에 표시됩니다. **도구 모음** 의 **Excel에서 분석** 을 클릭하여 Microsoft Office Excel로 데이터를 내보낸 다음 피벗 테이블로 결과를 볼 수도 있습니다. 다음 섹션에서는 각 모드의 **브라우저** 에 대한 도구 모음 및 모든 창에 대해 자세히 설명합니다.  
  
 텍스트 모드에서 작업할 때 있는지 확인 합니다 **자동** (![쿼리 자동 실행](media/rsqdicon-autoexecute.gif "쿼리 자동 실행")) 도구 모음에서 설정/해제 단추를 사용할 수 없는 합니다. 그러나 수동으로 실행할 수 있습니다 쿼리를 사용 하 여 합니다 **쿼리 실행** (![쿼리를 실행](media/rsqdicon-run.gif "쿼리를 실행")) 도구 모음의 단추입니다.  
  
## <a name="sections"></a>섹션  
 **도구 모음**  
 도구 모음에는 디자인 뷰 또는 쿼리 뷰에서 사용할 수 있는 도구가 포함되어 있습니다. 도구 모음 및 이러한 기능을 사용하는 방법은 [도구 모음&#40;브라우저 탭, 큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 **Excel에서 분석**  
 **Excel에서 분석** 기능을 사용하여 현재 선택된 큐브 데이터를 Excel로 보낸 다음 피벗 테이블에서 해당 데이터를 미리 볼 수 있습니다. 현재 선택된 데이터는 **메타데이터** 창에서 추가한 항목과 필터 및 쿼리 작성 함수를 사용하여 정의한 모든 필터에 의해 결정됩니다. 자세한 내용은 [Excel에서 분석&#40;브라우저 탭, 큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 **메타데이터**  
 **메타데이터** 창을 사용하여 큐브에 포함된 개체를 보고, 계층으로 드릴다운하고, 측정값을 탐색하고 사용할 수 있습니다. 선택한 후 **보고서** 창에서 연결된 데이터를 볼 수 있습니다. 이 창에 대한 자세한 내용은 [메타데이터&#40;브라우저 탭, 큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 **필터 및 쿼리**  
 이 디자인 화면 영역에서는 **메타데이터** 창에서 개체를 끌어서 놓고 원본 큐브 또는 차원에서 필터 조건을 지정하여 MDX 쿼리를 작성할 수 있습니다. 자세한 내용은 [쿼리 및 필터&#40;브라우저 탭, 큐브 디자이너&#41;&#40;Analysis Services - 다차원 데이터&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 개체 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [다차원 모델의 큐브](multidimensional-models/cubes-in-multidimensional-models.md)   
 [큐브 디자이너 &#40;Analysis Services-다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)  
  
  
