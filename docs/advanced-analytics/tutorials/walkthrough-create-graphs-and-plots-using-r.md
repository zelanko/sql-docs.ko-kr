---
title: "SQL 및 R을 사용한 그래프와 플롯(plot) 만들기(연습) | Microsoft Docs"
ms.date: 11/10/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 2a1572cf1bc6f8e3f6aff99255e5805bf977978d
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>SQL 및 R을 사용한 그래프와 플롯(plot) 만들기(연습)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 연습 부분에서는 점도 SQL Server 데이터를 R을 사용 하 여 맵을 생성 하는 기술을 배웁니다. 일부 연습 하는 간단한 히스토그램을 만들고 보다 복잡 한 맵을 플롯을 개발 합니다.

이 연습에서는 SQL Server 데이터와 R을 사용하여 플롯과 맵을 생성하는 기술을 배웁니다. 연습을 위해 간단한 히스토그램을 만들어 본 뒤 더 복잡한 지도 플롯을 개발합니다.


### <a name="create-a-histogram"></a>히스토그램 만들기

1. [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 함수를 사용하여 첫 번째 플롯을 생성합니다. RxHistogram 함수는 오픈 소스 R 패키지에 있는 것과 유사한 기능을 제공하지만 원격 실행 컨텍스트에서 실행할 수 있습니다.

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```


2. 이미지는 개발 환경을 위해 R 그래픽 장치로 반환됩니다. 예를 들어 RStudio에서 **Plot** 창을 클릭합니다.  [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]에서는 별도 그래픽 창이 열립니다.


    ![rxHistogram을 사용하여 요금 그리기](media/rsql-e2e-rxhistogramresult.png "rxHistogram을 사용하여 요금 그리기")

    > [!NOTE]

    > 그래프가 다르게 보입니까?
    >  
    > _inDataSource_ 가 상위 1000개 행만 사용하기 때문입니다. ORDER BY 절 없는 TOP의 행 순서는 비결정적이므로(역주. 정렬 순서가 보장되지 않는) 예상 데이터와 결과 그래프가 다를 수 있습니다. 이 이미지는 약 10,000개의 데이터 행으로 생성되었습니다. 서로 다른 행 수를 사용해서 다른 그래프를 생성하고 그 결과를 반환하는데 걸리는 시간을 확인해 보기를 권장합니다.

### <a name="create-a-map-plot"></a>지도 플롯 만들기

일반적으로 데이터베이스 서버는 인터넷 접근을 차단합니다. 이는 지도나 혹은  플롯을 생성하는 다른 이미지를 다운로드해야 하는 R 패키지를 사용할 때 불편할 수 있습니다. 그러나 자신의 응용 프로그램을 개발할 때 유용할 수도 있는 해결 방법이 있습니다. 기본적으로 클라이언트에서 지도 표현을 생성한 다음 SQL Server 테이블에 속성으로 저장된 점을 지도에 오버레이합니다.


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


    + *mapPlot* 함수는 두 개의 인수를 가집니다. RxSqlServerData를 사용하여 이전에 정의한 기존 데이터 개체, 그리고 클라이언트로 보낸 지도 표현입니다.
    + *ds* 변수로 시작하는 줄에서 rxImport는 이전에 만든 데이터 원본 *inDataSource*의 데이터를 메모리로 로드하는데 사용됩니다. (데이터 원본은 1000개 행만 포함합니다. 더 많은 데이터 포인트를 가진 지도를 만들고 싶은 경우 다른 데이터 원본을 대신 사용할 수 있습니다.)
    + **오픈 소스** R 함수를 사용할 때마다 데이터는 로컬 메모리내 데이터 프레임으로 저장되어야 합니다. 그러나 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 함수 호출을 통해서 원격 계산 컨텍스트의 메모리에서 실행할 수 있습니다.

2. 계산 컨텍스트를 로컬로 변경하고 지도를 만드는 데 필요한 라이브러리를 로드합니다.


    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 변수는 뉴욕 타임스퀘어의 좌표 집합을 저장합니다.

    + `googmap` 으로 시작하는 줄은 지정된 좌표가 중심인 지도를 생성합니다.


3. SQL Server 계산 컨텍스트로 전환하고 [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec)를 plot 함수로 래핑하여 결과를 렌더링합니다. rxExec 함수는 **RevoScaleR** 패키지의 일부이며 원격 계산 컨텍스트에서 임의의 R 함수 실행을 지원합니다.


    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````


    + `googMap`의 지도 데이터는 원격 실행 함수 *mapPlot*에 인수로 전달됩니다. 지도가 로컬 환경에서 생성되었기 때문에 SQL Server의 컨텍스트에서 플롯을 만들기 위해 함수로 전달되어야 합니다.


    + `plot`으로 시작하는 행이 실행되면 렌더링 데이터가 다시 로컬 R 환경으로 직렬화되어 R 클라이언트에서 볼 수 있게 됩니다.

    > [!NOTE]
    > Azure 가상 머신에서 SQL Server를 사용한다면 이 지점에서 오류가 발생할 수 있습니다. Azure의 기본 방화벽 규칙이 R 코드에서의 네트워크 접근을 차단하기 때문입니다. 이 오류의 해결 방법은 [Azure VM에서 R Services 설치](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)를 참조하세요.


4. 다음 그림은 출력 플롯을 보여줍니다. 택시 승차 위치가 지도에 빨간색 점으로 추가되었습니다. 사용한 데이터 원본의 위치 수에 따라 이미지가 다르게 보일 수 있습니다.


    ![사용자 지정 R 함수를 사용하여 택시 승차 그리기](media/rsql-e2e-mapplot.png "사용자 지정 R 함수를 사용하여 택시 승차 그리기")

## <a name="next-lesson"></a>다음 단원

[R과 SQL을 사용하여 데이터 특성 만들기](/walkthrough-create-data-features.md)

## <a name="previous-lesson"></a>이전 단원

[R을 사용한 데이터 요약](/walkthrough-view-and-summarize-data-using-r.md)
