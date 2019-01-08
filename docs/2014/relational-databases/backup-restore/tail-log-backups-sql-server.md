---
title: 비상 로그 백업(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], tail of log
- transaction log backups [SQL Server], tail-log backups
- NO_TRUNCATE clause
- backups [SQL Server], log backups
- tail-log backups
- backups [SQL Server], tail-log backups
ms.assetid: 313ddaf6-ec54-4a81-a104-7ffa9533ca58
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6da8f9de22f1b3191d6fba1918e8c05a64d062f2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507367"
---
# <a name="tail-log-backups-sql-server"></a>비상 로그 백업(SQL Server)
  이 항목에서는 전체 또는 대량 로그 복구 모델을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 백업 및 복원과 관련된 내용을 다룹니다.  
  
 *비상 로그 백업* 에서는 아직 백업되지 않은 로그 레코드를 캡처하여( *비상 로그*) 캡처하여 작업 손실을 방지하고 로그 체인을 그대로 유지합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 마지막 시점으로 복구하려면 트랜잭션 비상 로그를 백업해야 합니다. 비상 로그 백업은 데이터베이스에 대한 복구 계획의 마지막 백업입니다.  
  
> [!NOTE]  
>  모든 복원 시나리오에서 비상 로그 백업이 필요한 것은 아닙니다. 복구 시점이 이전 로그 백업에 포함될 경우에는 비상 로그 백업이 필요하지 않습니다. 데이터베이스를 이동 또는 대체(덮어쓰기)하며 가장 최근 백업 이후의 시점으로 이를 복원할 필요가 없을 경우에도 비상 로그 백업이 필요하지 않습니다.  
  
 
  
##  <a name="TailLogScenarios"></a> 비상 로그 백업이 필요한 시나리오  
 다음과 같은 경우에는 비상 로그 백업을 수행하는 것이 좋습니다.  
  
-   데이터베이스가 온라인이며 데이터베이스에서 복원 작업을 수행하려는 경우 먼저 비상 로그를 백업합니다. 온라인 데이터베이스에 대한 오류를 방지하려면 다음을 사용해야 합니다... WITH NORECOVERY 옵션입니다 합니다 [BACKUP](/sql/t-sql/statements/backup-transact-sql) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.  
  
-   데이터베이스가 오프라인이고 시작되지 않아서 데이터베이스를 복원해야 할 경우 먼저 비상 로그를 백업합니다. 이 시점에서는 트랜잭션이 발생할 수 없으므로 WITH NORECOVERY 옵션의 사용은 선택 사항입니다.  
  
-   데이터베이스가 손상된 경우 BACKUP 문의 WITH CONTINUE_AFTER_ERROR 옵션을 사용하여 비상 로그 백업을 수행합니다.  
  
     손상된 데이터베이스에 대한 비상 로그 백업은 로그 파일이 손상되지 않고, 데이터베이스가 비상 로그 백업을 지원하는 상태에 있고, 데이터베이스에 대량 로깅된 변경 내용이 없는 경우에만 성공할 수 있습니다. 배상 로그 백업을 만들 수 없는 경우 마지막 로그 백업 이후에 커밋된 모든 트랜잭션은 손실됩니다.  
  
 다음 표에는 BACKUP NORECOVERY 및 CONTINUE_AFTER_ERROR 옵션이 요약되어 있습니다.  
  
|BACKUP LOG 옵션|주석|  
|-----------------------|--------------|  
|NORECOVERY|데이터베이스에서 복원 작업을 계속하려는 경우 NORECOVERY를 사용합니다. NORECOVERY는 데이터베이스를 복원 중인 상태로 만듭니다. 이렇게 하면 비상 로그 백업 후 데이터베이스가 변경되지 않습니다.  NO_TRUNCATE 옵션 또는 COPY_ONLY 옵션을 함께 지정하지 않으면 로그가 잘립니다.<br /><br /> **\*\* 중요 \* \***  데이터베이스 손상 된 경우가 아니면 NO_TRUNCATE는 사용 하지 않는 것이 좋습니다.|  
|CONTINUE_AFTER_ERROR|손상된 데이터베이스의 비상 로그를 백업하는 경우에만 CONTINUE_AFTER_ERROR를 사용합니다.<br /><br /> 참고: 손상된 데이터베이스에서 비상 로그 백업을 사용하는 경우에는 일반적으로 로그 백업에서 캡처되는 메타데이터 일부를 사용할 수 없을 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [완전하지 않은 백업 메타데이터가 포함된 비상 로그 백업](#IncompleteMetadata)을 참조하세요.|  
  
##  <a name="IncompleteMetadata"></a> 완전하지 않은 백업 메타데이터가 포함된 비상 로그 백업  
 비상 로그 백업은 데이터베이스가 오프라인이거나 손상되었거나 데이터 파일이 없는 경우에도 비상 로그를 캡처합니다. 이로 인해 복원 정보 명령과 **msdb**의 메타데이터가 완전하지 않을 수 있습니다. 그러나 메타데이터가 완전하지 않은 경우에도 캡처된 로그는 완전한 상태이며 사용 가능합니다.  
  
 비상 로그 백업에 완전하지 않은 메타데이터가 있으면 [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) 테이블의 **has_incomplete_metadata** 가 **1**로 설정됩니다. 또한 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)출력에서 **HasIncompleteMetadata** 는 **1**로 설정됩니다.  
  
 비상 로그 백업의 메타데이터가 완전하지 않으면 [backupfilegroup](/sql/relational-databases/system-tables/backupfilegroup-transact-sql) 테이블은 비상 로그 백업 당시 파일 그룹에 대한 대부분의 정보를 잃게 됩니다. 대부분의 **backupfilegroup** 테이블 열은 NULL이 되며 다음 열만 의미를 갖습니다.  
  
-   **backup_set_id**  
  
-   **filegroup_id**  
  
-   **유형**  
  
-   **type_desc**  
  
-   **is_readonly**  
  
##  <a name="RelatedTasks"></a> 관련 작업  
 비상 로그 백업을 만들려면 [데이터베이스가 손상된 경우 트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)을 참조하세요.  
  
 트랜잭션 로그 백업을 복원하려면 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [SQL Server 데이터베이스 백업 및 복원](back-up-and-restore-of-sql-server-databases.md)   
 [복사 전용 백업&#40;SQL Server&#41;](copy-only-backups-sql-server.md)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)  
  
  
