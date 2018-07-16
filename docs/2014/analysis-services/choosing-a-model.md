---
title: 모델 선택 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data mining algorithms
- mining models
- mining structures
- data mining models
- data mining structures
ms.assetid: 444bbf9c-cec8-460e-881d-38784fb146fa
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9817f7e8906d9e75f7c2b5d55db679d77e7cc47e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273889"
---
# <a name="choosing-a-model"></a>모델 선택
  **마이닝 알고리즘:** 데이터 마이닝 *알고리즘* 데이터에서 패턴을 만드는 메커니즘입니다. 알고리즘은 데이터의 수를 세는 방법, 관계가 파생되는 방법 및 패턴을 저장하는 방법을 정의합니다. 분석할 데이터의 형식에 따라 선택할 알고리즘이 어느 정도는 달라집니다. 예를 들어 연속 숫자에서만 작동하는 알고리즘이 있는 반면 제한된 수의 고유 값에서 최상의 성능을 제공하는 알고리즘이 있습니다.  
  
 **마이닝 모델:** 에 저장 된 알고리즘에 의해 데이터 분석의 결과 *마이닝 모델*합니다. 마이닝 모델은 규칙, 통계 및 패턴의 컬렉션입니다. 합니다 *콘텐츠* 마이닝 모델의 데이터를 처리 하는 데 사용 되지만 다음을 포함할 수 있습니다 하는 알고리즘에 따라 다릅니다.  
  
-   트랜잭션에서 제품이 그룹화되는 방법을 설명하는 if-then 규칙  
  
-   결과로 이어지는 경로를 추적하는 의사 결정 트리와 각 경로의 발생 가능 확률  
  
-   모델 전체 또는 일부에 대한 수식이 포함된 수학적 모델  
  
-   유사한 항목의 컬렉션 (호출 *클러스터* 또는 *세그먼트*) 공유 되는 특성 및 유사성 점수를 기준 정의 되어 있습니다.  
  
-   *노드* 하 여 연결 된 네트워크에서 *가장자리*합니다. 노드는 항목 또는 항목 그룹을 나타냅니다. 가장자리는 노드 간 관계의 강도에 따라 점수가 부여됩니다.  
  
 **모델을 사용 하 여:** 모델을 만든, 제공된 된 뷰어를 사용 하 여 탐색을 하거나 모델에 대 한 쿼리를 만들 수 있습니다. 쿼리는 다음 작업을 수행하는 데 사용할 수 있습니다.  
  
-   미래 가치를 예측합니다.  
  
-   관련 제품 또는 권장 제품 집합을 생성합니다.  
  
-   모델의 규칙, 패턴 또는 수식을 반환합니다.  
  
-   모델에서 메타데이터를 가져옵니다.  
  
-   모든 예측 또는 일부 예측의 확률 및 지지도 값을 제공합니다.  
  
## <a name="types-of-machine-learning-algorithms"></a>시스템 학습 알고리즘 유형  
 알고리즘 유형에 따라 데이터가 다르게 사용되므로 모델을 만들 때는 목표와 분석하려는 데이터에 적합한 알고리즘을 선택해야 합니다.  
  
 Excel용 데이터 마이닝 추가 기능에는 다음과 같이 다양한 알고리즘 유형이 포함됩니다.  
  
-   *분류 알고리즘*합니다.  
  
     데이터 집합의 다른 특성을 기반으로 하나 이상의 불연속 변수를 예측합니다.  
  
-   *회귀 알고리즘*  
  
     데이터 집합의 다른 특성을 기반으로 수익 또는 손실과 같은 하나 이상의 연속 변수를 예측합니다.  
  
-   *세그먼트화 알고리즘*  
  
     데이터를 속성이 유사한 항목의 그룹 또는 클러스터로 나눕니다.  
  
-   *연결 알고리즘*  
  
     데이터 집합에 있는 여러 특성 사이의 상관 관계를 찾습니다. 이러한 종류의 알고리즘은 연결 규칙을 만드는 데 가장 일반적으로 사용됩니다. 연결 규칙은 시장 바구니 분석에 사용할 수 있습니다.  
  
-   *시퀀스 분석 알고리즘*  
  
     웹 사이트를 탐색하는 동안 사용자가 따라가는 경로와 같이 데이터에서 자주 사용하는 시퀀스 또는 에피소드를 요약합니다.  
  
 Office용 SQL Server 데이터 마이닝 추가 기능에서 사용하는 알고리즘은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 제공하는 알고리즘을 기반으로 합니다. 경우에 OLE DB for Data Mining 사양 준수 하는 타사 알고리즘을 사용할 수 있습니다 인스턴스의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 연결 되는 타사 알고리즘을 허용 하도록 구성 된 했습니다.  
  
