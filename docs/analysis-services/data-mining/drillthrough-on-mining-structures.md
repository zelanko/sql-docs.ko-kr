---
title: "마이닝 구조에서 드릴스루 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: db582bae24d9bfb18cbb9f7b7febf6a1e4da45fb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drillthrough-on-mining-structures"></a>마이닝 구조에서의 드릴스루
  *드릴스루* 는 마이닝 모델이나 마이닝 구조를 쿼리하고 모델에 노출되지 않는 세부 데이터를 가져오는 기능입니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 사례 데이터로 드릴스루하는 두 가지 옵션을 제공합니다. 마이닝 모델을 작성하는 데 사용된 데이터로 드릴스루하거나 마이닝 구조의 원본 데이터로 드릴스루할 수 있습니다.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>모델 사례로 드릴스루 및 구조로 드릴스루  
 **모델 사례** 로 드릴스루하는 기능은 모델의 규칙, 패턴 또는 클러스터에 대한 추가 세부 정보를 찾으려는 경우에 유용합니다.  
  
 반면 **구조 데이터로 드릴스루** 하는 기능은 모델에서 사용할 수 없었던 정보에 액세스하기 위한 것입니다. 예를 들어 적절한 사용 권한이 있는 경우 모델 학습 및 테스트에 사용된 데이터 행을 찾을 수 있습니다.  
  
 분석에 사용되지 않은 데이터가 구조 정의에 포함되어 있는 경우 해당 데이터의 특성을 볼 수도 있습니다. 예를 들어 마이닝 구조는 대개 여러 종류의 모델을 지원하지만, 데이터 형식이 호환되지 않거나 데이터가 분석에 유용하지 않아서 일부 구조 열이 모델에서 제외되는 경우도 있습니다. 예를 들어 고객 연락처 정보가 구조에 포함되었지만 클러스터링 모델에서 이 데이터를 사용하지 않을 경우, 드릴스루를 사용하면 데이터 원본에 대한 별도의 쿼리를 실행하지 않고도 이 정보에 액세스할 수 있습니다.  
  
## <a name="enabling-drillthrough-to-structure-data"></a>구조 데이터에 드릴스루 사용  
 마이닝 구조에 드릴스루를 사용하려면 다음 조건을 충족해야 합니다.  
  
-   모델에서도 드릴스루를 사용할 수 있어야 합니다. 기본적으로는 두 종류의 드릴스루가 모두 사용되지 않습니다. 데이터 마이닝 마법사에서 드릴스루를 사용하도록 설정하려면 마법사의 마지막 페이지에서 모델 사례에 대한 드릴스루를 사용하도록 설정하는 옵션을 선택합니다. 나중에 **AllowDrillthrough** 속성을 변경하여 모델에 드릴스루 기능을 추가할 수도 있습니다.  
  
-   DMX를 사용하여 마이닝 구조를 만드는 경우 WITH DRILLTHROUGH 절을 사용합니다. 자세한 내용은 [CREATE MINING STRUCTURE&#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md)를 참조하세요.  
  
-   드릴스루는 마이닝 구조를 처리할 때 캐시된 학습 사례에 대한 정보를 검색하는 방식으로 작동합니다. 따라서 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 속성을 **ClearAfterProcessing**으로 변경하여 구조를 처리한 후 캐시된 데이터를 지운 경우에는 드릴스루가 작동하지 않습니다. 구조 열로 드릴스루할 수 있도록 설정하려면 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 속성을 **KeepTrainingCases** 로 변경한 다음 구조를 다시 처리해야 합니다.  
  
-   마이닝 구조와 마이닝 모델 모두에서 [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) 속성이 **True**로 설정되어 있는지 확인합니다. 또한 사용자가 구조와 모델 모두에 대한 드릴스루 권한이 있는 역할의 멤버여야 합니다.  
  
## <a name="security-issues-for-drillthrough"></a>드릴스루의 보안 문제  
 드릴스루 권한은 구조와 모델에 개별적으로 설정됩니다. 모델 사용 권한이 있으면 구조에 대한 사용 권한이 없는 경우에도 모델에서 드릴스루할 수 있습니다. 구조에 대한 드릴스루 권한이 있으면 추가적으로 [StructureColumn&#40;DMX&#41;](../../dmx/structurecolumn-dmx.md) 함수를 사용하여 모델에서 드릴스루 쿼리에 구조 열을 포함할 수도 있습니다.  
  
 Analysis Services에서 역할을 만들고 권한을 할당하는 방법에 대한 자세한 내용은 [역할 디자이너&#40;Analysis Services - 다차원 데이터&#41;](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192)를 참조하세요.  
  
> [!NOTE]  
>  마이닝 구조와 마이닝 모델 모두에서 드릴스루를 사용할 수 있도록 설정하면 마이닝 모델에 대한 드릴스루 권한이 있는 역할의 멤버인 모든 사용자는 마이닝 모델에 마이닝 구조의 열이 포함되지 않은 경우에도 해당 열을 볼 수 있습니다. 따라서 중요한 데이터를 보호하려면 개인 정보를 마스킹하도록 데이터 원본 뷰를 설정하고 필요한 경우에만 마이닝 구조에 드릴스루 액세스를 허용해야 합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 마이닝 모델에 드릴스루를 사용하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
|||  
|-|-|  
|마이닝 모델 뷰어에서 구조로의 드릴스루 사용|[모델 뷰어에서 드릴스루 사용](../../analysis-services/data-mining/use-drillthrough-from-the-model-viewers.md)|  
|특정 모델 유형에 대한 드릴스루 쿼리의 예 참조|[데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)|  
|특정 마이닝 구조 및 마이닝 모델에 적용되는 사용 권한에 대한 정보 보기|[데이터 마이닝 구조 및 모델에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델에서의 드릴스루](../../analysis-services/data-mining/drillthrough-on-mining-models.md)  
  
  
