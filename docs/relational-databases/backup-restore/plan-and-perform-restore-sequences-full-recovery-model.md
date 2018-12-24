---
title: 복원 시퀀스 계획 및 수행(전체 복구 모델) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restore sequences [SQL Server], planning for
- full recovery model [SQL Server], planning restore sequences
ms.assetid: 9cbefaf8-d2b6-41c9-83fc-b3807a841fe2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ca126d0d8708e28af73c0faf6ddb9bc3d2ee280d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726221"
---
# <a name="plan-and-perform-restore-sequences-full-recovery-model"></a>복원 시퀀스 계획 및 수행(전체 복구 모델)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대해 일반적으로 전체 복구 모델을 사용하는 복원 시퀀스를 계획하고 수행하는 방법에 대해 설명합니다. *복원 시퀀스* 는 하나 이상의 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 문의 시퀀스입니다. 일반적으로 복원 시퀀스는 복원 중인 데이터베이스, 파일 및/또는 페이지의 내용을 초기화하고(데이터 복사 단계), 기록된 트랜잭션을 롤포워드하고(다시 실행 단계), 커밋되지 않은 트랜잭션을 롤백합니다(실행 취소 단계).  
  
 대부분의 경우 복원 시퀀스에는 전체 데이터베이스 백업, 차등 데이터베이스 백업 및 후속 로그 백업만 필요합니다. 이러한 경우 올바른 복원 시퀀스를 만드는 과정은 매우 간단하며 예를 들어 전체 데이터베이스를 실패 지점으로 복원하려면 먼저 활성 트랜잭션 로그( *비상* 로그)를 백업합니다. 그런 다음 가장 최근에 수행된 전체 데이터베이스 백업, 차등 데이터베이스 백업(있는 경우) 및 모든 후속 로그 백업을 순서대로 복원합니다.  
  
 보다 복잡한 경우에는 올바른 복원 시퀀스를 만드는 작업이 복잡해질 수 있습니다. 예를 들어 복원 시퀀스에서 여러 파일을 백업해야 하거나 데이터를 특정 지정 시간으로 복원해야 할 수 있습니다. 매우 복잡한 경우에는 하나 이상의 복구 분기 지점을 포함하는 분기 복구 경로를 순회해야 할 수 있습니다.  
  
> [!NOTE]  
>  *복구 경로* 는 데이터베이스를 특정 시점(복구 지점)으로 가져온 데이터 및 로그 백업 시퀀스입니다. 복구 경로는 데이터베이스의 일관성은 계속 유지한 채 시간 경과에 따라 점진적으로 데이터베이스를 변경시키는 특정 변환 집합입니다. 복구 경로는 시작점(LSN,GUID)에서부터 끝점(LSN,GUID)까지의 LSN 범위를 나타냅니다. 복구 경로의 LSN 범위는 하나 이상의 복구 분기의 시작부터 끝 전체에 이를 수 있습니다.  
  
## <a name="to-plan-a-restore-sequence"></a>복원 시퀀스를 계획하려면  
 복원 시퀀스를 시작하기 전에 다음 단계를 따르십시오.  
  
1.  가능한 경우 데이터베이스의 비상 로그 백업을 만듭니다. 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.  
  
2.  대상 복구 지점을 결정합니다.  
  
     대상 복구 지점은 트랜잭션 로그 백업 내의 지정 시간이나 표시로 결정할 수 있습니다. 자세한 내용은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md) 또는 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)를 참조하세요.  
  
3.  수행하려는 복원 유형을 결정합니다. 자세한 내용은 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)을 참조하세요.  
  
4.  필요한 백업을 확인하고 필요한 미디어 세트와 백업 디바이스를 사용할 수 있는지 확인합니다. 자세한 내용은 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md) 및 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.  
  
## <a name="to-perform-a-restore-sequence"></a>복원 시퀀스를 수행하려면  
 복원 시퀀스를 수행하려면 다음 단계를 따르십시오.  
  
1.  시퀀스를 시작하려면 데이터베이스 백업, 부분 백업, 하나 이상의 파일 백업과 같은 데이터 백업을 하나 이상 복원합니다.  
  
2.  필요에 따라 이러한 전체 백업을 기반으로 한 최신 차등 백업을 복원합니다.  
  
     복원하고자 하는 각각의 전체 백업에 대해 해당 백업이 모든 차등 백업에 대한 기반인지 여부를 확인합니다. 그럴 경우 가능하면 가장 최근의 차등 백업을 복원합니다. 자세한 내용은 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)을 참조하세요.  
  
3.  로그 백업을 순서대로 복원하여 복구 지점이 포함된 백업에서 완료함으로써 데이터베이스를 롤포워드합니다. 모든 로그 백업을 적용해야 하는지 여부는 대상 복구 지점을 포함하는 로그 백업에 따라 다음과 같이 달라집니다.  
  
    -   복구 지점이 실패 지점일 경우 복원한 마지막 데이터 전체 백업 또는 차등 백업 이후에 만든 모든 로그 백업을 복원해야 합니다. 자세한 내용은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)을 참조하세요.  
  
    -   지정 시간 복원의 경우 최신 로그 백업이 필요하지 않습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하면 데이터베이스 복구 관리자는 해당 시점에 복원하는 데 필요한 백업만 선택되도록 합니다. 이러한 백업은 지정 시간 복원에 필요한 권장 복원 계획을 구성합니다. 자세한 내용은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)을 참조하세요.  
  
## <a name="restarting-a-restore-sequence"></a>복원 시퀀스 다시 시작  
 복원 시퀀스의 결과에 문제가 발생한 경우 복원 시퀀스를 중지하고 처음부터 다시 시작할 수 있습니다. 예를 들어 실수로 너무 많은 로그 백업을 복원하여 의도한 복원 지점을 지나친 경우 대상 복구 지점을 포함하는 로그 백업까지 복원 시퀀스를 다시 시작해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
