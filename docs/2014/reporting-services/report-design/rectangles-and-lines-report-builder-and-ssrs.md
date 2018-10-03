---
title: 사각형 및 선(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5aa5aca2f152a66d838fd49662c937932586338a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48181173"
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>사각형 및 선(보고서 작성기 및 SSRS)
  사각형과 선을 사용하여 보고서에서 시각 효과를 만들 수 있습니다. 이러한 보고서 항목에 대한 표시 속성은 홈 탭의 테두리 섹션에서 설정할 수 있으며 다른 속성은 속성 창을 사용하여 설정할 수 있습니다. 사각형에는 배경색, 이미지, 도구 설명 또는 책갈피와 같은 기능을 추가할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RectanglesLinesReportParts"></a> 보고서 파트인 사각형 및 선  
 사각형과 그에 포함된 항목을 보고서와는 별도로 보고서 파트로 게시할 수 있습니다. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 사각형 내의 보고서 항목은 보고서 파트로 게시할 수 없습니다. 사용자가 사각형을 보고서에 추가하면 보고서에는 사각형과 함께 사각형에 포함된 항목도 추가됩니다.  
  

  
##  <a name="RectangleAsContainer"></a> 사각형을 컨테이너로 사용  
 사각형을 다른 항목의 컨테이너로 사용할 수 있습니다. 사각형을 이동하면 사각형 내의 항목도 함께 이동합니다. 사각형에 포함된 항목의 **Parent** 속성에는 사각형 이름이 표시됩니다. 사각형을 컨테이너로 사용하는 방법은 [사각형 또는 컨테이너 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md) 및 [행렬 및 차트에 같은 데이터 표시&#40;보고서 작성기&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)를 참조하세요.  
  
> [!NOTE]  
>  사각형은 사각형 안에서 만들거나 사각형 안으로 끌어 놓은 항목에 대한 컨테이너입니다. 디자인 화면에서 기존 항목을 포함하도록 사각형을 그려도 사각형이 기존 항목의 컨테이너로 동작하지 않습니다. 이 사각형은 기존 항목의 Parent 속성에 표시되지 않습니다.  
  
 사각형을 사용하여 보고서 항목을 포함할 때는 보고서 렌더링이 전체적으로 항목에 미치는 영향을 고려해야 합니다. 테이블과 같이 반복되는 데이터 행을 포함하는 보고서 항목은 쿼리에서 반환한 데이터를 수용하도록 확장되며 이는 사각형 내 다른 항목의 위치에 영향을 미칩니다. 항목이 데이터 영역 아래에 배치되어 있는 경우 테이블에서는 해당 항목을 아래로 밀어냅니다. 항목을 제자리에 고정하려면 테이블의 아래쪽 가장자리 위에 위쪽 가장자리가 있는 사각형의 내부에 보고서 항목을 배치합니다. 자세한 내용은 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  

  
##  <a name="ReportBorder"></a> 보고서 테두리 추가  
 선이나 사각형을 추가하지 않고 머리글, 바닥글 및 보고서 본문 자체에 테두리를 추가하여 보고서에 테두리를 추가할 수 있습니다. 자세한 내용은 [보고서에 테두리 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  

  
##  <a name="HowTo"></a> 방법 도움말 항목  
 [보고서에 테두리를 추가 &#40;보고서 작성기 및 SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [사각형 또는 컨테이너 추가 &#40;보고서 작성기 및 SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [추가 및 수정 된 줄 &#40;보고서 작성기 및 SSRS&#41;](add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>관련 항목  
 [사각형 또는 컨테이너 추가 &#40;보고서 작성기 및 SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
