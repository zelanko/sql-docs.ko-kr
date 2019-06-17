---
title: Excel에서 분석 (브라우저 탭, 큐브 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.datapane.f1
- sql12.asvs.ssms.analyzeinexcel.f1
ms.assetid: 890ed457-137e-44ac-9b2c-83344a1b8fc9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b2833fb2ecbbac269442ce149cd5673abedcf83c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062372"
---
# <a name="analyze-in-excel-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Excel에서 분석(브라우저 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 개발자는**Excel에서 분석** 을 사용하여 프로젝트가 최종 사용자에게 어떻게 표시될지 빠르게 검토할 수 있습니다. **Excel에서 분석** 기능은 Microsoft Excel을 열고 작업 영역 데이터베이스에 데이터 원본을 연결한 후 자동으로 워크시트에 피벗 테이블을 추가합니다. 이 기능은 이전 릴리스에서 브라우저 탭에 포함된 피벗 테이블을 제공하던 Office Web Control을 대체합니다.  
  
 **큐브 데이터를 보려면:**  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 솔루션 탐색기에서 큐브를 두 번 클릭하여 큐브 디자이너에서 엽니다.  
  
2.  **브라우저** 탭을 클릭합니다.  
  
3.  **다시 연결** 을 클릭하여 연결의 유효성을 검사합니다.  
  
4.  메뉴 모음에서 Excel 아이콘을 클릭합니다.  
  
5.  데이터 연결을 사용할지 묻는 메시지가 표시되면 **사용**을 클릭합니다. 현재 데이터 연결을 사용하여 Excel이 열리고 데이터 탐색을 시작할 수 있도록 워크시트에 피벗 테이블이 추가됩니다.  
  
 이제 팩트 테이블에서 값 영역으로 측정값을 끌어 놓고, 행 및 열 영역으로 차원 특성을 끌어 놓음으로써 대화식으로 피벗 테이블을 작성할 수 있습니다. 계층이 있을 경우 행 및 열 영역에 추가합니다. 계층을 롤업 또는 드릴다운하여 다양한 수준의 팩트 데이터를 검색할 수 있습니다.  
  
 개체 및 데이터는 유효 사용자 또는 역할 및 큐브 뷰의 컨텍스트 내에서 표시됩니다. Excel을 사용할 경우 쿼리 실행 시 **가장 정보** 페이지에 지정된 자격 증명이 아니라 현재 사용자의 자격 증명을 사용하여 데이터 원본에 연결됩니다.  
  
> [!NOTE]  
>  Excel에서 분석 기능을 사용하려면 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]와 동일한 컴퓨터에 Excel이 설치되어 있어야 합니다. 컴퓨터에 Excel이 설치되어 있지 않을 경우 다른 컴퓨터의 Excel을 사용하여 데이터 원본으로 큐브에 연결할 수 있습니다. 그런 다음 워크시트에 피벗 테이블을 수동으로 추가할 수 있습니다. 피벗 테이블 필드 목록에 모델 개체(테이블, 열, 측정값 및 KPI)가 필드로 포함됩니다.  
  
 **Excel에서 분석** 기능에 대한 자세한 내용은 다음 리소스를 참조하십시오.  
  
 [Excel에서 분석&#40;SSAS 테이블 형식&#41;](tabular-models/analyze-in-excel-ssas-tabular.md)  
  
 [Excel에서 테이블 형식 모델 분석&#40;SSAS 테이블 형식&#41;](tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)  
  
 [큐브에서 데이터 및 메타데이터 찾아보기](multidimensional-models/browse-data-and-metadata-in-cube.md)  
  
## <a name="see-also"></a>관련 항목  
 [브라우저 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [도구 모음 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [메타 데이터 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [쿼리 및 필터 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
