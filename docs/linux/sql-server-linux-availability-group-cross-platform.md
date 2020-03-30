---
title: Windows 및 Linux에서 SQL Server Always On 가용성 그룹 구성
description: Windows 및 Linux에서 복제본을 사용하여 SQL Server 가용성 그룹을 구성합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 651467463e0563c9da00e23115ffb7bc4f151d23
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "77479678"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>Windows 및 Linux에서 SQL Server Always On 가용성 그룹 구성(플랫폼 간)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

이 문서에서는 Windows Server의 복제본 1개와 Linux 서버의 복제본 1개를 사용하여 Always On AG(가용성 그룹)를 만드는 단계를 설명합니다. 복제본이 서로 다른 운영 체제에 있기 때문에 이 구성은 플랫폼 간에 지원됩니다. 한 플랫폼에서 다른 플랫폼으로 마이그레이션하거나 DR(재해 복구)하려는 경우 이 구성을 사용합니다. 플랫폼 간 구성을 관리할 클러스터 솔루션이 없기 때문에 이 구성은 고가용성을 지원하지 않습니다. 

![하이브리드 없음](./media/sql-server-linux-availability-group-overview/image1.png)

계속 진행하기 전에 Windows 및 Linux의 SQL Server 인스턴스 설치 및 구성을 잘 알고 있어야 합니다. 

## <a name="scenario"></a>시나리오

이 시나리오에서는 두 서버가 서로 다른 운영 체제에 있습니다. `WinSQLInstance`라는 Windows Server 2016에서 주 복제본을 호스트합니다. `LinuxSQLInstance`라는 Linux 서버는 보조 복제본을 호스트합니다.

## <a name="configure-the-ag"></a>AG 구성 

AG를 만드는 단계는 읽기 확장 워크로드를 위한 AG를 만드는 단계와 동일합니다. 클러스터 관리자가 없기 때문에 AG 클러스터 유형은 NONE입니다. 

   >[!NOTE]
   >이 문서의 스크립트에서 꺾쇠괄호 `<` 및 `>`는 해당 환경에 맞게 바꾸어야 하는 값을 식별합니다. 꺾쇠괄호 자체는 스크립트에 필요하지 않습니다. 

