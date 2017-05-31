---
title: "복사 전용 백업(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
caps.latest.revision: 48
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9a63e882e79ec725cca126e80369a70bbc4bc774
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="copy-only-backups-sql-server"></a>복사 전용 백업(SQL Server)
  *복사 전용 백업*은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업입니다. 일반적으로 백업을 수행하면 데이터베이스가 변경되므로 이후 백업이 복원되는 방식에 영향을 주게 됩니다. 그러나 백업 전체에 영향을 주지 않고 특별한 용도로 백업을 수행한 다음 데이터베이스에 대한 프로시저를 복원하는 것이 유용할 수도 있습니다. 이러한 용도로 복사 전용 백업이 제공됩니다.  
  
 복사 전용 백업의 종류는 다음과 같습니다.  
  
-   복사 전용 전체 백업(모든 복구 모델)  
  
     복사 전용 백업은 차등 기반 또는 차등 백업으로 사용될 수 없으며 차등 기반에 영향을 미치지 않습니다.  
  
     복사 전용 전체 백업을 복원하는 과정은 다른 전체 백업을 복원하는 과정과 동일합니다.  
  
-   복사 전용 로그 백업(전체 복구 모델 및 대량 로그 복구 모델 전용)  
  
     복사 전용 로그 백업은 기존 로그 보관 지점을 유지하므로 정기적인 로그 백업 시퀀스에 영향을 주지 않습니다. 복사 전용 로그 백업은 일반적으로 불필요한 백업입니다. 대신 WITH NORECOVERY를 사용하여 새 정기 로그 백업을 만든 다음 해당 백업을 복원 시퀀스에 필요한 모든 이전 로그 백업과 함께 사용할 수 있습니다. 하지만 복사 전용 로그 백업은 온라인 복원에도 유용할 수 있습니다. 해당 예제를 보려면 [예제: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)을 참조하세요.  
  
     복사 전용 백업 이후에는 트랜잭션 로그를 자를 수 없습니다.  
  
 복사 전용 백업은 **backupset** 테이블의 [is_copy_only](../../relational-databases/system-tables/backupset-transact-sql.md) 열에 기록됩니다.  
  
## <a name="to-create-a-copy-only-backup"></a>복사 전용 백업을 만들려면  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]또는 PowerShell을 사용하여 복사 전용 백업을 만들 수 있습니다.  

### <a name="examples"></a>예  
###  <a name="SSMSProcedure"></a> 1.  SQL Server Management Studio 사용  
이 예제에서는 `Sales` 데이터베이스의 복사 전용 백업이 기본 백업 위치에서 디스크에 백업됩니다.

1.  **개체 탐색기**에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.

2.  **데이터베이스**를 확장하고 `Sales`를 마우스 오른쪽 단추로 클릭한 다음 **태스크**를 가리키고 **백업...**을 클릭합니다.

3.  **일반** 페이지의 **소스** 확인 섹션에서 **복사 전용 백업** 확인란을 선택합니다.

4.  **확인**을 클릭합니다.

  
###  <a name="TsqlProcedure"></a>2.  Transact-SQL 사용  
이 예에서는 COPY_ONLY 매개 변수를 활용하여 `Sales` 데이터베이스에 대한 복사 전용 백업을 만듭니다.  트랜잭션 로그의 복사 전용 백업도 만듭니다.

```tsql
BACKUP DATABASE Sales
TO DISK = 'E:\BAK\Sales_Copy.bak'
WITH COPY_ONLY;

BACKUP LOG Sales
TO DISK = 'E:\BAK\Sales_LogCopy.trn'
WITH COPY_ONLY;
```
  
> [!NOTE]  
> DIFFERENTIAL 옵션과 함께 지정하면 COPY_ONLY가 적용되지 않습니다.  

  
###  <a name="PowerShellProcedure"></a>3.  PowerShell 사용  
이 예에서는 CopyOnly 매개 변수를 활용하여 `Sales` 데이터베이스에 대한 복사 전용 백업을 만듭니다.  
```powershell
Backup-SqlDatabase -ServerInstance 'SalesServer' -Database 'Sales' -BackupFile 'E:\BAK\Sales_Copy.bak' -CopyOnly
```  
  
##  <a name="RelatedTasks"></a> 관련 작업  
 **전체 또는 로그 백업을 만들려면**  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **복사 전용 백업을 보려면**  
  
-   [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [백업 및 복원으로 데이터베이스 복사](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
[BACKUP(Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[Backup-SqlDatabase](https://technet.microsoft.com/library/mt683378.aspx)

  

