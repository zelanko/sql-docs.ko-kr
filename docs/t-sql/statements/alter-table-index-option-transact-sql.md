---
title: index_option (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- index_option
ms.assetid: 8a14f12d-2fbf-4036-b8b2-8db3354e0eb7
caps.latest.revision: 68
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: e7563f9fe992dcf4f9308cccbf11f6310b7925a7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/08/2017

---
# <a name="alter-table-indexoption-transact-sql"></a>ALTER TABLE index_option (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  사용 하 여 만든 제약 조건 정의의 일부인 색인에 적용할 수 있는 옵션 집합이 지정 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)합니다.  
  
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
 PAD_INDEX  **=**  {ON | **OFF** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 인덱스 패딩을 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 FILLFACTOR로 지정된 사용 가능한 공간의 비율이 인덱스의 중간 수준 페이지에 적용됩니다.  
  
 OFF 또는 *fillfactor* 지정 하지 않으면  
 중간 수준 페이지는 중간 페이지의 키 집합이 지정된 경우 최소한 인덱스에 사용할 수 있는 최대 크기의 행 하나를 위한 공간을 남겨 두고 거의 채워집니다.  
  
 FILLFACTOR  **=**  *fillfactor*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 인덱스를 만들거나 변경할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. 지정한 값은 1에서 100까지의 정수 값이어야 합니다. 기본값은 0입니다.  
  
> [!NOTE]  
>  채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
 IGNORE_DUP_KEY  **=**  {ON | **OFF** }  
 삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려는 경우에 대한 오류 응답을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. 실행할 때이 옵션에 영향을 주지 않습니다 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), 또는 [업데이트](../../t-sql/queries/update-transact-sql.md)합니다. 기본값은 OFF입니다.  
  
 ON  
 중복 키 값이 고유 인덱스에 삽입 하는 경우 경고 메시지가 나타납니다. 고유성 제약 조건을 위반 하는 행만 실패 합니다.  
  
 OFF  
 오류 메시지가 중복 키 값이 고유 인덱스에 삽입 되 면 발생 합니다. 전체 INSERT 작업이 롤백됩니다.  
  
 뷰에 생성 된 인덱스, 고유 하지 않은 인덱스, XML 인덱스, 공간 인덱스 및 필터링 된 인덱스에 대 한 IGNORE_DUP_KEY는 ON으로 설정할 수 없습니다.  
  
 IGNORE_DUP_KEY를 보려면 사용 하 여 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.  
  
 이전 버전과 호환되는 구문에서 WITH IGNORE_DUP_KEY는 WITH IGNORE_DUP_KEY = ON과 같습니다.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | **OFF** }  
 통계를 다시 계산할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 이전 통계가 자동으로 다시 계산되지 않습니다.  
  
 OFF  
 자동 통계 업데이트가 설정됩니다.  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** | OFF}  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 행 잠금이 사용되지 않습니다.  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** | OFF}  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 페이지 잠금이 사용되지 않습니다.  
  
 SORT_IN_TEMPDB  **=**  {ON | **OFF** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 에 정렬 결과 저장할지 여부를 지정 **tempdb**합니다. 기본값은 OFF입니다.  
  
 ON  
 인덱스를 작성 하는 데 사용 되는 중간 정렬 결과에 저장 됩니다 **tempdb**합니다. 경우 인덱스를 만드는 데 필요한 시간이 줄어들 수 있습니다 **tempdb** 켜져 있습니다. 다른 사용자 데이터베이스는 디스크 집합입니다. 그러나 인덱스 작성 중에 사용되는 디스크 공간의 크기는 커집니다.  
  
 OFF  
 중간 정렬 결과가 인덱스와 같은 데이터베이스에 저장됩니다.  
  
 온라인  **=**  {ON | **OFF** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 인덱스 작업 중 쿼리 및 데이터 수정에 기본 테이블과 관련 인덱스를 사용할 수 있는지 여부를 지정합니다. 기본값은 OFF입니다. REBUILD 작업은 ONLINE 작업으로만 수행할 수 있습니다.  
  
> [!NOTE]  
>  고유 비클러스터형 인덱스는 온라인으로 만들 수 없습니다. 여기에는 UNIQUE 또는 PRIMARY KEY 제약 조건 때문에 생성된 인덱스가 포함됩니다.  
  
 ON  
 인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 작업의 주 단계 중 내재된 공유(IS) 잠금만 원본 테이블에 유지됩니다. 따라서 기본 테이블 및 인덱스에 대한 쿼리나 업데이트를 처리할 수 있습니다. 작업이 시작되면 아주 짧은 기간 동안 S(공유) 잠금이 원본 개체에 유지됩니다. 작업이 끝나면 짧은 기간 동안 비클러스터형 인덱스가 생성되는 경우에는 원본에 대해 S(공유) 잠금이 획득되고, 온라인 상태에서 클러스터형 인덱스가 생성 또는 삭제될 때와 클러스터형 또는 비클러스터형 인덱스가 다시 작성될 때는 SCH-M(스키마 수정) 잠금이 획득됩니다. 온라인 인덱스 잠금은 짧은 메타데이터 잠금이지만 특히 Sch-M 잠금은 이 테이블에서 모든 차단 트랜잭션이 완료될 때까지 기다려야 합니다. 대기 시간 동안 Sch-M 잠금은 동일 테이블에 액세스할 때 이 잠금 뒤에서 기다리는 다른 모든 트랜잭션을 차단합니다. 로컬 임시 테이블에서 인덱스를 생성하는 경우에는 ONLINE을 ON으로 설정할 수 없습니다.  
  
> [!NOTE]  
>  온라인 인덱스 다시 작성을 설정할 수는 *low_priority_lock_wait* 이 단원의 뒷부분에서 설명 하는 옵션입니다. *low_priority_lock_wait* 온라인 인덱스 다시 작성 하는 동안 S 및 Sch-m 잠금 우선 순위를 관리 합니다.  
  
 OFF  
 인덱스 작업 중에 테이블 잠금이 적용됩니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다. 클러스터형 인덱스를 생성, 다시 작성 또는 삭제하거나 비클러스터형 인덱스를 다시 작성 또는 삭제하는 오프라인 인덱스 작업을 통해 테이블의 SCH-M(스키마 수정) 잠금을 획득합니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다. 비클러스터형 인덱스를 만드는 오프라인 인덱스 작업을 통해 테이블의 S(공유) 잠금을 획득합니다. 따라서 기본 테이블을 업데이트할 수 없지만 SELECT 문과 같은 읽기 작업은 허용됩니다.  
  
 자세한 내용은 참조 [어떻게 온라인 인덱스 작동](../../relational-databases/indexes/how-online-index-operations-work.md)합니다.  
  
> [!NOTE]  
>  온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 MAXDOP  **=**  *max_degree_of_parallelism*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 재정의 **x degree of** 인덱스 작업의 기간에 대 한 구성 옵션입니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
 *max_degree_of_parallelism* 될 수 있습니다.  
  
 - 1-병렬 계획이 생성이 되지 않습니다.  
 - \>1-지정 된 병렬 인덱스 작업에 사용 되는 프로세서의 최대 수를 제한 합니다.  
 - 현재 시스템 작업에 따라 보다 적은 또는 0 (기본값)-실제 프로세서 수를 사용 합니다.  
  
 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]  
>  병렬 인덱스 작업의 일부 버전에서 사용할 수 없는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 DATA_COMPRESSION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.  
  
 없음  
 테이블 또는 지정된 파티션이 압축되지 않습니다. rowstore 테이블에만 적용되며 columnstore 테이블에는 적용되지 않습니다.  
  
 ROW  
 테이블 또는 지정된 파티션이 행 압축을 사용하여 압축됩니다. rowstore 테이블에만 적용되며 columnstore 테이블에는 적용되지 않습니다.  
  
 PAGE  
 테이블 또는 지정된 파티션이 페이지 압축을 사용하여 압축됩니다. rowstore 테이블에만 적용되며 columnstore 테이블에는 적용되지 않습니다.  
  
 COLUMNSTORE  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 columnstore 테이블에만 적용됩니다. COLUMNSTORE에서는 COLUMNSTORE_ARCHIVE 옵션으로 압축된 파티션을 압축 해제하도록 지정합니다. 데이터를 복원할 때 모든 columnstore 테이블에 사용 되는 columnstore 압축으로 압축 되도록 COLUMNSTORE 인덱스 계속 합니다.  
  
 COLUMNSTORE_ARCHIVE  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 클러스터형 columnstore 인덱스로 저장된 테이블인 columnstore 테이블에만 적용됩니다. COLUMNSTORE_ARCHIVE 더 작은 크기로 지정 된 파티션을 압축합니다. 보관하거나 보다 적은 저장소가 필요한 기타 상황에서 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
 압축에 대 한 자세한 내용은 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
ON PARTITIONS **(** { \<partition_number_expression > | \<범위 >} [ **,**...  *n*  ] **)** **적용할**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.  
  
 DATA_COMPRESSION 설정을 적용할 파티션을 지정합니다. 테이블이 분할 되지 않은 경우 ON PARTITIONS 인수 오류가 발생 합니다. ON PARTITIONS 절을 제공 하지 않으면 DATA_COMPRESSION 옵션이 분할된 된 테이블의 모든 파티션에 적용 됩니다.  
  
\<partition_number_expression > 다음과 같은 방법으로 지정할 수 있습니다.  
  
-   파티션 번호를 지정합니다(예: ON PARTITIONS (2)).  
-   여러 개별 파티션의 파티션 번호를 쉼표로 구분하여 지정합니다(예: ON PARTITIONS (1,5)).  
-   범위와 개별 파티션을 모두 지정합니다(예: ON PARTITIONS (2,4,6 TO 8)).  
  
\<범위 > 예를 들어, TO로 구분 된 파티션 번호로 지정할 수 있습니다: ON PARTITIONS (6 TO 8)).  
  
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
  
