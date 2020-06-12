---
title: IsTestCase (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 33c84ada33abee06a78fe0a9f8cc3f37242458ac
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670235"
---
# <a name="istestcase-dmx"></a>IsTestCase(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  사례가 지정된 데이터 마이닝 모델 또는 마이닝 구조의 테스트 사례로 사용되는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>결과 형식  
 사례가 테스트 데이터 집합의 일부인 경우 **true** 를 반환 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 데이터 마이닝 마법사를 사용하여 마이닝 구조 및 관련된 마이닝 모델을 만들면 테스트 데이터 집합으로 사용할 수 있도록 기본적으로 사례의 30%가 따로 설정됩니다. 나머지 사례는 데이터 마이닝 모델을 학습하는 데 사용됩니다. 해당 구조를 기반으로 하는 모든 모델에 동일한 테스트 데이터 집합을 사용할 수 있습니다. 그러나 DMX를 사용하여 마이닝 모델을 만들면 기본적으로 모든 데이터가 모델을 학습하는 데 사용되며 테스트 집합이 만들어지지 않습니다. 테스트 데이터 집합이 만들어지도록 하려면 WITH HOLDOUT 절의 매개 변수를 설정해야 합니다.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 및 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 속성의 값을 통해 테스트 집합이 특정 마이닝 구조에 대해 만들어졌는지 여부를 확인할 수 있습니다.  
  
> [!NOTE]  
>  IsTrainingCase 또는 IsTestCase 함수를 사용 하 여 특정 모델의 사례에 대 한 세부 정보를 반환 하려는 경우 모델에서 드릴스루를 사용 하도록 설정 해야 합니다. 자세한 내용은 [마이닝 모델에 드릴스루 사용](https://docs.microsoft.com/analysis-services/data-mining/enable-drillthrough-for-a-mining-model)을 참조하세요.  
  
 학습 데이터 집합의 일부인 사례를 반환 하려면 [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)함수를 사용 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Targeted Mailing` [기본 데이터 마이닝 자습서](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 만든 마이닝 구조를 사용 합니다. 쿼리는 테스트에 사용된 구조의 모든 사례를 반환합니다.  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 데이터 마이닝에 사용 되는 사례를 쿼리 하는 방법에 대 한 자세한 내용은 [SELECT FROM &#60;model&#62;을 참조 하세요. DMX&#41;&#40;사례](../dmx/select-from-model-cases-dmx.md) 는 [&#60;구조&#62;에서 선택 합니다. 사례](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>참고 항목  
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [데이터 마이닝 쿼리](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)   
 [데이터 집합 학습 및 테스트](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)  
  
  
