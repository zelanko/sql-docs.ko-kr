---
title: Azure에 저장 된 백업에서 복원 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6ae358b2-6f6f-46e0-a7c8-f9ac6ce79a0e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1ba9d2e6e607bbfae4ff1232af897145132c9370
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154699"
---
# <a name="restoring-from-backups-stored-in-azure"></a>Azure에 저장 된 백업에서 복원
  이 항목에서는 Azure Blob 저장소 서비스에 저장 된 백업을 사용 하 여 데이터베이스를 복원할 때의 고려 사항에 대해 간략하게 설명 합니다. 이 내용은 URL에 대한 SQL Server 백업이나 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하여 만들어진 백업에 적용됩니다.  
  
 복원 하려는 Azure Blob storage 서비스에 저장 된 백업이 있는 경우이 항목을 검토 하 고 온-프레미스 및 Azure 백업 모두에 대해 동일한 데이터베이스를 복원 하는 방법에 대 한 단계를 설명 하는 항목을 검토 하는 것이 좋습니다.  
  
## <a name="overview"></a>개요  
 온-프레미스 백업에서 데이터베이스를 백업하는 데 사용되는 도구 및 방법은 클라우드 백업에서 데이터베이스를 복원하는 데 적용됩니다.  다음 섹션에서는 이러한 고려 사항 및 Azure Blob storage 서비스에 저장 된 백업을 사용할 때 알아야 하는 차이점에 대해 설명 합니다.  
  
### <a name="using-transact-sql"></a>Transact-SQL 사용  
  
-   SQL Server는 백업 파일을 검색하기 위해 외부 원본에 연결해야 하므로 스토리지 계정을 인증하는 데 SQL 자격 증명이 사용됩니다. 결과적으로 RESTORE 문에 WITH CREDENTIAL 옵션이 필요합니다. 자세한 내용은 [Azure Blob Storage 서비스를 사용 하 여 백업 및 복원 SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)를 참조 하세요.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 사용하여 클라우드로의 백업을 관리하는 경우 **smart_admin.fn_available_backups** 시스템 함수를 사용하여 저장소에서 사용 가능한 모든 백업을 검토할 수 있습니다. 이 시스템 함수는 테이블에 데이터베이스에 대한 사용 가능한 모든 백업을 반환합니다. 결과가 테이블에 반환되면 해당 결과를 필터링하거나 정렬할 수 있습니다. 자세한 내용은 [smart_admin. fn_available_backups &#40;&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)를 참조 하세요.  
  
### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용  
  
-   복원 태스크는 SQL Server Management Studio를 사용하여 데이터베이스를 복원하는 데 사용됩니다. 이제 백업 미디어 페이지에는 Azure Blob 저장소 서비스에 저장 된 백업 파일을 표시 하는 **URL** 옵션이 포함 되어 있습니다. 스토리지 계정 인증에 사용되는 SQL 자격 증명도 제공해야 합니다. **복원에 사용할 백업 세트** 그리드는 Azure Blob 저장소에서 사용 가능한 백업으로 채워집니다. 자세한 내용은 [SQL Server Management Studio를 사용 하 여 Azure storage에서 복원](sql-server-backup-to-url.md#RestoreSSMS)을 참조 하세요.  
  
### <a name="optimizing-restores"></a>복원 최적화  
 복원 쓰기 시간을 줄이려면 SQL Server 사용자 계정에 **볼륨 유지 관리 작업 수행** 사용자 권한을 추가합니다. 자세한 내용은 [데이터베이스 파일 초기화](https://go.microsoft.com/fwlink/?LinkId=271622)를 참조하세요. 즉시 파일 초기화가 설정되었는데도 복원 속도가 느리면 데이터베이스가 백업된 인스턴스에서 로그 파일의 크기를 확인해야 합니다. 로그 크기가 매우 큰 경우(여러 GB) 복원 속도가 느려질 수 있습니다. 복원 중에 로그 파일이 초기화되어야 하며 여기에는 상당한 시간이 걸립니다.  
  
 복원 시간을 단축하기 위해서는 압축된 백업을 사용하는 것이 좋습니다.  25GB를 초과하는 백업 크기에 대해서는 [AzCopy 유틸리티](https://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx) (영문)를 사용하여 로컬 드라이브로 다운로드한 후 복원을 수행하세요. 기타 백업 모범 사례 및 권장 사항에 대해서는 [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](sql-server-backup-to-url-best-practices-and-troubleshooting.md)을 참조하세요.  
  
 추적 플래그 3051을 설정하여 복원을 수행할 때 자세한 로그를 생성할 수도 있습니다. 이 로그 파일은 로그 디렉터리에 배치되며 BackupToUrl-\<instancename>-\<dbname>-action-\<PID>.log. 로그 파일에는 문제를 진단 하는 데 도움이 될 수 있는 시간을 포함 하 여 Azure Storage에 대 한 각 라운드트립에 대 한 정보가 포함 됩니다.  
  
### <a name="topics-on-performing-restore-operations"></a>복원 작업 수행에 대한 항목  
  
-   [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](complete-database-restores-simple-recovery-model.md)  
  
-   [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
-   [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](complete-database-restores-full-recovery-model.md)  
  
-   [파일 복원&#40;단순 복구 모델&#41;](file-restores-simple-recovery-model.md)  
  
-   [파일 복원&#40;전체 복구 모델&#41;](file-restores-full-recovery-model.md)  
  
-   [증분 복원&#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
