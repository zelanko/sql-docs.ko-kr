---
title: Linux에서 SQL Server 복제 구성
description: 이 자습서에는 Linux에서 SQL Server 스냅숏 복제를 구성 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cd0c2f2463abdc124f32d88fa9bd877c47a2fb76
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834747"
---
# <a name="configure-replication-with-t-sql"></a>T-SQL을 사용 하 여 복제를 구성 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)] 

이 자습서에서는 TRANSACT-SQL을 사용 하 여 SQL Server의 두 인스턴스를 사용 하 여 Linux에서 SQL Server 스냅숏 복제를 구성 합니다. 게시자 및 배포자 동일한 인스턴스에 되며 구독자는 별도 인스턴스에서 됩니다.

> [!div class="checklist"]
> * Linux의 SQL Server 복제 에이전트를 사용 하도록 설정
> * 예제 데이터베이스 만들기
> * SQL Server 에이전트 액세스에 대 한 스냅숏 폴더를 구성 합니다.
> * 배포자 구성
> * 게시자 구성
> * 게시 및 아티클 구성
> * 구독자를 구성 합니다. 
> * 복제 작업 실행

모든 복제 구성을 사용 하 여 구성할 수 있습니다 [복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)합니다.

## <a name="prerequisites"></a>사전 요구 사항  
이 자습서를 완료 하려면 해야 합니다.

- Linux에서 SQL Server의 최신 버전을 사용 하 여 SQL Server의 두 인스턴스
- 쿼리를 실행할 T-SQL SQLCMD 또는 SSMS와 같은 복제를 설정 하는 도구

  참조 [SSMS를 사용 하 여 Linux의 SQL Server 관리](./sql-server-linux-manage-ssms.md)합니다.

## <a name="detailed-steps"></a>자세한 단계

1. 복제 에이전트를 사용 하려면 SQL Server 에이전트를 사용 하도록 설정 Linux에서 SQL Server 복제 에이전트를 사용 하도록 설정 합니다. 두 호스트 컴퓨터에서 터미널에서 다음 명령을 실행 합니다. 

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  sudo systemctl restart mssql-server
  ```

1. 예제 데이터베이스 및 테이블 게시자 만들기 예제 데이터베이스 및 게시에 대 한 아티클로 할 테이블을 만듭니다.

  ```sql
  CREATE DATABASE Sales
  GO
  USE [SALES]
  GO 
  CREATE TABLE CUSTOMER([CustomerID] [int] NOT NULL, [SalesAmount] [decimal] NOT NULL)
  GO 
  INSERT INTO CUSTOMER (CustomerID, SalesAmount) VALUES (1,100),(2,200),(3,300)
  ```

  다른 SQL Server 인스턴스의 구독자 문서를 수신 하도록 데이터베이스를 만듭니다.

  ```sql
  CREATE DATABASE Sales
  GO
  ```

1. 읽기/쓰기로 배포자에서 스냅숏 폴더를 만들고 'mssql' 사용자에 게 액세스 권한을 부여 하려면 SQL Server 에이전트에 대 한 스냅숏 폴더 만들기 

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

1. 이 예제에서 배포자를 구성, 배포자는 게시자가 될 수도 있습니다. 도 배포에 대 한 인스턴스를 구성 하려면 게시자에서 다음 명령을 실행 합니다.

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

1. 게시자에서 다음 TSQL 명령을 실행 하는 게시자를 구성 합니다.

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

1. 게시자에서 게시 작업을 실행한 다음 TSQL 명령의 구성 합니다.

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

1. 문서를 만들 실행 sales 테이블에서 다음 TSQL 명령을 게시자에서.

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

1. 구독 실행 구성 다음 TSQL 명령을 게시자에서 합니다.

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
  @subscriber_login =  @subscriberLogin,
  @subscriber_password =  @subscriberPassword,
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

1. 복제 에이전트 작업 실행

  작업의 목록을 가져오려면 다음 쿼리를 실행 합니다.

  ```sql
  SELECT name, date_modified FROM msdb.dbo.sysjobs order by date_modified desc
  ```

  스냅숏을 생성 하려면 스냅숏 복제 작업을 실행 합니다.

  ```sql
  USE msdb;  
  --generate snapshot of publications, for example
  EXEC dbo.sp_start_job N'PUBLISHER-PUBLICATION-SnapshotRepl-1'
  GO
  ```

  스냅숏을 생성 하려면 스냅숏 복제 작업을 실행 합니다.

  ```sql
  USE msdb;  
  --distribute the publication to subscriber, for example
  EXEC dbo.sp_start_job N'DISTRIBUTOR-PUBLICATION-SnapshotRepl-SUBSCRIBER'
  GO
  ```

1. 구독자를 연결 하 고 복제 된 데이터를 쿼리 합니다. 

  구독자에서 복제는 다음 쿼리를 실행 하 여 작동 하는지 확인 합니다.

  ```sql
  SELECT * from [Sales].[dbo].[CUSTOMER]
  ```

이 자습서에서는 TRANSACT-SQL을 사용 하 여 SQL Server의 두 인스턴스를 사용 하 여 Linux에서 SQL Server 스냅숏 복제를 구성 합니다.

> [!div class="checklist"]
> * Linux의 SQL Server 복제 에이전트를 사용 하도록 설정
> * 예제 데이터베이스 만들기
> * SQL Server 에이전트 액세스에 대 한 스냅숏 폴더를 구성 합니다.
> * 배포자 구성
> * 게시자 구성
> * 게시 및 아티클 구성
> * 구독자를 구성 합니다. 
> * 복제 작업 실행

## <a name="see-also"></a>참조

복제에 대 한 자세한 내용은 [SQL Server 복제 설명서](../relational-databases/replication/sql-server-replication.md)합니다.

## <a name="next-steps"></a>다음 단계

[개념: Linux에서 SQL Server 복제](sql-server-linux-replication.md)

[복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)합니다.
