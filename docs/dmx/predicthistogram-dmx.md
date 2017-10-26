---
title: PredictHistogram (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictHistogram
dev_langs:
- DMX
helpviewer_keywords:
- PredictHistogram function
ms.assetid: 85ffc542-96e7-4f58-aaa3-34d76befcedf
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2e0d45b8169d567bbdc69a916f242b2707f6570
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="predicthistogram-dmx"></a>PredictHistogram(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 열의 예측에 대한 히스토그램을 나타내는 테이블을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열 참조 또는 클러스터 열 참조. [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘을 제외한 모든 알고리즘 유형에 사용할 수 있습니다.  
  
## <a name="return-type"></a>반환 형식  
 테이블입니다.  
  
## <a name="remarks"></a>주의  
 히스토그램은 통계 열을 생성합니다. 반환된 된 히스토그램의 열 구조와 함께 사용 되는 열 참조의 형식에 따라 달라 집니다는 **PredictHistogram** 함수입니다.  
  
## <a name="scalar-columns"></a>스칼라 열  
 에 대 한는 \<스칼라 열 참조 >, 히스토그램 하는 **PredictHistogram** 함수 반환 값은 다음과 같은 열로 구성 됩니다.  
  
-   예측되는 값  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]데이터 마이닝 알고리즘을 지원 하지 않는 **$ProbabilityVariance**합니다. 이 열은 항상 [!INCLUDE[msCoName](../includes/msconame-md.md)] 알고리즘에 대해 0을 포함합니다.  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]데이터 마이닝 알고리즘을 지원 하지 않는 **$ProbabilityStdev**합니다. 이 열은 항상 [!INCLUDE[msCoName](../includes/msconame-md.md)] 알고리즘에 대해 0을 포함합니다.  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability** 열은 프로그램 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 확장을는 [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB for Data Mining 사양 합니다.  
  
## <a name="cluster-columns"></a>클러스터 열  
 히스토그램 하는 **PredictHistogram** 함수에 대해 반환는 \<클러스터 열 참조 > 다음과 같은 열으로 구성 됩니다.  
  
-   **$Cluster** (클러스터 이름을 나타냄)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>예  
 다음 예에서는 단일 쿼리를 사용하여 Bike Buyer 열의 예측 상태를 반환합니다. 쿼리에서 사용 하 여 얻은 조정 된 확률을 기반으로 Bike Buyer 특성의 상위 두 가능성이 가장 높은 상태 세부 정보도 반환 된 **PredictHistogram** 함수입니다.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>참고 항목  
 [클러스터 &#40; DMX &#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40; DMX &#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40; DMX &#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40; DMX &#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40; DMX &#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40; DMX &#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40; DMX &#41;](../dmx/predictvariance-dmx.md)   
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

