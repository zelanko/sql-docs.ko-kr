---
title: 트랜잭션 로그 백업(SQL Server) | Microsoft 문서
description: 데이터베이스 백업과 상관없이 자주 SQL Server 트랜잭션 로그를 백업할 수 있습니다. 트랜잭션 로그 백업의 시퀀스는 로그 체인입니다.
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server]
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ec8d0f5d72a6f195f489d67d6df32c2f33da7f12
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85642879"
---
# <a name="transaction-log-backups-sql-server"></a>트랜잭션 로그 백업(SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 전체 또는 대량 로그 복구 모델을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 트랜잭션 로그를 백업하는 방법에 대해 설명합니다.  
  
 로그 백업을 만들려면 최소한 하나의 전체 백업을 만들어야 합니다. 그렇게 해야 로그가 백업 중일 때를 제외하고 언제든지 트랜잭션 로그를 백업할 수 있습니다. 
 
로그 백업을 자주 수행하여 작업 손실 가능성을 최소화하고 트랜잭션 로그를 잘라내는 것이 좋습니다. 
 
데이터베이스 관리자는 보통 주기적(예: 매주)으로 전체 데이터베이스 백업을 만들고, 상황에 따라 더 짧은 간격(예: 매일)으로 차등 데이터베이스 백업을 만듭니다. 또한 데이터베이스 백업과 상관없이 더 자주 트랜잭션 로그를 백업합니다. 지정된 백업 유형의 최적 간격은 데이터의 중요도, 데이터베이스의 크기 및 서버의 작업과 같은 요소에 따라 달라집니다. 좋은 전략을 구현하는 방법에 대한 자세한 내용은 이 항목의 [권장 사항](#Recommendations)을 참조하세요. 
   
##  <a name="how-a-sequence-of-log-backups-works"></a><a name="LogBackupSequence"></a> 로그 백업 시퀀스의 작동 방법  
 트랜잭션 로그 백업 *로그 체인* 시퀀스는 데이터 백업과 독립되어 있습니다. 예를 들어 이벤트가 다음과 같은 순서로 발생한다고 가정합니다.  
  
|Time|이벤트|  
|----------|-----------|  
|8:00 AM|데이터베이스를 백업합니다.|  
|정오|트랜잭션 로그를 백업합니다.|  
|4:00 PM|트랜잭션 로그를 백업합니다.|  
|6:00 PM|데이터베이스를 백업합니다.|  
|8:00 PM|트랜잭션 로그를 백업합니다.|  
  
 8:00 PM에 생성된 트랜잭션 로그 백업에는 4:00 PM부터 전체 데이터베이스 백업이 생성된 6:00 PM을 거쳐 8:00 PM까지의 트랜잭션 로그 레코드가 포함됩니다. 트랜잭션 로그 백업 순서는 8:00 AM에 생성된 초기 전체 데이터베이스 백업부터 8:00 PM에 생성된 마지막 트랜잭션 로그 백업에 이르기까지 연속적입니다. 이러한 로그 백업을 적용하는 방법은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)의 예제를 참조하세요.  
  
##  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   트랜잭션 로그가 손상되면 최근의 유효 백업 이후에 수행한 작업이 손실됩니다. 따라서 내결함성이 있는 스토리지에 로그 파일을 보관하는 것이 좋습니다.  
  
-   데이터베이스가 손상되었거나 데이터베이스를 복원하려는 경우에는 데이터베이스를 현재의 지정 시간으로 복원할 수 있도록 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) 을 만드는 것이 좋습니다.  
  
-   기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 로그를 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.  

-   비즈니스 요구 사항, 특히 손상된 로그 스토리지에 의해 발생될 수 있는 작업 손실에 대한 허용 범위를 지원하기 위해 로그 백업을 충분히 자주 수행합니다. 
   -   로그 백업의 적절한 수행 빈도는 저장 및 관리는 물론 복원까지 가능할 수 있는 로그 백업의 횟수에 의해 조정되는 작업 손실 위험에 대한 허용 범위에 따라 달라집니다. 복구 전략을 구현할 때 필요한 [RTO](https://wikipedia.org/wiki/Recovery_time_objective) 및 [RPO](https://wikipedia.org/wiki/Recovery_point_objective), 특히 로그 백업 케이던스에 대해 생각해보세요.
   -   로그 백업에 걸리는 시간은 매 15분에서 30분이면 충분합니다. 비즈니스에서 작업 손실 위험을 최소화하려는 경우에는 로그 백업을 더 자주 수행해야 합니다. 로그 백업 횟수가 많아지면 로그 잘림이 더 자주 발생하여 로그 파일의 크기가 작아지는 이점이 있습니다.  
  
> [!IMPORTANT]
> 복원해야 하는 로그 백업의 수를 제한하려면 데이터를 정기적으로 백업해야 합니다. 예를 들어 주별 전체 데이터베이스 백업과 일별 차등 데이터베이스 백업을 예약할 수 있습니다.  
> 또 복구 전략을 구현할 때 필요한 [RTO](https://wikipedia.org/wiki/Recovery_time_objective) 및 [RPO](https://wikipedia.org/wiki/Recovery_point_objective), 특히 전체 및 차등 데이터베이스 백업 케이던스에 대해 생각해보세요.
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
 **트랜잭션 로그 백업을 만들려면**  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 백업 작업을 예약하려면 [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)을 참조하세요.  
  

## <a name="see-also"></a>참고 항목  
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드의 트랜잭션 로그 백업](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)     
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
