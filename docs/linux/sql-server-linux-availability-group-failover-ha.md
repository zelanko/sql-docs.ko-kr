---
title: 가용성 그룹 장애 조치(failover) 관리 - SQL Server on Linux
description: 이 문서에서는 자동 장애 조치(failover), 계획된 수동 장애 조치 및 강제 수동 장애 조치와 같은 장애 조치 유형에 대해 설명합니다. 자동 장애 조치와 계획된 수동 장애 조치에서는 모든 데이터가 보존됩니다.
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 60dbfed32581a7646da590004c839fc7cf3d316f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892299"
---
# <a name="always-on-availability-group-failover-on-linux"></a>Linux의 Always On 가용성 그룹 장애 조치(failover)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

AG(가용성 그룹)의 컨텍스트 내에서는 일반적으로 가용성 복제본의 주 역할과 보조 역할을 장애 조치(failover)라는 프로세스에서 서로 바꿀 수 있습니다. 자동 장애 조치(데이터가 손실되지 않음), 계획된 수동 장애 조치(데이터가 손실되지 않음)와 *강제 장애 조치(failover)* 라고 불리는 강제 수동 장애 조치(데이터가 손실될 수 있음)의 세 가지 형태가 있습니다. 자동 및 계획된 수동 장애 조치는 모든 데이터를 보존합니다. AG는 가용성 복제본의 수준에서 장애 조치됩니다. 즉, AG는 해당 보조 복제본 중 하나(현재 장애 조치(failover) 대상)로 장애 조치(failover)됩니다. 

장애 조치(failover)에 대한 배경 정보는 [장애 조치(failover) 및 장애 조치(failover) 모드](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)를 참조하세요.

## <a name="manual-failover"></a><a name="failover"></a> 수동 장애 조치(failover)

클러스터 관리 도구를 사용하여 외부 클러스터 관리자가 관리하는 AG를 장애 조치(failover)합니다. 예를 들어 솔루션에서 Pacemaker를 사용하여 Linux 클러스터를 관리하는 경우 `pcs`를 사용하여 RHEL 또는 Ubuntu에서 수동 장애 조치(failover)를 수행합니다. SLES에서는 `crm`을 사용합니다. 