## <a name="requirements"></a>요구 사항  
 각 알고리즘은 작업할 수 있는 데이터의 종류에 따라 다릅니다.  
  
-   선형 회귀 모델은 숫자 값만 모델링할 수 있습니다. 입력 변수와 대상 결과가 모두 연속 숫자 형식이어야 합니다. 불연속 변수와 연속 변수를 함께 사용해야 할 경우 의사 결정 트리 또는 예측 모델을 사용하십시오.  
  
-   Naïve Bayes 모델을 사용하려면 모든 숫자를 범주화해야 합니다. 이 알고리즘을 기반으로 한 마법사 중 하나를 사용할 경우 범주화가 자동으로 수행됩니다.  
  
-   의사 결정 트리 모델은 불연속 변수와 연속 변수를 모두 포함할 수 있습니다. 하지만 트리에서 분할이 필요한 경우에는 숫자가 자동으로 범주화됩니다.  
  
-   신경망 및 로지스틱 회귀 모델은 결과 또는 입력 변수로 사용되는 숫자를 자동으로 범주화합니다. 다른 기준에 따라 숫자를 그룹화하려는 경우 모델링 전에 레이블 재지정 도구를 사용하여 그룹화를 만들어야 합니다. 예를 들어, 하려는 값을 그룹화를 **Age** (예로 35.6-41.8 수 있음) 모델에서 발견 하는 통계적으로 중요 한 그룹화 하지 않고 (10-20, 21 ~ 30 및에 따라서) 분 위 수, 열입니다.  
  
