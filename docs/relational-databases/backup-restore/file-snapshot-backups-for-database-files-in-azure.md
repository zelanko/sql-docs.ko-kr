---
title: Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업 | Microsoft 문서
ms.custom: ''
ms.date: 05/23/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17a81fcd-8dbd-458d-a9c7-2b5209062f45
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d010a0b7ea33cdda98c62c07d6d52c61d01051cb
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="file-snapshot-backups-for-database-files-in-azure"></a>Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일-스냅숏 백업에서는 Azure 스냅숏을 사용하여 Azure Blob 저장소 서비스를 통해 저장된 데이터베이스 파일을 거의 즉시 백업하고 더욱 신속하게 복원합니다. 이 기능을 사용하면 백업 및 복원 정책을 간소화할 수 있습니다. 라이브 데모는 [지정 시간 복원 데모](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)를 참조하세요. Azure 블로그 저장소 서비스를 사용하여 데이터베이스 파일을 저장하는 자세한 방법은 [Microsoft Azure의 SQL Server 데이터 파일](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)을 참조하세요.  
  
 ![스냅숏 백업 아키텍처 다이어그램](../../relational-databases/backup-restore/media/snapshotbackups.PNG "snapshot backup architectural diagram")  
  
 **다운로드**  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]를 다운로드하려면  **[평가 센터](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**로 이동하세요.  
  
-   Azure 계정이 있으세요?  계정이 있는 경우 **[여기](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** 로 이동하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이 이미 설치된 가상 컴퓨터를 실행해 보세요.  
  
## <a name="using-azure-snapshots-to-back-up-database-files-stored-in-azure"></a>Azure 스냅숏을 사용하여 Azure에 저장된 데이터베이스 파일 백업  
  
### <a name="what-is-a-includessnoversionincludesssnoversion-mdmd-file-snapshot-backup"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일-스냅숏 백업이란?  
 파일-스냅숏 백업은 데이터베이스 파일을 포함하는 blo 및 이러한 파일-스냅숏에 대한 포인터를 포함하는 백업 파일의 Azure 스냅숏 집합으로 구성됩니다. 각 파일-스냅숏은 기본 blob과 함께 컨테이너에 저장됩니다. 백업 파일 자체가 URL, 디스크 또는 테이프에 기록되도록 지정할 수 있습니다. URL에 백업하는 것이 좋습니다. 백업에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조하고, URL에 백업하는 방법은 [URL에 대한 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md)을 참조하세요.  
  
 ![스냅숏 기능의 아키텍처](../../relational-databases/backup-restore/media/snapshotbackups-flat.png "architecture of snapshot feature")  
  
 기본 blob을 삭제하면 백업 집합이 무효화되고, 모든 파일-스냅숏과 함께 blob을 삭제하도록 명시적으로 선택하지 않는 한 파일-스냅숏이 포함된 blob을 삭제할 수 없습니다. 또한 데이터베이스 또는 데이터 파일을 삭제할 경우 기본 blob 또는 해당 파일-스냅숏은 삭제되지 않으며, 백업 파일을 삭제할 경우 백업 집합의 파일-스냅숏은 삭제되지 않습니다. 파일-스냅숏 백업 집합을 삭제하려면 **sys.sp_delete_backup** 시스템 저장 프로시저를 사용하세요.  
  
 **전체 데이터베이스 백업:** 파일-스냅숏 백업을 사용하여 전체 데이터베이스 백업을 수행하면 데이터베이스를 구성하는 각 데이터 및 로그 파일의 Azure 스냅숏이 생성되고, 트랜잭션 로그 백업 체인이 설정되며, 파일-스냅숏의 위치가 백업 파일에 기록됩니다.  
  
 **트랜잭션 로그 백업:** 파일-스냅숏 백업을 사용하여 트랜잭션 로그 백업을 수행하면 각 데이터베이스 파일(트랜잭션 로그뿐 아니라)의 파일-스냅숏이 생성되고, 파일-스냅숏 위치 정보가 백업 파일에 기록되며, 트랜잭션 로그 파일이 잘립니다.  
  
> [!IMPORTANT]  
>  트랜잭션 로그 백업 체인(파일-스냅숏 백업일 수 있음)을 설정하는 데 필요한 초기 전체 백업 후에는 각 트랜잭션 로그 파일-스냅숏 백업 집합에 모든 데이터베이스 파일의 파일-스냅숏이 포함되고 이를 사용하여 데이터베이스를 복원 또는 로그 복원을 수행할 수 있으므로 트랜잭션 로그 백업을 수행하기만 하면 됩니다. 초기 전체 데이터베이스 백업 후에는 원하지 않는 추가 전체 또는 차등 백업을 Azure Blob 저장소 서비스가 각 데이터베이스 파일에 대한 기본 blob의 현재 상태와 각 파일-스냅숏 간의 차이를 처리하기 때문에 전체 또는 차등 백업을 추가로 수행할 필요가 없습니다.  
  
> [!NOTE]  
>  Microsoft Azure Blob 저장소 서비스에서 SQL Server 2016을 사용하는 방법에 대한 자습서는 [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob 저장소 서비스 사용](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)을 참조하세요.  
  
### <a name="restore-using-file-snapshot-backups"></a>파일-스냅숏 백업을 사용하여 복원  
 각 파일-스냅숏 백업 집합은 각 데이터베이스 파일의 파일-스냅숏을 포함하기 때문에 복원 프로세스에는 인접한 두 개의 파일-스냅숏 백업 집합만 필요합니다. 백업 집합을 전체 데이터베이스 백업에서 가져오든 로그 백업에서 가져오든 상관없습니다. 이는 기존 스트리밍 백업 파일을 사용하여 복원 프로세스를 수행하는 경우와 매우 다릅니다. 기존 스트리밍 백업을 사용하는 경우에는 복원 프로세스에서 전체 백업 집합 체인(전체 백업, 차등 백업 및 하나 이상의 트랜잭션 로그 백업)을 사용해야 합니다. 복원 프로세스의 복구 부분은 복원에서 파일-스냅숏 백업을 사용하는지 또는 스트리밍 백업 집합을 사용하는지에 관계없이 동일하게 유지됩니다.  
  
 **백업 집합의 시점으로:** RESTORE DATABASE 작업을 수행하여 특정 파일-스냅숏 백업 집합의 시점으로 데이터베이스를 복원하려면 자체 기본 blob과 함께 특정 백업 집합만 있으면 됩니다. 트랜잭션 로그 파일-스냅숏 백업 집합을 사용하여 RESTORE DATABASE 작업을 수행할 수 있으므로 일반적으로 이 유형의 RESTORE DATABASE 작업을 수행할 때는 트랜잭션 로그 백업 집합을 사용하며, 전체 데이터베이스 백업 집합은 거의 사용하지 않습니다. 이 기술을 보여 주는 예제는 이 항목의 끝에 나와 있습니다.  
  
 **두 파일-스냅숏 백업 집합 사이의 지정 시간으로:** RESTORE DATABASE 작업을 수행하여 인접한 두 트랜잭션 로그 백업 집합 사이의 특정 지정 시간으로 데이터베이스를 복원하려면 데이터베이스를 복원할 지정 시간 이전과 이후의 트랜잭션 로그 백업 집합 두 개만 있으면 됩니다. 그러려면 이전 지정 시간의 트랜잭션 로그 파일-스냅숏 백업 집합을 사용하여 WITH NORECOVERY와 함께 RESTORE DATABASE 작업을 수행하고, 이후 지정 시간의 트랜잭션 로그 파일-스냅숏 백업 집합을 사용하여 WITH NORECOVERY와 함께 RESTORE LOG 작업을 수행합니다. 이때 STOPAT 인수를 사용하여 트랜잭션 로그 백업에서 복구를 중지할 지정 시간을 지정합니다. 이 기술을 보여 주는 예제는 이 항목의 끝에 나와 있습니다. 라이브 데모는 [지정 시간 복원 데모](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)를 참조하세요.  
  
### <a name="file-backup-set-maintenance"></a>파일-백업 집합 유지 관리  
 **파일-스냅숏 백업 집합 삭제:** FORMAT 인수를 사용하여 파일-스냅숏 백업 집합을 덮어쓸 수 없습니다. 원래 파일-스냅숏 백업을 사용하여 만든 분리된 파일-스냅숏이 남아 있는 것을 방지하기 위해 FORMAT 인수는 허용되지 않습니다. 파일-스냅숏 백업 집합을 삭제하려면 **sys.sp_delete_backup** 시스템 저장 프로시저를 사용하세요. 이 저장 프로시저는 백업 집합을 구성하는 파일-스냅숏 및 백업 파일을 삭제합니다. 다른 방법을 사용하여 파일-스냅숏 백업 집합을 삭제하면 백업 집합의 파일-스냅숏은 삭제되지 않고 백업 파일이 삭제될 수 있습니다.  
  
 **분리된 백업 파일-스냅숏 삭제:** **sys.sp_delete_backup** 시스템 저장 프로시저를 사용하지 않고 백업 파일을 삭제한 경우 또는 데이터베이스 또는 데이터베이스 파일을 포함하는 blob에 연결된 백업 파일-스냅숏이 있는 동안 데이터베이스 또는 데이터베이스 파일을 삭제한 경우 분리된 파일-스냅숏이 있을 수 있습니다. 분리될 수 있는 파일-스냅숏을 식별하려면 **sys.fn_db_backup_file_snapshots** 시스템 함수를 사용하여 데이터베이스 파일의 모든 파일-스냅숏을 나열합니다. 특정 파일-스냅숏 백업 집합의 일부인 파일-스냅숏을 식별하려면 RESTORE FILELISTONLY 시스템 저장 프로시저를 사용합니다. 그런 다음 **sys.sp_delete_backup_file_snapshot** 시스템 저장 프로시저를 사용하여 분리된 개별 백업 파일-스냅숏을 삭제할 수 있습니다. 이 시스템 함수 및 이러한 시스템 저장 프로시저를 사용하는 예제는 이 항목의 끝에 있습니다. 자세한 내용은 [sp_delete_backup&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md), [sys.fn_db_backup_file_snapshots&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md), [sp_delete_backup_file_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) 및 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)를 참조하세요.  
  
### <a name="considerations-and-limitations"></a>고려 사항 및 제한 사항  
 **프리미엄 저장소:** 프리미엄 저장소를 사용하는 경우 다음과 같은 제한 사항이 적용됩니다.  
  
-   프리미엄 저장소를 사용하여 백업 파일 자체를 저장할 수 없습니다.  
  
-   백업 빈도가 10분보다 짧을 수 없습니다.  
  
-   저장할 수 있는 최대 스냅숏 수는 100개입니다.  
  
-   RESTORE WITH MOVE가 필요합니다.  
  
-   프리미엄 저장소에 대한 자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 워크로드용 고성능 저장소](https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/)를 참조하세요.  
  
 **단일 저장소 계정:** 파일-스냅숏 및 대상 Blob에서 동일한 저장소 계정을 사용해야 합니다.  
  
 **대량 복구 모델:** 대량 로그된 복구 모드를 사용하고 최소 로그된 트랜잭션이 포함된 트랜잭션 로그 백업으로 작업하는 경우 트랜잭션 로그 백업을 사용하여 로그 복원(지정 시간 복구 포함)을 수행할 수 없습니다. 대신, 파일-스냅숏 백업 집합의 시점으로 데이터베이스 복원을 수행합니다. 이 제한 사항은 스트리밍 백업의 제한 사항과 동일합니다.  
  
 **온라인 복원:** 파일-스냅숏 백업을 사용하는 경우 온라인 복원을 수행할 수 없습니다. 온라인 복원에 대한 자세한 내용은 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)을 참조하세요.  
  
 **청구:** SQL Server 파일-스냅숏 백업을 사용하는 경우 데이터가 변경되면 추가 요금이 발생합니다. 자세한 내용은 [스냅숏에서 요금이 발생하는 방식 이해](https://msdn.microsoft.com/library/azure/hh768807.aspx)를 참조하세요.  
  
 **보관:** 파일-스냅숏 백업을 보관하려는 경우 Blob 저장소 또는 스트리밍 백업에 보관할 수 있습니다. Blob 저장소에 보관하려면 파일-스냅숏 백업 집합의 스냅숏을 별도 Blob에 복사합니다. 스트리밍 백업에 보관하려면 파일-스냅숏 백업을 새 데이터베이스로 복원한 다음 압축 및/또는 암호화를 사용하여 일반 스트리밍 백업을 수행하고 기본 blob에 독립적으로 원하는 기간 동안 보관합니다.  
  
> [!IMPORTANT]  
>  여러 파일-스냅숏 백업을 유지 관리하는 데에는 약간의 성능 오버헤드만 발생합니다. 그러나 과도한 개수의 파일-스냅숏 백업을 유지 관리하는 경우 데이터베이스의 I/O 성능에 영향을 줄 수 있습니다. 복구 지점 목표를 지원하는 데 필요한 파일-스냅숏 백업만 유지 관리하는 것이 좋습니다.  
  
## <a name="backing-up-the-database-and-log-using-a-file-snapshot-backup"></a>파일-스냅숏 백업을 사용하여 데이터베이스 및 로그 백업  
 아래 예제에서는 파일-스냅숏 백업을 사용하여 AdventureWorks2016 샘플 데이터베이스를 URL에 백업합니다.  
  
```  
-- To permit log backups, before the full database backup, modify the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE AdventureWorks2016  
   SET RECOVERY FULL;  
GO  
-- Back up the full AdventureWorks2016 database.  
BACKUP DATABASE AdventureWorks2016   
TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016.bak'   
WITH FILE_SNAPSHOT;  
GO  
-- Back up the AdventureWorks2016 log using a time stamp in the backup file name.  
DECLARE @Log_Filename AS VARCHAR (300);  
SET @Log_Filename = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_Log_'+   
REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
BACKUP LOG AdventureWorks2016  
 TO URL = @Log_Filename WITH FILE_SNAPSHOT;  
GO  
```  
  
## <a name="restoring-from-a-includessnoversionincludesssnoversion-mdmd-file-snapshot-backup"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일-스냅숏 백업에서 복원  
 다음 예제에서는 트랜잭션 로그 파일-스냅숏 백업 집합을 사용하여 AdventureWorks2016 데이터베이스를 복원하고 복구 작업을 보여 줍니다. 단일 트랜잭션 로그 파일-스냅숏 백업 집합에서 데이터베이스를 복원할 수 있습니다.  
  
```  
RESTORE DATABASE AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_16_00_00.trn'   
WITH RECOVERY, REPLACE;  
GO  
```  
  
## <a name="restoring-from-a-includessnoversionincludesssnoversion-mdmd-file-snapshot-backup-to-a-point-in-time"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일-스냅숏 백업에서 지정 시간으로 복원  
 다음 예제에서는 트랜잭션 로그 파일-스냅숏 백업 집합을 사용하여 지정된 시간의 상태로 AdventureWorks2016 데이터베이스를 복원하고 복구 작업을 보여 줍니다.  
  
```  
RESTORE DATABASE AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_16_00_00.trn'   
WITH NORECOVERY,REPLACE;  
GO   
  
RESTORE LOG AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_18_00_00.trn'   
WITH RECOVERY,STOPAT = 'May 18, 2015 5:35 PM';  
GO  
```  
  
## <a name="deleting-a-database-file-snapshot-backup-set"></a>데이터베이스 파일-스냅숏 백업 집합 삭제  
 파일-스냅숏 백업 집합을 삭제하려면 **sys.sp_delete_backup** 시스템 저장 프로시저를 사용하세요. 시스템에서 지정된 파일-스냅숏 백업 집합이 실제로 지정된 데이터베이스에 대한 백업인지 확인하도록 데이터베이스 이름을 지정합니다. 데이터베이스 이름을 지정하지 않으면 이러한 유효성 검사 없이 지정된 백업 집합이 해당 파일-스냅숏과 함께 삭제됩니다. 자세한 내용은 [sp_delete_backup&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)을 참조하세요.  
  
> [!WARNING]  
>  Microsoft Azure 관리 포털 또는 SQL Server Management Studio의 Azure Storage 뷰어와 같은 다른 방법을 사용하여 파일-스냅숏 백업 집합을 삭제하는 경우 백업 집합의 파일-스냅숏은 삭제되지 않습니다. 이러한 도구는 파일-스냅숏 백업 집합의 파일-스냅숏에 대한 포인터를 포함하는 백업 파일 자체만 삭제합니다. 백업 파일이 잘못 삭제된 후에도 남아 있는 백업 파일-스냅숏을 식별하려면 **sys.fn_db_backup_file_snapshots** 시스템 함수를 사용한 다음 **sys.sp_delete_backup_file_snapshot** 시스템 저장 프로시저를 사용하여 개별 파일-스냅숏 백업을 삭제합니다.  
  
 다음 예제에서는 지정된 백업 집합을 구성하는 파일-스냅숏 및 백업 파일을 포함하여 지정한 파일-스냅숏 백업 집합을 삭제합니다.  
  
```  
sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016.bak', 'adventureworks2016' ;  
GO  
  
```  
  
## <a name="viewing-database-backup-file-snapshots"></a>데이터베이스 백업 파일-스냅숏 보기  
 각 데이터베이스 파일에 대한 기본 Blob의 파일-스냅숏을 보려면 **sys.fn_db_backup_file_snapshots** 시스템 함수를 사용합니다. 이 시스템 함수를 사용하면 Azure Blob 저장소 서비스를 사용하여 저장된 데이터베이스에 대한 각 기본 blob의 모든 백업 파일-스냅숏을 볼 수 있습니다. 이 함수의 주요 사용 사례는 **sys.sp_delete_backup** 시스템 저장 프로시저가 아닌 다른 메커니즘을 사용하여 파일-스냅숏 백업 집합에 대한 백업 파일을 삭제한 경우에 남아 있는 데이터베이스의 백업 파일-스냅숏을 식별하는 것입니다. 원래 백업 집합의 일부인 백업 파일-스냅숏과 원래 백업 집합의 일부가 아닌 백업 파일-스냅숏을 식별하려면 **RESTORE FILELISTONLY** 시스템 저장 프로시저를 사용하여 각 백업 파일에 속한 파일-스냅숏을 나열합니다. 자세한 내용은 [sys.fn_db_backup_file_snapshots&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) 및 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)를 참조하세요.  
  
 다음 예제에서는 지정된 데이터베이스에 대한 모든 백업 파일-스냅숏 목록을 반환합니다.  
  
