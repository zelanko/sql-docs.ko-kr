---
title: ALTER INDEX (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER INDEX
- ALTER_INDEX_TSQL
dev_langs:
- TSQL
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
ms.assetid: b796c829-ef3a-405c-a784-48286d4fb2b9
caps.latest.revision: 222
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bfe0bfe90cfb8a168fd2c87d662ba978c12a898e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-index-transact-sql"></a>ALTER INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  인덱스를 비활성화, 다시 작성 또는 다시 구성하거나 인덱스에 대한 옵션을 설정하여 기존 테이블 또는 뷰 인덱스(관계형 또는 XML)를 수정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and SQL Database
  
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
 인덱스의 이름입니다. 인덱스 이름은 테이블이나 뷰에서 고유해야 하지만 데이터베이스 내에서 고유할 필요는 없습니다. 인덱스 이름은의 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 ALL  
 인덱스 유형에 관계없이 테이블이나 뷰에 연결된 모든 인덱스를 지정합니다. ALL을 지정하면 하나 이상의 인덱스가 오프라인 또는 읽기 전용 파일 그룹에 있거나 지정한 작업이 하나 이상의 인덱스 유형에 대해 허용되지 않을 경우 해당 문이 실패합니다. 다음 표에서는 인덱스 작업과 허용되지 않는 인덱스 유형을 나열합니다.  
  
|이 작업에 ALL 키워드를 사용 하 여|테이블에 다음 인덱스가 하나 이상 있으면 실패함|  
|----------------------------------------|----------------------------------------|  
|REBUILD WITH ONLINE = ON|XML 인덱스<br /><br /> 공간 인덱스<br /><br /> Columnstore 인덱스: **적용 대상:** Azure SQL 데이터베이스 및 SQL Server (SQL Server 2012부터 시작)입니다.|  
|REBUILD PARTITION = *partition_number*|분할되지 않은 인덱스, XML 인덱스, 공간 인덱스 또는 비활성 인덱스|  
|REORGANIZE|ALLOW_PAGE_LOCKS가 OFF로 설정된 인덱스|  
|파티션 재구성 = *partition_number*|분할되지 않은 인덱스, XML 인덱스, 공간 인덱스 또는 비활성 인덱스|  
|IGNORE_DUP_KEY = ON|XML 인덱스<br /><br /> 공간 인덱스<br /><br /> Columnstore 인덱스: **적용 대상:** Azure SQL 데이터베이스 및 SQL Server (SQL Server 2012부터 시작)입니다.|  
|ONLINE = ON|XML 인덱스<br /><br /> 공간 인덱스<br /><br /> Columnstore 인덱스: **적용 대상:** Azure SQL 데이터베이스 및 SQL Server (SQL Server 2012부터 시작)입니다.|
| 다시 시작 가능한 = ON  | 지원 되지 않았으므로 인덱스 **모든** 키워드입니다. <br /><br /> **적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작 |   
  
> [!WARNING]
>  온라인으로 수행할 수 있는 인덱스 작업에 대 한 정보를 자세한 참조 [온라인 인덱스 작업에 대 한 지침이](../../relational-databases/indexes/guidelines-for-online-index-operations.md)합니다.

 ALL을 지정 파티션 = *partition_number*, 모든 인덱스가 정렬 되어야 합니다. 즉, 해당 파티션 함수를 기준으로 인덱스가 분할됩니다. 파티션에 포함 된 모두 사용 하 여 모든 파티션이 인덱스와 동일한 *partition_number* 다시 작성 하거나 다시 구성 합니다. 분할된 인덱스에 대한 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.  
  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이나 뷰가 속한 스키마의 이름입니다.  
  
 *table_or_view_name*  
 인덱스와 관련된 테이블이나 뷰의 이름입니다. 개체에 있는 인덱스의 보고서를 표시 하려면 사용 된 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰.  
  
 SQL 데이터베이스는 세 부분으로 된 이름 형식 database_name을 지원합니다. [schema_name].table_or_view_name database_name이 현재 데이터베이스 또는 database_name이 tempdb 및 고 table_or_view_name이 #로 시작 합니다.  
  
 REBUILD [WITH **(**\<rebuild_index_option > [ **,**... *n*]**)** ]  
 동일한 열, 인덱스 유형, 고유성 특성 및 정렬 순서를 사용하여 인덱스가 다시 작성되도록 지정합니다. 이 절은 [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)합니다. REBUILD는 비활성 인덱스를 활성화합니다. ALL 키워드를 지정하지 않으면 클러스터형 인덱스를 다시 작성해도 관련 비클러스터형 인덱스는 다시 작성되지 않습니다. 기존 인덱스 옵션에 저장 된 값이 인덱스 옵션이 지정 되지 않은 경우 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 적용 됩니다. 인덱스 옵션 값에 저장 되지 않으므로 **sys.indexes**, 옵션의 인수 정의에 표시 된 기본값이 적용 됩니다.  
  
 ALL을 지정한 경우 기본 테이블이 힙이면 다시 작성 작업을 수행해도 테이블에는 아무 영향이 없습니다. 테이블에 연결된 비클러스터형 인덱스는 모두 다시 작성됩니다.  
  
 데이터베이스 복구 모델이 대량 로그 또는 단순으로 설정되어 있으면 다시 작성 작업이 최소한으로 기록될 수 있습니다.  
  
> [!NOTE]
>  기본 XML 인덱스를 다시 작성할 때는 인덱스 작업 중에 기본 사용자 테이블을 사용할 수 없습니다.  
  
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2012부터 시작)입니다.
  
 Columnstore 인덱스 다시 작성 작업:  
  
1.  정렬 순서를 사용 하지 않습니다.  
  
2.  다시 작성 작업이 발생한 동안 테이블 또는 파티션에서 배타적 잠금을 획득합니다.  NOLOCK, RCSI 또는 SI를 사용하는 경우에도 다시 작성 중에 데이터는 “오프라인”이며 사용할 수 없습니다.  
  
