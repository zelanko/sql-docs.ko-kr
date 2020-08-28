---
description: MSSQLSERVER_3414
title: MSSQLSERVER_3414 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a7a7d69c27ed422763c5c697f003ba9fb4c82286
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618092"
---
# <a name="mssqlserver_3414"></a>MSSQLSERVER_3414
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|3414|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|REC_GIVEUP|  
|메시지 텍스트|복구하는 동안 오류가 발생하여 데이터베이스 '%.*ls'(데이터베이스 ID %d)을(를) 다시 시작하지 못했습니다. 복구 오류를 진단하여 수정하거나 양호한 백업에서 복원하십시오. 오류를 수정할 수 없거나 예상할 수 없는 경우 기술 지원 서비스에 문의하십시오.|  
  
## <a name="explanation"></a>설명  
지정된 데이터베이스가 복구되었으나 복구 중 오류가 발생하여 시작에 실패했습니다. 이 오류가 발생하면 데이터베이스가 SUSPECT 상태가 됩니다. 주 파일 그룹(다른 파일 그룹도 해당될 수 있음)이 주의 대상이거나 손상되었을 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작하는 동안에는 데이터베이스를 복구할 수 없으므로 데이터베이스를 사용할 수 없습니다. 문제를 해결하려면 사용자 동작이 필요합니다. SQL Server Management Studio(데이터베이스 아이콘 옆)와 sys.databases.state_desc 열에서 모두 SUSPECT 상태가 표시됩니다. 이 상태에서 데이터베이스를 사용하려고 하면 다음 오류가 발생합니다.

```
Msg 926, Level 14, State 1, Line 1 
Database 'mydb' cannot be opened. It has been marked SUSPECT by recovery. See the SQL Server errorlog for more information
```
  
**tempdb**에서 이 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 종료됩니다.  

## <a name="cause"></a>원인
이 오류는 서버 인스턴스를 시작하거나 데이터베이스를 복구하려는 지정된 시도 중에 시스템에 존재하는 일시적인 상태에 의해 발생할 수 있습니다. 또한 데이터베이스를 시작할 때마다 발생하는 영구적인 오류로 인해 발생할 수도 있습니다. 일반적으로 복구 실패의 원인은 ERRORLOG 또는 이벤트 로그에서 3414 오류 앞에 나오는 오류에서 확인할 수 있습니다. 로그 파일의 해당 선행 오류에는 동일한 spid<n> 값이 포함되어 있습니다. 예를 들어 다음 복구 실패의 원인은 로그 블록을 읽으려고 할 때 발생하는 체크섬 오류입니다. *spid15s*는 모든 줄에 표시됩니다.

```
2020-03-31 17:33:13.00 spid15s     Error: 824, Severity: 24, State: 4.  
2020-03-31 17:33:13.00 spid15s     SQL Server detected a logical consistency-based I/O error: (bad checksum). It occurred during a read of page (0:-1) in database ID 13 at offset 0x0000000000b800 in file 'C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\mydb_log.LDF'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.   
2020-03-31 17:33:13.16 spid15s     Error: 3414, Severity: 21, State: 1.  
2020-03-31 17:33:13.16 spid15s     An error occurred during recovery, preventing the database 'mydb' (database ID 13) from restarting. Diagnose the recovery errors and fix them, or restore from a known good backup. If errors are not corrected or expected, contact Technical Support
```


데이터베이스 복구 실패를 초래할 수 있는 오류는 다양합니다. 사례별로 각 오류를 평가해야 하지만 데이터베이스 복구 실패에 대한 해결 방법은 일반적으로 아래 사용자 작업 섹션에서 설명하는 것과 같습니다.

## <a name="user-action"></a>사용자 조치  
 
