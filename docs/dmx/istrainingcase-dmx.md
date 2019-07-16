---
title: IsTrainingCase (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4a2dad29a3a1b0ca5fdae12b11b190fd7e59380f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937682"
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  사례를 지정된 데이터 마이닝 모델 또는 마이닝 구조의 학습 사례로 사용할지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>결과 유형  
 반환 **true** 사례가 학습 데이터 집합의 일부 이면 그렇지 않으면 **false**합니다.  
  
## <a name="remarks"></a>설명  
 데이터 마이닝 마법사를 사용하여 마이닝 구조 및 관련된 마이닝 모델을 만들면 테스트 데이터 집합으로 사용할 수 있도록 기본적으로 사례의 30%가 따로 설정됩니다. 사용자가 지정하는 데이터 원본의 나머지 사례는 모델을 학습하는 데 사용됩니다. 그러나 DMX(Data Mining Extensions)를 사용하여 마이닝 모델을 만들면 기본적으로 모든 데이터가 모델을 학습하는 데 사용되며 테스트 집합이 만들어지지 않습니다. 테스트 데이터 집합이 만들어지도록 하려면 WITH HOLDOUT 절의 매개 변수를 설정해야 합니다.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 및 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 속성 값을 통해 특정 데이터 마이닝 구조의 데이터가 테스트 집합과 학습 집합으로 분할되었는지 여부를 확인할 수 있습니다.  
  
> [!NOTE]  
>  모델의 사례에 대 한 정보를 반환할 IsTrainingCase 또는 IsTestCase 함수를 사용 하려는 경우 모델에 드릴스루를 사용 해야 합니다. 자세한 내용은 [마이닝 모델에 드릴스루 사용](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)을 참조하세요.  
  
 테스트 데이터 집합의 일부인 사례를 반환 하려면 함수를 사용 [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서 타겟된 메일링 시나리오에서 클러스터링 데이터 마이닝 모델을 사용 합니다 [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)합니다. 이 쿼리는 마이닝 모델을 학습하는 데 사용된 사례만 반환합니다. 또한 학습 사례는 40세 미만의 고객으로 제한됩니다.  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 데이터 마이닝에 사용 된 사례를 쿼리 하는 방법의 다른 예제를 참조 하세요 [선택에서 &#60;모델&#62;합니다. 경우 &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) 하 고 [SELECT FROM &#60;구조가&#62;합니다. 사례](../dmx/select-from-structure-cases.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [학습 및 테스트 데이터 집합](../analysis-services/data-mining/training-and-testing-data-sets.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [데이터 마이닝 쿼리](../analysis-services/data-mining/data-mining-queries.md)  
  
  
