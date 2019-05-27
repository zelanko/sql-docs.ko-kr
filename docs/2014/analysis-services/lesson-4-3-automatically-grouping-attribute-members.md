---
title: 자동으로 특성 멤버 그룹화 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9fb2cda3-a122-4a4c-82e0-3454865eef04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c521a3faf0c11cfab7bab337226de647e27cd060
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078653"
---
# <a name="automatically-grouping-attribute-members"></a>자동으로 특성 멤버 그룹화
  큐브를 찾아볼 때 일반적으로 한 특성 계층의 멤버 차원은 다른 특성 계층의 멤버별로 구분합니다. 예를 들어 고객 판매를 도시별, 구매 제품별 또는 성별로 그룹화할 수 있습니다. 그러나 특정 특성 유형의 경우에는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 특성 계층 내의 멤버 배포에 따라 자동으로 특성 멤버를 그룹화하도록 하는 것이 유용합니다. 예를 들어 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 고객의 연간 소득 값 그룹을 만들도록 할 수 있습니다. 이 작업을 수행하면 특성 계층을 찾아보는 사용자는 멤버 자체가 아니라 그룹의 이름과 값을 보게 됩니다. 이렇게 하면 사용자에게 표시되는 수준 수가 제한되므로 분석하는 데 보다 유용합니다.  
  
 **DiscretizationMethod** 속성은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 그룹화 생성 여부 및 수행되는 그룹화 유형을 결정합니다. 기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 그룹화를 수행하지 않습니다. 자동 그룹화를 사용하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 특성 구조에 따라 최적의 그룹화 방법을 자동으로 결정하도록 허용하거나 다음 목록에서 그룹화 알고리즘 중 하나를 선택하여 그룹화 방법을 지정할 수 있습니다.  
  
 **EqualAreas**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 총 차원 멤버 수가 그룹 전체에 동일하게 분포되도록 그룹 범위를 만듭니다.  
  
 **Clusters**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 가우스 분포와 함께 K-Means 클러스터링 메서드를 사용하여 입력 값에 단일 차원 클러스터링을 수행하는 방식으로 그룹을 만듭니다. 이 옵션은 숫자 열에만 유효합니다.  
  
 그룹화 방법을 지정한 후에 **DiscretizationBucketCount** 속성을 사용하여 그룹 수를 지정해야 합니다. 자세한 내용은 [특성 멤버 그룹화&#40;불연속화&#41;](multidimensional-models/attribute-properties-group-attribute-members.md)를 참조하세요.  
  
 이 항목의 태스크에서는 **Customer** 차원의 연간 소득 값, **Employees** 차원의 직원 병가 시간 및 **Employees** 차원의 직원 휴가 시간에 대해 서로 다른 유형의 그룹화를 사용하도록 설정한 다음 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브를 처리하고 검색하여 멤버 그룹의 결과를 표시하고, 마지막으로 멤버 그룹 속성을 수정하여 그룹화 유형의 변경 결과를 표시하는 방법에 대해 설명합니다.  
  
## <a name="grouping-attribute-hierarchy-members-in-the-customer-dimension"></a>Customer 차원의 특성 계층 멤버 그룹화  
  
1.  솔루션 탐색기의 **차원** 폴더에서 **Customer** 를 두 번 클릭하여 Customer 차원에 대한 차원 디자이너를 엽니다.  
  
2.  **데이터 원본 뷰** 창에서 **Customer** 테이블을 마우스 오른쪽 단추로 클릭한 다음 **데이터 탐색**을 클릭합니다.  
  
     **YearlyIncome** 열의 값 범위가 표시됩니다. 멤버 그룹화를 사용하도록 설정하지 않으면 이러한 값은 **Yearly Income** 특성 계층의 멤버가 됩니다.  
  
3.  **Customer 테이블 탐색** 탭을 닫습니다.  
  
4.  **특성** 창에서 **Yearly Income**을 선택합니다.  
  
5.  속성 창에서 값을 변경 합니다 **DiscretizationMethod** 속성을 **자동** 값을 변경 하 고는 **DiscretizationBucketCount** 속성 `5`입니다.  
  
     다음 그림에서는 **Yearly Income**의 수정된 속성을 보여 줍니다.  
  
     ![연간 소득에 대 한 속성을 수정한](../../2014/tutorials/media/l4-discretizationmethod-1.gif "Yearly Income에 대 한 속성을 수정 합니다.")  
  
## <a name="grouping-attribute-hierarchy-members-in-the-employee-dimension"></a>Employee 차원의 특성 계층 멤버 그룹화  
  
1.  Employee 차원에 대한 차원 디자이너로 전환합니다.  
  
2.  **데이터 원본 뷰** 창에서 **Employee** 테이블을 마우스 오른쪽 단추로 클릭한 다음 **데이터 탐색**을 클릭합니다.  
  
     **SickLeaveHours** 열 및 **VacationHours** 열의 값을 확인합니다.  
  
3.  **Employee 테이블 탐색** 탭을 닫습니다.  
  
4.  **특성** 창에서 **Sick Leave Hours**를 선택합니다.  
  
5.  속성 창에서 값을 변경 합니다 **DiscretizationMethod** 속성을 **클러스터** 값을 변경 하 고는 **DiscretizationBucketCount** 속성 `5`.  
  
6.  **특성** 창에서 **Vacation Hours**를 선택합니다.  
  
7.  속성 창에서 값을 변경 합니다 **DiscretizationMethod** 속성을 **Equal Areas** 값을 변경 하 고는 **DiscretizationBucketCount** 속성 `5`입니다.  
  
## <a name="browsing-the-modified-attribute-hierarchies"></a>수정된 특성 계층 찾아보기  
  
1.  **의** 빌드 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너로 전환한 후 **브라우저** 탭에서 **다시 연결** 을 클릭합니다.  
  
3.  Excel 아이콘을 클릭한 다음 **사용**을 클릭합니다.  
  
4.  **Internet Sales-Sales Amount** 측정값을 피벗 테이블 필드 목록의 값 영역으로 끌어옵니다.  
  
5.  필드 목록에서 **Product** 차원을 확장한 다음 **Product Model Lines** 사용자 계층을 필드 목록의 **행 레이블** 영역으로 끌어옵니다.  
  
6.  필드 목록에서 **Customer** 차원을 확장하고 **Demographic** 표시 폴더를 확장한 다음 **Yearly Income** 특성 계층을 **열 레이블** 영역으로 끌어옵니다.  
  
     **Yearly Income** 특성 계층 멤버는 이제 연간 소득을 알 수 없는 고객에 대한 판매 버킷을 포함하여 6개의 버킷으로 그룹화됩니다. 표시되지 않는 버킷도 있습니다.  
  
7.  열 영역에서 **Yearly Income** 특성 계층을 제거하고 **값** 영역에서 **Internet Sales-Sales Amount** 측정값을 제거합니다.  
  
8.  데이터 영역에 **Reseller Sales-Sales Amount** 측정값을 추가합니다.  
  
9. 필드 목록에서 **Employee** 차원과 **Organization**을 차례로 확장한 후 **Sick Leave Hours** 를 **열 레이블**로 끌어옵니다.  
  
     모든 판매는 두 그룹 중 하나에 속하는 직원에 의해 이루어진 것입니다. 병가로 32-42시간을 사용한 직원이 병가로 20-31시간을 사용한 직원보다 훨씬 더 많은 판매량을 달성했습니다.  
  
     다음 이미지에서는 직원 병가 시간별로 차원이 구분된 판매량을 보여 줍니다.  
  
     ![판매 직원 병가 별로 차원이 구분 시간 둡니다](../../2014/tutorials/media/l4-discretizationmethod-2.gif "판매 직원 병가 별로 차원이 구분 유지 시간")  
  
10. **Sick Leave Hours** 특성 계층을 **데이터** 창의 열 영역에서 제거합니다.  
  
11. **Vacation Hours** 를 **데이터** 창의 열 영역에 추가합니다.  
  
     같은 영역 그룹화 방법이 사용된 두 그룹이 나타납니다. 다른 3개의 그룹은 데이터 값이 없으므로 표시되지 않습니다.  
  
## <a name="modifying-grouping-properties-and-reviewing-the-effect-of-the-changes"></a>그룹화 속성 수정 및 변경 결과 검토  
  
1.  **Employee** 차원에 대한 차원 디자이너로 전환한 다음 **특성** 창에서 **Vacation Hours** 를 선택합니다.  
  
2.  속성 창에서 **DiscretizationBucketCount** 속성 값을 **10**으로 변경합니다.  
  
3.  **의** 빌드 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
4.  배포가 성공적으로 완료되면 다시 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너로 전환합니다.  
  
5.  **브라우저** 탭에서 **다시 연결** 을 클릭하고 Excel 아이콘을 클릭한 다음 그룹화 방법의 변경 결과를 볼 수 있도록 피벗 테이블을 다시 만듭니다.  
  
    1.  Reseller Sales-Sales Amount를 값으로 끌기  
  
    2.  Employees Organization 폴더의 Vacation Hours를 열로 끌기  
  
    3.  Product Model Lines를 행으로 끌기  
  
     이제 제품에 대한 판매량 값이 있는 **Vacation Hours** 특성 멤버에는 3개의 그룹이 있습니다. 다른 7개의 그룹에는 판매량 데이터가 없는 멤버가 포함됩니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [특성 계층 숨기기 및 비활성화](../analysis-services/lesson-4-4-hiding-and-disabling-attribute-hierarchies.md)  
  
## <a name="see-also"></a>관련 항목  
 [특성 멤버 그룹화&#40;불연속화&#41;](multidimensional-models/attribute-properties-group-attribute-members.md)  
  
  
