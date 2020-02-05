---
title: Microsoft Azure에 저장된 백업에서 복원 | Microsoft 문서
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6ae358b2-6f6f-46e0-a7c8-f9ac6ce79a0e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cda4fd3fa0bbb66e95d61ec87ff66dee809e2962
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70155447"
---
# <a name="restoring-from-backups-stored-in-microsoft-azure"></a>Microsoft Azure에 저장된 백업에서 복원
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 Azure Blob Storage 서비스에 저장된 백업을 사용하여 데이터베이스를 복원할 때의 고려 사항에 대해 간단히 설명합니다. 이 내용은 URL에 대한 SQL Server 백업이나 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하여 만들어진 백업에 적용됩니다.  
  
 복원할 백업이 Azure Blob Storage 서비스에 저장되어 있는 경우 이 항목을 검토한 다음 온-프레미스 백업과 Azure 백업 모두에 동일한 데이터베이스 복원 방법에 대한 단계를 설명하는 항목을 검토하는 것이 좋습니다.  
  
## <a name="overview"></a>개요  
 온-프레미스 백업에서 데이터베이스를 백업하는 데 사용되는 도구 및 방법은 클라우드 백업에서 데이터베이스를 복원하는 데 적용됩니다.  다음 섹션에서는 이러한 고려 사항 및 Azure Blob Storage 서비스에 저장된 백업을 사용할 때 알아야 하는 모든 차이점에 대해 설명합니다.  
  
### <a name="using-transact-sql"></a>Transact-SQL 사용  
  
-   SQL Server는 백업 파일을 검색하기 위해 외부 원본에 연결해야 하므로 스토리지 계정을 인증하는 데 SQL 자격 증명이 사용됩니다. 결과적으로 RESTORE 문에 WITH CREDENTIAL 옵션이 필요합니다. 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 사용하여 클라우드로의 백업을 관리하는 경우 **smart_admin.fn_available_backups** 시스템 함수를 사용하여 스토리지에서 사용 가능한 모든 백업을 검토할 수 있습니다. 이 시스템 함수는 테이블에 데이터베이스에 대한 사용 가능한 모든 백업을 반환합니다. 결과가 테이블에 반환되면 해당 결과를 필터링하거나 정렬할 수 있습니다. 자세한 내용은 [managed_backup.fn_available_backups&#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md)을(를) 참조하세요.  
  
### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용  
  
-   복원 태스크는 SQL Server Management Studio를 사용하여 데이터베이스를 복원하는 데 사용됩니다. 이제 백업 미디어 페이지에 Azure Blob Storage 서비스에 저장된 백업 파일을 표시하는 **URL** 옵션이 포함됩니다. 스토리지 계정 인증에 사용되는 SQL 자격 증명도 제공해야 합니다. 그러면 **복원할 백업 세트** 그리드가 Azure Blob Storage의 사용 가능한 백업으로 채워집니다. 자세한 내용은 [SQL Server Management Studio를 사용하여 Azure Storage에서 복원](../../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS)을 참조하세요.  
  
### <a name="optimizing-restores"></a>복원 최적화  
 복원 쓰기 시간을 줄이려면 SQL Server 사용자 계정에 **볼륨 유지 관리 작업 수행** 사용자 권한을 추가합니다. 자세한 내용은 [데이터베이스 파일 초기화](https://go.microsoft.com/fwlink/?LinkId=271622)를 참조하세요. 즉시 파일 초기화가 설정되었는데도 복원 속도가 느리면 데이터베이스가 백업된 인스턴스에서 로그 파일의 크기를 확인해야 합니다. 로그 크기가 매우 큰 경우(여러 GB) 복원 속도가 느려질 수 있습니다. 복원 중에 로그 파일이 초기화되어야 하며 여기에는 상당한 시간이 걸립니다.  
  
 복원 시간을 단축하기 위해서는 압축된 백업을 사용하는 것이 좋습니다.  25GB를 초과하는 백업 크기에 대해서는 [AzCopy 유틸리티](https://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx) (영문)를 사용하여 로컬 드라이브로 다운로드한 후 복원을 수행하세요. 기타 백업 모범 사례 및 권장 사항에 대해서는 [SQL Server Backup to URL Best Practices and Troubleshooting](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)을 참조하세요.  
  
 추적 플래그 3051을 설정하여 복원을 수행할 때 자세한 로그를 생성할 수도 있습니다. 이 로그 파일은 로그 디렉터리에 배치되며 BackupToUrl-\<instancename>-\<dbname>-action-\<PID>.log 형식을 사용하여 이름이 지정됩니다. 로그 파일에는 문제 진단에 도움이 될 수 있는 시간을 비롯하여 각각의 Azure Storage 왕복에 대한 정보가 포함됩니다.  
  
### <a name="topics-on-performing-restore-operations"></a>복원 작업 수행에 대한 항목  
  
-   [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
-   [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
  
-   [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)  
  
-   [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
