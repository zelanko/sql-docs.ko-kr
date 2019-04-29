---
title: Attribute Members (Discretization) 그룹 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- NameColumn property
- discretization [Analysis Services]
- member groups [Analysis Services]
- grouping members
- DiscretizationNumber property
- sort orders [Analysis Services]
- DiscretizationMethod property
- adding members to member group
- number of member groups
- members [Analysis Services], groups
- names [Analysis Services], member groups
ms.assetid: 5cf2f407-accc-4baf-b54f-7703af338325
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8f7ff454dd4464fab5173c4d0022bd94543c1dad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62701743"
---
# <a name="group-attribute-members-discretization"></a>특성 멤버 그룹화(불연속화)
  멤버 그룹은 시스템에서 생성된 연속적인 차원 멤버의 모음입니다.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 특성의 멤버를 불연속화라는 프로세스를 통해 여러 개의 멤버 그룹으로 그룹화할 수 있습니다. 계층의 수준에는 멤버 그룹이나 멤버 중 하나만 포함됩니다. 비즈니스 사용자가 멤버 그룹을 포함하는 수준을 탐색하는 경우 해당 멤버 그룹의 이름 및 셀 값이 표시됩니다. 멤버 그룹을 지원하기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 생성하는 멤버를 그룹화 멤버라고 하며 이는 일반 멤버와 유사합니다.  
  
 특성에 대한 `DiscretizationMethod` 속성은 멤버의 그룹화 방식을 제어합니다.  
  
|`DiscretizationMethod` 설정|설명|  
|--------------------------------------|-----------------|  
|`None`|멤버를 표시합니다.|  
|`Automatic`|`EqualAreas` 메서드 또는 `Clusters` 메서드 중에서 데이터를 가장 잘 표현하는 메서드를 선택합니다.|  
|`EqualAreas`|특성의 멤버를 동일한 수의 멤버를 포함하는 그룹으로 나눕니다.|  
|`Clusters`|학습 데이터를 샘플링하여 임의의 지점 수로 초기화하고 EM(Expectation-Maximization) 클러스터링 알고리즘을 몇 차례 반복 실행하여 특성의 멤버를 그룹으로 나눕니다.<br /><br /> 이 방법은 모든 분포 곡선에 대해 작동하므로 유용하지만 처리 시간 면에서는 비용이 더 듭니다.|  
  
 특성에 대한 `DiscretizationNumber` 속성은 표시할 그룹의 수를 지정합니다. 속성을 기본값인 0으로 설정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 `DiscretizationMethod` 속성의 설정에 따라 데이터를 샘플링하거나 읽어서 그룹 수를 결정합니다.  
  
 멤버 그룹의 멤버 정렬 순서는 특성의 `OrderBy` 속성을 사용하여 제어됩니다. 이 정렬 순서를 바탕으로 멤버 그룹의 멤버가 연속적으로 정렬됩니다.  
  
 멤버 그룹의 일반적인 용도는 멤버 수가 적은 수준에서 멤버 수가 많은 수준으로 드릴다운하는 것입니다. 사용자가 수준 간에 드릴다운할 수 있도록 하려면 멤버 수를 많이 포함하는 수준에 대해 특성의 `DiscretizationMethod` 속성을 `None`에서 앞 표에서 설명한 불연속화 메서드 중 하나로 변경합니다. 예를 들어 Client 차원에는 멤버가 500,000개인 Client Name이라는 특성 계층이 포함되어 있습니다. 이 특성의 이름을 Client Groups로 바꾸고 `DiscretizationMethod` 속성을 `Automatic`으로 변경하여 특성 계층 멤버 수준에서 멤버 그룹을 표시할 수 있습니다.  
  
 각 그룹의 개별 클라이언트로 드릴다운하려면 동일한 테이블 열에 바인딩된 Client Name이라는 특성 계층을 새로 만듭니다. 그런 다음 두 특성을 기반으로 새로운 사용자 계층을 만듭니다. 상위 수준은 Client Groups 특성을 기반으로 하고 하위 수준은 Client Name 특성을 기반으로 하면 됩니다. `IsAggregatable` 속성은 두 특성 모두에 대해 `True`가 됩니다. 그런 다음 사용자는 계층의 (All) 수준을 확장하여 그룹 멤버를 보고 그룹 멤버를 확장하여 계층의 리프 멤버를 볼 수 있습니다. 그룹이나 클라이언트 수준을 숨기려면 해당 특성의 `AttributeHierarchyVisible` 속성을 `False`로 설정합니다.  
  
