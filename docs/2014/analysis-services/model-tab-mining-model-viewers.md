---
title: 모델 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.timeseries.decisiontree.f1
ms.assetid: 50570bb4-fcac-411e-b530-0398437efda7
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 932874065a56b98f8eb532f62206430152c794ae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081431"
---
# <a name="model-tab-mining-model-viewers"></a>모델 탭(마이닝 모델 뷰어)
  Microsoft 시계열 뷰어의 **모델** 탭에는 의사 결정 트리 모델에서 사용되는 것과 유사하게 그래프의 노드로 시계열이 표시됩니다.  
  
 이 시계열 모델 뷰를 사용하여 그래프에 대한 수식, ARIMA 항, 계수 등, 시계열 분석에 대한 유용한 정보를 추출할 수 있습니다.  
  
 **자세한 내용:** [Microsoft 시계열 알고리즘](data-mining/microsoft-time-series-algorithm.md), [Microsoft 시계열 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md), [Microsoft 시계열 알고리즘](data-mining/microsoft-time-series-algorithm.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 확인할 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 이 모델 유형에 대한 사용자 지정 뷰어 또는 **Microsoft 일반 콘텐츠 트리** 뷰어를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **확대/축소**  
 다이어그램을 확대합니다.  
  
 **축소**  
 다이어그램을 축소합니다.  
  
 **그래프 뷰 복사**  
 다이어그램에서 표시되는 섹션을 클립보드로 복사합니다.  
  
 **전체 그래프 복사**  
 전체 다이어그램을 클립보드로 복사합니다.  
  
 **창에 맞게 다이어그램 크기 조정**  
 전체 다이어그램이 화면에 표시될 때까지 다이어그램을 축소합니다.  
  
 **트리**  
 뷰어에서 표시할 트리를 드롭다운 목록에서 선택합니다.  
  
 시계열 모델에 여러 계열이 포함되어 있으면 각 계열이 별도의 트리로 표시됩니다. 예를 들어 [Quantity] 및 [Sales Amount]에 대한 시간에 따른 예측을 만든 경우 각 예측 가능한 특성에 대해 별도의 계열이 만들어집니다.  
  
 목록에서 강조 표시하는 색의 길이는 트리의 수준 수를 나타냅니다. 즉, 단일 노드로 나타낼 수 있는 시계열 모델에는 추세를 설명하는 단일 수식이 있고 색이 지정된 막대는 매우 짧습니다. 물론 모델이 혼합 모델인 경우 노드에는 ARIMA 및 ARTXP 수식이 모두 포함됩니다.  
  
 드롭다운 목록에 표시된 트리에 색이 지정된 더 긴 막대가 있는 경우 모델의 트리에 많은 분기가 있음을 의미합니다. 분기는 회귀가 더 복잡하고 모델이 각 노드에서 서로 다른 수식(또는 수식 쌍)을 사용하는 여러 세그먼트로 분할되어야 함을 의미합니다.  
  
 **배경**  
 각 노드의 배경색이 나타내는 상태를 선택하려면 이 컨트롤을 사용합니다.  
  
 **기본 확장**  
 모델의 모든 트리에 대해 표시되는 기본 수준 수를 조정합니다.  
  
 **수준 표시**  
 트리에 표시되는 수준 수를 변경합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  