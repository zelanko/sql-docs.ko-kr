---
title: 복제 시스템 저장 프로시저 개념 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server replication], programming
- programming [SQL Server replication], system stored procedures
- programming interfaces [SQL Server replication]
- system stored procedures [SQL Server replication]
- replication [SQL Server], how-to topics
ms.assetid: 816d2bda-ed72-43ec-aa4d-7ee3dc25fd8a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2387a1ffa414feae48c52bbfcdcfc5a104e9ffe8
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914720"
---
# <a name="replication-system-stored-procedures-concepts"></a>Replication System Stored Procedures Concepts
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 복제 토폴로지의 사용자 구성 가능한 모든 기능에 대한 프로그래밍 방식 액세스는 시스템 저장 프로시저를 통해 제공됩니다. 저장 프로시저는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]나 sqlcmd 명령줄 유틸리티를 사용하여 개별적으로 실행할 수 있지만 복제 태스크의 논리적 시퀀스를 수행하기 위해 실행할 수 있는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트 파일을 작성하는 것이 효율적일 수 있습니다.  
  
 복제 태스크 스크립트를 작성하면 다음과 같은 이점이 있습니다.  
  
-   복제 토폴로지 배포에 사용한 단계의 영구 복사본을 유지할 수 있습니다.  
  
-   스크립트 하나로 여러 구독자를 구성할 수 있습니다.  
  
-   코드를 평가하고 이해하고 변경하거나 문제를 해결할 수 있게 하여 새로운 데이터베이스 관리자를 신속하게 교육할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  스크립트는 보안상 위험할 수 있습니다. 사용자 몰래 또는 사용자 개입 없이 시스템 함수를 호출할 수 있으며 보안 자격 증명을 일반 텍스트로 포함할 수도 있습니다. 스크립트를 사용하기 전에 스크립트에 보안 문제가 있는지 확인하십시오.  
  
## <a name="creating-replication-scripts"></a>복제 스크립트 만들기  
 복제의 관점에서 스크립트는 각 문이 복제 저장 프로시저를 실행하는 일련의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문입니다. 스크립트는 sqlcmd 유틸리티를 사용하여 실행할 수 있는 텍스트 파일로, 주로 .sql 파일 확장명을 사용합니다. 스크립트 파일을 실행하면 sqlcmd 유틸리티는 파일에 저장된 SQL 문을 실행합니다. 마찬가지로 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 프로젝트의 쿼리 개체로 스크립트를 저장할 수 있습니다.  
  
 복제 스크립트는 다음과 같은 방법으로 만들 수 있습니다.  
  
-   스크립트를 직접 만듭니다.  
  
-   복제 마법사에 제공되는 스크립트 생성 기능을 사용하거나  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]입니다. 자세한 내용은 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)을 참조하세요.  
  
-   RMO(복제 관리 개체)를 사용하여 RMO 개체를 만드는 스크립트를 프로그래밍 방식으로 생성합니다.  
  
 복제 스크립트를 직접 만들 경우에는 다음과 같은 사항을 고려해야 합니다.  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트에는 일괄 처리가 하나 이상 있습니다. GO 명령은 일괄 처리의 끝을 나타냅니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트에 GO 명령이 없으면 스크립트가 단일 일괄 처리로 실행됩니다.  
  
-   일괄 처리 하나에 복제 저장 프로시저를 여러 개 실행할 경우에는 첫 번째 프로시저 이후의 모든 프로시저 앞에 EXECUTE 키워드를 사용해야 합니다.  
  
-   일괄 처리에 포함된 모든 저장 프로시저가 컴파일되어야 일괄 처리가 실행됩니다. 그러나 일괄 처리가 컴파일되고 실행 계획이 작성된 후에는 런타임 오류가 발생하거나 발생하지 않을 수 있습니다.  
  
-   복제를 구성하는 스크립트를 만들 때는 스크립트 파일에 보안 자격 증명이 저장되지 않도록 Windows 인증을 사용하는 것이 좋습니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
## <a name="sample-replication-script"></a>복제 스크립트 예제  
 다음 스크립트를 실행하여 서버에 게시 및 배포를 설정할 수 있습니다.  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
 그런 다음 이 스크립트를 로컬에 `instdistpub.sql`로 저장하여 필요할 때 실행하거나 다시 실행할 수 있습니다.  
  
 위 스크립트에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 여러 복제 코드 예제에 사용된 **sqlcmd** 스크립팅 변수가 포함되어 있습니다. 스크립팅 변수는 `$(MyVariable)` 구문을 사용하여 정의되며 변수 값은 명령줄이나 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 스크립트에 전달할 수 있습니다. 자세한 내용은 이 항목의 다음 섹션인 "복제 스크립트 실행"을 참조하십시오.  
  
## <a name="executing-replication-scripts"></a>복제 스크립트 실행  
 복제 스크립트를 만든 후에는 다음 방법 중 하나로 실행할 수 있습니다.  
  
### <a name="creating-a-sql-query-file-in-sql-server-management-studio"></a>SQL Server Management Studio에서 SQL 쿼리 파일 만들기  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 프로젝트에서 SQL 쿼리 파일로 복제 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트 파일을 만들 수 있습니다. 스크립트를 작성하면 이 쿼리 파일에 대한 데이터베이스에 연결하여 스크립트를 실행할 수 있습니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 만드는 방법은 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)를 참조하세요.  
  
 스크립팅 변수가 포함된 스크립트를 사용하려면 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]가 **sqlcmd** 모드에서 실행 중이어야 합니다. **sqlcmd** 모드에서는 쿼리 편집기에서 **sqlcmd**와 관련된 추가적인 구문(예: 변수 값에 사용되는 `:setvar`)을 사용할 수 있습니다. **sqlcmd** 모드에 대한 자세한 내용은 [쿼리 편집기로 SQLCMD 스크립트 편집](../../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)을 참조하세요. 다음 스크립트에서는 `:setvar`를 사용하여 `$(DistPubServer)` 변수의 값을 제공합니다.  
  
