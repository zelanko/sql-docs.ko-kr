---
title: 데이터베이스를 새 위치로 복원(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- restoring databases [SQL Server], moving
- database restores [SQL Server], creating new databases
- restoring [SQL Server], with move
- restoring databases [SQL Server], creating new databases
- database backups [SQL Server], creating new database from
- backing up databases [SQL Server], creating new database from
- restoring databases [SQL Server], renaming
- database creation [SQL Server], restoring with move
ms.assetid: 4da76d61-5e11-4bee-84f5-b305240d9f42
caps.latest.revision: 64
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1e3f9f8ad10a31fa7af4b6a517c0c36fcc817494
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172214"
---
# <a name="restore-a-database-to-a-new-location-sql-server"></a>데이터베이스를 새 위치로 복원(SQL Server)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]데이터베이스를 새 위치로 복원하고 선택적으로 데이터베이스 이름을 바꾸는 방법에 대해 설명합니다. 데이터베이스를 새 디렉터리 경로로 이동하거나 동일한 서버 인스턴스 또는 다른 서버 인스턴스에 데이터베이스의 복사본을 만들 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **새 위치로 데이터베이스를 복원 및 필요에 따라 데이터베이스 이름 바꾸기를 사용 하 여:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   전체 데이터베이스 백업을 복원하는 시스템 관리자는 복원할 데이터베이스를 현재 사용 중인 유일한 사람이어야 합니다.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   전체 또는 대량 로그 복구 모델에서 데이터베이스를 복원하기 전에 활성 트랜잭션 로그를 백업해야 합니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)데이터베이스를 새 위치로 복원하고 선택적으로 데이터베이스 이름을 바꾸는 방법을 설명합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  
  
-   데이터베이스를 이동할 때 고려해야 할 사항에 대한 자세한 내용은 [백업 및 복원으로 데이터베이스 복사](../databases/copy-databases-with-backup-and-restore.md)를 참조하세요.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 복원하면 데이터베이스가 자동으로 업그레이드됩니다. 일반적으로 데이터베이스는 즉시 사용할 수 있습니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는  **upgrade_option** 서버 속성의 설정에 따라 인덱스를 가져오거나 다시 설정하거나 다시 작성합니다. 업그레이드 옵션이 가져오기(**upgrade_option** = 2) 또는 다시 작성(**upgrade_option** = 0)으로 설정되어 있는 경우 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 가져오기로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다. **upgrade_option** 서버 속성의 설정을 변경하려면 [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)를 사용합니다.  
  
###  <a name="Security"></a> 보안  
 보안을 위해서는 알 수 없거나 신뢰할 수 없는 출처의 데이터베이스는 연결 또는 복원하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요.  
  
####  <a name="Permissions"></a> Permissions  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-restore-a-database-to-a-new-location-and-optionally-rename-the-database"></a>데이터베이스를 새 위치로 복원하고 선택적으로 데이터베이스 이름을 바꾸려면  
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **데이터베이스 복원**을 클릭합니다. **데이터베이스 복원** 대화 상자가 열립니다.  
  
3.  **일반** 페이지에서 **원본** 섹션을 사용하여 복원할 백업 집합의 원본과 위치를 지정합니다. 다음 옵션 중 하나를 선택합니다.  
  
    -   **데이터베이스 백업**  
  
         복원할 데이터베이스를 드롭다운 목록에서 선택합니다. 목록에는 **msdb** 백업 기록에 따라 백업된 데이터베이스만 포함되어 있습니다.  
  
    > [!NOTE]  
    >  백업을 다른 서버에서 가져온 경우 대상 서버에 지정한 데이터베이스에 대한 백업 기록 정보가 없습니다. 이 경우 **장치** 를 선택하여 복원할 파일이나 장치를 수동으로 지정합니다.  
  
    1.  **장치**  
  
         찾아보기(**...**) 단추를 클릭하여 **백업 장치 선택** 대화 상자를 엽니다. **백업 미디어 유형** 상자에서 나열된 장치 유형 중 하나를 선택합니다. **백업 미디어** 상자에 대해 하나 이상의 장치를 선택하려면 **추가**를 클릭합니다.  
  
         원하는 장치를 **백업 미디어** 목록 상자에 추가한 후 **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.  
  
         **원본: 장치: 데이터베이스** 목록 상자에서 복원할 데이터베이스의 이름을 선택합니다.  
  
         **참고** 이 목록은 **장치** 를 선택한 경우에만 사용할 수 있습니다. 선택한 장치에 백업이 있는 데이터베이스만 사용할 수 있습니다.  
  
4.  **대상** 섹션의 **데이터베이스** 상자에는 복원할 데이터베이스의 이름이 자동으로 채워집니다. 데이터베이스의 이름을 변경하려면 **데이터베이스** 상자에 새 이름을 입력합니다.  
  
5.  **복원 위치** 상자에서 기본값인 **마지막으로 수행된 백업으로** 를 그대로 적용하거나 **시간대** 를 클릭하여 **백업 시간대** 대화 상자에 액세스한 후 복구 동작을 중지할 지정 시간을 직접 선택합니다. 특정 지정 시간을 지정하는 방법은 [Backup Timeline](backup-timeline.md) 를 참조하세요.  
  
6.  **복원에 사용할 백업 세트** 표에서 복원할 백업을 선택합니다. 이 표는 지정한 위치에서 사용 가능한 백업을 표시합니다. 기본적으로 복구 계획이 제안됩니다. 제안된 복구 계획을 재정의하려면 표에서 선택 항목을 변경합니다. 이전 백업의 선택이 취소되면 이전 백업 복원에 기반하는 백업도 자동으로 선택이 취소됩니다.  
  
     **복원에 사용할 백업 세트** 표의 열에 대한 자세한 내용은 [데이터베이스 복원&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)을 참조하세요.  
  
7.  데이터베이스 파일의 새 위치를 지정하려면 **파일** 페이지를 선택한 다음 **모든 파일을 폴더로 위치 변경**을 클릭합니다. **데이터 파일 폴더** 및 **로그 파일 폴더**에 대한 새 위치를 지정합니다. 이 표에 대한 자세한 내용은 [데이터베이스 복원&#40;파일 페이지&#41;](restore-database-files-page.md)을 참조하세요.  
  
8.  **옵션** 페이지에서 원하는 경우 옵션을 조정합니다. 이러한 옵션에 대한 자세한 내용은 [데이터베이스 복원&#40;옵션 페이지&#41;](restore-database-options-page.md)을 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-restore-a-database-to-a-new-location-and-optionally-rename-the-database"></a>데이터베이스를 새 위치로 복원하고 선택적으로 데이터베이스 이름을 바꾸려면  
  
1.  복원할 전체 데이터베이스 백업이 포함된 백업 세트에 있는 파일의 논리적 이름과 물리적 이름을 결정합니다(선택 사항). 이 문은 백업 세트에 포함된 데이터베이스와 로그 파일의 목록을 반환합니다. 기본 구문은 다음과 같습니다.  
  
     RESTORE FILELISTONLY FROM *<backup_device>* WITH FILE = *backup_set_file_number*  
  
     여기서 *backup_set_file_number*는 미디어 세트에서의 백업 위치를 나타냅니다. 백업 세트의 위치는 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) 문을 사용하여 가져올 수 있습니다. 자세한 내용은 [RESTORE 인수&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)에서 "백업 세트 지정"을 참조하세요.  
  
     이 문에는 WITH 옵션을 여러 개 지정할 수도 있습니다. 자세한 내용은 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)를 참조하세요.  
  
2.  [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql) 문을 사용하여 전체 데이터베이스 백업을 복원합니다. 기본적으로 데이터 및 로그 파일은 원래 위치로 복원됩니다. 데이터베이스의 위치를 다시 지정하려면 MOVE 옵션을 사용하여 각 데이터베이스 파일 위치를 옮기고 기존 파일과의 충돌을 피합니다.  
  
     데이터베이스를 새 위치 및 새 이름으로 복원하는 데 사용되는 기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 다음과 같습니다.  
  
     RESTORE DATABASE *new_database_name*  
  
     FROM *backup_device* [ ,...*n* ]  
  
     [ WITH  
  
     {  
  
     [ **RECOVERY** | NORECOVERY ]  
  
     [ , ] [ FILE ={ *backup_set_file_number* | @*backup_set_file_number* } ]  
  
     [ , ] MOVE '*logical_file_name_in_backup*' TO '*operating_system_file_name*' [ ,...*n* ]  
  
     }  
  
     ;  
  
    > [!NOTE]  
    >  데이터베이스 위치를 다른 디스크에 다시 지정할 때는 공간이 충분한지 확인하고 기존 파일과의 충돌 가능성이 있는지 확인합니다. 그러려면 RESTORE DATABASE 문에 사용하려는 것과 동일한 MOVE 매개 변수를 지정하는 [RESTORE VERIFYONLY](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql) 문을 사용해야 합니다.  
  
     다음 표에서는 새 위치로의 데이터베이스 복원과 관련된 이 RESTORE 문 인수에 대해 설명합니다. 이러한 인수에 대한 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)데이터베이스를 새 위치로 복원하고 선택적으로 데이터베이스 이름을 바꾸는 방법을 설명합니다.  
  
     *new_database_name*  
     데이터베이스의 새 이름입니다.  
  
    > [!NOTE]  
    >  데이터베이스를 다른 서버 인스턴스로 복원하는 경우 새 이름 대신 원래 데이터베이스 이름을 사용할 수 있습니다.  
  
     *backup_device* [ `,`... *n* ]  
     데이터베이스 백업 복원에 사용할 1-64개의 백업 장치 목록(쉼표로 구분됨)을 지정합니다. 물리적 백업 장치를 지정하거나, 정의된 경우 해당 논리적 백업 장치를 지정할 수 있습니다. 물리적 백업 장치를 지정하려면 다음 DISK 또는 TAPE 옵션을 사용합니다.  
  
     {디스크 | 테이프} `=` *physical_backup_device_name*  
  
     자세한 내용은 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)인스턴스에서 가져온 경우에 필요합니다.  
  
     { **RECOVERY** | NORECOVERY }  
     전체 복구 모델을 사용하는 데이터베이스의 경우, 데이터베이스를 복원한 후 트랜잭션 로그 백업을 적용해야 할 수도 있습니다. 이 경우 NORECOVERY 옵션을 지정하세요.  
  
     그렇지 않은 경우에는 기본값인 RECOVERY 옵션을 사용하세요.  
  
     FILE = { *backup_set_file_number* | @*backup_set_file_number* }  
     복원할 백업 세트를 나타냅니다. 예를 들어 *backup_set_file_number* 가 **1** 인 경우는 백업 미디어의 첫 번째 백업 세트를 나타내고 *backup_set_file_number* 가 **2** 인 경우는 두 번째 백업 세트를 나타냅니다. 백업 세트의 *backup_set_file_number* 는 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) 문을 사용하여 가져올 수 없습니다.  
  
     이 옵션이 지정되지 않은 경우에는 기본적으로 백업 장치의 첫 번째 백업 세트가 사용됩니다.  
  
     자세한 내용은 [RESTORE 인수&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)에서 "백업 세트 지정"을 참조하세요.  
  
     이동 **'*`logical_file_name_in_backup`*'** TO **'*`operating_system_file_name`*'** [ `,`... *n* ]  
     *logical_file_name_in_backup* 에 지정된 데이터 또는 로그 파일을 *operating_system_file_name*에 지정된 위치로 복원하도록 지정합니다. 백업 세트에서 새 위치로 복원할 모든 논리적 파일에 대해 MOVE 문을 지정합니다.  
  
    |옵션|Description|  
    |------------|-----------------|  
    |*logical_file_name_in_backup*|백업 세트에 있는 데이터 또는 로그 파일의 논리적 이름을 지정합니다. 백업 세트에 있는 데이터 또는 로그 파일의 논리적 파일 이름은 백업 세트 생성 시 데이터베이스의 해당 논리적 이름과 일치합니다.<br /><br /> 참고: 백업 세트에서 논리적 파일 목록을 가져오려면 [RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)를 사용합니다.|  
    |*operating_system_file_name*|*logical_file_name_in_backup*에 지정된 파일의 새 위치를 지정합니다. 파일이 이 위치로 복원됩니다.<br /><br /> *operating_system_file_name* 에서 복원 파일의 새 파일 이름을 지정합니다(선택 사항). 이 작업은 동일한 서버 인스턴스에 기존 데이터베이스의 복사본을 만들려는 경우에 필요합니다.|  
    |*n*|추가 MOVE 문을 지정할 수 있음을 나타내는 자리 표시자입니다.|  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예제에서는 `MyAdvWorks` 샘플 데이터베이스의 백업을 복원하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 라는 새 데이터베이스를 만듭니다. 여기에는 두 개의 파일 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Data 및 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Log가 포함되어 있습니다. 이 데이터베이스는 단순 복구 모델을 사용합니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스가 이미 서버 인스턴스에 있으므로 백업에 들어 있는 파일을 새 위치로 복원해야 합니다. RESTORE FILELISTONLY 문은 복원할 데이터베이스에 있는 파일의 수와 이름을 확인하는 데 사용합니다. 데이터베이스 백업은 백업 장치에 있는 첫 번째 백업 세트입니다.  
  
