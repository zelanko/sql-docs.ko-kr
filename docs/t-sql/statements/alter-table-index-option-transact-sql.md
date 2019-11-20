---
title: " | Microsoft Docs"
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- index_option
ms.assetid: 8a14f12d-2fbf-4036-b8b2-8db3354e0eb7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e70998bed1ed0f2681009622cfb086baa79dcf02
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982012"
---
# <a name="alter-table-index_option-transact-sql"></a>ALTER TABLE index_option(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)을 사용하여 만든 제약 조건 정의의 일부인 색인에 적용할 수 있는 옵션 집합을 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
{   
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF } 
  | OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF } 
  | SORT_IN_TEMPDB = { ON | OFF }   
  | ONLINE = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE |ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
<single_partition_rebuild__option> ::=  
{  
    SORT_IN_TEMPDB = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = {NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE } }  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                           ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
## <a name="arguments"></a>인수  
 PAD_INDEX **=** { ON | **OFF** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 인덱스 패딩을 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 FILLFACTOR로 지정된 사용 가능한 공간의 비율이 인덱스의 중간 수준 페이지에 적용됩니다.  
  
 OFF 또는 *fillfactor*를 지정되지 않음  
 중간 수준 페이지는 중간 페이지의 키 집합이 지정된 경우 최소한 인덱스에 사용할 수 있는 최대 크기의 행 하나를 위한 공간을 남겨 두고 거의 채워집니다.  
  
 FILLFACTOR **=** _fillfactor_  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 인덱스를 만들거나 변경할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. 지정한 값은 1에서 100까지의 정수 값이어야 합니다. 기본값은 0입니다.  
  
> [!NOTE]  
>  채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
 IGNORE_DUP_KEY **=** { ON | **OFF** }  
 삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려고 할 때 응답 유형을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) 또는 [UPDATE](../../t-sql/queries/update-transact-sql.md)를 실행하는 경우에는 이 옵션이 아무런 영향을 미치지 않습니다. 기본값은 OFF입니다.  
  
 ON  
 중복된 키 값이 고유 인덱스에 삽입되는 경우 경고 메시지가 나타나고 고유성 제약 조건을 위반하는 행만 실패합니다.  
  
 OFF  
 중복된 키 값이 고유 인덱스에 삽입되는 경우 오류 메시지가 나타나고 전체 INSERT 작업이 롤백됩니다.  
  
 뷰, 비고유 인덱스, XML 인덱스, 공간 인덱스 및 필터링된 인덱스에 생성된 인덱스의 경우 IGNORE_DUP_KEY를 ON으로 설정할 수 없습니다.  
  
 IGNORE_DUP_KEY를 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)를 사용하세요.  
  
 이전 버전과 호환되는 구문에서 WITH IGNORE_DUP_KEY는 WITH IGNORE_DUP_KEY = ON과 같습니다.  
  
 STATISTICS_NORECOMPUTE **=** { ON | **OFF** }  
 통계를 다시 계산할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 이전 통계가 자동으로 다시 계산되지 않습니다.  
  
 OFF  
 자동 통계 업데이트가 설정됩니다.  
  
 ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 행 잠금이 사용되지 않습니다.  
  
 ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 페이지 잠금이 사용되지 않습니다.  

 OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | **OFF** }

**적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 이상

