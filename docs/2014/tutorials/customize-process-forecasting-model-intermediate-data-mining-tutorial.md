---
title: 예측 모델 사용자 지정 및 처리 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4bd25e15-9d9e-4528-b7bc-ccb856643aec
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d2d0e73d1d9a4058ff63320552604b2bfa1bca8a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63249399"
---
# <a name="customizing-and-processing-the-forecasting-model-intermediate-data-mining-tutorial"></a>예측 모델 사용자 지정 및 처리(중급 데이터 마이닝 자습서)
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘은 모델을 만들고 시간 데이터를 분석하는 방법에 영향을 주는 여러 매개 변수를 제공합니다. 이러한 속성을 변경하면 마이닝 모델이 예측을 수행하는 방식에 큰 영향을 줄 수 있습니다.  
  
 자습서에서 이러한 태스크를 위해 다음 작업을 수행하여 모델을 변경합니다.  
  
1.  *PERIODICITY_HINT* 매개 변수에 대 한 새 값을 추가 하 여 모델이 기간을 처리 하는 방식을 사용자 지정 합니다.  
  
2.  Microsoft 시계열 알고리즘에 대 한 두 가지 중요 한 매개 변수, 즉 예측에 사용 되는 방법을 제어할 수 있는 FORECAST_METHOD 및 장기 및 단기 예측의 혼합을 사용자 지정할 수 있는 PREDICTION_SMOOTHING에 대해 알아봅니다.  
  
3.  필요에 따라 귀속되는 누락된 값의 처리 방식을 알고리즘에 알려 줍니다.  
  
4.  모든 변경이 적용되면 모델을 배포하고 처리합니다.  
  
## <a name="setting-time-series-parameters"></a>시계열 매개 변수 설정  
 **주기성 힌트**  
  
 *PERIODICITY_HINT* 매개 변수는 데이터에 표시 되어야 하는 추가 기간에 대 한 정보를 알고리즘에 제공 합니다. 기본적으로 시계열 모델은 자동으로 데이터에서 패턴을 감지하려고 합니다. 그러나 예측 시간 주기를 이미 알고 있는 경우 주기성 힌트를 제공하여 잠재적으로 모델의 정확도를 개선할 수 있습니다. 반면 잘못된 주기성 힌트를 제공한 경우 정확도를 떨어뜨릴 수 있으므로, 사용해야 할 값에 확신이 없는 경우 기본값을 사용하는 것이 최선입니다.  
  
 예를 들어, 이 모델에 사용된 뷰에서는 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]로부터 판매 데이터를 월별로 집계합니다. 따라서 모델에 사용된 각 시간 조각은 한 달을 나타내며 또한 모든 예측은 개월 수 기준입니다. 1 년에 12 개월이 발생 하 고 해당 판매 패턴이 매년 반복 될 것으로 간주 되기 때문에 *PERIODICITY_HINT* 매개 변수를로 `12`설정 하 여 12 개의 시간 조각 (months)이 전체 판매 주기를 구성 하도록 지정 합니다.  
  
 **예측 메서드**  
  
 *FORECAST_METHOD* 매개 변수는 시계열 알고리즘이 단기 또는 장기 예측에 대해 최적화 되어 있는지 여부를 제어 합니다. 기본적으로 *FORECAST_METHOD* 매개 변수는 MIXED로 설정 됩니다. 즉, 단기 및 장기 예측 모두에 적합 한 결과를 제공 하기 위해 서로 다른 두 알고리즘을 혼합 하 고 분산 합니다.  
  
 그러나 특정 알고리즘을 사용하려는 경우 값을 ARIMA 또는 ARTXP로 변경할 수 있습니다.  
  
 **장기 조건 및 단기 예측**  
  
 또한 PREDICTION_SMOOTHING 매개 변수를 사용하여 장기 및 단기 예측이 혼합되는 방식을 사용자 지정할 수도 있습니다. 기본적으로 이 매개 변수는 0.5로 설정됩니다. 이 값은 전체적으로 적절한 정확도를 제공합니다.  
  
#### <a name="to-change-the-algorithm-parameters"></a>알고리즘 매개 변수를 변경하려면  
  
1.  **마이닝 모델** 탭에서 **예측**을 마우스 오른쪽 단추로 클릭 하 고 **알고리즘 매개 변수 설정**을 선택 합니다.  
  