3.  모든 데이터를 columnstore로 다시 압축합니다. 다시 작성 작업이 발생한 동안에는 columnstore 인덱스의 두 복사본이 존재합니다. 다시 작성 작업이 끝나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 원래 columnstore 인덱스를 삭제합니다.  
  
 Columnstore 인덱스를 다시 작성 하는 방법에 대 한 자세한 내용은 참조 [Columnstore 인덱스 조각 모음](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
PARTITION  

**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.  
  
 인덱스의 한 파티션만 다시 작성하거나 다시 구성하도록 지정합니다. 경우에 파티션을 지정할 수 없습니다 *index_name* 분할 된 인덱스가 아닙니다.  
  
 PARTITION = ALL은 모든 파티션을 다시 작성합니다.  
  
> [!WARNING]
>  파티션 수가 1,000개를 초과하는 테이블에서 정렬되지 않은 인덱스를 만들거나 다시 작성할 수 있지만 해당 인덱스는 지원되지 않습니다. 그러면 작업 중에 성능이 저하되거나 메모리가 과도하게 소비될 수 있습니다. 파티션 수가 1,000개를 초과하는 경우에는 정렬된 인덱스만 사용하는 것이 좋습니다.  
  
 *partition_number*  
   
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.
  
 다시 작성하거나 다시 구성할 분할된 인덱스의 파티션 번호입니다. *partition_number* 변수를 참조할 수 있는 상수 식입니다. 여기에는 사용자 정의 형식 변수 또는 함수와 사용자 정의 함수가 포함될 수 있지만 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 참조할 수 없습니다. *partition_number* 있어야 또는 문이 실패 합니다.  
  
 와 **(**\<single_partition_rebuild_index_option >**)**  
   
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.  
  
 SORT_IN_TEMPDB, MAXDOP 및 DATA_COMPRESSION은 단일 파티션을 다시 작성할 때 지정할 수 있는 옵션 (파티션 =  *n* ). 단일 파티션 다시 작성 작업에는 XML 인덱스를 지정할 수 없습니다.  
  
 DISABLE  
 인덱스를 비활성 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 사용할 수 없음으로 표시합니다. 모든 인덱스를 비활성화할 수 있습니다. 비활성 인덱스의 인덱스 정의는 기본 인덱스 데이터 없이 시스템 카탈로그에 유지됩니다. 클러스터형 인덱스를 비활성화하면 사용자가 기본 테이블 데이터에 액세스하지 못합니다. 인덱스를 활성화하려면 ALTER INDEX REBUILD 또는 CREATE INDEX WITH DROP_EXISTING을 사용합니다. 자세한 내용은 참조 [사용 하지 않도록 설정 하는 인덱스 및 제약 조건](../../relational-databases/indexes/disable-indexes-and-constraints.md) 및 [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md)합니다.  
  
 Rowstore 인덱스를 다시 구성  
 Rowstore 인덱스에 대 한 REORGANIZE 인덱스 리프 수준이 다시 구성 하도록 지정 합니다.  인덱스 다시 구성 작업은 합니다.  
  
-   항상 온라인으로 수행 합니다. 즉, 장기간 차단 테이블 잠금이 유지되지 않으며 ALTER INDEX REORGANIZE 트랜잭션 중 기본 테이블에 대한 쿼리나 업데이트를 계속할 수 있습니다.  
  
-   비활성화 된 인덱스에 사용할 수 없습니다.  
  
-   ALLOW_PAGE_LOCKS가 OFF로 설정 하는 경우 사용할 수 없습니다.  
  
-   트랜잭션 내에서 수행 하는 것은 트랜잭션이 롤백될 때에 다시 롤백되지 않습니다.  
  
REORGANIZE와 **(** LOB_COMPACTION = { **ON** | OFF} **)**  
 Rowstore 인덱스에 적용 됩니다.  
  
LOB_COMPACTION = ON  
  
-   이러한 큰 개체 (LOB) 데이터 형식의 데이터가 포함 된 모든 페이지를 압축 하도록 지정: 이미지, 텍스트, ntext, varchar (max), nvarchar (max), varbinary (max), 및 xml입니다. 이 데이터를 압축 하면 데이터 디스크의 크기를 줄일 수 있습니다.  
  
-   클러스터형된 인덱스에 대 한 테이블에 포함 된 모든 LOB 열이 압축이 있습니다.  
  
-   비클러스터형 인덱스에 대 한 인덱스의 키가 아닌 (포괄된) 열인 모든 LOB 열을 압축이 됩니다.  
  
-   모두 다시 구성 LOB_COMPACTION 모든 인덱스에 대해 수행합니다. 각 인덱스에 대 한 클러스터형된 인덱스, 기본 테이블 또는 비클러스터형된 인덱스에 포괄된 열에 모든 LOB 열이 압축이 있습니다.  
  
LOB_COMPACTION = OFF  
  
-   큰 개체 데이터가 포함된 페이지가 압축되지 않습니다.  
  
-   OFF를 지정해도 힙에는 아무 영향이 없습니다.  
  
Columnstore 인덱스 다시 구성  
REORGANIZE는 온라인 상태로 수행 됩니다.  
  
Columnstore 인덱스에 대 한 REORGANIZE는 columnstore에 각 닫힌된 델타 행 그룹 압축 된 행 그룹으로 압축합니다.  
  
-   REORGANIZE는 압축 된 행 그룹으로 닫힌된 델타 행 그룹을 이동 하기 위해 필요 하지 않습니다. 백그라운드 튜플 이동 기 (TM) 프로세스 정기적으로 닫힌된 델타 행 그룹을 압축 합니다. 튜플 이동 기 지연 하는 경우에 REORGANIZE를 사용 하는 것이 좋습니다. REORGANIZE rowgroup 더 적극적으로 압축할 수 있습니다.  
  
-   모든 열기 및 CLOSED 행 그룹을 압축 하려면이 섹션에서는 다시 구성 된 (COMPRESS_ALL_ROW_GROUPS) 옵션을 참조 하십시오.  
  
REORGANIZE는 columnstore 인덱스의 SQL Server (2016부터 시작) 및 SQL 데이터베이스의 경우 다음과 같은 추가 조각 모음 최적화 온라인 수행:  
  
-   행 중 10% 이상을 논리적으로 삭제 된 행 그룹에서 행을 물리적으로 제거 합니다. 삭제 된 바이트는 물리적 미디어에서 회수 됩니다. 예를 들어 1 백만 행의 압축 된 행 그룹에는 삭제 100, 000 행이 SQL Server는 삭제 된 행 제거를 900 k 행이 포함 된 행 그룹을 다시 압축 합니다. 삭제 된 행을 제거 하 여 저장소에 저장 합니다.  
  
-   행 그룹당 최대 1,024,576 행을 높이기 위해 하나 이상의 압축 된 rowgroup을 결합 합니다. 예를 들어 대량으로 가져오면 5 수가 102, 400 행 일괄 처리 하는 경우 5 압축 된 행 그룹에 발생 합니다. REORGANIZE를 실행 하는 경우 해당 행이 그룹 크기 512,000 행 1 압축된 행 그룹으로 병합 되지 됩니다. 사전이 없습니다 크기나 메모리 제한 된 가정 합니다.  
  
-   행 중 10% 이상이 있는 논리적으로 삭제 된 행 그룹, SQL Server는이 행 그룹 하나 이상의 rowgroup으로 결합 하려고 합니다.    예를 들어 500, 000 행을 사용 하 여 압축 행 그룹 1 및 21 그룹이 compressed 임을 1048576 행의 최대 합니다.  행 그룹 21 409,830 행 생략 삭제 된 행의 60%에 있습니다. SQL Server 우선으로 이러한 두 909,830 행이 새 행 그룹을 압축 rowgroup을 결합 합니다.  
  
다시 구성 (COMPRESS_ALL_ROW_GROUPS = {ON | **OFF** })  
 SQL Server (2016부터 시작) 및 SQL 데이터베이스의 경우에 COMPRESS_ALL_ROW_GROUPS OPEN 또는 CLOSED 델타 행 그룹을 columnstore로 강제 하는 방법을 제공 합니다. 이 옵션을 델타 행 그룹 비워지도록 columnstore 인덱스 다시 작성 하는 데 필요한있지 않습니다.  이 함께 다른 제거 및 병합 조각 모음 기능을 통해 더 이상 트랜젹션 대부분의 경우에서 인덱스를 다시 작성 됩니다.    
-   ON 크기와 상태 (닫혀 있지 않거나 열)에 관계 없이 columnstore로 모든 rowgroup을 강제로 수행 합니다.  
  
-   OFF 모든 CLOSED 행 그룹이 columnstore로 강제로 수행합니다.  
  
설정 **(** \<set_index 옵션 > [ **,**... *n*] **)**  
 인덱스를 다시 작성하거나 다시 구성하지 않고 인덱스 옵션을 지정합니다. 비활성 인덱스에는 SET을 지정할 수 없습니다.  
  
PAD_INDEX = { ON | OFF }  
   
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.  
  
 인덱스 패딩을 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 FILLFACTOR로 지정된 사용 가능한 공간의 비율이 인덱스의 중간 수준 페이지에 적용됩니다. 채우기 비율에 저장 된 값이 동시에 PAD_INDEX를 ON으로 설정 되어 FILLFACTOR를 지정 하지 않으면, [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 사용 됩니다.  
  
 OFF 또는 *fillfactor* 지정 하지 않으면  
 중간 수준 페이지는 용량 한도 가까이 채워집니다. 이로 인해 중간 페이지의 키 집합을 기준으로 인덱스에 포함될 수 있는 최대 크기의 행 하나 이상을 위한 충분한 공간이 남겨집니다.  
  
 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
FILLFACTOR = *fillfactor*  
 
 **적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.
  
 인덱스를 만들거나 변경할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. *fillfactor* 100 1 까지의 정수 값 이어야 합니다. 기본값은 0입니다. 채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
 명시적 FILLFACTOR 설정은 인덱스를 처음 만들거나 다시 작성할 때만 적용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 페이지에 지정된 비율의 빈 공간을 동적으로 유지하지 않습니다. 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
 채우기 비율 설정을 보려면 **sys.indexes**합니다.  
  
> [!IMPORTANT]
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 클러스터형 인덱스를 만들 때 데이터를 다시 배포하므로 FILLFACTOR  값으로 클러스터형 인덱스를 만들거나 변경하면 데이터가 차지하는 저장 공간 크기에 영향이 미칩니다.  
  
 SORT_IN_TEMPDB = {ON | **OFF** }  
 

**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.  
  
 에 정렬 결과 저장할지 여부를 지정 **tempdb**합니다. 기본값은 OFF입니다.  
  
 ON  
 인덱스를 작성 하는 데 사용 되는 중간 정렬 결과에 저장 됩니다 **tempdb**합니다. 경우 **tempdb** 은 다른는 사용자 데이터베이스는 디스크 집합에 인덱스를 만드는 데 필요한 시간이 줄어들 수 있습니다. 그러나 인덱스 작성 중에 사용되는 디스크 공간의 크기는 커집니다.  
  
 OFF  
 중간 정렬 결과가 인덱스와 같은 데이터베이스에 저장됩니다.  
  
 정렬 작업이 필요하지 않거나 메모리에서 정렬을 수행할 수 있으면 SORT_IN_TEMPDB 옵션이 무시됩니다.  
  
 자세한 내용은 참조 [인덱스에 대 한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)합니다.  
  
 IGNORE_DUP_KEY  **=**  {ON | OFF}  
 삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려는 경우에 대한 오류 응답을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. 기본값은 OFF입니다.  
  
 ON  
 중복된 키 값이 고유 인덱스에 삽입되는 경우 경고 메시지가 나타나고 고유성 제약 조건을 위반하는 행만 실패합니다.  
  
 OFF  
 중복된 키 값이 고유 인덱스에 삽입되는 경우 오류 메시지가 나타나고 전체 INSERT 작업이 롤백됩니다.  
  
 뷰에 생성 된 인덱스, 고유 하지 않은 인덱스, XML 인덱스, 공간 인덱스 및 필터링 된 인덱스에 대 한 IGNORE_DUP_KEY는 ON으로 설정할 수 없습니다.  
  
 IGNORE_DUP_KEY를 보려면 사용 하 여 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.  
  
 이전 버전과 호환되는 구문에서 WITH IGNORE_DUP_KEY는 WITH IGNORE_DUP_KEY = ON과 같습니다.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | OFF}  
 배포 통계를 다시 계산할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 이전 통계가 자동으로 다시 계산되지 않습니다.  
  
 OFF  
 자동 통계 업데이트가 설정됩니다.  
  
 자동 통계 업데이트를 복원하려면 STATISTICS_NORECOMPUTE를 OFF로 설정하거나 NORECOMPUTE 절 없이 UPDATE STATISTICS를 실행합니다.  
  
> [!IMPORTANT]
>  배포 통계 자동 재계산 기능을 해제하면 쿼리 최적화 프로그램에서 테이블과 관련된 쿼리에 대해 최적의 실행 계획을 선택할 수 없습니다.  
  
 STATISTICS_INCREMENTAL = {ON | **OFF** }  
 때 **ON**, 파티션 통계 별로 통계가 작성 됩니다. 때 **OFF**, 통계 트리가 삭제 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계를 다시 계산 합니다. 기본값은 **OFF**합니다.  
  
 파티션별 통계가 지원되지 않는 경우에는 이 옵션이 무시되고 경고가 생성됩니다. 다음 통계 유형에 대해서는 증분 통계가 지원되지 않습니다.  
  
-   기본 테이블을 기준으로 파티션 정렬되지 않은 인덱스를 사용하여 작성된 통계입니다.  
  
-   Always On 읽기 가능한 보조 데이터베이스에 대해 작성된 통계입니다.  
  
-   읽기 전용 데이터베이스에 대해 작성된 통계입니다.  
  
-   필터링된 인덱스에 대해 작성된 통계입니다.  
  
-   뷰에 대해 작성된 통계입니다.  
  
-   내부 테이블에 대해 작성된 통계입니다.  
  
-   공간 인덱스 또는 XML 인덱스를 사용하여 작성된 통계입니다.  
  
 
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2014부터 시작)입니다.  
  
 온라인  **=**  {ON | **OFF** } \<rebuild_index_option에 적용 >  
 인덱스 작업 중 쿼리 및 데이터 수정에 기본 테이블과 관련 인덱스를 사용할 수 있는지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 XML 인덱스 또는 공간 인덱스의 경우 ONLINE = OFF만 지원되며 ONLINE을 ON으로 설정하면 오류가 발생합니다.  
  
