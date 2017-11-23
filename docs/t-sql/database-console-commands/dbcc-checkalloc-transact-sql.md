---
title: DBCC CHECKALLOC (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKALLOC_TSQL
- DBCC CHECKALLOC
- DBCC_CHECKALLOC_TSQL
- CHECKALLOC
dev_langs: TSQL
helpviewer_keywords:
- DBCC CHECKALLOC statement
- checking database space allocation
- database space allocation [SQL Server]
- consistency [SQL Server], disk space allocations
- space allocation [SQL Server]
- allocation checks
- disk space [SQL Server], allocation consistency checks
- space allocation [SQL Server], checking
ms.assetid: bc1218eb-ffff-44ce-8122-6e4fa7d68a79
caps.latest.revision: "76"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 09d190a3a27344d60fe3861b87443165f39ac352
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-checkalloc-transact-sql"></a>DBCC CHECKALLOC(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

지정된 데이터베이스에 대한 디스크 공간 할당 구조의 일관성을 검사합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC CHECKALLOC   
[  
    ( database_name | database_id | 0   
      [ , NOINDEX   
      | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]  
    )  
    [ WITH   
        {   
          [ ALL_ERRORMSGS ]  
          [ , NO_INFOMSGS ]   
          [ , TABLOCK ]   
          [ , ESTIMATEONLY ]   
        }  
    ]  
]  
```  
  
## <a name="arguments"></a>인수  
 *a s e _* | *database_id* | 0   
 이름 또는 할당 및 페이지 사용을 확인 하려는 데이터베이스의 ID입니다.
아무 값도 지정하지 않거나 0을 지정하면 현재 데이터베이스가 사용됩니다.
데이터베이스 이름에 대 한 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.

 NOINDEX  
 사용자 테이블의 비클러스터형 인덱스를 검사하지 않도록 지정합니다.<br>NOINDEX는 이전 버전과의 호환성을 위해서만 유지 관리되고 DBCC CHECKALLOC에는 영향을 주지 않습니다.

 REPAIR_ALLOW_DATA_LOSS \| REPAIR_FAST \| REPAIR_REBUILD  
 DBCC CHECKALLOC 실행 시 발견된 오류를 복구하도록 지정합니다. *a s e _* 단일 사용자 모드에 있어야 합니다.

 REPAIR_ALLOW_DATA_LOSS  
 발견된 오류를 복구하려고 시도합니다. 이러한 복구를 수행하면 일부 데이터가 손실될 수 있습니다. REPAIR_ALLOW_DATA_LOSS는 할당 오류를 복구하는 데 사용할 수 있는 유일한 옵션입니다.

 REPAIR_FAST  
 이전 버전과의 호환성을 위해서만 구문이 유지됩니다. 복구 동작은 수행되지 않습니다.

 REPAIR_REBUILD  
 이 오류에는 이 작업을 적용할 수 없습니다.  
 REPAIR 옵션은 최후의 수단으로만 사용하십시오. 오류를 복구하려면 백업에서 복원하는 것이 좋습니다. 복구 작업이 수행될 경우 테이블 자체나 테이블 간에 존재할 수 있는 제약 조건이 고려되지 않습니다. 지정된 테이블이 하나 이상의 제약 조건에 관련되면 복구 작업 후에 DBCC CHECKCONSTRAINTS를 실행하는 것이 좋습니다. REPAIR를 사용해야 하는 경우 복구 옵션 없이 DBCC CHECKDB를 실행하여 사용할 복구 수준을 확인합니다. REPAIR_ALLOW_DATA_LOSS 수준을 사용하는 경우 이 옵션으로 DBCC CHECKDB를 실행하기 전에 데이터베이스를 백업하는 것이 좋습니다.

 의 모든 멘션을  
 지정할 옵션을 활성화합니다.

 ALL_ERRORMSGS  
 모든 오류 메시지를 표시합니다. 기본적으로 모든 오류 메시지가 표시됩니다. 이 옵션을 지정하거나 생략하더라도 아무런 영향을 미치지 않습니다.

 NO_INFOMSGS  
 모든 정보 메시지와 사용한 공간 보고서를 표시하지 않습니다.

 TABLOCK  
 DBCC 명령으로 데이터베이스에 대한 배타적 잠금을 얻습니다.

 ESTIMATE ONLY  
 다른 모든 옵션이 지정 되 면 DBCC CHECKALLOC을 실행 하는 데 필요한 tempdb 공간의 예상된 크기를 표시 합니다.
  
## <a name="remarks"></a>주의  
DBCC CHECKALLOC은 페이지가 속한 페이지 유형이나 개체 유형과 관계없이 데이터베이스에 있는 모든 페이지의 할당을 검사합니다. 또한 이러한 페이지와 페이지 간 관계를 추적하는 데 사용되는 다양한 내부 구조의 유효성을 검사합니다.
NO_INFOMSGS가 지정되지 않은 경우 DBCC CHECKALLOC은 데이터베이스의 모든 개체에 대한 공간 사용률 정보를 수집합니다. 이 정보는 발견 된 오류와 함께 인쇄 됩니다.
  
> [!NOTE]  
>DBCC CHECKALLOC 기능은에 포함 되어 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 및 [DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)합니다. 따라서 이러한 문과 별도로 DBCC CHECKALLOC을 실행할 필요가 없습니다.   DBCC CHECKALLOC은 FILESTREAM 데이터를 검사하지 않습니다. FILESTREAM은 파일 시스템에 BLOB(Binary Large Object)을 저장합니다.  
  
## <a name="internal-database-snapshot"></a>내부 데이터베이스 스냅숏  
DBCC CHECKALLOC은 내부 데이터베이스 스냅숏을 사용하여 이러한 검사를 수행하는 데 필요한 트랜잭션 일관성을 지원합니다. 스냅숏을 만들 수 없거나 TABLOCK이 지정되어 있는 경우 DBCC CHECKALLOC은 데이터베이스에 대한 배타(X) 잠금을 얻어 필요한 일관성을 확보하려고 합니다.
  
> [!NOTE]  
> Tempdb에 대 한 DBCC CHECKALLOC을 실행 해도 아무런 검사도 수행 하지 않습니다. 이것은 성능상의 이유로 tempdb의 데이터베이스 스냅숏을 사용할 수 없기 때문입니다. 즉, 필요한 트랜잭션 일관성을 얻을 수 없음을 의미합니다. 중지 하 고 모든 tempdb 할당 문제를 해결 하려면 MSSQLSERVER 서비스를 시작 합니다. 이 작업을 삭제 하 고 다시 tempdb 데이터베이스를 만듭니다.  
  
## <a name="understanding-dbcc-error-messages"></a>DBCC 오류 메시지 이해  
DBCC CHECKALLOC 명령이 완료된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 메시지가 기록됩니다. DBCC 명령이 성공적으로 실행되면 메시지에 실행 완료 및 명령이 실행된 소요 시간이 표시됩니다. 오류로 인해 DBCC 명령이 검사를 완료하기 전에 중지되면 메시지에 명령 종료, 상태 값 및 명령이 실행된 소요 시간이 표시됩니다. 다음 표에서는 메시지에 포함될 수 있는 상태 값을 나열하고 설명합니다.
  
|State|Description|  
|---|---|  
|0|오류 번호 8930이 발생했습니다. 메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|  
|1.|오류 번호 8967이 발생했습니다. 내부 DBCC 오류가 있습니다.|  
|2|응급 모드 데이터베이스 복구 중에 오류가 발생했습니다.|  
|3|메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|  
|4|어설션 또는 액세스 위반이 감지되었습니다.|  
|5|알 수 없는 오류가 발생하여 DBCC 명령이 종료되었습니다.|  
  
## <a name="error-reporting"></a>오류 보고  
미니 덤프 파일 (SQLDUMP*nnnn*.txt)에서 만든는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBCC checkalloc 명령에서 손상 오류가 검색 될 때마다 로그 디렉터리입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 기능 사용 데이터 수집 및 오류 보고 기능을 설정하면 이 파일이 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에 자동으로 전달됩니다. 수집된 데이터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 향상시킬 수 있습니다.
덤프 파일에는 DBCC CHECKALLOC 명령의 결과 및 추가 진단 출력이 포함됩니다. 이 파일에는 제한된 DACL(임의 액세스 제어 목록)이 있습니다. 액세스가 제한 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 sysadmin 역할의 멤버입니다. 기본적으로 sysadmin 역할에는 Windows BUILTIN\Administrators 그룹 및 로컬 관리자 그룹의 모든 멤버가 포함됩니다. 데이터 수집 프로세스가 실패해도 DBCC 명령은 실패하지 않습니다.
  
## <a name="resolving-errors"></a>오류 해결  
DBCC CHECKALLOC이 오류를 보고하면 복구를 실행하는 대신 데이터베이스 백업으로 데이터베이스를 복원하는 것이 좋습니다. 백업이 없는 경우 복구를 실행하면 보고된 오류를 해결할 수 있지만 이렇게 하면 일부 페이지와 그 안의 데이터가 삭제될 수도 있습니다.
사용자 트랜잭션에서 복구를 수행할 수 있습니다. 이렇게 하면 변경 내용이 롤백될 수 있습니다. 변경 내용이 롤백되어도 데이터베이스에는 오류가 그대로 남아 있으므로 백업에서 데이터베이스를 복원해야 합니다. 복구를 완료한 후 데이터베이스를 백업합니다.
  
## <a name="result-sets"></a>결과 집합  
다음 표에서는 DBCC CHECKALLOC이 반환하는 정보에 대해 설명합니다.
  
|항목|Description|  
|---|---|  
|FirstIAM|내부적으로만 사용됩니다.|  
|Root|내부적으로만 사용됩니다.|  
|Dpages|데이터 페이지 수입니다.|  
|Pages used|할당된 페이지입니다.|  
|Dedicated extents|개체에 할당된 익스텐트입니다.<br /><br /> 혼합된 할당 페이지를 사용하는 경우에는 익스텐트가 없이 할당된 페이지가 있을 수도 있습니다.|  
  
또한 DBCC CHECKALLOC은 각 파일의 인덱스와 파티션에 대한 할당 요약을 보고합니다. 이 요약에서는 데이터 배포에 대해 설명합니다.
  
|항목|Description|  
|---|---|  
|Reserved pages|인덱스에 할당된 페이지 및 할당된 익스텐트에서 사용되지 않은 페이지입니다.|  
|Used pages|할당되었으며 인덱스에서 사용하고 있는 페이지입니다.|  
|Partition ID|내부적으로만 사용됩니다.|  
|Alloc unit ID|내부적으로만 사용됩니다.|  
|행 내부 데이터|페이지에 인덱스 또는 힙 데이터가 포함됩니다.|  
|LOB 데이터|페이지에 포함 되어 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **텍스트**, **ntext**, **xml**, 및 **이미지** 데이터입니다.|  
|행 오버플로 데이터|페이지에 행 외부로 밀어넣은 가변 길이 열 데이터가 포함됩니다.|  
  
DBCC CHECKALLOC은 ESTIMATEONLY 또는 NO_INFOMSGS가 지정된 경우를 제외하고 다음 결과 집합(값은 변화 가능)을 반환합니다.
  
```sql
DBCC results for 'master'.  
***************************************************************  
Table sysobjects                Object ID 1.  
Index ID 1         FirstIAM (1:11)   Root (1:12)    Dpages 22.  
    Index ID 1. 24 pages used in 5 dedicated extents.  
Index ID 2         FirstIAM (1:1368)   Root (1:1362)    Dpages 10.  
    Index ID 2. 12 pages used in 2 dedicated extents.  
Index ID 3         FirstIAM (1:1392)   Root (1:1408)    Dpages 4.  
    Index ID 3. 6 pages used in 0 dedicated extents.  
Total number of extents is 7.  
***************************************************************  
'...'  
***************************************************************  
Table spt_server_info                Object ID 1938105945.  
Index ID 1         FirstIAM (1:520)   Root (1:508)    Dpages 1.  
    Index ID 1. 3 pages used in 0 dedicated extents.  
Total number of extents is 0.  
***************************************************************  
Processed 52 entries in sysindexes for database ID 1.  
File 1. Number of extents = 210, used pages = 1126, reserved pages = 1280.  
           File 1 (number of mixed extents = 73, mixed pages = 184).  
    Object ID 1, Index ID 0, data extents 5, pages 24, mixed extent pages 9.  
'...'  
    Object ID 1938105945, Index ID 0, data extents 0, pages 3, mixed extent pages 3.  
Total number of extents = 210, used pages = 1126, reserved pages = 1280 in this database.  
       (number of mixed extents = 73, mixed pages = 184) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC results for 'master'.  
***************************************************************  
Table sys.sysrowsetcolumns                Object ID 4.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). FirstIAM (1:98). Root (1:94). Dpages 7.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). 9 pages used in 1 dedicated extents.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). FirstIAM (0:0). Root (0:0). Dpages 0.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). 0 pages used in 0 dedicated extents.  
Total number of extents is 1.  
...  
***************************************************************  
Processed 201 entries in system catalog for database ID 1.  
File 1. Number of extents = 44, used pages = 300, reserved pages = 345.  
           File 1 (number of mixed extents = 29, mixed pages = 225).  
    Object ID 4, index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 5, index ID 1, partition ID 327680, alloc unit ID 327680 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 7, index ID 1, partition ID 458752, alloc unit ID 458752 (type In-row data), data extents 0, pages 5, mixed extent pages 5.  
    Object ID 8, index ID 0, partition ID 524288, alloc unit ID 524288 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 13, index ID 1, partition ID 851968, alloc unit ID 851968 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 15, index ID 1, partition ID 983040, alloc unit ID 983040 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 26, index ID 1, partition ID 281474978414592, alloc unit ID 1703937 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 1, partition ID 281474978480128, alloc unit ID 1769473 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 2, partition ID 562949955190784, alloc unit ID 1769474 (type In-row data), index extents 0, pages 3, mixed extent pages 3.  
...  
    Object ID 1179151246, index ID 1, partition ID 72057594038845440, alloc unit ID 13435136 (type In-row data), data extents 2, pages 18, mixed extent pages 8.  
    Object ID 1179151246, index ID 2, partition ID 72057594038910976, alloc unit ID 13566208 (type In-row data), index extents 1, pages 16, mixed extent pages 8.  
    Object ID 1911677858, index ID 0, partition ID 72057594039631872, alloc unit ID 15073536 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
Total number of extents = 41, used pages = 289, reserved pages = 323 in this database.  
       (number of mixed extents = 27, mixed pages = 211) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
ESTIMATEONLY가 지정된 경우 DBCC CHECKALLOC은 다음 결과 집합을 반환합니다.
  
```sql
Estimated TEMPDB space needed for CHECKALLOC (KB)   
-------------------------------------------------   
34  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
Sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 현재 데이터베이스 및 `DBCC CHECKALLOC` 데이터베이스에 대해 `AdventureWorks2012`을 실행합니다.
  
```sql  
-- Check the current database.  
DBCC CHECKALLOC;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKALLOC (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

