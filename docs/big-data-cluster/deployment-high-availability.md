---
title: 고가용성을 사용하여 SQL Server 빅 데이터 클러스터 배포
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: 고가용성을 사용하여 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 09/18/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 17aaed99c8adb73b88a2d81482fcdefc7d8f68fd
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990024"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>고가용성을 사용하여 SQL Server 빅 데이터 클러스터 배포

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

SQL Server 빅 데이터 클러스터는 Kubernetes에 컨테이너화된 애플리케이션으로 제공되고 상태 저장 세트 및 영구 스토리지와 같은 기능을 사용하므로, 이 인프라에는 클러스터 구성 요소에서 서비스 상태를 유지하는 데 활용하는 기본적으로 제공되는 상태 모니터링, 실패 검색 및 장애 조치 메커니즘이 있습니다. 안정성을 높이기 위해 고가용성 구성에서 추가 복제본과 함께 배포하도록 SQL Server 마스터 인스턴스 및/또는 HDFS 이름 노드 및 Spark 공유 서비스를 구성할 수도 있습니다. 모니터링, 실패 검색 및 자동 장애 조치는 빅 데이터 클러스터 관리 서비스, 즉 제어 서비스를 통해 관리됩니다. 이 서비스는 사용자 개입 없이 가용성 그룹 설정, 데이터베이스 미러링 엔드포인트 구성에서 가용성 그룹에 데이터베이스 추가 또는 장애 조치(failover) 및 업그레이드 조정에 이르기까지 모든 기능을 제공합니다. 

다음 이미지는 SQL Server 빅 데이터 클러스터에서 가용성 그룹을 배포하는 방법을 나타냅니다.

:::image type="content" source="media/deployment-high-availability/contained-ag.png" alt-text="high-availability-ag-bdc":::

가용성 그룹에서 사용할 수 있는 몇 가지 기능은 다음과 같습니다.