> [!NOTE]
>  온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ON  
 인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 작업의 주 단계 중 내재된 공유(IS) 잠금만 원본 테이블에 유지됩니다. 따라서 기본 테이블 및 인덱스를 계속 쿼리 또는 업데이트할 수 있습니다. 작업이 시작될 때 아주 짧은 기간 동안 S(공유) 잠금이 원본 개체에서 유지됩니다. 작업이 끝날 때 짧은 기간 동안 비클러스터형 인덱스가 생성되는 경우에는 원본에 대해 S(공유) 잠금이 유지되고, 온라인 상태에서 클러스터형 인덱스가 생성 또는 삭제될 때나 클러스터형 또는 비클러스터형 인덱스가 다시 작성될 때는 SCH-M(스키마 수정) 잠금이 획득됩니다. 로컬 임시 테이블에서 인덱스를 생성하는 경우에는 ONLINE을 ON으로 설정할 수 없습니다.  
  
 OFF  
 인덱스 작업 중에 테이블 잠금이 적용됩니다. 클러스터형 인덱스, 공간 인덱스 또는 XML 인덱스를 생성, 다시 작성 또는 삭제하거나 비클러스터형 인덱스를 다시 작성 또는 삭제하는 오프라인 인덱스 작업은 테이블에 대해 SCH-M(스키마 수정) 잠금을 획득합니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다. 비클러스터형 인덱스를 만드는 오프라인 인덱스 작업을 통해 테이블의 S(공유) 잠금을 획득합니다. 따라서 기본 테이블을 업데이트할 수 없지만 SELECT 문과 같은 읽기 작업은 허용됩니다.  
  
 자세한 내용은 참조 [어떻게 온라인 인덱스 작동](../../relational-databases/indexes/how-online-index-operations-work.md)합니다.  
  
 전역 임시 테이블의 인덱스를 비롯한 인덱스를 온라인으로 다시 작성할 수 있습니다. 단, 다음 항목은 예외입니다.  
  
-   XML 인덱스  
  
-   로컬 임시 테이블의 인덱스  
  
-   분할된 인덱스의 하위 집합(분할된 전체 인덱스를 온라인으로 다시 작성할 수 있음)  

-  SQL 데이터베이스 V12, 이전 버전 및 SQL Server 2012 이전의 SQL Server를 허용 하지 않습니다는 `ONLINE` 클러스터형된 인덱스 작성에 대 한 다시 실행 하거나 기본 테이블을 포함 하는 경우 작업을 다시 작성 **varchar (max)** 또는 **varbinary (max)**  열입니다.

다시 시작 가능한  **=**  {ON | **OFF**}

**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작  

 온라인 인덱스 작업은 다시 시작할 수 있는지 여부를 지정 합니다.

 인덱스 작업은 다시 시작할 수 없습니다.

 인덱스 해제 작업을 다시 시작할 수 없습니다.

MAX_DURATION  **=**  *시간* [**분**] 사용한 **다시 시작 가능 = ON** (필요 **에ONLINE=**).
 
**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작  

시간을 나타냅니다 (분 단위로 지정 된 정수 값)를 다시 시작 가능한 온라인 인덱스 작업을 일시 중지 하기 전에 실행 됩니다. 

ALLOW_ROW_LOCKS  **=**  { **ON** | OFF}  
 
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.  
  
 행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 행 잠금이 사용되지 않습니다.  
  
ALLOW_PAGE_LOCKS  **=**  { **ON** | OFF}  
  
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.
  
 페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 페이지 잠금이 사용되지 않습니다.  
  
> [!NOTE]
>  ALLOW_PAGE_LOCKS가 OFF로 설정되면 인덱스를 다시 구성할 수 없습니다.  
  
 MAXDOP  **=**  max_degree_of_parallelism  
 
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.  
  
 재정의 **x degree of** 인덱스 작업의 기간에 대 한 구성 옵션입니다. 자세한 내용은 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
> [!IMPORTANT]
>  MAXDOP 옵션은 모든 XML 인덱스에 대해 구문으로는 지원되지만 공간 인덱스 또는 기본 XML 인덱스의 경우 ALTER INDEX는 현재 단일 프로세서만 사용합니다.  
  
 *max_degree_of_parallelism* 될 수 있습니다.  
  
 1.  
 병렬 계획이 생성되지 않습니다.  
  
 \>1  
 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 지정된 값으로 제한합니다.  
  
 0(기본값)  
 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]
>  병렬 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 COMPRESSION_DELAY  **=**  { **0** |*기간 [분]* }  
 이 기능은 SQL Server 2016부터 사용할 수  
  
 디스크 기반 테이블에 대 한 지연 SQL Server는 압축 된 행 그룹으로 압축할 수 전에 델타 행 그룹에 델타 행 그룹을 CLOSED 상태에서 유지 되어야 하는 시간 (분)의 최소 수를 지정 합니다. 디스크 기반 테이블에서 insert를 관리 하 고 업데이트할 하지 이후 시간에 개별 행을 SQL Server에 적용 됩니다 지연 CLOSED 상태에서 델타 행 그룹입니다.  
기본값은 0 분입니다.  
  
 기본값은 0 분입니다.  
  
 에 대 한 권장 시기 COMPRESSION_DELAY 실시간 운영 분석을 위한 Columnstore 인덱스를 참조 하십시오.  
  
 DATA_COMPRESSION  
 지정된 인덱스, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.  
  
 없음  
 인덱스 또는 지정된 파티션이 압축되지 않습니다. columnstore 인덱스에는 적용되지 않습니다.  
  
 ROW  
 인덱스 또는 지정된 파티션이 행 압축을 사용하여 압축됩니다. columnstore 인덱스에는 적용되지 않습니다.  
  
 PAGE  
 인덱스 또는 지정된 파티션이 페이지 압축을 사용하여 압축됩니다. columnstore 인덱스에는 적용되지 않습니다.  
  
 COLUMNSTORE  
   
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2014부터 시작)입니다.
  
 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE에서는 COLUMNSTORE_ARCHIVE 옵션으로 압축된 지정 파티션 또는 인덱스를 압축 해제하도록 지정합니다. 데이터는 복구될 때 모든 columnstore 인덱스에 사용된 columnstore 압축으로 계속 압축됩니다.  
  
 COLUMNSTORE_ARCHIVE  
  
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2014부터 시작)입니다.
  
 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE_ARCHIVE는 지정된 파티션을 보다 작은 크기로 압축합니다. 보다 적은 저장소 크기가 필요한 기타 상황에서 보관하는 데 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
 압축에 대 한 자세한 내용은 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
 ON PARTITIONS **(** { \<partition_number_expression > | \<범위 >} [**,**… n] **)**  
    
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다. 
  
 DATA_COMPRESSION 설정을 적용할 파티션을 지정합니다. 인덱스가 분할되지 않은 경우 ON PARTITIONS 인수를 사용하면 오류가 발생합니다. ON PARTITIONS 절을 제공하지 않으면 DATA_COMPRESSION 옵션이 분할된 인덱스의 모든 파티션에 적용됩니다.  
  
 \<partition_number_expression > 다음과 같은 방법으로 지정할 수 있습니다.  
  
