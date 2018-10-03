---
title: 마이닝 모델 연결에 대 한 모델 콘텐츠 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- mining model content, association models
- rules [Data Mining]
- associations [Analysis Services]
ms.assetid: d5849bcb-4b8f-4f71-9761-7dc5bb465224
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4cdbacc27816464440fe57db7c7d727026754220
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135063"
---
# <a name="mining-model-content-for-association-models-analysis-services---data-mining"></a>연결 모델에 대한 마이닝 모델 콘텐츠(Analysis Services - 데이터 마이닝)
  이 항목에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 알고리즘을 사용하는 모델에만 적용되는 마이닝 모델 콘텐츠에 대해 설명합니다. 모든 모델 유형에 적용되는 마이닝 모델 콘텐츠와 관련된 일반 용어 및 통계 용어에 대한 설명은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="understanding-the-structure-of-an-association-model"></a>연결 모델의 구조 이해  
 연결 모델의 구조는 간단합니다. 각 모델에는 모델과 메타데이터를 나타내는 부모 노드가 한 개 있고 각 부모 노드에는 항목 집합과 규칙에 대한 기본 목록이 있습니다. 항목 집합과 규칙은 트리로 구성되어 있지 않으며 다음 다이어그램에서와 같이 항목 집합 및 규칙 순으로 정렬됩니다.  
  
 ![연결 모델에 대 한 모델 콘텐츠 구조](../media/modelcontentstructure-assoc.gif "연결 모델에 대 한 모델 콘텐츠 구조")  
  
 각 항목 집합은 자체 노드(NODE_TYPE = 7)에 포함되어 있습니다. *노드* 에는 항목 집합의 정의, 이 항목 집합을 포함하는 사례 수 및 기타 정보가 포함되어 있습니다.  
  
 각 규칙도 자체 노드(NODE_TYPE = 8)에 포함되어 있습니다. *규칙* 은 항목이 연결되는 일반적인 패턴에 대해 설명하며 IF-THEN 문과 비슷합니다. 규칙의 왼쪽에는 기존 조건 또는 조건 집합이 표시되고 규칙의 오른쪽에는 일반적으로 왼쪽에 있는 조건과 연결되는 데이터 집합의 항목이 표시됩니다.  
  
 **참고** 규칙 또는 항목 집합을 추출하려는 경우 쿼리를 사용하여 원하는 노드 유형만 반환할 수 있습니다. 자세한 내용은 [연결 모델 쿼리 예제](association-model-query-examples.md)를 참조하세요.  
  
## <a name="model-content-for-an-association-model"></a>연결 모델에 대한 모델 콘텐츠  
 이 섹션에서는 연결 모델과 관련된 마이닝 모델 콘텐츠 열에 대한 세부 정보와 예만 제공합니다.  
  
 스키마 행 집합(예: MODEL_CATALOG 및 MODEL_NAME)의 범용 열에 대한 자세한 내용은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)를 참조하세요.  
  
 MODEL_CATALOG  
 모델이 저장되는 데이터베이스의 이름입니다.  
  
 MODEL_NAME  
 모델의 이름입니다.  
  
 ATTRIBUTE_NAME  
 이 노드에 해당하는 특성의 이름입니다.  
  
 NODE_NAME  
 노드 이름입니다. 연결 모델의 경우 이 열은 NODE_UNIQUE_NAME과 동일한 값을 포함합니다.  
  
 NODE_UNIQUE_NAME  
 노드의 고유한 이름입니다.  
  
 NODE_TYPE  
 연결 모델이 출력하는 노드 유형은 다음과 같습니다.  
  
|노드 유형 ID|형식|  
|------------------|----------|  
|1(모델)|루트 또는 부모 노드입니다.|  
|7(항목 집합)|항목 집합 또는 특성-값 쌍 모음입니다. 예를 들면 다음과 같습니다.<br /><br /> `Product 1 = Existing, Product 2 = Existing`<br /><br /> 로 구분하거나 여러<br /><br /> `Gender = Male`를 참조하세요.|  
|8(규칙)|항목 간의 관련 방식을 정의하는 규칙입니다.<br /><br /> 예:<br /><br /> `Product 1 = Existing, Product 2 = Existing -> Product 3 = Existing`를 참조하세요.|  
  
 NODE_CAPTION  
 노드와 연결된 레이블 또는 캡션입니다.  
  
 **항목 집합 노드** 쉼표로 구분된 항목 목록입니다.  
  
 **규칙 노드** 규칙의 왼쪽과 오른쪽을 포함합니다.  
  
 CHILDREN_CARDINALITY  
 현재 노드의 자식 수를 나타냅니다.  
  
 **부모 노드** 항목 집합 수에 규칙 수를 더한 값을 나타냅니다.  
  
