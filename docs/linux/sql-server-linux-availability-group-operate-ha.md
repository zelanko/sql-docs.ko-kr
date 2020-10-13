---
title: 가용성 그룹 SQL Server on Linux 작동
description: 이 문서에서는 가용성 그룹을 사용하여 Linux에서 SQL Server 인스턴스를 통해 롤링 업그레이드를 수행하는 방법을 설명합니다. 업그레이드에 앞서 모범 사례를 검토하세요.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: a95d3e53f5ca2b15e0cccf87bd267258e2f4baab
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784755"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Linux에서 Always On 가용성 그룹 작동

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

## <a name="upgrade-availability-group"></a>가용성 그룹 업그레이드

가용성 그룹을 업그레이드하기 전에 [가용성 그룹 복제본 인스턴스 업그레이드](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)에서 패턴 및 사례를 검토하세요.

다음 섹션에서는 가용성 그룹을 사용하여 Linux에서 SQL Server 인스턴스로 롤링 업그레이드를 수행하는 방법을 설명합니다. 

### <a name="upgrade-steps-on-linux"></a>Linux의 업그레이드 단계

가용성 그룹 복제본이 Linux의 SQL Server 인스턴스에 있는 경우 가용성 그룹의 클러스터 유형은 `EXTERNAL` 또는 `NONE`입니다. WSFC(Windows Server 장애 조치(failover) 클러스터) 외에 클러스터 관리자가 관리하는 가용성 그룹은 `EXTERNAL`입니다. Corosync가 있는 Pacemaker는 외부 클러스터 관리자의 예입니다. 클러스터 관리자가 없는 가용성 그룹의 클러스터 유형은 `NONE`입니다. 여기에 설명된 업그레이드 단계는 클러스터 유형 `EXTERNAL` 또는 `NONE`의 가용성 그룹에 해당합니다.

인스턴스를 업그레이드하는 순서는 해당 역할이 보조인지 여부 및 동기 또는 비동기 복제본을 호스트하는지 여부에 따라 달라집니다. 비동기 보조 복제본을 호스트하는 SQL Server의 인스턴스를 먼저 업그레이드합니다. 그런 다음, 동기 보조 복제본을 호스트하는 인스턴스를 업그레이드합니다. 

   >[!NOTE]
   >가용성 그룹에 비동기 복제본만 있는 경우 데이터 손실을 방지하려면 하나의 복제본을 동기로 변경하고 동기화될 때까지 대기합니다. 그런 다음, 이 복제본을 업그레이드합니다.
   
시작하기 전에 각 데이터베이스를 백업합니다.

1. 업그레이드 대상으로 지정된 보조 복제본을 호스트하는 노드에서 리소스를 중지합니다.
   
   업그레이드 명령을 실행하기 전에 클러스터에서 모니터링하고 불필요하게 장애 조치(failover)하지 않도록 리소스를 중지합니다. 다음 예제에서는 리소스를 중지하게 될 노드에 대한 위치 제약 조건을 추가합니다. 리소스 이름으로 `ag_cluster-master`를 업데이트하고 업그레이드 대상으로 지정된 복제본을 호스트하는 노드로 `nodeName1`을 업데이트합니다.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. 보조 복제본에서 SQL Server를 업그레이드합니다.

   다음 예제에서는 `mssql-server` 및 `mssql-server-ha` 패키지를 업그레이드합니다.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. 위치 제약 조건을 제거합니다.

   업그레이드 명령을 실행하기 전에 클러스터에서 모니터링하고 불필요하게 장애 조치(failover)하지 않도록 리소스를 중지합니다. 다음 예제에서는 리소스를 중지하게 될 노드에 대한 위치 제약 조건을 추가합니다. 리소스 이름으로 `ag_cluster-master`를 업데이트하고 업그레이드 대상으로 지정된 복제본을 호스트하는 노드로 `nodeName1`을 업데이트합니다.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   리소스가 시작되고(`pcs status` 명령 사용) 보조 복제본이 업그레이드 후에 연결되고 동기화된 상태인지 확인하는 것이 가장 좋습니다.

1. 모든 보조 복제본이 업그레이드된 후 동기 보조 복제본 중 하나로 수동으로 장애 조치(failover)합니다.

   클러스터 유형이 `EXTERNAL`인 가용성 그룹의 경우 클러스터 관리 도구를 사용하여 장애 조치(failover)합니다. 클러스터 유형이 `NONE`인 가용성 그룹은 Transact-SQL을 사용하여 장애 조치(failover)합니다. 
   다음 예제에서는 클러스터 관리 도구를 사용하여 가용성 그룹을 장애 조치(failover)합니다. `<targetReplicaName>`을 주 복제본이 될 동기 보조 복제본의 이름으로 바꿉니다.

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >다음 단계는 클러스터 관리자가 없는 가용성 그룹에만 적용됩니다.

   가용성 그룹 클러스터 유형이 `NONE`이면 수동으로 장애 조치(failover)합니다. 다음 단계를 순서대로 수행하세요.

      a. 다음 명령은 주 복제본을 보조 복제본으로 설정합니다. `AG1`을 가용성 그룹의 이름으로 바꿉니다. 주 복제본을 호스트하는 SQL Server 인스턴스에서 Transact-SQL 명령을 실행합니다.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. 다음 명령은 동기 보조 복제본을 주 복제본으로 설정합니다. SQL Server의 대상 인스턴스(동기 보조 복제본을 호스트하는 인스턴스)에서 다음 Transact-SQL 명령을 실행합니다.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. 장애 조치(failover)한 후 이전 절차를 반복하여 이전 주 복제본에서 SQL Server를 업그레이드합니다.

   다음 예제에서는 `mssql-server` 및 `mssql-server-ha` 패키지를 업그레이드합니다.

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

1. EXTERNAL 클러스터 유형을 사용하는 외부 클러스터 관리자가 있는 가용성 그룹의 경우 수동 장애 조치(failover)로 인해 발생한 위치 제약 조건을 정리합니다. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 새로 업그레이드된 보조 복제본(이전 주 복제본)에 대해 데이터 이동을 다시 시작합니다. 이 단계는 SQL Server의 상위 버전 인스턴스가 로그 블록을 가용성 그룹의 하위 버전 인스턴스로 전송할 때 필요합니다. 새 보조 복제본(이전 주 복제본)에서 다음 명령을 실행합니다.

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

모든 서버를 업그레이드한 후 장애 복구(failback)할 수 있습니다. 필요한 경우 다시 원래 주 복제본으로 장애 조치(failover)합니다. 

## <a name="drop-an-availability-group"></a>가용성 그룹 삭제

가용성 그룹 사용을 삭제하려면 [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md)을 실행합니다. 클러스터 유형이 `EXTERNAL` 또는 `NONE`이면 복제본을 호스트하는 SQL Server의 모든 인스턴스에서 명령을 실행합니다. 예를 들어 `group_name`이라는 가용성 그룹을 삭제하려면 다음 명령을 실행합니다.

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>다음 단계

[SQL Server 가용성 그룹 클러스터 리소스에 대해 Red Hat Enterprise Linux 클러스터 구성](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대해 SUSE Linux Enterprise Server 클러스터 구성](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대해 Ubuntu 클러스터 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
