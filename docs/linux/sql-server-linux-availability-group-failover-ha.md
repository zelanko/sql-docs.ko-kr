---
title: 가용성 그룹 장애 조치-Linux에서 SQL Server 관리 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: ddbe5f25cf3153b3354425fd426798e7061bdf36
ms.sourcegitcommit: 99e355b71ff2554782f6bc8e0da86e6d9e3e0bef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34799813"
---
# <a name="always-on-availability-group-failover-on-linux"></a>Linux에서 always On 가용성 그룹 장애 조치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

가용성 그룹 (AG)의 컨텍스트 내에서 주 역할과 보조 역할의 가용성 복제본은 장애 조치로 알려진 프로세스에서 서로 바꿀 수 있습니다. 자동 장애 조치(데이터가 손실되지 않음), 계획된 수동 장애 조치(데이터가 손실되지 않음)와 *강제 장애 조치(failover)* 라고 불리는 강제 수동 장애 조치(데이터가 손실될 수 있음)의 세 가지 형태가 있습니다. 자동 및 계획 된 수동 장애 조치는 모든 데이터를 보존 합니다. 가용성 복제본의 수준에서 장애 조치 AG 됩니다. 즉, AG 장애 조치 (현재 장애 조치 대상) 보조 복제본 중 하나로 됩니다. 

장애 조치에 대 한 배경 정보를 참조 하십시오. [장애 조치 및 장애 조치 모드](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)합니다.

## <a name="failover"></a>수동 장애 조치

장애 조치는 외부 클러스터 관리자에서 관리 하는 AG 클러스터 관리 도구를 사용 합니다. 예를 들어 Pacemaker를 사용 하 여 Linux 클러스터를 관리 하는 솔루션을 사용 하 여 `pcs` RHEL 또는 Ubuntu에서 수동 장애 조치를 수행할 수 있습니다. SLES에서 사용 하 여 `crm`합니다. 

