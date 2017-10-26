---
title: "데이터 마이닝 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ClusterCount property
- AllowedProvidersInOpenRowset property
- MinimumSeriesValue property
- ScoreMethod property
- MinimumImportance property
- ModellingCardinality property
- BrentTolerance property
- ComplexityPenalty property
- MaximumItemsetCount property
- MinimumSupport property
- AllowSessionMiningModels property
- HoldoutPercentage property
- ClusterCountPrior property
- MaximumSequenceStates property
- OptimizedPredictionCount property
- data mining [Analysis Services], properties
- MaximumStates property
- MaximumContinuousInputAttributes property
- MaximumOutputAttributes property
- AllowAdHocOpenRowsetQueries property
- Enabled property
- HistoricModelGap property
- SampleSize property
- MaximumInputAttributes property
- PeriodicityHint property
- MissingValueSubstitution property
- SplitMethod property
- ForceRegressor property
- MaximumBucketsForContinuousSplit property
- MaxConcurrentPredictionQueries property
- MinimumItemsetSize property
- AcyclicGraph property
- HoldoutMethod property
- StoppingTolerance property
- properties [data mining]
- AutoDetectPeriodicity property
- HoldoutTolerance property
- MinimumLeafCases property
- HoldoutSeed property
- MinimumClusterCases property
- ClusterCountDeviation property
- MinimumDependencyProbability property
- ClusteringMethod property
- MaximumItemsetSize property
- HiddenNodeRatio property
- MaximumSeriesValue property
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9d8dfbc8391518ff1375cf47102d4cb607992338
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-properties"></a>데이터 마이닝 속성
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 다음 표에 나열된 데이터 마이닝 서버 속성을 지원합니다. 추가 서버 속성 및 해당 속성 설정 방법에 대한 자세한 내용은 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)을 참조하세요.  
  
 **적용 대상:** 다차원 서버 모드에만  
  
## <a name="non-specific-category"></a>일반 범주  
 **AllowSessionMiningModels**  
 세션 마이닝 모델을 만들 수 있는지 여부를 나타내는 부울 속성입니다.  
  
 이 속성의 기본값은 False로 세션 마이닝 모델을 만들 수 없음을 나타냅니다.  
  
 **AllowAdHocOpenRowsetQueries**  
 임시로 열린 행 집합 쿼리가 허용되는지 여부를 나타내는 부울 속성입니다.  
  
 이 속성의 기본값은 False로 열린 행 집합 쿼리가 세션 중에는 허용되지 않음을 나타냅니다.  
  
 **AllowedProvidersInOpenRowset**  
 쉼표/세미콜론으로 구분된 공급자 ProgID 또는 그 외 경우 [All] 목록으로 구성된 열린 행 집합에서 어떤 공급자가 허용되는지를 식별하는 문자열 속성입니다.  
  
 **MaxConcurrentPredictionQueries**  
 최대 동시 예측 쿼리 수를 정의하는 부호 있는 32비트 정수 속성입니다.  
  
## <a name="algorithms-category"></a>알고리즘 범주  
 **Microsoft_Association_Rules\ Enabled**  
 Microsoft_Association_Rules 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **Microsoft_Clustering\ Enabled**  
 Microsoft_Clustering 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **Microsoft_Decision_Trees\ Enabled**  
 Microsoft_DecisionTrees 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **Microsoft_Naive_Bayes\ Enabled**  
 Microsoft_Naive_Bayes 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **Microsoft_Neural_Network\ Enabled**  
 Microsoft_Neural_Network 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **Microsoft_Sequence_Clustering\ Enabled**  
 Microsoft_Sequence_Clustering 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **Microsoft_Time_Series\ Enabled**  
 Microsoft_Time_Series 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **Microsoft_Linear_Regression\ Enabled**  
 Microsoft_Linear_Regression 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **Microsoft_Logistic_Regression\ Enabled**  
 Microsoft_Logistic_Regression 알고리즘이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
> [!NOTE]  
>  서버에서 사용할 수 있는 데이터 마이닝 서비스를 정의하는 속성 외에 특정 알고리즘의 동작을 정의하는 데이터 마이닝 속성도 있습니다. 이러한 속성은 서버 수준에서 데이터 마이닝 모델을 만들 때가 아니라 개별 데이터 마이닝 모델을 만들 때 구성합니다. 자세한 내용은 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [물리적 아키텍처&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  

