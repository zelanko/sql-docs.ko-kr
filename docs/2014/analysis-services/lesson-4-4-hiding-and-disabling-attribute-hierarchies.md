---
title: 특성 계층 숨기기 및 해제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 095039c2-7104-414c-a9a6-327b03ce79df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4381047ad4373a2a5b03dc9ba1c96274b37621f2
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530849"
---
# <a name="hiding-and-disabling-attribute-hierarchies"></a>특성 계층 숨기기 및 비활성화
  기본적으로 특성 계층은 차원의 모든 특성에 대해 만들어지며 각 계층을 팩트 데이터 차원 지정에 사용할 수 있습니다. 이 계층은 계층의 모든 멤버를 포함하는 “All” 수준 및 세부 수준으로 구성됩니다. 이미 설명한 대로 특성을 사용자 정의 계층으로 구성하여 큐브에 탐색 경로를 제공할 수 있습니다. 경우에 따라서는 일부 특성과 계층을 비활성화하거나 숨길 수 있습니다. 예를 들어 주민 등록 번호, 급여, 생년월일 및 로그인 정보와 같은 일부 특성은 사용자가 큐브 정보의 차원을 지정하는 데 사용하는 특성이 아닙니다. 일반적으로 이 정보는 특정 특성 멤버의 세부 사항으로만 표시됩니다. 이러한 특성 계층을 숨기고 특정 특성의 멤버 속성으로만 특성을 표시할 수 있습니다. 또한 고객 이름, 우편 번호 등의 다른 특성 멤버가 특성 계층을 통해 따로 표시되지 않고 사용자 계층을 통해 표시될 경우에만 이러한 특성 멤버를 표시할 수도 있습니다. 그 이유 중 하나는 특성 계층에 있는 고유한 멤버의 개수 때문입니다. 마지막으로 처리 성능을 향상시키기 위해 사용자가 탐색에 사용하지 않는 특성 계층을 비활성화해야 합니다.  
  
 **AttributeHierarchyEnabled** 속성 값은 특성 계층을 만들지 여부를 결정합니다. 이 속성을 **False**로 설정하면 특성 계층이 만들어지지 않으며 특성을 사용자 계층의 수준으로 사용할 수 없어 특성 계층이 멤버 속성으로만 존재합니다. 그러나 비활성화된 특성 계층은 여전히 다른 특성의 멤버를 정렬하는 데 사용할 수 있습니다. **AttributeHierarchyEnabled** 속성 값을 **True**로 설정하면 **AttributeHierarchyVisible** 속성 값이 사용자 정의 계층에서의 사용에 관계없이 특성 계층을 표시할지 여부를 결정합니다.  
  
 특성 계층을 활성화하면 다음 3개의 추가 속성 값을 지정할 수 있습니다.  
  
-   **IsAggregatable**  
  
     기본적으로 모든 특성 계층에 (All) 수준이 정의됩니다. 활성화된 특성 계층에 대해 (All) 수준을 비활성화하려면 이 속성의 값을 **False**로 설정합니다.  
  
    > [!NOTE]  
    >  **IsAggregatable** 속성이 false로 설정된 특성은 사용자 정의 계층의 루트로만 사용할 수 있으며 기본 멤버가 지정되어 있어야 합니다. 그렇지 않은 경우 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 엔진이 기본 멤버를 선택합니다.  
  
-   **AttributeHierarchyOrdered**  
  
     기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 처리하는 동안 활성화된 특성 계층의 멤버를 정렬한 다음 Name, Key 등 **OrderBy** 속성의 값에 따라 멤버를 저장합니다. 정렬이 중요하지 않은 경우에는 이 속성의 값을 **False**로 설정하여 처리 성능을 향상시킬 수 있습니다.  
  
-   **AttributeHierarchyOptimizedState**  
  
     기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 처리하는 동안 활성화된 각 특성 계층의 인덱스를 만들어 쿼리 성능을 향상시킵니다. 특성 계층을 찾아볼 수 없도록 하려면 이 속성의 값을 **NotOptimized**로 설정하여 처리 성능을 향상시킬 수 있습니다. 그러나 숨겨진 계층을 차원의 키 특성으로 사용할 경우 특성 멤버의 인덱스를 만들어도 성능이 향상됩니다.  
  
 특성 계층을 비활성화하면 이러한 속성이 적용되지 않습니다.  
  
 이 항목의 태스크에서는 찾아보는 데 사용하지 않을 Employee 차원의 주민 등록 번호 및 그 밖의 특성을 비활성화합니다. 그런 다음 고객 이름과 우편 번호 특성 계층을 Customer 차원에서 숨깁니다. 이러한 계층에 특성 멤버가 많으면 사용자 계층과 관계없이 이러한 계층을 찾아보는 데에 시간이 상당히 많이 걸립니다.  
  
