---
title: "차원 데이터 (Analysis Services)에 대 한 사용자 지정 액세스 부여 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.dimensiondata.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- AllowedSet property
- IsAllowed property
- DeniedSet property
- user access rights [Analysis Services], dimensions
- custom dimension data access [Analysis Services]
- permissions [Analysis Services], dimensions
- DefaultMember property
- VisualTotals property
- ApplyDenied property
ms.assetid: b028720d-3785-4381-9572-157d13ec4291
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 42ea70f08c2f051970898fa4e3e9498f7f8c1627
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>차원 데이터에 대한 사용자 지정 액세스 부여(Analysis Services)
  큐브에 대한 읽기 권한을 활성화한 후 차원 구성원(큐브에 사용된 모든 측정값을 포함하는 측정값 차원에 포함된 측정값 포함)에 대한 액세스를 명시적으로 허용하거나 거부하는 추가 권한을 설정할 수 있습니다. 예를 들어 여러 범주의 재판매인의 경우, 특정 비즈니스 유형에 대한 데이터를 제외하도록 권한을 설정할 수 있습니다. 다음은 Reseller 차원에서 Warehouse 비즈니스 유형에 대한 액세스 거부의 전후 효과를 설명합니다.  
  
 ![피벗 테이블 및 차원 구성원이 없는](../../analysis-services/multidimensional-models/media/ssas-permsdimdenied.png "와 차원 구성원이 없는 피벗 테이블")  
  
 기본적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브의 데이터를 읽을 수 있는 경우, 해당 큐브와 연결된 모든 측정값 및 차원 구성원에 대해 자동으로 읽기 권한을 가집니다. 많은 시나리오에 대해 이 동작이 충분하지만, 때때로 보안 요구 사항은 같은 차원의 여러 사용자에 대한 다양한 액세스 수준을 지닌 더 세분화된 승인 전략을 요구합니다.  
  
 액세스를 허용(AllowedSet)하거나 거부(DeniedSet)할 멤버를 선택하여 액세스를 제한할 수 있습니다. 역할에 포함하거나 역할에서 제외할 차원 구성원을 선택하거나 선택 취소하여 액세스를 제한합니다.  
  
 기본 차원 보안이 가장 간단합니다. 역할에 포함하거나 역할에서 제외할 차원 특성 및 차원 계층을 선택하기만 하면 됩니다. 고급 보안은 좀 더 복잡하며 MDX 스크립팅에 대한 전문 지식이 필요합니다. 아래에 두 방법이 설명되어 있습니다.  

> [!NOTE]  
>  다음 지침에서는 MDX에서 쿼리를 실행하는 클라이언트 연결을 가정합니다. 클라이언트에서 Power BI의 파워 뷰와 같은 DAX를 사용하는 경우 차원 보안이 쿼리 결과에 분명히 나타나지 않습니다. 자세한 내용은 [다차원 모델용 파워 뷰 이해](understanding-power-view-for-multidimensional-models.md) 를 참조하세요.
      
## <a name="prerequisites"></a>필수 구성 요소  
 일부 측정값 또는 차원 구성원은 사용자 지정 액세스 시나리오에 사용할 수 없습니다. 역할이 기본 측정값 또는 구성원에 대한 액세스를 제한하거나 측정값 식의 일부인 측정값에 대한 액세스를 제한하는 경우 연결에 실패합니다.  
  
 **차원 보안에 대한 장애물 확인: 기본 측정값, 기본 구성원 및 측정값 식에 사용된 측정값**  
  
1.  SQL Server Management Studio에서 큐브를 마우스 오른쪽 단추로 클릭하고 **큐브 스크립팅** | **변경** | **새 쿼리 편집기 창**을 선택합니다.  
  
2.  **DefaultMeasure**를 검색합니다. 큐브에 대해 하나, 각 큐브 뷰에 대해 하나를 찾아야 합니다. 차원 보안을 정의할 때 기본 측정값에 대한 액세스를 제한하지 않습니다.  
  
3.  다음으로 **MeasureExpression**을 검색합니다. 측정값 식은 계산에 종종 다른 측정값이 포함되는 계산을 기준으로 하는 측정값입니다. 제한하려는 측정값이 식에 사용되지 않는지 확인합니다. 또는 액세스를 제한하고 큐브의 해당 측정값에 대한 모든 참조를 제외하는지도 확인합니다.  
  
4.  마지막으로 **DefaultMember**를 검색합니다. 특성의 기본 구성원 역할을 하는 특성을 적어 둡니다. 차원 보안을 설정할 때 그러한 특성에 제한을 설정하지 않습니다.  
  
## <a name="basic-dimension-security"></a>기본 차원 보안  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 개체 탐색기에서 해당 데이터베이스에 대한 **역할** 을 확장한 다음 데이터베이스 역할을 클릭하거나 새 데이터베이스 역할을 만듭니다.  
  
     역할에 이미 큐브에 대한 읽기 권한이 있어야 합니다. 자세한 내용은 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) 를 참조하세요.  
  
