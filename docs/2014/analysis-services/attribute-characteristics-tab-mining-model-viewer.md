---
title: 특성 특징 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.characteristics.f1
ms.assetid: f0c3350d-84c0-4ab8-9fb8-1527c2647299
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e35cf7db00effb5ce700a1ac883877f67650d3cc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063044"
---
# <a name="attribute-characteristics-tab-mining-model-viewer"></a>특성 특징 탭(마이닝 모델 뷰어)
  **특성 특징** 창을 사용하여 Naïve Bayes 모델의 입력 특성과 결과 간의 관계를 탐색할 수 있습니다. 대상 특성의 값을 선택한 다음 결과에 가장 강한 영향을 주는 입력 특성의 목록을 볼 수 있습니다.  
  
 **참조 항목:** [Microsoft Naive Bayes 알고리즘](data-mining/microsoft-naive-bayes-algorithm.md), [Microsoft Naive Bayes 뷰어를 사용 하 여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조의 모델에서 보려는 마이닝 모델을 선택합니다. 마이닝 모델은 선택한 특정 모델 유형에 가장 적합한 사용자 지정 뷰어에서 자동으로 열립니다.  
  
 **Viewer**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 각 모델에 대해 사용자 지정 뷰어나 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어를 선택할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어도 이 목록에 나타납니다.  
  
 **특성**  
 분석하려는 예측 가능한 특성을 선택합니다.  
  
 **Value**  
 **특성**에서 설정한 예측 가능한 특성의 상태를 선택합니다. Naïve Bayes 모델은 연속 변수를 지원하지 않으므로 모든 대상 특성에는 불연속 또는 불연속화된 결과가 있습니다. 누락된 특성은 항상 자동으로 목록에 추가됩니다.  
  
 **에 대 한 특성 \<예측 가능한 상태 >**  
 이 그래프에는 입력 특성의 상태와 선택한 예측 가능한 특성 상태 간의 관계를 설명하는 다음 열이 포함되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**변수**|마이닝 모델의 입력 특성을 나열합니다.|  
|**값**|**변수**에 있는 입력 특성의 각 상태를 나열합니다.|  
|**확률**|이 막대는 행의 특성 및 값이 예측 가능한 특성의 선택한 상태와 관련되어 있을 확률을 나타냅니다. 이 막대를 마우스로 가리키면 백분율로 확률을 볼 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어&#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
