---
title: "사용자 정의 계층의 특성 관계 4-6 지정 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 456c2a47-d395-45f9-9efa-89f3fa2ac621
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2c9d71ea7710736a17a404a997e43e6683894cd7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="4-6-specifying-attribute-relationships-in-user-defined-hierarchy"></a>사용자 정의 계층의 특성 관계 4-6 지정
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]이 자습서에서 이미 설명한, 대로 탐색 경로를 제공할 큐브의 사용자에 대 한 사용자 계층 안에 수준으로 특성 계층을 구성할 수 있습니다. 사용자 계층은 구/군/시, 시/도 및 국가와 같은 자연 계층을 나타내거나 직원 이름, 직책 및 부서 이름과 같은 탐색 경로를 나타낼 수 있습니다. 계층을 탐색하는 사용자에게는 이 두 가지 유형의 사용자 계층이 동일합니다.  
  
자연 계층에서는 수준을 구성하는 특성 간의 특성 관계를 정의하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 특정한 특성의 집계를 사용하여 관련 특성에서 결과를 가져올 수 있습니다. 특성 간에 정의된 관계가 없으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 가 키 특성에서 키가 아닌 특성을 모두 집계합니다. 따라서 기본 데이터가 특성 관계를 지원하는 경우 특성 간의 특성 관계를 정의해야 합니다. 특성 관계를 정의하면 차원, 파티션 및 쿼리 처리 성능이 개선됩니다. 자세한 내용은 [특성 관계 정의](../analysis-services/multidimensional-models/attribute-relationships-define.md) 및 [특성 관계](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)를 참조하세요.  
  
특성 관계를 정의할 때 유동적 관계 또는 고정된 관계로 지정할 수 있습니다. 고정된 관계로 정의할 경우 차원이 업데이트되면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 가 집계를 보유합니다. 정의된 관계가 고정된 관계로 실제로 변경되면 차원이 전체적으로 처리되지 않을 경우 처리하는 동안 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 오류를 생성합니다. 관계와 관계 속성을 적절히 지정하면 쿼리와 처리 성능이 향상됩니다. 자세한 내용은 [특성 관계 정의](../analysis-services/multidimensional-models/attribute-relationships-define.md)및 [사용자 계층 속성](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)을 참조하세요.  
  
이 항목의 태스크에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트의 자연 사용자 계층에 있는 특성의 특성 관계를 정의합니다. **Customer** 차원의 **Customer Geography**계층, **Sales Territory** 차원의 **Sales Territory** 계층, **Product** 차원의 **Product Model Lines** 계층 및 **Date** 차원의 **Fiscal Date** 와 **Calendar Date** 계층이 여기에 포함됩니다. 이러한 사용자 계층은 모두 자연 계층입니다.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>Customer Geography 계층에 있는 특성의 특성 관계 정의  
  
1.  Customer 차원에 대한 차원 디자이너로 전환한 다음 **차원 구조** 탭을 클릭합니다.  
  
    **계층** 창에서 **Customer Geography** 사용자 정의 계층의 수준을 확인합니다. 수준 또는 특성 간의 관계가 정의되지 않았으므로 현재 이 계층은 사용자에 대한 드릴다운 경로에 불과합니다.  
  
2.  **특성 관계** 탭을 클릭합니다.  
  
    **Geography** 테이블의 키가 아닌 특성을 **Geography** 테이블의 키 특성에 연결하는 4개의 특성 관계를 확인합니다. **Geography** 특성은 **Full Name** 특성에 연결되어 있습니다. **Postal Code** 는 **Geography** 특성에 연결되고 **Geography** 특성은 **Full Name** 특성에 연결되므로 **Postal Code** 특성은 **Geography** 특성을 통해 **Full Name** 특성에 간접적으로 연결됩니다. 다음으로, **Geography** 특성을 사용하지 않도록 특성 관계를 변경합니다.  
  
3.  다이어그램에서 **Full Name** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
4.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Full Name**입니다. **관련 특성** 을 **Postal Code**로 설정합니다. 멤버 간의 관계는 시간이 지나면 변경될 수 있으므로 **관계 유형** 목록에서 관계 유형을 **유동**으로 설정된 상태로 둡니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    관계가 중복되기 때문에 다이어그램에 경고 아이콘이 표시됩니다. **Full Name** -> **Geography**-> **Postal Code** 관계는 이미 존재하고 **Full Name** -> **Postal Code**관계는 방금 만들었습니다. 이제 **Geography**-> **Postal Code** 관계는 중복되므로 제거합니다.  
  
6.  **특성 관계** 창에서 **Geography**-> **Postal Code** 를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
7.  **개체 삭제** 대화 상자가 나타나면 **확인**을 클릭합니다.  
  
8.  다이어그램에서 **Postal Code** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
9. **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Postal Code**입니다. **관련 특성** 을 **City**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **유동**으로 설정된 상태로 둡니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    이제 **Geography**-> **City** 관계는 중복되므로 삭제합니다.  
  
11. 특성 관계 창에서 **Geography**-> **City** 를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
12. **개체 삭제** 대화 상자가 나타나면 **확인**을 클릭합니다.  
  
