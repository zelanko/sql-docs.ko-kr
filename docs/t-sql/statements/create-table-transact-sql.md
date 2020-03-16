---
title: CREATE TABLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/24/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILESTREAM_TSQL
- TABLE
- CREATE_TABLE_TSQL
- CREATE TABLE
- FILESTREAM
- TABLE_TSQL
- FILESTREAM_ON
- FILESTREAM_ON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK constraints
- global temporary tables [SQL Server]
- local temporary tables [SQL Server]
- size [SQL Server], tables
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], columns
- maximum number of indexes per table
- number of tables per database
- number of indexes per table
- table creation [SQL Server], CREATE TABLE
- temporary tables [SQL Server], creating
- table size [SQL Server]
- nullability [SQL Server]
- partitioned tables [SQL Server], creating
- DEFAULT definition
- null values [SQL Server], columns
- number of rows per table
- maximum number of columns per table
- FOREIGN KEY constraints, creating
- PRIMARY KEY constraints
- number of bytes per row
- CREATE TABLE statement
- number of columns per table
- maximum number of bytes per row
ms.assetid: 1e068443-b9ea-486a-804f-ce7b6e048e8b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7e90aea4fc05a01f67527e33cac4ba90913405c7
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287667"
---
# <a name="create-table-transact-sql"></a>CREATE TABLE(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 새 테이블을 만듭니다.

> [!NOTE]
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 구문은 [CREATE TABLE(Azure SQL Data Warehouse)](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)를 참조하세요.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="simple-syntax"></a>간단한 구문

```
-- Simple CREATE TABLE Syntax (common if not using options)
CREATE TABLE
    { database_name.schema_name.table_name. | schema_name.table_name | table_name }
    ( { <column_definition> } [ ,...n ] )
[ ; ]
```

## <a name="full-syntax"></a>전체 구문

```
-- Disk-Based CREATE TABLE Syntax
CREATE TABLE
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    [ AS FileTable ]
    ( {   <column_definition>
        | <computed_column_definition>
        | <column_set_definition>
        | [ <table_constraint> ] [ ,... n ]
        | [ <table_index> ] }
          [ ,...n ]
          [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name
             , system_end_time_column_name ) ]
      )
    [ ON { partition_scheme_name ( partition_column_name )
           | filegroup
           | "default" } ]
    [ TEXTIMAGE_ON { filegroup | "default" } ]
    [ FILESTREAM_ON { partition_scheme_name
           | filegroup
           | "default" } ]
    [ WITH ( <table_option> [ ,...n ] ) ]
[ ; ]
  
<column_definition> ::=
column_name <data_type>
    [ FILESTREAM ]
    [ COLLATE collation_name ]
    [ SPARSE ]
    [ MASKED WITH ( FUNCTION = ' mask_function ') ]
    [ CONSTRAINT constraint_name [ DEFAULT constant_expression ] ]
    [ IDENTITY [ ( seed,increment ) ]
    [ NOT FOR REPLICATION ]
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]
    [ NULL | NOT NULL ]
    [ ROWGUIDCOL ]
    [ ENCRYPTED WITH
        ( COLUMN_ENCRYPTION_KEY = key_name ,
          ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,
          ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ) ]
    [ <column_constraint> [, ...n ] ]
    [ <column_index> ]
  
<data_type> ::=
[ type_schema_name . ] type_name
    [ ( precision [ , scale ] | max |
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]
  
<column_constraint> ::=
[ CONSTRAINT constraint_name ]
{     { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        [
            WITH FILLFACTOR = fillfactor
          | WITH ( < index_option > [ , ...n ] )
        ]
        [ ON { partition_scheme_name ( partition_column_name )
            | filegroup | "default" } ]
  
  | [ FOREIGN KEY ]
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
  
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
}
  
<column_index> ::=
 INDEX index_name [ CLUSTERED | NONCLUSTERED ]
    [ WITH ( <index_option> [ ,... n ] ) ]
    [ ON { partition_scheme_name (column_name )
         | filegroup_name
         | default
         }
    ]
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]
  
<computed_column_definition> ::=
column_name AS computed_column_expression
[ PERSISTED [ NOT NULL ] ]
[
    [ CONSTRAINT constraint_name ]
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        [
            WITH FILLFACTOR = fillfactor
          | WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name ( partition_column_name )
        | filegroup | "default" } ]
  
    | [ FOREIGN KEY ]
        REFERENCES referenced_table_name [ ( ref_column ) ]
        [ ON DELETE { NO ACTION | CASCADE } ]
        [ ON UPDATE { NO ACTION } ]
        [ NOT FOR REPLICATION ]
  
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
]
  
<column_set_definition> ::=
column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS
  
< table_constraint > ::=
[ CONSTRAINT constraint_name ]
{
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        (column [ ASC | DESC ] [ ,...n ] )
        [
            WITH FILLFACTOR = fillfactor
           |WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name (partition_column_name)
            | filegroup | "default" } ]
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )

< table_index > ::=
{  
    {  
      INDEX index_name  [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ]
         (column_name [ ASC | DESC ] [ ,... n ] )
    | INDEX index_name CLUSTERED COLUMNSTORE
    | INDEX index_name [ NONCLUSTERED ] COLUMNSTORE (column_name [ ,... n ] )
    }
    [ WITH ( <index_option> [ ,... n ] ) ]
    [ ON { partition_scheme_name (column_name )
         | filegroup_name
         | default
         }
    ]
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]
  
}

<table_option> ::=
{  
    [DATA_COMPRESSION = { NONE | ROW | PAGE }
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }
      [ , ...n ] ) ]]
    [ FILETABLE_DIRECTORY = <directory_name> ]
    [ FILETABLE_COLLATE_FILENAME = { <collation_name> | database_default } ]
    [ FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = <constraint_name> ]
    [ FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]
    [ FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]
    [ SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ] ]
    [ REMOTE_DATA_ARCHIVE =
      {
          ON [ ( <table_stretch_options> [,...n] ) ]
        | OFF ( MIGRATION_STATE = PAUSED )
      }
    ]
}
  
<table_stretch_options> ::=
{  
    [ FILTER_PREDICATE = { null | table_predicate_function } , ]
      MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }
 }
  
<index_option> ::=
{
    PAD_INDEX = { ON | OFF }
  | FILLFACTOR = fillfactor
  | IGNORE_DUP_KEY = { ON | OFF }
  | STATISTICS_NORECOMPUTE = { ON | OFF }
  | STATISTICS_INCREMENTAL = { ON | OFF }
  | ALLOW_ROW_LOCKS = { ON | OFF }
  | ALLOW_PAGE_LOCKS = { ON | OFF }
  | OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF }
  | COMPRESSION_DELAY= {0 | delay [Minutes]}
  | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }
       [ ON PARTITIONS ( { <partition_number_expression> | <range> }
       [ , ...n ] ) ]
}
<range> ::=
<partition_number_expression> TO <partition_number_expression>
```

```
-- Memory optimized CREATE TABLE Syntax
CREATE TABLE
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition>
    | [ <table_constraint> ] [ ,... n ]
    | [ <table_index> ]
      [ ,... n ] }
      [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name
        , system_end_time_column_name ) ]
)
    [ WITH ( <table_option> [ ,... n ] ) ]
 [ ; ]

<column_definition> ::=
column_name <data_type>
    [ COLLATE collation_name ]
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]
    [ NULL | NOT NULL ]
[
    [ CONSTRAINT constraint_name ] DEFAULT memory_optimized_constant_expression ]
    | [ IDENTITY [ ( 1, 1 ) ]
]
    [ <column_constraint> ]
    [ <column_index> ]
  
<data_type> ::=
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]

<column_constraint> ::=
 [ CONSTRAINT constraint_name ]
{
  { PRIMARY KEY | UNIQUE }
      {   NONCLUSTERED
        | NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count)
      }
  | [ FOREIGN KEY ]
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]
  | CHECK ( logical_expression )
}
  
< table_constraint > ::=
 [ CONSTRAINT constraint_name ]
{
   { PRIMARY KEY | UNIQUE }
     {
       NONCLUSTERED (column [ ASC | DESC ] [ ,... n ])
       | NONCLUSTERED HASH (column [ ,... n ] ) WITH ( BUCKET_COUNT = bucket_count )
                    }
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
    | CHECK ( logical_expression )
}

<column_index> ::=
  INDEX index_name
{ [ NONCLUSTERED ] | [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count)}

<table_index> ::=
  INDEX index_name
{   [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count)
  | [ NONCLUSTERED ] (column [ ASC | DESC ] [ ,... n ] )
      [ ON filegroup_name | default ]
  | CLUSTERED COLUMNSTORE [WITH ( COMPRESSION_DELAY = {0 | delay [Minutes]})]
      [ ON filegroup_name | default ]
  
}
  
<table_option> ::=
{  
    MEMORY_OPTIMIZED = ON
  | DURABILITY = {SCHEMA_ONLY | SCHEMA_AND_DATA}
  | SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ]
  
}
```

## <a name="arguments"></a>인수

*database_name* 테이블이 생성된 데이터베이스의 이름입니다. *database_name*은 기존 데이터베이스 이름을 지정해야 합니다. *database_name*을 지정하지 않으면 기본적으로 현재 데이터베이스가 됩니다. 현재 연결에 대한 로그인은 *database_name*에 지정된 데이터베이스의 기존 사용자 ID와 연결되어야 하며 해당 사용자 ID는 CREATE TABLE 권한을 갖고 있어야 합니다.

*schema_name* 새 테이블이 속한 스키마의 이름입니다.

