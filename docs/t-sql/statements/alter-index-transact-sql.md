---
title: ALTER INDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: tsql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER INDEX
- ALTER_INDEX_TSQL
dev_langs:
- t-sql
helpviewer_keywords:
- indexes [SQL Server], reorganizing
- ALTER INDEX statement
- indexes [SQL Server], disabling
- online index operations
- index reorganization [SQL Server]
- ALLOW_ROW_LOCKS option
- ALL keyword
- reorganizing indexes
- constraints [SQL Server], indexes
- row locks [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- locking [SQL Server], indexes
- partitioned indexes [SQL Server], rebuilding
- defragmenting indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- index modifications [SQL Server]
- indexes [SQL Server], modifying
- index options [SQL Server]
- modifying indexes
- index disabling [SQL Server]
- MAXDOP index option, ALTER INDEX statement
- spatial indexes [SQL Server], modifying
- indexes [SQL Server], options
- ALLOW_PAGE_LOCKS option
- page locks [SQL Server]
- index rebuild [SQL Server]
- index reorganize [SQL Server]
ms.assetid: b796c829-ef3a-405c-a784-48286d4fb2b9
caps.latest.revision: 222
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e7d913d7cf3214acb8683bca2bb0a7ebca0e7b45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="alter-index-transact-sql"></a>ALTER INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  인덱스를 비활성화, 다시 작성 또는 다시 구성하거나 인덱스에 대한 옵션을 설정하여 기존 테이블 또는 뷰 인덱스(관계형 또는 XML)를 수정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
ALTER INDEX { index_name | ALL } ON <object>  
{  
      REBUILD {  
            [ PARTITION = ALL ] [ WITH ( <rebuild_index_option> [ ,...n ] ) ]   
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> ) [ ,...n ] ]  
      }  
    | DISABLE  
    | REORGANIZE  [ PARTITION = partition_number ] [ WITH ( <reorganize_option>  ) ]  
    | SET ( <set_index_option> [ ,...n ] )   
    | RESUME [WITH (<resumable_index_options>,[…n])]
    | PAUSE
    | ABORT
}  
[ ; ]  
  
<object> ::=   
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<rebuild_index_option > ::=  
{  
      PAD_INDEX = { ON | OFF }  
    | FILLFACTOR = fillfactor   
    | SORT_IN_TEMPDB = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | STATISTICS_INCREMENTAL = { ON | OFF }  
    | ONLINE = {   
          ON [ ( <low_priority_lock_wait> ) ]   
        | OFF } 
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | COMPRESSION_DELAY = {0 | delay [Minutes]}  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }   
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]  
}  
  
<single_partition_rebuild_index_option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<reorganize_option>::=  
{  
       LOB_COMPACTION = { ON | OFF }  
    |  COMPRESS_ALL_ROW_GROUPS =  { ON | OFF}  
}  
  
<set_index_option>::=  
{  
      ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | COMPRESSION_DELAY= {0 | delay [Minutes]}  
}  

<resumable_index_option> ::=
 { 
    MAXDOP = max_degree_of_parallelism
    | MAX_DURATION =<time> [MINUTES]
    | <low_priority_lock_wait>  
 }
 
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                          ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )  
}  

```  
  
```  
-- Syntax for SQL Data Warehouse and Parallel Data Warehouse 
  
ALTER INDEX { index_name | ALL }  
    ON   [ schema_name. ] table_name  
{  
      REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_index_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> )] ] 
      }  
    | DISABLE  
    | REORGANIZE [ PARTITION = partition_number ]  
}  
[;]  

<rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
  
