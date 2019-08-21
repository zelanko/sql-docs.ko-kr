---
title: Spark 애플리케이션 디버그/진단
titleSuffix: SQL Server big data clusters
description: Spark 기록 서버를 사용 하 여에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]실행 중인 spark 응용 프로그램을 디버그 하 고 진단할 수 있습니다.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9df4f83d319c7d37dd438bcc6a787b4939757e47
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653670"
---
# <a name="debug-and-diagnose-spark-applications-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-spark-history-server"></a>Spark 기록 서버 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 에서 spark 응용 프로그램 디버그 및 진단

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 확장된 Spark 기록 서버를 사용하여 SQL Server 2019(미리 보기) 빅 데이터 클러스터의 Spark 애플리케이션을 디버그하고 진단하는 방법을 설명합니다. 이러한 디버그 및 진단 기능은 Spark 기록 서버에 기본 제공되며 Microsoft에서 제공합니다. 확장에는 데이터 탭, 그래프 탭, 진단 탭이 포함되어 있습니다. 데이터 탭에서는 사용자가 Spark 작업의 입력 및 출력 데이터를 확인할 수 있습니다. 그래프 탭에서는 사용자가 데이터 흐름을 확인하고 작업 그래프를 재생할 수 있습니다. 진단 탭에서는 사용자가 데이터 기울이기, 시간 기울이기 및 실행기 사용량 분석을 참조할 수 있습니다.

## <a name="get-access-to-spark-history-server"></a>Spark 기록 서버 액세스

