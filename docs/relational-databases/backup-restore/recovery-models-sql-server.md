---
title: 복구 모델(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 07/16/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- bulk-logged recovery model [SQL Server]
- recovery [SQL Server], recovery model
- restoring transaction logs [SQL Server], recovery models
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], about
- transaction log backups [SQL Server]
- simple recovery model [SQL Server]
- backups [SQL Server], recovery models
- recovery models [SQL Server]
- recovery models [SQL Server], transaction log management
- database restores [SQL Server], recovery models
- transaction log restores [SQL Server]
- logs [SQL Server], recovery models
- restoring databases [SQL Server], recovery models
- full recovery model [SQL Server]
- backing up transaction logs [SQL Server], recovery models
ms.assetid: 8cfea566-8f89-4581-b30d-c53f1f2c79eb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0c8c2efee10a38120717487fc6e04429de7f1bf6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653451"
---
# <a name="recovery-models-sql-server"></a>복구 모델(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원 작업은 데이터베이스 복구 모델의 컨텍스트 내에서 수행됩니다. 복구 모델은 트랜잭션 로그 유지 관리를 제어합니다. *복구 모델* 은 트랜잭션이 로깅되는 방법, 트랜잭션 로그에 백업이 필요하며 허용되는지 여부 및 사용 가능한 복원 작업의 종류를 제어하는 데이터베이스 속성입니다. 사용할 수 있는 복구 모델은 3가지로 단순, 전체 및 대량 로그 복구 모델입니다. 일반적으로 데이터베이스는 전체 복구 모델이나 단순 복구 모델을 사용합니다. 데이터베이스는 언제든지 다른 복구 모델로 전환이 가능합니다.  
  
 **항목 내용:**  
  
-   [복구 모델 개요](#RMov)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="RMov"></a> 복구 모델 개요  
 다음 표에서는 세 가지 복구 모델을 요약합니다.  
  
|복구 모델|설명|작업 손실 가능성|정해진 시간에 복구 가능 여부|  
|--------------------|-----------------|------------------------|-------------------------------|  
|**간단**|로그 백업 없음<br /><br /> 로그 공간을 자동으로 회수하여 공간 요구 사항을 적게 유지함으로써 트랜잭션 로그 공간을 관리할 필요가 없도록 함 단순 복구 모델에서의 데이터베이스 백업에 대한 자세한 내용은 [전체 데이터베이스 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)을 참조하세요.<br /><br /> 트랜잭션 로그 백업이 필요한 작업에는 단순 복구 모델이 지원되지 않습니다. 다음 기능은 단순 복구 모드에서 사용할 수 없습니다.<br /><br /> -로그 전달<br /><br /> -Always On 또는 데이터베이스 미러링<br /><br /> -데이터 손실 없는 미디어 복구<br /><br /> -지정 시간 복원|가장 최근 백업 이후의 변경 내용은 보호되지 않음. 재해가 발생할 경우 이러한 변경 내용을 다시 실행해야 함|백업의 끝으로만 복구 가능 자세한 내용은 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)을 참조하세요. <br><br> 단순 복구 모델에 대한 자세한 내용은 [SQL Server 단순 복구 모델](https://www.mssqltips.com/sqlservertutorial/4/sql-server-simple-recovery-model/) 의 동료들이 제공한 [SQL Server 단순 복구 모델](https://www.mssqltips.com)을 참조하세요.|  
|**전체**|로그 백업 필요<br /><br /> 데이터 파일의 손실 또는 손상으로 인한 작업의 손실이 없음<br /><br /> 임의의 지정 시간으로 복구 가능(예: 응용 프로그램이나 사용자 오류가 발생하기 이전) 전체 복구 모델에서 데이터베이스 백업에 대한 자세한 내용은 [전체 데이터베이스 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md) 및 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)을 참조하세요.|일반적으로는 없음<br /><br /> 비상 로그가 손상된 경우 가장 최근에 로그를 백업한 후에 변경된 사항을 다시 실행해야 함.|백업이 특정 시점까지 완료된 경우 해당 시점으로 복구 가능. 로그 백업을 사용하여 오류 지점으로 복원하는 방법은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)을 참조하세요.<br /><br /> 참고: 논리적으로 일치해야 하는 전체 복구 모델 데이터베이스가 둘 이상이면 이 데이터베이스의 복구 가능성을 확인하는 특수 절차를 구현해야 합니다. 자세한 내용은 [표시된 트랜잭션이 포함된 관련 데이터베이스 복구](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)를 참조하세요.|  
|**대량 로그**|로그 백업 필요<br /><br /> 성능 우선 대량 복사 작업을 허용하는 전체 복구 모델의 보충 모델<br /><br /> 대부분의 대량 작업에 대해 최소 로깅을 사용하여 로그 공간 사용량을 줄입니다. 최소 로깅이 가능한 작업에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.<br /><br /> 대량 로그된 복구 모델에서 데이터베이스 백업에 대한 자세한 내용은 [전체 데이터베이스 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md) 및 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)을 참조하세요.|로그가 손상되었거나 가장 최근의 로그 백업 이후 대량 로그 작업이 수행된 경우 마지막 백업 이후의 변경 내용을 다시 실행해야 함<br /><br /> 그 외에는 작업이 손실되지 않음|백업의 끝으로 복구 가능. 지정 시간 복구는 지원되지 않습니다.|  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [꽉 찬 트랜잭션 로그 문제 해결&#40;SQL Server 오류 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="see-also"></a>참고 항목  
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [관리 태스크 자동화&#40;SQL Server 에이전트&#41;](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
  
  
