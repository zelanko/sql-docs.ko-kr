---
title: DBCC SHRINKDATABASE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs: TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
caps.latest.revision: "62"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: b8ca8cceddccd4066b7c1762bc75dffee02be842
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

지정한 데이터베이스에 있는 데이터 및 로그 파일의 크기를 축소합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
 *database_name* | *database_id* | 0  
 축소할 데이터베이스의 이름 또는 ID입니다. 0을 지정하면 현재 데이터베이스가 사용됩니다.  
  
 *target_percent*  
 데이터베이스를 축소한 후 데이터베이스에 남겨둘 여유 공간의 비율입니다.  
  
 NOTRUNCATE  
 파일 끝에 있는 할당된 페이지를 파일 앞의 할당되지 않은 페이지로 이동하여 데이터 파일의 데이터를 압축합니다. *target_percent* 선택 사항입니다. 이 옵션은 Azure SQL 데이터 웨어하우스에서 지원 되지 않습니다. 
  
 파일 끝의 여유 공간이 운영 체제에 반환되지 않고, 파일의 물리적 크기가 변경되지 않습니다. 그러므로 NOTRUNCATE를 지정하면 데이터베이스가 축소되지 않는 것처럼 보입니다.  
  
 NOTRUNCATE는 데이터 파일에만 적용되며 로그 파일에는 영향을 주지 않습니다.  
  
 TRUNCATEONLY  
 파일 끝의 모든 여유 공간을 운영 체제로 해제하지만 파일 내에서 페이지 이동을 수행하지 않습니다. 데이터 파일은 마지막으로 할당된 익스텐트까지만 축소됩니다. *target_percent* TRUNCATEONLY와 함께 지정 해도 무시 됩니다. 이 옵션은 Azure SQL 데이터 웨어하우스에서 지원 되지 않습니다.
  
 TRUNCATEONLY는 로그 파일에 영향을 줍니다. 데이터 파일만 자르려면 DBCC SHRINKFILE을 사용합니다.  
  
 WITH NO_INFOMSGS  
 심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="result-sets"></a>결과 집합  
다음 표에서는 결과 집합의 열을 설명합니다.
  
|열 이름|Description|  
|-----------------|-----------------|  
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 축소하려고 시도한 파일의 데이터베이스 ID입니다.|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 축소하려고 시도한 파일의 파일 ID 번호|  
|**CurrentSize**|현재 파일이 차지하고 있는 8KB 페이지의 수입니다.|  
|**MinimumSize**|파일이 최소한으로 차지할 수 있는 8KB 페이지의 수입니다. 이 값은 파일의 최소 크기나 원래 만들어졌을 때의 크기와 일치합니다.|  
|**UsedPages**|현재 파일에서 사용되는 8KB 페이지의 수입니다.|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 예상하는 파일 축소 가능 크기에 해당하는 8KB 페이지의 수입니다.|  
  
>[!NOTE]
> [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 축소되지 않은 파일의 행은 표시하지 않습니다.  
  
## <a name="remarks"></a>주의  
특정 데이터베이스의 모든 데이터와 로그 파일을 축소하려면 DBCC SHRINKDATABASE 명령을 실행합니다. 실행 또는 특정 데이터베이스에 대 한 한 번에 파일을 로그의 한 데이터를 축소 하는 [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) 명령입니다.
  
데이터베이스의 여유 (할당 되지 않은) 공간의 현재 크기를 보려면 실행 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)합니다.
  
DBCC SHRINKDATABASE 작업은 진행 도중에 언제든지 중지될 수 있으며 완료된 작업은 모두 보존됩니다.
  
데이터베이스를 최소 데이터베이스 크기보다 작게 축소할 수는 없습니다. 최소 크기는 데이터베이스를 처음 만들 때 지정된 크기나 DBCC SHRINKFILE 또는 ALTER DATABASE와 같은 파일 크기 변경 작업을 사용하여 명시적으로 설정한 마지막 크기입니다. 예를 들어 원래 10MB로 생성된 데이터베이스가 100MB까지 증가한 경우 포함된 모든 데이터를 삭제하더라도 데이터베이스를 10MB 이하로는 축소할 수 없습니다.
  
