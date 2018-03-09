---
title: "페이지 나누기 추가(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3846cd48-2787-47e9-b13b-7fc45a205f68
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: f264f0fc3f601ba9433f5ec591674bfa03b07779
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="add-a-page-break-report-builder-and-ssrs"></a>페이지 나누기 추가(보고서 작성기 및 SSRS)
  사각형, 데이터 영역 또는 데이터 영역 내의 그룹에 페이지 나누기를 추가하여 각 페이지의 정보 양을 제어할 수 있습니다. 페이지 나누기를 추가하면 보고서를 볼 때 각 페이지에 있는 항목만 처리하면 되기 때문에 게시된 보고서의 성능이 향상될 수 있습니다. 전체 보고서가 단일 페이지로 이뤄진 경우에는 모든 항목이 처리된 후에 보고서를 볼 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-break-to-a-data-region"></a>데이터 영역에 페이지 나누기를 추가하려면  
  
1.  디자인 화면에서 데이터 영역의 모퉁이 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
2.  **일반** 탭의 **페이지 나누기 옵션**에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **앞에 페이지 나누기 추가**. 테이블 앞에 페이지 나누기를 추가하려면 이 옵션을 선택합니다.  
  
    -   **뒤에 페이지 나누기 추가**. 테이블 뒤에 페이지 나누기를 추가하려면 이 옵션을 선택합니다.  
  
    -   **가능하면 테이블을 한 페이지에 표시**. 데이터를 한 페이지에 표시하려면 이 옵션을 선택합니다.  
  
### <a name="to-add-a-page-break-to-a-rectangle"></a>사각형에 페이지 나누기를 추가하려면  
  
1.  디자인 화면에서 페이지 나누기를 추가하려는 사각형을 마우스 오른쪽 단추로 클릭한 다음 **사각형 속성**을 클릭합니다.  
  
2.  **일반** 탭의 **페이지 나누기 옵션**에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **앞에 페이지 나누기 추가**. 사각형 앞에 페이지 나누기를 추가하려면 이 옵션을 선택합니다.  
  
    -   **뒤에 페이지 나누기 추가**. 사각형 뒤에 페이지 나누기를 추가하려면 이 옵션을 선택합니다.  
  
    -   **페이지 나누기에 테두리 생략**. 페이지 나누기에 테두리를 표시하지 않으려면 이 옵션을 선택합니다.  
  
    -   **가능하면 내용을 단일 페이지에 유지**. 사각형 내의 내용을 한 페이지에 표시하려면 이 옵션을 선택합니다.  
  
### <a name="to-add-a-page-break-to-a-row-group-in-a-table-matrix-or-list"></a>테이블, 행렬, 또는 목록의 행 그룹에 페이지 나누기를 추가하려면  
  
1.  그룹화 창에서 행 그룹을 마우스 오른쪽 단추로 클릭한 다음 **그룹 속성**을 클릭합니다.  
  
    > [!NOTE]  
    >  열 그룹에서는 페이지 나누기가 무시됩니다.  
  
2.  테이블에 있는 그룹의 각 인스턴스 사이에 페이지 나누기를 추가하려면 **페이지 나누기** 탭에서 **각 그룹 인스턴스 사이** 를 선택합니다.  
  
3.  필요에 따라 **그룹 시작 부분에도** 또는 **그룹 끝 부분에도** 를 선택하여 그룹이 테이블에서 시작하거나 끝날 때 페이지 나누기가 추가되도록 지정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [페이지 머리글 및 바닥글&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
  
  
