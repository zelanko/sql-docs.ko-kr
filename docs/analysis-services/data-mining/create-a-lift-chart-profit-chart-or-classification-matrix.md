---
title: "리프트 차트, 수익 차트 또는 분류표 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Mining Accuracy Chart [Analysis Services], mining structures
ms.assetid: aa3d052f-58a9-4417-8e7a-5e6feb562af0
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4b4e29848a830cde36521967265eba3de8b9929c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="create-a-lift-chart-profit-chart-or-classification-matrix"></a>리프트 차트, 수익 차트 또는 분류표 만들기
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]에 대 한 정확도 차트를 만들 수는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 5 단계에서 데이터 마이닝 모델:  
  
-   비교할 마이닝 모델을 포함하는 마이닝 구조를 선택합니다.  
  
-   차트에 추가할 마이닝 모델을 선택합니다.  
  
-   차트를 생성하는 데 사용할 테스트 데이터 원본을 지정합니다.  
  
-   차트 종류를 선택합니다.  
  
-   차트 옵션을 구성합니다.  
  
 이러한 기본 단계는 리프트 차트, 수익 차트 및 분류표에도 동일하게 사용됩니다. 다음 절차는 이러한 차트 종류에 대해 기본 차트 옵션을 구성하는 단계에 대해 설명합니다. 교차 유효성 검사 보고서를 만드는 방법에 대한 자세한 내용은 [교차 유효성 검사 보고서의 측정값](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)을 참조하세요.  
  
### <a name="open-the-mining-structure-in-the-accuracy-chart-designer"></a>정확도 차트 디자이너에서 마이닝 구조 열기  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 데이터 마이닝 디자이너를 엽니다.  
  
2.  솔루션 탐색기에서 마이닝 모델이 포함된 구조를 두 번 클릭합니다.  
  
3.  **마이닝 정확도 차트** 탭을 클릭합니다.  
  
### <a name="select-mining-models-for-inclusion-in-the-chart"></a>차트에 포함될 마이닝 모델 선택  
  
1.  **데이터 마이닝 디자이너의** 마이닝 정확도 차트 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭에서 **입력 선택** 탭을 클릭합니다.  
  
     현재 구조에서 동일한 예측 가능한 특성이 있는 모든 모델이 목록에 표시됩니다.  
  
2.  차트에 포함시킬 각 모델의 **표시** 상자를 선택합니다.  
  
3.  **예측 가능한 열 이름** 입력란을 클릭하고 목록에서 예측 가능한 열의 이름을 선택합니다. 하나의 차트에 입력한 모든 모델은 같은 예측 가능한 열을 사용해야 합니다.  
  
4.  두 개의 모델을 비교하는데 예측 가능한 열의 값이나 데이터 형식이 서로 다를 경우 **예측 열과 값 동기화** 확인란의 선택을 취소하여 강제로 비교를 수행합니다.  
  
    > [!NOTE]  
    >  **예측 열과 값 동기화** 확인란을 선택하면 Analysis Services는 모델의 예측 가능한 열 데이터를 분석하고 데이터를 테스트한 다음 가장 일치하는 항목을 찾습니다. 그러므로 부득이하게 열 비교를 강제로 수행해야 경우가 아니라면 이 확인란의 선택을 취소하지 마십시오.  
  
5.  **예측 값** 입력란을 클릭하고 목록에서 값을 선택합니다. 예측 가능한 열의 데이터 형식이 연속일 경우 입력란에 값을 입력해야 합니다.  
  
     자세한 내용은 [마이닝 모델 테스트에 사용할 열 선택](../../analysis-services/data-mining/choose-the-column-to-use-for-testing-a-mining-model.md)을 참조하세요.  
  
### <a name="select-testing-data"></a>테스트 데이터 선택  
  
