---
title: 특성 프로필 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.profiles.f1
ms.assetid: 17c7e7ae-273c-4a6b-9a35-e8b9b8e65999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b2bb75ec06d9b5c14ce5c2dcc85561412b362b40
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063167"
---
# <a name="attribute-profiles-tab-mining-model-viewer"></a>특성 프로필 탭(마이닝 모델 뷰어)
  **특성 프로필** 탭을 사용하여 Naive Bayes 모델 상태의 입력 값 분포가 결과 특성의 각 상태에 주는 영향을 확인할 수 있습니다. 값의 분포는 색이 지정된 히스토그램으로 표시되고 모든 분포가 표 형식으로 제공되므로 보다 쉽게 값을 비교할 수 있습니다.  
  
 **참조 항목:** [Microsoft Naive Bayes 알고리즘](data-mining/microsoft-naive-bayes-algorithm.md), [Microsoft Naive Bayes 뷰어를 사용 하 여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>변수  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 보려는 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **Viewer**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 각 마이닝 모델에 대해 제공되는 사용자 지정 뷰어나 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 콘텐츠 뷰어를 선택할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **범례 표시**  
 **상태** 의 각 값을 분포 차트에서 사용된 색 중 하나와 일치시키는 키를 표시하려면 이 옵션을 선택합니다.  
  
 **히스토그램 막대**  
 히스토그램에 포함할 막대 수를 선택합니다. 선택한 것보다 더 많은 막대가 있는 경우 가장 중요한 막대만 유지되고 나머지 막대는 모두 **기타**로 그룹화됩니다.  
  
 **예측 가능한**  
 마이닝 모델에서 예측 가능한 열을 선택합니다.  
  
 **특성 프로필**  
 테이블에는 다음 열이 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**특성**|마이닝 모델에 포함된 마이닝 모델 열을 나열합니다.|  
|**상태**|필요에 따라 특성의 해당 행에 있는 색이 나타내는 상태를 설명하는 열입니다. **범례 표시** 확인란을 사용하여 추가하거나 제거합니다.|  
|**모집단**|전체 데이터 세트의 특성 배포를 표시합니다.|  
|**예측 가능한 특성의 상태에 대 한 열**|각 행이 모델의 입력 특성에 해당하는 예측 가능한 열의 각 상태에 대한 열을 표시합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어&#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
