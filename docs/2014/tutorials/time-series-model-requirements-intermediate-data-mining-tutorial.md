---
title: 시계열 모델에 대 한 요구 사항 이해 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1ce2b3e3-108a-4f7e-985f-a20b816d0da7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8e46d7fc8a0c214501841de448a94d1211b95fa1
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892966"
---
# <a name="understanding-the-requirements-for-a-time-series-model-intermediate-data-mining-tutorial"></a>시계열 모델에 대한 요구 사항 이해(중급 데이터 마이닝 자습서)
  예측 모델에서 사용할 데이터를 준비할 때 데이터에 시계열의 단계를 식별하는 데 사용할 수 있는 열이 포함되어 있는지 확인해야 합니다. 이 열은 `Key Time` 열로 지정됩니다. 이 열은 키이므로 고유 숫자 값을 포함해야 합니다.  
  
 `Key Time` 열에 대해 올바른 단위를 선택하는 것은 분석에 중요한 부분입니다. 예를 들어 판매 데이터가 분 단위로 갱신된다고 가정해 봅니다. 시계열에 대해 단위로 분을 사용할 필요는 없으며 판매 데이터를 날짜, 주 또는 월별로 롤업하는 것이 더 의미 있을 수 있습니다. 어떤 시간 단위를 사용할지 잘 모를 경우에는 각 집계에 대해 새 데이터 원본 뷰를 만들고 관련 모델을 작성하여 각 집계 수준에서 다른 추세가 나타나는지 확인할 수 있습니다.  
  
 이 자습서에서는 트랜잭션 판매 데이터베이스에서 판매 데이터가 일별로 수집되지만, 데이터 마이닝의 경우 데이터는 뷰를 사용하여 월별로 사전 집계됩니다.  
  
 또한 데이터 간격이 가능한 한 적을수록 분석에 적합합니다. 여러 데이터 계열을 분석하려는 경우 모든 계열이 가급적 같은 날짜에 시작하고 끝나야 합니다. 계열의 시작 또는 끝 외에 데이터 간격이 있을 경우 MISSING_VALUE_SUBSTITUTION 매개 변수를 사용하여 계열을 채울 수 있습니다. 또한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 평균 또는 상수 사용과 같이 누락된 데이터를 값으로 바꾸는 여러 가지 옵션을 제공합니다.  
  
> [!WARNING]  
>  이전 버전의 데이터 원본 뷰 디자이너에 포함되어 있던 피벗 차트 및 피벗 테이블 도구는 더 이상 제공되지 않습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에 포함된 데이터 프로파일러와 같은 도구를 사용하여 먼저 시계열 데이터의 간격을 식별하는 것이 좋습니다.  
  
### <a name="to-identify-the-time-key-for-the-forecasting-model"></a>예측 모델에 대한 시간 키를 식별하려면  
  
1.  **Salesbyregion dsv [Design]** 창에서 vTimeSeries 테이블을 마우스 오른쪽 단추로 클릭 한 다음 **데이터 탐색**을 선택 합니다.  
  
     **VTimeSeries 테이블 탐색**이라는 새 탭이 열립니다.  
  
2.  **테이블** 탭에서 Timeindex 및 Reporting Date 열에 사용 된 데이터를 검토 합니다.  
  
     이 두 열은 모두 고유한 값이 있는 시퀀스이며 시계열 키로 사용할 수 있지만 열의 데이터 형식이 서로 다릅니다. Microsoft 시계열 알고리즘에는 `datetime` 데이터 형식이 필요하지 않으며, 고유하게 정렬할 수 있는 값만 필요합니다. 따라서 한 열을 예측 모델에 대한 시간 키로 사용할 수 있습니다.  
  
3.  데이터 원본 뷰 디자인 화면에서 보고 날짜 열을 선택 하 고 **속성**을 선택 합니다. 그런 다음 TimeIndex 열을 클릭 하 고 **속성**을 선택 합니다.  
  
     TimeIndex 필드는 system.string 데이터 형식이 고, 필드 보고 날짜에는 system.string 데이터 형식이 있습니다. 많은 데이터 웨어하우스에서 날짜/시간 값을 정수로 변환하고 이 정수 열을 키로 사용하여 인덱싱 성능을 개선합니다. 그러나 이 열을 사용하는 경우 Microsoft 시계열 알고리즘은 201014 등의 미래 값을 사용하여 예측합니다. 달력 날짜를 사용 하 여 판매 데이터 예측을 표시 하려는 경우 보고 날짜 열을 고유한 계열 식별자로 사용 합니다.  
  
### <a name="to-set-the-key-in-the-data-source-view"></a>데이터 원본 뷰에 키를 설정하려면  
  
1.  **Salesbyregion dsv**창에서 vTimeSeries 테이블을 선택 합니다.  
  
2.  보고 날짜 열을 마우스 오른쪽 단추로 클릭 하 고 **논리적 기본 키 설정**을 선택 합니다.  
  
## <a name="handling-missing-data-optional"></a>누락된 데이터 처리(선택 사항)  
 계열에 누락된 데이터가 있을 경우 모델을 처리할 때 오류가 발생할 수 있습니다. 여러 가지 방법으로 누락된 데이터를 해결할 수 있습니다.  
  
-   평균을 계산하거나 이전 값을 사용하여 Analysis Services에서 누락된 값을 채우도록 할 수 있습니다. 이렇게 하려면 마이닝 모델에서 MISSING_VALUE_SUBSTITUTION 매개 변수를 설정합니다. 이 매개 변수에 대 한 자세한 내용은 [Microsoft 시계열 알고리즘 기술 참조](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)를 참조 하세요. 기존 마이닝 모델의 매개 변수를 변경 하는 방법에 대 한 자세한 내용은 [알고리즘 매개 변수 보기 또는 변경](../../2014/analysis-services/data-mining/view-or-change-algorithm-parameters.md)을 참조 하세요.  
  
-   데이터 원본을 변경하거나 기존 뷰를 필터링하여 비정형 계열을 삭제하거나 값을 바꿀 수 있습니다. 관계형 데이터 원본에서 이 작업을 수행하거나 명명된 사용자 지정 쿼리 또는 명명된 계산을 작성하여 데이터 원본 뷰를 수정할 수 있습니다. 자세한 내용은 [다차원 모델의 데이터 원본 뷰](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)를 참조하세요. 이 단원의 이후 태스크는 명명된 쿼리와 사용자 지정 계산을 작성하는 방식에 대한 예를 제공합니다.  
  
 이 시나리오의 경우 일부 데이터는 한 계열의 시작 부분에 없습니다. 즉, 7 월 2007 일까 지 T1000 제품 라인에 대 한 데이터가 없습니다. 이를 제외하면 모든 계열이 같은 날짜에 끝나며 누락된 값이 없습니다.  
  
 Microsoft 시계열 알고리즘의 요구 사항은 단일 모델에 포함 하는 모든 계열에 동일한 **끝점이** 있어야 한다는 점입니다. T1000 자전거 모델은 2007년에 추가되었으므로 이 계열의 데이터는 다른 자전거 모델의 계열보다 이후에 시작되지만 이 계열은 같은 날짜에 끝나므로 데이터를 사용할 수 있습니다.  
  
#### <a name="to-close-the-data-source-view-designer"></a>데이터 원본 뷰 디자이너를 닫으려면  
  
-   **VTimeSeries 테이블 탐색**탭을 마우스 오른쪽 단추로 클릭 하 고 **닫기**를 선택 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [예측 구조 및 모델 &#40;만들기 중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 시계열 알고리즘](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
