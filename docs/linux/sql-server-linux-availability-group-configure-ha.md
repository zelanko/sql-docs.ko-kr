---
title: 구성 SQL Server Always On 가용성 그룹 Linux에서 고가용성을 위해
titleSuffix: SQL Server
description: SQL Server 항상에서 AG (가용성 그룹) 고가용성을 위해 Linux에서 만들기에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e339d83503c8fa1f5cdd383004fa93d41529d12d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713432"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>구성 SQL Server Always On 가용성 그룹 Linux에서 고가용성을 위해

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서는 SQL Server 항상에서 AG (가용성 그룹) 고가용성을 위해 Linux에서 만드는 방법을 설명 합니다. Ag에 대 한 두 구성 종류가 있습니다. A *고가용성* 구성 클러스터 관리자를 사용 하 여 비즈니스 연속성을 제공 합니다. 이 구성에서 읽기-배율 복제본을 포함할 수도 있습니다. 이 문서에서는 고가용성에 대 한 AG를 만드는 방법을 설명 합니다.

만들 수도 있습니다 클러스터 없이 AG에 대 한 관리자 *읽기-배율*합니다. 읽기 배율에 대 한 AG 성능 확장에 대 한 읽기 전용 복제본을 제공합니다. 고가용성을 제공 하지는 않습니다. 읽기-배율에 대 한 AG를 만들려면 참조 [Linux에서 읽기-배율에 대 한 SQL Server 가용성 그룹 구성](sql-server-linux-availability-group-configure-rs.md)합니다.

높은 가용성 및 데이터 보호를 보장 하는 구성 2 개 또는 세 개의 동기 커밋 복제본 필요 합니다. 동기 복제본 3 개 이상의 서버를 사용할 수 없는 경우에 AG 복구할 자동으로 수 있습니다. 자세한 내용은 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다. 

