---
title: 클러스터 상태 보기
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 Azure Data Studio, Notebook 및 azdata 명령을 사용하여 빅 데이터 클러스터의 상태를 보는 방법을 설명합니다.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 028864712658e35913fa04fb1a85e4ca960ad573
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653278"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>빅 데이터 클러스터의 상태를 보는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 서비스 엔드포인트에 액세스하고 SQL Server 빅 데이터 클러스터(미리 보기)의 상태를 보는 방법을 설명합니다. Azure Data Studio 및 **azdata**를 모두 사용할 수 있으며, 이 문서에서는 두 가지 방법을 모두 설명합니다.

## <a id="datastudio"></a> Azure Data Studio 사용

[Azure Data Studio](https://aka.ms/azdata-insiders)의 최신 **참가자 빌드**를 다운로드한 후에 SQL Server 빅 데이터 클러스터 대시보드를 사용하여 서비스 엔드포인트와 빅 데이터 클러스터 상태를 볼 수 있습니다. 아래 기능 중 일부는 Azure Data Studio 참가자 빌드에서만 처음으로 제공되는 것입니다.

1. 먼저 Azure Data Studio에서 빅 데이터 클러스터에 연결합니다. 자세한 내용은 [Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조하세요.

1. 빅 데이터 클러스터 엔드포인트를 마우스 오른쪽 단추로 클릭하고 **관리**를 클릭합니다.

   ![관리를 마우스 오른쪽 단추로 클릭](media/view-cluster-status/right-click-manage.png)

1. **SQL Server 빅 데이터 클러스터** 탭을 선택하여 빅 데이터 클러스터 대시보드에 액세스합니다.

   ![빅 데이터 클러스터 대시보드](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>서비스 엔드포인트

빅 데이터 클러스터의 다양한 서비스에 쉽게 액세스할 수 있어야 합니다. 빅 데이터 클러스터 대시보드는 서비스 엔드포인트를 확인하고 복사할 수 있는 서비스 엔드포인트 테이블을 제공합니다.

![서비스 엔드포인트](media/view-cluster-status/service-endpoints.png)

처음 몇 개 행은 다음 서비스를 공개합니다.

- 애플리케이션 프록시
- 클러스터 관리 서비스
- HDFS 및 Spark
- 관리 프록시

서비스에는 해당 서비스에 연결하기 위한 엔드포인트가 필요할 때 복사하여 붙여넣을 수 있는 엔드포인트가 표시됩니다. 예를 들어 엔드포인트 오른쪽에 있는 복사 아이콘을 클릭한 다음, 해당 엔드포인트를 요청하는 텍스트 창에 붙여넣을 수 있습니다. 클러스터 관리 서비스 엔드포인트는 [클러스터 상태 Notebook](#notebook)을 실행하는 데 필요합니다.

### <a name="dashboards"></a>대시보드

서비스 엔드포인트 테이블은 모니터링에 사용되는 몇 개의 대시보드도 공개합니다.

- 메트릭(Grafana)
- 로그(Kibana)
- Spark 작업 모니터링
- Spark 리소스 관리

이러한 링크를 직접 클릭할 수 있습니다. 서비스에 연결하기 전에 사용자 이름과 암호를 입력하라는 메시지가 두 번 표시됩니다.

### <a id="notebook"></a> 클러스터 상태 Notebook

1. 클러스터 상태 Notebook을 시작하여 빅 데이터 클러스터의 클러스터 상태를 볼 수도 있습니다. Notebook을 시작하려면 **클러스터 상태** 작업을 클릭합니다.

    ![시작](media/view-cluster-status/cluster-status-launch.png)

2. 시작하기 전에 다음 항목이 필요합니다.

    - 빅 데이터 클러스터 이름
    - 컨트롤러 사용자 이름
    - 컨트롤러 암호
    - 컨트롤러 엔드포인트

    빅 데이터 클러스터의 기본 이름은 배포 중에 사용자 지정하지 않은 경우 **mssql-cluster**입니다. 서비스 엔드포인트 테이블의 빅 데이터 클러스터 대시보드에서 컨트롤러 엔드포인트를 찾을 수 있습니다. 엔드포인트는 **클러스터 관리 서비스**로 나열됩니다. 자격 증명을 모르는 경우 클러스터를 배포한 관리자에게 문의합니다.

3. 위쪽 도구 모음에서 **셀 실행**을 클릭합니다.

4. 프롬프트를 따라 자격 증명을 제공합니다. 빅 데이터 클러스터 이름, 컨트롤러 사용자 이름 및 컨트롤러 암호의 자격 증명을 각각 입력한 후에 Enter 키를 누릅니다.

    > [!Note]
    > 빅 데이터로 설정된 구성 파일이 없으면 컨트롤러 엔드포인트를 묻는 메시지가 표시됩니다. 입력하거나 붙여넣은 다음 Enter 키를 눌러 계속 진행합니다.

5. 성공적으로 연결된 경우 Notebook의 나머지 부분에 빅 데이터 클러스터의 각 구성 요소에 대한 출력이 표시됩니다. 특정 코드 셀을 다시 실행하려면 코드 셀을 마우스로 가리키고 **실행** 아이콘을 클릭합니다.

## <a name="use-azdata"></a>azdata 사용

[azdata](deploy-install-azdata.md) 명령을 사용하여 엔드포인트와 클러스터 상태를 모두 볼 수도 있습니다.

### <a name="service-endpoints"></a>서비스 엔드포인트

다음 단계를 사용하여 빅 데이터 클러스터의 외부 엔드포인트 IP 주소를 가져올 수 있습니다.

1. 다음 **kubectl** 명령의 EXTERNAL-IP 출력을 통해 컨트롤러 엔드포인트의 IP 주소를 찾습니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 배포 중에 기본 이름을 변경하지 않은 경우에는 위 명령에서 `-n mssql-cluster`를 사용합니다. **mssql-cluster**는 빅 데이터 클러스터의 기본 이름입니다.

1. [azdata login](reference-azdata.md)을 사용하여 빅 데이터 클러스터에 로그인합니다. **--controller-endpoint** 매개 변수를 컨트롤러 엔드포인트의 외부 IP 주소로 설정합니다.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   배포 중에 컨트롤러에 대해 구성한 사용자 이름 및 암호(CONTROLLER_USERNAME 및 CONTROLLER_PASSWORD)를 지정합니다.

1. [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md)를 실행하여 각 엔드포인트에 대한 설명과 해당 IP 주소 및 포트 값이 포함된 목록을 가져옵니다. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   다음 목록은 이 명령의 샘플 출력을 보여 줍니다.

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

[azdata bdc status show](reference-azdata-bdc-status.md) 명령을 사용하여 클러스터 상태를 볼 수 있습니다.

```bash
azdata bdc status show -o table
```

> [!TIP]
> 상태 명령을 실행하려면 먼저 이전 엔드포인트 섹션에 표시된 **azdata login** 명령을 사용하여 로그인해야 합니다.

다음은 이 명령의 샘플 출력을 보여 줍니다.

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

[azdata bdc pool status show](reference-azdata-bdc-pool-status.md) 명령을 사용하여 클러스터의 풀 상태를 볼 수 있습니다. 이 명령을 사용하려면 `--kind` 매개 변수를 통해 풀 유형을 지정합니다. 풀 유형은 다음과 같습니다.

- compute
- 데이터
- master
- spark
- storage

예를 들어 다음 명령은 스토리지 풀의 풀 상태를 표시합니다.

```bash
azdata bdc pool status show --kind storage
```

다음 출력과 유사한 텍스트가 표시되어야 합니다.

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

`logsUrl` 값은 로그 정보가 포함된 kibana 대시보드에 연결됩니다.

![Kibana 대시보드](./media/view-cluster-status/kibana-dashboard.png)

`nodeMetricsUrl` 및 `sqlMetricsUrl` 값은 노드 상태 및 SQL 메트릭을 모니터링하기 위한 grafana 대시보드에 연결됩니다.

![Grafana 대시보드](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>컨트롤러 상태 보기

[azdata bdc control status show](reference-azdata-bdc-control-status.md) 명령을 사용하여 컨트롤러 상태를 볼 수 있습니다. 빅 데이터 클러스터의 컨트롤러 노드와 관련된 모니터링 대시보드에 연결된 유사한 링크가 제공됩니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [항목 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](big-data-cluster-overview.md)을 참조 하세요.
