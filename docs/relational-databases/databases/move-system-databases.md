---
title: "시스템 데이터베이스 이동 | Microsoft 문서"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving system databases
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- tempdb database [SQL Server], moving
- system databases [SQL Server], moving
- scheduled disk maintenace [SQL Server]
- moving databases
- msdb database [SQL Server], moving
- moving database files
- relocating database files
- planned database relocations [SQL Server]
- master database [SQL Server], moving
- model database [SQL Server], moving
- Resource database [SQL Server]
- databases [SQL Server], moving
ms.assetid: 72bb62ee-9602-4f71-be51-c466c1670878
caps.latest.revision: "62"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f04dfdd5aeea21bad9d95bf72e99d6b566e9a0c7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="move-system-databases"></a>시스템 데이터베이스 이동
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 시스템 데이터베이스를 이동하는 방법에 대해 설명합니다. 시스템 데이터베이스 이동은 다음과 같은 경우에 유용할 수 있습니다.  
  
-   오류 복구. 하드웨어 오류로 인해 데이터베이스가 주의 대상 모드에 있거나 종료된 경우를 예로 들 수 있습니다.  
  
-   계획된 재배치  
  
-   예약된 디스크 유지 관리를 위한 재배치  
  
 다음 절차는 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 내에서 데이터베이스 파일을 이동하는 경우에 적용됩니다. 데이터베이스를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스나 다른 서버로 이동하려면 [백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 작업을 사용합니다.  

 이 항목의 절차를 사용하려면 데이터베이스 파일의 논리적 이름이 필요합니다. 논리적 파일 이름을 구하려면 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 카탈로그 뷰의 name 열을 쿼리합니다.  
  
> [!IMPORTANT]  
>  시스템 데이터베이스를 이동한 다음 나중에 master 데이터베이스를 다시 작성하는 경우 다시 작성 작업에서 모든 시스템 데이터베이스를 기본 위치에 설치하기 때문에 시스템 데이터베이스를 다시 이동해야 합니다.  

> [!IMPORTANT]  
>  파일을 이동하고 나면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 서비스 계정에 새 파일 폴더 위치에서 파일에 액세스할 수 있는 권한이 있어야 합니다.
    
  
##  <a name="Planned"></a> 계획된 재배치 및 예약된 디스크 유지 관리 절차  
 계획된 재배치 또는 예약된 유지 관리 작업의 일부로 시스템 데이터베이스 데이터나 로그 파일을 이동하려면 다음 단계를 따릅니다. 이 절차는 master 및 리소스 데이터베이스를 제외한 모든 시스템 데이터베이스에 적용됩니다.  
  
1.  이동할 각 파일에 대해 다음 문을 실행합니다.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 중지하거나 시스템을 종료하여 유지 관리를 수행합니다. 자세한 내용은 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)을 참조하세요.  
  
3.  파일을 새 위치로 이동합니다.  

4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스나 서버를 다시 시작합니다. 자세한 내용은 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)을 참조하세요.  
  
5.  다음 쿼리를 실행하여 파일 변경 내용을 확인합니다.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
 msdb 데이터베이스가 이동되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)을 구성한 경우 다음 단계를 추가로 완료합니다.  
  
1.  다음 쿼리를 실행하여 msdb 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 설정되어 있는지 확인합니다.  
  
    ```  
    SELECT is_broker_enabled   
    FROM sys.databases  
    WHERE name = N'msdb';  
    ```  
  
     [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 설정하는 방법은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
2.  테스트 메일을 보내 데이터베이스 메일이 작동하는지 확인합니다.  
  
##  <a name="Failure"></a> 오류 복구 절차  
 하드웨어 오류로 인해 파일을 이동해야 하는 경우 다음 단계에 따라 파일을 새 위치에 재배치합니다. 이 절차는 master 및 리소스 데이터베이스를 제외한 모든 시스템 데이터베이스에 적용됩니다.  
  
> [!IMPORTANT]  
>  데이터베이스가 주의 대상 모드에 있거나 복구할 수 없는 상태여서 시작할 수 없는 경우에는 sysadmin 고정 역할의 멤버만 파일을 이동할 수 있습니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작된 경우 중지합니다.  
  
2.  명령 프롬프트에서 다음 명령 중 하나를 입력하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 마스터 전용 복구 모드로 시작합니다. 이러한 명령에 지정된 매개 변수는 대/소문자를 구분합니다. 표시된 대로 매개 변수를 지정하지 않으면 명령이 실패합니다.  
  
    -   기본(MSSQLSERVER) 인스턴스의 경우 다음 명령을 실행합니다.  
  
        ```  
        NET START MSSQLSERVER /f /T3608
        ```  
  
    -   명명된 인스턴스의 경우 다음 명령을 실행합니다.  
  
        ```  
        NET START MSSQL$instancename /f /T3608
        ```  
  
     자세한 내용은 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)을 참조하세요.  
  
