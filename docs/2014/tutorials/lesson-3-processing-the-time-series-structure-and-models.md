---
title: '3 단원: 시계열 구조 및 모델 처리 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 16e27b57-eae1-47a7-a02c-47b6ed487d87
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 493d27c9836eb765c655eba5bbb004e4d48cde40
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63042879"
---
# <a name="lesson-3-processing-the-time-series-structure-and-models"></a>3단원: 시계열 구조 및 모델 처리
  이 단원에서는 [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) 문을 사용 하 여 만든 시계열 마이닝 구조 및 마이닝 모델을 처리 합니다.  
  
 마이닝 구조를 처리하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 원본 데이터를 읽은 다음 마이닝 모델을 지원하는 구조를 작성합니다. 처음 마이닝 모델 및 구조를 만들면 해당 마이닝 모델 및 구조를 항상 처리해야 합니다. INSERT INTO를 사용하여 마이닝 구조를 지정하는 경우 이 문은 마이닝 구조 및 연결된 모든 마이닝 모델을 처리합니다.  
  
 이미 처리된 마이닝 구조에 마이닝 모델을 추가하는 경우에는 `INSERT INTO MINING MODEL` 문을 사용하여 기존 데이터를 기반으로 새 마이닝 모델만 처리합니다.  
  
 마이닝 모델 처리에 대 한 자세한 내용은 [데이터 마이닝&#41;&#40;처리 요구 사항 및 고려 ](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)사항을 참조 하세요.  
  
## <a name="insert-into-statement"></a>INSERT INTO 문  
 시계열 마이닝 구조 및 연결 된 모든 마이닝 모델을 학습 하려면 [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) 문을 사용 합니다. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
-   마이닝 구조 식별  
  
-   마이닝 구조의 열 나열  
  
-   학습 데이터 정의  
  
 다음은 `INSERT INTO` 문의 일반적인 예입니다.  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY (<source data definition>)  
```  
  
 코드의 첫 번째 줄에서는 학습할 마이닝 구조를 식별합니다.  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 코드의 다음 줄에서는 마이닝 구조에서 정의한 열을 지정합니다. 마이닝 구조의 각 열을 나열해야 하며 각 열을 원본 쿼리 데이터 내에 포함된 열에 매핑해야 합니다.  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 코드의 마지막 줄에서는 마이닝 구조의 학습에 사용할 데이터를 정의합니다.  
  
```  
OPENQUERY (<source data definition>)  
```  
  
 이 단원에서는 `OPENQUERY`를 사용하여 원본 데이터를 정의합니다. 원본 데이터에 대 한 쿼리를 정의 하는 다른 방법에 대 한 자세한 내용은 [&#60;원본 데이터 쿼리&#62;](/sql/dmx/source-data-query)를 참조 하세요.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   Forecasting_MIXED_Structure 마이닝 구조 처리  
  
-   관련 마이닝 모델 Forecasting_MIXED, Forecasting_ARIMA 및 Forecasting_ARTXP 처리  
  
## <a name="processing-the-time-series-mining-structure"></a>시계열 마이닝 구조 처리  
  
#### <a name="to-process-the-mining-structure-and-related-mining-models-by-using-insert-into"></a>INSERT INTO를 사용하여 마이닝 구조 및 관련 마이닝 모델을 처리하려면  
  
1.  
  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  INSERT INTO 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    [<mining structure>]  
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    Forecasting_MIXED_Structure  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining structure columns>  
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    [ReportingDate],  
    [ModelRegion]   
    ```  
  
5.  다음 내용을  
  
    ```  
    OPENQUERY(<source data definition>)  
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    OPENQUERY([Adventure Works DW 2008R2],'SELECT [ReportingDate], [ModelRegion], [Quantity], [Amount]  
    FROM vTimeSeries ORDER BY [ReportingDate]')  
    ```  
  
     원본 쿼리는 IntermediateTutorial 샘플 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 프로젝트에 정의 된 데이터 원본을 참조 합니다. 원본 쿼리는 이 데이터 원본을 사용하여 vTimeSeries 뷰에 액세스합니다. 이 뷰에는 마이닝 모델의 학습에 사용할 원본 데이터가 포함되어 있습니다. 이 프로젝트 또는이 뷰에 익숙하지 않은 경우[2 단원: &#40;중급 데이터 마이닝 자습서를&#41;예측 시나리오 빌드 ](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)를 참조 하세요.  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    INSERT INTO MINING STRUCTURE [Forecasting_MIXED_Structure]  
    (  
       [ReportingDate],[ModelRegion],[Quantity],[Amount])  
    )  
    OPENQUERY(  
    [Adventure Works DW 2008R2],  
    'SELECT [ReportingDate],[ModelRegion],[Quantity],[Amount] FROM vTimeSeries ORDER BY [ReportingDate]'  
    )   
    ```  
  
6.  
  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
7.  다른 이름 **으로 저장** 대화 상자에서 해당 폴더로 이동한 다음 파일 `ProcessForecastingAll.dmx`이름을로 합니다.  
  
8.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
 쿼리 실행이 끝나면 처리된 마이닝 모델을 사용하여 예측을 만들 수 있습니다. 다음 단원에서는 만들어진 마이닝 모델을 기반으로 여러 예측을 만듭니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [4단원: DMX를 사용하여 시계열 예측 만들기](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝&#41;&#40;처리 요구 사항 및 고려 사항](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)   
 [&#60;원본 데이터 쿼리&#62;](/sql/dmx/source-data-query)   
 [OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery)  
  
  