```    
## <a name="arguments"></a>인수  
 *index_name*  
 인덱스의 이름입니다. 인덱스 이름은 테이블이나 뷰에서 고유해야 하지만 데이터베이스 내에서 고유할 필요는 없습니다. 인덱스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.  
  
 ALL  
 인덱스 유형에 관계없이 테이블이나 뷰에 연결된 모든 인덱스를 지정합니다. ALL을 지정하면 하나 이상의 인덱스가 오프라인 또는 읽기 전용 파일 그룹에 있거나 지정한 작업이 하나 이상의 인덱스 유형에 대해 허용되지 않을 경우 해당 문이 실패합니다. 다음 표에서는 인덱스 작업과 허용되지 않는 인덱스 유형을 나열합니다.  
  
|이 작업에 키워드 ALL 사용|테이블에 다음 인덱스가 하나 이상 있으면 실패함|  
|----------------------------------------|----------------------------------------|  
|REBUILD WITH ONLINE = ON|XML 인덱스<br /><br /> 공간 인덱스<br /><br /> columnstore 인덱스: **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|REBUILD PARTITION = *partition_number*|분할되지 않은 인덱스, XML 인덱스, 공간 인덱스 또는 비활성 인덱스|  
|REORGANIZE|ALLOW_PAGE_LOCKS가 OFF로 설정된 인덱스|  
|REORGANIZE PARTITION = *partition_number*|분할되지 않은 인덱스, XML 인덱스, 공간 인덱스 또는 비활성 인덱스|  
|IGNORE_DUP_KEY = ON|XML 인덱스<br /><br /> 공간 인덱스<br /><br /> columnstore 인덱스: **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|ONLINE = ON|XML 인덱스<br /><br /> 공간 인덱스<br /><br /> columnstore 인덱스: **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|
| RESUMABLE = ON  | 다시 시작할 수 있는 인덱스는 **All** 키워드에 대해 지원되지 않습니다. <br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] |   
  
> [!WARNING]
>  온라인으로 수행할 수 있는 인덱스 작업에 대한 자세한 내용은 [온라인 인덱스 작업 지침](../../relational-databases/indexes/guidelines-for-online-index-operations.md)을 참조하세요.

 ALL을 PARTITION = *partition_number*와 함께 지정하면 모든 인덱스가 정렬되어야 합니다. 즉, 해당 파티션 함수를 기준으로 인덱스가 분할됩니다. PARTITION 절에 ALL을 사용하면 같은 *partition_number*를 가진 모든 인덱스 파티션이 다시 작성되거나 다시 구성됩니다. 분할된 인덱스에 대한 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.  
  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이나 뷰가 속한 스키마의 이름입니다.  
  
 *table_or_view_name*  
 인덱스와 관련된 테이블이나 뷰의 이름입니다. 개체에 대한 인덱스 보고서를 표시하려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 사용합니다.  
  
 database_name이 현재 데이터베이스이거나 database_name이 tempdb이고 table_or_view_name이 #로 시작하는 경우 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]은 세 부분으로 구성된 이름 형식 database_name.[schema_name].table_or_view_name을 지원합니다.  
  
 REBUILD [ WITH **(**\<rebuild_index_option> [ **,**... *n*]**)** ]  
 동일한 열, 인덱스 유형, 고유성 특성 및 정렬 순서를 사용하여 인덱스가 다시 작성되도록 지정합니다. 이 절은 [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)와 동일합니다. REBUILD는 비활성 인덱스를 활성화합니다. ALL 키워드를 지정하지 않으면 클러스터형 인덱스를 다시 작성해도 관련 비클러스터형 인덱스는 다시 작성되지 않습니다. 인덱스 옵션을 지정하지 않으면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)에 저장된 기존 인덱스 옵션 값이 적용됩니다. **sys.indexes**에 값이 저장되지 않은 인덱스 옵션의 경우에는 옵션의 인수 정의에 표시된 기본값이 적용됩니다.  
  
 ALL을 지정한 경우 기본 테이블이 힙이면 다시 작성 작업을 수행해도 테이블에는 아무 영향이 없습니다. 테이블에 연결된 비클러스터형 인덱스는 모두 다시 작성됩니다.  
  
 데이터베이스 복구 모델이 대량 로그 또는 단순으로 설정되어 있으면 다시 작성 작업이 최소한으로 기록될 수 있습니다.  
  
> [!NOTE]
>  기본 XML 인덱스를 다시 작성할 때는 인덱스 작업 중에 기본 사용자 테이블을 사용할 수 없습니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 columnstore 인덱스의 다시 작성 작업은:  
  
1.  정렬 순서를 사용하지 않습니다.  
  
2.  다시 작성 작업이 발생한 동안 테이블 또는 파티션에서 배타적 잠금을 획득합니다.  NOLOCK, RCSI 또는 SI를 사용하는 경우에도 다시 작성 중에 데이터는 “오프라인”이며 사용할 수 없습니다.  
  
3.  모든 데이터를 columnstore로 다시 압축합니다. 다시 작성 작업이 발생한 동안에는 columnstore 인덱스의 두 복사본이 존재합니다. 다시 작성 작업이 끝나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 원래 columnstore 인덱스를 삭제합니다.  
  
 columnstore 인덱스 다시 작성에 대한 자세한 내용은 [columnstore 인덱스 - 조각 모음](../../relational-databases/indexes/columnstore-indexes-defragmentation.md) 참조  
  
PARTITION  

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 인덱스의 한 파티션만 다시 작성하거나 다시 구성하도록 지정합니다. *index_name*이 분할된 인덱스가 아니면 PARTITION을 지정할 수 없습니다.  
  
 PARTITION = ALL은 모든 파티션을 다시 작성합니다.  
  
> [!WARNING]
>  파티션 수가 1,000개를 초과하는 테이블에서 정렬되지 않은 인덱스를 만들거나 다시 작성할 수 있지만 해당 인덱스는 지원되지 않습니다. 그러면 작업 중에 성능이 저하되거나 메모리가 과도하게 소비될 수 있습니다. 파티션 수가 1,000개를 초과하는 경우에는 정렬된 인덱스만 사용하는 것이 좋습니다.  
  
 *partition_number*  
   
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 다시 작성하거나 다시 구성할 분할된 인덱스의 파티션 번호입니다. *partition_number*는 변수를 참조할 수 있는 상수 식입니다. 여기에는 사용자 정의 형식 변수 또는 함수와 사용자 정의 함수가 포함될 수 있지만 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 참조할 수 없습니다. *partition_number*를 지정하지 않으면 해당 문이 실패합니다.  
  
 WITH **(**\<single_partition_rebuild_index_option>**)**  
   
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 SORT_IN_TEMPDB, MAXDOP 및 DATA_COMPRESSION은 단일 파티션(PARTITION = *n*)을 다시 작성할 때 지정할 수 있는 옵션입니다. 단일 파티션 다시 작성 작업에는 XML 인덱스를 지정할 수 없습니다.  
  
 DISABLE  
 인덱스를 비활성 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 사용할 수 없음으로 표시합니다. 모든 인덱스를 비활성화할 수 있습니다. 비활성 인덱스의 인덱스 정의는 기본 인덱스 데이터 없이 시스템 카탈로그에 유지됩니다. 클러스터형 인덱스를 비활성화하면 사용자가 기본 테이블 데이터에 액세스하지 못합니다. 인덱스를 활성화하려면 ALTER INDEX REBUILD 또는 CREATE INDEX WITH DROP_EXISTING을 사용합니다. 자세한 내용은 [인덱스 및 제약 조건 비활성화](../../relational-databases/indexes/disable-indexes-and-constraints.md) 및 [인덱스 및 제약 조건 활성화](../../relational-databases/indexes/enable-indexes-and-constraints.md)를 참조하세요.  
  
 rowstore 인덱스 재구성(REORGANIZE)  
 rowstore 인덱스의 경우 REORGANIZE는 인덱스 리프 수준을 재구성하도록 지정합니다.  REORGANIZE 작업은:  
  
-   항상 온라인으로 수행됩니다. 즉, 장기간 차단 테이블 잠금이 유지되지 않으며 ALTER INDEX REORGANIZE 트랜잭션 중 기본 테이블에 대한 쿼리나 업데이트를 계속할 수 있습니다.  
  
-   비활성화된 인덱스에 대해서는 허용되지 않음  
  
-   ALLOW_PAGE_LOCKS가 OFF로 설정된 경우 허용되지 않음  
  
-   트랜잭션 내에서 수행되는 경우 롤백되지 않고 트랜잭션이 롤백됩니다.  
  
REORGANIZE WITH **(** LOB_COMPACTION = { **ON** | OFF } **)**  
 rowstore 인덱스에 적용됩니다.  
  
LOB_COMPACTION = ON  
  
-   다음과 같은 큰 개체(LOB) 데이터 형식의 데이터를 포함하는 모든 페이지를 압축하도록 지정합니다: 이미지, 텍스트, ntext, varchar(max), nvarchar(max), varbinary(max) 및 xml. 이 데이터를 압축하면 디스크상의 데이터 크기를 줄일 수 있습니다.  
  
-   클러스터형 인덱스의 경우 이렇게 하면 테이블에 포함된 모든 LOB 열이 압축됩니다.  
  
-   비클러스터형 인덱스의 경우 이렇게 하면 인덱스에서 키가 아닌(포괄) 열인 LOB 열이 모두 압축됩니다.  
  
-   REORGANIZE ALL은 모든 인덱스에 대해 LOB_COMPACTION을 수행합니다. 각 인덱스에 대해 클러스터형 인덱스의 모든 LOB 열, 기본 테이블 또는 비클러스터형 인덱스에 포함된 열이 압축됩니다.  
  
LOB_COMPACTION = OFF  
  
-   큰 개체 데이터가 포함된 페이지가 압축되지 않습니다.  
  
-   OFF를 지정해도 힙에는 아무 영향이 없습니다.  
  
columnstore 인덱스 재구성(REORGANIZE)  
REORGANIZE는 온라인으로 수행됩니다.  
  
columnstore 인덱스의 경우 REORGANIZE는 각 닫힌(CLOSED) 델타 rowgroup을 압축된 rowgroup으로 columnstore로 압축합니다.  
  
-   닫힌(CLOSED) 델타 rowgroup을 압축된 rowgroup으로 이동하는 데에는 REORGANIZE가 필요 없습니다. 배경 TM(튜플 이동기) 프로세스는 닫힌(CLOSED) 델타 rowgroup을 압축하기 위해 주기적으로 작동합니다. 튜플 이동기가 지연되는 경우 REORGANIZE를 사용하는 것이 좋습니다. REORGANIZE는 rowgroup를 더 적극적으로 압축할 수 있습니다.  
  
-   모든 열린(OPEN) 및 닫힌(CLOSED) rowgroup을 압축하려면 이 섹션의 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS) 옵션을 참조하세요.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](2016부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 columnstore 인덱스의 경우, REORGANIZE는 다음과 같은 추가 조각 모음 최적화를 온라인으로 수행합니다.  
  
-   행의 10% 이상이 논리적으로 삭제된 경우 rowgroup에서 행을 물리적으로 제거합니다. 삭제된 바이트는 물리적 미디어에서 회수됩니다. 예를 들어 행 1백만 개의 압축된 행 그룹이 삭제된 행 10만 개를 포함하는 경우, SQL Server는 삭제된 행을 제거하고 행이 90만 개인 rowgroup을 다시 압축합니다. 즉, 삭제된 행을 제거하여 저장소를 절약합니다.  
  
-   하나 이상의 압축된 rowgroup을 결합하여 rowgroup당 행 수를 최대 1,024,576개로 증가시킵니다. 예를 들어 행 102,400개의 대량 가져오기 5회를 수행하면 압축된 rowgroup 5개를 얻습니다. REORGANIZE를 실행하면 이러한 rowgroup이 크기 512,000행의 압축된 rowgroup 1개로 병합됩니다. 이때 사전 크기 또는 메모리 제한이 없는 것으로 가정합니다.  
  
-   행의 10% 이상이 논리적으로 삭제된 rowgroup의 경우 SQL Server는 이 rowgroup을 하나 이상의 rowgroup과 결합하려고 시도합니다.    예를 들어 rowgroup 1이 행 500,000개를 사용하여 압축된다면 rowgroup 21은 최대 1,048,576개의 행을 사용하여 압축됩니다.  즉, rowgroup 21은 삭제된 행 60%와 남은 행 409,830개를 포함합니다. SQL Server는 이러한 두 rowgroup을 결합하여 행 909,830개를 포함한 새 rowgroup을 압축하는 방법을 선호합니다.  
  
REORGANIZE WITH ( COMPRESS_ALL_ROW_GROUPS = { ON | **OFF** } )  

 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

COMPRESS_ALL_ROW_GROUPS는 열린(OPEN) 또는 닫힌(CLOSED) 델타 rowgroup을 columnstore로 강제 적용하는 방법을 제공합니다. 이 옵션을 사용할 때 델타 rowgroup을 비우기 위해 columnstore 인덱스를 다시 작성할 필요는 없습니다.  이 옵션은 다른 제거 및 병합 조각 모음 기능과 함께 결합할 경우 대부분의 상황에서 더 이상 인덱스를 다시 작성할 필요가 없습니다.    

-   ON은 크기 및 상태(CLOSED 또는 OPEN)와 상관없이 모든 rowgroup을 columnstore에 강제 적용합니다.  
  
-   OFF는 모든 닫힌(CLOSED) rowgroup을 columnstore에 강제 적용합니다.  
  
SET **(** \<set_index option> [ **,**... *n*] **)**  
 인덱스를 다시 작성하거나 다시 구성하지 않고 인덱스 옵션을 지정합니다. 비활성 인덱스에는 SET을 지정할 수 없습니다.  
  
PAD_INDEX = { ON | OFF }  
   
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 인덱스 패딩을 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 FILLFACTOR로 지정된 사용 가능한 공간의 비율이 인덱스의 중간 수준 페이지에 적용됩니다. FILLFACTOR를 지정함과 동시에 PAD_INDEX를 ON으로 설정하지 않으면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)에 저장된 채우기 비율 값이 사용됩니다.  
  
 OFF 또는 *fillfactor*를 지정되지 않음  
 중간 수준 페이지는 용량 한도 가까이 채워집니다. 이로 인해 중간 페이지의 키 집합을 기준으로 인덱스에 포함될 수 있는 최대 크기의 행 하나 이상을 위한 충분한 공간이 남겨집니다.  
  
 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
FILLFACTOR = *fillfactor*  
 
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 인덱스를 만들거나 변경할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. *fillfactor*는 1에서 100 사이의 정수 값이어야 하며 기본값은 0입니다. 채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
 명시적 FILLFACTOR 설정은 인덱스를 처음 만들거나 다시 작성할 때만 적용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 페이지에 지정된 비율의 빈 공간을 동적으로 유지하지 않습니다. 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
 채우기 비율 설정을 보려면 **sys.indexes**를 사용하세요.  
  
> [!IMPORTANT]
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 클러스터형 인덱스를 만들 때 데이터를 다시 배포하므로 FILLFACTOR  값으로 클러스터형 인덱스를 만들거나 변경하면 데이터가 차지하는 저장 공간 크기에 영향이 미칩니다.  
  
 SORT_IN_TEMPDB = { ON | **OFF** }  
 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 **tempdb**에 정렬 결과를 저장할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 인덱스 작성에 사용된 중간 정렬 결과가 **tempdb**에 저장됩니다. **tempdb**가 사용자 데이터베이스와는 다른 디스크 집합에 있으면 인덱스를 만드는 데 필요한 시간이 줄어들 수 있습니다. 그러나 인덱스 작성 중에 사용되는 디스크 공간의 크기는 커집니다.  
  
 OFF  
 중간 정렬 결과가 인덱스와 같은 데이터베이스에 저장됩니다.  
  
 정렬 작업이 필요하지 않거나 메모리에서 정렬을 수행할 수 있으면 SORT_IN_TEMPDB 옵션이 무시됩니다.  
  
 자세한 내용은 [인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)을 참조하세요.  
  
 IGNORE_DUP_KEY **=** { ON | OFF }  
 삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려는 경우에 대한 오류 응답을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. 기본값은 OFF입니다.  
  
 ON  
 중복된 키 값이 고유 인덱스에 삽입되는 경우 경고 메시지가 나타나고 고유성 제약 조건을 위반하는 행만 실패합니다.  
  
 OFF  
 중복된 키 값이 고유 인덱스에 삽입되는 경우 오류 메시지가 나타나고 전체 INSERT 작업이 롤백됩니다.  
  
 뷰, 비고유 인덱스, XML 인덱스, 공간 인덱스 및 필터링된 인덱스에 생성된 인덱스의 경우 IGNORE_DUP_KEY를 ON으로 설정할 수 없습니다.  
  
 IGNORE_DUP_KEY를 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)를 사용하세요.  
  
 이전 버전과 호환되는 구문에서 WITH IGNORE_DUP_KEY는 WITH IGNORE_DUP_KEY = ON과 같습니다.  
  
 STATISTICS_NORECOMPUTE **=** { ON | OFF }  
 배포 통계를 다시 계산할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 이전 통계가 자동으로 다시 계산되지 않습니다.  
  
 OFF  
 자동 통계 업데이트가 설정됩니다.  
  
 자동 통계 업데이트를 복원하려면 STATISTICS_NORECOMPUTE를 OFF로 설정하거나 NORECOMPUTE 절 없이 UPDATE STATISTICS를 실행합니다.  
  
> [!IMPORTANT]
> 배포 통계 자동 재계산 기능을 해제하면 쿼리 최적화 프로그램에서 테이블과 관련된 쿼리에 대해 최적의 실행 계획을 선택할 수 없습니다.  
  
 STATISTICS_INCREMENTAL = { ON | **OFF** }  
 **ON**으로 설정된 경우 파티션 통계별로 통계가 작성됩니다. **OFF**로 설정된 경우 통계 트리가 삭제되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 통계를 다시 계산합니다. 기본값은 **OFF**입니다.  
  
 파티션별 통계가 지원되지 않는 경우에는 이 옵션이 무시되고 경고가 생성됩니다. 다음 통계 유형에 대해서는 증분 통계가 지원되지 않습니다.  
  
-   기본 테이블을 기준으로 파티션 정렬되지 않은 인덱스를 사용하여 작성된 통계입니다.  
-   Always On 읽기 가능한 보조 데이터베이스에 대해 작성된 통계입니다.  
-   읽기 전용 데이터베이스에 대해 작성된 통계입니다.  
-   필터링된 인덱스에 대해 작성된 통계입니다.  
-   뷰에 대해 작성된 통계입니다.  
-   내부 테이블에 대해 작성된 통계입니다.  
-   공간 인덱스 또는 XML 인덱스를 사용하여 작성된 통계입니다.  
 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ONLINE **=** { ON | **OFF** } \<rebuild_index_option에 적용>  
 인덱스 작업 중 쿼리 및 데이터 수정에 기본 테이블과 관련 인덱스를 사용할 수 있는지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 XML 인덱스 또는 공간 인덱스의 경우 ONLINE = OFF만 지원되며 ONLINE을 ON으로 설정하면 오류가 발생합니다.  
  
> [!NOTE]
>  온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 대한 버전 및 지원되는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) 및 [SQL Server 2017에 대한 버전 및 지원되는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.  
  
 ON  
 인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 작업의 주 단계 중 내재된 공유(IS) 잠금만 원본 테이블에 유지됩니다. 따라서 기본 테이블 및 인덱스를 계속 쿼리 또는 업데이트할 수 있습니다. 작업이 시작될 때 아주 짧은 기간 동안 S(공유) 잠금이 원본 개체에서 유지됩니다. 작업이 끝날 때 짧은 기간 동안 비클러스터형 인덱스가 생성되는 경우에는 원본에 대해 S(공유) 잠금이 유지되고, 온라인 상태에서 클러스터형 인덱스가 생성 또는 삭제될 때나 클러스터형 또는 비클러스터형 인덱스가 다시 작성될 때는 SCH-M(스키마 수정) 잠금이 획득됩니다. 로컬 임시 테이블에서 인덱스를 생성하는 경우에는 ONLINE을 ON으로 설정할 수 없습니다.  
  
 OFF  
 인덱스 작업 중에 테이블 잠금이 적용됩니다. 클러스터형 인덱스, 공간 인덱스 또는 XML 인덱스를 생성, 다시 작성 또는 삭제하거나 비클러스터형 인덱스를 다시 작성 또는 삭제하는 오프라인 인덱스 작업은 테이블에 대해 SCH-M(스키마 수정) 잠금을 획득합니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다. 비클러스터형 인덱스를 만드는 오프라인 인덱스 작업을 통해 테이블의 S(공유) 잠금을 획득합니다. 따라서 기본 테이블을 업데이트할 수 없지만 SELECT 문과 같은 읽기 작업은 허용됩니다.  
  
 자세한 내용은 [온라인 인덱스 작업의 작동 원리](../../relational-databases/indexes/how-online-index-operations-work.md)를 참조하세요.  
  
 전역 임시 테이블의 인덱스를 비롯한 인덱스를 온라인으로 다시 작성할 수 있습니다. 단, 다음 항목은 예외입니다.  
  
-   XML 인덱스  
  
-   로컬 임시 테이블의 인덱스  
  
-   분할된 인덱스의 하위 집합(분할된 전체 인덱스를 온라인으로 다시 작성할 수 있음)  

-  V12 이전 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전 SQL Server는 기본 테이블이 **varchar(max)** 또는 **varbinary(max)** 열을 포함하는 경우 클러스터형 인덱스 작성 또는 다시 작성 작업에 대해 `ONLINE` 옵션을 허용하지 않습니다.

RESUMABLE **=** { ON | **OFF**}

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

 온라인 인덱스 작업이 다시 시작될 수 있는지 여부를 지정합니다.

 ON 인덱스 작업이 다시 시작될 수 있습니다.

 OFF 인덱스 작업이 다시 시작될 수 없습니다.

MAX_DURATION **=** *time* [**MINUTES**는] **RESUMABLE = ON** 상태에서만 사용됩니다(**ONLINE = ON** 필요).
 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

다시 시작할 수 있는 온라인 인덱스 작업이 일시 중지하기 전에 실행된 시간을 나타냅니다(분 단위로 지정된 정수 값). 

ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 행 잠금이 사용되지 않습니다.  
  
ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 페이지 잠금이 사용되지 않습니다.  
  
> [!NOTE]
>  ALLOW_PAGE_LOCKS가 OFF로 설정되면 인덱스를 다시 구성할 수 없습니다.  
  
 MAXDOP **=** max_degree_of_parallelism  
 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 인덱스 작업 기간 동안 **max degree of parallelism** 구성 옵션을 재정의합니다. 자세한 내용은 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
> [!IMPORTANT]
>  MAXDOP 옵션은 모든 XML 인덱스에 대해 구문으로는 지원되지만 공간 인덱스 또는 기본 XML 인덱스의 경우 ALTER INDEX는 현재 단일 프로세서만 사용합니다.  
  
 *max_degree_of_parallelism*은 다음 중 하나일 수 있습니다.  
  
 1  
 병렬 계획이 생성되지 않습니다.  
  
 \>1  
 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 지정된 값으로 제한합니다.  
  
 0(기본값)  
 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]
> 병렬 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 대한 버전 및 지원되는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 COMPRESSION_DELAY **=** { **0** |*duration [Minutes]* }  
 이 기능은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 사용할 수 있음  
  
 디스크 기반 테이블의 경우 지연은 CLOSED 상태의 델타 rowgroup이 SQL Server에서 압축된 rowgroup으로 압축할 수 있게 될 때까지 델타 rowgroup에 남아 있어야 하는 최소 분 수를 지정합니다. 디스크 기반 테이블은 개별 행에 대한 삽입 및 업데이트 시간을 추적하지 않으므로 SQL Server가 CLOSED 상태의 델타 rowgroup에 지연을 적용합니다.  
기본값은 0분입니다.  
  
 기본값은 0분입니다.  
  
 COMPRESSION_DELAY 사용 시기에 관한 권장 사항은 실시간 운영 분석을 위한 Columnstore 인덱스를 참조하세요.  
  
 DATA_COMPRESSION  
 지정된 인덱스, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.  
  
 없음  
 인덱스 또는 지정된 파티션이 압축되지 않습니다. columnstore 인덱스에는 적용되지 않습니다.  
  
 ROW  
 인덱스 또는 지정된 파티션이 행 압축을 사용하여 압축됩니다. columnstore 인덱스에는 적용되지 않습니다.  
  
 PAGE  
 인덱스 또는 지정된 파티션이 페이지 압축을 사용하여 압축됩니다. columnstore 인덱스에는 적용되지 않습니다.  
  
 COLUMNSTORE  
   
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE에서는 COLUMNSTORE_ARCHIVE 옵션으로 압축된 지정 파티션 또는 인덱스를 압축 해제하도록 지정합니다. 데이터는 복구될 때 모든 columnstore 인덱스에 사용된 columnstore 압축으로 계속 압축됩니다.  
  
 COLUMNSTORE_ARCHIVE  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE_ARCHIVE는 지정된 파티션을 보다 작은 크기로 압축합니다. 보다 적은 저장소 크기가 필요한 기타 상황에서 보관하는 데 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
 ON PARTITIONS **(** { \<partition_number_expression> | \<range> } [**,**...n] **)**  
    
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. 
  
 DATA_COMPRESSION 설정을 적용할 파티션을 지정합니다. 인덱스가 분할되지 않은 경우 ON PARTITIONS 인수를 사용하면 오류가 발생합니다. ON PARTITIONS 절을 제공하지 않으면 DATA_COMPRESSION 옵션이 분할된 인덱스의 모든 파티션에 적용됩니다.  
  
 \<partition_number_expression>은 다음과 같은 방법으로 지정할 수 있습니다.  
  
-   파티션의 번호를 지정합니다(예: ON PARTITIONS (2)).  
  
-   여러 개별 파티션의 파티션 번호를 쉼표로 구분하여 지정합니다(예: ON PARTITIONS (1,5)).  
  
-   범위와 개별 파티션을 모두 지정합니다(ON PARTITIONS (2,4,6 TO 8)).  
  
 \<range>는 단어 TO로 구분된 파티션 번호로 지정할 수 있습니다(예: ON PARTITIONS (6 TO 8)).  
  
 여러 파티션에 대해 서로 다른 데이터 압축 유형을 설정하려면 DATA_COMPRESSION 옵션을 두 번 이상 지정합니다. 예를 들면 다음과 같습니다.  
  
```sql  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
 ONLINE **=** { ON  | **OFF** } \<single_partition_rebuild_index_option에 적용>  
 기본 테이블의 인덱스 또는 인덱스 파티션을 온라인 또는 오프라인으로 다시 작성할 수 있는지 여부를 지정합니다. **REBUILD**가 온라인(**ON**)으로 수행될 경우, 인덱스 작업 중에 이 테이블의 데이터를 쿼리 및 데이터 수정을 위해 사용할 수 있습니다.  기본값은 **OFF**입니다.  
  
 ON  
 인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 작업의 주 단계 중 내재된 공유(IS) 잠금만 원본 테이블에 유지됩니다. 인덱스 다시 작성을 시작할 때 테이블에 대한 S-잠금이 필요하고 온라인 인덱스 다시 작성을 종료할 때 테이블에 대한 Sch-M 잠금이 필요합니다. 두 잠금 모두 짧은 메타데이터 잠금이지만 특히 Sch-M 잠금은 모든 차단 트랜잭션이 완료될 때까지 기다려야 합니다. 대기 시간 동안 Sch-M 잠금은 동일 테이블에 액세스할 때 이 잠금 뒤에서 기다리는 다른 모든 트랜잭션을 차단합니다.  
  
