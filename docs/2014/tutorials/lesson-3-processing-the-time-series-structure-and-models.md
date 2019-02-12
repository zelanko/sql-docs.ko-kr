---
title: '3단원: 처리 된 시계열 구조 및 모델 | Microsoft Docs'
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026274"
---
# <a name="lesson-3-processing-the-time-series-structure-and-models"></a>3단원: 시계열 구조 및 모델 처리
  이 단원에서는 사용할지는 [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) 시계열 마이닝 구조 및 마이닝 사용자가 만든 모델을 처리 하는 문입니다.  
  
 마이닝 구조를 처리하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 원본 데이터를 읽은 다음 마이닝 모델을 지원하는 구조를 작성합니다. 처음 마이닝 모델 및 구조를 만들면 해당 마이닝 모델 및 구조를 항상 처리해야 합니다. INSERT INTO를 사용하여 마이닝 구조를 지정하는 경우 이 문은 마이닝 구조 및 연결된 모든 마이닝 모델을 처리합니다.  
  
 이미 처리된 마이닝 구조에 마이닝 모델을 추가하는 경우에는 `INSERT INTO MINING MODEL` 문을 사용하여 기존 데이터를 기반으로 새 마이닝 모델만 처리합니다.  
  
 마이닝 모델을 처리 하는 방법에 대 한 자세한 내용은 참조 하세요. [처리 요구 사항 및 고려 사항 &#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)합니다.  
  
## <a name="insert-into-statement"></a>INSERT INTO 문  
 시계열 마이닝 구조 및 모든 관련된 마이닝 모델을 학습 하기 위해 사용 합니다 [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) 문입니다. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
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
  
 이 단원에서는 `OPENQUERY`를 사용하여 원본 데이터를 정의합니다. 원본 데이터에서 쿼리를 정의 하는 다른 방법에 대 한 자세한 내용은 참조 [ &#60;원본 데이터 쿼리&#62;](/sql/dmx/source-data-query)합니다.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   Forecasting_MIXED_Structure 마이닝 구조 처리  
  
-   관련 마이닝 모델 Forecasting_MIXED, Forecasting_ARIMA 및 Forecasting_ARTXP 처리  
  
## <a name="processing-the-time-series-mining-structure"></a>시계열 마이닝 구조 처리  
  
#### <a name="to-process-the-mining-structure-and-related-mining-models-by-using-insert-into"></a>INSERT INTO를 사용하여 마이닝 구조 및 관련 마이닝 모델을 처리하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  INSERT INTO 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    [<mining structure>]  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    Forecasting_MIXED_Structure  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining structure columns>  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [ReportingDate],  
    [ModelRegion]   
    ```  
  
5.  다음 내용을  
  
    ```  
    OPENQUERY(<source data definition>)  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    OPENQUERY([Adventure Works DW 2008R2],'SELECT [ReportingDate], [ModelRegion], [Quantity], [Amount]  
    FROM vTimeSeries ORDER BY [ReportingDate]')  
    ```  
  
     원본 쿼리 참조는 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 는 IntermediateTutorial 예제 프로젝트에 정의 된 데이터 원본입니다. 원본 쿼리는 이 데이터 원본을 사용하여 vTimeSeries 뷰에 액세스합니다. 이 뷰에는 마이닝 모델의 학습에 사용할 원본 데이터가 포함되어 있습니다. 이 프로젝트 또는이 뷰를 사용 하 여 잘 모르는 경우[단원 2: 예측 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)합니다.  
  
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
  
6.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
7.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `ProcessForecastingAll.dmx`입니다.  
  
8.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
 쿼리 실행이 끝나면 처리된 마이닝 모델을 사용하여 예측을 만들 수 있습니다. 다음 단원에서는 만들어진 마이닝 모델을 기반으로 여러 예측을 만듭니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [4단원: DMX를 사용 하 여 시계열 예측 만들기](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
  
## <a name="see-also"></a>관련 항목  
 [처리 요구 사항 및 고려 사항 &#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)   
 [&#60;원본 데이터 쿼리&#62;](/sql/dmx/source-data-query)   
 [OPENQUERY &AMP;#40;DMX&AMP;#41;](/sql/dmx/source-data-query-openquery)  
  
  
