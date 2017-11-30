---
title: "Linux에서 SQL Server에 대 한 읽기 확장성이 가용성 그룹 구성 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 10/20/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 84fe8851a6ff3ad71e9ad9007bddc8715efc8829
ms.sourcegitcommit: c41e1bf5a53e96855b4424de4e0897153070bb28
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2017
---
# <a name="configure-a-read-scale-availability-group-for-sql-server-on-linux"></a>Linux에서 SQL Server에 대 한 읽기 확장성이 가용성 그룹을 구성 합니다.

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Linux에서 SQL Server에 대 한 읽기 확장성이 가용성 그룹을 구성할 수 있습니다. 가용성 그룹에 대 한 두 아키텍처 가지가 있습니다. 고가용성 아키텍처는 클러스터 관리자를 사용 하 여 향상 된 비즈니스 연속성을 제공 합니다. 또한이 아키텍처 읽기 확장성이 복제본을 포함할 수 있습니다. 고가용성 아키텍처를 만들려면 참조 [Linux에서 SQL Server에 대 한 AlwaysOn 가용성 그룹 구성](sql-server-linux-availability-group-configure-ha.md)합니다.

이 문서에서는 클러스터 관리자 없이 읽기 확장성이 가용성 그룹을 만드는 방법에 설명 합니다. 이 아키텍처 읽기 소수 자릿수만 제공합니다. 고가용성을 제공 되지 않습니다.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>가용성 그룹 만들기

가용성 그룹을 만듭니다. Set `CLUSTER_TYPE = NONE`. 또한 각 복제본으로 설정할 `FAILOVER_MODE = NONE`합니다. 클라이언트 응용 프로그램 분석을 실행 또는 워크 로드를 보고 직접 수 보조 데이터베이스에 연결 합니다. 읽기 전용 라우팅 목록을 만들 수도 있습니다. 앞으로 주 복제본에 대 한 연결 라운드 로빈 방식으로 라우팅 목록에서 각 보조 복제본에 연결 요청을 읽습니다.

다음 TRANSACT-SQL 스크립트 라는 가용성 그룹을 만듭니다 `ag1`합니다. 스크립트는 구성 된 가용성 그룹 복제본 `SEEDING_MODE = AUTOMATIC`합니다. 이렇게이 설정 하면 SQL Server를 자동으로 가용성 그룹에 추가 된 후 각 보조 서버에 데이터베이스를 만듭니다. 사용자 환경에 대 한 다음 스크립트를 업데이트 합니다. 대체는 `**<node1>**` 및 `**<node2>**` 복제본을 호스팅하는 SQL Server 인스턴스 이름 사용 하 여 값입니다. 대체는 `**<5022>**` 끝점에 대해 설정 된 포트를 사용 하 여 값입니다. 주 복제본 SQL Server에서 다음 TRANSACT-SQL 스크립트를 실행 합니다.

```SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'**<node1>**' WITH (
            ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'**<node2>**' WITH ( 
            ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-availability-group"></a>보조 SQL Server 가용성 그룹에 조인

다음 TRANSACT-SQL 스크립트 라는 가용성 그룹에는 서버를 가입 시킵니다. `ag1`합니다. 사용자 환경에 대 한 스크립트를 업데이트 합니다. SQL Server 각 보조 복제본에서 가용성 그룹에 참가 하려면 다음 TRANSACT-SQL 스크립트를 실행 합니다.

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

이 가용성 그룹에는 가용성이 높은 구성 하지 않습니다. 고가용성이 필요한 경우의 지침에 따라 [Linux에서 SQL Server에 대 한 AlwaysOn 가용성 그룹 구성](sql-server-linux-availability-group-configure-ha.md)합니다. 특히 가용성 그룹을 만들 `CLUSTER_TYPE=WSFC` (Windows)에 또는 `CLUSTER_TYPE=EXTERNAL` (Linux)에서. 다음 중 하나가 Windows Server 장애 조치 Windows 또는 Linux에서 Pacemaker에서 클러스터링을 사용 하 여 클러스터 관리자와 통합 합니다.

## <a name="connect-to-read-only-secondary-replicas"></a>읽기 전용 보조 복제본에 연결

읽기 전용 보조 복제본에 연결 하는 방법은 두 가지가 있습니다. 응용 프로그램에 보조 복제본을 호스팅하는 SQL Server 인스턴스에 직접 연결 하 고 데이터베이스를 쿼리할 수 있습니다. 또한 사용할 수 있습니다 읽기 전용 라우팅만 수신기 필요 합니다.

* [읽기 가능한 보조 복제본](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [읽기 전용 라우팅](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>장애 조치 읽기 확장성이 가용성 그룹에 주 복제본

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>다음 단계

* [분산형된 가용성 그룹 구성](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)
* [가용성 그룹에 대 한 자세한 정보](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)
* [강제 수동 장애 조치(failover) 수행](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)

