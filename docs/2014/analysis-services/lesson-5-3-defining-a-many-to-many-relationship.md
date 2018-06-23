---
title: 다 대 다 관계 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7bebb174-148c-4cbb-a285-2f6d536a16d5
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 89ec38cf3bd3b197c6a58a5d51758ee6c6f29269
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182667"
---
# <a name="defining-a-many-to-many-relationship"></a>다 대 다 관계 정의
  차원을 정의할 경우 일반적으로 각 팩트는 하나의 차원 멤버에만 조인되지만 단일 차원 멤버는 여러 팩트와 연결될 수 있습니다. 예를 들어 각 고객은 여러 개의 주문을 가질 수 있지만 각 주문은 단일 컴퓨터에 속합니다. 관계형 데이터베이스 용어에서 이 관계를 *일 대 다 관계*라고 합니다. 그러나 단일 팩트가 여러 차원 멤버에 조인될 수도 있습니다. 관계형 데이터베이스 용어에서 이 관계를 *다 대 다 관계*라고 합니다. 예를 들어 고객이 구매하는 데는 여러 이유가 있고 구매 이유는 여러 구매와 연결될 수 있습니다. 조인 테이블을 사용하여 각 구매와 관련된 판매 이유를 정의합니다. 그러므로 이러한 관계에서 생성된 Sales Reason 차원에는 단일 판매 트랜잭션과 관련된 여러 멤버가 포함됩니다. 다 대 다 차원은 차원 모델을 표준 별모양 스키마 이상으로 확장하고 차원이 팩트 테이블에 직접 관련되지 않는 경우 복잡한 분석을 지원합니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 차원 테이블에 조인할 중간 팩트 테이블을 지정하여 차원과 측정값 그룹의 다 대 다 관계를 정의합니다. 이에 따라 중간 팩트 테이블은 팩트 테이블이 조인되는 중간 차원 테이블에 조인됩니다. 중간 팩트 테이블과 관계의 차원 테이블 및 중간 차원 모두 간의 다 대 다 관계는 주 차원 멤버와 관계에 의해 지정된 측정값 그룹의 측정값 간에 다 대 다 관계를 만듭니다. 중간 측정값 그룹을 통해 차원 및 측정값 그룹 간에 다 대 다 관계를 정의하려면 중간 측정값 그룹이 하나 이상의 차원을 원래의 측정값 그룹과 공유해야 합니다.  
  
 다 대 다 차원이 사용되면 값의 합계가 고유하게 계산됩니다. 이는 All 멤버에 대해 값이 두 번 이상 집계되지 않는다는 것을 의미합니다.  
  
> [!NOTE]  
>  다 대 다 차원 관계를 지원하려면 데이터 원본 뷰에서 관련되는 모든 테이블 간에 기본 키-외래 키 관계를 정의해야 합니다. 정의하지 않으면 큐브 디자이너의 **차원 용도** 탭에서 관계를 설정할 때 올바른 중간 측정값 그룹을 선택할 수 없습니다.  
  
 자세한 내용은 [차원 관계](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)와 [다 대 다 관계 및 다 대 다 관계 속성 정의](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)를 참조하세요.  
  
 이 항목의 태스크에서는 Sales Reasons 차원과 Sales Reasons 측정값 그룹을 정의하고 Sales Reasons 측정값 그룹을 통해 Sales Reasons 차원과 Internet Sales 측정값 그룹 간에 다 대 다 관계를 정의하는 방법에 대해 설명합니다.  
  
## <a name="adding-required-tables-to-the-data-source-view"></a>데이터 원본 뷰에 필수 테이블 추가  
  
1.  **Adventure Works DW 2012** 데이터 원본 뷰에 대한 데이터 원본 뷰 디자이너를 엽니다.  
  
2.  아무 곳 이나 마우스 오른쪽 단추로 클릭는 **다이어그램 구성 도우미** 창에서 클릭 **새 다이어그램**를 지정 하 고 `Internet Sales Order Reasons` 이 새 다이어그램의 이름으로 합니다.  
  
3.  **테이블** 창에서 **InternetSales** 테이블을 **다이어그램** 창으로 끌어옵니다.  
  
4.  **다이어그램** 창을 마우스 오른쪽 단추로 클릭한 다음 **테이블 추가/제거**를 클릭합니다.  
  
5.  **테이블 추가/제거** 대화 상자에서 **DimSalesReason** 테이블과 **FactInternetSalesReason** 테이블을 **포함된 개체** 목록에 추가한 다음 **확인**을 클릭합니다.  
  
     관련된 테이블 간 기본 키-외래 키 관계가 기본 관계형 데이터베이스에 정의되어 있으므로 해당 관계가 자동으로 설정됩니다. 이러한 관계가 기본 관계형 데이터베이스에 정의되어 있지 않으면 해당 관계를 데이터 원본 뷰에서 정의해야 합니다.  
  
6.  **서식** 메뉴에서 **자동 레이아웃**을 가리킨 다음 **다이어그램**을 클릭합니다.  
  
