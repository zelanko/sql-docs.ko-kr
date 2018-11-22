---
title: 가용성 그룹에서 SQL Server 배포 데이터베이스 구성 | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 94616b5950ca1ff7f33d9061d2bbc8bab53fbc8c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602633"
---
# <a name="set-up-replication-distribution-database-in-always-on-availability-group"></a>Always On 가용성 그룹에서 복제 배포 데이터베이스 설정

이 문서에서는 AG(Always On) 가용성 그룹에서 SQL Server 복제 배포 데이터베이스를 설정하는 방법에 대해 설명합니다.

SQL Server 2017 CU6 및 SQL Server 2016 SP2-CU3에서는 다음 메커니즘을 통해 AG에서 복제 배포 데이터베이스를 지원합니다.

- 배포 데이터베이스 AG에 수신기가 있어야 합니다. 게시자가 배포자를 추가할 때는 수신기 이름을 배포자의 이름으로 사용합니다.
- 수신기 이름을 배포자의 이름으로 사용하여 복제 작업을 만듭니다.
- 새 작업은 배포 데이터베이스의 상태(AG에서 주 또는 보조)를 모니터하며 배포 데이터베이스 상태에 따라 복제 작업을 사용하거나 사용하지 않도록 설정합니다.

아래 설명한 단계에 따라 AG의 배포 데이터베이스를 구성한 후에는 복제 구성과 런타임 작업이 배포 데이터베이스 AG 장애 조치(failover) 전후에 올바르게 실행될 수 있습니다.

## <a name="supported-scenarios"></a>지원되는 시나리오

- AG에 포함할 배포 데이터베이스 구성 
- AG 장애 조치 전후에 게시 및 구독 등 복제 구성
- 복제 작업이 장애 조치 전후에 작동 
- 배포 데이터베이스가 AG에 있을 때 배포자 및 게시자에서 복제 제거
- 기존 배포 데이터베이스 AG에 노드추가 또는 제거
- 배포자에는 여러 배포 데이터베이스가 있을 수 있습니다. 각 배포 데이터베이스는 자체 AG에 있을 수 있고 다른 AG에는 있을 수 없습니다. 여러 배포 데이터베이스가 AG를 공유할 수 있습니다.
- 게시자 및 배포자는 별도 SQL Server 인스턴스에 있어야 합니다.
- 배포 데이터베이스를 호스트하는 가용성 그룹에 대한 수신기가 기본값이 아닌 포트를 사용하도록 구성된 경우, 이 수신기에 대한 별칭과 기본값 이외 포트를 설정해야 합니다.

## <a name="limitations-or-exclusions"></a>제한 및 배제

- 로컬 배포자는 지원되지 않습니다. 예를 들어 게시자와 배포자는 다른 SQL Server 인스턴스여야 합니다. 스스로를 배포자로 사용하는 게시자(즉 로컬 배포자)는 AG의 배포 데이터베이스를 지원할 수 없습니다.
- Oracle 게시자는 지원되지 않습니다.
- 병합 복제는 지원되지 않습니다.
- 즉시 또는 업데이트 큐에 있는 구독자가 있는 트랜잭션 복제는 지원되지 않습니다.
- 피어 투 피어 복제는 지원되지 않습니다.
- 배포 데이터베이스 복제본을 호스팅하는 모든 SQL Server 인스턴스는 SQL Server 2017 CU 6 이상이어야 합니다. 
- 배포 데이터베이스 복제본을 호스팅하는 모든 SQL Server 인스턴스는 업데이트를 수행하는 시간 범위가 적은 경우를 제외하고 같은 버전이어야 합니다.
- 배포 데이터베이스는 전체 복구 모드여야 합니다.
- 복구와, 트랜잭션 로그 잘림을 허용하기 위해 전체 및 트랜잭션 로그 백업을 구성합니다.
- 배포 데이터베이스 AG에 수신기가 구성되어 있어야 합니다.
- 배포 데이터베이스 AG의 보조 복제본은 동기 또는 비동기가 될 수 있습니다. 동기 모드가 권장되며 기본 설정입니다.
- 양방향 트랜잭션 복제는 지원되지 않습니다.
- SSMS은 배포 데이터베이스가 가용성 그룹에 추가되면 배포 데이터베이스를 동기화 중/동기화됨으로 표시하지 않습니다.


   >[!NOTE]
   >보조 복제본에서 복제 저장 프로시저(예: `sp_dropdistpublisher`, `sp_dropdistributiondb`, `sp_dropdistributor`, `sp_adddistributiondb`, `sp_adddistpublisher`)를 실행하기 전에 복제본이 완전히 동기화되었는지 확인합니다.

