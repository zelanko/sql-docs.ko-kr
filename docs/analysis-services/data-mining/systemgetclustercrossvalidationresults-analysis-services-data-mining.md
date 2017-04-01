---
title: "SystemGetClusterCrossValidationResults(Analysis Services - 데이터 마이닝) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "SystemGetClusterCrossValidationResults"
  - "저장 프로시저 [Analysis Services], 데이터 마이닝"
  - "교차 유효성 검사 [데이터 마이닝]"
ms.assetid: 79de9b81-9f2e-4f20-ace9-e3b19d6a9759
caps.latest.revision: 21
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 21
---
# SystemGetClusterCrossValidationResults(Analysis Services - 데이터 마이닝)
  마이닝 구조를 지정된 수의 교집합 영역으로 분할하고 각 파티션의 모델을 학습한 다음 각 파티션의 정확도 메트릭을 반환합니다.  
  
 **참고** 이 저장 프로시저는 클러스터링 모델이 적어도 하나 포함되어 있는 마이닝 구조에만 사용할 수 있습니다. 클러스터링 이외의 모델에 대해 교차 유효성 검사를 실행하려면 [SystemGetCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)를 사용해야 합니다.  
  
## 구문  
  
```  
  
SystemGetClusterCrossValidationResults(  
<structure name>,   
[,<mining model list>]  
,<fold count>}  
,<max cases>  
<test list>])  
```  
  
## 인수  
 *마이닝 구조(mining structure)*  
 현재 데이터베이스의 마이닝 구조 이름입니다.  
  
 (필수)  
  
 *mining model list*  
 유효성을 검사할 마이닝 모델의 쉼표로 구분된 목록입니다.  
  
 마이닝 모델의 목록을 지정하지 않으면 지정된 구조와 연결된 모든 클러스터링 모델에 대해 교차 유효성 검사가 수행됩니다.  
  
> [!NOTE]  
>  클러스터링 모델이 아닌 모델의 교차 유효성 검사를 실행하려면 별도의 저장 프로시저인 [SystemGetCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)를 사용해야 합니다.  
  
 (옵션)  
  
 *접기 개수(fold count)*  
 데이터 집합을 분할할 파티션 수를 지정하는 정수입니다. 최소값은 2입니다. 최대 접기 수는 **maximum integer** 와 사례 수 중 더 작은 값입니다.  
  
 각 파티션에는 *max cases*/*fold count*와 거의 같은 수의 사례가 포함됩니다.  
  
 기본값은 없습니다.  
  
> [!NOTE]  
>  접기 수에 따라 교차 유효성 검사를 수행하는 데 필요한 시간이 크게 달라집니다. 너무 큰 값을 선택하면 쿼리가 장시간 실행될 수 있으며 경우에 따라서는 서버가 응답하지 않거나 제한 시간이 초과될 수 있습니다.  
  
 (필수)  
  
 *max cases*  
 테스트할 수 있는 최대 사례 수를 지정하는 정수입니다.  
  
 값을 0으로 지정하면 데이터 원본의 모든 사례가 사용됩니다.  
  
 데이터 집합의 실제 사례 수보다 큰 값을 지정하면 데이터 원본의 모든 사례가 사용됩니다.  
  
 (필수)  
  
 *테스트 목록*  
 테스트 옵션을 지정하는 문자열입니다.  
  
 **참고** 이 매개 변수는 나중에 사용하기 위해 예약되어 있습니다.  
  
 (옵션)  
  
## 반환 형식  
 반환 형식 표에는 각 개별 파티션의 점수와 모든 모델에 대한 집계가 포함됩니다.  
  
 다음 표에서는 반환되는 열을 설명합니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|ModelName|테스트한 모델의 이름입니다.|  
|AttributeName|예측 가능한 열의 이름입니다. 클러스터 모델의 경우 항상 **null**입니다.|  
|AttributeState|예측 가능한 열의 지정된 대상 값입니다. 클러스터 모델의 경우 항상 **null.**|  
|PartitionIndex|결과가 적용되는 파티션을 식별하는 인덱스(1부터 시작)입니다.|  
|PartitionSize|각 파티션에 포함된 사례 수를 나타내는 정수입니다.|  
|테스트|수행한 테스트 유형입니다.|  
|이름|테스트에서 반환한 측정값의 이름입니다. 각 모델의 측정값은 예측 가능한 값의 유형에 따라 달라집니다. 각 측정값의 정의는 [교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)를 참조하세요.<br /><br /> 각 예측 가능 유형에 대해 반환된 측정값 목록은 [교차 유효성 검사 보고서의 측정값](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)을 참조하세요.|  
|Value|지정된 테스트 측정값의 값입니다.|  
  
## 주의  
 전체 데이터 집합에 대한 정확도 메트릭을 반환하려면 [SystemGetClusterAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)를 사용합니다.  
  
 또한 마이닝 모델이 접기로 이미 분할된 경우에는 [SystemGetClusterAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)를 사용하여 처리를 건너뛰고 교차 유효성 검사의 결과만 반환할 수 있습니다.  
  
## 예  
 다음 예에서는 마이닝 구조를 3개의 접기로 분할한 다음 마이닝 구조에 연결된 클러스터링 모델 두 개를 테스트하는 방법을 보여 줍니다.  
  
 코드의 세 번째 줄에는 테스트할 마이닝 모델이 나열됩니다. 목록을 지정하지 않으면 구조에 연결된 모든 클러스터링 모델이 사용됩니다.  
  
 코드의 네 번째 줄에서는 접기 수를 지정하고 다섯 번째 줄에서는 사용할 최대 사례 수를 지정합니다.  
  
 모두 클러스터링 모델이므로 예측 가능한 특성이나 값을 지정하지 않아도 됩니다.  
  
```  
CALL SystemGetClusterCrossValidationResults(  
[v Target Mail],  
[Cluster 1], [Cluster 2],  
3,  
10000  
)  
```  
  
 예제 결과:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|테스트|이름|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|클러스터 1|||1.|3025|Clustering|사례 유사도|0.930524511864121|  
|클러스터 1|||2|3025|Clustering|사례 유사도|0.919184178430778|  
|클러스터 1|||3|3024|Clustering|사례 유사도|0.929651120490248|  
|클러스터 2|||1.|1289|Clustering|사례 유사도|0.922789726933607|  
|클러스터 2|||2|1288|Clustering|사례 유사도|0.934865535691068|  
|클러스터 2|||3|1288|Clustering|사례 유사도|0.924724595688798|  
  
## 요구 사항  
 교차 유효성 검사는 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 해당)에서만 사용할 수 있습니다.  
  
## 관련 항목:  
 [SystemGetCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  