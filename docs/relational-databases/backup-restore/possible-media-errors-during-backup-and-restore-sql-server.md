---
title: "백업 및 복원 중 발생 가능한 미디어 오류(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- media errors [SQL Server]
- CONTINUE_AFTER_ERROR option
- errors [SQL Server], backups
- backups [SQL Server], errors
- RESTORE VERIFYONLY statement
- backup media [SQL Server], error management
- page checksums [SQL Server]
- backup checksums [SQL Server]
- backing up [SQL Server], media errors
- RESTORE statement, media errors
- NO_CHECKSUM option
- checksums [SQL Server]
ms.assetid: 83a27b29-1191-4f8d-9648-6e6be73a9b7c
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 750aa24dcfae82a4e44a32de345299a964df0de8
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="possible-media-errors-during-backup-and-restore-sql-server"></a>백업 및 복원 중 발생 가능한 미디어 오류(SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 오류가 검색되면 데이터베이스를 복구할 수 있는 옵션을 제공합니다. 중요한 새 오류 검색 메커니즘을 사용하면 백업 작업으로 만들고 복원 작업으로 유효성을 검사할 수 있는 백업 체크섬을 만들 수 있습니다. 작업에서 오류를 검사할지 여부 및 오류 발생 시 작업을 중지할지 아니면 계속할지를 제어할 수 있습니다. 백업에 백업 체크섬이 들어 있으면 RESTORE 문과 RESTORE VERIFYONLY 문으로 오류를 검사할 수 있습니다.  
  
> [!NOTE]  
>  미러된 백업은 미디어 세트 복사본(미러)을 4개까지 제공하고 손상된 미디어로 인한 오류를 복구하기 위한 대체 복사본을 제공합니다. 자세한 내용은 [미러된 백업 미디어 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)를 참조하세요.  
  
  
##  <a name="BckChecksums"></a> 백업 체크섬  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 페이지 체크섬, 로그 블록 체크섬 및 백업 체크섬의 3가지 유형의 체크섬을 지원합니다. 백업 체크섬을 생성할 때 BACKUP은 데이터베이스에서 읽은 데이터가 데이터베이스에 들어 있는 체크섬이나 조각난 페이지 표시와 일치하는지 확인합니다.  
  
 BACKUP 문은 필요에 따라 백업 스트림에 대한 백업 체크섬을 계산합니다. 페이지 체크섬 또는 조각난 페이지 정보가 지정한 페이지에 있을 경우 BACKUP은 해당 페이지를 백업하면서 해당 페이지의 체크섬과 조각난 페이지 상태 및 페이지 ID도 확인합니다. 백업 체크섬을 만들 때 백업 작업은 체크섬을 페이지에 추가하지 않습니다. 페이지는 데이터베이스에 있는 대로 백업되고 페이지가 백업에 의해 수정되지 않습니다.  
  
 백업 체크섬을 사용하면 백업 체크섬을 확인하고 생성하는 오버헤드로 인해 성능이 저하될 수 있습니다. 작업과 백업 처리량이 모두 영향을 받을 수 있습니다. 그러므로 백업 체크섬은 필요한 경우에만 사용하세요. 백업하는 동안 체크섬을 생성하기로 결정했으면 시스템에서 실행 중인 동시 작업에 대한 영향과 CPU 오버헤드 발생을 주의 깊게 모니터링하세요.  
  
 BACKUP은 디스크에 있는 원본 페이지와 페이지의 내용을 절대로 수정하지 않습니다.  
  
 백업 체크섬을 사용하도록 설정하면 백업 작업에서 다음 단계가 수행됩니다.  
  
1.  백업 미디어에 페이지를 쓰기 전에 백업 작업은 페이지 체크섬 또는 조각난 페이지 검색 등 페이지 수준 정보(있는 경우)를 확인합니다. 아무 것도 없으면 백업이 페이지를 확인할 수 없습니다. 확인할 수 없으면 페이지가 있는 그대로 포함되고 해당 콘텐츠가 전체 백업 체크섬에 추가됩니다.  
  
     확인 중 백업 작업에 페이지 오류가 발생할 경우 백업이 실패합니다.  
  
    > [!NOTE]  
    >  페이지 체크섬과 조각난 페이지 검색에 대한 자세한 내용은 ALTER DATABASE 문의 PAGE_VERIFY 옵션을 참조하세요. 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
2.  페이지 체크섬이 있는지 여부에 관계없이 BACKUP은 백업 스트림에 대해 별도의 백업 체크섬을 생성합니다. 복원 작업은 경우에 따라 백업 체크섬을 사용하여 백업이 손상되지 않았는지 확인할 수 있습니다. 백업 체크섬은 데이터베이스 페이지가 아니라 백업 미디어에 저장됩니다. 백업 체크섬은 복원할 때 사용되기도 합니다.  
  
3.  백업 세트의 플래그는 **msdb..backupset** 의 **has_backup_checksums**열에서 포함 백업 체크섬으로 지정됩니다. 자세한 내용은 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)를 참조하세요.  
  
 복원 작업 중 백업 미디어에 백업 체크섬이 있을 경우 기본적으로 RESTORE 문과 RESTORE VERIFYONLY 문은 백업 체크섬과 페이지 체크섬을 모두 확인합니다. 백업 체크섬이 없을 경우 복원 작업은 확인 없이 진행됩니다. 백업 체크섬이 없으면 복원이 페이지 체크섬을 안정적으로 확인할 수 없기 때문입니다.  
  
## <a name="response-to-page-checksum-errors-during-a-backup-or-restore-operation"></a>백업 또는 복원 작업 중에 페이지 체크섬 오류에 응답  
 기본적으로 페이지 체크섬 오류가 발생한 후 BACKUP 또는 RESTORE 작업이 실패하고 RESTORE VERIFYONLY 작업이 계속됩니다. 하지만 오류가 발생할 때 지정된 작업이 실패하도록 하거나 가능한 한 작업을 계속하도록 할지를 제어할 수 있습니다.  
  
 오류가 발생한 후 BACKUP 작업이 계속될 경우 작업에서 다음 단계가 수행됩니다.  
  
1.  백업 미디어의 백업 세트에 오류가 포함되었다는 플래그를 지정하고 **msdb** 데이터베이스의 **suspect_pages** 테이블에 들어 있는 페이지를 추적합니다. 자세한 내용은 [suspect_pages&#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)를 참조하세요.  
  
2.  SQL Server 오류 로그에 오류를 기록합니다.  
  
3.  **msdb.backupset** 의 **is_damaged**열에 이런 종류의 오류가 들어 있는 것으로 백업 세트를 표시합니다. 자세한 내용은 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)를 참조하세요.  
  
4.  백업이 생성되었지만 페이지 오류가 있다는 메시지를 표시합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **백업 체크섬을 설정 또는 해제하려면**  
  
-   [백업 또는 복원 중 백업 체크섬 설정 또는 해제&#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
 **백업 작업 중 오류에 대한 응답을 제어하려면**  
  
-   [오류 발생 후 백업 또는 복원 작업 계속 또는 중지 여부 지정&#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [미러된 백업 미디어 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
  
