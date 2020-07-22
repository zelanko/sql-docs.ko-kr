---
title: DBCC CHECKFILEGROUP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKFILEGROUP_TSQL
- DBCC_CHECKFILEGROUP_TSQL
- DBCC CHECKFILEGROUP
- CHECKFILEGROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKFILEGROUP statement
- database objects [SQL Server], checking
- allocation checks
- integrity [SQL Server], database objects
- filegroups [SQL Server], consistency checks
- table integrity checks [SQL Server]
- checking database objects
ms.assetid: 8c70bf34-7570-4eb6-877a-e35064a1380a
author: pmasl
ms.author: umajay
ms.openlocfilehash: b194f23779914961899cdf8b07c82a4d0986aa79
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485289"
---
# <a name="dbcc-checkfilegroup-transact-sql"></a>DBCC CHECKFILEGROUP(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
현재 데이터베이스의 지정한 파일 그룹에서 모든 테이블과 인덱싱된 뷰의 할당과 구조적 무결성을 검사합니다.
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
DBCC CHECKFILEGROUP   
[  
    [ ( { filegroup_name | filegroup_id | 0 }   
        [ , NOINDEX ]   
  ) ]  
    [ WITH   
        {   
            [ ALL_ERRORMSGS | NO_INFOMSGS ]   
            [ , TABLOCK ]   
            [ , ESTIMATEONLY ]  
            [ , PHYSICAL_ONLY ]    
            [ , MAXDOP  = number_of_processors ]  
        }   
    ]  
]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *filegroup_name*  
 테이블 할당과 구조적 무결성을 검사할 현재 데이터베이스의 파일 그룹 이름입니다. 아무 값도 지정하지 않거나 0을 지정하면 기본값은 주 파일 그룹입니다. 파일 그룹 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.  
 *filegroup_name*은 FILESTREAM 파일 그룹이 될 수 없습니다.  
  
 *filegroup_id*  
 테이블 할당과 구조적 무결성을 검사할 현재 데이터베이스의 파일 그룹 ID입니다.  
  
 NOINDEX  
 사용자 테이블의 비클러스터형 인덱스에 대해 집중적인 검사가 수행되지 않도록 지정합니다. 이렇게 하면 전반적인 실행 시간이 줄어듭니다. DDBCC CHECKFILEGROUP에서 항상 모든 시스템 테이블 인덱스를 검사하므로 NOINDEX는 시스템 테이블에 영향을 주지 않습니다.  
  
 ALL_ERRORMSGS  
 개체당 오류를 무제한으로 표시합니다. 기본적으로 모든 오류 메시지가 표시됩니다. 이 옵션을 지정하거나 생략하더라도 아무런 영향을 미치지 않습니다.  
  
 NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
 TABLOCK  
 내부 데이터베이스 스냅샷을 사용하는 대신 DBCC CHECKFILEGROUP이 잠금을 획득하도록 합니다.  
  
 ESTIMATE ONLY  
 지정된 다른 모든 옵션과 함께 DBCC CHECKFILEGROUP을 실행하는 데 필요한 tempdb 공간의 예상 크기를 표시합니다.  
  
 PHYSICAL_ONLY  
 무결성 검사를 페이지의 물리적 구조, B-트리의 물리적 구조 및 레코드 헤더로 제한합니다. 이 검사는 파일 그룹에 대한 물리적 일관성 검사의 오버헤드를 줄이기 위한 목적으로 사용하며 데이터가 손상될 가능성이 있는 조각난 페이지와 일반적인 하드웨어 오류도 찾습니다. 다음과 같은 원인으로 DBCC CHECKFILEGROUP 전체 실행에 이전 버전에서보다 현저히 더 많은 시간이 걸릴 수 있습니다.  
 -   논리적 검사가 더 포괄적입니다.  
 -   검사할 기본 구조 일부가 더 복잡해졌습니다.  
 -   새로운 기능을 포괄할 수 있도록 여러 가지 검사 작업이 새로 도입되었습니다.  
 따라서 대형 파일 그룹에서는 PHYSICAL_ONLY 옵션을 사용하여 DBCC CHECKFILEGROUP 실행 시간을 훨씬 단축시킬 수 있으므로 프로덕션 시스템에서의 잦은 검사 작업에는 이 옵션을 사용하는 것이 좋습니다. 하지만 정기적으로 DBCC CHECKFILEGROUP 전체 실행을 수행하는 것이 좋습니다. 이러한 실행 빈도는 개별 비즈니스 및 프로덕션 환경과 관련된 여러 가지 요소에 따라 달라집니다. PHYSICAL_ONLY는 항상 NO_INFOMSGS를 의미하며 복구 옵션과는 함께 사용할 수 없습니다.  
  
