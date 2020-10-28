---
description: CREATE INDEX(Transact-SQL)
title: CREATE INDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE INDEX
- INDEX
- INDEX_TSQL
- CREATE_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- PRIMARY XML INDEX statement
- indexes [SQL Server], creating
- online index operations
- index keys [SQL Server]
- PROPERTY INDEX statement
- computed columns, index creation
- clustered indexes, creating
- indexed views [SQL Server], index creation
- partitioned indexes [SQL Server], creating
- VALUE INDEX statement
- index creation [SQL Server], CREATE INDEX statement
- DROP_EXISTING clause
- row locks [SQL Server]
- composite indexes
- MAXDOP index option, CREATE INDEX statement
- filtered indexes [SQL Server], creating
- PATH INDEX statement
- locking [SQL Server], indexes
- unique indexes, creating
- primary indexes [SQL Server]
- CREATE PRIMARY XML INDEX statement
- SET statement, index creation
- index options [SQL Server]
- included columns
- ONLINE option
- nonclustered indexes [SQL Server], creating
- CREATE INDEX statement
- IGNORE_DUP_KEY option
- deterministic functions
- keys [SQL Server], index
- SECONDARY XML INDEX statement
- page locks [SQL Server]
- secondary indexes [SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: d2297805-412b-47b5-aeeb-53388349a5b9
author: pmasl
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ecba395399d758bbab2cae59ec4400554d3c665a
ms.sourcegitcommit: bd3a135f061e4a49183bbebc7add41ab11872bae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92300605"
---
# <a name="create-index-transact-sql"></a>CREATE INDEX(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

테이블 또는 뷰에 관계 인덱스를 만듭니다. 이 인덱스는 클러스터형 또는 비클러스터형 B-트리 인덱스이므로 rowstore 인덱스라고도 합니다. 테이블에 데이터가 채워지기 전에 rowstore 인덱스를 만들 수 있습니다. 특히 쿼리가 특정 열에서 값을 선택하거나 값을 특정 순서로 정렬해야 하는 경우 rowstore 인덱스를 사용하여 쿼리 성능을 개선할 수 있습니다.

> [!NOTE]
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 현재 Unique 제약 조건을 지원하지 않습니다. Unique 제약 조건을 참조하는 예제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에만 적용할 수 있습니다.
> [!TIP]
> 인덱스 디자인 지침에 대한 자세한 내용은 [SQL Server 인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

 **간단한 예제:**

```sql
-- Create a nonclustered index on a table or view
CREATE INDEX i1 ON t1 (col1);

-- Create a clustered index on a table and use a 3-part name for the table
CREATE CLUSTERED INDEX i1 ON d1.s1.t1 (col1);

-- Syntax for SQL Server and Azure SQL Database
-- Create a nonclustered index with a unique constraint
-- on 3 columns and specify the sort order for each column
CREATE UNIQUE INDEX i1 ON t1 (col1 DESC, col2 ASC, col3 DESC);
```

**주요 시나리오:**

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]부터 columnstore 인덱스에 비클러스터형 인덱스를 사용하여 데이터 웨어하우징 쿼리 성능을 개선할 수 있습니다. 자세한 내용은 [Columnstore 인덱스 - 데이터 웨어하우징](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)을 참조하세요.

추가 인덱스 형식은 다음을 참조하세요.

- [CREATE XML INDEX](../../t-sql/statements/create-xml-index-transact-sql.md)
- [CREATE SPATIAL INDEX](../../t-sql/statements/create-spatial-index-transact-sql.md)
- [CREATE COLUMNSTORE INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md)

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

### <a name="syntax-for-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에 대한 구문

```syntaxsql
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name
    ON <object> ( column [ ASC | DESC ] [ ,...n ] )
    [ INCLUDE ( column_name [ ,...n ] ) ]
    [ WHERE <filter_predicate> ]
    [ WITH ( <relational_index_option> [ ,...n ] ) ]
    [ ON { partition_scheme_name ( column_name )
         | filegroup_name
         | default
         }
    ]
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]
  
[ ; ]
  
<object> ::=
{ database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }

<relational_index_option> ::=
{
    PAD_INDEX = { ON | OFF }
  | FILLFACTOR = fillfactor
  | SORT_IN_TEMPDB = { ON | OFF }
  | IGNORE_DUP_KEY = { ON | OFF }
  | STATISTICS_NORECOMPUTE = { ON | OFF }
  | STATISTICS_INCREMENTAL = { ON | OFF }
  | DROP_EXISTING = { ON | OFF }
  | ONLINE = { ON | OFF }
  | RESUMABLE = { ON | OFF }
  | MAX_DURATION = <time> [MINUTES]
  | ALLOW_ROW_LOCKS = { ON | OFF }
  | ALLOW_PAGE_LOCKS = { ON | OFF }
  | OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF }
  | MAXDOP = max_degree_of_parallelism
  | DATA_COMPRESSION = { NONE | ROW | PAGE }
     [ ON PARTITIONS ( { <partition_number_expression> | <range> }
     [ , ...n ] ) ]
}

<filter_predicate> ::=
    <conjunct> [ AND <conjunct> ]

<conjunct> ::=
    <disjunct> | <comparison>

<disjunct> ::=
        column_name IN (constant ,...n)

<comparison> ::=
        column_name <comparison_op> constant

<comparison_op> ::=
    { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< }

<range> ::=
<partition_number_expression> TO <partition_number_expression>
```

### <a name="backward-compatible-relational-index"></a>이전 버전과 호환되는 관계형 인덱스

> [!IMPORTANT]
> 이전 버전과 호환되는 관계형 인덱스 구문 구조는 나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거됩니다.
> 새 개발 작업에서는 이 구문 구조를 사용하지 않도록 하고 현재 이 기능을 사용하는 애플리케이션은 수정하십시오.
> 대신 <relational_index_option>에서 지정된 구문 구조를 사용합니다.

```syntaxsql
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name
    ON <object> ( column_name [ ASC | DESC ] [ ,...n ] )
    [ WITH <backward_compatible_index_option> [ ,...n ] ]
    [ ON { filegroup_name | "default" } ]

<object> ::=
{
    [ database_name. [ owner_name ] . | owner_name. ]
    table_or_view_name
}

<backward_compatible_index_option> ::=
{
    PAD_INDEX
  | FILLFACTOR = fillfactor
  | SORT_IN_TEMPDB
  | IGNORE_DUP_KEY
  | STATISTICS_NORECOMPUTE
  | DROP_EXISTING
}
```

### <a name="syntax-for-azure-synapse-analytics-and-parallel-data-warehouse"></a>Azure Synapse Analytics 및 병렬 데이터 웨어하우스용 구문

```syntaxsql

CREATE CLUSTERED COLUMNSTORE INDEX index_name
    ON [ database_name . [ schema ] . | schema . ] table_name
    [ORDER (column[,...n])]
    [WITH ( DROP_EXISTING = { ON | OFF } )]
[;]


CREATE [ CLUSTERED | NONCLUSTERED ] INDEX index_name
    ON [ database_name . [ schema ] . | schema . ] table_name
        ( { column [ ASC | DESC ] } [ ,...n ] )
    WITH ( DROP_EXISTING = { ON | OFF } )
[;]


```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

UNIQUE      
테이블 또는 뷰에 고유 인덱스를 만듭니다. 고유 인덱스는 두 개의 행에 동일한 인덱스 키 값을 가질 수 없습니다. 뷰의 클러스터형 인덱스는 고유해야 합니다.

IGNORE_DUP_KEY가 ON으로 설정되어 있는지 여부에 관계없이 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 이미 중복 값이 들어 있는 열에 고유 인덱스를 만들 수 없습니다. 이 작업을 시도하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 오류 메시지를 표시합니다. 열에 고유 인덱스를 만들려면 먼저 중복 값을 제거해야 합니다. 고유 인덱스를 만들 때 여러 개의 Null 값은 중복 값으로 취급되므로 고유 인덱스에서 사용되는 열은 NOT NULL로 설정해야 합니다.

CLUSTERED      
키 값의 논리적 순서가 테이블에 있는 해당 행의 물리적 순서를 결정하는 인덱스를 만듭니다. 클러스터형 인덱스의 최하위 수준인 리프 수준에는 테이블의 실제 데이터 행이 있습니다. 테이블 또는 뷰는 한 번에 클러스터형 인덱스 하나만 허용합니다.

고유 클러스터형 인덱스가 있는 뷰를 인덱싱된 뷰라고 합니다. 뷰에서 고유 클러스터형 인덱스를 만들면 물리적으로 뷰를 구체화합니다. 같은 뷰에 다른 인덱스를 정의하려면 먼저 고유 클러스터형 인덱스를 만들어야 합니다. 자세한 내용은 [인덱싱된 뷰 만들기](../../relational-databases/views/create-indexed-views.md)를 참조하세요.

비클러스터형 인덱스를 만들기 전에 항상 클러스터형 인덱스를 만듭니다. 테이블에 있는 기존의 비클러스터형 인덱스는 클러스터형 인덱스를 만들 때 다시 작성됩니다.

`CLUSTERED`를 지정하지 않으면 비클러스터형 인덱스가 만들어집니다.

> [!NOTE]
> 클러스터형 인덱스의 리프 수준과 데이터 페이지는 정의에 의해 동일하므로, 클러스터형 인덱스를 만들고 ON *partition_scheme_name* 또는 ON *filegroup_name* 절을 사용하면 결과적으로 테이블을 만든 파일 그룹의 테이블이 새 파티션 구성표 또는 파일 그룹으로 이동하게 됩니다. 특정 파일 그룹에서 테이블이나 인덱스를 만들기 전에 사용 가능한 파일 그룹과 인덱스를 만들 공간이 충분한지 확인합니다.

일부 경우 클러스터형 인덱스를 만들면 이전에 비활성화된 인덱스를 사용할 수 있습니다. 자세한 내용은 [인덱스 및 제약 조건 활성화](../../relational-databases/indexes/enable-indexes-and-constraints.md) 및 [인덱스 및 제약 조건 비활성화](../../relational-databases/indexes/disable-indexes-and-constraints.md)를 참조하세요.

NONCLUSTERED      
테이블의 논리적 순서를 지정하는 인덱스를 만듭니다. 비클러스터형 인덱스에서는 데이터 행의 물리적 순서가 인덱싱된 순서와 다릅니다.

각 테이블에는 비클러스터형 인덱스를 PRIMARY KEY와 UNIQUE 제약 조건을 사용하여 암시적으로 만들거나 CREATE INDEX를 사용하여 명시적으로 만드는 방법에 관계없이 999개까지 만들 수 있습니다.

인덱싱된 뷰의 경우 비클러스터형 인덱스는 이미 고유 클러스터형 인덱스가 정의되어 있는 뷰에서만 만들 수 있습니다.

달리 지정하지 않으면 기본 인덱스 유형은 NONCLUSTERED입니다.

*index_name*      
 인덱스의 이름입니다. 인덱스 이름은 테이블이나 뷰에서 고유해야 하지만 데이터베이스 내에서 고유할 필요는 없습니다. 인덱스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.

*열*      
 인덱스의 기준이 되는 열입니다. 지정된 열에 있는 결합된 값에 복합 인덱스를 만들려면 두 개 이상의 열 이름을 지정합니다. 복합 인덱스에 포함할 열을 *table_or_view_name* 다음의 괄호 안에 정렬 우선 순위 순서대로 나열합니다.

단일 복합 인덱스 키에 최대 32개의 열을 결합할 수 있으며 복합 인덱스 키의 모든 열은 동일한 테이블 또는 뷰에 있어야 합니다. 결합된 인덱스 값의 최대 허용 크기는 클러스터형 인덱스의 경우 900바이트, 비클러스터형 인덱스의 경우 1,700바이트입니다. 한도는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이전 버전의 경우 16열 및 900바이트입니다.

큰 개체(LOB) 데이터 형식 **ntext** , **text** , **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml** 또는 **image** 인 열은 인덱스의 키 열로 지정할 수 없습니다. 또한 CREATE INDEX 문에 참조되지 않은 경우에도 뷰 정의에 **ntext** , **text** 또는 **image** 열을 포함할 수 없습니다.

이진 순서를 지원하는 CLR 사용자 정의 형식 열에 인덱스를 만들 수 있습니다. 메서드가 결정적으로 표시되고 데이터 액세스 작업을 수행하지 않는 동안 사용자 정의 형식 열의 메서드 호출로 정의된 계산 열에 인덱스를 만들 수도 있습니다. CLR 사용자 정의 형식 열을 인덱싱하는 방법은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.

[ **ASC** | DESC ]      
특정 인덱스 열의 정렬 방향을 오름차순 또는 내림차순으로 지정합니다. 기본값은 ASC입니다.

INCLUDE **(** _column_ [ **,** ... *n* ] **)**       
비클러스터형 인덱스의 리프 수준에 키가 아닌 열을 추가하도록 지정합니다. 비클러스터형 인덱스는 고유하거나 고유하지 않을 수 있습니다.

열 이름을 INCLUDE 목록에 반복 사용할 수 없으며 키 열과 키가 아닌 열로 동시에 사용할 수 없습니다. 클러스터형 인덱스가 테이블에 정의되어 있으면 비클러스터형 인덱스는 항상 클러스터형 인덱스 열을 포함합니다. 자세한 내용은 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)을 참조하세요.