> [!IMPORTANT]
> 정상 작업에서 장애 조치 하지 마십시오 SSMS 또는 PowerShell과 같은 TRANSACT-SQL 또는 SQL Server 관리 도구를 사용 합니다. 때 `CLUSTER_TYPE = EXTERNAL`만 사용 가능한 값에 대 한 `FAILOVER_MODE` 은 `EXTERNAL`합니다. 이러한 설정을 사용 하 여 모든 수동 또는 자동 장애 조치 작업이 외부 클러스터 관리자에서 실행 됩니다. 데이터 손실 될 가능성이 있는 장애 조치를 강제로 지침은 [강제 장애 조치](#forceFailover)합니다.

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">수동 장애 조치 단계

장애 조치, 보조 복제본은 주 복제본을 동기 복제본 이어야 합니다. 보조 복제본이 비동기 [가용성 모드 변경](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)합니다.

수동 장애 조치 두 단계를 수행에서 합니다.

   첫째,[ AG 리소스 이동를 하나씩 수동으로 장애](#manualMove) 새 노드는 리소스를 소유 하 고 클러스터 노드에서 합니다.

   클러스터 AG 리소스를 장애 조치 되 고 위치 제약 조건을 추가 합니다. 이 제약 조건은 새 노드에서 실행 하는 리소스를 구성 합니다. 성공적으로 장애 조치 이후에 하기 위해이 제약 조건을 제거 합니다.

   두 번째, [위치 제약 조건을 제거](#removeLocConstraint)합니다.

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">1 단계입니다. 가용성 그룹 리소스 이동를 하나씩 수동으로 실패

수동 장애 조치 라는 AG 리소스를 *ag_cluster* 라는 클러스터 노드로 *nodeName2*, 배포에 필요한 적절 한 명령을 실행:

- **RHEL/Ubuntu 예제**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 예제**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>리소스에 대해 수동으로 장애 후 자동으로 추가 된 위치 제약 조건부 터 제거 해야 합니다.

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> 2 단계입니다. 위치 제약 조건 제거

수동 장애 조치 동안는 `pcs` 명령 `move` 또는 `crm` 명령 `migrate` 새 대상 노드에 배치 될 리소스에 대 한 위치 제약 조건을 추가 합니다. 새 제약 조건을 확인하려면 리소스를 수동으로 이동한 후 다음 명령을 실행합니다.

- **RHEL/Ubuntu 예제**

   ```bash
   sudo pcs constraint list --full
   ```

- **SLES 예제**

   ```bash
   crm config show
   ```

수동 장애 조치 때문에 생성 하는 제약 조건의 예입니다. 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

- **RHEL/Ubuntu 예제**

   다음 명령에서 `cli-prefer-ag_cluster-master`는 제거해야 하는 제약 조건의 ID입니다. `sudo pcs constraint list --full`은 이 ID를 반환합니다. 
   
   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
   
- **SLES 예제**

   다음 명령에서 `cli-prefer-ms-ag_cluster` 제약 조건의 ID입니다. `crm config show`은 이 ID를 반환합니다. 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>자동 장애 조치(failover)는 위치 제약 조건을 추가하지 않으므로 정리가 필요하지 않습니다. 

자세한 내용은 다음을 참조하세요.
- [Red Hat - Managing Cluster Resources](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)(Red Hat - 클러스터 리소스 관리)
- [Pacemaker-리소스를 수동으로 이동](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
 [SLES 관리 가이드-리소스](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 
## <a name="forceFailover"></a> 강제 장애 조치 

강제 장애 조치는 재해 복구에 엄격 하 게 사용 됩니다. 이 경우 없습니다 장애 조치 클러스터 관리 도구와 기본 데이터 센터 다운 이므로 합니다. 동기화되지 않은 보조 복제본으로 강제 장애 조치(failover)를 수행하면 데이터 손실이 발생할 수 있습니다. AG에 서비스 즉시 복원 해야 하 고 데이터 손실을 감수할지 하는 경우에 장애 조치를 강제로 합니다.

클러스터 주 데이터 센터에서 재해 이벤트로 인해 응답 하지 않으면 클러스터-예를 들어 상호 작용 하기 위한 클러스터 관리 도구를 사용할 수 없으면, 강제 장애를 외부 클러스터 관리자를 사용 하지 않을 해야 합니다. 데이터가 손실 될 위험이 있으므로 일반 작업을 위해이 절차를 권장 되지 않습니다. 장애 조치 작업을 실행 하는 클러스터 관리 도구에 실패 하는 경우 사용 합니다. 이 절차는 비슷합니다 기능적으로 [강제 수동 장애 조치를 수행](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) Windows의 AG에 있습니다.
 
강제 장애 조치에 대 한이 프로세스는 Linux에서 SQL Server에만.

1. AG 리소스 관리 되지 않도록 클러스터에서 더 이상 확인 합니다. 

      - 대상 클러스터 노드에서 리소스 관리 되지 않는 모드로 설정 합니다. 이 명령은 리소스 에이전트를 중지 리소스 모니터링 및 관리를 알립니다. 예를 들어: 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - 관리 되지 않는 모드로 리소스 모드를 설정 하 고 시도가 실패 하는 경우에 리소스를 삭제 합니다. 예를 들어:

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >리소스를 삭제 하는 경우 또한 삭제 모든 관련된 제약 조건을 합니다. 

1. 보조 복제본을 호스팅하는 SQL Server의 인스턴스에서 세션 컨텍스트 변수 설정 `external_cluster`합니다.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. TRANSACT-SQL과 함께 AG 장애 조치할 합니다. 다음 예제에서는 대체 `<MyAg>` 프로그램 AG의 이름으로 합니다. 대상 보조 복제본을 호스팅하는 SQL Server의 인스턴스에 연결 하 고 다음 명령을 실행 합니다.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  강제 장애 조치 후 클러스터 리소스 모니터링 및 관리를 다시 시작 하거나 AG 리소스를 다시 만들기 전에 정상 상태로 AG 상태로 전환 합니다. 검토는 [강제 장애 조치 후 필수 태스크](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp)합니다.

1.  다시 시작 하거나 클러스터 리소스 모니터링 및 관리:

   클러스터 리소스 모니터링 및 관리를 다시 시작 하려면 다음 명령을 실행 합니다.

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   클러스터 리소스를 삭제 한 경우 다시 만듭니다. 지침에 따라 클러스터 리소스를 다시 만들려면 [가용성 그룹 리소스를 만들](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)합니다.

>[!Important]
>데이터 손실 위험이 때문에 재해 복구 훈련에 대 한 위의 단계를 사용 하지 마십시오. 대신 고 비동기 복제본이 동기, 및에 대 한 지침을 변경할 [일반 수동 장애 조치](#manualFailover)합니다.

## <a name="database-level-monitoring-and-failover-trigger"></a>데이터베이스 수준 모니터링 및 장애 조치 트리거

에 대 한 `CLUSTER_TYPE=EXTERNAL`, 장애 조치 트리거 의미 체계는 다른 WSFC에 비해 합니다. AG wsfc에서 SQL Server의 인스턴스로 설정 하면 아웃의 전환을 `ONLINE` AG 상태는 오류 보고를 사용 하면 데이터베이스에 대 한 상태입니다. 클러스터 관리자에 대 한 응답에서 한 장애 조치 작업을 트리거합니다. Linux에서 SQL Server 인스턴스 클러스터와 통신할 수 없습니다. 데이터베이스 상태 작업 수행에 대 한 모니터링 *간접적인*합니다. 데이터베이스 수준 장애 조치 모니터링 및 장애 조치에 대 한 사용자에 옵트인 하는 경우 (옵션을 설정 하 여 `DB_FAILOVER=ON` AG를 만들 때), 데이터베이스 상태는 클러스터는 확인 `ONLINE` 모니터링 작업을 실행할 때마다 합니다. 클러스터의 상태를 쿼리 `sys.databases`합니다. 다른 모든 상태에 대 한 `ONLINE`, 자동으로 (자동 장애 조치 조건이 충족 될 경우)는 장애 조치를 트리거합니다. 장애 조치의 실제 시간 sys.databases에서 업데이트 되는 데이터베이스 상태 뿐만 아니라 모니터링 작업의 빈도에 따라 달라 집니다.

자동 장애 조치 동기 복제본이 하나 이상 필요합니다.

## <a name="next-steps"></a>다음 단계

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Red Hat Enterprise Linux 클러스터를 구성 합니다.](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 SUSE Linux Enterprise Server 클러스터 구성](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Ubuntu 클러스터 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
