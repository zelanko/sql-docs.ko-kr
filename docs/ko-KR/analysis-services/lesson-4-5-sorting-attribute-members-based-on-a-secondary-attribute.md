---
title: 보조 특성을 기준으로 특성 멤버 정렬 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 67dacf68-9ab7-4524-8698-844d0f6e6c6d
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 329e327aab9aa8ce15a3b41d130515221eb95fd0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-4-5---sorting-attribute-members-based-on-a-secondary-attribute"></a>단원 4-5-보조 특성에 따라 특성 멤버 정렬
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]
3단원에서는 이름이나 키 값을 기준으로 특성 멤버를 정렬하는 방법과 복합 멤버 키를 사용하여 특성 멤버와 정렬 순서를 조정하는 방법에 대해 배웠습니다. 자세한 내용은 [Date 차원 수정](../analysis-services/lesson-3-4-modifying-the-date-dimension.md)을 참조하세요. 그러나 특성의 키나 이름으로는 원하는 정렬 순서를 얻을 수 없는 경우 보조 특성을 사용하여 필요한 순서에 따라 정렬할 수 있습니다. 특성 간의 관계를 정의함으로써 두 번째 특성을 사용하여 첫 번째 특성의 멤버를 정렬할 수 있습니다.  
  
특성 관계는 특성 간의 관계나 종속성을 정의합니다. 하나의 관계형 테이블을 기준으로 하는 차원에서는 일반적으로 모든 특성이 키 특성을 통해 서로 연결됩니다. 이는 차원에 대한 모든 특성이 차원의 키 특성으로 각 관련 측정값 그룹의 팩트 테이블에 있는 팩트에 연결된 멤버에 대한 정보를 제공하기 때문입니다. 여러 테이블을 기준으로 하는 차원에서는 일반적으로 특성이 테이블 간의 조인 키를 기준으로 연결됩니다. 기본 데이터에서 지원하는 경우 관련 특성을 사용하여 정렬 순서를 지정할 수 있습니다. 예를 들어, 관련 특성에 대한 정렬 논리를 제공하는 새 특성을 만들 수 있습니다.  
  
차원 디자이너를 사용하면 특성 간의 추가 관계를 정의하거나 기본 관계를 변경하여 성능을 개선할 수 있습니다. 특성 관계를 만들 경우 참조된 특성에는 연결된 특성의 멤버에 대한 값이 하나 이하여야 한다는 주요 제약 조건이 있습니다. 두 특성의 관계를 정의할 경우 나중에 멤버 간의 관계가 변경될지 여부에 따라 관계를 고정된 관계나 유동적 관계로 정의할 수 있습니다. 예를 들어 직원은 다른 판매 지역으로 이동할 수 있지만 도시는 다른 시/도로 이동할 수 없습니다. 관계를 고정된 관계로 정의하면 차원이 증분 처리될 때마다 특성 집계가 다시 계산되지는 않습니다. 그러나 멤버 간의 관계가 변경되면 차원이 전체적으로 처리되어야 합니다. 자세한 내용은 [특성 관계](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md), [특성 관계 정의](../analysis-services/multidimensional-models/attribute-relationships-define.md), [특성 관계 속성 구성](../analysis-services/multidimensional-models/attribute-relationships-configure-attribute-properties.md)및 [사용자 정의 계층의 특성 간 특성 관계 지정](../analysis-services/4-6-specifying-attribute-relationships-in-user-defined-hierarchy.md)을 참조하세요.  
  
이 항목의 태스크에서는 기본 차원 테이블의 기존 열을 기반으로 **Date** 차원에 새 특성을 정의하고 이 새로운 특성을 사용하여 사전순이 아니라 시간순으로 월 멤버를 정렬합니다. 또한 **Commute Distance** 특성 멤버를 정렬하는 데 사용할 명명된 계산을 기반으로 **Customer** 차원에 새 특성을 정의합니다. 다음 항목의 태스크에서는 특성 관계를 사용하여 쿼리 성능을 높이는 방법에 대해 설명합니다.  
  
## <a name="defining-an-attribute-relationship-and-sort-order-in-the-date-dimension"></a>Date 차원의 특성 관계 및 정렬 순서 정의  
  
1.  **Date** 차원에 대한 차원 디자이너를 열고 속성 창에서 **Month Name** 특성의 **OrderBy** 속성을 검토합니다.  
  
    **Month Name** 특성 멤버는 키 값을 기준으로 정렬됩니다.  
  
