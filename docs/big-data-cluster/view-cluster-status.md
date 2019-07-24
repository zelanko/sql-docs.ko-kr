---
title: 클러스터 상태 보기
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 Azure Data Studio, 노트북 및 azdata 명령을 사용 하 여 빅 데이터 클러스터의 상태를 보는 방법을 설명 합니다.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6dca94b8bd7547222394d7809cb003b9e936982
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419293"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>빅 데이터 클러스터의 상태를 확인 하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 서비스 끝점에 액세스 하 고 SQL Server 빅 데이터 클러스터 (미리 보기)의 상태를 확인 하는 방법을 설명 합니다. Azure Data Studio 및 **azdata**를 모두 사용할 수 있으며,이 문서에서는 두 가지 방법을 모두 다룹니다.

## <a id="datastudio"></a>Azure Data Studio 사용

[Azure Data Studio](https://aka.ms/azdata-insiders)의 최신 **참가자 빌드** 를 다운로드 한 후에는 SQL Server 빅 데이터 클러스터 대시보드를 사용 하 여 서비스 끝점과 빅 데이터 클러스터의 상태를 볼 수 있습니다. 아래 기능 중 일부는 Azure Data Studio의 참가자 빌드에서는 처음에만 사용할 수 있습니다.

1. 먼저 Azure Data Studio에서 빅 데이터 클러스터에 대 한 연결을 만듭니다. 자세한 내용은 [Azure Data Studio를 사용 하 여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조 하세요.

1. 빅 데이터 클러스터 끝점을 마우스 오른쪽 단추로 클릭 하 고 **관리**를 클릭 합니다.

   ![관리를 마우스 오른쪽 단추로 클릭 합니다.](media/view-cluster-status/right-click-manage.png)

1. 빅 데이터 클러스터 **SQL Server** 탭을 선택 하 여 빅 데이터 클러스터 대시보드에 액세스 합니다.

   ![빅 데이터 클러스터 대시보드](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>서비스 끝점

빅 데이터 클러스터 내에서 다양 한 서비스에 쉽게 액세스할 수 있도록 하는 것이 중요 합니다. 빅 데이터 클러스터 대시보드는 서비스 끝점을 보고 복사할 수 있는 서비스 끝점 테이블을 제공 합니다.

![서비스 끝점](media/view-cluster-status/service-endpoints.png)

처음 몇 개 행은 다음 서비스를 노출 합니다.

- 응용 프로그램 프록시
- 클러스터 관리 서비스
- HDFS 및 Spark
- 관리 프록시

이러한 서비스에는 해당 서비스에 연결 하기 위해 끝점이 필요할 때 복사 하 고 붙여 넣을 수 있는 끝점이 나열 됩니다. 예를 들어 끝점의 오른쪽에 있는 복사 아이콘을 클릭 한 다음 해당 끝점을 요청 하는 텍스트 창에 붙여 넣을 수 있습니다. 클러스터 관리 서비스 끝점은 [클러스터 상태 노트북](#notebook)을 실행 하는 데 필요 합니다.

### <a name="dashboards"></a>대시보드

또한 서비스 끝점 테이블은 모니터링에 대 한 여러 대시보드를 노출 합니다.

- 메트릭 (Grafana)
- 로그 (Kibana)
- Spark 작업 모니터링
- Spark 리소스 관리

이러한 링크를 직접 클릭할 수 있습니다. 서비스에 연결 하기 전에 사용자 이름과 암호를 입력 하 라는 메시지가 두 번 표시 됩니다.

### <a id="notebook"></a>클러스터 상태 노트북

1. 클러스터 상태 노트북을 시작 하 여 빅 데이터 클러스터의 클러스터 상태를 볼 수도 있습니다. 노트북을 시작 하려면 **클러스터 상태** 작업을 클릭 합니다.

    ![시작한](media/view-cluster-status/cluster-status-launch.png)

2. 시작 하기 전에 다음 항목이 필요 합니다.

    - 빅 데이터 클러스터 이름
    - 컨트롤러 사용자 이름
    - 컨트롤러 암호
    - 컨트롤러 끝점

    기본 빅 데이터 클러스터 이름은 배포 중에 사용자 지정 하지 않는 한 **mssql-cluster** 입니다. 서비스 끝점 테이블의 빅 데이터 클러스터 대시보드에서 컨트롤러 끝점을 찾을 수 있습니다. 끝점은 **클러스터 관리 서비스로**나열 됩니다. 자격 증명을 모르는 경우 클러스터를 배포한 관리자에 게 문의 하세요.

3. 위쪽 도구 모음에서 **셀 실행** 을 클릭 합니다.

4. 자격 증명에 대 한 프롬프트를 따릅니다. 빅 데이터 클러스터 이름, 컨트롤러 사용자 이름 및 컨트롤러 암호에 대 한 각 자격 증명을 입력 한 후 enter 키를 누릅니다.

    > [!Note]
    > 빅 데이터를 사용 하 여 구성 파일을 설치 하지 않은 경우 컨트롤러 끝점을 묻는 메시지가 표시 됩니다. 입력 하거나 붙여 넣은 다음 ENTER 키를 눌러 계속 합니다.

5. 성공적으로 연결 된 경우 노트북의 나머지 부분에는 빅 데이터 클러스터의 각 구성 요소에 대 한 출력이 표시 됩니다. 특정 코드 셀을 다시 실행 하려면 코드 셀 위로 마우스를 이동 하 여 **실행** 아이콘을 클릭 합니다.

## <a name="use-azdata"></a>Azdata 사용

[Azdata](deploy-install-azdata.md) 명령을 사용 하 여 끝점과 클러스터 상태를 모두 볼 수도 있습니다.

### <a name="service-endpoints"></a>서비스 끝점

다음 단계를 사용 하 여 빅 데이터 클러스터에 대 한 외부 끝점의 IP 주소를 가져올 수 있습니다.

1. 다음 **kubectl** 명령의 외부 ip 출력을 살펴보면 컨트롤러 끝점의 IP 주소를 찾습니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 배포 하는 동안 기본 이름을 변경 하지 않은 경우에는 `-n mssql-cluster` 이전 명령을 사용 합니다. **mssql-cluster** 는 빅 데이터 클러스터의 기본 이름입니다.

1. [Azdata 로그인](reference-azdata.md)을 사용 하 여 빅 데이터 클러스터에 로그인 합니다. **--Controller-endpoint** 매개 변수를 컨트롤러 끝점의 외부 IP 주소로 설정 합니다.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   배포 하는 동안 컨트롤러에 대해 구성한 사용자 이름 및 암호 (CONTROLLER_USERNAME 및 CONTROLLER_PASSWORD)를 지정 합니다.

1. [Azdata bdc 끝점 목록을](reference-azdata-bdc-endpoint.md) 실행 하 여 각 끝점에 대 한 설명과 해당 IP 주소 및 포트 값이 포함 된 목록을 가져옵니다. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   다음 목록에서는이 명령의 샘플 출력을 보여 줍니다.

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

[Azdata bdc status show](reference-azdata-bdc-status.md) 명령을 사용 하 여 클러스터의 상태를 볼 수 있습니다.

```bash
azdata bdc status show -o table
```

> [!TIP]
> 상태 명령을 실행 하려면 먼저 이전 끝점 섹션에 표시 된 **azdata login** 명령을 사용 하 여 로그인 해야 합니다.

다음은이 명령의 샘플 출력을 보여 줍니다.

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

[Azdata bdc pool status show](reference-azdata-bdc-pool-status.md) 명령을 사용 하 여 클러스터 내에서 풀의 상태를 볼 수 있습니다. 이 명령을 사용 하려면 `--kind` 매개 변수를 사용 하 여 풀 유형을 지정 합니다. 풀 유형은 다음과 같습니다.

- 계산
- data
- master
- 떠
- 저장할

예를 들어 다음 명령은 저장소 풀의 풀 상태를 표시 합니다.

```bash
azdata bdc pool status show --kind storage
```

다음 출력과 유사한 텍스트가 표시 되어야 합니다.

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

값 `logsUrl` 은 로그 정보를 사용 하 여 kibana 대시보드에 연결 됩니다.

![Kibana 대시보드](./media/view-cluster-status/kibana-dashboard.png)

`nodeMetricsUrl` 및`sqlMetricsUrl` 값은 노드 상태 및 SQL 메트릭을 모니터링 하기 위한 grafana 대시보드에 연결 됩니다.

![Grafana 대시보드](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>컨트롤러 상태 보기

[Azdata bdc control status show](reference-azdata-bdc-control-status.md) 명령을 사용 하 여 컨트롤러 상태를 볼 수 있습니다. 빅 데이터 클러스터의 컨트롤러 노드와 관련 된 모니터링 대시보드와 유사한 링크를 제공 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [SQL Server 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
