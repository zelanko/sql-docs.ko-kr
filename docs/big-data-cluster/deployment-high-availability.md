---
title: 고가용성을 사용 하 여 빅 데이터 클러스터 SQL Server 배포
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: 고가용성을 사용 하 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 여에 (미리 보기)를 배포 하는 방법에 대해 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4053ac15309b821a9cf50cf067ad459256369418
ms.sourcegitcommit: af5e1f74a8c1171afe759a4a8ff2fccb5295270a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71823583"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>고가용성을 사용 하 여 빅 데이터 클러스터 SQL Server 배포

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

빅 데이터 클러스터 (BDC)를 배포할 때 가용성 그룹 구성에서 배포 되도록 SQL Server master를 구성할 수 있습니다. 이 구성은 Kubernetes 인프라에서 기본 제공 상태 모니터링, 실패 검색 및 장애 조치 (failover) 메커니즘을 사용 하 여 사용 하도록 설정 하는 SQL Server 마스터의 안정성을 높입니다. AG (가용성 그룹)는 SQL Server 인스턴스에 중복성을 추가 합니다. 이 구성에서 모니터링, 실패 검색 및 장애 조치 (failover) 작업은 빅 데이터 클러스터 관리 서비스인 제어 서비스를 통해 관리 됩니다.

또한 데이터베이스 미러링 끝점 설정, 가용성 그룹 만들기 및 가용성 그룹에 데이터베이스 추가와 같은 기타 관리 작업은 빅 데이터 클러스터 플랫폼에서 제공 됩니다.

가용성 그룹에서 사용할 수 있는 몇 가지 기능은 다음과 같습니다.

1. 배포 구성 파일에 고가용성 설정이 지정 된 경우 이라는 `containedag` 단일 가용성 그룹이 만들어집니다. 기본적으로에 `containedag` 는 주 복제본을 포함 하 여 세 개의 복제본이 있습니다. 가용성 그룹에 대 한 모든 CRUD 작업은 내부적으로 관리 됩니다.
1. 모든 데이터베이스는 및 `master` `msdb`를 포함 하 여 가용성 그룹에 자동으로 추가 됩니다. Polybase 구성 데이터베이스는 각 복제본과 관련 된 인스턴스 수준 메타 데이터를 포함 하기 때문에 가용성 그룹에 포함 되지 않습니다.
1. 외부 끝점은 AG 데이터베이스에 연결 하기 위해 자동으로 프로 비전 됩니다. 이 끝점 `master-svc-external` 은 AG 수신기의 역할을 수행 합니다.
1. 보조 복제본에 대 한 읽기 전용 연결에 대해 두 번째 외부 끝점이 프로 비전 됩니다. 


# <a name="deploy"></a>배포

가용성 그룹에 SQL Server 마스터를 배포 하려면 다음을 수행 합니다.

1. `hadr` 기능 사용
1. AG에 대 한 복제본 수를 지정 합니다 (최소 3).
1. 읽기 전용 보조 복제본에 대 한 연결에 대해 만든 두 번째 외부 끝점의 세부 정보를 구성 합니다.

다음 단계는 이러한 설정을 포함 하는 패치 파일을 만드는 방법과 `aks-dev-test` 또는 `kubeadm-dev-test` 구성 프로필에 적용 하는 방법을 보여 줍니다. 이러한 단계는 HA 특성을 추가 하기 위해 `aks-dev-test` 프로필을 패치 하는 방법에 대 한 예제를 안내 합니다. Kubeadm 클러스터에 대 한 배포의 경우 비슷한 패치가 적용 되지만, **끝점** 섹션에서 **ServiceType** 에 대해 *nodeport* 를 사용 하 고 있는지 확인 합니다.

