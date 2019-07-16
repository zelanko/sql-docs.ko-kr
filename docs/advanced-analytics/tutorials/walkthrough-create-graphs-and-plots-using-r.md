---
title: 그래프 및 SQL 및 R 함수-SQL Server Machine Learning을 사용 하 여 그림 만들기
description: 그래프 및 SQL Server에서 R 언어 함수를 사용 하 여 그림을 만드는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 542e36e01565ab454cce8beae9a4fa65279d8fa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961783"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>SQL 및 R을 사용한 그래프와 플롯(plot) 만들기(연습)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 연습에서는 SQL Server 데이터와 R을 사용하여 플롯과 맵을 생성하는 기술을 배웁니다. 간단한 히스토그램을 만들고 더 복잡 한 지도 그림을 개발 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 단계에서는이 연습의 이전 단계에 따라 진행 중인 R 세션을 가정 합니다. 이러한 단계에서 만든 연결 문자열 및 데이터 원본 개체를 사용 합니다. 스크립트를 실행 하려면 다음 도구 및 패키지 사용 됩니다.

+ Rgui.exe R 명령을 실행 하려면
+ T-SQL을 실행 하기 위해 management Studio
+ googMap
+ ggmap 패키지
+ mapproj 패키지

## <a name="create-a-histogram"></a>히스토그램 만들기

1. [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 함수를 사용하여 첫 번째 플롯을 생성합니다.  RxHistogram 함수는 오픈 소스 R 패키지와 비슷한 기능을 제공 하지만 원격 실행 컨텍스트에서 실행할 수 있습니다.

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. 이미지는 개발 환경을 위해 R 그래픽 장치로 반환됩니다.  예를 들어 RStudio에서 **Plot** 창을 클릭합니다.  [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]에서는 별도 그래픽 창이 열립니다.

    ![rxHistogram을 사용하여 요금 그리기](media/rsql-e2e-rxhistogramresult.png "rxHistogram을 사용하여 요금 그리기")

    > [!NOTE]
    > 그래프가 다르게 보이나요?
    >  
    > _inDataSource_ 가 상위 1000개 행만 사용하기 때문입니다. ORDER BY 절 없는 TOP의 행 순서는 비결정적이므로(역주: 정렬 순서가 보장되지 않는) 예상 데이터와 결과 그래프가 다를 수 있습니다.
    > 이 이미지는 약 10,000개의 데이터 행으로 생성되었습니다. 서로 다른 행 수를 사용해서 다른 그래프를 생성하고 그 결과를 반환하는데 걸리는 시간을 확인해 보기를 권장합니다.

## <a name="create-a-map-plot"></a>지도 플롯 만들기

일반적으로 데이터베이스 서버는 인터넷 접근을 차단합니다. 이는 지도나 플롯을 생성하는 다른 이미지를 다운로드해야 하는 R 패키지를 사용할 때 불편할 수 있습니다. 그러나 자신의 응용 프로그램을 개발할 때 유용할 수도 있는 해결 방법이 있습니다. 기본적으로 클라이언트에서 지도 표현을 생성한 다음 SQL Server 테이블에 속성으로 저장된 점을 지도에 오버레이합니다.

1. R 플롯 개체를 만드는 함수를 정의합니다. 사용자 지정 함수 *mapPlot*은 택시 승차 위치를 사용하는 산점도(scatter plot)를 생성하고 각 위치에서 시작한 탑승 수를 표시합니다. 사용 하 여는 **ggplot2** 하 고 **ggmap** 이미 있어야 하는 패키지 [설치 및 로드](walkthrough-data-science-end-to-end-walkthrough.md#add-packages)합니다.

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
    + *ds* 변수로 시작하는 줄에서 rxImport는 이전에 만든 데이터 원본 *inDataSource* 의 데이터를 메모리로 로드하는데 사용됩니다. (데이터 원본은 1000개 행만 포함합니다. 더 많은 데이터 포인트를 가진 지도를 만들고 싶은 경우 다른 데이터 원본을 대신 사용할 수 있습니다.)
    + 오픈 소스 R 함수를 사용할 때마다 로컬 메모리에 데이터 프레임으로 데이터를 로드 해야 합니다. 그러나 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 함수 호출을 통해서 원격 계산 컨텍스트의 메모리에서 실행할 수 있습니다.

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

3. SQL Server 계산 컨텍스트로 전환하고 [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) 를 plot 함수로 래핑하여 결과를 렌더링합니다. rxExec 함수는 **RevoScaleR** 패키지의 일부이며 원격 계산 컨텍스트에서 임의의 R 함수 실행을 지원합니다.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + `googMap` 의 지도 데이터는 원격 실행 함수 *mapPlot* 에 인수로 전달됩니다. 지도가 로컬 환경에서 생성되었기 때문에 SQL Server의 컨텍스트에서 플롯을 만들기 위해 함수로 전달되어야 합니다.

    + `plot` 으로 시작하는 행이 실행되면 렌더링 데이터가 다시 로컬 R 환경으로 직렬화되어 R 클라이언트에서 볼 수 있게 됩니다.

    > [!NOTE]
    > SQL Server를 Azure 가상 머신에서 사용 하는 경우 오류가 발생할 수 있습니다는 시점에서. 기본 방화벽 규칙이 Azure에서 R 코드에서 네트워크 액세스를 차단 하는 경우 오류가 발생 했습니다. 이 오류를 해결 하는 방법에 대 한 세부 정보를 참조 하세요 [Machine Learning 설치 (R) 서비스는 Azure VM에서](../install/sql-machine-learning-azure-virtual-machine.md)합니다.

4. 다음 그림은 출력 플롯을 보여줍니다. 택시 승차 위치가 지도에 빨간색 점으로 추가되었습니다. 사용한 데이터 원본의 위치 수에 따라 이미지가 다르게 보일 수 있습니다.

    ![사용자 지정 R 함수를 사용하여 택시 승차 그리기](media/rsql-e2e-mapplot.png "사용자 지정 R 함수를 사용하여 택시 승차 그리기")

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R과 SQL을 사용하여 데이터 특성 만들기](walkthrough-create-data-features.md)