NOTRUNCATE 옵션이나 TRUNCATEONLY 옵션을 지정하지 않고 DBCC SHRINKDATABASE를 실행하는 것은 NOTRUNCATE를 사용하여 DBCC SHRINKDATABASE 작업을 실행한 다음 TRUNCATEONLY를 사용하여 DBCC SHRINKDATABASE 작업을 실행하는 것과 같습니다.
  
축소할 데이터베이스는 단일 사용자 모드가 아니어도 됩니다. 즉, 다른 사용자가 데이터베이스에서 작업 중이라도 데이터베이스를 축소할 수 있습니다. 시스템 데이터베이스의 경우에도 그렇습니다.
  
데이터베이스가 백업되는 동안에는 데이터베이스를 축소할 수 없습니다. 반대로 데이터베이스에 대한 축소 작업이 처리되는 동안에는 데이터베이스를 백업할 수 없습니다.

>[!NOTE]
> 현재 Azure SQL 데이터 웨어하우스 사용 하도록 설정 하는 TDE와 DBCC SHRINKDATABASE를 지원 하지 않습니다.
  
## <a name="how-dbcc-shrinkdatabase-works"></a>DBCC SHRINKDATABASE 작동 방법  
DBCC SHRINKDATABASE는 파일 단위로 데이터 파일을 축소하지만 로그 파일이 모두 한 연속 로그 풀에 있는 것처럼 로그 파일을 축소합니다. 항상 파일은 끝부터 축소됩니다.
  
라는 데이터베이스를 가정 **mydb** 데이터 파일 및 두 개의 로그 파일입니다. 데이터 및 로그 파일은 각각 10MB와 데이터 파일에는 6MB의 데이터가 포함 되어 있습니다.
  
각 파일에 대해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 대상 크기를 계산합니다. 이 크기는 파일을 축소할 크기입니다. DBCC SHRINKDATABASE가 지정 된 경우 *target_percent*, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 대상 크기를 계산 하는 *target_percent* 축소 후 파일에서 사용 가능한 공간의 크기입니다. 예를 들어, 지정 하는 경우는 *target_percent* 축소 25 **mydb**, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 8mb (6MB의 데이터 + 2MB의 여유 공간)을 데이터 파일에 대 한 대상 크기를 계산 합니다. 따라서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 데이터 파일의 마지막 2MB에서 데이터 파일의 처음 8MB에 포함 된 여유 공간에 데이터를 이동한 다음 파일을 축소 합니다.
  
데이터 파일을 가정 **mydb** 7MB의 데이터가 포함 되어 있습니다. 지정 하는 *target_percent* 30 30의 사용 가능한 공간 비율을 축소할 수이 데이터 파일에 대 한 허용 합니다. 그러나 지정 하는 *target_percent* 40 줄어들지 않습니다 데이터 파일 때문에 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 현재 데이터가 차지 하는 보다 작은 크기로 파일을 축소 되지 것입니다. 생각할 수도이 문제의 다른 방식으로: 원하는 여유 공간 40% + 전체 데이터 파일 70% (10MB 부족 7MB)는 100% 보다 큽니다. 원하는 무료 비율와 데이터 파일이 차지 하는 현재 백분율을 초과 하는 (10%)에서 100% 모두 때문에 *target_size* 이상 30 데이터 파일이 축소 되지 것입니다.
  
로그 파일에 대 한는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 사용 하 여 *target_percent* 전체 로그;에 대 한 대상 크기를 계산 하려면 따라서 *target_percent* 축소 작업 후 로그에서 가능한 공간의 양입니다. 그런 다음 전체 로그의 대상 크기가 각 로그 파일의 대상 크기로 변환됩니다.
  
DBCC SHRINKDATABASE는 즉시 각 물리적 로그 파일을 대상 크기로 축소하려고 합니다. 가상 로그에 로그 파일의 대상 크기보다 큰 논리 로그 부분이 없는 경우 파일이 성공적으로 잘리며 DBCC SHRINKDATABASE는 메시지를 표시하지 않고 완료됩니다. 그러나 가상 로그에 대상 크기보다 큰 논리 로그 부분이 있는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 가능한 한 많은 공간을 해제하고 정보용 메시지를 표시합니다. 이 메시지는 파일 끝의 가상 로그에서 논리 로그를 이동하기 위해 수행해야 하는 동작을 설명합니다. 동작이 수행되고 나면 DBCC SHRINKDATABASE를 사용하여 나머지 공간을 해제할 수 있습니다.
  
