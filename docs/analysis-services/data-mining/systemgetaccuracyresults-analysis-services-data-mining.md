---
title: "SystemGetAccuracyResults (Analysis Services-데이터 마이닝) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetAccuracyResults
- cross-validation [data mining]
ms.assetid: 54ff584c-c6ce-4c31-9515-0a645719bd1a
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6b2eca528b40afd905661e2508e93529159b8627
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="systemgetaccuracyresults-analysis-services---data-mining"></a>SystemGetAccuracyResults(Analysis Services - 데이터 마이닝)
  클러스터링 모델을 제외한 모든 관련 모델 및 마이닝 구조에 대한 교차 유효성 검사 정확도 메트릭을 반환합니다.  
  
 이 저장 프로시저는 전체 데이터 집합에 대한 메트릭을 하나의 파티션으로 반환합니다. 데이터 집합을 교집합 영역으로 분할하여 각 파티션에 대한 메트릭을 반환하려면 [SystemGetCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)를 사용합니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘이나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 사용하여 작성된 모델에 대해서는 지원되지 않습니다. 또한 클러스터링 모델인 경우 별도의 저장 프로시저 [SystemGetClusterAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)를 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SystemGetAccuracyResults(<mining structure>,   
[,<mining model list>]  
,<data set>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>인수  
 *마이닝 구조(mining structure)*  
 현재 데이터베이스의 마이닝 구조 이름입니다.  
  
 (필수)  
  
 *모델 목록*  
 유효성을 검사할 모델의 쉼표로 구분된 목록입니다.  
  
 기본값은 **null**입니다. null 값은 적용 가능한 모든 모델이 사용됨을 의미합니다. 기본값을 사용할 경우 클러스터링 모델은 처리 후보 목록에서 자동으로 제외됩니다.  
  
 (옵션)  
  
 *데이터 집합(data set)*  
 마이닝 구조에서 테스트용으로 사용되는 파티션을 나타내는 정수 값입니다. 이 값은 다음 값의 합계를 나타내는 비트 마스크에서 파생되며 각 값은 선택 사항입니다.  
  
|||  
|-|-|  
|학습 사례|0x0001|  
|테스트 사례|0x0002|  
|모델 필터|0x0004|  
  
 가능한 값의 전체 목록은 이 항목의 설명 섹션을 참조하십시오.  
  
 (필수)  
  
 *대상 특성*  
 예측 가능한 개체의 이름을 포함하는 문자열입니다. 예측 가능한 개체는 마이닝 모델의 열, 중첩 테이블 열 또는 중첩 테이블 키 열일 수 있습니다.  
  
 (필수)  
  
 *대상 상태*  
 예측할 특정 값을 포함하는 문자열입니다.  
  
 값을 지정하면 해당 상태에 대해 메트릭이 수집됩니다.  
  
 값을 지정하지 않거나 null을 지정하면 각 예측에서 가능성이 가장 높은 상태에 대해 메트릭이 계산됩니다.  
  
 기본값은 **null**입니다.  
  
 (옵션)  
  
 *대상 임계값*  
 0.0에서 1 사이의 숫자로, 예측 값이 올바른 것으로 간주되는 최소 확률을 지정합니다.  
  
 기본값은 **null**이며 이는 모든 예측이 올바른 것으로 간주됨을 의미합니다.  
  
 (옵션)  
  
 *테스트 목록*  
 테스트 옵션을 지정하는 문자열입니다. 이 매개 변수는 나중에 사용하도록 예약되어 있습니다.  
  
 (옵션)  
  
## <a name="return-type"></a>반환 형식  
 반환되는 행 집합에는 각 파티션의 점수와 모든 모델에 대한 집계가 포함됩니다.  
  
 다음 표에는 **GetValidationResults**에서 반환하는 열이 나열되어 있습니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|Model|테스트한 모델의 이름입니다. **All** 은 결과가 모든 모델의 집계임을 나타냅니다.|  
|AttributeName|예측 가능한 열의 이름입니다.|  
|AttributeState|예측 가능한 열의 대상 값입니다.<br /><br /> 이 열에 값이 있으면 지정된 상태에 대해서만 메트릭이 수집됩니다.<br /><br /> 이 값을 지정하지 않거나 값이 null이면 각 예측에서 가능성이 가장 높은 상태에 대해 메트릭이 계산됩니다.|  
|PartitionIndex|결과가 적용되는 파티션을 나타냅니다.<br /><br /> 이 프로시저의 경우에는 값이 항상 0입니다.|  
|PartitionCases|에 따라 사례 집합의 행 수를 나타내는 정수는  *\<데이터 집합 >* 매개 변수입니다.|  
|테스트|수행한 테스트 유형입니다.|  
|이름|테스트에서 반환한 측정값의 이름입니다. 각 모델의 측정값은 모델 유형 및 예측 가능한 값의 유형에 따라 달라집니다.<br /><br /> 각 예측 가능 유형에 대해 반환된 측정값 목록은 [교차 유효성 검사 보고서의 측정값](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)을 참조하세요.<br /><br /> 각 측정값의 정의는 [교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)를 참조하세요.|  
|Value|지정된 측정값에 대한 값입니다.|  
  
## <a name="remarks"></a>주의  
 다음 표에서는 교차 유효성 검사에 사용되는 마이닝 구조의 데이터를 지정하는 데 사용할 수 있는 값의 예를 보여 줍니다. 교차 유효성 검사에 테스트 사례를 사용하려면 마이닝 구조에 테스트 데이터 집합이 이미 포함되어 있어야 합니다. 마이닝 구조를 만들 때 테스트 데이터 집합을 정의하는 방법에 대한 자세한 내용은 [데이터 집합 학습 및 테스트](../../analysis-services/data-mining/training-and-testing-data-sets.md)를 참조하세요.  
  
|정수 값|Description|  
|-------------------|-----------------|  
|1.|학습 사례만 사용합니다.|  
|2|테스트 사례만 사용합니다.|  
|3|학습 사례와 테스트 사례를 모두 사용합니다.|  
|4|잘못된 조합입니다.|  
|5|학습 사례만 사용하고 모델 필터를 적용합니다.|  
|6|테스트 사례만 사용하고 모델 필터를 적용합니다.|  
|7|학습 및 테스트 사례를 모두 사용하고 모델 필터를 적용합니다.|  
  
 교차 유효성 검사를 사용할 수 있는 시나리오에 대한 자세한 내용은 [테스트 및 유효성 검사&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)를 참조하세요.  
  
## <a name="examples"></a>예  
 이 예에서는 `v Target Mail DT`마이닝 구조에 연결된 `vTargetMail` 라는 의사 결정 트리 모델 하나에 대해 정확도 측정값을 반환합니다. 네 번째 줄의 코드는 결과가 테스트 사례를 기반으로 하고 모델별 필터를 사용하여 각 모델에 대해 필터링되어야 함을 나타냅니다.  `[Bike Buyer]` 는 예측할 열을 지정하고 그 다음 줄에 나오는 1은 "예. 구입합니다"를 의미하는 1이라는 값에 대해서만 모델을 평가해야 함을 나타냅니다.  
  
 코드의 마지막 줄에서는 상태 임계값을 0.5로 지정합니다. 이는 정확도를 계산할 때 확률이 50% 이상인 예측을 "올바른" 예측으로 간주해야 함을 나타냅니다.  
  
```  
CALL SystemGetAccuracyResults (  
[vTargetMail],  
[vTargetMail DT],  
6,  
'Bike Buyer',  
1,  
0.5  
)  
```  
  
 예제 결과:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|테스트|이름|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|v Target Mail DT|Bike Buyer|1.|0|1638|분류|참 긍정|605|  
|v Target Mail DT|Bike Buyer|1.|0|1638|분류|거짓 긍정|177|  
|v Target Mail DT|Bike Buyer|1.|0|1638|분류|참 부정|501|  
|v Target Mail DT|Bike Buyer|1.|0|1638|분류|거짓 부정|355|  
|v Target Mail DT|Bike Buyer|1.|0|1638|Likelihood|로그 점수|-0.598454638753028|  
|v Target Mail DT|Bike Buyer|1.|0|1638|Likelihood|리프트|0.0936717116894395|  
|v Target Mail DT|Bike Buyer|1.|0|1638|Likelihood|제곱 평균 오차|0.361630800104946|  
  
## <a name="requirements"></a>요구 사항  
 교차 유효성 검사는 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 해당)에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SystemGetCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40; Analysis Services-데이터 마이닝 &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  