모든 서버는 물리적 이거나 가상 해야 하며 가상 서버는 동일한 가상화 플랫폼에 있어야 합니다. 이 요구 사항은 펜싱 에이전트 플랫폼 특정 하기 때문입니다. 참조 [게스트 클러스터에 대 한 정책을](https://access.redhat.com/articles/29440#guest_policies)합니다.

## <a name="roadmap"></a>로드맵

고가용성을 위해 Linux 서버에서 AG를 만드는 단계는 Windows Server 장애 조치 클러스터에 대 한 단계와 다릅니다. 다음과 같은 단계를 간략히 설명 합니다. 

1. [세 가지 클러스터 서버에서 SQL Server 구성](sql-server-linux-setup.md)합니다.

   >[!IMPORTANT]
   >AG의 모든 세 서버 고가용성 Linux 펜스 에이전트를 사용 하 여 서버에서 리소스를 격리할 수 있으므로 물리적 또는 가상 동일한 플랫폼에서 되도록 해야 합니다. 펜싱 에이전트는 각 플랫폼에 대 한 특정입니다.

2. AG를 만듭니다. 이 단계는 현재이 문서에서 다룹니다. 

3. Pacemaker와 같은 클러스터 리소스 관리자를 구성 합니다.
   
   클러스터 리소스 관리자를 구성 하는 방법은 특정 Linux 배포에 따라 달라 집니다. 자세한 배포 지침은 다음 링크를 참조 하세요. 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >프로덕션 환경에 같은 고가용성에 대 한 STONITH는 펜싱 에이전트가 필요합니다. 이 문서의 데모는 펜싱 에이전트를 사용 하지 마세요. 데모 테스트 및 유효성 검사에만 됩니다. 
   
   >Linux 클러스터는 클러스터를 알려진된 상태로 반환할 펜싱을 사용 합니다. 펜스를 구성 하는 방법은 배포 및 환경에 따라 달라 집니다. 현재 펜스는 일부 클라우드 환경에서 사용할 수 없습니다. 자세한 내용은 [RHEL 높은 가용성 클러스터-가상화 플랫폼에 대 한 지원 정책을](https://access.redhat.com/articles/29440)합니다.
   
   >SLES를 참조 하세요 [SUSE Linux Enterprise 높은 가용성 확장](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)합니다.

5. AG를 클러스터 리소스로 추가 합니다.  

   AG를 클러스터 리소스로 추가 하는 방법은 Linux 배포판에 따라 달라 집니다. 자세한 배포 지침은 다음 링크를 참조 하세요. 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>AG 만들기

이 섹션의 예에서는 TRANSACT-SQL을 사용 하 여 가용성 그룹을 만드는 방법을 설명 합니다. SQL Server Management Studio 가용성 그룹 마법사를 사용할 수도 있습니다. 마법사를 사용 하 여 AG를 만들 때 AG에 복제본을 조인 하는 경우 오류가 반환 됩니다. 이 문제를 해결 하려면 권한을 부여 `ALTER`, `CONTROL`, 및 `VIEW DEFINITIONS` 모든 복제본에서 AG에서 pacemaker를 합니다. 주 복제본에서 권한을 부여 되 면 마법사를 통해 하지만 제대로 작동 하려면 모든 복제본에 대 한 권한 부여 HA에 대 한 AG에 노드를 연결 합니다.

자동 장애 조치를 보장 하는 고가용성 구성에 대 한 AG에 3 개 이상의 복제본에 필요 합니다. 고가용성을 지원할 수 있습니다 다음 구성 중 하나:

- [세 개의 동기 복제본](sql-server-linux-availability-group-ha.md#threeSynch)

- [두 개의 동기 복제본 plus 구성 복제본](sql-server-linux-availability-group-ha.md#twoSynch)

정보를 참조 하세요 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다.

>[!NOTE]
>가용성 그룹 추가 동기 또는 비동기 복제본을 포함할 수 있습니다. 

Linux에서 고가용성에 대 한 AG를 만듭니다. 사용 된 [CREATE AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql) 사용 하 여 `CLUSTER_TYPE = EXTERNAL`입니다. 

* 가용성 그룹- `CLUSTER_TYPE = EXTERNAL` AG를 관리 하는 외부 클러스터 엔터티를 지정 합니다. Pacemaker는 클러스터 외부 엔터티의 예시입니다. 클러스터 유형 AG는 외부 

* 주 복제본과 보조 복제본 설정 `FAILOVER_MODE = EXTERNAL`합니다. 
   Pacemaker와 같은 외부 클러스터 관리자를 사용 하 여 복제본 상호 작용 한다고 지정 합니다. 

다음 TRANSACT-SQL 스크립트 만들기 라는 고가용성에 대 한 AG `ag1`합니다. 스크립트는 `SEEDING_MODE = AUTOMATIC`으로 AG 복제본을 구성합니다. 이렇게이 설정 하면 SQL Server를 자동으로 각 보조 서버에 데이터베이스를 만듭니다. 사용자 환경에 대해 다음 스크립트를 업데이트합니다. 대체는 `<node1>`, `<node2>`, 또는 `<node3>` 복제본을 호스팅하는 SQL Server 인스턴스의 이름 가진 값입니다. 대체는 `<5022>` 데이터 미러링 끝점에 대해 설정한 포트를 사용 하 여 합니다. AG를 만들려면 주 복제본을 호스팅하는 SQL Server 인스턴스에서 다음 TRANSACT-SQL을 실행 합니다.

실행할 **하나만** 다음 스크립트 중: 

- [동기 복제본 3 개 create Availability Group](#threeSynch)합니다.
- [두 개의 동기 복제본과 구성 복제본을 사용 하 여 가용성 그룹 만들기](#configOnly)
- [두 개의 동기 복제본을 사용 하 여 create Availability Group](#readScale)합니다.

<a name="threeSynch"></a>

- AG를 동기 복제본 3 개 만들기

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >동기 복제본 3 개 AG를 만들려면 앞의 스크립트를 실행 한 후 다음 스크립트를 실행 하지 않습니다.

<a name="configOnly"></a>
- 두 개의 동기 복제본과 구성 복제본을 사용 하 여 AG를 만듭니다.

   >[!IMPORTANT]
   >이 아키텍처에는 모든 버전을의 SQL Server 세 번째 복제본을 호스팅할 수 있습니다. 예를 들어, SQL Server Enterprise Edition에서 세 번째 복제본을 호스팅할 수 있습니다. Enterprise Edition에만 유효한 끝점 유형이 `WITNESS`합니다. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- 두 개의 동기 복제본을 사용 하 여 AG를 만들기

   동기 가용성 모드를 사용 하 여 두 개의 복제본을 포함 합니다. 예를 들어, 다음 스크립트를 만들고 호출 AG `ag1`합니다. `node1` 및 `node2` 자동 시드 및 자동 장애 조치를 사용 하 여 동기 모드에서 복제본을 호스트 합니다.

   >[!IMPORTANT]
   >만 두 개의 동기 복제본을 사용 하 여 AG를 만들려면 다음 스크립트를 실행 합니다. 앞의 스크립트 중 하나를 실행 하는 경우에 다음 스크립트를 실행 하지 마십시오. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


사용 하 여 AG를 구성할 수도 있습니다 `CLUSTER_TYPE=EXTERNAL` SQL Server Management Studio 또는 PowerShell을 사용 합니다. 

### <a name="join-secondary-replicas-to-the-ag"></a>보조 복제본 AG에 조인

Pacemaker 표시할지 `ALTER`, `CONTROL`, 및 `VIEW DEFINITION` 모든 복제본에서 가용성 그룹에 대 한 권한. 사용 권한을 부여 하려면 가용성 그룹에 추가 된 후에 즉시 가용성 그룹 주 복제본에서 각 보조 복제본에 만든 후 다음 TRANSACT-SQL 스크립트를 실행 합니다. 스크립트를 실행 하기 전에 대체 `<pacemakerLogin>` pacemaker 사용자 계정의 이름입니다.

```Transact-SQL
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

다음 TRANSACT-SQL 스크립트를 명명 된 AG에 SQL Server 인스턴스를 조인 `ag1`합니다. 사용자 환경에 대해 스크립트를 업데이트합니다. 보조 복제본을 호스팅하는 각 SQL Server 인스턴스의 AG에 조인 하려면 다음 TRANSACT-SQL을 실행 합니다.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>AG를 만든 후 고가용성을 위해 Pacemaker와 같은 클러스터 기술을 사용 하 여 통합을 구성 해야 합니다. Ag를 사용 하 여 시작을 사용 하 여 읽기-배율 구성 [!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)], 클러스터를 설정 하지 않아도 됩니다.

이 문서의 단계를 수행 하는 경우 아직 클러스터 되지 않은 AG 해야 합니다. 다음 단계는 클러스터를 추가 하는 것입니다. 이 구성은 읽기-배율/부하 분산 시나리오에 대 한 유효한, 고가용성을 위해 완전 하지 않습니다. 고가용성을 위해 AG를 클러스터 리소스로 추가 해야 합니다. 참조 [다음 단계](#next-steps) 지침에 대 한 합니다. 

## <a name="notes"></a>참고

>[!IMPORTANT]
>클러스터를 구성 하 고를 클러스터 리소스로 AG를 추가한 후에 AG 리소스를 장애 조치할 Transact SQL을 사용할 수 없습니다. Linux의 SQL Server 클러스터 리소스 연계 되지 않습니다와 긴밀 하 게 운영 체제에는 서버 장애 조치 클러스터 (WSFC (Windows) 같습니다. SQL Server 서비스를 클러스터의 현재 상태 인식 없습니다. 모든 오케스트레이션은 클러스터 관리 도구를 통해 수행 됩니다. RHEL 또는 Ubuntu에서 사용 하 여 `pcs`입니다. SLES에서 사용 하 여 `crm`입니다. 

>[!IMPORTANT]
>AG는 클러스터 리소스를 경우 알려진된 문제로 현재 릴리스에서 비동기 복제본에 데이터 손실이 있는 강제 장애 조치 작동 하지 않습니다. 이 향후 릴리스에서 수정 될 예정입니다. 동기 복제본으로 수동 또는 자동 장애 조치 성공합니다.


## <a name="next-steps"></a>다음 단계

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Red Hat Enterprise Linux 클러스터를 구성 합니다.](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 SUSE Linux Enterprise Server 클러스터 구성](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Ubuntu 클러스터 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