- 배포 데이터베이스 AG의 모든 보조 복제본은 읽을 수 있어야 합니다.
- 배포 데이터베이스 AG의 모든 노드는 SQL Server 에이전트 실행을 위해 동일한 도메인 계정을 사용해야 하며 이 도메인 계정은 각 노드에서 동일한 권한을 가져야 합니다.
- 프록시 계정에서 실행되는 복제 에이전트가 있는 경우 프록시 계정이 배포 데이터베이스 AG의 모든 노드에 있고 각 노드에서 동일한 권한을 가져야 합니다.
- 배포 데이터베이스 AG에 참여하는 모든 복제본에서 배포자 또는 배포 데이터베이스 속성을 변경합니다.
- 배포 데이터베이스 AG에 참여하는 모든 복제본에서 msdb 저장 프로시저 또는 SQL Server Management Studi를 통해 복제 작업을 변경합니다.
- 게시자에 대한 배포자 구성은 스크립트를 통해 수행해야 합니다. 복제 마법사는 사용할 수 없습니다. 다른 용도에는 복제 마법사 및 속성 시트를 사용할 수 있습니다.
- 배포 데이터베이스에 대한 AG 구성은 스크립트를 통해서만 가능합니다.
- AG에서 배포 데이터베이스를 설정하려면 새 복제 구성이어야 합니다. 기존 배포 데이터베이스를 AG 전환하는 것은 지원되지 않습니다. 또한 배포 데이터베이스가 AG로 가면 더 이상 유효한 배포 데이터베이스로 작동하지 않으며 삭제해야 합니다. 

## <a name="configuration-architecture"></a>구성 아키텍처

이 문서의 예에서는 다음 서버 이름 및 설정을 사용합니다.

- DIST1, DIST2, DIST3은 배포자 서버입니다.
- PUB는 게시자 서버입니다.
- 배포 데이터베이스 AG가 구성된 후 수신기 이름은 DISTLISTENER입니다.
- DIST1은 배포 데이터베이스 AG의 최초 주 복제본이 됩니다.

## <a name="configure-distributor-distribution-database-and-publisher"></a>배포자, 배포 데이터베이스 및 게시자 구성

이 예에서는 새 배포자와 게시자를 구성하고 AG에 배포 데이터베이스를 넣습니다.

### <a name="distributors-workflow"></a>배포자 워크플로

1. `sp_adddistributor @@servername`을 통해 배포자로 DIST1, DIST2, DIST3을 구성합니다. `@password`를 통해 `distributor_admin`에 대한 암호를 지정합니다. `@password`는 DIST1, DIST2, DIST3 전체에서 동일해야 합니다.
2. `sp_adddistributiondb`를 통해 DIST1에 배포 데이터베이스를 만듭니다. 배포 데이터베이스의 이름은 `distribution`입니다. `distribution` 데이터베이스의 복구 모두를 simple에서 full로 변경합니다.
3. DIST1, DIST2 및 DIST3에서 복제본을 통해 `distribution` 데이터베이스에 대한 AG를 만듭니다. 모든 복제본은 동기 상태인 것이 좋습니다. 보조 복제본을 읽기 가능 또는 읽기 허용으로 구성합니다. 이번에는 배포 데이터베이스가 AG, DIST1이 주 복제본, DIST2 및 DIST3이 보조 복제본입니다.
4. AG에 대해 이름이 `DISTLISTENER`인 수신기를 구성합니다.
5. 복구와, 트랜잭션 로그 잘림을 허용하기 위해 전체 및 트랜잭션 로그 백업을 구성합니다.
6. DIST2 및 DIST3에서 다음을 실행합니다.

   ```sql
   sp_adddistributiondb 'distribution'
   ```

1. DIST1에서 `PUB`를 게시자로 추가하려면 다음을 실행합니다.
   
   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` 값은 DIST1, DIST2 및 DIST3과는 별개인 네트워크 경로여야 합니다.

1. DIST2 및 DIST3에서 다음을 실행합니다.  

   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` 값은 이전 단계와 동일해야 합니다.

### <a name="publisher-workflow"></a>게시자 워크플로