**\<single_partition_rebuild__option >**  
 대부분의 경우 인덱스를 다시 작성하면 분할된 인덱스의 모든 파티션이 다시 작성됩니다. 다음 옵션을 단일 파티션에 적용하는 경우 일부 파티션이 다시 작성되지 않습니다.  
  
-   SORT_IN_TEMPDB  
-   MAXDOP  
-   DATA_COMPRESSION  
  
**low_priority_lock_wait**  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 A **스위치** 또는 온라인 인덱스 다시 작성이이 테이블에 대 한 차단 작업이 없는 경우 즉시 완료 됩니다. *WAIT_AT_LOW_PRIORITY* 경우 나타냅니다는 **스위치** 또는 온라인 인덱스 다시 작성 작업을 즉시 완료할 수 없을 때까지 대기 합니다. 작업에는 잠금을 계속 하려면는 DDL 문을 사용 하 여 충돌 하는 유지 하는 다른 작업을 허용 하는 낮은 우선 순위 잠금을 보유 합니다. 생략 된 **WAIT AT LOW PRIORITY** 옵션은 `WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`합니다.  
  
MAX_DURATION = *시간* [**분** ]  
 대기 시간 (분 단위로 지정 된 정수 값) 하는 **스위치** DDL 명령을 실행할 때까지 대기 하는 온라인 인덱스 다시 작성 잠금이 획득 해야 하는 또는 합니다. SWITCH 또는 온라인 인덱스 다시 작성 작업은 즉시 완료하려고 시도합니다. 작업에 대 한 차단 된 경우는 **MAX_DURATION** 시간 중 하나는 **ABORT_AFTER_WAIT** 동작이 실행 됩니다. **MAX_DURATION** 시간은 항상 분 단위 이며 단어 **분** 생략할 수 있습니다.  
  
ABORT_AFTER_WAIT = [**NONE** | **자체** | **블로 커가** }]  
 없음  
 계속는 **스위치** 또는 온라인 인덱스 작업 (일반 우선 순위 사용) 잠금 우선 순위를 변경 하지 않고 다시 작성 합니다.  
  
SELF  
 이 종료 되 고 **스위치** 또는 작업을 수행 하지 않고 현재 실행 중인 온라인 인덱스 다시 작성 DDL 작업 합니다.  
  
BLOCKERS  
 현재 차단 하는 모든 사용자 트랜잭션을 종료는 **스위치** 또는 온라인 인덱스 다시 작성 DDL 작업의 작업을 계속할 수 있도록 합니다.  
 블로 커가 필요는 **ALTER ANY CONNECTION** 권한.  
  
## <a name="remarks"></a>주의  
 인덱스 옵션의 전체 설명은 참조 하세요. [CREATE index&#40; Transact SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_constraint &#40; Transact SQL &#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)   
 [computed_column_definition &#40; Transact SQL &#41;](../../t-sql/statements/alter-table-computed-column-definition-transact-sql.md)   
 [table_constraint &#40; Transact SQL &#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  
  
 