1.  **마이닝 정확도 차트** 탭의 **입력 선택** 탭에서 **정확도 차트에 사용할 데이터 집합을 선택하십시오.**그룹의 옵션 중 하나를 선택하여 차트를 생성하는 데 사용할 데이터 원본을 지정합니다.  
  
    -   모델을 만드는 동안 적용되었을 수 있는 필터와 마이닝 구조 테스트 사례의 교차에 의해 정의되는 사례의 하위 집합을 사용하려면 **마이닝 모델 테스트 사례 사용**옵션을 선택합니다.  
  
    -   마이닝 구조 홀드아웃 데이터 집합의 일부로 정의된 전체 테스트 사례 집합을 사용하려면 **마이닝 구조 테스트 사례 사용**옵션을 선택합니다.  
  
    -   외부 데이터를 사용하려는 경우 **다른 데이터 집합 지정**옵션을 선택합니다.  데이터 집합을 데이터 원본 뷰로 사용할 수 있어야 합니다.   찾아보기(**…**) 단추를 클릭하여 정확도 차트에 사용할 데이터 테이블을 선택합니다. 자세한 내용은 [Choose and Map Model Testing Data](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)을 참조하세요.  
  
         외부 데이터 집합을 사용하고 있는 경우 선택적으로 입력 데이터 집합을 필터링할 수 있습니다. 자세한 내용은 [모델 테스트 데이터에 필터 적용](../../analysis-services/data-mining/apply-filters-to-model-testing-data.md)을 참조하세요.  
  
> [!NOTE]  
>  **입력 선택** 탭에서는 모델 테스트 사례 또는 마이닝 구조 테스트 사례에 대한 필터를 만들 수 없습니다. 마이닝 모델에 대한 필터를 만들려면 모델의 필터 속성을 수정하십시오. 자세한 내용은 [마이닝 모델에 필터 적용](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)을 참조하세요.  
  
### <a name="configure-chart-settings-and-generate-the-chart"></a>차트 설정 구성 및 차트 생성  
  
1.  **마이닝 정확도 차트** 탭에서 만들려는 차트 탭을 클릭합니다.  
  
2.  **리프트 차트**의 경우 **리프트 차트** 탭을 클릭합니다. 방금 선택한 모델, 예측 가능한 특성 및 입력 데이터를 기반으로 차트가 자동으로 생성됩니다.  
  
3.  **분류표**의 경우 **분류표** 탭을 클릭합니다. 추가 설정은 필요하지 않습니다. 선택한 입력 데이터 및 모델을 기반으로 차트가 자동으로 생성됩니다.  
  
4.  **수익 차트**의 경우 먼저 **리프트 차트** 탭을 클릭합니다. 그런 다음 **차트 종류** 드롭다운 목록에서 **수익 차트**를 선택합니다.  
  
     **수익 차트 설정** 대화 상자에서 다음 설정을 입력합니다.  
  
     **모집단**  
     리프트 차트를 만들 때 사용할 데이터 집합의 사례 수입니다.  
  
     모델은 항상 확률의 내림차순으로 사례를 선택합니다. 즉, 잠재 고객을 평가하는 중이고 고객 데이터베이스의 레코드 절반만 나타내는 수를 선택할 경우 사용자의 모델에 가장 적합한 사례의 하위 집합에 대한 정확도가 모델에서 측정됩니다.  
  
     이 이유 때문에 모델을 사용하여 메일을 생성하거나 캠페인을 만들 때 긍정적으로 응답할 확률이 가장 높은 고객만 대상으로 삼기 위해 각 사례와 관련된 예측 확률을 사용합니다.  
  
     **고정 비용**  
     비즈니스상의 문제와 관련된 고정 비용입니다.  
  
     대상 메일 솔루션에 대한 것일 경우 고정 비용은 홍보 메일 준비를 위한 초기 비용을 포함한 프린터 설치 요금을 나타낼 수 있습니다.  
  
     이 비용은 전체 대상 모집단에 한 번 적용됩니다.  
  
     **개별 비용**  
     고정 비용 외에 각 고객에게 연락하는 데 드는 비용입니다. 예를 들어 홍보 메일에 대한 우편 비용이나 전화를 거는 데 드는 비용을 입력할 수 있습니다.  
  
     이 비용은 전체 대상 모집단에 동일해야 합니다. 대상이 되는 사례 수를 각 값에 곱합니다.  
  
     **개인별 수익**  
     성공적인 각 판매와 관련된 수익입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [리프트 차트&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [분류표&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)  
  
  
