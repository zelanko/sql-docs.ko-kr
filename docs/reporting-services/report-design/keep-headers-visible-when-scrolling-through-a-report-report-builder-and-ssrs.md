---
title: 보고서를 스크롤할 때 머리글 계속 표시(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 710b0d5be1521aed0a5ba79166e1d050b1f90c62
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs"></a>보고서를 스크롤할 때 머리글 계속 표시(보고서 작성기 및 SSRS)
  보고서를 렌더링한 다음 스크롤할 때 행 및 열 레이블이 화면에서 사라지지 않도록 하려면 행 또는 열 머리글을 고정할 수 있습니다.  
  
 행과 열을 제어하는 방법은 테이블 또는 행렬이 있는지 여부에 따라 다릅니다. 테이블이 있는 경우 정적 멤버(행 및 열 머리글)가 계속 표시되도록 구성합니다. 행렬이 있는 경우 행 및 열 그룹 머리글이 계속 표시되도록 구성합니다.  
  
 Excel로 보고서를 내보내는 경우 머리글이 자동으로 고정되지 않습니다. Excel에서 창을 고정할 수 있습니다. 자세한 내용은 [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)의 **페이지 머리글 및 바닥글** 섹션을 참조하세요.  
  
> [!NOTE]  
>  테이블에 행 및 열 그룹이 있는 경우에도 스크롤하는 동안 이러한 그룹 머리글이 계속 표시되도록 할 수 없습니다.  
  
 다음 이미지에서는 표를 보여 줍니다.  
  
 ![테이블](../../reporting-services/report-design/media/table.png "테이블")  
  
 다음 이미지에서는 행렬을 보여 줍니다.  
  
 ![행렬](../../reporting-services/report-design/media/matrix.png "행렬")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-matrix-group-headers-visible-while-scrolling"></a>스크롤하는 동안 행렬 그룹 머리글을 계속 표시하려면  
  
1.  테이블릭스 데이터 영역에서 행, 열 또는 모퉁이 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
2.  **일반** 탭의 **행 머리글** 또는 **열 머리글**아래에서 **스크롤하는 동안 머리글 계속 표시**를 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-keep-a-static-tablix-member-row-or-column-visible-while-scrolling"></a>스크롤하는 동안 정적 테이블릭스 멤버(행 또는 열)를 계속 표시하려면  
  
1.  디자인 화면에서 테이블의 아무 곳이나 클릭하여 그룹 창에 그룹과 함께 정적 멤버를 표시합니다.  
  
     ![그룹화 창](../../reporting-services/report-design/media/grouppane-updated.png "그룹화 창")  
  
     행 그룹 창에 행 그룹 계층 구조의 정적 및 동적 멤버 계층이 표시되고 열 그룹 창에 열 그룹 계층 구조의 비슷한 정적 및 동적 멤버 계층이 표시됩니다.  
  
2.  그룹화 창의 오른쪽에서 아래쪽 화살표를 클릭한 다음 **고급 모드**를 클릭합니다.  
  
3.  스크롤하는 동안 계속 표시할 정적 멤버(행 또는 열)를 클릭합니다. 속성 창에 **테이블릭스 멤버** 속성이 표시됩니다.  
  
     ![테이블릭스 구성원 속성](../../reporting-services/report-design/media/grouppane-tablixmember-updated.png "테이블릭스 구성원 속성")  
  
4.  속성 창에서 **FixedData** 를 **True**로 설정합니다.  
  
5.  스크롤하는 동안 계속 표시할 인접 멤버의 수만큼 이 과정을 반복합니다.  
  
6.  보고서를 미리 봅니다.  
  
 보고서 페이지를 아래로 또는 옆으로 이동할 때 정적 테이블릭스 멤버가 계속 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [그룹과 함께 머리글 및 바닥글 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [여러 페이지에 행 및 열 머리글 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [그룹화 창&#40;보고서 작성기&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md)  
  
  
