---
title: "스파크 라인과 데이터 막대 (보고서 작성기 및 SSRS)를 추가 합니다. | Microsoft Docs"
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
ms.assetid: 0b297c2e-d48b-41b0-aabd-29680cdcdb05
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a9f084fc55a0f3011a40c6f2d8a2cfcdf61dc9f2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="add-sparklines-and-data-bars-report-builder-and-ssrs"></a>스파크라인 및 데이터 막대 추가(보고서 작성기 및 SSRS)
  스파크라인과 데이터 막대는 불필요한 정보는 거의 없이 많은 정보를 제공하는 작은 여분의 차트입니다. 자세한 내용은 [스파크라인 및 데이터 막대 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)를 참조하세요.  
  
 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 스파크라인과 데이터 막대는 가장 일반적으로 테이블이나 행렬의 셀에 배치됩니다. 일반적으로 스파크라인은 각각 한 계열만 표시하며 데이터 막대는 하나 이상의 데이터 요소를 포함할 수 있습니다. 스파크라인과 데이터 막대는 모두 테이블이나 행렬의 각 행에 대한 계열 정보를 반복하여 효과를 끌어냅니다.  
  
## <a name="to-add-a-sparkline-or-data-bar-to-a-table-or-matrix"></a>테이블이나 행렬에 스파크라인 또는 데이터 막대를 추가하려면  
  
1.  [테이블](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) 이나 [행렬](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md) 을 아직 만들지 않은 경우 표시할 데이터가 포함된 테이블이나 행렬을 만듭니다.  
  
2.  테이블이나 행렬에 열을 삽입합니다. 자세한 내용은 [열 삽입 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)를 참조하세요.  
  
3.  **삽입** 탭에서 **스파크라인** 또는 **데이터 막대**를 클릭한 다음 새 열의 셀을 클릭합니다.  
  
    > [!NOTE]  
    >  스파크라인은 테이블의 세부 그룹에는 배치할 수 없으며 그룹과 연결된 셀에 배치해야 합니다.  
  
4.  **스파크라인/데이터 막대 유형 변경** 대화 상자에서 원하는 스파크라인이나 데이터 막대의 유형을 클릭한 다음 **확인**을 클릭합니다.  
  
5.  스파크라인이나 데이터 막대를 클릭합니다.  
  
     **차트 데이터** 창이 열립니다.  
  
6.  **값** 영역에서 **필드 추가** 더하기 기호(**+**)를 클릭한 다음 차트에 표시할 값이 포함된 필드를 클릭합니다.  
  
7.  **범주 그룹** 영역에서 **필드 추가** 더하기 기호(**+**)를 클릭한 다음 그룹화할 값이 포함된 필드를 클릭합니다.  
  
     일반적으로 스파크라인과 데이터 막대의 경우 각 행에 한 계열만 필요하기 때문에 **계열 그룹** 영역에 필드를 추가하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [테이블 또는 행렬에서 차트의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  

