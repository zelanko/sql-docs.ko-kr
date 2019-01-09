---
title: 측정값 그룹의 차원 세분성 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 4f079485-9eb4-405c-9a20-81258298b810
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1d7b619cb711938f07ae7902dc1b9544adc5890
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512287"
---
# <a name="defining-dimension-granularity-within-a-measure-group"></a>측정값 그룹의 차원 세분성 정의
  사용자는 다양한 목적에 맞게 팩트 데이터의 차원을 세밀하게 또는 구체적으로 구분할 수 있습니다. 예를 들어 대리점이나 인터넷 판매의 판매 데이터는 매일 기록하고 판매 할당량 정보는 월별 또는 분기별로 기록할 수 있습니다. 이러한 시나리오에서 사용자는 서로 다른 팩트 테이블 각각에 대해 수준이 다양한 시간 차원을 사용할 수 있습니다. 새 데이터베이스 차원을 이러한 다른 수준을 가진 시간 차원으로 정의할 수 있지만 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 더 쉬운 방법이 있습니다.  
  
 기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 측정값 그룹에 차원을 사용하면 해당 차원의 데이터 수준은 차원의 키 특성을 기반으로 합니다. 예를 들어 시간 차원이 측정값 그룹 내에 포함되어 있고 시간 차원의 기본 수준이 매일이면 측정값 그룹에서 해당 차원의 기본 수준은 매일이 됩니다. 이 자습서의 **Internet Sales** 및 **Reseller Sales** 측정값 그룹과 같은 많은 경우에 이 수준이 적절하게 사용됩니다. 그러나 차원이 Sales Quotas 또는 Budget 측정값 그룹과 같은 다른 종류의 측정값 그룹에 포함되어 있을 때는 일반적으로 월별 또는 분기별 수준이 보다 적절합니다.  
  
 큐브 차원에 기본 수준 이외의 수준을 지정하려면 큐브 디자이너의 **차원 용도** 탭에서 특정 측정값 그룹에 사용된 대로 큐브 차원 세분성 특성을 수정합니다. 특정 측정값 그룹 내 차원의 수준을 해당 차원의 키 특성이 아닌 특성으로 변경하면 측정값 그룹의 모든 다른 특성이 직접 또는 간접적으로 새 세분성 특성에 관련되도록 해야 합니다. 다른 모든 특성과 측정값 그룹의 세분성 특성으로 지정된 특성 간 특성 관계를 지정하여 이 작업을 수행합니다. 이 경우에는 특성 관계를 이동하는 대신에 추가 특성 관계를 정의합니다. 세분성 특성으로 지정된 특성이 차원의 나머지 특성을 위해 측정값 그룹에서 사실상 키 특성이 됩니다. 특성 관계를 적절하게 지정하지 않으면 이 항목의 태스크에서 설명된 대로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 값을 제대로 집계할 수 없습니다.  
  
 자세한 내용은 [차원 관계](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md), [일반 관계 및 일반 관계 속성 정의](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)를 참조하세요.  
  
 이 항목의 태스크에서는 Sales Quotas 측정값 그룹을 추가하고 이 측정값 그룹의 Date 차원 세분성이 월별이 되도록 정의한 다음 월 특성과 다른 차원 특성 간 특성 관계를 정의하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 값을 제대로 집계하도록 하는 방법에 대해 설명합니다.  
  
## <a name="adding-tables-and-defining-the-sales-quotas-measure-group"></a>테이블 추가 및 Sales Quotas 측정값 그룹 정의  
  
1.  **Adventure Works DW 2012** 데이터 원본 뷰로 전환합니다.  
  
2.  아무 곳 이나 마우스 오른쪽 단추로 클릭 합니다 **다이어그램 구성 도우미** 창 클릭 **새 다이어그램**에 다음 다이어그램의 이름을 `Sales Quotas`입니다.  
  
3.  끌어서 합니다 **직원**, **Sales Territory**, 및 `Date` 에서 테이블을 **테이블** 창을 **다이어그램** 창.  
  
