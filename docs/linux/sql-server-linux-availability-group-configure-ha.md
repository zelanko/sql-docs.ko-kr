---
title: "구성 SQL Server Always On 가용성 그룹 Linux에서 고가용성을 위해 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/24/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: On Demand
ms.openlocfilehash: b9aeae97abc2f60a9bb6c9c54f5061f68b61a1c9
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>구성 SQL Server Always On 가용성 그룹 Linux에서 고가용성을 위해

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서는 SQL Server 항상에 AG (가용성 그룹) 고가용성을 위해 Linux에서 만드는 방법을 설명 합니다. Ag에 대 한 구성 형식은 두 가지가 있습니다. A *고가용성* 구성 클러스터 관리자를 사용 하 여 비즈니스 연속성을 제공 합니다. 이 구성은 읽기 확장성이 복제본을 포함할 수도 있습니다. 이 문서에서는 고가용성을 위한 AG를 만드는 방법을 설명 합니다.

만들 수도 있습니다는 클러스터 없이 AG에 대 한 관리자 *읽기 확장성이*합니다. 읽기 눈금에 대 한 AG 성능 확장에 대 한 읽기 전용 복제본을 제공합니다. 고가용성을 제공 하지는 않습니다. 읽기 눈금에 대 한 AG 만들려면 [linux 읽기 눈금에 대 한 SQL Server 가용성 그룹 구성](sql-server-linux-availability-group-configure-rs.md)합니다.

높은 가용성 및 데이터 보호를 보장 하는 구성 2 또는 3 개의 동기 커밋 복제본 필요 합니다. 세 개의 동기 복제본을 사용 하 여 하나의 서버를 사용할 수 없는 경우에 AG 복구할 자동으로 수 있습니다. 자세한 내용은 참조 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다. 