> [!IMPORTANT]
> 정상적으로 작동하는 경우 Transact-SQL 또는 SQL Server 관리 도구(예: SSMS 또는 PowerShell)를 사용하여 장애 조치(failover)하지 마세요. `CLUSTER_TYPE = EXTERNAL`인 경우 `FAILOVER_MODE`의 허용되는 값은 `EXTERNAL`뿐입니다. 이 설정을 사용하면 모든 수동 또는 자동 장애 조치(failover) 작업이 외부 클러스터 관리자에 의해 실행됩니다. 데이터가 손실될 가능성에 대해 강제 장애 조치(failover)를 수행하기 위한 지침은 [강제 장애 조치(failover)](#forceFailover)를 참조하세요.

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">수동 장애 조치(failover) 단계

장애 조치하려면 주 복제본이 될 보조 복제본이 동기 상태여야 합니다. 보조 복제본이 비동기 상태인 경우에는 [가용성 모드를 변경](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)합니다.

두 단계로 수동 장애 조치(failover)합니다.

   먼저, 리소스를 소유하는 클러스터 노드에서 새 노드로 [AG 리소스를 이동하여 수동으로 장애 조치(failover)](#manualMove)합니다.

   클러스터가 AG 리소스를 장애 조치(failover)하고 위치 제약 조건을 추가합니다. 이 제약 조건은 새 노드에서 실행할 리소스를 구성합니다. 나중에 제대로 장애 조치하기 위해 이 제약 조건을 제거합니다.

   두 번째로, [위치 제약 조건을 제거](#removeLocConstraint)합니다.

#### <a name="step-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove"></a> 1단계. 가용성 그룹 리소스를 이동하여 수동으로 장애 조치(failover)

*ag_cluster*라는 AG 리소스를 *nodeName2*라는 클러스터 노드로 수동으로 장애 조치(failover)하려면 사용 중인 배포에 해당하는 명령을 실행합니다.

- **RHEL/Ubuntu 예제**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 예제**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>리소스를 수동으로 장애 조치(failover)한 후 자동으로 추가되는 위치 제약 조건을 제거해야 합니다.

#### <a name="step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> </a> 2단계. 위치 제약 조건 제거

수동으로 장애 조치(failover)하는 동안 `pcs` 명령 `move` 또는 `crm` 명령 `migrate`는 새 대상 노드에 배치될 리소스에 대한 위치 제약 조건을 추가합니다. 새 제약 조건을 확인하려면 리소스를 수동으로 이동한 후 다음 명령을 실행합니다.

- **RHEL/Ubuntu 예제**

   ```bash
   sudo pcs constraint list --full
   ```

- **SLES 예제**

   ```bash
   crm config show
   ```

수동 장애 조치(failover)로 인해 생성되는 제약 조건의 예입니다. 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

   > [!NOTE]
   > Red Hat Enterprise Linux 8.x 및 Ubuntu 18.04에서 Pacemaker 클러스터의 AG 리소스 이름은 리소스 관련 명명법이 승격 가능한 복제를 사용하도록 진화하고 있으므로 *ag_cluster-clone*과 비슷할 수 있습니다. 

- **RHEL/Ubuntu 예제**

   다음 명령에서 `cli-prefer-ag_cluster-master`는 제거해야 하는 제약 조건의 ID입니다. `sudo pcs constraint list --full`은 이 ID를 반환합니다. 
   
   ```bash
   sudo pcs resource clear ag_cluster-master  
   ```
   또는
   
   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
  
   다음과 같이 한 줄에서 자동 생성된 제약 조건의 이동 및 삭제를 모두 수행할 수 있습니다. 다음 예제에서는 Red Hat Enterprise Linux 8.x에 따라 복제라는 용어를 사용합니다. 
  
   ```bash
   sudo pcs resource move ag_cluster-clone --master nodeName2 && sleep 30 && sudo pcs resource clear ag_cluster-clone

   ```
  
- **SLES 예제**

   다음 명령에서 `cli-prefer-ms-ag_cluster`는 제약 조건의 ID입니다. `crm config show`은 이 ID를 반환합니다. 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>자동 장애 조치(failover)는 위치 제약 조건을 추가하지 않으므로 정리가 필요하지 않습니다. 

자세한 내용은 다음을 참조하세요.
- [Red Hat - Managing Cluster Resources](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)(Red Hat - 클러스터 리소스 관리)
- [Pacemaker - Move Resources Manually](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/_move_resources_manually.html)(Pacemaker - 수동으로 리소스 이동)
 [SLES Administration Guide - Resources](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource)(SLES 관리 가이드 - 리소스) 
 
## <a name="force-failover"></a><a name="forceFailover"></a> 강제 장애 조치(failover) 

강제 장애 조치(failover)는 재해 복구에만 사용됩니다. 이 경우 주 데이터 센터의 작동이 중단되기 때문에 클러스터 관리 도구를 사용하여 장애 조치(failover)할 수 없습니다. 동기화되지 않은 보조 복제본으로 강제 장애 조치(failover)를 수행하면 데이터 손실이 발생할 수 있습니다. 데이터 손실을 감수하더라도 즉시 AG로 서비스를 복원해야 하는 경우에만 강제로 장애 조치(failover)합니다.

클러스터와 상호 작용하는 데 클러스터 관리 도구를 사용할 수 없는 경우(예: 주 데이터 센터에 재해가 발생하여 클러스터가 응답하지 않는 경우)에는 외부 클러스터 관리자를 무시하기 위해 강제로 장애 조치(failover)해야 할 수 있습니다. 데이터가 손실될 위험이 있으므로 이 절차는 정상적인 운영 시에는 권장되지 않습니다. 이 절차는 클러스터 관리 도구가 장애 조치(failover) 작업을 실행하지 못할 때 사용합니다. 기능적으로 이 절차는 Windows의 AG에서 [강제 수동 장애 조치(failover)를 수행](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)하는 것과 유사합니다.
 
이 강제 장애 조치(failover) 프로세스는 SQL Server on Linux에만 적용됩니다.

1. AG 리소스가 더 이상 클러스터에서 관리되지 않는지 확인합니다. 

      - 대상 클러스터 노드에서 리소스를 비관리형 모드로 설정합니다. 이 명령은 리소스 모니터링 및 관리를 중지하도록 리소스 에이전트에 신호를 보냅니다. 예를 들면 다음과 같습니다. 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - 리소스 모드를 비관리리형 모드로 설정하지 못하는 경우에는 리소스를 삭제합니다. 예를 들면 다음과 같습니다.

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >리소스를 삭제하면 연결된 모든 제약 조건도 삭제됩니다. 

1. 보조 복제본을 호스트하는 SQL Server 인스턴스에서 세션 컨텍스트 변수 `external_cluster`를 설정합니다.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Transact-SQL을 사용하여 AG를 장애 조치(failover)합니다. 다음 예제에서 `<MyAg>`를 AG 이름으로 바꿉니다. 대상 보조 복제본을 호스트하는 SQL Server 인스턴스에 연결하고 다음 명령을 실행합니다.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  강제 장애 조치(failover) 후에는 클러스터 리소스 모니터링 및 관리를 다시 시작하거나 AG 리소스를 다시 만들기 전에 AG를 정상 상태로 전환합니다. [강제 장애 조치(failover) 후 필수 작업](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp)을 검토하세요.

1.  클러스터 리소스 모니터링 및 관리를 다시 시작합니다.

   클러스터 리소스 모니터링 및 관리를 다시 시작하려면 다음 명령을 실행합니다.

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   클러스터 리소스를 삭제한 경우 다시 만듭니다. 클러스터 리소스를 다시 만들려면 [가용성 그룹 리소스 만들기](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)의 지침을 따릅니다.

>[!Important]
>데이터가 손실될 위험이 있으므로 재해 복구 연습에는 앞의 단계를 사용하지 마세요. 대신, 비동기 복제본을 동기로 변경하고 [일반적인 수동 장애 조치(failover)](#manualFailover)의 지침을 따릅니다.

## <a name="database-level-monitoring-and-failover-trigger"></a>데이터베이스 수준 모니터링 및 장애 조치(failover) 트리거

`CLUSTER_TYPE=EXTERNAL`의 경우 장애 조치(failover) 트리거 의미 체계는 WSFC와 다릅니다. AG가 WSFC의 SQL Server 인스턴스에 있는 경우 데이터베이스의 `ONLINE` 상태에서 전환하면 AG 상태에서 오류가 보고됩니다. 이에 대한 응답으로 클러스터 관리자가 장애 조치(failover) 작업을 트리거합니다. Linux에서 SQL Server 인스턴스는 클러스터와 통신할 수 없습니다. 데이터베이스 상태 모니터링은 ‘외부에서’ 수행됩니다. 사용자가 AG를 만들 때 `DB_FAILOVER=ON` 옵션을 설정하여 데이터베이스 수준 장애 조치(failover) 모니터링 및 장애 조치(failover)를 설정한 경우 클러스터는 모니터링 작업을 실행할 때마다 데이터베이스 상태가 `ONLINE`인지 확인합니다. 클러스터는 `sys.databases`에서 상태를 쿼리합니다. 상태가 `ONLINE`과 다른 경우에는 자동으로 장애 조치(failover)를 트리거합니다(자동 장애 조치(failover) 조건이 충족되는 경우). 실제 장애 조치(failover) 시간은 sys.databases에서 업데이트되는 데이터베이스 상태뿐 아니라 모니터링 작업 빈도에 따라 달라집니다.

자동 장애 조치(failover)에는 하나 이상의 동기 복제본이 필요합니다.

## <a name="next-steps"></a>다음 단계

[SQL Server 가용성 그룹 클러스터 리소스에 대해 Red Hat Enterprise Linux 클러스터 구성](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대해 SUSE Linux Enterprise Server 클러스터 구성](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대해 Ubuntu 클러스터 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