3.  이동할 각 파일에 대해 **sqlcmd** 명령 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 다음 문을 실행합니다.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
     **sqlcmd** 유틸리티 사용에 대한 자세한 내용은 [sqlcmd 유틸리티 사용](../../relational-databases/scripting/sqlcmd-use-the-utility.md)을 참조하세요.  
  
4.  **sqlcmd** 유틸리티 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 종료합니다.  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 중지합니다. 예를 들어 `NET STOP MSSQLSERVER`를 실행합니다.  
  
6.  파일을 새 위치로 이동합니다.  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작합니다. 예를 들어 `NET START MSSQLSERVER`를 실행합니다.  
  
8.  다음 쿼리를 실행하여 파일 변경 내용을 확인합니다.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
##  <a name="master"></a> master 데이터베이스 이동  
 master 데이터베이스를 이동하려면 다음 단계를 수행합니다.  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  **SQL Server 서비스** 노드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스(예: **SQL Server(MSSQLSERVER)**)를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
3.  **SQL Server(***instance_name***) 속성** 대화 상자에서 **시작 매개 변수** 탭을 클릭합니다.  
  
4.  **기존 매개 변수** 상자에서 –d 매개 변수를 선택하여 마스터 데이터 파일을 이동합니다. **업데이트** 를 클릭하여 변경 내용을 저장합니다.  
  
     **시작 매개 변수 지정** 상자에서 매개 변수를 master 데이터베이스의 새 경로로 변경합니다.  
  
5.  **기존 매개 변수** 상자에서 –l 매개 변수를 선택하여 마스터 로그 파일을 이동합니다. **업데이트** 를 클릭하여 변경 내용을 저장합니다.  
  
     **시작 매개 변수 지정** 상자에서 매개 변수를 master 데이터베이스의 새 경로로 변경합니다.  
  
     데이터 파일의 매개 변수 값은 `-d` 매개 변수 뒤에 와야 하고 로그 파일의 값은 `-l` 매개 변수 뒤에 와야 합니다. 다음 예에서는 마스터 데이터 파일의 기본 위치에 대한 매개 변수 값을 보여 줍니다.  
  
     `-dC:\Program Files\Microsoft SQL Server\MSSQL<version>.MSSQLSERVER\MSSQL\DATA\master.mdf`  
  
     `-lC:\Program Files\Microsoft SQL Server\MSSQL<version>.MSSQLSERVER\MSSQL\DATA\mastlog.ldf`  
  
     마스터 데이터 파일의 계획된 재배치가 `E:\SQLData`인 경우 매개 변수 값은 다음과 같이 변경됩니다.  
  
     `-dE:\SQLData\master.mdf`  
  
     `-lE:\SQLData\mastlog.ldf`  
  
6.  인스턴스 이름을 마우스 오른쪽 단추로 클릭하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 중지 **를 선택하여**인스턴스를 중지합니다.  
  
7.  master.mdf 및 mastlog.ldf 파일을 새 위치로 이동합니다.  
  
8.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작합니다.  
  
9. 다음 쿼리를 실행하여 master 데이터베이스에 대한 파일 변경 내용을 확인합니다.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID('master');  
    GO  
    ```  

10. 이 시점에서 SQL Server는 정상적으로 실행되어야 합니다. 그러나 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\instance_ID\Setup`에서 레지스트리 항목을 조정하는 것이 좋습니다. 여기서 *instance_ID* 는 `MSSQL13.MSSQLSERVER`와 비슷합니다. 해당 Hive에서 `SQLDataRoot` 값을 새 경로로 변경합니다. 레지스트리 업데이트에 실패하면 패치 및 업그레이드도 실패할 수 있습니다.

  
##  <a name="Resource"></a> 리소스 데이터베이스 이동  
 Resource 데이터베이스의 위치는 \<*드라이브*>:\Program Files\Microsoft SQL Server\MSSQL\<version>.\<*instance_name*>\MSSQL\Binn\\입니다. 데이터베이스는 이동할 수 없습니다.  
  
