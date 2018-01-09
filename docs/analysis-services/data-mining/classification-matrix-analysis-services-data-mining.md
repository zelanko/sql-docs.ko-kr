---
title: "분류 행렬 (Analysis Services-데이터 마이닝) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- displaying mining accuracy
- confusion matrix [data mining]
- classification matrix [Analysis Services]
- accuracy testing [data mining]
ms.assetid: 5c12f202-2ed9-41fa-bee2-0f7ab3ff058a
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7897c756eb0aa9aa53ed56356052974e53afd601
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="classification-matrix-analysis-services---data-mining"></a>분류 행렬(Analysis Services - 데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]A *분류 행렬* 범주 예측된 값의 실제 값과 일치 하는지 여부를 확인 하 여 모델의 모든 사례를 정렬 합니다. 그런 다음 각 범주의 모든 사례 수가 계산되고 행렬에 합계가 표시됩니다. 분류 행렬은 통계 모델을 평가하기 위한 표준 도구로 *혼동 행렬*이라고도 합니다.  
  
 **분류 행렬** 옵션을 선택하면 생성되는 차트는 지정된 예측 상태별로 실제 값과 예측된 값을 비교합니다. 행렬에 대한 행은 모델의 예측 값을 나타내고 열은 실제 값을 나타냅니다. 분석에는 *거짓 긍정*, *참 긍정*, *거짓 부정*및 *참 부정*의 4가지 범주가 사용됩니다.  
  
 분류 행렬은 잘못된 예측의 영향을 간편하게 파악하고 분석할 수 있으므로 예측의 결과를 평가할 수 있는 중요한 도구입니다. 이 행렬의 각 셀에 나와 있는 합계와 비율을 통해 모델이 정확하게 예측한 빈도를 빠르게 확인할 수 있습니다.  
  
 이 섹션에서는 분류 행렬을 만드는 방법과 결과를 해석하는 방법에 대해 설명합니다.  
  
## <a name="understanding-the-classification-matrix"></a>분류 행렬 이해  
 기본 데이터 마이닝 자습서에서 만든 모델을 예로 들어 보겠습니다. 타겟 메일링 캠페인을 만드는 데 사용되는 [TM_DecisionTree] 모델을 사용하여 자전거를 구매할 가능성이 가장 많은 고객을 예측할 수 있습니다. 이 모델이 예측을 만드는 데 유효한지 평가하려면 결과 속성 [Bike Buyer]의 값에 대한 별도의 데이터 집합을 사용합니다. 일반적으로 모델 학습을 수행하는 데 사용되는 마이닝 구조를 작성할 때 따로 설정한 테스트 데이터 집합을 사용합니다.  
  
 예(고객이 자전거를 구매할 가능성이 있음)와 아니요(고객이 자전거를 구매할 가능성이 없음)의 두 가지 가능한 결과가 있습니다. 따라서 결과 분류 행렬은 상대적으로 간단합니다.  
  
## <a name="interpreting-the-results"></a>결과 해석  
 다음 표에 TM_DecisionTree 모델에 대한 분류 행렬이 나와 있습니다. 이 예측 가능한 특성에서 0은 구매 가능성이 없음을, 1은 구매 가능성이 있음을 의미합니다.  
  