*table_name* 새 테이블의 이름입니다. 테이블 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 따라야 합니다. 로컬 임시 테이블 이름(단일 숫자 기호(#)가 접두사로 붙은 이름이며 최대 116자)을 제외하면 *table_name*은 최대 128자가 될 수 있습니다.

AS FileTable **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상).

새 테이블을 FileTable로 만듭니다. FileTable에는 고정 스키마가 있으므로 열을 지정하지 않아도 됩니다. 자세한 내용은 [FileTables](../../relational-databases/blob/filetables-sql-server.md)를 참조하세요.

*column_name*
*computed_column_expression* 계산 열의 값을 정의하는 식입니다. 계산 열은 해당 열에 PERSISTED 표시가 없는 한 테이블에 물리적으로 저장되지 않는 가상의 열입니다. 이 열은 같은 테이블의 다른 열을 사용하는 식에서 계산됩니다. 예를 들어 계산 열에는 **cost** AS **price** \* **qty** 정의가 있을 수 있습니다. 식은 계산되지 않은 열 이름, 상수, 함수, 변수 및 이러한 요소를 하나 이상의 연산자로 연결한 조합이 될 수 있습니다. 식은 하위 쿼리가 되거나 별칭 데이터 형식을 포함할 수 없습니다.

계산 열은 SELECT 목록, WHERE 절, ORDER BY 절 또는 정규식을 사용할 수 있는 다른 위치에서 사용할 수 있습니다. 단, 다음과 같은 경우는 예외입니다.

- FOREIGN KEY 또는 CHECK 제약 조건에 참여하려면 계산 열이 PERSISTED로 표시되어야 합니다.
- 계산 열 값이 결정적 식에 의해 정의되고 결과의 데이터 형식이 인덱스 열에 허용되는 경우에는 계산 열을 인덱스의 키 열이나 PRIMARY KEY 또는 UNIQUE 제약 조건의 일부로 사용할 수 있습니다.

   예를 들어 테이블에 **a**와 **b**라는 정수 열이 있을 때 계산 열 **a+b**는 인덱싱할 수 있지만 계산 열 **a+DATEPART(dd, GETDATE())** 는 다음 호출 시 값이 바뀌므로 인덱싱할 수 없습니다.

- 계산 열은 INSERT 또는 UPDATE 문의 대상이 될 수 없습니다.

> [!NOTE]
> 테이블의 각 행은 계산 열과 연관된 열에 대해 다른 값을 가질 수 있습니다. 따라서 계산 열은 각 행에 대해 동일한 값을 갖지 않습니다.

계산 열의 Null 허용 여부는 사용되는 식을 바탕으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 자동으로 결정합니다. 대부분 식의 결과는 언더플로 또는 오버플로에 의한 Null 결과를 생성할 수 있으므로 Null이 허용되지 않는 열만 사용하더라도 결국 식은 Null을 허용하는 것으로 간주됩니다. **AllowsNull** 속성과 함께 `COLUMNPROPERTY` 함수를 사용하여 테이블에 있는 계산 열의 Null 허용 여부를 확인합니다. Null을 허용하는 식은 *check_expression* 상수로 `ISNULL`을 지정하여 NULL을 허용하지 않는 식으로 바꿀 수 있습니다. 여기서 이 상수는 NULL 결과를 대체하는 Null이 아닌 값입니다. CLR(공용 언어 런타임) 사용자 정의 형식의 식을 바탕으로 한 계산 열에는 해당 형식에 대한 REFERENCES 권한이 필요합니다.

PERSISTED [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]이 계산된 값을 테이블에 물리적으로 저장하고 계산 열이 종속된 다른 열이 업데이트되면 해당 값을 업데이트하도록 지정합니다. 계산 열을 `PERSISTED`로 표시하면 결정적이지만 정확하지는 않은 계산 열에 인덱스를 만들 수 있습니다. 자세한 내용은 [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md)을 참조하세요. 분할된 테이블의 분할 열로 사용되는 모든 계산 열은 명시적으로 `PERSISTED`로 표시되어야 합니다. `PERSISTED`를 지정할 때 *computed_column_expression*은 결정적이어야 합니다.

ON { *partition_scheme* | *filegroup* |  **“default”** } 테이블이 저장된 파티션 구성표 또는 파일 그룹을 지정합니다. *partition_scheme*을 지정하면 해당 테이블은 *partition_scheme*에 지정된 하나 이상의 파일 그룹 집합에 파티션이 저장되는 분할된 테이블이 됩니다. *filegroup*을 지정한 경우에는 테이블이 명명된 파일 그룹에 저장됩니다. 파일 그룹은 데이터베이스 내에 있어야 합니다. **"default"** 를 지정하거나 ON을 전혀 지정하지 않으면 기본 파일 그룹에 테이블이 저장됩니다. CREATE TABLE에 지정된 테이블의 스토리지 메커니즘은 곧이어 변경할 수 없습니다.

ON {*partition_scheme* | *filegroup* |  **"default"** }은 PRIMARY KEY나 UNIQUE 제약 조건에도 지정할 수 있습니다. 이러한 제약 조건은 인덱스를 만듭니다. *filegroup*을 지정한 경우에는 인덱스가 명명된 파일 그룹에 저장됩니다. **"default"** 를 지정하거나 ON을 전혀 지정하지 않으면 테이블과 동일한 파일 그룹에 인덱스가 저장됩니다. `PRIMARY KEY` 또는 `UNIQUE` 제약 조건이 클러스터형 인덱스를 만드는 경우에는 테이블에 대한 데이터 페이지가 인덱스와 동일한 파일 그룹에 저장됩니다. `CLUSTERED`를 지정하거나 아니면 제약 조건이 클러스터형 인덱스를 만들고 테이블 정의의 *partition_scheme* 또는 *filegroup*과는 다르게 *partition_scheme*을 지정하거나 그 반대인 경우에는 제약 조건 정의만 유지하고 나머지는 무시합니다.

> [!NOTE]
> 이 컨텍스트에서 *default*는 키워드가 아닙니다. 기본 파일 그룹에 대한 식별자이며 ON **"default"** 또는 ON **[** default **]** 와 같이 구분되어야 합니다. **"default"** 를 지정하면 현재 세션의 `QUOTED_IDENTIFIER` 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.
>
> 분할된 테이블을 만든 후에는 테이블의 `LOCK_ESCALATION` 옵션을 `AUTO`로 설정하는 것이 좋습니다. 이렇게 하면 테이블 수준이 아닌 파티션(HoBT) 수준으로 잠금이 에스컬레이션되도록 하여 동시성을 향상시킬 수 있습니다. 자세한 내용은 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.

TEXTIMAGE_ON { *filegroup*|  **“default”** } 지정된 파일 그룹에 **text**, **ntext**, **image**, **xml**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** 및 CLR 사용자 정의 형식 열(기하 도형 및 지리 포함)이 저장되어 있음을 나타냅니다.

테이블에 큰 값 열이 없는 경우에는 `TEXTIMAGE_ON`이 허용되지 않습니다. *partition_scheme*을 지정하면 `TEXTIMAGE_ON`을 지정할 수 없습니다. **"default"** 를 지정하거나 `TEXTIMAGE_ON`을 전혀 지정하지 않으면 큰 값 열이 기본 파일 그룹에 저장됩니다. `CREATE TABLE`에 지정된 큰 값 열 데이터의 스토리지는 나중에 변경할 수 없습니다.

> [!NOTE]
> Varchar(max), nvarchar(max), varbinary(max), xml 및 큰 UDT 값은 레코드에 맞는 한 최대 8,000바이트까지 데이터 행에 직접 저장됩니다. 값이 레코드에 맞지 않으면 포인터는 행 내부에 저장되고 나머지는 행 외부 LOB 스토리지 공간에 저장됩니다. 0은 모든 값이 데이터 행에 직접 저장됨을 나타내는 기본값입니다.
>
> `TEXTIMAGE_ON`은 "LOB 스토리지 공간"의 위치만 변경하며, 데이터가 행 내부에 저장되는 경우 아무 영향도 주지 않습니다. sp_tableoption의 large value types out of row 옵션을 사용하여 전체 LOB 값을 행 외부에 저장합니다.
>
> 이 컨텍스트에서 default는 키워드가 아니라 기본 파일 그룹에 대한 식별자이며 `TEXTIMAGE_ON "default"` 또는 `TEXTIMAGE_ON [default]`와 같이 구분되어야 합니다. **"default"** 를 지정하면 현재 세션의 `QUOTED_IDENTIFIER` 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.

FILESTREAM_ON { *partition_scheme_name* | filegroup | **"** default **"** } **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 이상). [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 `FILESTREAM`을 지원하지 않습니다.

FILESTREAM 데이터의 파일 그룹을 지정합니다.

테이블에 FILESTREAM 데이터가 포함되어 있고 테이블이 분할된 경우에는 FILESTREAM_ON 절을 포함해야 하며 이 절에서 FILESTREAM 파일 그룹의 파티션 구성표를 지정해야 합니다. 이 파티션 구성표는 테이블의 파티션 구성표와 동일한 파티션 함수 및 파티션 열을 사용해야 합니다. 그렇지 않으면 오류가 발생합니다.

테이블이 분할되지 않은 경우에는 FILESTREAM 열을 분할할 수 없습니다. 테이블의 FILESTREAM 데이터는 단일 파일 그룹에 저장되어야 합니다. 이 파일 그룹은 FILESTREAM_ON 절에 지정됩니다.

테이블이 분할되지 않고 `FILESTREAM_ON` 절이 지정되지 않은 경우에는 `DEFAULT` 속성이 설정된 FILESTREAM 파일 그룹이 사용됩니다. FILESTREAM 파일 그룹이 없으면 오류가 발생합니다.

ON 및 `TEXTIMAGE_ON`과 마찬가지로 `FILESTREAM_ON`에 대해 `CREATE TABLE`을 사용하여 설정한 값은 다음과 같은 경우를 제외하고 변경할 수 없습니다.

- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 문은 힙을 클러스터형 인덱스로 변환합니다. 이 경우 다른 FILESTREAM 파일 그룹, 파티션 구성표 또는 NULL을 지정할 수 있습니다.
- [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) 문은 클러스터형 인덱스를 힙으로 변환합니다. 이 경우 다른 FILESTREAM 파일 그룹, 파티션 구성표 또는 **"default"** 를 지정할 수 있습니다.

`FILESTREAM_ON <filegroup>` 절의 파일 그룹이나 파티션 구성표에 명명되어 있는 각 FILESTREAM 파일 그룹에는 파일 그룹에 대해 정의된 파일이 하나 포함되어 있어야 합니다. 이 파일은 [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017) 또는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 정의해야 합니다. 그러지 않으면 오류가 발생합니다.

관련 FILESTREAM 항목은 [BLOB(Binary Large Object) - Blob 데이터](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.

[ _type\_schema\_name_ **.** ] *type_name* 열의 데이터 형식과 열이 속한 스키마를 지정합니다. 디스크 기반 테이블의 데이터 형식은 다음 중 하나일 수 있습니다.

- 시스템 데이터 형식
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 기반으로 하는 별칭 형식. 별칭 데이터 형식은 `CREATE TYPE` 문으로 만들어진 다음, 테이블 정의에서 사용됩니다. 별칭 데이터 형식에 대한 NULL 또는 NOT NULL 할당은 `CREATE TABLE` 문 중에 재정의할 수 있습니다. 그러나 길이 지정은 변경할 수 없습니다. 즉, 별칭 데이터 유형의 길이는 `CREATE TABLE` 문에서 지정할 수 없습니다.
- CLR 사용자 정의 형식. CLR 사용자 정의 데이터 형식은 `CREATE TYPE` 문으로 만들어진 다음, 테이블 정의에서 사용됩니다. CLR 사용자 정의 형식으로 열을 만들려면 해당 형식에 대한 REFERENCES 권한이 필요합니다.

*type_schema_name*을 지정하지 않으면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 다음 순서로 *type_name*을 참조합니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식
- 현재 데이터베이스에 있는 현재 사용자의 기본 스키마
- 현재 데이터베이스의 **dbo** 스키마

메모리 최적화 테이블에 대해 지원되는 시스템 형식의 목록은 [메모리 내 OLTP에 지원되는 데이터 형식](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)을 참조하세요.

*precision* 지정된 데이터 형식의 전체 자릿수입니다. 유효한 전체 자릿수 값에 대한 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.

*scale* 지정된 데이터 형식의 소수 자릿수입니다. 유효한 소수 자릿수 값에 대한 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.

**max** 2^31바이트의 문자와 이진 데이터 및 2^30바이트의 유니코드 데이터를 저장하기 위한 **varchar**, **nvarchar** 및 **varbinary** 데이터 형식에만 적용됩니다.

CONTENT *column_name*에 있는 **xml** 데이터 형식의 각 인스턴스가 여러 개의 최상위 요소를 포함할 수 있도록 지정합니다. CONTENT는 **xml** 데이터 형식에만 적용되며 *xml_schema_collection*도 지정한 경우에만 지정할 수 있습니다. 지정하지 않은 경우에는 CONTENT가 기본 동작입니다.

DOCUMENT *column_name*에 있는 **xml** 데이터 형식의 각 인스턴스가 최상위 요소를 하나만 포함할 수 있도록 지정합니다. DOCUMENT는 **xml** 데이터 형식에만 적용되며 *xml_schema_collection*도 지정한 경우에만 지정할 수 있습니다.

*xml_schema_collection* XML 스키마 컬렉션과의 연결을 위해 **xml** 데이터 형식에만 적용됩니다. 스키마에 **xml** 열을 입력하기 전에 먼저 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)을 사용하여 데이터베이스에 해당 스키마를 만들어야 합니다.

DEFAULT 삽입 중에 값이 명시적으로 지정되지 않은 경우에 열에 대해 제공되는 값을 지정합니다. DEFAULT 정의는 **타임스탬프**로 정의되거나 `IDENTITY` 속성이 있는 열을 제외한 모든 열에 적용할 수 있습니다. 사용자 정의 형식 열에 대해 기본값을 지정할 경우 *constant_expression*에서 해당 사용자 정의 형식으로 암시적으로 변환할 수 있어야 합니다. DEFAULT 정의는 테이블이 삭제될 때 제거됩니다. 문자열과 같은 상수 값, 스칼라 함수(시스템 함수, 사용자 정의 함수 또는 CLR 함수) 또는 NULL만 기본값으로 사용할 수 있습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환성을 유지하기 위해 DEFAULT에 제약 조건 이름을 할당할 수 있습니다.

*constant_expression* 열의 기본값으로 사용되는 상수, NULL 또는 시스템 함수입니다.

*memory_optimized_constant_expression* 열의 기본값으로 사용되는 상수, NULL 또는 시스템 함수입니다. 고유하게 컴파일된 저장 프로시저에서 지원되어야 합니다. 고유하게 컴파일된 저장 프로시저의 기본 제공 함수에 대한 자세한 내용은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)을 참조하세요.

IDENTITY 새 열이 ID 열임을 나타냅니다. 테이블에 새 행이 추가되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 열에 대해 고유한 증가값을 제공합니다. ID 열은 일반적으로 PRIMARY KEY 제약 조건과 함께 사용되어 테이블에 대한 고유한 행 식별자 역할을 합니다. `IDENTITY` 속성은 **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)** 또는 **numeric(p,0)** 열에 할당할 수 있습니다. ID 열은 테이블당 하나만 만들 수 있습니다. ID 열에는 바인딩된 기본값 및 DEFAULT 제약 조건을 사용할 수 없습니다. 초기값과 증가값은 둘 다 지정하거나 또는 둘 다 지정하지 않아야 합니다. 둘 다 지정하지 않은 경우에는 기본값 (1,1)이 사용됩니다.

*seed* 테이블에 로드되는 첫 번째 행에 사용하는 값입니다.

*increment* 로드된 이전 행의 ID 값에 추가되는 증가값입니다.

NOT FOR REPLICATION `CREATE TABLE` 문에서 IDENTITY 속성, FOREIGN KEY 제약 조건 및 CHECK 제한 조건에 대해 `NOT FOR REPLICATION` 절을 지정할 수 있습니다. `IDENTITY` 속성에 대해 이 절을 지정하면 복제 에이전트가 삽입 작업을 수행할 때 ID 열의 값이 증가하지 않습니다. 제약 조건에 대해 이 절을 지정하면 복제 에이전트가 삽입, 업데이트 또는 삭제 작업을 수행할 때 해당 제약 조건이 강제로 적용되지 않습니다.

GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] [ NOT NULL ] **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

시스템이 지정된 `datetime2` 열을 사용하여 레코드가 유효한 시작 시간 또는 레코드가 유효한 종료 시간을 기록하도록 지정합니다. 열은 `NOT NULL`로 정의되어야 합니다. 이들을 `NULL`로 지정하려고 하면 시스템에서 오류가 throw됩니다. 기간 열에 NOT NULL을 명시적으로 지정하지 않으면 시스템은 기본적으로 해당 열을 `NOT NULL`로 정의합니다. `PERIOD FOR SYSTEM_TIME` 및 `WITH SYSTEM_VERSIONING = ON` 인수를 이 인수와 함께 사용하여 테이블에서 시스템 버전 관리를 활성화합니다. 자세한 내용은 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)을 참조하세요.

기간 열 한 개 또는 두 개를 모두 **HIDDEN** 플래그로 표시하여 **SELECT \* FROM** _`<table>`_ 이 이러한 열에 대해 값을 반환하지 않도록 해당 열을 암시적으로 숨길 수 있습니다. 기본적으로 기간 열은 숨겨지지 않습니다. 숨겨진 열을 사용하려면 temporal 테이블을 직접 참조하는 모든 쿼리에 이러한 열을 명시적으로 포함해야 합니다. 기존 기간 열의 **HIDDEN** 특성을 변경하려면 **PERIOD**를 삭제하고 다른 숨겨진 플래그를 사용하여 다시 만들어야 합니다.

INDEX *index_name* [ CLUSTERED | NONCLUSTERED ] (*column_name* [ ASC | DESC ] [ ,... *n* ] ) **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

테이블에 인덱스를 만들도록 지정합니다. 이는 클러스터형 인덱스 또는 비클러스터형 인덱스일 수 있습니다. 인덱스는 나열된 열을 포함하며 데이터를 오름차순 또는 내림차순으로 정렬합니다.

