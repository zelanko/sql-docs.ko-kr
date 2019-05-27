---
title: 열 삽입 또는 삭제(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e9db79e2-7e7d-4359-a706-cb746c94182a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e1d5f5d846a690676942e0d4ffcba0475a35595a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105683"
---
# <a name="insert-or-delete-a-column-report-builder-and-ssrs"></a>열 삽입 또는 삭제(보고서 작성기 및 SSRS)
  테이블릭스 데이터 영역의 열을 추가하거나 삭제할 수 있습니다. 테이블릭스 데이터 영역은 테이블, 행렬 또는 목록일 수 있습니다. 차트 및 계기 데이터 영역에는 다음 절차가 적용되지 않습니다.  
  
 테이블릭스 데이터 영역에서는 그룹과 연결되어 있는 열(그룹 내부의 열)이나 연결되지 않은 열(그룹 외부의 열)을 추가할 수 있습니다. 그룹 내부의 열은 고유 그룹 값마다 한 번씩 반복됩니다. 예를 들어 색 이름이 들어 있는 데이터 열의 값을 기반으로 하는 그룹 내부의 열은 고유한 색 이름마다 한 번씩 반복됩니다. 중첩된 그룹의 경우 열은 자식 그룹의 외부에 있으면서 부모 그룹의 내부에 있을 수 있습니다. 이 경우 행은 부모 그룹의 각 고유 값에 대해 한 번씩 반복됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-select-a-data-region-so-that-the-row-and-column-handles-appear"></a>데이터 영역을 선택하여 행 및 열 핸들을 표시하려면  
  
-   디자인 뷰에서 테이블릭스 데이터 영역의 왼쪽 위 모퉁이를 클릭하여 해당 데이터 영역의 위쪽과 옆쪽에 열 및 행 핸들을 표시합니다.  
  
     데이터 영역에 대 한 자세한 내용은 참조 하세요. [나열 &#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)합니다.  
  
### <a name="to-insert-a-column-in-a-selected-data-region"></a>선택한 데이터 영역에 열을 삽입하려면  
  
-   열을 삽입할 위치의 열 핸들을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 클릭한 다음 **왼쪽** 또는 **오른쪽**을 클릭합니다.  
  
     -- 또는 --  
  
-   데이터 영역에서 열을 삽입할 위치의 셀을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 클릭한 다음 **왼쪽** 또는 **오른쪽**을 클릭합니다.  
  
### <a name="to-delete-a-column-from-a-selected-data-region"></a>선택한 데이터 영역에서 열을 삭제하려면  
  
-   삭제할 열을 하나 이상 선택하고 그중 하나의 핸들을 마우스 오른쪽 단추로 클릭한 다음 **열 삭제**를 클릭합니다.  
  
     -- 또는 --  
  
-   데이터 영역에서 열을 삭제할 위치의 셀을 마우스 오른쪽 단추로 클릭한 다음 **열 삭제**를 클릭합니다.  
  
### <a name="to-insert-a-column-in-a-group-in-a-selected-data-region"></a>선택한 데이터 영역의 그룹에 열을 삽입하려면  
  
-   테이블릭스 데이터 영역의 열 그룹 영역에서 열을 삽입할 위치의 열 그룹 셀을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 클릭한 다음 **왼쪽 - 외부 그룹**, **왼쪽 - 내부 그룹**, **오른쪽 - 내부 그룹**또는 **오른쪽 - 외부 그룹**을 클릭합니다.  
  
     클릭한 열 그룹 셀이 나타내는 그룹의 내부나 외부에 열이 추가됩니다.  
  
### <a name="to-delete-a-column-from-a-group-in-a-selected-data-region"></a>선택한 데이터 영역의 그룹에서 열을 삭제하려면  
  
-   테이블릭스 데이터 영역의 열 그룹 영역에서 열을 삭제할 위치의 열 그룹 셀을 마우스 오른쪽 단추로 클릭한 다음 **열 삭제**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)   
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [테이블&#40;보고서 작성기 및 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [행렬&#40;보고서 작성기 및 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