## <a name="setting-attribute-hierarchy-properties-in-the-employee-dimension"></a>Employee 차원의 특성 계층 속성 설정  
  
1.  Employee 차원에 대한 차원 디자이너로 전환한 다음 **브라우저** 탭을 클릭합니다.  
  
2.  **계층** 목록에 다음 특성 계층이 나타나는지 확인합니다.  
  
    -   **기본 비율**  
  
    -   **생년월일**  
  
    -   **로그인 ID**  
  
    -   **관리자 SSN**  
  
    -   **SSN**  
  
3.  **차원 구조** 탭으로 전환한 다음 **특성** 창에서 다음 특성을 선택합니다. CTRL 키를 누른 채 각 측정값을 클릭하면 여러 측정값을 선택할 수 있습니다.  
  
    -   **기본 비율**  
  
    -   **생년월일**  
  
    -   **로그인 ID**  
  
    -   **관리자 SSN**  
  
    -   **SSN**  
  
4.  속성 창에서 선택한 특성에 대해 **AttributeHierarchyEnabled** 속성 값을 **False** 로 설정합니다.  
  
     **특성** 창에서는 각 특성에 대한 아이콘이 변경되어 해당 특성이 활성화되지 않은 상태임을 나타냅니다.  
  
     다음 이미지에서는 선택한 특성에 대해 False로 설정된 **AttributeHierarchyEnabled** 속성을 보여 줍니다.  
  
     ![AttributeHierarchyEnabled 속성을 False로 설정 합니다](../../2014/tutorials/media/l4-hierarchyenabled-1.gif "AttributeHierarchyEnabled 속성을 False로 설정 합니다") .  
  
5.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
6.  처리가 성공적으로 완료되면 **브라우저** 탭으로 전환하고 **다시 연결**을 클릭한 다음 수정한 특성 계층을 찾아봅니다.  
  
     수정한 특성의 멤버는 **계층** 목록의 특성 계층에서 찾아볼 수 없습니다. 비활성화된 특성 계층 하나를 사용자 계층의 수준으로 추가하려고 하면 특성 계층을 활성화해야 사용자 정의 계층에 포함할 수 있다고 알리는 오류가 표시됩니다.  
  
## <a name="setting-attribute-hierarchy-properties-in-the-customer-dimension"></a>Customer 차원의 특성 계층 속성 설정  
  
1.  Customer 차원에 대한 차원 디자이너로 전환한 다음 **브라우저** 탭을 클릭합니다.  
  
2.  **계층** 목록에 다음 특성 계층이 나타나는지 확인합니다.  
  
    -   **전체 이름**  
  
    -   **우편 번호**  
  
3.  **차원 구조** 탭으로 전환한 다음 Ctrl 키를 사용하여 한 번에 여러 특성을 선택할 수 있으므로 **특성** 창에서 다음 특성을 선택합니다.  
  
    -   **전체 이름**  
  
    -   **우편 번호**  
  
4.  속성 창에서 선택한 특성에 대해 **AttributeHierarchyVisible** 속성 값을 **False** 로 설정합니다.  
  
     이러한 특성 계층의 멤버는 팩트 데이터 차원 지정에 사용되므로 이 특성 계층의 멤버를 정렬하고 최적화하면 성능이 향상됩니다. 따라서 이러한 특성의 속성을 변경하면 안 됩니다.  
  
     다음 이미지에서는 False로 설정된 **AttributeHierarchyVisible** 속성을 보여 줍니다.  
  
     ![AttributeHierarchyVisible 속성을 False로 설정 합니다](../../2014/tutorials/media/l4-hierarchyvisible-1.gif "AttributeHierarchyVisible 속성을 False로 설정 합니다") .  
  
5.  **특성** 창의 **우편 번호** 특성을 **계층 및 수준** 창에 있는 **고객 지리** 사용자 계층의 **구/군/시** 수준 바로 아래로 끌어 놓습니다.  
  
     숨겨진 특성도 사용자 계층의 수준이 될 수 있습니다.  
  
6.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
7.  배포가 성공적으로 완료되면 Customer 차원의 **브라우저** 탭으로 전환한 다음 **다시 연결**을 클릭합니다.  
  
8.  **계층** 목록에서 수정한 특성 계층을 선택해 봅니다.  
  
     수정한 특성 계층은 **계층** 목록에 나타나지 않습니다.  
  
9. **계층** 목록에서 **고객 지리**를 선택한 다음 브라우저 창에서 각 수준을 찾아봅니다.  
  
     숨겨진 수준인 **우편 번호** 와 **전체 이름**이 사용자 정의 계층에 표시됩니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [보조 특성을 기준으로 특성 멤버 정렬](lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)  
  
  