> [!NOTE]
>  온라인 인덱스 다시 작성은 이 섹션의 뒷부분에서 설명하는 *low_priority_lock_wait* 옵션을 설정할 수 있습니다.  
  
 OFF  
 인덱스 작업 중에 테이블 잠금이 적용됩니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다.  
  
 **ONLINE=ON**은 WAIT_AT_LOW_PRIORITY 상태에서만 사용됩니다.  
 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 온라인 인덱스 다시 작성에서 이 테이블의 차단 작업을 대기해야 합니다. **WAIT_AT_LOW_PRIORITY**는 온라인 인덱스 작성 작업이 대기하는 동안 다른 작업을 진행할 수 있도록 온라인 인덱스 재작성 작업이 우선 순위가 낮은 잠금을 대기함을 나타냅니다. **WAIT AT LOW PRIORITY** 옵션을 생략하는 것은 `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`와 동일합니다. 자세한 내용은 [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md)를 참조하세요. 
  
 MAX_DURATION = *time* [**MINUTES**]  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 DDL 명령을 실행할 때 온라인 인덱스 다시 작성 잠금이 낮은 우선 순위로 대기하는 시간(분 단위로 지정된 정수 값)입니다. 작업이 **MAX_DURATION** 시간 동안 차단되면 **ABORT_AFTER_WAIT** 작업 중 하나가 실행됩니다. **MAX_DURATION** 시간은 항상 분 단위이며 단어 **MINUTES**는 생략할 수 있습니다.  
 
 ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERS** } ]  
   
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 없음  
 보통(일반) 우선 순위로 잠금을 계속 대기합니다.  
  
 SELF  
 어떤 동작도 수행하지 않고 현재 실행 중인 온라인 인덱스 다시 작성 DDL 작업을 종료합니다.  
  
 BLOCKERS  
 작업을 계속할 수 있도록 온라인 인덱스 다시 작성 DDL 작업을 차단하는 모든 사용자 트랜잭션을 종료합니다. **BLOCKERS** 옵션을 사용하려면 **ALTER ANY CONNECTION** 권한을 가진 로그인이 필요합니다.  
 
 RESUME 
 
