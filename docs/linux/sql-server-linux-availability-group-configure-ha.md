---
title: SQL Server on Linux의 가용성 그룹 구성
description: Linux에서 고가용성을 위해 SQL Server Always On AG(가용성 그룹)를 만드는 방법을 알아봅니다.
author: VanMSFT
ms.custom: seo-lt-2019
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: cfe799e9a0abb8731642ee8b2d8d293c8a8851a2
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784849"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Linux에서 고가용성을 위한 SQL Server Always On 가용성 그룹 구성

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux에서 고가용성을 위한 SQL Server Always On AG(가용성 그룹)를 만드는 방법을 설명합니다. AG의 구성 유형에는 두 가지가 있습니다. ‘고가용성’ 구성은 클러스터관리자를 사용하여 비즈니스 연속성을 제공합니다.  이 구성에는 읽기 확장 복제본도 포함될 수 있습니다. 이 문서에서는 고가용성을 위한 AG를 만드는 방법을 설명합니다.

클러스터 관리자 없이 ‘읽기 확장’을 위한 AG를 만들 수도 있습니다.  읽기 확장을 위한 AG는 성능 확장을 위해 읽기 전용 복제본만 제공합니다. 고가용성을 제공하지 않습니다. 읽기 확장을 위한 AG를 만들려면 [Linux에서 읽기 확장을 위한 SQL Server 가용성 그룹 구성](sql-server-linux-availability-group-configure-rs.md)을 참조하세요.

고가용성 및 데이터 보호를 보장하는 구성에는 두 개 또는 세 개의 동기 커밋 복제본이 필요합니다. 세 개의 동기 복제본을 사용하면, 서버 중 하나를 사용할 수 없는 경우에도 AG가 자동으로 복구할 수 있습니다. 자세한 내용은 [가용성 그룹 구성의 고가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)를 참조하세요. 

