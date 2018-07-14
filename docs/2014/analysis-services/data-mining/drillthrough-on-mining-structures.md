---
title: 마이닝 구조에서 드릴스루 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4e01f903d28368179a7c249f3a8bbb7ac7c159e8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246105"
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
  
-   모델에서도 드릴스루를 사용할 수 있어야 합니다. 기본적으로는 두 종류의 드릴스루가 모두 사용되지 않습니다. 데이터 마이닝 마법사에서 드릴스루를 사용하도록 설정하려면 마법사의 마지막 페이지에서 모델 사례에 대한 드릴스루를 사용하도록 설정하는 옵션을 선택합니다. 또한 나중 추가할 수 있습니다 기능이 모델에 드릴스루를 변경 하 여는 `AllowDrillthrough` 속성입니다.  
  
-   DMX를 사용하여 마이닝 구조를 만드는 경우 WITH DRILLTHROUGH 절을 사용합니다. 자세한 내용은 [CREATE MINING STRUCTURE&#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)를 참조하세요.  
  
-   드릴스루는 마이닝 구조를 처리할 때 캐시된 학습 사례에 대한 정보를 검색하는 방식으로 작동합니다. 따라서 변경 하 여 구조를 처리 한 후 캐시 된 데이터를 지운 경우 합니다 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 속성을 `ClearAfterProcessing`, 드릴스루가 작동 하지 것입니다. 구조 열으로 드릴스루를 사용 하려면 변경 해야 합니다 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 속성을 `KeepTrainingCases` 다음 구조를 다시 처리 하 고 있습니다.  
  
-   마이닝 구조와 마이닝 모델 모두 있는지 확인 합니다 [AllowDrillThrough](../scripting/properties/allowdrillthrough-element-assl.md) 속성으로 설정 `True`합니다. 또한 사용자가 구조와 모델 모두에 대한 드릴스루 권한이 있는 역할의 멤버여야 합니다.  
  
## <a name="security-issues-for-drillthrough"></a>드릴스루의 보안 문제  
 드릴스루 권한은 구조와 모델에 개별적으로 설정됩니다. 모델 사용 권한이 있으면 구조에 대한 사용 권한이 없는 경우에도 모델에서 드릴스루할 수 있습니다. 구조에 대한 드릴스루 권한이 있으면 추가적으로 [StructureColumn&#40;DMX&#41;](/sql/dmx/structurecolumn-dmx) 함수를 사용하여 모델에서 드릴스루 쿼리에 구조 열을 포함할 수도 있습니다.  
  
 Analysis Services에서 역할을 만들고 권한을 할당하는 방법에 대한 자세한 내용은 [역할 디자이너&#40;Analysis Services - 다차원 데이터&#41;](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx)를 참조하세요.  
  
> [!NOTE]  
>  마이닝 구조와 마이닝 모델 모두에서 드릴스루를 사용할 수 있도록 설정하면 마이닝 모델에 대한 드릴스루 권한이 있는 역할의 멤버인 모든 사용자는 마이닝 모델에 마이닝 구조의 열이 포함되지 않은 경우에도 해당 열을 볼 수 있습니다. 따라서 중요한 데이터를 보호하려면 개인 정보를 마스킹하도록 데이터 원본 뷰를 설정하고 필요한 경우에만 마이닝 구조에 드릴스루 액세스를 허용해야 합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 마이닝 모델에 드릴스루를 사용하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
|||  
|-|-|  
|마이닝 모델 뷰어에서 구조로의 드릴스루 사용|[모델 뷰어에서 드릴스루 사용](use-drillthrough-from-the-model-viewers.md)|  
|특정 모델 유형에 대한 드릴스루 쿼리의 예 참조|[데이터 마이닝 쿼리](data-mining-queries.md)|  
|특정 마이닝 구조 및 마이닝 모델에 적용되는 사용 권한에 대한 정보 보기|[데이터 마이닝 구조 및 모델에 대 한 권한 부여 &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델에 대한 드릴스루](drillthrough-on-mining-models.md)  
  
  
