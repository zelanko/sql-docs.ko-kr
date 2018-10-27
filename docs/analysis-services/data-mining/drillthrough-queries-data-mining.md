---
title: 드릴스루 쿼리 (데이터 마이닝) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f85c297c7ae8786d5cd387a2f25a81f507425dda
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148018"
---
# <a name="drillthrough-queries-data-mining"></a>드릴스루 쿼리(데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  *드릴스루 쿼리* 를 사용하면 마이닝 모델로 쿼리를 전송하여 기본 사례 또는 구조 데이터에서 세부 사항을 검색할 수 있습니다. 드릴스루는 모델 학습에 사용된 사례와 모델 테스트에 사용된 사례를 비교해서 보거나 사례 데이터에서 추가 정보를 확인하려는 경우에 유용합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 마이닝은 다음과 같은 두 가지 드릴스루 옵션을 제공합니다.  
  
-   **모델 사례**로 드릴스루  
  
     모델 사례로의 드릴스루는 의사 결정 트리의 분기 또는 클러스터와 같은 모델의 특정 패턴에서 이동하여 개별 사례에 대한 자세한 정보를 보려는 경우에 사용됩니다.  
  
-   **구조 사례**로 드릴스루  
  
     구조 사례로의 드릴스루는 구조에 모델에서 사용할 수 없는 정보가 포함된 경우에 사용됩니다. 예를 들어 고객 연락처 정보가 구조에 포함되어 있더라도 클러스터링 모델에 해당 데이터는 사용하지 않을 것입니다. 그러나 모델을 작성한 후 특정 클러스터로 그룹화된 고객에 대한 연락처 정보를 검색할 수 있습니다.  
  
 이 섹션에서는 이러한 쿼리를 만드는 방법에 대한 예를 제공합니다.  
  
 [데이터 마이닝 디자이너에서 드릴스루 사용](#bkmk_Designer)  
  
 [DMX를 사용하여 드릴스루 쿼리 만들기](#bkmk_DMX)  
  
 [드릴스루 사용 시의 고려 사항](#bkmk_Considerations)  
  
-   [보안 문제](#bkmk_Security)  
  
-   [제한 사항](#bkmk_Limits)  
  
##  <a name="bkmk_Designer"></a> 데이터 마이닝 디자이너에서 드릴스루 사용  
 드릴스루를 허용하도록 마이닝 모델을 구성했으며 적절한 사용 권한이 있는 경우 모델을 찾을 때 적절한 뷰어에서 노드를 클릭하고 해당 특정 노드의 사례에 대한 세부 정보를 검색할 수 있습니다.  
  
 [마이닝 모델에서 사례 데이터로 드릴스루](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md).  
  
 마이닝 구조를 처리할 때 학습 사례를 캐시했으며 필요한 사용 권한이 있는 경우 마이닝 모델에 포함되지 않은 열을 비롯하여 모델 사례 및 마이닝 구조의 정보를 반환할 수 있습니다.  
  
##  <a name="bkmk_DMX"></a> DMX를 사용하여 드릴스루 쿼리 만들기  
 모델 또는 구조에 대한 사용 권한을 가지고 있는 경우 DMX 쿼리를 만들어 사례 데이터로 드릴스루할 수 있습니다. DMX에서 드릴스루 쿼리를 만들기 위한 구문의 예를 보려면 다음 항목을 참조하십시오.  
  
 [DMX를 사용하여 드릴스루 쿼리 만들기](../../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)  
  
##  <a name="bkmk_Considerations"></a> 드릴스루 사용 시의 고려 사항  
  
-   데이터 마이닝 마법사를 사용하는 경우 모델 사례로 드릴스루할 수 있도록 설정하는 옵션은 마법사의 마지막 페이지에 있습니다. 드릴스루는 기본적으로 해제되어 있습니다. 자세한 내용은 [마법사 완료&#40;데이터 마이닝 마법사&#41;](http://msdn.microsoft.com/library/6aef1548-35eb-42fd-ae87-63650a79eda1)를 참조하세요.  
  
-   기존 마이닝 모델에 드릴스루 기능을 추가할 수 있지만 이렇게 하면 모델을 다시 처리해야 데이터로 드릴스루할 수 있습니다.  
  
-   드릴스루는 마이닝 구조를 처리할 때 캐시된 학습 사례에 대한 정보를 검색하는 방식으로 작동합니다. 따라서 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 속성을 **ClearAfterProcessing**으로 변경하여 구조를 처리한 후 캐시된 데이터를 지운 경우에는 드릴스루가 작동하지 않습니다. 구조 열로 드릴스루할 수 있도록 설정하려면 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 속성을 **KeepTrainingCases** 로 변경한 다음 구조를 다시 처리해야 합니다.  
  
-   드릴스루가 마이닝 구조에서는 허용되지 않지만 마이닝 모델에서는 허용되는 경우 마이닝 구조가 아닌 모델 사례에서만 정보를 볼 수 있습니다.  
  
###  <a name="bkmk_Security"></a> 드릴스루의 보안 문제  
 모델의 구조 사례로 드릴스루하려는 경우 마이닝 구조와 마이닝 모델 모두에서 [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) 속성이 **True**로 설정되어 있는지 확인해야 합니다. 또한 사용자가 구조와 모델 모두에 대한 드릴스루 권한이 있는 역할의 멤버여야 합니다. 역할을 만드는 방법에 대한 자세한 내용은 [역할 디자이너&#40;Analysis Services - 다차원 데이터&#41;](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192)를 참조하세요. 다음을 참조하십시오.  
  
 드릴스루 권한은 구조와 모델에 개별적으로 설정됩니다. 모델 사용 권한이 있으면 구조에 대한 사용 권한이 없는 경우에도 모델에서 드릴스루할 수 있습니다. 구조에 대한 드릴스루 권한이 있으면 추가적으로 [StructureColumn&#40;DMX&#41;](../../dmx/structurecolumn-dmx.md) 함수를 사용하여 모델에서 드릴스루 쿼리에 구조 열을 포함할 수도 있습니다.  
  
> [!NOTE]  
>  마이닝 구조와 마이닝 모델 모두에서 드릴스루를 사용할 수 있도록 설정하면 마이닝 모델에 대한 드릴스루 권한이 있는 역할의 멤버인 모든 사용자는 마이닝 모델에 마이닝 구조의 열이 포함되지 않은 경우에도 해당 열을 볼 수 있습니다. 따라서 중요한 데이터를 보호하려면 개인 정보를 마스킹하도록 데이터 원본 뷰를 설정하고 필요한 경우에만 마이닝 구조에 드릴스루 액세스를 허용해야 합니다.  
  
###  <a name="bkmk_Limits"></a> 드릴스루의 제한 사항  
  
-   모델을 만드는 데 사용된 알고리즘에 따라 모델의 드릴스루 작업에 다음 제한 사항이 적용됩니다.  
  
|알고리즘 이름|문제점|  
|--------------------|-----------|  
|Microsoft Naïve Bayes 알고리즘|지원되지 않습니다. 이러한 알고리즘은 콘텐츠의 특정 노드에 사례를 할당하지 않습니다.|  
|Microsoft 신경망 알고리즘|지원되지 않습니다. 이러한 알고리즘은 콘텐츠의 특정 노드에 사례를 할당하지 않습니다.|  
|Microsoft 로지스틱 회귀 알고리즘|지원되지 않습니다. 이러한 알고리즘은 콘텐츠의 특정 노드에 사례를 할당하지 않습니다.|  
|Microsoft 선형 회귀 알고리즘|지원됩니다. 그러나 모델은 단일 노드인 **All**을 만들기 때문에 드릴스루 시 모델에 대한 모든 학습 사례가 반환됩니다. 학습 집합이 큰 경우 결과를 로드하는 데 시간이 많이 소요될 수 있습니다.|  
|Microsoft 시계열 알고리즘|지원됩니다. 그러나 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 를 사용하여 구조 또는 사례 데이터로 드릴스루할 수 없습니다. 대신 DMX 쿼리를 만들어야 합니다.<br /><br /> 특정 노드로 드릴스루하거나 DMX 쿼리를 작성하여 시계열 모델의 특정 노드에 있는 사례를 검색할 수도 없습니다. 날짜 또는 특성 값과 같은 다른 기준을 사용하여 모델이나 구조에서 사례 데이터를 검색할 수 있습니다.<br /><br /> [Lag&#40;DMX&#41;](../../dmx/lag-dmx.md) 함수를 사용하여 모델의 사례에서 날짜를 반환할 수도 있습니다.<br /><br /> Microsoft 시계열 알고리즘에 의해 생성된 ARTXP 및 ARIMA 노드에 대한 세부 정보를 보려면 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)를 사용합니다.|  
  
##  <a name="bkmk_Tasks"></a> 관련 태스크  
 특정 시나리오에서 드릴스루를 사용하려면 다음 링크를 사용하십시오.  
  
|태스크|링크|  
|----------|----------|  
|데이터 마이닝 디자이너의 드릴스루 사용을 설명하는 절차|[마이닝 모델에서 사례 데이터로 드릴스루](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)|  
|드릴스루를 허용하도록 기존 마이닝 모델 변경|[마이닝 모델에 드릴스루 사용](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)|  
|DMX WITH DRILLTHROUGH 절을 사용하여 마이닝 구조에서 드릴스루를 사용하도록 설정|[CREATE MINING STRUCTURE&#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md)|  
|마이닝 구조 및 마이닝 모델에 대한 드릴스루에 적용되는 권한 할당에 대한 정보|[데이터 마이닝 구조 및 모델에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 모델 뷰어](../../analysis-services/data-mining/data-mining-model-viewers.md)   
 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