-   연결 모델을 사용하려면 각각 여러 항목 또는 행을 참조하는 트랜잭션으로 데이터를 그룹화해야 합니다. 사용 중인 경우는 [연결 마법사 &#40;Excel 용 데이터 마이닝 클라이언트&#41; ](associate-wizard-data-mining-client-for-excel.md) 마법사와 [시장 바구니 분석 &#40;Excel 용 테이블 분석 도구&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) 도구를 데이터 에 표시 된 대로 배치 해야 합니다 **연결** 샘플 통합 문서 탭 합니다.  
  
     외부 데이터 원본에서 중첩된 테이블을 사용 하려는 경우 사용 해야 합니다 [고급 모델링 &#40;Excel 용 데이터 마이닝 추가 기능&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md) 서버에 저장 되는 마이닝 모델과 마이닝 구조를 만드는 옵션을 모델링 합니다. Excel에서는 중첩 테이블을 지원하지 않습니다.  
  
## <a name="feature-selection"></a>기능 선택  
 데이터 집합에 따라 알고리즘 적용 될 수 있습니다 *기능 선택*, 유용 하지 않은 열을 제거 하는 데 결과 관련 하 여 통계적으로 중요 한 데이터 열을 확인 합니다.  
  
 각 알고리즘은 약간씩 다른 기능 선택 방법(예: entropy 또는 다양한 정보 점수)을 사용하여 중요한 추세와 무시할 수 있는 차이점을 결정합니다.  
  
 Excel용 데이터 마이닝 추가 기능에서는 각 알고리즘에 적합한 점수 매기기 방법을 사용하여 기능 선택이 자동으로 적용됩니다. 기능 선택 결과 변경 하려는 경우에 마법사를 사용 합니다 **데이터 마이닝** 리본을 클릭 **고급** 를 사용 하 여 매개 변수를 설정 하는 **알고리즘 매개 변수**대화 상자.  
  
 기능 선택 목록은 각 알고리즘에서 사용 하는 방법에 항목을 참조 [기능 선택 &#40;데이터 마이닝&#41; ](data-mining/feature-selection-data-mining.md) SQL Server 온라인 설명서의 합니다.  
  
## <a name="list-of-supported-algorithms"></a>지원되는 알고리즘 목록  
 다음은 기본적으로 제공되는 알고리즘입니다.  
  
|알고리즘 이름|Description|사용 대상|  
|--------------------|-----------------|-------------|  
|Microsoft 연결 규칙|트랜잭션 내에 함께 나타날 가능성이 높은 항목을 설명하는 규칙을 작성합니다.|[연결 마법사 &#40;Excel 용 데이터 마이닝 클라이언트&#41;](associate-wizard-data-mining-client-for-excel.md)<br /><br /> [시장 바구니 분석 &#40;Excel 테이블 분석 도구&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)|  
|Microsoft 클러스터링|일시적인 관찰만으로는 논리적으로 이끌어 내지 못할 수 있는 데이터 집합 내 관계를 식별합니다. 반복 기술을 사용하여 비슷한 특징을 가진 클러스터로 레코드를 그룹화합니다.|[범주 검색 &#40;Excel 용 테이블 분석 도구&#41;](detect-categories-table-analysis-tools-for-excel.md)<br /><br /> [클러스터 마법사 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft 의사 결정 트리|데이터 집합에 있는 열 간의 관계를 기반으로 예측을 수행하고 관계를 특정 값에 대한 트리와 비슷한 분할 집합으로 모델링합니다.<br /><br /> 불연속 및 연속 특성에 대한 예측을 모두 지원합니다.|[분류 마법사 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](classify-wizard-data-mining-add-ins-for-excel.md)<br /><br /> [추정 마법사 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft 선형 회귀|대상 변수 및 검사하는 변수 간에 선형 종속성이 있는 경우 대상 및 해당 입력 간의 가장 효과적인 관계를 찾습니다.<br /><br /> 연속 특성 예측을 지원합니다.|이 알고리즘은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 사용할 수 있습니다. Office용 데이터 마이닝 추가 기능에서 구조를 만든 후 직접 모델을 추가하여 이 알고리즘을 사용하는 모델을 만들 수 있습니다.<br /><br /> 자세한 내용은 [고급 모델링 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)합니다.|  
|Microsoft 로지스틱 회귀|결과에 영향을 주는 요인을 분석합니다. 여기에서 결과는 일반적으로 이벤트가 발생함 또는 발생하지 않음의 두 값으로 제한됩니다.<br /><br /> 불연속 및 연속 특성에 대한 예측을 모두 지원합니다.|[예제에서 입력 &#40;Excel 용 테이블 분석 도구&#41;](fill-from-example-table-analysis-tools-for-excel.md)<br /><br /> [목표 검색 시나리오 &#40;Excel 용 테이블 분석 도구&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)<br /><br /> [가상 시나리오 &#40;Excel 용 테이블 분석 도구&#41;](what-if-scenario-table-analysis-tools-for-excel.md)<br /><br /> [예측 계산기 &#40;Excel 용 테이블 분석 도구&#41;](prediction-calculator-table-analysis-tools-for-excel.md)|  
|Microsoft Naïve Bayes|모든 입력 및 예측 가능 열 간의 관계에 대한 확률을 찾습니다. 이 알고리즘은 관계를 검색하는 마이닝 모델을 신속하게 생성하는 데 유용합니다.<br /><br /> 불연속 또는 불연속화 특성만 지원합니다.<br /><br /> 모든 입력 특성을 독립적인 것으로 취급합니다.|[주요 영향 요인 분석 &#40;Excel 용 테이블 분석 도구&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)|  
|Microsoft 신경망|복잡한 입력 데이터를 분석하거나 상당한 양의 학습 데이터가 있지만 다른 알고리즘으로 쉽게 규칙을 이끌어 낼 수 없는 비즈니스 문제를 분석합니다.<br /><br /> 여러 특성을 예측할 수 있습니다.<br /><br /> 불연속 특성 및 연속 특성의 회귀를 분류하는 데 사용할 수 있습니다.|이 알고리즘은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 사용할 수 있습니다. Office용 데이터 마이닝 추가 기능에서 구조를 만든 후 직접 모델을 추가하여 이 알고리즘을 사용하는 모델을 만들 수 있습니다.<br /><br /> 자세한 내용은 [고급 모델링 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)합니다.|  
|Microsoft 시퀀스 클러스터링|시퀀스에서 비슷한 순서로 정렬된 이벤트의 클러스터를 식별합니다.<br /><br /> 시퀀스 분석과 클러스터링의 조합을 제공합니다.|이 알고리즘은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서만 사용할 수 있습니다. 하지만 Office용 데이터 마이닝 추가 기능에서 구조를 만든 후 직접 모델을 추가하여 이 알고리즘을 사용하는 모델을 만들 수 있습니다.<br /><br /> 자세한 내용은 [고급 모델링 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)합니다.|  
|Microsoft 시계열|선형 의사 결정 트리를 사용하여 시간 관련 데이터를 분석합니다.<br /><br /> 시계열에서 미래의 값을 예측하는 데 패턴을 사용할 수 있습니다.|[예측 &#40;Excel 용 테이블 분석 도구&#41;](forecast-table-analysis-tools-for-excel.md)<br /><br /> [예측 마법사 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Office용 데이터 마이닝 추가 기능에 포함된 항목](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
