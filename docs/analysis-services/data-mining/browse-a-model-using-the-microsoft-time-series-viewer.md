---
title: "Microsoft 시계열 뷰어를 사용 하 여 모델 찾아보기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], continuous columns
- mining model content, viewing
- Microsoft Time Series Viewer
- charts [Analysis Services]
- Time Series Viewer [Analysis Services]
- continuous columns
- regression algorithms [Analysis Services]
ms.assetid: a77c16cd-1cd0-4fc5-afeb-d1dab30d1e25
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0de59252e18921c4c280143b695000b5913a5aa2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="browse-a-model-using-the-microsoft-time-series-viewer"></a>Microsoft 시계열 뷰어를 사용하여 모델 찾아보기
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 시계열 뷰어는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘으로 작성한 마이닝 모델을 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘은 예측 시나리오에서 제품 판매량과 같은 연속 열을 예측하기 위해 데이터 마이닝 모델을 만드는 회귀 알고리즘입니다. 이 시계열 모델은 다음과 같이 다른 알고리즘을 기반으로 한 정보를 포함할 수 있습니다.  
  
-   단기 예측에 대해 최적화되어 있는 ARIxp 알고리즘  
  
-   장기 예측에 대해 최적화되어 있는 ARIMA 알고리즘  
  
-   ARTxp 및 ARIMA 알고리즘의 혼합  
  
 이러한 알고리즘에 대한 자세한 내용은 [Microsoft Time Series Algorithm](../../analysis-services/data-mining/microsoft-time-series-algorithm.md) 및 [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)를 참조하십시오.  
  
> [!NOTE]  
>  발견된 패턴 및 모델에 사용된 수식에 대한 자세한 정보를 보려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어를 사용하십시오. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) 또는 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)를 참조하세요.  
  
##  <a name="BKMK_ViewerTabs"></a> 뷰어 탭  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 마이닝 모델을 찾으면 해당 모델의 적절한 뷰어에서 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 탭에 해당 모델이 표시됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 뷰어에는 다음과 같은 탭이 있습니다.  
  