**적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터  

수동으로 일시 중지되거나 실패로 인해 발생한 인덱스 작업을 다시 시작합니다.

MAX_DURATION은 **RESUMABLE=ON** 상태에서만 사용됨

 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

다시 시작된 후 다시 시작할 수 있는 온라인 인덱스 작업이 실행되는 시간(분 단위로 지정한 정수 값)입니다. 시간이 만료된 후 다시 시작할 수 있는 작업이 여전히 실행 중인 경우 일시 중지됩니다.

WAIT_AT_LOW_PRIORITY는 **RESUMABLE=ON** 및 **ONLINE = ON** 상태에서만 사용됩니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 
  
 일시 중지 후 온라인 인덱스 다시 작성을 다시 시작하려면 이 테이블에 대한 작업이 차단되기를 기다려야 합니다. **WAIT_AT_LOW_PRIORITY**는 온라인 인덱스 작성 작업이 대기하는 동안 다른 작업을 진행할 수 있도록 온라인 인덱스 재작성 작업이 우선 순위가 낮은 잠금을 대기함을 나타냅니다. **WAIT AT LOW PRIORITY** 옵션을 생략하는 것은 `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`와 동일합니다. 자세한 내용은 [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md)를 참조하세요. 


일시 중지
 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 
  
다시 시작 가능한 온라인 인덱스 다시 작성 작업을 일시 중지합니다.

중단

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

다시 시작한 것으로 선언된 실행 중이거나 일시 중지된 인덱스 작업을 중단합니다. 다시 시작할 수 있는 인덱스 다시 작성 작업을 종료하려면 **중단** 명령을 명시적으로 실행해야 합니다. 다시 시작할 수 있는 인덱스 작업이 실패하거나 일시 중지해도 실행이 종료되지 않으며, 그 대신 작업이 무한한 일시 중지 상태로 남아 있습니다.
  
## <a name="remarks"></a>Remarks  
 인덱스를 다시 분할하거나 다른 파일 그룹으로 이동하는 데는 ALTER INDEX를 사용할 수 없습니다. 이 문을 사용하여 열 추가 또는 삭제, 열 순서 변경과 같은 인덱스 정의를 수정할 수 없습니다. 이러한 작업을 수행하려면 DROP_EXISTING 절에 CREATE INDEX를 사용하세요.  
  
 옵션을 명시적으로 지정하지 않으면 현재 설정이 적용됩니다. 예를 들어, REBUILD 절에 FILLFACTOR 설정을 지정하지 않으면 다시 작성하는 동안 시스템 카탈로그에 저장된 채우기 비율 값이 사용됩니다. 현재 인덱스 옵션 설정을 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)를 사용하세요.  
  
> [!NOTE]
> ONLINE, MAXDOP 및 SORT_IN_TEMPDB에 대한 값은 시스템 카탈로그에 저장되지 않습니다. 인덱스 문에서 지정하지 않으면 해당 옵션의 기본값이 사용됩니다.
  
 다중 프로세서 컴퓨터에서는 다른 쿼리의 경우와 마찬가지로 ALTER INDEX REBUILD가 자동으로 프로세서를 더 사용하여 인덱스 수정과 관련된 정렬 및 검색 작업을 수행합니다. LOB_COMPACTION을 사용하거나 사용하지 않고 ALTER INDEX REORGANIZE를 실행할 경우 **max degree of parallelism** 값은 단일 스레드 작업입니다. 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
 인덱스가 위치한 파일 그룹이 오프라인이거나 읽기 전용으로 설정되어 있으면 인덱스를 다시 구성할 수 없습니다. ALL 키워드를 지정하면 하나 이상의 인덱스가 오프라인 또는 읽기 전용 파일 그룹에 있을 경우 해당 문이 실패합니다.  
  
