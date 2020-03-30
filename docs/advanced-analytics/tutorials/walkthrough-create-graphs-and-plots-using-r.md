---
title: 'R 자습서: 그래프 및 플롯 만들기'
description: SQL Server에서 R 언어 함수를 사용하여 그래프 및 플롯을 만드는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 34ec0c2814dda7d2cf4bada10e5e53c05f8e08b9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73724014"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>SQL 및 R을 사용하여 그래프 및 플롯 만들기(연습)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 연습 부분에서는 SQL Server 데이터에 R을 사용하여 플롯 및 지도를 생성하는 기술을 알아봅니다. 간단한 히스토그램을 만들고 더 복잡한 지도 그림을 개발합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 단계는 이 연습의 이전 단계에서 진행 중인 R 세션을 전제로 합니다. 이전 단계에서 만든 연결 문자열과 데이터 원본 개체를 사용합니다. 다음 도구 및 패키지는 스크립트를 실행하는 데 사용됩니다.

+ R 명령을 실행하는 Rgui.exe
+ T-SQL을 실행하는 Management Studio
+ googMap
+ ggmap 패키지
+ mapproj 패키지

## <a name="create-a-histogram"></a>히스토그램 만들기

1. [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 함수를 사용하여 첫 번째 그림을 생성합니다.  rxHistogram 함수는 오픈 소스 R 패키지에 있는 것과 유사한 기능을 제공하지만 원격 실행 컨텍스트에서 실행할 수 있습니다.

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. 이미지는 개발 환경용 R 그래픽 디바이스에 반환됩니다.  예를 들어 RStudio에서 **그리기** 창을 클릭합니다.  [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]에서 별도 그래픽 창이 열립니다.

    ![rxHistogram을 사용하여 운임 그리기](media/rsql-e2e-rxhistogramresult.png "rxHistogram을 사용하여 운임 그리기")

    > [!NOTE]
    > 그래프가 다르게 보이나요?.
    >  
    > _inDataSource_가 상위 1,000개 행만 사용하기 때문입니다. TOP을 사용하는 행의 순서 매기기는 ORDER BY 절이 없으면 비결정적으로 수행되므로 데이터와 결과 그래프가 다를 수 있습니다.
    > 이 특정 이미지는 약 10,000개의 데이터 행으로 생성되었습니다. 여러 행 수로 실험하여 각기 다른 그래프를 가져오고 환경의 결과를 반환하는 데 걸리는 시간을 확인하는 것이 좋습니다.

## <a name="create-a-map-plot"></a>지도 그림 만들기

일반적으로 데이터베이스 서버는 인터넷 액세스를 차단합니다. 따라서 플롯을 생성하기 위해 지도나 다른 이미지를 다운로드해야 하는 R 패키지를 사용하는 경우에는 불편할 수 있습니다. 그렇지만 고유한 애플리케이션을 개발할 때 유용할 수 있는 해결 방법이 있습니다. 기본적으로 클라이언트에서 지도 표현을 생성한 다음, SQL Server 테이블에 특성으로 저장된 지점을 지도에 오버레이합니다.

1. R 그림 개체를 만드는 함수를 정의합니다. 사용자 지정 함수 *mapPlot*은 택시 승차 위치를 사용하고 각 위치에서 시작된 승차 수를 그리는 산점도를 만듭니다. 이미 [설치되고 로드되어](walkthrough-data-science-end-to-end-walkthrough.md#add-packages) 있어야 하는 **ggplot2** 및 **ggmap** 패키지를 사용합니다.

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

    + *mapPlot* 함수는 앞에서 RxSqlServerData를 사용하여 정의한 기존 데이터 개체와 클라이언트에서 전달된 지도 표현의 두 인수를 사용합니다.
    + *ds* 변수로 시작하는 줄에서 rxImport를 사용하여 이전에 만든 데이터 원본 *inDataSource*에서 메모리 데이터를 로드합니다. (이 데이터 원본에는 1,000개의 행만 포함되어 있습니다. 더 많은 데이터 요소가 포함된 지도를 만들려면 다른 데이터 원본을 대체할 수 있습니다.)
    + 오픈 소스 R 함수를 사용할 때마다 로컬 메모리의 데이터 프레임에 데이터를 로드해야 합니다. 그러나 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 함수를 호출하여 원격 컴퓨팅 컨텍스트의 메모리에서 실행할 수 있습니다.

2. 컴퓨팅 컨텍스트를 로컬로 변경하고 지도를 만드는 데 필요한 라이브러리를 로드합니다.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 변수는 뉴욕 타임스퀘어의 좌표 집합을 저장합니다.

    + `googmap` 으로 시작하는 줄에서는 지정된 좌표가 중심인 지도를 생성합니다.

3. SQL Server 컴퓨팅 컨텍스트로 전환하고 여기에 표시된 것처럼 [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec)에 플롯 함수를 래핑하여 결과를 렌더링합니다. rxExec 함수는 **RevoScaleR** 패키지에 포함되어 있으며 원격 컴퓨팅 컨텍스트에서 임의의 R 함수 실행을 지원합니다.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + `googMap`의 지도 데이터가 원격으로 실행되는 함수 *mapPlot*에 인수로 전달됩니다. 지도가 로컬 환경에서 생성되었으므로 SQL Server의 컨텍스트에서 그림을 만들기 위해 함수에 전달되어야 합니다.

    + `plot`로 시작하는 줄이 실행될 때 렌더링된 데이터는 R 클라이언트에서 볼 수 있도록 로컬 R 환경으로 다시 serialize됩니다.

    > [!NOTE]
    > Azure Virtual Machine에서 SQL Server를 사용하는 경우 이 시점에서 오류가 발생할 수 있습니다. Azure의 기본 방화벽 규칙이 R 코드의 네트워크 액세스를 차단하는 경우 오류가 발생합니다. 이 오류를 해결하는 방법에 대한 자세한 내용은 [Azure VM에 Machine Learning(R) 서비스 설치](../install/sql-machine-learning-azure-virtual-machine.md)를 참조하세요.

4. 다음 그림은 출력 그림을 보여 줍니다. 택시 승차 위치가 지도에 빨간색 점으로 추가되었습니다. 사용한 데이터 원본에 있는 위치 수에 따라 이미지가 다르게 보일 수 있습니다.

    ![사용자 지정 R 함수를 사용하여 택시 승차 위치 그리기](media/rsql-e2e-mapplot.png "사용자 지정 R 함수를 사용하여 택시 승차 위치 그리기")

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R 및 SQL을 사용하여 데이터 기능 만들기](walkthrough-create-data-features.md)
