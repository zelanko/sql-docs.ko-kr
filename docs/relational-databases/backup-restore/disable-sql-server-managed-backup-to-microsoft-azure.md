---
title: "Microsoft Azure에 대한 SQL Server Managed Backup 해제 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3e02187f-363f-4e69-a82f-583953592544
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: caf1e311db9cc0844294417dfd06e4a384265a4b
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="disable-sql-server-managed-backup-to-microsoft-azure"></a>Microsoft Azure에 대한 SQL Server Managed Backup 해제
  이 항목은 데이터베이스 및 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 해제 또는 일시 중지하는 방법에 대해 설명합니다.  
  
##  <a name="DatabaseDisable"></a> 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 해제  
 시스템 저장 프로시저 [managed_backup.sp_backup_config_basic(Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)을 사용하여 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 설정을 해제할 수 있습니다. *@enable_backup* 매개 변수를 사용하면 특정 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성을 설정하고 해제할 수 있습니다. 여기서 1은 구성 설정을 설정하고 0은 해제합니다.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-a-specific-database"></a>특정 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 해제하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
```  
EXEC msdb.managed_backup.sp_backup_config_basic  
                @database_name = 'TestDB'   
                ,@enable_backup = 0;  
GO  
  
```  
  
##  <a name="DatabaseAllDisable"></a> 인스턴스의 모든 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 해제  
 다음 절차는 인스턴스에서 현재 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정되어 있는 모든 데이터베이스의 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성 설정을 해제하려는 경우에 해당됩니다.  저장소 URL, 보존 및 SQL 자격 증명과 같은 구성 설정은 메타데이터에 남아 있으며 나중에 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정되는 경우 다시 사용할 수 있습니다. 일시적으로 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 서비스를 일시 중지하는 경우 이 항목의 뒷부분에 나오는 섹션에서 설명하는 마스터 스위치를 사용할 수 있습니다.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-all-the-databases"></a>모든 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 해제하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예제는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 인스턴스 수준 및 인스턴스에 대한 모든 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 설정 데이터베이스에서 구성된 경우를 식별하고 시스템 저장 프로시저 **sp_backup_config_basic** 을 실행하여 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 해제합니다.  
  
```  
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM   
  
       msdb.managed_backup.fn_backup_db_config (NULL)  
       WHERE is_managed_backup_enabled = 1  
  
       --Select DBName from @DBNames  
  
       select @rowid = min(RowID)  
       FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin  
  
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC msdb.managed_backup.sp_backup_config_basic    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END  
```  
  
 인스턴스의 모든 데이터베이스에 대한 구성 설정을 보려면 다음 쿼리를 사용합니다.  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL);  
GO  
  
```  
  
##  <a name="InstanceDisable"></a> 인스턴스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 기본 설정 해제  
 인스턴스 수준의 기본 설정은 해당 인스턴스에 대해 만든 모든 새 데이터베이스에 적용됩니다.  더 이상 기본 설정이 필요하지 않는 경우 **@database_name** 매개 변수를 NULL로 설정하여 *@database_name* 시스템 저장 프로시저를 사용하여 이 구성을 해제할 수 있습니다. 해제하는 경우 저장소 URL, 보존 설정, SQL 자격 증명 이름 등의 다른 구성 설정이 제거되지 않습니다. 이러한 설정은 나중에 인스턴스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정되면 사용됩니다.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-default-configuration-settings"></a>[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 기본 구성 설정을 해제하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    EXEC msdb.managed_backup.sp_backup_config_basic  
                    @database_name = 'TestDB'   
                    ,@enable_backup = 0;  
    GO  
  
    ```  
  
##  <a name="InstancePause"></a> 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 일시 중지  
 짧은 시간 동안 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 서비스를 일시 중지해야 하는 경우가 있습니다.  **managed_backup.sp_backup_master_switch** 시스템 저장 프로시저를 사용하여 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 서비스를 해제할 수 있습니다.  동일한 저장 프로시저를 사용하여 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 다시 시작할 수 있습니다. @state 매개 변수는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 설정해야 할지 해제해야 할지를 정의하는 데 사용됩니다.  
  
#### <a name="to-pause-includesssmartbackupincludesss-smartbackup-mdmd-services-using-transact-sql"></a>Transact-SQL을 사용하여 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 서비스를 일시 중지하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣은 후 **실행**을 클릭합니다.  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
#### <a name="to-resume-includesssmartbackupincludesss-smartbackup-mdmd-using-transact-sql"></a>Transact-SQL을 사용하여 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 다시 시작하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣은 후 **실행**을 클릭합니다.  
  
```  
Use msdb;  
Go  
EXEC managed_backup. sp_backup_master_switch @new_state=1;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Azure에 대한 SQL Server Managed Backup 설정](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)  
  
  
