---
title: 신경망 모델 찾아보기 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- mining model, neural network
- neural networks
- dependency network
ms.assetid: e4224cb7-115b-4889-ac07-03f096fb55fc
author: minewiskan
ms.author: owend
ms.openlocfilehash: e47f887425c2294785bd6e6624961727bf65eb17
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527733"
---
# <a name="browsing-a-neural-network-model"></a>신경망 모델 찾아보기
  **찾아보기**를 사용하여 신경망 또는 로지스틱 회귀 모델을 열면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 신경망 모델 뷰어와 비슷한 대화형 뷰어에 모델이 표시됩니다. 이 뷰어에서는 상관 관계를 탐색하고 모델 및 기본 데이터의 패턴에 대한 정보를 얻을 수 있습니다.

##  <a name="explore-the-model"></a><a name="BKMK_Tabs"></a>모델 탐색
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 신경망 또는 로지스틱 회귀 알고리즘을 기반으로 하는 모델은 알려진 입력과 출력 간의 연결 집합으로 데이터를 분석한다는 점에서 유사합니다. **찾아보기** 뷰어에서 다음과 같은 컨트롤을 사용하여 이러한 연결을 쉽게 탐색할 수 있습니다.

-   [변수](#BKMK_Variables)

-   [입력](#BKMK_Inputs)

-   [outputs](#BKMK_Outputs)

 이 뷰어를 시험해 보려는 경우 [분류 마법사&#40;Excel용 데이터 마이닝 추가 기능&#41;](classify-wizard-data-mining-add-ins-for-excel.md) 마법사를 사용하여 모델을 만들고 **고급** 옵션을 사용하여 **알고리즘 매개 변수** 대화 상자에서 Microsoft 로지스틱 회귀로 알고리즘을 변경할 수 있습니다.

###  <a name="variables"></a><a name="BKMK_Variables"></a>변수
 **변수** 창에는 모델에 미치는 영향의 순서로 입력 변수의 목록이 표시됩니다. **입력** 및 **출력** 컨트롤을 통해 모델을 필터링하여 표시되는 변수와 그 순서에 영향을 줄 수 있습니다.

 이 뷰어를 사용하면 고객이 자전거 구매자 범주와 비구매자 범주 중에서 어디에 속할 가능성이 큰지를 결정하는 데 가장 중요한 요인을 탐색할 수 있습니다.

 ![선택한 특성의 결과에 미치는 영향 테스트](media/dm13-neuralnet-agebuyer1.gif "선택한 특성의 결과에 미치는 영향 테스트")

##### <a name="explore-variables"></a>변수 탐색

1.  처음에 **변수** 창은 현재 필터에 따라 가장 중요한 특성의 순서대로 정렬됩니다. 막대의 길이는 요인의 강도를 나타냅니다.

     이 예에서는 소득이 가장 영향력 있는 요인이고 지역이 그 다음 요인임을 확인할 수 있습니다. 반면에 자동차를 여러 대 소유하고 자녀가 많은 고객은 자전거를 구입할 확률이 매우 낮습니다.

2.  **변수** 창에서 **특성**의 열 머리글을 클릭합니다.

     특성을 기준으로 정렬하면 각 입력 열에 대해 만들어진 bin을 확인할 수 있습니다. 직업과 같은 불연속 값이 포함된 열은 리터럴 값에 따라 *범주화*됩니다.

3.  **Age** 및 **Income**에 대해 발견된 값의 범위를 확인합니다.

     숫자인 입력 열이 있는 경우(즉, 데이터의 전체 열이 연속 숫자 데이터 형식임) 숫자가 불연속 범위로 버킷팅 또는 범주화됩니다.

     소득의 경우 78.4-154.06(가장 높은 소득 범위의 경우)과 같은 그룹으로 열이 세분화되었습니다.

     ![변수가 범주화되는 방식을 보기 위한 정렬](media/dm13-nn-bucketing-variables.gif "변수가 범주화되는 방식을 보기 위한 정렬")

     다른 그룹화를 원하는 경우 모델을 작성하기 전에 [레이블 재지정&#40;SQL Server 데이터 마이닝 추가 기능&#41;](relabel-sql-server-data-mining-add-ins.md) 도구나 Excel 함수를 사용하여 새로운 소득 범주를 만들어야 합니다.

4.  **유사성 있음**을 클릭하여 그래프를 기본 뷰로 복원합니다.

     기본적으로 뷰는 첫 번째 결과 값에 대한 **유사성** 값을 기준으로 정렬됩니다. **출력**에서 **값 1**과 **값 2**에 대한 새 값을 선택하여 첫 번째 및 두 번째 열에 할당되는 결과를 변경할 수 있습니다.

5.  차트에서 맨 위에 있는 색이 지정된 막대 위에 마우스를 놓습니다.

     *중요도* 점수, *확률* 점수 쌍 및 *리프트* 값 쌍이 포함된 도구 설명이 나타납니다.

    -   **중요도**는 전체 데이터 세트에서 계산되고 모든 입력이 제공된 경우에 대상 결과와 상관 관계가 가장 높은 특성을 식별합니다. 뷰어에서 중요도 점수를 기준으로 차트의 값이 정렬됩니다.

    -   **확률**은 전체 데이터 집합에서 대상 결과에 대한 특성-값 쌍의 각 집합에 대해 계산됩니다.

    -   **리프트**는 이 특정한 특성-값 쌍이 한 결과나 다른 결과를 촉진하는 데 얼마나 유용한지를 알려 줍니다.

     참고: 마우스를 어느 열에 놓든 간에 도구 설명에는 동일한 정보가 포함됩니다.

 [맨 위로 이동](#BKMK_Tabs)

###  <a name="inputs"></a><a name="BKMK_Inputs"></a>내용
 **입력** 창에서 일련의 입력을 선택하여 모델에 필터로 적용할 수 있으며, 이를 통해 학습 데이터를 기반으로 결과에 대한 해당 선택의 영향을 확인할 수 있습니다.

##### <a name="explore-inputs"></a>입력 탐색

1.  특정 그룹을 대상으로 한다고 가정하고 해당 그룹에서 구매에 가장 큰 영향을 미치는 요인을 확인합니다.

     **입력** 창에서 **\<All>** **특성**아래의 셀을 클릭 하 고 **Age**를 선택 합니다.

     **값**에 대해 가장 어린 연령 범주를 선택합니다.

2.  특정 연령 그룹에 대해 필터링하는 경우에도 태평양 지역은 목록 위쪽에 옵니다. 이는 태평양 지역의 고객이 다른 지역의 고객보다 자전거를 구매할 확률이 훨씬 크기 때문입니다.

     지역이 영향을 미칠 수 있는 요인이 아니므로 이 변수를 고려 대상에서 제거하고 다른 요인을 보기 위해 입력을 다시 변경할 수 있습니다.

     **입력** 창에서 **Age** 아래의 빈 셀을 클릭하고 **Region**을 선택합니다.

     **값**에 대해 **Europe**을 선택합니다.

3.  입력 필터를 계속 추가하여 관심이 있는 그룹에 초점을 맞춥니다.

     예를 들어 입력 특성에 대해 **Gender**를 추가하고 **Female**을 값으로 선택합니다.

     ![선택한 특성의 결과에 미치는 영향 테스트](media/dm13-neuralnet-agebuyer2.gif "선택한 특성의 결과에 미치는 영향 테스트")

     변수 목록이 어떻게 변경되는지 확인합니다. 이제 **Income**이 대상 결과를 예측하는 데 가장 중요한 변수입니다.

     입력 필터를 적용하는 순서는 결과에 영향을 미치지 않습니다.

 [맨 위로 이동](#BKMK_Tabs)

###  <a name="outputs"></a><a name="BKMK_Outputs"></a>출력
 **출력** 창에서 관심이 있는 결과를 선택할 수 있습니다. 신경망을 사용하면 결과 열을 원하는 만큼 지정할 수 있지만, 결과를 더 추가하면 모델이 복잡해지고 처리 시간이 훨씬 오래 걸릴 수 있습니다.

 두 출력을 비교하려면 해당 출력이 **예측** 또는 **예측만** 열로 지정되어 있어야 합니다.

##### <a name="explore-outputs"></a>출력 탐색

1.  **출력 특성** 목록을 사용하여 특성을 선택합니다.

2.  값 1 및 값 2 목록에서 두 결과를 선택합니다. 출력 특성의 이러한 두 가지 상태는 **변수** 창에서 비교됩니다.

 [맨 위로 이동](#BKMK_Tabs)

## <a name="more-about-neural-network-models"></a>신경망 모델에 대한 추가 정보
 뷰어의 정보는 이 모델 유형과 관련된 저장 프로시저인 System.Microsoft.AnalysisServices.System.DataMining.NeuralNet.GetAttributeScores를 사용하여 서버에서 검색됩니다.

 추가 기능을 사용하여 예측 가능한 여러 특성으로 모델을 만들려면 **고급** 모델링 옵션을 사용합니다.

 자세한 내용은 [마이닝 구조 만들기&#40;SQL Server 데이터 마이닝 추가 기능&#41;](create-mining-structure-sql-server-data-mining-add-ins.md) 및 [구조에 모델 추가&#40;Excel용 데이터 마이닝 추가 기능&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)를 참조하세요.

## <a name="see-also"></a>참고 항목
 [Excel &#40;SQL Server 데이터 마이닝 추가 기능을 검색 하는 모델&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)


