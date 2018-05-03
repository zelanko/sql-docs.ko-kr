---
title: 마이닝 모델 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- mining models [Analysis Services]
- logical architecture [Analysis Services Multidimensional Data]
- properties [Analysis Services]
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: cd4df273-0c6a-4b3e-9572-8a7e313111e8
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 74ce9756752ca98057c0a4a1c75544063c1d392b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mining-models-analysis-services---data-mining"></a>마이닝 모델(Analysis Services - 데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  *마이닝 모델* 은 데이터에 알고리즘을 적용하여 만들지만 단순한 알고리즘 또는 메타데이터 컨테이너가 아니며, 새로운 데이터에 적용하여 예측을 생성하고 관계를 추론할 수 있는 데이터, 통계 및 패턴의 집합입니다.  
  
 이 섹션에서는 데이터 마이닝 모델의 정의와 용도에 대해 설명합니다. 즉, 모델 및 구조의 기본 아키텍처, 마이닝 모델의 속성, 마이닝 모델을 만들고 사용하는 방법에 대해 설명합니다.  
  
 [마이닝 모델 아키텍처](#bkmk_mdlArch)  
  
 [데이터 마이닝 모델 정의](#bkmk_mdlDefine)  
  
 [마이닝 모델 속성](#bkmk_mdlProps)  
  
 [마이닝 모델 열](#bkmk_mdlCols)  
  
 [마이닝 모델 처리](#bkmk_mdlProcess)  
  
 [마이닝 모델 보기 및 쿼리](#bkmk_mdlView)  
  
##  <a name="bkmk_mdlArch"></a> 마이닝 모델 아키텍처  
 데이터 마이닝 모델은 마이닝 구조에서 데이터를 가져온 다음 데이터 마이닝 알고리즘을 사용하여 해당 데이터를 분석합니다. 마이닝 구조와 마이닝 모델은 별개의 개체입니다. 마이닝 구조에는 데이터 원본을 정의하는 정보가 저장되고, 마이닝 모델에는 분석 결과로 발견된 패턴과 같이 데이터의 통계적 처리에서 파생된 정보가 저장됩니다.  
  
 마이닝 모델은 마이닝 구조에서 제공한 데이터가 처리 및 분석되기 전까지 비어 있습니다. 마이닝 모델이 처리된 후에는 메타데이터, 결과 및 마이닝 구조에 대한 바인딩으로 채워집니다.  
  
 ![모델 메타 데이터, 패턴 및 바인딩이 포함](../../analysis-services/data-mining/media/dmcon-modelarch2.gif "모델 메타 데이터, 패턴 및 바인딩이 포함")  
  
 메타데이터는 모델의 이름과 해당 모델이 저장된 서버뿐 아니라 모델을 만드는 데 사용된 마이닝 구조의 열을 비롯한 모델 정의, 모델을 처리할 때 적용된 필터 정의 및 데이터를 분석하는 데 사용된 알고리즘도 지정합니다. 데이터 열, 데이터 유형, 필터, 알고리즘 등 모든 선택 항목은 분석 결과에 상당한 영향을 줍니다.  
  
 예를 들어 클러스터링 알고리즘, 의사 결정 트리 알고리즘 및 Naïve Bayes 알고리즘을 사용하여 동일한 데이터로 여러 모델을 만들 수 있습니다. 각 모델 유형은 예측을 만드는 데 사용할 수 있는 서로 다른 패턴, 항목 집합, 규칙 또는 수식 집합을 만듭니다. 일반적으로 각 알고리즘은 데이터를 다양한 방법으로 분석하므로 결과 모델의 *콘텐츠* 도 다른 구조로 구성됩니다. 한 모델 유형에서는 데이터와 패턴이 *클러스터*로 그룹화되고, 다른 모델 유형에서는 데이터가 트리, 분기, 트리와 분기를 분류하고 정의하는 규칙으로 구성될 수 있습니다.  
  
 또한 모델은 모델 학습에 사용된 데이터의 영향을 받습니다. 따라서 분석 중에 데이터를 다르게 필터링하거나 다른 초기값을 사용하면 모델이 동일한 마이닝 구조에 대해 학습된 경우에도 다른 결과가 나타날 수 있습니다. 하지만 실제 데이터는 모델에 저장되지 않고 마이닝 구조에 그대로 있는 상태로 요약 통계만 저장됩니다. 모델을 학습할 때 데이터에 대한 필터를 만든 경우 필터 정의도 모델 개체와 함께 저장됩니다.  
  
 모델은 마이닝 구조에 캐시된 데이터를 다시 가리키는 바인딩 집합을 포함합니다. 데이터가 구조에 캐시되었고 처리 후 아직 지워지지 않은 경우 이러한 바인딩을 통해 결과에서 해당 결과를 지원하는 사례로 드릴스루할 수 있습니다. 그러나 실제 데이터는 모델이 아니라 구조 캐시에 저장됩니다.  
  
 [마이닝 모델 아키텍처](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlDefine"></a> 데이터 마이닝 모델 정의  
 데이터 마이닝 모델을 만드는 일반적인 단계는 다음과 같습니다.  
  
-   기본 마이닝 구조를 만들고 필요한 데이터 열을 포함시킵니다.  
  
-   분석 태스크에 가장 적합한 알고리즘을 선택합니다.  
  
-   구조에서 모델에 사용할 열을 선택하고 열을 사용하는 방법(예측할 결과를 포함하는 열, 입력 전용 열, 등)을 지정합니다.  
  
-   필요에 따라 매개 변수를 설정하여 알고리즘에 의한 처리를 세부 조정합니다.  
  
-   구조 및 모델을 *처리* 하여 모델에 데이터를 채웁니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 마이닝 모델을 관리하는 데 유용한 다음과 같은 도구를 제공합니다.  
  
-   데이터 마이닝 마법사 - 구조와 관련 마이닝 모델을 만들 수 있습니다. 이 도구를 사용하는 것이 가장 쉬운 방법입니다. 이 마법사를 사용하면 필요한 마이닝 구조가 자동으로 만들어지며 중요한 설정을 구성하는 데 도움이 됩니다.  
  
-   DMX CREATE MODEL 문 - 모델을 정의하는 데 사용할 수 있습니다. 필요한 구조가 처리 과정에서 자동으로 만들어지므로 이 방법을 사용할 경우에는 기존 구조를 다시 사용할 수 없습니다. 만들려는 모델을 이미 정확히 알고 있거나 모델을 스크립팅하려는 경우에 이 방법을 사용합니다.  
  
-   DMX ALTER STRUCTURE ADD MODEL 문 - 기존 구조에 새 마이닝 모델을 추가하는 데 사용할 수 있습니다. 동일한 데이터 집합을 기반으로 하는 다양한 모델을 시험하려면 이 방법을 사용합니다.  
  
 AMO 또는 XML/A를 사용하거나 Excel용 데이터 마이닝 클라이언트 등의 다른 클라이언트를 사용하여 프로그래밍 방식으로 마이닝 모델을 만들 수도 있습니다. 자세한 내용은 다음 항목을 참조하세요.  
  
 [마이닝 모델 아키텍처](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlProps"></a> 마이닝 모델 속성  
 각 마이닝 모델에는 모델 및 해당 메타데이터를 정의하는 속성이 있습니다. 이러한 속성으로는 이름, 설명, 모델이 마지막으로 처리된 날짜, 모델에 대한 사용 권한, 학습에 사용되는 데이터에 대한 필터 등이 있습니다.  
  
 각 마이닝 모델에는 마이닝 구조에서 파생되었으며 해당 모델에서 사용하는 데이터의 열을 설명하는 속성도 있습니다. 모델에 사용된 열이 중첩 테이블인 경우 열에도 별도의 필터가 적용될 수 있습니다.  
  
 또한 각 마이닝 모델에는 <xref:Microsoft.AnalysisServices.MiningModel.Algorithm%2A> 및 <xref:Microsoft.AnalysisServices.MiningModelColumn.Usage%2A>라는 두 특수 속성이 있습니다.  
  
-   **Algorithm 속성** 모델을 만드는 데 사용되는 알고리즘을 지정합니다. 사용 가능한 알고리즘은 사용 중인 공급자에 따라 달라집니다. 와 함께 제공 되는 알고리즘 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 참조 [Data Mining Algorithms &#40;Analysis Services-데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)합니다. **Algorithm** 속성은 마이닝 모델에 적용되며 각 모델에 대해 한 번만 설정할 수 있습니다. 나중에 알고리즘을 변경할 수 있지만 마이닝 모델의 일부 열은 선택하는 알고리즘에서 지원하지 않는 경우 사용할 수 없게 될 수 있습니다. 이 속성을 변경한 후 모델을 항상 다시 처리해야 합니다.  
  
-   **Usage 속성** 모델에서 각 열이 사용되는 방법을 정의합니다. 열 사용을 **Input**, **Predict**, **Predict Only**또는 **Key**로 정의할 수 있습니다. **Usage** 속성은 개별 마이닝 모델 열에 적용되고 모델에 포함되어 있는 각 열에 대해 개별적으로 설정되어야 합니다. 구조에 모델에서 사용하지 않는 열이 포함되어 있는 경우 사용이 **Ignore**로 설정됩니다. 마이닝 구조에 포함되지만 분석에 사용되지 않는 데이터의 예로는 고객 이름, 전자 메일 주소 등이 있습니다. 이렇게 하면 분석 단계에서 데이터를 포함시키지 않고 나중에 해당 데이터를 쿼리할 수 있습니다.  
  
 마이닝 모델을 만든 후 마이닝 모델 속성의 값을 변경할 수 있습니다. 그러나 마이닝 모델의 이름을 포함하여 어떤 속성이든 변경할 경우에는 해당 모델을 다시 처리해야 합니다. 모델을 다시 처리한 후에는 다른 결과가 표시될 수 있습니다.  
  
 [마이닝 모델 아키텍처](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlCols"></a> 마이닝 모델 열  
 마이닝 모델은 마이닝 구조에 정의된 열에서 가져온 데이터 열을 포함합니다. 마이닝 구조에서 모델에 사용할 열을 선택할 수 있을 뿐 아니라, 마이닝 구조 열의 복사본을 만든 다음 해당 이름을 바꾸거나 사용법을 변경할 수 있습니다. 모델 작성 프로세스 중에 모델별 열 사용법도 정의해야 합니다. 여기에는 열이 키인지 여부, 열이 예측에 사용되는지 여부, 알고리즘에서 열을 무시할 수 있는지 여부 등과 같은 정보가 포함됩니다.  
  
 모델을 작성하는 동안 사용할 수 있는 모든 데이터 열을 자동으로 추가하는 것보다는 구조 내의 데이터를 신중히 검토하여 분석에 유용한 열만 모델에 포함되도록 하는 것이 좋습니다. 예를 들어 동일한 데이터를 반복하는 여러 열을 포함하지 말고 대부분 고유한 값을 갖는 열을 사용하지 않도록 합니다. 특정 열이 사용하기에 적합하지 않다고 생각되는 경우 해당 열을 마이닝 구조나 마이닝 모델에서 삭제할 필요는 없고, 대신 모델을 만들 때 열을 무시하도록 지정하는 플래그를 해당 열에 설정하면 됩니다. 그러면 열이 마이닝 구조에 유지되지만 마이닝 모델에 사용되지 않습니다. 모델에서 마이닝 구조로의 드릴스루를 사용하도록 설정한 경우 나중에 열에서 정보를 검색할 수 있습니다.  
  
 선택한 알고리즘에 따라 마이닝 구조의 일부 열은 특정 모델 유형과 호환되지 않거나 적절하지 않은 결과를 제공할 수 있습니다. 예를 들어 Income 열과 같이 데이터에 연속 숫자 데이터가 포함되고 있고 모델에 개별 값이 필요할 경우 데이터를 개별 범위로 변환하거나 데이터를 모델에서 제거해야 할 수 있습니다. 일부의 경우 알고리즘에서 데이터를 자동으로 변환하거나 저장하지만 원하는 결과나 필요한 결과가 나타나지 않을 수도 있습니다. 열에 대한 추가 복사본을 만들어 다른 모델을 시도해 보십시오. 개별 열에 플래그를 설정하여 특수 처리가 필요한 위치를 나타낼 수도 있습니다. 예를 들어 데이터에 null이 포함되어 있는 경우 모델링 플래그를 사용하여 처리를 제어할 수 있습니다. 특정 열을 모델의 회귀 변수로 간주하려면 모델링 플래그를 사용할 수 있습니다.  
  
 모델을 만든 후 모델 이름 변경이나 열 추가 또는 제거 등의 변경 작업을 수행할 수 있습니다. 그러나 모델 메타데이터만 변경할 경우를 포함하여 어떤 항목이든 변경할 경우에는 해당 모델을 다시 처리해야 합니다.  
  
 [마이닝 모델 아키텍처](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlProcess"></a> 마이닝 모델 처리  
 데이터 마이닝 모델은 처리되기 전까지는 비어 있는 개체입니다. 모델을 처리하면 구조에서 캐시된 데이터가 필터(모델에 정의된 필터가 있는 경우)를 통과하고 알고리즘에 의해 분석됩니다. 이 알고리즘은 데이터를 설명하는 요약 통계 집합을 계산하고, 데이터 내의 규칙과 패턴을 파악한 다음 이를 사용하여 모델을 채웁니다.  
  
 마이닝 모델이 처리된 후 해당 마이닝 모델에는 데이터에 대한 풍부한 정보와 분석에서 얻은 패턴(통계, 규칙, 회귀 수식 등)이 포함되어 있습니다. 사용자 지정 뷰어를 사용하여 이 정보를 찾아보거나, 데이터 마이닝 쿼리를 만들어 이 정보를 검색한 다음 분석 및 프레젠테이션에 사용할 수 있습니다.  
  
 [마이닝 모델 아키텍처](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlView"></a> 마이닝 모델 보기 및 쿼리  
 모델을 처리한 후에는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 제공하는 사용자 지정 뷰어를 사용하여 모델을 탐색할 수 있습니다. For  
  
 마이닝 모델에 대한 쿼리를 작성하여 예측을 만들거나 모델 메타데이터 또는 해당 모델에서 생성된 패턴을 검색할 수도 있습니다. 쿼리를 작성하려면 DMX(Data Mining Extensions)를 사용합니다.  
  
## <a name="related-content"></a>관련 내용  
  
|항목|링크|  
|------------|-----------|  
|여러 마이닝 모델을 지원할 수 있는 마이닝 구조를 작성하는 방법에 대해 알아봅니다. 모델의 열 사용법에 대해 알아봅니다.|[마이닝 구조 열](../../analysis-services/data-mining/mining-structure-columns.md)<br /><br /> [마이닝 모델 열](../../analysis-services/data-mining/mining-model-columns.md)<br /><br /> [콘텐츠 형식 & #40; 데이터 마이닝 & #41;](../../analysis-services/data-mining/content-types-data-mining.md)|  
|선택한 알고리즘이 모델 콘텐츠에 미치는 영향과 다른 알고리즘에 대해 알아봅니다.|[마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)<br /><br /> [데이터 마이닝 알고리즘 & #40; Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)|  
|컴퍼지션과 동작에 영향을 미치는 모델에 대한 속성을 설정하는 방법에 대해 알아봅니다.|[마이닝 모델 속성](../../analysis-services/data-mining/mining-model-properties.md)<br /><br /> [모델링 플래그 & #40; 데이터 마이닝 & #41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)|  
|데이터 마이닝에 대한 프로그래밍 가능한 인터페이스에 대해 알아봅니다.|[분석 관리 개체 & #40;를 사용 하 여 개발 AMO & #41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)<br /><br /> [DMX&#40;Data Mining Extensions&#41; 참조](../../dmx/data-mining-extensions-dmx-reference.md)|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 사용자 지정 데이터 마이닝 뷰어를 사용하는 방법에 대해 알아봅니다.|[데이터 마이닝 모델 뷰어](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|데이터 마이닝 모델에 대해 사용할 수 있는 다양한 쿼리 유형의 예를 봅니다.|[데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)|  
  
## <a name="related-tasks"></a>관련 작업  
 다음 링크를 사용하여 데이터 마이닝 모델 작업에 대한 자세한 정보를 확인할 수 있습니다.  
  
|태스크|링크|  
|----------|----------|  
|마이닝 모델 추가 및 삭제|[기존 마이닝 구조에 마이닝 모델 추가](../../analysis-services/data-mining/add-a-mining-model-to-an-existing-mining-structure.md)<br /><br /> [마이닝 구조에서 마이닝 모델 삭제](../../analysis-services/data-mining/delete-a-mining-model-from-a-mining-structure.md)|  
|마이닝 모델 열 작업|[마이닝 모델에서 열 제외](../../analysis-services/data-mining/exclude-a-column-from-a-mining-model.md)<br /><br /> [모델 열의 별칭 만들기](../../analysis-services/data-mining/create-an-alias-for-a-model-column.md)<br /><br /> [마이닝 모델에 있는 열의 분할 변경](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)<br /><br /> [모델에서 회귀 변수로 사용할 열 지정](../../analysis-services/data-mining/specify-a-column-to-use-as-regressor-in-a-model.md)|  
|모델 속성 변경|[마이닝 모델의 속성 변경](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)<br /><br /> [마이닝 모델에 필터를 적용 합니다.](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)<br /><br /> [마이닝 모델에서 필터 삭제](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)<br /><br /> [마이닝 모델에 드릴스루 사용](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)<br /><br /> [보기 또는 변경 알고리즘 매개 변수](../../analysis-services/data-mining/view-or-change-algorithm-parameters.md)|  
|복사. 모델 복사, 이동 또는 관리|[마이닝 모델의 복사본 만들기](../../analysis-services/data-mining/make-a-copy-of-a-mining-model.md)<br /><br /> [마이닝 모델의 뷰 복사](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md)<br /><br /> [내보내기 & #40; DMX & #41;](../../dmx/export-dmx.md)<br /><br /> [IMPORT&#40;DMX&#41;](../../dmx/import-dmx.md)|  
|모델에 데이터 채우기 또는 모델의 데이터 업데이트|[마이닝 모델 처리](../../analysis-services/data-mining/process-a-mining-model.md)|  
|OLAP 모델 작업|[데이터 마이닝 차원 만들기](../../analysis-services/data-mining/create-a-data-mining-dimension.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 개체&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
