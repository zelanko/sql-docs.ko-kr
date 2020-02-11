---
title: 가용성 그룹 만들기(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: 8b0a6301-8b79-4415-b608-b40876f30066
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7b09bb2f08095af33f80fe4161032036482f835
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75228788"
---
# <a name="create-an-availability-group-transact-sql"></a>가용성 그룹 만들기(Transact-SQL)
  이 항목에서는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 기능이 설정된 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 인스턴스에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용하여 가용성 그룹을 만들고 구성하는 방법을 설명합니다. 
  *가용성 그룹* 은 단일 단위로 장애 조치(Failover)될 사용자 데이터베이스 집합과 장애 조치(Failover)를 지원하는 장애 조치(Failover) 파트너 집합( *가용성 복제본*이라고 함)을 정의합니다.  
  
> [!NOTE]  
>  가용성 그룹에 대한 소개는 [AlwaysOn 가용성 그룹 개요&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.  

> [!NOTE]  
>  
  [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하는 대신 가용성 그룹 만들기 마법사나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell cmdlet을 사용할 수도 있습니다. 자세한 내용은 [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md), [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)또는 [가용성 그룹 만들기&#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)를 참조하세요.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 가용성 그룹을 처음 만들어 보는 경우 이 섹션을 먼저 읽는 것이 좋습니다.  
  
###  <a name="PrerequisitesRestrictions"></a>사전 요구 사항, 제한 사항 및 권장 사항  
  
-   가용성 그룹을 만들기 전에 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 동일한 WSFC 장애 조치(Failover) 클러스터 내의 다른 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에 있는지 확인합니다. 또한 각 서버 인스턴스가 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 기타 모든 필수 구성 요소를 충족하는지도 확인합니다. 자세한 내용은 [AlwaysOn 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
###  <a name="SummaryTsqlStatements"></a>태스크 및 해당 Transact-sql 문 요약  
 다음 표에서는 가용성 그룹을 만들고 구성하는 데 필요한 기본 태스크와 이러한 태스크에 사용할 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 보여 줍니다. 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 태스크는 표에 나오는 순서대로 수행해야 합니다.  
  
|Task|Transact-SQL 문|태스크를 수행할 위치**<sup>*</sup>**|  
|----------|----------------------------------|-------------------------------------------|  
|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스당 하나의 데이터베이스 미러링 엔드포인트 만들기|[끝점 만들기](/sql/t-sql/statements/create-endpoint-transact-sql) *endpointName* ... DATABASE_MIRRORING|데이터베이스 미러링 엔드포인트가 없는 각 서버 인스턴스에서 실행합니다.|  
|가용성 그룹 만들기|[CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)|초기 주 복제본을 호스트할 서버 인스턴스에서 실행합니다.|  
|가용성 그룹에 보조 복제본 조인|[ALTER AVAILABILITY GROUP](join-a-secondary-replica-to-an-availability-group-sql-server.md) *group_name* JOIN|보조 복제본을 호스팅하는 각 서버 인스턴스에서 실행합니다.|  
|보조 데이터베이스 준비|[백업](/sql/t-sql/statements/backup-transact-sql) 및 [복원](/sql/t-sql/statements/restore-statements-transact-sql).|주 복제본을 호스트하는 서버 인스턴스에 백업을 만듭니다.<br /><br /> RESTORE WITH NORECOVERY를 사용하여 보조 복제본을 호스팅하는 각 서버 인스턴스에 백업을 복원합니다.|  
|가용성 그룹에 각 보조 데이터베이스를 조인하여 데이터 동기화 시작|[ALTER database](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) *DATABASE_NAME* SET HADR AVAILABILITY GROUP = *group_name*|보조 복제본을 호스팅하는 각 서버 인스턴스에서 실행합니다.|  
  
 **<sup>*</sup>** 지정 된 태스크를 수행 하려면 표시 된 서버 인스턴스에 연결 합니다.  
  
##  <a name="TsqlProcedure"></a>Transact-sql을 사용 하 여 가용성 그룹 만들기 및 구성  
  
> [!NOTE]  
>  이러한 각 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문의 코드 예가 포함된 샘플 구성 프로시저는 [예: Windows 인증을 사용하는 가용성 그룹 구성](#ExampleConfigAGWinAuth)을 참조하세요.  
  
1.  주 복제본을 호스팅할 서버 인스턴스에 연결합니다.  
  
2.  [Create availability group](/sql/t-sql/statements/create-availability-group-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용 하 여 가용성 그룹을 만듭니다.  
  
3.  새 보조 복제본을 가용성 그룹에 조인합니다. 자세한 내용은 [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)를 참조하세요.  
  
4.  가용성 그룹의 각 데이터베이스에 대해 RESTORE WITH NORECOVERY를 사용하여 주 데이터베이스의 최신 백업을 복원하는 방법으로 보조 데이터베이스를 만듭니다. 자세한 내용은 [예: Windows 인증을 사용하여 가용성 그룹 설정(Transact-SQL)](create-an-availability-group-transact-sql.md)에서 데이터베이스 백업을 복원하는 단계부터 참조하세요.  
  
5.  모든 새 보조 데이터베이스를 가용성 그룹에 조인합니다. 자세한 내용은 [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)를 참조하세요.  
  
##  <a name="ExampleConfigAGWinAuth"></a>예: Windows 인증을 사용 하는 가용성 그룹 구성  
 이 예에서 만드는 예제 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 구성 프로시저는 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 Windows 인증을 사용하는 데이터베이스 미러링 엔드포인트를 설정하고, 가용성 그룹과 해당 보조 데이터베이스를 만들고 구성합니다.  
  
 이 예에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [샘플 구성 프로시저를 사용 하기 위한 필수 구성 요소](#PrerequisitesForExample)  
  
-   [샘플 구성 프로시저](#SampleProcedure)  
  
-   [예제 구성 프로시저에 대 한 전체 코드 예제](#CompleteCodeExample)  
  
###  <a name="PrerequisitesForExample"></a>샘플 구성 프로시저를 사용 하기 위한 필수 구성 요소  
 이 예제 프로시저에 대한 요구 사항은 다음과 같습니다.  
  
-   서버 인스턴스에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원해야 합니다. 자세한 내용은 [AlwaysOn 가용성 그룹 &#40;SQL Server&#41;에 대 한 필수 조건, 제한 사항 및 권장 사항 ](prereqs-restrictions-recommendations-always-on-availability.md)을 참조 하세요.  
  
-   두 예제 데이터베이스 *MyDb1* 및 *MyDb2*는 주 복제본을 호스팅할 서버 인스턴스에 있어야 합니다. 다음 코드 예에서는 이러한 두 데이터베이스를 만들고 구성하며 각 데이터베이스의 전체 백업을 만듭니다. 예제 가용성 그룹을 만들려는 서버 인스턴스에서 이러한 코드 예를 실행합니다. 이 서버 인스턴스는 예제 가용성 그룹의 초기 주 복제본을 호스팅합니다.  
  
    1.  다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 예에서는 이러한 데이터베이스를 만든 다음 전체 복구 모델을 사용하도록 데이터베이스를 변경합니다.  
  
        ```sql
        -- Create sample databases:  
        CREATE DATABASE MyDb1;  
        GO  
        ALTER DATABASE MyDb1 SET RECOVERY FULL;  
        GO  
  
        CREATE DATABASE MyDb2;  
        GO  
        ALTER DATABASE MyDb2 SET RECOVERY FULL;  
        GO  
        ```  
  
    2.  다음 코드 예제에서는 *MyDb1* 및 *MyDb2*의 전체 데이터베이스 백업을 만듭니다. 이 코드 예제에서는 가상의 백업 공유 \\ \\ *FILESERVER*\\*sqlbackups*을 사용 합니다.  
  
        ```sql
        -- Backup sample databases:  
        BACKUP DATABASE MyDb1   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
            WITH FORMAT  
        GO  
  
        BACKUP DATABASE MyDb2   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
            WITH FORMAT  
        GO
        ```  
  
###  <a name="SampleProcedure"></a> 예제 구성 프로시저  
 이 예제 구성에서는 서비스 계정이 다르지만 트러스트된 도메인 계정(`DOMAIN1` 및 `DOMAIN2`)으로 실행되는 두 개의 독립 실행형 서버 인스턴스에 가용성 복제본이 만들어집니다.  
  
 다음 표에는 이 예제 구성에 사용된 값이 요약되어 있습니다.  
  
|초기 역할|시스템|호스트 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스|  
|------------------|------------|---------------------------------------------|  
|주|`COMPUTER01`|`AgHostInstance`|  
|보조|`COMPUTER02`|기본 인스턴스입니다.|  
  
1.  가용성 그룹을 만들 서버 인스턴스( *에 있는* 라는 인스턴스)에 `AgHostInstance` dbm_endpoint `COMPUTER01`라는 데이터베이스 미러링 엔드포인트를 만듭니다. 이 엔드포인트는 포트 7022를 사용합니다. 가용성 그룹을 만드는 서버 인스턴스는 주 복제본을 호스팅합니다.  
  
    ```sql
    -- Create endpoint on server instance that hosts the primary replica:  
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO
    ```  
  
2.  보조 복제본을 호스트할 서버 인스턴스( *에 있는 기본 서버 인스턴스)에* dbm_endpoint `COMPUTER02`라는 엔드포인트를 만듭니다. 이 엔드포인트는 포트 5022를 사용합니다.  
  
    ```sql
    -- Create endpoint on server instance that hosts the secondary replica:   
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=5022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO
    ```  
  
3.  > [!NOTE]  
    >  가용성 복제본을 호스팅할 서버 인스턴스의 서비스 계정이 동일한 도메인 계정으로 실행되는 경우에는 이 단계가 필요하지 않습니다. 이 단계를 생략하고 다음 단계로 직접 이동합니다.  
  
     서버 인스턴스의 서비스 계정이 다른 도메인 사용자로 실행되는 경우에는 각 서버 인스턴스에서 다른 서버 인스턴스에 대한 로그인을 만들고 로컬 데이터베이스 미러링 엔드포인트에 액세스할 수 있는 권한을 이 로그인에 부여합니다.  
  
     다음 코드 예에서는 로그인을 만들고 이 로그인에 엔드포인트에 대한 사용 권한을 부여하기 위한 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 보여 줍니다. 여기에서 원격 서버 인스턴스의 도메인 계정은 *domain_name*\\*user_name*으로 표시됩니다.  
  
    ```sql
    -- If necessary, create a login for the service account, domain_name\user_name  
    -- of the server instance that will host the other replica:  
    USE master;  
    GO  
    CREATE LOGIN [domain_name\user_name] FROM WINDOWS;  
    GO  
    -- And Grant this login connect permissions on the endpoint:  
    GRANT CONNECT ON ENDPOINT::dbm_endpoint   
       TO [domain_name\user_name];  
    GO  
    ```  
  
4.  사용자 데이터베이스가 있는 서버 인스턴스에서 가용성 그룹을 만듭니다.  
  
     다음 코드 예제에서는 *MyDb1* 및 *MyDb2* 라는 샘플 데이터베이스가 만들어진 서버 인스턴스에 *MyAG*라는 가용성 그룹을 만듭니다. `AgHostInstance`COMPUTER01 *에 있는 로컬 서버 인스턴스* 가 먼저 지정됩니다. 이 인스턴스는 초기 주 복제본을 호스팅합니다. *COMPUTER02*에 기본 서버 인스턴스인 원격 서버 인스턴스가 보조 복제본을 호스트하도록 지정됩니다. 두 가용성 복제본 모두 수동 장애 조치와 함께 비동기 커밋 모드를 사용하도록 구성됩니다. 비동기 커밋 복제본에 대한 수동 장애 조치는 데이터 손실이 가능한 강제 장애 조치를 의미합니다.  
  
    ```sql
    -- Create the availability group, MyAG:   
    CREATE AVAILABILITY GROUP MyAG   
       FOR   
          DATABASE MyDB1, MyDB2   
       REPLICA ON   
          'COMPUTER01\AgHostInstance' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',   
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             ),  
          'COMPUTER02' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );   
    GO  
    ```  
  
     가용성 그룹을 만드는 다른 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 코드 샘플을 보려면 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)을 참조하세요.  
  
5.  보조 복제본을 호스팅하는 서버 인스턴스에서 보조 복제본을 가용성 그룹에 조인합니다.  
  
     다음 코드 예에서는 `COMPUTER02` 의 보조 복제본을 `MyAG` 가용성 그룹에 조인합니다.  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- join the secondary replica to the availability group:  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    GO  
    ```  
  
6.  보조 복제본을 호스팅하는 서버 인스턴스에서 보조 데이터베이스를 만듭니다.  
  
     다음 코드 예제에서는 RESTORE WITH NORECOVERY를 사용하여 데이터베이스 백업을 복원하는 방법으로 *MyDb1* 및 *MyDb2* 보조 데이터베이스를 만듭니다.  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- Restore database backups using the WITH NORECOVERY option:  
    RESTORE DATABASE MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NORECOVERY  
    GO  
  
    RESTORE DATABASE MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH NORECOVERY  
    GO
    ```  
  
7.  주 복제본을 호스팅하는 서버 인스턴스에서 각 주 데이터베이스의 트랜잭션 로그를 백업합니다.  
  
    > [!IMPORTANT]  
    >  실제 가용성 그룹을 구성할 때는 해당 보조 데이터베이스를 가용성 그룹에 조인한 후에 주 데이터베이스에 대한 로그 백업 태스크를 수행하는 것이 좋습니다.  
  
     다음 코드 예에서는 MyDb1 및 MyDb2에 트랜잭션 로그 백업을 만듭니다.  
  
    ```sql
    -- On the server instance that hosts the primary replica,   
    -- Backup the transaction log on each primary database:  
    BACKUP LOG MyDb1   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NOFORMAT  
    GO  
  
    BACKUP LOG MyDb2   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITHNOFORMAT  
    GO
    ```  
  
    > [!TIP]  
    >  일반적으로 로그 백업은 각 주 데이터베이스에서 만든 다음 WITH NORECOVERY를 사용하여 해당하는 보조 데이터베이스에 복원해야 합니다. 그러나 데이터베이스를 방금 만들었으며 아직 로그 백업을 만들지 않았거나 복구 모델이 방금 SIMPLE에서 FULL로 변경된 경우에는 이 로그 백업이 필요하지 않을 수도 있습니다.  
  
8.  보조 복제본을 호스팅하는 서버 인스턴스에서 보조 데이터베이스에 로그 백업을 적용합니다.  
  
     다음 코드 예제에서는 RESTORE WITH NORECOVERY를 사용하여 데이터베이스 백업을 복원하는 방법으로 *MyDb1* 및 *MyDb2* 보조 데이터베이스에 백업을 적용합니다.  
  
    > [!IMPORTANT]  
    >  실제 보조 데이터베이스를 준비할 때는 처음부터 항상 RESTORE WITH NORECOVERY를 사용하여 보조 데이터베이스를 만들 때 사용한 데이터베이스 백업보다 나중에 만들어진 모든 로그 백업을 적용해야 합니다. 물론, 전체 데이터베이스 백업과 차등 데이터베이스 백업을 모두 복원하는 경우에는 차등 백업 이후에 만들어진 로그 백업만 적용하면 됩니다.  
  
    ```sql
    -- Restore the transaction log on each secondary database,  
    -- using the WITH NORECOVERY option:  
    RESTORE LOG MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    RESTORE LOG MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
9. 보조 복제본을 호스팅하는 서버 인스턴스에서 새 보조 데이터베이스를 가용성 그룹에 조인합니다.  
  
     다음 코드 예제에서는 *MyDb1* 보조 데이터베이스를 조인한 다음 *MyDb2* 보조 데이터베이스를 *MyAG* 가용성 그룹에 조인합니다.  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- join each secondary database to the availability group:  
    ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
    GO  
  
    ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
    GO
    ```  
  
###  <a name="CompleteCodeExample"></a> 예제 구성 프로시저에 대한 전체 코드 예  
 다음 예에서는 예제 구성 프로시저의 모든 단계에 포함된 코드 예를 병합합니다. 다음 표에는 이 코드 예에 사용된 자리 표시자 값이 요약되어 있습니다. 이 코드 예의 단계에 대한 자세한 내용은 이 항목 윗부분의 [예제 구성 프로시저를 사용하기 위한 사전 요구 사항](#PrerequisitesForExample) 및 [예제 구성 프로시저](#SampleProcedure)를 참조하세요.  
  
|자리 표시자|Description|  
|-----------------|-----------------|  
|\\\\*FILESERVER*\\*SQLbackups*|가상의 백업 공유입니다.|  
|\\\\*FILESERVER*\\*SQLbackups\MyDb1.bak*|MyDb1의 백업 파일입니다.|  
|\\\\*FILESERVER*\\*SQLbackups\MyDb2.bak*|MyDb2의 백업 파일입니다.|  
|*7022*|각 데이터베이스 미러링 엔드포인트에 할당된 포트 번호입니다.|  
|*COMPUTER01\AgHostInstance*|초기 주 복제본을 호스팅하는 서버 인스턴스입니다.|  
|*COMPUTER02*|초기 보조 복제본을 호스팅하는 서버 인스턴스입니다. 이 인스턴스는 `COMPUTER02`의 기본 서버 인스턴스입니다.|  
|*에 있는*|각 데이터베이스 미러링 엔드포인트에 지정된 이름입니다.|  
|*MyDb1*|예제 가용성 그룹의 이름입니다.|  
|*MyDb1*|첫 번째 예제 데이터베이스의 이름입니다.|  
|*MyDb2*|두 번째 예제 데이터베이스의 이름입니다.|  
|*DOMAIN1\user1*|초기 주 복제본을 호스팅할 서버 인스턴스의 서비스 계정입니다.|  
|*DOMAIN2\user2*|초기 보조 복제본을 호스팅할 서버 인스턴스의 서비스 계정입니다.|  
|TCP://*COMPUTER01.Adventure-Works.com*:*7022*|COMPUTER01에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 AgHostInstance 인스턴스의 엔드포인트 URL입니다.|  
|TCP://*COMPUTER02.Adventure-Works.com*:*5022*|COMPUTER02에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 기본 인스턴스의 엔드포인트 URL입니다.|  
  
> [!NOTE]  
>  가용성 그룹을 만드는 다른 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 코드 샘플을 보려면 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)을 참조하세요.  
  
```sql
-- on the server instance that will host the primary replica,   
-- create sample databases:  
CREATE DATABASE MyDb1;  
GO  
ALTER DATABASE MyDb1 SET RECOVERY FULL;  
GO  
  
CREATE DATABASE MyDb2;  
GO  
ALTER DATABASE MyDb2 SET RECOVERY FULL;  
GO  
  
-- Backup sample databases:  
BACKUP DATABASE MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FORMAT  
GO  
  
BACKUP DATABASE MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FORMAT  
GO  
  
-- Create the endpoint on the server instance that will host the primary replica:  
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- Create the endpoint on the server instance that will host the secondary replica:   
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the primary replica,   
-- create a login for the service account   
-- of the server instance that will host the secondary replica, DOMAIN2\user2,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
CREATE LOGIN [DOMAIN2\user2] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN2\user2];  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the secondary replica,  
-- create a login for the service account   
-- of the server instance that will host the primary replica, DOMAIN1\user1,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
  
CREATE LOGIN [DOMAIN1\user1] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN1\user1];  
GO  
  
-- On the server instance that will host the primary replica,   
-- create the availability group, MyAG:  
CREATE AVAILABILITY GROUP MyAG   
   FOR   
      DATABASE MyDB1, MyDB2   
   REPLICA ON   
      'COMPUTER01\AgHostInstance' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         ),  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         );   
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join the secondary replica to the availability group:  
ALTER AVAILABILITY GROUP MyAG JOIN;  
GO  
  
-- Restore database backups onto this server instance, using RESTORE WITH NORECOVERY:  
RESTORE DATABASE MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NORECOVERY  
GO  
  
RESTORE DATABASE MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH NORECOVERY  
GO  
  
-- Back up the transaction log on each primary database:  
BACKUP LOG MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NOFORMAT  
GO  
  
BACKUP LOG MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITHNOFORMAT  
GO  
  
-- Restore the transaction log on each secondary database,  
-- using the WITH NORECOVERY option:  
RESTORE LOG MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FILE=1, NORECOVERY  
GO  
RESTORE LOG MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FILE=1, NORECOVERY  
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join each secondary database to the availability group:  
ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
GO  
  
ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
GO
```  
  
##  <a name="RelatedTasks"></a> 관련 작업  
 **가용성 그룹 및 복제본 속성을 구성하려면**  
  
-   [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [유연한 장애 조치(failover) 정책을 구성하여 자동 장애 조치의 상태 제어(AlwaysOn 가용성 그룹)](configure-flexible-automatic-failover-policy.md)  
  
-   [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [가용성 복제본에 백업 구성&#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [가용성 복제본에 대한 세션 제한 시간 변경&#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **가용성 그룹 구성을 완료하려면**  
  
-   [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **가용성 그룹을 만드는 다른 방법**  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹 만들기&#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
 **AlwaysOn 가용성 그룹을 사용하도록 설정하려면**  
  
-   [AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **데이터베이스 미러링 엔드포인트를 구성하려면**  
  
-   [AlwaysOn 가용성 그룹 &#40;SQL Server PowerShell에 대 한 데이터베이스 미러링 끝점을 만듭니다&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **AlwaysOn 가용성 그룹 구성 문제를 해결하려면**  
  
-   [삭제 된 SQL Server (AlwaysOn 가용성 그룹 구성) 문제 해결](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [실패 한 파일 추가 작업 문제 해결 AlwaysOn 가용성 그룹 &#40;&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [AlwaysON - HADRON 학습 시리즈: HADRON 지원 데이터베이스에 대한 작업자 풀 사용](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](https://blogs.msdn.com/b/psssql/)  
  
-   **비디오:**  
  
     [Microsoft SQL Server 코드 이름 "Denali" AlwaysOn 시리즈, 1부: 차세대 고가용성 솔루션 소개](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server 코드 이름 "Denali" AlwaysOn 시리즈, 파트 2: AlwaysOn을 사용하여 중요 환경 고가용성 솔루션 빌드](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **백서:**  
  
     [고가용성 및 재해 복구를 위한 Microsoft SQL Server AlwaysOn 솔루션 가이드](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012에 대한 Microsoft 백서](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](http://sqlcat.com/)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
