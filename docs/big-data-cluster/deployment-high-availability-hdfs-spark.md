---
title: 고가용성으로 HDFS 또는 Spark 배포
titleSuffix: SQL Server Big Data Clusters
description: 고가용성을 사용하여 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 688031d9301710ada0ba5952ab45dba02bf46de0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774535"
---
# <a name="deploy-hdfs-name-node-and-shared-spark-services-in-a-highly-available-configuration"></a>HDFS 이름 노드 및 공유 Spark 서비스를 고가용성 구성으로 배포

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

고가용성 그룹을 사용하여 SQL Server 마스터 인스턴스를 고가용성 구성으로 배포하는 것 외에도 빅 데이터 클러스터에 여타 중요 업무용 서비스를 배포하여 안정성 수준을 높일 수 있습니다. `sparkhead` 아래에 그룹화된 공유 Spark 서비스와 `HDFS name node`를 추가 복제본으로 구성할 수 있습니다. 이때 빅 데이터 클러스터에 다음 서비스를 위한 클러스터 코디네이터 및 메타데이터 저장소로 사용될 `Zookeeper`도 배포됩니다. 

- HDFS 이름 노드
- Livy 및 Yarn Resource Manager. 

Spark 기록, 작업 기록 및 Hive 메타데이터 서비스는 상태 비저장 서비스입니다. Zookeeper는 이러한 구성 요소의 서비스 상태를 유지하는 데 관여하지 않습니다. 

위와 같은 서비스에 대한 복제본을 여러 개 배포하면 확장성, 안정성, 그리고 사용 가능한 복제본 사이의 워크로드 부하 분산이 향상됩니다.

> [!NOTE]
> 다음 서비스는 `sparkhead` pod에서 컨테이너로 배포됩니다. 
> - Livy
> - Yarn Resource Manager
> - Spark 기록
> - 작업 기록
> - Hive 메타데이터 서비스  
>

다음 이미지는 SQL Server 빅 데이터 클러스터의 Spark HA 배포를 보여 줍니다.

:::image type="content" source="media/deployment-high-availability-hdfs-spark/spark-ha.png" alt-text="spark-ha-bdc":::

다음 이미지는 SQL Server 빅 데이터 클러스터의 HDFS HA 배포를 보여 줍니다.

:::image type="content" source="media/deployment-high-availability-hdfs-spark/hdfs-ha.png" alt-text="hdfs-ha-bdc":::

## <a name="deploy"></a>배포

두 복제본이 이름 노드와 spark head 중 어느 것으로도 구성되지 않은 경우, 복제본 3개를 사용하여 Zookeeper 리소스를 구성해야 합니다. HDFS 이름 노드의 고가용성 구성에서는 2개의 pod `nmnode-0`과 `nmnode-1`이 2개의 복제본을 호스트합니다. 이 구성은 활성-수동입니다. 이름 노드 중 한 번에 하나만 활성 상태입니다. 다른 하나는 대기 상태이며, 장애 조치(failover) 이벤트가 발생할 경우 그 결과 활성 상태가 됩니다. 

기본 제공되는 `aks-dev-test-ha` 또는 `kubeadm-prod` 구성 프로필을 사용하여 빅 데이터 클러스터 배포의 사용자 지정을 시작할 수 있습니다. 프로필에는 추가 고가용성을 구성할 수 있는 리소스에 필요한 설정이 포함됩니다. 예를 들어, 다음은 HDFS 이름 노드, Zookeeper 및 공유 Spark 리소스(`sparkhead`)를 고가용성으로 배포하는 것과 관련된 `bdc.json` 구성 파일의 한 섹션입니다.  

```json
{
  ...
    "nmnode-0": {
        "spec": {
            "replicas": 2
        }
    },
    "sparkhead": {
        "spec": {
            "replicas": 2
        }
    },
    "zookeeper": {
        "spec": {
            "replicas": 3
        }
    },
  ...
}
```

프로덕션 배포에서는 HDFS 블록 복제를 3으로 구성하는 것이 가장 좋습니다. 이 설정은 `aks-dev-test-ha` 및 `kubeadm-prod` 프로필에 이미 지정되어 있습니다. 아래에서 `bdc.json` 구성 파일의 섹션을 살펴보세요.

```json
{
  ...
  "hdfs": {
      "resources": [
          "nmnode-0",
          "zookeeper",
          "storage-0",
          "sparkhead"
      ],
      "settings": {
          "hdfs-site.dfs.replication": "3"
      }
  },
  ...
}
```

## <a name="known-limitations"></a>알려진 제한 사항

SQL Server 빅 데이터 클러스터에서 Hadoop 서비스를 고가용성으로 구성하는 것과 관련하여 알려진 문제와 제한 사항은 다음과 같습니다.

- 모든 구성이 빅 데이터 클러스터 배포 시점에 지정되어야 합니다. SQL Server 2019 CU1 릴리스의 경우 배포 후에는 고가용성 구성을 사용하도록 설정할 수 없습니다.

## <a name="next-steps"></a>다음 단계

- 빅 데이터 클러스터 배포에서 구성 파일을 사용하는 방법에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md#configfile)을 참조하세요.
- 빅 데이터 클러스터의 SQL Server 마스터 고가용성 옵션에 대한 자세한 내용은 [SQL Server 마스터 인스턴스를 고가용성으로 배포](deployment-high-availability.md) 항목을 참조하세요.