모든 서버는 물리적 서버 또는 가상 서버여야 하며, 가상 서버는 동일한 가상화 플랫폼에 있어야 합니다. 이 요구 사항은 펜싱 에이전트가 플랫폼별로 지정되기 때문입니다. [게스트 클러스터 정책](https://access.redhat.com/articles/29440#guest_policies)을 참조하세요.

## <a name="roadmap"></a>로드맵

Linux 서버에서 고가용성을 위한 AG를 만드는 단계는 Windows Server 장애 조치(failover) 클러스터의 단계와 다릅니다. 다음 목록에서는 개괄적인 단계를 설명합니다. 

1. [세 개의 클러스터 서버에서 SQL Server를 구성합니다](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Linux 고가용성은 펜싱 에이전트를 사용하여 서버의 리소스를 격리하기 때문에 AG에 포함된 세 개의 서버가 모두 동일한 플랫폼(물리적 또는 가상)에 있어야 합니다. 펜싱 에이전트는 플랫폼별로 지정됩니다.

2. AG를 만듭니다. 이 단계는 현재 문서에서 설명합니다. 

3. Pacemaker와 같은 클러스터 리소스 관리자를 구성합니다.
   
   클러스터 리소스 관리자를 구성하는 방법은 특정 Linux 배포에 따라 다릅니다. 배포 관련 지침은 다음 링크를 참조하세요. 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >프로덕션 환경에는 고가용성을 위한 STONITH와 같은 펜싱 에이전트가 필요합니다. 이 설명서의 데모에서는 펜싱 에이전트를 사용하지 않습니다. 데모는 테스트 및 유효성 검사를 위해서만 제공됩니다. 
   
   >Linux 클러스터는 펜싱을 사용하여 클러스터를 알려진 상태로 되돌립니다. 펜싱을 구성하는 방법은 배포 및 환경에 따라 달라집니다. 현재, 일부 클라우드 환경에서는 펜싱을 사용할 수 없습니다. 자세한 내용은 [RHEL 고가용성 클러스터의 지원 정책 - 가상화 플랫폼](https://access.redhat.com/articles/29440)을 참조하세요.
   
   >SLES의 경우 [SUSE Linux Enterprise 고가용성 확장](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)을 참조하세요.

5. 클러스터에 AG를 리소스로 추가합니다.  

   클러스터에 AG를 리소스로 추가하는 방법은 Linux 배포에 따라 다릅니다. 배포 관련 지침은 다음 링크를 참조하세요. 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>AG 만들기

이 섹션의 예제에서는 Transact-SQL을 사용하여 가용성 그룹을 만드는 방법을 설명합니다. SQL Server Management Studio 가용성 그룹 마법사를 사용할 수도 있습니다. 마법사를 사용하여 AG를 만드는 경우 AG에 복제본을 조인하면 오류가 반환됩니다. 이 문제를 해결하려면 모든 복제본의 AG에 대한 `ALTER`, `CONTROL` 및 `VIEW DEFINITIONS` 권한을 pacemaker에 부여합니다. 주 복제본에 대한 사용 권한이 부여된 후에 마법사를 통해 AG에 노드를 조인합니다. 단, HA가 제대로 작동하려면 모든 복제본에 대한 사용 권한을 부여합니다.

자동 장애 조치(failover)를 보장하는 고가용성 구성에서는 AG에는 세 개 이상의 복제본이 필요합니다. 고가용성을 지원할 수 있는 구성은 다음 중 하나입니다.

- [동기 복제본 3개](sql-server-linux-availability-group-ha.md#threeSynch)

- [동기 복제본 2개와 구성 복제본 1개](sql-server-linux-availability-group-ha.md#twoSynch)

자세한 내용은 [가용성 그룹 구성의 고가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)를 참조하세요.

>[!NOTE]
>가용성 그룹에 동기 또는 비동기 복제본을 추가로 포함할 수 있습니다. 

Linux에서 고가용성을 위한 AG를 만듭니다. [CREATE AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql)에 `CLUSTER_TYPE = EXTERNAL`을 사용합니다. 

* 가용성 그룹 - `CLUSTER_TYPE = EXTERNAL`로 설정합니다. 외부 클러스터 엔터티가 AG를 관리함을 나타냅니다. Pacemaker는 외부 클러스터 엔터티의 예입니다. AG 클러스터 유형이 external인 경우, 

* 주 복제본과 보조 복제본을 `FAILOVER_MODE = EXTERNAL`로 설정합니다. 
   복제본이 Pacemaker와 같은 외부 클러스터 관리자와 상호 작용함을 나타냅니다. 

다음 Transact-SQL 스크립트는 `ag1`이라는 고가용성을 위한 AG를 만듭니다. 스크립트는 `SEEDING_MODE = AUTOMATIC`으로 AG 복제본을 구성합니다. 이렇게 설정하면 SQL Server가 각 보조 서버에 자동으로 데이터베이스를 만듭니다. 사용자 환경에 대해 다음 스크립트를 업데이트합니다. `<node1>`, `<node2>` 또는 `<node3>` 값을 복제본을 호스트하는 SQL Server 인스턴스 이름으로 바꿉니다. `<5022>`를 데이터 미러링 엔드포인트에 대해 설정한 포트로 바꿉니다. AG를 만들려면 주 복제본을 호스트하는 SQL Server 인스턴스에서 다음 Transact-SQL을 실행합니다.

다음 스크립트 중 **하나만** 실행합니다. 

- [동기 복제본 3개가 포함된 가용성 그룹 만들기](#threeSynch)
- [동기 복제본 2개와 구성 복제본 1개가 포함된 가용성 그룹 만들기](#configOnly)
- [동기 복제본 2개가 포함된 가용성 그룹 만들기](#readScale)

<a name="threeSynch"></a>

- 동기 복제본 3개가 포함된 AG 만들기

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
   >위 스크립트를 실행하여 동기 복제본 3개가 포함된 AG를 만든 후에는 다음 스크립트를 실행하지 마세요.

<a name="configOnly"></a>
- 동기 복제본 2개와 구성 복제본 1개가 포함된 AG 만들기

   >[!IMPORTANT]
   >이 아키텍처에서는 모든 버전의 SQL Server에서 세 번째 복제본을 호스트할 수 있습니다. 예를 들어 SQL Server Express Edition에서 세 번째 복제본을 호스트할 수 있습니다. Express Edition에서 유효한 엔드포인트 유형은 `WITNESS`뿐입니다. 

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

- 동기 복제본 2개가 포함된 AG 만들기

   동기 가용성 모드인 복제본 2개를 포함합니다. 예를 들어 다음 스크립트는 `ag1`이라는 AG를 만듭니다. `node1` 및 `node2`는 동기 모드로 복제본을 호스트하며 자동 시드 및 자동 장애 조치(failover)를 사용합니다.

   >[!IMPORTANT]
   >다음 스크립트는 동기 복제본 2개가 포함된 AG를 만드는 경우에만 실행합니다. 위 스크립트 중 하나를 실행한 경우에는 다음 스크립트를 실행하지 마세요. 

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


SQL Server Management Studio 또는 PowerShell을 사용하여 `CLUSTER_TYPE=EXTERNAL`로 AG를 구성할 수도 있습니다. 

### <a name="join-secondary-replicas-to-the-ag"></a>AG에 보조 복제본 조인

pacemaker 사용자에게 모든 복제본의 가용성 그룹에 대한 `ALTER`, `CONTROL` 및 `VIEW DEFINITION` 권한이 필요합니다. 사용 권한을 부여하려면 가용성 그룹이 생성된 후의 주 복제본과 보조 복제본이 가용성 그룹에 추가된 직후의 각 보조 복제본에서 다음 Transact-SQL을 실행합니다. 스크립트를 실행하기 전에 `<pacemakerLogin>`을 pacemaker 사용자 계정 이름으로 바꿉니다. Pacemaker용 로그인이 없는 경우 [Pacemaker용 SQL 서버 로그인을 만듭니다](sql-server-linux-availability-group-cluster-ubuntu.md#create-a-sql-server-login-for-pacemaker).

```sql
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

다음 Transact-SQL 스크립트는 `ag1`이라는 AG에 SQL Server 인스턴스를 조인합니다. 사용자 환경에 대해 스크립트를 업데이트합니다. 보조 복제본을 호스트하는 각 SQL Server 인스턴스에서 다음 Transact-SQL을 실행하여 AG에 참가합니다.

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>AG를 만든 후에는 고가용성을 위해 Pacemaker와 같은 클러스터 기술과의 통합을 구성해야 합니다. AG를 사용하는 읽기 확장 구성의 경우 [!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)]부터 클러스터를 설정하지 않아도 됩니다.

이 문서의 단계를 수행한 경우 아직 클러스터링되지 않은 AG가 있습니다. 다음 단계는 클러스터를 추가하는 것입니다. 이 구성은 읽기 확장/부하 분산 시나리오에 적합하며, 고가용성은 완전하지 않습니다. 고가용성을 지원하려면 AG를 클러스터 리소스로 추가해야 합니다. 자세한 내용은 [다음 단계](#next-steps)를 참조하세요. 

## <a name="notes"></a>메모

>[!IMPORTANT]
>클러스터를 구성하고 AG를 클러스터 리소스로 추가한 후에는 Transact-SQL을 사용하여 AG 리소스를 장애 조치(failover)할 수 없습니다. Linux의 SQL Server 클러스터 리소스는 WSFC(Windows Server 장애 조치(failover) 클러스터)에 있을 때처럼 운영 체제와 긴밀하게 결합되지 않습니다. SQL Server 서비스는 클러스터의 현재 상태를 인식하지 못합니다. 모든 오케스트레이션이 클러스터 관리 도구를 통해 수행됩니다. RHEL 또는 Ubuntu에서 `pcs`를 사용합니다. SLES에서는 `crm`을 사용합니다. 

>[!IMPORTANT]
>AG가 클러스터 리소스인 경우 현재 릴리스에는 비동기 복제본에 대한 데이터 손실이 있는 강제 장애 조치(failover)가 작동하지 않는 알려진 문제가 있습니다. 이 문제는 이후 릴리스에서 해결될 예정입니다. 동기 복제본에 대한 수동 또는 자동 장애 조치(failover)는 성공합니다.


## <a name="next-steps"></a>다음 단계

[SQL Server 가용성 그룹 클러스터 리소스에 대해 Red Hat Enterprise Linux 클러스터 구성](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대해 SUSE Linux Enterprise Server 클러스터 구성](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대해 Ubuntu 클러스터 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
