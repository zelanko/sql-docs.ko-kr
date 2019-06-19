---
title: 입력 선택 탭 (마이닝 정확도 차트 뷰) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.columnmapping.f1
ms.assetid: f8b1193c-5c86-4c7e-8e35-158d293184fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3fb4771c7345eb270e91a377d2755a25606f9a93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080418"
---
# <a name="input-selection-tab-mining-accuracy-chart-view"></a>입력 선택 탭(마이닝 정확도 차트 뷰)
  **마이닝 정확도 차트** 디자이너의 **입력 선택** 탭을 사용하여 모델을 테스트하고 정확도 차트를 작성하는 데 사용되는 데이터 원본을 지정할 수 있습니다.  
  
 **자세한 내용은 다음을 참조하세요.** [테스트 및 유효성 검사&#40;데이터 마이닝&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>변수  
 **예측 열과 값**  **동기화**  
 표의 예측 가능한 여러 특성을 통합하여 특성의 이름이 달라도 모델을 학습하는 동안 특성이 동일한 예측 가능한 마이닝 구조 열에서 파생되도록 하려면 선택합니다.  
  
 **참고** 이 옵션은 기본적으로 선택되어 있습니다. 두 마이닝 구조 열이 동일한 기본 관계형 또는 다차원 원본에서 파생되며 이 두 열이 동일한 상태를 포함하거나 동일한 방법으로 불연속화된 경우에만 이 확인란의 선택을 취소해야 합니다.  
  
 **리프트 차트에 표시할 예측 가능한 마이닝 모델 열 선택**  
 리프트 차트에 포함될 모델 및 리프트 차트에서 해당 모델이 사용되는 방법을 제어하는 열을 포함하는 표입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**표시**|마이닝 모델의 예측 가능한 열 중 차트에 표시할 각 열의 이름 옆에 있는 상자를 선택합니다.<br /><br /> 차트가 너무 복잡해서 보기 어려우면 하나 이상의 열 옆에 있는 상자의 선택을 취소하여 차트를 간단하게 만듭니다.<br /><br /> 참고: 하나 이상의 열을 선택 하지 않으면 정확도 차트를 만들 수 없습니다.|  
|**마이닝 모델**|마이닝 구조에 포함된 마이닝 모델을 나열합니다.|  
|**예측 가능한 열 이름**|마이닝 모델에 포함된 예측 가능한 열 중 리프트 차트를 만드는 데 사용할 열을 선택합니다.|  
|**예측 값**|예측 가능한 열의 값을 선택합니다. 이 필드를 비워 두면 리프트 차트에서는 예측 가능한 열의 모든 상태에 대한 모델의 성능을 예측합니다.|  
  
 **정확도 차트에 사용할 데이터 집합 선택**  
 정확도 테스트 데이터를 지정하는 세 가지 옵션을 포함하는 옵션 그룹입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**마이닝 모델 테스트 사례 사용**|마이닝 구조를 분할할 때 만든 테스트 집합을 사용하고 모델에 정의된 필터를 적용합니다. 모델 필터에 대한 자세한 내용은 [Filters for Mining Models &#40;Analysis Services - Data Mining&#41;](data-mining/mining-models-analysis-services-data-mining.md)|  
|**마이닝 구조 테스트 사례 사용**|마이닝 구조를 분할할 때 만든 테스트 집합을 사용합니다.|  
|**다른 데이터 집합 지정**|기존 데이터 원본 뷰에서 테스트 데이터 집합으로 사용할 테이블을 지정합니다.|  
  
## <a name="filtering-options"></a>필터링 옵션  
 **다른 데이터 집합 지정**옵션을 선택하는 경우 데이터 원본 뷰를 정의하고 해당 데이터에 적용할 필터를 만들 수 있습니다. 필터를 만들 때는 데이터 원본 뷰에서 테스트 데이터를 반환하는 쿼리에 WHERE 절을 만드는 것입니다.  
  
 **참고**   **입력 선택** 탭을 사용하여 마이닝 모델에 필터를 지정할 수는 없습니다. 모델 필터를 만들려면 **마이닝 모델** 탭을 클릭하고 모델 속성을 편집하십시오.  
  
 마이닝 구조를 만들 때 테스트용 홀드아웃 집합을 만들지 않은 경우 이 옵션을 선택한 다음 원래 데이터 원본 뷰를 테스트 집합으로 지정할 수 있습니다. 이 해결 방법을 사용하면 원래 데이터 집합에 필터를 설정할 수도 있습니다.  
  
 **열 매핑 지정**  
 데이터 원본을 선택하고, 사례 테이블과 중첩 테이블을 지정하고, 외부 데이터 열을 마이닝 구조 열에 매핑하는 **열 매핑 지정** 대화 상자를 엽니다.  
  
 자세한 내용은 [열 매핑 지정 대화 상자&#40;마이닝 정확도 차트&#41;](specify-column-mapping-dialog-box-mining-accuracy-chart.md)를 참조하세요.  
  
 **필터 식**  
 필터 편집기를 사용하여 작성하는 필터 조건을 표시합니다.  
  
 **필터 편집기 열기**  
 외부 테이블을 선택하고 사례 테이블 열에 조건을 설정할 수 있는 **데이터 집합 필터** 대화 상자와 선택한 테이블의 개별 열 또는 중첩 테이블의 열에 적용되는 조건을 작성할 수 있는 **필터** 대화 상자를 엽니다.  
  
## <a name="see-also"></a>관련 항목  
 [테스트 및 유효성 검사 태스크 및 방법 &#40;데이터 마이닝&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [마이닝 정확도 차트 디자이너 &#40;데이터 마이닝&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [마이닝 모델에 필터를 적용 합니다.](data-mining/apply-a-filter-to-a-mining-model.md)   
 [마이닝 모델에 대한 필터&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/mining-models-analysis-services-data-mining.md)  
  
  
