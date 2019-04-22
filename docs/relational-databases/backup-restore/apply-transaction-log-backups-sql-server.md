---
title: 트랜잭션 로그 백업 적용(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 08/14/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 777b83d5021a61ea42610680d52345ad4ca001b5
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240593"
---
# <a name="apply-transaction-log-backups-sql-server"></a>트랜잭션 로그 백업 적용(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 전체 복구 모델 또는 대량 로그 복구 모델과 관련된 내용을 다룹니다.  
  
 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 복원의 일부로 수행되는 트랜잭션 로그 백업 적용에 대해 설명합니다.  
 
  
##  <a name="Requirements"></a> 트랜잭션 로그 백업 복원을 위한 요구 사항  
 트랜잭션 로그 백업을 적용하려면 다음 요구 사항을 충족해야 합니다.  
  
-   **복원 시퀀스를 위한 충분한 로그 백업:** 복원 순서를 완료하려면 백업된 로그 레코드가 충분히 있어야 합니다. 복원 시퀀스를 시작하려면 필요한 로그 백업(필요한 경우 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) 을 포함)을 반드시 확보해야 합니다.  
  
-   **올바른 복원 순서:**  바로 이전의 전체 데이터베이스 백업 또는 차등 데이터베이스 백업을 먼저 복원해야 합니다. 그런 후 전체 또는 차등 데이터베이스 백업 후에 생성된 모든 트랜잭션 로그를 시간순으로 복원해야 합니다. 이 로그 체인의 트랜잭션 로그 백업이 손실되거나 손상된 경우 손실된 트랜잭션 로그 이전의 트랜잭션 로그만 복원할 수 있습니다.  
  
-   **아직 복구되지 않은 데이터베이스:**  마지막 트랜잭션 로그가 적용될 때까지 데이터베이스를 복구할 수 없습니다. 로그 체인이 끝나기 이전의 중간 트랜잭션 로그 백업 중 하나를 복원한 후 데이터베이스를 복구할 경우 해당 시점 이후의 데이터베이스를 복원하려면 전체 데이터베이스 백업부터 시작하여 전체 복원 시퀀스를 다시 시작해야 합니다.  
  
    > **팁** 최선의 방법은 모든 로그 백업을 복원하는 것입니다(RESTORE LOG *database_name* WITH NORECOVERY). 그런 후 마지막 로그 백업을 복원한 후 데이터베이스를 별도의 작업으로 복구합니다(RESTORE DATABASE *database_name* WITH RECOVERY).  
  
##  <a name="RecoveryAndTlogs"></a> 복구 및 트랜잭션 로그  
 복원 작업을 완료하고 데이터베이스를 복구할 때 완료되지 않은 트랜잭션은 모두 롤백되는데 이것을 *실행 취소 단계*라고 합니다. 롤백은 데이터베이스의 무결성을 복원하는 데 필요합니다. 롤백 후 데이터베이스는 온라인 상태가 되고 트랜잭션 로그 백업이 더 이상 데이터베이스에 적용되지 않습니다.  
  
 예를 들어 일련의 트랜잭션 로그 백업은 장기 실행 트랜잭션을 포함합니다. 트랜잭션의 시작은 첫 번째 트랜잭션 로그 백업에 기록되지만 트랜잭션의 끝은 두 번째 트랜잭션 로그 백업에 기록됩니다. 첫 번째 트랜잭션 로그 백업에는 커밋 또는 롤백 작업의 기록이 없습니다. 첫 번째 트랜잭션 로그 백업이 적용될 때 복구 작업이 실행되면 장기 실행 트랜잭션은 완료되지 않은 것으로 취급되고 해당 트랜잭션에 대한 첫 번째 트랜잭션 로그 백업에 기록된 데이터 수정이 롤백됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이 시점 이후에 두 번째 트랜잭션 로그 백업을 적용할 수 없습니다.  
  
> **참고:** 경우에 따라서는 로그 복원 중에 파일을 명시적으로 추가할 수 있습니다.  
  
##  <a name="PITrestore"></a> 로그 백업을 사용하여 오류 지점까지 복원  
 예를 들어 다음과 같은 순서의 이벤트가 발생한다고 가정합니다.  
  
|Time|이벤트|  
|----------|-----------|  
|8:00 A.M.|데이터베이스를 백업하여 전체 데이터베이스 백업을 만듭니다.|  
|정오|트랜잭션 로그를 백업합니다.|  
|오후 4:00|트랜잭션 로그를 백업합니다.|  
|오후 6:00|데이터베이스를 백업하여 전체 데이터베이스 백업을 만듭니다.|  
|8:00 P.M.|트랜잭션 로그를 백업합니다.|  
|9:45 P.M.|오류가 발생합니다.|  
  
> 이 백업 시퀀스의 예제에 대한 설명은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)을 참조하세요.  
  
 데이터베이스를 오류 발생 시점인 오후 9:45의 상태로 복원하려면 다음 대체 절차 중 하나를 사용하십시오.  

[!INCLUDE[Freshness](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 **대체 1: 가장 최근의 전체 데이터베이스 백업을 사용하여 데이터베이스 복원**  
  
1.  오류 발생 시점에 활성화되어 있던 트랜잭션 로그의 비상 로그 백업을 만듭니다.  
  
2.  8:00 A.M.의 전체 데이터베이스 백업을 시간이 오래 걸립니다. 대신 가장 최근의 6:00 P.M. 전체 데이터베이스 백업을 복원한 다음 8:00 P.M. 로그 백업 및 비상 로그 백업을 적용합니다.  
  
 **대체 2: 이전의 전체 데이터베이스 백업을 사용하여 데이터베이스 복원**  
  
> 이 대체 프로세스는 문제로 인해 6:00 P.M.의 전체 데이터베이스 백업을 사용할 수 없는 경우에 시간이 오래 걸립니다. 6:00 P.M.의 전체 데이터베이스 백업에서 복원하는 것보다 시간이 오래 걸립니다.  
  
1.  오류 발생 시점에 활성화되어 있던 트랜잭션 로그의 비상 로그 백업을 만듭니다.  
  
2.  8:00 A.M.의 전체 데이터베이스 백업을 복원한 다음 4개의 트랜잭션 로그 백업을 순서대로 복원합니다. 이렇게 하면 완료된 모든 트랜잭션을 9:45 P.M.까지 롤포워드합니다.  
  
     이 대체 프로세스를 통해 일련의 전체 데이터베이스 백업에서 트랜잭션 로그 백업 체인을 유지함으로써 제공되는 중복 보안을 확인할 수 있습니다.  
  
> 경우에 따라 트랜잭션 로그를 사용하여 데이터베이스를 지정 시간으로 복원할 수도 있습니다. 자세한 내용은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)라고 합니다.  
  
##  <a name="RelatedTasks"></a> Related tasks  
 **트랜잭션 로그 백업을 적용하려면**  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
 **복구 지점으로 복원하려면**  
  
-   [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [표시된 트랜잭션이 포함된 관련 데이터베이스 복구](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [로그 시퀀스 번호로 복구&#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
 **WITH NORECOVERY를 사용하여 백업을 복원한 후 데이터베이스를 복구하려면**  
  
-   [데이터를 복원하지 않고 데이터베이스 복구&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목:  
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
