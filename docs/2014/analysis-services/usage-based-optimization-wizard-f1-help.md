---
title: 사용 빈도 기반 최적화 마법사 F1 도움말 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.f1
helpviewer_keywords:
- Usage-Based Optimization Wizard
ms.assetid: e5f5a938-ae7c-4f4e-9416-a7f94ac82763
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5e94818245ba1e87d90f87539ae07e9531e5450
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065566"
---
# <a name="usage-based-optimization-wizard-f1-help"></a>사용 빈도 기반 최적화 마법사 F1 도움말
  사용 빈도 기반 최적화 마법사는 출력 면에서 집계 디자인 마법사와 유사하며 파티션에 대한 집계를 디자인하는 데 사용됩니다. 그러나 사용 빈도 기반 최적화 마법사는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스의 쿼리 로그에 기록된 쿼리의 특정 사용 패턴을 기반으로 집계를 디자인합니다. 집계를 사용하면 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 각 쿼리에 대해 기본 데이터 원본의 데이터를 다시 계산할 필요 없이 큐브 저장소에서 직접 미리 계산된 합계를 검색할 수 있으므로 성능이 향상됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]내에서 사용 빈도 기반 최적화 마법사를 열려면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트의 큐브 디자이너를 연 다음 **집계** 탭을 클릭합니다. 도구 모음에서 **사용 빈도 기반 최적화** 단추를 클릭합니다.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]내에서 사용 빈도 기반 최적화 마법사를 열려면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 연결한 다음 **큐브** 폴더를 엽니다. 큐브를 선택한 다음 **측정값 그룹** 폴더를 열고 수정하려는 측정값 그룹을 확장합니다. **파티션** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **사용 빈도 기반 최적화**를 선택합니다.  
  
 이러한 집계를 디자인하려면 집계 디자인 마법사를 사용합니다. 이 마법사는 다음 단계로 이루어져 있습니다.  
  
-   스토리지에 대한 표준 또는 사용자 지정 설정 선택 및 파티션, 측정값 그룹 또는 큐브의 캐싱 옵션 선택  
  
-   파티션, 측정값 그룹 또는 큐브에서 참조하는 예상 또는 실제 개체 수 제공  
  
-   집계 옵션 및 제한을 지정하여 디자인된 집계에서 제공하는 스토리지 및 쿼리 성능 최적화  
  
-   파티션, 측정값 그룹 또는 큐브를 저장하고 선택적으로 처리하여 정의된 집계 생성  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 집계 디자인 마법사를 사용하여 저장소 크기 또는 예상 성능 향상으로 제한할 수 있는 집계 디자인의 배달을 위해 파티션 구조의 통계 분석을 기반으로 집계를 디자인할 수 있습니다. 집계 디자인 마법사를 사용하여 파티션의 전반적인 성능을 향상시킬 수도 있지만 집계 디자인이 비즈니스 사용자의 특정 요구에 부합하지 않을 수 있습니다. 사용 빈도 기반 최적화 마법사에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 쿼리 로그에 특정 쿼리 생성에 필요한 정보가 충분히 포함된 경우 이러한 특정 요구에 부합하는 집계 디자인을 제공할 수 있습니다.  
  
 일반적으로 두 마법사를 함께 사용하여 배포 시는 물론 지속적으로 성능을 향상시킬 수 있습니다. 파티션 또는 파티션이 포함된 큐브 또는 측정값 그룹을 처음에 배포한 경우에는 집계 디자인 마법사를 먼저 사용하여 전반적인 성능을 향상시켜야 합니다. 일정 기간이 지나 쿼리 로그에 파티션에 대한 비즈니스 사용자의 쿼리를 기록한 다음에는 사용 빈도 기반 최적화 마법사를 사용하여 집계 디자인이 비즈니스 사용자의 성능 및 쿼리 요구 사항을 보다 잘 처리할 수 있도록 할 수 있습니다.  
  
> [!NOTE]  
>  쿼리 로그 구성 방법은 [Configuring the Analysis Services Query Log](instances/log-operations-in-analysis-services.md?view=sql-server-2014#bkmk_querylog)(Analysis Services 쿼리 로그 구성)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [수정할 파티션 선택 &#40;사용 빈도 기반 최적화 마법사&#41;](select-partitions-to-modify-usage-based-optimization-wizard.md)  
  
-   [쿼리 조건 지정 &#40;사용 빈도 기반 최적화 마법사&#41;](specify-query-criteria-usage-based-optimization-wizard.md)  
  
-   [최적화 될 쿼리 확인 &#40;사용 빈도 기반 최적화 마법사&#41;](review-the-queries-that-will-be-optimized-usage-based-optimization-wizard.md)  
  
-   [집계 사용 검토 &#40;사용 빈도 기반 최적화 마법사&#41;](review-aggregation-usage-usage-based-optimiation-wizard.md)  
  
-   [개체 수 지정 &#40;사용 빈도 기반 최적화 마법사&#41;](specify-object-counts-usage-based-optimization-wizard.md)  
  
-   [집계 옵션 설정 &#40;사용 빈도 기반 최적화 마법사&#41;](set-aggregation-options-usage-based-optimization-wizard.md)  
  
-   [마법사 완료 &#40;사용 빈도 기반 최적화 마법사&#41;](completing-the-wizard-usage-based-optimization-wizard.md)  
  
## <a name="see-also"></a>관련 항목  
 [집계 및 집계 디자인](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [다차원 모델의 큐브](multidimensional-models/cubes-in-multidimensional-models.md)   
 [집계 디자인 마법사 F1 도움말](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 마법사 &#40;다차원 데이터&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