4.  **다이어그램** 창을 마우스 오른쪽 단추로 클릭하고 **테이블 추가/제거** 를 선택하여 **FactSalesQuota** 테이블을 **다이어그램**창에 추가합니다.  
  
     **SalesTerritory** 테이블은 **Employee** 테이블을 통해 **FactSalesQuota** 테이블에 연결되어 있습니다.  
  
5.  **FactSalesQuota** 테이블의 열을 검토한 다음 이 테이블의 데이터를 탐색합니다.  
  
     이 테이블의 데이터 수준은 FactSalesQuota 테이블의 최하위 수준인 분기입니다.  
  
6.  데이터 원본 뷰 디자이너에서 변경 합니다 **FriendlyName** 의 속성을 **FactSalesQuota** 테이블 `SalesQuotas`합니다.  
  
7.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브로 전환한 다음 **큐브 구조** 탭을 클릭합니다.  
  
8.  아무 곳 이나 마우스 오른쪽 단추로 클릭 합니다 **측정값** 창 클릭 **새 측정값 그룹**, 클릭 `SalesQuotas` 에 **새 측정값 그룹** 대화 상자를 선택한 다음 클릭**확인**합니다.  
  
     `Sales Quotas` 측정값 그룹에 표시 합니다 **측정값** 창입니다. 에 **차원** 창은 새 `Date` 큐브 차원도 정의 되어 기반는 `Date` 데이터베이스 차원입니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 Sales Quotas 측정값 그룹의 기반이 되는 **FactSalesQuota** 팩트 테이블의 **DateKey** 열과 관련된 기존 시간 관련 큐브 차원을 인식하지 못하므로 새 시간 관련 큐브 차원이 정의됩니다. 이 항목의 다른 태스크에서 이 큐브 차원을 변경합니다.  
  
9. 확장 된 `Sales Quotas` 측정값 그룹입니다.  
  
10. **측정값** 창에서 **Sales Amount Quota**를 선택한 다음 속성 창에서 **FormatString** 속성 값을 **Currency** 로 설정합니다.  
  
11. 선택 합니다 **Sales Quotas Count** 측정값을 선택한 다음 입력 `#,#` 에 대 한 값으로는 **FormatString** 속성 창에서 속성입니다.  
  
12. 삭제 합니다 **Calendar Quarter** 에서 측정 된 `Sales Quotas` 측정값 그룹입니다.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 Calendar Quarter 측정값의 기반이 되는 열을 측정값이 포함된 열로 감지합니다. 그러나 이 열과 CalendarYear 열은 이 항목의 뒷부분에서 Sales Quotas 측정값 그룹을 Date 차원에 연결하는 데 사용할 값을 포함합니다.  
  
13. 에 **측정값** 창 마우스 오른쪽 단추로 클릭 합니다 `Sales Quotas` 측정값 그룹을 마우스 클릭 **새 측정값**합니다.  
  
     **합계** 사용 유형을 사용하는 측정값에 사용 가능한 원본 열이 포함되어 있는 **새 측정값**대화 상자가 열립니다.  
  
14. 에 **새 측정값** 대화 상자에서 **고유 카운트** 에 **사용** 나열 되었는지 확인 합니다 `SalesQuotas` 에서 선택한를 **원본테이블** 목록에서 **EmployeeKey** 에 **원본 열** 목록을 연 다음 클릭 **확인**합니다.  
  
     **Sales Quotas 1**이라는 새 측정값 그룹에 측정값이 생성됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 고유 카운트 측정값이 자체 측정값 그룹에 생성되므로 처리 성능을 극대화합니다.  
  
15. 값을 변경 합니다 **이름** 속성에 대 한를 **Employee Key Distinct Count** 측정값을 `Sales Person Count`, 입력 `#,#` 값으로는 **FormatString** 속성입니다.  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>Sales Quota 측정값 그룹에서 날짜별로 측정값 찾아보기  
  
1.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너에서 **브라우저** 탭을 클릭한 다음 **다시 연결** 단추를 클릭합니다.  
  
3.  Excel 바로 가기를 클릭한 다음 **사용**을 클릭합니다.  
  
