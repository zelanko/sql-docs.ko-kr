---
title: DBCC SHRINKFILE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SHRINKFILE
- DBCC_SHRINKFILE_TSQL
- DBCC SHRINKFILE
- SHRINKFILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- TRUNCATEONLY option
- shrinking files
- NOTRUNCATE option
- shrinking databases
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
- DBCC SHRINKFILE statement
ms.assetid: e02b2318-bee9-4d84-a61f-2fddcf268c9f
author: pmasl
ms.author: umajay
ms.openlocfilehash: ac274000ffdb1bcd29ebad2a2e0d0395b8daba0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930323"
---
# <a name="dbcc-shrinkfile-transact-sql"></a>DBCC SHRINKFILE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

현재 데이터베이스의 지정된 데이터 또는 로그 파일 크기를 축소합니다. 파일을 비우고 데이터베이스 제거를 허용하는 동일한 파일 그룹의 파일 간에 데이터를 이동하는 데 사용할 수 있습니다. 최소 파일 크기를 새 값으로 다시 설정하여 파일을 만들 때 해당 크기보다 작게 축소할 수 있습니다.
  
![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
DBCC SHRINKFILE   
(  
    { file_name | file_id }   
    { [ , EMPTYFILE ]   
    | [ [ , target_size ] [ , { NOTRUNCATE | TRUNCATEONLY } ] ]  
    }  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
*file_name*  
축소할 파일의 논리적 이름입니다.
  
*file_id*  
축소할 파일의 ID 번호입니다. 파일 ID를 가져오려면 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) 시스템 함수를 사용하거나 현재 데이터베이스의 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 카탈로그 뷰를 쿼리합니다.
  
*target_size*  
정수 - 파일의 새 메가바이트 크기입니다. 이 값을 지정하지 않으면 DBCC SHRINKFILE은 파일 생성 크기를 줄입니다.
  
> [!NOTE]  
>  DBCC SHRINKFILE *target_size*를 사용하여 빈 파일의 기본 크기를 줄일 수 있습니다. 예를 들어 5MB 파일을 만든 다음 파일이 아직 비어 있을 때 파일을 3MB로 줄이면 기본 파일 크기가 3MB로 설정됩니다. 이 내용은 데이터가 포함된 적이 없는 빈 파일에만 적용됩니다.  
  
이 옵션은 FILESTREAM 파일 그룹 컨테이너에서 지원되지 않습니다.  
이 값을 지정하면 DBCC SHRINKFILE은 *target_size*로 파일을 축소합니다. 해제할 파일 영역에서 사용된 페이지는 파일 보유 영역의 사용 가능한 공간으로 이동됩니다. 예를 들어 10MB의 데이터 파일을 사용하면 *target_size*가 8인 DBCC SHRINKFILE 작업이 파일의 마지막 2MB에서 사용된 모든 페이지를 파일의 처음 8MB에서 할당되지 않은 페이지로 이동합니다. DBCC SHRINKFILE은 필요한 저장 데이터 크기 이하로 파일을 축소하지 않습니다. 예를 들어 10MB 데이터 파일에서 7MB가 사용되는 경우 *target_size*가 6인 DBCC SHRINKFILE 문은 파일을 6MB가 아니라 7MB로만 축소합니다.
  
EMPTYFILE  
지정한 파일의 모든 데이터를 **동일한 파일 그룹**의 다른 파일로 마이그레이션합니다. 즉, EMPTYFILE은 지정된 파일의 데이터를 동일한 파일 그룹의 다른 파일로 마이그레이션합니다. EMPTYFILE은 이 파일이 읽기 전용이 아니더라도 파일에 새 데이터가 추가되지 않는다고 가정합니다. [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 파일을 제거할 수 있습니다. [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 파일 크기를 변경하면 읽기 전용 플래그가 재설정되고 데이터를 추가할 수 있습니다.

FILESTREAM 파일 그룹 컨테이너의 경우 FILESTREAM 가비지 수집기가 실행되어 EMPTYFILE이 다른 컨테이너에 복사한 불필요한 파일 그룹 컨테이너 파일을 모두 삭제할 때까지 파일을 제거하는 데 ALTER DATABASE를 사용할 수 없습니다. 자세한 내용은 [sp_filestream_force_garbage_collection&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)을 참조하세요.
  
> [!NOTE]  
>  FILESTREAM 컨테이너를 제거하는 방법에 대한 내용은 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)에서 해당 섹션을 참조하세요.  
  
NOTRUNCATE  
*target_percent*의 지정 여부와 관계없이 데이터 파일의 끝에서 할당된 페이지를 파일 앞의 할당되지 않은 페이지로 이동합니다. 파일 끝의 사용 가능한 공간이 운영 체제에 반환되지 않고, 파일의 물리적 크기가 변경되지 않습니다. 그러므로 NOTRUNCATE를 지정하면 파일이 축소되지 않는 것처럼 보입니다.
NOTRUNCATE는 데이터 파일에만 적용되며 로그 파일에는 영향을 주지 않습니다.   이 옵션은 FILESTREAM 파일 그룹 컨테이너에서 지원되지 않습니다.
  
TRUNCATEONLY  
파일 끝의 모든 사용 가능한 공간을 운영 체제로 해제하지만 파일 내에서 페이지 이동을 수행하지 않습니다. 데이터 파일은 마지막으로 할당된 익스텐트까지만 축소됩니다.
TRUNCATEONLY로 지정되면 *target_size*가 무시됩니다.  
TRUNCATEONLY 옵션은 로그에 있는 정보를 이동시키지 않습니다. 하지만 로그 파일의 끝에서 비활성 상태의 VLF를 제거합니다. 이 옵션은 FILESTREAM 파일 그룹 컨테이너에서 지원되지 않습니다.
  
WITH NO_INFOMSGS  
모든 정보 메시지를 표시하지 않습니다.
  
## <a name="result-sets"></a>결과 집합  
다음 표에서 결과 집합 열에 대해 설명합니다.
  
|열 이름|설명|  
|---|---|
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 축소하려고 시도한 파일의 데이터베이스 ID입니다.|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 축소하려고 시도한 파일의 파일 ID입니다.|  
|**CurrentSize**|현재 파일이 차지하고 있는 8KB 페이지의 수입니다.|  
|**MinimumSize**|파일이 최소한으로 차지할 수 있는 8KB 페이지의 수입니다. 이 수는 파일의 최소 크기나 원래 만들어졌을 때의 크기와 일치합니다.|  
|**UsedPages**|현재 파일에서 사용되는 8KB 페이지의 수입니다.|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 예상하는 파일 축소 가능 크기에 해당하는 8KB 페이지의 수입니다.|  
  
## <a name="remarks"></a>Remarks  
DBCC SHRINKFILE은 현재 데이터베이스의 파일에 적용됩니다. 현재 데이터베이스를 변경하는 방법에 대한 자세한 내용은 [USE&#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)를 참조하세요.
  
DBCC SHRINKFILE 작업은 언제든지 중지될 수 있으며 완료된 작업은 모두 그대로 유지됩니다. EMPTYFILE 매개 변수를 사용하고 작업을 취소하면 다른 데이터가 추가되지 않도록 파일이 표시되지 않습니다.
  
DBCC SHRINKFILE 작업이 실패하면 오류가 발생합니다.
  
 파일을 축소하는 동안 다른 사용자가 데이터베이스에서 작업할 수 있습니다. 데이터베이스가 단일 사용자 모드일 필요가 없습니다. 시스템 데이터베이스를 축소하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드에서 실행하지 않아도 됩니다.  
  
## <a name="shrinking-a-log-file"></a>로그 파일 축소  

로그 파일의 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 *target_size*를 사용하여 전체 로그의 대상 크기를 계산합니다. 따라서 *target_size*는 축소 작업 후 로그에서 사용 가능한 공간의 크기입니다. 그런 다음, 전체 로그의 대상 크기가 각 로그 파일의 대상 크기로 변환됩니다. DBCC SHRINKFILE은 즉시 각 물리적 로그 파일을 대상 크기로 축소하려고 시도합니다. 그러나 가상 로그에 대상 크기보다 큰 논리 로그 부분이 있는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 가능한 한 많은 공간을 해제하고 정보용 메시지를 표시합니다. 이 메시지는 파일 끝의 가상 로그에서 논리 로그를 이동하기 위해 수행해야 하는 동작을 설명합니다. 동작이 수행되고 나면 DBCC SHRINKFILE을 사용하여 나머지 공간을 확보할 수 있습니다.
  
로그 파일은 가상 로그 파일 크기만큼만 축소할 수 있으므로 사용 중이 아닌 로그 파일이라도 가상 로그 파일의 크기보다 작게 축소할 수는 없습니다. 로그 파일이 생성되거나 확장될 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 동적으로 가상 파일 로그 크기를 선택합니다.
  
## <a name="best-practices"></a>최선의 구현 방법 
 
파일을 축소할 때는 다음 정보를 고려하십시오.
-   축소 작업은 테이블 잘라내기 또는 테이블 삭제 작업과 같이 사용되지 않는 공간이 많이 생기는 작업을 수행한 후에 가장 효과적입니다.  

-   대부분의 데이터베이스에는 정기적인 일상 작업에 사용 가능한 일정 공간이 필요합니다. 데이터베이스를 반복해서 축소하지만 데이터베이스 크기가 다시 늘어나는 경우 일반 작업에는 축소된 공간이 필요합니다. 이러한 경우 데이터베이스를 반복해서 축소하는 것은 불필요한 작업입니다.  

-   축소 작업은 데이터베이스 인덱스의 조각화 상태를 보존하지 않으며 일반적으로 조각화 정도를 어느 정도까지 늘리기도 합니다. 이 조각화는 데이터베이스를 반복해서 축소하지 않아야 하는 또 다른 이유입니다.  

-   동일한 데이터베이스의 여러 파일을 동시에 축소하지 않고 순차적으로 축소합니다. 시스템 테이블에 대한 경합으로 인해 차단이 발생하고, 그 결과 지연이 발생할 수 있습니다.  
  
## <a name="troubleshooting"></a>문제 해결  
이 섹션에서는 DBCC SHRINKFILE 명령을 실행할 때 발생할 수 있는 문제를 진단하고 해결하는 방법에 대해 설명합니다.
  
### <a name="the-file-doesnt-shrink"></a>파일이 축소되지 않음
  
오류 없는 축소 작업 후에 파일 크기가 변경되지 않는 경우에는 다음을 시도하여 파일에 적절한 사용 가능한 공간이 있는지 확인합니다.

- 다음 쿼리를 실행합니다.  
  
```sql
SELECT name ,size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 AS AvailableSpaceInMB
FROM sys.database_files;
```

-   [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md) 명령을 실행하여 트랜잭션 로그에 사용된 공간을 반환합니다.  

사용 가능한 공간이 부족하면 축소 작업에서 파일 크기를 더 이상 줄일 수 없습니다.
  
일반적으로 축소되지 않는 것처럼 보이는 파일은 로그 파일입니다. 일반적으로 축소되지 않는 것은 로그 파일이 잘리지 않았기 때문입니다. 로그를 자르려면 데이터베이스 복구 모델을 SIMPLE로 설정하거나 로그를 백업한 후 DBCC SHRINKFILE 작업을 다시 실행합니다.
  
### <a name="the-shrink-operation-is-blocked"></a>축소 작업이 차단됨  

[행 버전 관리 기반 격리 수준](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)에서 실행 중인 트랜잭션이 축소 작업을 차단할 수 있습니다. 예를 들어 DBCC SHRINK DATABASE 작업을 실행할 때 행 버전 관리 기반 격리 수준에서 실행 중인 대규모 삭제 작업이 진행되고 있으면 축소 작업은 계속하기 전에 삭제 작업이 완료될 때까지 기다립니다. 이 차단이 발생하면 DBCC SHRINKFILE 및 DBCC SHRINKDATABASE 작업은 SQL Server 오류 로그에 정보 메시지(SHRINKDATABASE의 경우 5202, SHRINKFILE의 경우 5203)를 인쇄합니다. 이 메시지는 처음 한 시간 동안에는 5분마다 그리고 그 다음부터는 한 시간마다 기록됩니다. 예를 들어 오류 로그에 다음 오류 메시지가 포함된 경우 다음과 같은 오류가 발생합니다.
  
```sql
DBCC SHRINKFILE for file ID 1 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
이 메시지는 축소 작업이 완료된 마지막 트랜잭션인 109보다 오래된 타임스탬프가 있는 스냅샷 트랜잭션이 축소 작업을 차단하고 있음을 의미합니다. 또한 [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) 동적 관리 뷰의 **transaction_sequence_num** 또는 **first_snapshot_sequence_num** 열에 15인 값이 포함되어 있음을 나타냅니다. **transaction_sequence_num** 또는 **first_snapshot_sequence_num** 뷰 열에 축소 작업의 마지막으로 완료된 트랜잭션(109)보다 작은 숫자가 포함되면 축소 작업은 해당 트랜잭션이 완료될 때까지 기다립니다.
  
문제를 해결하려면 다음 태스크 중 하나를 수행하십시오.
-   축소 작업을 차단하는 트랜잭션을 종료합니다.
-   축소 작업을 종료합니다. 축소 작업이 종료되면 완료된 작업이 모두 유지됩니다.  
-   아무 작업도 하지 않고 차단하는 트랜잭션이 완료될 때까지 축소 작업이 대기할 수 있게 합니다.  
  
## <a name="permissions"></a>사용 권한  
**sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="examples"></a>예  
  
### <a name="shrinking-a-data-file-to-a-specified-target-size"></a>데이터 파일을 지정한 대상 크기로 축소  
다음 예제에서는 `UserDB` 사용자 데이터베이스의 `DataFile1`이라는 데이터 파일의 크기를 7MB로 축소합니다.
  
```sql  
USE UserDB;  
GO  
DBCC SHRINKFILE (DataFile1, 7);  
GO  
```  
  
### <a name="shrinking-a-log-file-to-a-specified-target-size"></a>로그 파일을 지정한 대상 크기로 축소  
다음 예에서는 `AdventureWorks` 데이터베이스에 있는 로그 파일을 1MB로 축소합니다. DBCC SHRINKFILE 명령이 파일을 축소할 수 있도록 먼저 데이터베이스 복구 모델을 SIMPLE로 설정하여 파일을 자릅니다.
  
```sql  
USE AdventureWorks2012;  
GO  
-- Truncate the log by changing the database recovery model to SIMPLE.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY SIMPLE;  
GO  
-- Shrink the truncated log file to 1 MB.  
DBCC SHRINKFILE (AdventureWorks2012_Log, 1);  
GO  
-- Reset the database recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-truncating-a-data-file"></a>C. 데이터 파일 자름  
다음 예에서는 `AdventureWorks` 데이터베이스의 주 데이터 파일을 자릅니다. `sys.database_files` 카탈로그 뷰를 쿼리하여 데이터 파일의 `file_id`를 가져옵니다.
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name  
FROM sys.database_files;  
GO  
DBCC SHRINKFILE (1, TRUNCATEONLY);  
```  
  
### <a name="d-emptying-a-file"></a>D. 파일 비우기  
다음 예에서는 데이터베이스에서 제거할 수 있도록 파일을 비우는 방법을 보여 줍니다. 이 예에서 사용하기 위해 데이터 파일이 먼저 생성되고 데이터를 포함합니다.
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create a data file and assume it contains data.  
ALTER DATABASE AdventureWorks2012   
ADD FILE (  
    NAME = Test1data,  
    FILENAME = 'C:\t1data.ndf',  
    SIZE = 5MB  
    );  
GO  
-- Empty the data file.  
DBCC SHRINKFILE (Test1data, EMPTYFILE);  
GO  
-- Remove the data file from the database.  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE Test1data;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKDATABASE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
[FILE_ID&#40;Transact-SQL&#41;](../../t-sql/functions/file-id-transact-sql.md)  
[sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[파일 축소](../../relational-databases/databases/shrink-a-file.md)
  
  
