---
title: "(보고서 작성기 및 SSRS) 계기 패널에 표시기 및 계기 포함 | Microsoft Docs"
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
ms.assetid: 4dff9b67-b483-4c51-a822-6dbe706a6840
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eb8b6569d75891a2922b283fbde37840910213db
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs"></a>계기 패널에 표시기 및 계기 포함(보고서 작성기 및 SSRS)
  계기 패널은 하나 이상의 계기 및 표시기가 포함되는 최상위 컨테이너입니다. 표시기는 계기 패널에서 계기에 포함하거나 계기 옆에 배치할 수 있습니다.  
  
 표시기와 계기가 계기 패널에서 인접해 있으며 서로 다른 필드의 데이터를 표시하는 경우 계기와 표시기가 각각 나타내는 데이터를 명확하게 파악할 수 있도록 레이블을 추가할 수 있습니다.  
  
 식을 사용하여 계기 및 표시기 옵션을 설정할 수 있습니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-indicator-in-a-gauge"></a>계기에 표시기를 포함하려면  
  
1.  기존 보고서를 열거나 표시할 데이터가 있는 테이블 및 행렬을 포함하는 새 보고서를 만듭니다.   
  
2.  테이블이나 행렬에 열을 삽입합니다. 자세한 내용은 [열 삽입 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)를 참조하세요.  
  
3.  **삽입** 탭의 **데이터 영역** 그룹에서 **계기**를 클릭한 다음 새 열의 셀을 클릭합니다. **계기 유형 선택** 대화 상자가 나타납니다.  
  
4.  **방사형**을 클릭합니다. 그러면 첫 번째 방사형 계기가 선택됩니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  계기를 클릭합니다. **계기 데이터** 창이 열립니다.  
  
7.  **값** 영역의 **(지정하지 않음)** 목록 상자에서 계기에 표시할 값이 포함된 필드를 클릭합니다. 보고서 데이터 집합에서 사용할 필드를 끌어다 놓을 수도 있습니다.  
  
8.  계기를 마우스 오른쪽 단추로 클릭하고 **표시기 추가**를 클릭한 다음 **자식**을 클릭합니다. **표시기 스타일 선택** 대화 상자가 열립니다.  
  
9. **표시기 스타일 선택** 대화 상자의 왼쪽 창에서 원하는 표시기 유형을 클릭한 다음 표시기 집합을 클릭합니다.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
11. 표시기를 클릭합니다. **계기 데이터** 창이 열립니다.  
  
12. **값** 영역의 **(지정하지 않음)** 드롭다운 상자에서 표시기로 표시할 값이 포함된 필드를 클릭합니다. 보고서 데이터 집합에서 사용할 필드를 끌어다 놓을 수도 있습니다.  
  
     이 필드는 계기에 사용하는 필드와 같아도 되고 달라도 됩니다.  
  
13. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-show-an-indicator-and-gauge-side-by-side"></a>표시기와 계기를 나란히 표시하려면  
  
1.  기존 보고서를 열거나 표시할 데이터가 있는 테이블 및 행렬을 포함하는 새 보고서를 만듭니다.  
  
2.  테이블이나 행렬에 열을 삽입합니다. 자세한 내용은 [열 삽입 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)를 참조하세요.  
  
3.  **삽입** 탭의 **데이터 영역** 그룹에서 **계기**를 클릭한 다음 삽입한 열의 셀을 클릭합니다. **계기 유형 선택** 대화 상자가 나타납니다.  
  
4.  **방사형**을 클릭합니다. 그러면 첫 번째 방사형 계기가 선택됩니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  계기를 클릭합니다. **계기 데이터** 창이 열립니다.  
  
7.  **값** 영역의 **(지정하지 않음)** 목록 상자에서 계기에 표시할 값이 포함된 필드를 클릭합니다. 보고서 데이터 집합에서 사용할 필드를 끌어다 놓을 수도 있습니다.  
  
8.  계기를 마우스 오른쪽 단추로 클릭하고 **표시기 추가**를 클릭한 다음 **인접**을 클릭합니다. **표시기 스타일 선택** 대화 상자가 열립니다.  
  
9. **표시기 스타일 선택** 대화 상자의 왼쪽 창에서 원하는 표시기 유형을 클릭한 다음 표시기 집합을 클릭합니다.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
11. 표시기를 클릭합니다. **계기 데이터** 창이 열립니다.  
  
12. **값** 영역의 **(지정하지 않음)** 드롭다운 상자에서 표시기로 표시할 값이 포함된 필드를 클릭합니다. 보고서 데이터 집합에서 사용할 필드를 끌어다 놓을 수도 있습니다.  
  
     이 필드는 계기에 사용하는 필드와 같아도 되고 달라도 됩니다.  
  
13. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
14. 계기 패널을 마우스 오른쪽 단추로 클릭하고 **레이블 추가**를 클릭합니다. 레이블이 계기 패널에 추가됩니다. 같은 작업을 한 번 더 반복합니다.  
  
     이제 계기 패널에는 두 개의 레이블이 있습니다.  
  
15. 각 레이블을 계기 또는 표시기 근처의 위치로 끕니다.  
  
16. 계기 근처의 레이블을 마우스 오른쪽 단추로 클릭하고 **레이블 속성**을 클릭한 다음 **텍스트** 상자에 원하는 텍스트를 입력합니다.  
  
17. 표시기 옆의 레이블을 마우스 오른쪽 단추로 클릭하고 **레이블**속성을 클릭한 다음 **텍스트** 상자에 원하는 텍스트를 입력합니다.  
  
18. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [표시기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