-   [Model](#BKMK_Tree)  
  
-   [차트](#BKMK_Charts)  
  
 **참고** 모델 콘텐츠 및 마이닝 범례에 대해 표시된 정보는 모델에서 사용하는 알고리즘에 따라 달라집니다. 그러나 **모델** 및 **차트** 탭은 알고리즘 혼합에 관계없이 동일합니다.  
  
###  <a name="BKMK_Tree"></a> Model  
 시계열 모델을 작성할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 완료된 모델을 트리로 표시합니다. 데이터에 여러 가지 사례 계열이 포함된 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 각 계열에 대해 별도의 트리를 작성합니다. 예를 들어 태평양, 북미 및 유럽 지역의 판매를 예측하는 경우 이러한 각 지역에 대한 예측은 사례 계열입니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 이러한 각 계열에 대해 별도의 트리를 작성합니다. 특정 계열을 보려면 **트리** 목록에서 계열을 선택합니다.  
  
 각 트리에서 시계열 모델은 **모두** 노드를 포함한 다음 알고리즘에서 발견한 주기적 구조를 나타내는 노드 계열로 분리합니다. 각 노드를 클릭하여 일련의 사례와 수식 등의 통계를 표시할 수 있습니다.  
  
 ARTxp만 사용하여 모델을 만든 경우 루트 노드의 **마이닝 범례** 에는 총 사례 수만 포함됩니다. 루트가 아닌 각 노드의 **마이닝 범례** 에는 분할된 트리에 대한 세부 정보가 포함됩니다. 예를 들어 사례 수 및 노드에 대한 수식이 표시됩니다. 범례의 *규칙* 에는 계열을 식별하는 정보와 규칙이 적용되는 시간 조각이 포함됩니다. 예를 들어 범례 텍스트 `M200 Europe Amount -2` 는 노드가 두 개의 시간 조각 이전 기간에서 M200 Europe 계열의 모델을 나타냄을 가리킵니다.  
  
 ARIMA만 사용하여 모델을 만든 경우 **모델** 탭에는 **모두**라는 캡션이 있는 단일 노드가 포함됩니다. 루트 노드의 **마이닝 범례** 에는 ARIMA 수식이 포함됩니다.  
  
 혼합 모델을 만든 경우 루트 노드에는 사례 수와 ARIMA 수식만 포함됩니다. 루트 노드 다음에 트리는 각 주기적 구조에 대한 별도의 노드로 분리됩니다. 루트가 아닌 각 노드에서 마이닝 범례에는 ARTxp 및 ARIMA 알고리즘 모두와 노드의 수식, 노드 내 사례 수가 포함됩니다. ARTxp 수식은 처음 나열되고 트리 노드 수식이라는 레이블이 붙습니다. 그 다음에 ARIMA 수식이 나열됩니다. 이 정보를 해석하는 방법은 [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)를 참조하십시오.  
  
 일반적으로 의사 결정 트리 그래프는 가장 중요한 분리인 **모두** 노드를 뷰어의 왼쪽에 표시합니다. 의사 결정 트리에서 **모두** 노드 다음의 분할은 학습 데이터의 사례를 가장 확실하게 분리하는 조건을 포함하므로 가장 중요합니다. 시계열 모델에서 주 분기는 가능성이 가장 높은 계절적 주기를 나타냅니다. **All** 노드 다음의 분할은 분기의 오른쪽에 나타납니다.  
  
 트리의 개별 노드를 확장하거나 축소하여 각 노드 다음에 발생하는 분할을 표시하거나 숨길 수 있습니다. **의사 결정 트리** 탭의 옵션을 사용하여 트리 표시 방법을 변경할 수도 있습니다. **수준 표시** 슬라이더를 사용하여 트리에 표시되는 수준의 개수를 조정할 수 있습니다. **기본 확장** 을 사용하여 모델의 모든 트리에 표시되는 기본 수준 개수를 설정할 수 있습니다.  
  
 각 노드의 배경색 음영은 노드에 있는 사례 수를 의미합니다. 노드에 있는 정확한 사례 수를 찾으려면 노드 위로 포인터를 가져가서 해당 노드에 대한 정보 팁을 봅니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a> 차트  
 **차트** 탭에서는 시간에 따른 예측 특성의 동작과 함께 5개의 예측 미래 값을 보여 주는 그래프를 표시합니다. 차트의 세로 축은 계열 값을 나타내고 가로 축은 시간을 나타냅니다.  
  
> [!NOTE]  
>  시간 축에 사용되는 시간 조각은 데이터에 사용된 단위에 따라 일, 월 또는 초를 나타낼 수 있습니다.  
  
 **Abs** 단추를 사용하여 절대 곡선과 상대 곡선을 전환할 수 있습니다. 차트에 여러 모델이 포함된 경우 각 모델에 대한 데이터의 배율이 크게 다를 수 있습니다. 절대 곡선을 사용하는 경우 한 모델은 일직선으로 나타나는 반면 다른 모델은 상당한 변경을 나타낼 수 있습니다. 이는 한 모델의 배율이 다른 모델의 배율보다 크기 때문입니다. 상대 곡선으로 전환하여 절대값 대신 변경 비율을 표시하도록 배율을 변경할 수 있습니다. 이렇게 하면 다른 배율을 기반으로 한 모델을 비교하기 편리합니다.  
  
 마이닝 모델에 여러 시계열이 포함되어 있으면 차트에 표시할 계열을 하나 이상 선택할 수 있습니다. 뷰어의 오른쪽에 있는 목록을 클릭한 다음 목록에서 원하는 계열을 선택합니다. 차트가 너무 복잡해지면 범례의 계열 확인란을 선택하거나 선택을 취소하여 표시되는 계열을 필터링할 수 있습니다.  
  
 차트에는 기록 데이터와 예측 데이터가 모두 표시됩니다. 예측 데이터는 기록 데이터와 구분하기 위해 음영으로 표시됩니다. 데이터 값에서 기록 데이터는 실선으로 표시되고 예측은 점선으로 표시됩니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 속성을 설정하여 각 계열에 대해 사용되는 선 색을 변경할 수 있습니다. 자세한 내용은 [데이터 마이닝 뷰어에서 사용되는 색 변경](../../analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md)을 참조하세요.  
  
 확대/축소 옵션을 사용하여 표시된 시간 범위를 조정할 수 있습니다. 또한 차트를 클릭하고 선택한 시간 영역을 차트에서 끈 다음 다시 클릭하여 선택한 범위를 확대하면 특정 시간 범위를 볼 수 있습니다.  
  
 **예측 단계** 를 사용하여 모델에서 볼 예측 시간 **단계**개수를 선택할 수 있습니다. **편차 표시** 확인란을 선택하면 예측 값의 정확도를 볼 수 있는 오차 막대가 뷰어에 표시됩니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft 시계열 알고리즘](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [시계열 모델 쿼리 예제](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [데이터 마이닝 모델 뷰어](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
