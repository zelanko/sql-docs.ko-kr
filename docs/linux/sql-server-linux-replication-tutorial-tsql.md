---
title: Linux에서 SQL Server 복제 구성
description: 이 자습서에서는 Linux에서 SQL Server 스냅샷 복제를 구성하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: acc3f556371c52d02789a03813a28606435d86cd
ms.sourcegitcommit: 56fb0b7750ad5967f5d8e43d87922dfa67b2deac
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2019
ms.locfileid: "75001986"
---
# <a name="configure-replication-with-t-sql"></a>T-SQL을 사용하여 복제 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)] 

이 자습서에서는 Transact-SQL을 사용하여 Linux에서 두 개의 SQL Server 인스턴스로 SQL Server 스냅샷 복제를 구성합니다. 게시자와 배포자는 동일한 인스턴스이고, 구독자는 별도의 인스턴스에 있습니다.

> [!div class="checklist"]
> * Linux에서 SQL Server 복제 에이전트 사용
> * 예제 데이터베이스 만들기
> * SQL Server 에이전트 액세스를 위해 스냅샷 폴더 구성
> * 배포자 구성
> * 게시자 구성
> * 게시 및 아티클 구성
> * 구독자 구성 
> * 복제 작업 실행

모든 복제 구성은 [복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)를 사용하여 구성할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 다음 항목이 필요합니다.

