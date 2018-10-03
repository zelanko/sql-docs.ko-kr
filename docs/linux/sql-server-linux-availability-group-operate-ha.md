---
title: Linux의 SQL Server 가용성 그룹을 작동 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: a33c18175a03b589f7b431655ff4704356f5eeaf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796001"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Linux의 가용성 그룹에 대해 항상 작동

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>가용성 그룹 업그레이드

패턴 및 사례에서 가용성 그룹을 업그레이드 하기 전에 검토 [가용성 그룹 복제본 인스턴스 업그레이드](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)합니다.

다음 섹션에서는 가용성 그룹을 사용 하 여 Linux에서 SQL Server 인스턴스를 사용 하 여 롤링 업그레이드를 수행 하는 방법에 설명 합니다. 

### <a name="upgrade-steps-on-linux"></a>Linux에서 업그레이드 단계

가용성 그룹의 클러스터 유형 중 하나는 Linux의 SQL server 인스턴스에서 가용성 그룹 복제본이 되 면 `EXTERNAL` 또는 `NONE`합니다. 이외에 Windows Server 장애 조치 클러스터 (WSFC) 클러스터 관리자에서 관리 되는 가용성 그룹 `EXTERNAL`합니다. Corosync는 pacemaker는 외부 클러스터 관리자의 예시입니다. 클러스터 관리자가 없는 가용성 그룹 클러스터 유형이 `NONE` 여기에 설명 된 업그레이드 단계는 가용성 그룹 클러스터 형식에 대 한 특정 `EXTERNAL` 또는 `NONE`합니다.

인스턴스를 업그레이드 하는 순서에 따라 달라 집니다 경우 해당 역할은 보조 복제본은 동기 또는 비동기 복제본을 호스트 하는 여부 및 합니다. 먼저 비동기 보조 복제본을 호스팅하는 SQL Server의 인스턴스를 업그레이드 합니다. 동기 보조 복제본을 호스팅하는 인스턴스를 업그레이드 합니다. 

   >[!NOTE]
   >가용성 그룹에 있는 비동기 데이터 손실을 방지 하려면 복제본을 동기 복제본이 하나 변경 및 동기화 될 때까지 기다립니다. 이 복제본을 업그레이드 합니다.
   
시작 하기 전에 각 데이터베이스를 백업 합니다.

1. 업그레이드에 대 한 대상 보조 복제본을 호스팅하는 노드의 리소스를 중지 합니다.
   
   업그레이드 명령을 실행 하기 전에 클러스터 모니터링 및 불필요 하 게 실패 하지 것입니다 있도록 리소스를 중지 합니다. 다음 예제에서는 중지 될 리소스를 일으키는 노드에 위치 제약 조건을 추가 합니다. 업데이트 `ag_cluster-master` 리소스 이름 및 `nodeName1` 업그레이드에 대 한 대상 복제본을 호스팅하는 노드를 사용 하 여 합니다.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. 보조 복제본에서 SQL Server를 업그레이드 합니다.

   다음 예제에서는 업그레이드 `mssql-server` 고 `mssql-server-ha` 패키지 있습니다.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. 위치 제약 조건을 제거 합니다.

   업그레이드 명령을 실행 하기 전에 클러스터 모니터링 및 불필요 하 게 실패 하지 것입니다 있도록 리소스를 중지 합니다. 다음 예제에서는 중지 될 리소스를 일으키는 노드에 위치 제약 조건을 추가 합니다. 업데이트 `ag_cluster-master` 리소스 이름 및 `nodeName1` 업그레이드에 대 한 대상 복제본을 호스팅하는 노드를 사용 하 여 합니다.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   모범 사례에 확인 된 리소스가 시작 될 (사용 하 여 `pcs status` 명령) 및 보조 복제본에 연결 되 고 업그레이드 후 상태를 동기화 합니다.

1. 모든 보조 복제본은 업그레이드 후 수동 장애 조치를 동기 보조 복제본 중 하나입니다.

   가용성 그룹에 대 한 `EXTERNAL` 클러스터 유형, 클러스터 관리 도구를 사용 하 여 장애 조치;와 함께 가용성 그룹 `NONE` 클러스터 유형이 TRANSACT-SQL를 사용 하 여 장애 조치 해야 합니다. 
   다음 예제에서는 클러스터 관리 도구를 사용 하 여 가용성 그룹의 장애 실패합니다. 대체 `<targetReplicaName>` 기본 될 동기 보조 복제본의 이름:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >다음 단계는 클러스터 관리자를 갖지 않는 가용성 그룹에만 적용 합니다.

   가용성 그룹 클러스터 유형이 경우 `NONE`수동으로 장애 조치 합니다. 다음 단계를 순서대로 수행하세요.

      1. 다음 명령은 보조 주 복제본을 설정합니다. 대체 `AG1` 가용성 그룹의 이름입니다. 주 복제본을 호스팅하는 SQL Server 인스턴스에서 TRANSACT-SQL 명령을 실행 합니다.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      2. 다음 명령은 주 동기 보조 복제본을 설정합니다. 동기 보조 복제본을 호스팅하는 인스턴스에 SQL Server 대상 인스턴스에서 다음 TRANSACT-SQL 명령을 실행 합니다.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. 장애 조치 후 위의 절차를 반복 하 여 이전 주 복제본에서 SQL Server를 업그레이드 합니다.

   다음 예제에서는 업그레이드 `mssql-server` 고 `mssql-server-ha` 패키지 있습니다.

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

1. 클러스터 유형 인 외부-외부 클러스터 관리자는 가용성 그룹에 대 한 수동 장애 조치 하 여 발생 하는 위치 제약 조건이 정리 합니다. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 새로 업그레이드 된 보조 복제본-이전 주 복제본에 대 한 데이터 이동을 다시 시작 합니다. 이 단계는 더 높은 버전 인스턴스에 SQL server는 가용성 그룹의 낮은 버전 인스턴스에 로그 블록을 전송 하는 경우에 필요 합니다. 새 보조 복제본 (이전의 주 복제본)에서 다음 명령을 실행 합니다.

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

모든 서버를 업그레이드 한 후 하면 다시 장애 복구할 수 있습니다. 필요한 경우 원래 기본으로 다시 장애 조치 합니다. 

## <a name="drop-an-availability-group"></a>가용성 그룹을 삭제

가용성 그룹을 삭제 하려면 [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md)합니다. 클러스터 형식이 `EXTERNAL` 또는 `NONE` 복제본을 호스팅하는 SQL Server의 모든 인스턴스에서 명령을 실행 합니다. 예를 들어 라는 가용성 그룹을 삭제 하려면 `group_name` 다음 명령을 실행 합니다.

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>다음 단계

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Red Hat Enterprise Linux 클러스터를 구성 합니다.](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 SUSE Linux Enterprise Server 클러스터 구성](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Ubuntu 클러스터 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
