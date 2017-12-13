---
title: "다차원 모델 (Analysis Services) 처리 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- online mode [Analysis Services]
- processing objects [Analysis Services]
- partitions [Analysis Services], processing
- jobs [Analysis Services]
- objects [Analysis Services], processing
- reprocessing objects
- impact analysis [Analysis Services]
- dimensions [Analysis Services], processing
- project mode [Analysis Services]
- cubes [Analysis Services], processing
ms.assetid: 625aa5a6-aa09-4bac-be8a-778fa81c5a61
caps.latest.revision: "52"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a919efd37f8e10259ee23b9d6b879c46812d2721
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="processing-a-multidimensional-model-analysis-services"></a>다차원 모델 처리(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]처리 단계 또는 일련의 단계를 Analysis Services 다차원 모델에 관계형 데이터 원본에서 데이터 로드는입니다. MOLAP 저장소를 사용하는 개체의 경우 데이터가 데이터베이스 파일 폴더의 디스크에 지정됩니다. ROLAP 저장소의 경우 처리는 개체에 대한 MDX 쿼리의 응답으로 요청 시 발생합니다. ROLAP 저장소를 사용하는 개체의 경우 처리는 쿼리 결과를 반환하기 전 캐시를 업데이트하는 과정을 의미합니다.  
  
 기본적으로 처리는 서버에 솔루션을 배포할 때 수행됩니다. 또한 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 또는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]와 같은 도구를 사용하여 솔루션의 전체 또는 일부를 임시로 처리하거나 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 SQL Server 에이전트를 사용하여 예약을 통해 처리할 수 있습니다. 차원을 제거하거나 해당 호환성 수준을 변경하는 등 모델을 구조적으로 변경할 경우 모델의 물리적 및 논리적 특성을 동기화하도록 다시 처리해야 합니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
 [필수 구성 요소](#bkmk_prereq)  
  
 [도구 또는 방법 선택](#bkmk_tool)  
  
 [개체 처리](#bkmk_proc)  
  
 [Reprocessing Objects](#bkmk_reproc)  
  
##  <a name="bkmk_prereq"></a> 필수 구성 요소  
  
-   처리하려면 Analysis Services 인스턴스에 대한 관리 권한이 필요합니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]로부터 대화식으로 처리할 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 서버 관리자 역할의 멤버여야 합니다. SQL Server 에이전트를 통해 예약하는 SSIS 패키지를 사용하는 경우같이 수동으로 실행되는 처리의 경우 패키지 실행에 사용되는 계정이 서버 관리자 역할의 멤버여야 합니다. 관리자 권한 설정에 대한 자세한 내용은 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)를 참조하세요.  
  
-   데이터를 검색하는 데 사용되는 계정은 데이터 원본 개체에 가장 옵션으로(Windows 인증을 사용하는 경우) 또는 연결 문자열의 사용자 이름으로(데이터베이스 인증을 사용하는 경우) 지정됩니다. 이 계정은 모델에서 사용되는 관계형 데이터 원본에 대한 읽기 권한이 있어야 합니다.  
  
-   개체를 처리하려면 먼저 프로젝트 또는 솔루션을 배포해야 합니다.  
  
     처음에 모델 개발의 초기 단계에서는 배포 및 처리가 함께 수행됩니다. 하지만 솔루션을 배포한 후 나중에 모델을 처리하도록 옵션을 설정할 수 있습니다. 배포에 대한 자세한 내용은 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)를 참조하세요.  
  
##  <a name="bkmk_tool"></a> 도구 또는 방법 선택  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]와 같은 클라이언트 응용 프로그램이나 SQL Server 에이전트 작업 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지로 실행되는 스크립팅된 작업을 사용하여 대화형으로 개체를 처리할 수 있습니다.  
  
 데이터를 처리하는 방법은 모델이 활성 개발 환경에 있는지 프로덕션 환경에 있는지에 따라 상당히 많이 달라집니다. 모델을 프로덕션 서버에 배포한 후에는 다차원 데이터의 무결성과 가용성을 유지하기 위해 처리를 엄격하게 제어해야 합니다. 개체는 상호 종속적이므로 다른 개체가 동시에 처리되거나 처리되지 않는 등 일반적으로 처리 결과 모델 간에 연쇄적인 효과가 있습니다. 일부 개체가 처리되지 않은 상태에 있는 경우 해당 데이터에 대한 쿼리는 확인되지 않으며 해당 데이터를 사용하는 보고서나 응용 프로그램은 모두 손상됩니다. 프로덕션 데이터베이스를 처리하는 방법을 개발할 때 연산자 오류나 건너뛰는 단계가 발생하지 않도록 디버깅하고 테스트한 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 또는 스크립트를 사용하는 것이 좋습니다.  
  
 자세한 내용은 [도구 및 처리 접근 방법&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_proc"></a> 개체 처리  
 처리는 측정값 그룹, 파티션, 차원, 큐브, 마이닝 모델, 마이닝 구조 및 데이터베이스와 같은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 영향을 줍니다. 개체에 하나 이상의 개체가 포함된 경우 최상위 수준의 개체를 처리하면 하위 수준의 모든 개체도 처리됩니다. 예를 들어 큐브는 일반적으로 하나 이상의 측정값 그룹과 차원을 포함하며 각 측정값 그룹에는 파티션이 하나 이상 포함되어 있습니다. 큐브를 처리하면 큐브 내의 모든 측정값 그룹 및 현재 처리되지 않은 상태에 있는 모든 차원이 처리됩니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 처리에 대한 자세한 내용은 [Analysis Services 개체 처리](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)를 참조하세요.  
  
 처리 작업이 진행되는 동안에는 영향을 받는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 쿼리를 위해 액세스할 수 있습니다. 처리 작업은 트랜잭션 내부에서 수행되며 트랜잭션은 커밋하거나 롤백할 수 있습니다. 처리 작업이 실패하면 트랜잭션이 롤백됩니다. 처리 작업이 성공하면 변경 내용이 커밋될 때 해당 개체에 배타 잠금이 설정되므로 쿼리 또는 처리를 위해 해당 개체를 일시적으로 사용할 수 없습니다. 트랜잭션의 커밋 단계를 수행하는 동안에도 개체에 쿼리를 보낼 수 있지만 이러한 쿼리는 커밋이 완료될 때까지 지연됩니다.  
  
 처리 작업을 수행하는 동안 개체의 처리 여부 및 개체가 처리되는 방법은 해당 개체에 대해 설정된 처리 옵션에 따라 달라집니다. 각 개체에 적용할 수 있는 특정 처리 옵션에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_reproc"></a> Reprocessing Objects  
 처리되지 않은 요소가 포함된 큐브를 찾아보려면 먼저 다시 처리해야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 큐브에는 측정값 그룹 및 파티션이 포함되어 있으며 이들을 처리해야만 큐브를 쿼리할 수 있습니다. 차원이 처리되지 않은 상태에 있을 경우 큐브를 처리하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 큐브의 구성 차원을 처리합니다. 개체를 처음 처리한 다음에는 다음과 같은 상황 중 하나가 발생할 때마다 개체를 부분 또는 전체적으로 다시 처리해야 합니다.  
  
-   팩트 테이블의 열 삭제 등을 통해 개체 구조가 변경된 경우  
  
-   개체에 대한 집계 디자인이 변경된 경우  
  
-   개체의 데이터를 업데이트해야 하는 경우  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 개체를 처리할 때는 처리 옵션을 선택하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 적절한 처리 유형을 결정하도록 할 수 있습니다. 사용 가능한 처리 방법은 개체에 따라 달라지며 개체 유형을 기반으로 합니다. 또한 사용 가능한 방법은 개체를 마지막으로 처리한 후 적용된 개체 변경 내용을 기반으로 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 자동으로 처리 방법을 선택하도록 하면 최단 시간 내에 개체를 전체 처리된 상태로 반환하는 방법이 사용됩니다. 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [논리적 아키텍처&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