- 최신 버전의 SQL Server on Linux가 설치된 두 개의 SQL Server 인스턴스
- 복제를 설정하기 위해 T-SQL 쿼리를 실행하는 도구(예: SQLCMD 또는 SSMS)

   [SSMS를 사용하여 SQL Server on Linux 관리](./sql-server-linux-manage-ssms.md)를 참조하세요.

   >[!NOTE]
   >[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)]([CU18](https://support.microsoft.com/help/4527377)) 이상에서는 SQL Server on Linux 인스턴스의 SQL Server 복제를 지원합니다.

## <a name="detailed-steps"></a>자세한 단계

1. Linux에서 SQL Server 복제 에이전트를 사용하도록 설정합니다. 두 호스트 머신의 터미널에서 다음 명령을 실행합니다. 

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   sudo systemctl restart mssql-server
   ```

1. 샘플 데이터베이스 및 테이블을 만듭니다. 게시자에서 게시할 아티클 역할을 하는 샘플 데이터베이스 및 테이블을 만듭니다.

   ```sql
   CREATE DATABASE Sales
   GO
   USE [SALES]
   GO 
   CREATE TABLE CUSTOMER([CustomerID] [int] NOT NULL, [SalesAmount] [decimal] NOT NULL)
   GO 
   INSERT INTO CUSTOMER (CustomerID, SalesAmount) VALUES (1,100),(2,200),(3,300)
   ```

   다른 SQL Server 인스턴스인 구독자에서 아티클을 받을 데이터베이스를 만듭니다.

   ```sql
   CREATE DATABASE Sales
   GO
   ```

1. SQL Server 에이전트가 배포자에서 읽고 쓰는 스냅샷 폴더를 만들고, 스냅샷 폴더를 만들고 ‘mssql’ 사용자에게 액세스 권한을 부여합니다. 

   ```bash
   sudo mkdir /var/opt/mssql/data/ReplData/
   sudo chown mssql /var/opt/mssql/data/ReplData/
   sudo chgrp mssql /var/opt/mssql/data/ReplData/
   ```

1. 배포자를 구성합니다. 이 예에서는 게시자도 배포자가 됩니다. 게시자에서 다음 명령을 실행하여 배포용 인스턴스도 구성합니다.

   ```sql
   DECLARE @distributor AS sysname
   DECLARE @distributorlogin AS sysname
   DECLARE @distributorpassword AS sysname
   -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
   SET @distributor = N'<distributor instance name>'--in this example, it will be the name of the publisher
   SET @distributorlogin = N'<distributor login>'
   SET @distributorpassword = N'<distributor password>'
   -- Specify the distribution database. 
   
   use master
   exec sp_adddistributor @distributor = @distributor -- this should be the hostname

   -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
   exec sp_adddistributiondb @database = N'distribution', @log_file_size = 2, @deletebatchsize_xact = 5000, @deletebatchsize_cmd = 2000, @security_mode = 0, @login = @distributorlogin, @password = @distributorpassword
   GO

   DECLARE @snapshotdirectory AS nvarchar(500)
   SET @snapshotdirectory = N'/var/opt/mssql/data/ReplData/'

   -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
   use [distribution] 
   if (not exists (select * from sysobjects where name = 'UIProperties' and type = 'U ')) 
          create table UIProperties(id int) 
   if (exists (select * from ::fn_listextendedproperty('SnapshotFolder', 'user', 'dbo', 'table', 'UIProperties', null, null))) 
          EXEC sp_updateextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties' 
   else 
         EXEC sp_addextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties'
   GO
   ```

1. 게시자를 구성합니다. 게시자에서 다음 TSQL 명령을 실행합니다.

   ```sql
   DECLARE @publisher AS sysname
   DECLARE @distributorlogin AS sysname
   DECLARE @distributorpassword AS sysname
   -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
   SET @publisher = N'<instance name>' 
   SET @distributorlogin = N'<distributor login>'
   SET @distributorpassword = N'<distributor password>'
   -- Specify the distribution database. 

   -- Adding the distribution publishers
   exec sp_adddistpublisher @publisher = @publisher, 
   @distribution_db = N'distribution', 
   @security_mode = 0, 
   @login = @distributorlogin, 
   @password = @distributorpassword, 
   @working_directory = N'/var/opt/mssql/data/ReplData', 
   @trusted = N'false', 
   @thirdparty_flag = 0, 
   @publisher_type = N'MSSQLSERVER'
   GO
   ```

1. 게시 작업을 구성합니다. 게시자에서 다음 TSQL 명령을 실행합니다.

   ```sql
   DECLARE @replicationdb AS sysname
   DECLARE @publisherlogin AS sysname
   DECLARE @publisherpassword AS sysname
   SET @replicationdb = N'Sales'
   SET @publisherlogin = N'<Publisher login>'
   SET @publisherpassword = N'<Publisher Password>'

   use [Sales]
   exec sp_replicationdboption @dbname = N'Sales', @optname = N'publish', @value = N'true'
   
   -- Add the snapshot publication
   exec sp_addpublication 
   @publication = N'SnapshotRepl', 
   @description = N'Snapshot publication of database ''Sales'' from Publisher ''<PUBLISHER HOSTNAME>''.',
   @retention = 0, 
   @allow_push = N'true', 
   @repl_freq = N'snapshot', 
   @status = N'active', 
   @independent_agent = N'true'

   exec sp_addpublication_snapshot @publication = N'SnapshotRepl', 
   @frequency_type = 1, 
   @frequency_interval = 1, 
   @frequency_relative_interval = 1, 
   @frequency_recurrence_factor = 0, 
   @frequency_subday = 8, 
   @frequency_subday_interval = 1, 
   @active_start_time_of_day = 0,
   @active_end_time_of_day = 235959, 
   @active_start_date = 0, 
   @active_end_date = 0, 
   @publisher_security_mode = 0, 
   @publisher_login = @publisherlogin, 
   @publisher_password = @publisherpassword
   ```

1. sales 테이블에서 아티클 만들기 - 게시자에서 다음 TSQL 명령을 실행합니다.

   ```sql
   use [Sales]
   exec sp_addarticle 
   @publication = N'SnapshotRepl', 
   @article = N'customer', 
   @source_owner = N'dbo', 
   @source_object = N'customer', 
   @type = N'logbased', 
   @description = null, 
   @creation_script = null, 
   @pre_creation_cmd = N'drop', 
   @schema_option = 0x000000000803509D,
   @identityrangemanagementoption = N'manual', 
   @destination_table = N'customer', 
   @destination_owner = N'dbo', 
   @vertical_partition = N'false'
   ```

1. 구독을 구성합니다. 게시자에서 다음 TSQL 명령을 실행합니다.

   ```sql
   DECLARE @subscriber AS sysname
   DECLARE @subscriber_db AS sysname
   DECLARE @subscriberLogin AS sysname
   DECLARE @subscriberPassword AS sysname
   SET @subscriber = N'<Instance Name>' -- for example, MSSQLSERVER
   SET @subscriber_db = N'Sales'
   SET @subscriberLogin = N'<Subscriber Login>'
   SET @subscriberPassword = N'<Subscriber Password>'

   use [Sales]
   exec sp_addsubscription 
   @publication = N'SnapshotRepl', 
   @subscriber = @subscriber,
   @destination_db = @subscriber_db, 
   @subscription_type = N'Push', 
   @sync_type = N'automatic', 
   @article = N'all', 
   @update_mode = N'read only', 
   @subscriber_type = 0

   exec sp_addpushsubscription_agent 
   @publication = N'SnapshotRepl', 
   @subscriber = @subscriber,
   @subscriber_db = @subscriber_db, 
   @subscriber_security_mode = 0, 
   @subscriber_login = @subscriberLogin,
   @subscriber_password = @subscriberPassword,
   @frequency_type = 1,
   @frequency_interval = 0, 
   @frequency_relative_interval = 0, 
   @frequency_recurrence_factor = 0, 
   @frequency_subday = 0, 
   @frequency_subday_interval = 0, 
   @active_start_time_of_day = 0, 
   @active_end_time_of_day = 0, 
   @active_start_date = 0, 
   @active_end_date = 19950101
   GO
   ```

1. 복제 에이전트 작업을 실행합니다. 다음 쿼리를 실행하여 작업 목록을 가져옵니다.

   ```sql
   SELECT name, date_modified FROM msdb.dbo.sysjobs order by date_modified desc
   ```

   스냅샷 복제 작업을 실행하여 스냅샷을 생성합니다.

   ```sql
   USE msdb;   
   --generate snapshot of publications, for example
   EXEC dbo.sp_start_job N'PUBLISHER-PUBLICATION-SnapshotRepl-1'
   GO
   ```

   스냅샷 복제 작업을 실행하여 스냅샷을 생성합니다.

   ```sql
   USE msdb;
   --distribute the publication to subscriber, for example
   EXEC dbo.sp_start_job N'DISTRIBUTOR-PUBLICATION-SnapshotRepl-SUBSCRIBER'
   GO
   ```

1. 구독자를 연결하고 복제된 데이터를 쿼리합니다.    

   구독자에서 다음 쿼리를 실행하여 복제가 작동하는지 확인합니다.

   ```sql
   SELECT * from [Sales].[dbo].[CUSTOMER]
   ```

이 자습서에서는 Transact-SQL을 사용하여 Linux에서 두 개의 SQL Server 인스턴스로 SQL Server 스냅샷 복제를 구성합니다.

> [!div class="checklist"]
> * Linux에서 SQL Server 복제 에이전트 사용
> * 예제 데이터베이스 만들기
> * SQL Server 에이전트 액세스를 위해 스냅샷 폴더 구성
> * 배포자 구성
> * 게시자 구성
> * 게시 및 아티클 구성
> * 구독자 구성 
> * 복제 작업 실행

## <a name="see-also"></a>참고 항목

복제에 대한 자세한 내용은 [SQL Server 복제 설명서](../relational-databases/replication/sql-server-replication.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

[개념: Linux의 SQL Server 복제](sql-server-linux-replication.md)

[복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)