마지막 페이지 삽입 경합에 최적화할지 여부를 지정합니다. 기본값은 OFF입니다. 자세한 내용은 CREATE INDEX 페이지의 [순차 키](./create-index-transact-sql.md#sequential-keys) 섹션을 참조하세요.
 
 SORT_IN_TEMPDB **=** { ON | **OFF** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 정렬 결과를 **tempdb**에 저장할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 인덱스 작성에 사용된 중간 정렬 결과가 **tempdb**에 저장됩니다. 이 경우 사용자 데이터베이스가 아닌 다른 디스크 집합에 **tempdb**가 있으면 인덱스 생성에 필요한 시간이 단축될 수 있습니다. 그러나 인덱스 작성 중에 사용되는 디스크 공간의 크기는 커집니다.  
  
 OFF  
 중간 정렬 결과가 인덱스와 같은 데이터베이스에 저장됩니다.  
  
 ONLINE **=** { ON | **OFF** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 인덱스 작업 중 쿼리 및 데이터 수정에 기본 테이블과 관련 인덱스를 사용할 수 있는지 여부를 지정합니다. 기본값은 OFF입니다. REBUILD 작업은 ONLINE 작업으로만 수행할 수 있습니다.  
  
> [!NOTE]  
>  고유 비클러스터형 인덱스는 온라인으로 만들 수 없습니다. 여기에는 UNIQUE 또는 PRIMARY KEY 제약 조건 때문에 생성된 인덱스가 포함됩니다.  
  
 ON  
 인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 작업의 주 단계 중 내재된 공유(IS) 잠금만 원본 테이블에 유지됩니다. 따라서 기본 테이블 및 인덱스에 대한 쿼리나 업데이트를 처리할 수 있습니다. 작업이 시작되면 아주 짧은 기간 동안 S(공유) 잠금이 원본 개체에 유지됩니다. 작업이 끝나면 짧은 기간 동안 비클러스터형 인덱스가 생성되는 경우에는 원본에 대해 S(공유) 잠금이 획득되고, 온라인 상태에서 클러스터형 인덱스가 생성 또는 삭제될 때와 클러스터형 또는 비클러스터형 인덱스가 다시 작성될 때는 SCH-M(스키마 수정) 잠금이 획득됩니다. 온라인 인덱스 잠금은 짧은 메타데이터 잠금이지만 특히 Sch-M 잠금은 이 테이블에서 모든 차단 트랜잭션이 완료될 때까지 기다려야 합니다. 대기 시간 동안 Sch-M 잠금은 동일 테이블에 액세스할 때 이 잠금 뒤에서 기다리는 다른 모든 트랜잭션을 차단합니다. 로컬 임시 테이블에서 인덱스를 생성하는 경우에는 ONLINE을 ON으로 설정할 수 없습니다.  
  
> [!NOTE]  
>  온라인 인덱스 다시 작성은 이 섹션의 뒷부분에서 설명하는 *low_priority_lock_wait* 옵션을 설정할 수 있습니다. *low_priority_lock_wait*는 온라인 인덱스 다시 작성 중에 S 및 Sch-M 잠금 우선 순위를 관리합니다.  
  
 OFF  
 인덱스 작업 중에 테이블 잠금이 적용됩니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다. 클러스터형 인덱스를 생성, 다시 작성 또는 삭제하거나 비클러스터형 인덱스를 다시 작성 또는 삭제하는 오프라인 인덱스 작업을 통해 테이블의 SCH-M(스키마 수정) 잠금을 획득합니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다. 비클러스터형 인덱스를 만드는 오프라인 인덱스 작업을 통해 테이블의 S(공유) 잠금을 획득합니다. 따라서 기본 테이블을 업데이트할 수 없지만 SELECT 문과 같은 읽기 작업은 허용됩니다.  
  
 자세한 내용은 [온라인 인덱스 작업의 작동 원리](../../relational-databases/indexes/how-online-index-operations-work.md)를 참조하세요.  
  
> [!NOTE]
>  온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 MAXDOP **=** _max_degree_of_parallelism_  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 인덱스 작업 기간 동안 **max degree of parallelism** 구성 옵션을 재정의합니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
 *max_degree_of_parallelism*은 다음 중 하나일 수 있습니다.  
  
 - 1 - 병렬 계획이 생성되지 않습니다.  
 - \> 1 - 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 지정된 값으로 제한합니다.  
 - 0(기본값) - 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]
>  병렬 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 DATA_COMPRESSION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.  
  
 없음  
 테이블 또는 지정된 파티션이 압축되지 않습니다. rowstore 테이블에만 적용되며 columnstore 테이블에는 적용되지 않습니다.  
  
 ROW  
 테이블 또는 지정된 파티션이 행 압축을 사용하여 압축됩니다. rowstore 테이블에만 적용되며 columnstore 테이블에는 적용되지 않습니다.  
  
 PAGE  
 테이블 또는 지정된 파티션이 페이지 압축을 사용하여 압축됩니다. rowstore 테이블에만 적용되며 columnstore 테이블에는 적용되지 않습니다.  
  
 COLUMNSTORE  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상  
  
 columnstore 테이블에만 적용됩니다. COLUMNSTORE에서는 COLUMNSTORE_ARCHIVE 옵션으로 압축된 파티션을 압축 해제하도록 지정합니다. 데이터는 복구될 때 모든 columnstore 테이블에 사용된 columnstore 압축으로 COLUMNSTORE 인덱스는 계속 압축됩니다.  
  
 COLUMNSTORE_ARCHIVE  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상  
  
 클러스터형 columnstore 인덱스로 저장된 테이블인 columnstore 테이블에만 적용됩니다. COLUMNSTORE_ARCHIVE는 지정된 파티션을 보다 작은 크기로 압축합니다. 보관하거나 보다 적은 스토리지가 필요한 기타 상황에서 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
ON PARTITIONS **(** { \<partition_number_expression> | \<range> } [ **,** ...*n* ] **)** **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 DATA_COMPRESSION 설정을 적용할 파티션을 지정합니다. 테이블이 분할되지 않은 경우 ON PARTITIONS 인수를 사용하면 오류가 발생합니다. ON PARTITIONS 절을 제공하지 않으면 DATA_COMPRESSION 옵션이 분할된 테이블의 모든 파티션에 적용됩니다.  
  
\<partition_number_expression>은 다음과 같은 방법으로 지정할 수 있습니다.  
  
-   파티션의 번호를 지정합니다(예: ON PARTITIONS(2).  
-   여러 개별 파티션의 파티션 번호를 쉼표로 구분하여 지정합니다. 예를 들면 다음과 같습니다. ON PARTITIONS(1, 5).  
-   범위와 개별 파티션을 모두 지정합니다. 예를 들면 다음과 같습니다. ON PARTITIONS(2, 4, 6~8).  
  
\<range>는 TO라는 단어로 구분된 파티션 번호로 지정할 수 있습니다. 예를 들면 다음과 같습니다. ON PARTITIONS(6~8).  
  
 여러 파티션에 대해 서로 다른 데이터 압축 유형을 설정하려면 DATA_COMPRESSION 옵션을 두 번 이상 지정합니다. 예를 들면 다음과 같습니다.  
  
```sql  
--For rowstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
  
--For columnstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = COLUMNSTORE ON PARTITIONS (1, 3, 5),   
DATA_COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (2, 4, 6 TO 8)  
)  
```  
  
**\<single_partition_rebuild__option>**  
 대부분의 경우 인덱스를 다시 작성하면 분할된 인덱스의 모든 파티션이 다시 작성됩니다. 다음 옵션을 단일 파티션에 적용하는 경우 일부 파티션이 다시 작성되지 않습니다.  
  
-   SORT_IN_TEMPDB  
-   MAXDOP  
-   DATA_COMPRESSION  
  
**low_priority_lock_wait**  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상  
  
 **SWITCH** 또는 온라인 인덱스 다시 작성은 이 테이블에 대한 차단 작업이 없는 경우 즉시 완료됩니다. *WAIT_AT_LOW_PRIORITY*는 **SWITCH** 또는 온라인 인덱스 다시 작성 작업을 즉시 완료할 수 없는 경우 대기한다는 것을 나타냅니다. 이 작업은 우선 순위가 낮은 잠금을 보류하여, DDL 문과 충돌하는 잠금을 가진 다른 작업이 계속 수행될 수 있도록 허용합니다. **WAIT AT LOW PRIORITY** 옵션을 생략하는 것은 `WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`와 동일합니다.  
  
MAX_DURATION = *time* [**MINUTES** ]  
 DDL 명령을 실행할 때 **SWITCH** 또는 획득해야 하는 온라인 인덱스 다시 작성 잠금이 기다리는 대기 시간(분 단위로 지정된 정수 값)입니다. SWITCH 또는 온라인 인덱스 다시 작성 작업은 즉시 완료하려고 시도합니다. 작업이 **MAX_DURATION** 시간 동안 차단되면 **ABORT_AFTER_WAIT** 작업 중 하나가 실행됩니다. **MAX_DURATION** 시간은 항상 분 단위이며 **MINUTES** 단어는 생략할 수 있습니다.  
  
ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERS** } ]  
 없음  
 잠금 우선 순위를 변경하지 않고 **SWITCH** 또는 온라인 인덱스 다시 작성 작업을 계속합니다(일반 우선 순위 사용).  
  
SELF  
 어떤 동작도 수행하지 않고 현재 실행 중인 **SWITCH** 또는 온라인 인덱스 다시 작성 DDL 작업을 종료합니다.  
  
BLOCKERS  
 작업을 계속할 수 있도록 **SWITCH** 또는 온라인 인덱스 다시 작성 DDL 작업을 현재 차단하는 모든 사용자 트랜잭션을 종료합니다.  
 BLOCKERS에는 **ALTER ANY CONNECTION** 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
 인덱스 옵션에 대한 자세한 설명은 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)   
 [computed_column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-computed-column-definition-transact-sql.md)   
 [table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  
  
 
