---
title: Spark 응용 프로그램을 디버그/진단
titleSuffix: SQL Server big data clusters
description: Spark 기록 서버를 사용 하 여 디버그 및 SQL Server 2019 빅 데이터 클러스터에서 실행 중인 Spark 응용 프로그램 진단.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: e7444a9f5bcdc480425ba02c8a068831c081b47a
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860335"
---
# <a name="debug-and-diagnose-spark-applications-on-sql-server-big-data-clusters-in-spark-history-server"></a>디버그 및 Spark 기록 서버에서 SQL Server 빅 데이터 클러스터에 Spark 응용 프로그램 진단

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 확장 된 Spark 기록 서버를 사용 하 여 디버그를 SQL Server 2019 (미리 보기) 빅 데이터 클러스터에 Spark 응용 프로그램을 진단 하는 방법에 지침을 제공 합니다. 이러한 디버그 및 진단 기능 Spark 기록 서버에 기본 제공 되며 Microsoft에서 제공 됩니다. 확장에 데이터 탭 및 그래프 탭 진단 탭에 포함 됩니다. 데이터 탭에서 사용자는 Spark 작업의 입력 및 출력 데이터를 확인할 수 있습니다. 그래프 탭에서 사용자는 데이터 흐름을 확인 하 고 작업 그래프를 재생할 수 있습니다. 진단 탭에서 사용자는 실행 기 사용 현황 분석 데이터 기울이기, 시간 오차를 참조할 수 있습니다.

## <a name="get-access-to-spark-history-server"></a>Spark 기록 서버에 액세스