-   파티션의 번호를 지정합니다(예: ON PARTITIONS (2)).  
  
-   여러 개별 파티션의 파티션 번호를 쉼표로 구분하여 지정합니다(예: ON PARTITIONS (1,5)).  
  
-   범위와 개별 파티션을 모두 지정합니다(ON PARTITIONS (2,4,6 TO 8)).  
  
 \<범위 > 예를 들어, TO로 구분 된 파티션 번호로 지정할 수 있습니다: ON PARTITIONS (6 TO 8)).  
  
 여러 파티션에 대해 서로 다른 데이터 압축 유형을 설정하려면 DATA_COMPRESSION 옵션을 두 번 이상 지정합니다. 예를 들면 다음과 같습니다.  
  
```tsql  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
 온라인  **=**  {ON | **OFF** } \<single_partition_rebuild_index_option에 적용 >  
 여부 인덱스 또는 테이블의 인덱스 파티션을 다시 작성할 수 있습니다 온라인 또는 오프 라인으로 지정 합니다. 경우 **다시 작성** 온라인으로 수행 됨 (**ON**)이이 테이블의 데이터를 인덱스 작업 중 쿼리 및 데이터 수정을 위해 사용할 수 있습니다.  기본값은 **OFF**합니다.  
  
 ON  
 인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 작업의 주 단계 중 내재된 공유(IS) 잠금만 원본 테이블에 유지됩니다. 인덱스 다시 작성 하 고 온라인 인덱스 다시 작성의 끝에 있는 테이블에 대 한 Sch-m 잠금을의 시작 부분에는 테이블에 대 한 S-잠금이 필요 합니다. 두 잠금 모두 짧은 메타데이터 잠금이지만 특히 Sch-M 잠금은 모든 차단 트랜잭션이 완료될 때까지 기다려야 합니다. 대기 시간 동안 Sch-M 잠금은 동일 테이블에 액세스할 때 이 잠금 뒤에서 기다리는 다른 모든 트랜잭션을 차단합니다.  
  
> [!NOTE]
>  온라인 인덱스 다시 작성을 설정할 수는 *low_priority_lock_wait* 이 단원의 뒷부분에서 설명 하는 옵션입니다.  
  
 OFF  
 인덱스 작업 중에 테이블 잠금이 적용됩니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다.  
  
 WAIT_AT_LOW_PRIORITY 사용한 **ONLINE = ON** 만 합니다.  
 
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2014부터 시작)입니다.
  
 온라인 인덱스 다시 작성에서 이 테이블의 차단 작업을 대기해야 합니다. **WAIT_AT_LOW_PRIORITY** 온라인 인덱스 다시 작성 작업은 다른 작업을 온라인 인덱스 작성 작업을 대기 하는 동안 진행할 수 있도록 하는 낮은 우선 순위 잠금을 대기 함을 나타냅니다. 생략 된 **WAIT AT LOW PRIORITY** 옵션은 `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`합니다. 자세한 내용은 참조 [WAIT_AT_LOW_PRIORITY](https://msdn.microsoft.com/library/ms188388.aspx)합니다. 
  
 MAX_DURATION = *시간* [**분**]  
  
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2014부터 시작)입니다.
  
 DDL 명령을 실행할 때 온라인 인덱스 다시 작성 잠금이 낮은 우선 순위로 대기하는 시간(분 단위로 지정된 정수 값)입니다. 작업에 대 한 차단 된 경우는 **MAX_DURATION** 시간 중 하나는 **ABORT_AFTER_WAIT** 작업 실행 됩니다. **MAX_DURATION** 시간은 항상 분 단위 이며 단어 **분** 생략할 수 있습니다.  
 
 ABORT_AFTER_WAIT = [**NONE** | **자체** | **블로 커가** }]  
   
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2014부터 시작)입니다.
  
 없음  
 보통(일반) 우선 순위로 잠금을 계속 대기합니다.  
  
 SELF  
 어떤 동작도 수행하지 않고 현재 실행 중인 온라인 인덱스 다시 작성 DDL 작업을 종료합니다.  
  
 BLOCKERS  
 작업을 계속할 수 있도록 온라인 인덱스 다시 작성 DDL 작업을 차단하는 모든 사용자 트랜잭션을 종료합니다. **블로 커가** 옵션을 사용 하려면 로그인이 가지 **ALTER ANY CONNECTION** 권한.  
 
 RESUME 
 
**적용 대상**: SQL Server 2017 (기능은 공개 미리 보기 상태에서)로 시작

수동으로 또는 오류로 인해 일시 중지 하는 인덱스 작업을 다시 시작 합니다.

MAX_DURATION 사용한 **다시 시작 가능 = ON**

 
**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작

시간 (분 단위로 지정 된 정수 값) 다시 시작 후 다시 시작 가능한 온라인 인덱스 작업이 실행 됩니다. 이 시간이 만료 되 면 여전히 실행 되는 경우 다시 시작 될 작업을 일시 중지 됩니다.

WAIT_AT_LOW_PRIORITY 사용한 **다시 시작 가능 = ON** 및 **ONLINE = ON**합니다.  
  
**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작
  
 이 테이블에 대 한 차단 작업을 대기 하는 일시 중지 한 후 온라인 인덱스 다시 작성을 다시 시작 합니다. **WAIT_AT_LOW_PRIORITY** 온라인 인덱스 다시 작성 작업은 다른 작업을 온라인 인덱스 작성 작업을 대기 하는 동안 진행할 수 있도록 하는 낮은 우선 순위 잠금을 대기 함을 나타냅니다. 생략 된 **WAIT AT LOW PRIORITY** 옵션은 `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`합니다. 자세한 내용은 참조 [WAIT_AT_LOW_PRIORITY](https://msdn.microsoft.com/library/ms188388.aspx)합니다. 


일시 중지
 
**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작
  
다시 시작 가능한 온라인 인덱스 다시 작성 작업을 일시 중지 합니다.

중단

**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작   

다시 시작 가능 상태로 선언 된 실행 중이거나 일시 중지 된 인덱스 작업을 중단 합니다. 명시적으로 실행 해야는 **중단** 명령이 종료 된 다시 시작 가능한 인덱스 다시 작성 작업 합니다. 오류 또는 다시 시작 가능한 인덱스 작업을 일시 중지;의 실행을 종료 하지 않습니다. 대신, 작업을 무기한 일시 중지 상태로 둡니다.
  
## <a name="remarks"></a>주의  
 인덱스를 다시 분할하거나 다른 파일 그룹으로 이동하는 데는 ALTER INDEX를 사용할 수 없습니다. 이 문을 사용하여 열 추가 또는 삭제, 열 순서 변경과 같은 인덱스 정의를 수정할 수 없습니다. 이러한 작업을 수행하려면 DROP_EXISTING 절에 CREATE INDEX를 사용하세요.  
  
 옵션을 명시적으로 지정하지 않으면 현재 설정이 적용됩니다. 예를 들어, REBUILD 절에 FILLFACTOR 설정을 지정하지 않으면 다시 작성하는 동안 시스템 카탈로그에 저장된 채우기 비율 값이 사용됩니다. 현재 인덱스 옵션 설정을 보려면 사용 하 여 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.  
  
> [!NOTE]
>  ONLINE, MAXDOP 및 SORT_IN_TEMPDB에 대한 값은 시스템 카탈로그에 저장되지 않습니다. 인덱스 문에서 지정하지 않으면 해당 옵션의 기본값이 사용됩니다.
  
 다중 프로세서 컴퓨터에서는 다른 쿼리의 경우와 마찬가지로 ALTER INDEX REBUILD가 자동으로 프로세서를 더 사용하여 인덱스 수정과 관련된 정렬 및 검색 작업을 수행합니다. 실행할 때 ALTER INDEX REORGANIZE를 LOB_COMPACTION을 유무는 **x degree of** 값은 단일 스레드 작업이 됩니다. 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
 인덱스가 위치한 파일 그룹이 오프라인이거나 읽기 전용으로 설정되어 있으면 인덱스를 다시 구성할 수 없습니다. ALL 키워드를 지정하면 하나 이상의 인덱스가 오프라인 또는 읽기 전용 파일 그룹에 있을 경우 해당 문이 실패합니다.  
  
## <a name="rebuilding-indexes"></a>인덱스 다시 작성  
 인덱스를 다시 작성하면 이 인덱스가 삭제된 다음 다시 생성됩니다. 이렇게 하면 조각화를 제거하고, 지정된 채우기 비율 또는 기존 채우기 비율 설정을 기준으로 페이지를 압축하여 디스크 공간을 회수하고, 인덱스 행을 연속된 페이지로 다시 정렬할 수 있습니다. ALL을 지정하면 테이블의 모든 인덱스가 단일 트랜잭션으로 삭제되고 다시 작성됩니다. FOREIGN KEY 제약 조건은 미리 삭제하지 않아도 됩니다. 익스텐트가 128개 이상인 인덱스를 다시 작성하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 실제 페이지 할당 취소와 해당 관련 잠금이 트랜잭션 커밋 후까지 지연됩니다.  
  
 작은 인덱스는 다시 작성하거나 다시 구성해도 조각화가 줄어들지 않는 경우가 많습니다. 작은 인덱스의 페이지는 종종 혼합 익스텐트에 저장됩니다. 혼합 익스텐트는 최대 8개의 개체가 공유할 수 있으므로 인덱스를 다시 작성하거나 다시 구성한 후에도 작은 인덱스의 조각화가 줄어들지 않을 수 있습니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 분할된 인덱스를 만들거나 다시 작성할 때 테이블의 모든 행을 검사하여 통계를 작성하지 않습니다. 대신 쿼리 최적화 프로그램에서 기본 샘플링 알고리즘을 사용하여 통계를 생성합니다. 테이블의 모든 행을 검사하여 분할된 인덱스에 대한 통계를 얻으려면 FULLSCAN 절에서 CREATE STATISTICS 또는 UPDATE STATISTICS를 사용합니다.  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 비클러스터형 인덱스를 다시 작성하여 하드웨어 오류로 인한 불일치를 해결할 수 있는 경우도 있습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상에서도 비클러스터형 인덱스를 오프라인으로 다시 작성하여 인덱스와 클러스터형 인덱스 간의 불일치를 복구할 수 있습니다. 그러나 인덱스를 온라인으로 다시 작성하는 경우에는 비클러스터형 인덱스 간의 불일치를 해결할 수 없습니다. 온라인으로 다시 작성하는 경우 기존의 비클러스터형 인덱스를 사용하므로 불일치가 계속 남아 있게 됩니다. 경우에 따라 오프라인으로 인덱스를 다시 작성하면 클러스터형 인덱스 검색 또는 힙 검색이 수행되어 불일치가 제거됩니다. 클러스터형된 인덱스에서 다시 작성되도록 하려면 비클러스터형 인덱스를 삭제한 후 다시 만드세요. 이전 버전의 경우처럼 영향을 받은 데이터를 백업한 후 복원하여 불일치를 제거하는 것이 좋습니다. 비클러스터형 인덱스의 경우에는 오프라인으로 인덱스를 다시 작성하여 인덱스 간 불일치를 해결할 수 있습니다. 자세한 내용은 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 참조하세요.  
  
 클러스터형 columnstore 인덱스를 다시 작성하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  다시 작성 작업이 발생한 동안 테이블 또는 파티션에서 배타적 잠금을 획득합니다. 다시 작성 중에 데이터는 “오프라인”이며 사용할 수 없습니다.  
  
2.  테이블에서 논리적으로 삭제된 행을 물리적으로 삭제하여 columnstore를 조각 모음합니다. 삭제된 바이트는 물리적 미디어에서 회수됩니다.  
  
3.  deltastore를 비롯하여 원래 columnstore 인덱스의 모든 데이터를 읽습니다. 데이터를 새 행 그룹으로 결합하고 행 그룹을 columnstore로 압축합니다.  
  
4.  다시 작성이 진행되는 동안 실제 미디어에 columnstore 인덱스의 사본을 두 개 저장할 공간이 필요합니다. 다시 작성 작업이 끝나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 원래 클러스터형 columnstore 인덱스를 삭제합니다.  
  
## <a name="reorganizing-indexes"></a>인덱스 다시 구성  
 인덱스를 다시 구성할 때는 최소한의 시스템 리소스가 사용됩니다. 이때는 왼쪽에서 오른쪽으로 표시되는 리프 노드의 논리적 순서에 맞도록 리프 수준 페이지를 물리적으로 다시 정렬하여 테이블 및 뷰의 클러스터형 및 비클러스터형 인덱스의 리프 수준에 대한 조각 모음을 수행합니다. 다시 구성 작업을 수행하면 인덱스 페이지도 압축됩니다. 이때 압축은 기존 채우기 비율 값을 기준으로 수행됩니다. 채우기 비율 설정을 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.  
  
 ALL을 지정하면 테이블에서 관계형 인덱스, 클러스터형 및 비클러스터형 모두와 XML 인덱스가 다시 구성됩니다. ALL을 지정할 때는 몇 가지 제한 사항이 적용됩니다. 자세한 내용은 인수 섹션에서 ALL에 대한 정의를 참조하세요.  
  
 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
## <a name="disabling-indexes"></a>인덱스 비활성화  
 인덱스를 비활성화하면 사용자가 인덱스에 액세스할 수 없으며 클러스터형 인덱스의 경우 기본 테이블 데이터에도 액세스할 수 없습니다. 인덱스 정의는 시스템 카탈로그에 유지됩니다. 뷰의 비클러스터형 인덱스 또는 클러스터형 인덱스를 비활성화하면 인덱스 데이터가 물리적으로 삭제됩니다. 클러스터형 인덱스를 비활성화하면 데이터에 액세스할 수 없지만 인덱스가 삭제되거나 다시 작성될 때까지는 데이터가 B-트리에서 유지 관리되지 않는 상태로 남아 있습니다. 활성 또는 비활성 인덱스의 상태를 확인 하려면 쿼리는 **is_disabled** 열에는 **sys.indexes** 카탈로그 뷰에 있습니다.  
  
 트랜잭션 복제 게시의 테이블에서는 기본 키 열과 연결된 인덱스를 해제할 수 없습니다. 이러한 인덱스는 복제에 필요합니다. 인덱스를 해제하려면 먼저 게시에서 테이블을 삭제해야 합니다. 자세한 내용은 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)를 참조하세요.  
  
 ALTER INDEX REBUILD 문 또는 CREATE INDEX WITH DROP_EXISTING 문을 사용하여 인덱스를 활성화할 수 있습니다. ONLINE 옵션이 ON으로 설정되어 있으면 비활성화된 클러스터형 인덱스를 다시 작성할 수 없습니다. 자세한 내용은 [인덱스 및 제약 조건 비활성화](../../relational-databases/indexes/disable-indexes-and-constraints.md)를 참조하세요.  
  
## <a name="setting-options"></a>옵션 설정  
 지정한 인덱스에 대해 해당 인덱스를 다시 작성하거나 다시 구성하지 않고 ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, IGNORE_DUP_KEY 및 STATISTICS_NORECOMPUTE 옵션을 설정할 수 있습니다. 수정된 값은 인덱스에 바로 적용됩니다. 이러한 설정을 보려면 사용 하 여 **sys.indexes**합니다. 자세한 내용은 [인덱스 옵션 설정](../../relational-databases/indexes/set-index-options.md)을 참조하세요.  
  
### <a name="row-and-page-locks-options"></a>행 및 페이지 잠금 옵션  
 ALLOW_ROW_LOCKS = ON이고 ALLOW_PAGE_LOCK = ON이면 인덱스에 액세스할 때 행 수준, 페이지 수준 및 테이블 수준 잠금이 허용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 적절한 잠금을 선택하고 행 또는 페이지 잠금에서 테이블 잠금으로 잠금을 에스컬레이션할 수 있습니다.  
  
 ALLOW_ROW_LOCKS = OFF이고 ALLOW_PAGE_LOCK = OFF이면 인덱스에 액세스할 때 테이블 수준 잠금만 허용됩니다.  
  
 행 또는 페이지 잠금 옵션이 설정된 경우 ALL을 지정하면 설정이 모든 인덱스에 적용됩니다. 기본 테이블이 힙인 경우 다음과 같은 방식으로 설정이 적용됩니다.  
  
|||  
|-|-|  
|ALLOW_ROW_LOCKS = ON 또는 OFF|힙 및 연결된 비클러스터형 인덱스|  
|ALLOW_PAGE_LOCKS = ON|힙 및 연결된 비클러스터형 인덱스|  
|ALLOW_PAGE_LOCKS = OFF|비클러스터형 인덱스 전체. 즉, 비클러스터형 인덱스에는 모든 페이지 잠금이 허용되지 않습니다. 힙에서는 페이지에 대한 공유(S), 업데이트(U) 및 배타(X) 잠금만 허용되지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 내부에서 사용하기 위해 의도 페이지 잠금(IS,  IU  또는 IX)을 획득할 수 있습니다.|  
  
## <a name="online-index-operations"></a>온라인 인덱스 작업  
 인덱스를 다시 작성할 때 ONLINE 옵션이 ON으로 설정되어 있으면 기본 개체, 테이블 및 연결된 인덱스를 쿼리와 데이터 수정에 사용할 수 있습니다. 단일 파티션에 있는 인덱스 부분을 온라인으로 다시 작성할 수도 있습니다. 변경 중에는 아주 잠시 동안만 배타적 테이블 잠금이 유지됩니다.  
  
 인덱스를 다시 구성하는 과정은 항상 온라인으로 수행됩니다. 이 프로세스는 잠금을 장기간 유지하지 않으므로 실행 중인 업데이트나 쿼리를 차단하지 않습니다.  
  
 다음을 수행할 때만 동일한 테이블 또는 테이블 파티션에서 동시 온라인 작업을 수행할 수 있습니다.  
  
-   여러 개의 비클러스터형 인덱스 생성  
  
-   동일한 테이블에서 여러 인덱스 다시 구성  
  
-   동일한 테이블에서 겹치지 않는 인덱스를 다시 작성하는 동안 여러 인덱스 다시 구성  
  
 동시에 수행된 다른 온라인 인덱스 작업이 모두 실패합니다. 예를 들어, 동일한 테이블에서 두 개 이상의 인덱스를 다시 작성할 수 없습니다. 또는 동일한 테이블에서 기존 인덱스를 다시 작성하면서 새 인덱스를 생성할 수 없습니다.  

### <a name="resumable-index-operations"></a>다시 시작 가능한 인덱스 작업

**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작

다시 시작 가능을 사용 하 여 다시 시작 가능으로 지정 된 온라인 인덱스 다시 작성 = ON 옵션입니다. 
-  다시 시작 가능한 옵션에 지정된 된 인덱스에 대 한 메타 데이터는 영구 저장소가 아니며 현재 DDL 문의 기간에만 적용 됩니다. 따라서 다시 시작 가능 = ON 절을 작업 재개를 사용 하도록 설정 하려면 명시적으로 지정 해야 합니다.

-  두 가지 MAX_DURATION 옵션 note 하십시오. 하나는 low_priority_lock_wait 관련이 다시 시작 가능 관련이 있으면 다른 = ON 옵션입니다.
   -  MAX_DURATION 옵션은 다시 시작 가능에 대 한 지원 = ON 옵션 또는 **low_priority_lock_wait** 인수 옵션입니다. 
   MAX_DURATION 다시 시작 가능한 옵션에 대 한 다시 작성 되 고 인덱스에 대 한 시간 간격을 지정 합니다. 이 현재 사용 되 면 인덱스 다시 작성은 일시 중지 되었거나 해당 실행을 완료 합니다. 사용자가 일시 중지 된 인덱스에 대 한 다시 빌드를 다시 시작할 수 있습니다. **시간** MAX_DURATION 분 0 분 보다 크거나 같은 1 주 (7 x 24 x 60 = 10080 분) 이어야 합니다. 발생 하는 인덱스 작업에 대 한 오래 지연 된 특정 테이블에 대 한 DML 성능에 영향을 줄 수 뿐만 아니라 모두 데이터베이스 디스크 용량 원래 인덱스 및 새로 만든된 것 필요한 디스크 공간 및 DML 작업 하는 동안 업데이트 해야 합니다. MAX_DURATION 옵션을 생략 하면 인덱스 작업의 완료 될 때까지 또는 오류가 발생할 때까지 계속 됩니다. 
-   \<low_priority_lock_wait > 인수 옵션 Sch-m 잠금을 차단 될 때 인덱스 작업을 진행할 수는 방법을 결정할 수 있습니다.
 
-  동일한 매개 변수를 사용 하 여 원래 ALTER INDEX REBUILD 문을 다시 실행 하는 일시 중지 된 인덱스 다시 작성 작업을 다시 시작 합니다. 또한 ALTER INDEX를 다시 시작 문을 실행 하 여 일시 중지 된 인덱스 다시 작성 작업을 재개할 수 있습니다.
-  SORT_IN_TEMPDB = ON 옵션은 다시 시작 가능한 인덱스에 대 한 지원 되지 않습니다 
-  다시 시작 가능을 사용 하 여 DDL 명령을 = ON 명시적 트랜잭션 내에서 실행 될 수 없습니다 (포함 될 수 없습니다... tran 시작 커밋 블록)입니다.
-  만 일시 중지 된 인덱스 작업은 다시 시작할 수 없습니다.
-   일시 중지 하는 인덱스 작업을 다시 시작할 때 MAXDOP 값을 새 값으로 변경할 수 있습니다.  MAXDOP 지정 되지 않은 경우, 일시 중지 하는 인덱스 작업을 다시 시작 하는 경우 마지막 MAXDOP 값을 가져옵니다. 인덱스 다시 작성 작업에 대 한 MAXDOP 옵션 전혀 지정 하지 않으면 기본 값을 가져옵니다.
- 인덱스 작업을 즉시 일시 중지, 지속적인 명령 (Ctrl + C)를 중지할 수 있습니다 또는 KILL 또는 ALTER INDEX를 일시 중지 명령을 실행할 수 있습니다 *session_id* 명령입니다. 명령이 일시 중지 되 면 다시 시작 옵션을 사용 하 여 다시 시작할 수 있습니다.
-  해당 프로세스를 중단 명령을 원래 인덱스를 다시 호스트 하 고 인덱스 작업을 중단 하는 세션 중지  
-  된을 제외 하 고 다시 시작 가능한 인덱스 다시 작성에 필요한 추가 리소스가
   -    인덱스 일시 중지 되는 시간을 포함 하는 인덱스를 작성 중인 유지 하는 데 필요한 추가 공간
   -    DDL 수 정의 모든 방지 DDL 상태
-  삭제할 레코드 정리는 인덱스 일시 중지 단계 중에 실행 되지만 인덱스를 실행 하는 동안 일시 중지 됩니다.   
다시 시작 가능한 인덱스 다시 작성 작업에 대 한 다음과 같은 기능 사용 불가능
   -    비활성화 되어 있는 인덱스를 다시 작성은 지원 되지 않습니다 다시 시작 가능 = ON
   -    ALTER INDEX REBUILD ALL 명령
   -    인덱스 다시 작성을 사용 하 여 ALTER TABLE  
   -    사용 하는 DDL 명령은 "RESUMEABLE = ON" 명시적 트랜잭션 내에서 실행 될 수 없습니다 (포함 될 수 없습니다... tran 시작 커밋 블록)
   -    키 열으로 계산 않은 인덱스 또는 타임 스탬프 열을 다시 작성 합니다.
-   인덱스 다시 작성 하려면이 작업의 시작 부분에서 Sch-m 잠금이 필요 고 기본 테이블에 LOB 열 다시 시작 가능한 클러스터 된 경우
   -    SORT_IN_TEMPDB = ON 옵션은 다시 시작 가능한 인덱스에 대 한 지원 되지 않습니다 

> [!NOTE]
> DDL 명령을 완료, 일시 중지 되거나 실패할 때까지 실행 합니다. 명령이 일시 중지 하는 경우 작업을 일시 중지 된 하 고 인덱스 만들기가 완료 하지 않았음을 나타내는 오류가 발생 합니다. 현재 인덱스 상태에 대 한 자세한 정보를 얻을 수 있습니다 [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md)합니다. 로 하기 전에 오류가 발생 한 경우는 오류가 발생 합니다도 합니다. 

  
 자세한 내용은 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요.  
  
 ### <a name="waitatlowpriority-with-online-index-operations"></a>온라인 인덱스 작업과 함께 WAIT_AT_LOW_PRIORITY  
  
 온라인 인덱스 다시 작성을 위해 DDL 문을 실행하려면 특정 테이블에서 실행 중인 모든 활성 차단 트랜잭션이 완료되어야 합니다. 온라인 인덱스 다시 작성이 실행되면 이 테이블에서 실행을 시작할 준비가 되어 있는 모든 새로운 트랜잭션이 차단됩니다. 온라인 인덱스 다시 작성에 대한 잠금 기간은 매우 짧지만 특정 테이블에서 열려 있는 모든 트랜잭션이 완료될 때까지 기다리고 새로운 트랜잭션이 시작되지 않도록 차단하기 위해서는 처리량에 상당한 영향을 주어 작업 속도가 느려지거나 시간 초과가 발생할 수 있으며, 기본 테이블에 대한 액세스가 크게 제한될 수 있습니다. **WAIT_AT_LOW_PRIORITY** 옵션을 사용 하면 DBA의 온라인 인덱스 다시 작성 하 고 3 개 옵션 중 하나를 선택 하도록 허용 하는 데 필요한 S-잠금 및 Sch-m 잠금을 관리할 수 있습니다. 세 가지 경우 모두, 대기 시간 동안에서 ( `(MAX_DURATION = n [minutes])` ), 차단 활동이 없으면는, 온라인 인덱스 다시 작성은 대기 하지 않고 즉시 실행 되 고 DDL 문이 완료 됩니다.  
  
## <a name="spatial-index-restrictions"></a>공간 인덱스 제한 사항  
 공간 인덱스를 다시 작성할 때는 공간 인덱스에 스키마 잠금이 유지되기 때문에 인덱스 작업 중에 기본 사용자 테이블을 사용할 수 없습니다.  
  
 공간 인덱스가 해당 테이블의 열에 정의된 경우 사용자 테이블에 있는 PRIMARY KEY 제약 조건을 수정할 수 없습니다. PRIMARY KEY 제약 조건을 변경하려면 먼저 테이블의 모든 공간 인덱스를 삭제해야 합니다. PRIMARY KEY 제약 조건을 수정한 후에는 각 공간 인덱스를 다시 만들 수 있습니다.  
  
 단일 파티션 다시 작성 작업에서는 공간 인덱스를 지정할 수 없습니다. 하지만 전체 파티션을 다시 작성할 때는 공간 인덱스를 지정할 수 있습니다.  
  
 공간 인덱스에 지정된 옵션(예: BOUNDING_BOX 또는 GRID)을 변경하려면 DROP_EXISTING = ON을 지정하는 CREATE SPATIAL INDEX 문을 사용하거나 해당 공간 인덱스를 삭제하고 새로 만들 수 있습니다. 예제를 보려면 [CREATE SPATIAL INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)의 "주의" 섹션을 참조하세요.  
  
## <a name="data-compression"></a>Data Compression  
 데이터 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
 페이지 및 행 압축을 변경 내용이 미치는 영향을 테이블, 인덱스 또는 파티션을 평가 수행 하려면 사용 하 여는 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 저장 프로시저입니다.  
  
 다음은 분할된 인덱스에 적용되는 제한 사항입니다.  
  
-   사용 하는 경우 `ALTER INDEX ALL ...`, 압축 설정을 단일 파티션의 테이블에 있는 경우 변경할 수 없습니다 정렬 되지 않은 인덱스가 있습니다.  
  
-   ALTER INDEX \<인덱스 >... REBUILD  PARTITION  ...  구문은 인덱스의 지정된 파티션을 다시 작성합니다.  
  
-   ALTER INDEX \<인덱스 >... REBUILD  WITH  ...  구문은 인덱스의 모든 파티션을 다시 작성합니다.  
  
## <a name="statistics"></a>통계  
 실행 하는 동안 **ALTER INDEX ALL...** 테이블에서 인덱스와 통계 associates만 업데이트 됩니다. 인덱스 대신 테이블에 대해 만들어진 자동 또는 수동 통계는 업데이트되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 ALTER INDEX를 실행하려면 최소한 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
## <a name="version-notes"></a>버전 정보  
  
-   SQL 데이터베이스 파일 그룹 및 filestream 옵션을 사용 하지 않습니다.  
  
-   Columnstore 인덱스는 SQL Server 2012 이전의 지원 되지 않습니다. 

-  다시 시작 가능한 인덱스 작업은 SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 사용할 수 있는 시작 |   
  
## <a name="basic-syntax-example"></a>기본 구문 예제:   
  
```tsql 
ALTER INDEX index1 ON table1 REBUILD;  
  
