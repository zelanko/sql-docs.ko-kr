---
title: "정확도 차트 유형 선택 및 집합 차트 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- Mining Accuracy Chart [Analysis Services]
- mining models [Analysis Services], validating
- classification accuracy [data mining]
- accuracy testing [data mining]
ms.assetid: bd24dd4a-624f-478a-9c94-b1361e857680
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40b6e4e67306c225af2ba3d2cd418ceaed2d2541
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="choose-an-accuracy-chart-type-and-set-chart-options"></a>정확도 차트 유형 선택 및 차트 옵션 설정
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 여러 가지 방법으로 마이닝 모델의 유효성을 확인할 수 있습니다. 각 모델 또는 구조에 대해 만들 수 있는 정확도 차트의 유형은 다음 요소에 따라 달라집니다.  
  
-   모델을 만드는 데 사용된 알고리즘 유형  
  
-   예측 가능한 특성의 데이터 형식  
  
-   측정할 예측 가능한 특성의 수  
  
 이 항목에서는 여러 가지 정확도 차트에 대해 간략하게 설명합니다.  
  
 **참고** 차트와 차트 정의는 저장되지 않습니다. 차트가 포함된 창을 닫으면 차트를 다시 만들어야 합니다.  
  
## <a name="accuracy-chart-types"></a>정확도 차트 유형  
 선택하는 차트 종류에 따라 옵션을 추가로 구성하거나, 차트를 찾아보거나, 차트를 클립보드에 복사하고 Excel에서 데이터를 사용할 수 있습니다.  
  
#### <a name="lift-chart"></a>리프트 차트  
 모델 및 테스트 데이터에 대한 옵션을 구성한 후에는 **리프트 차트** 탭을 클릭하여 결과를 볼 수 있습니다. 또한 차트를 클립보드에 복사하거나 마이닝 범례에서 개별 추세 선 또는 데이터 요소에 대한 세부 정보를 볼 수 있습니다.  
  
#### <a name="profit-chart"></a>수익 차트  
 모델 및 테스트 데이터에 대한 옵션을 구성한 후에는 **리프트 차트** 탭을 클릭하고 **차트 종류** 목록에서 **수익 차트** 를 선택하여 수익 차트 옵션을 설정한 다음 **확인** 을 클릭하여 결과를 볼 수 있습니다.  
  
 **수익 차트 설정** 대화 상자를 원하는 만큼 여러 번 사용하여 다른 비용 옵션을 시도하고 차트를 다시 표시할 수 있습니다. 마이닝 범례에는 각 모델의 예상 수익에 대한 세부 정보가 포함됩니다. 차트와 마이닝 범례의 내용을 클립보드에 복사하고 Excel에서 사용할 수도 있습니다.  
  
#### <a name="scatter-plot"></a>산점도  
 적절한 모델 유형을 선택한 경우 **리프트 차트** 탭을 클릭하면 차트 종류가 **산점도** 로 자동 설정되고 산점도가 표시됩니다. 더 이상의 추가 구성은 불가능합니다. 차트를 클립보드에 복사하고 Excel 또는 다른 응용 프로그램에 그래픽으로 붙여넣을 수도 있습니다.  
  
#### <a name="classification-matrix"></a>분류표  
 분류 행렬의 경우 **입력 선택** 탭을 사용하여 모델 및 테스트 데이터를 선택한 다음 **분류 행렬** 탭을 클릭하여 결과를 볼 수 있습니다.  
  
 분류 행렬의 내용은 모든 모델 유형에서 동일하며 구성할 수 없습니다. 차트의 데이터를 클립보드에 복사한 다음 Excel에서 사용할 수 있습니다.  
  
#### <a name="cross-validation-report"></a>교차 유효성 검사 보고서  
 교차 유효성 검사 보고서의 경우 솔루션 탐색기에서 마이닝 구조 또는 마이닝 모델을 선택한 후 **교차 유효성 검사** 탭을 클릭하고 모든 관련 옵션을 구성한 다음 **결과 가져오기** 를 클릭하여 보고서를 생성할 수 있습니다. 더 이상의 추가 구성은 불가능합니다.  
  
 교차 유효성 검사 보고서의 형식은 모든 모델 유형에서 동일하며 구성할 수 없습니다. 그러나 보고서의 내용은 분석하는 모델의 유형 및 예측 가능한 특성의 데이터 형식에 따라 달라집니다. 보고서의 결과를 클립보드에 복사하고 Excel에서 데이터를 사용할 수도 있습니다.  
  
  