**text** , **ntext** 및 **image** 를 제외한 모든 데이터 형식을 사용할 수 있습니다. 지정된 키가 아닌 열 중 하나가 **varchar(max)** , **nvarchar(max)** 또는 **varbinary(max)** 데이터 형식인 경우 인덱스를 오프라인으로 만들거나 다시 만들어야 합니다(ONLINE = OFF).

결정적이면서 정확하거나 정확하지 않은 계산 열은 포괄 열이 될 수 있습니다. **image** , **ntext** , **text** , **varchar(max)** , **nvarchar(max)** , **varbinary(max)** 및 **xml** 데이터 형식에서 파생된 계산된 열은 해당 계산된 열 데이터 형식이 포함된 열로 허용된다면 키가 아닌 열에 포함할 수 있습니다. 자세한 내용은 [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md)을 참조하세요.

XML 인덱스 만들기에 대한 자세한 내용은 [CREATE XML INDEX](../../t-sql/statements/create-xml-index-transact-sql.md)를 참조하세요.

WHERE \<filter_predicate>      
인덱스에 포함할 행을 지정하여 필터링된 인덱스를 만듭니다. 필터링된 인덱스는 테이블의 비클러스터형 인덱스여야 합니다. 필터링된 인덱스의 데이터 행에 대한 필터링된 통계를 만듭니다.

필터 조건자는 간단한 비교 논리를 사용하며 계산 열, UDT 열, 공간 데이터 형식 열 또는 HierarchyID 데이터 형식 열을 참조할 수 없습니다. 비교 연산자에는 NULL 리터럴을 사용한 비교를 사용할 수 없습니다. 대신 IS NULL 및 IS NOT NULL 연산자를 사용합니다.

다음은 `Production.BillOfMaterials` 테이블에 대한 필터 조건자의 몇 가지 예입니다.

```sql
WHERE StartDate > '20000101' AND EndDate <= '20000630'

WHERE ComponentID IN (533, 324, 753)

WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL
```

필터링된 인덱스는 XML 인덱스 및 전체 텍스트 인덱스에는 적용되지 않습니다. UNIQUE 인덱스의 경우에는 선택한 행만 고유 인덱스 값을 가져야 합니다. 필터링된 인덱스에서는 IGNORE_DUP_KEY 옵션이 허용되지 않습니다.

ON *partition_scheme_name* **( _column_name_ )**      

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

분할된 인덱스의 파티션이 매핑될 파일 그룹을 정의하는 파티션 구성표를 지정합니다. 파티션 구성표는 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) 또는 [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)의 실행을 통해 데이터베이스 내에 있어야 합니다. *column_name* 은 분할된 인덱스가 분할되는 기준으로 사용할 열을 지정합니다. 이 열은 *partition_scheme_name* 에서 사용하는 파티션 함수의 인수와 데이터 형식, 길이 및 전체 자릿수가 일치해야 합니다. *column_name* 은 인덱스 정의의 열만 사용할 필요는 없으며 기본 테이블의 모든 열을 지정할 수 있습니다. 단, UNIQUE 인덱스를 분할할 때 고유 키로 사용되는 열 중에서 *column_name* 을 선택해야 하는 경우는 제외합니다. 이 제한 사항으로 인해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 단일 파티션 내에서만 키 값의 고유성을 확인할 수 있습니다.

> [!NOTE]
> 비고유 클러스터형 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 기본적으로 지정되지 않은 분할 열을 클러스터형 인덱스 키 목록에 추가합니다. 비고유 비클러스터형 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 지정되지 않은 분할 열을 인덱스의 키가 아닌 포괄 열로 추가합니다.

_partition_scheme_name_ 또는 _filegroup_ 이 지정되지 않고 테이블이 분할된 경우 인덱스는 동일한 분할 열을 사용하여 동일한 파티션 구성표에 기본 테이블로 배치됩니다.

> [!NOTE]
> XML 인덱스에서 파티션 구성표를 지정할 수 없습니다. 기본 테이블이 분할되면 XML 인덱스는 테이블과 동일한 파티션 구성표를 사용합니다.

분할 인덱스에 대한 자세한 내용은 [분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.

ON _filegroup_name_      

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상).

주어진 파일 그룹에 지정된 인덱스를 만듭니다. 지정된 위치가 없고 테이블 또는 뷰가 분할되지 않은 경우 인덱스는 동일한 파일 그룹을 기본 테이블 또는 뷰로 사용합니다. 파일 그룹은 이미 존재해야 합니다.

ON **"** default **"**      

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

테이블 또는 보기와 동일한 파일 그룹 또는 파티션 구성표에 지정된 인덱스를 만듭니다.

이 컨텍스트에서 default는 키워드가 아닙니다. 이것은 기본 파일 그룹에 대한 식별자이며 ON **"** default **"** 또는 ON **[** default **]** 와 같이 구분되어야 합니다. "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.

> [!NOTE]
> "default"는 CREATE INDEX의 컨텍스트에서 데이터베이스 기본 파일 그룹을 나타내지 않습니다. 이는 CREATE TABLE과 다르며, 여기서 "default"는 데이터베이스 기본 파일 그룹에서 테이블을 찾습니다.

[ FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL" } ]      

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상).

클러스터형 인덱스를 만들 때 테이블에 대한 FILESTREAM 데이터의 위치를 지정합니다. FILESTREAM_ON 절에서 FILESTREAM 데이터를 다른 FILESTREAM 파일 그룹 또는 파티션 구성표로 이동할 수 있습니다.

_filestream_filegroup_name_ 은 FILESTREAM 파일 그룹의 이름입니다. 파일 그룹에는 [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md) 또는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 파일 그룹에 대해 정의된 파일이 하나 포함되어야 하며, 그렇지 않으면 오류가 발생합니다.

테이블이 분할된 경우에는 FILESTREAM_ON 절이 포함되어야 하며 이 절에서 테이블의 파티션 구성표와 동일한 파티션 함수 및 파티션 열을 사용하는 FILESTREAM 파일 그룹의 파티션 구성표를 지정해야 합니다. 그렇지 않으면 오류가 발생합니다.

테이블이 분할되지 않은 경우에는 FILESTREAM 열을 분할할 수 없습니다. 테이블의 FILESTREAM 데이터는 FILESTREAM_ON 절에 지정된 단일 파일 그룹에 저장되어야 합니다.

클러스터형 인덱스가 생성되고 테이블에 FILESTREAM 열이 포함되지 않은 경우 CREATE INDEX 문에 `FILESTREAM_ON NULL`을 지정할 수 있습니다.

자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.

**\<object>::=**      

인덱스할 정규화되거나 정규화되지 않은 개체입니다.

_database_name_      
데이터베이스의 이름입니다.

*schema_name*      
테이블이나 뷰가 속한 스키마의 이름입니다.

*table_or_view_name*      
인덱싱할 테이블 또는 뷰의 이름입니다.

