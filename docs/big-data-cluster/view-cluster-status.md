---
title: 클러스터 상태 보기
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 Azure Data Studio, 노트북 및 mssqlctl 명령을 사용 하 여 빅 데이터 클러스터의 상태를 확인 하는 방법에 설명 합니다.
author: yualan
ms.author: alayu
manager: jroth
ms.date: 06/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2edd49c37655d420cf8022677c0d0287028a0b93
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413970"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>빅 데이터 클러스터의 상태를 보는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 서비스 끝점에 액세스 하 고 SQL Server 빅 데이터 클러스터 (미리 보기)의 상태를 확인 하는 방법을 설명 합니다. 두 Azure Data Studio를 사용할 수 있습니다 하 고 **mssqlctl**,이 문서에서는 두 가지 방법을 모두 설명 하 고 있습니다.

## <a id="datastudio"></a> Azure Data Studio 사용

최신 버전을 다운로드 한 후 **참가자 빌드** 의 [Azure Data Studio](https://aka.ms/azdata-insiders), 서비스 끝점을 확인할 수 있습니다 및 SQL Server 빅 데이터 클러스터 대시보드를 사용 하 여 빅 데이터의 상태를 클러스터 합니다. 참고 아래의 기능 중 일부는 먼저 Azure Data Studio의 참가자 빌드를 사용할 수 있습니다.

1. 먼저 Azure 데이터 스튜디오에서 빅 데이터 클러스터에 대 한 연결을 만듭니다. 자세한 내용은 [Azure Data Studio를 사용 하 여 빅 데이터 클러스터를 SQL Server에 연결](connect-to-big-data-cluster.md)합니다.

1. 빅 데이터 클러스터 끝점을 마우스 오른쪽 단추로 클릭 하 고 클릭 **관리**합니다.

   ![마우스 오른쪽 단추로 클릭 관리](media/view-cluster-status/right-click-manage.png)

1. 선택 된 **SQL Server 빅 데이터 클러스터** 빅 데이터 클러스터 대시보드에 액세스 하려면 탭 합니다.

   ![빅 데이터 클러스터 대시보드](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>서비스 끝점

빅 데이터 클러스터 내에서 다양 한 서비스를 쉽게 액세스할 수 있어야 하는 것이 반드시 합니다. 빅 데이터 클러스터 대시보드 보고 서비스 끝점을 복사 할 수 있는 서비스 끝점 테이블을 제공 합니다.

![서비스 끝점](media/view-cluster-status/service-endpoints.png)

처음 몇 행 다음 서비스를 노출합니다.

- 응용 프로그램 프록시
- 클러스터 관리 서비스
- HDFS 및 Spark
- 관리 프록시

이러한 서비스는 복사 하 고 해당 서비스에 연결 하기 위한 끝점을 할 때를 붙여넣을 수 있는 끝점을 나열 합니다. 예를 들어, 끝점의 오른쪽에 복사 아이콘을 클릭 하 고 해당 끝점을 요청 하는 텍스트 창에 붙여넣을 수 있습니다. 클러스터 관리 서비스 끝점은 실행 해야 합니다 [클러스터 상태 notebook](#notebook)합니다.

### <a name="dashboards"></a>대시보드

서비스 끝점 테이블에는 모니터링에 대 한 몇 가지 대시보드는 노출합니다.

- 메트릭 (Grafana)
- 로그 (Kibana)
- Spark 작업 모니터링
- Spark 리소스 관리

직접 이러한 링크를 클릭할 수 있습니다. 서비스에 연결 하기 전에 사용자 이름과 암호를 제공 하는 두 번 묻는 메시지가 나타납니다.

### <a id="notebook"></a> 클러스터 상태 notebook

1. 또한 클러스터 상태 notebook을 실행 하 여 빅 데이터 클러스터의 클러스터 상태를 볼 수 있습니다. 노트북을 시작 하려면 클릭 합니다 **클러스터 상태** 작업 합니다.

    ![시작](media/view-cluster-status/cluster-status-launch.png)

2. 시작 하기 전에 다음 항목이 필요 합니다.

    - 빅 데이터 클러스터 이름
    - 컨트롤러 사용자 이름
    - 컨트롤러 암호
    - 컨트롤러 끝점

    기본 빅 데이터 클러스터 이름이 **mssql 클러스터** 배포 하는 동안 사용자 지정 하지 않으면. 서비스 끝점 테이블에서 빅 데이터 클러스터 대시보드에서 컨트롤러 끝점을 찾을 수 있습니다. 끝점으로 나열 됩니다 **클러스터 관리 서비스**합니다. 자격 증명을 알 수 없는 경우 요청 하는 관리자가 클러스터를 배포 합니다.

3. 클릭 **셀 실행** 상단 도구 모음에서 합니다.

4. 자격 증명에 대 한 프롬프트를 따릅니다. Press ENTER 키를 눌러 하면 빅 데이터 클러스터 이름, 컨트롤러 사용자 이름 및 컨트롤러 암호에 대 한 각 자격 증명을 입력 합니다.

    > [!Note]
    > 빅 데이터를 사용 하 여 구성 파일 설정 없으면 컨트롤러 끝점에 대해 묻는 메시지가 나타납니다. 입력 하거나 붙여넣고 enter 키를 눌러 계속 합니다.

5. 성공적으로 연결한 경우 notebook의 나머지 부분에는 빅 데이터 클러스터의 각 구성 요소의 출력을 표시 됩니다. 특정 코드 셀을 다시 실행 하려는 코드 셀을 마우스로 클릭 하 여 **실행** 아이콘입니다.

## <a name="use-mssqlctl"></a>mssqlctl 사용

사용할 수도 있습니다 [mssqlctl](deploy-install-mssqlctl.md) 끝점 및 클러스터 상태를 보기 위해 명령입니다.

### <a name="service-endpoints"></a>서비스 끝점

다음 단계를 사용 하 여 빅 데이터 클러스터에 대 한 외부 끝점의 IP 주소를 가져올 수 있습니다.

1. 다음의 외부 IP 출력을 보면 컨트롤러 끝점의 IP 주소를 찾으려면 **kubectl** 명령:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 사용 하 여 배포 하는 동안 기본 이름을 변경 하지 않은, 경우 `-n mssql-cluster` 이전 명령에서. **mssql 클러스터** 빅 데이터 클러스터에 대 한 기본 이름입니다.

1. 사용 하 여 빅 데이터 클러스터에 로그인 [mssqlctl 로그인](reference-mssqlctl.md)합니다. 설정 된 **-컨트롤러 끝점** 컨트롤러 끝점의 외부 IP 주소 매개 변수입니다.

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   배포 하는 동안 사용자 이름 및 컨트롤러 (CONTROLLER_USERNAME 및 CONTROLLER_PASSWORD)에 대해 구성한 암호를 지정 합니다.

1. 실행할 [mssqlctl bdc 끝점 목록](reference-mssqlctl-bdc-endpoint.md) 각 끝점 및 해당 IP 주소 및 포트 값에 대 한 설명 사용 하 여 목록을 가져올 수 있습니다. 

   ```bash
   mssqlctl bdc endpoint list -o table
   ```

   다음은이 명령의 샘플 출력을 보여 줍니다.

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

### <a name="view-cluster-status"></a>클러스터 상태 보기

사용 하 여 클러스터의 상태를 볼 수는 [mssqlctl bdc 상태 표시](reference-mssqlctl-bdc-status.md) 명령입니다.

```bash
mssqlctl bdc status show -o table
```

> [!TIP]
> 상태 명령을 실행 하려면 하면 먼저 로그인 해야 합니다 **mssqlctl 로그인** 이전 끝점 섹션에 표시 된 명령입니다.

다음은이 명령의 샘플 출력입니다.

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

### <a name="view-pool-status"></a>풀 상태 보기

사용 하 여 클러스터 내에서 풀의 상태를 볼 수 있습니다 합니다 [mssqlctl bdc 풀 상태 표시](reference-mssqlctl-bdc-pool-status.md) 명령입니다. 이 명령을 사용 하려면 사용 하 여 풀의 유형을 지정 합니다 `--kind` 매개 변수입니다. 풀 유형은 다음과 같습니다.

- 계산
- data
- master
- Spark
- 저장소

예를 들어 다음 명령은 저장소 풀의 풀 상태 표시:

```bash
mssqlctl bdc pool status show --kind storage
```

다음 출력과 유사한 텍스트가 표시 됩니다.

```output
[
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/logs/ui",
    "name": "storage-0-0",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/sqlmetrics/ui",
    "state": "Running"
  },
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/logs/ui",
    "name": "storage-0-1",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/sqlmetrics/ui",
    "state": "Running"
  }
]
```

`logsUrl` 로그 정보를 사용 하 여 kibana 대시보드에 대 한 링크를 값:

![kibana 대시보드](./media/view-cluster-status/kibana-dashboard.png)

합니다 `nodeMetricsUrl` 및 `sqlMetricsUrl` 값 노드 상태 및 SQL 메트릭을 모니터링 하는 것에 대 한 grafana 대시보드에 연결 합니다.

![Grafana 대시보드](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>컨트롤러 상태 보기

사용 하 여 컨트롤러 상태를 볼 수는 [mssqlctl bdc 컨트롤 상태 표시](reference-mssqlctl-bdc-control-status.md) 명령입니다. 유사한 링크 빅 데이터 클러스터 노드의 컨트롤러와 관련 된 모니터링 대시보드를 제공 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하십시오 [SQL Server 빅 데이터 클러스터 이란](big-data-cluster-overview.md)합니다.