```  
--Either specify the database name or set the database context  
USE AdventureWorks2016  
select * from sys.fn_db_backup_file_snapshots (null) ;  
GO  
select * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016') ;  
GO  
  
```  
  
## <a name="deleting-an-individual-database-backup-file-snapshot"></a>개별 데이터베이스 백업 파일-스냅숏 삭제  
 데이터베이스 기본 Blob의 개별 백업 파일-스냅숏을 삭제하려면 **sys.sp_delete_backup_file_snapshot** 시스템 저장 프로시저를 사용합니다. 이 시스템 저장 프로시저의 주요 사용 사례는 **sys.sp_delete_backup** 시스템 저장 프로시저가 아닌 다른 방법을 사용하여 백업 파일을 삭제한 후에 남아 있는 분리된 파일-스냅숏 파일을 삭제하는 것입니다. 자세한 내용은 [sp_delete_backup_file_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)을 참조하세요.  
  
> [!WARNING]  
>  파일-스냅숏 백업 집합의 일부인 개별 파일-스냅숏을 삭제하면 백업 집합이 무효화됩니다.  
  
 다음 예제에서는 지정된 백업 파일-스냅숏을 삭제합니다. 지정된 백업의 URL은 **sys.fn_db_backup_file_snapshots** 시스템 함수를 사용하여 가져왔습니다.  
  
```  
sys.sp_delete_backup_file_snapshot N'adventureworks2016', N'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016Data.mdf?snapshot=2015-05-29T21:31:31.6502195Z';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob 저장소 서비스 사용](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)  
  
  