## <a name="naming-template"></a>명명 템플릿  
 멤버 그룹 이름은 멤버 그룹이 생성될 때 자동으로 생성됩니다. 명명 템플릿을 지정하지 않으면 기본 명명 템플릿이 사용됩니다. 특성의 `Format` 속성에 대한 `NameColumn` 옵션에 대해 명명 템플릿을 지정하여 이러한 명명 방법을 변경할 수 있습니다. 특성의 `Translations` 속성에 사용된 열 바인딩의 `NameColumn` 모음에 지정된 모든 언어에 대해 다양한 명명 템플릿을 다시 정의할 수 있습니다.  
  
 `Format` 설정은 다음 문자열 식을 사용하여 명명 템플릿을 정의합니다.  
  
 `<Naming template> ::= <First definition> [;<Intermediate definition>;<Last definition>]`  
  
 `<First definition> ::= <Name expression>`  
  
 `<Intermediate definition> ::= <Name expression>`  
  
 `<Last definition> ::= <Name expression>`  
  
 `<First definition>` 매개 변수는 불연속화 메서드에 의해 생성된 첫 번째 또는 존재하는 유일한 멤버 그룹에만 적용됩니다. 선택적 매개 변수인 `<Intermediate definition>` 과 `<Last definition>` 을 제공하지 않으면 해당 특성에 대해 생성된 모든 측정값 그룹에 대해 `<First definition>` 매개 변수가 사용됩니다.  
  
 `<Last definition>` 매개 변수는 분할 메서드에 의해 생성된 마지막 멤버 그룹에만 적용됩니다.  
  
 `<Intermediate bucket name>` 매개 변수는 분할 메서드에 의해 생성된 첫 번째 또는 마지막 멤버 그룹을 제외한 모든 멤버 그룹에 적용됩니다. 둘 이하의 그룹이 생성된 경우에는 이 매개 변수가 무시됩니다.  
  
 `<Bucket name>` 매개 변수는 멤버 또는 멤버 그룹 정보를 멤버 그룹 이름의 일부로 나타내기 위해 일련의 변수를 통합할 수 있는 문자열 식입니다.  
  
|변수|설명|  
|--------------|-----------------|  
|%{First bucket member}|현재 멤버 그룹에 포함할 첫 번째 멤버의 이름입니다.|  
|%{Last bucket member}|현재 멤버 그룹에 포함할 마지막 멤버의 이름입니다.|  
|%{Previous bucket last member}|이전 멤버 그룹에 할당된 마지막 멤버의 이름입니다.|  
|%{Next bucket first member}|다음 멤버 그룹에 할당할 첫 번째 멤버의 이름입니다.|  
|%{Bucket Min}|현재 멤버 그룹에 할당할 멤버의 최소값입니다.|  
|%{Bucket Max}|현재 멤버 그룹에 할당할 멤버의 최대값입니다.|  
|%{Previous Bucket Max}|이전 멤버 그룹에 할당할 멤버의 최대값입니다.|  
|%{Next Bucket Min}|다음 멤버 그룹에 할당할 멤버의 최소값입니다.|  
  
 이전 버전의 `"%{First bucket member} - %{Last bucket member}"`와의 호환성을 제공하기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]가 기본 명명 템플릿으로 사용됩니다.  
  
> [!NOTE]  
>  세미콜론(;)을 리터럴 문자로 명명 템플릿에 포함하려면 앞에 백분율(%) 문자를 붙입니다.  
  
### <a name="example"></a>예제  
 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 예제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 있는 Customer 차원의 Yearly Income 특성을 분류하는 데 다음 문자열 식을 사용할 수 있습니다. 여기서 Yearly Income 특성은 멤버 그룹화를 사용합니다.  
  
 "Less than %{Next Bucket Min};Between %{First bucket member} and %{Last bucket member};Greater than %{Previous Bucket Max}"  
  
## <a name="adding-new-members-to-existing-member-groups"></a>기존 멤버 그룹에 새 멤버 추가  
 차원에 새 멤버를 추가하면 멤버의 값과 현재 멤버 그룹 레이아웃을 비교하여 적절한 멤버 그룹에 할당합니다.  
  
 새 멤버가 이전 멤버 그룹의 마지막 멤버와 다음 멤버 그룹의 첫 번째 멤버 사이에 삽입되면 이전 멤버 그룹의 마지막 멤버가 됩니다.  
  
## <a name="updating-a-dimension-with-discretized-attributes"></a>불연속화된 특성이 있는 차원 업데이트  
 차원을 처리할 때 불연속화된 특성은 전체 업데이트(ProcessFull)를 통해서만 다시 불연속화됩니다. 특성을 다시 불연속화하려면 차원의 전체 업데이트를 수행해야 합니다. 불연속화된 특성의 차원 테이블이 업데이트된 경우 증분 업데이트(ProcessAdd)를 통해 차원을 처리하면 불연속화된 특성이 다시 불연속화되지 않습니다. 새 버킷의 이름과 자식은 동일하게 유지됩니다. 차원 처리 방법에 대한 자세한 내용은 [Analysis Services 개체 처리](processing-analysis-services-objects.md)를 참조하세요.  
  
## <a name="usage-limitations"></a>사용 제한 사항  
  
-   계층의 최상위 수준이나 최하위 수준에서는 멤버 그룹을 만들 수 없습니다. 그러나 최상위 또는 최하위 수준에 멤버 그룹을 만들어야 하는 경우에는 해당 수준이 더 이상 최상위 또는 최하위 수준이 아니도록 수준을 추가합니다. 추가한 수준의 `Visible` 속성을 `False`로 설정하여 숨길 수 있습니다.   
  
-   한 계층에서 연속되는 두 개의 수준에 멤버 그룹을 만들 수 없습니다.  
  
-   ROLAP 스토리지 모드를 사용하는 차원에 대해서는 멤버 그룹이 지원되지 않습니다.  
  
-   멤버 그룹이 포함된 차원의 차원 테이블이 업데이트된 후 해당 차원이 완전히 처리되면 새로운 멤버 그룹 집합이 생성됩니다. 새 멤버 그룹의 이름과 자식은 원래의 멤버 그룹과 다를 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [특성 및 특성 계층](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