4.  피벗 테이블 필드 목록에서를 확장 합니다 `Sales Quotas` 측정값 그룹을 끌어서 놓습니다 합니다 **Sales Amount Quota** 측정값을 값 영역입니다.  
  
5.  **Sales Territory** 차원을 확장한 다음 **Sales Territories** 사용자 정의 계층을 행 레이블로 끌어옵니다.  
  
     다음 이미지에서와 같이 Sales Territory 큐브 차원은 Fact Sales Quota 테이블에 직접 또는 간접적으로 관련되어 있지 않습니다.  
  
     ![Sales Territory 큐브 차원은](../../2014/tutorials/media/l5-granularity-2.gif "Sales Territory 큐브 차원")  
  
     이 항목의 다음과 같은 일련의 단계에서는 이 차원과 이 팩트 테이블 간 참조 차원 관계를 정의합니다.  
  
6.  **Sales Territories** 사용자 계층을 행 레이블 영역에서 열 레이블 영역으로 이동합니다.  
  
7.  피벗 테이블 필드 목록에서 **Sales Territories** 사용자 정의 계층을 선택한 다음 오른쪽의 아래쪽 화살표를 클릭합니다.  
  
     ![필드 목록의 sales Territories 계층](../../2014/tutorials/media/l5-granularity-1a.png "필드 목록의 Sales Territories 계층")  
  
8.  필터에서 모두 선택 확인란을 클릭하여 모든 선택 항목의 선택을 취소한 다음 **North America**만 선택합니다.  
  
     ![North America 선택을 위한 필터 창](../../2014/tutorials/media/l5-granularity-1b.png "North America 선택을 위한 필터 창")  
  
9. 피벗 테이블 필드 목록에서 확장 `Date`합니다.  
  
10. **Date.Fiscal Date** 사용자 계층을 행 레이블로 끌어옵니다.  
  
11. 피벗 테이블에서 행 레이블 옆에 있는 아래쪽 화살표를 클릭합니다. **FY 2008**을 제외한 모든 연도를 선택 취소합니다.  
  
     멤버만 합니다 **2007 년 7 월** 의 멤버는 **월** 수준이 나타납니다 대신는 **2007 년 7 월**, **2007 년 8 월**, 및 **2007 년 9 월** 멤버인 **월** 수준 및만 하는 **2007 년 7 월 1 일** 의 멤버는 `Date` 모든 31 일이 아닌 수준에서 표시 됩니다. 이 동작은 팩트 테이블의 데이터 수준이 분기 수준이 고은 때문에 발생 합니다 `Date` 차원 일별 수준입니다. 이 항목의 다음 태스크에서는 이 동작을 변경하는 방법에 대해 설명합니다.  
  
     월 및 일 수준의 **Sales Amount Quota** 값도 분기 수준의 값과 같은 $13,733,000.00가 됩니다. Sales Quotas 측정값 그룹의 데이터 최하위 수준이 분기 수준이기 때문입니다. 6단원에서는 이 동작을 변경하는 방법을 설명합니다.  
  
     다음 그림에서는 **Sales Amount Quota**의 값을 보여 줍니다.  
  
     ![값 Sales Amount 할당량](../../2014/tutorials/media/l5-granularity-3.png "값 Sales Amount 할당량")  
  
## <a name="defining-dimension-usage-properties-for-the-sales-quotas-measure-group"></a>Sales Quotas 측정값 그룹의 차원 용도 속성 정의  
  
1.  **Employee** 차원에 대한 차원 디자이너를 열고 **데이터 원본 뷰** 창에서 **SalesTerritoryKey** 를 마우스 오른쪽 단추로 클릭한 다음 **열의 새 특성**을 클릭합니다.  
  
2.  **특성** 창에서 **SalesTerritoryKey**를 선택한 후 속성 창에서 **AttributeHierarchyVisible** 속성을 **False** 로, **AttributeHierarchyOptimizedState** 속성을 **NotOptimized**로, **AttributeHierarchyOrdered** 속성을 **False**로 설정합니다.  
  
     연결 하려면이 특성이 필요 합니다 **Sales Territory** 차원을 합니다 `Sales Quotas` 및 **Sales Quotas 1** 참조 차원으로 측정값 그룹.  
  