## <a name="rebuilding-indexes"></a> 인덱스 다시 작성  
 인덱스를 다시 작성하면 이 인덱스가 삭제된 다음 다시 생성됩니다. 이렇게 하면 조각화를 제거하고, 지정된 채우기 비율 또는 기존 채우기 비율 설정을 기준으로 페이지를 압축하여 디스크 공간을 회수하고, 인덱스 행을 연속된 페이지로 다시 정렬할 수 있습니다. ALL을 지정하면 테이블의 모든 인덱스가 단일 트랜잭션으로 삭제되고 다시 작성됩니다. FOREIGN KEY 제약 조건은 미리 삭제하지 않아도 됩니다. 익스텐트가 128개 이상인 인덱스를 다시 작성하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 실제 페이지 할당 취소와 해당 관련 잠금이 트랜잭션 커밋 후까지 지연됩니다.  
  
 작은 인덱스는 다시 작성하거나 다시 구성해도 조각화가 줄어들지 않는 경우가 많습니다. 작은 인덱스의 페이지는 종종 혼합 익스텐트에 저장됩니다. 혼합 익스텐트는 최대 8개의 개체가 공유할 수 있으므로 인덱스를 다시 작성하거나 다시 구성한 후에도 작은 인덱스의 조각화가 줄어들지 않을 수 있습니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 분할된 인덱스를 만들거나 다시 작성할 때 테이블의 모든 행을 검사하여 통계를 작성하지 않습니다. 대신 쿼리 최적화 프로그램에서 기본 샘플링 알고리즘을 사용하여 통계를 생성합니다. 테이블의 모든 행을 검사하여 분할된 인덱스에 대한 통계를 얻으려면 FULLSCAN 절에서 CREATE STATISTICS 또는 UPDATE STATISTICS를 사용합니다.  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 비클러스터형 인덱스를 다시 작성하여 하드웨어 오류로 인한 불일치를 해결할 수 있는 경우도 있습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상에서도 비클러스터형 인덱스를 오프라인으로 다시 작성하여 인덱스와 클러스터형 인덱스 간의 불일치를 복구할 수 있습니다. 그러나 인덱스를 온라인으로 다시 작성하는 경우에는 비클러스터형 인덱스 간의 불일치를 해결할 수 없습니다. 온라인으로 다시 작성하는 경우 기존의 비클러스터형 인덱스를 사용하므로 불일치가 계속 남아 있게 됩니다. 경우에 따라 오프라인으로 인덱스를 다시 작성하면 클러스터형 인덱스 검색 또는 힙 검색이 수행되어 불일치가 제거됩니다. 클러스터형된 인덱스에서 다시 작성되도록 하려면 비클러스터형 인덱스를 삭제한 후 다시 만드세요. 이전 버전의 경우처럼 영향을 받은 데이터를 백업한 후 복원하여 불일치를 제거하는 것이 좋습니다. 비클러스터형 인덱스의 경우에는 오프라인으로 인덱스를 다시 작성하여 인덱스 간 불일치를 해결할 수 있습니다. 자세한 내용은 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 참조하세요.  
  
 클러스터형 columnstore 인덱스를 다시 작성하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  다시 작성 작업이 발생한 동안 테이블 또는 파티션에서 배타적 잠금을 획득합니다. 다시 작성 중에 데이터는 “오프라인”이며 사용할 수 없습니다.  
  
2.  테이블에서 논리적으로 삭제된 행을 물리적으로 삭제하여 columnstore를 조각 모음합니다. 삭제된 바이트는 물리적 미디어에서 회수됩니다.  
  
3.  deltastore를 비롯하여 원래 columnstore 인덱스의 모든 데이터를 읽습니다. 데이터를 새 행 그룹으로 결합하고 행 그룹을 columnstore로 압축합니다.  
  
4.  다시 작성이 진행되는 동안 실제 미디어에 columnstore 인덱스의 사본을 두 개 저장할 공간이 필요합니다. 다시 작성 작업이 끝나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 원래 클러스터형 columnstore 인덱스를 삭제합니다.  
  
## <a name="reorganizing-indexes"></a> 인덱스 다시 구성  
 인덱스를 다시 구성할 때는 최소한의 시스템 리소스가 사용됩니다. 이때는 왼쪽에서 오른쪽으로 표시되는 리프 노드의 논리적 순서에 맞도록 리프 수준 페이지를 물리적으로 다시 정렬하여 테이블 및 뷰의 클러스터형 및 비클러스터형 인덱스의 리프 수준에 대한 조각 모음을 수행합니다. 다시 구성 작업을 수행하면 인덱스 페이지도 압축됩니다. 이때 압축은 기존 채우기 비율 값을 기준으로 수행됩니다. 채우기 비율 설정을 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)를 사용하세요.  
  
 ALL을 지정하면 테이블에서 관계형 인덱스, 클러스터형 및 비클러스터형 모두와 XML 인덱스가 다시 구성됩니다. ALL을 지정할 때는 몇 가지 제한 사항이 적용됩니다. 자세한 내용은 인수 섹션에서 ALL에 대한 정의를 참조하세요.  
  
 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
## <a name="disabling-indexes"></a> 인덱스 비활성화  
 인덱스를 비활성화하면 사용자가 인덱스에 액세스할 수 없으며 클러스터형 인덱스의 경우 기본 테이블 데이터에도 액세스할 수 없습니다. 인덱스 정의는 시스템 카탈로그에 유지됩니다. 뷰의 비클러스터형 인덱스 또는 클러스터형 인덱스를 비활성화하면 인덱스 데이터가 물리적으로 삭제됩니다. 클러스터형 인덱스를 비활성화하면 데이터에 액세스할 수 없지만 인덱스가 삭제되거나 다시 작성될 때까지는 데이터가 B-트리에서 유지 관리되지 않는 상태로 남아 있습니다. 활성 또는 비활성 인덱스의 상태를 보려면 **sys.indexes** 카탈로그 뷰의 **is_disabled** 열을 쿼리합니다.  
  
 트랜잭션 복제 게시의 테이블에서는 기본 키 열과 연결된 인덱스를 해제할 수 없습니다. 이러한 인덱스는 복제에 필요합니다. 인덱스를 해제하려면 먼저 게시에서 테이블을 삭제해야 합니다. 자세한 내용은 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)를 참조하세요.  
  
 ALTER INDEX REBUILD 문 또는 CREATE INDEX WITH DROP_EXISTING 문을 사용하여 인덱스를 활성화할 수 있습니다. ONLINE 옵션이 ON으로 설정되어 있으면 비활성화된 클러스터형 인덱스를 다시 작성할 수 없습니다. 자세한 내용은 [인덱스 및 제약 조건 비활성화](../../relational-databases/indexes/disable-indexes-and-constraints.md)를 참조하세요.  
  
## <a name="setting-options"></a>옵션 설정  
 지정한 인덱스에 대해 해당 인덱스를 다시 작성하거나 다시 구성하지 않고 ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, IGNORE_DUP_KEY 및 STATISTICS_NORECOMPUTE 옵션을 설정할 수 있습니다. 수정된 값은 인덱스에 바로 적용됩니다. 이러한 설정을 보려면 **sys.indexes**를 사용하세요. 자세한 내용은 [인덱스 옵션 설정](../../relational-databases/indexes/set-index-options.md)을 참조하세요.  
  
### <a name="row-and-page-locks-options"></a>행 및 페이지 잠금 옵션  
 ALLOW_ROW_LOCKS = ON이고 ALLOW_PAGE_LOCK = ON이면 인덱스에 액세스할 때 행 수준, 페이지 수준 및 테이블 수준 잠금이 허용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 적절한 잠금을 선택하고 행 또는 페이지 잠금에서 테이블 잠금으로 잠금을 에스컬레이션할 수 있습니다.  
  
 ALLOW_ROW_LOCKS = OFF이고 ALLOW_PAGE_LOCK = OFF이면 인덱스에 액세스할 때 테이블 수준 잠금만 허용됩니다.  
  
 행 또는 페이지 잠금 옵션이 설정된 경우 ALL을 지정하면 설정이 모든 인덱스에 적용됩니다. 기본 테이블이 힙인 경우 다음과 같은 방식으로 설정이 적용됩니다.  
  
|||  
|-|-|  
|ALLOW_ROW_LOCKS = ON 또는 OFF|힙 및 연결된 비클러스터형 인덱스|  
|ALLOW_PAGE_LOCKS = ON|힙 및 연결된 비클러스터형 인덱스|  
|ALLOW_PAGE_LOCKS = OFF|비클러스터형 인덱스 전체. 즉, 비클러스터형 인덱스에는 모든 페이지 잠금이 허용되지 않습니다. 힙에서는 페이지에 대한 공유(S), 업데이트(U) 및 배타(X) 잠금만 허용되지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 내부에서 사용하기 위해 의도 페이지 잠금(IS,  IU  또는 IX)을 획득할 수 있습니다.|  
  
## <a name="online-index-operations"></a> 온라인 인덱스 작업  
 인덱스를 다시 작성할 때 ONLINE 옵션이 ON으로 설정되어 있으면 기본 개체, 테이블 및 연결된 인덱스를 쿼리와 데이터 수정에 사용할 수 있습니다. 단일 파티션에 있는 인덱스 부분을 온라인으로 다시 작성할 수도 있습니다. 변경 중에는 아주 잠시 동안만 배타적 테이블 잠금이 유지됩니다.  
  
 인덱스를 다시 구성하는 과정은 항상 온라인으로 수행됩니다. 이 프로세스는 잠금을 장기간 유지하지 않으므로 실행 중인 업데이트나 쿼리를 차단하지 않습니다.  
  
 다음을 수행할 때만 동일한 테이블 또는 테이블 파티션에서 동시 온라인 작업을 수행할 수 있습니다.  
  
-   여러 개의 비클러스터형 인덱스 생성  
-   동일한 테이블에서 여러 인덱스 다시 구성  
-   동일한 테이블에서 겹치지 않는 인덱스를 다시 작성하는 동안 여러 인덱스 다시 구성  
  
 동시에 수행된 다른 온라인 인덱스 작업이 모두 실패합니다. 예를 들어, 동일한 테이블에서 두 개 이상의 인덱스를 다시 작성할 수 없습니다. 또는 동일한 테이블에서 기존 인덱스를 다시 작성하면서 새 인덱스를 생성할 수 없습니다.  

