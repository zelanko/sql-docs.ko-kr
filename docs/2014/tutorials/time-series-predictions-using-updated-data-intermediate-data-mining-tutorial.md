---
title: 업데이트 된 데이터 (중급 데이터 마이닝 자습서)를 사용 하 여 시계열 예측 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74bc6afe0c5c3bddd4b36ebe844ae963da8fbe28
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185493"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>업데이트된 데이터를 사용한 시계열 예측(중급 데이터 마이닝 자습서)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>확장 판매 데이터를 사용하여 예측 만들기  
 이 단원에서는 모델에 새 판매 데이터를 추가하는 예측 쿼리를 만듭니다. 새 데이터로 모델을 확장하여 최신 데이터 요소를 포함하는 최신 예측을 얻을 수 있습니다.  
  
 새 데이터를 사용 하는 시계열 예측 만들기는 쉽습니다: EXTEND_MODEL_CASES 매개 변수를 간단히 추가에 [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) 함수를 새 데이터의 원본을 지정 하 고 지정 개수 가져오려는 예측 합니다.  
  
> [!WARNING]  
>  매개 변수 EXTEND_MODEL_CASES는 선택 사항입니다. 기본적으로 모델은 새 데이터를 입력으로 조인하여 시계열 예측 쿼리를 만드는 시간에 따라 확장됩니다.  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>예측 쿼리를 작성하고 새 데이터를 추가하려면  
  
1.  모델이 아직 열려 있지 않으면 Forecasting 구조를 두 번 클릭 하 고 데이터 마이닝 디자이너에서을 클릭 합니다 **마이닝 모델 예측** 탭 합니다.  
  
2.  에 **마이닝 모델** 창, 이미 선택 되어 Forecasting 모델입니다. 선택 하지 않으면 클릭 **모델 선택**를 선택한 다음 모델을 예측 합니다.  
  
3.  에 **입력 테이블 선택** 창 클릭 **사례 테이블 선택**합니다.  
  
4.  에 **테이블 선택** 대화 상자에서 데이터 원본을 선택 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]합니다.  
  
     데이터 원본 뷰 목록에서 NewSalesData를 선택 하 고 클릭 **확인**합니다.  
  
5.  디자인 영역의 화면을 마우스 오른쪽 단추로 누르고 **연결 수정**합니다.  
  
6.  사용 하 여 합니다 **매핑 수정** 대화 상자에서 다음과 같이 외부 데이터의 열을 모델의 열을 매핑합니다.  
  
    -   NewDate 열 입력된 데이터에 마이닝 모델의 ReportingDate 열을 매핑하십시오.  
  
    -   마이닝 모델에서 Amount 열을 NewAmount 열을 입력된 데이터에 매핑됩니다.  
  
    -   NewQty 열 입력된 데이터에 마이닝 모델의 수량 열을 매핑하십시오.  
  
    -   입력된 데이터의 시계열 열에 마이닝 모델에서 ModelRegion 열을 매핑하십시오.  
  
7.  이제 예측 쿼리를 작성합니다.  
  
     우선, 예측이 적용되는 계열을 출력하기 위해 예측 쿼리에 열을 추가합니다.  
  
    1.  표의 첫 번째 빈 행을 아래에서 클릭 **원본**를 선택한 다음 예측 합니다.  
  
    2.  에 **필드** 선택 Model Region 열 및 **별칭**, 형식 `Model Region`합니다.  
  
8.  다음으로 예측 함수를 추가하고 편집합니다.  
  
    1.  빈 행을 클릭 하 고 **소스**를 선택 **예측 함수**합니다.  
  
    2.  에 대 한 **필드**를 선택 **PredictTimeSeries**합니다.  
  
    3.  에 대 한 **별칭**, 형식 **Predicted Values**합니다.  
  
    4.  수량 필드를 끌어에서 **마이닝 모델** 창에는 **조건/인수** 열입니다.  
  
    5.  에 **조건/인수** 열에서 필드 이름 뒤에 오는 다음 텍스트를 입력: **5, EXTEND_MODEL_CASES**  
  
         전체 텍스트를 **조건/인수** 입력란 다음과 같아야 합니다. `[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. 클릭 **결과** 결과 검토 합니다.  
  
     예측은 7월(원래 데이터의 끝에서부터 첫 번째 시간 조각)에 시작되고 11월(원래 데이터 끝에서부터 다섯 번째 시간 조각)에 끝납니다.  
  
 이러한 유형의 예측 쿼리를 사용하려면 기존 데이터가 언제 끝나며 새 데이터에 시간 조각이 몇 개 있는지 알고 있어야 함을 알 수 있습니다.  
  
 예를 들어 이 모델에서 원래 데이터 계열은 6월에 끝났고 데이터는 7, 8, 9월에 대한 데이터입니다.  
  
 EXTEND_MODEL_CASES를 사용하는 예측은 항상 원래 데이터 계열의 끝에서 시작됩니다. 따라서 결과를 알 수 없는 개월에 대한 예측만 구하려면 예측의 시작점과 끝점을 지정해야 합니다. 양쪽 값 모두 기존 데이터의 끝에서 시작되는 시간 조각의 수로 지정됩니다.  
  
 다음 절차에서는 이를 수행하는 방법을 보여 줍니다.  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>예측의 시작점과 끝점 변경  
  
1.  예측 쿼리 작성기에서 클릭 **쿼리** DMX 뷰로 전환 합니다.  
  
2.  PredictTimeSeries 함수가 포함된 DMX 문을 찾아 다음과 같이 변경합니다.  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  클릭 **결과** 결과 검토 합니다.  
  
     이제 예측은 10월(원래 데이터의 끝에서부터 네 번째 시간 조각)에 시작되고 12월(원래 데이터의 끝에서부터 여섯 번째 시간 조각)에 끝납니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [대체 데이터를 사용 하 여 시계열 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 시계열 알고리즘 기술 참조](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [마이닝 모델 콘텐츠 시계열 모델에 대 한 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