3.  에 대 한 큐브 디자이너의를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 클릭 합니다 **차원 용도** 탭을 클릭 한 다음 내에서 차원 용도 검토 합니다 `Sales Quotas` 및 **Sales Quotas 1** 측정값 그룹.  
  
     있음을 합니다 **직원** 및 `Date` 큐브 차원에 연결 된 합니다 **Sales quotas 및 Sales Quotas 1** 측정값 그룹과 일반 관계를 통해. **Sales Territory** 큐브 차원은 이러한 측정값 그룹에 연결되어 있지 않습니다.  
  
4.  교집합에서 셀을 클릭 합니다 **Sales Territory** 차원 및 `Sales Quotas` 측정값 그룹 및 찾아보기 단추를 클릭 (**...** ). **관계 정의** 대화 상자가 열립니다.  
  
5.  **관계 유형 선택** 목록에서 **참조**를 선택합니다.  
  
6.  **중간 차원** 목록에서 **Employee**를 선택합니다.  
  
7.   **참조 차원 특성** 목록에서 **Sales Territory Region**을 선택합니다.  
  
8.  **중간 차원 특성** 목록에서 **Sales Territory Key**를 선택합니다. Sales Territory Region 특성의 키 열은 SalesTerritoryKey 열입니다.  
  
9. **구체화** 확인란이 선택되어 있는지 확인합니다.  
  
10. **확인**을 클릭합니다.  
  
11. 교집합에서 셀을 클릭 합니다 **Sales Territory** 차원 및 **Sales Quotas 1&lt;/ui&gt** 측정값 그룹 및 찾아보기 단추를 클릭 (**...** ). **관계 정의** 대화 상자가 열립니다.  
  
12. **관계 유형 선택** 목록에서 **참조**를 선택합니다.  
  
13. **중간 차원** 목록에서 **Employee**를 선택합니다.  
  
14.  **참조 차원 특성** 목록에서 **Sales Territory Region**을 선택합니다.  
  
15. **중간 차원 특성** 목록에서 **Sales Territory Key**를 선택합니다. Sales Territory Region 특성의 키 열은 SalesTerritoryKey 열입니다.  
  
16. **구체화** 확인란이 선택되어 있는지 확인합니다.  
  
17. **확인**을 클릭합니다.  
  
18. 삭제 된 `Date` 큐브 차원입니다.  
  
     4 개의 시간 관련 큐브 차원이 대신 사용할지는 **Order Date** 큐브 차원에는 `Sales Quotas` 기준이 판매 할당량 차원을 구분할 날짜로 측정값 그룹입니다. 또한 이 큐브 차원을 큐브의 주 날짜 차원으로 사용합니다.  
  
19. 에 **차원** 목록에서 이름 바꾸기는 **Order Date** 큐브 차원의 `Date`합니다.  
  
     이름 바꾸기는 **Order Date** 큐브 차원의 `Date` 사용자가 차원의 역할을이 큐브의 주 날짜 차원으로 이해 하기 쉽게 합니다.  
  
20. 찾아보기 단추를 클릭 (**...** )의 교집합에서 셀에는 `Sales Quotas` 측정값 그룹 및 `Date` 차원입니다.  
  
21. **관계 정의** 대화 상자의 **관계 유형 선택** 목록에서 **일반** 을 선택합니다.  
  
22. **세분성 특성** 목록에서 **Calendar Quarter**를 선택합니다.  
  
     세분성 특성으로 키가 아닌 특성을 선택했으므로 모든 다른 특성을 멤버 속성으로 지정하여 해당 특성이 직접 또는 간접적으로 세분성 특성에 관련되도록 해야 함을 알리는 경고가 나타납니다.  
  
23. **관계 정의** 대화 상자의 **관계** 영역에서 Date 큐브 차원의 기반이 되는 테이블의 **CalendarYear** 및 **CalendarQuarter** 차원 열을 Sales Quota 측정값 그룹의 기반이 되는 테이블의 **CalendarYear** 및 **CalendarQuarter** 열에 연결한 다음 **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  Sales Quotas 측정값 그룹의 Date 큐브 차원에 대한 세분성 특성은 Calendar Quarter로 정의되지만 Internet Sales 및 Reseller Sales 측정값 그룹의 세분성 특성에는 Date 특성이 계속 사용됩니다.  
  
