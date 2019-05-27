---
title: 교차 유효성 검사 탭 (마이닝 정확도 차트 뷰) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.crossvalidation.f1
ms.assetid: bd215a68-1ad7-4046-9c44-ec8e2be13a64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5a8508218ed6a2b4407943fe962959e3cd4f97d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086621"
---
# <a name="cross-validation-tab-mining-accuracy-chart-view"></a>교차 유효성 검사 탭(마이닝 정확도 차트 뷰)
  교차 유효성 검사를 사용하면 마이닝 구조를 교집합 영역으로 분할하고 각 교집합 영역에 대해 모델을 반복적으로 학습 및 테스트할 수 있습니다. 데이터를 분할할 접기 수를 지정하면 각 접기가 테스트 데이터로 사용되고 나머지 데이터는 새 모델을 학습하는 데 사용됩니다. 그러면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]가 각 모델에 대해 표준 정확도 메트릭 집합을 생성합니다. 각 교집합 영역에 대해 생성된 모델의 메트릭을 비교하여 전체 데이터 집합에 대한 마이닝 모델의 안정성을 파악할 수 있습니다.  
  
 자세한 내용은 [교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/cross-validation-analysis-services-data-mining.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 사용하여 작성한 모델에는 교차 유효성 검사를 사용할 수 없습니다. 이러한 모델 유형을 포함하는 마이닝 구조에서 보고서를 실행하면 해당 모델이 보고서에 포함되지 않습니다.  
  
## <a name="task-list"></a>작업 목록  
  
-   접기 수를 지정합니다.  
  
-   교차 유효성 검사에 사용할 최대 사례 수를 지정합니다.  
  
-   예측 가능한 열을 지정합니다.  
  
-   필요에 따라 예측 가능한 상태를 지정합니다.  
  
-   필요에 따라 예측의 정확도 평가 방법을 제어하는 매개 변수를 설정합니다.  
  
-   **결과 가져오기** 를 클릭하여 교차 유효성 검사의 결과를 표시합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **접기 개수**  
 만들 접기 또는 파티션의 수를 지정합니다. 최소값은 데이터 집합의 절반은 테스트에 사용되고 나머지 절반은 학습에 사용됨을 의미하는 2입니다.  
  
 세션 마이닝 구조의 경우 최대값은 10입니다.  
  
 마이닝 구조가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 저장되는 경우 최대값은 256입니다.  
  
> [!NOTE]  
>  접기 수를 늘리면 교차 유효성 검사를 수행하는 데 필요한 시간도 마찬가지로 n배 증가합니다. 사례 수가 크고 **접기 개수** 값도 큰 경우 성능 문제가 발생할 수 있습니다.  
  
 **최대 사례**  
 교차 유효성 검사에 사용할 최대 사례 수를 지정합니다. 특정 접기의 사례 수는 **최대 사례** 값을 **접기 개수** 값으로 나눈 값과 같습니다.  
  
 **0**을 사용하면 원본 데이터의 모든 사례가 교차 유효성 검사에 사용됩니다.  
  
 기본값은 없습니다.  
  
> [!NOTE]  
>  사례 수를 늘리면 처리 시간도 증가합니다.  
  
 **대상 특성**  
 모든 모델에서 찾은 예측 가능한 열 목록에서 열을 선택합니다. 교차 유효성 검사를 수행할 때마다 하나의 예측 가능한 열만 선택할 수 있습니다.  
  
 클러스터링 모델만 테스트하려면 **클러스터**를 선택합니다.  
  
 **대상 상태**  
 값을 입력하거나 드롭다운 값 목록에서 대상 값을 선택합니다.  
  
 기본값은 `null`로 모든 상태가 테스트된 것으로 간주됩니다.  
  
 클러스터링 모델에서는 사용되지 않습니다.  
  
 **대상**  **임계값**  
 예측 확률을 나타내는 0-1의 값을 지정합니다. 이 임계값을 초과하는 예측 상태는 올바른 것으로 간주됩니다. 이 값은 0.1 단위로 설정할 수 있습니다.  
  
 기본값은 `null`로 가장 가능성이 높은 예측이 올바른 것으로 간주됩니다.  
  
> [!NOTE]  
>  이 값을 0.0으로 설정할 수 있지만 이 값을 사용하면 처리 시간이 늘어나고 의미 있는 결과가 생성되지 않습니다.  
  
 **결과 가져오기**  
 지정한 매개 변수를 사용하여 모델의 교차 유효성 검사를 시작하려면 클릭합니다.  
  
 모델이 지정한 접기 수로 분할되고 각 접기에 대해 별도의 모델이 테스트됩니다. 따라서 교차 유효성 검사가 결과를 반환할 때까지 다소 시간이 걸릴 수 있습니다.  
  
 교차 유효성 검사 보고서의 결과를 해석하는 방법은 [교차 유효성 검사 보고서의 측정값](data-mining/measures-in-the-cross-validation-report.md)을 참조하세요.  
  
## <a name="setting-the-accuracy-threshold"></a>정확도 임계값 설정  
  **대상** **임계값**을 설정하여 예측 정확도를 측정하기 위한 표준을 제어할 수 있습니다. 임계값은 일종의 정확도 막대를 나타냅니다. 각 예측에는 예측 값이 정확할 확률이 할당됩니다. 따라서 **대상** **임계값** 을 1에 가깝게 설정하면 특정 예측의 확률이 매우 높아야 예측이 올바른 예측으로 간주됩니다. 반대로 **대상** **임계값** 을 0에 가깝게 설정하면 확률 값이 낮은 예측도 "올바른" 예측으로 간주됩니다.  
  
 예측의 확률은 만드는 예측의 유형과 데이터의 양에 따라 달라지므로 권장되는 임계값은 없습니다. 확률 수준이 다른 몇 가지 예측을 검토하여 데이터에 적합한 정확도 막대를 결정해야 합니다.  **대상** **임계값** 에 설정하는 값은 측정된 모델의 정확도에 영향을 주므로 이 작업을 수행하는 것이 중요합니다.  
  
 예를 들어 특정 대상 상태에 대해 세 개의 예측을 만들었으며 각 예측의 확률이 0.05, 0.15 및 0.8이라고 가정합니다. 임계값을 0.5로 설정하면 한 예측만 올바른 것으로 간주됩니다.  **대상** **임계값** 을 0.10으로 설정하면 두 예측이 올바른 것으로 간주됩니다.  
  
 때 **대상** **임계값** 로 설정 된 `null`, 기본 값, 각 사례에 대해 가장 가능성이 높은 예측이 올바른 것으로 간주 됩니다. 위의 예에서 0.05, 0.15 및 0.8은 세 개의 사례에서 예측에 대한 확률입니다. 확률이 서로 많이 다르지만 각 사례는 하나의 예측만 생성하고 이러한 예측은 사례에 대한 최상의 예측이므로 각 예측은 올바른 것으로 간주됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [테스트 및 유효성 검사 & #40; 데이터 마이닝 & #41;](data-mining/testing-and-validation-data-mining.md)   
 [교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/cross-validation-analysis-services-data-mining.md)   
 [교차 유효성 검사 보고서의 측정값](data-mining/measures-in-the-cross-validation-report.md)   
 [데이터 마이닝 저장 프로시저&#40;Analysis Services - 데이터 마이닝&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
