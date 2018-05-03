---
title: SystemGetCrossValidationResults (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SystemGetCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: f70c3337-c930-434a-b278-caf1ef0c3b3b
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cdb80f65fcde712def73201bcfe562ac7fe92149
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="systemgetcrossvalidationresults-analysis-services---data-mining"></a>SystemGetCrossValidationResults(Analysis Services - 데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  마이닝 구조를 지정된 수의 교집합 영역으로 분할하고 각 파티션의 모델을 학습한 다음 각 파티션의 정확도 메트릭을 반환합니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 클러스터링 모델 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘이나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 사용하여 작성된 모델에 대해 교차 유효성 검사를 실행하는 데 사용할 수 없습니다. 별도의 저장 프로시저인 [SystemGetClusterCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)를 사용하여 클러스터링 모델의 교차 유효성 검사를 실행할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SystemGetCrossValidationResults(  
<mining structure>  
[, <mining model list>]  
,<fold count>  
,<max cases>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>인수  
 *마이닝 구조(mining structure)*  
 현재 데이터베이스의 마이닝 구조 이름입니다.  
  
 (필수)  
  
 *mining model list*  
 유효성을 검사할 마이닝 모델의 쉼표로 구분된 목록입니다.  
  
 식별자 이름에 사용할 수 없는 문자가 모델 이름에 포함된 경우에는 이름을 괄호로 묶어야 합니다.  
  
 마이닝 모델의 목록을 지정하지 않으면 지정된 구조와 연결되었고 예측 가능한 특성을 포함하는 모든 모델에 대해 교차 유효성 검사가 수행됩니다.  
  
> [!NOTE]  
>  클러스터링 모델의 교차 유효성 검사를 실행하려면 별도의 저장 프로시저인 [SystemGetClusterCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)를 사용하여 클러스터링 모델의 교차 유효성 검사를 실행할 수 있습니다.  
  
 (옵션)  
  
 *접기 개수(fold count)*  
 데이터 집합을 분할할 파티션 수를 지정하는 정수입니다. 최소값은 2입니다. 최대 접기 수는 **maximum integer** 와 사례 수 중 더 작은 값입니다.  
  
 각 파티션에는 *max cases*/*fold count*와 거의 같은 수의 사례가 포함됩니다.  
  
 기본값은 없습니다.  
  
> [!NOTE]  
>  접기 수에 따라 교차 유효성 검사를 수행하는 데 필요한 시간이 크게 달라집니다. 너무 큰 값을 선택하면 쿼리가 장시간 실행될 수 있으며 경우에 따라서는 서버가 응답하지 않거나 제한 시간이 초과될 수 있습니다.  
  
 (필수)  
  
 *max cases*  
 모든 접기에 대해 테스트할 수 있는 최대 사례 수를 지정하는 정수입니다.  
  
 값을 0으로 지정하면 데이터 원본의 모든 사례가 사용됩니다.  
  
 데이터 집합의 실제 사례 수보다 큰 값을 지정하면 데이터 원본의 모든 사례가 사용됩니다.  
  
 기본값은 없습니다.  
  
 (필수)  
  
 *대상 특성*  
 예측 가능한 특성의 이름을 포함하는 문자열입니다. 예측 가능한 특성은 마이닝 모델의 열, 중첩 테이블 열 또는 중첩 테이블 키 열일 수 있습니다.  
  
> [!NOTE]  
>  대상 특성이 있는지 여부는 런타임에만 확인됩니다.  
  
 (필수)  
  
 *대상 상태*  
 예측할 값을 지정하는 수식입니다. 대상 값을 지정하면 지정한 값에 대해서만 메트릭이 수집됩니다.  
  
 값을 지정하지 않거나 값이 **null**이면 각 예측에서 가능성이 가장 높은 상태에 대해 메트릭이 계산됩니다.  
  
 기본값은 **null**입니다.  
  
 지정한 특성에 대해 지정한 값이 유효하지 않거나 수식의 유형이 올바르지 않으면 유효성을 검사하는 동안 오류가 발생합니다.  
  
 (옵션)  
  
 *대상*  *임계값*  
 0보다 크고 1보다 작은**Double** 이며, 지정된 대상 상태에 대한 예측을 올바른 것으로 간주하기 위해 얻어야 하는 최소 확률 점수를 나타냅니다.  
  
 확률이 이 값보다 작거나 같은 예측은 올바르지 않은 것으로 간주됩니다.  
  
 값을 지정하지 않거나 값이 **null**이면 확률 점수에 관계없이 가능성이 가장 높은 상태가 사용됩니다.  
  
 기본값은 **null**입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 설정 하는 경우 오류가 발생 하지 것입니다 *상태 임계값* 를 0.0으로이 값에 절대 사용 하지만 합니다. 실제로 임계값이 0.0이면 확률이 0%인 예측이 올바른 것으로 간주됨을 의미합니다.  
  
 (옵션)  
  
 *테스트 목록*  
 테스트 옵션을 지정하는 문자열입니다.  
  
 **참고** 이 매개 변수는 나중에 사용하기 위해 예약되어 있습니다.  
  
 (옵션)  
  
## <a name="return-type"></a>반환 형식  
 반환되는 행 집합에는 각 모델의 각 파티션에 대한 점수가 포함됩니다.  
  
 다음 표에서는 이 행 집합의 열을 설명합니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|ModelName|테스트한 모델의 이름입니다.|  
|AttributeName|예측 가능한 열의 이름입니다.|  
|AttributeState|예측 가능한 열의 지정된 대상 값입니다. 이 값이 **null**이면 가능성이 가장 높은 예측이 사용된 것입니다.<br /><br /> 이 열에 값이 있으면 이 값에 대해서만 모델의 정확도가 평가됩니다.|  
|PartitionIndex|결과가 적용되는 파티션을 식별하는 인덱스(1부터 시작)입니다.|  
|PartitionSize|각 파티션에 포함된 사례 수를 나타내는 정수입니다.|  
|테스트|수행된 테스트의 범주입니다. 범주 및 각 범주에 포함된 테스트에 대한 설명은 [교차 유효성 검사 보고서의 측정값](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)을 참조하세요.|  
|이름|테스트에서 반환한 측정값의 이름입니다. 각 모델의 측정값은 예측 가능한 값의 유형에 따라 달라집니다. 각 측정값의 정의는 [교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)를 참조하세요.<br /><br /> 각 예측 가능 유형에 대해 반환된 측정값 목록은 [교차 유효성 검사 보고서의 측정값](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)을 참조하세요.|  
|Value|지정된 테스트 측정값의 값입니다.|  
  
## <a name="remarks"></a>주의  
 전체 데이터 집합에 대한 정확도 메트릭을 반환하려면 [SystemGetAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)를 사용하여 클러스터링 모델의 교차 유효성 검사를 실행할 수 있습니다.  
  
 마이닝 모델이 접기로 이미 분할된 경우에는 [SystemGetAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)를 사용하여 클러스터링 모델의 교차 유효성 검사를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 교차 유효성 검사를 위해 마이닝 구조를 2개의 접기로 분할한 다음 `[v Target Mail]`이라는 마이닝 구조에 연결된 마이닝 모델 두 개를 테스트하는 방법을 보여 줍니다.  
  
 코드의 세 번째 줄에는 테스트할 마이닝 모델이 나열됩니다. 목록을 지정하지 않으면 구조에 연결된 모든 클러스터링 이외의 모델이 사용됩니다. 코드의 네 번째 줄에서는 파티션 수를 지정합니다. *max cases*에 값을 지정하지 않았으므로 마이닝 구조의 모든 사례가 사용되어 모든 파티션에 균등하게 분산됩니다.  
  
 다섯 번째 줄에서는 예측 가능한 특성으로 Bike Buyer를 지정하고 여섯 번째 줄에서는 예측할 값을 1("예. 구입합니다"를 의미함)로 지정합니다.  
  
 일곱 번째 줄의 NULL 값은 충족해야 할 최소 확률 기준이 없음을 나타냅니다. 따라서 확률이 0%가 아닌 첫 번째 예측이 정확도 평가에 사용됩니다.  
  
```  
CALL SystemGetCrossValidationResults(  
[v Target Mail],  
[Target Mail DT], [Target Mail NB],  
2,  
'Bike Buyer',  
1,  
NULL  
)  
```  
  
 예제 결과:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|테스트|이름|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Target Mail DT|Bike Buyer|1.|1.|500|분류|참 긍정|144|  
|Target Mail DT|Bike Buyer|1.|1.|500|분류|거짓 긍정|105|  
|Target Mail DT|Bike Buyer|1.|1.|500|분류|참 부정|186|  
|Target Mail DT|Bike Buyer|1.|1.|500|분류|거짓 부정|65|  
|Target Mail DT|Bike Buyer|1.|1.|500|Likelihood|로그 점수|-0.619042807138345|  
|Target Mail DT|Bike Buyer|1.|1.|500|Likelihood|리프트|0.0740963734002671|  
|Target Mail DT|Bike Buyer|1.|1.|500|Likelihood|제곱 평균 오차|0.346946279977653|  
|Target Mail DT|Bike Buyer|1.|2|500|분류|참 긍정|162|  
|Target Mail DT|Bike Buyer|1.|2|500|분류|거짓 긍정|86|  
|Target Mail DT|Bike Buyer|1.|2|500|분류|참 부정|165|  
|Target Mail DT|Bike Buyer|1.|2|500|분류|거짓 부정|87|  
|Target Mail DT|Bike Buyer|1.|2|500|Likelihood|로그 점수|-0.654117781086519|  
|Target Mail DT|Bike Buyer|1.|2|500|Likelihood|리프트|0.038997399132084|  
|Target Mail DT|Bike Buyer|1.|2|500|Likelihood|제곱 평균 오차|0.342721344892651|  
  
## <a name="requirements"></a>요구 사항  
 교차 유효성 검사는 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 해당)에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SystemGetCrossValidationResults](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services-데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services-데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults & #40; Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
