---
title: Microsoft 시계열 알고리즘 기술 참조 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ARTXP
- HISTORICAL_MODEL_GAP parameter
- AUTO_DETECT_PERIODICITY parameter
- time series algorithms [Analysis Services]
- ARIMA
- INSTABILITY_SENSITIVITY parameter
- PERIODICITY_HINT parameter
- MAXIMUM_SERIES_VALUE parameter
- time series [Analysis Services]
- MINIMUM_SUPPORT parameter
- HISTORIC_MODEL_COUNT parameter
- FORECAST_METHOD parameter
- MISSING_VALUE_SUBSTITUTION parameter
- MINIMUM_SERIES_VALUE parameter
- COMPLEXITY_PENALTY parameter
- PREDICTION_SMOOTHING parameter
ms.assetid: 7ab203fa-b044-47e8-b485-c8e59c091271
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c5ffde59f990602964ac178e629a9967d6304d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083758"
---
# <a name="microsoft-time-series-algorithm-technical-reference"></a>Microsoft Time Series Algorithm Technical Reference
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘에는 시계열을 분석하기 위한 두 가지 알고리즘이 포함되어 있습니다.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 소개된 ARTXP 알고리즘은 계열의 적절한 다음 값을 예측하도록 최적화되어 있습니다.  
  
-   ARIMA 알고리즘은 장기 예측의 정확도를 향상시키기 위해 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 에서 추가되었습니다.  
  
 기본적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 각 알고리즘을 별개로 사용하여 모델 학습을 수행한 다음 결과를 혼합하여 여러 개의 예측에 대한 최상의 예측을 생성합니다. 또한 데이터 및 예측 요구 사항을 기반으로 하는 알고리즘 중 하나만 사용할 수도 있습니다. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]에서는 예측 중 알고리즘 혼합을 제어하는 구분 시점을 사용자 지정할 수도 있습니다.  
  
 이 항목에서는 각 알고리즘이 구현되는 방법과 분석 및 예측 결과를 세부 조정하기 위해 매개 변수를 설정하여 알고리즘을 사용자 지정하는 방법에 대한 추가 정보를 제공합니다.  
  
## <a name="implementation-of-the-microsoft-time-series-algorithm"></a>Microsoft 시계열 알고리즘 구현  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Research는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 의사 결정 트리 알고리즘에 대한 구현을 기초로 하여 SQL Server 2005에 처음 사용된 ARTXP 알고리즘을 개발했습니다. 따라서 ARTXP 알고리즘은 주기 시계열 데이터를 나타내는 자동 회귀 트리 모델로 설명할 수 있습니다. 이 알고리즘은 다양한 수의 과거 항목을 예측 중인 각 현재 항목과 연결합니다. ARTXP라는 이름은 자동 회귀 트리 방법(ART 알고리즘)이 알려지지 않은 여러 이전 상태에 적용된다는 사실에서 기인한 것입니다. ARTXP 알고리즘에 대한 자세한 내용은 [시계열 분석을 위한 자동 회귀 트리 모델](https://go.microsoft.com/fwlink/?LinkId=45966)을 참조하세요.  
  
 ARIMA 알고리즘은 장기 예측의 정확도를 향상시키기 위해 SQL Server 2008의 Microsoft 시계열 알고리즘에 추가되었습니다. 이 알고리즘은 Box 및 Jenkins가 설명한 자동 회귀 통합 이동 평균 계산을 위한 프로세스를 구현한 기술입니다. ARIMA 방식에서는 순차적으로 관측된 결과에서 종속성을 확인하고 모델 중에 임의 충격을 사용할 수 있습니다. ARIMA 방식은 또한 승제 계절성을 지원합니다. ARIMA 알고리즘에 대한 자세한 내용이 필요한 경우 Box 및 Jenkins의 세미나 자료를 참조하십시오. 이 섹션에서는 Microsoft 시계열 알고리즘에서 ARIMA 방식이 어떻게 구현되었는지에 대해서만 설명합니다.  
  
 기본적으로 Microsoft 시계열 알고리즘에서는 ARTXP와 ARIMA 방식을 모두 사용하고 결과를 혼합하여 예측 정확도를 향상시킬 수 있도록 합니다. 특정 방식만 사용하려는 경우에는 알고리즘 매개 변수를 사용하여 ARTXP 또는 ARIMA만 사용하도록 지정하거나 알고리즘 결과의 혼합 방식을 제어할 수 있습니다. ARTXP 알고리즘에서는 교차 예측을 지원하지만 ARIMA 알고리즘에서는 교차 예측을 지원하지 않습니다. 따라서 교차 예측은 알고리즘을 혼합하여 사용하는 경우나 ARTXP만 사용하도록 모델을 구성한 경우에만 사용할 수 있습니다.  
  