1. Windows Server 2016에서 SQL Server 2017을 설치하고 SQL Server 구성 관리자에서 Always On 가용성 그룹을 사용하도록 설정한 다음, 혼합 모드 인증을 설정합니다. 

   >[!TIP]
   >Azure에서 이 솔루션의 유효성을 검사하는 경우 두 서버를 동일한 가용성 집합에 배치하여 데이터 센터에서 분리되도록 합니다. 

   **가용성 그룹 사용**

   자세한 내용은 [Always On 가용성 그룹 사용 및 사용 안 함(SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)을 참조하세요.

   ![가용성 그룹 사용](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   SQL Server 구성 관리자에서 컴퓨터가 장애 조치(failover) 클러스터의 노드가 아님을 확인합니다. 

   가용성 그룹을 사용하도록 설정한 후 SQL Server를 다시 시작합니다.

   **혼합 모드 인증**

   자세한 내용은 [서버 인증 모드 변경](../database-engine/configure-windows/change-server-authentication-mode.md#change-authentication-mode-with-ssms)을 참조하세요.

1. Linux에서 SQL Server 2017을 설치합니다. 자세한 내용은 [SQL Server 설치](sql-server-linux-setup.md)를 참조하세요. mssql-conf를 통해 `hadr`을 사용하도록 설정합니다.

   셸 프롬프트에서 mssql-conf를 통해 `hadr`을 사용하도록 설정하려면 다음 명령을 실행합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   `hadr`을 사용하도록 설정한 후 SQL Server 인스턴스를 다시 시작합니다.  

   다음 그림은 이 전체 단계를 보여 줍니다.

   ![가용성 그룹 Linux 사용](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. 두 서버에서 모두 hosts 파일을 구성하거나 서버 이름을 DNS에 등록합니다.

1. Windows와 Linux에서 모두 TCP 1433 및 5022의 방화벽 포트를 엽니다.

1. 주 복제본에서 데이터베이스 로그인 및 암호를 만듭니다.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. 주 복제본에서 마스터 키와 인증서를 만든 다음, 프라이빗 키를 사용하여 인증서를 백업합니다.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. 인증서 및 프라이빗 키를 Linux 서버(보조 복제본)의 `/var/opt/mssql/data`에 복사합니다. `pscp`를 사용하여 Linux 서버에 파일을 복사할 수 있습니다. 

1. 프라이빗 키와 인증서의 그룹 및 소유권을 `mssql:mssql`로 설정합니다.

   다음 스크립트는 파일의 그룹 및 소유권을 설정합니다. 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   다음 다이어그램에서는 인증서 및 키의 소유권과 그룹이 올바르게 설정되었습니다.

   ![가용성 그룹 Linux 사용](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. 보조 복제본에서 데이터베이스 로그인 및 암호를 만든 다음, 마스터 키를 만듭니다.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. 보조 복제본에서 복사한 인증서를 `/var/opt/mssql/data`로 복원합니다. 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. 주 복제본에서 엔드포인트를 만듭니다.

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >수신기 TCP 포트에 대해 방화벽이 열려 있어야 합니다. 위 스크립트에서 포트는 5022입니다. 사용 가능한 아무 TCP 포트나 사용합니다. 

1. 보조 복제본에서 엔드포인트를 만듭니다. 보조 복제본에서 위 스크립트를 반복하여 엔드포인트를 만듭니다. 

1. 주 복제본에서 `CLUSTER_TYPE = NONE`을 사용하여 AG를 만듭니다. 예제 스크립트에서는 `SEEDING_MODE = AUTOMATIC`을 사용하여 AG를 만듭니다. 

   >[!NOTE]
   >SQL Server의 Windows 인스턴스에서 데이터와 로그 파일에 대해 서로 다른 경로를 사용하는 경우, 보조 복제본에는 해당 경로가 없기 때문에 SQL Server의 Linux 인스턴스에 대한 자동 시드가 실패합니다. 플랫폼 간 AG에 대해 다음 스크립트를 사용하려면 데이터베이스가 제대로 작동하기 위해 Windows Server의 데이터 및 로그 파일 경로가 같아야 합니다. 또는 스크립트를 업데이트하여 `SEEDING_MODE = MANUAL`을 설정한 다음, `NORECOVERY`로 데이터베이스를 백업 및 복원하여 데이터베이스를 시드할 수 있습니다. 
   >
   >이 동작은 Azure Marketplace 이미지에 적용됩니다. 
   >
   >자동 시드에 대한 자세한 내용은 [자동 시드 - 디스크 레이아웃](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout)을 참조하세요. 

   스크립트를 실행하기 전에 해당 AG의 값을 업데이트합니다.

      * `<WinSQLInstance>`를 주 복제본 SQL Server 인스턴스의 서버 이름으로 바꿉니다.

      * `<LinuxSQLInstance>`를 보조 복제본 SQL Server 인스턴스의 서버 이름으로 바꿉니다. 

   AG를 만들려면 값을 업데이트하고 주 복제본에서 스크립트를 실행합니다.  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   자세한 내용은 [CREATE AVAILABILITY GROUP(Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)을 참조하세요.

1. 보조 복제본에서 AG를 조인합니다.

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. AG의 데이터베이스를 만듭니다. 예제 단계에서는 `<TestDB>`라는 데이터베이스를 사용합니다. 자동 시드를 사용하는 경우 데이터와 로그 파일에 대해 동일한 경로를 설정합니다. 

   스크립트를 실행하기 전에 해당 데이터베이스의 값을 업데이트합니다.

      * `<TestDB>`를 해당 데이터베이스의 이름으로 바꿉니다.

      * `<F:\Path>`를 해당 데이터베이스 및 로그 파일의 경로로 바꿉니다. 데이터베이스 및 로그 파일에 대해 동일한 경로를 사용합니다. 

      기본 경로를 사용할 수도 있습니다. 

    데이터베이스를 만들려면 스크립트를 실행합니다. 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. 데이터베이스의 전체 백업을 수행합니다. 

1. 자동 시드를 사용하지 않는 경우 보조 복제본(Linux) 서버에서 데이터베이스를 복원합니다. [백업 및 복원을 사용하여 Windows에서 Linux로 SQL Server 데이터베이스를 마이그레이션합니다](sql-server-linux-migrate-restore-database.md). 보조 복제본에서 `WITH NORECOVERY` 데이터베이스를 복원합니다. 

1. AG에 데이터베이스를 추가합니다. 예제 스크립트를 업데이트합니다. `<TestDB>`를 해당 데이터베이스의 이름으로 바꿉니다. 주 복제본에서 SQL 쿼리를 실행하여 AG에 데이터베이스를 추가합니다.

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. 데이터베이스가 보조 복제본에 채워지고 있는지 확인합니다. 

## <a name="fail-over-the-primary-replica"></a>주 복제본 장애 조치(failover)

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

이 문서에서는 마이그레이션 또는 읽기 확장 워크로드를 지원하기 위해 플랫폼 간 AG를 만드는 단계를 검토했습니다. 이 AG는 수동 재해 복구에 사용할 수 있습니다. AG를 장애 조치(failover)하는 방법도 설명했습니다. 플랫폼 간 AG는 클러스터 유형 `NONE`을 사용하며, 플랫폼 간 클러스터 도구가 없기 때문에 고가용성을 지원하지 않습니다. 

## <a name="next-steps"></a>다음 단계

[Always On 가용성 그룹 개요](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Linux 배포의 SQL Server 가용성 기본 사항](sql-server-linux-ha-basics.md)