2.  **차원 데이터** | **기본**에서 권한을 설정하려는 차원을 선택합니다.  
  
3.  특성 계층을 선택합니다. 일부 특성은 사용할 수 없습니다. **AttributeHierarchyEnabled** 가 있는 특성만 **특성 계층** 목록에 표시됩니다.  
  
4.  액세스를 허용하거나 거부할 구성원을 선택합니다. **멤버 모두 선택** 옵션에서 액세스 허용이 기본값입니다. 이 기본값을 유지한 다음 이 역할을 통해 **멤버 자격** 창의 Windows 사용자 및 그룹 계정에 표시하지 않을 각 구성원을 선택 해제하는 것이 좋습니다. 향후 처리 작업에서 추가되는 새 구성원이 이 역할을 통해 연결하는 사람들에게 자동으로 표시되는 이점이 있습니다.  
  
     또는 **멤버 모두 선택 취소** 하여 전체 액세스를 취소한 다음 허용할 구성원을 선택할 수 있습니다. 향후 처리 작업에서, 차원 데이터 보안을 수동으로 편집하여 새 구성원에 대한 액세스를 허용할 때까지 새 구성원이 표시되지 않습니다.  
  
5.  필요에 따라 **고급** 을 클릭하여 이 특성 계층에 대해 **보이는 값 합계** 를 사용합니다. 이 옵션은 역할을 통해 사용 가능한 구성원을 기준으로 집계를 다시 계산합니다.  
  
    > [!NOTE]  
    >  차원 구성원을 지우는 권한을 적용할 때, 집계된 합계가 자동으로 다시 계산되지 않습니다. 권한이 적용되기 전에 특성 계층의 **All** 구성원이 200을 반환한다고 가정합시다. 일부 구성원에 대한 액세스를 거부하는 권한이 적용된 후, 사용자에게 표시되는 구성원 값이 200보다 훨씬 적음에도 불구하고 **All** 은 계속 200을 반환합니다. 큐브의 소비자가 혼동하지 않도록 **All** 구성원을 특성 계층의 모든 구성원에 대한 집계가 아니라, 역할 구성원에 대한 구성원의 집계로 구성할 수 있습니다. 이 동작을 호출하기 위해 차원 보안을 구성할 때 고급 **Visual Totals** **탭에서** 를 활성화할 수 있습니다. 이 기능을 설정하면 미리 계산된 집계에서 가져오지 않고 쿼리 시 집계가 계산됩니다. 이 기능은 쿼리 성능에 많은 영향을 미칠 수 있으므로 필요한 경우에만 사용하세요.  
  
## <a name="hiding-measures"></a>측정값 숨기기  
 [Grant custom access to cell data &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)에서는 셀 데이터가 아닌 측정값의 모든 보이는 측면을 완전히 숨기려면 차원 멤버에 대한 권한이 필요하다고 설명했습니다. 이 섹션에서는 측정값의 개체 메타데이터에 대한 액세스를 거부하는 방법을 설명합니다.  
  
1.  **차원 데이터** | **기본**에서 큐브 차원에 도달할 때까지 차원 목록을 아래로 스크롤한 다음 **측정값 차원**을 선택합니다.  
  
2.  측정값 목록에서 이 역할을 통해 연결하는 사용자에게 표시되지 않아야 하는 측정값의 확인란을 선택 취소합니다.  
  
> [!NOTE]  
>  역할 보안을 위반할 수 있는 측정값을 식별하는 방법을 보려면 필수 구성 요소를 확인하세요.  
  
