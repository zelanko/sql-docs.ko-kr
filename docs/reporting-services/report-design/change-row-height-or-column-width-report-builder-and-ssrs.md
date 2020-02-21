---
title: 행 높이 또는 열 너비 변경(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: adf756e3ef9cbed7689a5cceb80e6ef4d93e2fb9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581724"
---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>행 높이 또는 열 너비 변경(보고서 작성기 및 SSRS)
  행 높이를 설정하면 렌더링되는 보고서의 최대 행 높이가 지정됩니다. 하지만 기본적으로 행의 입력란은 런타임에 행의 데이터 크기에 맞게 세로로 늘어나도록 설정되어 있으므로 행 높이가 지정한 높이를 초과할 수 있습니다. 고정 행 높이를 설정하려면 입력란 속성을 변경하여 입력란이 자동으로 늘어나지 않도록 해야 합니다.  
  
 열 너비를 설정하면 렌더링되는 보고서의 최대 열 너비가 지정됩니다. 열은 텍스트 크기에 맞게 너비가 자동으로 변경되지는 않습니다.  
  
 행 또는 열의 셀에 사각형 또는 데이터 영역이 들어 있는 경우 셀의 최소 높이 및 너비는 포함된 항목의 높이 및 너비에 따라 결정됩니다. 자세한 내용은 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>행 핸들을 이동하여 행 높이를 변경하려면  
  
1.  디자인 뷰에서 테이블릭스 데이터 영역의 아무 곳이나 클릭하여 선택합니다. 테이블릭스 데이터 영역의 바깥쪽 테두리에 회색 행 핸들이 나타납니다.  
  
2.  늘리려는 쪽의 행 핸들을 포인터로 가리킵니다. 양방향 화살표가 나타납니다.  
  
3.  행의 가장자리를 클릭한 상태로 위쪽 또는 아래쪽으로 이동하여 행 높이를 조정합니다.  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>셀 속성을 설정하여 행 높이를 변경하려면  
  
1.  디자인 뷰에서 테이블 행의 셀을 클릭합니다.  
  
     ![테이블의 선택된 셀](../../reporting-services/report-design/media/table-selectcell.png "테이블의 선택된 셀")  
  
2.  표시되는 **속성** 창에서 **높이** 속성을 수정한 다음 **속성** 창 외부 아무 곳이나 클릭합니다.  
  
     ![선택한 테이블 셀의 속성 창](../../reporting-services/report-design/media/cell-propertiespane.png "선택한 테이블 셀의 속성 창")  
  
### <a name="to-prevent-a-row-from-automatically-expanding-vertically"></a>행 높이가 자동으로 늘어나지 않도록 하려면  
  
1.  디자인 뷰에서 테이블릭스 데이터 영역의 아무 곳이나 클릭하여 선택합니다. 테이블릭스 데이터 영역의 바깥쪽 테두리에 회색 행 핸들이 나타납니다.  
  
2.  행 핸들을 클릭하여 행을 선택합니다.  
  
3.  속성 창에서 CanGrow를 **False**로 설정합니다.  
  
    > [!NOTE]  
    >  속성 창이 표시되지 않는 경우 **보기** 메뉴에서 **속성**을 클릭하세요.  
  
### <a name="to-change-column-width"></a>열 너비를 변경하려면  
  
1.  디자인 뷰에서 테이블릭스 데이터 영역의 아무 곳이나 클릭하여 선택합니다. 테이블릭스 데이터 영역의 바깥쪽 테두리에 회색 열 핸들이 나타납니다.  
  
2.  늘리려는 쪽의 열 핸들을 포인터로 가리킵니다. 양방향 화살표가 나타납니다.  
  
3.  열의 가장자리를 클릭한 상태로 왼쪽 또는 오른쪽으로 이동하여 열 너비를 조정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블릭스 데이터 영역(보고서 작성기 및 SSRS)](tablix-data-region-report-builder-and-ssrs.md)   
 [테이블릭스 데이터 영역 셀, 행 및 열(보고서 작성기 및 SSRS)](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)   
 [테이블(보고서 작성기 및 SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [행렬(보고서 작성기 및 SSRS)](create-a-matrix-report-builder-and-ssrs.md)   
 [목록(보고서 작성기 및 SSRS)](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록(보고서 작성기 및 SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
