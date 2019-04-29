---
title: 트랜잭션 로그 백업(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server[
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6dc94409e607c91944a2263ac5dfb3e8a3f4ce54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920683"
---
# <a name="transaction-log-backups-sql-server"></a>트랜잭션 로그 백업(SQL Server)
  이 항목에서는 전체 또는 대량 로그 복구 모델을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 트랜잭션 로그를 백업하는 방법에 대해 설명합니다.  
  
 로그 백업을 만들려면 최소한 하나의 전체 백업을 만들어야 합니다. 그렇게 해야 로그가 백업 중일 때를 제외하고 언제든지 트랜잭션 로그를 백업할 수 있습니다. 로그 백업을 자주 수행하여 작업 손실 가능성을 최소화하고 트랜잭션 로그를 잘라내는 것이 좋습니다. 데이터베이스 관리자는 보통 주기적(예: 매주)으로 전체 데이터베이스 백업을 만들고, 상황에 따라 더 짧은 간격(예: 매일)으로 차등 데이터베이스 백업을 만듭니다. 또한 데이터베이스 백업과 상관없이 더 자주(예: 매 10분) 트랜잭션 로그를 백업합니다. 지정된 백업 유형의 최적 간격은 데이터의 중요도, 데이터베이스의 크기 및 서버의 작업과 같은 요소에 따라 달라집니다.  
  
 **항목 내용:**  
  
-   [로그 백업 시퀀스의 작동 원리](#LogBackupSequence)  
  
-   [권장 사항](#Recommendations)  
  
-   [관련 작업](#RelatedTasks)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="LogBackupSequence"></a> 로그 백업 시퀀스의 작동 원리  
 트랜잭션 로그 백업 *로그 체인* 시퀀스는 데이터 백업과 독립되어 있습니다. 예를 들어 이벤트가 다음과 같은 순서로 발생한다고 가정합니다.  
  
| Time |이벤트|  
|----------|-----------|  
|8:00 A.M.|데이터베이스를 백업합니다.|  
|정오|트랜잭션 로그를 백업합니다.|  
|오후 4:00|트랜잭션 로그를 백업합니다.|  
|오후 6:00|데이터베이스를 백업합니다.|  
|8:00 P.M.|트랜잭션 로그를 백업합니다.|  
  
 저녁 8시에 만든 트랜잭션 로그 백업에는 오후 4시부터 저녁 8시까지 기록한 트랜잭션 로그 레코드가 포함됩니다. 이 시간대에는 전체 데이터베이스 백업을 만든 오후 6시도 포함됩니다. 트랜잭션 로그 백업의 시퀀스는 오전 8시에 만든 첫째 전체 데이터베이스 백업부터 저녁 8시에 만든 마지막 트랜잭션 로그 백업까지 이어집니다. 이러한 로그 백업을 적용하는 방법은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)의 예제를 참조하세요.  
  
##  <a name="Recommendations"></a> 권장 사항  
  
-   트랜잭션 로그가 손상되면 최근의 유효 백업 이후에 수행한 작업이 손실됩니다. 따라서 내결함성이 있는 스토리지에 로그 파일을 보관하는 것이 좋습니다.  
  
-   데이터베이스가 손상되었거나 데이터베이스를 복원하려는 경우에는 데이터베이스를 현재의 지정 시간으로 복원할 수 있도록 [비상 로그 백업](tail-log-backups-sql-server.md) 을 만드는 것이 좋습니다.  
  
-   기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 로그를 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **트랜잭션 로그 백업을 만들려면**  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 백업 작업을 예약하려면 [Use the Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md)을 참조하세요.  
  
##  <a name="RelatedContent"></a> 관련 내용  
 없음  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 로그&#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [SQL Server 데이터베이스 백업 및 복원](back-up-and-restore-of-sql-server-databases.md)   
 [비상 로그 백업&#40;SQL Server&#41;](tail-log-backups-sql-server.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)  
  
  