INDEX *index_name* CLUSTERED COLUMNSTORE **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

전체 테이블을 클러스터형 columnstore 인덱스를 포함한 열 형식으로 저장하도록 지정합니다. 이는 언제나 테이블의 모든 열을 포함합니다. 데이터는 행이 columnstore의 압축 이점을 얻도록 구성되므로 알파벳순 또는 숫자 순서로 정렬되지 않습니다.

INDEX *index_name* [ NONCLUSTERED ] COLUMNSTORE (*column_name* [ ,... *n* ] ) **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

테이블에 비클러스터형 columnstore 인덱스를 만들도록 지정합니다. 기본 테이블은 rowstore 힙 또는 클러스터형 인덱스이거나 클러스터형 columnstore 인덱스일 수 있습니다. 모든 경우 테이블에 비클러스터형 columnstore 인덱스를 만들면 인덱스 열에 대한 데이터의 두 번째 복사본이 저장됩니다.

비클러스터형 columnstore 인덱스는 클러스터형 columnstore 인덱스로 저장 및 관리됩니다. 이는 열이 제한될 수 있고 테이블에 보조 인덱스로 존재하기 때문에 비클러스터형 columnstore 인덱스라고 부릅니다.

ON _partition\_scheme\_name_ **(** _column\_name_ **)** 분할된 인덱스의 파티션이 매핑될 파일 그룹을 정의하는 파티션 구성표를 지정합니다. 파티션 구성표는 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) 또는 [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)의 실행을 통해 데이터베이스 내에 있어야 합니다. *column_name*은 분할된 인덱스가 분할되는 기준으로 사용할 열을 지정합니다. 이 열은 *partition_scheme_name*에서 사용하는 파티션 함수의 인수와 데이터 형식, 길이 및 전체 자릿수가 일치해야 합니다. *column_name*은 인덱스 정의의 열만 사용할 필요는 없으며 기본 테이블의 모든 열을 지정할 수 있습니다. 단, UNIQUE 인덱스를 분할할 때 고유 키로 사용되는 열 중에서 *column_name*을 선택해야 하는 경우는 제외합니다. 이 제한 사항으로 인해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 단일 파티션 내에서만 키 값의 고유성을 확인할 수 있습니다.

> [!NOTE]
> 비고유 클러스터형 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 기본적으로 지정되지 않은 분할 열을 클러스터형 인덱스 키 목록에 추가합니다. 비고유 비클러스터형 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 지정되지 않은 분할 열을 인덱스의 키가 아닌 포괄 열로 추가합니다.

*partition_scheme_name* 또는 *filegroup*이 지정되지 않고 테이블이 분할된 경우 인덱스는 동일한 분할 열을 사용하여 동일한 파티션 구성표에 기본 테이블로 배치됩니다.

> [!NOTE]
> XML 인덱스에서 파티션 구성표를 지정할 수 없습니다. 기본 테이블이 분할되면 XML 인덱스는 테이블과 동일한 파티션 구성표를 사용합니다.

분할 인덱스에 대한 자세한 내용은 [분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.

ON *filegroup_name* 주어진 파일 그룹에 지정된 인덱스를 만듭니다. 지정된 위치가 없고 테이블 또는 뷰가 분할되지 않은 경우 인덱스는 동일한 파일 그룹을 기본 테이블 또는 뷰로 사용합니다. 파일 그룹은 이미 존재해야 합니다.

ON **"default"** 기본 파일 그룹에 지정된 인덱스를 만듭니다.

이 컨텍스트에서 default는 키워드가 아닙니다. 기본 파일 그룹에 대한 식별자이며 ON **"default"** 또는 ON **[default]** 와 같이 구분되어야 합니다. "default"를 지정하면 현재 세션의 `QUOTED_IDENTIFIER` 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.

[ FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL" } ] **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 이상).

클러스터형 인덱스를 만들 때 테이블에 대한 FILESTREAM 데이터의 위치를 지정합니다. FILESTREAM_ON 절에서 FILESTREAM 데이터를 다른 FILESTREAM 파일 그룹 또는 파티션 구성표로 이동할 수 있습니다.

*filestream_filegroup_name*은 FILESTREAM 파일 그룹의 이름입니다. 파일 그룹에는 [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md) 또는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 파일 그룹에 대해 정의된 파일이 하나 포함되어야 하며, 그렇지 않으면 오류가 발생합니다.

테이블이 분할된 경우에는 `FILESTREAM_ON` 절이 포함되어야 하며 이 절에서 테이블의 파티션 구성표와 동일한 파티션 함수 및 파티션 열을 사용하는 FILESTREAM 파일 그룹의 파티션 구성표를 지정해야 합니다. 그렇지 않으면 오류가 발생합니다.

테이블이 분할되지 않은 경우에는 FILESTREAM 열을 분할할 수 없습니다. 테이블의 FILESTREAM 데이터는 `FILESTREAM_ON` 절에 지정된 단일 파일 그룹에 저장되어야 합니다.

클러스터형 인덱스가 만들어지고 테이블에 FILESTREAM 열이 포함되어 있지 않은 경우 `CREATE INDEX` 문에 `FILESTREAM_ON NULL`을 지정할 수 있습니다.

자세한 내용은 [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.

ROWGUIDCOL 새 열이 행 GUID 열임을 나타냅니다. 테이블당 한 개의 **uniqueidentifier** 열만 ROWGUIDCOL 열로 지정할 수 있으며 ROWGUIDCOL 속성을 적용하면 `$ROWGUID`를 사용하여 열을 참조할 수 있습니다. ROWGUIDCOL 속성은 **uniqueidentifier** 열에만 할당할 수 있습니다. 사용자 정의 데이터 형식 열은 ROWGUIDCOL로 지정할 수 없습니다.

ROWGUIDCOL 속성은 열에 저장된 값이 고유하도록 강제 적용하지 않습니다. 또한 테이블에 삽입된 새 행에 대한 값을 자동으로 생성하지도 않습니다. 각 열에 고유한 값을 생성하려면 [INSERT](../../t-sql/statements/insert-transact-sql.md) 문에 [NEWID](../../t-sql/functions/newid-transact-sql.md) 또는 [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) 함수를 사용하거나 열에 대한 기본값으로 이러한 함수를 사용하십시오.

ENCRYPTED WITH [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능을 사용하여 열 암호화를 지정합니다.

COLUMN_ENCRYPTION_KEY = *key_name* 열 암호화 키를 지정합니다. 자세한 내용은 [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)를 참조하세요.

ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } **결정적 암호화**는 지정된 일반 텍스트 값에 대해 항상 동일한 암호화된 값을 생성하는 방법을 사용합니다. 결정적 암호화를 사용하면 암호화된 값을 기반으로 같음 비교를 이용한 검색, 그룹화 및 같음 조인을 이용한 조인이 가능하지만, 권한이 없는 사용자가 암호화된 열의 패턴을 검사하여 암호화된 값에 관한 정보를 추측할 수도 있습니다. 결정적으로 암호화된 열의 두 테이블 조인은 두 열이 모두 같은 열 암호화 키를 사용하여 암호화된 경우에만 가능합니다. 결정적 암호화에서는 문자 열에 대해 binary2 정렬 순서를 적용하는 열 데이터 정렬을 사용해야 합니다.

**임의 암호화** 는 예측하기 어려운 방식으로 데이터를 암호화하는 방법을 사용합니다. 임의 암호화는 좀 더 안전하지만 SQL Server 인스턴스가 보안 Enclave를 사용한 Always Encrypted를 지원하지 않으면, 암호화된 열에서 계산 및 인덱싱을 수행할 수 없습니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.

Always Encrypted(보안 Enclave를 사용하지 않음)를 사용할 경우 매개 변수 또는 그룹화 매개 변수(예: 정부 ID 번호)를 사용하여 검색할 열에 대해 결정적 암호화를 사용합니다. 다른 레코드와 함께 그룹화되지 않거나 테이블을 조인하는 데 사용되고 관심이 있는 암호화된 열을 포함한 행을 찾는 데에는 다른 열(거래 번호 등)을 사용하기 때문에 검색되지 않는 데이터(예: 신용 카드 번호)에 임의 암호화를 사용합니다.

보안 Enclave에서 Always Encrypted를 사용할 경우 임의 암호화가 권장되는 암호화 유형입니다.

열은 한정 데이터 형식이어야 합니다.

ALGORITHM **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상).

**'AEAD_AES_256_CBC_HMAC_SHA_256'** 이어야 합니다.

기능 제약 조건을 포함한 자세한 내용은 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요.

SPARSE 열이 스파스 열임을 나타냅니다. 스파스 열의 스토리지는 Null 값에 대해 최적화됩니다. 스파스 열은 NOT NULL로 지정할 수 없습니다. 추가 제한 사항 및 스파스 열에 대한 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.

MASKED WITH ( FUNCTION = ' *mask_function* ') **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상).

동적 데이터 마스크를 지정합니다. *mask_function*은 적절한 매개 변수를 포함한 마스킹 함수의 이름 입니다. 네 개의 함수를 사용할 수 있습니다.

- default()
- email()
- partial()
- random()

함수 매개 변수에 대해서는 [동적 데이터 마스킹](../../relational-databases/security/dynamic-data-masking.md)을 참조하세요.

FILESTREAM **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 이상)

**varbinary(max)** 열에 대해서만 유효합니다. **varbinary(max)** BLOB 데이터에 대한 FILESTREAM 스토리지를 지정합니다.

테이블에는 ROWGUIDCOL 특성을 갖는 **uniqueidentifier** 데이터 형식의 열도 있어야 합니다. 이 열은 Null 값을 허용하지 않으며 UNIQUE 또는 PRIMARY KEY 단일 열 제약 조건을 가져야 합니다. 열의 GUID 값은 애플리케이션에서 데이터를 삽입할 때 제공하거나 NEWID () 함수를 사용하는 DEFAULT 제약 조건을 통해 제공해야 합니다.

테이블에 대해 정의된 FILESTREAM 열이 있는 동안에는 ROWGUIDCOL 열을 삭제하고 관련 제약 조건을 변경할 수 없습니다. ROWGUIDCOL 열은 마지막 FILESTREAM 열이 삭제된 이후에만 삭제될 수 있습니다.

열에 대해 FILESTREAM 스토리지 특성이 지정된 경우 해당 열의 모든 값이 파일 시스템에 있는 FILESTREAM 데이터 컨테이너에 저장됩니다.

COLLATE *collation_name* 열에 대한 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. *collation_name*은 **char**, **varchar**, **text**, **nchar**, **nvarchar** 및 **ntext** 데이터 형식의 열에만 적용할 수 있습니다. 지정하지 않은 경우 열이 사용자 정의 데이터 형식이면 사용자 정의 데이터 형식의 데이터 정렬에 열이 할당되고 그렇지 않은 경우에는 데이터베이스의 기본 데이터 정렬에 할당됩니다.

Windows 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [Windows 데이터 정렬 이름](../../t-sql/statements/windows-collation-name-transact-sql.md)과 [SQL 데이터 정렬 이름](../../t-sql/statements/sql-server-collation-name-transact-sql.md)을 참조하세요.

자세한 내용은 [COLLATE](~/t-sql/statements/collations.md)를 참조하세요.

CONSTRAINT PRIMARY KEY, NOT NULL, UNIQUE, FOREIGN KEY 또는 CHECK 제약 조건 정의의 시작을 표시하는 선택적인 키워드입니다.

*constraint_name* 제약 조건의 이름입니다. 제약 조건 이름은 테이블이 속한 스키마 내에서 고유한 이름이어야 합니다.

NULL | NOT NULL 열의 Null 값 허용 여부를 결정합니다. NULL은 엄격하게 말해 제약 조건이 아니지만 NOT NULL처럼 지정할 수 있습니다. 계산 열에서는 PERSISTED를 지정한 경우에만 NOT NULL을 지정할 수 있습니다.

PRIMARY KEY 지정한 열에 고유 인덱스를 통해 엔터티 무결성을 적용하는 제약 조건입니다. PRIMARY KEY 제약 조건은 각 테이블마다 하나만 만들 수 있습니다.

UNIQUE 지정한 열에 대해 고유 인덱스를 통해 엔터티 무결성을 적용하는 제약 조건입니다. 하나의 테이블이 여러 개의 UNIQUE 제약 조건을 가질 수 있습니다.

CLUSTERED | NONCLUSTERED PRIMARY KEY 또는 UNIQUE 제약 조건에 대해 클러스터형 또는 비클러스터형 인덱스를 만들도록 지정합니다. PRIMARY KEY 제약 조건의 기본값은 CLUSTERED이며 UNIQUE 제약 조건의 기본값은 NONCLUSTERED입니다.

`CREATE TABLE` 문에서는 하나의 제약 조건에만 CLUSTERED를 지정할 수 있습니다. UNIQUE 제약 조건에 대해 CLUSTERED를 지정하고 PRIMARY KEY 제약 조건도 지정한 경우 PRIMARY KEY의 기본값은 NONCLUSTERED입니다.

FOREIGN KEY REFERENCES 열에 있는 데이터에 대한 참조 무결성을 제공하는 제약 조건입니다. FOREIGN KEY 제약 조건을 지정하려면 열의 각 값이 참조된 테이블의 참조된 해당 열에 있어야 합니다. FOREIGN KEY 제약 조건은 참조되는 테이블의 PRIMARY KEY 또는 UNIQUE 제약 조건 열이나 참조되는 테이블의 UNIQUE INDEX에서 참조되는 열만 참조할 수 있습니다. 계산 열의 외래 키 또한 PERSISTED로 표시되어야 합니다.

[ _schema\_name_ **.** ] *referenced_table_name*] FOREIGN KEY 제약 조건이 참조하는 테이블과 그 테이블이 속한 스키마의 이름입니다.

**(** *ref_column* [ **,** ... *n* ] **)** FOREIGN KEY 제약 조건이 참조하는 테이블의 열 또는 열 목록입니다.

