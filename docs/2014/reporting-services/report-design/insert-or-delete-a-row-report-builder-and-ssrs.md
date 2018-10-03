---
title: 행 삽입 또는 삭제(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b8ee7c9665186648217f522ce1642cc791274ad0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48053573"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>행 삽입 또는 삭제(보고서 작성기 및 SSRS)
  테이블릭스 데이터 영역의 행을 추가하거나 삭제할 수 있습니다. 테이블릭스 데이터 영역은 테이블, 행렬 또는 목록일 수 있습니다. 차트 및 계기 데이터 영역에는 다음 절차가 적용되지 않습니다.  
  
 테이블릭스 데이터 영역에서는 그룹과 연결되어 있는 행(그룹 내부의 행)이나 연결되지 않은 행(그룹 외부의 행)을 추가할 수 있습니다. 그룹 내부의 행은 고유 그룹 값마다 한 번씩 반복됩니다. 예를 들어 색 이름이 들어 있는 데이터 열의 값을 기반으로 하는 그룹 내부의 행은 고유한 색 이름마다 한 번씩 반복됩니다. 중첩된 그룹의 경우 행은 자식 그룹의 외부에 있으면서 부모 그룹의 내부에 있을 수 있습니다. 이 경우 행은 부모 그룹의 각 고유 값에 대해 한 번씩 반복됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>데이터 영역을 선택하여 행 및 열 핸들을 표시하려면  
  
-   디자인 뷰에서 테이블릭스 데이터 영역의 왼쪽 위 모퉁이를 클릭하여 해당 데이터 영역의 위쪽과 옆쪽에 열 및 행 핸들을 표시합니다.  
  
     데이터 영역에 대 한 자세한 내용은 참조 하세요. [나열 &#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)합니다.  
  
### <a name="to-insert-a-row-in-a-selected-data-region"></a>선택한 데이터 영역에 행을 삽입하려면  
  
-   행을 삽입할 위치의 행 핸들을 마우스 오른쪽 단추로 클릭하고 **행 삽입**을 클릭한 다음 **위** 또는 **아래**를 클릭합니다.  
  
     \- 또는-  
  
-   데이터 영역에서 행을 삽입할 위치의 셀을 마우스 오른쪽 단추로 클릭하고 **행 삽입**을 클릭한 다음 **위** 또는 **아래**를 클릭합니다.  
  
### <a name="to-delete-a-row-from-a-selected-data-region"></a>선택한 데이터 영역에서 행을 삭제하려면  
  
-   삭제할 행을 하나 이상 선택하고 그중 하나의 핸들을 마우스 오른쪽 단추로 클릭한 다음 **행 삭제**를 클릭합니다.  
  
     \- 또는-  
  
-   데이터 영역에서 행을 삭제할 위치의 셀을 마우스 오른쪽 단추로 클릭한 다음 **행 삭제**를 클릭합니다.  
  
### <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>선택한 데이터 영역의 그룹에 행을 삽입하려면  
  
-   테이블릭스 데이터 영역의 행 그룹 영역에서 행을 삽입할 위치의 행 그룹 셀을 마우스 오른쪽 단추로 클릭하고 **행 삽입**을 클릭한 다음 **위 - 외부 그룹**, **위 - 내부 그룹**, **아래 - 내부 그룹**또는 **아래 - 외부 그룹**을 클릭합니다.  
  
     클릭한 행 그룹 셀이 나타내는 그룹의 내부나 외부에 행이 추가됩니다.  
  
### <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>선택한 데이터 영역의 그룹에서 행을 삭제하려면  
  
-   테이블릭스 데이터 영역의 행 그룹 영역에서 행을 삭제할 위치의 행 그룹 셀을 마우스 오른쪽 단추로 클릭한 다음 **행 삭제**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [그룹 이해 &#40;보고서 작성기 및 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)   
 [테이블&#40;보고서 작성기 및 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [행렬&#40;보고서 작성기 및 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
