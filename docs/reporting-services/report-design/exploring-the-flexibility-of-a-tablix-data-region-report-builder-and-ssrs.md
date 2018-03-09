---
title: "테이블릭스 데이터 영역의 유연성 살펴보기(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fef19359-a618-4d21-a7e4-e391cdefd4eb
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b795c6ab6d2106c781dbcd75cbf913dda85298d5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs"></a>테이블릭스 데이터 영역의 유연성 살펴보기(보고서 작성기 및 SSRS)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서에서는 리본의 삽입 탭에서 테이블, 행렬 또는 목록 데이터 영역을 추가할 때 테이블릭스 데이터 영역에 대한 초기 템플릿으로 시작합니다. 하지만 이 템플릿만 사용할 수 있는 것은 아닙니다. 그룹, 행 및 열 같은 테이블릭스 데이터 영역 기능을 추가하거나 제거하여 데이터 표시 방식을 계속 개발할 수 있습니다.  
  
 행 또는 열 그룹을 삭제하면 그룹 값을 표시하는 데 사용되는 행과 열을 삭제할 수 있습니다. 행과 열을 수동으로 추가하거나 제거할 수도 있습니다. 행과 열을 사용하여 세부 데이터 및 그룹 데이터를 표시하는 방법을 이해하려면 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)을 참조하세요.  
  
 테이블릭스 데이터 영역의 구조를 변경한 후에는 속성을 설정하여 보고서에서 데이터 영역이 렌더링되는 방식을 제어할 수 있습니다. 예를 들어 모든 페이지의 맨 위에 열 머리글이 반복되게 하거나 그룹에 그룹 머리글을 항상 표시할 수 있습니다. 자세한 내용은 [보고서 페이지에서 테이블릭스 데이터 영역 표시 제어&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="changing-a-table-to-a-matrix"></a>테이블을 행렬로 변경  
 기본적으로 테이블에는 보고서 데이터 집합의 값을 표시하는 정보 행이 있습니다. 일반적으로 테이블에는 세부 데이터를 그룹별로 구성하는 행 그룹이 포함된 다음 각 그룹에 기반한 집계된 값이 포함됩니다. 테이블을 행렬로 변경하려면 열 그룹을 추가해야 합니다. 일반적으로 데이터 영역에 행 그룹과 열 그룹이 모두 있는 경우 세부 정보 그룹을 제거하여 그룹에 대한 요약 값만 표시할 수 있습니다. 자세한 내용은 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
 정의에 따르면 행렬을 만들 때는 테이블릭스 모퉁이 셀을 추가해야 합니다. 이 영역의 셀을 병합하고 레이블을 추가할 수 있습니다. 자세한 내용은 [데이터 영역의 셀 병합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/merge-cells-in-a-data-region-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="changing-a-matrix-to-a-table"></a>행렬을 테이블로 변경  
 기본적으로 행렬에는 행 그룹과 열 그룹이 있으며 세부 정보 그룹은 없습니다. 행렬을 테이블로 변경하려면 열 그룹을 제거하고 정보 행에 표시할 세부 정보 그룹을 추가합니다. 자세한 내용은 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) 및 [세부 정보 그룹 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="changing-a-default-list-to-a-grouped-list"></a>기본 목록을 그룹화된 목록으로 변경  
 기본적으로 목록에는 정보 행이 있고 그룹은 없습니다. 그룹 행을 사용하기 위해 목록을 변경하려면 세부 정보 그룹의 이름을 변경하고 그룹 식을 지정합니다. 자세한 내용은 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="creating-stepped-displays"></a>단계별 레이아웃 만들기  
 기본적으로 테이블릭스 데이터 영역에 그룹을 추가하면 행 그룹 머리글 영역의 셀에서 그룹 값이 열로 표시됩니다. 중첩된 그룹이 있으면 각 그룹은 별도의 열에 표시됩니다. 단계별 레이아웃을 만들려면 하나를 제외한 모든 그룹 열을 제거하고 나머지 열에 서식을 지정하여 그룹 계층 구조를 들여쓰기 형식의 텍스트로 표시합니다. 자세한 내용은 [단계별 보고서 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-a-stepped-report-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="adding-an-adjacent-details-group"></a>인접 세부 정보 그룹 추가  
 기본적으로 세부 정보 그룹은 그룹 계층 구조의 가장 안쪽 자식 그룹입니다. 그룹을 세부 정보 그룹 아래에 중첩할 수 없습니다. 예를 들어 인접 세부 정보 그룹을 추가로 만들어 판매 상위 5개 제품과 하위 5개 제품을 표시할 수 있습니다. 각 그룹에 필터 및 정렬 식을 추가할 수 있기 때문에 동일한 데이터 집합을 기반으로 하는 두 개의 세부 데이터 보기를 하나의 테이블릭스 데이터 영역에 표시할 수 있습니다. 자세한 내용은 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md), [데이터 영역에서 그룹 추가 및 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) 및 [데이터 집합에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [테이블&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [행렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
  
  
