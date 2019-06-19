---
title: '1단원: 시계열 마이닝 모델 및 마이닝 구조 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b201f2b8-9ab5-425b-9ff3-fe321a60a7b7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2513bc3837dd224f6561eb0015ced538ea3add8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678445"
---
# <a name="lesson-1-creating-a-time-series-mining-model-and-mining-structure"></a>1단원: 시계열 마이닝 모델 및 마이닝 구조 만들기
  이 단원에서는 기록 데이터를 기반으로 시간 경과에 따라 값을 예측할 수 있는 마이닝 모델을 만듭니다. 모델을 만들면 기본 구조가 자동으로 생성되고 추가 마이닝 모델에 대한 기초로 사용될 수 있습니다.  
  
 이 단원에서는 사용자가 예측 모델과 Microsoft 시계열 알고리즘의 요구 사항을 잘 알고 있다고 가정합니다. 자세한 내용은 [Microsoft Time Series Algorithm](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)을 참조하세요.  
  
## <a name="create-mining-model-statement"></a>CREATE MINING MODEL 문  
 마이닝 모델을 직접 만들고 기본 마이닝 구조를 자동으로 생성, 하기 위해 사용 하는 [CREATE MINING MODEL &#40;DMX&#41; ](/sql/dmx/create-mining-model-dmx) 문. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
-   모델 이름 지정  
  
-   타임스탬프 정의  
  
-   선택적 계열 키 열 정의  
  
-   예측 가능한 특성 정의  
  
 다음은 CREATE MINING MODEL 문의 일반적인 예입니다.  
  
```  
CREATE MINING MODEL [<Mining Structure Name>]  
(  
   <key columns>,  
   <predictable attribute columns>  
)  
USING <algorithm name>([parameter list])  
WITH DRILLTHROUGH  
```  
  
 코드의 첫 번째 줄에서는 마이닝 모델의 이름을 정의합니다.  
  
```  
CREATE MINING MODEL [Mining Model Name]  
```  
  
 Analysis Services에서는 모델 이름에 "_structure"를 추가하여 기본 구조의 이름을 자동으로 생성하므로 구조 이름이 모델 이름과 달리 고유합니다. DMX에서 개체를 이름 지정에 대 한 자세한 내용은 [식별자 &#40;DMX&#41;](/sql/dmx/identifiers-dmx)합니다.  
  
 코드의 다음 줄에서는 시계열 모델의 경우 원본 데이터의 시간 단계를 고유하게 식별하는 마이닝 모델에 대한 키 열을 정의합니다. 시간 단계는 열 이름과 데이터 형식 뒤에 `KEY TIME` 키워드로 식별합니다. 시계열 모델에 별도의 계열 키가 있으면 `KEY` 키워드를 사용하여 해당 키를 식별합니다.  
  
```  
<key columns>  
```  
  
 코드의 다음 줄은 예측할 모델의 열을 정의하는 데 사용됩니다. 단일 마이닝 모델에 예측 가능한 특성이 여러 개 있을 수 있습니다. 예측 가능한 특성이 여러 개 있으면 Microsoft 시계열 알고리즘에서 각 계열에 대해 별도의 분석을 생성합니다.  
  
```  
<predictable attribute columns>  
```  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   비어 있는 새 쿼리 만들기  
  
-   마이닝 모델을 만들기 위해 쿼리 변경  
  
-   쿼리 실행  
  
## <a name="creating-the-query"></a>쿼리 만들기  
 첫 번째 단계는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결하고 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 새 DNX 쿼리를 만드는 것입니다.  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>SQL Server Management Studio에서 새 DMX 쿼리를 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  **서버에 연결** 대화 상자에서 **서버 유형**으로 **Analysis Services**를 선택합니다. **서버 이름**, 형식 `LocalHost`, 또는 인스턴스의 이름을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이 단원에 연결 하려는 합니다. **연결**을 클릭합니다.  
  
3.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
## <a name="altering-the-query"></a>쿼리 변경  
 다음 단계는 예측을 위해 사용되는 마이닝 모델과 해당 기본 마이닝 구조를 함께 만들기 위해 CREATE MINING MODEL 문을 수정하는 것입니다.  
  
#### <a name="to-customize-the-create-mining-model-statement"></a>CREATE MINING MODEL 문을 사용자 지정하려면  
  
1.  쿼리 편집기에서 CREATE MINING MODEL 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
2.  다음 내용을  
  
    ```  
    [mining model name]   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
3.  다음 내용을  
  
    ```  
    <key columns>  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Reporting Date] DATE KEY TIME,  
    [Model Region] TEXT KEY  
    ```  
  
     `TIME KEY` 키워드는 ReportingDate 열에 값을 정렬하는 데 사용되는 시간 단계 값이 포함되어 있는지 나타냅니다. 값이 고유하고 데이터가 정렬되어 있으면 시간 단계는 날짜 및 시간, 정수 또는 정렬된 모든 데이터 형식일 수 있습니다.  
  
     `TEXT` 및 `KEY` 키워드는 ModelRegion 열에 추가 계열 값이 포함되어 있는지 나타냅니다. 하나의 계열 키만 포함할 수 있으며 열의 값은 고유해야 합니다.  
  
4.  다음 내용을  
  
    ```  
    < predictable attribute columns> )  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Quantity] LONG CONTINUOUS PREDICT,  
    [Amount] DOUBLE CONTINUOUS PREDICT  
    )  
    ```  
  
5.  다음 내용을  
  
    ```  
    USING <algorithm name>([parameter list])  
    WITH DRILLTHROUGH  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    USING Microsoft_Time_Series(AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
    ```  
  
     알고리즘 매개 변수 `AUTO_DETECT_PERIODICITY` = 0.8은 사용자가 데이터의 주기를 검색하는 알고리즘을 원하는지 나타냅니다. 이 값을 1에 가깝게 설정하면 많은 패턴을 검색하지만 처리 속도가 느릴 수 있습니다.  
  
     알고리즘 매개 변수 `FORECAST_METHOD`는 사용자가 ARTXP, ARIMA 또는 이 둘의 조합을 사용하여 분석할 데이터를 원하는지 여부를 나타냅니다.  
  
     `WITH DRILLTHROUGH` 키워드는 사용자가 모델이 완료된 후 원본 데이터의 자세한 통계를 볼 수 있는지 지정합니다. Microsoft 시계열 뷰어를 사용하여 모델을 찾아볼 경우 이 절을 추가해야 합니다. 예측에는 이 절이 필요하지 않습니다.  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    CREATE MINING MODEL [Forecasting_MIXED]  
         (  
        [Reporting Date] DATE KEY TIME,  
        [Model Region] TEXT KEY,  
        [Quantity] LONG CONTINUOUS PREDICT,  
        [Amount] DOUBLE CONTINUOUS PREDICT  
        )  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
  
    ```  
  
6.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
7.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Forecasting_MIXED.dmx`입니다.  
  
## <a name="executing-the-query"></a>쿼리 실행  
 마지막 단계는 쿼리를 실행하는 것입니다. 쿼리를 만들어 저장한 다음 서버에 마이닝 모델 및 해당 마이닝 구조를 만들려면 해당 쿼리를 실행해야 합니다. 쿼리 편집기에서 쿼리를 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. [데이터베이스 엔진 쿼리 편집기 &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)합니다.  
  
#### <a name="to-execute-the-query"></a>쿼리를 실행하려면  
  
-   쿼리 편집기의 도구 모음에서 **실행**을 클릭합니다.  
  
     문의 실행이 끝나면 쿼리 상태가 쿼리 편집기 아래쪽의 **메시지** 탭에 표시됩니다. 메시지는 다음과 같아야 합니다.  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     이제 **Forecasting_MIXED_Structure** 라는 새 구조가 관련 마이닝 모델인 **Forecasting_MIXED**와 함께 서버에 있습니다.  
  
 다음 단원에서는 방금 만든 **Forecasting_MIXED** 마이닝 구조에 마이닝 모델을 추가합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [2단원: 시계열 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 콘텐츠 시계열 모델에 대 한 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)   
 [Microsoft 시계열 알고리즘 기술 참조](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
