---
title: 시퀀스 클러스터링 클러스터 판별 탭 (마이닝 모델 뷰어) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.discrimination.f1
ms.assetid: 7dd16479-2633-4f4b-83bf-cf55972a2241
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 914629fca09d4bcffb5ac931316331bbb7e7eebe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66069143"
---
# <a name="sequence-clustering-cluster-discrimination-tab-mining-model-viewer"></a>시퀀스 클러스터링 클러스터 판별 탭(마이닝 모델 뷰어)
  **Microsoft 시퀀스 클러스터링 뷰어** 의 **클러스터 판별** 탭에서는 시퀀스 클러스터링 모델에서 선택한 클러스터를 비교합니다.  
  
 이 시퀀스 클러스터링 모델 뷰를 사용하여 두 클러스터를 비교하고 서로 다른 상태와 전환을 확인할 수 있습니다.  
  
 **자세한 내용:** [Microsoft 시퀀스 클러스터링 알고리즘](data-mining/microsoft-sequence-clustering-algorithm.md), [Microsoft 시퀀스 클러스터 뷰어를 사용하여 모델 찾아보기](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>옵션  
 **뷰어 내용 새로 고침**  
 뷰어에서 마이닝 모델을 다시 로드합니다.  
  
 **마이닝 모델**  
 현재 마이닝 구조에서 볼 마이닝 모델을 선택합니다. 관련 뷰어에서 마이닝 모델이 열립니다.  
  
 **뷰어**  
 선택한 마이닝 모델을 탐색하는 데 사용할 뷰어를 선택합니다. 사용자 지정 뷰어 또는 **Microsoft 일반 콘텐츠 트리 뷰어**를 사용할 수 있습니다. 또한 사용 가능한 경우 플러그 인 뷰어를 사용할 수 있습니다.  
  
 **클러스터 1**  
 모델에서 클러스터를 선택합니다.  
  
 **클러스터 2**  
 **클러스터 1**과 비교할 두 번째 클러스터를 마이닝 모델에서 선택합니다.  
  
 다른 클러스터를 선택하지 않으면 기본적으로 선택된 클러스터가 해당 보수와 비교되므로 클러스터 1에 없는 모델의 모든 사례와 비교됩니다.  
  
 **클러스터 1> \<및 \<클러스터 2>에 대 한 판별 점수**  
 이 차트에서는 선택한 클러스터를 자세히 비교합니다. 일반적으로 클러스터링 모델은 단일 클러스터에만 상태나 값을 할당하는 일이 거의 없습니다. 따라서 뷰어에서는 특정 특성이나 상태가 특정 클러스터와 *유사* 하다는 것만 나타냅니다.  
  
 전반적으로 특정 클러스터에는 상태가 둘 이상 포함될 수 있습니다.예를 들어 일반 상태는 Water Bottle 및 Water Bottle Cage를 순서대로 구매하는 것일 수 있습니다. 그러나 이 순서는 보다 중요한 결정적인 특징이 있는 다른 클러스터에도 존재합니다. 예를 들어 다른 클러스터의 가장 강한 특징은 매우 짧은 트랜잭션 시간이고, 분석은 Water Bottle 및 Water Bottle Cage 항목이 항상 그런 것은 아니지만 일반적으로 이 클러스터에 그룹화될 수 있음을 보여 줍니다.  
  
|값|설명|  
|-----------|-----------------|  
|**변수**|마이닝 모델의 특성입니다.|  
|**값**|**변수**에 나열된 특성의 상태입니다.|  
|**클러스터 \<1>에 우선**|**변수** 및 **값** 에 나열된 특성 및 상태와 **클러스터 1**에서 선택한 클러스터의 유사한 정도를 나타내는 음영 처리된 막대를 포함합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 모델 뷰어 &#40;데이터 마이닝 모델 디자이너&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [데이터 마이닝 모델 뷰어](data-mining/data-mining-model-viewers.md)  
  
  
