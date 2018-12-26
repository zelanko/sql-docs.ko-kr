---
title: 트랜잭션 로그(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 01/04/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f22f0ea25b141cf7ee5a3130153837dcf4a1132
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072893"
---
# <a name="the-transaction-log-sql-server"></a>트랜잭션 로그(SQL Server)
  각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에는 각 트랜잭션에 의해 적용된 모든 트랜잭션 및 데이터베이스 수정 내용을 기록하는 트랜잭션 로그가 있습니다. 트랜잭션 로그가 채워지지 않도록 트랜잭션 로그를 정기적으로 잘라야 합니다. 그러나 일부 요소로 인해 로그 잘림이 지연될 수 있으므로 로그 크기를 모니터링하는 것이 중요합니다. 일부 작업을 최소로 기록하여 트랜잭션 로그 크기에 주는 영향을 줄일 수 있습니다.  
  
 트랜잭션 로그는 데이터베이스의 주요 구성 요소이며 시스템 오류가 발생할 경우 데이터베이스를 다시 일관된 상태로 만들려면 트랜잭션 로그가 필요할 수 있습니다. 트랜잭션 로그를 삭제하거나 이동할 경우의 결과를 완전히 이해하고 있는 경우를 제외하고는 트랜잭션 로그를 절대 삭제하거나 이동해서는 안 됩니다.  
  
> [!NOTE]  
>  데이터베이스 복구 중 트랜잭션 로그 적용을 시작할 알려진 올바른 지점은 검사점에 의해 만들어집니다. 자세한 내용은 [데이터베이스 검사점&#40;SQL Server&#41;](database-checkpoints-sql-server.md)을 참조하세요.  
  
 **항목 내용:**  
  
-   [트랜잭션 로그를 지 원하는 이점: 작업](#Benefits)  
  
-   [트랜잭션 로그 잘림](#Truncation)  
  
-   [로그 잘림을 지연 시킬 수 있는 요소](#FactorsThatDelayTruncation)  
  
-   [최소 로깅 가능한 작업](#MinimallyLogged)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="Benefits"></a> 트랜잭션 로그를 지 원하는 이점: 작업  
 트랜잭션 로그는 다음 작업을 지원합니다.  
  
-   개별 트랜잭션 복구  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작될 때 불완전한 모든 트랜잭션 복구  
  
-   복원된 데이터베이스, 파일, 파일 그룹 또는 페이지를 오류 지점으로 롤포워드  
  
-   트랜잭션 복제 지원  
  
-   고가용성 및 재해 복구 솔루션 지원: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], 데이터베이스 미러링 및 로그 전달  
  
##  <a name="Truncation"></a> 트랜잭션 로그 잘림  
 로그 잘림은 트랜잭션 로그에서 다시 사용할 수 있도록 로그 파일의 공간을 확보하는 것입니다. 로그가 가득 차지 않도록 하기 위해 로그 잘림은 필수적입니다. 로그 잘림은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 논리 트랜잭션 로그에서 비활성 가상 로그 파일을 삭제하여 물리적 트랜잭션 로그에서 다시 사용할 수 있도록 논리 로그의 공간을 확보합니다. 트랜잭션 로그가 잘리지 않으면 물리적 로그 파일에 할당된 디스크 공간이 모두 트랜잭션 로그로 채워지게 됩니다.  
  
 이 문제를 방지하기 위해 어떤 이유로 로그 잘림이 지연되고 있지 않는 한 다음과 같은 경우에 잘림이 자동으로 수행됩니다.  
  
-   단순 복구 모델에서는 검사점 이후 잘림이 수행됩니다.  
  
-   전체 복구 모델 또는 대량 로그 복구 모델에서는 이전 백업 이후에 검사점이 발생한 경우 로그 백업 후 잘림이 수행됩니다(복사 전용 로그 백업이 아닌 경우).  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 [로그 잘림을 지연시킬 수 있는 요소](#FactorsThatDelayTruncation)를 참조하십시오.  
  
> [!NOTE]  
>  로그 잘림을 수행해도 물리적 로그 파일의 크기는 줄어들지 않습니다. 물리적 로그 파일의 실제 크기를 줄이려면 로그 파일을 축소해야 합니다. 물리적 로그 파일의 크기를 축소하는 방법은 [트랜잭션 로그 파일의 크기 관리](manage-the-size-of-the-transaction-log-file.md)를 참조하십시오.  
  
##  <a name="FactorsThatDelayTruncation"></a> 로그 잘림을 지연 시킬 수 있는 요소  
 오랜 시간 동안 로그 레코드가 활성 상태로 유지되는 경우 로그 잘림이 지연되고 트랜잭션 로그가 가득 찰 수 있습니다.  
  
> [!IMPORTANT]  
>  가득 찬 트랜잭션 로그에 응답하는 방법에 대한 자세한 내용은 [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)을 참조하세요.  
  
 여러 요소로 인해 로그 잘림이 지연될 수 있습니다. 로그 잘림이 발생하지 않는 이유는 **sys.databases** 카탈로그 뷰의 **log_reuse_wait** 및 [log_reuse_wait_desc](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 열을 쿼리하여 확인할 수 있습니다. 다음 표에서는 이러한 열의 값에 대해 설명합니다.  
  
|log_reuse_wait 값|log_reuse_wait_desc 값|Description|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|현재 다시 사용 가능한 가상 로그 파일이 하나 이상 있습니다.|  
|1|CHECKPOINT|마지막 로그 잘림이나 로그 헤더가 가상 로그 파일을 넘어서 이동되지 않았기 때문에 검사점이 발생하지 있습니다(모든 복구 모델).<br /><br /> 로그 잘림 지연을 유발하는 일반적인 이유입니다. 자세한 내용은 [데이터베이스 검사점&#40;SQL Server&#41;](database-checkpoints-sql-server.md)을 참조하세요.|  
|2|LOG_BACKUP|트랜잭션 로그를 자르려면 먼저 로그 백업이 필요합니다. 이는 전체 또는 대량 로그 복구 모델의 경우에만 해당됩니다.<br /><br /> 다음 로그 백업이 완료되면 일부 로그 공간이 다시 사용될 수 있습니다.|  
|3|ACTIVE_BACKUP_OR_RESTORE|데이터 백업이나 복원이 진행되고 있습니다(모든 복구 모델).<br /><br /> 데이터 백업으로 인해 로그 잘림이 발생하지 않을 경우 해당 백업 작업을 취소하면 즉시 문제를 해결할 수 있습니다.|  
|4|ACTIVE_TRANSACTION|트랜잭션이 활성 상태입니다(모든 복구 모델).<br /><br /> 로그 백업 시작 시 장기 실행 트랜잭션이 있을 수 있습니다. 이 경우 공간을 확보하려면 다른 로그 백업이 필요할 수 있습니다. 장기 실행 트랜잭션이 없는는 트랜잭션 로그는 각 자동 검사점에서 잘립니다 일반적으로 단순 복구 모델을 비롯 한 모든 복구 모델에서 로그 잘림이 방지 참고 합니다.<br /><br /> 트랜잭션이 지연되었습니다. *지연된 트랜잭션* 은 사실상 일부 사용할 수 없는 리소스로 인해 롤백이 차단된 활성 트랜잭션입니다. 지연된 트랜잭션의 원인 및 이러한 트랜잭션을 지연된 상태에서 벗어나게 하는 방법에 대한 자세한 내용은 [지연된 트랜잭션&#40;SQL Server&#41;](../backup-restore/deferred-transactions-sql-server.md)을 참조하십시오. <br /><br />장기 실행 트랜잭션은 tempdb의 트랜잭션 로그를 채울 수도 있습니다. Tempdb는 정렬을 위한 작업 테이블, 해싱을 위한 작업 파일, 커서 작업 테이블 및 행 버전 관리 등 내부 개체에 대한 사용자 트랜잭션에 의해 암시적으로 사용됩니다. 사용자 트랜잭션 읽기만 데이터 (선택 쿼리)를 포함 하는 경우에 내부 개체를 생성 하 고 사용자 트랜잭션 하에서 사용할 수 있습니다. 그런 다음 tempdb 트랜잭션 로그를 채울 수 있습니다.|  
|5|DATABASE_MIRRORING|데이터베이스 미러링이 일시 중지되거나 성능 우선 모드에서는 미러 데이터베이스가 주 데이터베이스보다 훨씬 않습니다(전체 복구 모델에만 해당).<br /><br /> 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.|  
|6|REPLICATION|트랜잭션 복제 중에 게시와 관련된 트랜잭션이 배포 데이터베이스로 배달되지 않습니다(전체 복구 모델에만 해당).<br /><br /> 트랜잭션 복제에 대한 자세한 내용은 [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md)를 참조하십시오.|  
|7|DATABASE_SNAPSHOT_CREATION|데이터베이스 스냅숏이 생성되고 있습니다(모든 복구 모델).<br /><br /> 로그 잘림 지연을 유발하는 일반적인 이유입니다.|  
|8|LOG_SCAN|로그 검색이 수행되고 있습니다(모든 복구 모델).<br /><br /> 로그 잘림 지연을 유발하는 일반적인 이유입니다.|  
|9|AVAILABILITY_REPLICA|가용성 그룹의 보조 복제본에서 해당하는 보조 데이터베이스에 이 데이터베이스의 트랜잭션 로그 레코드를 적용하고 있습니다(전체 복구 모델).<br /><br /> 자세한 내용은 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)합니다.|  
|10|—|내부용으로만 사용할 수 있습니다.|  
|11|—|내부용으로만 사용할 수 있습니다.|  
|12|—|내부용으로만 사용할 수 있습니다.|  
|13|OLDEST_PAGE|데이터베이스가 간접 검사점을 사용하도록 구성된 경우 데이터베이스의 가장 오래된 페이지가 검사점 LSN보다 오래되었을 수 있습니다. 이 경우 가장 오래된 페이지는 로그 잘림이 지연될 수 있습니다(모든 복구 모델).<br /><br /> 간접 검사점에 대한 자세한 내용은 [Database Checkpoints &#40;SQL Server&#41;](database-checkpoints-sql-server.md)을 참조하세요.|  
|14|OTHER_TRANSIENT|이 값은 현재 사용되지 않습니다.|  
|16|XTP_CHECKPOINT|자동 될 때까지 트랜잭션 로그가 잘릴 수 없습니다 데이터베이스는 메모리 최적화 파일 그룹에 있는 경우 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 검사점이 트리거될 (발생 하는 모든 512MB 로그 증가에).<br /><br /> 참고: 512mb 미만의 트랜잭션 로그를 자를, 해당 데이터베이스에 대해 수동으로 검사점 명령을 실행 합니다.|  
  
##  <a name="MinimallyLogged"></a> 최소 로깅 가능한 작업  
 *최소 로깅* 은 지정 시간 복구를 지원하지 않고 트랜잭션을 복구하는 데 필요한 정보만 기록합니다. 이 항목에서는 대량 로그 복구 모델 및 단순 복구 모델(백업이 실행 중인 경우 제외)에서 최소 로깅되는 작업을 식별합니다.  
  
> [!NOTE]  
>  최소 로깅은 메모리 최적화 테이블에 대해 지원되지 않습니다.  
  
> [!NOTE]  
>  전체 복구 모델에서는 모든 대량 작업을 완전히 기록합니다. 그러나 대량 작업에 대해 일시적으로 데이터베이스를 대량 로그 복구 모델로 전환하여 대량 작업 집합의 로깅을 최소화할 수 있습니다. 최소 로깅은 전체 로깅보다 효율적이며 대규모 대량 작업이 대량 트랜잭션 중에 사용 가능한 트랜잭션 로그 공간을 꽉 채울 가능성을 줄여줍니다. 그러나 최소 로깅을 사용할 때 데이터베이스가 손상되거나 손실되면 데이터베이스를 오류 지점으로 복구할 수 없습니다.  
  
 전체 복구 모델에서 전체 로깅되는 다음 작업은 단순 및 대량 로그 복구 모델에서 최소 로깅됩니다.  
  
-   대량 가져오기 작업([bcp](../../tools/bcp-utility.md), [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) 및 [INSERT... SELECT](/sql/t-sql/statements/insert-transact-sql)) 테이블로 대량 가져오기 작업이 최소한으로 기록되는 경우에 대한 자세한 내용은 [Prerequisites for Minimal Logging in Bulk Import](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하십시오.  
  
    > [!NOTE]  
    >  트랜잭션 복제를 사용하는 경우 대량 로그 복구 모델에서도 BULK INSERT 작업이 모두 기록됩니다.  
  
-   SELECT [INTO](/sql/t-sql/queries/select-into-clause-transact-sql) 작업  
  
    > [!NOTE]  
    >  트랜잭션 복제를 사용하는 경우 대량 로그 복구 모델에서도 SELECT INTO 작업이 모두 기록됩니다.  
  
-   새 데이터를 삽입 또는 추가할 때 [UPDATE](/sql/t-sql/queries/update-transact-sql) 문의 .WRITE 절을 사용하여 큰 값 데이터 형식을 부분적으로 업데이트하는 작업. 기존 값이 업데이트되는 경우 최소 로깅이 사용되지 않습니다. 큰 값 데이터 형식에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)을 참조하세요.  
  
-   [WRITETEXT](/sql/t-sql/queries/writetext-transact-sql) 하 고 [UPDATETEXT](/sql/t-sql/queries/updatetext-transact-sql) 문을 삽입 또는 새 데이터를 추가할 때를 `text`, `ntext`, 및 `image` 데이터 형식 열입니다. 기존 값이 업데이트되는 경우 최소 로깅이 사용되지 않습니다.  
  
    > [!NOTE]  
    >  WRITETEXT 및 UPDATETEXT 문은 더 이상 사용되지 않으므로 새 애플리케이션에서 사용하지 마십시오.  
  
-   데이터베이스가 단순 또는 대량 로그 복구 모델로 설정되면 작업이 오프라인으로 실행되든 온라인으로 실행되든 관계없이 일부 인덱스 DDL 작업이 최소 로깅됩니다. 최소한으로 로깅되는 인덱스 작업은 다음과 같습니다.  
  
    -   [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) 작업(인덱싱된 뷰 포함)  
  
    -   [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql) REBUILD 또는 DBCC DBREINDEX 작업  
  
        > [!NOTE]  
        >  DBCC DBREINDEX 문은 더 이상 사용되지 않으므로 새 애플리케이션에서 사용하지 마십시오.  
  
    -   DROP INDEX 새 힙 다시 작성(해당 사항이 있을 경우)  
  
        > [!NOTE]  
        >  인덱스 페이지 할당 취소 하는 동안에 [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql) 작업은 항상 모두 기록 합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 `Managing the transaction log`  
  
-   [트랜잭션 로그 파일의 크기 관리](manage-the-size-of-the-transaction-log-file.md)  
  
-   [꽉 찬 트랜잭션 로그 문제 해결&#40;SQL Server 오류 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **트랜잭션 로그 백업(전체 복구 모델)**  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **트랜잭션 로그 복원(전체 복구 모델)**  
  
-  [트랜잭션 로그 백업 복원](../backup-restore/restore-a-transaction-log-backup-sql-server.md)   
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 내구성 제어](control-transaction-durability.md)   
 [대량 가져오기의 최소 로깅을 위한 필수 조건](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [SQL Server 데이터베이스 백업 및 복원](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [데이터베이스 검사점&#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [데이터베이스의 속성 보기 또는 변경](../databases/view-or-change-the-properties-of-a-database.md)   
 [복구 모델&#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)  
  
  
