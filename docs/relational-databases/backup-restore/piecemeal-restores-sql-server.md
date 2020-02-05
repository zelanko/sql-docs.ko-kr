---
title: 증분 복원(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- partial updates [SQL Server]
- staged restores [SQL Server]
- piecemeal restores [SQL Server]
- restoring [SQL Server], piecemeal restore scenario
ms.assetid: 208f55e0-0762-4cfb-85c4-d36a76ea0f5b
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7d818eb992ae95527281de6f53a2e17007490b3b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72916003"
---
# <a name="piecemeal-restores-sql-server"></a>증분 복원(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 엔터프라이즈 버전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](온라인 복원) 또는 표준 버전(오프라인 복원)의 데이터베이스에 여러 개의 파일 또는 파일 그룹이 있는 경우 및 단순 모델에서 읽기 전용 파일 그룹인 경우에 대해서만 다룹니다.  
  
 증분 복원과 메모리 최적화 테이블에 대한 자세한 내용은 [메모리 최적화 테이블이 있는 데이터베이스의 증분 복원](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)을 참조하세요.  
  
 *증분 복원* 을 사용하면 여러 파일 그룹을 포함하는 데이터베이스를 단계별로 복원 및 복구할 수 있습니다. 증분 복원에는 주 파일 그룹에서 시작하여 경우에 따라 하나 이상의 보조 파일 그룹까지 단계별로 복원하는 일련의 복원 순서가 포함됩니다. 증분 복원에서는 데이터베이스가 최종적으로 일관성 있는 상태가 되도록 검사를 유지 관리합니다. 복원 순서가 완료되었을 때 복구된 파일이 유효하고 데이터베이스와 일치하는 경우 이 파일을 즉시 온라인 상태로 만들 수 있습니다.  
  
 증분 복원 작업은 모든 복구 모델에서 가능하지만 단순 모델보다는 전체 및 대량 로그 모델에 대해 더 융통성이 있습니다.  
  
 모든 증분 복원은 *부분 복원 순서*라는 초기 복원 순서로 시작됩니다. 최소한 부분 복원 순서에서는 주 파일 그룹을 복원 및 복구하고 단순 복구 모델을 사용할 경우 모든 읽기/쓰기 파일 그룹을 복원 및 복구합니다. 증분 복원 순서 중에 전체 데이터베이스는 오프라인 상태가 되어야 합니다. 그 후에 데이터베이스가 온라인 상태가 되고 복원된 파일 그룹을 사용할 수 있습니다. 그러나 복원되지 않은 파일 그룹은 오프라인으로 유지되고 액세스할 수 없습니다. 나중에 파일 복원을 수행하여 오프라인 파일 그룹을 복원하고 온라인 상태로 만들 수 있습니다.  
  
 데이터베이스에서 사용하는 복구 모델에 관계없이 부분 복원 순서는 전체 백업을 복원하고 PARTIAL 옵션을 지정하는 RESTORE DATABASE 문으로 시작됩니다. PARTIAL 옵션은 항상 새로운 증분 복원을 시작하므로 부분 복원 순서의 맨 처음 문에서 한 번만 PARTIAL 옵션을 지정해야 합니다. 부분 복원 순서가 완료되고 데이터베이스가 온라인 상태가 되면 파일의 복구가 연기되므로 나머지 파일은 "복구 보류" 상태가 됩니다.  
  
 그 후 증분 복원은 일반적으로 하나 이상의 복원 순서를 포함하게 되며 이를 *파일 그룹 복원 순서*라고 합니다. 특정 파일 그룹 복원 순서의 경우 원하는 기간 동안 수행을 대기할 수 있습니다. 각 파일 그룹 복원 순서는 하나 이상의 오프라인 파일 그룹을 데이터베이스와 일치하는 지점으로 복원 및 복구합니다. 파일 그룹 복원 순서의 타이밍과 개수는 복구 목표, 복원할 오프라인 파일 그룹 수 및 파일 그룹 복원 순서당 복원할 오프라인 파일 그룹 수에 따라 달라집니다.  
  
 증분 복원을 수행하기 위한 정확한 요구 사항은 데이터베이스의 복구 모델에 따라 달라집니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "단순 복구 모델에서의 증분 복원" 및 "전체 복구 모델에서의 증분 복원"을 참조하십시오.  
  
## <a name="piecemeal-restore-scenarios"></a>증분 복원 시나리오  
 모든 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 오프라인 증분 복원을 지원합니다. 엔터프라이즈 버전에서는 온라인 또는 오프라인 상태에서 증분 복원을 수행할 수 있습니다. 오프라인 및 온라인 증분 복원의 의미는 다음과 같습니다.  
  
-   오프라인 증분 복원 시나리오  
  
     오프라인 증분 복원 시 데이터베이스는 부분 복원 순서 후에 온라인 상태가 됩니다. 복원되지 않은 파일 그룹은 오프라인 상태로 남지만 필요한 경우 데이터베이스를 오프라인 상태로 만든 후 해당 파일 그룹을 복원할 수 있습니다.  
  
-   온라인 증분 복원 시나리오  
  
     온라인 증분 복원 시에는 부분 복원 순서 후 데이터베이스가 온라인 상태가 되고 주 파일 그룹과 복구된 모든 보조 파일 그룹을 사용할 수 있습니다. 복원되지 않은 파일 그룹은 오프라인 상태로 남지만 필요한 경우 데이터베이스를 온라인으로 유지한 상태에서 해당 파일을 복원할 수 있습니다.  
  
     온라인 증분 복원에는 지연된 트랜잭션이 사용될 수 있습니다. 파일 그룹의 하위 집합만 복원된 경우 온라인 파일 그룹에 종속된 데이터베이스의 트랜잭션이 지연될 수 있습니다. 이것은 전체 데이터베이스가 일치해야 하므로 정상적인 현상입니다. 자세한 내용은 [지연된 트랜잭션&#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)에서 존재하지 않는 파일 그룹을 제거하는 방법에 대해 설명합니다.  
  
-   [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 증분 복원 시나리오  
  
     메모리 내 OLTP 데이터베이스의 증분 복원에 대한 자세한 내용은 [메모리 액세스에 최적화된 테이블이 포함된 데이터베이스의 증분 백업 및 복원](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)을 참조하세요.  
  
## <a name="restrictions"></a>제한  
 부분 복원 순서에서 [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) 파일 그룹이 제외될 경우 지정 시간 복원은 지원되지 않습니다. 복원 순서를 강제로 계속할 수 있지만 RESTORE 문에서 누락된 FILESTREAM 파일 그룹은 복원되지 않습니다. 지정 시간 복원을 강제로 수행하려면 후속 RESTORE LOG 문에도 지정해야 하는 STOPAT, STOPATMARK 또는 STOPBEFOREMARK 옵션과 함께 CONTINUE_AFTER_ERROR 옵션을 지정합니다. CONTINUE_AFTER_ERROR를 지정하면 부분 복원 순서가 성공하고 FILESTREAM 파일 그룹이 복구 불가능한 상태가 됩니다.  
  
## <a name="piecemeal-restore-under-the-simple-recovery-model"></a>단순 복구 모델에서의 증분 복원  
 단순 복구 모델에서 증분 복원 순서는 전체 데이터베이스 백업 또는 부분 백업으로 시작해야 합니다. 그런 다음 복원된 백업이 차등 기반일 경우 최근의 차등 백업을 복원합니다.  
  
 첫 번째 부분 복원 순서 중에 읽기/쓰기 파일 그룹의 하위 집합만 복원할 경우 복원되지 않은 파일 그룹은 부분 복원된 데이터베이스를 복구할 때 존재하지 않는 상태가 됩니다. 다음과 같은 경우에만 부분 복원 순서에서 읽기/쓰기 파일 그룹을 제외할 수 있습니다.  
  
-   복원되지 않은 파일 그룹을 존재하지 않는 상태로 만들려는 경우  
  
-   부분 복원 순서의 이전 복원 중에 복원되지 않은 각 파일 그룹이 읽기 전용, 삭제 또는 존재하지 않게 된 복구 지점에 복원 순서가 도달하는 경우  
  
-   데이터베이스가 단순 복구 모델을 사용하는 동안 전체 백업이 수행되었으나 복구 지점은 데이터베이스가 전체 복구 모델을 사용 중인 시점에 있는 경우. 자세한 내용은 이 항목의 뒷부분에 있는 "단순 복구 모델에서 전체 복구 모델로 전환된 데이터베이스의 증분 복원 수행"을 참조하십시오.  
  
### <a name="requirements-for-piecemeal-restore-under-the-simple-recovery-model"></a>단순 복구 모델에서의 증분 복원에 대한 요구 사항  
 단순 복구 모델에서 초기 단계는 주 파일 그룹과 모든 읽기/쓰기 보조 파일 그룹을 복원 및 복구합니다. 초기 단계가 완료되었을 때 복구된 파일이 유효하고 데이터베이스와 일치하는 경우 이 파일을 온라인 상태로 직접 연결할 수 있습니다.  
  
 그 후에 하나 이상의 추가 단계로 읽기 전용 파일 그룹을 복원할 수 있습니다.  
  
 증분 복원은 다음 조건을 만족하는 경우 읽기 전용 보조 파일 그룹에 대해 사용할 수 있습니다.  
  
-   백업 시 읽기 전용이었던 파일 그룹  
  
-   읽기 전용으로 남아 있는 파일 그룹(논리적으로 주 파일 그룹과 일관성 유지)  
  
 증분 복원을 수행하려면 다음 지침을 따라야 합니다.  
  
-   단순 복구 모델 데이터베이스의 증분 복원을 위한 전체 백업 세트에 다음이 포함되어야 합니다.  
  
    -   주 파일 그룹과 백업 당시 읽기/쓰기 상태였던 모든 파일 그룹을 포함하는 부분 또는 전체 데이터베이스 백업  
  
    -   각 읽기 전용 파일의 백업  
  
-   읽기 전용 파일의 백업이 주 파일 그룹의 백업과 일치하려면 보조 파일 그룹은 백업된 당시부터 주 파일 그룹을 포함하는 백업이 완료될 때까지 읽기 전용 상태여야 합니다. 파일 그룹이 읽기 전용 상태가 된 후 차등 파일 백업을 가져온 경우 차등 파일 백업을 사용할 수 있습니다.  
  
### <a name="piecemeal-restore-stages-simple-recovery-model"></a>증분 복원 단계(단순 복구 모델)  
 증분 복원 시나리오에는 다음 단계가 포함됩니다.  
  
-   초기 단계(주 파일 그룹과 모든 읽기/쓰기 파일 그룹 복원 및 복구)  
  
     초기 상태에서는 부분 복원을 수행합니다. 부분 복원 순서에서는 주 파일 그룹과 모든 읽기/쓰기 보조 파일 그룹을 복원하고 선택적으로 읽기 전용 파일 그룹의 일부를 복원합니다. 초기 단계에서 전체 데이터베이스는 오프라인 상태가 되어야 합니다. 초기 단계 후에 데이터베이스가 온라인 상태가 되고 복원된 파일 그룹을 사용할 수 있습니다. 하지만 복원되지 않은 모든 읽기 전용 파일 그룹은 오프라인 상태를 유지합니다.  
  
     초기 단계에서 첫 번째 RESTORE 문은 다음을 수행해야 합니다.  
  
    -   주 파일 그룹과 백업 당시 읽기/쓰기 상태였던 모든 파일 그룹을 포함하는 부분 또는 전체 데이터베이스 백업을 사용합니다. 일반적으로 부분 복원 순서는 부분 백업을 복원하여 시작합니다.  
  
    -   증분 복원의 시작을 나타내는 PARTIAL 옵션을 지정합니다.  
  
    > [!NOTE]  
    >  PARTIAL 옵션은 보안 검사를 수행하므로 결과 데이터베이스를 프로덕션 데이터베이스로 사용할 수 있습니다.  
  
    -   백업이 전체 데이터베이스 백업인 경우 READ_WRITE_FILEGROUPS 옵션을 지정합니다.  
  
-   데이터베이스가 온라인 상태이면 하나 이상의 온라인 파일 복원을 사용하여 백업 당시 읽기 전용이었던 오프라인 읽기 전용 파일을 복원 및 복구할 수 있습니다. 온라인 파일 복원의 타이밍은 데이터가 온라인 상태가 되어야 하는 시기에 따라 달라집니다.  
  
     데이터를 파일로 복원해야 하는지 여부는 다음에 따라 달라집니다.  
  
    -   데이터베이스와 일치하는 유효한 읽기 전용 파일은 데이터를 복원하지 않고 복구하여 즉시 온라인 상태로 만들 수 있습니다.  
  
    -   손상되거나 데이터베이스와 일치하지 않는 파일은 복구하기 전에 복원해야 합니다.  
  
### <a name="examples"></a>예  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="piecemeal-restore-under-the-full-recovery-model"></a>전체 복구 모델에서의 증분 복원  
 전체 복구 모델 또는 대량 로그 복구 모델에서는 여러 파일 그룹이 있는 모든 데이터베이스에 대해 증분 복원을 사용하여 해당 데이터베이스를 임의의 시점으로 복원할 수 있습니다. 증분 복원의 복원 순서는 다음과 같이 동작합니다.  
  
-   부분 복원 순서  
  
     부분 복원 순서에서는 주 파일 그룹과 필요할 경우 보조 파일 그룹을 일부 복원합니다.  
  
     첫 번째 RESTORE DATABASE 문은 다음을 수행해야 합니다.  
  
    -   PARTIAL 옵션을 지정합니다. 이는 증분 복원의 시작을 나타냅니다.  
  
    -   주 파일 그룹을 포함하는 전체 데이터베이스 백업을 사용합니다. 일반적으로 부분 복원 순서는 부분 백업을 복원하여 시작합니다.  
  
    -   특정 시점으로 복원하려면 부분 복원 순서에서 시간을 지정해야 하며 복원 순서의 모든 연속 단계에서 동일한 시간을 지정해야 합니다.  
  
-   파일 그룹 복원 순서는 추가 파일 그룹을 데이터베이스와 일치하는 온라인 시점으로 가져옵니다.  
  
     엔터프라이즈 버전에서 데이터베이스가 온라인 상태인 동안에는 오프라인 보조 파일 그룹을 복원 및 복구할 수 있습니다. 특정 읽기 전용 파일이 손상되지 않았고 데이터베이스와 일치하면 해당 파일을 복원할 필요가 없습니다. 자세한 내용은 [데이터를 복원하지 않고 데이터베이스 복구&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)를 참조하세요.  
  
### <a name="applying-log-backups"></a>로그 백업 적용  
 파일 백업이 생성되기 이전부터 읽기 전용 파일 그룹이 읽기 전용이었으면 로그 백업을 파일 그룹에 적용할 필요가 없으며 파일 복원 시 이 작업은 생략됩니다. 읽기/쓰기가 가능한 파일 그룹의 경우 파일 그룹을 현재 로그 파일로 전달하려면 손상되지 않은 로그 백업 체인을 마지막 전체 복원 또는 차등 복원에 적용해야 합니다. 복구 프로세스에 대한 자세한 내용은 [복원 및 복구 개요(SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)를 참조하세요.
  
### <a name="examples"></a>예  
  
-   [예제: 데이터베이스의 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
## <a name="performing-a-piecemeal-restore-of-a-database-whose-recovery-model-has-been-switched-from-simple-to-full"></a>단순 복구 모델에서 전체 복구 모델로 전환된 데이터베이스의 증분 복원 수행  
 전체 또는 부분 데이터베이스 백업 이후 단순 복구 모델에서 전체 복구 모델로 전환된 데이터베이스의 증분 복원을 수행할 수 있습니다. 예를 들어 다음 단계를 수행할 데이터베이스가 있다고 가정합니다.  
  
1.  단순 모델 데이터베이스의 부분 백업(backup_1)을 만듭니다.  
  
2.  조만간 복구 모델을 전체 모델로 변경합니다.  
  
3.  차등 백업을 만듭니다.  
  
4.  로그 백업을 시작합니다.  
  
 이제 다음 순서를 수행할 수 있습니다.  
  
1.  일부 보조 파일 그룹을 생략한 부분 복원  
  
2.  다른 필수 복원 후 이어지는 차등 복원  
  
3.  나중에 backup_1 부분 백업에서 읽기/쓰기 보조 파일 그룹의 파일을 WITH NORECOVERY 옵션을 사용하여 복원  
  
4.  데이터를 원래 복구 지점으로 복원하기 위한 원래 증분 복원으로 다른 모든 백업이 복원된 후 이어지는 차등 백업  

## <a name="see-also"></a>참고 항목  
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [복원 시퀀스 계획 및 수행 &#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/plan-and-perform-restore-sequences-full-recovery-model.md)    
 [복원 및 복구 개요(SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)     
  