ALTER INDEX ALL ON table1 REBUILD;  
  
ALTER INDEX ALL ON dbo.table1 REBUILD;  
```

## <a name="examples-columnstore-indexes"></a>예: Columnstore 인덱스  
 이 예에서는 columnstore 인덱스에 적용 합니다.  
  
### <a name="a-reorganize-demo"></a>1. 데모를 다시 구성  
 이 예에서는 ALTER INDEX REORGANIZE 명령을 사용 예를 보여 줍니다.  여러 개의 rowgroup 및 다음 REORGANIZE rowgroup 병합 하는 방법을 보여 줍니다 테이블을 만듭니다.  
  
```  
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
```tsql
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;  
```  
  
 TABLOCK 옵션을 사용 하 여 병렬의 행을 삽입 합니다. SQL Server 2016 부터는 INSERT INTO 작업을 동시에 실행할 수 TABLOCK 사용 되는 경우.  
  
```tsql  
INSERT INTO cci_target WITH (TABLOCK) 
SELECT TOP 300000 * FROM staging;  
```  
  
 열린 델타 행 그룹을 확인 하려면이 명령을 실행 합니다. Rowgroup의 수는 병렬 처리 수준에 따라 달라 집니다.  
  
```tsql  
SELECT *   
FROM sys.dm_db_column_store_row_group_physical_stats   
WHERE object_id  = object_id('cci_target');  
```  
  
 모든 CLOSED 및 OPEN rowgroup을 columnstore로 강제로 수행 하려면이 명령을 실행 합니다.  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
 이 명령을 다시 실행 하 고 더 작은 행 그룹이 압축 된 행 그룹 하나에 병합 됩니다 표시 됩니다.  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="b-compress-closed-delta-rowgroups-into-the-columnstore"></a>2. 닫힌된 델타 행 그룹을 columnstore로 압축 합니다.  
 이 예제에서는 REORGANIZE 옵션을 압축 각 닫힌된 델타 행 그룹을 columnstore로 압축 된 행 그룹으로 합니다.   이 작업은 필요 하지 하지만 튜플 이동 기가 있을 정도로 충분히 빠르면 CLOSED 행 그룹이 압축 되지 않습니다 때 유용 합니다.  
  
