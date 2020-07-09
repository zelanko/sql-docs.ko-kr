---
title: 오류 발생 후 백업 또는 복원 설정
description: SQL Server에서 SQL Server Management Studio 또는 Transact-SQL을 사용하여 오류 발생 후 백업 또는 복원 작업을 계속할지 지정하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], backups
- backing up databases [SQL Server], errors
- backups [SQL Server], errors
- database backups [SQL Server], errors
ms.assetid: 042be17a-b9b0-4629-b6bb-b87a8bc6c316
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 003fbc933de445b6540c797d57b02dbad834e0bf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759053"
---
# <a name="specify-backup-or-restore-to-continue-or-stop-after-error"></a>오류 발생 후 계속 또는 중지하도록 백업 또는 복원 지정
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 오류 발생 후 백업 또는 복원 작업을 계속할지 중지할지를 지정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **오류가 발생한 후 백업 또는 복원 작업을 계속할지 여부를 지정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 BACKUP  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 디바이스의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 디바이스를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 디바이스에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 백업 디바이스의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
 RESTORE  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-specify-whether-backup-continues-or-stops-after-an-error-is-encountered"></a>오류가 발생한 후 백업을 계속할지 중지할지를 지정하려면  
  
1.  [데이터베이스 백업 만들기](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)단계를 따릅니다.  
  
2.  **옵션** 페이지의 **안정성** 섹션에서 **미디어에 쓰기 전에 체크섬 수행** 과 **오류 발생 시 계속**을 차례로 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-specify-whether-a-backup-operation-continues-or-stops-after-encountering-an-error"></a>오류가 발생한 후 백업 작업을 계속할지 중지할지를 지정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  [BACKUP](../../t-sql/statements/backup-transact-sql.md) 문에서 계속하려면 CONTINUE_AFTER ERROR 옵션을 지정하고 중지하려면 STOP_ON_ERROR 옵션을 지정합니다. 기본 동작은 오류가 발생한 후 중지하는 것입니다. 이 예에서는 오류가 발생하더라도 백업 작업을 계속하도록 지시합니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM, CONTINUE_AFTER_ERROR;  
GO  
```  
  
#### <a name="to-specify-whether-a-restore-operation-continues-or-stops-after-encountering-an-error"></a>오류가 발생한 후 복원 작업을 계속할지 중지할지를 지정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 문에서 계속하려면 CONTINUE_AFTER ERROR 옵션을 지정하고 중지하려면 STOP_ON_ERROR 옵션을 지정합니다. 기본 동작은 오류가 발생한 후 중지하는 것입니다. 이 예에서는 오류가 발생하더라도 복원 작업을 계속하도록 지시합니다.  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
 FROM DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'   
   WITH CHECKSUM, CONTINUE_AFTER_ERROR;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE 인수&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [백업 또는 복원 중 백업 체크섬 설정 또는 해제&#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
  