## <a name="understanding-arima-difference-order"></a>ARIMA의 차분 차수 이해  
 이 섹션에서는 ARIMA 모델을 이해하는 데 필요한 몇 가지 용어를 소개하고 Microsoft 시계열 알고리즘에서 사용되는 *차분* 의 구현 방식에 대해 설명합니다. 이러한 용어와 개념에 대한 완전한 설명을 보려면 Box 및 Jenkins가 작성한 설명서를 참조하는 것이 좋습니다.  
  
-   항은 수학 방정식의 한 요소입니다. 예를 들어 다항 방정식에서 한 항은 여러 변수와 상수의 조합을 포함할 수 있습니다.  
  
-   Microsoft 시계열 알고리즘에 포함된 ARIMA 수식에는 *자동 회귀* 및 *이동 평균* 항이 모두 사용됩니다.  
  
-   시계열 모델은 *정상* 또는 *비정상*모델일 수 있습니다. *정상 모델* 은 순환 변동이 있더라도 평균으로 회귀하는 모델이며, *비정상 모델* 은 균형에 초점을 두지 않고 *충격*또는 외부 변수로 인한 높은 편차 또는 변동폭을 갖기 쉽습니다.  
  
-   *차분* 의 목적은 시계열을 정상화하여 정상 모델로 만드는 것입니다.  
  
-   *차분 차수* 는 값들 간의 차분이 시계열에 사용된 횟수를 나타냅니다.  
  
 Microsoft 시계열 알고리즘은 데이터 계열에서 값을 가져와 데이터를 패턴에 맞추려고 시도합니다. 데이터 계열이 아직 정상이 아니면 알고리즘이 차분 차수를 적용합니다. 차분 차수가 증가할 때마다 시계열이 점점 더 정상화됩니다.  
  
 예를 들어 (z1, z2,..., zn) 시계열을 하나의 차분 차수를 사용 하 여 계산을 수행 하는 경우 가져와야 새 계열 (y1, y2,..., yn-1), 여기서 *yi = zi + 1-zi*합니다. 차분 차수가 2 이면 알고리즘이 사항과 다른 시리즈 (x1, x2,..., xn-2) 방정식에서 파생 된 y 계열을 기반으로 생성 합니다. 올바른 차분 양은 데이터에 따라 다릅니다. 단일 차분 차수는 일정한 추세를 표시하는 모델에서 가장 일반적으로 사용됩니다. 두 번째 차분 차수는 시간에 따라 변동되는 추세를 나타낼 수 있습니다.  
  
 기본적으로 Microsoft 시계열 알고리즘에 사용된 차분 차수는 -1로서, 알고리즘이 차분 차수의 최적 값을 자동으로 감지합니다. 일반적으로 최적 값은 1이지만(차분이 필요한 경우), 특정 상황에서는 알고리즘이 값을 최대값 2로 늘립니다.  
  
 Microsoft 시계열 알고리즘은 자동 회귀 값을 사용하여 최적의 ARIMA 차분 차수를 결정합니다. 알고리즘은 AR 값을 검사하고 AR 항의 순서를 나타내는 숨겨진 매개 변수인 ARIMA_AR_ORDER를 설정합니다. 이 숨겨진 매개 변수 ARIMA_AR_ORDER의 값 범위는 -1~8입니다. 기본값이 -1이면 알고리즘이 적합한 차분 차수를 자동으로 선택합니다.  
  
 ARIMA_AR_ORDER 값이 1보다 크면 알고리즘이 다항식 항으로 시계열을 곱합니다. 다항식의 한 항이 루트 1 또는 1에 근접한 수로 확인되면 알고리즘이 항을 제거하고 차분 차수를 1 늘려서 모델의 안정성을 보존하려고 시도합니다. 차분 차수가 이미 최대값인 경우 항이 제거되고 차분 차수가 변경되지 않습니다.  
  
 예를 들어 경우 AR의 값 = 2 이면 결과 AR 다항식 항은 다음과 같이 표시 될 수 있습니다. 1 - 1.4B + .45B^2 = (1- .9B) (1- 0.5B). 약 0.9의 루트에 있는 용어 (1-.9B) note 합니다. 알고리즘은 다항식에서 이 항을 제거하지만 이미 최대값 2이기 때문에 차분 차수를 1 늘릴 수 없습니다.  
  
 차분 차수를 **강제로** 변경할 수 있는 유일한 방법은 지원되지 않는 매개 변수인 ARIMA_DIFFERENCE_ORDER를 사용하는 것입니다. 사용자 지정 알고리즘 매개 변수를 입력하여 설정할 수 있는 이 숨겨진 매개 변수는 알고리즘이 시계열에서 차분을 수행하는 횟수를 제어합니다. 하지만 실험 준비가 되어 있지 않고 관련된 계산에 익숙하지 않다면 이 값을 변경하지 않는 것이 좋습니다. 또한 숨겨진 매개 변수를 포함하여 차분 차수의 증분이 발생하는 임계값을 제어할 수 있는 메커니즘은 현재까지 존재하지 않습니다.  
  
 마지막으로 위에서 설명한 수식은 계절성 힌트가 포함되지 않은 단순화된 사례의 수식입니다. 계절성 힌트가 제공된 경우 각 계절성 힌트에 대해 방정식의 왼쪽에 별도의 AR 다항식 항이 추가되며, 차분 계열을 불안정화할 수 있는 항을 제거하기 위해 동일한 전략이 사용됩니다.  
  