```tsql  
-- Uses AdventureWorksDW  
-- REORGANIZE all partitions  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
  
-- REORGANIZE a specific partition  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;  
```  
  
### <a name="c-compress-all-open-and-closed-delta-rowgroups-into-the-columnstore"></a>3. 모든 열린 및 닫힌 델타 행 그룹이 columnstore로 압축  
 에 적용 되지 않습니다: SQL Server 2012 및 2014  
  
 SQL Server 2016 부터는 실행할 수 있습니다 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON) 각 열리고 닫힌 델타 행 그룹으로 압축된 된 행 그룹이 columnstore로 압축 합니다.    deltastore가 비우고 모든 행을 columnstore로 압축 되도록 합니다. 이러한 작업에 하나 이상의 deltastore가 행을 저장 하므로 많은 삽입 작업을 수행 하는 후에 특히 유용 합니다.  
  
 REORGANIZE 결합 rowgroup이 최대 행 수 까지의 행 그룹을 채우는 \<1,024,576 = 합니다. 따라서 모든 열기 및 CLOSED 행 그룹이 압축 하면 않습니다 /fd만 행을 몇 개 압축 된 rowgroup 많이 합니다. 원하는 rowgroup이 수를 채움 압축 된 크기를 줄이고 쿼리 성능을 향상 시킬 수 있습니다.  
  
