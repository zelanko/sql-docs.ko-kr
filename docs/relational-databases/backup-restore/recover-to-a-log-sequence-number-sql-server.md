---
title: 로그 시퀀스 번호로 복구(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log sequence numbers [SQL Server]
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- LSNs
- database recovery [SQL Server]
- database restores [SQL Server], point in time
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 46ab24ff86eb7a68e48f58e67f03a859d0c43aa7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72916044"
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>로그 시퀀스 번호로 복구(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 전체 또는 대량 로그 복구 모델을 사용하는 데이터베이스와 관련된 내용을 다룹니다.  
  
 LSN(로그 시퀀스 번호)을 사용하여 복원 작업에 대한 복구 지점을 정의할 수 있습니다. 그러나 이 기능은 도구 공급업체를 위해 특별히 제작된 기능으로 일반적으로 유용한 기능은 아닙니다.  
  
##  <a name="LSNs"></a> 로그 시퀀스 번호 개요  
 LSN은 RESTORE 순서 중에 내부적으로 사용되어 데이터가 복원될 지정 시간을 추적합니다. 백업을 복구할 때 데이터는 백업이 이루어진 지정 시간에 해당하는 LSN으로 복원됩니다. 차등 및 로그 백업의 경우 데이터베이스는 보다 나중의 것으로 복원되며 이는 더 높은 LSN에 해당합니다. LSN에 대한 자세한 내용은 [SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)를 참조하세요.  
  
> [!NOTE]  
> LSN은 **numeric(25,0)** 데이터 형식의 값입니다. 더하기나 빼기와 같은 산술 연산은 의미가 없으며 LSN과 함께 사용하면 안 됩니다.  
 
## <a name="viewing-lsns-used-by-backup-and-restore"></a>백업과 복원에 사용된 LSN 보기  
 다음 중 하나 이상의 방법을 사용하여 지정된 백업 및 복원 이벤트가 발생했을 때의 로그 레코드 LSN을 볼 수 있습니다.  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md); [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
-   [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
> [!NOTE]  
>  또한 LSN은 오류 로그의 일부 메시지에도 표시됩니다.  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>LSN으로 복원하기 위한 Transact-SQL 구문  
 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 문을 사용하여 다음과 같은 LSN에서 또는 이전에 즉시 중지할 수 있습니다.  
  
-   WITH STOPATMARK **='** lsn: _<lsn_number>_ **'** 절을 사용합니다. 여기서 lsn: *\<lsnNumber>* 는 지정한 LSN이 포함된 로그 레코드가 복구 지점이 되도록 지정하는 문자열입니다.  
  
     STOPATMARK는 복구 중지 지점을 나타내며 지정된 로그 레코드를 포함하는 지점까지 롤포워드됩니다.  
  
-   WITH STOPBEFOREMARK **='** lsn: _<lsn_number>_ **'** 절을 사용합니다. 여기서 lsn: *\<lsnNumber>* 는 지정한 LSN 번호가 포함된 로그 레코드 바로 앞의 로그 레코드가 복구 지점이 되도록 지정하는 문자열입니다.  
  
     STOPBEFOREMARK는 LSN에 롤포워드하고 롤포워드의 해당 로그 레코드를 제외합니다.  
  
 일반적으로 특정 트랜잭션을 포함하거나 제외하도록 선택합니다. 필수는 아니지만 대개 지정된 로그 레코드는 트랜잭션 커밋 레코드입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks` 데이터베이스가 전체 복구 모델을 사용하도록 변경되었다고 가정합니다.  
  
```sql  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [데이터베이스를 표시된 트랜잭션으로 복원&#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [복원 및 복구 개요(SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)       
 [SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)      
  