13. 다이어그램에서 **City** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
14. **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **City**입니다. **관련 특성** 을 **State-Province**로 설정합니다. 구/군/시와 시/도의 관계는 시간이 지나도 변경되지 않으므로 **관계 유형** 목록에서 관계 유형을 **고정** 으로 설정합니다.  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. **Geography** 와 **State-Province** 사이의 화살표를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
17. **개체 삭제** 대화 상자가 나타나면 **확인**을 클릭합니다.  
  
18. 다이어그램에서 **State-Province** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
19. **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **State-Province**입니다. **관련 특성** 을 **Country-Region**으로 설정합니다. 시/도와 국가/지역의 관계는 시간이 지나도 변경되지 않으므로 **관계 유형** 목록에서 관계 유형을 **고정** 으로 설정합니다.  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. 특성 관계 창에서 **Geography**-> **Country-Region** 을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
22. **개체 삭제** 대화 상자가 나타나면 **확인**을 클릭합니다.  
  
23. **차원 구조** 탭을 클릭합니다.  
  
    **Geography** 와 다른 특성 간 마지막 특성 관계를 삭제하면 해당 **Geography** 자체가 삭제됩니다. 특성이 더 이상 사용되지 않기 때문입니다.  
  
24. 파일 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>Sales Territory 계층에 있는 특성의 특성 관계 정의  
  
1.  **Sales Territory** 차원에 대한 차원 디자이너를 연 다음 **특성 관계** 탭을 클릭합니다.  
  
2.  다이어그램에서 **Sales Territory Country** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
3.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Sales Territory Country**입니다. **관련 특성** 을 **Sales Territory Group**으로 설정합니다. **관계 유형** 목록에서 관계 유형을 **유동**으로 설정된 상태로 둡니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    이제**Sales Territory Group** 은 **Sales Territory Country**에 연결되고 **Sales Territory Country** 은 **Sales Territory Region**에 연결됩니다. 한 국가의 지역 그룹화와 국가의 그룹화는 나중에 달라질 수 있으므로 이러한 각 관계의 **RelationshipType** 속성은 **유동** 으로 설정됩니다.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>Product Model Lines 계층에 있는 특성의 특성 관계 정의  
  
1.  **Product** 차원에 대한 차원 디자이너를 연 다음 **특성 관계** 탭을 클릭합니다.  
  
2.  다이어그램에서 **Model Name** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
3.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Model Name**입니다. **관련 특성**을 **Product Line**으로 설정합니다. **관계 유형** 목록에서 관계 유형을 **유동**으로 설정된 상태로 둡니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>Fiscal Date 계층에 있는 특성의 특성 관계 정의  
  
1.  **Date** 차원에 대한 차원 디자이너로 전환한 다음 **특성 관계** 탭을 클릭합니다.  
  
2.  다이어그램에서 **Month Name** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
3.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Month Name**입니다. **관련 특성** 을 **Fiscal Quarter**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  다이어그램에서 **Fiscal Quarter** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
6.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Fiscal Quarter**입니다. **관련 특성** 을 **Fiscal Semester**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  다이어그램에서 **Fiscal Semester** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
9. **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Fiscal Semester**입니다. **관련 특성** 을 **Fiscal Year**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>Calendar Date 계층에 있는 특성의 특성 관계 정의  
  
1.  다이어그램에서 **Month Name** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
2.  **특성 관계 만들기** 대화 상자에서 **원본 특성**은 **Month Name**입니다. **관련 특성** 을 **Calendar Quarter**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  다이어그램에서 **Calendar Quarter** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
5.  **특성 관계 만들기** 대화 상자에서 **원본 특성**은 **Calendar Quarter**입니다. **관련 특성** 을 **Calendar Semester**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  다이어그램에서 **Calendar Semester** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
8.  **특성 관계 만들기** 대화 상자에서 **원본 특성**은 **Calendar Semester**입니다. **관련 특성** 을 **Calendar Year**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>Geography 계층에 있는 특성의 특성 관계 정의  
  
1.  Geography 차원에 대한 차원 디자이너를 연 다음 **특성 관계** 탭을 클릭합니다.  
  
2.  다이어그램에서 **Postal Code** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
3.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Postal Code**입니다. **관련 특성** 을 **City**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **유동**으로 설정합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  다이어그램에서 **City** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
6.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **City**입니다. **관련 특성**을 **State-Province**로 설정합니다. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  다이어그램에서 **State-Province** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 선택합니다.  
  
9. **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **State-Province**입니다. **관련 특성** 을 **Country-Region**으로 설정합니다. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 다이어그램에서 **Geography Key** 특성을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
12. **AttributeHierarchyOptimizedState** 속성을 **NotOptimized**로, **AttributeHierarchyOrdered** 속성을 **False**로, **AttributeHierarchyVisible** 속성을 **False**로 설정합니다.  
  
13. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
14. **의** 빌드 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[알 수 없는 멤버 및 Null 처리 속성 정의](../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>관련 항목:  
[특성 관계 정의](../analysis-services/multidimensional-models/attribute-relationships-define.md)  
[사용자 계층 속성](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
  