```tsql  
-- Uses AdventureWorksDW2016  
-- Move all OPEN and CLOSED delta rowgroups into the columnstore.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
-- For a specific partition, move all OPEN AND CLOSED delta rowgroups into the columnstore  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="d-defragment-a-columnstore-index-online"></a>4. Columnstore 인덱스를 온라인 조각 모음  
 에 적용 되지 않습니다: SQL Server 2012 및 2014 합니다.  
  
 SQL Server 2016 부터는 REORGANIZE는 columnstore로 델타 행 그룹을 여러 개 압축지 않습니다. 또한 온라인 조각 모음을 수행합니다. 첫째, 물리적으로 삭제 된 행 그룹의 행 중 10% 이상을 삭제 된 행을 제거 하 여 columnstore의 크기를 줄입니다.  그런 다음 rowgroup 당 1,024,576 행의 최대 해야 하는 보다 큰 행 그룹을 형성 하는 rowgroup를 결합 합니다.  이 변경 되는 모든 rowgroup 다시 압축 합니다.  
  
> [!NOTE]
>  SQL Server 2016 부터는 columnstore 인덱스 다시 작성은 더 이상 대부분의 경우에서 필요한 REORGANIZE에서 물리적으로 삭제 된 행을 제거 하 고 행 그룹 병합 합니다. 에 COMPRESS_ALL_ROW_GROUPS 옵션이 이전에 수행할 수 있었습니다 다시 빌드를 사용 하 여 columnstore에 모든 OPEN 또는 CLOSED 델타 행 그룹을 강제로 수행 합니다.   REORGANIZE는 온라인 상태 이며 쿼리 작업이 발생 하면 계속 될 수 있도록 백그라운드에서 발생 합니다.  
  
```tsql  
-- Uses AdventureWorks  
-- Defragment by physically removing rows that have been logically deleted from the table, and merging rowgroups.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
```  
  
### <a name="e-rebuild-a-clustered-columnstore-index-offline"></a>5. 오프 라인으로 클러스터형된 columnstore 인덱스를 다시 작성  
 적용 대상: SQL Server 2012, SQL Server 2014  
  
 이상 SQL Server 2016 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], ALTER INDEX REBUILD 대신 ALTER INDEX REORGANIZE를 사용 하는 것이 좋습니다.  
  
> [!NOTE]
>  SQL Server 2012 및 2014 REORGANIZE CLOSED 행 그룹이 columnstore로 압축만 사용 됩니다. 조각 모음 작업을 수행 하 고 모든 델타 rowgroup이 columnstore로 강제로 하는 유일한 방법은 인덱스를 다시 작성 됩니다.  
  
 이 예에서는 클러스터형된 columnstore 인덱스 다시 작성 하 고 모든 델타 rowgroup이 columnstore로 강제로 하는 방법을 보여 줍니다. 첫 단계에서는 클러스터형 columnstore 인덱스가 있는 FactInternetSales2 테이블을 준비하고 첫 번째 네 열에서 데이터를 삽입합니다.  
  
```tsql  
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
  
 결과 표시는 OPEN 행 그룹이 하나, 즉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 더 많은 행을 행 그룹을 닫고 및 데이터를 columnstore로 이동 하기 전에 추가 될 때까지 대기 합니다. 다음 문에서 모든 행을 columnstore로 강제로 클러스터형된 columnstore 인덱스 다시 작성 합니다.  
  