## <a name="customizing-the-microsoft-time-series-algorithm"></a>Microsoft 시계열 알고리즘 사용자 지정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘은 결과 마이닝 모델의 동작, 성능 및 정확도에 영향을 주는 다음 매개 변수를 지원합니다.  
  
> [!NOTE]  
>  Microsoft 시계열 알고리즘은 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있지만 시계열 분석을 사용자 지정하는 매개 변수와 같은 고급 기능은 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서만 지원됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2012 버전에서 지원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)을 참조하세요.  
  
### <a name="detection-of-seasonality"></a>계절성 검색  
 ARIMA 및 ARTXP 알고리즘은 모두 계절성 또는 주기 검색을 지원합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 고속 푸리에 변환을 사용하여 학습 전에 계절성을 검색합니다. 그러나 알고리즘 매개 변수를 설정하여 계절성 검색 및 시계열 분석의 결과에 영향을 줄 수 있습니다.  
  
-   *AUTODETECT_SEASONALITY*의 값을 변경하여 생성되는 가능한 시간 세그먼트의 수에 영향을 줄 수 있습니다.  
  
-   *PERIODICITY_HINT*에 대한 하나 이상의 값을 설정하여 데이터의 예상되는 주기에 대한 정보를 알고리즘에 제공하고 검색의 정확도를 높일 수 있습니다.  
  
> [!NOTE]  
>  ARTXP 및 ARIMA 알고리즘은 둘 다 계절성 힌트에 매우 민감합니다. 따라서 잘못된 힌트를 제공하면 결과에 부정적인 영향을 줄 수 있습니다.  
  
### <a name="choosing-an-algorithm-and-specifying-the-blend-of-algorithms"></a>알고리즘 선택 및 알고리즘 혼합 지정  
 기본적으로 또는 MIXED 옵션을 선택하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 알고리즘을 결합하고 알고리즘에 동일한 가중치를 할당합니다. 그러나 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]에서는 특정 알고리즘을 지정하거나 단기 또는 장기 예측에 대해 결과에 가중치를 적용하는 매개 변수를 설정하여 결과에서 각 알고리즘의 비율을 사용자 지정할 수 있습니다. 기본적으로 *FORECAST_METHOD* 매개 변수가 MIXED로 설정되며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 두 알고리즘을 모두 사용하고 해당 값에 가중치를 적용하여 각 알고리즘의 장점을 극대화합니다.  
  