> [!NOTE]  
>  지정 시간 복원을 비롯하여 트랜잭션 로그를 백업 및 복원하는 예에서는 다음 `MyAdvWorks_FullRM` 예와 마찬가지로 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]에서 만든 `MyAdvWorks` 데이터베이스를 사용합니다. 그러나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 ALTER DATABASE <database_name> SET RECOVERY FULL을 사용하여 결과로 생성된 `MyAdvWorks_FullRM` 데이터베이스가 전체 복구 모델을 사용하도록 변경되어야 합니다.  
  
```tsql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
-- AdventureWorks2012_Backup is the name of the backup device.  
RESTORE FILELISTONLY  
   FROM AdventureWorks2012_Backup;  
-- Restore the files for MyAdvWorks.  
RESTORE DATABASE MyAdvWorks  
   FROM AdventureWorks2012_Backup  
   WITH RECOVERY,  
   MOVE 'AdventureWorks2012_Data' TO 'D:\MyData\MyAdvWorks_Data.mdf',   
   MOVE 'AdventureWorks2012_Log' TO 'F:\MyLog\MyAdvWorks_Log.ldf';  
GO  
  
```  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 전체 데이터베이스 백업을 만드는 방법의 예제는 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [백업 및 복원으로 데이터베이스 복사](../databases/copy-databases-with-backup-and-restore.md)  
  
  