> [!NOTE]  
>  PHYSICAL_ONLY를 지정하면 DBCC CHECKFILEGROUP이 FILESTREAM 데이터에 대한 모든 검사를 건너뜁니다.  
  
 MAXDOP  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 SP2에서 [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)까지  
  
 명령문에 대한 **sp_configure**의 **최대 병렬 처리 수준** 구성 옵션을 재정의합니다. MAXDOP은 sp_configure로 구성한 값을 초과할 수 있습니다. MAXDOP가 Resource Governor로 구성한 값을 초과하면, 데이터베이스 엔진에서 ALTER WORKLOAD GROUP(Transact-SQL)에서 설명한 Resource Governor MAXDOP 값을 사용합니다. max degree of parallelism 구성 옵션에 사용된 모든 의미 체계 규칙을 MAXDOP 쿼리 힌트 사용 시 적용할 수 있습니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.  
  
> [!CAUTION]  
>  MAXDOP가 0으로 설정되면 서버는 최대 병렬 처리 수준을 선택합니다.  
  
## <a name="remarks"></a>설명  
DBCC CHECKFILEGROUP과 DBCC CHECKDB는 유사한 DBCC 명령입니다. 주요 차이점은 DBCC CHECKFILEGROUP이 지정된 단일 파일 그룹과 필수 테이블로 제한된다는 것입니다.
DBCC CHECKFILEGROUP은 다음과 같은 명령을 수행합니다.
-   파일 그룹에 대한 [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)  
-   파일 그룹의 모든 테이블 및 인덱싱된 뷰에 대한 [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
  
DBCC CHECKALLOC 또는 DBCC CHECKTABLE을 DBCC CHECKFILEGROUP과 별도로 실행할 필요는 없습니다.
  
## <a name="internal-database-snapshot"></a>내부 데이터베이스 스냅샷  
DBCC CHECKFILEGROUP은 내부 데이터베이스 스냅샷을 사용하여 이러한 검사를 수행하는 데 필요한 트랜잭션 일관성을 유지합니다. 자세한 내용은 [데이터베이스 스냅샷의 스파스 파일의 크기 보기&#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) 및 [DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)의 "DBCC 내부 데이터베이스 스냅샷 사용법" 섹션을 참조하세요.
스냅샷을 만들 수 없거나 TABLOCK 옵션이 지정된 경우 DBCC CHECKFILEGROUP은 필요한 일관성을 얻기 위해 잠금을 획득합니다. 이 경우 할당 검사를 위해서는 배타적 데이터베이스 잠금이 필요하며 테이블 검사를 위해서는 공유 테이블 잠금이 필요합니다. TABLOCK을 사용하면 로드가 많은 데이터베이스에서 DBCC CHECKFILEGROUP이 더 빠르게 실행됩니다. 그러나 DBCC CHECKFILEGROUP이 실행되는 동안 데이터베이스에 대한 동시성은 줄어듭니다.
  
> [!NOTE]  
>  tempdb에 대해 DBCC CHECKFILEGROUP을 실행하면 할당 검사가 수행되지 않으며 테이블 검사를 수행하려면 공유 테이블 잠금을 획득해야 합니다. 이것은 성능상의 이유로 tempdb의 데이터베이스 스냅샷을 사용할 수 없기 때문입니다. 즉, 필요한 트랜잭션 일관성을 얻을 수 없음을 의미합니다.  
  
## <a name="checking-objects-in-parallel"></a>병렬로 개체 검사  
기본적으로 DBCC CHECKFILEGROUP은 개체의 병렬 검사를 수행합니다. 병렬 처리 수준은 쿼리 프로세서에 의해 자동으로 결정됩니다. 최대 병렬 처리 수준은 병렬 쿼리와 동일하게 구성됩니다. DBCC 검사에 사용할 수 있는 최대 프로세서 수를 제한하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용합니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.
추적 플래그 2528을 사용하면 병렬 검사를 비활성화할 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.
  
## <a name="nonclustered-indexes-on-separate-filegroups"></a>개별 파일 그룹의 비클러스터형 인덱스  
지정된 파일 그룹의 비클러스터형 인덱스가 다른 파일 그룹의 테이블과 연결된 경우 유효성 검사 시 기본 테이블을 사용할 수 없으므로 인덱스가 검사되지 않습니다.
지정된 파일 그룹의 테이블이 다른 파일 그룹의 비클러스터형 인덱스와 연결된 경우 비클러스터형 인덱스는 다음과 같은 이유로 검사되지 않습니다.
-   기본 테이블 구조는 비클러스터형 인덱스의 구조에 종속되지 않습니다. 기본 테이블을 검사하기 위해 비클러스터형 인덱스를 검색할 필요는 없습니다.  
-   DBCC CHECKFILEGROUP 명령은 지정된 파일 그룹에 있는 개체의 유효성만 검사합니다.  
클러스터형 인덱스와 테이블은 서로 다른 파일 그룹에 있을 수 없으므로 위의 고려 사항은 비클러스터형 인덱스에만 적용됩니다.
  
## <a name="partitioned-tables-on-separate-filegroups"></a>개별 파일 그룹의 분할된 테이블  
여러 파일 그룹에 분할된 테이블이 있을 경우 DBCC CHECKFILEGROUP이 지정된 파일 그룹에 있는 파티션 행 집합을 검사하고 다른 파일 그룹에서 해당 행 집합을 무시합니다. 정보 메시지 2594는 확인되지 않은 파티션을 나타냅니다. 지정된 파일 그룹에 상주하지 않는 비클러스터형 인덱스는 검사하지 않습니다.
  
## <a name="understanding-dbcc-error-messages"></a>DBCC 오류 메시지 이해  
DBCC CHECKFILEGROUP 명령이 완료된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 메시지가 기록됩니다. DBCC 명령이 성공적으로 실행되면 메시지에 실행 완료 및 명령이 실행된 소요 시간이 표시됩니다. 오류로 인해 DBCC 명령이 검사를 완료하기 전에 중지되면 메시지에 명령 종료, 상태 값 및 명령이 실행된 소요 시간이 표시됩니다. 다음 표에서는 메시지에 포함될 수 있는 상태 값을 나열하고 설명합니다.
  
|시스템 상태|Description|  
|-----------|-----------------|  
|0|오류 번호 8930이 발생했습니다. 메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|  
|1|오류 번호 8967이 발생했습니다. 내부 DBCC 오류가 있습니다.|  
|2|응급 모드 데이터베이스 복구 중에 오류가 발생했습니다.|  
|3|메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|  
|4|어설션 또는 액세스 위반이 감지되었습니다.|  
|5|알 수 없는 오류가 발생하여 DBCC 명령이 종료되었습니다.|  
  
## <a name="error-reporting"></a>오류 보고  
DBCC CHECKFILEGROUP에서 손상 오류가 검색될 때마다  *LOG 디렉터리에 미니덤프 파일(SQLDUMP*nnnn[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].txt)이 만들어집니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 기능 사용량 현황 데이터 수집 및 오류 보고 기능을 설정하면 이 파일이 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에 자동으로 전달됩니다. 수집된 데이터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 향상시킬 수 있습니다.
덤프 파일에는 DBCC CHECKFILEGROUP 명령의 결과 및 추가 진단 출력이 포함됩니다. 이 파일에는 제한된 DACL(임의 액세스 제어 목록)이 있습니다. 액세스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 **sysadmin** 역할의 멤버로 제한됩니다. 기본적으로 **sysadmin** 역할에는 Windows BUILTIN\Administrators 그룹 및 로컬 관리자 그룹의 모든 멤버가 포함됩니다. 데이터 수집 프로세스가 실패해도 DBCC 명령은 실패하지 않습니다.
  
## <a name="resolving-errors"></a>오류 해결  
DBCC CHECKFILEGROUP이 오류를 보고할 경우 데이터베이스 백업에서 데이터베이스를 복원하는 것이 좋습니다. 복구 옵션은 DBCC CHECKFILEGROUP에 지정할 수 없습니다.
백업이 없을 경우 복구 옵션을 지정하여 DBCC CHECKDB를 실행하면 보고된 오류를 수정할 수 있습니다. 사용할 복구 옵션은 보고된 오류 목록 끝에 지정됩니다. REPAIR_ALLOW_DATA_LOSS 옵션을 사용하여 오류를 수정하면 일부 페이지, 즉 데이터의 삭제가 필요할 수 있습니다.
  
## <a name="result-sets"></a>결과 집합  
DBCC CHECKFILEGROUP은 다음 결과 집합을 반환합니다. 값은 다를 수 있습니다.
-   ESTIMATEONLY 또는 NO_INFOMSGS가 지정된 경우는 제외합니다.  
-   데이터베이스가 지정되지 않은 경우에는 옵션(NOINDEX 제외) 지정 여부에 관계없이 현재 데이터베이스에 해당됩니다.  
  
```sql
DBCC results for 'master'.  
DBCC results for 'sys.sysrowsetcolumns'.  
There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.  
DBCC results for 'sys.sysrowsets'.  
There are 97 rows in 1 pages for object 'sys.sysrowsets'.  
DBCC results for 'sysallocunits'.  
There are 195 rows in 3 pages for object 'sysallocunits'.  
  
There are 2340 rows in 16 pages for object 'spt_values'.  
DBCC results for 'MSreplication_options'.  
There are 2 rows in 1 pages for object 'MSreplication_options'.  
CHECKFILEGROUP found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
NO_INFOMSGS가 지정된 경우 DBCC CHECKFILEGROUP은 다음을 반환합니다.
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
 ESTIMATEONLY가 지정된 경우 DBCC CHECKFILEGROUP은 다음을 반환합니다. 값은 다를 수 있습니다.  

```sql
Estimated TEMPDB space needed for CHECKALLOC (KB)
-------------------------------------------------   
15  
  
(1 row(s) affected)  
  
Estimated TEMPDB space needed for CHECKTABLES (KB)   
--------------------------------------------------   
207  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>사용 권한  
**sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="examples"></a>예  
### <a name="a-checking-the-primary-filegroup-in-the-a-database"></a>A. 데이터베이스의 PRIMARY 파일 그룹 검사  
다음 예에서는 현재 데이터베이스의 주 파일 그룹을 검사합니다.
  
```sql  
  
DBCC CHECKFILEGROUP;  
GO  
```  
  
### <a name="b-checking-the-adventureworks-primary-filegroup-without-nonclustered-indexes"></a>B. 비클러스터형 인덱스를 제외한 AdventureWorks PRIMARY 파일 그룹 검사  
다음 예제에서는 PRIMARY 파일 그룹의 ID 번호 및 `AdventureWorks2012`를 지정하여 `NOINDEX` 데이터베이스의 PRIMARY 파일 그룹(비클러스터형 인덱스 제외)을 검사합니다.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKFILEGROUP (1, NOINDEX);  
GO  
```  
  
### <a name="c-checking-the-primary-filegroup-with-options"></a>C. 옵션을 사용하여 PRIMARY 파일 그룹 검사  
다음 예에서는 `master` 옵션을 지정하여 `ESTIMATEONLY` 데이터베이스의 PRIMARY 파일 그룹을 검사합니다.
  
```sql  
USE master;  
GO  
DBCC CHECKFILEGROUP (1)  
WITH ESTIMATEONLY;  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[FILEGROUP_ID&#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-id-transact-sql.md)  
[sp_helpfile&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)  
[sp_helpfilegroup&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)  
[sys.sysfilegroups&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysfilegroups-transact-sql.md)  
[DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKALLOC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)  
[DBCC CHECKTABLE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)
  
  
