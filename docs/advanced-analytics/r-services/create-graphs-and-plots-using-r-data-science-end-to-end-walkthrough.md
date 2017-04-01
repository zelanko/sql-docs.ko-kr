---
title: "R을 사용하여 그래프 및 그림 생성(데이터 과학 종단 간 연습) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# R을 사용하여 그래프 및 그림 생성(데이터 과학 종단 간 연습)
이 단원에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터와 함께 R을 사용하여 그림과 지도를 생성하는 방법을 알아봅니다.  서버에서 생성된 그림을 얼마나 쉽게 볼 수 있는지 및 그래픽 개체를 서버에 전달하는 방법을 확인할 수 있습니다.  
  
## <a name="creating-graphics"></a>그래픽 만들기
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서는 모델과 결과뿐 아니라 그래픽 개체도 컴퓨터와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 컨텍스트 간에 직렬화됩니다.

대부분의 프로덕션 데이터베이스 서버는 인터넷 액세스를 완전히 차단하기 때문에 SQL Server 계산 컨텍스트를 사용할 때 지도 표시를 다운로드하지 못할 수도 있습니다.  따라서 두 번째 그림 집합을 만들려면 클라이언트에서 지도 표현을 생성한 다음 *nyctaxi_sample* 테이블에 특성으로 저장된 지점을 지도에 오버레이합니다.   

이렇게 하려면 먼저 Google 지도를 호출하여 지도 표현을 만든 다음 SQL 컨텍스트에 지도 표현을 전달합니다.  
  
이 패턴은 고유한 응용 프로그램을 개발할 때 유용할 수 있습니다.   
  
### <a name="create-a-histogram"></a>히스토그램 만들기  
히스토그램을 만들려면 앞에서 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본을 R Services에서 제공하는 `rxHistogram` 함수와 함께 사용합니다.  
  
1.  *rxHistogram* 함수를 사용하여 첫 번째 그림을 생성합니다.  *rxHistogram* 함수는 오픈 소스 R 패키지에 있는 것과 유사한 기능을 제공하지만 원격 실행 컨텍스트에서 실행할 수 있습니다. 
  
    ```R  
    #Plot fare amount on SQL Server and return the plot  
    start.time <- proc.time()  
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```         
  
2.  이미지는 개발 환경용 R 그래픽 장치에 반환됩니다.  예를 들어 RStudio에서 **그리기** 창을 클릭합니다.  [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]에서 별도 그래픽 창이 열립니다.  
  
    ![using rxHistogram to plot fare amounts](../../advanced-analytics/r-services/media/rsql-e2e-rxhistogramresult.png "using rxHistogram to plot fare amounts")  
  
    > [!NOTE]  TOP을 사용한 행의 순서 매기기는 ORDER BY 절 없이 비결정적으로 수행되므로 전혀 다른 결과가 나타날 수 있습니다. 여러 행 수로 실험하여 각기 다른 그래프를 가져오고 환경의 결과를 반환하는 데 걸리는 시간을 확인하는 것이 좋습니다.  이 특정 이미지는 최대 10,000개의 데이터 행으로 생성되었습니다.
  
### <a name="create-a-map-plot"></a>지도 그림 만들기  
이 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 계산 컨텍스트로 사용하여 그림 개체를 생성한 다음 렌더링을 위해 그림 개체를 로컬 계산 컨텍스트에 반환합니다.  
   
1.  먼저 그림 개체를 만드는 함수를 정의합니다.  

    ```R  
    mapPlot <- function(inDataSource, googMap){  
        library(ggmap)  
        library(mapproj)     
        ds <- rxImport(inDataSource)  
        p <- ggmap(googMap)+  
        geom_point(aes(x = pickup_longitude, y =pickup_latitude ), data=ds, alpha =.5,  
    color="darkred", size = 1.5)  
        return(list(myplot=p))  
    }  
    ```  
    + 사용자 지정 R 함수 *mapPlot*은 택시 승차 위치를 사용하여 각 위치에서 시작된 탑승 수를 그리는 산점도를 만듭니다. 이미 설치되고 로드되어 있어야 하는 **ggplot2** 및  **ggmap** 패키지를 사용합니다.  
    + *mapPlot* 함수는 앞에서 *RxSqlServerData*를 사용하여 정의한 기존 데이터 개체와 클라이언트에서 전달된 지도 표현의 두 인수를 사용합니다.    
    + *ds* 변수를 사용하여 이전에 만든 데이터 원본 *inDataSource*에서 데이터를 로드합니다.  오픈 소스 R 함수를 사용할 때마다 메모리의 데이터 프레임에 데이터를 로드해야 합니다. 이렇게 하려면 **RevoScaleR** 패키지의 *rxImport* 함수를 사용합니다.  그러나 이 함수는 앞에서 정의한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트의 메모리에서 실행됩니다. 즉, 함수는 로컬 워크스테이션의 메모리를 사용하지 않습니다.  
  
2.  다음에는 로컬 R 환경에서 지도를 만드는 데 필요한 라이브러리를 로드합니다.  
  
    ```R  
    library(ggmap)  
    library(mapproj)  
    gc <- geocode("Times Square", source = "google")  
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color';    
    ```  
    + 이 코드는 R 클라이언트에서 실행됩니다. **ggmap** 및 **mapproj**라이브러리가 반복해서 호출됩니다. 이는 이전 함수 정의가 서버 컨텍스트에서 실행되었으며 라이브러리가 로컬에 로드된 적이 없기 때문입니다. 이제 그리기 작업을 워크스테이션으로 다시 가져옵니다.  
  
    -   *gc* 변수는 뉴욕 타임스퀘어의 좌표 집합을 저장합니다.  
  
    -   *googmap*으로 시작하는 줄에서는 지정된 좌표가 중심인 지도를 생성합니다.  
          
  
3.  그리기 함수를 실행하고 결과를 로컬 R 환경에 렌더링합니다. 이렇게 하려면 다음과 같이 그리기 함수를 *rxExec*에 래핑합니다.  *rxExec* 함수는 **RevoScaleR** 패키지에 포함되어 있으며 원격 계산 컨텍스트에서 임의의 R 함수 실행을 지원합니다. 
  
    ```R  
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)  
    plot(myplots[[1]][["myplot"]]);  
  
    ```  
    + 첫 번째 줄에서 지도 데이터가 원격으로 실행된 함수*mapPlot*에 인수(*googMap*)로 전달되는 것을 확인할 수 있습니다. 이는 지도가 로컬 환경에서 생성되었으며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 컨텍스트에서 그림을 만들기 위해 함수에 전달되어야 하기 때문입니다.   
  
        그런 다음 RStudio 또는 다른 R 그래픽 장치의 **그리기** 창에서 볼 수 있도록 렌더링된 데이터가 로컬 R 환경으로 다시 직렬화됩니다.  
  
  
4.  다음은 승차 위치를 지도에 빨간색 점으로 표시하는 출력 그림입니다.  
  
    ![plotting taxi rides using a custom R function](../../advanced-analytics/r-services/media/rsql-e2e-mapplot.png "plotting taxi rides using a custom R function")  
  
## <a name="next-lesson"></a>다음 단원  
[3단원: 데이터 기능 만들기&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
