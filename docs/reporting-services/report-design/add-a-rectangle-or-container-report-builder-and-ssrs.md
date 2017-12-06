---
title: "사각형 또는 컨테이너 추가(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10061"
- sql13.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 706d719a813508541f3eda5df4045937a3af4643
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>사각형 또는 컨테이너 추가(보고서 작성기 및 SSRS)
  보고서 영역을 구분하거나, 보고서 영역을 강조하거나, 하나 이상의 보고서 항목에 대해 배경을 제공하기 위해 그래픽 요소가 필요한 경우 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서에 사각형을 추가합니다. 사각형은 보고서에서 데이터 영역이 렌더링되는 방식을 제어하는 데 도움이 되는 컨테이너로도 사용됩니다. 배경색 및 테두리 색과 같은 사각형 속성을 편집하여 사각형의 모양을 사용자 지정할 수 있습니다. 사각형을 컨테이너로 사용하는 방법은 [사각형 및 선&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md) 및 [행렬 및 차트에 같은 데이터 표시&#40;보고서 작성기&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)를 참조하세요.    
   
## <a name="to-add-a-rectangle"></a>사각형을 추가하려면    
    
1.  **삽입** 탭의 **보고서 항목** 그룹에서 **사각형**을 클릭합니다.    
    
2.  디자인 화면에서 사각형 왼쪽 위 모퉁이를 배치할 위치를 클릭한 다음 오른쪽 아래 모퉁이로 지정할 위치까지 끕니다.    
    
     커서를 이동할 때 커서가 디자인 화면의 다른 개체와 일렬이 되면 "맞춤선"이 나타납니다. 맞춤선을 사용하면 개체를 쉽게 정렬할 수 있습니다.    
    
## <a name="to-create-a-container"></a>컨테이너를 만들려면    
    
1.  보고서에 사각형 보고서 항목을 추가합니다.    
    
2.  다른 보고서 항목을 사각형으로 끌어옵니다.    
    
    > [!NOTE]    
    >  사각형은 사각형 안에서 만들거나 사각형 안으로 끌어 놓은 항목에 대한 컨테이너입니다. 디자인 화면에서 기존 항목을 포함하도록 사각형을 그려도 사각형이 기존 항목의 컨테이너로 동작하지 않습니다.    
    
## <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>색, 스타일 또는 두께와 같은 사각형 속성을 변경하려면    
    
1.  사각형을 선택한 다음 홈 탭의 **테두리** 섹션에서 선 색, 스타일 또는 두께 옵션을 클릭합니다.    
    
2.  **테두리** 단추 옆의 화살표를 클릭하여 변경할 사각형의 면을 지정합니다.    
    
    > [!NOTE]    
    >  선 스타일을 **이중선** 으로 설정하고 선 두께를 1 1/2pt 이하로 설정하면 보고서 작성기, 보고서 디자이너 또는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털에서 보고서를 실행할 때 선이 이중선으로 표시되지 않을 수 있습니다. 보고서를 Microsoft Word 및 Acrobat PDF 같은 다른 형식으로 내보내면 이중선이 표시됩니다.    
    
## <a name="see-also"></a>관련 항목:    
 [사각형 및 선&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)     
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)    
    
  