24. **Sales Quotas 1** 측정값 그룹에 대해 이전 네 단계를 반복합니다.  
  
## <a name="defining-attribute-relationships-between-the-calendar-quarter-attribute-and-the-other-dimension-attributes-in-the-date-dimension"></a>Date 차원의 Calendar Quarter 특성과 다른 차원 특성 간의 특성 관계 정의  
  
1.  전환할 **차원 디자이너** 에 대 한는 `Date` 차원 및 클릭 합니다 **특성 관계** 탭 합니다.  
  
     되었지만 **역 년** 연결 된 **Calendar Quarter** 를 통해 합니다 **Calendar Semester** 회계 달력 특성 하나에 연결 된 특성 다른; 에 연결 되지 않은 합니다 **Calendar Quarter** 특성 및 따라서 됩니다에서 제대로 집계 되지는 `Sales Quotas` 측정값 그룹입니다.  
  
2.  다이어그램에서 **Calendar Quarter** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
3.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Calendar Quarter**입니다. **관련 특성** 을 **Fiscal Quarter**로 설정합니다.  
  
4.  **확인**을 클릭합니다.  
  
     경고 메시지가 나타납니다는는 `Date` 차원 데이터가 키가 아닌 특성이 세분성 특성으로 사용 될 때 집계 되지 못할 수도 있다는 하나 이상의 중복 특성 관계가 포함 되어 있습니다.  
  
5.  **Month Name** 특성과 **Fiscal Quarter** 특성 간의 특성 관계를 삭제합니다.  
  
6.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>Sales Quota 측정값 그룹에서 날짜별로 측정값 찾아보기  
  
1.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 **Tutorial 큐브에 대한 큐브 디자이너에서** 브라우저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 탭을 클릭한 다음 **다시 연결**을 클릭합니다.  
  
3.  Excel 바로 가기를 클릭한 다음 **사용**을 클릭합니다.  
  
4.  **Sales Amount Quota** 측정값을 값 영역으로 끌어옵니다.  
  
5.  **Sales Territories** 사용자 계층을 열 레이블로 끌어온 다음 **North America**를 필터링합니다.  
  
6.  **Date.FiscalDate** 사용자 계층을 행 레이블로 끌어간 다음 피벗 테이블에서 **행 레이블** 옆의 아래쪽 화살표를 클릭하고 **FY 2008**을 제외한 모든 확인란의 선택을 취소하여 2008 회계 연도만 표시합니다.  
  
7.  확인을 클릭합니다.  
  
8.  **FY 2008**, **H1 FY 2008**, **Q1 FY 2008**을 차례로 확장합니다.  
  
     다음 그림에서는 Sales Quota 측정값 그룹의 차원이 올바르게 구분되어 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 피벗 테이블을 보여 줍니다.  
  
     회계 분기 수준의 각 멤버 값이 분기 수준 값과 동일합니다. **Q1 FY 2008** 을 예로 사용하면 **Q1 FY 2008** 의 할당량인 $9,180,000.00가 각 해당 멤버의 값이기도 합니다. 이 동작은 팩트 테이블의 데이터 수준이 분기이고 Date 차원의 수준도 분기이기 때문에 발생합니다. 6단원에서는 분기별 판매량을 각 월에 비례하게 할당하는 방법을 설명합니다.  
  
     ![Sales Quota 측정값 그룹 차원이 올바르게 구분 되어](../../2014/tutorials/media/l5-granularity-7.gif "Sales Quota 측정값 그룹의 차원이 올바르게 구분 되어")  
  
## <a name="next-lesson"></a>다음 단원  
 [6 단원: 계산 정의](lesson-6-defining-calculations.md)  
  
## <a name="see-also"></a>관련 항목  
 [차원 관계](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [일반 관계 및 일반 관계 속성 정의](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)   
 [데이터 원본 뷰 디자이너에서의 다이어그램 작업&#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
