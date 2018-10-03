---
title: 대체 데이터 (중급 데이터 마이닝 자습서)를 사용 하 여 시계열 예측 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 815b50c8d687c1df76b9dc5de4b1fbe34f15f233
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120285"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>대체 데이터를 사용한 시계열 예측(중급 데이터 마이닝 자습서)
  이 태스크에서는 전 세계 판매 데이터를 기준으로 새 모델을 작성합니다. 그런 다음 개별 지역 중 한 곳에 전 세계 판매 모델을 적용하는 예측 쿼리를 만듭니다.  
  
## <a name="building-a-general-model"></a>일반 모델 작성  
 원래 마이닝 모델의 결과 분석에서는 특정 지역 간 및 제품 라인 간에 큰 차이를 보였음을 기억하십시오. 예를 들어 북미 지역에서는 M200 모델의 판매량이 높았던 반면 T1000 모델의 판매량은 그다지 높지 않았습니다. 그러나 일부 계열에는 그리 많지 않은 데이터가 포함되어 있었고 데이터마다 다른 시간에 시작되었다는 점 때문에 분석이 복잡해집니다. 일부 데이터는 누락되기도 했습니다.  
  
 ![M200 및 T1000 수량을 예측 하는 계열](../../2014/tutorials/media/6series-defaultforecasting.gif "M200 및 T1000 수량을 예측 하는 계열")  
  
 데이터 품질 문제 중 일부를 해결하기 위해, 전 세계의 판매 데이터를 병합하고 일반적인 해당 판매 추세 집합을 사용하여 모든 지역에서의 향후 판매를 예측하는 데 적용할 수 있는 모델을 작성합니다.  
  
 예측을 만들 때는 전 세계 판매 데이터에 대한 학습을 통해 생성된 패턴을 사용하지만 기록 데이터 요소는 각 개별 지역의 판매 데이터로 바꿉니다. 이 방법을 통해 추세의 셰이프는 보존되나 예측 값은 각 지역 및 모델에 대한 판매 기록 수치에 정렬됩니다.  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>시계열 모델에 교차 예측 수행  
 다른 계열의 추세를 예측하기 위해 계열 하나의 데이터를 사용하는 프로세스를 교차 예측이라고 합니다. 대부분의 시나리오에서는 교차 예측을 사용할 수 있습니다: 예를 들어 텔레비전 sales 전반적인 경제 활동의 좋은 지표가 이며 텔레비전 영업을 일반 경제 데이터에서 학습 된 모델을 적용을 결정할 수 있습니다.  
  
 교차 예측 함수에 대 한 인수 내의 매개 변수 REPLACE_MODEL_CASES를 사용 하 여 수행 하면에서 SQL Server 데이터 마이닝 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)합니다.  
  
 다음 태스크에서는 REPLACE_MODEL_CASES를 사용하는 방법을 배워 봅니다. 병합된 전 세계 판매 데이터를 사용하여 모델을 작성한 다음 일반 모델을 대체 데이터에 매핑하는 예측 쿼리를 만듭니다.  
  
 사용자가 현재 데이터 마이닝 모델을 작성하는 방법에 익숙하다고 가정하고 모델 작성 지침을 간소화했습니다.  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>집계 데이터를 사용하여 마이닝 구조 및 마이닝 모델을 작성하려면  
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **마이닝 구조**를 선택한 후 **새 마이닝 구조** 데이터 마이닝 마법사를 시작 합니다.  
  
2.  데이터 마이닝 마법사에서 다음을 선택합니다.  
  
    -   알고리즘: Microsoft 시계열  
  
    -   이 고급 단원에서 이전에 작성했던 데이터 원본을 모델의 원본으로 사용합니다. 참조 [고급 시계열 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)합니다.  
  
         데이터 원본 뷰: `AllRegions`  
  
    -   계열 키 및 시간 키에 대해 다음 열을 선택합니다.  
  
         시간 키: ReportingDate  
  
         키: 지역  
  
    -   `Input` 및 `Predict`에 대해 다음 열을 선택합니다.  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   에 대 한 **마이닝 구조 이름**, 유형: `All Regions`  
  
    -   에 대 한 **마이닝 모델 이름**, 유형: `All Regions`  
  
3.  새 구조 및 새 모델을 처리합니다.  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>예측 쿼리를 작성하고 대체 데이터를 매핑하려면  
  
1.  모델이 아직 열려 있지 않으면 AllRegions 구조를 두 번 클릭 하 고 데이터 마이닝 디자이너에서을 클릭 합니다 **마이닝 모델 예측** 탭 합니다.  
  
2.  에 **마이닝 모델** 창, 이미 선택 되어 AllRegions 모델입니다. 선택 하지 않으면 클릭 **모델 선택**, 한 다음 AllRegions 모델을 선택 합니다.  
  
3.  에 **입력 테이블 선택** 창 클릭 **사례 테이블 선택**합니다.  
  
4.  에 **테이블 선택** 대화 상자에서 변경 된 데이터 원본을 T1000 Pacific Region 및 클릭 **확인**합니다.  
  