1. `patch.json` 파일 만들기

    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.resources.master.spec",
          "value": {
            "type": "Master",
            "replicas": 3,
            "endpoints": [
              {
                "name": "Master",
                "serviceType": "LoadBalancer",
                "port": 31433
              },
              {
                "name": "MasterSecondary",
                "serviceType": "LoadBalancer",
                "port": 31436
              }
            ],
            "settings": {
              "sql": {
                "hadr.enabled": "true"
              }
            }
          }
        }
      ]
    }
    ```

1. 대상 프로필 복제

    ```bash
    azdata bdc config init --source aks-dev-test --target custom-aks
    ```

1. 사용자 지정 프로필에 패치 파일을 적용 합니다.

    ```bash
    azdata bdc config patch -c custom-aks/bdc.json --patch-file patch.json
    ```
1. 위에서 만든 클러스터 구성 프로필을 사용 하 여 클러스터 배포를 시작 합니다.

    ```bash
    azdata bdc create --config-profile custom-aks --accept-eula yes
    ```

## <a name="connect-to-sql-server-databases"></a>SQL Server 데이터베이스에 연결

SQL Server 마스터에 대해 실행 하려는 작업의 유형에 따라 읽기 전용 작업의 경우 보조 복제본의 데이터베이스에 대 한 읽기/쓰기 작업의 주 복제본에 연결할 수 있습니다. 각 연결 유형에 대 한 개요는 다음과 같습니다.

### <a name="connect-to-databases-on-the-primary-replica"></a>주 복제본의 데이터베이스에 연결

주 복제본에 연결 하려면 끝점을 사용 `sql-server-master` 합니다. 이 끝점은 AG에 대 한 수신기 이기도 합니다. 모든 연결은 가용성 그룹의 컨텍스트에 있습니다. 예를 들어이 끝점을 사용 하는 기본 연결은 SQL Server 인스턴스 `master` `master` 데이터베이스가 아니라 AG 내의 데이터베이스에 연결 됩니다.

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

`Description                           Endpoint             Name               Protocol`
`------------------------------------  -------------------  -----------------  ----------`
`SQL Server Master Instance Front-End  13.64.235.192,31433  sql-server-master  tds`

> [!NOTE]
> 장애 조치 (Failover) 이벤트는 HDFS 또는 데이터 풀과 같은 원격 데이터 원본에서 데이터에 액세스 하는 분산 쿼리를 실행 하는 동안 발생할 수 있습니다. 응용 프로그램은 장애 조치 (failover)로 인해 연결이 끊어지는 경우 연결 다시 시도 논리를 갖도록 디자인 해야 합니다.  
>

### <a name="connect-to-databases-on-the-secondary-replicas"></a>보조 복제본의 데이터베이스에 연결

보조 복제본의 데이터베이스에 대 한 읽기 전용 연결의 경우 `sql-server-master-readonly` 끝점을 사용 합니다. 이 끝점은 모든 보조 복제본에서 부하 분산 장치 처럼 작동 합니다. 연결 문자열에 사용자 데이터베이스 컨텍스트를 제공 합니다.

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

`Description                                    Endpoint            Name                        Protocol`
`---------------------------------------------  ------------------  --------------------------  ----------`
`SQL Server Master Readable Secondary Replicas  13.64.238.24,31436  sql-server-master-readonly  tds`

### <a id="instance-connect"></a>SQL Server 인스턴스에 연결

서버 수준 구성을 설정 하거나 가용성 그룹에 데이터베이스를 수동으로 추가 하는 것과 같은 특정 작업 (데이터베이스를 복원 워크플로를 사용 하 여 만든 경우)에는 인스턴스에 연결 해야 합니다. 이 연결을 제공 하려면 외부 끝점을 노출 합니다. 다음은이 끝점을 노출 한 다음 복원 워크플로를 사용 하 여 만든 데이터베이스를 가용성 그룹에 추가 하는 방법을 보여 주는 예입니다.

- `sql-server-master` 끝점에 연결 하 고를 실행 하 여 주 복제본을 호스트 하는 pod를 확인 합니다.

    ```sql
    SELECT @@SERVERNAME
   ```

- 새 Kubernetes 서비스를 만들어 외부 끝점 노출

    Kubeadm 클러스터의 경우 아래 명령을 실행 합니다. 을 `podName` 이전 단계에서 반환 된 서버의 이름으로 바꾸고,를 `serviceName` 만든 `namespaceName`Kubernetes 서비스에 대 한 기본 이름으로 바꾸고,을 BDC 클러스터의 이름으로 바꿉니다.

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    Aks 클러스터를 실행 하는 경우 생성 되는 서비스의 형식이가 `LoadBalancer`된다는 점을 제외 하 고 동일한 명령을 실행 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    다음은 aks에 대해 실행 되는이 명령의 예입니다 `master-0`. 여기에서 주 복제본을 호스팅하는 pod는 다음과 같습니다.

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    만든 Kubernetes 서비스의 IP를 가져옵니다.

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> 가장 좋은 방법은 다음 명령을 실행 하 여 위에서 만든 Kubernetes 서비스를 삭제 하는 것입니다.
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- 가용성 그룹에 데이터베이스를 추가합니다.

    AG에 데이터베이스를 추가 하려면 전체 복구 모드에서 실행 해야 하 고 로그 백업을 수행 해야 합니다. 위에서 만든 Kubernetes 서비스에서 IP를 사용 하 고 SQL Server 인스턴스에 연결한 후 아래와 같이 TSQL 문을 실행 합니다.

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    다음 예에서는 인스턴스에서 복원 된 라는 `sales` 데이터베이스를 추가 합니다.

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>알려진 제한 사항

다음은 빅 데이터 클러스터에서 SQL Server 마스터의 가용성 그룹에 대 한 알려진 문제 및 제한 사항입니다.

- 이와 다른 워크플로의 결과로 만들어진 데이터베이스는 가용성 그룹에 자동으로 추가 되지 않습니다. `CREATE DATABASE FROM SNAPSHOT` `CREATE DATABASE` `RESTORE` [인스턴스에 연결](#instance-connect) 하 고 데이터베이스를 가용성 그룹에 수동으로 추가 합니다.
- 에서 `sp_configure` 서버 구성 설정 실행과 같은 특정 작업을 수행 하려면 마스터 인스턴스에 연결 해야 합니다. 해당 하는 기본 끝점을 사용할 수 없습니다. [지침](#instance-connect) 에 따라 SQL Server 인스턴스에 연결 하 고를 실행 `sp_configure`합니다.
- BDC를 배포할 때 고가용성 구성을 만들어야 합니다. 가용성 그룹 배포 후 배포를 사용 하 여 고가용성 구성을 사용 하도록 설정할 수 없습니다.

## <a name="next-steps"></a>다음 단계

- 빅 데이터 클러스터 배포에서 구성 파일을 사용 하는 방법에 대 한 자세한 내용은 [Kubernetes에서 배포 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 하는 방법](deployment-guidance.md#configfile)을 참조 하세요.
- SQL Server의 가용성 그룹 기능에 대 한 자세한 내용은 [Always On 가용성 그룹 개요 (SQL Server)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2017)를 참조 하세요.
