---
title: 신경망 구조 및 모델 만들기 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- DISCRETIZED column
- DiscretizationBuckets property
- DiscretizationMethod property
- EQUAL_AREAS method
ms.assetid: 3f16215c-531e-4ecf-a11f-ee7c6a764463
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6787db165770f944838a312ecd3e0386d161da38
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62856321"
---
# <a name="creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial"></a>신경망 구조 및 모델 만들기(중급 데이터 마이닝 자습서)
  데이터 마이닝 모델을 만들려면 먼저 데이터 마이닝 마법사를 사용하여 새 데이터 원본 뷰를 기반으로 새 마이닝 구조를 만들어야 합니다. 이 태스크에서는 마법사를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] 신경망 알고리즘 기반의 마이닝 구조를 만들고 이와 동시에 관련 마이닝 모델을 만듭니다.  
  
 신경망은 매우 유연하고 많은 입력 및 출력 조합을 분석할 수 있기 때문에 최상의 결과를 얻기 위해 여러 가지 데이터 처리 방법을 시험해야 합니다. 예를 들어 특정 비즈니스 요구 사항을 대상으로 지정 하기 위해 서비스 품질에 대 한 숫자 대상을 범주화 하거나 그룹화 *하는 방법을*사용자 지정할 수 있습니다. 이렇게 하려면 숫자 데이터를 다른 방식으로 그룹화하는 새 열을 마이닝 구조에 추가한 다음 새 열을 사용하는 모델을 만듭니다. 이러한 마이닝 모델을 사용하여 탐색을 수행합니다.  
  
 마지막으로, 신경망 모델을 통해 비즈니스 질문에 가장 큰 영향을 주는 요인을 찾았으면 예측 및 평가에 사용할 별도의 모델을 만들어야 합니다. 여기서는 신경망 모델에 기반을 두지만 특정 입력을 바탕으로 솔루션을 찾도록 최적화된 [!INCLUDE[msCoName](../includes/msconame-md.md)] 로지스틱 회귀 알고리즘을 사용합니다.  
  
 **단계**  
  
 [기본 마이닝 구조 및 모델 만들기](#bkmk_defaul)  
  
 [분할을 사용하여 예측 가능한 열 범주화](#bkmk_ColumnCopy)  
  
 [열을 복사하고 다른 모델에 대한 분할 메서드 변경](#bkmk_Alias)  
  
 [모델을 비교할 수 있도록 예측 가능한 열에 대한 별칭 만들기](#bkmk_Alias2)  
  
 [모든 모델 처리](#bkmk_SeedProcess)  
  
## <a name="create-the-default-call-center-structure"></a>기본 콜 센터 구조 만들기<a name="bkmk_defaul"></a>  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]솔루션 탐색기에서 **마이닝 구조** 를 마우스 오른쪽 단추로 클릭 하 고 **새 마이닝 구조**를 선택 합니다.  
  
2.  **데이터 마이닝 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **정의 방법 선택** 페이지에서 **기존 관계형 데이터베이스 또는 데이터 웨어하우스** 를 선택 했는지 확인 하 고 **다음**을 클릭 합니다.  
  
4.  **데이터 마이닝 구조 만들기** 페이지에서 **마이닝 모델을 사용 하 여 마이닝 구조 만들기** 옵션이 선택 되어 있는지 확인 합니다.  
  
5.  **사용할 데이터 마이닝 기술 선택** 옵션에 대한 드롭다운 목록을 클릭한 다음 **Microsoft 신경망**을 선택합니다.  
  
     로지스틱 회귀 모델이 신경망을 기반으로 하기 때문에 동일한 구조를 다시 사용하여 새 마이닝 모델을 추가할 수 있습니다.  
  
6.  **다음**을 클릭합니다.  
  
     **데이터 원본 뷰 선택** 페이지가 나타납니다.  
  
7.  **사용 가능한 데이터 원본 뷰**에서을 `Call Center`선택 하 고 **다음**을 클릭 합니다.  
  
8.  **테이블 유형 지정** 페이지에서 **FactCallCenter** 테이블 옆의 **사례** 확인란을 선택 합니다. 나이 **날짜**에는 아무것도 선택 하지 마십시오. **다음**을 클릭합니다.  
  
9. **학습 데이터 지정** 페이지에서 FactCallCenterID 열 옆에 있는 **키** 를 선택 합니다 **.**  
  
10. `Predict` 및 **입력** 확인란을 선택 합니다.  
  
11. 다음 표와 같이 **키**, **입력**및 `Predict` 확인란을 선택 합니다.  
  
    |테이블/열|키/입력/예측|  
    |---------------------|-------------------------|  
    |AutomaticResponses|입력|  
    |AverageTimePerIssue|입력/예측|  
    |Calls|입력|  
    |DateKey|사용 안 함|  
    |DayOfWeek|입력|  
    |FactCallCenterID|Key|  
    |IssuesRaised|입력|  
    |LevelOneOperators|입력/예측|  
    |LevelTwoOperators|입력|  
    |Orders|입력/예측|  
    |ServiceGrade|입력/예측|  
    |Shift|입력|  
    |TotalOperators|사용 안 함|  
    |WageType|입력|  
  
     여러 개의 예측 가능한 열이 선택되었습니다. 신경망 알고리즘의 강점 중 하나는 입력 및 출력 특성의 가능한 모든 조합을 분석할 수 있다는 것입니다. 대량 데이터 집합에 대해이 작업을 수행 하지 않는 것이 좋습니다 .이 경우 처리 시간이 크게 늘어날 수 있습니다.  
  
12. **열 내용 및 데이터 형식 지정** 페이지에서 다음 표와 같이 표에 열, 내용 유형 및 데이터 형식이 포함 되어 있는지 확인 한 **후 다음을 클릭 합니다**.  
  
    |열|콘텐츠 형식|데이터 형식|  
    |-------------|------------------|----------------|  
    |AutomaticResponses|연속|long|  
    |AverageTimePerIssue|연속|long|  
    |Calls|연속|long|  
    |DayOfWeek|불연속|텍스트|  
    |FactCallCenterID|Key|long|  
    |IssuesRaised|연속|long|  
    |LevelOneOperators|연속|long|  
    |LevelTwoOperators|연속|long|  
    |Orders|연속|long|  
    |ServiceGrade|연속|Double|  
    |Shift|불연속|텍스트|  
    |WageType|불연속|텍스트|  
  
13. **테스트 집합 만들기** 페이지에서 **테스트용 데이터 비율**옵션에 대 한 텍스트 상자의 선택을 취소 합니다. **다음**을 클릭합니다.  
  
14. **마법사 완료** 페이지에서 **마이닝 구조 이름**에을 입력 `Call Center`합니다.  
  
15. **마이닝 모델 이름**에를 입력 `Call Center Default NN`한 다음 **마침**을 클릭 합니다.  
  
     신경망 모델을 사용 하 여 데이터로 드릴스루할 수 없으므로 **드릴스루 허용** 상자를 사용할 수 없습니다.  
  
16. 솔루션 탐색기에서 방금 만든 데이터 마이닝 구조의 이름을 마우스 오른쪽 단추로 클릭 하 고 **처리**를 선택 합니다.  
  
## <a name="use-discretization-to-bin-the-target-column"></a>분할을 사용하여 대상 열 범주화  
 기본적으로 예측 가능한 숫자 특성을 포함하는 신경망 모델을 만들 때 Microsoft 신경망 알고리즘은 특성을 연속 숫자로 처리합니다. 예를 들어 ServiceGrade 특성은 이론상으로 0.00(모든 호출이 응답됨)에서 1.00(모든 호출자가 호출을 중단함)에 이르는 숫자입니다. 이 데이터 집합의 경우 값이 다음과 같이 분포됩니다.  
  
 ![서비스 등급 값 분포](../../2014/tutorials/media/skt-service-grade-valuesc.gif "서비스 등급 값 분포")  
  
 따라서 모델을 처리할 때 출력이 예상과 다르게 그룹화될 수 있습니다. 예를 들어 클러스터링을 사용 하 여 가장 적합 한 값 그룹을 식별 하는 경우 알고리즘은 ServiceGrade의 값을 0.0748051948-0.09716216215와 같은 범위로 나눕니다. 이 그룹화가 수학적으로 정확하기는 하지만 비즈니스 사용자에게는 이러한 범위가 의미가 없을 수 있습니다.  
  
 이 단계에서는 결과를 보다 직관적으로 만들기 위해 숫자 값을 다르게 그룹화 하 여 숫자 데이터 열의 복사본을 만듭니다.  
  
### <a name="how-discretization-works"></a>분할 작동 방법  
 Analysis Services에서는 숫자 데이터를 범주화하거나 처리하는 다양한 방법을 제공합니다. 다음 표에서는 출력 특성 ServiceGrade를 세 가지 방식으로 처리했을 때 결과의 차이를 보여 줍니다.  
  
-   연속 숫자로 처리합니다.  
  
-   알고리즘이 클러스터링을 사용하여 최적의 값 배열을 식별하도록 지정합니다.  
  
-   Equal Areas 메서드를 사용하여 숫자를 범주화하도록 지정합니다.  
  
 기본 모델(연속)  
  
|값|별칭|  
|-----------|-------------|  
|Missing|0|  
|0.09875|120|  
  
 클러스터링에 의한 범주화  
  
|값|별칭|  
|-----------|-------------|  
|\<0.0748051948|34|  
|0.0748051948-0.09716216215|27|  
|0.09716216215 - 0.13297297295|39|  
|0.13297297295 - 0.167499999975|10|  
|>= 0.167499999975|10|  
  
 Equal Areas에 의한 범주화  
  
|값|별칭|  
|-----------|-------------|  
|\<0.07|26|  
|0.07-0.00|22|  
|0.09-0.11|36|  
|>= 0.12|36|  
  
> [!NOTE]  
>  이러한 통계는 모든 데이터를 처리한 후 모델의 한계 통계 노드에서 가져올 수 있습니다. 한계 통계 노드에 대 한 자세한 내용은 [Analysis Services 데이터 마이닝&#41;&#40;신경망 모델에 대 한 마이닝 모델 콘텐츠 ](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)를 참조 하세요.  
  
 이 테이블에서 VALUE 열은 ServiceGrade 수가 어떻게 처리되었는지를 보여 줍니다. SUPPORT 열은 해당 값을 갖고 있거나 해당 범위에 속한 사례 수를 보여 줍니다.  
  
-   **연속 숫자 사용(기본값)**  
  
     기본 메서드를 사용한 경우 알고리즘은 평균 값이 0.09875인 고유 값 120에 대한 결과를 컴퓨팅합니다. 또한 누락된 값의 개수도 알 수 있습니다.  
  
-   **클러스터링에 의한 범주화**  
  
     Microsoft 클러스터링 알고리즘에서 선택 사항인 값의 그룹화를 결정하도록 한 경우, 알고리즘은 ServiceGrade에 대한 값을 다섯 개의 범위로 그룹화합니다. SUPPORT 열로부터 알 수 있듯, 각 범위의 사례 수는 고르게 분산되어 있지 않습니다.  
  
-   **Equal Areas에 의한 범주화**  
  
     이 메서드를 선택한 경우 알고리즘은 동일한 크기의 버킷에 값을 강제로 집어넣어 결과적으로 각 범위의 상한 및 하한이 변경됩니다. 버킷 수를 지정할 수는 있지만 버킷에 너무 적은 수의 값이 포함되지 않도록 하는 것이 좋습니다.  
  
 범주화 옵션에 대 한 자세한 내용은 [데이터 마이닝&#41;&#40;분할 방법 ](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md)을 참조 하세요.  
  
 또는 숫자 값을 사용 하는 것이 아니라 서비스 등급을 미리 정의 된 대상 범위로 분류 하는 별도의 파생 열을 추가할 수 **Best** 있습니다 (예: \<Best (servicegrade = 0.05), **허용** 가능 (0.10 > Servicegrade > 0.05) 및 **나쁨** (servicegrade >= 0.10).  
  
###  <a name="create-a-copy-of-a-column-and-change-the-discretization-method"></a><a name="bkmk_newColumn"></a>열의 복사본을 만들고 분할 메서드를 변경 합니다.  
 대상 특성인 ServiceGrade를 포함 하는 마이닝 열의 복사본을 만들고 숫자를 그룹화 하는 방법을 변경 합니다. 예측 가능한 특성을 비롯하여 임의의 열의 여러 복사본을 마이닝 구조에서 만들 수 있습니다.  
  
 이 자습서에서는 Equal Areas 분할 메서드를 사용하고 4개의 버킷을 지정합니다. 이 메서드에서 생성되는 그룹화는 비즈니스 사용자가 관심을 가지는 대상 값에 매우 근접해 있습니다.  
  
####  <a name="to-create-a-customized-copy-of-a-column-in-the-mining-structure"></a><a name="bkmk_ColumnCopy"></a>마이닝 구조에 열에 대 한 사용자 지정 복사본을 만들려면  
  
1.  솔루션 탐색기에서 앞에서 만든 마이닝 구조를 두 번 클릭합니다.  
  
2.  마이닝 구조 탭에서 **마이닝 구조 열 추가**를 클릭 합니다.  
  
3.  **열 선택** 대화 상자의 **원본 열**목록에서 servicegrade를 선택 하 고 **확인**을 클릭 합니다.  
  
     새 열이 마이닝 구조 열의 목록에 추가됩니다. 기본적으로 새 마이닝 열의 이름은 기존 열의 이름과 같으며 ServiceGrade 1과 같이 뒤에 숫자가 붙습니다. 이 열의 이름을 좀 더 구체적인 이름으로 변경할 수 있습니다.  
  
     분할 메서드도 지정합니다.  
  
4.  ServiceGrade 1을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.  
  
5.  **속성** 창에서 **이름** 속성을 찾아 이름을 **서비스 등급** 에 맞게 변경 합니다.  
  
6.  관련된 모든 마이닝 모델 열의 이름을 동일하게 변경할 것인지 묻는 대화 상자가 나타납니다. **아니요**를 클릭합니다.  
  
7.  **속성** 창에서 섹션 **데이터 형식을** 찾고 필요한 경우 확장 합니다.  
  
8.  `Content` 속성의 값을 `Continuous`에서 `Discretized`로 변경합니다.  
  
     이제 사용할 수 있는 속성은 다음과 같습니다. 다음 표에 있는 대로 속성 값을 변경합니다.  
  
    |속성|기본값|새 값|  
    |--------------|-------------------|---------------|  
    |`DiscretizationMethod`|`Continuous`|`EqualAreas`|  
    |`DiscretizationBucketCount`|값 없음|4|  
  
    > [!NOTE]  
    >  <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>의 기본값은 0이며, 이는 알고리즘이 자동으로 최적의 버킷 수를 결정함을 의미합니다. 따라서 이 속성 값을 기본값으로 다시 설정하려면 0을 입력합니다.  
  
9. 데이터 마이닝 디자이너에서 **마이닝 모델** 탭을 클릭 합니다.  
  
     마이닝 구조 열의 복사본을 추가할 때 복사본의 사용법 플래그가 자동으로 `Ignore`로 설정됩니다. 일반적으로 열의 복사본을 마이닝 구조에 추가할 때 원래 열과 함께 분석용 복사본을 사용하지 않습니다. 복사본을 사용하면 알고리즘에서 두 열의 강한 상관 관계를 발견하므로 다른 관계가 명확하게 드러나지 않을 수도 있습니다.  
  
##  <a name="add-a-new-mining-model-to-the-mining-structure"></a><a name="bkmk_NewModel"></a>마이닝 구조에 새 마이닝 모델 추가  
 대상 특성의 새로운 그룹화 방식을 만들었으므로 분할 열을 사용하는 새 마이닝 모델을 추가해야 합니다. 완료하면 CallCenter 마이닝 구조에 두 가지 마이닝 모델이 포함됩니다.  
  
-   Call Center Default NN 마이닝 모델은 ServiceGrade 값을 연속 범위로 처리합니다.  
  
-   동일한 크기의 네 버킷으로 분산 된 ServiceGrade 열의 값을 대상으로 하는 것으로를 사용 하는 새 마이닝 모델 인 Call Center는 새 마이닝 모델을 만듭니다.  
  
#### <a name="to-add-a-mining-model-based-on-the-new-discretized-column"></a>새로운 불연속화 열 기반의 마이닝 모델을 추가하려면  
  
1.  솔루션 탐색기에서 방금 만든 마이닝 구조를 마우스 오른쪽 단추로 클릭 하 고 **열기**를 선택 합니다.  
  
2.  **마이닝 모델** 탭을 클릭합니다.  
  
3.  **관련 마이닝 모델 만들기를**클릭 합니다.  
  
4.  **새 마이닝 모델** 대화 상자의 **모델 이름**에을 입력 `Call Center Binned NN`합니다. **알고리즘 이름** 드롭다운 목록에서 **Microsoft 신경망**을 선택 합니다.  
  
5.  새 마이닝 모델에 포함된 열의 목록에서 ServiceGrade를 찾고 사용법을 `Predict`에서 `Ignore`로 변경합니다.  
  
6.  이와 마찬가지로 ServiceGrade Binned를 찾고 사용법을 `Ignore`에서 `Predict`로 변경합니다.  
  
##  <a name="create-an-alias-for-the-target-column"></a><a name="bkmk_Alias2"></a>대상 열에 대 한 별칭 만들기  
 일반적으로 예측 가능한 여러 특성을 사용하는 마이닝 모델은 비교할 수 없습니다. 그러나 마이닝 모델 열의 별칭을 만들 수는 있습니다. 즉, 마이닝 모델 내에서 원본 열과 동일한 이름을 갖도록 ServiceGrade 열의 이름을 바꿀 수 있습니다. 이렇게 한 다음 데이터가 다르게 분할된 경우에도 정확도 차트에서 이러한 두 모델을 직접 비교할 수 있습니다.  
  
###  <a name="to-add-an-alias-for-a-mining-structure-column-in-a-mining-model"></a><a name="bkmk_Alias"></a>마이닝 모델의 마이닝 구조 열에 대 한 별칭을 추가 하려면  
  
1.  **마이닝 모델** 탭의 **구조**에서 servicegrade 범주화를 선택 합니다.  
  
     **속성** 창에는 ScalarMiningStructure column 개체의 속성이 표시 됩니다.  
  
2.  ServiceGrade Binned NN 마이닝 모델의 열 아래에서 ServiceGrade Binned 열에 해당하는 셀을 클릭합니다.  
  
     이제 **속성** 창에 MiningModelColumn 개체의 속성이 표시 됩니다.  
  
3.  **Name** 속성을 찾고 값을로 `ServiceGrade`변경 합니다.  
  
4.  **설명** 속성을 찾고 **임시 열 별칭**을 입력 합니다.  
  
     **속성** 창에는 다음 정보가 포함 되어야 합니다.  
  
    |속성|값|  
    |--------------|-----------|  
    |**설명**|Temporary column alias|  
    |**ID**|ServiceGrade Binned|  
    |**모델링 플래그**||  
    |**이름**|Service Grade|  
    |**SourceColumn ID**|Service Grade 1|  
    |**사용법**|예측|  
  
5.  **마이닝 모델** 탭에서 아무 곳 이나 클릭 합니다.  
  
     표를 업데이트 하 여 열 사용 옆에 새 임시 열 `ServiceGrade`별칭을 표시 합니다. 마이닝 구조와 두 마이닝 모델이 포함된 표는 다음과 같습니다.  
  
    |구조|Call Center Default NN|Call Center Binned NN|  
    |---------------|----------------------------|---------------------------|  
    ||Microsoft 신경망|Microsoft 신경망|  
    |AutomaticResponses|입력|입력|  
    |AverageTimePerIssue|예측|예측|  
    |Calls|입력|입력|  
    |DayOfWeek|입력|입력|  
    |FactCallCenterID|Key|Key|  
    |IssuesRaised|입력|입력|  
    |LevelOneOperators|입력|입력|  
    |LevelTwoOperators|입력|입력|  
    |Orders|입력|입력|  
    |ServceGrade Binned|무시|예측(ServiceGrade)|  
    |ServiceGrade|예측|무시|  
    |Shift|입력|입력|  
    |Total Operators|입력|입력|  
    |WageType|입력|입력|  
  
## <a name="process-all-models"></a>모든 모델 처리  
 마지막으로, 위에서 만든 모델을 쉽게 비교할 수 있도록 기본 모델과 범주화된 모델에 대한 초기값 매개 변수를 설정합니다. 초기값을 설정하면 각 모델이 동일한 지점에서 데이터 처리를 시작합니다.  
  
> [!NOTE]  
>  초기값 매개 변수에 대한 숫자 값을 지정하지 않으면 SQL Server Analysis Services에서 모델 이름을 기반으로 하여 초기값을 생성합니다. 모델의 이름은 항상 서로 다르므로 동일한 순서로 데이터를 처리하도록 초기값을 설정해야 합니다.  
  
###  <a name="to-specify-the-seed-and-process-the-models"></a><a name="bkmk_SeedProcess"></a>초기값을 지정 하 고 모델을 처리 하려면  
  
1.  **마이닝 모델** 탭에서 Call CENTER-LR 이라는 모델의 열을 마우스 오른쪽 단추로 클릭 하 고 **알고리즘 매개 변수 설정**을 선택 합니다.  
  
2.  HOLDOUT_SEED 매개 변수에 대 한 행에서 **값**아래에 있는 빈 셀을 클릭 하 고 `1`을 입력 합니다. **확인**을 클릭합니다. 구조와 연관된 각 모델에 대해 이 단계를 반복합니다.  
  
    > [!NOTE]  
    >  모든 관련 모델에 대해 동일한 초기값을 사용하는 경우에는 초기값으로 선택한 값이 중요하지 않습니다.  
  
3.  **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리**를 선택 합니다. 업데이트 된 데이터 마이닝 프로젝트를 서버에 배포 하려면 **예** 를 클릭 합니다.  
  
4.  **마이닝 모델 처리** 대화 상자에서 **실행**을 클릭 합니다.  
  
5.  **닫기** 를 클릭 하 여 **처리 진행률** 대화 상자를 닫은 다음 **마이닝 모델 처리** 대화 상자에서 **닫기** 를 다시 클릭 합니다.  
  
 관련된 두 가지 마이닝 모델을 만들었으므로 데이터를 탐색하여 데이터에서 관계를 찾습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [중급 데이터 마이닝 자습서 &#40;콜 센터 모델 탐색&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