`distribution` 데이터베이스 AG 수신기를 배포자로 추가하려면 PUB에서 다음을 실행합니다. 

   ```sql
   sp_adddistributor @distributor = 'DISTLISTENER', @password = <distributor_admin password> 
   ```

   @password 값은 배포자가 배포 워크플로에서 구성될 때 지정한 값이어야 합니다.

## <a name="remove-distributor-and-publisher"></a>배포자 및 게시자 제거

이 예에서는 배포 데이터베이스가 AG에 있을 때 게시자 및 배포자를 제거합니다.

### <a name="publisher-workflow"></a>게시자 워크플로

이제 PUB에서 이 게시자에 대한 모든 구독 및 게시자가 `sp_dropdistributor`를 호출합니다.

### <a name="distributors-workflow"></a>배포자 워크플로

이 예에서 DIST1은 `distribution` 데이터베이스 AG의 현재 주 복제본입니다. DIST2 및 DIST3은 보조 복제본입니다.

1. DIST2 및 DIST3에서 다음을 실행합니다.

   ```sql
   sp_dropdistpublisher 'PUB',  @no_checks = 1
   ```

1. DIST1에서 다음을 실행합니다.

   ```sql
   sp_dropdistpublisher 'PUB'
   ```

1. AG를 삭제합니다.
2. DIST2 및 DIST3에서 복구로 데이터베이스를 복원하여 `distribution` 데이터베이스를 read_write 모드로 변경합니다.
   
   ```sql
   RESTORE DATABASE distribution WITH RECOVERY, KEEP_REPLICATION
   ```

1. `distribution` 데이터베이스를 삭제하고 스냅숏 디렉터리를 유지하려면 다음을 실행합니다. 

   ```sql
   sp_dropdistributiondb 'distribution' , @former_ag_secondary=1
   ```

  이 절차에서는 이 복제본에 따른 모든 작업을 삭제합니다. 

1. DIST1에서 `distribution` 데이터베이스를 삭제하려면 다음을 실행합니다.

   ```sql
   sp_dropdistributiondb 'distribution'
   ``` 

1. AG에 다른 배포 데이터베이스가 없는 경우 DIST3 DIST1, DIST2에서 `sp_dropdistributor`를 실행합니다.

## <a name="add-a-replica-to-distribution-database-ag"></a>배포 데이터베이스 AG에 복제본 추가

이 예에서는 AG의 배포 데이터베이스로 기존 복제 구성에 새 배포자를 추가합니다. 이 예에서 기존 배포 데이터베이스는 AG에 있습니다. DIST1 및 DIST2는 배포자, `distribution`은 AG의 배포 데이터베이스, PUB는 게시자입니다. AG의 복제본으로 DIST3을 추가합니다.

### <a name="distributors-workflow"></a>배포자 워크플로

1. DIST3은 `sp_adddistributor @@servername`을 통해 배포자로 구성되어야 합니다. `distributor_admin`에 대한 암호는 @password 매개 변수를 통해 지정되어야 합니다. 암호는 DIST1 및 DIST2에 대해 지정 된 것과 동일해야 합니다.
2. 현재 배포 데이터베이스에 대한 AG에 DIST3을 추가합니다.
3. DIST3에서 다음을 실행합니다.

   ```sql
   sp_adddistributiondb 'distribution'
   ```