```  
:setvar DistPubServer N'MyPublisherAndDistributor';  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
--  
-- Additional code goes here  
--  
```  
  
### <a name="using-the-sqlcmd-utility-from-the-command-line"></a>명령줄에서 sqlcmd 유틸리티 사용  
 다음 예제에서는 명령줄에서 [sqlcmd 유틸리티](../../../tools/sqlcmd-utility.md)를 사용하여 `instdistpub.sql` 스크립트 파일을 실행하는 방법을 보여 줍니다.  
  
```  
sqlcmd.exe -E -S sqlserverinstance -i C:\instdistpub.sql -o C:\output.log -v DistPubServer="N'MyDistributorAndPublisher'"  
```  
  
 이 예에서 `-E` 스위치는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 Windows 인증을 사용함을 나타냅니다. Windows 인증을 사용하면 스크립트 파일에 사용자 이름과 암호를 저장하지 않아도 됩니다. 스크립트 파일의 경로와 이름은 `-i` 스위치로 지정하고 출력 파일의 이름은 `-o` 스위치(이 스위치를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 출력이 콘솔 대신 이 파일에 작성됨)로 지정합니다. `sqlcmd` 유틸리티를 사용하면 `-v` 스위치를 사용하여 런타임에 스크립팅 변수를 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트에 전달할 수 있습니다. 이 예제에서 `sqlcmd`는 실행되기 전에 스크립트에서 `$(DistPubServer)`의 모든 인스턴스를 `N'MyDistributorAndPublisher'` 값으로 바꿉니다.  
  
> [!NOTE]  
>  `-X` 스위치는 스크립팅 변수를 사용하지 않도록 설정합니다.  
  
### <a name="automating-tasks-in-a-batch-file"></a>배치 파일로 태스크 자동화  
 배치 파일을 사용하면 복제 관리 태스크, 복제 동기화 태스크 및 기타 태스크를 이 배치 파일에서 자동화할 수 있습니다. 다음 배치 파일은 **sqlcmd** 유틸리티를 사용하여 구독 데이터베이스를 삭제한 후 다시 만들고 병합 끌어오기 구독을 추가합니다. 그런 다음 이 파일은 병합 에이전트를 호출하여 새 구독을 동기화합니다.  
  
```  
REM ----------------------Script to synchronize merge subscription ----------------------  
REM -- Creates subscription database and   
REM -- synchronizes the subscription to MergeSalesPerson.  
REM -- Current computer acts as both Publisher and Subscriber.  
REM -------------------------------------------------------------------------------------  
  
SET Publisher=%computername%  
SET Subscriber=%computername%  
SET PubDb=AdventureWorks  
SET SubDb=AdventureWorksReplica  
SET PubName=AdvWorksSalesOrdersMerge  
  
REM -- Drop and recreate the subscription database at the Subscriber  
sqlcmd /S%Subscriber% /E /Q"USE master IF EXISTS (SELECT * FROM sysdatabases WHERE name='%SubDb%' ) DROP DATABASE %SubDb%"  
sqlcmd /S%Subscriber% /E /Q"USE master CREATE DATABASE %SubDb%"  
  
REM -- Add a pull subscription at the Subscriber  
sqlcmd /S%Subscriber% /E /Q"USE %SubDb% EXEC sp_addmergepullsubscription @publisher = %Publisher%, @publication = %PubName%, @publisher_db = %PubDb%"  
sqlcmd /S%Subscriber% /E /Q"USE %SubDb%  EXEC sp_addmergepullsubscription_agent @publisher = %Publisher%, @publisher_db = %PubDb%, @publication = %PubName%, @subscriber = %Subscriber%, @subscriber_db = %SubDb%, @distributor = %Publisher%"  
  
REM -- This batch file starts the merge agent at the Subscriber to   
REM -- synchronize a pull subscription to a merge publication.  
REM -- The following must be supplied on one line.  
"\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE"  -Publisher  %Publisher% -Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB  %PubDb% -SubscriberDB %SubDb% -Publication %PubName% -PublisherSecurityMode 1 -OutputVerboseLevel 1  -Output  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1 -Validate 3  
  
```  
  
## <a name="scripting-common-replication-tasks"></a>일반적인 복제 태스크 스크립팅  
 다음은 시스템 저장 프로시저를 사용하여 스크립트로 작성할 수 있는 가장 일반적인 복제 태스크입니다.  
  
-   게시 및 배포 구성  
  
-   게시자 및 배포자 속성 수정  
  
-   게시 및 배포 해제  
  
-   게시 만들기 및 아티클 정의  
  
-   게시 및 아티클 삭제  
  
-   끌어오기 구독 만들기  
  
-   끌어오기 구독 수정  
  
-   끌어오기 구독 삭제  
  
-   밀어넣기 구독 만들기  
  
-   밀어넣기 구독 수정  
  
-   밀어넣기 구독 삭제  
  
-   끌어오기 구독 동기화  
  
## <a name="see-also"></a>참고 항목  
 [복제 프로그래밍 개념](../../../relational-databases/replication/concepts/replication-programming-concepts.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [복제 스크립팅](../../../relational-databases/replication/scripting-replication.md)  
  
  