2.  **브라우저** 탭으로 전환하여 **계층** 목록에서 **Calendar Date** 가 선택되어 있는지 확인한 다음 사용자 정의 계층의 수준을 확장하여 월 정렬 순서를 검색합니다.  
  
    특성 계층의 멤버는 해당 멤버 키의 ASCII 값인 월 및 연도를 기준으로 정렬됩니다. 이 경우 특성 이름이나 키를 기준으로 정렬하면 월이 시간순으로 정렬되지 않습니다. 이 문제를 해결하려면 새 특성인 **MonthNumberOfYear** 특성을 기준으로 특성 계층의 멤버를 정렬합니다. 편의를 위해 **Date** 차원 테이블에 있는 열을 기준으로 이 특성을 만듭니다.  
  
3.  Date 차원의 **차원 구조** 탭으로 전환하여 **데이터 원본 뷰** 창의 **MonthNumberOfYear** 를 마우스 오른쪽 단추로 클릭한 다음 **열의 새 특성**을 클릭합니다.  
  
4.  **특성** 창에서 **Month Number Of Year**를 선택한 후 속성 창에서 **AttributeHierarchyEnabled** 속성을 **False** 로, **AttributeHierarchyOptimizedState** 속성을 **NotOptimized**로, **AttributeHierarchyOrdered** 속성을 **False**로 설정합니다.  
  
    이러한 설정은 사용자에게 보이지 않도록 특성을 숨기며 처리 시간을 단축합니다. 이 특성은 탐색에는 사용되지 않으며 다른 특성의 멤버를 정렬하는 데에만 사용됩니다.  
  
    > [!NOTE]  
    > 속성 창에서 속성을 사전순으로 정렬하면 이러한 3개의 속성이 서로 인접하여 정렬되므로 이 태스크가 단순해집니다.  
  
5.  **특성 관계** 탭을 클릭합니다.  
  
    **Date** 차원의 모든 특성은 **Date** 특성과 직접 연결되며 이 특성은 차원 멤버를 관련된 측정값 그룹의 팩트에 연결하는 멤버 키입니다. **Month Name** 특성과 **Month Number Of Year** 특성 사이에는 관계가 정의되어 있지 않습니다.  
  
6.  다이어그램에서 **Month Name** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
7.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Month Name**입니다. **관련 특성** 을 **Month Number Of Year**로 설정합니다.  
  
8.  **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
    **Month Name** 특성과 **Month Number Of Year** 특성의 멤버 간 관계는 시간이 지나도 변경되지 않습니다. 결과적으로 Analysis Services는 증분 처리 도중에 이 관계에 대한 집계를 삭제하지 않습니다. 관계가 변경되면 증분 처리 도중에 처리 오류가 발생하며 차원의 전체 처리를 수행해야 합니다. 이제 **Month Name**의 멤버에 대한 정렬 순서를 설정할 수 있습니다.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. **차원 구조** 탭을 클릭합니다.  
  
11. **특성** 창에서 **Month Name** 을 선택한 다음 속성 창에서 **OrderBy** 속성 값을 **AttributeKey** 로, **OrderByAttribute** 속성 값을 **Month Number Of Year**로 변경합니다.  
  
12. **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
13. 배포가 성공적으로 완료되면 Date 차원에 대한 **브라우저** 탭으로 전환하고 **다시 연결**을 클릭한 다음 **Calendar Date** 및 **Fiscal Date** 사용자 계층을 찾아 월이 시간순으로 정렬되는지 확인합니다.  
  
    다음 이미지와 같이 이제 월이 시간순으로 정렬됩니다.  
  
    ![시간 순서에 따라 사용자 계층 구조 수정](../analysis-services/media/l4-memberproperties-3.gif "시간 순서에 따라 사용자 계층 구조 수정")  
  
## <a name="defining-attribute-relationships-and-sort-order-in-the-customer-dimension"></a>Customer 차원의 특성 관계 및 정렬 순서 정의  
  