4. DIST3에서 다음을 실행합니다. 

   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` 값은 DIST1 및 DIST2에 대해 지정 된 것과 동일해야 합니다.

4. DIST3에서는 구독자에 대한 연결된 서버를 다시 만들어야 합니다.

## <a name="remove-a-replica-from-distribution-database-ag"></a>배포 데이터베이스 AG에서 복제본 제거

이 예에서는 현재 배포 데이터베이스 AG에서 배포자를 제거하며, 배포 데이터베이스 AG의 나머지 복제본에는 영향이 없습니다. 이 예에서 배포 데이터베이스는 AG에 있습니다. DIST1, DIST2 및 DIST3은 배포자, `distribution`은 AG의 배포 데이터베이스, PUB는 게시자입니다. DIST3을 AG에서 제거합니다.

### <a name="distributors-workflow"></a>배포자 워크플로

1. DIST3은 `distribution` 데이터베이스 AG의 보조여야 합니다.
2. DIST3을 `distribution` 데이터베이스에서 제거합니다.
3. DIST3에서 복구로 데이터베이스를 복원하여 `distribution` 데이터베이스를 read_write 모드로 변경합니다. 예를 들어 다음 명령을 실행합니다.  
   
   ```sql
   RESTORE DATABASE distribution WITH RECOVERY, KEEP_REPLICATION.
   ```
   
1. DIST3에서 분리된 모든 작업을 제거하려면 다음을 실행합니다. 

   ```sql
   sp_dropdistpublisher 'PUB', @no_checks = 1
   ```

1. DIST3에서 다음을 실행합니다.

   ```sql
   sp_dropdistributiondb 'distribution', @former_ag_secondary=1
   ```

1. DIST3에서 다음을 실행합니다. 

   ```sql
   sp_dropdistributor
   ```

## <a name="remove-a-publisher-from-distribution-database-ag"></a>배포 데이터베이스 AG에서 게시자 제거

이 예에서는 현재 배포 데이터베이스 AG에서 게시자를 제거하며, 배포 데이터베이스 AG에서 서비스하는 나머지 게시자에는 영향이 없습니다. 이 예에서는 기존 구성이 AG에 배포 데이터베이스를 갖습니다. DIST1, DIST2 및 DIST3은 배포자, `distribution`은 AG의 배포 데이터베이스, PUB1 및 PUB2는 `distribution` 데이터베이스에서 서비스하는 게시자입니다. 이 예에서는 이러한 배포자에서 PUB1을 제거합니다. 

### <a name="publisher-workflow"></a>게시자 워크플로

이제 PUB1에서 이 게시자에 대한 모든 구독 및 게시자가 `sp_dropdistributor`를 호출합니다.

### <a name="distributor-workflow"></a>배포자 워크플로

DIST1은 `distribution` 데이터베이스 AG의 현재 주 복제본입니다.

1. DIST2 및 DIST3에서 다음을 실행합니다.

   ```sql
   sp_dropdistpublisher 'PUB1',  @no_checks = 1
   ```

1. DIST1에서 다음을 실행합니다.

   ```sql
   sp_dropdistpublisher 'PUB1'
   ```

1. 이 시점에서 DIST2 또는 DIST3의 PUB1과 관련한 분리된 작업이 있을 수 있습니다. DIST2 및 DIST3에서 장애 조치(failover)가 발생할 때마다 PUB1의 모든 게시와 관련한 분리된 작업은 `Monitor and sync replication agent jobs` 작업을 통해 제거됩니다.

## <a name="add-subscription"></a>구독 추가

이 예는 배포자 간에 구독자 정보를 올바르게 구성하는 방법에 대한 것입니다. 이 예에서는 구독자를 추가합니다. DIST1은 현재 AG에서 배포 데이터베이스의 주 복제본이며 DIST2와 DIST3은 AG에서 배포 데이터베이스의 보조 복제본입니다. 구독자 이름은 SUB입니다.

### <a name="publisher-workflow"></a>게시자 워크플로

`SUB` 구독자에서 하는 것처럼 PUB에서 구독을 추가합니다. 

### <a name="distributor-workflow"></a>배포자 워크플로

이전에 DIST2 및 DIST3에 등록하지 않은 경우 DIST2 및 DIST3에서 'SUB'에 대해 연결된 서버를 추가합니다. 다음은 연결된 서버 만들기를 위한 샘플 TSQL입니다.

   ```sql 
   EXEC master.dbo.sp_addlinkedserver@server =N'SUB', @srvproduct=N'SQL Server'
   /* For security reasons the linked server remote logins password is changed with ######## */
   EXEC master.dbo.sp_addlinkedsrvlogin@rmtsrvname=N'SUB', @useself=N'True',@locallogin=NULL,@rmtuser=NULL,@rmtpassword=NULL
   ```

## <a name="add-a-pull-subscription"></a>끌어오기 구독 추가

### <a name="subscriber-workflow"></a>구독자 워크플로

AG에서 배포 데이터베이스를 통해 게시에 대한 끌어오기 구독을 추가하려면 `sp_addpullsubscription_agent`의 `@distributor` 매개 변수에서 AG 수신기 이름을 사용합니다.

## <a name="sample-t-sql-create-distribution-db-in-ag"></a>샘플 T-SQL: AG에서 배포 DB 만들기

다음 스크립트는 가용성 그룹에서 배포 데이터베이스를 사용하도록 설정합니다. 

```sql
--- WorkFlow to Enable Distribution Database In AG.

-- SECTION 1 ---- CONFIGURE THE DISTRIBUTOR SERVERS

-- Step1 - Configure the Distribution DB nodes (AG Replicas) to act as a distributor
:Connect SQLNode1
sp_adddistributor @distributor = @@ServerName, @password = 'Pass@word1'
Go 
:Connect SQLNode2
sp_adddistributor @distributor = @@ServerName, @password = 'Pass@word1'
Go