### <a name="resumable-indexes"></a> 다시 시작 가능한 인덱스 작업

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

ONLINE INDEX REBUILD는 RESUMABLE=ON 옵션을 사용하여 다시 시작 가능한 것으로 지정됩니다. 
-  RESUMABLE 옵션은 지정된 인덱스에 대해 메타데이터에서 지속되며 현재 DDL 문의 기간에만 적용됩니다.  그러므로 다시 시작이 가능하도록 하려면 RESUMABLE=ON 절을 명시적으로 지정해야 합니다.
-  MAX_DURATION 옵션은 두 가지가 있습니다. 하나는 low_priority_lock_wait와 관련되며 다른 하나는 RESUMABLE=ON 옵션과 관련이 있습니다.
   -  MAX_DURATION 옵션은 RESUMABLE=ON 옵션 또는 **low_priority_lock_wait** 인수 옵션에 대해 지원됩니다. 
   -  RESUMABLE에 대한 MAX_DURATION은 다시 작성하는 인덱스의 시간 간격을 지정합니다. 이 시간이 사용된 후 인덱스 다시 작성이 일시 중지되거나 그 실행이 완료됩니다. 사용자는 일시 중지된 인덱스에 대한 다시 작성이 다시 시작될 수 있는 시기를 결정합니다. MAX_DURATION에 대한 분 단위의 **시간**은 0분보다 크거나 1주일(7 * 24 * 60 = 10080분) 이하여야 합니다. 원래 인덱스와 새로 만든 인덱스 두 인덱스가 모두 디스크 공간을 필요로 하고 DML 작업 중에 업데이트되어야 하므로, 인덱스 작업을 오랫동안 일시 중지하면 특정 테이블에 대한 DML 성능 및 데이터베이스 디스크 용량에 영향을 미칠 수 있습니다. MAX_DURATION 옵션을 생략하면 인덱스 작업은 완료될 때까지 또는 실패가 발생할 때까지 계속됩니다. 
-   \<low_priority_lock_wait> 인수 옵션을 사용하면 인덱스 작업이 SCH-M 잠금에 대해 차단될 경우 계속할 수 있는 방법을 결정할 수 있습니다.
 
-  같은 매개 변수를 지정하고 원본 ALTER INDEX REBUILD 문을 다시 실행하면 일시 중지된 인덱스 다시 작성 작업이 다시 시작됩니다. 또한 ALTER INDEX RESUME 문을 실행하여 일시 중지된 인덱스 다시 작성 작업을 다시 시작할 수도 있습니다.
-  SORT_IN_TEMPDB=ON 옵션은 다시 시작 가능한 인덱스에 대해 지원되지 않습니다. 
-  RESUMABLE=ON 상태의 DDL 명령은 명시적 트랜잭션 내에서 실행할 수 없습니다(begin tran ... commit block의 일부일 수 없음).
-  일시 중지된 인덱스 작업만이 다시 시작될 수 있습니다.
-  일시 중지된 인덱스 작업을 다시 시작할 때 MAXDOP 값을 새 값으로 변경할 수 있습니다.  일시 중지된 인덱스 작업을 다시 시작할 때 MAXDOP를 지정하지 않으면 마지막 MAXDOP 값을 가져옵니다. 인덱스 다시 작성 작업에 대해 MAXDOP 옵션을 전혀 지정하지 않으면 기본값을 가져옵니다.
- 인덱스 작업을 즉시 일시 중지하려면 진행 중인 명령을 중지하거나(Ctrl-C) ALTER INDEX PAUSE 명령 또는 KILL *session_id* 명령을 실행할 수 있습니다. 명령이 일시 중지된 후 RESUME 옵션을 사용하여 다시 시작할 수 있습니다.
-  ABORT 명령은 원본 인덱스 다시 작성을 호스팅한 세션을 종료하고 인덱스 작업을 중단합니다.  
-  다음을 제외하고 다시 시작 가능한 인덱스 다시 작성을 위해 필요한 추가 리소스는 없습니다.
   -    인덱스가 일시 중지될 시간을 포함하여 작성 중인 인덱스를 유지하기 위해 필요한 추가 공간
   -    DDL 수정을 하지 못하게 하는 DDL 상태
-  고스트 정리는 인덱스 일시 중지 단계 중에 실행되지만 인덱스 실행 중에 일시 중지됩니다.   
다음 기능은 다시 시작 가능한 인덱스 다시 작성 작업에 대해 비활성화됩니다.
   -    비활성화된 인덱스 다시 작성은 RESUMABLE=ON 상태에서 지원되지 않습니다.
   -    ALTER INDEX REBUILD ALL 명령
   -    인덱스 다시 작성을 사용한 ALTER TABLE  
   -    "RESUMABLE=ON" 상태의 DDL 명령은 명시적 트랜잭션 내에서 실행할 수 없습니다(begin tran ... commit  block의 일부일 수 없음).
   -    계산되었거나 TIMESTAMP 열을 키 열로 포함하는 인덱스를 다시 작성합니다.
-   LOB 열을 포함하는 기본 테이블의 경우 다시 시작 가능한 클러스터형 인덱스를 다시 작성하려면 이 작업의 시작 부분에 Sch-M 잠금이 필요합니다.
   -    SORT_IN_TEMPDB=ON 옵션은 다시 시작 가능한 인덱스에 대해 지원되지 않습니다. 

> [!NOTE]
> DDL 명령은 완료, 일시 중지 또는 실패할 때까지 실행됩니다. 명령이 일시 중지된 경우 작업이 일시 중지되었고 인덱스 만들기가 완료되지 않았음을 알려 주는 오류가 발생합니다. 현재 인덱스 상태에 대한 더 자세한 내용은 [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md)에서 가져올 수 있습니다. 이전과 마찬가지로 실패의 경우 오류도 발생합니다. 

 자세한 내용은 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요.  
  
 ### <a name="waitatlowpriority-with-online-index-operations"></a>온라인 인덱스 작업에 대한 WAIT_AT_LOW_PRIORITY  
  
 온라인 인덱스 다시 작성을 위해 DDL 문을 실행하려면 특정 테이블에서 실행 중인 모든 활성 차단 트랜잭션이 완료되어야 합니다. 온라인 인덱스 다시 작성이 실행되면 이 테이블에서 실행을 시작할 준비가 되어 있는 모든 새로운 트랜잭션이 차단됩니다. 온라인 인덱스 다시 작성에 대한 잠금 기간은 매우 짧지만 특정 테이블에서 열려 있는 모든 트랜잭션이 완료될 때까지 기다리고 새로운 트랜잭션이 시작되지 않도록 차단하기 위해서는 처리량에 상당한 영향을 주어 작업 속도가 느려지거나 시간 초과가 발생할 수 있으며, 기본 테이블에 대한 액세스가 크게 제한될 수 있습니다. DBA는 **WAIT_AT_LOW_PRIORITY** 옵션을 사용해서 온라인 인덱스 다시 작성에 필요한 S-잠금 및 Sch-M 잠금을 관리할 수 있으며, 3개 옵션 중 하나를 선택할 수 있습니다. 세 가지 경우 모두, 대기 시간(`(MAX_DURATION = n [minutes])`) 중에 차단 활동이 없으면 대기 없이 온라인 인덱스 다시 작성이 즉시 실행되고 DDL 문이 완료됩니다.  
  
## <a name="spatial-index-restrictions"></a>공간 인덱스 제한 사항  
 공간 인덱스를 다시 작성할 때는 공간 인덱스에 스키마 잠금이 유지되기 때문에 인덱스 작업 중에 기본 사용자 테이블을 사용할 수 없습니다.  
  
 공간 인덱스가 해당 테이블의 열에 정의된 경우 사용자 테이블에 있는 PRIMARY KEY 제약 조건을 수정할 수 없습니다. PRIMARY KEY 제약 조건을 변경하려면 먼저 테이블의 모든 공간 인덱스를 삭제해야 합니다. PRIMARY KEY 제약 조건을 수정한 후에는 각 공간 인덱스를 다시 만들 수 있습니다.  
  
 단일 파티션 다시 작성 작업에서는 공간 인덱스를 지정할 수 없습니다. 하지만 전체 파티션을 다시 작성할 때는 공간 인덱스를 지정할 수 있습니다.  
  
 공간 인덱스에 지정된 옵션(예: BOUNDING_BOX 또는 GRID)을 변경하려면 DROP_EXISTING = ON을 지정하는 CREATE SPATIAL INDEX 문을 사용하거나 해당 공간 인덱스를 삭제하고 새로 만들 수 있습니다. 예제를 보려면 [CREATE SPATIAL INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)의 "주의" 섹션을 참조하세요.  
  
## <a name="data-compression"></a>Data Compression  
 데이터 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
 페이지(PAGE) 및 행(ROW) 압축을 변경할 경우 테이블, 인덱스 또는 파티션에 어떤 영향을 주는지 확인하려면 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 저장 프로시저를 사용합니다.  
  
다음은 분할된 인덱스에 적용되는 제한 사항입니다.  
  
-   `ALTER INDEX ALL ...`을 사용하는 경우 테이블에 정렬되지 않은 인덱스가 있으면 단일 파티션의 압축 설정을 변경할 수 없습니다.  
-   The ALTER INDEX \<index> ... REBUILD  PARTITION  ...  구문은 인덱스의 지정된 파티션을 다시 작성합니다.  
-   The ALTER INDEX \<index> ... REBUILD  WITH  ...  구문은 인덱스의 모든 파티션을 다시 작성합니다.  
  