ON DELETE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT } 행이 참조 관계를 가지고 참조된 행이 부모 테이블에서 삭제될 경우에 테이블의 행에 수행될 동작을 지정합니다. 기본값은 NO ACTION입니다.

NO ACTION [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 오류가 발생하며 부모 테이블의 행에 대한 삭제 동작이 롤백됩니다.

CASCADE 부모 테이블에서 행을 삭제한 경우 참조 테이블에서 해당 행이 삭제됩니다.

SET NULL 부모 테이블에서 해당 행을 삭제하면 외래 키를 구성하는 모든 값이 NULL로 설정됩니다. 이 제약 조건을 실행하려면 외래 키 열이 Null을 허용해야 합니다.

SET DEFAULT 부모 테이블에서 해당 행을 삭제하면 외래 키를 구성하는 모든 값이 기본값으로 설정됩니다. 이 제약 조건을 실행하려면 모든 외래 키 열에 기본 정의가 있어야 합니다. 열이 Null을 허용하고 명시적 기본값이 설정되어 있지 않은 경우 NULL은 해당 열의 암시적 기본값이 됩니다.

논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 CASCADE를 지정하지 마세요. 논리적 레코드에 대한 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.

`INSTEAD OF` 트리거 `ON DELETE`가 테이블에 이미 있는 경우 `ON DELETE CASCADE`를 정의할 수 없습니다.

예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 **ProductVendor** 테이블은 **Vendor** 테이블과 참조 관계를 갖습니다. **ProductVendor.BusinessEntityID** 외래 키는 **Vendor.BusinessEntityID** 기본 키를 참조합니다.

**Vendor** 테이블의 행에서 `DELETE` 문이 실행되고 **ProductVendor.BusinessEntityID**에 대해 `ON DELETE CASCADE` 작업이 지정된 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]는 **ProductVendor** 테이블에서 하나 이상의 종속 행이 있는지 확인합니다. **ProductVendor** 테이블에 종속 행이 있는 경우 삭제되며 **Vendor** 테이블에서 참조된 행도 삭제됩니다.

반대로 `NO ACTION`을 지정한 경우 **ProductVendor** 테이블에 **Vendor** 행을 참조하는 행이 하나 이상 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생하고 Vendor 행의 삭제 동작이 롤백됩니다.

ON UPDATE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT } 변경된 테이블의 행에 참조 관계가 있고 참조된 행이 부모 테이블에서 업데이트될 경우 해당 행에 대해 발생할 동작을 지정합니다. 기본값은 NO ACTION입니다.

NO ACTION [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 오류가 발생하며 부모 테이블의 행에 대한 업데이트 동작이 롤백됩니다.

CASCADE 부모 테이블에서 행이 업데이트될 때 참조 테이블에서도 해당 행이 업데이트됩니다.

SET NULL 부모 테이블에서 행을 업데이트하면 해당 외래 키를 구성하는 모든 값이 NULL로 설정됩니다. 이 제약 조건을 실행하려면 외래 키 열이 Null을 허용해야 합니다.

SET DEFAULT 부모 테이블에서 행을 업데이트하면 해당 외래 키를 구성하는 모든 값이 기본값으로 설정됩니다. 이 제약 조건을 실행하려면 모든 외래 키 열에 기본 정의가 있어야 합니다. 열이 Null을 허용하고 명시적 기본값이 설정되어 있지 않은 경우 NULL은 해당 열의 암시적 기본값이 됩니다.

논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 `CASCADE`를 지정하지 마세요. 논리적 레코드에 대한 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.

`INSTEAD OF` 트리거 `ON UPDATE`가 테이블에 이미 있는 경우 `ON UPDATE CASCADE`, `SET NULL` 또는 `SET DEFAULT`를 정의할 수 없습니다.

예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 **ProductVendor** 테이블은 **Vendor** 테이블과 참조 관계를 갖습니다. **ProductVendor.BusinessEntity** 외래 키는 **Vendor.BusinessEntityID** 기본 키를 참조합니다.

**Vendor** 테이블의 행에 대해 UPDATE 문을 실행하고 **ProductVendor.BusinessEntityID**에 대해 ON UPDATE CASCADE 동작을 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 **ProductVendor** 테이블에 하나 이상의 종속 행이 있는지 확인합니다. **ProductVendor** 테이블에 종속 행이 있는 경우 업데이트되며 **Vendor** 테이블에서 참조된 행도 업데이트됩니다.

반대로 NO ACTION을 지정한 경우 **ProductVendor** 테이블에 **Vendor** 행을 참조하는 행이 하나 이상 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류가 발생하고 Vendor 행의 업데이트 동작이 롤백됩니다.

CHECK 열에 입력 가능한 값을 제한하여 도메인 무결성을 적용하는 제약 조건입니다. 계산 열의 CHECK 제약 조건 또한 PERSISTED로 표시되어야 합니다.

*logical_expression* TRUE 또는 FALSE를 반환하는 논리 식입니다. 별칭 데이터 형식은 식에 포함될 수 없습니다.

*column* 제약 조건 정의에서 사용하는 열을 표시하기 위해 테이블 제약 조건에서 괄호로 묶어 사용하는 열 또는 열 목록입니다.

[ **ASC** | DESC ] 테이블 제약 조건에 사용되는 열의 정렬 순서를 지정합니다. 기본값은 ASC입니다.

*partition_scheme_name* 분할된 테이블의 파티션이 매핑될 파일 그룹을 정의하는 파티션 구성표의 이름입니다. 파티션 구성표는 데이터베이스 내에 있어야 합니다.

[ _partition\_column\_name_ **.** ] 분할된 테이블의 분할 기준 열을 지정합니다. 열은 *partition_scheme_name*에서 사용하는 파티션 함수에 지정된 열과 데이터 형식, 길이 및 전체 자릿수에서 일치해야 합니다. 파티션 함수에 참여하는 계산 열은 명시적으로 PERSISTED로 표시되어야 합니다.

> [!IMPORTANT]
> 분할된 테이블 및 ALTER TABLE...SWITCH 작업의 원본이나 대상인 분할되지 않은 테이블의 분할 열에 NOT NULL을 지정하는 것이 좋습니다. 이렇게 하면 분할 열의 CHECK 제약 조건에서 Null 값을 확인하지 않아도 됩니다.

WITH FILLFACTOR **=** _fillfactor_[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 인덱스 데이터를 저장하는 데 사용하는 각 인덱스 페이지를 채우는 정도를 지정합니다. 사용자가 지정한 *fillfactor* 값은 1에서 100 사이일 수 있습니다. 값을 지정하지 않으면 기본값 0이 사용됩니다. 채우기 비율 값 0과 100은 모든 면에서 동일합니다.

> [!IMPORTANT]
> 현재 WITH FILLFACTOR = *fillfactor*가 PRIMARY KEY 또는 UNIQUE 제약 조건에 적용되는 유일한 인덱스 옵션으로 기술되어 있는 것은 이전 버전과의 호환성을 위한 것이며 이후 릴리스에서는 이런 식으로 기술되지 않을 것입니다.

*column_set_name* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS 열 집합의 이름입니다. 열 집합은 구조화된 출력으로 테이블의 모든 스파스 열을 결합하는 형식화되지 않은 XML 표현입니다. 열 집합에 대한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.

PERIOD FOR SYSTEM_TIME (*system_start_time_column_name* , *system_end_time_column_name* ) **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

시스템에서 레코드가 유효한 기간을 기록하기 위해 사용할 열의 이름을 지정합니다. GENERATED ALWAYS AS ROW { START | END } 및 WITH SYSTEM_VERSIONING = ON 인수와 함께 이 인수를 사용하여 테이블에 대한 시스템 버전 관리를 활성화합니다. 자세한 내용은 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)을 참조하세요.

COMPRESSION_DELAY **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

메모리 최적화를 위해 행이 columnstore 인덱스로 압축에 적합하게 될 때까지 변경되지 않고 테이블에 남아 있어야 하는 최소 분 수를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 마지막 업데이트 시간에 따라 압축할 특정 행을 선택합니다. 예를 들어 행이 두 시간 동안 자주 변경되는 경우 `COMPRESSION_DELAY = 120 Minutes`를 설정하여 SQL Server가 행을 압축하기 전에 업데이트가 완료되도록 할 수 있습니다.

디스크 기반 테이블의 경우 지연은 CLOSED 상태의 델타 rowgroup을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 압축된 rowgroup으로 압축할 수 있게 될 때까지 델타 rowgroup에 남아 있어야 하는 최소 시간(분)을 지정합니다. 디스크 기반 테이블은 개별 행에 대한 삽입 및 업데이트 시간을 추적하지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 CLOSED 상태의 델타 rowgroup에 지연을 적용합니다.

기본값은 0분입니다.

`COMPRESSION_DELAY` 사용 시기에 관한 권장 사항은 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)을 참조하세요.

\< table_option> ::= 하나 이상의 테이블 옵션을 지정합니다.

DATA_COMPRESSION 지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 옵션은 다음과 같습니다.

NONE 테이블 또는 지정된 파티션이 압축되지 않습니다.

ROW 테이블 또는 지정된 파티션이 행 압축을 사용하여 압축됩니다.

PAGE 테이블 또는 지정된 파티션이 페이지 압축을 사용하여 압축됩니다.

COLUMNSTORE

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE는 성능이 가장 우수한 columnstore 압축으로 압축하도록 지정합니다. 이는 일반적인 선택입니다.

COLUMNSTORE_ARCHIVE **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE_ARCHIVE는 테이블 또는 파티션을 보다 작은 크기로 더욱 압축합니다. 보다 적은 스토리지 크기가 필요한 기타 상황에서 보관하는 데 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.

자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.

ON PARTITIONS **(** { `<partition_number_expression>` | [ **,** ...*n* ] **)** DATA_COMPRESSION 설정을 적용할 파티션을 지정합니다. 테이블이 분할되지 않은 경우 `ON PARTITIONS` 인수를 사용하면 오류가 발생합니다. `ON PARTITIONS` 절이 제공되지 않으면 `DATA_COMPRESSION` 옵션이 분할된 테이블의 모든 파티션에 적용됩니다.

*partition_number_expression*은 다음과 같은 방법으로 지정할 수 있습니다.

- 파티션의 파티션 번호를 제공합니다(예: `ON PARTITIONS (2)`).
- 여러 개별 파티션의 파티션 번호를 쉼표로 구분하여 지정합니다. 예: `ON PARTITIONS (1, 5)`
- 범위와 개별 파티션을 모두 지정합니다. 예: `ON PARTITIONS (2, 4, 6 TO 8)`

`<range>`는 TO라는 단어로 구분된 파티션 번호로 지정할 수 있습니다(예: `ON PARTITIONS (6 TO 8)`).

여러 파티션에 대해 서로 다른 데이터 압축 유형을 설정하려면 `DATA_COMPRESSION` 옵션을 두 번 이상 지정합니다. 예를 들면 다음과 같습니다.

```sql
WITH
(
    DATA_COMPRESSION = NONE ON PARTITIONS (1),
    DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),
    DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)
)
```

\<index_option> ::= 하나 이상의 인덱스 옵션을 지정합니다. 이러한 옵션에 대한 자세한 설명은 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.

PAD_INDEX = { ON | **OFF** } ON이면 FILLFACTOR로 지정한 사용 가능한 공간의 비율을 인덱스의 중간 수준 페이지에 적용합니다. OFF이거나 FILLFACTOR 값을 지정하지 않으면 중간 페이지의 키 집합을 고려하여 인덱스가 가질 수 있는 최대 크기의 행을 최소한 하나만큼 저장할 공간을 남기고 용량 한계에 가깝게 중간 수준 페이지를 채웁니다. 기본값은 OFF입니다.

FILLFACTOR **=** _fillfactor_ 인덱스를 만들거나 변경할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. *fillfactor*는 1에서 100 사이의 정수 값이어야 하며 기본값은 0입니다. 채우기 비율 값 0과 100은 모든 면에서 동일합니다.

IGNORE_DUP_KEY = { ON | **OFF** } 이 옵션은 삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려는 경우에 대한 오류 응답을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) 또는 [UPDATE](../../t-sql/queries/update-transact-sql.md)를 실행하는 경우에는 이 옵션이 아무런 영향을 미치지 않습니다. 기본값은 OFF입니다.

ON 중복된 키 값이 고유 인덱스에 삽입되는 경우 경고 메시지가 나타나고 고유성 제약 조건을 위반하는 행만 실패합니다.

OFF 중복된 키 값이 고유 인덱스에 삽입되는 경우 오류 메시지가 나타나고 전체 INSERT 작업이 롤백됩니다.

뷰, 비고유 인덱스, XML 인덱스, 공간 인덱스 및 필터링된 인덱스에 생성된 인덱스의 경우 `IGNORE_DUP_KEY`를 ON으로 설정할 수 없습니다.

`IGNORE_DUP_KEY`를 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)를 사용합니다.

이전 버전과 호환되는 구문에서 `WITH IGNORE_DUP_KEY`는 `WITH IGNORE_DUP_KEY = ON`과 동일합니다.

STATISTICS_NORECOMPUTE **=** { ON | **OFF** } ON이면 오래된 인덱스 통계를 자동으로 다시 계산하지 않습니다. OFF이면 자동 통계 업데이트를 활성화합니다. 기본값은 OFF입니다.

ALLOW_ROW_LOCKS **=** { **ON** | OFF } ON이면 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다. OFF이면 행 잠금을 사용하지 않습니다. 기본값은 ON입니다.

ALLOW_PAGE_LOCKS **=** { **ON** | OFF } ON이면 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다. OFF이면 페이지 잠금을 사용하지 않습니다. 기본값은 ON입니다.

OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | **OFF** } **적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 이상. <BR>
마지막 페이지 삽입 경합에 최적화할지 여부를 지정합니다. 기본값은 OFF입니다. 자세한 내용은 CREATE INDEX 페이지의 [순차 키](./create-index-transact-sql.md#sequential-keys) 섹션을 참조하세요.

FILETABLE_DIRECTORY = *directory_name*

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상).

Windows 호환 FileTable 디렉터리 이름을 지정합니다. 이 이름은 데이터베이스의 모든 FileTable 디렉터리 이름 중에서 고유해야 합니다. 고유성을 비교할 때는 데이터 정렬 설정과 관계없이 대/소문자가 구분되지 않습니다. 이 값을 지정하지 않으면 Filetable의 이름이 사용됩니다.

FILETABLE_COLLATE_FILENAME = { *collation_name* | database_default }

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상). [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 `FILETABLE`을 지원하지 않습니다.

FileTable의 **Name** 열에 적용할 데이터 정렬의 이름을 지정합니다. 데이터 정렬은 Windows 운영 체제 파일 명명 의미 체계를 따르도록 대/소문자를 구분하지 않아야 합니다. 이 값을 지정하지 않으면 데이터베이스 기본 데이터 정렬이 사용됩니다. 데이터베이스 기본 데이터 정렬이 대/소문자를 구분하면 오류가 발생하고 CREATE TABLE 작업이 실패합니다.

*collation_name* 대/소문자를 구분하지 않는 데이터 정렬의 이름입니다.

database_default 데이터베이스의 기본 데이터 정렬을 사용하도록 지정합니다. 이 데이터 정렬은 대/소문자를 구분하지 않아야 합니다.

FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = *constraint_name*
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상).

FileTable에 자동으로 만들어지는 기본 키 제약 조건에 사용할 이름을 지정합니다. 이 값을 지정하지 않으면 시스템에서 제약 조건 이름을 생성합니다.

FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = *constraint_name*
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상).

FileTable에서 **stream_id** 열에 자동으로 만들어지는 고유한 제약 조건에 사용할 이름을 지정합니다. 이 값을 지정하지 않으면 시스템에서 제약 조건 이름을 생성합니다.

FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = *constraint_name*
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상).

FileTable에서 **parent_path_locator** 및 **name** 열에 자동으로 만들어지는 고유한 제약 조건에 사용할 이름을 지정합니다. 이 값을 지정하지 않으면 시스템에서 제약 조건 이름을 생성합니다.

SYSTEM_VERSIONING **=** ON [ ( HISTORY_TABLE **=** *schema_name* .*history_table_name* [, DATA_CONSISTENCY_CHECK **=** { **ON** | OFF } ] ) ] **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]).

데이터 형식, NULL 허용 여부 제약 조건 및 기본 키 제약 조건 요구 사항이 충족된 경우 테이블의 시스템 버전 관리를 활성화합니다. `HISTORY_TABLE` 인수를 사용하지 않는 경우 시스템에서 현재 테이블의 동일한 파일 그룹에 있는 현재 테이블의 스키마와 일치하는 새 기록 테이블을 생성하여 두 테이블 간에 링크를 만들고 시스템이 기록 테이블의 현재 테이블에서 각 레코드의 기록을 기록할 수 있도록 합니다. 이 기록 테이블의 이름은 `MSSQL_TemporalHistoryFor<primary_table_object_id>`가 됩니다. 기본적으로 기록 테이블은 **PAGE** (으)로 압축됩니다. `HISTORY_TABLE` 인수를 사용하여 기존 기록 테이블에 대한 링크를 만들고 해당 테이블을 사용하면 현재 테이블과 지정된 테이블 간에 링크가 생성됩니다. 구성 분할은 현재 테이블에서 기록 테이블로 자동 복제를 수행하지 않기 때문에 현재 테이블이 분할된 경우 기록 테이블은 기본 파일 그룹에 생성됩니다. 기록 테이블 생성 도중 기록 테이블의 이름을 지정하는 경우 스키마와 테이블 이름을 지정해야 합니다. 기존 기록 테이블에 대한 링크를 만드는 경우 데이터 일관성 검사를 수행하도록 선택할 수 있습니다. 이 데이터 일관성 확인을 통해 기존 레코드가 겹치지 않도록 합니다. 기본값은 데이터 일관성 검사를 수행하는 것입니다. `PERIOD FOR SYSTEM_TIME` 및 `GENERATED ALWAYS AS ROW { START | END }` 인수를 이 인수와 함께 사용하여 테이블에서 시스템 버전 관리를 활성화합니다. 자세한 내용은 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)을 참조하세요.

REMOTE_DATA_ARCHIVE = { ON [ ( *table_stretch_options* [,...n] ) ] | OFF ( MIGRATION_STATE = PAUSED ) } **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상).

Stretch Database가 활성화 또는 비활성화된 상태에서 새 테이블을 만듭니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.

**테이블에 대해 Stretch Database 활성화**

테이블에 대해 `ON`을 지정하여 Stretch를 사용하도록 설정한 경우 선택적으로 `MIGRATION_STATE = OUTBOUND`를 지정하여 데이터 마이그레이션을 즉시 시작하거나 `MIGRATION_STATE = PAUSED`를 지정하여 데이터 마이그레이션을 연기할 수 있습니다. 기본값은 `MIGRATION_STATE = OUTBOUND`입니다. 테이블의 Stretch 활성화에 대한 자세한 내용은 [테이블에 대한 Stretch Database 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)를 참조하세요.

**필수 구성 요소**. 테이블에 대해 Stretch를 활성화하기 전에 서버 및 데이터베이스에서 Stretch를 활성화해야 합니다. 자세한 내용은 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)를 참조하십시오.

**사용 권한**. 데이터베이스 또는 테이블에 대해 Stretch를 활성화하려면 db_owner 권한이 필요합니다. 또한 테이블에 대해 Stretch를 활성화하면 테이블에 대한 ALTER 권한이 필요합니다.

[ FILTER_PREDICATE = { null | *predicate* } ] **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상).

선택적으로 필터 조건자를 지정하여 기록 및 현재 데이터를 모두 포함하는 테이블에서 마이그레이션할 행을 선택합니다. 조건자는 결정적 인라인 테이블 반환 함수를 호출해야 합니다. 자세한 내용은 [테이블에 대해 Stretch Database 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 및 [필터 함수를 사용하여 마이그레이션할 행 선택](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조하세요.

> [!IMPORTANT]
> 제대로 수행되지 않는 필터 조건자를 제공하면 데이터 마이그레이션 성능도 저하됩니다. Stretch Database는 CROSS APPLY 연산자를 사용하여 테이블에 필터 조건자를 적용합니다.

필터 조건자를 지정하지 않으면 전체 테이블이 마이그레이션됩니다.

필터 조건자를 지정할 경우 *MIGRATION_STATE*도 지정해야 합니다.

MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED } **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

- `OUTBOUND`를 지정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]로 데이터를 마이그레이션합니다.
- `INBOUND`를 지정하여 테이블의 원격 데이터를 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 다시 복사하고 테이블에 대한 Stretch를 비활성화합니다. 자세한 내용은 [Stretch Database 비활성화 및 원격 데이터 다시 가져오기](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)를 사용하세요.

   이 작업은 데이터 전송 비용이 소요되며, 취소할 수 없습니다.

- `PAUSED`를 지정하여 데이터 마이그레이션을 일시 중지하거나 연기합니다. 자세한 내용은 [데이터 마이그레이션 일시 중지 및 다시 계속 - Stretch Database](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)를 참조하세요.

MEMORY_OPTIMIZED **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]). [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 관리형 인스턴스는 메모리 최적화 테이블을 지원하지 않습니다.

값 ON은 테이블이 메모리 최적화된 형식임을 나타냅니다. 메모리 최적화된 테이블은 트랜잭션 처리의 성능을 최적화하기 위해 사용되는 메모리 내 OLTP 기능의 일부입니다. 메모리 내 OLTP를 시작하려면 [빠른 시작 1: 더 빠른 Transact-SQL 성능을 위한 메모리 내 OLTP 기술](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)을 참조하세요. 메모리 최적화 테이블에 대한 더 심층적인 내용은 [메모리 최적화 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)을 참조하세요.

기본값 OFF는 테이블이 디스크 기반임을 나타냅니다.

DURABILITY **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

`SCHEMA_AND_DATA`의 값은 테이블이 내구성이 있음을 나타냅니다. 이는 변경 내용이 디스크에 유지되고 다시 시작 또는 장애 조치(failover) 시에 존속된다는 것을 의미합니다. SCHEMA_AND_DATA는 기본값입니다.

`SCHEMA_ONLY`의 값은 테이블이 비영구적임을 나타냅니다. 테이블 스키마는 유지되지만 데이터 업데이트는 데이터베이스를 다시 시작하거나 장애 조치할 때 삭제됩니다. `DURABILITY = SCHEMA_ONLY`는 `MEMORY_OPTIMIZED = ON`에서만 허용됩니다.

> [!WARNING]
> **DURABILITY = SCHEMA_ONLY**를 사용하여 테이블이 만들어지고 그 후에 **READ_COMMITTED_SNAPSHOT**이 **ALTER DATABASE**를 사용하여 변경되면 테이블의 데이터는 손실됩니다.

BUCKET_COUNT **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

해시 인덱스에서 만들어야 하는 버킷 수를 나타냅니다. 해시 인덱스에서 BUCKET_COUNT의 최대값은 1,073,741,824입니다. 메모리 최적화 테이블의 인덱스에 대한 자세한 내용은 [Memory-Optimized Tables에 대한 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)를 참조하세요.

Bucket_count는 필수 인수입니다.

INDEX **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]).

CREATE TABLE 문의 일부로 열 및 테이블 인덱스를 지정할 수 있습니다. 메모리 최적화 테이블에서 인덱스 추가 및 제거에 대한 자세한 내용은 다음을 참조하세요. [메모리 액세스에 최적화된 테이블 변경](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)

HASH **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

HASH 인덱스가 만들어졌음을 나타냅니다.

해시 인덱스는 메모리 최적화 테이블에서만 지원됩니다.

## <a name="remarks"></a>설명

허용되는 테이블, 열, 제약 조건 및 인덱스 수에 대한 자세한 내용은 [SQL Server에 대한 최대 용량 사양](../../sql-server/maximum-capacity-specifications-for-sql-server.md)을 참조하세요.

테이블 및 인덱스에 대한 공간 할당은 일반적으로 한 번에 한 익스텐트씩 이루어집니다. `ALTER DATABASE`의 `SET MIXED_PAGE_ALLOCATION` 옵션이 TRUE로 설정되거나 항상 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이전에 테이블 또는 인덱스가 생성될 때 이는 균일 익스텐트를 채울 수 있는 충분한 페이지가 있을 때까지 혼합 익스텐트에서 페이지가 할당됩니다. 균일 익스텐트를 채울 정도로 충분한 페이지를 받은 이후에는 현재 할당된 익스텐트가 가득 찰 때마다 추가 익스텐트가 할당됩니다. 테이블에서 할당하고 사용하는 공간의 크기에 대한 보고서의 경우 `sp_spaceused`를 실행하세요.

[!INCLUDE[ssDE](../../includes/ssde-md.md)]은 열 정의에 DEFAULT, IDENTITY, ROWGUIDCOL 또는 열 제약 조건을 지정하는 특정한 순서를 요구하지는 않습니다.

QUOTED IDENTIFIER 옵션은 테이블을 만들 때 OFF로 설정되어 있더라도 해당 테이블의 메타데이터에 항상 ON으로 저장됩니다.

## <a name="temporary-tables"></a>임시 테이블

로컬 및 전역 임시 테이블을 만들 수 있습니다. 로컬 임시 테이블은 현재 세션에서만 볼 수 있으며 전역 임시 테이블은 모든 세션에서 볼 수 있습니다. 임시 테이블은 분할할 수 없습니다.