3414 오류가 발생한 원인에 대한 내용을 보려면 Windows 이벤트 로그 또는 ERRORLOG에서 해당 실패를 나타내는 이전 오류를 살펴보세요. 적절한 사용자 동작은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류가 일시적인 상태에 의해 발생했는지 영구적인 문제에 의해 발생했는지를 나타내는 Windows 이벤트 로그의 정보에 따라 달라집니다. 오류 메시지는 “diagnose recovery errors and fix them, or restore from a known good backup”(복구 오류를 진단하여 수정하거나 알려진 양호한 백업에서 복원하세요.)입니다. 따라서 복구를 완료할 수 있도록 발생하는 오류를 수정할 수 있습니다([수정 가능한 오류 및 지연된 트랜잭션](#correctable-errors-and-deferred-transactions) 참조).

오류를 수정할 수 없는 경우 이 문제를 해결하는 가장 좋은 옵션은 양호한 백업에서 복원하는 것입니다. 하지만 백업에서 복구할 수 없는 경우 전체 데이터 복구를 보장하지 않는 두 가지 추가 옵션이 있습니다. 첫 번째는 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 사용한 응급 복구를 사용하는 것이고, 두 번째는 최대한 많은 데이터를 다른 데이터베이스에 복사해 보는 것입니다. 

 1. 마지막으로 알려진 양호한 데이터베이스 백업에서 복원합니다.
 1. [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)에서 제공하는 응급 복구 방법을 사용합니다.
 1. 최대한 많은 데이터를 다른 데이터베이스에 복사해 봅니다.

양호한 데이터베이스 백업을 복원하는 첫 번째 방법은 데이터베이스를 알려진 일관된 상태로 전환하는 가장 좋은 선택입니다.  

백업을 사용할 수 없는 경우 두 번째로 좋은 선택은 데이터베이스를 액세스 가능한 온라인 상태로 전환하는 것입니다. 그러나 복구에 실패한 후에는 트랜잭션 일관성을 보장할 수 없음을 알아야 합니다. 롤백 또는 롤포워드되어야 했지만 복구 실패로 인해 허용되지 않은 트랜잭션을 알 수 있는 방법은 없습니다. 응급 복구를 진행하는 단계는 DBCC CHECKDB 설명서의 [응급 모드에서 데이터베이스 오류 해결](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md#resolving-errors-in-database-emergency-mode) 섹션에서 설명합니다. 

응급 복구가 작동하지 않고 일부 데이터를 다른 데이터베이스에 복구하려는 경우 데이터베이스에 대한 액세스 권한을 얻는 방법은 ALTER DATABASE <dbname> SET EMERGENCY 명령을 통해 응급 모드에서 데이터베이스를 설정하는 것입니다. 그런 다음, 테이블에서 데이터 복사를 시도할 수 있습니다.

### <a name="correctable-errors-and-deferred-transactions"></a>수정 가능한 오류 및 지연된 트랜잭션
데이터베이스 복구 중에 발생하는 모든 오류로 인해 복구 실패 및 주의 대상 데이터베이스가 발생하는 것은 아닙니다.

데이터베이스 및/또는 트랜잭션 로그 파일을 처음 열 때 발생하는 오류는 복구 전에 발생합니다. 해당 오류의 예시는 [17204](mssqlserver-17204-database-engine-error.md) 및 [17207](mssqlserver-17207-database-engine-error.md)입니다. 이러한 오류를 수정한 후에는 복구 진행이 가능할 수 있지만 다른 복구 오류가 발생하는 경우에는 완료를 보장할 수 없습니다. 17204 및 17207과 같은 오류로 인해 SUSPECT 데이터베이스가 발생하지는 않습니다. 실제로 이러한 문제가 발생할 때 데이터베이스의 상태는 RECOVERY_PENDING입니다. 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하면 페이지 수준 오류가 발생하는 경우에도 복구를 완료할 수 있으며 트랜잭션 일관성이 계속 유지됩니다. 이 프로세스를 통해 SUSPECT 데이터베이스가 발생하는 시나리오가 줄었습니다. 이 개념을 [지연된 트랜잭션](../backup-restore/deferred-transactions-sql-server.md)이라고 합니다.

복구 중에 발생한 오류가 데이터베이스 페이지의 문제를 나타내는 경우(예: 체크섬 오류 또는 824 메시지) 오류가 보류되면서 복구를 완료할 수 있습니다. 트랜잭션이 커밋되지 않은 경우 페이지의 오류로 인해 [지연된 트랜잭션](../backup-restore/deferred-transactions-sql-server.md)이 발생하여 복구를 완료할 수 있습니다.  

다음 ERRORLOG 항목은 복구 중에 [824](mssqlserver-824-database-engine-error.md) 메시지 오류가 발생했지만 지연된 트랜잭션으로 복구를 완료할 수 있었던 경우를 보여 줍니다. 이 경우 3414 오류가 없는 점과 데이터베이스 복구가 완료되었다는 메시지를 확인합니다.

```2010-03-31 19:17:18.45 spid7s      Error: 824, Severity: 24, State: 2.   
2010-03-31 19:17:18.45 spid7s      SQL Server detected a logical consistency-based I/O error: incorrect checksum (expected: 0xb2c87a0a; actual: 0xb6c0a5e2). It occurred during a read of page (1:153) in database ID 13 at offset 0x00000000132000 in file 'C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\mydb.mdf'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.   
2010-03-31 19:17:18.45 spid7s      Error: 3314, Severity: 21, State: 1.   
2010-03-31 19:17:18.45 spid7s      During undoing of a logged operation in database 'mydb', an error occurred at log record ID (25:100:19). Typically, the specific failure is logged previously as an error in the Windows Event Log service. Restore the database or file from a backup, or repair the database.
2010-03-31 19:17:18.45 spid7s      Errors occurred during recovery while rolling back a transaction. The transaction was deferred. Restore the bad page or file, and re-run recovery.   
2010-03-31 19:17:18.45 spid7s      Recovery completed for database mydb (database ID 13) in 2 second(s) (analysis 204 ms, redo 25 ms, undo 1832 ms.) This is an informational message only. No user action is required.   
```

커밋된 트랜잭션을 롤포워드해야 하는 경우 페이지는 액세스할 수 없는 것으로 표시될 수 있으며(이후 페이지에 액세스하려는 경우 829 메시지 발생) 복구를 완료할 수 있습니다. 이 경우 백업에서 페이지를 복원하거나 복구 옵션이 있는 DBCC CHECKDB를 사용하여 페이지의 할당을 취소하여 오류를 수정해야 합니다.


  
## <a name="see-also"></a>참고 항목  
[ALTER DATABASE&#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB&#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[전체 데이터베이스 복원&#40;단순 복구 모델&#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[지연된 트랜잭션](../backup-restore/deferred-transactions-sql-server.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases&#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)

  
