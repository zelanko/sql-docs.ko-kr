---
title: 마이닝 모델에 대 한 드릴스루 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f179a467-7d03-4d61-8e9a-6b5afb5fc2d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b955ade0251f43d6a482abe346c286c6bafd0ce7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084603"
---
# <a name="drillthrough-on-mining-models"></a>마이닝 모델에서의 드릴스루
  *드릴스루* 는 마이닝 모델이 나 마이닝 구조를 쿼리하고 모델에 노출 되지 않는 세부 데이터를 가져오는 기능을 의미 합니다.  
  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 사례 데이터로 드릴스루하는 두 가지 옵션을 제공합니다. 데이터를 작성하는 데 사용된 사례로 드릴스루하거나 마이닝 구조의 사례로 드릴스루할 수 있습니다.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>모델 사례로 드릴스루 및 구조로 드릴스루  
 
  **모델 사례** 로 드릴스루하는 기능은 모델의 규칙, 패턴 또는 클러스터에 대한 추가 세부 정보를 찾으려는 경우에 유용합니다. 예를 들어 클러스터링 모델에서는 분석을 위해 고객 연락처 정보를 사용 하지 않습니다. 데이터를 사용할 수 있는 경우에도 드릴스루를 사용 하면 모델에서 해당 정보에 액세스할 수 있습니다.  
  
 반면 **구조 데이터로 드릴스루** 하는 기능은 모델에서 사용할 수 없었던 정보에 액세스하기 위한 것입니다. 예를 들어 데이터 형식이 호환되지 않거나 데이터가 분석에 유용하지 않아서 일부 구조 열이 모델에서 제외되는 경우도 있습니다.  
  
## <a name="enabling-drillthrough-on-a-model"></a>모델에서 드릴스루 사용  
 마이닝 모델에서 드릴스루를 사용하려면 다음 조건을 충족해야 합니다.  
  
-   모델 사례에만 드릴스루를 구성하고 마이닝 구조에는 구성하지 않을 수 있지만 그 반대로는 할 수 없습니다.  즉 마이닝 구조로의 드릴스루를 허용하려면 마이닝 모델에 드릴스루를 설정해야 합니다.  
  
-   모델 및 구조의 드릴스루는 모두 기본적으로 사용하지 않도록 설정되어 있습니다. 데이터 마이닝 마법사를 사용하는 경우 모델 사례로 드릴스루할 수 있도록 설정하는 옵션은 마법사의 마지막 페이지에 있습니다.  
  
-   기존 마이닝 모델에 드릴스루 기능을 추가할 수 있지만 이렇게 하면 모델을 다시 처리해야 데이터로 드릴스루할 수 있습니다.  
  
-   학습 과정에서 만들어진 캐시가 유지되지 않은 경우 드릴스루는 작동하지 않습니다. 캐싱을 제어하는 속성에 대한 자세한 내용은 [마이닝 구조에서의 드릴스루](drillthrough-on-mining-structures.md)를 참조하세요.  
  
## <a name="models-that-support-drillthrough"></a>드릴스루를 지원하는 모델  
 드릴스루를 허용하도록 마이닝 모델을 구성했으며 적절한 사용 권한이 있는 경우 모델을 찾을 때 적절한 뷰어에서 노드를 클릭하고 해당 특정 노드의 사례에 대한 세부 정보를 검색할 수 있습니다.  
  
 일부 모델은 드릴스루를 지원하지 않습니다. 드릴스루 지원 여부는 모델을 만드는 데 사용된 알고리즘에 따라 다릅니다. 다음 표에서는 드릴스루를 지원하지 않는 모델 유형 또는 드릴스루 지원에 제한 사항이 있는 모델 유형을 보여 줍니다. 여기에 나열되지 않은 모델 유형은 드릴스루를 지원합니다.  
  
|**알고리즘 이름**|**드릴스루 지원**|  
|------------------------|----------------------------------|  
|Microsoft Naïve Bayes 알고리즘|지원되지 않습니다.<br /><br /> 이러한 알고리즘은 콘텐츠의 특정 노드에 사례를 할당하지 않습니다.|  
|Microsoft 신경망 알고리즘|지원되지 않습니다.<br /><br /> 이러한 알고리즘은 콘텐츠의 특정 노드에 사례를 할당하지 않습니다.|  
|Microsoft 로지스틱 회귀 알고리즘|지원되지 않습니다.<br /><br /> 이러한 알고리즘은 콘텐츠의 특정 노드에 사례를 할당하지 않습니다.|  
|Microsoft 선형 회귀 알고리즘|지원됩니다.<br /><br /> 그러나 모델은 단일 노드인 `All`을 만들기 때문에 드릴스루 시 모델에 대한 모든 학습 사례가 반환됩니다. 학습 집합이 큰 경우 결과를 로드하는 데 시간이 많이 소요될 수 있습니다.|  
|Microsoft Time Series 알고리즘|지원됩니다.<br /><br /> 그러나 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 를 사용하여 구조 또는 사례 데이터로 드릴스루할 수 없습니다. 대신 DMX 쿼리를 만들어야 합니다.<br /><br /> 특정 노드로 드릴스루하거나 DMX 쿼리를 작성하여 시계열 모델의 특정 노드에 있는 사례를 검색할 수도 없습니다. 날짜 또는 특성 값과 같은 다른 기준을 사용하여 모델이나 구조에서 사례 데이터를 검색할 수 있습니다.<br /><br /> Microsoft Time Series 알고리즘에 의해 생성된 ARTXP 및 ARIMA 노드에 대한 세부 정보를 보려면 [Microsoft 일반 콘텐츠 트리 뷰어&amp;#40;데이터 마이닝 속성&amp;#41;](../microsoft-generic-content-tree-viewer-data-mining.md)를 사용하는 것이 좋습니다.|  
  
## <a name="related-tasks"></a>관련 작업  
 마이닝 모델에 드릴스루를 사용하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
|작업|링크|  
|-----------|-----------|  
|마이닝 모델 뷰어에서 드릴스루 사용|[모델 뷰어에서 드릴스루 사용](use-drillthrough-from-the-model-viewers.md)|  
|드릴스루를 사용하여 모델에 대한 사례 데이터 검색|[마이닝 모델에서 사례 데이터로 드릴스루](drill-through-to-case-data-from-a-mining-model.md)|  
|기존 마이닝 모델에서 드릴스루 사용|[마이닝 모델에 드릴스루 사용](enable-drillthrough-for-a-mining-model.md)|  
|특정 모델 유형에 대한 드릴스루 쿼리의 예 참조|[데이터 마이닝 쿼리](data-mining-queries.md)|  
|마이닝 모델 마법사에서 드릴스루 사용|[데이터 마이닝 마법사를&#41;&#40;마법사를 완료 ](../completing-the-wizard-data-mining-wizard.md)합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 구조에서의 드릴스루](drillthrough-on-mining-structures.md)  
  
  
