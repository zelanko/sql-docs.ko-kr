---
title: '2 단원: 시계열 마이닝 구조에 마이닝 모델을 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 75c2a74b-21ce-44fb-a26b-68be4c685c12
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cee3d839ae7a7bcce62c8a3a1d2f7cb62b1155e2
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312491"
---
# <a name="lesson-2-adding-mining-models-to-the-time-series-mining-structure"></a>2단원: 시계열 마이닝 구조에 마이닝 모델 추가
  이 단원에서는 방금 만든 마이닝 구조에 새 마이닝 모델 추가 합니다 [1 단원: 시계열 마이닝 모델 및 마이닝 구조 만들기](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)합니다.  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE 문  
 새 마이닝 모델을 기존 마이닝 구조를 추가 하기 위해 사용 하 여 [ALTER MINING STRUCTURE &#40;DMX&#41;] ((~/dmx/alter-mining-structure-dmx.md) 문입니다. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
-   마이닝 구조 식별  
  
-   마이닝 모델 이름 지정  
  
-   키 열 정의  
  
-   예측 가능한 열 정의  
  
-   알고리즘 및 매개 변수 변경 내용 지정  
  
 다음은 ALTER MINING STRUCTURE 문의 일반적인 예입니다.  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
   ([<key columns>],  
    <mining model columns>  
   )  
USING <algorithm name>([<algorithm parameters>])  
[WITH DRILLTHROUGH]  
```  
  
 코드의 첫 번째 줄에서는 마이닝 모델을 추가할 기존 마이닝 구조를 식별합니다.  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 코드의 다음 줄에서는 마이닝 구조에 추가할 마이닝 모델의 이름을 지정합니다.  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 DMX에서 개체 이름을 지정 하는 방법에 대 한 정보를 참조 하십시오. [식별자 &#40;DMX&#41;](/sql/dmx/identifiers-dmx)합니다.  
  
 코드의 다음 줄에서는 마이닝 모델에서 사용할 마이닝 구조의 열을 정의합니다.  
  
```  
[<key columns>],  
<mining model columns>  
```  
  
 마이닝 구조에 이미 있는 열만 사용할 수 있으며 목록의 첫 번째 열은 마이닝 구조의 키 열이어야 합니다.  
  
 코드의 다음 줄에서는 마이닝 모델을 생성하는 마이닝 알고리즘 및 이 알고리즘에 설정할 수 있는 알고리즘 매개 변수를 정의하고 마이닝 모델에서 드릴다운하여 학습 사례의 세부 데이터를 볼 수 있는지 여부를 지정합니다.  
  
```  
USING <algorithm name>([<algorithm parameters>])  
WITH DRILLTHROUGH  
```  
  
 조정할 수 있는 알고리즘 매개 변수에 대 한 자세한 내용은 참조 [Microsoft Time Series Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)합니다.  
  
 다음 구문을 사용하여 마이닝 모델의 열이 예측에 사용되도록 지정할 수 있습니다.  
  
```  
<mining model column> PREDICT  
```  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   구조에 새 시계열 마이닝 모델을 추가합니다.  
  
-   다른 분석 및 예측 방법을 사용하도록 알고리즘 매개 변수를 변경합니다.  
  
## <a name="adding-an-arima-time-series-model-to-the-structure"></a>구조에 ARIMA 시계열 모델 추가  
 첫 번째 단계는 기존 구조에 새 예측 마이닝 모델을 추가하는 것입니다. 기본적으로 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘은 ARIMA와 ARTXP라는 두 알고리즘을 사용하고 결과를 혼합하여 시계열 마이닝 모델을 만듭니다. 그러나 사용할 단일 알고리즘을 지정하거나 정확한 알고리즘의 혼합을 지정할 수 있습니다. 이 단계에서는 ARIMA 알고리즘만 사용하는 새 모델을 추가합니다. 이 알고리즘은 장기 예측에 대해 최적화되어 있습니다.  
  
#### <a name="to-add-an-arima-time-series-mining-model"></a>ARIMA 시계열 마이닝 모델을 추가하려면  
  
1.  **개체 탐색기**의 인스턴스를 마우스 오른쪽 단추로 클릭 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 가리킨 **새 쿼리**, 클릭 하 고 **DMX** 를 쿼리 편집기와 비어 있는 새 쿼리를 엽니다.  
  
2.  ALTER MINING STRUCTURE 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <mining structure name>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Forecasting_MIXED_Structure]  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining model name>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    Forecasting_ARIMA  
    ```  
  
5.  다음 내용을  
  
    ```  
    <key columns>,  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [ReportingDate],  
    [ModelRegion]  
    ```  
  
     CREATE MINING MODEL 문에 제공한 날짜 유형 또는 내용 유형 정보는 이미 마이닝 구조에 저장되어 있으므로 이러한 정보를 반복하지 않아도 됩니다.  
  
6.  다음 내용을  
  
    ```  
    <mining model columns>  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    ([Quantity] PREDICT,  
    [Amount] PREDICT  
    )  
    ```  
  
7.  다음 내용을  
  
    ```  
    USING <algorithm name>([<algorithm parameters>])   
    [WITH DRILLTHROUGH]  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
     이제 결과 문이 다음과 같아야 합니다.  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARIMA]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
8.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
9. 에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Forecasting_ARIMA.dmx`합니다.  
  
10. 도구 모음에서 **실행** 단추를 클릭합니다.  
  
## <a name="adding-an-artxp-time-series-model-to-the-structure"></a>구조에 ARTXP 시계열 모델 추가  
 ARTXP 알고리즘은 SQL Server 2005의 기본 시계열 알고리즘으로, 단기 예측에 대해 최적화되어 있습니다. 모든 세 시계열 알고리즘을 사용하여 예측을 비교하기 위해 ARTXP 알고리즘을 기반으로 하는 모델을 하나 더 추가합니다.  
  
#### <a name="to-add-an-artxp-time-series-mining-model"></a>ARTXP 시계열 마이닝 모델을 추가하려면  
  
1.  다음 코드를 빈 쿼리 창에 복사합니다.  
  
     새 마이닝 모델의 이름과 FORECAST_METHOD 매개 변수의 값을 제외한 나머지는 변경할 필요가 없습니다.  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARTXP]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARTXP')  
    WITH DRILLTHROUGH  
    ```  
  
2.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
3.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Forecasting_ARTXP.dmx`합니다.  
  
4.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
 다음 단원에서는 모든 모델과 마이닝 구조를 처리합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [3단원: 시계열 구조 및 모델 처리](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 시계열 알고리즘](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft 시계열 알고리즘 기술 참조](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