##  <a name="Follow"></a> 후속 작업: 모든 시스템 데이터베이스를 이동한 후  
 모든 시스템 데이터베이스를 새 드라이브 또는 볼륨으로 이동했거나 다른 드라이브 문자를 사용하는 다른 서버에 이동한 경우 다음과 같이 업데이트하세요.  
  
-   SQL Server 에이전트 로그 경로를 변경합니다. 이 경로를 업데이트하지 않으면 SQL Server 에이전트가 시작되지 않습니다.  
  
-   데이터베이스 기본 위치를 변경합니다. 기본 위치로 지정한 드라이브 문자 및 경로가 존재하지 않을 경우 새 데이터베이스 만들기가 실패할 수 있습니다.  
  
#### <a name="change-the-sql-server-agent-log-path"></a>SQL Server 에이전트 로그 경로를 변경합니다.  
  
1.  SQL Server Management Studio의 개체 탐색기에서 **SQL Server 에이전트**를 확장합니다.  
  
2.  **오류 로그** 를 마우스 오른쪽 단추로 클릭한 다음 **구성**을 클릭합니다.  
  
3.  **SQL Server 에이전트 오류 로그 구성** 대화 상자에서 SQLAGENT.OUT 파일의 새 위치를 지정합니다. 기본 위치는 C:\Program Files\Microsoft SQL Server\MSSQL\<version>.<instance_name>\MSSQL\Log\\입니다.  
  
#### <a name="change-the-database-default-location"></a>데이터베이스 기본 위치 변경  
  
1.  SQL Server Management Studio의 개체 탐색기에서 SQL Server 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **서버 속성** 대화 상자에서 **데이터베이스 설정**을 선택합니다.  
  
3.  **데이터베이스 기본 위치**에서 데이터 및 로그 파일의 새 위치를 찾습니다.  
  
4.  변경을 완료하려면 SQL Server 서비스를 중지한 후 시작합니다.  
  
##  <a name="Examples"></a> 예  
  
### <a name="a-moving-the-tempdb-database"></a>1. tempdb 데이터베이스 이동  
 다음 예에서는 계획된 재배치의 일부로 `tempdb` 데이터와 로그 파일을 새 위치로 이동합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 시작할 때마다 tempdb가 다시 생성되므로 데이터와 로그 파일을 물리적으로 이동할 필요는 없습니다. 3단계에서 서비스를 다시 시작할 때 새 위치에 파일이 생성됩니다. 서비스를 다시 시작할 때까지는 tempdb에서 계속 기존 위치의 데이터와 로그 파일을 사용합니다.  
  
1.  `tempdb` 데이터베이스의 논리적 파일 이름 및 디스크에서의 현재 위치를 확인합니다.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    GO  
    ```  
  
2.  `ALTER DATABASE`를 사용하여 각 파일의 위치를 변경합니다.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'F:\SQLLog\templog.ldf');  
    GO  
    ```  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 중지한 후 다시 시작합니다.  
  
4.  파일 변경 내용을 확인합니다.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    ```  
  
5.  원래 위치에서 `tempdb.mdf` 및 `templog.ldf` 파일을 삭제합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Resource 데이터베이스](../../relational-databases/databases/resource-database.md)   
 [tempdb 데이터베이스](../../relational-databases/databases/tempdb-database.md)   
 [master 데이터베이스](../../relational-databases/databases/master-database.md)   
 [msdb 데이터베이스](../../relational-databases/databases/msdb-database.md)   
 [model 데이터베이스](../../relational-databases/databases/model-database.md)   
 [사용자 데이터베이스 이동](../../relational-databases/databases/move-user-databases.md)   
 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)   
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [시스템 데이터베이스 다시 작성](../../relational-databases/databases/rebuild-system-databases.md)  
  
  