인덱스를 만들 뷰는 SCHEMABINDING으로 정의되어야 합니다. 뷰에 비클러스터형 인덱스를 만들려면 먼저 고유 클러스터형 인덱스를 만들어야 합니다. 인덱싱된 뷰에 대한 자세한 내용은 주의 섹션을 참조하세요.

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 개체는 클러스터형 columnstore 인덱스와 함께 저장된 테이블일 수 있습니다.

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 세 부분으로 구성된 이름 형식( _database_name_ .[ _schema_name_ ]. _object_name_ )을 지원합니다. 단, *database_name* 이 현재 데이터베이스이거나 _database_name_ 이 `tempdb`이고 _object_name_ 이 #으로 시작해야 합니다.

**\<relational_index_option\>::=**       
인덱스를 만들 때 사용할 옵션을 지정합니다.

PAD_INDEX = { ON | **OFF** }      

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

인덱스 패딩을 지정합니다. 기본값은 OFF입니다.

켜기      
*fillfactor* 로 지정된 사용 가능한 공간의 비율이 인덱스의 중간 수준 페이지에 적용됩니다.

OFF 또는 _fillfactor_ 를 지정되지 않음      
중간 수준 페이지는 중간 페이지의 키 집합을 고려하며 인덱스가 가질 수 있는 최대 크기의 한 행에 필요한 공간을 충분히 남기고 용량을 거의 채웁니다.

PAD_INDEX는 FILLFACTOR에 지정된 비율을 사용하므로 FILLFACTOR가 지정된 경우에만 PAD_INDEX 옵션을 사용할 수 있습니다. FILLFACTOR에 지정된 비율이 한 행을 저장하기에도 부족하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 내부적으로 허용된 최소 비율을 무시합니다. _fillfactor_ 값이 아무리 작더라도 중간 인덱스 페이지의 행 수는 두 개 이상입니다.

이전 버전과 호환되는 구문에서 WITH PAD_INDEX는 WITH PAD_INDEX = ON과 같습니다.

FILLFACTOR **=** _fillfactor_      

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

인덱스를 만들거나 다시 작성할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. *fillfactor* 는 1에서 100 사이의 정수 값이어야 하며 *fillfactor* 가 100이면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]는 리프 페이지가 꽉 찬 인덱스를 만듭니다.

FILLFACTOR 설정은 인덱스를 만들거나 다시 작성하는 경우에만 적용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 페이지에 지정된 비율의 빈 공간을 동적으로 유지하지 않습니다. 채우기 비율 설정을 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 사용하세요.

> [!IMPORTANT]
> [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 클러스터형 인덱스를 만들 때 데이터를 다시 배포하므로 FILLFACTOR가 100 미만인 클러스터형 인덱스를 만들면 데이터가 차지하는 스토리지 공간 크기에 영향을 줍니다.

자세한 내용은 [인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)을 참조하세요.

SORT_IN_TEMPDB = { ON | **OFF** }      

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

**tempdb** 에 임시 정렬 결과를 저장할지 여부를 지정합니다. Azure SQL Database 하이퍼스케일을 제외하고 기본값은 OFF입니다. 하이퍼스케일의 모든 인덱스 작성 작업에서는, 다시 시작 가능한 인덱스 재작성을 사용하지 않을 경우 지정된 옵션에 관계없이 SORT_IN_TEMPDB가 항상 ON입니다.

켜기      
인덱스 작성에 사용된 중간 정렬 결과가 **tempdb** 에 저장됩니다. 이 경우 사용자 데이터베이스가 아닌 다른 디스크 집합에 **tempdb** 가 있으면 인덱스 생성에 필요한 시간이 단축될 수 있습니다. 그러나 인덱스 작성 중에 사용되는 디스크 공간의 크기는 커집니다.

OFF      
중간 정렬 결과가 인덱스와 같은 데이터베이스에 저장됩니다.

사용자 데이터베이스에서 인덱스를 만드는 데 필요한 공간 외에 **tempdb** 에는 중간 정렬 결과를 저장할 정도의 동일한 공간이 추가로 필요합니다. 자세한 내용은 [인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)을 참조하세요.

이전 버전과 호환되는 구문에서 WITH SORT_IN_TEMPDB는 WITH SORT_IN_TEMPDB = ON과 같습니다.

IGNORE_DUP_KEY = { ON | **OFF** }      
삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려는 경우에 대한 오류 응답을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) 또는 [UPDATE](../../t-sql/queries/update-transact-sql.md)를 실행하는 경우에는 이 옵션이 아무런 영향을 미치지 않습니다. 기본값은 OFF입니다.

켜기      
중복된 키 값이 고유 인덱스에 삽입되는 경우 경고 메시지가 나타나고 고유성 제약 조건을 위반하는 행만 실패합니다.

OFF      
중복된 키 값이 고유 인덱스에 삽입되는 경우 오류 메시지가 나타나고 전체 INSERT 작업이 롤백됩니다.

뷰, 비고유 인덱스, XML 인덱스, 공간 인덱스 및 필터링된 인덱스에 생성된 인덱스의 경우 IGNORE_DUP_KEY를 ON으로 설정할 수 없습니다.

IGNORE_DUP_KEY를 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)를 사용하세요.

이전 버전과 호환되는 구문에서 WITH IGNORE_DUP_KEY는 WITH IGNORE_DUP_KEY = ON과 같습니다.

STATISTICS_NORECOMPUTE = { ON | **OFF** }      
배포 통계를 다시 계산할지 여부를 지정합니다. 기본값은 OFF입니다.

켜기      
이전 통계가 자동으로 다시 계산되지 않습니다.

OFF      
자동 통계 업데이트가 설정됩니다.

자동 통계 업데이트를 복원하려면 STATISTICS_NORECOMPUTE를 OFF로 설정하거나 NORECOMPUTE 절 없이 UPDATE STATISTICS를 실행합니다.

> [!IMPORTANT]
> 배포 통계 자동 재계산 기능을 해제하면 쿼리 최적화 프로그램에서 테이블과 관련된 쿼리에 대해 최적의 실행 계획을 선택할 수 없습니다.

이전 버전과 호환되는 구문에서 WITH STATISTICS_NORECOMPUTE는 WITH STATISTICS_NORECOMPUTE = ON과 같습니다.

STATISTICS_INCREMENTAL = { ON | **OFF** }     

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

**ON** 으로 설정된 경우 파티션 통계별로 통계가 작성됩니다. **OFF** 로 설정된 경우 통계 트리가 삭제되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 통계를 다시 계산합니다. 기본값은 **OFF** 입니다.

파티션별 통계가 지원되지 않는 경우에는 이 옵션이 무시되고 경고가 생성됩니다. 다음 통계 유형에 대해서는 증분 통계가 지원되지 않습니다.

- 기본 테이블을 기준으로 파티션 정렬되지 않은 인덱스를 사용하여 작성된 통계입니다.
- Always On 읽기 가능한 보조 데이터베이스에 대해 작성된 통계입니다.
- 읽기 전용 데이터베이스에 대해 작성된 통계입니다.
- 필터링된 인덱스에 대해 작성된 통계입니다.
- 뷰에 대해 작성된 통계입니다.
- 내부 테이블에 대해 작성된 통계입니다.
- 공간 인덱스 또는 XML 인덱스를 사용하여 작성된 통계입니다.

DROP_EXISTING = { ON | **OFF** }      
수정된 열 사양을 사용하여 기존 클러스터형 또는 비클러스터형 인덱스를 삭제하고 다시 만들며 인덱스 이름을 동일하게 유지하는 옵션입니다. 기본값은 OFF입니다.

켜기      
기존 인덱스를 삭제하고 다시 만들도록 지정하며, 이름은 *index_name* 매개 변수와 같아야 합니다.

OFF      
기존 인덱스를 삭제하고 다시 만들지 않도록 지정합니다. 지정된 인덱스 이름이 이미 존재하는 경우 SQL Server 오류가 표시됩니다.

DROP_EXISTING을 사용하여 다음을 변경할 수 있습니다.

- 비클러스터형 rowstore 인덱스를 클러스터형 rowstore 인덱스로.

DROP_EXISTING을 사용하여 다음을 변경할 수 없습니다.

- 클러스터형 rowstore 인덱스를 비클러스터형 rowstore 인덱스로.
- 클러스터형 columnstore 인덱스를 임의 형식의 rowstore 인덱스로.

이전 버전과 호환되는 구문에서 WITH DROP_EXISTING은 WITH DROP_EXISTING = ON과 같습니다.

ONLINE = { ON | **OFF** }      
인덱스 작업 중 쿼리 및 데이터 수정에 기본 테이블과 관련 인덱스를 사용할 수 있는지 여부를 지정합니다. 기본값은 OFF입니다.

> [!IMPORTANT]
> 온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2016.md)을 참조하세요.

켜기      
인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 작업의 주 단계 중 내재된 공유(IS) 잠금만 원본 테이블에 유지됩니다. 따라서 기본 테이블 및 인덱스에 대한 쿼리나 업데이트를 처리할 수 있습니다. 작업이 시작되면 아주 짧은 기간 동안 S(공유) 잠금이 원본 개체에 유지됩니다. 작업이 끝나면 짧은 기간 동안 비클러스터형 인덱스가 생성되는 경우에는 원본에 대해 S(공유) 잠금이 획득되고, 온라인 상태에서 클러스터형 인덱스가 생성 또는 삭제될 때와 클러스터형 또는 비클러스터형 인덱스가 다시 작성될 때는 SCH-M(스키마 수정) 잠금이 획득됩니다. 로컬 임시 테이블에서 인덱스를 생성하는 경우에는 ONLINE을 ON으로 설정할 수 없습니다.

OFF      
인덱스 작업 중에 테이블 잠금이 적용됩니다. 클러스터형 인덱스를 생성, 다시 작성 또는 삭제하거나 비클러스터형 인덱스를 다시 작성 또는 삭제하는 오프라인 인덱스 작업을 통해 테이블의 SCH-M(스키마 수정) 잠금을 획득합니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다. 비클러스터형 인덱스를 만드는 오프라인 인덱스 작업을 통해 테이블의 S(공유) 잠금을 획득합니다. 따라서 기본 테이블을 업데이트할 수 없지만 SELECT 문과 같은 읽기 작업은 허용됩니다.

자세한 내용은 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요.  