-   알고리즘 선택을 제어하려면 *FORECAST_METHOD* 매개 변수를 설정합니다.  
  
-   ARIMA에서 교차 예측을 지원하지 않으므로 교차 예측을 사용하려면 ARTXP 또는 MIXED 옵션을 사용해야 합니다.  
  
-   단기 예측을 우선시하려면 *FORECAST_METHOD* 를 ARTXP로 설정합니다.  
  
-   장기 예측을 개선하려면 *FORECAST_METHOD* 를 ARIMA로 설정합니다.  
  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 ARIMA 및 ARTXP 알고리즘의 조합을 혼합하는 방법을 사용자 지정할 수도 있습니다. *PREDICTION_SMOOTHING* 매개 변수를 설정하여 혼합을 위한 시작점과 변경 비율을 제어할 수 있습니다.  
  
-   *PREDICTION_SMOOTHING* 을 0으로 설정하는 경우 모델에서는 ARTXP만 사용합니다.  
  
-   *PREDICTION_SMOOTHING* 을 1로 설정하는 경우 모델에서는 ARIMA만 사용합니다.  
  
-   *PREDICTION_SMOOTHING* 을 0과 1 사이의 값으로 설정하는 경우 모델에서는 예측 단계의 지수적 감소 함수로 ARTXP 알고리즘에 가중치를 적용합니다. 이와 동시에 모델은 ARTXP 가중치의 1의 보수로 ARIMA 알고리즘에 가중치를 적용합니다. 곡선을 부드럽게 만들기 위해 정규화 및 안정화 상수가 모델에서 사용됩니다.  
  
 일반적으로 5개까지의 시간 조각을 예측할 경우 ARTXP가 거의 대부분 적합합니다. 그러나 예측할 시간 조각 수가 늘어나면 일반적으로 ARIMA가 더 적합합니다.  
  
 다음 다이어그램에서는 *PREDICTION_SMOOTHING* 이 기본값인 0.5로 설정된 경우 모델에서 알고리즘을 혼합하는 방법을 보여 줍니다. 처음에 ARIMA 및 ARTXP에 동일한 가중치가 적용되지만 예측 단계 수가 증가하면서 ARIMA에 더 많은 가중치가 적용됩니다.  
  
 ![시계열 알고리즘 혼합에 대 한 감소 커브](../media/time-series-mixing-default.gif "시계열 알고리즘 혼합에 대 한 감소 커브")  
  
 반대로 다음 다이어그램에서는 *PREDICTION_SMOOTHING* 이 0.2로 설정된 경우의 알고리즘 혼합을 보여 줍니다. [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]단계의 경우 모델은 ARIMA는 0.2로, ARTXP는 0.8로 가중치를 적용합니다. 그런 다음 ARIMA의 가중치가 지수적으로 증가하고 ARTXP의 가중치가 지수적으로 감소합니다.  
  
 ![시계열 모델 혼합에 대 한 감소 커브](../media/time-series-blending-curve.gif "시계열 모델 혼합에 대 한 감소 커브")  
  
### <a name="setting-algorithm-parameters"></a>알고리즘 매개 변수 설정  
 다음 표에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘에서 사용할 수 있는 매개 변수에 대해 설명합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*AUTO_DETECT_PERIODICITY*|주기를 검색하는 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 및 1 사이의 숫자 값을 지정합니다. 기본값은 0.6입니다.<br /><br /> 이 값을 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]에 가깝게 설정하면 주기성이 강한 데이터만 검색합니다.<br /><br /> 이 값을 1에 가깝게 설정하면 거의 주기적인 패턴을 다양하게 검색하고 주기 힌트를 자동으로 생성할 수 있습니다.<br /><br /> 참고: 많은 주기 힌트를 처리할수록 모델 학습 시간은 현저, 길어지지만 보다 정확한 모델을 만들 수 있습니다.|  
