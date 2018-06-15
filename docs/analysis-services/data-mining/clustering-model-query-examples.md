---
title: 클러스터링 모델 쿼리 예제 | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6e415c0b82738ec153b20cb79e19af59bacba16
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019430"
---
# <a name="clustering-model-query-examples"></a>클러스터링 모델 쿼리 예제
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터 마이닝 모델에 대한 쿼리를 만들 때 모델에 대한 메타데이터를 검색하거나, 분석 시 발견된 패턴에 대한 세부 정보를 제공하는 내용 쿼리를 만들 수 있습니다. 또는 모델의 패턴을 사용하여 새 데이터에 대한 예측을 만드는 예측 쿼리를 작성할 수 있습니다. 각 유형의 쿼리는 서로 다른 정보를 제공합니다. 예를 들어 내용 쿼리는 발견된 클러스터에 대한 추가 세부 정보를 제공하지만 예측 쿼리는 새 데이터 요소가 속해 있을 가능성이 가장 높은 클러스터를 알려 줍니다.  
  
 이 섹션에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘을 기반으로 하는 모델에 대해 쿼리를 만드는 방법을 설명합니다.  
  
 **내용 쿼리**  
  
 [DMX를 사용하여 모델 메타데이터 가져오기](#bkmk_Query1)  
  
 [스키마 행 집합에서 모델 메타데이터 검색](#bkmk_Query2)  
  
 [클러스터 또는 클러스터 목록 반환](#bkmk_Query3)  
  
 [클러스터에 대한 특성 반환](#bkmk_Query4)  
  
 [시스템 저장 프로시저를 사용하여 클러스터 프로필 반환](#bkmk_Query5)  
  
 [클러스터에 대한 판별 요소 찾기](#bkmk_Query6)  
  
 [클러스터에 속한 사례 반환](#bkmk_Query7)  
  
 **예측 쿼리**  
  
 [클러스터링 모델에서 결과 예측](#bkmk_Query8)  
  
 [클러스터 멤버 자격 결정](#bkmk_Query9)  
  
 [확률과 거리가 포함된 가능한 모든 클러스터 반환](#bkmk_Query10)  
  
##  <a name="bkmk_top2"></a> 모델 정보 찾기  
 모든 마이닝 모델은 마이닝 모델 스키마 행 집합이라고 하는 표준화된 스키마에 따라, 알고리즘을 통해 학습한 내용을 표시합니다. 마이닝 모델 스키마 행 집합에 대한 쿼리는 DMX(Data Mining Extensions) 문을 사용하여 만들 수 있습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 스키마 행 집합을 직접 시스템 테이블로 쿼리할 수도 있습니다.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: DMX를 사용하여 모델 메타데이터 가져오기  
 다음 쿼리는 기본 데이터 마이닝 자습서에서 만든 클러스터링 모델 `TM_Clustering`에 대한 기본 메타데이터를 반환합니다. 클러스터링 모델의 부모 노드에서 사용할 수 있는 메타데이터에는 모델 이름, 모델이 저장된 데이터베이스, 모델의 자식 노드 수 등이 있습니다. 이 쿼리는 DMX 내용 쿼리를 사용하여 모델의 부모 노드에서 메타데이터를 검색합니다.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  CHILDREN_CARDINALITY 열의 이름을 대괄호로 묶어 동일한 이름의 MDX(Multidimensional Expressions) 예약 키워드와 구분해야 합니다.  
  
 예제 결과:  
  
|||  
|-|-|  
|MODEL_CATALOG|TM_Clustering|  
|MODEL_NAME|Adventure Works DW|  
|NODE_CAPTION|Cluster Model|  
|NODE_SUPPORT|12939|  
|CHILDREN_CARDINALITY|10|  
|NODE_DESCRIPTION|모두|  
  
 클러스터링 모델에서 이러한 열의 의미에 대한 정의는 [클러스터링 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)를 참조하세요.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: 스키마 행 집합에서 모델 메타데이터 검색  
 데이터 마이닝 스키마 행 집합을 쿼리하면 DMX 내용 쿼리에 반환되는 것과 동일한 정보를 찾을 수 있는데, 스키마 행 집합은 몇 개의 열을 추가로 제공합니다. 여기에는 모델을 만들 때 사용했던 매개 변수, 모델이 마지막으로 처리된 날짜와 시간, 모델 소유자 등이 있습니다.  
  
 다음 예에서는 모델을 만든 날짜, 수정한 날짜 및 마지막으로 처리한 날짜와 함께 모델을 작성하는 데 사용한 클러스터링 매개 변수와 학습 집합의 크기를 반환합니다. 이 정보는 모델을 문서화하거나 기존 모델을 만들 때 사용했던 클러스터링 옵션을 확인하는 데 유용할 수 있습니다.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Clustering'  
```  
  
 예제 결과:  
  
|||  
|-|-|  
|MODEL_NAME|TM_Clustering|  
|DATE_CREATED|10/12/2007 7:42:51 PM|  
|LAST_PROCESSED|10/12/2007 8:09:54 PM|  
|PREDICTION_ENTITY|Bike Buyer|  
|MINING_PARAMETERS|CLUSTER_COUNT=10,<br /><br /> CLUSTER_SEED=0,<br /><br /> CLUSTERING_METHOD=1,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100,<br /><br /> MINIMUM_SUPPORT=1,<br /><br /> MODELLING_CARDINALITY=10,<br /><br /> SAMPLE_SIZE=50000,<br /><br /> STOPPING_TOLERANCE=10|  
  
 [맨 위로 이동](#bkmk_top2)  
  
## <a name="finding-information-about-clusters"></a>클러스터 정보 찾기  
 클러스터링 모델에 대한 가장 유용한 내용 쿼리는 일반적으로 **클러스터 뷰어**에서 찾아볼 수 있는 것과 동일한 유형의 정보를 반환합니다. 여기에는 클러스터 프로필, 클러스터 특징 및 클러스터 판별 등이 포함됩니다. 이 섹션에서는 이러한 정보를 검색하는 예제 쿼리를 제공합니다.  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: 클러스터 또는 클러스터 목록 반환  
 모든 클러스터의 노드 유형이 5이므로 모델 콘텐츠에서 해당 유형의 노드만 쿼리하면 클러스터 목록을 쉽게 검색할 수 있습니다. 이 예에서와 같이 확률 또는 지지도로 반환되는 노드를 필터링할 수도 있습니다.  
  
```  
SELECT NODE_NAME, NODE_CAPTION ,NODE_SUPPORT, NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 5 AND NODE_SUPPORT > 1000  
```  
  
 예제 결과:  
  
|||  
|-|-|  
|NODE_NAME|002|  
|NODE_CAPTION|클러스터 2|  
|NODE_SUPPORT|1649|  
|NODE_DESCRIPTION|English Education=Graduate Degree , 32 <=Age <=48 , Number Cars Owned=0 , 35964.0771121808 <=Yearly Income <=97407.7163393957 , English Occupation=Professional , Commute Distance=2-5 Miles , Region=North America , Bike Buyer=1 , Number Children At Home=0 , Number Cars Owned=1 , Commute Distance=0-1 Miles , English Education=Bachelors , Total Children=1 , Number Children At Home=2 , English Occupation=Skilled Manual , Marital Status=S , Total Children=0 , House Owner Flag=0 , Gender=F , Total Children=2 , Region=Pacific|  
  
 클러스터를 정의하는 특성은 데이터 마이닝 스키마 행 집합의 두 열에서 찾을 수 있습니다.  
  
-   NODE_DESCRIPTION 열에는 쉼표로 구분된 특성 목록이 들어 있습니다. 특성 목록이 표시용으로 축약될 수도 있습니다.  
  
-   NODE_DISTRIBUTION 열의 중첩 테이블에는 클러스터에 대한 전체 특성 목록이 들어 있습니다. 클라이언트에서 계층적 행 집합을 지원하지 않는 경우 SELECT 열 목록 앞에 FLATTEN 키워드를 추가하여 중첩 테이블을 반환할 수 있습니다. FLATTENED 키워드 사용에 대한 자세한 내용은 [SELECT FROM &#60;model&#62;.CONTENT &#40;DMX&#41;](../../dmx/select-from-model-content-dmx.md)를 참조하세요.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query4"></a> 예제 쿼리 4: 클러스터에 대한 특성 반환  
 **클러스터 뷰어** 에는 각 클러스터의 특성과 특성 값을 나열하는 프로필이 표시됩니다. 또한 모델에 포함된 사례의 전체 모집단에 대한 값 분포를 보여 주는 히스토그램도 표시됩니다. 뷰어에서 모델을 검색하는 경우 마이닝 범례에서 히스토그램을 손쉽게 복사한 다음 Excel 또는 Word 문서에 붙여넣을 수 있습니다. 또한 뷰어의 클러스터 특징 창에서 다른 클러스터의 특성을 그래픽으로 비교할 수도 있습니다.  
  
 그러나 한 번에 둘 이상의 클러스터에 대한 값을 구해야 하는 경우 모델을 쿼리하는 것이 더 간단합니다. 예를 들어 모델을 검색할 때 `Number Cars Owned`특성과 관련하여 상위 두 클러스터가 서로 다를 경우 각 클러스터에 대한 값을 추출하려고 합니다.  
  
```  
SELECT TOP 2 NODE_NAME,   
(SELECT ATTRIBUTE_VALUE, [PROBABILITY] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Number Cars Owned')  
AS t  
FROM [TM_Clustering].CONTENT  
WHERE NODE_TYPE = 5  
```  
  
 첫 번째 코드 줄에는 상위 두 클러스터만 사용하도록 지정되어 있습니다.  
  
> [!NOTE]  
>  기본적으로 클러스터는 지지도 순으로 순서가 지정됩니다. 따라서 NODE_SUPPORT 열은 생략할 수 있습니다.  
  
 두 번째 코드 줄에는 중첩 테이블 열에서 특정 열만 반환하는 하위 SELECT 문이 추가되어 있습니다. 또한 중첩 테이블의 행을 대상 특성 `Number Cars Owned`와 관련된 행으로 제한합니다. 간단하게 표시하기 위해 중첩 테이블은 별칭으로 지정되어 있습니다.  
  
> [!NOTE]  
>  중첩 테이블 열 `PROBABILITY`는 MDX 예약어의 이름이기도 하므로 대괄호로 묶어야 합니다.  
>   
>  예제 결과:  
  
|NODE_NAME|T.ATTRIBUTE_VALUE|T.PROBABILITY|  
|----------------|------------------------|-------------------|  
|001|2|0.829207754|  
|001|1.|0.109354156|  
|001|3|0.034481552|  
|001|4|0.013503302|  
|001|0|0.013453236|  
|001|Missing|0|  
|002|0|0.576980023|  
|002|1.|0.406623939|  
|002|2|0.016380082|  
|002|3|1.60E-05|  
|002|4|0|  
|002|Missing|0|  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> 예제 쿼리 5: 시스템 저장 프로시저를 사용하여 클러스터 프로필 반환  
 DMX를 사용하여 직접 쿼리를 작성하는 것보다는 클러스터 작업을 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용하는 시스템 저장 프로시저를 호출하는 것이 더 간단할 수 있습니다. 다음 예에서는 내부 저장 프로시저를 사용하여 ID가 002인 클러스터에 대한 프로필을 반환하는 방법을 보여 줍니다.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('TM_Clustering", '002',0.0005  
```  
  
 마찬가지로 다음 예에서와 같이 시스템 저장 프로시저를 사용하여 특정 클러스터의 특징을 반환할 수 있습니다.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('TM_Clustering", '009',0.0005  
```  
  
 예제 결과:  
  
|특성|값|빈도|지원|  
|----------------|------------|---------------|-------------|  
|Number Children at Home|0|0.999999829076798|899|  
|Region|North America|0.999852875241508|899|  
|Total Children|0|0.993860958572323|893|  
  
> [!NOTE]  
>  데이터 마이닝 시스템 저장 프로시저는 내부적으로만 사용할 수 있으며 필요에 따라 이 프로시저를 변경할 수 있는 권한은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에 있습니다. 따라서 프로덕션 환경에서는 DMX, AMO 또는 XMLA를 사용하여 쿼리를 만드는 것이 좋습니다.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query6"></a> 예제 쿼리 6: 클러스터에 대한 판별 요소 찾기  
 **클러스터 뷰어** 의 **클러스터 판별** 탭에서는 손쉽게 한 클러스터와 다른 클러스터를 비교하거나, 한 클러스터와 나머지 모든 사례(나머지 클러스터)를 비교할 수 있습니다.  
  
 그러나 이러한 정보를 반환하는 쿼리를 만드는 것이 복잡할 수 있으며 임시 결과를 저장하고 둘 이상의 쿼리 결과를 비교하기 위해서는 클라이언트에서 약간의 추가 처리가 필요할 수 있습니다. 이 경우 간단하게 시스템 저장 프로시저를 사용할 수 있습니다.  
  
 다음 쿼리는 노드 ID가 각각 009와 007인 두 클러스터 간의 주요 판별 요소를 나타내는 단일 테이블을 반환합니다. 양수 값을 갖는 특성은 클러스터 009를 선호하며 음수 값을 갖는 특성은 클러스터 007을 선호합니다.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','007',0.0005,true)  
```  
  
 예제 결과:  
  
|특성|값|점수|  
|----------------|------------|-----------|  
|Region|North America|100|  
|English Occupation|Skilled Manual|94.9003803898654|  
|Region|Europe|-72.5041051379789|  
|English Occupation|수동|-69.6503163202722|  
  
 첫 번째 드롭다운 목록에서 클러스터 9를 선택하고 두 번째 드롭다운 목록에서 클러스터 7을 선택한 경우 이는 **클러스터 판별** 뷰어의 차트에 표시되는 정보와 동일합니다. 클러스터 9를 나머지 클러스터와 비교하려면 다음 예에서와 같이 두 번째 매개 변수에 빈 문자열을 사용하십시오.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','',0.0005,true)  
```  
  
> [!NOTE]  
>  데이터 마이닝 시스템 저장 프로시저는 내부적으로만 사용할 수 있으며 필요에 따라 이 프로시저를 변경할 수 있는 권한은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에 있습니다. 따라서 프로덕션 환경에서는 DMX, AMO 또는 XMLA를 사용하여 쿼리를 만드는 것이 좋습니다.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> 예제 쿼리 7: 클러스터에 속한 사례 반환  
 마이닝 모델에 드릴스루를 사용하도록 설정한 경우 모델에 사용된 사례에 대한 세부 정보를 반환하는 쿼리를 만들 수 있습니다. 또한 마이닝 구조에도 드릴스루를 사용하도록 설정한 경우 [StructureColumn&#40;DMX&#41;](../../dmx/structurecolumn-dmx.md) 함수를 사용하여 기본 구조의 열을 포함할 수 있습니다.  
  
 다음 예에서는 모델에 사용된 Age 및 Region 열과 모델에 사용되지 않은 First Name 열을 추가로 반환합니다. 이 쿼리는 Cluster 1로 분류된 사례만 반환합니다.  
  
```  
SELECT [Age], [Region], StructureColumn('First Name')  
FROM [TM_Clustering].CASES  
WHERE IsInNode('001')  
```  
  
 클러스터에 속한 사례를 반환하려면 클러스터 ID를 알아야 합니다. 클러스터 ID는 뷰어 중 하나에서 모델을 탐색하여 확인할 수 있습니다. 또는 보다 쉬운 참조를 위해 클러스터의 이름을 바꾼 다음 ID 번호 대신 바꾼 이름을 사용할 수 있습니다. 그러나 모델을 다시 처리하면 클러스터에 할당된 이름이 손실됩니다.  
  
 [맨 위로 이동](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>모델을 사용하여 예측 수행  
 데이터를 설명하고 이해하는 데 클러스터링이 일반적으로 사용되지만 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 구현을 사용해도 클러스터 멤버 자격에 대한 예측을 만들고 예측과 연관된 확률을 반환할 수 있습니다. 이 섹션에서는 클러스터링 모델에 대한 예측 쿼리를 만드는 방법에 대한 예를 제공합니다. 테이블 형식 데이터 원본을 지정하여 여러 사례에 대한 예측을 만들거나 단일 쿼리를 만들어 한 번에 새 값을 제공할 수 있습니다. 의미를 명확하게 전달하기 위해 이 섹션의 예는 모두 단일 쿼리입니다.  
  
 DMX를 사용하여 예측 쿼리를 만드는 방법은 [데이터 마이닝 쿼리 도구](../../analysis-services/data-mining/data-mining-query-tools.md)를 참조하세요.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query8"></a> 예제 쿼리 8: 클러스터링 모델에서 결과 예측  
 만든 클러스터링 모델에 예측 가능한 특성이 포함되어 있는 경우 이 모델을 사용하여 결과에 대한 예측을 만들 수 있습니다. 그러나 예측 가능한 열을 **Predict** 로 설정했는지 또는 **PredictOnly**로 설정했는지에 따라 모델이 예측 가능한 특성을 다르게 처리합니다. 열 사용법을 **Predict**로 설정하면 해당 특성 값이 클러스터링 모델에 추가되고 완성된 모델에 특성으로 표시됩니다. 그러나 열 사용법을 **PredictOnly**로 설정하면 해당 값이 클러스터를 만드는 데 사용되지 않습니다. 대신 모델이 완성된 후 클러스터링 알고리즘이 각 사례가 속해 있는 클러스터를 기반으로 **PredictOnly** 특성에 대한 새 값을 생성합니다.  
  
 다음 쿼리는 모델에 새로운 단일 사례를 제공하는데, 사례에 대한 유일한 정보는 연령과 성별입니다. SELECT 문에 관심 있는 예측 가능한 특성/값 쌍을 지정하고 [PredictProbability&#40;DMX&#41;](../../dmx/predictprobability-dmx.md) 함수는 이러한 특성이 포함된 사례의 대상 결과 확률을 알려 줍니다.  
  
```  
SELECT  
  [TM_Clustering].[Bike Buyer], PredictProbability([Bike Buyer],1)  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 열 사용법이 **Predict**로 설정된 경우의 예제 결과는 다음과 같습니다.  
  
|Bike Buyer|식|  
|----------------|----------------|  
|1.|0.592924735740338|  
  
 열 사용법이 **PredictOnly** 로 설정되어 있고 모델이 다시 처리된 경우의 예제 결과는 다음과 같습니다.  
  
|Bike Buyer|식|  
|----------------|----------------|  
|1.|0.55843544003102|  
  
 이 예에서 모델의 차이는 그다지 중요하지 않습니다. 그러나 실제 값 분포와 모델에서 예측하는 분포의 차이를 알아내는 것이 때로는 중요할 수 있습니다. [PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md) 함수는 해당 모델이 제공될 경우 사례가 나타날 가능성을 알려 주므로 이러한 경우에 유용합니다.  
  
 PredictCaseLikelihood 함수에 의해 반환되는 값은 확률이므로 항상 0과 1 사이이며 임의의 결과를 나타내는 경우 값이 .5입니다. 그러므로 점수가 .5 미만인 경우 해당 모델이 제공될 경우 예측 사례가 나타날 가능성이 별로 없음을 의미하고 점수가 .5 이상인 경우에는 예측 사례가 해당 모델에 적합하지 않은 경우보다 나타날 가능성이 높음을 의미합니다.  
  
 예를 들어 다음 쿼리는 새로운 샘플 사례가 나타날 가능성의 특징을 결정하는 두 개의 값을 반환합니다. 정규화되지 않은 값은 현재 모델이 제공될 경우의 확률을 나타냅니다. NORMALIZED 키워드를 사용할 경우 함수에 의해 반환되는 유사도 점수는 "모델이 포함된 확률"을 "모델이 포함되지 않은 확률"로 나누어 조정됩니다.  
  
```  
SELECT  
PredictCaseLikelihood(NORMALIZED) AS [NormalizedValue], PredictCaseLikelihood(NONNORMALIZED) AS [NonNormalizedValue]  
FROM  
  [TM_Clustering_PredictOnly]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 예제 결과:  
  
|NormalizedValue|NonNormalizedValue|  
|---------------------|------------------------|  
|5.56438372679893E-11|8.65459953145182E-68|  
  
 이 결과 값은 과학적 표기법으로 표시됩니다.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query9"></a> 예제 쿼리 3: 클러스터 멤버 자격 결정  
 이 예에서는 [Cluster&#40;DMX&#41;](../../dmx/cluster-dmx.md) 함수를 사용하여 새로운 사례가 속해 있을 가능성이 가장 높은 클러스터를 반환하고, [ClusterProbability&#40;DMX&#41;](../../dmx/clusterprobability-dmx.md) 함수를 사용하여 해당 클러스터의 멤버 자격에 대한 확률을 반환합니다.  
  
```  
SELECT Cluster(), ClusterProbability()  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status]) AS t  
```  
  
 예제 결과:  
  
|$CLUSTER|식|  
|--------------|----------------|  
|클러스터 2|0.397918596951617|  
  
 **참고** 기본적으로 **ClusterProbability** 함수는 발생할 가능성이 가장 높은 클러스터의 확률을 반환합니다. 그러나 `ClusterProbability('cluster name')`구문을 사용하여 다른 클러스터를 지정할 수 있습니다. 이 경우 각 예측 함수의 결과는 다른 결과에 대해 독립적입니다. 따라서 두 번째 열의 확률 점수는 첫 번째 열에 명명된 클러스터가 아닌 다른 클러스터를 참조할 수 있습니다.  
  
 [맨 위로 이동](#bkmk_top2)  
  
###  <a name="bkmk_Query10"></a> 예제 쿼리 10: 확률과 거리가 포함된 가능한 모든 클러스터 반환  
 이전 예에서 확률 점수는 그리 높지 않았습니다. 보다 나은 클러스터가 있는지 확인하기 위해 [PredictHistogram&#40;DMX&#41;](../../dmx/predicthistogram-dmx.md) 함수를 [Cluster&#40;DMX&#41;](../../dmx/cluster-dmx.md) 함수와 함께 사용하여 새로운 사례가 각 클러스터에 속해 있을 확률과 함께 가능한 모든 클러스터를 포함하는 중첩 테이블을 반환합니다. FLATTENED 키워드는 보다 쉽게 볼 수 있도록 계층적 행 집합을 플랫 테이블로 변경하는 데 사용됩니다.  
  
```  
SELECT FLATTENED PredictHistogram(Cluster())  
From  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status])  
```  
  
|Expression.$CLUSTER|Expression.$DISTANCE|Expression.$PROBABILITY|  
|-------------------------|--------------------------|-----------------------------|  
|클러스터 2|0.602081403048383|0.397918596951617|  
|클러스터 10|0.719691686785675|0.280308313214325|  
|클러스터 4|0.867772590378791|0.132227409621209|  
|클러스터 5|0.931039872200985|0.0689601277990149|  
|클러스터 3|0.942359230072167|0.0576407699278328|  
|클러스터 6|0.958973668972756|0.0410263310272437|  
|클러스터 7|0.979081275926724|0.0209187240732763|  
|클러스터 1|0.999169044818624|0.000830955181376364|  
|클러스터 9|0.999831227795894|0.000168772204105754|  
|클러스터 8|1.|0|  
  
 기본적으로 결과는 확률 순으로 순위가 지정됩니다. 결과를 통해 Cluster 2의 확률이 매우 낮지만 그래도 Cluster 2가 새 데이터 요소에 가장 적합하다는 것을 알 수 있습니다.  
  
 **참고** 추가 열 `$DISTANCE`는 데이터 요소에서 클러스터까지의 거리를 나타냅니다. 기본적으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘은 Scalable EM 클러스터링을 사용하여 여러 개의 클러스터를 각 데이터 요소에 할당하고 가능한 클러스터의 순위를 지정합니다.  그러나 K-Means 알고리즘을 사용하여 클러스터링 모델을 만드는 경우 각 데이터 요소에 한 개의 클러스터만 할당할 수 있으므로 이 쿼리는 한 개의 행만 반환합니다. [PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md) 함수를 사용하여 기본 구조의 열을 포함할 수 있습니다. EM 클러스터링과 K-means 클러스터링의 차이점에 대한 자세한 내용은 [Microsoft 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)를 참조하세요.  
  
 [맨 위로 이동](#bkmk_top2)  
  
## <a name="function-list"></a>함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터링 알고리즘을 사용하여 작성된 모델은 다음 표에 나열된 함수를 추가로 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[Cluster&#40;DMX&#41;](../../dmx/cluster-dmx.md)|입력 사례가 포함되었을 가능성이 가장 높은 클러스터를 반환합니다.|  
|[ClusterDistance&#40;DMX&#41;](../../dmx/clusterdistance-dmx.md)|입력 사례와 지정된 클러스터 사이의 거리를 반환합니다. 클러스터가 지정되지 않은 경우에는 입력 사례와 가장 가능성 있는 클러스터 사이의 거리를 반환합니다.<br /><br /> 입력 사례가 지정한 클러스터에 속할 확률을 반환합니다.|  
|[ClusterProbability&#40;DMX&#41;](../../dmx/clusterprobability-dmx.md)|입력 사례가 지정한 클러스터에 속할 확률을 반환합니다.|  
|[IsDescendant & #40; DMX & #41;](../../dmx/isdescendant-dmx.md)|한 노드가 모델에서 다른 노드의 자식인지 여부를 확인합니다.|  
|[IsInNode & #40; DMX & #41;](../../dmx/isinnode-dmx.md)|지정한 노드에 현재 사례가 포함되었는지 여부를 나타냅니다.|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|가중치 확률을 반환합니다.|  
|[PredictAssociation & #40; DMX & #41;](../../dmx/predictassociation-dmx.md)|연관 데이터 집합에서의 멤버 자격을 예측합니다.|  
|[PredictCaseLikelihood&#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md)|입력 사례가 기존 모델에 적합할 가능성을 반환합니다.|  
|[PredictHistogram&#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|현재 예측된 값과 관련 된 값의 테이블을 반환 합니다.|  
|[PredictNodeId & #40; DMX & #41;](../../dmx/predictnodeid-dmx.md)|각 사례에 대한 Node_ID를 반환합니다.|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|예측 값의 확률을 반환합니다.|  
|[PredictStdev & #40; DMX & #41;](../../dmx/predictstdev-dmx.md)|지정된 열의 예측 표준 편차를 반환합니다.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|지정한 상태에 대한 지원 값을 반환합니다.|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|지정한 열의 분산을 반환합니다.|  
  
 특정 함수의 구문은 [DMX&#40;Data Mining Extensions&#41; 함수 참조](../../dmx/data-mining-extensions-dmx-function-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 클러스터링 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)   
 [Microsoft 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)  
  
  