2.  `PERIODICITY_HINT` **알고리즘 매개 변수** 대화 상자의 행에서 **값** 열을 클릭 한 다음 중괄호를 포함 하 `{12}`여을 입력 합니다.  
  
     기본적으로 알고리즘에서도 값 {1}을 추가합니다.  
  
3.  행에서 **값** 텍스트 상자가 비어 있거나로 `MIXED`설정 되었는지 확인 합니다. `FORECAST_METHOD` 다른 값을 입력 한 경우를 입력 `MIXED` 하 여 매개 변수를 다시 기본값으로 변경 합니다.  
  
4.  **PREDICTION_SMOOTHING** 행에서 **값** 텍스트 상자가 비어 있거나 0.5로 설정 되어 있는지 확인 합니다. 다른 값을 입력 한 경우 **값** 을 클릭 하 고를 `0.5` 입력 하 여 매개 변수를 다시 기본값으로 변경 합니다.  
  
    > [!NOTE]  
    >  PREDICTION_SMOOTHING 매개 변수는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise에서만 사용할 수 있습니다. 따라서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard에서 PREDICTION_SMOOTHING 매개 변수의 값을 보거나 변경할 수 없습니다. 하지만 기본 동작은 두 알고리즘을 모두 사용하고 두 알고리즘에 똑같은 가중치를 지정하는 것입니다.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="handling-missing-data-optional"></a>누락된 데이터 처리(선택 사항)  
 대부분의 경우 매출 데이터는 Null로 채워지는 간격이 있거나 매장에서 보고 최종 기한을 충족하지 않아 계열의 끝에 빈 셀이 있을 수 있습니다. 그러한 시나리오에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]가 다음 오류를 발생시키고 모델을 처리하지 않습니다.  
  
 "오류 (데이터 마이닝): 마이닝 모델, \< \<모델 이름>의 series Series name>부터 타임 스탬프가 동기화 되지 않았습니다. 모든 시계열은 같은 시간 표식에서 끝나야 하며 임의의 누락 데이터 요소가 있으면 안 됩니다. MISSING_VALUE_SUBSTITUTION 매개 변수를 Previous 또는 숫자 상수로 설정하면 누락 데이터 요소가 자동으로 패치됩니다."  
  
 이 오류가 발생하지 않도록 하려면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 다음 메서드 중 하나를 사용하여 간격을 채울 새 값을 자동으로 제공하도록 지정할 수 있습니다.  
  
-   평균 값 사용. 평균은 같은 데이터 계열의 유효한 모든 값을 사용하여 계산됩니다.  
  
-   이전 값 사용. 누락된 여러 셀에 대해 이전 값을 대체할 수 있지만 시작 값을 채울 수 없습니다.  
  
-   제공한 상수 값 사용  
  
#### <a name="to-specify-that-gaps-be-filled-by-averaging-values"></a>평균값을 계산하여 간격을 채우도록 지정하려면  
  
1.  **마이닝 모델** 탭에서 **예측** 열을 마우스 오른쪽 단추로 클릭 하 고 **알고리즘 매개 변수 설정**을 선택 합니다.  
  
2.  **알고리즘 매개 변수** 대화 상자의 **MISSING_VALUE_SUBSTITUTION** 행에서 **값** 열을 클릭 하 고을 입력 `Mean`합니다.  
  
## <a name="build-the-model"></a>모델 작성  
 모델을 사용하려면 모델을 서버에 배포하고 알고리즘을 통해 학습 데이터를 실행하여 모델을 처리해야 합니다.  
  
#### <a name="to-process-the-forecasting-model"></a>예측 모델을 처리하려면  
  
1.  의 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리**를 선택 합니다.  
  
2.  프로젝트를 빌드 및 배포할지를 요청 하는 경고에서 **예**를 클릭 합니다.  
  
3.  **마이닝 구조 처리-예측** 대화 상자에서 **실행**을 클릭 합니다.  
  
     **처리 진행률** 대화 상자가 열리고 모델 처리에 대 한 정보를 표시 합니다. 모델 처리는 시간이 걸릴 수 있습니다.  
  
4.  처리가 완료 되 면 **닫기** 를 클릭 하 여 처리 **진행률** 대화 상자를 종료 합니다.  
  
5.  **닫기** 를 다시 클릭 하 여 **마이닝 구조 처리-예측** 대화 상자를 종료 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [예측 모델 탐색 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft 시계열 알고리즘 기술 참조](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Microsoft 시계열 알고리즘](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [처리 요구 사항 및 고려 사항&#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
