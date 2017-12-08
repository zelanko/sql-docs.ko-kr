---
title: "테스트 데이터를 모델에 필터 적용 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input row filtering [SQL Server]
- filtering input rows [Analysis Services]
- Mining Accuracy Chart [Analysis Services], filtering input rows
ms.assetid: 9ccc9a23-5597-4b35-a05f-2fc8eb885147
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 39d35b7421b9d3ddeff5cede6e1539b34b7012c2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="apply-filters-to-model-testing-data"></a>모델 테스트 데이터에 필터 적용
  모델을 테스트하는 데 사용할 외부 데이터 원본을 지정할 경우 필요에 따라 입력 데이터를 제한하기 위한 필터를 적용할 수 있습니다. 예를 들어 특별히 특정 수입 범위 내의 고객에 대해 예측하기 위해 모델을 테스트하려고 할 수 있습니다.  
  
 예를 들어 Adventure Works의 대상인 메일링 시나리오에서 테스트 데이터가 포함된 테이블인 ProspectiveBuyer에 다음과 같은 필터 식을 만들고 사례를 수입 범위별로 테스트하도록 제한할 수 있습니다.  
  
 `[YearlyIncome] = '50000'`  
  
 필터의 동작은 모델 학습 데이터를 필터링하는지 테스트 데이터 집합을 필터링하는지에 따라 크게 달라집니다.  
  
-   테스트 데이터 집합에 대한 필터를 정의할 때는 들어오는 데이터에 대한 WHERE 절을 만듭니다. 모델을 평가하는 데 사용되는 입력 데이터 집합을 필터링할 경우 필터 식이 Transact-SQL 문으로 변환되고 차트 생성 시 입력 테이블에 적용됩니다. 따라서 테스트 사례 수가 크게 줄어들 수 있습니다.  
  
-   마이닝 모델에 필터를 적용할 때는 만드는 필터 식이 DMX(Data Mining Extensions) 문으로 변환되고 개별 모델에 적용됩니다. 따라서 모델에 필터를 적용할 때는 모델 학습에 원래 데이터의 하위 집합만 사용됩니다. 이 경우 모델이 특정 데이터 집합으로 조정되도록 한 가지 조건 집합을 사용하여 학습 모델을 필터링한 다음 다른 조건 집합을 사용하여 모델을 테스트하면 문제가 발생할 수 있습니다.  
  
-   구조를 만들 때 테스트 데이터 집합을 정의한 경우 학습에 사용되는 모델 사례에는 마이닝 구조 학습 집합에 있으며 **또한** 필터 조건에 맞는 사례만 포함됩니다. 따라서 모델을 테스트할 때 **마이닝 모델 테스트 사례 사용**옵션을 선택하면 테스트 사례에는 마이닝 구조 테스트 집합에 있으며 필터 조건에 맞는 사례만 포함됩니다. 그러나 홀드아웃 데이터 집합을 정의하지 않은 경우 테스트에 사용되는 모델 사례에는 필터 조건에 맞는 데이터 집합의 모든 사례가 포함됩니다.  
  
-   모델에 적용하는 필터 조건은 모델 사례에 대한 드릴스루 쿼리에도 적용됩니다.  
  
 요약하면, 여러 모델을 테스트할 때는 모든 모델이 동일한 마이닝 구조를 기반으로 하더라도 모델에 따라 학습 및 테스트에 다른 데이터 하위 집합이 사용될 수 있다는 것을 알고 있어야 합니다. 이 경우 정확도 차트에 다음과 같은 영향이 있을 수 있습니다.  
  
-   테스트 집합의 총 사례 수는 테스트하는 모델에 따라 달라질 수 있습니다.  
  