전역 임시 테이블의 인덱스를 비롯한 인덱스를 온라인으로 만들 수 있습니다. 단, 다음 사례는 예외입니다.

- XML 인덱스
- 로컬 임시 테이블의 인덱스
- 뷰의 초기 고유 클러스터형 인덱스
- 사용하지 않도록 설정된 클러스터형 인덱스
- columnstore 인덱스
- 기본 테이블이 LOB 데이터 형식( **image** , **ntext** , **text** ) 및 공간 데이터 형식을 포함하는 경우 클러스터형 인덱스입니다.
- **varchar(max)** 및 **varbinary(max)** 열은 인덱스의 일부일 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 테이블에 **varchar(최대)** 또는 **varbinary(최대)** 열이 포함된 경우 **ONLINE** 옵션을 사용하여 다른 열을 포함하는 클러스터형 인덱스를 빌드하거나 다시 빌드할 수 있습니다. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 기본 테이블에 **varchar(최대)** 또는 **varbinary(최대)** 열이 포함된 경우 **ONLINE** 옵션을 허용하지 않습니다.

자세한 내용은 [온라인 인덱스 작업의 작동 원리](../../relational-databases/indexes/how-online-index-operations-work.md)를 참조하세요.

RESUMABLE **=** { ON | **OFF** }      

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

 온라인 인덱스 작업이 다시 시작될 수 있는지 여부를 지정합니다.

 켜기      
인덱스 작업이 다시 시작될 수 있습니다.

 OFF      
인덱스 작업이 다시 시작될 수 없습니다.

MAX_DURATION **=** *time* [ **MINUTES** ]는 **RESUMABLE = ON** 상태에서 사용됩니다( **ONLINE = ON** 필요).   

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

다시 시작할 수 있는 온라인 인덱스 작업이 일시 중지하기 전에 실행된 시간을 나타냅니다(분 단위로 지정된 정수 값).

> [!IMPORTANT]
> 온라인으로 수행할 수 있는 인덱스 작업에 대한 자세한 내용은 [온라인 인덱스 작업 지침](../../relational-databases/indexes/guidelines-for-online-index-operations.md)을 참조하세요.

> [!NOTE] 
> columnstore 인덱스에서는 다시 시작 가능한 온라인 인덱스 다시 빌드가 지원되지 않습니다.

ALLOW_ROW_LOCKS = { **ON** | OFF }      
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.

켜기      
인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.

OFF      
행 잠금이 사용되지 않습니다.

ALLOW_PAGE_LOCKS = { **ON** | OFF }      
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.

켜기      
인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.

OFF      
페이지 잠금이 사용되지 않습니다.

OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | **OFF** }      
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

