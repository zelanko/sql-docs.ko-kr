---
title: "Linux에서 SQL Server 가용성 그룹 동작 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 07/20/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 23eedac40aff1fcab50c2e05406d3c87b988e392
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Linux에서 가용성 그룹에 대해 항상 작동

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

## <a name="failover"></a>가용성 그룹 장애 조치

에 외부 클러스터 관리자에서 관리 하는 가용성 그룹 장애 조치 클러스터 관리 도구를 사용 합니다. 예를 들어 Pacemaker를 사용 하 여 Linux 클러스터를 관리 하는 솔루션을 사용 하 여 `pcs` RHEL 또는 Ubuntu에서 수동 장애 조치를 수행할 수 있습니다. SLES에서 사용 하 여 `crm`합니다. 

> [!IMPORTANT]
> 정상 작업에서 장애 조치 하지 마십시오 SSMS 또는 PowerShell과 같은 TRANSACT-SQL 또는 SQL Server 관리 도구를 사용 합니다. 때 `CLUSTER_TYPE = EXTERNAL`만 사용 가능한 값에 대 한 `FAILOVER_MODE` 은 `EXTERNAL`합니다. 이러한 설정을 사용 하 여 모든 수동 또는 자동 장애 조치 작업이 외부 클러스터 관리자에서 실행 됩니다. 

### <a name="manual-failover-examples"></a>수동 장애 조치 예제