> [!NOTE]  
>  항목 집합 및 규칙 수에 대한 세부 분류를 보려면 모델 루트 노드의 NODE_DESCRIPTION을 참조하십시오.  
  
 **항목 집합 또는 규칙 노드** 항상 0입니다.  
  
 PARENT_UNIQUE_NAME  
 노드 부모의 고유한 이름입니다.  
  
 **부모 노드** 항상 NULL입니다.  
  
 **항목 집합 또는 규칙 노드** 항상 0입니다.  
  
 NODE_DESCRIPTION  
 노드 콘텐츠에 대한 알기 쉬운 설명입니다.  
  
 **부모 노드** 다음과 같은 모델 정보 목록을 쉼표로 구분하여 포함합니다.  
  
|항목|Description|  
|----------|-----------------|  
|ITEMSET_COUNT|모델에 있는 모든 항목 집합 수입니다.|  
|RULE_COUNT|모델에 있는 모든 규칙 수입니다.|  
|MIN_SUPPORT|단일 항목 집합에 대해 발견된 최소 지지도입니다.<br /><br /> **참고** 이 값은 *MINIMUM _SUPPORT* 매개 변수에 설정한 값과 다를 수 있습니다.|  
|MAX_SUPPORT|단일 항목 집합에 대해 발견된 최대 지지도입니다.<br /><br /> **참고** 이 값은 *MAXIMUM_SUPPORT* 매개 변수에 설정한 값과 다를 수 있습니다.|  
|MIN_ITEMSET_SIZE|최소 항목 집합의 크기이며 항목 수로 표시됩니다.<br /><br /> 값이 0 이면는 `Missing` 상태가 개별 항목으로 처리 되었습니다.<br /><br /> **참고** *MINIMUM_ITEMSET_SIZE* 매개 변수의 기본값은 1입니다.|  
|MAX_ITEMSET_SIZE|발견된 가장 큰 항목 집합의 크기를 나타냅니다.<br /><br /> **참고** 이 값은 모델을 만들 때 *MAX_ITEMSET_SIZE* 매개 변수에 설정한 값에 따라 제약을 받습니다. 즉, 해당 매개 변수 값보다 작거나 같아야 합니다. 기본값은 3입니다.|  
|MIN_PROBABILITY|모델에 있는 단일 항목 집합 또는 규칙에 대해 발견된 최소 확률입니다.<br /><br /> 예: 0.400390625<br /><br /> **참고** 항목 집합의 경우 이 값은 모델을 만들 때 *MINIMUM_PROBABILITY* 매개 변수에 설정한 값보다 항상 큽니다.|  
|MAX_PROBABILITY|모델에 있는 단일 항목 집합 또는 규칙에 대해 발견된 최대 확률입니다.<br /><br /> 예: 1<br /><br /> **참고** 항목 집합의 최대 확률을 제약하는 매개 변수는 없습니다. 너무 자주 사용되는 항목을 제거하려면 *MAXIMUM_SUPPORT* 매개 변수를 대신 사용하세요.|  
|MIN_LIFT|모델이 항목 집합에 제공하는 최소 리프트 양입니다.<br /><br /> 예: 0.14309369632511<br /><br /> 참고: 최소 리프트를 알면 한 항목 집합에 대한 리프트가 중요한지 여부를 확인할 수 있습니다.|  
|MAX_LIFT|모델이 항목 집합에 제공하는 최대 리프트 양입니다.<br /><br /> 예: 1.95758227647523 **참고** 최대 리프트를 알면 한 항목 집합에 대한 리프트가 중요한지 여부를 확인할 수 있습니다.|  
  
 **항목 집합 노드** 항목 집합 노드는 항목 목록을 포함하며 쉼표로 구분된 텍스트 문자열로 표시됩니다.  
  
 예:  
  
 `Touring Tire = Existing, Water Bottle = Existing`  
  
 이는 Touring Tire와 Water Bottle을 함께 구매했음을 의미합니다.  
  
 **규칙 노드** 규칙 노드는 화살표로 구분된 규칙의 왼쪽과 오른쪽을 포함합니다.  
  
 예: `Touring Tire = Existing, Water Bottle = Existing -> Cycling cap = Existing`  
  
 이는 누군가가 Touring Tire와 Water Bottle을 구매했는데 이 사람이 Cycling cap을 구매했을 가능성도 있음을 의미합니다.  
  
 NODE_RULE  
 노드에 포함된 규칙 또는 항목 집합을 설명하는 XML 조각입니다.  
  
 **부모 노드** 비어 있습니다.  
  
 **항목 집합 노드** 비어 있습니다.  
  
 **규칙 노드** XML 조각은 지지도, 신뢰성, 항목 수, 규칙의 왼쪽을 나타내는 노드의 ID 등과 같은 유용한 추가 규칙 정보를 포함합니다.  
  
 MARGINAL_RULE  
 비어 있습니다.  
  
 NODE_PROBABILITY  
 항목 집합 또는 규칙과 관련된 확률 또는 신뢰성 점수입니다.  
  
 **부모 노드** 항상 0입니다.  
  
 **항목 집합 노드** 항목 집합의 확률입니다.  
  
 **규칙 노드** 규칙에 대한 신뢰성 값입니다.  
  
 MARGINAL_PROBABILITY  
 NODE_PROBABILITY와 동일합니다.  
  
 NODE_DISTRIBUTION  
 이 테이블은 노드가 항목 집합인지 또는 규칙인지에 따라 매우 다른 정보를 포함합니다.  
  
 **부모 노드** 비어 있습니다.  
  
 **항목 집합 노드** 항목 집합에 포함된 각 항목을 확률 및 지지도 값과 함께 나열합니다. 예를 들어 항목 집합이 두 개의 제품을 포함할 경우 각 제품의 이름이 이 제품에 포함된 사례 수와 함께 나열됩니다.  
  
 **규칙 노드** 두 개의 행을 포함합니다. 첫 번째 행은 규칙의 오른쪽에 있는 특성 즉, 예상 항목을 신뢰성 점수와 함께 표시합니다.  
  
 두 번째 행은 연결 모델에만 해당되며 규칙 오른쪽에 있는 항목 집합에 대한 포인터를 포함합니다. 이 포인터는 ATTRIBUTE_VALUE 열에 오른쪽 항목만 포함하는 항목 집합의 ID로 표시됩니다.  
  
 예를 들어 규칙이 `If {A,B} Then {C}`일 경우 테이블은 항목 `{C}`의 이름 및 항목 C에 대한 항목 집합을 포함하는 노드의 ID를 포함합니다.  
  
 이 포인터는 항목 집합 노드에서 오른쪽 제품을 포함하는 모든 사례 수를 확인할 수 있으므로 유용합니다. `If {A,B} Then {C}` 규칙의 영향을 받는 사례는 `{C}`에 대한 항목 집합에 나열된 사례의 하위 집합입니다.  
  
 NODE_SUPPORT  
 이 노드를 지지하는 사례 수입니다.  
  
 **부모 노드** 모델에 포함된 사례 수입니다.  
  
 **항목 집합 노드** 항목 집합의 모든 항목을 포함하는 사례 수입니다.  
  
 **규칙 노드** 규칙에 포함된 모든 항목을 포함하는 사례 수입니다.  
  
 MSOLAP_MODEL_COLUMN  
 노드가 항목 집합인지 또는 규칙인지에 따라 다른 정보를 포함합니다.  
  
 **부모 노드** 비어 있습니다.  
  
 **항목 집합 노드** 비어 있습니다.  
  
 **규칙 노드** 규칙의 왼쪽에 있는 항목을 포함하는 항목 집합의 ID입니다. 예를 들어 규칙이 `If {A,B} Then {C}`일 경우 이 열은 항목 `{A,B}`만 포함하는 항목 집합의 ID를 포함합니다.  
  
 MSOLAP_NODE_SCORE  
 **부모 노드** 비어 있습니다.  
  
 **항목 집합 노드** 항목 집합의 중요도 점수입니다.  
  
 **규칙 노드** 규칙의 중요도 점수입니다.  
  
> [!NOTE]  
>  중요도는 항목 집합 및 규칙에 대해 서로 다르게 계산됩니다. 자세한 내용은 [Microsoft 연결 알고리즘 기술 참조](microsoft-association-algorithm-technical-reference.md)를 참조하세요.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 비어 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 콘텐츠 &#40;Analysis Services-데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Microsoft 연결 알고리즘](microsoft-association-algorithm.md)   
 [연결 모델 쿼리 예제](association-model-query-examples.md)  
  
  
