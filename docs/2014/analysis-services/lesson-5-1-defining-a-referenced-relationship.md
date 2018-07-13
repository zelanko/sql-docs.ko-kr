---
title: 참조 관계 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4a34ba52-e3b3-4e8a-8e55-73e0cd5a97bd
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f49d90e05c7d76129b5c2385ed1af05fc6e3731a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200383"
---
# <a name="defining-a-referenced-relationship"></a>참조 관계 정의
  이 자습서의 이전 단원에서는 정의한 각 큐브 차원은 기본 키와 외래 키의 관계를 통해 측정값 그룹의 팩트 테이블에 직접 연결된 테이블을 기반으로 하였습니다. 이 항목의 태스크에서는 **Geography** 차원을 **참조 차원** 이라고 하는 *Reseller*차원을 통해 대리점 판매에 대한 팩트 테이블에 연결하는 방법을 설명합니다. 이를 통해 사용자는 지리별로 대리점 판매 차원을 구분할 수 있습니다. 자세한 내용은 [참조 관계 및 참조 관계 속성 정의](multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)를 참조하세요.  
  
## <a name="dimensioning-reseller-sales-by-geography"></a>지리별로 Reseller Sales 차원 구분  
  
1.  솔루션 탐색기의 **큐브** 폴더에서 **Analysis Services Tutorial** 을 마우스 오른쪽 단추로 클릭한 다음 **찾아보기**를 클릭합니다.  
  
2.  데이터 창에서 모든 계층을 제거한 다음 **Reseller Sales-Sales Amount** 측정값이 데이터 창의 데이터 영역에 나타나는지 확인합니다. 이 측정값이 표시되어 있지 않으면 측정값을 데이터 창에 추가합니다.  
  
3.  메타데이터 창의 **Geography** 차원에서 **Geography** 사용자 정의 계층을 데이터 창의 **행 필드를 여기로 끌어옵니다.** 영역으로 끌어다 놓습니다.  
  
     **Reseller Sales-Sales Amount** 측정값은 **Regions** 계층의 **Country-Region** 특성 멤버별로 차원이 제대로 구분되지 않습니다. **Reseller Sales-Sales Amount** 에 대한 값이 각 **Country-Region** 특성 멤버에 대해 반복됩니다.  
  
     ![Reseller Sales-sales Amount 측정값 차원이](../../2014/tutorials/media/l5-referencedrelationship-1.gif "차원이 Reseller Sales-sales Amount 측정값")  
  
4.  **Adventure Works DW 2012** 데이터 원본 뷰에 대한 데이터 원본 뷰 디자이너를 엽니다.  
  
5.  **다이어그램 구성 도우미** 창에서 **Geography** 테이블과 **ResellerSales** 테이블 간의 관계를 확인합니다.  
  
     이러한 테이블은 직접 연결되어 있지 않습니다. 그러나 **Reseller** 테이블이나 **SalesTerritory** 테이블 중 하나를 통해 이러한 테이블은 간접 연결됩니다.  
  
6.  **Geography** 테이블과 **Reseller** 테이블의 관계를 나타내는 화살표를 두 번 클릭합니다.  
  
     **관계 편집** 대화 상자에서 **GeographyKey** 열은 **Geography** 테이블의 기본 키이며 **Reseller** 테이블의 외래 키입니다.  
  
7.  **취소**를 클릭하고 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너로 전환한 후 **차원 용도** 탭을 클릭합니다.  
  
     현재 **Geography** 큐브 차원은 **Internet Sales** 측정값 그룹이나 **Reseller Sales** 측정값 그룹과 관계가 정의되어 있지 않습니다.  
  
8.  **Customer**차원과 **Internet Sales** 측정값 그룹의 교집합에서 **Full Name** 셀의 줄임표 단추( **…** )를 클릭합니다.  
  
     **관계 정의** 대화 상자에는 **DimCustomer** 차원 테이블과 **FactInternetSales** 측정값 그룹 테이블 각각의 **CustomerKey** 열을 기반으로 이러한 테이블 간 **일반** 관계가 정의되어 있습니다. 이 작업 이전에 이 자습서에서 정의한 모든 관계는 일반 관계입니다.  
  
     다음 그림에서는 **DimCustomer** 차원 테이블과 **FactInternetSales** 측정값 그룹 테이블의 일반 관계가 정의된 **관계 정의** 대화 상자를 보여 줍니다.  
  
     ![정의 관계 대화 상자](../../2014/tutorials/media/l5-referencedrelationship-4.gif "관계 정의 대화 상자")  
  
9. **취소**를 클릭합니다.  
  
10. **Geography**차원과 **Reseller Sales** 측정값 그룹의 교집합에서 명명되지 않은 셀의 줄임표 단추( **…** )를 클릭합니다.  
  
     **관계 정의** 대화 상자에는 현재 Geography 큐브 차원과 Reseller Sales 측정값 그룹 간에 관계가 정의되어 있지 않습니다. Geography 차원의 차원 테이블과 Reseller Sales 측정값 그룹의 팩트 테이블 간 직접 관계가 없으므로 일반 관계를 정의할 수 없습니다.  
  
11. **관계 유형 선택** 목록에서 **참조**를 선택합니다.  
  
     *에서 참조 차원을 팩트 테이블에 연결하는 데 사용할 수 있는 측정값 그룹 테이블에 직접 연결된*중간 차원 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이라는 차원을 지정하여 참조 관계를 정의합니다. 그런 다음 참조 차원을 중간 차원에 연결하는 특성을 지정합니다.  
  