- 고가용성 설정이 배포 구성 파일에 지정되면 `containedag`라는 단일 가용성 그룹이 만들어집니다. 기본적으로 `containedag`에는 주 복제본을 포함하여 세 개의 복제본이 있습니다. 가용성 그룹 만들기 또는 만들어진 가용성 그룹에 복제본 조인을 포함하여 가용성 그룹에 대한 모든 CRUD 작업은 내부적으로 관리됩니다. 빅 데이터 클러스터의 SQL Server 마스터 인스턴스에서는 추가 가용성 그룹을 만들 수 없습니다.
- 모든 사용자 및 시스템 데이터베이스(예: `master` 및 `msdb`)를 포함하여 모든 데이터베이스가 가용성 그룹에 자동으로 추가됩니다. 이 기능은 가용성 그룹 복제본 전체에서 단일 시스템 보기를 제공합니다. 추가 모델 데이터베이스(`model_replicatedmaster` 및 `model_msdb`)는 시스템 데이터베이스의 복제된 부분을 시드하는 데 사용됩니다. 이러한 데이터베이스 외에도 인스턴스에 직접 연결하면 `containedag_master` 및 `containedag_msdb` 데이터베이스가 표시됩니다. `containedag` 데이터베이스는 가용성 그룹 내의 `master` 및 `msdb`를 나타냅니다.

  > [!IMPORTANT]
  > 데이터베이스 연결과 같은 워크플로 결과로 인스턴스에 생성된 데이터베이스는 가용성 그룹에 자동으로 추가되지 않으며, 빅 데이터 클러스터 관리자가 수동으로 추가해야 합니다. SQL Server 인스턴스 master 데이터베이스에 임시 엔드포인트를 사용하도록 설정하는 방법에 대한 지침은 [SQL Server 인스턴스에 연결](#instance-connect) 섹션을 참조하세요. SQL Server 2019 CU2 릴리스 이전에는 RESTORE 문의 결과로 생성된 데이터베이스에도 동일한 동작이 적용되어, 포함된 가용성 그룹에 데이터베이스를 수동으로 추가해야 했습니다.
  >
- Polybase 구성 데이터베이스는 각 복제본과 관련된 인스턴스 수준 메타데이터를 포함하므로 가용성 그룹에 포함되지 않습니다.
- 외부 엔드포인트는 가용성 그룹 내의 데이터베이스에 연결하기 위해 자동으로 프로비저닝됩니다. 이 `master-svc-external` 엔드포인트는 가용성 그룹 수신기의 역할을 수행합니다.
- 두 번째 외부 엔드포인트는 보조 복제본에 대한 읽기 전용 연결을 위해 프로비저닝되어 읽기 워크로드를 확장합니다.

## <a name="deploy"></a>배포

SQL Server 마스터를 가용성 그룹에 배포하려면 다음을 수행합니다.

1. `hadr` 기능을 사용하도록 설정합니다.
1. AG에 대한 복제본 수(최소 3개)를 지정합니다.
1. 읽기 전용 보조 복제본에 연결하기 위해 만든 두 번째 외부 엔드포인트에 대한 세부 정보를 구성합니다.

`aks-dev-test-ha` 또는 기본 제공되는 `kubeadm-prod` 구성 프로필을 사용하여 빅 데이터 클러스터 사용자 지정을 시작할 수 있습니다. 프로필에는 추가 고가용성을 구성할 수 있는 리소스에 필요한 설정이 포함됩니다. 예를 들어 SQL Server 마스터 인스턴스에 대한 가용성 그룹을 사용하도록 설정하는 것과 관련된 `bdc.json` 구성 파일의 섹션은 다음과 같습니다.  

```json
{
  ...
    "spec": {
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
  ...
}
```

다음 단계에서는 `aks-dev-test-ha` 프로필에서 시작하여 빅 데이터 클러스터 배포 구성을 사용자 지정하는 방법에 대한 예제를 안내합니다. `kubeadm` 클러스터에 배포하는 경우 비슷한 단계가 적용되지만 `endpoints` 섹션의 `serviceType`에 `NodePort`를 사용하고 있는지 확인합니다.

1. 대상 프로필을 복제합니다.

    ```bash
    azdata bdc config init --source aks-dev-test-ha --target custom-aks-ha
    ```

1. 필요에 따라 사용자 지정 프로필을 편집합니다. 
1. 위에서 만든 클러스터 구성 프로필을 사용하여 클러스터 배포를 시작합니다.

    ```bash
    azdata bdc create --config-profile custom-aks-ha --accept-eula yes
    ```

## <a name="connect-to-sql-server-databases-in-the-availability-group"></a>가용성 그룹의 SQL Server 데이터베이스에 연결

SQL Server 마스터에 대해 실행하려는 작업의 유형에 따라 읽기-쓰기 작업의 경우 주 복제본에 연결하거나, 읽기 전용 작업 유형의 경우 보조 복제본의 데이터베이스에 연결할 수 있습니다. 각 연결 유형에 대한 개요는 다음과 같습니다.

### <a name="connect-to-databases-on-the-primary-replica"></a>주 복제본의 데이터베이스에 연결

주 복제본에 연결하려면 `sql-server-master` 엔드포인트를 사용합니다. 이 엔드포인트는 AG의 수신기이기도 합니다. 이 엔드포인트를 사용하는 경우 모든 연결이 가용성 그룹 내의 데이터베이스 컨텍스트에 있습니다. 예를 들어 이 엔드포인트를 사용하는 기본 연결로 인해 SQL Server 인스턴스 `master` 데이터베이스가 아니라 가용성 그룹 내의 `master` 데이터베이스에 연결됩니다. 다음 명령을 실행하여 엔드포인트를 찾습니다.

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

```
Description                           Endpoint             Name               Protocol
------------------------------------  -------------------  -----------------  ----------
SQL Server Master Instance Front-End  11.11.111.111,11111  sql-server-master  tds
```

> [!NOTE]
> 장애 조치 이벤트는 HDFS 또는 데이터 풀과 같은 원격 데이터 원본의 데이터에 액세스하는 분산 쿼리를 실행하는 동안 발생할 수 있습니다. 장애 조치로 인해 연결이 끊기는 경우 애플리케이션에서 연결 다시 시도 논리를 사용하도록 설계하는 것이 좋습니다.  
>

### <a name="connect-to-databases-on-the-secondary-replicas"></a>보조 복제본의 데이터베이스에 연결

보조 복제본의 데이터베이스에 대한 읽기 전용 연결의 경우 `sql-server-master-readonly` 엔드포인트를 사용합니다. 이 엔드포인트는 모든 보조 복제본에서 부하 분산 장치처럼 작동합니다.  이 엔드포인트를 사용하는 경우 모든 연결이 가용성 그룹 내의 데이터베이스 컨텍스트에 있습니다. 예를 들어 이 엔드포인트를 사용하는 기본 연결로 인해 SQL Server 인스턴스 `master` 데이터베이스가 아니라 가용성 그룹 내의 `master` 데이터베이스에 연결됩니다. 

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

```
Description                                    Endpoint            Name                        Protocol
---------------------------------------------  ------------------  --------------------------  ----------
SQL Server Master Readable Secondary Replicas  11.11.111.11,11111  sql-server-master-readonly  tds
```

## <a name="connect-to-sql-server-instance"></a><a id="instance-connect"></a> SQL Server 인스턴스에 연결

서버 수준 구성 설정 또는 수동으로 가용성 그룹에 데이터베이스 추가와 같은 특정 작업의 경우 SQL Server 인스턴스에 연결해야 합니다. SQL Server 2019 CU2 이전에는 `sp_configure`, `RESTORE DATABASE` 또는 가용성 그룹 DDL과 같은 작업에 이 연결 형식이 필요합니다. 기본적으로 빅 데이터 클러스터에는 인스턴스 연결을 사용하도록 설정하는 엔드포인트가 포함되지 않으므로 이 엔드포인트는 수동으로 공개해야 합니다. 

> [!IMPORTANT]
> SQL Server 인스턴스 연결에 공개된 엔드포인트는 Active Directory를 사용하도록 설정된 클러스터에서도 SQL 인증만 지원합니다. 빅 데이터 클러스터를 배포하는 동안 기본적으로 `sa` 로그인을 사용하지 않도록 설정되고, 배포 시 `AZDATA_USERNAME` 및 `AZDATA_PASSWORD` 환경 변수에 제공되는 값에 따라 새 `sysadmin` 로그인이 프로비저닝됩니다.

> [!IMPORTANT]
> 포함된 가용성 그룹 DDL은 BDC가 단독으로 자체 관리합니다. 포함된 가용성 또는 데이터베이스 미러링 엔드포인트를 삭제하려는 (외부 사용자의) 시도는 지원되지 않으며, 이로 인해 복구할 수 없는 BDC 상태가 될 수 있습니다.

이 엔드포인트를 공개한 다음, 복원 워크플로를 사용하여 만든 데이터베이스를 가용성 그룹에 추가하는 방법을 보여 주는 예제는 다음과 같습니다. `sp_configure`를 사용하여 서버 구성을 변경하려는 경우 SQL Server 마스터 인스턴스에 대한 연결을 설정하는 방법에 대한 비슷한 지침이 적용됩니다.

> [!NOTE]
> SQL Server 2019 CU2부터 복원 워크플로의 결과로 생성된 데이터베이스가 포함된 가용성 그룹에 자동으로 추가됩니다.

- `sql-server-master` 엔드포인트에 연결하여 주 복제본을 호스팅하는 Pod를 결정하고 다음을 실행합니다.

    ```sql
    SELECT @@SERVERNAME
   ```

- 새 Kubernetes 서비스를 만들어 외부 엔드포인트를 공개합니다.

    `kubeadm` 클러스터의 경우 아래 명령을 실행합니다. `podName`을 이전 단계에서 반환된 서버의 이름으로 바꾸고, `serviceName`을 만든 Kubernetes 서비스의 기본 설정 이름으로 바꾸고, `namespaceName`*을 BDC 클러스터의 이름으로 바꿉니다.

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    AKS 클러스터 실행의 경우 만드는 서비스의 유형이 `LoadBalancer`라는 점을 제외하고 동일한 명령을 실행합니다. 다음은 그 예입니다. 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    AKS에 대해 실행되는 이 명령의 예제는 다음과 같습니다. 여기서 주 복제본을 호스팅하는 Pod는 `master-0`입니다.

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    생성한 Kubernetes 서비스의 IP를 가져옵니다.

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> 다음 명령을 실행하여 위에서 만든 Kubernetes 서비스를 삭제하여 정리하는 것이 좋습니다.
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- 가용성 그룹에 데이터베이스를 추가합니다.

    데이터베이스를 AG에 추가하려면 해당 데이터베이스를 전체 복구 모드에서 실행하고 로그 백업을 수행해야 합니다. 위에서 만든 Kubernetes 서비스의 IP를 사용하여 SQL Server 인스턴스에 연결한 다음, TSQL 문을 아래와 같이 실행합니다.

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    다음 예제에서는 인스턴스에 복원된 `sales`라는 데이터베이스를 추가합니다.

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>알려진 제한 사항

빅 데이터 클러스터의 SQL Server 마스터에 대하여 포함된 가용성 그룹 관련 알려진 문제 및 제한 사항은 다음과 같습니다.

- 빅 데이터 클러스터가 배포될 때 고가용성 구성을 만들어야 합니다. 배포 후에는 가용성 그룹을 사용하여 고가용성 구성을 사용하도록 설정할 수 없습니다. 지금은 동기 커밋 복제본에 대한 구성만 사용하도록 설정됩니다.

> [!WARNING]
> 쿼럼 커밋의 모든 복제본에 대한 비동기 커밋으로 동기화 모드를 업데이트하면 고가용성 구성이 잘못 생성됩니다. 이러한 구성에서 실행하면 실패 이벤트가 주 복제본에 영향을 미칠 때 자동 장애 조치(failover)가 트리거되지 않으므로 데이터 손실의 위험이 있으며, 수동 장애 조치(failover) 사용 시 데이터 손실 위험을 감수해야 합니다.

- 다른 서버에 생성된 백업에서 TDE 사용 데이터베이스를 복원하려면 SQL Server 인스턴스 마스터와 포함된 AG 마스터에서 모두 [필수 인증서](../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)를 복원해야 합니다. 인증서를 백업하고 복원하는 방법에 대한 예제는 [여기](https://www.sqlshack.com/restoring-transparent-data-encryption-tde-enabled-databases-on-a-different-server/)를 참조하세요.
- `sp_configure`를 사용하여 서버 구성 설정을 실행하는 것과 같은 특정 작업을 수행하려면 `master` 가용성 그룹이 아니라 SQL Server 인스턴스 `master` 데이터베이스에 연결해야 합니다. 해당 기본 엔드포인트는 사용할 수 없습니다. [지침](#instance-connect)에 따라 엔드포인트를 공개하고, SQL Server 인스턴스에 연결하고, `sp_configure`를 실행합니다. 엔드포인트를 수동으로 공개하여 SQL Server 인스턴스 `master` 데이터베이스에 연결하는 경우에만 SQL 인증을 사용할 수 있습니다.
- 포함된 msdb 데이터베이스는 가용성 그룹에 포함되어 있고 SQL 에이전트 작업은 두루 복제되지만 일정에 따라서만 주 복제본에서 실행됩니다.
- SQL Server 2019 CU2 이전에는 `CREATE DATABASE` 및 `RESTORE DATABASE`(예: `CREATE DATABASE FROM SNAPSHOT`) 이외의 워크플로 결과로 생성된 데이터베이스가 가용성 그룹에 자동으로 추가되지 않았습니다. [인스턴스에 연결](#instance-connect)하고, 데이터베이스를 가용성 그룹에 수동으로 추가합니다.

## <a name="next-steps"></a>다음 단계

- 빅 데이터 클러스터 배포에서 구성 파일을 사용하는 방법에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md#configfile)을 참조하세요.
- SQL Server의 가용성 그룹 기능에 대한 자세한 내용은 [AlwaysOn 가용성 그룹 개요(SQL Server)](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.
