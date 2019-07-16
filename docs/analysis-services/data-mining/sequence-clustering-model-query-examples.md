---
title: 시퀀스 클러스터링 모델 쿼리 예제 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e14fd39a1e917532b61b9f55415281e53598e564
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209677"
---
# <a name="sequence-clustering-model-query-examples"></a>시퀀스 클러스터링 모델 쿼리 예제
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터 마이닝 모델에 대한 쿼리를 만들 때 모델에 저장된 정보에 대한 세부 정보를 제공하는 내용 쿼리를 만들거나, 모델의 패턴을 사용하여 사용자가 제공한 새 데이터를 기반으로 예측을 만드는 예측 쿼리를 만들 수 있습니다. 시퀀스 클러스터링 모델의 경우 내용 쿼리는 일반적으로 발견된 클러스터나 해당 클러스터 내의 전환에 대한 추가 정보를 제공합니다. 쿼리를 사용하여 모델에 대한 메타데이터를 검색할 수도 있습니다.  
  
 시퀀스 클러스터링 모델에 대한 예측 쿼리는 일반적으로 시퀀스와 전환, 모델에 포함된 비시퀀스 특성, 또는 시퀀스 특성과 비시퀀스 특성의 조합 중 하나에 따라 권장 구성을 생성합니다.  
  
 이 섹션에서는 Microsoft 시퀀스 클러스터링 알고리즘 기반의 모델에 대해 쿼리를 만드는 방법을 설명합니다. 쿼리를 만드는 방법에 대한 일반적인 내용은 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)를 참조하세요.  
  
 **내용 쿼리**  
  
 [데이터 마이닝 스키마 행 집합을 사용하여 모델 매개 변수 반환](#bkmk_Query1)  
  
 [상태에 대한 시퀀스 목록 가져오기](#bkmk_Query2)  
  
 [시스템 저장 프로시저 사용](#bkmk_Query3)  
  
 **예측 쿼리**  
  
 [다음 상태 예측](#bkmk_Query4)  
  
##  <a name="bkmk_ContentQueries"></a> 시퀀스 클러스터링 모델에 대한 정보 찾기  
 마이닝 모델의 콘텐츠에 대한 의미 있는 쿼리를 만들려면 모델 콘텐츠의 구조와 노드 유형에 따라 저장되는 정보의 종류를 이해해야 합니다. 자세한 내용은 [시퀀스 클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)를 참조하세요.  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: 데이터 마이닝 스키마 행 집합을 사용 하 여 모델 매개 변수를 반환 합니다.  
 데이터 마이닝 스키마 행 집합을 쿼리하면 기본적인 메타데이터, 모델이 만들어진 날짜 및 시간, 모델이 마지막으로 처리된 날짜 및 시간, 모델의 기반이 되는 마이닝 구조의 이름, 예측 가능한 특성으로 사용된 열 등을 비롯하여 모델에 대한 다양한 종류의 정보를 찾을 수 있습니다.  
  
 다음 쿼리는 `[Sequence Clustering]`모델의 작성 및 학습에 사용된 매개 변수를 반환합니다. 이 모델은 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)의 5단원에서 만들 수 있습니다.  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Sequence Clustering'  
```  
  
 예제 결과:  
  
|MINING_PARAMETERS|  
|------------------------|  
|CLUSTER_COUNT=15,MINIMUM_SUPPORT=10,MAXIMUM_STATES=100,MAXIMUM_SEQUENCE_STATES=64|  
  
 이 모델은 CLUSTER_COUNT에 기본값 10을 사용하여 작성되었습니다. CLUSTER_COUNT에 클러스터 수로 0이 아닌 숫자를 지정하면 알고리즘에서는 이 숫자를 찾을 클러스터의 대략적인 개수에 대한 힌트로 간주합니다. 그러나 분석 과정에서 알고리즘이 찾는 클러스터 수는 그보다 많을 수도 있고 적을 수도 있습니다. 이 예의 경우에 알고리즘은 학습 데이터에 가장 적합한 클러스터를 15개 찾았습니다. 따라서 완성된 모델의 매개 변수 값 목록에서는 모델을 만들 때 전달된 값이 아니라 알고리즘에 의해 결정된 클러스터 수가 보고됩니다.  
  
 단순히 알고리즘에서 최적의 클러스터 수를 결정하도록 하는 방법과 이 방법에는 차이점이 있습니다. 시험 삼아 이와 동일한 데이터를 사용하되 CLUSTER_COUNT는 0으로 설정하여 클러스터링 모델을 하나 더 만들어 볼 수 있습니다. 이 경우에는 알고리즘에서 찾는 클러스터 수가 32개가 됩니다. 따라서 CLUSTER_COUNT에 기본값 10을 사용하면 결과의 개수를 제한할 수 있습니다.  
  
 클러스터 수를 줄이면 대부분의 사용자가 데이터의 그룹화를 쉽게 찾아보고 이해할 수 있으므로 기본적으로 값 10이 사용됩니다. 그러나 각 모델 및 데이터 집합은 서로 다릅니다. 클러스터 수를 다르게 하여 시험해 보면 어떤 매개 변수 값이 가장 정확한 모델을 생성하는지 확인할 수 있습니다.  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: 상태에 대 한 시퀀스 목록 가져오기  
 마이닝 모델 콘텐츠에는 학습 데이터에서 찾은 시퀀스가 첫 번째 상태에 관련된 모든 두 번째 상태의 목록이 결합되어 저장됩니다. 첫 번째 상태는 시퀀스의 레이블로 사용되며, 관련된 두 번째 상태는 전환이라고 합니다.  
  
 예를 들어 다음 쿼리는 시퀀스가 클러스터로 그룹화되기 전에 모델의 첫 번째 상태가 모두 들어 있는 목록을 반환합니다.  모델 루트 노드를 부모(PARENT_UNIQUE_NAME = 0)로 갖는 시퀀스(NODE_TYPE = 13) 목록을 반환하면 이 목록을 가져올 수 있습니다. FLATTENED 키워드는 결과를 읽기 쉽게 해 줍니다.  
  
> [!NOTE]  
>  열 이름 PARENT_UNIQUE_NAME, Support 및 Probability는 대괄호로 묶어 동일한 이름의 예약 키워드와 구별해야 합니다.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME,  
(SELECT ATTRIBUTE_VALUE AS [Product 1],  
[Support] AS [Sequence Support],   
[Probability] AS [Sequence Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_TYPE = 13  
AND [PARENT_UNIQUE_NAME] = 0  
```  
  
 일부 결과:  
  
|NODE_UNIQUE_NAME|Product 1|시퀀스 지지도|시퀀스 확률|  
|------------------------|---------------|----------------------|--------------------------|  
|1081327|Missing|0|#######|  
|1081327|All-Purpose Bike Stand|17|0.00111|  
|1081327|Bike Wash|64|0.00418|  
|1081327|(4-36행 생략)|||  
|1081327|Women's Mountain Shorts|506|0.03307|  
  
 모델의 시퀀스 목록은 항상 알파벳 오름차순으로 정렬됩니다. 시퀀스의 순서 번호를 보면 관련된 전환을 알 수 있으므로 시퀀스의 순서는 중요합니다. **Missing** 값은 항상 전환 0입니다.  
  
 예를 들어 앞의 결과에서 "Women's Mountain Shorts" 제품은 모델에서 시퀀스 번호 37에 해당합니다. 이 정보를 사용하여 "Women's Mountain Shorts" 다음에 구매된 모든 제품을 볼 수 있습니다.  
  
 이렇게 하려면 먼저 이전 쿼리에서 NODE_UNIQUE_NAME에 대해 반환된 값을 참조하여 해당 모델의 모든 시퀀스가 들어 있는 노드의 ID를 가져옵니다. 이 값을 쿼리에 부모 노드의 ID로 전달하여 이 노드에 포함된 전환만 가져옵니다. 여기에는 해당 모델의 전체 시퀀스 목록이 들어 있습니다. 그러나 특정 클러스터의 전환 목록을 보려면 클러스터 노드의 ID를 전달하고 해당 클러스터와 연결된 시퀀스만 확인하면 됩니다.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_DESCRIPTION = 'Transition row for sequence state 37'  
AND [PARENT_UNIQUE_NAME] = '1081327'  
```  
  
 예제 결과:  
  
|NODE_UNIQUE_NAME|  
|------------------------|  
|1081365|  
  
 이 ID가 나타내는 노드에는 "Women's Mountain Shorts" 제품 다음에 오는 시퀀스의 목록이 지지도 및 확률 값과 함께 들어 있습니다.  
  
```  
SELECT FLATTENED  
(SELECT ATTRIBUTE_VALUE AS Product2,  
[Support] AS [P2 Support],  
[Probability] AS [P2 Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_UNIQUE_NAME = '1081365'  
```  
  
 예제 결과:  
  
|t.Product2|t.P2 Support|t.P2 Probability|  
|----------------|------------------|----------------------|  
|Missing|230.7419|0.456012|  
|Classic Vest|8.16129|0.016129|  
|Cycling Cap|60.83871|0.120235|  
|Half-Finger Gloves|30.41935|0.060117|  
|Long-Sleeve Logo Jersey|86.80645|0.171554|  
|Racing Socks|28.93548|0.057185|  
|Short-Sleeve Classic Jersey|60.09677|0.118768|  
  
 해당 모델에서 "Women's Mountain Shorts"와 관련된 다양한 시퀀스의 지지도는 506입니다. 전환의 지지도 값도 합이 506입니다. 그러나 이 숫자는 정수가 아니므로 지지도가 단순히 각 전환을 포함하는 사례 수를 나타낼 것으로 예상한 경우에는 이것이 약간 이상하게 보일 수 있습니다. 그러나 클러스터 생성 방법에서는 부분 멤버 자격을 계산하므로 클러스터 내에 있는 모든 전환의 확률은 해당 클러스터에 속할 확률에 따라 가중치가 적용되어야 합니다.  
  
 예를 들어 네 개의 클러스터가 있고 특정 시퀀스가 클러스터 1, 클러스터 2, 클러스터 3 및 클러스터 4에 속할 가능성이 각각 40%, 30%, 20% 및 10%라면 알고리즘은 해당 전환이 속할 가능성이 가장 큰 클러스터를 확인한 후 클러스터의 이전 확률에 따라 클러스터 내의 확률에 가중치를 적용합니다.  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: 시스템 저장 프로시저 사용  
 앞의 쿼리 예제에서는 모델에 저장된 정보가 복잡하며 필요한 정보를 얻으려면 여러 쿼리를 만들어야 할 수도 있다는 것을 보여 줍니다. 그러나 Microsoft 시퀀스 클러스터링 뷰어에서는 시퀀스 클러스터링 모델에 들어 있는 정보를 그래픽 방식으로 찾아보기 위한 강력한 여러 도구를 제공하며, 이 뷰어를 사용하여 모델을 쿼리하고 드릴다운할 수도 있습니다.  
  
 대부분의 경우 Microsoft 시퀀스 클러스터링 뷰어에서 보여 주는 정보는 Analysis Services 시스템 저장 프로시저를 사용하여 모델을 쿼리하는 방법으로 생성됩니다. 모델 콘텐츠에 대한 DMX(Data Mining Extensions) 쿼리를 작성하여 동일한 정보를 검색할 수도 있지만 Analysis Services 시스템 저장 프로시저를 사용하면 모델을 보다 편리하게 탐색하거나 테스트할 수 있습니다.  
  
> [!NOTE]  
>  시스템 저장 프로시저는 Analysis Services 서버와의 상호 작용을 위해 Microsoft에서 제공하는 클라이언트와 서버에서 내부 처리에 사용됩니다. 따라서 Microsoft는 언제든지 시스템 저장 프로시저를 변경할 권리를 보유합니다. 여기에서는 사용자의 편의를 위해 시스템 저장 프로시저에 대해 설명하지만 프로덕션 환경에서는 시스템 저장 프로시저가 지원되지 않습니다. 프로덕션 환경의 안정성과 호환성을 보장하려면 항상 DMX를 사용하여 직접 쿼리를 작성해야 합니다.  
  
 이 섹션에서는 시스템 저장 프로시저를 사용하여 시퀀스 클러스터링 모델에 대한 쿼리를 만드는 방법을 보여 주는 몇 가지 예제를 제공합니다.  
  
#### <a name="cluster-profiles-and-sample-cases"></a>클러스터 프로필 및 예제 사례  
 클러스터 프로필 탭에서는 모델에 있는 클러스터의 목록과 각 클러스터의 크기, 그리고 클러스터에 포함된 상태를 나타내는 히스토그램을 보여 줍니다. 쿼리에서 비슷한 정보를 검색하는 데 사용할 수 있는 시스템 저장 프로시저는 다음 두 가지가 있습니다.  
  
-   `GetClusterProfile` 은(는) 클러스터의 특성과 해당 클러스터의 NODE_DISTRIBUTION 테이블에서 찾은 모든 정보를 반환합니다.  
  
-   `GetNodeGraph` - 시퀀스 클러스터링 보기의 첫 번째 탭에서 표시되는 내용에 해당하는 클러스터의 수학적 그래프 표현을 생성하는 데 사용할 수 있는 노드 및 가장자리를 반환합니다. 노드는 클러스터이고 가장자리는 가중치 또는 수준을 나타냅니다.  
  
 다음 예에서는 시스템 저장 프로시저인 `GetClusterProfiles`를 사용하여 각각의 프로필이 있는 모델 내의 모든 클러스터를 반환합니다. 이 저장 프로시저는 모델의 전체 프로필 집합을 반환하는 일련의 DMX 문을 실행합니다. 그러나 이 저장 프로시저를 사용하려면 모델의 주소를 알고 있어야 합니다.  
  
 `CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('Sequence Clustering', 2147483647, 0)`  
  
 다음 예에서는 시스템 저장 프로시저 `GetNodeGraph`를 사용하고 클러스터 ID를 지정하여 특정 클러스터(클러스터 12)의 프로필을 검색하는 방법을 보여 줍니다. 클러스터 ID는 일반적으로 클러스터 이름의 숫자와 동일합니다.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','12',0)  
```  
  
 다음 쿼리에서와 같이 클러스터 ID를 지정하지 않으면 `GetNodeGraph` 는 모든 클러스터 프로필의 정렬되고 결합된 목록을 반환합니다.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','',0)  
```  
  
 **클러스터 프로필** 탭에는 모델 예제 사례의 히스토그램도 표시됩니다. 이러한 예제 사례는 모델의 이상적인 사례를 나타냅니다. 이 사례는 모델에 학습 데이터와 동일한 방식으로 저장되지 않으므로 모델의 예제 사례를 검색하려면 특수한 구문을 사용해야 합니다.  
  
```  
SELECT * FROM [Sequence Clustering].SAMPLE_CASES WHERE IsInNode('12')  
```  
  
 자세한 내용은 [SELECT FROM &#60;model&#62;.SAMPLE_CASES&#40;DMX&#41;](../../dmx/select-from-model-sample-cases-dmx.md)를 참조하세요.  
  
#### <a name="cluster-characteristics-and-cluster-discrimination"></a>클러스터 특징 및 클러스터 차원  
 **클러스터 특징** 탭에는 각 클러스터의 주요 특성이 확률에 따라 순위가 지정되어 요약됩니다. 클러스터에 속하는 사례의 수와 클러스터의 사례 분포 어떤는 찾을 수 있습니다. 각 특징에는 특정 지지도 있습니다. 특정 클러스터의 특징을 보려면 해당 클러스터의 ID를 알고 있어야 합니다.  
  
 다음 예에서는 시스템 저장 프로시저인 `GetClusterCharacteristics`를 사용하여 클러스터 12의 특징 중 확률 점수가 지정된 임계값 0.0005를 초과하는 모든 특징을 반환합니다.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','12',0.0005)  
```  
  
 모든 클러스터의 특징을 반환하려면 클러스터 ID를 비워 둡니다.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','',0.0005)  
```  
  
 다음 예에서는 시스템 저장 프로시저 `GetClusterDiscrimination` 을 호출하여 클러스터 1과 클러스터 12의 특징을 비교합니다.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('Sequence Clustering','1','12',0.0005,true)  
```  
  
 DMX로 직접 쿼리를 작성하여 두 클러스터를 비교하거나 클러스터를 나머지 클러스터와 비교하려면 먼저 특징 집합 하나를 검색한 다음 관심 있는 특정 클러스터에 대한 특징을 검색하고 두 집합을 비교해야 합니다. 이 시나리오는 보다 복잡하여 일반적으로 클라이언트 처리를 필요로 합니다.  
  
#### <a name="states-and-transitions"></a>상태 및 전환  
 Microsoft 시퀀스 클러스터링의 **상태 전환** 탭에서는 백 엔드에 대한 복잡한 쿼리를 수행하여 서로 다른 여러 클러스터의 통계를 검색하고 비교합니다. 이러한 결과를 다시 생성하려면 보다 복잡한 쿼리와 클라이언트 처리가 필요합니다.  
  
 그러나 [내용 쿼리](#bkmk_ContentQueries)섹션의 예 2에 설명된 DMX 쿼리를 사용하면 시퀀스나 개별 전환에 대한 확률 및 상태를 검색할 수 있습니다.  
  
## <a name="using-the-model-to-make-predictions"></a>모델을 사용하여 예측 만들기  
 시퀀스 클러스터링 모델에 대한 예측 쿼리에서는 다른 클러스터링 모델에서 사용되는 예측 함수를 상당수 사용할 수 있습니다. 또한 특수한 예측 함수인 [PredictSequence&#40;DMX&#41;](../../dmx/predictsequence-dmx.md)를 사용하여 권장 구성을 생성하거나 다음 상태를 예측할 수 있습니다.  
  
###  <a name="bkmk_Query4"></a> 예제 쿼리 4: 다음 상태 예측  
 [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md) 함수를 사용하여 특정 값에 대해 다음으로 가능성이 높은 상태를 예측할 수 있습니다. 여러 개의 다음 상태를 예측할 수도 있습니다. 예를 들어 고객이 구입할 가능성이 가장 높은 세 가지 제품의 목록을 반환하여 권장 제품 목록을 표시할 수 있습니다.  
  
 다음 예제 쿼리는 상위 5개의 예측과 해당 확률을 반환하는 단일 예측 쿼리입니다. 해당 모델에는 중첩 테이블이 포함되어 있으므로 예측을 만들 때는 중첩 테이블 `[v Assoc Seq Line Items]`를 열 참조로 사용해야 합니다. 또한 입력 값을 지정할 때는 중첩된 SELECT 문에 표시된 것과 같이 사례 테이블 및 중첩 테이블 열을 모두 조인해야 합니다.  
  
```  
SELECT FLATTENED PredictSequence([v Assoc Seq Line Items], 7)  
FROM [Sequence Clustering]  
NATURAL PREDICTION JOIN  
(SELECT  (SELECT 1 as [Line Number],  
   'All-Purpose Bike Stand' as [Model]) AS [v Assoc Seq Line Items])   
AS t  
```  
  
 예제 결과:  
  
|Expression.$Sequence|Expression.Line Number|Expression.Model|  
|--------------------------|----------------------------|----------------------|  
|1||Cycling Cap|  
|2||Cycling Cap|  
|3||Sport-100|  
|4||Long-Sleeve Logo Jersey|  
|5||Half-Finger Gloves|  
|6||All-Purpose Bike Stand|  
|7||All-Purpose Bike Stand|  
  
 한 열만 반환될 것으로 예상했을 수 있지만 이 쿼리는 항상 사례 테이블에 대한 열을 반환하므로 결과에는 세 개의 열이 포함되어 있습니다. 이 경우 결과는 결합됩니다. 그렇지 않으면 쿼리에서는 두 개의 중첩된 테이블 열이 들어 있는 단일 열을 반환합니다.  
  
 $sequence 열은 예측 결과를 정렬하기 위해 `PredictSequence` 함수에서 기본적으로 반환되는 열입니다. `[Line Number]`열은 모델의 시퀀스 키와 일치시키는 데 필요하지만 키는 출력되지 않습니다.  
  
 흥미로운 점은 All-Purpose Bike Stand 이후의 예측된 최상위 시퀀스가 Cycling Cap과 Cycling Cap이라는 것입니다. 이는 오류가 아닙니다. 고객에게 데이터가 제공되는 방식과 모델을 학습할 때 데이터가 그룹화되는 방식에 따라 이러한 종류의 시퀀스도 얼마든지 있을 수 있습니다. 예를 들어 고객이 빨간색 Cycling Cap을 구입한 뒤 파란색 Cycling Cap을 하나 더 구입했을 수도 있고, 수량을 지정할 방법이 없어서 두 개의 Cycling Cap을 연달아 구입했을 수도 있습니다.  
  
 6행과 7행의 값은 자리 표시자입니다. 가능한 전환의 체인 끝에 도달하면 예측 결과가 종료되는 것이 아니라 입력으로 전달된 값이 결과에 추가됩니다. 예를 들어 예측 수를 20개로 늘리면 6-20행의 값은 모두 동일하게 All-Purpose Bike Stand가 됩니다.  
  
## <a name="function-list"></a>함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘은 다음 표에 나열된 함수를 추가로 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[Cluster&#40;DMX&#41;](../../dmx/cluster-dmx.md)|입력 사례가 포함되었을 가능성이 가장 높은 클러스터를 반환합니다.|  
|[ClusterDistance&#40;DMX&#41;](../../dmx/clusterdistance-dmx.md)|입력 사례와 지정된 클러스터 사이의 거리를 반환합니다. 클러스터가 지정되지 않은 경우에는 입력 사례와 가장 가능성 있는 클러스터 사이의 거리를 반환합니다.<br /><br /> 이 함수는 EM과 K-Means를 비롯한 모든 종류의 클러스터링 모델과 함께 사용할 수 있지만 알고리즘에 따라 결과가 달라집니다.|  
|[ClusterProbability&#40;DMX&#41;](../../dmx/clusterprobability-dmx.md)|입력 사례가 지정한 클러스터에 속할 확률을 반환합니다.|  
|[IsInNode&#40;DMX&#41;](../../dmx/isinnode-dmx.md)|지정한 노드에 현재 사례가 포함되었는지 여부를 나타냅니다.|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|지정한 상태에 대한 조정된 확률을 반환합니다.|  
|[PredictAssociation&#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|연관된 멤버 자격을 예측합니다.|  
|[PredictCaseLikelihood&#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md)|입력 사례가 기존 모델에 적합할 가능성을 반환합니다.|  
|[PredictHistogram & #40; DMX & #41;](../../dmx/predicthistogram-dmx.md)|지정된 열의 예측에 대한 히스토그램을 나타내는 테이블을 반환합니다.|  
|[PredictNodeId & #40; DMX & #41;](../../dmx/predictnodeid-dmx.md)|사례가 분류되어 있는 노드의 Node_ID를 반환합니다.|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|지정한 상태에 대한 확률을 반환합니다.|  
|[PredictSequence&#40;DMX&#41;](../../dmx/predictsequence-dmx.md)|지정한 시퀀스 데이터 집합에 대한 미래의 시퀀스 값을 예측합니다.|  
|[PredictStdev&#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|지정된 열의 예측 표준 편차를 반환합니다.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|지정한 상태에 대한 지원 값을 반환합니다.|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|지정한 열의 분산을 반환합니다.|  
  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘에 공통된 함수 목록은 [일반 예측 함수&#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md)를 참조하세요. 특정 함수의 구문은 [DMX&#40;Data Mining Extensions&#41; 함수 참조](../../dmx/data-mining-extensions-dmx-function-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 시퀀스 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [시퀀스 클러스터링 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