|*COMPLEXITY_PENALTY*|의사 결정 트리의 증가를 제어합니다. 기본값은 0.1입니다.<br /><br /> 이 값을 줄이면 분할 가능성이 높아지고 값을 늘리면 가능성이 낮아집니다.<br /><br /> 참고: 이 매개 변수는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서만 사용할 수 있습니다.|  
|*FORECAST_METHOD*|분석과 예측에 사용할 알고리즘을 지정합니다. 가능한 값은 ARTXP, ARIMA 또는 MIXED입니다. 기본값은 MIXED입니다.|  
|*HISTORIC_MODEL_COUNT*|작성할 기록 모델 수를 지정합니다. 기본값은 1입니다.<br /><br /> 참고: 이 매개 변수는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서만 사용할 수 있습니다.|  
|*HISTORICAL_MODEL_GAP*|두 연속 기록 모델 간의 지연 시간을 지정합니다. 기본값은 10입니다. 이 값은 시간 단위 수를 나타내며 단위는 모델에 의해 정의됩니다.<br /><br /> 예를 들어 이 값을 g로 설정하면 g, 2*g, 3\*g 등의 시간 간격으로 데이터를 잘라 기록 모델을 작성합니다.<br /><br /> 참고: 이 매개 변수는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서만 사용할 수 있습니다.|  
|*INSTABILITY_SENSITIVITY*|예측 분산이 특정 임계값을 초과하고 ARTXP 알고리즘이 예측을 표시하지 않는 지점을 제어합니다. 기본값은 1입니다.<br /><br /> 참고: 이 매개 변수는 ARIMA만 사용 하는 모델에 적용 되지 않습니다.<br /><br /> 기본값 1은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서와 동일한 동작을 제공합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 각 예측에 대한 정규화된 표준 편차를 모니터링합니다. 이 값이 예측에 대한 임계값을 초과하자마자 시계열 알고리즘은 NULL을 반환하고 예측 프로세스를 중지합니다.<br /><br /> [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 값은 불안정 검색을 중지합니다. 이는 분산에 상관없이 만들 수 있는 예측 수에 제한이 없다는 것을 의미합니다.<br /><br /> 참고: 이 매개 변수에서 수정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard의 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 기본값 1만 사용됩니다.|  
|*MAXIMUM_SERIES_VALUE*|예측에 사용할 최대값을 지정합니다. 이 매개 변수는 *MINIMUM_SERIES_VALUE*와 함께 예측을 예상 범위로 제한하는 데 사용됩니다. 예를 들어 특정 일의 예상 판매 수량이 재고 제품 수를 초과하지 않도록 지정할 수 있습니다.<br /><br /> 참고: 이 매개 변수는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서만 사용할 수 있습니다.|  
|*MINIMUM_SERIES_VALUE*|예측할 수 있는 최소값을 지정합니다. 이 매개 변수는 *MAXIMUM_SERIES_VALUE*와 함께 예측을 예상 범위로 제한하는 데 사용됩니다. 예를 들어 예측된 판매 수량이 음수가 아니어야 함을 지정할 수 있습니다.<br /><br /> 참고: 이 매개 변수는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서만 사용할 수 있습니다.|  
|*MINIMUM_SUPPORT*|각 시계열 트리에서 분할을 생성하는 데 필요한 최소 시간 조각 수를 지정합니다. 기본값은 10입니다.|  
|*MISSING_VALUE_SUBSTITUTION*|기록 데이터의 간격을 채우는 방법을 지정합니다. 기본적으로 데이터의 간격은 허용되지 않습니다. 데이터에 여러 계열이 포함된 경우 계열은 또한 비정형 가장자리를 가질 수 없습니다. 즉, 모든 계열은 동일한 시작점과 끝점을 가져야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 또한 시계열 모델에서 `PREDICTION JOIN`을 수행할 때 새 데이터의 간격을 채우기 위해 이 매개 변수의 값이 사용됩니다. 다음 표에서는 이 매개 변수에 사용할 수 있는 값을 나열합니다.<br /><br /> None: 기본. 누락된 값을 학습된 모델의 곡선을 따라 표시된 값으로 대체합니다.<br /><br /> 이전: 이전 시간 조각의 값을에서 반복합니다.<br /><br /> 평균: 학습에 사용 되는 시간 조각의 이동 평균을 사용 합니다.<br /><br /> 숫자 상수: 지정된 된 숫자를 사용 하 여 모든 누락 값으로 바꿉니다.|  
|*PERIODICITY_HINT*|데이터의 주기성과 관련된 알고리즘에 대한 힌트를 제공합니다. 예를 들어 판매량이 매년 다르고 계열의 측정 단위가 월인 경우 주기성은 12입니다. 이 매개 변수는 {n [, n]} 형식이며, 여기서 n은 임의의 양수입니다.<br /><br /> 대괄호([]) 안의 n은 선택 사항이며 필요한 만큼 반복할 수 있습니다. 예를 들어 매월 제공되는 데이터에 대한 여러 주기 힌트를 제공하려면 년, 분기 및 월에 대한 패턴을 검색하기 위해 {12, 3, 1}을 입력할 수 있습니다. 그러나 주기는 모델 품질에 큰 영향을 줍니다. 제공한 힌트가 실제 주기와 다르면 결과에 부정적인 영향을 줄 수 있습니다.<br /><br /> 기본값은 {1}입니다.<br /><br /> 참고: 중괄호가 필요 합니다. 또한 이 매개 변수는 문자열 데이터 형식을 가집니다. 따라서 이 매개 변수를 DMX(Data Mining Extensions) 문의 일부로 입력할 경우 숫자와 중괄호를 따옴표로 묶어야 합니다.|  
|*PREDICTION_SMOOTHING*|예측을 최적화하기 위해 모델을 혼합해야 하는 방법을 지정합니다. 이 매개 변수는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서만 사용할 수 있습니다. [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 및 1 사이의 값을 입력하거나 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]: 예측에서 ARTXP만 사용하도록 지정합니다. 예측은 적은 예측에 맞게 최적화됩니다.<br /><br /> 0.5: (기본값) 두 알고리즘을 사용 해야 하는 예측 하 고 결과가 혼합을 지정 합니다.<br /><br /> 1: 예측에서 ARIMA만 지정 합니다. 예측은 많은 예측에 맞게 최적화됩니다.<br /><br /> <br /><br /> 참고: 사용 된 *FORECAST_METHOD* 매개 변수 학습을 제어 합니다.|  
  
### <a name="modeling-flags"></a>모델링 플래그  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘은 다음과 같은 모델링 플래그를 지원합니다. 마이닝 구조나 마이닝 모델을 만들 경우 분석 중 각 열의 값이 처리되는 방법을 지정하기 위해 모델링 플래그를 정의합니다. 자세한 내용은 [모델링 플래그&#40;데이터 마이닝&#41;](modeling-flags-data-mining.md)를 참조하세요.  
  
|모델링 플래그|Description|  
|-------------------|-----------------|  
|NOT NULL|열에 null이 포함될 수 없음을 나타냅니다. 따라서 Analysis Services가 모델 학습 중 Null을 발견할 경우 오류가 발생합니다.<br /><br /> 마이닝 구조 열에 적용됩니다.|  
|MODEL_EXISTENCE_ONLY|열의 상태를 가진 것으로 간주 됩니다 것을 의미 합니다. Missing 및 Existing 합니다. Null은 누락 값입니다.<br /><br /> 마이닝 모델 열에 적용됩니다.|  
  
## <a name="requirements"></a>요구 사항  
 시계열 모델은 고유한 값, 입력 열 및 하나 이상의 예측 가능한 열을 포함하는 Key Time 열을 포함해야 합니다.  
  
### <a name="input-and-predictable-columns"></a>입력 열과 예측 가능한 열  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘은 다음 표에 나열된 특정 입력 열 내용 유형, 예측 가능한 열 내용 유형 및 모델링 플래그를 지원합니다.  
  
|Column|내용 유형|  
|------------|-------------------|  
|입력 특성|Continuous, Key, Key Time 및 Table|  
|예측 가능한 특성|Continuous, Table|  
  
> [!NOTE]  
>  Cyclical  및 Ordered  내용 유형이 지원되기는 하지만 알고리즘은 해당 유형을 불연속 값으로 처리하고 특수한 처리를 수행하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 시계열 알고리즘](microsoft-time-series-algorithm.md)   
 [시계열 모델 쿼리 예제](time-series-model-query-examples.md)   
 [시계열 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