마지막 페이지 삽입 경합에 최적화할지 여부를 지정합니다. 기본값은 OFF입니다. 자세한 내용은 [순차 키](#sequential-keys) 섹션을 참조하세요.

MAXDOP = *max_degree_of_parallelism*      
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

인덱스 작업 기간 동안 **max degree of parallelism** 구성 옵션을 재정의합니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.

*max_degree_of_parallelism* 은 다음 중 하나일 수 있습니다.

1      
병렬 계획이 생성되지 않습니다.

\>1      
병렬 인덱스 작업에 사용되는 최대 프로세서 수를 현재 시스템 작업에 따라 지정된 수 또는 더 적은 수로 제한합니다.

0(기본값)      
현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.

 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.

> [!NOTE]
> 병렬 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016에 대한 버전 및 지원되는 기능](../../sql-server/editions-and-components-of-sql-server-2016.md) 및 [SQL Server 2017에 대한 버전 및 지원되는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.

DATA_COMPRESSION      
지정된 인덱스, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 옵션은 다음과 같습니다.

없음      
인덱스 또는 지정된 파티션이 압축되지 않습니다.

ROW      
인덱스 또는 지정된 파티션이 행 압축을 사용하여 압축됩니다.

PAGE      
인덱스 또는 지정된 파티션이 페이지 압축을 사용하여 압축됩니다.

압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.

ON PARTITIONS **(** { \<partition_number_expression> | \<range> } [ **,** ... _n_ ] **)**       
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

DATA_COMPRESSION 설정을 적용할 파티션을 지정합니다. 인덱스가 분할되지 않은 경우 ON PARTITIONS 인수를 사용하면 오류가 발생합니다. ON PARTITIONS 절을 제공하지 않으면 DATA_COMPRESSION 옵션이 분할된 인덱스의 모든 파티션에 적용됩니다.

\<partition_number_expression>은 다음과 같은 방법으로 지정할 수 있습니다.

- 파티션의 번호를 지정합니다. 예를 들면 다음과 같습니다. ON PARTITIONS(2).
- 여러 개별 파티션의 파티션 번호를 쉼표로 구분하여 지정합니다. 예를 들면 다음과 같습니다. ON PARTITIONS(1, 5).
- 범위와 개별 파티션을 모두 지정합니다. 예를 들면 다음과 같습니다. ON PARTITIONS(2, 4, 6~8).

\<range>는 TO라는 단어로 구분된 파티션 번호로 지정할 수 있습니다(예: `ON PARTITIONS (6 TO 8)`).

 여러 파티션에 대해 서로 다른 데이터 압축 유형을 설정하려면 DATA_COMPRESSION 옵션을 두 번 이상 지정합니다. 예를 들면 다음과 같습니다.

```sql
REBUILD WITH
(
  DATA_COMPRESSION = NONE ON PARTITIONS (1),
  DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),
  DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)
);
```

## <a name="remarks"></a>설명
CREATE INDEX 문은 다른 쿼리와 마찬가지로 최적화됩니다. I/O 작업을 줄이기 위해 쿼리 프로세서에서 테이블 검색을 수행하는 대신 다른 인덱스를 검색하도록 선택할 수도 있습니다. 정렬 작업을 제거해야 하는 경우도 있습니다. 다중 프로세서 컴퓨터에서 CREATE INDEX는 다른 쿼리에서 수행하는 것과 같은 방법으로 더 많은 프로세서를 사용하여 인덱스 만들기와 관련된 스캔 및 정렬 작업을 수행할 수 있습니다. 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.

데이터베이스 복구 모델이 대량 로그 또는 단순으로 설정된 경우 인덱스 생성 작업은 최소로 기록될 수 있습니다.

임시 테이블에 인덱스를 만들 수 있습니다. 테이블이 삭제되거나 세션이 종료되면 인덱스가 삭제됩니다.

기본 키가 생성될 때 테이블 변수에 클러스터형 인덱스를 빌드할 수 있습니다. 쿼리가 완료되거나 세션이 종료되면 인덱스가 삭제됩니다.

인덱스는 확장 속성을 지원합니다.

## <a name="clustered-indexes"></a>클러스터형 인덱스
테이블(힙)에 클러스터형 인덱스를 만들거나 기존 클러스터형 인덱스를 삭제하고 다시 만들려면 데이터베이스에서 데이터 정렬 및 원본 테이블의 임시 사본이나 기존 클러스터형 인덱스 데이터의 임시 사본을 보관할 수 있는 추가 작업 영역이 필요합니다. 클러스터형 인덱스에 대한 자세한 내용은 [클러스터형 인덱스 만들기](../../relational-databases/indexes/create-clustered-indexes.md) 및 [SQL Server 인덱스 아키텍처 및 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

## <a name="nonclustered-indexes"></a>비클러스터형 인덱스
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터, 그리고 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서는 클러스터형 columnstore 인덱스로 저장된 테이블에 비클러스터형 인덱스를 만들 수 있습니다. 힙 또는 클러스터형 인덱스로 저장된 테이블에 비클러스터형 인덱스를 먼저 만드는 경우, 나중에 테이블을 클러스터형 columnstore 인덱스로 변환하면 인덱스가 유지됩니다. 또한 클러스터형 columnstore 인덱스를 다시 작성할 때 비클러스터형 인덱스를 삭제하지 않아도 됩니다.

제한 사항:

- `FILESTREAM_ON` 옵션은 클러스터형 columnstore 인덱스로 저장된 테이블에 비클러스터형 인덱스를 만드는 경우 유효하지 않습니다.

## <a name="unique-indexes"></a>고유 인덱스
고유 인덱스가 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 삽입 작업으로 데이터를 추가할 때마다 중복 값이 있는지 확인합니다. 중복 키 값을 생성하는 삽입 작업은 롤백되며 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 오류 메시지를 표시합니다. 이런 현상은 삽입 작업을 통해 많은 행을 변경할 때 중복 값이 하나만 있어도 발생합니다. 고유 인덱스가 있고 IGNORE_DUP_KEY 절이 ON으로 설정된 경우 데이터를 입력하려고 하면 UNIQUE 인덱스를 위반하는 행만 실패합니다.

## <a name="partitioned-indexes"></a>분할된 인덱스
분할된 인덱스는 분할된 테이블과 비슷한 방법으로 만들어지며 유지 관리됩니다. 그러나 보통 인덱스와 같이 별도의 데이터베이스 개체로 처리됩니다. 분할되지 않은 테이블에 분할된 인덱스가 있을 수 있으며 분할된 테이블에 분할되지 않은 인덱스가 있을 수 있습니다.

분할된 테이블에 인덱스를 만들고 인덱스를 배치할 파일 그룹을 지정하지 않으면 인덱스는 기본 테이블과 같은 방법으로 분할됩니다. 이렇게 되는 이유는 기본적으로 인덱스가 기본 테이블처럼 동일한 파일 그룹에 배치되고 동일한 분할 열을 사용하는 동일한 파티션 구성표의 분할된 테이블에 대해 배치되기 때문입니다. 인덱스에 테이블과 동일한 파티션 구성표 및 분할 열을 사용하는 경우 인덱스는 테이블과 함께 *정렬* 됩니다.

> [!WARNING]
> 파티션 수가 1,000개를 초과하는 테이블에서 정렬되지 않은 인덱스를 만들거나 다시 작성할 수 있지만 해당 인덱스는 지원되지 않습니다. 그러면 작업 중에 성능이 저하되거나 메모리가 과도하게 소비될 수 있습니다. 파티션 수가 1,000개를 초과하는 경우에는 정렬된 인덱스만 사용하는 것이 좋습니다.

비고유 클러스터형 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 기본적으로 지정되지 않은 모든 분할 열을 클러스터형 인덱스 키 목록에 추가합니다.

인덱싱된 뷰는 테이블의 인덱스와 같은 방법으로 분할된 테이블에 만들 수 있습니다. 분할 인덱스에 대한 자세한 내용은 [분할 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md) 및 [SQL Server 인덱스 아키텍처 및 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 분할된 인덱스를 만들거나 다시 작성할 때 테이블의 모든 행을 검사하여 통계를 작성하지 않습니다. 대신 쿼리 최적화 프로그램에서 기본 샘플링 알고리즘을 사용하여 통계를 생성합니다. 테이블의 모든 행을 검사하여 분할된 인덱스에 대한 통계를 얻으려면 `FULLSCAN` 절에서 `CREATE STATISTICS` 또는 `UPDATE STATISTICS`를 사용합니다.

## <a name="filtered-indexes"></a>필터링된 인덱스
필터링된 인덱스는 테이블에서 적은 비율의 행을 선택하는 쿼리에 적합한 최적화된 비클러스터형 인덱스입니다. 이 인덱스에서는 필터 조건자를 사용하여 테이블의 일부 데이터를 인덱싱합니다. 잘 디자인된 필터링된 인덱스는 쿼리 성능을 개선하고 스토리지 비용과 유지 관리 비용을 줄일 수 있습니다.

### <a name="required-set-options-for-filtered-indexes"></a>필터링된 인덱스에 필요한 SET 옵션

다음 조건이 발생할 때마다 필요한 값 열에 SET 옵션을 사용해야 합니다.

- 필터링된 인덱스를 만듭니다.
- INSERT, UPDATE, DELETE 또는 MERGE 작업으로 필터링된 인덱스의 데이터를 수정합니다.
- 필터링된 인덱스는 쿼리 최적화 프로그램이 쿼리 계획을 작성할 때 사용됩니다.

    |Set 옵션|필수 값|기본 서버 값|기본값<br /><br /> OLE DB 및 ODBC 값|기본값<br /><br /> DB-Library 값|
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|
    |ANSI_NULLS|켜기|켜기|켜기|OFF|
    |ANSI_PADDING|켜기|켜기|켜기|OFF|
    |ANSI_WARNINGS*|켜기|켜기|켜기|OFF|
    |ARITHABORT|켜기|켜기|OFF|OFF|
    |CONCAT_NULL_YIELDS_NULL|켜기|켜기|켜기|OFF|
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|
    |QUOTED_IDENTIFIER|켜기|켜기|켜기|OFF|
  
     * 데이터베이스 호환성 수준이 90 이상으로 설정된 경우 ANSI_WARNINGS를 ON으로 설정하면 암시적으로 ARITHABORT가 ON으로 설정됩니다. 데이터베이스 호환성 수준이 80 이하로 설정된 경우에는 명시적으로 ARITHABORT 옵션을 ON으로 설정해야 합니다.

SET 옵션이 올바르지 않은 경우 다음 조건이 발생할 수 있습니다.

- 필터링된 인덱스가 만들어지지 않습니다.
- [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류를 생성하고 인덱스의 데이터를 변경하는 INSERT, UPDATE, DELETE 또는 MERGE 문을 롤백합니다.
- 쿼리 최적화 프로그램에서 Transact-SQL 문의 실행 계획에 있는 인덱스를 고려하지 않습니다.

 필터링된 인덱스에 대한 자세한 내용은 [필터링된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md) 및 [SQL Server 인덱스 아키텍처 및 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

## <a name="spatial-indexes"></a>공간 인덱스
공간 인덱스에 대한 자세한 내용은 [CREATE SPATIAL INDEX](../../t-sql/statements/create-spatial-index-transact-sql.md) 및 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.

## <a name="xml-indexes"></a>XML 인덱스
XML 인덱스에 대한 자세한 내용은 [CREATE XML INDEX](../../t-sql/statements/create-xml-index-transact-sql.md) 및 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)를 참조하세요.

## <a name="index-key-size"></a>인덱스 키 크기
인덱스 키의 최대 크기는 클러스터형 인덱스의 경우 900바이트, 비클러스터형 인덱스의 경우 1,700바이트입니다. ([!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이전의 한도는 항상 900바이트였습니다.) 인덱스가 만들어질 때 바이트 한도를 초과하는 **varchar** 열의 기존 데이터가 한도를 초과하지 않는 경우 인덱스를 만들 수 있습니다. 그러나 전체 크기가 한도를 초과하는 열에 대한 이후 삽입 작업이나 업데이트 동작은 실패합니다. 클러스터형 인덱스의 인덱스 키는 ROW_OVERFLOW_DATA 할당 단위에 기존 데이터가 있는 **varchar** 열을 포함할 수 없습니다. **varchar** 열에 대한 클러스터형 인덱스를 만들고 기존 데이터가 IN_ROW_DATA 할당 단위에 있는 경우에는 데이터를 행 외부로 밀어넣는 열에 대한 후속 삽입 또는 업데이트 동작이 실패합니다.

비클러스터형 인덱스는 인덱스의 리프 수준에 키가 아닌 열을 포함할 수 있습니다. 인덱스 키 크기를 계산할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 이러한 열을 고려하지 않습니다. 자세한 내용은 [포괄 열을 사용하여 인덱스 만들기](../../relational-databases/indexes/create-indexes-with-included-columns.md) 및 [SQL Server 인덱스 아키텍처 및 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

> [!NOTE]
> 테이블이 분할된 경우 분할 키 열이 비고유 클러스터형 인덱스에 아직 없으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 의해 해당 열이 인덱스에 추가됩니다. 인덱싱된 열(포함 열 제외)과 추가된 분할 열의 결합된 크기는 비고유 클러스터형 인덱스에서 1,800바이트를 초과할 수 없습니다.

## <a name="computed-columns"></a>계산 열
계산 열에 인덱스를 만들 수 있습니다. 또한 계산 열은 PERSISTED 속성을 가질 수 있습니다. 즉, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 계산된 값을 테이블에 저장하고 계산 열이 종속된 다른 열이 업데이트되면 해당 값을 업데이트합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 열에 인덱스를 만들 때와 이 인덱스가 쿼리에서 참조될 때 이러한 지속형 값을 사용합니다.

계산 열을 인덱싱하려면 계산 열이 결정적이고 정확해야 합니다. 그러나 PERSISTED 속성을 사용하면 인덱싱할 수 있는 계산 열 유형이 다음을 포함하도록 확장할 수 있습니다.

- [!INCLUDE[tsql](../../includes/tsql-md.md)]을 기반으로 하는 계산 열 및 사용자가 결정적으로 표시한 CLR 사용자 정의 형식 메서드 및 CLR 함수
- [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 정의한 대로 결정적이지만 정확하지 않은 식을 기반으로 하는 계산 열

지속형 계산 열의 경우 다음 SET 옵션을 앞부분에 나온 [필터링된 인덱스에 필요한 SET 옵션](#required-set-options-for-filtered-indexes) 섹션처럼 설정해야 합니다.

UNIQUE나 PRIMARY KEY 제약 조건은 인덱싱을 위해 모든 조건을 충족하는 한 계산 열을 포함할 수 있습니다. 특히 계산 열은 결정적이고 정확하거나 결정적이고 지속되어야 합니다. 결정성에 대한 자세한 내용은 [결정적 함수 및 비결정적 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요.

**image** , **ntext** , **text** , **varchar(max)** , **nvarchar(max)** , **varbinary(max)** 및 **xml** 데이터 형식에서 파생된 계산된 열은 계산된 열 데이터 형식이 인덱스 키 열 또는 키가 아닌 열로 허용된다면 키로 인덱싱하거나 키가 아닌 열을 포함할 수 있습니다. 예를 들어 계산된 **xml** 열에 기본 XML 인덱스를 만들 수 없습니다. 인덱스 키 크기가 900바이트를 초과하면 경고 메시지가 표시됩니다.

계산 열에 인덱스를 만들면 이전에 작업한 삽입 또는 업데이트 작업이 실패할 수 있습니다. 계산 열에서 산술 오류가 발생하는 경우 이러한 실패가 발생할 수 있습니다. 예를 들어 다음 테이블의 계산 열 `c`에 산술 오류가 발생해도 INSERT 문은 실행됩니다.

```sql
CREATE TABLE t1 (a INT, b INT, c AS a/b);
INSERT INTO t1 VALUES (1, 0);
```

대신 테이블을 만든 후 계산 열 `c`에 인덱스를 만들면 동일한 `INSERT` 문이 이번에는 실패합니다.

```sql
CREATE TABLE t1 (a INT, b INT, c AS a/b);
CREATE UNIQUE CLUSTERED INDEX Idx1 ON t1(c);
INSERT INTO t1 VALUES (1, 0);
```

자세한 내용은 [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md)을 참조하세요.

## <a name="included-columns-in-indexes"></a>인덱스의 포괄 열
포괄 열이라고 하는 키가 아닌 열은 비클러스터형 인덱스의 리프 수준에 추가되어 쿼리를 포함함으로써 쿼리 성능을 향상시킬 수 있습니다. 즉, 쿼리에서 참조되는 모든 열은 키 열 또는 키가 아닌 열로 인덱스에 포함됩니다. 따라서 쿼리 최적화 프로그램은 인덱스 스캔에서 필요한 모든 정보를 찾을 수 있으므로 테이블 또는 클러스터형 인덱스 데이터에 액세스되지 않습니다. 자세한 내용은 [포괄 열을 사용하여 인덱스 만들기](../../relational-databases/indexes/create-indexes-with-included-columns.md) 및 [SQL Server 인덱스 아키텍처 및 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

## <a name="specifying-index-options"></a>인덱스 옵션 지정
[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에는 새 인덱스 옵션이 추가되었으며 옵션 지정 방법도 수정되었습니다. 이전 버전과 호환되는 구문에서 WITH *option_name* 은 WITH **(** \<option_name> **= ON )** 과 같습니다. 인덱스 옵션을 설정하면 다음 규칙이 적용됩니다.

- 새 인덱스 옵션은 WITH ( **_option\_name_ = ON | OFF** )를 사용해서만 지정할 수 있습니다.
- 옵션은 동일한 문에 이전 버전과 호환되는 구문 및 새 구문 모두를 사용하여 지정할 수 없습니다. 예를 들어 WITH ( **DROP_EXISTING, ONLINE = ON** )을 지정하면 문이 실패합니다.
- XML 인덱스를 만들 때 WITH( **_option_name_ = ON | OFF** )를 사용하여 옵션을 지정해야 합니다.

## <a name="drop_existing-clause"></a>DROP_EXISTING 절
DROP_EXISTING 절을 사용하여 인덱스 다시 작성, 열 추가 또는 삭제, 옵션 수정, 열 정렬 순서 수정 또는 파티션 구성표나 파일 그룹 변경 등의 작업을 수행할 수 있습니다.

인덱스가 PRIMARY KEY 또는 UNIQUE 제약 조건을 강제 적용하고 인덱스 정의가 변경되지 않으면 이 인덱스는 삭제되고 기존 제약 조건을 보존한 상태에서 다시 만들어집니다. 그러나 인덱스 정의가 변경되면 이 문은 실패합니다. PRIMARY KEY 또는 UNIQUE 제약 조건의 정의를 변경하려면 제약 조건을 삭제하고 새 정의가 있는 제약 조건을 추가합니다.

비클러스터형 인덱스가 있는 테이블에서 동일하거나 서로 다른 키 집합을 사용하여 클러스터형 인덱스를 다시 만들 때 DROP_EXISTING을 사용하면 성능이 향상됩니다. DROP_EXISTING은 이전에 클러스터형 인덱스에 대해 DROP INDEX 문을 실행한 다음 새로 클러스터형 인덱스를 만드는 CREATE INDEX 문을 실행하는 것과 같습니다. 비클러스터형 인덱스는 인덱스 정의가 변경된 경우에만 다시 한번 만들어집니다. 인덱스 정의에 원래 인덱스와 같은 인덱스 이름, 키 및 파티션 열, 고유성 특성 및 정렬 순서가 있으면 DROP_EXISTING 절은 비클러스터형 인덱스를 다시 만들지 않습니다.

비클러스터형 인덱스는 다시 만들지 여부에 관계없이 항상 원래 파일 그룹 또는 파티션 구성표에 남아 있으며 원래 파티션 함수를 사용합니다. 클러스터형 인덱스를 다른 파일 그룹이나 파티션 구성표에 다시 만들면 비클러스터형 인덱스는 클러스터형 인덱스의 새 위치와 일치하도록 이동되지 않습니다. 따라서 비클러스터형 인덱스가 이전에 클러스터형 인덱스와 일치하도록 맞춰진 경우에도 일치하지 않을 수 있습니다. 분할된 인덱스 정렬에 대한 자세한 내용은 [분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.

인덱스 문이 비클러스터형 인덱스를 지정하고 ONLINE 옵션이 OFF로 설정되어 있지 않은 경우 동일 인덱스 키 열이 동일한 순서의 동일한 오름차순 또는 내림차순을 사용하면 DROP_EXISTING 절은 데이터를 다시 정렬하지 않습니다. 클러스터형 인덱스가 해제되면 ONLINE을 OFF로 설정한 상태에서 CREATE INDEX WITH DROP_EXISTING 작업을 수행해야 합니다. 비클러스터형 인덱스가 해제되고 해제된 클러스터형 인덱스와 관련이 없는 경우에는 ONLINE을 OFF 또는 ON으로 설정한 상태에서 CREATE INDEX WITH DROP_EXISTING 작업을 수행할 수 있습니다.

> [!NOTE]
> 익스텐트가 128 이상인 인덱스를 삭제하거나 다시 작성하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 트랜잭션이 커밋될 때까지 실제 페이지 할당 취소 및 이와 관련된 잠금을 지연합니다.

## <a name="online-option"></a>ONLINE 옵션
다음 지침은 인덱스 작업을 온라인 상태로 수행할 때 적용됩니다.

- 온라인 인덱스 작업이 진행되는 동안에는 기본 테이블을 변경하거나 자르거나 삭제할 수 없습니다.
- 인덱스 작업 중에 임시 디스크 공간이 추가로 필요합니다.
- 온라인 작업은 분할된 인덱스 및 지속형 계산 열이 들어 있는 인덱스 또는 포괄 열에서 수행될 수 있습니다.

자세한 내용은 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요.

### <a name="resumable-index-operations"></a><a name="resumable-indexes"></a> 다시 시작 가능한 인덱스 작업
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

다음 지침은 다시 시작 가능한 인덱스 작업에 적용됩니다.

- 온라인 인덱스 생성은 `RESUMABLE = ON` 옵션을 사용하여 resumable로 지정됩니다.
- RESUMABLE 옵션은 지정된 인덱스에 대해 메타데이터에서 지속되며 현재 DDL 문의 기간에만 적용됩니다. 그러므로 다시 시작이 가능하도록 하려면 `RESUMABLE = ON` 절을 명시적으로 지정해야 합니다.
- MAX_DURATION 옵션은 `RESUMABLE = ON` 옵션에만 지원됩니다.
- RESUMABLE에 대한 MAX_DURATION은 인덱스 작성 시간 간격을 지정합니다. 이 시간이 사용된 후 인덱스 다시 작성이 일시 중지되거나 실행이 완료됩니다. 사용자는 일시 중지된 인덱스의 작성을 다시 시작할 시간을 결정합니다. MAX_DURATION에 대한 분 단위의 **시간** 은 0분보다 크거나 1주일(7 \* 24 \* 60 = 10080분) 이하여야 합니다. 원래 인덱스와 새로 만든 인덱스 두 인덱스가 모두 디스크 공간을 필요로 하고 DML 작업 중에 업데이트되어야 하므로, 인덱스 작업을 오랫동안 일시 중지하면 특정 테이블에 대한 DML 성능 및 데이터베이스 디스크 용량에 영향을 미칠 수 있습니다. MAX_DURATION 옵션을 생략하면 인덱스 작업은 완료될 때까지 또는 실패가 발생할 때까지 계속됩니다.
- 인덱스 작업을 즉시 일시 중지하려면 진행 중인 명령을 중지하거나(Ctrl-C) [ALTER INDEX](alter-index-transact-sql.md) PAUSE 명령을 실행하거나 `KILL <session_id>` 명령을 실행합니다. 명령이 일시 중지되면 [ALTER INDEX](alter-index-transact-sql.md) 명령을 사용하여 다시 시작할 수 있습니다.
- 다시 시작 가능한 인덱스의 원래 CREATE INDEX 문을 다시 실행하면 일시 중지된 인덱스 작성 작업이 자동으로 다시 시작됩니다.
- 다시 시작 가능한 인덱스의 경우 `SORT_IN_TEMPDB = ON` 옵션이 지원되지 않습니다.
- `RESUMABLE = ON` 상태의 DDL 명령은 명시적 트랜잭션 내에서 실행할 수 없습니다(begin TRAN … COMMIT 블록에 포함될 수 없음).
- 인덱스 만들기/다시 작성을 다시 시작/중단하려면 [ALTER INDEX](alter-index-transact-sql.md) T-SQL 구문을 사용합니다.

> [!NOTE]
> DDL 명령은 완료, 일시 중지 또는 실패할 때까지 실행됩니다. 명령이 일시 중지된 경우 작업이 일시 중지되었고 인덱스 만들기가 완료되지 않았음을 알려 주는 오류가 발생합니다. 현재 인덱스 상태에 대한 더 자세한 내용은 [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md)에서 가져올 수 있습니다. 이전과 마찬가지로 실패의 경우 오류도 발생합니다.

인덱스 만들기가 다시 시작 가능한 작업으로 실행되도록 지정하려면 [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md)를 참조하세요.

#### <a name="resources"></a>리소스
다시 시작 가능한 온라인 인덱스 만들기 작업에는 다음 리소스가 필요합니다.

- 인덱스가 일시 중지될 시간을 포함하여 작성 중인 인덱스를 유지하기 위해 필요한 추가 공간
- 정렬 단계 중의 추가 로그 처리량. 다시 시작 가능한 인덱스의 전체 로그 공간 사용량이 일반 온라인 인덱스 만들기에 비교해 적으므로 이 작업 중에 로그가 잘릴 수 있습니다.
- DDL 수정을 하지 못하게 하는 DDL 상태
- 일시 중지된 동안 및 작업이 실행되는 동안의 작업 기간에 작성 중인 인덱스에 대한 고스트 정리는 차단됩니다.

#### <a name="current-functional-limitations"></a>현재 기능 제한 사항
다음 기능은 다시 시작 가능한 인덱스 만들기 작업에 사용할 수 없습니다.

- 다시 시작 가능한 온라인 인덱스 만들기 작업이 일시 중지된 후에는 MAXDOP의 초기 값을 변경할 수 없음
- 다음을 포함하는 인덱스를 만듭니다.

  - Computed 또는 TIMESTAMP 열을 키 열로 포함
  - 다시 시작 가능한 인덱스 만들기용으로 LOB 열을 포함된 열로 포함
  - 필터링된 인덱스

## <a name="row-and-page-locks-options"></a>행 및 페이지 잠금 옵션
`ALLOW_ROW_LOCKS = ON` 및 `ALLOW_PAGE_LOCK = ON`인 경우 인덱스에 액세스할 때 행, 페이지 및 테이블 수준 잠금이 허용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 적절한 잠금을 선택하고 행 또는 페이지 잠금에서 테이블 잠금으로 잠금을 에스컬레이션할 수 있습니다.

`ALLOW_ROW_LOCKS = OFF` 및 `ALLOW_PAGE_LOCK = OFF`인 경우 인덱스에 액세스할 때 테이블 수준 잠금만 허용됩니다.

## <a name="sequential-keys"></a>순차 키
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

마지막 페이지 삽입 경합은 다수의 동시 스레드가 순차 키를 사용하여 인덱스에 행을 삽입하려고 할 때 발생하는 일반적인 성능 문제입니다. ID 열이나 기본적으로 현재 날짜/시간으로 설정되는 날짜와 같이 항상 증가(또는 감소)하는 값이 선행 키 열에 포함되는 경우 인덱스가 순차적이라고 간주됩니다. 삽입되는 키가 순차적이므로 모든 새 행이 인덱스 구조의 끝, 즉 동일한 페이지에 삽입됩니다. 이 경우 메모리에서 페이지 경합이 발생하며, 여러 스레드가 해당 페이지의 PAGELATCH_EX를 대기하는 상황을 통해 확인할 수 있습니다.

OPTIMIZE_FOR_SEQUENTIAL_KEY 인덱스 옵션을 켜면 데이터베이스 엔진 내에서 인덱스에 대한 높은 동시성 삽입 처리량을 향상하는 데 도움이 되는 최적화 기능을 사용할 수 있습니다. 순차 키가 있어서 마지막 페이지 삽입 경합이 발생하기 쉬운 인덱스에 사용되지만, B-트리 인덱스 구조의 다른 영역에 핫 스폿이 있는 인덱스에도 도움이 될 수 있습니다.

## <a name="viewing-index-information"></a>인덱스 정보 보기
인덱스 정보를 반환하려면 카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용할 수 있습니다.

## <a name="data-compression"></a>Data Compression
데이터 압축은 [데이터 압축](../../relational-databases/data-compression/data-compression.md) 토픽에서 설명합니다. 고려해야 할 주요 요소는 다음과 같습니다.

- 압축하면 한 페이지에 더 많은 행을 저장할 수 있지만 최대 행 크기는 변경되지 않습니다.
- 인덱스의 비-리프 페이지는 압축된 페이지가 아니지만 행은 압축할 수 있습니다.
- 각각의 비클러스터형 인덱스에는 개별 압축 설정이 있으며 기본 테이블의 압축 설정을 상속하지 않습니다.
- 힙에 클러스터형 인덱스를 만드는 경우 이 클러스터형 인덱스는 다른 압축 상태를 지정하지 않는 한 힙의 압축 상태를 상속합니다.

다음은 분할된 인덱스에 적용되는 제한 사항입니다.

- 테이블에 정렬되지 않은 인덱스가 있으면 단일 파티션의 압축 설정을 변경할 수 없습니다.
- ALTER INDEX \<index> ... REBUILD PARTITION ... 구문은 인덱스의 지정된 파티션을 다시 빌드합니다.
- ALTER INDEX \<index> ... REBUILD WITH ... 구문은 인덱스의 모든 파티션을 다시 빌드합니다.

압축 상태를 변경할 경우 테이블, 인덱스 또는 파티션에 어떤 영향을 주는지 확인하려면 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 저장 프로시저를 사용합니다.

## <a name="permissions"></a>사용 권한
테이블 또는 보기에 대한 `ALTER` 권한이 필요합니다. 사용자는 `sysadmin` 고정 서버 역할의 멤버이거나 `db_ddladmin` 또는 `db_owner` 고정 데이터베이스 역할의 멤버여야 합니다.

## <a name="limitations-and-restrictions"></a>제한 사항
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서는 다음을 만들 수 없습니다.

- columnstore 인덱스가 이미 존재하는 경우 데이터 웨어하우스 테이블에 대한 클러스터형 또는 비클러스터형 rowstore 인덱스. 이 동작은 rowstore와 columnstore 인덱스가 같은 테이블에 공존할 수 있게 해주는 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다릅니다.
- 뷰에서 인덱스를 만들 수 없습니다.

## <a name="metadata"></a>메타데이터
기존 인덱스에 대한 자세한 정보를 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 쿼리할 수 있습니다.

## <a name="version-notes"></a>버전 참고 사항

[!INCLUDE[ssSDS](../../includes/sssds-md.md)]는 파일 그룹 및 파일 스트림 옵션을 지원하지 않습니다.

## <a name="examples-all-versions-uses-the-adventureworks-database"></a>예제: 모든 버전. AdventureWorks 데이터베이스를 사용합니다.

### <a name="a-create-a-simple-nonclustered-rowstore-index"></a>A. 간단한 비클러스터형 rowstore 인덱스 만들기
다음 예제에서는 `Purchasing.ProductVendor` 테이블의 `VendorID` 열에 비클러스터형 인덱스를 만듭니다.

```sql
CREATE INDEX IX_VendorID ON ProductVendor (VendorID);
CREATE INDEX IX_VendorID ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);
CREATE INDEX IX_VendorID ON Purchasing..ProductVendor (VendorID);
```

### <a name="b-create-a-simple-nonclustered-rowstore-composite-index"></a>B. 간단한 비클러스터형 rowstore 복합 인덱스 만들기
다음 예제에서는 `Sales.SalesPerson` 테이블의 `SalesQuota` 및 `SalesYTD` 열에 비클러스터형 복합 인덱스를 만듭니다.

```sql
CREATE NONCLUSTERED INDEX IX_SalesPerson_SalesQuota_SalesYTD ON Sales.SalesPerson (SalesQuota, SalesYTD);
```

### <a name="c-create-an-index-on-a-table-in-another-database"></a>C. 다른 데이터베이스의 테이블에 인덱스 만들기
다음 예제에서는 `Purchasing` 데이터베이스에 있는 `ProductVendor` 테이블의 `VendorID` 열에 클러스터형 인덱스를 만듭니다.

```sql
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID ON Purchasing..ProductVendor (VendorID);
```

### <a name="d-add-a-column-to-an-index"></a>D. 인덱스에 열 추가
다음 예제에서는 dbo.FactFinance 테이블의 열 2개를 사용하여 IX_FF 인덱스를 만듭니다. 다음 명령문은 하나 이상의 열을 포함한 인덱스를 다시 만들며 기존 이름을 유지합니다.

```sql
CREATE INDEX IX_FF ON dbo.FactFinance (FinanceKey ASC, DateKey ASC);

-- Rebuild and add the OrganizationKey
CREATE INDEX IX_FF ON dbo.FactFinance (FinanceKey, DateKey, OrganizationKey DESC)
  WITH (DROP_EXISTING = ON);
```

## <a name="examples-sql-server-azure-sql-database"></a>예제: SQL Server, Azure SQL Database

### <a name="e-create-a-unique-nonclustered-index"></a>E. 고유한 비클러스터형 인덱스 만들기
다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Name` 테이블의 `Production.UnitMeasure` 열에 고유한 비클러스터형 인덱스를 만듭니다. 인덱스는 `Name` 열에 삽입된 데이터의 고유성을 강제 적용합니다.

```sql
CREATE UNIQUE INDEX AK_UnitMeasure_Name
  ON Production.UnitMeasure(Name);
```

다음 쿼리는 기존 행과 동일한 값을 가진 행을 삽입하여 고유성 제약 조건을 테스트합니다.

```sql
-- Verify the existing value.
SELECT Name FROM Production.UnitMeasure WHERE Name = N'Ounces';
GO

INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name, ModifiedDate)
  VALUES ('OC', 'Ounces', GETDATE());
```

결과 오류 메시지는 다음과 같습니다.

```
Server: Msg 2601, Level 14, State 1, Line 1
Cannot insert duplicate key row in object 'UnitMeasure' with unique index 'AK_UnitMeasure_Name'. The statement has been terminated.
```

### <a name="f-use-the-ignore_dup_key-option"></a>F. IGNORE_DUP_KEY 옵션 사용
다음 예에서는 `IGNORE_DUP_KEY` 옵션을 먼저 `ON`으로 설정한 후 다시 `OFF`로 설정한 상태에서 여러 행을 임시 테이블에 삽입했을 때 미치는 영향을 보여 줍니다. 두 번째 여러 행 `#Test` 문이 실행될 때 의도적으로 중복 값을 발생시키는 `INSERT` 테이블에 단일 행을 삽입합니다. 테이블의 행 수가 삽입된 행 수를 반환합니다.

```sql
CREATE TABLE #Test (C1 NVARCHAR(10), C2 NVARCHAR(50), C3 DATETIME);
GO

CREATE UNIQUE INDEX AK_Index ON #Test (C2)
  WITH (IGNORE_DUP_KEY = ON);
GO

INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;
GO

SELECT COUNT(*) AS [Number of rows] FROM #Test;
GO

DROP TABLE #Test;
GO
```

두 번째 `INSERT` 문의 결과는 다음과 같습니다.

```cmd
Server: Msg 3604, Level 16, State 1, Line 5 Duplicate key was ignored.

Number of rows
--------------
38
```

고유성 제약 조건을 위반하지 않은 `Production.UnitMeasure` 테이블에서 삽입된 행이 성공적으로 삽입되었습니다. 경고가 발생하고 중복된 행이 무시되었지만 전체 트랜잭션은 롤백되지 않았습니다.

같은 문이 다시 실행되지만 `IGNORE_DUP_KEY`를 `OFF`로 설정한 상태입니다.

```sql
CREATE TABLE #Test (C1 NVARCHAR(10), C2 NVARCHAR(50), C3 DATETIME);
GO

CREATE UNIQUE INDEX AK_Index ON #Test (C2)
  WITH (IGNORE_DUP_KEY = OFF);
GO

INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;
GO

SELECT COUNT(*) AS [Number of rows] FROM #Test;
GO

DROP TABLE #Test;
GO
```

두 번째 `INSERT` 문의 결과는 다음과 같습니다.

```
Server: Msg 2601, Level 14, State 1, Line 5
Cannot insert duplicate key row in object '#Test' with unique index
'AK_Index'. The statement has been terminated.

Number of rows
--------------
1
```

`Production.UnitMeasure` 테이블에서 오직 한 행만 `UNIQUE` 인덱스 제약 조건을 위반했지만 이 테이블에서 어떤 행도 삽입되지 않았습니다.

### <a name="g-using-drop_existing-to-drop-and-re-create-an-index"></a>G. DROP_EXISTING을 사용하여 인덱스 삭제 및 다시 만들기
다음 예에서는 `ProductID` 옵션을 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Production.WorkOrder` 테이블의 `DROP_EXISTING` 열에서 기존 인덱스를 삭제하고 다시 만듭니다. `FILLFACTOR` 및 `PAD_INDEX` 옵션도 설정됩니다.

```sql
CREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID
  ON Production.WorkOrder(ProductID)
    WITH (FILLFACTOR = 80,
      PAD_INDEX = ON,
      DROP_EXISTING = ON);
GO
```

### <a name="h-create-an-index-on-a-view"></a>H. 뷰에 인덱스 만들기
다음 예에서는 뷰를 만들고 이 뷰에 인덱스를 만듭니다. 인덱싱된 뷰를 사용하는 두 개의 쿼리가 포함되어 있습니다.

```sql
-- Set the options to support indexed views
SET NUMERIC_ROUNDABORT OFF;
SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,
  QUOTED_IDENTIFIER, ANSI_NULLS ON;
GO

-- Create view with schemabinding
IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL
  DROP VIEW Sales.vOrders;
GO

CREATE VIEW Sales.vOrders
  WITH SCHEMABINDING
AS
  SELECT SUM(UnitPrice * OrderQty * (1.00 - UnitPriceDiscount)) AS Revenue,
    OrderDate, ProductID, COUNT_BIG(*) AS COUNT
  FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o
  WHERE od.SalesOrderID = o.SalesOrderID
  GROUP BY OrderDate, ProductID;
GO

-- Create an index on the view
CREATE UNIQUE CLUSTERED INDEX IDX_V1
  ON Sales.vOrders (OrderDate, ProductID);
GO

-- This query can use the indexed view even though the view is
-- not specified in the FROM clause.
SELECT SUM(UnitPrice * OrderQty * (1.00 - UnitPriceDiscount)) AS Rev,
  OrderDate, ProductID
FROM Sales.SalesOrderDetail AS od
  JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID = o.SalesOrderID
    AND ProductID BETWEEN 700 AND 800
    AND OrderDate >= CONVERT(DATETIME, '05/01/2002', 101)
GROUP BY OrderDate, ProductID
ORDER BY Rev DESC;
GO

-- This query can use the above indexed view
SELECT OrderDate, SUM(UnitPrice * OrderQty * (1.00 - UnitPriceDiscount)) AS Rev
FROM Sales.SalesOrderDetail AS od
  JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID = o.SalesOrderID
    AND DATEPART(mm, OrderDate) = 3
  AND DATEPART(yy, OrderDate) = 2002
GROUP BY OrderDate
ORDER BY OrderDate ASC;
GO
```

### <a name="i-create-an-index-with-included-non-key-columns"></a>9\. (키가 아닌) 포함 열이 있는 인덱스 만들기
다음 예에서는 1개의 키 열(`PostalCode`)과 4개의 키가 아닌 열(`AddressLine1`, `AddressLine2`, `City`, `StateProvinceID`)이 있는 비클러스터형 인덱스를 만듭니다. 인덱스에서 처리하는 쿼리가 이어집니다. 쿼리 최적화 프로그램에서 선택한 인덱스를 표시하려면 쿼리를 실행하기 전에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **쿼리** 메뉴에서 **실제 실행 계획 표시** 를 선택합니다.

```sql
CREATE NONCLUSTERED INDEX IX_Address_PostalCode
  ON Person.Address (PostalCode)
  INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);
GO

SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode
FROM Person.Address
WHERE PostalCode BETWEEN N'98000' and N'99999';
GO
```

### <a name="j-create-a-partitioned-index"></a>J. 분할된 인덱스 만들기
다음은 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 기존 파티션 구성표인 `TransactionsPS1`에 분할된 비클러스터형 인덱스를 만드는 예입니다. 이 예에서는 분할된 인덱스 샘플이 설치되었다고 가정합니다.

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

```sql
CREATE NONCLUSTERED INDEX IX_TransactionHistory_ReferenceOrderID
  ON Production.TransactionHistory (ReferenceOrderID)
  ON TransactionsPS1 (TransactionDate);
GO
```

### <a name="k-creating-a-filtered-index"></a>11. 필터링된 인덱스 만들기
다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 Production.BillOfMaterials 테이블에 필터링된 인덱스를 만듭니다. 필터 조건자는 필터링된 인덱스에 키 열이 아닌 열을 포함할 수 있습니다. 이 예에서 조건자는 EndDate가 NULL이 아닌 행만 선택합니다.

```sql
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithEndDate"
  ON Production.BillOfMaterials (ComponentID, StartDate)
  WHERE EndDate IS NOT NULL;
```

### <a name="l-create-a-compressed-index"></a>12. 압축 인덱스 만들기
다음 예에서는 행 압축을 사용하여 분할되지 않은 테이블에 인덱스를 만듭니다.

```sql
CREATE NONCLUSTERED INDEX IX_INDEX_1
  ON T1 (C2)
  WITH (DATA_COMPRESSION = ROW);
GO
```

다음 예에서는 인덱스의 모든 파티션에서 행 압축을 사용하여 분할된 테이블에 인덱스를 만듭니다.

```sql
CREATE CLUSTERED INDEX IX_PartTab2Col1
  ON PartitionTable1 (Col1)
  WITH (DATA_COMPRESSION = ROW);
GO
```

 다음 예에서는 인덱스의 `1` 파티션에서 페이지 압축을 사용하고 `2`-`4` 파티션에서 행 압축을 사용하여 분할된 테이블에 인덱스를 만듭니다.

```sql
CREATE CLUSTERED INDEX IX_PartTab2Col1
  ON PartitionTable1 (Col1)
  WITH (
    DATA_COMPRESSION = PAGE ON PARTITIONS(1),
    DATA_COMPRESSION = ROW ON PARTITIONS (2 TO 4)
  );
GO
```

### <a name="m-create-resume-pause-and-abort-resumable-index-operations"></a>13. 다시 시작 가능한 인덱스 작업 만들기, 다시 시작, 일시 중지 및 중단
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

```sql
-- Execute a resumable online index create statement with MAXDOP=1
CREATE INDEX test_idx1 ON test_table (col1) WITH (ONLINE = ON, MAXDOP = 1, RESUMABLE = ON);

-- Executing the same command again (see above) after an index operation was paused, resumes automatically the index create operation.

-- Execute a resumable online index creates operation with MAX_DURATION set to 240 minutes. After the time expires, the resumable index create operation is paused.
CREATE INDEX test_idx2 ON test_table (col2) WITH (ONLINE = ON, RESUMABLE = ON, MAX_DURATION = 240);

-- Pause a running resumable online index creation
ALTER INDEX test_idx1 ON test_table PAUSE;
ALTER INDEX test_idx2 ON test_table PAUSE;

-- Resume a paused online index creation
ALTER INDEX test_idx1 ON test_table RESUME;
ALTER INDEX test_idx2 ON test_table RESUME;

-- Abort resumable index create operation which is running or paused
ALTER INDEX test_idx1 ON test_table ABORT;
ALTER INDEX test_idx2 ON test_table ABORT;
```

## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### <a name="n-basic-syntax"></a>14. 기본 구문
다시 시작 가능한 인덱스 작업 만들기, 다시 시작, 일시 중지 및 중단       

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

```sql
-- Execute a resumable online index create statement with MAXDOP=1
CREATE INDEX test_idx ON test_table WITH (ONLINE = ON, MAXDOP = 1, RESUMABLE = ON);

-- Executing the same command again (see above) after an index operation was paused, resumes automatically the index create operation.

-- Execute a resumable online index creates operation with MAX_DURATION set to 240 minutes. After the time expires, the resumable index create operation is paused.
CREATE INDEX test_idx ON test_table WITH (ONLINE = ON, RESUMABLE = ON, MAX_DURATION = 240);

-- Pause a running resumable online index creation
ALTER INDEX test_idx ON test_table PAUSE;

-- Resume a paused online index creation
ALTER INDEX test_idx ON test_table RESUME;

-- Abort resumable index create operation which is running or paused
ALTER INDEX test_idx ON test_table ABORT;
```

### <a name="o-create-a-nonclustered-index-on-a-table-in-the-current-database"></a>15. 현재 데이터베이스의 테이블에 비클러스터형 인덱스 만들기
다음 예에서는 `ProductVendor` 테이블의 `VendorID` 열에 비클러스터형 인덱스를 만듭니다.

```sql
CREATE INDEX IX_ProductVendor_VendorID
  ON ProductVendor (VendorID);
```

### <a name="p-create-a-clustered-index-on-a-table-in-another-database"></a>16. 다른 데이터베이스의 테이블에 클러스터형 인덱스 만들기
다음 예에서는 `Purchasing` 데이터베이스에 있는 `ProductVendor` 테이블의 `VendorID` 열에 비클러스터형 인덱스를 만듭니다.

```sql
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID
  ON Purchasing..ProductVendor (VendorID);
```
### <a name="q-create-an-ordered-clustered-index-on-a-table"></a>17. 테이블에 순서가 지정된 클러스터형 인덱스 만들기  
다음 예제에서는 `MyDB` 데이터베이스에 있는 `T1` 테이블의 `c1` 및 `c2` 열에 순서가 지정된 클러스터형 인덱스를 만듭니다.

```sql
CREATE CLUSTERED COLUMNSTORE INDEX MyOrderedCCI ON MyDB.dbo.T1 
ORDER (c1, c2);

```

### <a name="r-convert-a-cci-to-an-ordered-clustered-index-on-a-table"></a>18. 테이블에서 CCI를 순서가 지정된 클러스터형 인덱스로 변환  
다음 예제에서는 `MyDB` 데이터베이스에 있는 `T2` 테이블의 `c1` 및 `c2` 열에서 기존 클러스터형 columnstore 인덱스를 `MyOrderedCCI`라는 순서가 지정된 클러스터형 columnstore 인덱스로 변환합니다.

```sql
CREATE CLUSTERED COLUMNSTORE INDEX MyOrderedCCI ON MyDB.dbo.T2
ORDER (c1, c2)
WITH (DROP_EXISTING = ON);

```

## <a name="see-also"></a>참고 항목
[SQL Server 인덱스 아키텍처 및 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)     
[온라인으로 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)  
[인덱스 및 ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md#indexes-and-alter-table)     
[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)     
[CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)     
[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)     
[CREATE SPATIAL INDEX](../../t-sql/statements/create-spatial-index-transact-sql.md)      
[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)     
[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)    
[CREATE XML INDEX](../../t-sql/statements/create-xml-index-transact-sql.md)     
[데이터 형식](../../t-sql/data-types/data-types-transact-sql.md)    
[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)    
[DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)    
[XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)     
[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)     
[sys.index_columns](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)    
[sys.xml_indexes](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)     
[EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)