```tsql  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 SELECT 문 결과는 행 그룹이 COMPRESSED임을 보여 주며 행 그룹의 열 세그먼트가 이제 압축되고 columnstore에 저장됨을 의미합니다.  
  
### <a name="f-rebuild-a-partition-of-a-clustered-columnstore-index-offline"></a>6. 오프 라인으로 클러스터형된 columnstore 인덱스의 파티션을 다시 작성  
 에 대해이 사용 하 여: SQL Server 2012, SQL Server 2014  
  
 대규모 클러스터형된 columnstore 인덱스의 파티션을 다시 작성 하려면 파티션 옵션과 함께 ALTER INDEX REBUILD를 사용 합니다. 이 예에서는 12 파티션을 다시 작성합니다. SQL Server 2016 부터는 좋습니다 REORGANIZE 다시 작성 경로로 바꿉니다.  
  
```tsql  
ALTER INDEX cci_fact3   
ON fact3  
REBUILD PARTITION = 12;  
```  
  
### <a name="g-change-a-clustered-columstore-index-to-use-archival-compression"></a>7. 보관 압축을 사용 하는 클러스터 된 columstore 인덱스 변경  
 에 적용 되지 않습니다: SQL Server 2012  
  
 COLUMNSTORE_ARCHIVE 데이터 압축 옵션을 사용 하 여 클러스터형된 columnstore 인덱스를 더욱 해소의 크기를 줄일 수 있습니다. 이 오래 된 데이터가 더 저렴 한 저장소에 유지 하려는 것이 적합 합니다. 기본 COLUMNSTORE 압축으로 보다 느립니다은 이후 자주 액세스 하지 않은 데이터에 대 한 압축을 풀만 사용 하는 것이 좋습니다.  
  
 다음 예에서는 보관 압축을 사용하기 위해 클러스터형 columnstore 인덱스를 다시 작성한 다음 보관 압축을 제거하는 방법을 보여 줍니다. 마지막 결과에서는 columnstore 압축만 사용합니다.  
  
```tsql  
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
  
## <a name="examples-rowstore-indexes"></a>예: Rowstore 인덱스  
  
### <a name="a-rebuilding-an-index"></a>1. 인덱스 다시 작성  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Employee` 테이블의 단일 인덱스를 다시 작성합니다.  
  
```tsql  
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;  
```  
  
### <a name="b-rebuilding-all-indexes-on-a-table-and-specifying-options"></a>2. 테이블의 모든 인덱스 다시 작성 및 옵션 지정  
 다음 예에서는 `ALL` 키워드를 지정합니다. 그러면 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 Production.Product 테이블과 연결된 모든 인덱스를 다시 작성합니다. 3개의 옵션이 지정됩니다.  
  
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.  
  
```tsql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);  
```  
  
 다음 예에서는 낮은 우선 순위 잠금 옵션을 포함하여 ONLINE 옵션을 추가하고 행 압축 옵션을 추가합니다.  
  
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2014부터 시작)입니다.  
  
```tsql  
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
  
```tsql  
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION);  
```  
  
### <a name="d-setting-options-on-an-index"></a>4. 인덱스에 옵션 설정  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `AK_SalesOrderHeader_SalesOrderNumber` 인덱스에 몇 가지 옵션을 설정합니다.  
  
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2008부터 시작)입니다.  
  
```tsql  
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
  
```tsql  
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```  
  
### <a name="f-disabling-constraints"></a>6. 제약 조건 비활성화  
 다음 예제에서 기본 키 인덱스를 비활성화 하 여 PRIMARY KEY 제약 조건을 사용 하지 않도록 설정 된 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다. 기본 테이블에 대한 FOREIGN KEY 제약 조건이 자동으로 비활성화되고 경고 메시지가 표시됩니다.  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;  
```  
  
 결과 집합에서 다음과 같은 경고 메시지를 반환합니다.  
  
 ```tsql  
 Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'  
 on table 'EmployeeDepartmentHistory' referencing table 'Department'  
 was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
 ```  
  
### <a name="g-enabling-constraints"></a>7. 제약 조건 활성화  
 다음 예에서는 6번 예에서 비활성화된 PRIMARY KEY와 FOREIGN KEY 제약 조건을 활성화합니다.  
  
 PRIMARY KEY 인덱스를 다시 작성하여 PRIMARY KEY 제약 조건이 활성화됩니다.  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;  
```  
  
 그런 다음 FOREIGN KEY 제약 조건이 활성화됩니다.  
  
```tsql  
ALTER TABLE HumanResources.EmployeeDepartmentHistory  
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;  
GO  
```  
  
### <a name="h-rebuilding-a-partitioned-index"></a>8. 분할된 인덱스 다시 작성  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 분할된 인덱스 `5`의 단일 파티션인 파티션 번호 `IX_TransactionHistory_TransactionDate`를 다시 작성합니다. 파티션 5가 온라인으로 다시 작성되고 낮은 우선 순위 잠금에 대한 10분 대기 시간이 인덱스 다시 작성 작업으로 획득된 모든 잠금에 개별적으로 적용됩니다. 이 시간 동안에는 인덱스 다시 작성을 완료하기 위한 잠금을 획득할 수 없으며, 다시 작성 작업 문이 중단됩니다.  
  
**적용 대상**: Azure SQL 데이터베이스 및 SQL Server (SQL Server 2014부터 시작)입니다.  
  
```tsql  
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
  
```tsql
ALTER INDEX IX_INDEX1   
ON T1  
REBUILD   
WITH (DATA_COMPRESSION = PAGE);  
GO  
```  
  
 추가 데이터 압축 예 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
 
### <a name="j-online-resumable-index-rebuild"></a>10. 다시 시작 가능한 온라인 인덱스 다시 작성

**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 (기능은 공개 미리 보기 상태에서)로 시작    

 다음 예에서는 다시 시작 가능한 온라인 인덱스 다시 작성을 사용 하는 방법을 보여 줍니다. 

1. MAXDOP으로 작업을 다시 시작 가능으로 온라인 인덱스 다시 작성 실행 = 1입니다.

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, MAXDOP=1, RESUMABLE=ON) ;
   ```

2. 동일한 실행 명령을 다시 (위 참조)는 인덱스 작업을 일시 중지 된 후 자동으로 재개 인덱스 다시 작성 작업 합니다.

3. MAX_DURATION 집합 240 분으로 다시 시작 가능한 작업으로 온라인 인덱스 다시 작성을 실행 합니다.

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, RESUMABLE=ON, MAX_DURATION=240) ; 
   ```
4. 실행 중인 다시 시작 가능한 온라인 인덱스 다시 작성을 일시 중지 합니다.

   ```tsql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```   
5. MAXDOP에 대 한 새 값을 지정 하는 다시 시작 될 작업을 4로 설정 하는 대로 실행 된 인덱스를 다시 작성에 대 한 온라인 인덱스 다시 작성을 다시 시작 합니다.

   ```tsql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP=4) ;
   ```
6. 다시 시작 가능 상태로 실행 된 인덱스 온라인 다시 작성에 대 한 온라인 인덱스 다시 작성 작업을 다시 시작 합니다. MAXDOP를 2로 설정, 240 분 및 10 분 잠금 대기에서 차단 되는 인덱스의 경우 resmumable로 실행 되 고 인덱스에 대 한 실행 시간을 설정 및 그 후 모든 블 로커를 중지 합니다. 

   ```tsql
      ALTER INDEX test_idx on test_table  
         RESUME WITH (MAXDOP=2, MAX_DURATION= 240 MINUTES, 
         WAIT_AT_LOW_PRIORITY (MAX_DURATION=10, ABORT_AFTER_WAIT=BLOCKERS)) ;
   ```      
7. 실행 중이거나 일시 중지 되는 다시 시작 가능한 인덱스 다시 작성 작업을 중단 합니다.

   ```tsql
   ALTER INDEX test_idx on test_table ABORT ;
   ``` 
  
## <a name="see-also"></a>관련 항목:  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [공간 인덱스 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [XML 인덱스 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [DROP index&#40; Transact SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [인덱스 및 제약 조건 비활성화](../../relational-databases/indexes/disable-indexes-and-constraints.md)   
 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [온라인 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)   
 [Reorganize와 인덱스를 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  



