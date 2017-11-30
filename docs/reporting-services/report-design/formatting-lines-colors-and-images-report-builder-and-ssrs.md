---
title: "선, 색 및 이미지 서식 지정(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.textboxproperties.border.f1
- "10502"
- "10094"
- sql13.rtp.rptdesigner.shared.borderdv.f1
- sql13.rtp.rptdesigner.reportbody.border.f1
- "10063"
- sql13.rtp.rptdesigner.pictureproperties.border.f1
- sql13.rtp.rptdesigner.rectangleproperties.border.f1
- "10055"
- "10126"
- "10066"
- sql13.rtp.rptdesigner.subreportproperties.border.f1
ms.assetid: 0f5f0d2a-9537-4152-b441-b40d7f04cf4c
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5c4ebd52faa7a3061c58037d394d53e9647c8a6c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="formatting-lines-colors-and-images-report-builder-and-ssrs"></a>선, 색 및 이미지 서식 지정(보고서 작성기 및 SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 사용하면 선, 색, 데이터 영역, 이미지 및 다른 보고서 항목의 서식을 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="borders-lines-and-gridlines"></a>테두리, 선 및 눈금선  
 테두리, 선 및 눈금선은 페이지에서 항목을 시각적으로 함께 연결하고 보고서를 읽는 사용자가 보고서의 내용을 보다 쉽게 읽을 수 있도록 도와 줍니다. 미리 정의된 테두리 스타일을 사용하여 입력란 주위의 테두리, 입력란 그룹 또는 이미지를 빠르게 추가할 수 있습니다. 또한 테두리, 선 및 눈금선의 스타일, 두께 및 색을 변경할 수 있습니다. 선택한 전체 항목 주위 또는 항목 가장자리를 따라 테두리 주위(예: 입력란 아래쪽 테두리)에 테두리가 추가됩니다.  
  
 입력란, 보고서 레이아웃 또는 이미지 주위에서 테두리 및 눈금선의 서식을 지정하려면 보고서 항목의 **속성** 대화 상자에 있는 **테두리** 탭을 사용합니다. 예를 들어 이미지 주위에 테두리를 추가하려는 경우 이미지를 마우스 오른쪽 단추로 클릭한 다음 **이미지 속성** 대화 상자에서 **테두리**를 클릭합니다.  
  
 차트에 표준 테두리 프레임 이외에도 추가 테두리 프레임을 적용할 수 있습니다. 자세한 내용은 [차트에 테두리 프레임 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)를 참조하세요.  
  
 보고서 자체에 테두리를 추가할 수도 있습니다. 자세한 내용은 [보고서에 테두리 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)에 대해 자세히 알아봅니다.  
  
## <a name="applying-background-colors"></a>배경색 적용  
 전체 보고서의 배경, 보고서 내의 입력란 또는 데이터 영역 내의 셀 또는 셀 그룹에 단색을 추가할 수 있습니다. 기본적으로 배경색은 흰색이지만 보고서 항목의 **속성** 대화 상자에 있는 **채우기** 탭에서 색을 선택할 수 있습니다. 예를 들어 입력란의 배경색을 변경할 경우 입력란을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 선택합니다. **채우기** 를 클릭한 다음 원하는 색을 선택합니다. 이 대화 상자에서 선택한 항목의 배경색을 선택하거나 배경에 나타나는 이미지를 추가할 수 있습니다.  
  
 차트를 사용하는 경우 배경색에 대한 그라데이션 및 패턴 스타일을 지정할 수도 있습니다. 자세한 내용은 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="using-images-as-formatting"></a>이미지를 서식으로 사용  
 이미지가 포함된 필드를 데이터 영역에 추가할 수 있습니다. 이미지 필드를 사용하는 경우 보고서를 실행하면 이미지가 보고서에 나타납니다.  
  
 보고서의 배경이나 사각형, 입력란, 테이블, 행렬, 차트의 일부분 또는 보고서의 본문 및 페이지 구역에 로고와 같은 이미지를 추가할 수도 있습니다. 자세한 내용은 [이미지&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [텍스트 및 자리 표시자 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [숫자 및 날짜 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [입력란의 텍스트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)   
 [채우기 대화 상자&#40;보고서 작성기 및 SSRS&#41;](http://msdn.microsoft.com/library/93a91d02-d558-4a0e-8d17-3fdf21e208d3)  
  
  
