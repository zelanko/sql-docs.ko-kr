---
title: IsTrainingCase (DMX) | Microsoft Docs
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
- IsTrainingCase
dev_langs:
- DMX
helpviewer_keywords:
- IsTrainingCase function
ms.assetid: 63eab315-e743-470d-9c4c-edfc3f4058a3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ed062df083d4c11c635f9241eac38b4ec4406a32
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="istrainingcase-dmx"></a>IsTrainingCase(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사례를 지정된 데이터 마이닝 모델 또는 마이닝 구조의 학습 사례로 사용할지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>결과 유형  
 반환 **true** 경우의 학습 데이터 집합의 일부인 경우 그렇지 않으면 **false**합니다.  
  
## <a name="remarks"></a>주의  
 데이터 마이닝 마법사를 사용하여 마이닝 구조 및 관련된 마이닝 모델을 만들면 테스트 데이터 집합으로 사용할 수 있도록 기본적으로 사례의 30%가 따로 설정됩니다. 사용자가 지정하는 데이터 원본의 나머지 사례는 모델을 학습하는 데 사용됩니다. 그러나 DMX(Data Mining Extensions)를 사용하여 마이닝 모델을 만들면 기본적으로 모든 데이터가 모델을 학습하는 데 사용되며 테스트 집합이 만들어지지 않습니다. 테스트 데이터 집합이 만들어지도록 하려면 WITH HOLDOUT 절의 매개 변수를 설정해야 합니다.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 및 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 속성 값을 통해 특정 데이터 마이닝 구조의 데이터가 테스트 집합과 학습 집합으로 분할되었는지 여부를 확인할 수 있습니다.  
  
> [!NOTE]  
>  IsTrainingCase 또는 IsTestCase 함수를 사용 하 여 모델에 사례에 대 한 세부 정보를 반환 하려는 경우 모델에 드릴스루를 사용 해야 합니다. 자세한 내용은 [마이닝 모델에 드릴스루 사용](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)을 참조하세요.  
  
 테스트 데이터 집합의 일부인 사례를 반환 하려면 함수를 사용 하 여 [IsTestCase &#40; DMX &#41;](../dmx/istestcase-dmx.md)합니다.  
  
## <a name="examples"></a>예  
 타겟된 메일링 시나리오에서 클러스터링 데이터 마이닝 모델을 사용 하 여 다음 예제는 [기본 데이터 마이닝 자습서](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)합니다. 이 쿼리는 마이닝 모델을 학습하는 데 사용된 사례만 반환합니다. 또한 학습 사례는 40세 미만의 고객으로 제한됩니다.  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 데이터 마이닝에 사용 된 사례를 쿼리 하는 방법의 다른 예 참조 [SELECT FROM &#60; 모델 &#62;. 경우 &#40; DMX &#41; ](../dmx/select-from-model-cases-dmx.md) 및 [SELECT FROM &#60; 구조 &#62;. 경우](../dmx/select-from-structure-cases.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [학습 및 테스트 데이터 집합](../analysis-services/data-mining/training-and-testing-data-sets.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [데이터 마이닝 쿼리](../analysis-services/data-mining/data-mining-queries.md)  
  
  