7.  속성 창에서 변경는 **FriendlyName** 속성의는 **DimSalesReason** 테이블 `SalesReason`, 한 다음 변경는 **FriendlyName** 의 속성은 **FactInternetSalesReason** 테이블 `InternetSalesReason`합니다.  
  
8.  **테이블** 창에서 **InternetSalesReason(dbo.FactInternetSalesReason)** 을 확장하고 **SalesOrderNumber**를 클릭한 다음 속성 창에서 이 데이터 열의 **DataType** 속성을 검토합니다.  
  
     **SalesOrderNumber** 열의 데이터 형식은 문자열 데이터 형식입니다.  
  
9. 다른 열에 대 한 데이터 형식을 검토는 `InternetSalesReason` 테이블입니다.  
  
     이 테이블의 다른 두 개의 열에 대한 데이터 형식은 숫자 데이터 형식입니다.  
  
10. **테이블** 창에서 **InternetSalesReason(dbo.FactInternetSalesReason)** 을 마우스 오른쪽 단추로 클릭한 다음 **데이터 탐색**을 클릭합니다.  
  
     다음 이미지에서와 같이 각 주문에서 각 줄 번호의 키 값은 해당 줄 항목의 구매에 대한 판매 이유를 식별합니다.  
  
     ![키 값을 구입에 대 한 판매 이유를 식별](../../2014/tutorials/media/l5-many-to-many-1.gif "키 값을 구입에 대 한 판매 이유를 식별 합니다.")  
  
## <a name="defining-the-intermediate-measure-group"></a>중간 측정값 그룹 정의  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너로 전환한 다음 **큐브 구조** 탭을 클릭합니다.  
  
2.  **측정값** 창을 마우스 오른쪽 단추로 클릭한 다음 **새 측정값 그룹**을 클릭합니다. 자세한 내용은 [다차원 모델의 측정값 및 측정값 그룹 만들기](multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)를 참조하세요.  
  
3.  에 **새 측정값 그룹** 대화 상자에서 `InternetSalesReason` 에 **데이터 원본 뷰에서 테이블 선택** 목록으로 이동한 다음 클릭 **확인**합니다.  
  
     이제 **Internet Sales Reason** 측정값 그룹이 **측정값** 창에 나타납니다.  
  
4.  **Internet Sales Reason** 측정값 그룹을 확장합니다.  
  
     이 새 측정값 그룹에는 단일 측정값 **Internet Sales Reason Count** 만 정의되어 있습니다.  
  
5.  **Internet Sales Reason Count** 를 선택하고 속성 창에서 이 측정값의 속성을 검토합니다.  
  
     이 측정값의 **AggregateFunction** 속성은 **Sum** 이 아니라 **Count**로 정의됩니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 기본 데이터 형식이 문자열 데이터 형식이므로 **Count** 를 선택했습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 기본 팩트 테이블의 다른 두 열을 실제 측정값이 아니라 숫자 키로 검색하므로 해당 열은 측정값으로 선택되지 않습니다. 자세한 내용은 [반가산적 동작 정의](multidimensional-models/define-semiadditive-behavior.md)를 참조하세요.  
  
6.  속성 창에서 **Internet Sales Reason Count** 측정값의 **Visible** 속성을 **False**로 변경합니다.  
  
     이 측정값은 Internet Sales 측정값 그룹 다음에 정의할 Sales Reason 차원을 조인하는 데만 사용됩니다. 사용자가 이 측정값을 직접 찾아보지는 않습니다.  
  
     다음 그림에서는 **Internet Sales Reason Count** 측정값의 속성을 보여 줍니다.  
  
     ![Internet Sales Reason Count 측정값에 대 한 속성](../../2014/tutorials/media/l5-many-to-many-2.gif "Internet Sales Reason Count 측정값에 대 한 속성")  
  
## <a name="defining-the-many-to-many-dimension"></a>다 대 다 차원 정의  
  
1.  솔루션 탐색기에서 **차원**을 마우스 오른쪽 단추로 클릭한 다음 **새 차원**을 클릭합니다.  
  
2.  **차원 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **생성 방법 선택** 페이지에서 **기존 테이블 사용** 옵션이 선택되어 있는지 확인하고 **다음**을 클릭합니다.  
  
4.  **원본 정보 지정** 페이지에서 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012 데이터 원본 뷰가 선택되어 있는지 확인합니다.  
  
5.  에 **주 테이블** 목록에서 `SalesReason`합니다.  
  
6.  **키 열** 목록에 **SalesReasonKey** 가 있는지 확인합니다.  
  
7.  **이름 열** 목록에서 **SalesReasonName**을 선택합니다.  
  
8.  **다음**을 클릭합니다.  
  
9. **차원 특성 선택** 페이지에서 키 특성인 **Sales Reason Key** 특성이 자동으로 선택됩니다. 옆의 확인란을 선택 된 **Sales Reason Reason Type** 특성을 변경 하 고 이름을 `Sales Reason Type`, 클릭 하 고 **다음**합니다.  
  
10. **마법사 완료** 페이지에서 **마침** 을 클릭하여 Sales Reason 차원을 만듭니다.  
  
11. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
12. 에 **특성** 에 대 한 차원 디자이너의 창은 **Sales Reason** 차원을 선택 하 **Sales Reason Key**, 한 다음 변경는 **이름**를 속성 창에서 속성 `Sales Reason.`  
  
13. 에 **계층** 차원 디자이너의 창 만들기는 **Sales Reasons** 사용자 계층 구조를 포함 하는 `Sales Reason Type` 수준 및 **Sales Reason** 수준에서 해당 순서입니다.  
  
14. 속성 창에서 정의 `All Sales Reasons` 에 대 한 값으로는 **AllMemberName** Sales Reasons 계층의 속성입니다.  
  
15. 정의 `All Sales Reasons` 에 대 한 값으로 **AttributeAllMemberName** Sales Reason 차원의 속성입니다.  
  
16. 새로 만들어진 차원을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 큐브 차원으로 추가하려면 **큐브 디자이너**로 전환합니다. **큐브 구조** 탭에서 **차원** 창을 마우스 오른쪽 단추로 클릭하고 **큐브 차원 추가**를 선택합니다.  
  
17. **큐브 차원 추가** 대화 상자에서 **Sales Reason** 을 선택한 후 **확인**을 클릭합니다.  
  
18. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="defining-the-many-to-many-relationship"></a>다 대 다 관계 정의  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너로 전환한 다음 **차원 용도** 탭을 클릭합니다.  
  
     **Sales Reason** 차원은 **Internet Sales Reason** 측정값 그룹과 일반 관계가 정의되어 있지만 **Internet Sales** 또는 **Reseller Sales** 측정값 그룹과는 관계가 정의되어 있지 않습니다. 또한 **Internet Sales Order Details** 차원은 **Internet Sales** 측정값 그룹과 **Fact Relationship** 관계가 정의되어 있는 **Internet Sales Reason** 차원과 일반 관계가 정의되어 있습니다. 이 차원이 없거나 **Internet Sales Reason** 및 **Internet Sales** 측정값 그룹과 관계가 정의된 다른 차원이 없을 경우 다 대 다 관계를 정의할 수 없습니다.  
  
2.  **Internet Sales** 측정값 그룹과 **Sales Reason** 차원의 교집합에 있는 셀을 클릭한 다음 찾아보기 단추(**...**)를 클릭합니다.  
  
3.  **관계 정의** 대화 상자의 **관계 유형 선택** 목록에서 **다 대 다** 를 선택합니다.  
  
     Sales Reason 차원을 Internet Sales 측정값 그룹에 연결하는 중간 측정값 그룹을 정의해야 합니다.  
  
4.  **중간 측정값 그룹** 목록에서 **Internet Sales Reason**을 선택합니다.  
  
     다음 그림에서는 **관계 정의** 대화 상자의 변경 내용을 보여 줍니다.  
  
     ![정의 관계 대화 상자](../../2014/tutorials/media/l5-many-to-many-3.gif "관계 정의 대화 상자")  
  
5.  **확인**을 클릭합니다.  
  
     Sales Reason 차원과 Internet Sales 측정값 그룹 간의 관계를 나타내는 다 대 다 아이콘이 표시됩니다.  
  
## <a name="browsing-the-cube-and-the-many-to-many-dimension"></a>큐브 및 다 대 다 차원 찾아보기  
  
1.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 **Tutorial 큐브에 대한 큐브 디자이너에서** 브라우저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 탭으로 전환한 다음 **다시 연결**을 클릭합니다.  
  
3.  데이터 창의 데이터 영역에 **Internet Sales-Sales Amount** 측정값을 추가합니다.  
  
4.  **Sales Reason** 차원의 **Sales Reasons** 사용자 정의 계층을 데이터 창의 행 영역에 추가합니다.  
  
5.  메타데이터 창에서 **Customer**, **Location**, **Customer Geography**, **Members**, **All Customers**, **Australia**를 차례로 확장하고 **Queensland**를 마우스 오른쪽 단추로 클릭한 다음 **필터에 추가**를 클릭합니다.  
  
6.  확장의 각 멤버는 `Sales Reason Type` 수준 Queensland의 고객이 구매 지정 하는 각 이유와 연결 된 달러 값을 검토 하는 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 인터넷을 통해 제품입니다.  
  
     각 판매 이유와 연결된 합계가 총 판매량보다 크며 이는 일부 고객이 여러 구매 이유를 언급했기 때문입니다.  
  
     다음 그림에서는 큐브 디자이너의 **필터** 창과 **데이터** 창을 보여 줍니다.  
  
     ![큐브 디자이너의 필터 창과 데이터 창](../../2014/tutorials/media/l5-many-to-many-5.gif "큐브 디자이너의 필터 창과 데이터 창")  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [측정값 그룹의 차원 세분성 정의](../analysis-services/lesson-5-4-defining-dimension-granularity-within-a-measure-group.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 뷰 디자이너에서의 다이어그램 작업 &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [차원 관계](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [다 대 다 관계 및 다 대 다 관계 속성 정의](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)  
  
  