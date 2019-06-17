---
title: 신경망 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.neuralnet.f1
ms.assetid: 18d87e7b-a821-40ea-9bd8-c6fecf189a1c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05654d9206f09d151abd5557d0aa6aae90b1b9ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072314"
---
# <a name="neural-network-mining-model-viewer"></a>신경망(마이닝 모델 뷰어)
  **신경망** 뷰어를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] 신경망 알고리즘 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 로지스틱 회귀 알고리즘을 기반으로 하는 마이닝 모델을 탐색할 수 있습니다.  
  
 **참조 항목:** [Microsoft 신경망 알고리즘](data-mining/microsoft-neural-network-algorithm.md)하십시오 [Microsoft 로지스틱 회귀 알고리즘](data-mining/microsoft-logistic-regression-algorithm.md),[Microsoft 신경망 뷰어를 사용 하 여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 보려는 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **Viewer**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 사용자 지정 뷰어 또는 **Microsoft 일반 콘텐츠 트리 뷰어**를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **Input**  
 입력 특성과 해당 값을 선택하려면 이 영역을 사용합니다. 이후에 이러한 항목이 결과에 주는 영향을 탐색할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**특성**|목록에서 입력 특성을 선택합니다. 기본적으로 선택 영역을 두면  **\<모든 >** , 차트에는 예측 가능한 특성에 대 한 영향 순으로 순위가 지정 된 모든 입력된 특성의 목록을 보여 줍니다.|  
|**Value**|입력 특성의 값을 선택합니다.|  
  
 **출력**  
 막대 그래프에서 분석하고 비교할 예측 가능한 특성 및 값을 선택하려면 이러한 컨트롤을 사용합니다. 선택 항목을 변경하지 않는 경우 막대 그래프에서 맨 위의 두 결과 상태가 비교됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**출력 특성**|예측 가능한 특성을 선택합니다. 모델을 만들었을 때 열을 예측 가능한 열로 정의하지 않은 경우 여기에서 열을 추가할 수 없습니다.|  
|**값 1**|**값 2**에 포함된 상태와 비교할 예측 가능한 특성의 상태를 선택합니다.<br /><br /> 두 불연속 값이나 불연속화 값을 비교할 수 있지만 다른 뷰어에서처럼 값을 보수와 비교할 수 없습니다.|  
|**값 2**|**값 1**에 포함된 상태와 비교할 예측 가능한 특성의 상태를 선택합니다.|  
  
 **변수**  
 **신경망** 탭의 이 부분에는 입력 및 출력 특성에 대해 선택하는 항목에 응답하는 대화형 막대 그래프가 포함되어 있습니다. 신경망에서 특정 값이 특정 결과에 영향을 주는 확률을 계산하기 때문에 어떠한 조합의 입력이든 선택할 수 있으며 가로 막대형 차트에 해당 조합이 비교할 결과 쌍에 미치는 영향이 표시됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**특성**|**특성**에서 선택한 입력 특성의 이름을 보여 줍니다.|  
|**Value**|선택한 입력 특성의 값을 보여 줍니다.|  
|**유사성 \<1 값 >**|이 특정 특성-값 조합이 **값 1**에서 선택한 대상 결과에 얼마나 많은 영향을 주는지를 나타내는 막대를 표시합니다.|  
|**유사성 \<2 값 >**|이 특정 특성-값 조합이 **값 2**에서 선택한 대상 결과에 얼마나 많은 영향을 주는지를 나타내는 막대를 표시합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어&#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
