---
title: 내용 쿼리 (데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c4f4a5a8-a230-4222-bece-9d563501f65f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f6b20c32ee955023ea24af2f70a83a7793ba1d64
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66085647"
---
# <a name="content-queries-data-mining"></a>내용 쿼리(데이터 마이닝)
  내용 쿼리는 마이닝 모델의 내부 통계와 구조에 대한 정보를 추출하는 한 방법입니다. 내용 쿼리는 때때로 뷰어에서 쉽게 사용할 수 없는 세부 정보를 제공할 수 있습니다. 내용 쿼리의 결과를 사용하여 다른 용도로 사용할 정보를 프로그래밍 방식으로 추출할 수도 있습니다.  
  
 이 섹션에서는 내용 쿼리 및 내용 쿼리에 대한 일반 DMX 구문을 사용하여 검색할 수 있는 정보의 유형에 대한 일반적인 정보를 제공합니다.  
  
 [기본 내용 쿼리](#bkmk_ContentQuery)  
  
-   [구조 및 사례 데이터에 대 한 쿼리](#bkmk_Structure)  
  
-   [모델 패턴에 대한 쿼리](#bkmk_Patterns)  
  
 [예제](#bkmk_Examples)  
  
-   [연결 모델에 대한 내용 쿼리](#bkmk_Assoc)  
  
-   [의사 결정 트리 모델에 대한 내용 쿼리](#bkmk_DecTree)  
  
 [쿼리 결과 작업](#bkmk_Results)  
  
##  <a name="basic-content-queries"></a><a name="bkmk_ContentQuery"></a>기본 내용 쿼리  
 예측 쿼리 작성기를 사용하여 내용 쿼리를 만들거나, SQL Server Management Studio에 제공되는 DMX 내용 쿼리 템플릿을 사용하거나, DMX에서 쿼리를 직접 작성할 수 있습니다. 예측 쿼리와 달리 외부 데이터를 조인할 필요가 없으므로 내용 쿼리를 쉽게 작성할 수 있습니다.  
  
 이 섹션에서는 만들 수 있는 내용 쿼리의 유형에 대한 개요를 제공합니다.  
  
-   마이닝 구조 또는 사례 데이터에 대한 쿼리를 통해 학습에 사용된 세부 데이터를 볼 수 있습니다.  
  
-   모델에 대한 쿼리는 패턴, 특성 목록, 수식 등을 반환할 수 있습니다.  
  
###  <a name="queries-on-structure-and-case-data"></a><a name="bkmk_Structure"></a> 구조 및 사례 데이터에 대한 쿼리  
 DMX는 마이닝 구조와 마이닝 모델을 작성하는 데 사용되는 캐시된 데이터에 대한 쿼리를 지원합니다. 기본적으로 이 캐시는 마이닝 구조를 정의할 때 만들어지고 구조 또는 모델을 처리할 때 채워집니다.  
  
> [!WARNING]  
>  데이터를 학습 및 테스트 집합으로 분리해야 할 경우 이 캐시를 지우거나 삭제할 수 없습니다. 캐시를 지울 경우 사례 데이터를 쿼리할 수 없습니다.  
  
 다음 예에서는 사례 데이터에 대한 쿼리나 마이닝 구조의 데이터에 대한 쿼리를 만들기 위한 일반적인 패턴을 보여 줍니다.  
  
 **모델에 대한 모든 사례 가져오기**  
 `SELECT FROM <model>.CASES`  
  
 이 문을 사용하여 모델을 작성하는 데 사용되는 사례 데이터에서 지정된 열을 검색할 수 있습니다. 이 쿼리를 실행하려면 모델에 대한 드릴스루 권한이 있어야 합니다.  
  
 **구조에 포함된 모든 데이터 보기**  
 `SELECT FROM <structure>.CASES`  
  
 이 문을 사용하면 특정 마이닝 모델에 포함되지 않은 열을 포함하여 구조에 포함된 모든 데이터를 볼 수 있습니다. 마이닝 구조에서 데이터를 검색하려면 모델과 구조 모두에 대한 드릴스루 권한이 있어야 합니다.  
  
 **값 범위 가져오기**  
 `SELECT DISTINCT RangeMin(<column>), RangeMax(<column>) FROM <model>`  
  
 이 문을 사용하여 연속 열 또는 불연속화 열 버킷의 최소값, 최대값 및 평균을 찾을 수 있습니다.  
  
 **고유 값 가져오기**  
 `SELECT DISTINCT <column>FROM <model>`  
  
 이 문을 사용하여 불연속 열의 모든 값을 검색할 수 있습니다.  불연속화 열에 이 문을 사용하지 마십시오. 대신 `RangeMin` 및 `RangeMax` 함수를 사용해야 합니다.  
  
 **모델 또는 구조를 학습하는 데 사용된 사례 찾기**  
 `SELECT  FROM <mining structure.CASES WHERE IsTrainingCase()`  
  
 이 문을 사용하여 모델을 학습하는 데 사용된 전체 데이터 집합을 가져올 수 있습니다.  
  
 **모델 또는 구조를 테스트하는 데 사용되는 사례 찾기**  
 `SELECT  FROM <mining structure.CASES WHERE IsTestingCase()`  
  
 이 문을 사용하여 특정 구조와 관련된 마이닝 모델의 테스트를 위해 따로 설정된 데이터를 가져올 수 있습니다.  
  
 **특정 모델 패턴에서 기본 사례 데이터로 드릴스루**  
 `SELECT FROM <model>.CASESWHERE IsTrainingCase() AND IsInNode(<node>)`  
  
 이 문을 사용하여 학습된 모델에서 자세한 사례 데이터를 검색할 수 있습니다. 특정 노드를 지정해야 합니다. 예를 들어 클러스터, 의사 결정 트리의 특정 분기 등의 노드 ID를 알아야 합니다. 이뿐만 아니라 이 쿼리를 실행하려면 모델에 대한 드릴스루 권한이 있어야 합니다.  
  
###  <a name="queries-on-model-patterns-statistics-and-attributes"></a><a name="bkmk_Patterns"></a>모델 패턴, 통계 및 특성에 대 한 쿼리  
 데이터 마이닝 모델의 콘텐츠는 다양한 용도로 사용됩니다. 모델 내용 쿼리를 사용하여 다음을 수행할 수 있습니다.  
  
-   사용자 고유의 계산을 만들기 위해 수식 또는 확률 추출  
  
-   연결 모델의 경우 예측을 생성하는 데 사용되는 규칙 검색  
  
-   사용자 지정 애플리케이션에서 규칙을 사용할 수 있도록 특정 규칙에 대한 설명 검색  
  
-   시계열 모델에 의해 검색되는 이동 평균 보기  
  
-   추세 선의 일부 세그먼트에 대한 회귀 수식 구하기  
  
-   특정 클러스터의 일부로 식별되는 고객에 대한 동작 가능한 정보 검색  
  
 다음 예에서는 모델 콘텐츠에 대한 쿼리를 만들기 위한 일반적인 패턴을 보여 줍니다.  
  
 **모델에서 패턴 가져오기**  
 `SELECT FROM <model>.CONTENT`  
  
 이 문을 사용하여 모델의 특정 노드에 대한 자세한 정보를 검색할 수 있습니다. 알고리즘 유형에 따라 노드는 규칙과 수식, 지지도 및 분산 통계 등을 포함할 수 있습니다.  
  
 **훈련된 모델에 사용된 특성 검색**  
 `CALL System.GetModelAttributes(<model>)`  
  
 이 저장 프로시저를 사용하여 모델에 사용된 특성 목록을 검색할 수 있습니다. 예를 들어 이 정보는 기능 선택의 결과로 제거된 특성을 결정하는 데 유용합니다.  
  
 **데이터 마이닝 차원에 저장된 콘텐츠 검색**  
 `SELECT FROM <model>.DIMENSIONCONTENT`  
  
 이 문을 사용하여 데이터 마이닝 차원에서 데이터를 검색할 수 있습니다.  
  
 이 쿼리 유형은 주로 내부용입니다. 이 기능을 지원하지 않는 알고리즘도 있습니다. 지원 여부는 MINING_SERVICES 스키마 행 집합에 플래그로 표시됩니다.  
  
 사용자 고유의 플러그 인 알고리즘을 개발할 경우 이 문을 사용하여 테스트할 모델의 콘텐츠를 확인할 수 있습니다.  
  
 **모델의 PMML 표현 가져오기**  
 `SELECT * FROM <model>.PMML`  
  
 PMML 형식으로 모델을 표현하는 XML 문서를 가져옵니다. 일부 모델 유형은 지원되지 않습니다.  
  
##  <a name="examples"></a><a name="bkmk_Examples"></a> 예  
 일부 모델 콘텐츠는 모든 알고리즘에 적용되는 표준이지만, 콘텐츠의 일부 부분은 모델을 작성하는 데 사용한 알고리즘에 따라 크게 달라집니다. 따라서 내용 쿼리를 만들 때 특정 모델에 가장 유용한 정보를 알고 있어야 합니다.  
  
 선택한 알고리즘이 모델에 저장된 정보의 종류에 어떠한 영향을 미치는지를 보여 주는 몇 가지 예가 이 섹션에서 제공됩니다. 마이닝 모델 콘텐츠 및 각 모델 유형에 지정된 콘텐츠에 대한 자세한 내용은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)를 참조하세요.  
  
###  <a name="example-1-content-query-on-an-association-model"></a><a name="bkmk_Assoc"></a> 예 1: 연결 모델에 대한 내용 쿼리  
 `SELECT FROM <model>.CONTENT`문은 쿼리하는 모델의 유형에 따라 서로 다른 종류의 정보를 반환합니다. 연결 모델의 경우 주요 정보는 *노드 유형*입니다. 노드는 모델 콘텐츠의 정보에 대한 컨테이너와 같습니다. 연결 모델에서 규칙을 나타내는 노드에는 NODE_TYPE 값 8이 있지만 항목 집합을 나타내는 노드에는 NODE_TYPE 값 7이 있습니다.  
  
 따라서 다음 쿼리는 지지도 순으로 순위가 지정된(기본 순서) 상위 10개 항목 집합을 반환합니다.  
  
```  
SELECT TOP 10 NODE_DESCRIPTION, NODE_PROBABILITY, SUPPORT  
FROM <model>.CONTENT WHERE NODE_TYPE = 7  
```  
  
 다음 쿼리는 이 정보를 기반으로 합니다. 이 쿼리는 노드의 ID, 전체 규칙, 항목 집합의 오른쪽에 있는 제품 즉, 항목 집합의 일부로 서 일부 다른 제품과 연결 될 것으로 예측 되는 제품의 세 열을 반환 합니다.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME, NODE_DESCRIPTION,  
     (SELECT RIGHT(ATTRIBUTE_NAME, (LEN(ATTRIBUTE_NAME)-LEN('Association model name')))   
FROM NODE_DISTRIBUTION  
WHERE LEN(ATTRIBUTE_NAME)>2  
)   
AS RightSideProduct  
FROM [<Association model name>].CONTENT  
WHERE NODE_TYPE = 8   
ORDER BY NODE_SUPPORT DESC  
```  
  
 FLATTENED 키워드는 중첩 행 집합을 플랫 테이블로 변환해야 함을 나타냅니다. 규칙의 오른쪽에 있는 제품을 나타내는 특성은 NODE_DISTRIBUTION 테이블에 포함되어 있습니다. 따라서 길이가 2보다 커야 한다는 요구 사항을 추가하여 특성 이름을 포함하는 행만 검색합니다.  
  
 단순 문자열 함수는 세 번째 열에서 모델 이름을 제거하는 데 사용됩니다. 일반적으로 모델 이름은 중첩 열 값의 앞에 옵니다.  
  
 WHERE 절은 규칙만 검색하기 위해 NODE_TYPE 값을 8로 지정합니다.  
  
 자세한 내용은 [연결 모델 쿼리 예제](association-model-query-examples.md)를 참조하세요.  
  
###  <a name="example-2-content-query-on-a-decision-trees-model"></a><a name="bkmk_DecTree"></a> 예 2: 의사 결정 트리 모델에 대한 내용 쿼리  
 의사 결정 트리 모델은 예측뿐만 아니라 분류에도 사용할 수 있습니다.  이 예에서는 모델을 사용하여 결과를 예측한다고 가정하지만 결과를 분류하는 데 사용할 수 있는 요소나 규칙을 찾으려고 할 수도 있습니다.  
  
 의사 결정 트리 모델에서 노드는 트리 및 리프 노드를 나타내는 데 사용됩니다. 각 노드에 대한 캡션에는 결과 경로에 대한 설명이 포함되어 있습니다. 따라서 특정 결과에 대한 경로를 추적하려면 해당 결과가 포함된 노드를 식별하고 해당 노드에 대한 세부 정보를 얻어야 합니다.  
  
 다음 예와 같이 예측 쿼리에서 예측 함수 [PredictNodeId&#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)를 추가하여 관련 노드의 ID를 가져옵니다.  
  
```  
SELECT  Predict([Bike Buyer]), PredictNodeID([Bike Buyer])   
FROM [<decision tree model name>]  
PREDICTION JOIN   
<input rowset>   
```  
  
 결과가 포함된 노드의 ID가 있으면 다음과 같이 NODE_CAPTION을 포함하는 내용 쿼리를 만들어 예측에 대해 설명하는 규칙이나 경로를 검색할 수 있습니다.  
  
```  
SELECT NODE_CAPTION  
FROM [<decision tree model name>]   
WHERE NODE_UNIQUE_NAME= '<node id>'  
```  
  
 자세한 내용은 [의사 결정 트리 모델 쿼리 예제](decision-trees-model-query-examples.md)를 참조하세요.  
  
##  <a name="working-with-the-query-results"></a><a name="bkmk_Results"></a>쿼리 결과 작업  
 예에서 설명한 것처럼 내용 쿼리는 일반적으로 테이블 형식의 행 집합을 반환하지만, 중첩 열의 정보를 포함할 수도 있습니다. 반환되는 행 집합을 평면화할 수 있지만, 그러면 결과 작업이 더 복잡해질 수 있습니다. 특히 NODE_DISTRIBUTION 노드의 콘텐츠는 중첩되지만 모델에 대한 매우 유용한 정보를 포함합니다.  
  
 계층적 행 집합으로 작업하는 방법은 MSDN에서 OLEDB 사양을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [DMX Select 문 이해](/sql/dmx/understanding-the-dmx-select-statement)   
 [데이터 마이닝 쿼리](data-mining-queries.md)  
  
  