수동으로 외부 클러스터 관리 도구와 함께 가용성 그룹 장애 조치할 합니다. 정상 작업에서 TRANSACT-SQL로 장애 조치를 시작 하지 마십시오. 외부 클러스터 관리 도구, 응답 하지 않는 경우에 가용성 그룹이 장애 조치를 강제로 수 있습니다. 강제 수동 장애 조치를 참조 하십시오 [클러스터 도구 응답 하지 않습니다. 수동 이동](#forceManual)합니다.

두 가지 단계로 수동 장애 조치를 완료 합니다. 

1. 새 노드는 리소스를 소유 하 고 클러스터 노드에서 가용성 그룹 리소스를 이동 합니다.

   클러스터 관리자의 가용성 그룹 리소스가 이동한 위치 제약 조건을 추가 합니다. 이 제약 조건은 새 노드에서 실행 하는 리소스를 구성 합니다. 하거나 수동 또는 자동으로 장애 조치 앞으로 이동 하려면이 제약 조건을 제거 해야 합니다.

2. 위치 제약 조건을 제거 합니다.

#### <a name="1-manually-fail-over"></a>1. 수동 장애 조치

수동 장애 조치 라는 가용성 그룹 리소스를 *ag_cluster* 라는 클러스터 노드로 *nodeName2*, 배포에 필요한 적절 한 명령을 실행:

- **RHEL/Ubuntu 예제**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 예제**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```



>[!IMPORTANT]
>리소스에 대해 수동으로 장애 후 자동으로 이동 하는 동안 추가 된 위치 제약 조건부 터 제거 해야 합니다.

#### <a name="2-remove-the-location-constraint"></a>2. 위치 제약 조건 제거

수동 이동 중의 `pcs` 명령 `move` 또는 `crm` 명령 `migrate` 새 대상 노드에 배치 될 리소스에 대 한 위치 제약 조건을 추가 합니다. 새 제약 조건을 확인하려면 리소스를 수동으로 이동한 후 다음 명령을 실행합니다.

- **RHEL/Ubuntu 예제**

   ```bash
   sudo pcs constraint --full
   ```

- **SLES 예제**

   ```bash
   crm config show
   ```

위치 제약 조건을 제거해야 자동 장애 조치(failover)를 포함한 이후 이동이 성공합니다. 

제약 조건을 제거하려면 다음 명령을 실행합니다. 

- **RHEL/Ubuntu 예제**

   이 예에서 `ag_cluster-master` 이동 된 리소스의 이름입니다. 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **SLES 예제**

   이 예에서 `ag_cluster` 이동 된 리소스의 이름입니다. 

   ```bash
   crm resource clear ag_cluster
   ```

또는 다음 명령을 실행하여 위치 제약 조건을 제거할 수 있습니다.  

- **RHEL/Ubuntu 예제**

   다음 명령에서 `cli-prefer-ag_cluster-master`는 제거해야 하는 제약 조건의 ID입니다. `sudo pcs constraint --full`은 이 ID를 반환합니다. 

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
 

### <a name="forceManual"></a>수동 이동할 때 클러스터 도구 응답 하지 않습니다. 

극단적인 경우 클러스터와의 상호 작용 하기 위한 사용자 클러스터 관리 도구를 사용할 수 없는 경우 (즉, 클러스터 응답 하지 않으면, 클러스터 관리 도구에는 잘못 된 동작이) 사용자-수동으로 장애 조치 해야 할 수는 외부 클러스터 관리자를 무시 합니다. 이 정기적인 작업에 권장 되지 않습니다 및 클러스터는 클러스터 관리 도구를 사용 하 여 장애 조치 작업 실행에 실패 하는 경우 내에서 사용 해야 합니다.

클러스터 관리 도구와 함께 가용성 그룹으로 실패할 수 없는 경우 SQL Server 도구에서 장애 조치 하려면 다음이 단계를 따르십시오.

1. 가용성 그룹 리소스 관리 되지 않도록 클러스터에서 더 이상 확인 합니다. 

      - 리소스를 관리 되지 않는 모드로 설정 하려고 합니다. 이 신호를 리소스 에이전트 리소스 모니터링을 중지 하 고 관리 합니다. 예를 들어 
      
      ```bash
      sudo pcs resource unmanage <**resourceName**>
      ```

      - 관리 되지 않는 모드로 리소스 모드를 설정 하 고 시도가 실패 하는 경우에 리소스를 삭제 합니다. 예를 들어

      ```bash
      sudo pcs resource delete <**resourceName**>
      ```

      >[!NOTE]
      >리소스를 삭제 하는 경우 또한 삭제 모든 관련된 제약 조건을 합니다. 

1. 세션 컨텍스트 변수를 수동으로 설정 `external_cluster`합니다.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. TRANSACT-SQL은 가용성 그룹을 장애 조치할 합니다. 바꾸기 아래 예제에서는 `<**MyAg**>` 가용성 그룹의 이름으로 합니다. 대상 보조 복제본을 호스팅하는 SQL Server의 인스턴스에 연결 하 고 다음 명령을 실행 합니다.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <**MyAg**> FAILOVER;
   ```

1. 클러스터 리소스 모니터링 및 관리를 다시 시작 합니다. 다음 명령을 실행합니다.

   ```bash
   sudo pcs resource manage <**resourceName**>
   sudo pcs resource cleanup <**resourceName**>
   ```

## <a name="database-level-monitoring-and-failover-trigger"></a>데이터베이스 수준 모니터링 및 장애 조치 트리거

에 대 한 `CLUSTER_TYPE=EXTERNAL`, 장애 조치 트리거 의미 체계는 다른 WSFC에 비해 합니다. 가용성 그룹 wsfc에서 SQL Server의 인스턴스로 설정 하면 아웃의 전환을 `ONLINE` 데이터베이스 하면 오류를 보고 하기 위해 가용성 그룹 상태에 대 한 상태입니다. 이 신호를 장애 조치 작업을 트리거하는 클러스터 관리자를 보내는 합니다. Linux에서 SQL Server 인스턴스 클러스터와 통신할 수 없습니다. "외부의" 데이터베이스 상태에 대 한 모니터링이 수행 됩니다. 데이터베이스 수준 장애 조치 모니터링 및 장애 조치에 대 한 사용자에 옵트인 하는 경우 (옵션을 설정 하 여 `DB_FAILOVER=ON` 가용성 그룹을 만들 때), 클러스터 데이터베이스 상태 인지 확인 합니다 `ONLINE` 될 때마다 모니터링 작업을 실행 합니다. 클러스터의 상태를 쿼리 `sys.databases`합니다. 다른 모든 상태에 대 한 `ONLINE`, 자동으로 (자동 장애 조치 조건이 충족 될 경우)는 장애 조치를 트리거합니다. 장애 조치의 실제 시간 sys.databases에서 업데이트 되는 데이터베이스 상태 뿐만 아니라 모니터링 작업의 빈도에 따라 달라 집니다.

## <a name="upgrade-availability-group"></a>가용성 그룹을 업그레이드

가용성 그룹을 업그레이드 하기 전에에서 모범 사례를 검토 [가용성 그룹 복제본 인스턴스 업그레이드](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)합니다.

다음 섹션에서는 Linux에서 가용성 그룹이 포함 된 SQL Server 인스턴스에서 롤링 업그레이드를 수행 하는 방법을 설명 합니다. 

### <a name="upgrade-steps-on-linux"></a>Linux에서 업그레이드 단계

Linux에서 SQL Server의 인스턴스에서 가용성 그룹 복제본을 가용성 그룹의 클러스터 유형 중 하나는 `EXTERNAL` 또는 `NONE`합니다. 이외에 Windows Server 장애 조치 클러스터 (WSFC)는 클러스터 관리자에서 관리 되는 가용성 그룹 `EXTERNAL`합니다. Corosync와 pacemaker는 외부 클러스터 관리자의 예시입니다. 클러스터 관리자가 없습니다 포함 된 가용성 그룹에 클러스터 형식이 `NONE` 여기에 설명 된 업그레이드 단계는 클러스터 유형의 가용성 그룹에 대 한 특정 `EXTERNAL` 또는 `NONE`합니다.

1. 시작 하기 전에 각 데이터베이스를 백업 합니다.
2. 보조 복제본을 호스팅하는 SQL Server의 인스턴스를 업그레이드 합니다.

    a. 비동기 보조 복제본을 먼저 업그레이드 합니다.

    b. 동기 보조 복제본을 업그레이드 합니다.

   >[!NOTE]
   >가용성 그룹에 있는 비동기 데이터 손실을 방지 하기 위해 복제본-하나의 복제본을 동기 변경한 동기화 될 때까지 기다립니다. 이 복제를 업그레이드 합니다.
   
   b.1. 업그레이드에 대 한 대상 보조 복제본을 호스팅하는 노드의에 리소스를 중지 합니다.
   
   업그레이드 명령을 실행 하기 전에 클러스터 모니터링은 되 불필요 하 게 실패 하지 하도록 리소스를 중지 합니다. 다음 예제에서는 중지 될 리소스에 취소할 수 있는 노드의 위치 제약 조건을 추가 합니다. 업데이트 `ag_cluster-master` 리소스 이름으로 및 `nodeName1` 노드를 복제본을 호스팅하는 업그레이드에 대 한 대상으로 합니다.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```
   b.2. 보조 복제본에서 SQL Server 업그레이드

   다음 예제에서는 업그레이드 `mssql-server` 및 `mssql-server-ha` 패키지 합니다.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   b.3. 위치 제약 조건 제거

   업그레이드 명령을 실행 하기 전에 클러스터 모니터링은 되 불필요 하 게 실패 하지 하도록 리소스를 중지 합니다. 다음 예제에서는 중지 될 리소스에 취소할 수 있는 노드의 위치 제약 조건을 추가 합니다. 업데이트 `ag_cluster-master` 리소스 이름으로 및 `nodeName1` 노드를 복제본을 호스팅하는 업그레이드에 대 한 대상으로 합니다.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   모범 사례로, 리소스에서 시작 되었는지 확인 하십시오 (사용 하 여 `pcs status` 명령) 보조 복제본 연결 되어 있으며 업그레이드 후 상태를 동기화 하 고 있습니다.

1. 보조 복제본을 모두를 업그레이드 한 후 수동 장애 조치를 동기 보조 복제본 중 하나입니다.

   인 가용성 그룹에 대 한 `EXTERNAL` 형식 클러스터, 클러스터 관리 도구를 사용 하 여 장애 조치; 인 가용성 그룹 `NONE` 클러스터 유형 TRANSACT-SQL을 사용 하 여 장애 조치 해야 합니다. 
   다음 예제에서는 클러스터 관리 도구를 사용 하는 가용성 그룹을 통해 실패합니다. 대체 `<targetReplicaName>` 주 역할을 할 때 동기 보조 복제본의 이름으로:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >다음 단계는 클러스터 관리자를 갖지 않는 가용성 그룹에만 적용 합니다.  
   가용성 그룹 클러스터 유형이 `NONE`수동으로 장애 조치 합니다. 다음 단계를 순서대로 수행하세요.

      a. 다음 명령은 보조를 주 복제본을 설정합니다. 대체 `AG1` 가용성 그룹의 이름으로 합니다. 주 복제본을 호스팅하는 SQL Server의 인스턴스에 TRANSACT-SQL 명령을 실행 합니다.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. 다음 명령은 기본 동기 보조 복제본으로 설정 합니다. 대상 인스턴스의 SQL Server-동기 보조 복제본을 호스팅하는 인스턴스에 다음 TRANSACT-SQL 명령을 실행 합니다.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. 장애 조치 후 이전 주 복제본에서 SQL Server b.1 b.3 위의 단계에서 설명한 동일한 절차를 반복 하 여 업그레이드 합니다.

   다음 예제에서는 업그레이드 `mssql-server` 및 `mssql-server-ha` 패키지 합니다.

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. 외부 클러스터와는 가용성 그룹에 대 한 관리자-클러스터 입력할 수 있는 EXTERNAL, 정리 수동 장애 조치에 의해 발생 한 위치 제약 조건입니다. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 새로 업그레이드 된 보조 복제본-이전 주 복제본에 대 한 데이터 이동을 다시 시작 합니다. 이 가용성 그룹에서 더 낮은 버전 인스턴스를 더 높은 버전 인스턴스에 SQL Server의 로그 블록을 전송 하는 경우에 필요 합니다. 새로운 보조 복제본 (이전의 주 복제본)에서 다음 명령을 실행 합니다.

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

-장애 복구를 할 수 있습니다 모든 서버를 업그레이드 한 후 다시 장애 조치 원본 주-필요한 경우. 

## <a name="drop-an-availability-group"></a>가용성 그룹 삭제

가용성 그룹을 삭제 하려면 실행 [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md)합니다. 클러스터 형식이 `EXTERNAL` 또는 `NONE` 복제본을 호스팅하는 SQL Server의 모든 인스턴스에서 명령을 실행 합니다. 예를 들어 라는 가용성 그룹을 삭제 하려면 `group_name` 다음 명령을 실행 합니다.

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>다음 단계

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Red Hat Enterprise Linux 클러스터를 구성 합니다.](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 SUSE Linux Enterprise Server 클러스터 구성](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Ubuntu 클러스터 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
