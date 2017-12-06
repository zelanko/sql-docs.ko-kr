---
title: "그래프 및 SQL과 R (연습)를 사용 하 여 점도 만들기 | Microsoft Docs"
ms.date: 11/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 8cf83243f4c2c9dd5d114799166160d53573c90f
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>그래프 및 플롯 SQL과 R (연습)를 사용 하 여 만들기

이 연습 부분에서는 점도 SQL Server 데이터를 R을 사용 하 여 맵을 생성 하는 기술을 배웁니다. 일부 연습 하는 간단한 히스토그램을 만들고 보다 복잡 한 맵을 플롯을 개발 합니다.

### <a name="create-a-histogram"></a>히스토그램을 만듭니다

1. [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 함수를 사용하여 첫 번째 그림을 생성합니다.  RxHistogram 함수 비슷한 기능을 제공 하는 오픈 소스 R 패키지에 있지만 원격 실행 컨텍스트에서 실행할 수 있습니다.

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. 이미지는 개발 환경용 R 그래픽 장치에 반환됩니다.  예를 들어 RStudio에서 **그리기** 창을 클릭합니다.  [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]에서 별도 그래픽 창이 열립니다.

    ![rxHistogram을 사용하여 요금 그리기](media/rsql-e2e-rxhistogramresult.png "rxHistogram을 사용하여 요금 그리기")

    > [!NOTE]
    > 가 그래프 모양이 달라 짐
    >  
    > 때문 _inDataSource_ 상위 1000 개 행만 사용 합니다. TOP를 사용 하 여 행의 순서는 예상 하지만 데이터 및 결과 그래프 달라질 수 있으므로 ORDER BY 절을 지정 하지 않을 경우에서 결정적입니다.
    > 이 특정 이미지는 약 10,000개의 데이터 행으로 생성되었습니다. 여러 행 수로 실험하여 각기 다른 그래프를 가져오고 환경의 결과를 반환하는 데 걸리는 시간을 확인하는 것이 좋습니다.

### <a name="create-a-map-plot"></a>지도 점도 만들기

일반적으로 데이터베이스 서버는 인터넷 액세스를 차단 합니다. 이 수 불편할 수 지방 지도나 플롯을 생성 하는 다른 이미지를 다운로드 해야 하는 R 패키지를 사용 하는 경우. 그러나 하면 유용할 수 있는 사용자의 응용 프로그램을 개발 하는 경우 해결 방법이 있습니다. 기본적으로, 클라이언트에서 맵 표현을 생성 하 고 지도에 오버레이 다음 SQL Server 테이블에에서 있는 특성으로 저장 되는 지점입니다.

1. R 플롯 개체를 만드는 함수를 정의 합니다. 사용자 지정 함수 *mapPlot* 택시 픽업 위치를 사용 되 고 각 위치의 시작 타기의 수를 표시 하는 산 점도 만듭니다. 이미 설치되고 로드되어 있어야 하는 **ggplot2** 및  **ggmap** 패키지를 사용합니다.

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

    + *mapPlot* 함수는 두 개의 인수: RxSqlServerData를 사용 하 여 이전 버전을 정의 하 고 클라이언트에서 전달 된 맵 표현 기존 데이터 개체입니다.
    + 로 시작 하는 줄에에서는 *ds* 변수인 rxImport 하는 데 이전에 만든된 데이터 원본의 메모리 내 데이터를 로드 *inDataSource*합니다. (해당 데이터 원본만 1000 개 행을 포함; 더 많은 데이터 요소를 사용 하 여 지도 만들려면 원하는 경우 다른 데이터 원본을 대신 사용할 수 있습니다.)
    + 사용할 때마다 **오픈 소스** 로컬 메모리에 데이터 프레임으로 R 함수, 데이터를 로드 해야 합니다. 그러나 호출 하 여는 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 함수는 원격 계산 컨텍스트는 메모리에서 실행할 수 있습니다.

2. 로컬로 계산 컨텍스트를 변경 하 고 맵을 만드는 데 필요한 라이브러리를 로드 합니다.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 변수는 뉴욕 타임스퀘어의 좌표 집합을 저장합니다.

    + `googmap` 으로 시작하는 줄에서는 지정된 좌표가 중심인 지도를 생성합니다.

3. SQL Server 계산 컨텍스트에서로 전환 하 고 결과에서 그림 함수를 래핑하여 렌더링 [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) 다음과 같이 합니다. 일부인 rxExec 함수는 **RevoScaleR** 패키지 및 원격 계산 컨텍스트에서 임의 R 함수 실행을 지원 합니다.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + 지도 데이터의 `googMap` 원격으로 실행 되는 함수에 인수로 전달 *mapPlot*합니다. 맵을 로컬 환경에서 생성 된, 때문에 전달 되어야 함수에 SQL Server의 컨텍스트에서 플롯을 만들기 위해 합니다.

    + 때로 시작 하는 줄 `plot` R 클라이언트에서 볼 수 있도록 실행을 렌더링된 한 데이터 로컬 R 환경으로 다시 serialize 됩니다.

    > [!NOTE]
    > SQL Server는 Azure 가상 컴퓨터를 사용 하는 경우이 시점에서 오류가 발생할 수 있습니다. R 코드에서 네트워크 액세스를 차단 하는 Azure의 기본 방화벽 규칙 때문입니다. 이 오류를 해결 하는 방법에 대 한 세부 정보를 참조 하십시오. [Azure VM에서 R Services 설치](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)합니다.

4. 다음 그림은 출력 그림을 보여 줍니다. 택시 승차 위치가 지도에 빨간색 점으로 추가되었습니다. 이미지는 위치의 수에 사용한 데이터 원본에 따라 다르게 보일 수 있습니다.

    ![사용자 지정 R 함수를 사용하여 택시 승차 그리기](media/rsql-e2e-mapplot.png "사용자 지정 R 함수를 사용하여 택시 승차 그리기")

## <a name="next-lesson"></a>다음 단원

[R과 SQL을 사용 하 여 데이터 기능 만들기](/walkthrough-create-data-features.md)

## <a name="previous-lesson"></a>이전 단원

[R을 사용 하 여 데이터를 요약 합니다.](/walkthrough-view-and-summarize-data-using-r.md)