## <a name="advanced-dimension-security"></a>고급 차원 보안  
 MDX 전문 지식을 가지고 있는 경우, 액세스를 허용하거나 거부할 구성원에 대한 기준을 설정하는 MDX 식을 쓸 수도 있습니다. **역할 만들기** | **차원 데이터** | **고급** 을 클릭하여 스크립트를 제공합니다.  
  
 MDX 작성기를 사용하여 MDX 문을 쓸 수 있습니다. 자세한 내용은 [MDX 작성기&#40;Analysis Services - 다차원 데이터&#41;](http://msdn.microsoft.com/library/fecbf093-65ea-4e1b-b637-f04876f1cb0f)를 참조하세요. **고급** 탭에는 다음 옵션이 있습니다.  
  
 **Attribute**  
 멤버 보안을 관리할 특성을 선택합니다.  
  
 **허용된 멤버 집합**  
 AllowedSet은 멤버 없음(기본값), 모든 멤버 또는 일부 멤버로 분석할 수 있습니다. 특성에 대한 액세스를 허용하고 허용 집합의 멤버를 정의하지 않으면 모든 멤버에 대한 액세스 권한이 부여됩니다. 특성에 대한 액세스를 허용하고 특정한 특성 구성원 집합을 정의하면 명시적으로 허용된 구성원만 표시됩니다.  
  
 AllowedSet을 생성하면 특성이 여러 수준 계층에 참여할 때 파급 효과가 있습니다. 예를 들어 역할이 워싱턴 주에 대한 액세스를 허용한다고 가정해 봅시다(역할이 회사의 워싱턴 주 영업 부서에 대한 권한을 부여하는 시나리오를 가정). 이 역할을 통해 연결된 사람은 상위 항목(미국) 또는 하위 항목(시애틀 및 레드먼드)이 포함된 쿼리를 통해 워싱턴 주를 포함한 체인의 구성원만 볼 수 있습니다. 다른 주를 명시적으로 허용하지 않았기 때문에 거부된 것과 같은 효과가 나타납니다.  
  
> [!NOTE]  
>  특성 구성원의 빈 집합 ({})을 정의하면 데이터베이스 역할에 대해 어떤 특성 구성원도 표시되지 않습니다. 허용 집합이 없는 경우가 빈 집합으로 해석되지는 않습니다.  
  
 **거부된 멤버 집합**  
 DeniedSet 속성은 멤버 없음, 모든 멤버(기본값) 또는 일부 특성 멤버로 분석할 수 있습니다. 거부 집합에 특정한 특성 구성원 집합만 포함되어 있으면 특성이 여러 수준 계층에 있는 경우 하위 항목뿐만 아니라 그러한 특정 구성원에 대해서만 데이터베이스 역할의 액세스가 거부됩니다. 워싱턴 주 영업 부서 예를 생각해 봅시다. 워싱턴이 DeniedSet에 있는 경우 이 역할을 통해 연결하는 사람들에게 워싱턴과 하위 특성을 제외한 다른 모든 주가 표시됩니다.  
  
 거부된 집합이 고정된 컬렉션인 이전 섹션을 생각해 보세요. 이후 처리에서 액세스가 거부되어야 하는 새 구성원이 사용되는 경우, 이 역할을 편집하여 해당 구성원을 목록에 추가해야 합니다.  
  
 **기본 멤버**  
 DefaultMember 속성은 쿼리에 특성이 명시적으로 포함되어 있지 않을 때 클라이언트에 반환되는 데이터 집합을 결정합니다. 특성이 명시적으로 포함되어 있지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 특성에 대해 다음 기본 멤버 중 하나를 사용합니다.  
  
-   데이터베이스 역할이 특성에 대한 기본 멤버를 정의하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 이 기본 멤버를 사용합니다.  
  
-   데이터베이스 역할이 특성에 대한 기본 멤버를 정의하지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 특성 자체에 대해 정의된 기본 멤버를 사용합니다. 특성이 집계할 수 없는 것으로 정의된 경우를 제외하고는 달리 지정하지 않는 한 특성에 대한 기본 멤버는 **All** 멤버입니다.  
  
 예를 들어 데이터베이스 역할이 **Male** 을 **Gender** 특성에 대한 기본 구성원으로 지정한다고 가정합니다. 쿼리가 **Gender** 특성을 명시적으로 포함하면서 이 특성에 대해 다른 멤버를 지정하는 경우가 아니면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 남성 고객만 포함하는 데이터 집합을 반환합니다. 기본 멤버 설정에 대한 자세한 내용은 [기본 멤버 정의](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)를 참조하세요.  
  
 **보이는 값 합계 사용**  
 VisualTotals 속성은 표시되는 집계된 셀 값이 모든 셀 값에 따라 계산되는지 또는 데이터베이스 역할에 표시되는 셀 값에 따라서만 계산되는지 나타냅니다.  
  
 VisualTotals 속성은 기본적으로 사용되지 않습니다( **False**로 설정). 이 기본 설정을 사용하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 계산할 셀 값을 선택하는 데 시간을 들이는 대신 모든 셀 값의 합계를 빠르게 계산할 수 있기 때문에 성능이 향상됩니다.  
  
 그러나 VisualTotals 속성이 사용되지 않는 경우 사용자가 집계된 셀 값을 사용하여 자신의 데이터베이스 역할이 액세스할 수 없는 특성 멤버의 값을 추론할 수 있다면 보안 문제가 발생할 수 있습니다. 예를 들어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 세 개의 특성 멤버 값을 사용하여 집계된 셀 값을 계산한다고 가정합니다. 이 경우 데이터베이스 역할은 이러한 세 개의 특성 멤버 중 두 개를 볼 수 있는 액세스 권한을 가집니다. 이 데이터베이스 역할의 멤버는 집계된 셀 값을 사용하여 세 번째 특성 멤버의 값을 추론할 수 있습니다.  
  
 VisualTotals 속성을 **True** 로 설정하면 이 위험을 제거할 수 있습니다. VisualTotals 속성을 사용할 경우 데이터베이스 역할은 해당 역할이 사용 권한을 갖는 차원 멤버에 대해 집계된 합계만 볼 수 있습니다.  
  
 **확인**  
 이 페이지에서 정의한 MDX 구문을 테스트하려면 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [셀 데이터 &#40;에 대 한 사용자 지정 액세스 부여 Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)   
 [데이터 마이닝 구조 및 모델 &#40;에 대 한 권한 부여 Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [데이터 원본 개체에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  

