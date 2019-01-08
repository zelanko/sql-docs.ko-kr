---
title: 마이닝 모델 테스트에 사용할 열 선택 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], predictable mining columns
- Mining Accuracy Chart [Analysis Services], columns
- predictable mining columns [Analysis Services]
ms.assetid: c6a8f23a-da21-4f31-9521-99460d624649
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 340080271318073983b29abebeab85122993b489
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540249"
---
# <a name="choose-the-column-to-use-for-testing-a-mining-model"></a>마이닝 모델 테스트에 사용할 열 선택
  마이닝 모델의 정확도를 측정하려면 먼저 평가할 결과를 결정해야 합니다. 대부분의 데이터 마이닝 모델에서는 모델을 만들 때 예측 가능한 특성으로 사용할 열을 하나 이상 선택해야 합니다. 따라서 모델의 정확도를 테스트할 때는 일반적으로 테스트할 특성을 선택해야 합니다.  
  
 다음 목록에서는 테스트에 사용할 예측 가능한 특성을 선택할 때 추가적으로 고려할 사항에 대해 설명합니다.  
  
-   일부 유형의 데이터 마이닝 모델에는 여러 특성와 같은 여러 특성 간의 관계를 탐색할 수 있는 신경망 예측할 수 있습니다.  
  
-   다른 유형의 마이닝 모델 등과 같이 클러스터링 모델 수행 하지 않을 예측 가능한 특성이 있습니다. 예측 가능한 특성이 없는 클러스터링 모델은 테스트할 수 없습니다.  
  
-   회귀 모델의 산점도를 만들거나 정확도를 측정하려면 연속된 예측 가능한 특성을 결과로 선택해야 합니다. 이 경우 대상 값은 지정할 수 없습니다. 산점도가 아닌 다른 항목을 만들려면 기본 마이닝 구조 열의 내용 유형이 **불연속** 또는 **분할**이어야 합니다.  
  
-   불연속 특성을 예측 가능한 결과로 선택한 경우에는 대상 값을 지정하거나 **예측 값** 필드를 비워 둘 수 있습니다. 포함 하는 경우는 **예측 값**, 차트에서 예측 된 대상 값 에서만 모델의 효율성을 측정 합니다. 대상 결과를 지정하지 않으면 모든 결과를 예측할 때 모델의 정확도가 측정됩니다.  
  
-   여러 모델을 포함하여 하나의 정확도 차트에서 비교하려면 모든 모델에서 동일한 예측 가능한 열을 사용해야 합니다.  
  
-   교차 유효성 검사 보고서를 만드는 경우에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 예측 가능한 특성이 동일한 모든 모델을 자동으로 분석합니다.  
  
-   **예측 열과 값 동기화**옵션을 선택한 경우에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 이름이 같고 데이터 형식이 일치하는 예측 가능한 열을 자동으로 선택합니다. 열이 이러한 조건을 충족하지 않는 경우 이 옵션을 해제하고 예측 가능한 열을 수동으로 선택할 수 있습니다. 모델과 다른 열이 있는 외부 데이터 집합을 사용하여 모델을 테스트하는 경우에 예측 가능한 열을 수동으로 선택해야 할 수 있습니다. 그러나 데이터 형식이 잘못된 열을 선택하면 오류가 발생하거나 잘못된 결과가 나타납니다.  
  
### <a name="specify-the-outcome-to-predict"></a>예측할 결과 지정  
  
1.  마이닝 구조를 두 번 클릭하여 데이터 마이닝 디자이너에서 엽니다.  
  
2.  **마이닝 정확도 차트** 탭을 선택합니다.  
  
3.  **입력 선택** 탭을 선택합니다.  
  
4.  **입력 선택** 탭의 **예측 가능한 열 이름**에서 행을 클릭하고 차트에 포함할 각 모델에 대한 예측 가능한 열을 선택합니다.  
  
     **예측 가능한 열 이름** 상자에 제공되는 마이닝 모델 열은 사용 유형이 **예측** 또는 **예측만**으로 설정된 열로 제한됩니다.  
  
5.  모델의 리프트를 결정하려면 **예측 값** 목록에서 측정할 특정 결과 값을 선택해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [모델 테스트 데이터 선택 및 매핑](choose-and-map-model-testing-data.md)   
 [정확도 차트 유형 선택 및 차트 옵션 설정](choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