## <a name="statistics"></a>통계  
 **ALTER INDEX ALL ...** 을 테이블에 대해 실행하면 인덱스와 연관된 통계만 업데이트됩니다. 인덱스 대신 테이블에 대해 만들어진 자동 또는 수동 통계는 업데이트되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 ALTER INDEX를 실행하려면 최소한 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
## <a name="version-notes"></a>버전 참고 사항  
  
-  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]는 파일 그룹 및 파일 스트림 옵션을 사용하지 않습니다.  
-  columnstore 인덱스는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전에 사용할 수 없습니다. 
-  다시 시작 가능한 인덱스 작업은 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]부터 사용할 수 있습니다.   
  
## <a name="basic-syntax-example"></a>기본 구문 예제:   
  
```sql 
ALTER INDEX index1 ON table1 REBUILD;  
  
ALTER INDEX ALL ON table1 REBUILD;  
  
ALTER INDEX ALL ON dbo.table1 REBUILD;  
```

## <a name="examples-columnstore-indexes"></a>예제: columnstore 인덱스  
 이 예제는 columnstore 인덱스에는 적용되지 않습니다.  
  
### <a name="a-reorganize-demo"></a>1. REORGANIZE 데모  
 이 예제에서는 ALTER INDEX REORGANIZE 명령의 작동 원리를 보여줍니다.  복수의 rowgroup이 있는 테이블을 만든 다음, REORGANIZE가 rowgroup을 병합하는 방법을 보여줍니다.  
  
```sql  
-- Create a database   
CREATE DATABASE [ columnstore ];  
GO  
  
-- Create a rowstore staging table  
CREATE TABLE [ staging ] (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey     int  
     )  
  
-- Insert 10 million rows into the staging table.   
DECLARE @loop int  
DECLARE @AccountDescription varchar(50)  
DECLARE @AccountKey int  
DECLARE @AccountType varchar(50)  
DECLARE @AccountCode int  
  
SELECT @loop = 0  
BEGIN TRAN  
    WHILE (@loop < 300000)   
      BEGIN  
        SELECT @AccountKey = CAST (RAND()*10000000 as int);  
        SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountCode =  CAST (RAND()*10000000 as int);  
  
        INSERT INTO  staging VALUES (@AccountKey, @AccountDescription, @AccountType, @AccountCode);  
  
        SELECT @loop = @loop + 1;  
    END  
COMMIT  
  
-- Create a table for the clustered columnstore index  
  
CREATE TABLE cci_target (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey int  
     )  
  
-- Convert the table to a clustered columnstore index named inxcci_cci_target;  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;  
```  
  
 TABLOCK 옵션을 사용하여 행을 병렬로 삽입합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 INSERT INTO 작업은 TABLOCK이 사용되는 경우 병렬로 실행할 수 있습니다.  
  
```sql  
INSERT INTO cci_target WITH (TABLOCK) 
SELECT TOP 300000 * FROM staging;  
```  
  
 OPEN 델타 rowgroup을 보려면 이 명령을 실행합니다. rowgroup 수는 병렬 처리 수준에 따라 달라집니다.  
  
```sql  
SELECT *   
FROM sys.dm_db_column_store_row_group_physical_stats   
WHERE object_id  = object_id('cci_target');  
```  
  
 모든 닫힌(CLOSED) 및 열린(OPEN) rowgroup을 columnstore에 강제 적용하려면 이 명령을 실행합니다.  
  
```sql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
 이 명령을 다시 실행하면 더 작은 rowgroup들이 압축된 rowgroup으로 병합되는 것을 확인할 수 있습니다.  
  
```sql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="b-compress-closed-delta-rowgroups-into-the-columnstore"></a>2. 닫힌(CLOSED) 델타 rowgroup을 columnstore으로 압축  
 이 예제에서는 REORGANIZE 옵션을 사용하여 각 닫힌(CLOSED) 델타 rowgroup을 압축된 rowgroup으로 columnstore으로 압축합니다.   이 작업은 필수는 아니지만 튜플 이동기가 닫힌(CLOSED) rowgroup을 충분히 빠르게 압축하지 않는 경우에 유용합니다.  
  
```sql  
-- Uses AdventureWorksDW  
-- REORGANIZE all partitions  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
  
-- REORGANIZE a specific partition  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;  
```  
  
### <a name="c-compress-all-open-and-closed-delta-rowgroups-into-the-columnstore"></a>3. 모든 열린(OPEN) 및 닫힌(CLOSED) 델타 rowgroup을 columnstore으로 압축  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 
  
 REORGANIZE WITH ( COMPRESS_ALL_ROW_GROUPS = ON ) 명령은 각 열린(OPEN) 및 닫힌(CLOSED) 델타 rowgroup을 압축된 rowgroup으로 columnstore로 압축합니다. 이렇게 하면 deltastore가 비워지고 모든 행이 columnstore로 압축되도록 강제 적용합니다. 이러한 작업은 행을 하나 이상의 델타 행 그룹에 저장하므로 이 기능은 많은 삽입 작업을 수행한 후 특히 유용합니다.  
  
 REORGANIZE는 rowgroup을 결합하여 rowgroup을 행 수 \<= 1,024,576까지 채웁니다. 그러므로 모든 열린(OPEN) 및 닫힌(CLOSED) rowgroup을 압축하는 경우 몇몇 행만 포함한 압축된 rowgroup이 손실됩니다. rowgroup을 채우면서도 압축된 크기를 가능하면 줄이고 쿼리 성능을 개선하기를 원할 것입니다.  
  
```sql  
-- Uses AdventureWorksDW2016  
-- Move all OPEN and CLOSED delta rowgroups into the columnstore.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
-- For a specific partition, move all OPEN AND CLOSED delta rowgroups into the columnstore  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="d-defragment-a-columnstore-index-online"></a>4. 온라인에서 columnstore 인덱스를 조각 모음  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에는 적용되지 않습니다.  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 REORGANIZE는 델타 rowgroup을 columnstore으로 압축하는 것 이상의 작업을 수행합니다. 또한 온라인 조각 모음도 수행합니다. 먼저, rowgroup 행 수의 10% 이상이 삭제된 경우 삭제된 행을 물리적으로 제거하여 columnstore의 크기를 줄입니다.  그런 다음, rowgroup들을 함께 결합하여 rowgroup당 최대 1,024,576개의 행을 포함하는 더 큰 rowgroup을 형성합니다.  변경된 모든 rowgroup은 다시 압축됩니다.  
  
> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 REORGANIZE가 삭제된 행을 물리적으로 제거하고 rowgroup을 병합하므로 columnstore 인덱스 다시 작성은 더 이상 필요하지 않습니다. COMPRESS_ALL_ROW_GROUPS 옵션은 모든 열린(OPEN) 또는 닫힌(CLOSED) 델타 rowgroup을 columnstore으로 강제 적용하며, 이전에 이 기능은 다시 작성으로만 수행할 수 있었습니다. REORGANIZE는 온라인으로 배경에서 수행되므로 쿼리는 작업이 이루어지는 동안 계속할 수 있습니다.  
  
```sql  
-- Uses AdventureWorks  
-- Defragment by physically removing rows that have been logically deleted from the table, and merging rowgroups.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
```  
  
### <a name="e-rebuild-a-clustered-columnstore-index-offline"></a>5. 오프라인으로 클러스터형 columnstore 인덱스 다시 작성  
적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터)   
  
> [!TIP]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서, 그리고 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]부터 ALTER INDEX REBUILD 대신에 ALTER INDEX REORGANIZE를 사용할 것을 권장합니다.  
  
> [!NOTE]
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 REORGANIZE는 닫힌(CLOSED) rowgroup을 columnstore으로 압축하기 위해서만 사용됩니다. 조각 모음 작업을 수행하고 모든 델타 rowgroup을 columnstore으로 강제 적용하는 유일한 방법은 인덱스를 다시 작성하는 것뿐입니다.  
  
 이 예제에서는 클러스터형 columnstore 인덱스를 다시 작성하고 모든 델타 rowgroup을 columnstore으로 강제 적용하는 방법을 보여줍니다. 첫 단계에서는 클러스터형 columnstore 인덱스가 있는 FactInternetSales2 테이블을 준비하고 첫 번째 네 열에서 데이터를 삽입합니다.  
  
```sql  
-- Uses AdventureWorksDW  
  
