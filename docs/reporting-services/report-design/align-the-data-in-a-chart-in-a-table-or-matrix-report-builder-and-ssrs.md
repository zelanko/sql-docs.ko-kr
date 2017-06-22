---
title: "테이블 또는 행렬 (보고서 작성기 및 SSRS)에서 차트의 데이터 정렬 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d64ebc0ee2345088419e44ab819c0d94d26274a8
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>테이블 또는 행렬에서 차트의 데이터 정렬(보고서 작성기 및 SSRS)
  스파크라인과 데이터 막대는 불필요한 정보는 거의 없이 많은 정보를 제공하는 작고 단순한 차트입니다. 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서에서 이 옵션을 선택하면 스파크라인과 데이터 막대의 값이 테이블 또는 행렬의 전체 셀에서 정렬됩니다. 이는 기반 데이터에서 누락된 값이 있어도 마찬가지입니다.  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 이 이미지에서 세로 막대형 차트에는 각 직원의 일일 판매량이 표시됩니다. 직원의 판매량이 없는 일의 경우 차트에서 공백으로 표시되고 이후의 일이 가로로 정렬됩니다. 또한 각 차트의 크기를 상대적으로 지정하여 차트를 세로로 맞춥니다. 자세한 내용은 [스파크라인 및 데이터 막대 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="align-the-data-in-a-sparkline-or-data-bar"></a>스파크라인이나 데이터 막대의 데이터 정렬  
  
1.  테이블이나 행렬에[스파크라인 또는 데이터 막대를 추가](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) 합니다.  
  
2. 스파크라인이나 데이터 막대를 클릭한 다음 **가로 축 속성** 또는 **세로 축 속성**을 클릭합니다.  
  
2.  **축 옵션** 탭에서 **축 정렬 기준** 상자를 선택한 다음 드롭다운 상자에서 축을 정렬할 그룹을 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [스파크라인 및 데이터 막대 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