5.  마이닝 모델과 입력된 데이터 간의 조인 선을 마우스 오른쪽 단추로 클릭 **연결 수정**합니다. 데이터 원본 뷰에 있는 데이터를 다음과 같이 모델에 매핑합니다.  
  
    1.  마이닝 모델의 ReportingDate 열은 입력된 데이터의 ReportingDate 열에 매핑되어 있는지 확인 합니다.  
  
    2.  에 **매핑 수정** 대화 상자의 AvgQty, 모델 열에 대 한 행에서 클릭 **테이블 열** 한 다음 T1000 Pacific.Quantity를 선택 합니다. **확인**을 클릭합니다.  
  
         이 단계에서는 모델에서 평균 수량 예측을 위해 만든 열을 판매 수량에 대한 T1000 계열의 실제 데이터로 매핑합니다.  
  
    3.  모델에서 열 영역의 모든 입력된 열으로 매핑되지 않습니다.  
  
         모델이 모든 계열의 데이터를 집계했으므로 T1000 Pacific과 같은 계열에 해당하는 항목이 없으며 예측 쿼리를 실행하면 오류가 발생합니다.  
  
6.  이제 예측 쿼리를 작성합니다.  
  
     우선 모델로부터 예측과 함께 AllRegions 레이블을 출력하는 결과에 열을 추가합니다. 이 방법을 통해 결과가 일반 모델을 기반으로 한다는 것을 알 수 있습니다.  
  
    1.  표의 첫 번째 빈 행을 아래에서 클릭 **원본**, 한 다음 AllRegions 마이닝 모델을 선택 합니다.  
  
    2.  에 대 한 **필드**, 지역을 선택 합니다.  
  
    3.  에 대 한 **별칭**, 형식 **모델을 사용 하**합니다.  
  
7.  다음으로 예측이 계열용임을 알 수 있도록 다른 레이블을 결과에 추가합니다.  
  
    1.  빈 행을 클릭 하 고 **원본**를 선택 **사용자 지정 식**합니다.  
  
    2.  에 **별칭** 열, 형식 **ModelRegion**합니다.  
  
    3.  에 **조건/인수** 열, 형식 `'T1000 Pacific'`합니다.  
  
8.  이제 교차 예측 함수를 설정합니다.  
  
    1.  빈 행을 클릭 하 고 **소스**를 선택 **예측 함수**합니다.  
  
    2.  에 **필드** 열 선택 **PredictTimeSeries**합니다.  
  
    3.  에 대 한 **별칭**, 형식 **Predicted Values**합니다.  
  
    4.  AvgQty 필드를 끌어에서 합니다 **마이닝 모델** 창에는 **조건/인수** 끌어서 놓기 작업을 사용 하 여 열입니다.  
  
    5.  에 **조건/인수** 열, 필드 이름 뒤에 오는 다음 텍스트를 입력 합니다. `,5, REPLACE_MODEL_CASES`  
  
         전체 텍스트를 **조건/인수** 입력란 다음과 같아야 합니다. `[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
9. 클릭 **결과**합니다.  
  
## <a name="creating-the-cross-prediction-query-in-dmx"></a>DMX에서 교차 예측 쿼리 만들기  
 교차 예측을 사용 하 여 문제가 보았을 수 있습니다: 즉, 북미 지역의 T1000 제품 모델과 같이 다른 데이터 계열에 일반 모델에 적용할 만들어 해야 각 계열에 대 한 다른 쿼리를 각에 매핑할 수 있도록 설정의 모델에 배치합니다.  
  
 그러나 디자이너에서 쿼리를 작성하지 않고 DMX 뷰로 전환하여 이미 작성된 DMX 문을 편집할 수 있습니다. 예를 들어 다음 DMX 문은 작성한 쿼리를 나타냅니다.  
  
```  
SELECT  
      ([All Regions].[Region]) as [Model Used],  
      ('T-1000 Pacific') as [ModelRegion],  
      (PredictTimeSeries([All Regions].[Avg Qty],5, REPLACE_MODEL_CASES)) as [Predicted Quantity]  
     FROM [All Regions]  
PREDICTION JOIN  
    OPENQUERY([Adventure Works DW2003R2], 'SELECT [ReportingDate] FROM  
      (  
       SELECT  ReportingDate, ModelRegion, Quantity, Amount   
       FROM dbo.vTimeSeries   
       WHERE (ModelRegion = N''T1000 Pacific'')  
       ) as [T1000 Pacific]    ')   
    AS t  
ON   
[All Regions].[Reporting Date] = t.[ReportingDate]   
AND   
[All Regions].[Avg Qty] = t.[Quantity]  
```  
  
 이를 다른 모델에 적용하려면 쿼리 문을 편집하여 필터 조건을 바꾸고 각 결과에 연결된 레이블을 업데이트합니다.  
  
 예를 들어 'Pacific'을 'North America'로 바꿔 필터 조건 및 열 레이블을 변경하는 경우 일반 모델의 패턴을 기반으로 북미의 T1000 제품에 대한 예측을 얻게 됩니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [예측 모델에 대 한 예측 비교 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [시계열 모델 쿼리 예제](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