12. **중간 차원** 목록에서 **Reseller**를 선택합니다.  
  
     Geography 차원의 기본 테이블이 Reseller 차원의 기본 테이블을 통해 팩트 테이블에 연결됩니다.  
  
13. **참조 차원 특성** 목록에서 **Geography Key**를 선택한 다음 **중간 차원 특성** 목록에서 **Geography Key** 를 선택해 봅니다.  
  
     **Geography Key** 는 **중간 차원 특성** 목록에 나타나지 않습니다. **GeographyKey** 열이 **Reseller** 차원의 특성으로 정의되어 있지 않기 때문입니다.  
  
14. **취소**를 클릭합니다.  
  
 다음 태스크에서는 Reseller 차원의 GeographyKey 열을 기반으로 특성을 정의하여 이 문제를 해결하는 방법에 대해 설명합니다.  
  
## <a name="defining-the-intermediate-dimension-attribute-and-the-referenced-dimension-relationship"></a>중간 차원 특성 및 참조 차원 관계 정의  
  
1.  **Reseller** 차원에 대한 차원 디자이너를 연 다음 **데이터 원본 뷰** 창에서 **Reseller** 테이블의 열을 확인하고 **특성** 창에서 **Reseller** 차원의 정의된 특성을 확인합니다.  
  
     GeographyKey는 Reseller 테이블에 열로 정의되어 있지만 이 열을 기반으로 Reseller 차원에 정의된 차원 특성은 없습니다. Geography는 Geography 차원의 기본 테이블을 팩트 테이블에 연결하는 키 열이므로 해당 차원의 차원 특성으로 정의됩니다.  
  
2.  **Reseller** 차원에 **Geography Key** 특성을 추가하려면 **데이터 원본 뷰** 창의 **GeographyKey** 를 마우스 오른쪽 단추로 클릭하고 **열의 새 특성**을 클릭합니다.  
  
3.  **특성** 창에서 **Geography Key**를 선택한 후 속성 창에서 **AttributeHierarchyOptimizedState** 속성을 **NotOptimized**로, **AttributeHierarchyOrdered** 속성을 **False**로, **AttributeHierarchyVisible** 속성을 **False**로 설정합니다.  
  
     Reseller 차원의 Geography Key 특성은 Geography 차원을 Reseller Sales 팩트 테이블에 연결하는 데만 사용됩니다. 이 특성은 찾아보기에는 사용되지 않으므로 이 특성 계층을 표시하도록 정의하는 값은 없습니다. 또한 특성 계층 정렬 및 최적화는 처리 성능에 부정적 영향만 미칩니다. 그러나 두 차원 간 링크로 기능하려면 해당 특성이 설정되어 있어야 합니다.  
  
4.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너로 전환하고 **차원 용도** 탭을 클릭한 다음**Reseller Sales**측정값 그룹과 **Geography** 큐브 차원의 교집합에서 줄임표 단추( **…** )를 클릭합니다.  
  
5.  **관계 유형 선택** 목록에서 **참조**를 선택합니다.  
  
6.  **중간 차원** 목록에서 **Reseller**를 선택합니다.  
  
7.  **참조 차원 특성** 목록에서 **Geography Key**를 선택한 다음 **중간 차원 특성** 목록에서 **Geography Key** 를 선택합니다.  
  
     **구체화** 확인란이 선택되어 있습니다. 이것은 MOLAP 차원의 기본 설정입니다. 차원의 MOLAP 구조에서 차원 특성 링크를 구체화하면 처리하는 동안 팩트 테이블과 각 행의 참조 차원 간 링크 값이 구체화되거나 저장됩니다. 이렇게 해도 처리 성능과 저장 요구 사항에는 거의 영향을 주지 않지만 쿼리 성능은 향상되며 때로 크게 향상되는 경우도 있습니다.  
  
8.  **확인**을 클릭합니다.  
  
     **Geography** 큐브 차원이 **Reseller Sales** 측정값 그룹에 연결되어 있습니다. 이 아이콘은 해당 관계가 참조 차원 관계임을 나타냅니다.  
  
9. **차원 용도** 탭의 **차원** 목록에서 **Geography**를 마우스 오른쪽 단추로 클릭한 다음 **이름 바꾸기**를 클릭합니다.  
  
10. 이 큐브 차원의 이름을 변경할 `Reseller Geography`합니다.  
  
     이제 이 큐브 차원이 **Reseller Sales** 측정값 그룹에 연결되었으므로 사용자는 큐브에서 해당 차원의 용도를 명시적으로 정의하여 사용자 혼동을 방지할 수 있습니다.  
  
## <a name="successfully-dimensioning-reseller-sales-by-geography"></a>지리별로 Reseller Sales 차원 구분  
  
1.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 **Tutorial 큐브에 대한 큐브 디자이너에서** 브라우저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 탭을 클릭한 다음 **다시 연결** 단추를 클릭합니다.  
  
3.  메타 데이터 창에서 확장 `Reseller Geography`를 마우스 오른쪽 단추로 클릭 **지역**를 클릭 하 고 **행 영역에 추가**합니다.  
  
     다음 그림에 표시된 것처럼 이제 **Reseller Sales-Sales Amount** 측정값은 **Geographies** 사용자 정의 계층의 **Country-Region** 특성별로 차원이 제대로 구분됩니다.  
  
     ![정의 관계 대화 상자](../../2014/tutorials/media/l5-referencedrelationship-5.gif "관계 정의 대화 상자")  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [팩트 관계 정의](../analysis-services/lesson-5-2-defining-a-fact-relationship.md)  
  
## <a name="see-also"></a>관련 항목  
 [특성 관계](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)   
 [참조 관계 및 참조 관계 속성 정의](multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
  
