---
title: "변경 데이터 캡처 및 기타 SQL Server 기능 | Microsoft 문서"
ms.custom: 
ms.date: 05/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 80603e457fdd610f354221aefc61c870445d9c53
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="change-data-capture-and-other-sql-server-features"></a>변경 데이터 캡처 및 기타 SQL Server 기능
  이 항목에서는 다음 기능으로 변경 데이터 캡처와 상호 작용하는 방법에 대해 설명합니다.  
  
-   [변경 내용 추적](#ChangeTracking)  
  
-   [데이터베이스 미러링](#DatabaseMirroring)  
  
-   [트랜잭션 복제](#TransReplication)  
  
-   [변경 데이터 캡처가 설정된 데이터베이스 복원 또는 연결](#RestoreOrAttach)  
  
##  <a name="ChangeTracking"></a> Change Tracking  
 동일한 데이터베이스에서 변경 데이터 캡처 및 [변경 내용 추적](../../relational-databases/track-changes/about-change-tracking-sql-server.md) 을 설정할 수 있습니다. 특별한 고려 사항은 필요하지 않습니다. 자세한 내용은 [변경 내용 추적 사용&#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)을 참조하세요.  
  
##  <a name="DatabaseMirroring"></a> 데이터베이스 미러링  
 변경 데이터 캡처가 설정된 데이터베이스를 미러링할 수 있습니다. 장애 조치(Failover) 후 캡처 및 정리가 자동으로 발생하도록 하려면 다음 단계를 따릅니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 새 주 서버 인스턴스에서 실행 중인지 확인합니다.  
  
2.  새 주 데이터베이스(이전에는 미러 데이터베이스)에 대한 캡처 작업 및 정리 작업을 만듭니다. 작업을 만들려면 [sp_cdc_add_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md) 저장 프로시저를 사용합니다.  
  
 정리 또는 캡처 작업의 현재 구성을 보려면 새 주 서버 인스턴스에서 [sys.sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md) 저장 프로시저를 사용합니다. 지정된 데이터베이스에 대해 캡처 작업의 이름은 cdc.*database_name*_capture로 지정되고 정리 작업의 이름은 cdc.*database_name*_cleanup으로 지정됩니다. 여기서 *database_name* 은 데이터베이스의 이름입니다.  
  
 작업의 구성을 변경하려면 [sys.sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md) 저장 프로시저를 사용합니다.  
  
 데이터베이스 미러링에 대한 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
##  <a name="TransReplication"></a> Transactional Replication  
 변경 데이터 캡처 및 트랜잭션 복제는 동일한 데이터베이스에 함께 존재할 수 있지만 두 기능이 모두 설정된 경우 변경 테이블 채우기가 다르게 처리됩니다. 변경 데이터 캡처 및 트랜잭션 복제는 항상 동일한 [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)프로시저를 사용하여 트랜잭션 로그에서 변경 내용을 읽습니다. 변경 데이터 캡처가 자체적으로 설정된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 **sp_replcmds**를 호출합니다. 동일한 데이터베이스에 두 기능이 모두 설정된 경우 로그 판독기 에이전트는 **sp_replcmds**를 호출합니다. 이 에이전트는 변경 테이블과 배포 데이터베이스 테이블을 모두 채웁니다. 자세한 내용은 [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)을 참조하세요.  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 변경 데이터 캡처가 설정되어 있고 두 테이블에 캡처가 설정된 시나리오를 생각해 보십시오. 변경 테이블을 채우기 위해 캡처 작업은 **sp_replcmds**를 호출합니다. 데이터베이스에 트랜잭션 복제가 설정되고 게시가 만들어집니다. 그런 다음 데이터베이스에 로그 판독기 에이전트가 만들어지고 캡처 작업이 삭제됩니다. 로그 판독기 에이전트는 변경 테이블에 커밋된 마지막 로그 시퀀스 번호에서 로그를 계속 검색합니다. 이렇게 하면 변경 테이블의 데이터 일관성이 보장됩니다. 이 데이터베이스에서 트랜잭션 복제가 해제되면 로그 판독기 에이전트가 제거되고 캡처 작업이 다시 만들어집니다.  
  
> [!NOTE]  
>  변경 데이터 캡처 및 트랜잭션 복제 모두에 로그 판독기 에이전트가 사용된 경우 복제된 변경 사항은 먼저 배포 데이터베이스에 기록됩니다. 그런 다음 캡처된 변경 사항이 변경 테이블에 기록됩니다. 두 작업은 함께 커밋됩니다. 배포 데이터베이스에 대한 쓰기 작업이 지연될 경우 변경 테이블에 변경 내용도 그만큼 늦게 표시됩니다.  
  
 변경 데이터 캡처를 사용하면 트랜잭션 복제의 **proc exec** 옵션을 사용할 수 없습니다.  
  
##  <a name="RestoreOrAttach"></a> 변경 데이터 캡처가 설정된 데이터베이스 복원 또는 연결  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 다음과 같은 논리에 따라 데이터베이스가 복원 또는 연결된 후 변경 데이터 캡처가 설정된 상태를 유지하는지 확인합니다.  
  
-   데이터베이스가 동일한 서버에 동일한 데이터베이스 이름으로 복원되는 경우 변경 데이터 캡처는 설정된 상태를 유지합니다.  
  
-   데이터베이스가 다른 서버로 복원되는 경우에는 기본적으로 변경 데이터 캡처가 해제되고 관련된 모든 메타데이터가 삭제됩니다.  
  
     변경 데이터 캡처를 유지하려면 데이터베이스를 복원할 때 **KEEP_CDC** 옵션을 사용합니다. 이 옵션에 대한 자세한 내용은 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)를 참조하세요.  
  
-   데이터베이스가 분리된 후 다시 동일한 서버 또는 다른 서버에 연결될 경우 변경 데이터 캡처는 설정된 상태를 유지합니다.  
  
-   데이터베이스가 **KEEP_CDC** 옵션을 사용하여 Enterprise 이외의 다른 버전에 연결 또는 복원된 경우 변경 데이터 캡처에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise가 필요하기 때문에 작업이 차단됩니다. 오류 메시지 934가 표시됩니다.  
  
     `SQL Server cannot load database '%.*ls' because Change Data Capture is enabled. The currently installed edition of SQL Server does not support Change Data Capture. Either restore database without KEEP_CDC option, or upgrade the instance to one that supports Change Data Capture.`  
  
 [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) 를 사용하여 복원 또는 연결된 데이터베이스에서 변경 데이터 캡처를 제거할 수 있습니다.  
  
## <a name="change-data-capture-and-always-on"></a>변경 데이터 캡처 및 Always On  
 Always On을 사용할 때는 보조 복제에서 변경 내용 열거를 수행하여 주 복제에서 디스크 부하를 줄여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [변경 데이터 캡처 관리 및 모니터링&#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