-- Step2 - Configure the Distribution Database
:Connect SQLNode1
USE master
EXEC sp_adddistributiondb @database = 'DistributionDB', @security_mode = 1;
GO
Alter Database [DistributionDB] Set Recovery Full
Go
Backup Database [DistributionDB] to Disk = 'Nul'
Go
-- Step 3 - Create AG for the Distribution DB.
:Connect SQLNode1
USE [master]
GO
CREATE ENDPOINT [Hadr_endpoint] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)   
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE
, ENCRYPTION = REQUIRED ALGORITHM AES)
GO

:Connect SQLNode2
USE [master]
GO
CREATE ENDPOINT [Hadr_endpoint] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)   
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE
, ENCRYPTION = REQUIRED ALGORITHM AES)
GO

:Connect SQLNode1
-- Create the Availability Group
CREATE AVAILABILITY GROUP [DistributionDB_AG]
FOR DATABASE [DistributionDB]
REPLICA ON 'SQLNode1'
WITH (ENDPOINT_URL = N'TCP://SQLNode1.contoso.com:5022', 
         FAILOVER_MODE = AUTOMATIC, 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
         BACKUP_PRIORITY = 50, 
         SECONDARY_ROLE(ALLOW_CONNECTIONS = ALL), 
         SEEDING_MODE = AUTOMATIC),
N'SQLNode2' WITH (ENDPOINT_URL = N'TCP://SQLNode2.contoso.com:5022', 
     FAILOVER_MODE = AUTOMATIC, 
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
     BACKUP_PRIORITY = 50, 
     SECONDARY_ROLE(ALLOW_CONNECTIONS = ALL), 
     SEEDING_MODE = AUTOMATIC);
 GO


:Connect SQLNode2
ALTER AVAILABILITY GROUP [DistributionDB_AG] JOIN
GO  
ALTER AVAILABILITY GROUP [DistributionDB_AG] GRANT CREATE ANY DATABASE
Go

--STEP4 - Create the Listener for the Availability Group. This is very important.
:Connect SQLNode1

USE [master]
GO
ALTER AVAILABILITY GROUP [DistributionDB_AG]
ADD LISTENER N'DistributionDBList' (
WITH IP
((N'10.0.0.8', N'255.255.255.0')) , PORT=1500);
GO

-- STEP 5 - Enable SQLNode1 also as a Distributor
:CONNECT SQLNODE2
EXEC sp_adddistributiondb @database = 'DistributionDB', @security_mode = 1;
GO

--STEP 6 - On all Distributor Nodes Configure the Publisher Details 
:CONNECT SQLNODE1
EXEC sp_addDistPublisher @publisher = 'SQLNode4', @distribution_db = 'DistributionDB', 
    @working_directory = '\\sqlfileshare\Dist_Work_Directory\'
GO
:CONNECT SQLNODE2
EXEC sp_addDistPublisher @publisher = 'SQLNode4', @distribution_db = 'DistributionDB', 
    @working_directory = '\\sqlfileshare\Dist_Work_Directory\'
GO

-- SECTION 2 ---- CONFIGURE THE PUBLISHER SERVER
:CONNECT SQLNODE4
EXEC sp_addDistributor @distributor = 'DistributionDBList', -- Listener for the Distribution DB.    
    @password = 'Pass@word1'
Go

-- SECTION 3 ---- CONFIGURE THE SUBSCRIBERS 
-- On Publisher, create the publication as one would normally do.
-- On the Secondary replicas of the Distribution DB, add the Subscriber as a linked server.
:CONNECT SQLNODE2
EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE5', @srvproduct=N'SQL Server'
 /* For security reasons the linked server remote logins password is changed with ######## */
EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname=N'SQLNODE5',@useself=N'True',@locallogin=NULL,@rmtuser=NULL,@rmtpassword=NULL 
```

## <a name="see-also"></a>참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [배포자 보안 설정](../../relational-databases/replication/security/secure-the-distributor.md)  
  
## <a name="next-steps"></a>다음 단계
 [배포자 및 게시자 속성 보기 및 수정](view-and-modify-distributor-and-publisher-properties.md)  
 [게시 및 배포 해제](disable-publishing-and-distribution.md)  
 [데이터베이스 복제 설정(SQL Server Management Studio)](enable-a-database-for-replication-sql-server-management-studio.md) 
