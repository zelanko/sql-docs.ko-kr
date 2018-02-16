---
title: "차원 및 파티션에 대 한 문자열 저장소 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 987f6cfc-da82-4b2e-96ef-a8af88339e5f
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c10be134f541434543c43c186181b122188a379f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="configure-string-storage-for-dimensions-and-partitions"></a>차원 및 파티션에 대한 문자열 저장소 구성
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
문자열 저장소에 대한 4GB 파일 크기 제한을 초과하는 차원 특성 또는 파티션의 매우 큰 문자열을 수용할 수 있도록 문자열 저장소를 다시 구성할 수 있습니다. 차원 또는 파티션이 이 크기의 문자열 저장소를 포함하는 경우, 연결된(로컬 또는 원격) 개체는 물론 로컬 개체에 대해 차원 또는 파티션 수준에서 **StringStoresCompatibilityLevel** 속성을 변경하여 파일 크기 제한을 해결할 수 있습니다.  
  
 추가 용량을 필요로 하는 개체에 대해서만 문자열 저장소를 늘릴 수 있습니다. 대부분의 다차원 모델에서 문자열 데이터는 차원과 연결됩니다. 하지만 문자열의 맨 위에 고유 카운트 측정값이 들어 있는 파티션도 이 설정의 혜택을 받을 수 있습니다. 이 설정은 문자열용이므로 숫자 데이터는 영향을 받지 않습니다.  
  
 이 속성에 유효한 값은 다음과 같습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**1050**|저장소당 최대 파일 크기가 4GB인 기본 문자열 저장소 아키텍처를 지정합니다.|  
|**1100**|저장소당 최대 40억 개의 고유 문자열을 지원하는 더 큰 문자열 저장소를 지정합니다.|  
  
> [!IMPORTANT]  
>  개체의 문자열 저장소 설정을 변경하면 개체 자체 및 모든 종속 개체를 다시 처리해야 합니다. 이 절차를 완료하려면 처리가 필요합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [문자열 저장소 정보](#bkmk_background)  
  
-   [필수 구성 요소](#bkmk_prereq)  
  
-   [1단계: SQL Server Data Tools에서 StringStoreCompatiblityLevel 속성 설정](#bkmk_step1)  
  
-   [2단계: 개체 처리](#bkmk_step2)  
  
##  <a name="bkmk_background"></a> 문자열 저장소 정보  
 문자열 저장소 구성은 선택 사항이므로 새 데이터베이스를 만들 때에도 최대 파일 크기가 4GB인 기본 문자열 저장소 아키텍처를 사용합니다. 더 큰 문자열 저장소 아키텍처를 사용하면 성능에 작지만 눈에 띄는 영향을 줍니다. 따라서 문자열 저장소 파일이 최대 4GB 제한에 근접했거나 도달한 경우에만 이 아키텍처를 사용해야 합니다.  
  
> [!NOTE]  
>  이 설정은 데이터 마이닝 모델에 적용되지 않습니다. 현재까지는 데이터 마이닝 구조를 포함하는 모델에서 GB 파일 크기 제한이 발생할 수 있습니다.  
  
 Analysis Services 다차원 데이터베이스에서는 데이터의 특성에 따른 최적화를 허용하기 위해 문자열이 숫자 데이터와 별도로 저장됩니다. 일반적으로 문자열 데이터는 이름이나 설명을 나타내는 차원 특성에 있습니다. 고유 카운트 측정값에도 문자열 데이터가 있을 수 있습니다. 문자열 데이터는 키에서도 사용할 수 있습니다.  
  
 파일 확장명(예: .asstore, .bstore, .ksstore 또는 .string 파일)으로 문자열 저장소를 식별할 수 있습니다. 기본적으로 이러한 각 파일에는 최대 4GB 제한이 적용됩니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서는 필요에 따라 문자열 저장소가 커질 수 있도록 하는 대체 저장소 메커니즘을 지정하여 최대 파일 크기를 무시할 수 있습니다.  
  
 실제 파일의 크기를 제한하는 기본 문자열 저장소 아키텍처와 달리, 더 큰 문자열 저장소는 최대 문자열 수를 기반으로 합니다. 더 큰 문자열 저장소의 최대 제한은 40억 개의 고유 문자열 또는 40억 개의 레코드 중 먼저 발생하는 것입니다. 더 큰 문자열 저장소는 짝수 크기의 레코드를 만들며 각 레코드는 64K페이지입니다. 단일 레코드에 맞지 않는 매우 긴 문자열이 있는 경우 효과적인 제한은 40억 개의 문자열 미만입니다.  
  
##  <a name="bkmk_prereq"></a> 필수 구성 요소  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]가 있어야 합니다.  
  
 차원 및 파티션은 MOLAP 저장소를 사용해야 합니다.  
  
 데이터베이스 호환성 수준이 1100으로 설정되어야 합니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 사용하여 데이터베이스를 만들거나 배포하는 경우 데이터베이스 호환성 수준은 이미 1100으로 설정되어 있습니다. 이전 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 만든 데이터베이스를 ssSQL11 이상으로 이동한 경우 호환성 수준을 업데이트해야 합니다. 이동은 하지만 다시 배포하지 않으려는 데이터베이스의 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 호환성 수준을 설정할 수 있습니다. 자세한 내용은 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)을 참조하십시오.  
  
##  <a name="bkmk_step1"></a> 1단계: SQL Server Data Tools에서 StringStoreCompatiblityLevel 속성 설정  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 수정할 차원 또는 파티션이 포함된 프로젝트를 엽니다.  
  
2.  차원에 대한 문자열 저장소를 변경하려면 솔루션 탐색기를 엽니다. 문자열 저장소를 수정할 차원을 두 번 클릭합니다.  
  
3.  차원 디자이너의 특성 창에서 차원의 부모 노드가 선택되어 있는지 확인합니다. 예를 들어, 차원이 Customers이면 자식 특성 중 하나가 아니라 Customers를 선택합니다.  
  
4.  속성 창의 고급 섹션에서 **StringStoresCompatibilityLevel** 을 **1100**으로 설정합니다. 더 큰 저장소가 필요한 다른 차원에 대해 반복하거나 나머지 차원 값을 **1050** 으로 그대로 둡니다.  
  
5.  솔루션 탐색기에서 파티션에 대한 큐브를 엽니다.  
  
6.  파티션 탭을 클릭합니다.  
  
7.  파티션을 확장하고 추가 저장소 용량이 필요한 파티션을 선택한 다음 **StringStoresCompatibilityLevel** 속성을 수정합니다.  
  
8.  파일을 저장합니다.  
  
##  <a name="bkmk_step2"></a> 2단계: 개체 처리  
 새 저장소 아키텍처는 개체를 처리한 후 사용됩니다. 개체를 처리하면 이전에 문자열 저장소 오버플로 조건을 보고한 오류가 더 이상 발생하지 않으므로 저장소 제한 문제를 성공적으로 해결한 것도 증명됩니다.  
  
-   솔루션 탐색기에서 수정한 차원을 마우스 오른쪽 단추로 클릭하고 **처리**를 선택합니다.  
  
 새 문자열 저장소 아키텍처를 사용하는 각 개체에 대해 전체 처리 옵션을 사용해야 합니다. 처리하기 전에 차원에 대한 영향 분석을 실행하여 종속 개체에도 재처리가 필요한지 여부를 확인해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [도구 및 처리 접근 방법&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)   
 [처리 옵션 및 설정 &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [파티션 저장소 모드 및 처리](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)   
 [차원 저장소](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)  
  
  