오픈 소스의 Spark 기록 서버 사용자 환경이 작업 그래프의 작업별 데이터 및 대화형 시각화와 빅 데이터 클러스터의 데이터 흐름을 포함하는 정보를 사용하여 향상되었습니다. 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>URL을 통해 Spark 기록 서버 웹 UI 열기
다음 URL로 이동하여 Spark 기록 서버를 엽니다. `<Ipaddress>` 및 `<Port>`를 빅 데이터 클러스터 관련 정보로 바꿉니다. 자세한 내용은 다음을 참조하세요. [SQL Server 빅 데이터 클러스터 배포](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

Spark 기록 서버 웹 UI는 다음과 같습니다.

![Spark 기록 서버](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>Spark 기록 서버의 데이터 탭
작업 ID를 선택하고 도구 메뉴에서 **데이터**를 클릭하여 데이터 뷰를 표시합니다.

+ 각 탭을 선택하여 **입력**, **출력** 및 **테이블 작업**을 확인합니다.

    ![Spark 기록 서버 데이터 탭](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ **복사** 단추를 클릭하여 모든 행을 복사합니다.

    ![모든 행 복사](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ **csv** 단추를 클릭하여 모든 데이터를 CSV 파일로 저장합니다.

    ![CSV 파일로 데이터 저장](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ **검색** 필드에 키워드를 입력하여 검색하면 검색 결과가 즉시 표시됩니다.

    ![키워드를 사용하여 검색](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ 열 머리글을 클릭하여 테이블을 정렬하거나, 더하기 기호를 클릭하여 더 많은 정보를 표시하도록 행을 확장하거나, 빼기 기호를 클릭하여 행을 축소합니다.

    ![데이터 테이블 기능](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ 오른쪽에 있는 **부분 다운로드** 단추를 클릭하여 단일 파일을 다운로드하면 선택한 파일이 로컬 위치로 다운로드됩니다. 파일이 존재하지 않으면 새 탭이 열리고 오류 메시지가 표시됩니다.

    ![데이터 행 다운로드](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ 다운로드 메뉴에서 펼쳐지는 **전체 경로 복사** 또는 **상대 경로 복사**를 선택하여 전체 경로 또는 상대 경로를 복사합니다. Azure Data Lake Storage 파일의 경우 **Azure Storage Explorer에서 열기**를 선택하면 Azure Storage Explorer가 시작됩니다. 로그인 시 정확한 폴더를 찾습니다.

    ![전체 경로 또는 상대 경로 복사](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ 행 수가 너무 많아서 한 페이지에 표시할 수 없는 경우 테이블 아래에 있는 숫자를 클릭하여 페이지를 탐색합니다. 

    ![데이터 페이지](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ 데이터 옆에 있는 물음표를 마우스로 가리켜 도구 설명을 표시하거나, 물음표를 클릭하여 추가 정보를 가져옵니다.

    ![데이터 추가 정보](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ **피드백 보내기**를 클릭하여 문제와 함께 피드백을 보냅니다.

    ![그래프 피드백](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>Spark 기록 서버의 그래프 탭

작업 ID를 선택하고 도구 메뉴에서 **그래프**를 클릭하여 작업 그래프 뷰를 표시합니다.

+ 생성된 작업 그래프에서 작업 개요를 확인합니다. 

+ 기본적으로 모든 작업이 표시되며, **작업 ID**를 기준으로 필터링할 수 있습니다.

    ![그래프 작업 ID](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ **진행률**을 기본값으로 유지합니다. 사용자는 **표시**드롭다운 목록에서 **읽기** 또는 **쓰기** 를 선택 하 여 데이터 흐름을 확인할 수 있습니다.

    ![그래프 표시](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    그래프 노드는 열 지도를 보여 주는 색으로 표시됩니다.

    ![그래프 열 지도](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ **재생** 단추를 클릭하여 작업을 재생하고 언제든지 중지 단추를 클릭하여 중지합니다. 재생 시 작업이 각 상태를 나타내는 색으로 표시됩니다.

    + 성공한 경우 녹색: 작업이 완료되었습니다.
    + 다시 시도한 경우 주황색: 실패했지만 작업의 최종 결과에 영향을 주지 않는 작업 인스턴스입니다. 해당 작업에는 중복 또는 다시 시도 인스턴스가 있었으며, 나중에 성공할 수 있습니다.
    + 실행 중인 경우 파란색: 작업이 실행 중입니다.
    + 대기 중이거나 건너뛴 경우 흰색: 작업이 실행 대기 중이거나 단계를 건너뛰었습니다.
    + 실패한 경우 빨간색: 작업이 실패했습니다.

    ![그래프 색 샘플, 실행 중](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    건너뛴 단계는 흰색으로 표시됩니다.
    ![그래프 색 샘플, 건너뛰기](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![그래프 색 샘플, 실패](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > 각 작업을 재생할 수 있습니다. 완료되지 않은 작업은 재생할 수 없습니다.


+ 마우스를 스크롤하여 작업 그래프를 확대/축소하거나 **크기에 맞게**를 클릭하여 화면 크기에 맞춥니다.
 
    ![그래프 크기에 맞게](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ 실패한 작업이 있을 경우 그래프 노드를 마우스로 가리켜 도구 설명을 확인하고, 단계를 클릭하여 단계 페이지를 엽니다.

    ![그래프 도구 설명](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ 작업 그래프 탭에서 아래 조건을 충족하는 작업이 있을 경우 단계에 도구 설명 및 작은 아이콘이 표시됩니다.
    + 데이터 기울이기: 데이터 읽기 크기 > 이 단계에 속한 모든 작업의 평균 데이터 읽기 크기 * 2 및 데이터 읽기 크기 > 10MB
    + 시간 기울이기: 실행 시간 > 이 단계에 속한 모든 작업의 평균 실행 시간 * 2 및 실행 시간 > 2분

    ![그래프 기울이기 아이콘](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ 작업 그래프 노드에는 각 단계에 대한 다음 정보가 표시됩니다.
    + ID를 삭제합니다.
    + 이름 또는 설명
    + 총 작업 수
    + 데이터 읽기: 입력 크기와 무작위 읽기 크기의 합계
    + 데이터 쓰기: 출력 크기와 무작위 쓰기 크기의 합계
    + 실행 시간: 첫 번째 시도 시작 시간과 마지막 시도 완료 시간 사이의 시간
    + 행 개수: 입력 레코드, 출력 레코드, 무작위 읽기 레코드 및 무작위 쓰기 레코드의 합계
    + 진행률

    > [!NOTE]
    > 기본적으로 작업 그래프 노드에는 단계 실행 시간을 제외하고 각 단계의 마지막 시도 정보가 표시되지만, 재생 중에는 그래프 노드에 각 시도의 정보가 표시됩니다.

    > [!NOTE]
    > 읽기 및 쓰기의 데이터 크기에는 1MB = 1000KB = 1000 * 1000바이트를 사용합니다.

+ **피드백 보내기**를 클릭하여 문제와 함께 피드백을 보냅니다.

    ![그래프 피드백](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>Spark 기록 서버의 진단 탭
작업 ID를 선택하고 도구 메뉴에서 **진단**을 클릭하여 작업 진단 뷰를 표시합니다. 진단 탭에는 **데이터 기울이기**, **시간 기울이기** 및 **실행기 사용량 분석**이 포함되어 있습니다.
    
+ 각 탭을 선택하여 **데이터 기울이기**, **시간 기울이기** 및 **실행기 사용량 분석**을 확인합니다.

    ![진단 탭](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>데이터 기울이기
**데이터 기울이기** 탭을 클릭하면 지정한 매개 변수에 따라 해당 기울이기 작업이 표시됩니다. 

+ **매개 변수 지정** - 첫 번째 섹션에는 데이터 기울이기를 검색하는 데 사용되는 매개 변수가 표시됩니다. 기본 제공 규칙은 작업 데이터 읽기가 평균 작업 데이터 읽기의 3배보다 크고, 작업 데이터 읽기가 10MB를 초과하는 것입니다. 기울어진 작업에 대한 고유한 규칙을 정의하려는 경우 매개 변수를 선택할 수 있으며 **기울어진 단계** 및 **문자 기울이기** 섹션이 그에 따라 새로 고쳐집니다. 

+ **기울어진 단계** - 두 번째 섹션에는 위에 지정된 조건을 충족하는 기울어진 작업이 있는 단계가 표시됩니다. 단계에 기울어진 작업이 두 개 이상 있는 경우 기울어진 단계 테이블에는 가장 많이 기울어진 작업(예: 데이터 기울이기 데이터가 가장 큰 작업)만 표시됩니다. 

    ![데이터 기울이기 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **기울이기 차트** - 기울이기 단계 테이블에서 행을 선택하면 기울이기 차트에 데이터 읽기 및 실행 시간을 기준으로 더 많은 작업 분포 정보가 표시됩니다. 기울어진 작업은 빨간색으로 표시되고 일반 작업은 파란색으로 표시됩니다. 성능을 고려하여 차트에는 최대 100개의 샘플 작업만 표시됩니다. 작업 정보는 오른쪽 아래 패널에 표시됩니다.

    ![데이터 기울이기 section3](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>시간 기울이기
**시간 기울이기** 탭에는 작업 실행 시간을 기준으로 기울어진 작업이 표시됩니다. 

+ **매개 변수 지정** - 첫 번째 섹션에는 시간 기울이기를 검색하는 데 사용되는 매개 변수가 표시됩니다. 시간 기울이기를 검색하는 기본 기준은 작업 실행 시간이 평균 실행 시간의 3배보다 크고 작업 실행 시간이 30초를 초과하는 것입니다. 필요에 따라 매개 변수를 변경할 수 있습니다. **기울어진 작업** 및 **기울이기 차트**에는 위의 **데이터 기울이기** 탭과 마찬가지로 해당 단계 및 작업 정보가 표시됩니다.

+ **시간 기울이기**를 클릭하면 **매개 변수 지정** 섹션에 설정된 매개 변수에 따라 필터링된 결과가 **기울어진 단계** 섹션에 표시됩니다. **기울어진 단계** 섹션에서 한 항목을 클릭하면 해당 차트가 section3에 초안으로 작성되고 작업 정보가 오른쪽 아래 패널에 표시됩니다.

    ![시간 기울이기 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>실행기 사용량 분석
실행기 사용량 그래프는 Spark 작업 실제 실행기 할당 및 실행 상태를 시각화합니다.  

+ **실행기 사용량 분석**을 클릭한 다음, 실행기 사용량에 대한 네 가지 유형 곡선의 초안을 작성합니다. 여기에는 **할당된 실행기**, **실행 중인 실행기**, **유휴 실행기** 및 **최대 실행기 인스턴스**가 포함됩니다. 할당된 실행기와 관련해서 각 “실행기 추가됨” 또는 “실행기 제거됨” 이벤트는 할당된 실행기를 늘리거나 줄입니다. 자세한 비교를 위해 “작업” 탭에서 “이벤트 타임라인”을 확인할 수 있습니다.

    ![실행기 탭](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ 색 아이콘을 클릭하여 모든 초안에서 해당 콘텐츠를 선택하거나 선택 취소합니다.

    ![차트 선택](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>알려진 문제
Spark 기록 서버에는 다음과 같은 알려진 문제가 있습니다.

+ 현재, Spark 2.3 클러스터에서만 작동합니다.

+ RDD를 사용하는 입출력 데이터는 데이터 탭에 표시되지 않습니다.

## <a name="next-steps"></a>다음 단계

* [시작 하기[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://docs.microsoft.com/en-us/sql/big-data-cluster/deploy-get-started?view=sqlallproducts-allversions)
* [Spark 설정 구성](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-settings)