Spark 기록 서버 사용자 환경에서 오픈 소스 빅 데이터 클러스터에 대 한 작업 그래프와 데이터 흐름의 대화형 시각화 및 작업 관련 데이터를 포함 하는 정보를 사용 하 여 향상 되었습니다. 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>Spark 기록 서버 웹 URL로 UI 열기
다음 URL로 이동 하 여 Spark 기록 서버 열기 바꿉니다 `<Ipaddress>` 및 `<Port>` 빅 데이터 클러스터에 대 한 특정 정보를 사용 하 여 합니다. 자세한 정보를 참조할 수 있습니다. [SQL Server 빅 데이터 클러스터를 배포 합니다.](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

Spark 기록 서버 웹 UI 다음과 같습니다.

![Spark 기록 서버](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>Spark 기록 서버에서 데이터 탭
작업 ID를 선택한 다음 클릭 **데이터** 데이터 뷰를 가져오려면 도구 메뉴에서.

+ 확인 합니다 **입력**를 **출력**, 및 **테이블 작업** 별도로 탭을 선택 하 여 합니다.

    ![Spark 기록 서버 데이터 탭](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ 단추를 클릭 하 여 모든 행을 복사 **복사**합니다.

    ![모든 행 복사](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ 단추를 클릭 하 여 모든 데이터 CSV 파일로 저장 **csv**합니다.

    ![CSV 파일로 데이터를 저장 합니다.](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ 검색 필드에서 키워드를 입력 하 여 **검색**, 검색 결과 즉시 표시 됩니다.

    ![키워드를 사용 하 여 검색](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ 테이블을 정렬, 자세한 세부 정보를 표시할 행을 확장 하려면 더하기 기호를 클릭 하거나 행을 축소 하려면 빼기 기호를 클릭 하려면 열 머리글을 클릭 합니다.

    ![데이터 테이블 기능](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ 단추를 클릭 하 여 단일 파일 다운로드 **부분 다운로드** 선택한 파일은 로컬 위치에 다운로드 한 다음 오른쪽에 배치 하는입니다. 파일이 더 이상 존재 하지 않는, 오류 메시지를 표시할 새 탭이 열립니다.

    ![데이터 행을 다운로드 합니다.](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ 선택 하 여 전체 경로 또는 상대 경로 복사 합니다 **전체 경로 복사**를 **상대 경로 복사** 다운로드 메뉴에서를 확장 하는 합니다. Azure 데이터 레이크 저장소 파일에 대 한 **Azure Storage 탐색기에서 열기** Azure Storage 탐색기 시작 됩니다. 로그인 할 때 정확한 폴더를 찾습니다.

    ![전체 경로나 상대 경로 복사](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ 한 페이지에 표시할 행 대부분 이동할 수 표 아래 너무 때 페이지를 클릭 합니다. 

    ![데이터 페이지](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ 도구 설명에 표시할 데이터 옆에 있는 물음표를 마우스로 가리키거나 자세한 정보를 보려면 물음표를 클릭 합니다.

    ![데이터 자세한 정보](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ 클릭 하 여 문제를 사용 하 여 피드백을 전송할 **피드백을 제공**합니다.

    ![그래프 피드백](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>Spark 기록 서버에서 그래프 탭

작업 ID를 선택한 다음 클릭 **그래프** 작업 그래프 뷰를 가져오려면 도구 메뉴에서.

+ 생성 된 작업 그래프에서 작업의 개요를 확인 합니다. 

+ 기본적으로 모든 작업이 표시 됩니다 및에서 필터링 할 수 있습니다 **작업 ID**합니다.

    ![그래프 작업 ID](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ 상태로 두면 **진행률** 기본값으로 합니다. 사용자를 선택 하 여 데이터 흐름을 확인할 수 있습니다 **읽기** 또는 * * Written * 드롭다운 목록의 **표시**합니다.

    ![그래프 표시](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    열 지도 보여 주는 색 그래프 노드 표시 합니다.

    ![그래프 열 지도](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ 클릭 하 여 작업을 재생 합니다 **재생** 단추 및 [중지] 단추를 클릭 하 여 언제 든 지 중지 합니다. 재생 하는 경우 다른 상태를 표시 하도록 색에 표시 되는 작업:

    + 녹색 성공에 대 한 합니다. 작업이 완료 되었습니다.
    + 주황색에 대 한 다시 시도 합니다. 작업 실패 했지만 작업의 최종 결과 영향을 주지 않습니다의 인스턴스. 이러한 작업 복제 해야 하거나 나중에 처리할 수 있는 인스턴스를 다시 시도 하세요.
    + 실행에 대 한 파란색: 작업 실행 중입니다.
    + 대기 흰색이 나 작업을 건너뛰었습니다. 를 실행 하려고 대기 하는 작업 또는 단계를 무시 했습니다.
    + 빨간색 실패 했습니다. 작업에 실패 했습니다.

    ![색 샘플을 실행 중인 그래프](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    흰색에서 건너뛴된 단계 표시입니다.
    ![색 샘플 그래프를 건너뛰기](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![그래프 색상 샘플, 실패](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > 각 작업에 대 한 재생 허용 됩니다. 불완전 한 작업에 대 한 재생은 지원 되지 않습니다.


+ 입/출력 작업 그래프를 확대/축소 하거나 클릭 마우스 스크롤 **에 맞게 확대/축소** 화면에 맞춤 되도록 합니다.
 
    ![맞게 그래프 확대/축소](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ 도구 설명이 있는 경우 실패 한 작업을 보려면 그래프 노드에서 놓고 단계 단계 페이지를 열려면 클릭 합니다.

    ![그래프 도구 설명](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ 작업이 그래프 탭에서 단계 해야 도구 설명 및 작은 아이콘을 충족 하는 작업이 있는 경우 표시 되는 조건 아래:
    + 데이터 기울이기: 데이터 읽기 크기 > 평균 데이터 읽기이 단계 내의 모든 작업의 크기 * 2 및 데이터 읽기 크기 > 10MB
    + 시간차: 실행 시간 >이 단계 내의 모든 작업의 평균 실행 시간 * 2와 실행 시간 > 2 분

    ![그래프 오차 아이콘](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ 작업 그래프 노드는 각 단계에 다음 정보가 표시 됩니다.
    + ID를 삭제합니다.
    + 이름 또는 설명입니다.
    + 총 작업 수입니다.
    + 읽은 데이터: 순서 섞기 및 입력된 크기의 합은 읽기 크기입니다.
    + 데이터 쓰기: 출력 크기와 순서 섞기의 합은 쓰기 크기입니다.
    + 실행 시간: 첫 번째 시도의 시작 시간과 완료 시간이 마지막 시도의 간격입니다.
    + 행 개수: 출력 레코드, 읽기 레코드 순서 섞기 및 쓰기 레코드 순서 섞기가 입력된 레코드의 합계입니다.
    + 진행률입니다.

    > [!NOTE]
    > 기본적으로 작업 그래프 노드 (스테이지 실행 시간)을 제외 하 고 각 단계의 마지막 시도에서 정보를 표시 됩니다 있지만 노드 재생 그래프 중 각 시도의 정보를 표시 합니다.

    > [!NOTE]
    > 읽기 및 쓰기를 사용 하 여 1의 데이터 크기에 대 한 MB = 1000 KB = 1000 * 1000 바이트입니다.

+ 클릭 하 여 문제를 사용 하 여 피드백을 전송할 **피드백을 제공**합니다.

    ![그래프 피드백](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>Spark 기록 서버에서 진단 탭
작업 ID를 선택한 다음 클릭 **진단** 작업 진단 보기를 가져오려면 도구 메뉴에서. 진단 탭에는 **데이터 기울이기**를 **시간차**, 및 **실행자 사용 현황 분석**합니다.
    
+ 확인 합니다 **데이터 기울이기**를 **시간차**, 및 **실행자 사용 현황 분석** 각각 탭을 선택 하 여 합니다.

    ![진단 탭](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>데이터 기울이기
클릭 **데이터 기울이기** 해당 탭 불균형된 작업은 지정 된 매개 변수에 따라 표시 됩니다. 

+ **매개 변수를 지정** -첫 번째 섹션은 데이터 기울이기 검색에 사용 되는 매개 변수를 표시 합니다. 기본 제공 규칙 다음과 같습니다. 읽은 태스크 데이터를 읽은 평균 작업 데이터의 세 번 보다 큰 이며 읽은 태스크 데이터 10MB 이상. 불균형된 작업에 대 한 사용자 고유의 규칙을 정의 하려는 경우에 매개 변수를 선택할 수 있습니다 합니다 **기울어진 스테이지**, 및 **Char 기울이기** 섹션 그에 따라 새로 고쳐지는 합니다. 

+ **기울어진 스테이지** -두 번째 섹션은 위에 지정 된 조건을 충족 하는 작업을 기울였을 수 있는 단계를 표시 합니다. 단계에 둘 이상의 불균형된 작업 인 경우 기울어진된 스테이지 테이블 가장 불균형된 작업 (예를 들어, 데이터 오차에 대 한 가장 큰 데이터)만 표시 됩니다. 

    ![데이터 기울이기 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **차트를 기울이기** -오차 준비 테이블의 행을 선택 하는 경우 더 많은 작업에 대 한 배포 세부 정보 데이터 읽기 및 실행 시간에 따라 오차 차트가 표시 합니다. 불균형 된 작업을 빨간색으로 표시 됩니다 하 고 일반 작업을 파란색으로 표시 됩니다. 차트에는 성능 고려 사항에 대 한 최대 100 개의 샘플 태스크만 표시 됩니다. 작업 세부 정보는 오른쪽 아래 패널에 표시 됩니다.

    ![데이터 기울이기 section3](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>시간차
합니다 **시간차** 태스크 실행 시간에 따라 기울어진된 작업 탭에 표시 됩니다. 

+ **매개 변수를 지정** -첫 번째 섹션은 시간차 감지에 사용 되는 매개 변수를 표시 합니다. 시간차를 검색할 기본 조건은: 작업 실행 시간을 세 번의 평균 실행 시간 초과 및 태스크 실행 시간 30 초 보다 큽니다. 필요에 따라 매개 변수를 변경할 수 있습니다. 합니다 **기울어진 스테이지** 및 **기울이기 차트** 것과 마찬가지로 해당 단계 및 작업 정보를 표시 합니다 **데이터 기울이기** 위의 탭 합니다.

+ 클릭 **시간차**에 필터링 된 결과에 표시 됩니다 **기울어진 스테이지** 섹션에서 설정 매개 변수에 따라 섹션 **매개 변수 지정**합니다. 항목을 하나 클릭 **기울어진 스테이지** 섹션에서 해당 차트 section3의 초안을 작성 하 고 작업 세부 정보는 오른쪽 아래 패널에 표시 됩니다.

    ![시간 오차 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>실행 기 사용 현황 분석
실행 기 사용 그래프는 Spark 작업 실행 기 실제 할당 및 실행 상태를 시각화합니다.  

+ 클릭 **실행자 사용 현황 분석**, 실행자 사용에 대 한 네 가지 형식 곡선 초안에서는 다음입니다. 이들은 **실행자 할당**, **실행 기**를 **실행 기를 유휴**, 및 **최대 실행 기 인스턴스**합니다. 할당 된 실행 기에 대 한 각 "실행 자가 추가" 또는 "실행 자가 제거" 이벤트 증가 하거나 감소 실행 기를 할당된 합니다. 자세한 비교에 대 한 "작업" 탭에서 이벤트 타임 라인을 확인할 수 있습니다.

    ![실행 기 탭](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ 선택 하 여 모든 임시 보관 함에서 해당 콘텐츠를 선택 취소 합니다. 색 아이콘을 클릭 합니다.

    ![차트를 선택 합니다.](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>알려진 문제
Spark 기록 서버에 다음과 같은 알려진된 문제가 있습니다.

+ 현재에 작동 2.3 Spark 클러스터에 대 한 합니다.

+ RDD를 사용 하 여 입/출력 데이터 데이터 탭에 표시 되지 않습니다.

## <a name="next-steps"></a>다음 단계

* [HDInsight에서 Spark 클러스터용 리소스 관리](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-resource-manager)
* [Spark 설정 구성](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-settings)