CREATE TABLE dbo.FactInternetSales2 (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_FactInternetSales2  
ON dbo.FactInternetSales2;  
  
INSERT INTO dbo.FactInternetSales2  
SELECT ProductKey, OrderDateKey, DueDateKey, ShipDateKey  
FROM dbo.FactInternetSales;  
  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 결과는 열린(OPEN) rowgroup이 하나임을 보여 주며, 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 rowgroup을 닫고 데이터를 columnstore로 이동하기 전에 여러 행이 추가되도록 대기한다는 것을 의미합니다. 다음 명령문은 모든 행을 columnstore로 강제 적용하는 클러스터형 columnstore 인덱스를 다시 작성합니다.  
  
```sql  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 SELECT 문 결과는 행 그룹이 COMPRESSED임을 보여 주며 행 그룹의 열 세그먼트가 이제 압축되고 columnstore에 저장됨을 의미합니다.  
  
### <a name="f-rebuild-a-partition-of-a-clustered-columnstore-index-offline"></a>6. 오프라인으로 클러스터형 columnstore의 파티션 다시 작성  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터)  
 
 대규모 클러스터형 columnstore 인덱스의 파티션을 다시 작성하려면 파티션 옵션과 함께 ALTER INDEX REBUILD를 사용합니다. 이 예제에서는 파티션 12를 다시 작성합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 REBUILD를 REORGANIZE로 대체할 것을 권장합니다.  
  
```sql  
ALTER INDEX cci_fact3   
ON fact3  
REBUILD PARTITION = 12;  
```  
  
### <a name="g-change-a-clustered-columstore-index-to-use-archival-compression"></a>7. 클러스터형 columstore를 보관 압축을 사용하도록 변경  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에는 적용되지 않습니다.  
  
 COLUMNSTORE_ARCHIVE 데이터 압축 옵션을 사용하여 클러스터형 columstore 인덱스의 크기를 훨씬 더 줄이는 방법을 선택할 수 있습니다. 이 방법은 저렴한 저장소에 보관하려는 오래된 데이터에 실용적입니다. 일반적인 COLUMNSTORE 압축을 사용하면 압축 해제가 더 느려지므로 자주 액세스하지 않는 데이터에 대해서만 이 방법을 사용하는 것이 좋습니다.  
  
 다음 예에서는 보관 압축을 사용하기 위해 클러스터형 columnstore 인덱스를 다시 작성한 다음 보관 압축을 제거하는 방법을 보여 줍니다. 마지막 결과에서는 columnstore 압축만 사용합니다.  
  
```sql  
--Prepare the example by creating a table with a clustered columnstore index.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL  
);  
  
CREATE CLUSTERED INDEX cci_SimpleTable ON SimpleTable (ProductKey);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_SimpleTable  
ON SimpleTable  
WITH (DROP_EXISTING = ON);  
  
--Compress the table further by using archival compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE);  
  
--Remove the archive compression and only use columnstore compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE);  
GO  
```  
  
## <a name="examples-rowstore-indexes"></a>예제: rowstore 인덱스  
  
### <a name="a-rebuilding-an-index"></a>1. 인덱스 다시 작성  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Employee` 테이블의 단일 인덱스를 다시 작성합니다.  
  
```sql  
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;  
```  
  
### <a name="b-rebuilding-all-indexes-on-a-table-and-specifying-options"></a>2. 테이블의 모든 인덱스 다시 작성 및 옵션 지정  
 다음 예에서는 `ALL` 키워드를 지정합니다. 그러면 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 Production.Product 테이블과 연결된 모든 인덱스를 다시 작성합니다. 3개의 옵션이 지정됩니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);  
```  
  
다음 예에서는 낮은 우선 순위 잠금 옵션을 포함하여 ONLINE 옵션을 추가하고 행 압축 옵션을 추가합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH   
(  
    FILLFACTOR = 80,   
    SORT_IN_TEMPDB = ON,  
    STATISTICS_NORECOMPUTE = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, ABORT_AFTER_WAIT = BLOCKERS ) ),   
    DATA_COMPRESSION = ROW  
);  
```  
  
### <a name="c-reorganizing-an-index-with-lob-compaction"></a>3. 인덱스 다시 구성과 LOB 압축  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 단일 클러스터형 인덱스를 다시 구성합니다. 인덱스에 리프 수준의 LOB 데이터 형식이 포함되어 있으므로 해당 문은 큰 개체 데이터가 포함된 페이지도 모두 압축합니다. 기본값이 ON이므로 WITH(LOB_COMPACTION) 옵션은 지정하지 않아도 됩니다.  
  
```sql  
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION);  
```  
  
### <a name="d-setting-options-on-an-index"></a>4. 인덱스에 옵션 설정  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `AK_SalesOrderHeader_SalesOrderNumber` 인덱스에 몇 가지 옵션을 설정합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX AK_SalesOrderHeader_SalesOrderNumber ON  
    Sales.SalesOrderHeader  
SET (  
    STATISTICS_NORECOMPUTE = ON,  
    IGNORE_DUP_KEY = ON,  
    ALLOW_PAGE_LOCKS = ON  
    ) ;  
GO
```  
  
### <a name="e-disabling-an-index"></a>5. 인덱스 비활성화  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Employee` 테이블의 비클러스터형 인덱스를 비활성화합니다.  
  
```sql  
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```  
  
### <a name="f-disabling-constraints"></a>6. 제약 조건 비활성화  
 다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 PRIMARY KEY 인덱스를 비활성화하여 PRIMARY KEY 제약 조건을 비활성화합니다. 기본 테이블에 대한 FOREIGN KEY 제약 조건이 자동으로 비활성화되고 경고 메시지가 표시됩니다.  
  
```sql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;  
```  
  
결과 집합에서 다음과 같은 경고 메시지를 반환합니다.  
  
```  
Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'  
on table 'EmployeeDepartmentHistory' referencing table 'Department'  
was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
```  
  
### <a name="g-enabling-constraints"></a>7. 제약 조건 활성화  
 다음 예에서는 6번 예에서 비활성화된 PRIMARY KEY와 FOREIGN KEY 제약 조건을 활성화합니다.  
  
PRIMARY KEY 인덱스를 다시 작성하여 PRIMARY KEY 제약 조건이 활성화됩니다.  
  
```sql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;  
```  
  
그런 다음 FOREIGN KEY 제약 조건이 활성화됩니다.  
  
```sql  
ALTER TABLE HumanResources.EmployeeDepartmentHistory  
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;  
GO  
```  
  
### <a name="h-rebuilding-a-partitioned-index"></a>8. 분할된 인덱스 다시 작성  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 분할된 인덱스 `5`의 단일 파티션인 파티션 번호 `IX_TransactionHistory_TransactionDate`를 다시 작성합니다. 파티션 5가 온라인으로 다시 작성되고 낮은 우선 순위 잠금에 대한 10분 대기 시간이 인덱스 다시 작성 작업으로 획득된 모든 잠금에 개별적으로 적용됩니다. 이 시간 동안에는 인덱스 다시 작성을 완료하기 위한 잠금을 획득할 수 없으며, 다시 작성 작업 문이 중단됩니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
-- Verify the partitioned indexes.  
SELECT *  
FROM sys.dm_db_index_physical_stats (DB_ID(),OBJECT_ID(N'Production.TransactionHistory'), NULL , NULL, NULL);  
GO  
--Rebuild only partition 5.  
ALTER INDEX IX_TransactionHistory_TransactionDate  
ON Production.TransactionHistory  
REBUILD Partition = 5   
   WITH (ONLINE = ON (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 10 minutes, ABORT_AFTER_WAIT = SELF)));  
GO  
```  
  
### <a name="i-changing-the-compression-setting-of-an-index"></a>9. 인덱스의 압축 설정 변경  
 다음 예에서는 분할되지 않은 rowstore 테이블에 인덱스를 다시 작성합니다.  
  
```sql
ALTER INDEX IX_INDEX1   
ON T1  
REBUILD   
WITH (DATA_COMPRESSION = PAGE);  
GO  
```  
  
데이터 압축 예제를 더 보려면 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
 
### <a name="j-online-resumable-index-rebuild"></a>10. 온라인으로 다시 시작 가능한 인덱스 다시 작성

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

 다음 예제에서는 온라인 다시 시작 가능한 인덱스 다시 작성을 사용하는 방법을 보여줍니다. 

1. MAXDOP=1로 설정하고 온라인 인덱스 다시 작성을 다시 시작 가능한 작업으로 실행합니다.

   ```sql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, MAXDOP=1, RESUMABLE=ON) ;
   ```

2. 인덱스 작업이 일시 중지된 후 같은 명령을 다시 실행하면(위 참조) 인덱스 다시 작성 작업이 자동으로 다시 시작됩니다.

3. MAX_DURATION을 240분으로 설정하여 온라인 인덱스 다시 작성을 다시 시작 가능한 작업으로 실행합니다.

   ```sql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, RESUMABLE=ON, MAX_DURATION=240) ; 
   ```
4. 실행 중인 다시 시작 가능한 온라인 인덱스 다시 작성을 일시 중지합니다.

   ```sql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```   
5. MAXDOP에 대한 새 값을 4로 지정하여 다시 시작 가능한 작업으로 실행된 인덱스 다시 작성에 대해 온라인 인덱스 다시 작성을 다시 시작합니다.

   ```sql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP=4) ;
   ```
6. 다시 시작 가능한 것으로 실행된 인덱스 온라인 다시 작성에 대해 온라인 인덱스 다시 작성 작업을 다시 시작합니다. MAXDOP를 2로 설정하고, 다시 시작 가능한 것으로 실행 중인 인덱스의 실행 시간을 240분으로 실행하며, 잠금에 대해 차단된 인덱스의 경우 10분 대기하고 그 후에는 모든 블로커를 종료합니다. 

   ```sql
      ALTER INDEX test_idx on test_table  
         RESUME WITH (MAXDOP=2, MAX_DURATION= 240 MINUTES, 
         WAIT_AT_LOW_PRIORITY (MAX_DURATION=10, ABORT_AFTER_WAIT=BLOCKERS)) ;
   ```      
7. 실행 중이거나 일시 중지된 다시 시작 가능한 인덱스 다시 작성 작업을 중단합니다.

   ```sql
   ALTER INDEX test_idx on test_table ABORT ;
   ``` 
  
## <a name="see-also"></a>참고 항목  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [인덱스 및 제약 조건 비활성화](../../relational-databases/indexes/disable-indexes-and-constraints.md)   
 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [온라인으로 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)   
 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