로컬 임시 테이블 이름 앞에는 숫자 기호가 하나 추가되고(예: #*table_name*) 전역 임시 테이블 이름 앞에는 숫자 기호가 두 개 추가됩니다(예: ##*table_name*).

[!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 `CREATE TABLE` 문의 *table_name*에 대해 지정된 값을 사용하여 임시 테이블을 참조합니다. 예를 들면 다음과 같습니다.

```sql
CREATE TABLE #MyTempTable (
    col1 INT PRIMARY KEY
);

INSERT INTO #MyTempTable
VALUES (1);
```

단일 저장 프로시저나 일괄 처리 내에 둘 이상의 임시 테이블을 만드는 경우 그 이름이 서로 달라야 합니다.

임시 테이블을 만들거나 테이블에 액세스할 때 *schema_name*을 포함하면 무시됩니다. 모든 임시 테이블은 dbo 스키마에서 생성됩니다.

여러 사용자가 동시에 실행할 수 있는 저장 프로시저 또는 애플리케이션에서 로컬 임시 테이블을 만드는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 다른 사용자가 만든 테이블을 구별할 수 있어야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 내부적으로 각 로컬 임시 테이블 이름에 숫자 접미사를 추가하여 구별합니다. **tempdb**의 **sysobjects** 테이블에 저장된 것과 같은 임시 테이블의 전체 이름은 CREATE TABLE 문에서 지정한 테이블 이름과 시스템이 생성한 숫자 접미사로 구성됩니다. 접미사를 추가해야 하므로 로컬 임시 이름으로 지정된 *table_name*은 116자를 초과할 수 없습니다.

임시 테이블은 DROP TABLE을 사용하여 명시적으로 삭제하지 않으면 범위를 벗어날 때 자동으로 삭제됩니다.

- 저장 프로시저에서 만든 로컬 임시 테이블은 저장 프로시저를 마칠 때 자동으로 삭제합니다. 테이블은 해당 테이블을 만든 저장 프로시저가 실행하는 모든 중첩된 저장 프로시저에서 참조할 수 있습니다. 테이블을 만든 저장 프로시저를 호출한 프로세스는 해당 테이블을 참조할 수 없습니다.
- 기타 모든 로컬 임시 테이블은 현재 세션이 끝날 때 자동으로 삭제됩니다.
- 전역 임시 테이블은 테이블을 만든 세션이 끝나고 이를 참조하는 다른 모든 태스크가 중지되면 자동으로 삭제됩니다. 태스크와 테이블 간의 연결은 단일 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 사용 기간 동안만 유지 관리됩니다. 즉, 전역 임시 테이블은 만들기 세션이 끝났을 때 활동적으로 테이블을 참조하는 마지막 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 완료되면 삭제됩니다.

저장 프로시저 또는 트리거에서 만드는 로컬 임시 테이블은 저장 프로시저 또는 트리거를 호출하기 전에 만든 임시 테이블과 동일한 이름을 사용할 수 있습니다. 그러나 쿼리가 임시 테이블을 참조하고 이때 같은 이름을 가진 두 개의 임시 테이블이 동시에 존재하면 쿼리가 확인할 테이블은 정의되지 않습니다. 중첩된 저장 프로시저도 이를 호출한 저장 프로시저가 만든 임시 테이블과 동일한 이름으로 임시 테이블을 만들 수 있습니다. 그러나 중첩된 프로시저에서 만든 테이블에 대한 수정 사항을 확인하려면 테이블의 구조 및 열 이름이 호출 프로시저에서 만든 테이블과 같아야 합니다. 이는 다음 예에서 확인할 수 있습니다.

```sql
CREATE PROCEDURE dbo.Test2
AS
    CREATE TABLE #t (x INT PRIMARY KEY);
    INSERT INTO #t VALUES (2);
    SELECT Test2Col = x FROM #t;
GO

CREATE PROCEDURE dbo.Test1
AS
    CREATE TABLE #t (x INT PRIMARY KEY);
    INSERT INTO #t VALUES (1);
    SELECT Test1Col = x FROM #t;
    EXEC Test2;
GO

CREATE TABLE #t(x INT PRIMARY KEY);
INSERT INTO #t VALUES (99);
GO

EXEC Test1;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
(1 row(s) affected)
Test1Col
-----------
1

(1 row(s) affected)
 Test2Col
 -----------
 2
 ```

로컬 또는 글로벌 임시 테이블을 만들 때 `CREATE TABLE` 구문은 FOREIGN KEY 제약 조건을 제외한 다른 모든 제약 조건 정의를 지원합니다. 임시 테이블에서 FOREIGN KEY 제약 조건을 지정하면 문에서 해당 제약 조건을 건너뛰었다는 경고 메시지를 반환하며 FOREIGN KEY 제약 조건 없이 테이블을 만듭니다. 임시 테이블은 FOREIGN KEY 제약 조건에서 참조할 수 없습니다.

명명된 제약 조건으로 사용자 정의 트랜잭션의 범위 내에 임시 테이블을 만드는 경우 한 번에 한 사용자만 임시 테이블을 만드는 문을 실행할 수 있습니다. 예를 들어 저장 프로시저에서 명명된 기본 키 제약 조건을 사용하여 임시 테이블을 만드는 경우 여러 사용자가 동시에 저장 프로시저를 실행할 수 없습니다.

## <a name="database-scoped-global-temporary-tables-azure-sql-database"></a>데이터베이스 범위 전역 임시 테이블(Azure SQL Database)

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 글로벌 임시 테이블(## 테이블 이름으로 시작)은 tempdb에 저장되며 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 걸쳐 모든 사용자 세션 간에 공유됩니다. SQL 테이블 형식에 대한 자세한 내용은 테이블 만들기에 관한 위의 섹션을 참조하세요.

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 tempdb에도 저장되고 데이터베이스 수준을 범위로 하는 전역 임시 테이블을 지원합니다. 즉, 글로벌 임시 테이블은 같은 동일한 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 내의 모든 사용자 세션에 공유됩니다. 다른 데이터베이스의 사용자 세션은 전역 임시 테이블에 액세스할 수 없습니다.

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 대한 전역 임시 테이블은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 임시 테이블에 대해 사용하는 것과 같은 구문과 의미 체계를 따릅니다. 마찬가지로 전역 임시 저장 프로시저도 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 데이터베이스 수준을 범위로 합니다. 로컬 임시 테이블(# 테이블 이름으로 시작)은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에도 지원되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 사용하는 것과 같은 구문과 의미 체계를 따릅니다. [임시 테이블](#temporary-tables)에 관한 위의 섹션을 참조하세요.  

> [!IMPORTANT]
> 이 기능은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 사용할 수 있습니다.

### <a name="troubleshooting-global-temporary-tables-for-azure-sql-database"></a>Microsoft Azure SQL Database에 대한 전역 임시 테이블 문제 해결

tempdb 문제 해결에 대한 자세한 내용은 [tempdb 사용 모니터링 방법](../../relational-databases/databases/tempdb-database.md#how-to-monitor-tempdb-use)을 참조하세요.

> [!NOTE]
> 서버 관리자만 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 문제 해결 DMV에 액세스할 수 있습니다.

### <a name="permissions"></a>사용 권한

모든 사용자가 전역 임시 개체를 만들 수 있습니다. 사용자가 추가 사용 권한을 받는 경우를 제외하고 자신의 고유 개체에만 액세스할 수 있습니다.

## <a name="partitioned-tables"></a>분할된 테이블

CREATE TABLE을 사용하여 분할된 테이블을 만들기 전에 테이블이 분할되는 방식을 지정하는 파티션 함수를 만들어야 합니다. [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)을 사용하여 파티션 함수를 만들 수 있습니다. 그런 다음 파티션 구성표를 만들어 파티션 함수가 표시하는 파티션을 유지하는 파일 그룹을 지정해야 합니다. [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)을 사용하여 파티션 구성표를 만들 수 있습니다. 분할된 테이블에는 파일 그룹을 분리하는 PRIMARY KEY 또는 UNIQUE 제약 조건을 지정할 수 없습니다. 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)을 참조하세요.

## <a name="primary-key-constraints"></a>PRIMARY KEY 제약 조건

- 테이블은 하나의 PRIMARY KEY 제약 조건만 포함할 수 있습니다.
- PRIMARY KEY 제약 조건에 의해 생성된 인덱스 수는 비클러스터형 인덱스 999개, 클러스터형 인덱스 1개인 테이블의 인덱스 수 제한을 초과할 수 없습니다.
- PRIMARY KEY 제약 조건에 대해 CLUSTERED 또는 NONCLUSTERED를 지정하지 않은 경우 UNIQUE 제약 조건에 대해 클러스터형 인덱스를 지정하지 않으면 CLUSTERED가 사용됩니다.
- PRIMARY KEY 제약 조건 내에서 정의된 모든 열은 NOT NULL로 정의되어야 합니다. NULL 허용 여부를 지정하지 않은 경우에는 PRIMARY KEY 제약 조건에 참여하는 모든 열의 NULL 허용 여부가 NOT NULL로 설정됩니다.

    > [!NOTE]
    > 메모리 최적화 테이블의 경우 NULL을 허용하는 키 열이 허용됩니다.

- CLR 사용자 정의 형식 열에 기본 키를 정의하는 경우 형식 구현이 이진 순서를 지원해야 합니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.

## <a name="unique-constraints"></a>UNIQUE 제약 조건

- UNIQUE 제약 조건에 CLUSTERED 또는 NONCLUSTERED를 지정하지 않은 경우에는 기본적으로 NONCLUSTERED가 사용됩니다.
- 각 UNIQUE 제약 조건은 인덱스를 생성합니다. UNIQUE 제약 조건의 수가 많아도 테이블의 비클러스터형 인덱스는 999개, 클러스터형 인덱스는 1개를 초과할 수 없습니다.
- CLR 사용자 정의 형식 열에 UNIQUE 제약 조건을 정의하는 경우 형식 구현이 이진 순서 또는 연산자 기반의 순서를 지원해야 합니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.

## <a name="foreign-key-constraints"></a>FOREIGN KEY 제약 조건

- FOREIGN KEY 제약 조건의 열에 NULL 외의 다른 값을 입력한 경우에는 그 값이 참조되는 열에 있어야 합니다. 그렇지 않은 경우에는 외래 키 위반 오류 메시지가 반환됩니다.
- 원본 열을 지정하지 않는 한 FOREIGN KEY 제약 조건이 선행 열에 적용됩니다.
- FOREIGN KEY 제약 조건은 같은 서버의 같은 데이터베이스 내에 있는 테이블만 참조할 수 있습니다. 상호 데이터베이스 참조 무결성은 트리거를 통해 구현해야 합니다. 자세한 내용은 [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md)를 참조하세요.
- FOREIGN KEY 제약 조건은 같은 테이블에 있는 다른 열을 참조할 수 있습니다. 이것을 자체 참조라고 합니다.
- 열 수준 FOREIGN KEY 제약 조건의 REFERENCES 절은 참조 열을 하나만 나열할 수 있습니다. 이 열의 데이터 형식은 제약 조건이 정의된 열의 데이터 형식과 같아야 합니다.
- 테이블 수준 FOREIGN KEY 제약 조건의 REFERENCES 절에는 제약 조건 열 목록의 열 개수와 같은 수의 참조 열이 있어야 합니다. 각 참조 열의 데이터 형식도 열 목록의 해당 열과 같아야 합니다.
- **timestamp** 유형의 열이 외래 키 또는 참조 키의 일부인 경우에는 CASCADE, SET NULL 또는 SET DEFAULT를 지정할 수 없습니다.
- CASCADE, SET NULL, SET DEFAULT 및 NO ACTION은 서로 참조 관계를 가진 테이블에서 결합될 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 NO ACTION을 발견하면 관련된 CASCADE, SET NULL 및 SET DEFAULT 동작을 멈추고 롤백합니다. DELETE 문으로 CASCADE, SET NULL, SET DEFAULT 및 NO ACTION 동작을 결합하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 NO ACTION을 확인하기 전에 모든 CASCADE, SET NULL 및 SET DEFAULT 동작을 적용합니다.
- [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 테이블에 포함하여 다른 테이블을 참조하는 FOREIGN KEY 제약 조건의 수나 특정 테이블을 참조하는 다른 테이블 소유의 FOREIGN KEY 제약 조건의 수에 미리 한계를 정의하지 않습니다.

  하지만 실제로 사용할 수 있는 FOREIGN KEY 제약 조건의 수는 하드웨어 구성 및 데이터베이스와 애플리케이션의 디자인에 따라 제한됩니다. 테이블에 포함되거나 이 테이블을 참조하는 FOREIGN KEY 제약 조건의 수가 각각 253개를 넘지 않도록 하는 것이 좋습니다. 유효 한계는 애플리케이션과 하드웨어에 따라 더 많거나 적을 수 있습니다. 데이터베이스와 애플리케이션을 디자인할 때는 FOREIGN KEY 제약 조건을 적용하는 비용도 고려하십시오.

- 임시 테이블에는 FOREIGN KEY 제약 조건이 적용되지 않습니다.
- FOREIGN KEY 제약 조건은 참조되는 테이블의 PRIMARY KEY 또는 UNIQUE 제약 조건에 있는 열이나 참조되는 테이블의 UNIQUE INDEX에 있는 열만 참조할 수 있습니다.
- CLR 사용자 정의 형식 열에 외래 키를 정의하는 경우 형식 구현이 이진 순서를 지원해야 합니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.
- 외래 키 관계에 참여하는 열은 같은 길이와 배율로 정의되어야 합니다.

## <a name="default-definitions"></a>DEFAULT 정의

- 하나의 열에는 하나의 DEFAULT 정의만 있을 수 있습니다.
- DEFAULT 정의는 상수 값, 함수, SQL 표준 무항 함수 또는 NULL을 포함할 수 있습니다. 다음 표에서는 무항 함수 및 무항 함수가 INSERT 문에서 기본적으로 반환하는 값을 보여 줍니다.

    |SQL-92 무항 함수|반환 값|
    |------------------------------|--------------------|
    |CURRENT_TIMESTAMP|현재 날짜 및 시간입니다.|
    |CURRENT_USER|삽입을 수행하는 사용자의 이름입니다.|
    |SESSION_USER|삽입을 수행하는 사용자의 이름입니다.|
    |SYSTEM_USER|삽입을 수행하는 사용자의 이름입니다.|
    |USER|삽입을 수행하는 사용자의 이름입니다.|
- DEFAULT 정의 내의 *constant_expression*은 해당 테이블의 다른 열, 다른 테이블, 뷰 또는 저장 프로시저를 참조할 수 없습니다.
- **timestamp** 데이터 형식의 열 또는 IDENTITY 속성이 있는 열에는 DEFAULT 정의를 만들 수 없습니다.
- 별칭 데이터 형식이 기본 개체에 바인딩된 경우에는 별칭 데이터 형식의 열에 대해 DEFAULT 정의를 만들 수 없습니다.

## <a name="check-constraints"></a>CHECK 제약 조건

- 하나의 열은 원하는 수만큼의 CHECK 제약 조건을 가질 수 있으며 조건은 AND 및 OR로 결합된 여러 논리 식을 포함할 수 있습니다. 열에 대한 여러 CHECK 제약 조건은 만든 순서대로 검사됩니다.
- 검색 조건은 부울 식으로 계산되어야 하며 다른 테이블을 참조할 수 없습니다.
- 열 수준의 CHECK 제약 조건은 제약된 열만 참조할 수 있으며 테이블 수준의 CHECK 제약 조건은 같은 테이블의 열만 참조할 수 있습니다.

  CHECK CONSTRAINTS 및 규칙은 INSERT 및 UPDATE 문 동안 데이터의 유효성을 검사하는 동일한 역할을 합니다.

- 열에 규칙 및 하나 이상의 CHECK 제약 조건이 있는 경우에는 모든 제한을 평가합니다.
- **text**, **ntext** 또는 **image** 열에는 CHECK 제약 조건을 정의할 수 없습니다.

## <a name="additional-constraint-information"></a>추가 제약 조건 정보

- 제약 조건에 대해 생성된 인덱스는 `DROP INDEX`를 사용하여 삭제할 수 없습니다. `ALTER TABLE`을 사용하여 삭제해야 합니다. 제약 조건이 만들고 사용하는 인덱스는 `ALTER INDEX ... REBUILD`를 사용하여 다시 작성할 수 있습니다. 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.
- 제약 조건 이름은 [identifiers](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 따라야 하지만 숫자 기호(#)로 시작될 수 없습니다. *constraint_name*을 지정하지 않으면 시스템에서 생성한 이름이 제약 조건에 할당됩니다. 제약 조건 이름은 제약 조건 위반에 대한 모든 오류 메시지에 표시됩니다.
- `INSERT`, `UPDATE` 또는 `DELETE` 문에서 제약 조건을 위반하면 명령문이 종료됩니다. 하지만 `SET XACT_ABORT`를 OFF로 설정하면 명령문이 명시적 트랜잭션의 일부인 경우 그 트랜잭션은 계속 처리됩니다. `SET XACT_ABORT`를 ON으로 설정하면 전체 트랜잭션이 롤백됩니다. 또한 `@@ERROR` 시스템 함수를 확인하여 트랜잭션 정의와 함께 `ROLLBACK TRANSACTION` 문을 사용할 수도 있습니다.
- `ALLOW_ROW_LOCKS = ON`이고 `ALLOW_PAGE_LOCK = ON`이면 인덱스에 액세스할 때 행, 페이지 및 테이블 수준 잠금이 허용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 적절한 잠금을 선택하고 행 또는 페이지 잠금에서 테이블 잠금으로 잠금을 에스컬레이션할 수 있습니다. `ALLOW_ROW_LOCKS = OFF`이고 `ALLOW_PAGE_LOCK = OFF`이면 인덱스에 액세스할 때 테이블 수준 잠금만 허용됩니다.
- 테이블에 FOREIGN KEY 또는 CHECK CONSTRAINTS 및 트리거가 있는 경우에는 트리거를 실행하기 전에 제약 조건에 대한 조건을 평가합니다.

테이블 및 해당 열에 대한 보고서는 `sp_help` 또는 `sp_helpconstraint`를 사용합니다. 테이블 이름을 바꾸려면 `sp_rename`을 사용합니다. 테이블에 종속적인 뷰 및 저장 프로시저에 대한 보고서를 만들려면 [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) 및 [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)를 사용하십시오.

## <a name="nullability-rules-within-a-table-definition"></a>테이블 정의 내의 NULL 허용 여부 규칙

열의 Null 허용 여부에 따라 해당 열의 데이터로 Null 값(NULL)을 허용할 수 있는지 여부가 결정됩니다. NULL은 0 또는 공백이 아닙니다. 항목을 만들지 않았거나 명시적인 NULL을 지정했음을 의미하는 것으로 일반적으로 값을 알 수 없거나 적용할 수 없음을 나타냅니다.

`CREATE TABLE` 또는 `ALTER TABLE`을 사용하여 테이블을 만들거나 변경할 때 데이터베이스 및 세션 설정은 열 정의에 사용되는 데이터 형식의 Null 허용 여부에 영향을 주거나 이를 무시할 수 있습니다. 비계산 열은 항상 NULL 또는 NOT NULL로 명시적으로 정의하는 것이 좋으며 사용자 정의 데이터 형식을 사용할 때는 열에 해당 데이터 형식의 기본 Null 허용 여부를 적용하는 것이 좋습니다. 스파스 열은 항상 NULL을 허용해야 합니다.

열의 Null 허용 여부를 명시적으로 지정하지 않은 경우 열의 Null 허용 여부는 다음 표의 규칙을 따릅니다.

|열 데이터 형식|규칙|
|----------------------|----------|
|별칭 데이터 형식|[!INCLUDE[ssDE](../../includes/ssde-md.md)]은 데이터 형식을 만들 때 지정한 Null 허용 여부를 사용합니다. 데이터 형식의 기본 NULL 허용 여부를 결정하려면 **sp_help**를 사용합니다.|
|CLR 사용자 정의 형식(CLR user-defined type)|열 정의에 따라 Null 허용 여부를 결정합니다.|
|시스템이 제공하는 데이터 형식|시스템이 제공하는 데이터 형식에 옵션이 하나뿐인 경우에는 이 옵션이 우선 순위를 갖습니다. **timestamp** 데이터 형식은 NOT NULL이어야 합니다. SET를 사용하여 모든 세션 설정을 ON으로 설정한 경우:<br />**ANSI_NULL_DFLT_ON** = ON, NULL이 할당됩니다. <br />**ANSI_NULL_DFLT_OFF** = ON, NOT NULL이 할당됩니다.<br /><br /> ALTER DATABASE를 사용하여 모든 데이터베이스 설정을 구성한 경우:<br />**ANSI_NULL_DEFAULT_ON** = ON, NULL이 할당됩니다. <br />**ANSI_NULL_DEFAULT_OFF** = ON, NOT NULL이 할당됩니다.<br /><br /> ANSI_NULL_DEFAULT에 대한 데이터베이스 설정을 보려면 **sys.databases** 카탈로그 뷰를 사용하십시오.|

세션에 대해 어떠한 ANSI_NULL_DFLT 옵션도 설정하지 않고 데이터베이스를 기본값(ANSI_NULL_DEFAULT가 OFF)으로 설정하면 기본값인 NOT NULL이 할당됩니다.

열이 계산 열인 경우에는 항상 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 열의 Null 허용 여부를 자동으로 결정합니다. 이런 유형을 가진 열의 Null 허용 여부를 알려면 `COLUMNPROPERTY` 함수에 **AllowsNull** 속성을 사용하세요.

> [!NOTE]
> SQL Server ODBC 드라이버 및 SQL Server OLE DB 드라이버 모두는 기본적으로 ANSI_NULL_DFLT_ON이 ON으로 설정되어 있습니다. ODBC 및 OLE DB 사용자는 ODBC 데이터 원본에서 이를 구성하거나 애플리케이션이 설정한 연결 속성 또는 특성을 사용하여 이를 구성할 수 있습니다.

## <a name="data-compression"></a>Data Compression

시스템 테이블에는 압축을 사용할 수 없습니다. 테이블을 만들 때 데이터 압축은 달리 지정하지 않는 한 NONE으로 설정됩니다. 범위를 벗어난 파티션 목록을 지정하면 오류가 발생합니다. 데이터 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.

압축 상태를 변경할 경우 테이블, 인덱스 또는 파티션에 어떤 영향을 주는지 확인하려면 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 저장 프로시저를 사용합니다.

## <a name="permissions"></a>사용 권한

데이터베이스의 `CREATE TABLE` 권한과 테이블이 생성되는 스키마에 대한 `ALTER` 권한이 필요합니다.

`CREATE TABLE` 문의 열이 사용자 정의 형식으로 정의되면 해당 형식에 대한 `REFERENCES` 권한이 필요합니다.

`CREATE TABLE` 문에 있는 열을 CLR 사용자 정의 형식으로 정의하는 경우 해당 유형의 소유권이나 이에 대한 `REFERENCES` 권한이 필요합니다.

`CREATE TABLE` 문의 열에 연관된 XML 스키마 컬렉션이 있는 경우 XML 스키마 컬렉션의 소유권이나 이에 대한 `REFERENCES` 권한이 필요합니다.

모든 사용자가 tempdb에 임시 테이블을 만들 수 있습니다.

## <a name="examples"></a>예

### <a name="a-create-a-primary-key-constraint-on-a-column"></a>A. 열에 PRIMARY KEY 제약 조건 만들기

다음 예에서는 `EmployeeID` 테이블의 `Employee` 열에 클러스터형 인덱스가 있는 PRIMARY KEY 제약 조건에 대한 열 정의를 보여 줍니다. 제약 조건 이름을 지정하지 않았기 때문에 시스템에서 제약 조건 이름을 제공합니다.

```sql
CREATE TABLE dbo.Employee (
    EmployeeID INT PRIMARY KEY CLUSTERED
);
```

### <a name="b-using-foreign-key-constraints"></a>B. FOREIGN KEY 제약 조건 사용

FOREIGN KEY 제약 조건은 다른 테이블을 참조하는 데 사용됩니다. 외래 키는 단일 열 키 또는 복수 열 키가 될 수 있습니다. 다음 예에서는 `SalesOrderHeader` 테이블을 참조하는 `SalesPerson` 테이블에 대한 단일 열 FOREIGN KEY 제약 조건을 보여 줍니다. 단일 열 FOREIGN KEY 제약 조건에는 REFERENCES 절만 필요합니다.

```sql
SalesPersonID INT NULL REFERENCES SalesPerson(SalesPersonID)
```

또한 명시적으로 FOREIGN KEY 절을 사용하여 열 특성을 다시 정할 수 있습니다. 두 테이블에서 같은 열 이름을 사용할 필요는 없습니다.

```sql
FOREIGN KEY (SalesPersonID) REFERENCES SalesPerson(SalesPersonID)
```

테이블 제약 조건으로 복수 열 키 제약 조건을 만듭니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 `SpecialOfferProduct` 테이블은 복수 열 PRIMARY KEY를 포함합니다. 다음 예에서는 다른 테이블에서 이 키를 참조하는 방법을 보여 줍니다. 명시적인 제약 조건 이름은 선택적입니다.

```sql
CONSTRAINT FK_SpecialOfferProduct_SalesOrderDetail
    FOREIGN KEY (ProductID, SpecialOfferID)
    REFERENCES SpecialOfferProduct (ProductID, SpecialOfferID)
```

### <a name="c-using-unique-constraints"></a>C. UNIQUE 제약 조건 사용

UNIQUE 제약 조건은 기본 키가 아닌 열에 고유성을 적용합니다. 다음 예에서는 `Name` 테이블의 `Product` 열이 고유한 것이어야 한다는 제한을 적용합니다.

```sql
Name NVARCHAR(100) NOT NULL
UNIQUE NONCLUSTERED
```

### <a name="d-using-default-definitions"></a>D. DEFAULT 정의 사용

기본값은 값을 지정하지 않은 경우 사용할 값을 INSERT 및 UPDATE 문으로 제공합니다. 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스는 회사에서 직원이 담당하는 각기 다른 업무를 나열하는 조회 테이블을 포함할 수 있습니다. 각각의 업무를 기술하는 열에 실제 설명을 명시적으로 입력하지 않으면 문자열 기본값으로 설명을 제공할 수 있습니다.

```sql
DEFAULT 'New Position - title not formalized yet'
```

DEFAULT 정의는 제약 조건 외에도 함수를 포함할 수 있습니다. 항목의 현재 날짜를 보려면 다음 예를 사용하십시오.

```sql
DEFAULT (GETDATE())
```

무항 함수 검색도 데이터 무결성을 향상시킵니다. 행을 삽입한 사용자를 추적하려면 USER에 대한 무항 함수를 사용하십시오. 무항 함수를 괄호로 묶지 마십시오.

```sql
DEFAULT USER
```

### <a name="e-using-check-constraints"></a>E. CHECK 제약 조건 사용

다음 예에서는 `CreditRating` 테이블의 `Vendor` 열에 입력한 값에 대한 제한을 보여 줍니다. 제약 조건은 명명되지 않았습니다.

```sql
CHECK (CreditRating >= 1 and CreditRating <= 5)
```

다음 예에서는 테이블의 열에 입력된 문자 데이터에 대한 패턴 제한이 있는 명명된 제약 조건을 보여 줍니다.

```sql
CONSTRAINT CK_emp_id CHECK (
    emp_id LIKE '[A-Z][A-Z][A-Z][1-9][0-9][0-9][0-9][0-9][FM]'
    OR emp_id LIKE '[A-Z]-[A-Z][1-9][0-9][0-9][0-9][0-9][FM]'
)
```

다음 예에서는 값이 특정 목록에 있도록 하거나 지정한 패턴을 따르도록 지정합니다.

```sql
CHECK (
    emp_id IN ('1389', '0736', '0877', '1622', '1756')
    OR emp_id LIKE '99[0-9][0-9]'
)
```

### <a name="f-showing-the-complete-table-definition"></a>F. 전체 테이블 정의 표시

다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 만든 `PurchaseOrderDetail` 테이블에 대한 모든 제약 조건 정의를 가진 전체 테이블 정의를 보여 줍니다. 예제를 실행하기 위해 테이블 스키마가 `dbo`로 변경됩니다.

```sql
CREATE TABLE dbo.PurchaseOrderDetail
(
    PurchaseOrderID int NOT NULL
        REFERENCES Purchasing.PurchaseOrderHeader(PurchaseOrderID),
    LineNumber smallint NOT NULL,
    ProductID int NULL
        REFERENCES Production.Product(ProductID),
    UnitPrice money NULL,
    OrderQty smallint NULL,
    ReceivedQty float NULL,
    RejectedQty float NULL,
    DueDate datetime NULL,
    rowguid uniqueidentifier ROWGUIDCOL NOT NULL
        CONSTRAINT DF_PurchaseOrderDetail_rowguid DEFAULT (NEWID()),
    ModifiedDate datetime NOT NULL
        CONSTRAINT DF_PurchaseOrderDetail_ModifiedDate DEFAULT (GETDATE()),
    LineTotal AS ((UnitPrice*OrderQty)),
    StockedQty AS ((ReceivedQty-RejectedQty)),
    CONSTRAINT PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber
               PRIMARY KEY CLUSTERED (PurchaseOrderID, LineNumber)
               WITH (IGNORE_DUP_KEY = OFF)
)
ON PRIMARY;
```

### <a name="g-creating-a-table-with-an-xml-column-typed-to-an-xml-schema-collection"></a>G. XML 스키마 컬렉션 유형의 xml 열을 가진 테이블 만들기

다음 예에서는 XML 스키마 컬렉션 `xml` 유형의 `HRResumeSchemaCollection` 열이 있는 테이블을 만듭니다. `DOCUMENT` 키워드는 *column_name*에 있는 `xml` 데이터 형식의 각 인스턴스가 하나의 최상위 요소만 포함할 수 있도록 지정합니다.

```sql
CREATE TABLE HumanResources.EmployeeResumes
(
    LName nvarchar(25),
    FName nvarchar(25),
    Resume xml(DOCUMENT HumanResources.HRResumeSchemaCollection)
);
```

### <a name="h-creating-a-partitioned-table"></a>H. 분할된 테이블 만들기

다음 예에서는 테이블이나 인덱스를 4개의 파티션으로 분할하는 파티션 함수를 만듭니다. 그런 다음 4개의 파티션을 각각 보관할 파일 그룹을 지정하는 파티션 구성표를 만듭니다. 마지막으로 파티션 구성표를 사용하는 테이블을 만듭니다. 이 예에서는 데이터베이스에 이미 파일 그룹이 있다고 가정합니다.

```sql
CREATE PARTITION FUNCTION myRangePF1 (int)
    AS RANGE LEFT FOR VALUES (1, 100, 1000);
GO

CREATE PARTITION SCHEME myRangePS1
    AS PARTITION myRangePF1
    TO (test1fg, test2fg, test3fg, test4fg);
GO  
  
CREATE TABLE PartitionTable (col1 int, col2 char(10))
    ON myRangePS1 (col1);
GO
```

`col1`의 `PartitionTable` 열 값을 바탕으로 하여 다음과 같은 방법으로 파티션을 할당합니다.

|파일 그룹|test1fg|test2fg|test3fg|test4fg|
|---------------|-------------|-------------|-------------|-------------|
|**파티션**|1|2|3|4|
|**값**|col 1 \<= 1|col1 > 1 AND col1 \<= 100|col1 > 100 AND col1 \<= 1,000|col1 > 1000|

### <a name="i-using-the-uniqueidentifier-data-type-in-a-column"></a>9\. 열에 uniqueidentifier 데이터 형식 사용

다음 예에서는 `uniqueidentifier` 열이 있는 테이블을 만듭니다. 이 예에서는 PRIMARY KEY 제약 조건을 사용하여 사용자가 중복 값을 삽입하지 못하도록 테이블을 보호하고 `NEWSEQUENTIALID()` 제약 조건의 `DEFAULT` 함수를 사용하여 새 행에 대한 값을 제공합니다. `uniqueidentifier` 열을 $ROWGUID 키워드로 참조할 수 있도록 이 열에 ROWGUIDCOL 속성이 적용됩니다.

```sql
CREATE TABLE dbo.Globally_Unique_Data
(
    GUID UNIQUEIDENTIFIER
        CONSTRAINT Guid_Default DEFAULT
        NEWSEQUENTIALID() ROWGUIDCOL,
    Employee_Name VARCHAR(60)
    CONSTRAINT Guid_PK PRIMARY KEY (GUID)
);
```

### <a name="j-using-an-expression-for-a-computed-column"></a>J. 계산 열에 식 사용

다음 예에서는 `(low + high)/2` 계산 열을 계산하기 위해 식(`myavg`)을 사용하는 방법을 보여 줍니다.

```sql
CREATE TABLE dbo.mytable
(
    low INT,
    high INT,
    myavg AS (low + high)/2
);
```

### <a name="k-creating-a-computed-column-based-on-a-user-defined-type-column"></a>11. 사용자 정의 형식의 열을 기반으로 계산 열 만들기

다음 예에서는 유형의 어셈블리와 유형 자체를 현재 데이터베이스에 이미 만들었다고 가정하고 사용자 정의 형식 `utf8string`으로 정의된 하나의 열을 가진 테이블을 만드는 방법을 보여 줍니다. 두 번째 열은 `utf8string`을 기반으로 정의되며 **type(class)** `utf8string`의 `ToString()` 메서드를 사용하여 해당 열에 대한 값을 컴퓨팅합니다.

```sql
CREATE TABLE UDTypeTable
(
    u UTF8STRING,
    ustr AS u.ToString() PERSISTED
);
```

### <a name="l-using-the-user_name-function-for-a-computed-column"></a>12. 계산 열에 USER_NAME 함수 사용

다음 예에서는 `USER_NAME()` 열에 `myuser_name` 함수를 사용하는 방법을 보여 줍니다.

```sql
CREATE TABLE dbo.mylogintable
(
    date_in DATETIME,
    user_id INT,
    myuser_name AS USER_NAME()
);
```

### <a name="m-creating-a-table-that-has-a-filestream-column"></a>13. FILESTREAM 열이 있는 테이블 만들기

다음 예에서는 `FILESTREAM` 열 `Photo`가 있는 테이블을 만듭니다. 하나 이상의 `FILESTREAM` 열이 있는 테이블에는 하나의 `ROWGUIDCOL` 열이 있어야 합니다.

```sql
CREATE TABLE dbo.EmployeePhoto
(
    EmployeeId INT NOT NULL PRIMARY KEY,
    Photo VARBINARY(MAX) FILESTREAM NULL,
    MyRowGuidColumn UNIQUEIDENTIFIER NOT NULL ROWGUIDCOL UNIQUE DEFAULT NEWID()
);
```

### <a name="n-creating-a-table-that-uses-row-compression"></a>14. 행 압축을 사용하는 테이블 만들기

다음 예에서는 행 압축을 사용하는 테이블을 만듭니다.

```sql
CREATE TABLE dbo.T1
(
    c1 INT,
    c2 NVARCHAR(200)
)
WITH (DATA_COMPRESSION = ROW);
```

데이터 압축 예제를 더 보려면 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.

### <a name="o-creating-a-table-that-has-sparse-columns-and-a-column-set"></a>15. 스파스 열 및 열 집합이 있는 테이블 만들기

다음 예에서는 스파스 열이 있는 테이블과 두 개의 스파스 열 및 열 집합이 있는 테이블을 만드는 방법을 보여 줍니다. 이 예에서는 기본 구문을 사용합니다. 더 복잡한 예제를 보려면 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md) 및 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.

이 예에서는 스파스 열이 있는 테이블을 만듭니다.

```sql
CREATE TABLE dbo.T1
(
    c1 INT PRIMARY KEY,
    c2 VARCHAR(50) SPARSE NULL
);
```

이 예에서는 두 개의 스파스 열과 `CSet`이라는 열 집합이 있는 테이블을 만듭니다.

```sql
CREATE TABLE T1
(
    c1 INT PRIMARY KEY,
    c2 VARCHAR(50) SPARSE NULL,
    c3 INT SPARSE NULL,
    CSet XML COLUMN_SET FOR ALL_SPARSE_COLUMNS
);
```

### <a name="p-creating-a-system-versioned-disk-based-temporal-table"></a>16. 시스템 버전 디스크 기반 임시 테이블 만들기

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

다음 예제는 새 기록 테이블에 연결된 임시 테이블을 만드는 방법 및 기존 기록 테이블에 연결된 임시 테이블을 만드는 방법을 보여 줍니다. 참고로 임시 테이블은 시스템 버전 관리를 활성화하려면 테이블에 대해 정의된 기본 키를 활성화해야 합니다. 예를 들어 기존 테이블에 대한 시스템 버전 관리를 추가 또는 제거하는 방법을 보여 주는 예제는 [예제](../../t-sql/statements/alter-table-transact-sql.md#Example_Top)의 시스템 버전 관리를 참조하세요. 사용 사례는 [임시 테이블](../../relational-databases/tables/temporal-tables.md)을 참조하세요.

이 예제에서는 새 기록 테이블에 연결된 새 임시 테이블을 만듭니다.

```sql
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON);
```

이 예제에서는 기존 기록 테이블에 연결된 새 임시 테이블을 만듭니다.

```sql
-- Existing table
CREATE TABLE Department_History
(
    DepartmentNumber CHAR(10) NOT NULL,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 NOT NULL,
    SysEndTime DATETIME2 NOT NULL
);

-- Temporal table
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON));
```

### <a name="q-creating-a-system-versioned-memory-optimized-temporal-table"></a>17. 시스템 버전 관리 메모리 최적화 임시 테이블 만들기

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

다음 예제는 새 디스크 기반 기록 테이블에 연결된 시스템 버전 관리 메모리 최적화 임시 테이블을 만드는 방법을 보여 줍니다.

이 예제에서는 새 기록 테이블에 연결된 새 임시 테이블을 만듭니다.

```sql
CREATE SCHEMA History;
GO

CREATE TABLE dbo.Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY NONCLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH
(
    MEMORY_OPTIMIZED = ON,
    DURABILITY = SCHEMA_AND_DATA,
    SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)
);
```

이 예제에서는 기존 기록 테이블에 연결된 새 임시 테이블을 만듭니다.

```sql
-- Existing table
CREATE TABLE Department_History
(
    DepartmentNumber CHAR(10) NOT NULL,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 NOT NULL,
    SysEndTime DATETIME2 NOT NULL
);

-- Temporal table
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH
(
    SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON)
);
```

### <a name="r-creating-a-table-with-encrypted-columns"></a>18. 암호화된 열이 있는 테이블 만들기

다음 예제에서는 암호화된 열 두 개가 있는 테이블을 만듭니다. 자세한 내용은 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요.

```sql
CREATE TABLE Customers (
    CustName NVARCHAR(60)
        ENCRYPTED WITH (
            COLUMN_ENCRYPTION_KEY = MyCEK,
            ENCRYPTION_TYPE = RANDOMIZED,
            ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ),
    SSN VARCHAR(11) COLLATE Latin1_General_BIN2
        ENCRYPTED WITH (
            COLUMN_ENCRYPTION_KEY = MyCEK,
            ENCRYPTION_TYPE = DETERMINISTIC ,
            ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ),
    Age INT NULL
);
```

### <a name="s-create-an-inline-filtered-index"></a>S.는 인라인 필터링된 인덱스 만들기

인라인 필터링된 인덱스가 있는 테이블을 만듭니다.

```sql
CREATE TABLE t1
(
    c1 INT,
    index IX1 (c1) WHERE c1 > 0
);
```

### <a name="t-create-an-inline-index"></a>20. 인라인 인덱스 만들기

다음은 디스크 기반 테이블에 대한 NONCLUSTERED 인라인을 사용하는 방법을 보여줍니다.

```sql
CREATE TABLE t1
(
    c1 INT,
    INDEX ix_1 NONCLUSTERED (c1)
);

CREATE TABLE t2
(
    c1 INT,
    c2 INT INDEX ix_1 NONCLUSTERED
);

CREATE TABLE t3
(
    c1 INT,
    c2 INT,
    INDEX ix_1 NONCLUSTERED (c1,c2)
);
```

### <a name="u-create-a-temporary-table-with-an-anonymously-named-compound-primary-key"></a>21. 익명으로 명명된 복합 기본 키로 임시 테이블 만들기

익명으로 명명된 복합 기본 키로 테이블을 만듭니다. 이 방법은 각각 별도의 세션에 있는 두 개의 세션 범위 임시 테이블이 제약 조건에 동일한 이름을 사용할 경우 발생하는 런타임 충돌을 방지하는 데 유용합니다.

```sql
CREATE TABLE #tmp
(
    c1 INT,
    c2 INT,
    PRIMARY KEY CLUSTERED ([c1], [c2])
);
GO
```

제약 조건의 이름을 명시적으로 지정하는 경우 두 번째 세션은 다음과 같은 오류가 생성됩니다.

```
Msg 2714, Level 16, State 5, Line 1
There is already an object named 'PK_#tmp' in the database.
Msg 1750, Level 16, State 1, Line 1
Could not create constraint or index. See previous errors.
```

임시 테이블 이름은 고유하지만 제약 조건은 고유하지 않기 때문에 문제가 발생합니다.

### <a name="v-using-global-temporary-tables-in-azure-sql-database"></a>V. Azure SQL Database에서 글로벌 임시 테이블 사용

세션 A는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb1에 전역 임시 테이블 ##test를 만들고 1행을 추가합니다.

```sql
CREATE TABLE ##test (
    a INT,
    b INT
);

INSERT INTO ##test
VALUES (1, 1);

-- Obtain object ID for temp table ##test
SELECT OBJECT_ID('tempdb.dbo.##test') AS 'Object ID';
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
1253579504
```

tempdb(2)에서 지정된 개체 ID 1253579504에 대한 글로벌 임시 테이블 이름 가져오기

```sql
SELECT name FROM tempdb.sys.objects WHERE object_id = 1253579504;
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```sql
##test
```

세션 B는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb1에 연결하며 세션 A에서 만든 테이블 ##test에 액세스할 수 있습니다.

```sql
SELECT * FROM ##test;
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```sql
1, 1
```

세션 C는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb2의 다른 데이터베이스에 연결하며 testdb1에서 만든 ##test에 액세스하려고 합니다. 이 작업은 전역 임시 테이블에 대한 데이터베이스 범위 때문에 실패합니다.

```sql
SELECT * FROM ##test
```

다음과 같은 오류가 발생합니다.

```
Msg 208, Level 16, State 0, Line 1
Invalid object name '##test'
```

현재 사용자 데이터베이스 testdb1에서 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tempdb의 시스템 개체 주소 지정

```sql
SELECT * FROM tempdb.sys.objects;
SELECT * FROM tempdb.sys.columns;
SELECT * FROM tempdb.sys.database_files;
```

## <a name="next-steps"></a>다음 단계

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)
- [CREATE  INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)
- [데이터 형식](../../t-sql/data-types/data-types-transact-sql.md)
- [DROP  INDEX](../../t-sql/statements/drop-index-transact-sql.md)
- [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)
- [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)
- [DROP TABLE](../../t-sql/statements/drop-table-transact-sql.md)
- [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)
- [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)
- [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_help](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)
- [sp_helpconstraint](../../relational-databases/system-stored-procedures/sp-helpconstraint-transact-sql.md)
- [sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