-   모델에서 서로 다른 학습 데이터 또는 테스트 데이터의 하위 집합이 사용되는 경우 차트에서 각 모델의 백분율이 정렬되지 않을 수 있습니다.  
  
 결과에 영향을 줄 수 있는 미리 정의된 필터가 모델에 포함되어 있는지 확인하려면 **속성** 창에서 **Filter** 속성을 확인하거나 데이터 마이닝 스키마 행 집합을 사용하여 모델을 쿼리합니다. 예를 들어 다음 쿼리는 지정된 모델에 대한 필터 텍스트를 반환합니다.  
  
 `SELECT [FILTER] FROM $system.DMSCHEMA_MINING_MODELS WHERE MODEL_NAME = 'name of model’`  
  
> [!WARNING]  
>  기존 마이닝 모델에서 필터를 제거하거나 필터 조건을 변경하려는 경우에는 마이닝 모델을 다시 처리해야 합니다.  
  
 적용할 수 있는 필터 종류에 대한 자세한 내용과 필터 식이 계산되는 방법은 [모델 필터 구문 및 예&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)를 참조하세요.  
  
### <a name="create-a-filter-on-external-testing-data"></a>외부 테스트 데이터에 대한 필터 만들기  
  
1.  테스트할 모델이 포함된 마이닝 구조를 두 번 클릭하여 데이터 마이닝 디자이너를 엽니다.  
  
2.  **마이닝 정확도 차트** 탭을 선택한 다음 **입력 선택** 탭을 선택합니다.  
  
3.  **입력 선택** 탭의 **정확도 차트에 사용할 데이터 집합을 선택하십시오.**에서 **다른 데이터 집합 지정**옵션을 선택합니다.  
  
4.  찾아보기 단추 **(…)** 를 클릭하여 대화 상자를 열고 외부 데이터 집합을 선택합니다.  
  
5.  사례 테이블을 선택하고, 필요한 경우 중첩된 테이블을 추가합니다. 필요한 경우 모델의 열을 외부 데이터 집합의 열에 매핑합니다. **열 매핑 지정** 대화 상자를 닫아 원본 테이블 정의를 저장합니다.  
  
6.  **필터 편집기 열기** 를 클릭하여 데이터 집합에 대한 필터를 정의합니다.  
  
     **데이터 집합 필터** 대화 상자가 열립니다. 구조에 중첩 테이블이 포함된 경우 두 부분으로 필터를 만들 수 있습니다. 먼저 **데이터 집합 필터** 대화 상자를 사용하여 사례 테이블에 대한 조건을 설정한 다음 **필터** 대화 상자를 사용하여 중첩 행에 대한 조건을 설정합니다.  
  
7.  **데이터 집합 필터** 대화 상자에서 **마이닝 구조 열**아래에 있는 표의 맨 위 행을 클릭하고 목록에서 테이블 또는 열을 선택합니다.  
  
     데이터 원본 뷰에 여러 테이블이나 중첩 테이블이 포함된 경우에는 먼저 테이블 이름을 선택해야 합니다. 또는 사례 테이블에서 열을 직접 선택할 수 있습니다.  
  
     필터링할 각 열에 대해 새 행을 추가합니다.  
  
8.  **연산자**및 **값** 열을 사용하여 열이 필터링되는 방법을 정의합니다.  
  
     **참고** 따옴표를 사용하지 않고 값을 입력하십시오.  
  
9. **및/또는** 입력란을 클릭하고 논리 연산자를 선택하여 여러 조건이 결합되는 방법을 정의합니다.  
  
10. 필요에 따라 **값** 텍스트 상자의 오른쪽에 있는 찾아보기 단추 **(…)** 를 클릭하여 **필터** 대화 상자를 열고 중첩 테이블 또는 개별 사례 테이블 열에 대한 조건을 설정합니다.  
  
11. **식** 창의 텍스트를 읽어 전체 필터 조건이 올바른지 확인합니다.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     필터 조건은 정확도 차트를 만들 때 데이터 원본에 적용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [모델 테스트 데이터 선택 및 매핑](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [사용 하 여 중첩 테이블 데이터를 입력으로 정확도 차트에 대 한](../../analysis-services/data-mining/using-nested-table-data-as-an-input-for-an-accuracy-chart.md)   
 [정확도 차트 유형 선택 및 차트 옵션 설정](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