|예측|0(실제)|1(실제)|  
|---------------|------------------|------------------|  
|0|362|144|  
|1.|121|373|  
  
 값 362가 포함된 첫 번째 결과 셀은 값 0에 대한 *참 긍정* 수를 나타냅니다. 0은 고객이 자전거를 구매하지 않았다는 것을 나타내므로 362개의 사례에서 모델이 자전거 비구매자에 대한 올바른 값을 예측했음을 이 통계에서 알 수 있습니다.  
  
 값 121을 포함하는 바로 아래의 셀은 *거짓 긍정*수 또는 누군가가 실제로 자전거를 구매하지 않았는데 자전거를 구매할 것이라고 모델에서 예측한 횟수를 나타냅니다.  
  
 값 144가 포함된 셀은 값 1에 대한 *거짓 긍정* 수를 나타냅니다. 1은 고객이 자전거를 구매했다는 것을 나타내므로 144개의 사례에서 누군가가 실제로 자전거를 구매했는데 자전거를 구매하지 않을 것이라 모델에서 예측했음을 이 통계에서 알 수 있습니다.  
  
 마지막으로 값 373을 포함하는 셀은 대상 값 1에 대한 참 긍정 수를 나타냅니다. 즉, 373개의 사례에서 모델은 누군가가 자전거를 구매할 것으로 정확하게 예측했습니다.  
  
 대각선으로 인접한 셀의 값에 대한 합계를 구하면 모델의 전체적인 정확도를 확인할 수 있습니다. 대각선 하나는 정확한 예측의 총 개수를 나타내고 다른 하나는 잘못된 예측의 총 개수를 나타냅니다.  
  
### <a name="using-multiple-predictable-values"></a>여러 예측 가능한 값 사용  
 [Bike Buyer] 사례는 두 개의 가능한 값만 있으므로 특히 쉽게 해석할 수 있습니다. 예측 가능한 특성에 여러 가능한 값이 있는 경우 분류 행렬은 각 가능한 실제 값에 대한 새 열을 추가하고 각 예측된 값에 대한 일치하는 항목 수를 계산합니다. 다음 표에서는 3개의 가능한 값(0, 1, 2)이 있는 다른 모델의 결과를 보여 줍니다.  
  
|예측|0(실제)|1(실제)|2(실제)|  
|---------------|------------------|------------------|------------------|  
|0|111|3|5|  
|1|2|123|17|  
|2|19|0|20|  
  
 열이 추가되어 보고서가 더 복잡해 보이지만 잘못된 예측의 누적 비용을 평가하려는 경우 추가 세부 정보가 매우 유용할 수 있습니다. 대각선의 합계를 구하거나 다른 행 조합의 결과를 비교하려면 **분류 행렬** 탭에서 제공된 **복사** 단추를 클릭하고 보고서를 Excel에 붙여넣습니다. 또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 지원하는 Excel용 데이터 마이닝 클라이언트와 같은 클라이언트를 사용하여 개수 및 비율을 모두 포함하는 분류 보고서를 Excel에서 직접 만들 수 있습니다. 자세한 내용은 [SQL Server 데이터 마이닝(SQL Server Data Mining)](http://go.microsoft.com/fwlink/?LinkID=77733)을 참조하십시오.  
  
## <a name="restrictions-on-the-classification-matrix"></a>분류 행렬의 제한 사항  
 분류 행렬은 예측 가능한 불연속 특성에서만 사용할 수 있습니다.  
  
 **마이닝 정확도 차트** 디자이너의 **입력 선택** 탭에서 모델을 선택할 때 여러 모델을 추가할 수 있지만 **분류 행렬** 탭에는 각 모델에 대해 별도의 행렬을 표시합니다.  
  
## <a name="related-content"></a>관련 내용  
 다음 항목에는 분류 행렬과 기타 차트를 만들고 사용하는 방법에 대해 보다 자세한 내용이 나와 있습니다.  
  
|항목|링크|  
|------------|-----------|  
|타겟 메일링 모델에 대한 리프트 차트를 만드는 방법을 보여 주는 연습을 제공합니다.|[기본 데이터 마이닝 자습서](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)<br /><br /> [리프트 차트를 사용하여 정확도 테스트&#40;기본 데이터 마이닝 자습서&#41;](http://msdn.microsoft.com/library/822d414b-4a39-473f-80c3-53476e30655a)|  
|관련 차트 종류에 대해 설명합니다.|[리프트 차트&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [수익 차트&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [산점도&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|마이닝 모델 및 마이닝 구조에 대한 교차 유효성 검사의 용도를 설명합니다.|[교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|리프트 차트 및 기타 정확도 차트를 만드는 단계를 설명합니다.|[테스트 및 유효성 검사 태스크 및 방법&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [테스트 및 유효성 검사&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
