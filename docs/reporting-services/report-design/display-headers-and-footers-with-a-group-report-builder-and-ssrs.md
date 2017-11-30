---
title: "그룹과 함께 머리글 및 바닥글 표시(보고서 작성기 및 SSRS) | Microsoft Docs"
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
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 5c1004a59c0cda51fb5cf9230b81a18945765005
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="display-headers-and-footers-with-a-group-report-builder-and-ssrs"></a>그룹과 함께 머리글 및 바닥글 표시(보고서 작성기 및 SSRS)
  그룹 머리글 또는 바닥글 같은 정적 행을 테이블릭스 데이터 영역의 그룹과 연결된 동적 행과 함께 렌더링할지 여부를 제어할 수 있습니다.  
  
 모든 열 머리글 또는 행 머리글을 여러 페이지에서 반복하려면 테이블릭스 데이터 영역에 대해 속성을 설정할 수 있습니다. 자세한 내용은 [여러 페이지에 행 및 열 머리글 표시(보고서 작성기 및 SSRS)](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)를 참조하세요.  
  
 중첩된 그룹에 연결된 동적 행 및 열 또는 레이블이나 부분합과 연결된 정적 행 및 열의 렌더링 동작을 제어하려면 테이블릭스 멤버에 대해 속성을 설정해야 합니다. 테이블릭스 멤버는 정적이거나 동적인 행 또는 열을 나타냅니다. 정적 멤버는 한 번씩 반복되는 멤버로, 총합계 행을 예로 들 수 있습니다. 동적 멤버는 그룹 인스턴스당 한 번씩 반복됩니다. 예를 들어 그룹 식 [Territory]가 있는 그룹과 연결된 행은 해당 지역의 각 고유 값에 대해 한 번씩 반복됩니다. 테이블릭스 멤버에 대한 자세한 내용은 [테이블릭스 데이터 영역 셀, 행 및 열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)을 참조하세요.  
  
 그룹화 창에서 테이블릭스 멤버를 선택하고 속성 창에서 **KeepWithGroup**, **KeepTogether**및 **RepeatOnNewPage** 속성을 설정할 수 있습니다. 그룹 머리글 및 바닥글이 그룹과 같은 페이지에 표시되도록 하려면 **KeepWithGroup** 을 사용합니다. 정적 멤버가 그룹의 행이나 열과 함께 표시되도록 하려면 **KeepTogether** 를 사용합니다. **KeepWithGroup** 값으로 지정된 행 그룹 멤버의 전체 인스턴스를 적어도 하나 이상 표시하는 모든 페이지에서 그룹 머리글 또는 바닥글을 반복하려면 **RepeatOnNewPage** 를 사용합니다. 열 그룹 멤버에 대해서는**RepeatOnNewPage** 가 지원되지 않습니다.  
  
> [!NOTE]  
>  **KeepWithGroup**, **KeepTogether** 및 **RepeatOnNewPage**는 그룹화 창의 **고급 모드**를 사용하여 설정할 수 있는 그룹 멤버 속성입니다. 자세한 내용은 [그룹화 창&#40;보고서 작성기#41;](../../reporting-services/report-design/grouping-pane-report-builder.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-a-static-row-with-a-set-of-dynamic-rows-associated-with-a-row-group"></a>정적 행을 행 그룹과 연결된 동적 행 집합과 함께 표시하려면  
  
1.  디자인 화면에서 테이블릭스 데이터 영역의 아무 곳이나 클릭하여 선택합니다. 그룹화 창에 데이터 영역에 대한 행 및 열 그룹이 표시됩니다.  
  
2.  그룹화 창의 오른쪽에서 아래쪽 화살표를 클릭한 다음 **고급 모드**를 클릭합니다. 행 그룹 창에 행 그룹 계층 구조의 계층적 정적 및 동적 멤버가 표시됩니다.  
  
3.  그룹 행과 함께 유지할 행 머리글 또는 바닥글에 해당하는 정적 멤버를 클릭합니다. 속성 창에 **테이블릭스 멤버** 속성이 표시됩니다.  
  
4.  속성 창에서 **KeepWithGroup**을 클릭하고 드롭다운 목록에서 다음 값 중 하나를 선택합니다.  
  
    -   **없음** 이 멤버를 선택된 행 그룹의 멤버와 함께 유지하도록 설정하지 않으려면 이 옵션을 선택합니다.  
  
    -   **이전** 이 멤버를 이전 그룹의 멤버와 함께 유지하려면 이 옵션을 선택합니다. 이 옵션은 그룹 바닥글 행에 사용할 수 있습니다.  
  
    -   **이후** 이 멤버를 다음 그룹의 멤버와 함께 유지하려면 이 옵션을 선택합니다. 이 옵션은 그룹 머리글 행에 사용할 수 있습니다.  
  
5.  (옵션) 보고서를 미리 봅니다. 가능한 경우, 보고서는 이 멤버를 지정된 행 그룹 멤버와 함께 렌더링합니다.  
  
### <a name="to-keep-a-static-column-with-a-set-of-dynamic-columns-associated-with-a-column-group"></a>정적 열을 열 그룹과 연결된 동적 열 집합과 함께 표시하려면  
  
1.  디자인 화면에서 테이블릭스 데이터 영역의 아무 곳이나 클릭하여 선택합니다. 그룹화 창에 데이터 영역에 대한 행 및 열 그룹이 표시됩니다.  
  
2.  그룹화 창의 오른쪽에서 아래쪽 화살표를 클릭한 다음 **고급 모드**를 클릭합니다. 열 그룹 창에 열 그룹 계층 구조의 계층적 정적 및 동적 멤버가 표시됩니다.  
  
3.  그룹 열과 함께 유지할 정적 열에 해당하는 정적 멤버를 클릭합니다. 속성 창에 **테이블릭스 멤버** 속성이 표시됩니다.  
  
4.  속성 창에서 **KeepWithGroup**을 클릭하고 드롭다운 목록에서 다음 값 중 하나를 선택합니다.  
  
    -   **없음** 이 멤버를 선택된 열 그룹의 멤버와 함께 유지하도록 기본 설정하지 않으려면 이 옵션을 선택합니다.  
  
    -   **이전** 이 멤버를 이전 그룹의 멤버와 함께 유지하려면 이 옵션을 선택합니다. 이 옵션은 지정한 열 그룹 멤버 이전에 표시되는 열 레이블에 사용할 수 있습니다.  
  
    -   **이후** 이 멤버를 다음 그룹의 멤버와 함께 유지하려면 이 옵션을 선택합니다. 이 옵션은 지정한 열 그룹 멤버 이후에 표시되는 열 합계에 사용할 수 있습니다.  
  
5.  (옵션) 보고서를 미리 봅니다. 가능한 경우, 보고서는 이 멤버를 지정된 열 그룹 멤버와 함께 렌더링합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블릭스 데이터 영역 셀, 행 및 열(보고서 작성기 및 SSRS)](tablix-data-region-report-builder-and-ssrs.md)   
 
  
  
