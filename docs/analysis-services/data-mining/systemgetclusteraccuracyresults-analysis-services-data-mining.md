---
title: SystemGetClusterAccuracyResults (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b9521cfd6e2b9ec0d08f290c60167c682c98e46f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019160"
---
# <a name="systemgetclusteraccuracyresults-analysis-services---data-mining"></a>SystemGetClusterAccuracyResults(Analysis Services - 데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  마이닝 구조 및 관련된 클러스터링 모델에 대한 교차 유효성 검사 정확도 메트릭을 반환합니다.  
  
 이 저장 프로시저는 전체 데이터 집합에 대한 메트릭을 하나의 파티션으로 반환합니다. 데이터 집합을 교집합 영역으로 분할하여 각 파티션에 대한 메트릭을 반환하려면 [SystemGetClusterCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)를 사용합니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 클러스터링 모델에 대해서만 사용할 수 있습니다. 클러스터링 이외의 모델의 경우 [SystemGetAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)를 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SystemGetClusterAccuracyResults(  
<mining structure>   
[,<mining model list>]  
,<data set>  
,<test list>])  
```  
  
## <a name="arguments"></a>인수  
 *마이닝 구조(mining structure)*  
 현재 데이터베이스의 마이닝 구조 이름입니다.  
  
 (필수)  
  
 *mining model list*  
 유효성을 검사할 모델의 쉼표로 구분된 목록입니다.  
  
 기본값은 **null**이며 이는 적용 가능한 모든 모델을 사용함을 의미합니다. 기본값을 사용할 경우 클러스터링 이외의 모델은 처리 후보 목록에서 자동으로 제외됩니다.  
  
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
  
 *테스트 목록*  
 테스트 옵션을 지정하는 문자열입니다. 이 매개 변수는 나중에 사용하도록 예약되어 있습니다.  
  
 (옵션)  
  
## <a name="return-type"></a>반환 형식  
 각 개별 파티션의 점수와 모든 모델에 대한 집계가 포함된 표입니다.  
  
 다음 표에는 **SystemGetClusterAccuracyResults**에서 반환하는 열이 나열되어 있습니다. 저장 프로시저에서 반환된 정보를 해석하는 방법은 [교차 유효성 검사 보고서의 측정값](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)을 참조하세요.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|ModelName|테스트한 모델의 이름입니다. **All** 은 결과가 모든 모델의 집계임을 나타냅니다.|  
|AttributeName|클러스터링 모델에는 적용되지 않습니다.|  
|AttributeState|클러스터링 모델에는 적용되지 않습니다.|  
|PartitionIndex|파티션을 나타내는 번호입니다.<br /><br /> 이 저장 프로시저의 경우에는 번호가 항상 0입니다.|  
|PartitionCases|테스트된 사례 수를 나타내는 정수입니다.|  
|테스트|수행한 테스트 유형입니다.|  
|이름|테스트에서 반환한 측정값의 이름입니다. 각 모델의 측정값은 모델 유형 및 예측 가능한 값의 유형에 따라 달라집니다.<br /><br /> 각 예측 가능 유형에 대해 반환된 측정값 목록은 [교차 유효성 검사 보고서의 측정값](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)을 참조하세요.<br /><br /> 각 측정값의 정의는 [교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)를 참조하세요.|  
|Value|클러스터 사례 유사도를 나타내는 확률 점수입니다.|  
  
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
 이 예에서는 vTargetMail 마이닝 구조에 연결되고 이름이 `Cluster 1` 과 `Cluster 2`인 클러스터링 모델 두 개에 대한 정확도 측정값을 반환합니다. 네 번째 줄의 코드는 각 모델과 관련된 필터를 사용하지 않고 테스트 사례만을 기준으로 결과를 반환해야 함을 나타냅니다.  
  
```  
CALL SystemGetClusterAccuracyResults (  
[vTargetMail],  
[Cluster 1], [Cluster 2],  
2  
)  
```  
  
 예제 결과:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|테스트|이름|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|클러스터 1|||0|5545|Clustering|사례 유사도|0.796514342249313|  
|클러스터 2|||0|5545|Clustering|사례 유사도|0.732122471228572|  
  
## <a name="requirements"></a>요구 사항  
 교차 유효성 검사는 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 해당)에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SystemGetCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services-데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services-데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemClusterGetAccuracyResults](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