1.  Customer 차원에 대한 차원 디자이너의 **브라우저** 탭으로 전환한 후 **Commute Distance** 특성 계층의 멤버를 탐색합니다.  
  
    이 특성 계층의 멤버는 멤버 키의 ASCII 값을 기준으로 정렬됩니다. 이 경우 특성 이름이나 키를 기준으로 정렬하면 통근 거리가 짧은 순서대로 정렬되지 않습니다. 이 태스크에서는 열의 개별 값에 따라 알맞은 정렬 번호를 매기는 **CommuteDistanceSort** 명명된 계산을 기준으로 특성 계층의 멤버를 정렬합니다. 시간 절약을 위해 이 명명된 계산은 이미 **DW 데이터 원본 뷰의** Customer [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 테이블에 추가되어 있습니다. 이 데이터 원본 뷰로 전환하여 이 명명된 계산에 사용된 SQL 스크립트를 볼 수 있습니다. 자세한 내용은 [데이터 원본 뷰에서 명명된 계산 정의&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
    다음 이미지에서는 멤버 키의 ASCII 값을 기준으로 정렬된 **Commute Distance** 특성 계층 멤버를 보여 줍니다.  
  
    ![통근 거리 특성 계층](../analysis-services/media/l4-memberproperties-4.gif "통근 거리 특성 계층")  
  
2.  Customer 차원에 대한 차원 디자이너에서 **차원 구조** 탭으로 전환하여 **데이터 원본 뷰** 창의 **Customer** 테이블에 있는 **CommuteDistanceSort** 를 마우스 오른쪽 단추로 클릭한 다음 **열의 새 특성**을 클릭합니다.  
  
3.  **특성** 창에서 **Commute Distance Sort**를 선택한 후 속성 창에서 이 특성의 **AttributeHierarchyEnabled** 속성을 **False** 로, **AttributeHierarchyOptimizedState** 속성을 **NotOptimized**로, **AttributeHierarchyOrdered** 속성을 **False**로 설정합니다.  
  
    이러한 설정은 사용자에게 보이지 않도록 특성을 숨기며 처리 시간을 단축합니다. 이 특성은 탐색에는 사용되지 않으며 다른 특성의 멤버를 정렬하는 데에만 사용됩니다.  
  
4.  **Geography**를 선택한 다음 속성 창에서 **AttributeHierarchyVisible** 속성을 **False** 로, **AttributeHierarchyOptimizedState** 속성을 **NotOptimized**로, **AttributeHierarchyOrdered** 속성을 **False**로 설정합니다.  
  
    이러한 설정은 사용자에게 보이지 않도록 특성을 숨기며 처리 시간을 단축합니다. 이 특성은 탐색에는 사용되지 않으며 다른 특성의 멤버를 정렬하는 데에만 사용됩니다. **Geography** 에는 멤버 속성이 있으므로 **AttributeHierarchyEnabled** 속성을 **True**로 설정해야 합니다. 따라서 특성을 숨기려면 **AttributeHierarchyVisible** 속성을 **False**로 설정합니다.  
  
5.  **특성 관계** 탭을 클릭합니다.  
  
6.  특성 목록에서 **Commute Distance** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
7.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Commute Distance**입니다. **관련 특성** 을 **Commute Distance Sort**로 설정합니다.  
  
8.  **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
    **Commute Distance** 특성과 **Commute Distance Sort** 특성의 멤버 간 관계는 시간이 지나도 변경되지 않습니다.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    이제 **Commute Distance** 특성의 정렬 순서를 설정할 수 있습니다.  
  
10. **차원 구조** 탭을 클릭합니다.  
  
11. **특성** 창에서 **Commute Distance**를 선택한 다음 속성 창에서 **OrderBy** 속성 값을 **AttributeKey**로, **OrderByAttribute** 속성 값을 **Commute Distance Sort**로 변경합니다.  
  
12. **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
13. 배포가 성공적으로 완료되면 Customer 차원에 대한 차원 디자이너의 **브라우저** 탭으로 전환하고 **다시 연결**을 클릭한 다음 **Commute Distance** 특성 계층을 찾아봅니다.  
  
    다음 이미지와 같이 이제 특성 계층 멤버가 증가하는 거리를 기준으로 논리적 순서에 따라 정렬됩니다.  
  
    ![통근 거리 특성 계층을 다시 정렬](../analysis-services/media/l4-memberproperties-5.gif "Re-sorted 통근 거리 특성 계층")  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[사용자 정의 계층의 특성 간 특성 관계 지정](../analysis-services/4-6-specifying-attribute-relationships-in-user-defined-hierarchy.md)  
  
  
  