모든 서버는 물리적 이거나 가상 장치일 수 있어야 하 고 가상 서버에서 동일한 가상화 플랫폼에 있어야 합니다. 이 요구 사항은 펜스 에이전트 플랫폼 특정 하기 때문입니다. 참조 [게스트 클러스터에 대 한 정책을](https://access.redhat.com/articles/29440#guest_policies)합니다.

## <a name="roadmap"></a>로드맵

고가용성을 위해 Linux 서버에는 AG를 만드는 단계는 Windows Server 장애 조치 클러스터에는 단계와에서 다릅니다. 다음 목록에서는 단계를 간략히 설명합니다. 

1. [3 명의 클러스터 서버에서 SQL Server 구성](sql-server-linux-setup.md)합니다.

   >[!IMPORTANT]
   >AG의 세 서버 모두에 있어야에서 동일한 플랫폼-물리적 또는 가상-Linux 고가용성 펜스 에이전트를 사용 하 여 서버의 리소스를 격리 합니다. 펜스 에이전트는 각 플랫폼에 대 한 특정입니다.

2. AG를 만듭니다. 이 단계는 현재이 문서에서 설명 합니다. 

3. Pacemaker 같은 클러스터 리소스 관리자를 구성 합니다.
   
   클러스터 리소스 관리자를 구성 하는 방법은 특정 Linux 배포에 따라 달라 집니다. 배포 구체적인 지침은 다음 링크 참조: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >프로덕션 환경에서는 고가용성을 위해 STONITH 같은 펜스 에이전트를 해야 합니다. 이 설명서에서 데모 펜싱 에이전트를 사용 하지 마십시오. 데모는 테스트 및 유효성 검사에만 적용 됩니다. 
   
   >Linux 클러스터 펜싱을 사용 하 여 알려진 상태로 클러스터를 반환 합니다. 펜싱을 구성 하는 방법은 배포 및 환경에 따라 달라 집니다. 현재, 펜싱은 일부 클라우드 환경에서 사용할 수 없습니다. 자세한 내용은 참조 [RHEL 높은 가용성 클러스터-가상화 플랫폼에 대 한 지원 정책을](https://access.redhat.com/articles/29440)합니다.
   
   >SLES, 참조 [SUSE Linux Enterprise 높은 가용성 확장](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)합니다.

5. AG에 클러스터 리소스로 추가 합니다.  

   AG에 클러스터 리소스로 추가 하는 방법은 Linux 배포판에 따라 달라 집니다. 배포 구체적인 지침은 다음 링크 참조: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>AG 만들기

자동 장애 조치를 보장 하는 고가용성 구성을 최소 세 개의 복제본 AG 필요 합니다. 고가용성을 지원할 수는 다음 구성 중 하나:

- [세 개의 동기 복제본](sql-server-linux-availability-group-ha.md#threeSynch)

- [2 개의 동기 복제본 플러스 구성 복제본](sql-server-linux-availability-group-ha.md#twoSynch)

자세한 내용은 참조 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다.

>[!NOTE]
>가용성 그룹 추가 동기 또는 비동기 복제를 포함할 수 있습니다. 

Linux에서 고가용성을 위한 AG를 만듭니다. 사용 하 여 [가용성 그룹 만들기](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-availability-group-transact-sql) 와 `CLUSTER_TYPE = EXTERNAL`합니다. 

* 가용성 그룹- `CLUSTER_TYPE = EXTERNAL` AG 외부 클러스터 엔터티를 관리 하는 지정 합니다. Pacemaker는 외부 클러스터 엔터티의 예시입니다. AG 클러스터 종류는 외부 

* 주 복제본과 보조 복제본 설정 `FAILOVER_MODE = EXTERNAL`합니다. 
   복제본 Pacemaker 같은 외부 클러스터 관리자와 상호 작용 한다고 지정 합니다. 

다음 TRANSACT-SQL 스크립트 만들기 라는 고가용성에 대 한 AG `ag1`합니다. 스크립트는 구성 된 AG 복제본 `SEEDING_MODE = AUTOMATIC`합니다. 이렇게이 설정 하면 SQL Server를 자동으로 각 보조 서버에서 데이터베이스를 만듭니다. 사용자 환경에 대 한 다음 스크립트를 업데이트 합니다. 대체는 `**<node1>**`, `**<node2>**`, 또는 `**<node3>**` 복제본을 호스팅하는 SQL Server 인스턴스 이름 사용 하 여 값입니다. 대체는 `**<5022>**` 데이터 미러링 끝점에 대해 설정 된 포트입니다. AG를 만들려면 다음 TRANSACT-SQL 주 복제본을 호스팅하는 SQL Server 인스턴스에서 실행 합니다.

실행 **하나만** 다음 스크립트 중: 

- [Create Availability Group과 세 개의 동기 복제본](#threeSynch)합니다.
- [2 개의 동기 복제본 및 구성 복제본과 가용성 그룹 만들기](#configOnly)
- [Create Availability Group과 2 개의 동기 복제본](#readScale)합니다.

<a name="threeSynch"></a>

- 세 개의 동기 복제본 AG 만들기

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'**<node1>**' 
            WITH (
               ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'**<node2>**' 
            WITH ( 
               ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'**<node3>**'
           WITH( 
              ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >세 개의 동기 복제본을 사용 하 여 AG를 만들려면 이전 스크립트를 실행 한 후 다음 스크립트를 실행 하지 마십시오.

- AG 2 개의 동기 복제본과 구성 복제본으로 만듭니다.

   >[!IMPORTANT]
   >이 구조는 모든 버전의 세 번째 복제본을 호스팅할 SQL Server를 사용 합니다. 예를 들어 SQL Server Enterprise Edition에서 세 번째 복제본을 호스팅할 수 있습니다. Enterprise edition만 유효한 끝점 유형이 `WITNESS`합니다. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'**<node1>**' WITH ( 
          ENDPOINT_URL = N'tcp://**<node1>**:**<5022>**', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'**<node2>**' WITH (  
          ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'**<node3>**' WITH ( 
          ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- AG 2 개의 동기 복제본 만들기

   동기 가용성 모드와 두 개의 복제본을 포함 합니다. 예를 들어 다음 스크립트 만듭니다 라는 AG `ag1`합니다. `node1`및 `node2` 동기 모드, 자동 시드 및 자동 장애 조치에에서 대 한 복제본을 호스트 합니다.

   >[!IMPORTANT]
   >만과 2 개의 동기 복제본 AG를 만들려면 다음 스크립트를 실행 합니다. 위의 스크립트를 실행 한 경우에 다음 스크립트를 실행 하지 마십시오. 

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


AG와 구성할 수도 있습니다 `CLUSTER_TYPE=EXTERNAL` SQL Server Management Studio 또는 PowerShell을 사용 하 여 합니다. 

### <a name="join-secondary-replicas-to-the-ag"></a>AG에 보조 복제본 조인

다음 TRANSACT-SQL 스크립트 라는 AG에 SQL Server 인스턴스를 조인 `ag1`합니다. 사용자 환경에 대 한 스크립트를 업데이트 합니다. 보조 복제본을 호스팅하는 각 SQL Server 인스턴스를 다음 TRANSACT-SQL에는 AG 가입을 실행 합니다.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>AG를 만든 후에 고가용성을 위해 Pacemaker 같은 클러스터 기술로 통합을 구성 해야 합니다. 부터는 Ag를 사용 하 여 읽기 확장성이 구성에 대 한 [!INCLUDE [SQL Server version](..\includes\sssqlv14-md.md)], 필요 하지 않습니다는 클러스터를 설정 합니다.

이 문서의 단계를 따른 경우 아직 클러스터 되지 않은 AG 해야 합니다. 다음 단계에서는 클러스터를 추가 하는 것입니다. 이 구성은 읽기-대규모/부하 분산 시나리오에 대 한 유효한, 고가용성에 대 한 완료 되지 않았습니다. 고가용성을 위해 AG를 클러스터 리소스로 추가 해야 합니다. 참조 [다음 단계](#next-steps) 지침에 대 한 합니다. 

## <a name="notes"></a>참고

>[!IMPORTANT]
>클러스터를 구성 하 고를 클러스터 리소스로 AG를 추가한 후 TRANSACT-SQL AG 리소스 장애 조치를 사용할 수 없습니다. Linux에서 SQL Server 클러스터 리소스 Windows Server 장애 조치 클러스터 (WSFC)에 운영 체제와 엄격히 결합 되지 됩니다. SQL Server 서비스가 클러스터의 사용 여부 인식 하지 않습니다. 모든 오케스트레이션 클러스터 관리 도구를 통해 수행 됩니다. RHEL 또는 Ubuntu에서 사용 하 여 `pcs`합니다. SLES에서 사용 하 여 `crm`합니다. 

>[!IMPORTANT]
>클러스터 리소스는 AG의 경우에 없는 경우 알려진된 문제로 현재 릴리스의 데이터 손실 비동기 복제본에 강제 장애 조치 작동 하지 않습니다. 이 곧 출시 될 릴리스에 수정 될 예정입니다. 동기 복제본으로 수동 또는 자동 장애 조치 성공합니다. 


## <a name="next-steps"></a>다음 단계

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Red Hat Enterprise Linux 클러스터를 구성 합니다.](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 SUSE Linux Enterprise Server 클러스터 구성](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 가용성 그룹 클러스터 리소스에 대 한 Ubuntu 클러스터 구성](sql-server-linux-availability-group-cluster-ubuntu.md)