로그 파일은 가상 로그 파일 크기만큼만 축소할 수 있으므로 사용 중이 아닌 로그 파일이라도 가상 로그 파일의 크기보다 작게 축소할 수는 없습니다. 로그 파일이 생성되거나 확장될 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 동적으로 가상 로그 파일의 크기가 선택됩니다.
  
## <a name="best-practices"></a>최선의 구현 방법  
데이터베이스를 축소할 때는 다음을 고려하세요.
-   축소 작업은 테이블 잘라내기 또는 테이블 삭제 작업과 같이 사용되지 않는 공간이 많이 생기는 작업을 수행한 후에 가장 효과적입니다.  
-   대부분의 데이터베이스에는 정기적인 일상 작업에 사용 가능한 일정 여유 공간이 필요합니다. 데이터베이스를 반복해서 축소했지만 데이터베이스 크기가 다시 늘어나는 경우 일반 작업을 위해 축소된 공간이 필요한 것입니다. 이러한 경우 데이터베이스를 반복해서 축소하는 것은 불필요한 작업입니다.  
-   축소 작업은 데이터베이스 인덱스의 조각화 상태를 보존하지 않으며 일반적으로 조각화 정도를 어느 정도까지 늘리기도 합니다. 이것은 데이터베이스를 반복해서 축소하지 않아야 하는 또 다른 이유입니다.  
-   특정 요구 사항이 없을 경우 AUTO_SHRINK 데이터베이스 옵션을 ON으로 설정하지 마세요.  
  
## <a name="troubleshooting"></a>문제 해결  
 축소 작업이 실행 되는 트랜잭션에 의해 차단 될 수 있기를 [행 버전 관리 기반 격리 수준](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)합니다. 예를 들어 DBCC SHRINK DATABASE 작업을 실행할 때 행 버전 관리 기반 격리 수준에서 실행 중인 대규모 삭제 작업이 진행되고 있으면 축소 작업은 파일을 축소하기 전에 삭제 작업이 완료될 때까지 기다립니다. 이러한 경우 DBCC SHRINKFILE 및 DBCC SHRINKDATABASE 작업은 처음 한 시간 동안에는 5분마다 그리고 그 다음부터는 한 시간마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 정보 메시지(SHRINKDATABASE의 경우 5202 그리고 SHRINKFILE의 경우 5203)를 인쇄합니다. 예를 들어 오류 로그에 다음과 같은 오류 메시지가 있습니다.  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
이는 축소 작업이 완료된 마지막 트랜잭션인 109보다 오래된 타임스탬프가 있는 스냅숏 트랜잭션에 의해 축소 작업이 차단됨을 의미합니다. 또한 의미는 **transaction_sequence_num**, 또는 **first_snapshot_sequence_num** 열에는 [sys.dm_tran_active_snapshot_database_transactions &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) 동적 관리 뷰 15의 값을 포함 합니다. 경우는 **transaction_sequence_num**, 또는 **first_snapshot_sequence_num** 보기의 열 (109) 축소 작업이 완료 된 마지막 트랜잭션 보다 작은 숫자를 포함 된 축소 작업에서 해당 트랜잭션이 완료 때까지 대기 합니다.
  
문제를 해결하려면 다음 태스크 중 하나를 수행하십시오.
-   축소 작업을 차단하는 트랜잭션을 종료합니다.  
-   축소 작업을 종료합니다. 완료된 작업은 모두 보존됩니다.  
-   아무 작업도 하지 않고 차단하는 트랜잭션이 완료될 때까지 축소 작업이 대기할 수 있게 합니다.  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>1. 데이터베이스 축소 및 여유 공간의 백분율 지정  
 다음 예에서는 `UserDB` 사용자 데이터베이스에 10%의 여유 공간이 남도록 데이터베이스의 데이터 및 로그 파일 크기를 줄입니다.  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>2. 데이터베이스 자름  
 다음 예에서는 `AdventureWorks` 예제 데이터베이스의 데이터 및 로그 파일을 마지막으로 할당된 익스텐트까지 축소합니다.  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>참고 항목  
[ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[데이터베이스 축소](../../relational-databases/databases/shrink-a-database.md)
  
  
