---
title: "테이블 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 256
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0978041b1c2683f6af3f6c531ddc10edc6b9bcbf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-transact-sql"></a>CREATE TABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  새 테이블을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
> [!NOTE]   
>  에 대 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 구문 참조 [CREATE TABLE (Azure SQL 데이터 웨어하우스)](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
--Simple CREATE TABLE Syntax (common if not using options)  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
[ ; ]  
```  
  
## <a name="syntax"></a>구문  
  
```  
--Disk-Based CREATE TABLE Syntax  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    [ AS FileTable ]  
    ( {   <column_definition>   
        | <computed_column_definition>    
        | <column_set_definition>   
        | [ <table_constraint> ]   
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
    [ <column_constraint> [ ...n ] ]   
    [ <column_index> ]  
  
<data type> ::=   
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
      INDEX index_name [ CLUSTERED | NONCLUSTERED ]   
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
  | ALLOW_ROW_LOCKS = { ON | OFF}   
  | ALLOW_PAGE_LOCKS ={ ON | OFF}   
  | COMPRESSION_DELAY= {0 | delay [Minutes]}  
  | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
       [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
       [ , ...n ] ) ]  
}  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
```  
  
```  
  
      --Memory optimized CREATE TABLE Syntax  
CREATE TABLE  
    [database_name . [schema_name ] . | schema_name . ] table_name  
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
  
<data type> ::=  
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
{ [ NONCLUSTERED ] | [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count)  }  
  
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
 *database_name*  
 테이블이 생성된 데이터베이스의 이름입니다. *a s e _* 기존 데이터베이스의 이름을 지정 해야 합니다. 지정 하지 않으면 *database_name* 현재 데이터베이스에 대 한 기본값입니다. 현재 연결에 대 한 로그인에 지정 된 데이터베이스의 기존 사용자 ID와 연결 되어 있어야 *database_name*, 되며 해당 사용자 ID는 CREATE TABLE 권한을 갖고 있어야 합니다.  
  
 *schema_name*  
 새 테이블이 속한 스키마의 이름입니다.  
  
 *table_name*  
 새 테이블의 이름입니다. 테이블 이름에 대 한 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. *table_name* 최대 로컬 임시 테이블 이름 제외 하 고 128 자가 될 수 있습니다 (단일 숫자 기호를 접두사로 붙은 이름이 (#))는 116 자를 초과할 수 없습니다.  
  
 AS FileTable 
 
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
 
 새 테이블을 FileTable로 만듭니다. FileTable에는 고정 스키마가 있으므로 열을 지정하지 않아도 됩니다. Filetable에 대 한 자세한 내용은 참조 [Filetable &#40; SQL Server &#41; ](../../relational-databases/blob/filetables-sql-server.md).  
  
 *column_name*  
 *computed_column_expression*  
 계산 열의 값을 정의하는 식입니다. 계산 열은 해당 열에 PERSISTED 표시가 없는 한 테이블에 물리적으로 저장되지 않는 가상의 열입니다. 이 열은 같은 테이블의 다른 열을 사용하는 식에서 계산됩니다. 예를 들어 계산된 열 정의 가질 수 있습니다: **비용** AS **가격** \* **qty**합니다. 식은 계산되지 않은 열 이름, 상수, 함수, 변수 및 이러한 요소를 하나 이상의 연산자로 연결한 조합이 될 수 있습니다. 식은 하위 쿼리가 되거나 별칭 데이터 형식을 포함할 수 없습니다.  
  
 계산 열은 SELECT 목록, WHERE 절, ORDER BY 절 또는 정규식을 사용할 수 있는 다른 위치에서 사용할 수 있습니다. 단, 다음과 같은 경우는 예외입니다.  
  
-   FOREIGN KEY 또는 CHECK 제약 조건에 참여하려면 계산 열이 PERSISTED로 표시되어야 합니다.  
  
-   계산 열 값이 결정적 식에 의해 정의되고 결과의 데이터 형식이 인덱스 열에 허용되는 경우에는 계산 열을 인덱스의 키 열이나 PRIMARY KEY 또는 UNIQUE 제약 조건의 일부로 사용할 수 있습니다.  
  
     예를 들어 테이블에 열이 정수 **는** 및 **b**, 계산된 열 **a + b** 인덱싱될 수 있지만 계산된 열 **a + DATEPART (dd, GETDATE())**  다음 호출에서 값이 변경 될 수 있으므로 인덱싱할 수 없습니다.  
  
-   계산 열은 INSERT 또는 UPDATE 문의 대상이 될 수 없습니다.  
  
> [!NOTE]  
>  테이블의 각 행은 계산 열과 연관된 열에 대해 다른 값을 가질 수 있습니다. 따라서 계산 열은 각 행에 대해 동일한 값을 갖지 않습니다.  
  
 계산 열의 Null 허용 여부는 사용되는 식을 바탕으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 자동으로 결정합니다. 대부분 식의 결과는 언더플로 또는 오버플로에 의한 Null 결과를 생성할 수 있으므로 Null이 허용되지 않는 열만 사용하더라도 결국 식은 Null을 허용하는 것으로 간주됩니다. COLUMNPROPERTY 함수를 사용 하 여는 **AllowsNull** 속성을 테이블에 있는 계산 열의 null 허용 여부를 조사 합니다. Null을 허용 하는 식 ISNULL을 지정 하 여 nonnullable 스테레오로 변환할 수 있습니다는 *check_expression* 상수, 상수는 null이 아닌 값이 NULL 결과를 대체 합니다. CLR(공용 언어 런타임) 사용자 정의 형식의 식을 바탕으로 한 계산 열에는 해당 형식에 대한 REFERENCES 권한이 필요합니다.  
  
 PERSISTED  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]이 계산된 값을 테이블에 물리적으로 저장하고 계산 열이 종속된 다른 열이 업데이트되면 해당 값을 업데이트하도록 지정합니다. 계산 열을 PERSISTED로 표시하면 결정적이지만 정확하지는 않은 계산 열에 인덱스를 만들 수 있습니다. 자세한 내용은 [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md)을 참조하세요. 분할된 테이블의 분할 열로 사용되는 계산 열은 명시적으로 PERSISTED로 표시해야 합니다. *computed_column_expression* PERSISTED를 지정할 때 결정적 이어야 합니다.  
  
 ON { *partition_scheme* | *파일 그룹* | **"**기본**"** }  

 테이블이 저장된 파티션 구성표 또는 파일 그룹을 지정합니다. 경우 *partition_scheme* 지정는에 지정 된 많은 파일 그룹 또는 파티션을 집합이 하나에 저장 된 분할된 된 테이블 수는 테이블이 *partition_scheme*합니다. 경우 *파일 그룹* 를 지정 된 테이블은 명명된 된 파일 그룹에 저장 합니다. 파일 그룹은 데이터베이스 내에 있어야 합니다. 경우 **"**기본**"** 를 지정 하거나 ON을 전혀 지정 하지 않으면, 테이블의 기본 파일 그룹에 저장 됩니다. CREATE TABLE에 지정된 테이블의 저장 메커니즘은 곧이어 변경할 수 없습니다.  
  
 ON {*partition_scheme* | *파일 그룹* | **"**기본**"**} 기본 키에 지정 될 수도 있습니다 또는 UNIQUE 제약 조건을 지정 합니다. 이러한 제약 조건은 인덱스를 만듭니다. 경우 *파일 그룹* 를 지정 된 인덱스는 명명된 된 파일 그룹에 저장 됩니다. 경우 **"**기본**"** 를 지정 하거나 ON 전혀 지정 하지 않으면 인덱스는 테이블과 동일한 파일 그룹에 저장 됩니다. PRIMARY KEY 또는 UNIQUE 제약 조건이 클러스터형 인덱스를 만드는 경우에는 테이블에 대한 데이터 페이지가 인덱스와 동일한 파일 그룹에 저장됩니다. CLUSTERED를 지정 하거나 아니면 제약 조건이 클러스터형된 인덱스를 만드는 경우 *partition_scheme* 은 지정 된 *partition_scheme* 또는 *파일그룹* 테이블 정의 또는 그 반대로의 제약 조건 정의 유지 하 고 다른 무시 됩니다.  
  
> [!NOTE]  
>  이 컨텍스트에서 default는 키워드가 아니라 기본 파일 그룹에 대 한 식별자 이며 ON 같이 구분 되어야 합니다 **"**기본**"** 또는 ON **[**기본**]**합니다. 경우 **"**기본**"** 지정, QUOTED_IDENTIFIER 옵션은 현재 세션에 대 한 ON 이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  분할된 테이블을 만든 후에는 테이블의 LOCK_ESCALATION 옵션을 AUTO로 설정하십시오. 이렇게 하면 테이블 수준이 아닌 파티션(HoBT) 수준으로 잠금이 에스컬레이션되도록 하여 동시성을 향상시킬 수 있습니다. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 TEXTIMAGE_ON { *파일 그룹*| **"**기본**"** }  
 나타냅니다는 **텍스트**, **ntext**, **이미지**, **xml**, **varchar (max)**,  **nvarchar (max)**, **varbinary (max)**, 및 CLR 사용자 정의 형식 열 (기 하 도형 및 지리 포함)는 지정된 된 파일 그룹에 저장 됩니다.  
  
 테이블에 큰 값 열이 없는 경우에는 TEXTIMAGE_ON이 허용되지 않습니다. 경우에 TEXTIMAGE_ON를 지정할 수 없습니다 *partition_scheme* 지정 됩니다. 경우 **"**기본**"** 를 지정 하거나 TEXTIMAGE_ON을 전혀 지정 하지 않으면, 큰 값 열은 기본 파일 그룹에 저장 합니다. CREATE TABLE에 지정된 큰 값 열 데이터를 저장한 후에는 곧이어 변경할 수 없습니다.  

> [!NOTE]  
> Varchar (max), nvarchar (max), varbinary (max), xml 및 큰 UDT 값 데이터 행에 직접 저장 됩니다, 그리고 한 최대 8000 바이트 값을 최대 레코드 들어갈 수 있습니다. 포인터 값이 레코드에 맞지 않는 경우 정렬에 행과 나머지 행 외부 LOB 저장 공간에 저장 됩니다. 0의 기본값입니다.
TEXTIMAGE_ON "LOB 저장소 공간"의 위치 변경, 데이터를 행에 저장된 하는 경우에이 영향을 주지 않습니다. Out of row 옵션 sp_tableoption의 큰 값 형식을 사용 하 여를 행 외부 전체 LOB 값을 저장 합니다. 


> [!NOTE]  
>  이 컨텍스트에서 default는 키워드가 아니라 기본 파일 그룹에 대 한 식별자 이며 TEXTIMAGE_ON 같이 구분 되어야 합니다 **"**기본**"** 또는 TEXTIMAGE_ON **[**기본**]**. 경우 **"**기본**"** 지정, QUOTED_IDENTIFIER 옵션은 현재 세션에 대 한 ON 이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
 FILESTREAM_ON { *partition_scheme_name* | 파일 그룹 | **"**기본**"** } **적용할**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 
 
 FILESTREAM 데이터의 파일 그룹을 지정합니다.  
  
 테이블에 FILESTREAM 데이터가 포함되어 있고 테이블이 분할된 경우에는 FILESTREAM_ON 절을 포함해야 하며 이 절에서 FILESTREAM 파일 그룹의 파티션 구성표를 지정해야 합니다. 이 파티션 구성표는 테이블의 파티션 구성표와 동일한 파티션 함수 및 파티션 열을 사용해야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 테이블이 분할되지 않은 경우에는 FILESTREAM 열을 분할할 수 없습니다. 테이블의 FILESTREAM 데이터는 단일 파일 그룹에 저장되어야 합니다. 이 파일 그룹은 FILESTREAM_ON 절에 지정됩니다.  
  
 테이블이 분할되지 않고 FILESTREAM_ON 절이 지정되지 않은 경우에는 DEFAULT 속성이 설정된 FILESTREAM 파일 그룹이 사용됩니다. FILESTREAM 파일 그룹이 없으면 오류가 발생합니다.  
  
-   ON 및 TEXTIMAGE_ON과 마찬가지로 FILESTREAM_ON에 대해 CREATE TABLE을 사용하여 설정한 값은 다음과 같은 경우를 제외하고 변경할 수 없습니다.  
  
-   A [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 문이 클러스터형 인덱스로 힙 변환 합니다. 이 경우 다른 FILESTREAM 파일 그룹, 파티션 구성표 또는 NULL을 지정할 수 있습니다.  
  
-   A [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) 문에 클러스터형된 인덱스를 힙으로 변환 합니다. 이 경우, 다른 FILESTREAM 파일 그룹, 파티션 구성표 또는 **"**기본**"** 지정할 수 있습니다.  
  
 파일 그룹은 `FILESTREAM_ON <filegroup>` 절 또는 파티션 구성표에 명명 되어 있는 각 FILESTREAM 파일 그룹에는 파일 그룹에 대해 정의 된 파일이 하나 있어야 합니다. 이 파일을 사용 하 여 정의 해야 합니다는 [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) 또는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을; 그렇지 않으면 오류가 발생 합니다.  
  
 관련된 FILESTREAM 항목을 참조 하세요. [Binary Large Object &#40; Blob&#41; 데이터 &#40; SQL Server &#41; ](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 [ *type_schema_name***합니다.** ] *type_name*  
 열의 데이터 형식과 열이 속한 스키마를 지정합니다. 디스크 기반 테이블의 데이터 형식은 다음 중 하나일 수 있습니다.  
  
-   시스템 데이터 형식입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 기반으로 하는 별칭 형식. 별칭 데이터 형식은 CREATE TYPE 문으로 만들어진 다음 테이블 정의에 사용됩니다. 별칭 데이터 형식에 대한 NULL 또는 NOT NULL 할당은 CREATE TABLE 문 중에서 덮어쓸 수 있지만 길이 지정은 변경할 수 없습니다. 즉, CREATE TABLE 문에서 별칭 데이터 형식의 길이를 지정할 수 없습니다.  
  
-   CLR 사용자 정의 형식. CLR 사용자 정의 데이터 형식은 CREATE TYPE 문으로 만들어진 다음 테이블 정의에서 사용됩니다. CLR 사용자 정의 형식으로 열을 만들려면 해당 형식에 대한 REFERENCES 권한이 필요합니다.  
  
 경우 *type_schema_name* 를 지정 하지 않으면는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 참조 *type_name* 다음과 같은 순서로:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식  
  
-   현재 데이터베이스에 있는 현재 사용자의 기본 스키마  
  
-   현재 데이터베이스의 **dbo** 스키마  
  
 메모리 액세스에 최적화 된 테이블에 대 한 참조 [메모리 내 OLTP에 대 한 데이터 형식을 지원](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) 지원 되는 시스템 형식의 목록에 대 한 합니다.  
  
 *전체 자릿수*  
 지정된 데이터 형식의 전체 자릿수입니다. 유효한 전체 자릿수 값에 대 한 자세한 내용은 참조 [전체 자릿수, 소수 자릿수 및 길이](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)합니다.  
  
 *소수 자릿수*  
 지정된 데이터 형식의 소수 자릿수입니다. 유효한 소수 자릿수 값에 대 한 자세한 내용은 참조 [전체 자릿수, 소수 자릿수 및 길이](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)합니다.  
  
 **max**  
 에 적용 됩니다는 **varchar**, **nvarchar**, 및 **varbinary** 2를 저장 하기 위한 데이터 형식 ^31 바이트의 문자 및 이진 데이터를 2 ^30 바이트의 유니코드 데이터입니다.  
  
 CONTENT  
 지정의 각 인스턴스는 **xml** 의 데이터 형식이 *column_name* 여러 개의 최상위 요소를 포함할 수 있습니다. 콘텐츠에만 적용 됩니다는 **xml** 데이터 입력 한 경우에 지정할 수 있습니다 *xml_schema_collection* 도 지정 합니다. 지정하지 않은 경우에는 CONTENT가 기본 동작입니다.  
  
 DOCUMENT  
 지정 하는 각 인스턴스에 **xml** 데이터 형식에 *column_name* 하나의 최상위 요소만 포함 될 수 있습니다. 문서에만 적용 됩니다는 **xml** 데이터 입력 한 경우에 지정할 수 있습니다 *xml_schema_collection* 도 지정 합니다.  
  
 *xml_schema_collection*  
 에 적용 됩니다는 **xml** 형식과 XML 스키마 컬렉션을 연결 하기 위한 데이터 형식입니다. 입력 하기 전에 **xml** 스키마에 대 한 열에서 스키마 만들어야 데이터베이스에서 사용 하 여 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)합니다.  
  
 DEFAULT  
 삽입 중에 값이 명시적으로 지정되지 않은 경우에 열에 대해 제공되는 값을 지정합니다. DEFAULT 정의로 정의 된 제외한 모든 열에 적용할 수 있습니다 **타임 스탬프**, 또는 IDENTITY 속성이 있는 합니다. 형식에서의 암시적 변환이 기본 값을 사용자 정의 형식 열에 대해 지정 하는 경우 지원 해야 *constant_expression* 사용자 정의 형식에 있습니다. DEFAULT 정의는 테이블이 삭제될 때 제거됩니다. 문자열과 같은 상수 값, 스칼라 함수(시스템 함수, 사용자 정의 함수 또는 CLR 함수) 또는 NULL만 기본값으로 사용할 수 있습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환성을 유지하기 위해 DEFAULT에 제약 조건 이름을 할당할 수 있습니다.  
  
 *constant_expression*  
 열의 기본값으로 사용되는 상수, NULL 또는 시스템 함수입니다.  
  
 *memory_optimized_constant_expression*  
 열의 기본값으로 사용되는 상수, NULL 또는 시스템 함수입니다. 고유하게 컴파일된 저장 프로시저에서 지원되어야 합니다. 고유 하 게 컴파일된 저장된 프로시저의 기본 제공 함수에 대 한 자세한 내용은 참조 [고유 하 게 컴파일된 T-SQL 모듈의 지원 되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)합니다.  
  
 IDENTITY  
 새 열이 ID 열임을 나타냅니다. 테이블에 새 행이 추가되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 열에 대해 고유한 증가값을 제공합니다. ID 열은 일반적으로 PRIMARY KEY 제약 조건과 함께 사용되어 테이블에 대한 고유한 행 식별자 역할을 합니다. IDENTITY 속성에 지정할 수 **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)**, 또는 **numeric(p,0)** 열입니다. ID 열은 테이블당 하나만 만들 수 있습니다. ID 열에는 바인딩된 기본값 및 DEFAULT 제약 조건을 사용할 수 없습니다. 초기값과 증가값은 둘 다 지정하거나 또는 둘 다 지정하지 않아야 합니다. 둘 다 지정하지 않은 경우에는 기본값 (1,1)이 사용됩니다.  
  
 메모리 액세스에 최적화 된 테이블에 허용 되는 유일한 값 모두에 대 한 *시드* 및 *증분* 은 1 이며, (1, 1)에 대 한 기본값이 *시드* 및 *증분*합니다.  
  
 *시드*  
 테이블에 로드되는 첫 번째 행에 사용하는 값입니다.  
  
 *증가값*  
 로드된 이전 행의 ID 값에 추가되는 증가값입니다.  
  
 NOT FOR REPLICATION  
 CREATE TABLE 문에서 IDENTITY 속성, FOREIGN KEY 제약 조건 및 CHECK 제한 조건에 대해 NOT FOR REPLICATION 절을 지정할 수 있습니다. IDENTITY 속성에 이 절을 지정하면 복제 에이전트가 삽입 작업을 수행할 때 ID 열의 값이 증가하지 않습니다. 제약 조건에 대해 이 절을 지정하면 복제 에이전트가 삽입, 업데이트 또는 삭제 작업을 수행할 때 해당 제약 조건이 강제로 적용되지 않습니다.  
  
 생성 된 항상 AS 행 {시작 | [숨겨진]을 (를) 종료 [NOT NULL]  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 지정 된 datetime2 열 레코드가 유효 시작 시간 또는 레코드는 유효한 종료 시간을 기록 하는 시스템에서 사용될지를 지정 합니다. 열을 정의 해야 NOT NULL로 합니다. NULL로 지정 하려고 하면 시스템에서 오류를 throw 합니다. 기간 열에 NOT NULL을 명시적으로 지정 하지 않으면 시스템은 기본적으로 열을 NOT NULL로 정의 합니다. 이 인수를 사용 하 여 PERIOD FOR SYSTEM_TIME 및 SYSTEM_VERSIONING와 함께 = 테이블에 시스템 버전 관리를 사용 하도록 설정 하려면 인수에 대 한 합니다. 자세한 내용은 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)을 참조하세요.  
  
 하나 또는 둘 다 기간 열을 표시할 수 있습니다 **HIDDEN** 암시적으로 이러한 열 숨기기 위한 플래그를 되도록 **선택 \* FROM**  *`<table>`*  하지 않습니다 이 열에 값을 반환 합니다. 기본적으로 기간 열 숨겨지지 않습니다. 를 사용 하려면 숨겨진된 열 임시 테이블을 직접 참조 하는 모든 쿼리에 명시적으로 포함 되어야 합니다. 변경 하는 **HIDDEN** 기존 기간 열에 대 한 특성 **기간** 삭제 하 고 다른 숨겨진 플래그로 다시 생성 해야 합니다.  
  
 `INDEX *index_name* [ CLUSTERED | NONCLUSTERED ] (*column_name* [ ASC | DESC ] [ ,... *n* ] )`  
     
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.

테이블에 인덱스를 만들를 지정 합니다. 이 클러스터형 인덱스나 비클러스터형된 인덱스 수 있습니다. 인덱스 나열 된 열이 포함 되어 및 데이터를 오름차순 또는 내림차순 정렬 됩니다.  
  
 인덱스 *index_name* CLUSTERED COLUMNSTORE  
   
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.
  
 클러스터형된 columnstore 인덱스가 있는 열 형식에는 전체 테이블을 저장 하도록 지정 합니다. 이 항상 테이블의 모든 열을 포함 합니다. 데이터가 행 columnstore 압축 향상을 구성 하는 이후 영문자 또는 숫자 순서로 정렬 되지 않은 합니다.  
  
 인덱스 *index_name* [NONCLUSTERED] COLUMNSTORE (*column_name* [,... *n* ] )  
   
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.
  
 테이블에 비클러스터형 columnstore 인덱스를 만들려면를 지정 합니다. Rowstore 힙 또는 클러스터형된 인덱스를 사용 하는 테이블이 될 수 있습니다 또는 클러스터형된 columnstore 인덱스를 수 있습니다. 모든 경우에 테이블에 비클러스터형 columnstore 인덱스를 만들 인덱스의 열에 대 한 데이터의 두 번째 복사본을 저장 합니다.  
  
 비클러스터형 columnstore 인덱스가 저장 되 고 클러스터형된 columnstore 인덱스로 관리 합니다. 에 대 한 비클러스터형 columnstore 인덱스가 열 제한 될 수 있습니다에 보조 인덱스는 테이블에 존재 하기 때문에 호출 됩니다.  
  
 ON *partition_scheme_name***(***column_name***)**  
 분할된 인덱스의 파티션이 매핑될 파일 그룹을 정의하는 파티션 구성표를 지정합니다. 실행 하 여 파티션 구성표는 데이터베이스 내에 있어야 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) 또는 [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)합니다. *column_name* 된 분할 된 인덱스가 분할 될 열을 지정 합니다. 이 열에는 데이터 형식, 길이, 일치 해야 하 고는 함수에 파티션의 전체 자릿수가 *partition_scheme_name* 사용 합니다. *column_name* 인덱스 정의의 열에 제한 되지 않습니다. 기본 테이블의 모든 열을 지정할 수는 경우 고유 인덱스를 분할 하는 제외 하 고 *column_name* 고유 키로 사용 되는 선택 해야 합니다. 이 제한 사항으로 인해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 단일 파티션 내에서만 키 값의 고유성을 확인할 수 있습니다.  
  
> [!NOTE]  
>  비고유 클러스터형 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 기본적으로 지정되지 않은 분할 열을 클러스터형 인덱스 키 목록에 추가합니다. 비고유 비클러스터형 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 지정되지 않은 분할 열을 인덱스의 키가 아닌 포괄 열로 추가합니다.  
  
 경우 *partition_scheme_name* 또는 *파일 그룹* 지정 하지 않으면 테이블이 분할 된 하 고, 동일한 분할 열을 사용 하 여 기본 테이블과 동일한 파티션 구성표에 인덱스가 있습니다.  
  
> [!NOTE]  
>  XML 인덱스에서 파티션 구성표를 지정할 수 없습니다. 기본 테이블이 분할되면 XML 인덱스는 테이블과 동일한 파티션 구성표를 사용합니다.  
  
 인덱스를 분할 하는 방법에 대 한 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)합니다.  
  
 ON *filegroup_name*  
 주어진 파일 그룹에 지정된 인덱스를 만듭니다. 지정된 위치가 없고 테이블 또는 뷰가 분할되지 않은 경우 인덱스는 동일한 파일 그룹을 기본 테이블 또는 뷰로 사용합니다. 파일 그룹은 이미 존재해야 합니다.  
  
 ON **"**기본**"**  
 기본 파일 그룹에 지정된 인덱스를 만듭니다.  
  
 이 컨텍스트에서 default는 키워드가 아닙니다. 기본 파일 그룹에 대 한 식별자 이며 ON 같이 구분 되어야 합니다 **"**기본**"** 또는 ON **[**기본**]**합니다. "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
 [FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL"을 (를)]  
   
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion.md)].

 클러스터형 인덱스를 만들 때 테이블에 대한 FILESTREAM 데이터의 위치를 지정합니다. FILESTREAM_ON 절에서 FILESTREAM 데이터를 다른 FILESTREAM 파일 그룹 또는 파티션 구성표로 이동할 수 있습니다.  
  
 *filestream_filegroup_name* FILESTREAM 파일 그룹의 이름입니다. 파일 그룹에 사용 하 여 파일 그룹에 대해 정의 된 한 파일이 있어야 합니다.는 [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) 또는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을; 그렇지 않으면 오류가 발생 합니다.  
  
 테이블이 분할된 경우에는 FILESTREAM_ON 절이 포함되어야 하며 이 절에서 테이블의 파티션 구성표와 동일한 파티션 함수 및 파티션 열을 사용하는 FILESTREAM 파일 그룹의 파티션 구성표를 지정해야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 테이블이 분할되지 않은 경우에는 FILESTREAM 열을 분할할 수 없습니다. 테이블의 FILESTREAM 데이터는 FILESTREAM_ON 절에 지정된 단일 파일 그룹에 저장되어야 합니다.  
  
 클러스터형 인덱스가 생성되고 있고 테이블에 FILESTREAM 열이 포함되지 않은 경우 CREATE INDEX 문에 FILESTREAM_ON NULL을 지정할 수 있습니다.  
  
 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
 ROWGUIDCOL  
 새 열이 행 GUID 열임을 나타냅니다. 하나의 **uniqueidentifier** 테이블당 열 ROWGUIDCOL 열으로 지정 될 수 있습니다. ROWGUIDCOL 속성을 적용하면 $ROWGUID를 사용하여 열을 참조할 수 있습니다. ROWGUIDCOL 속성에만 할당할 수는 **uniqueidentifier** 열입니다. 사용자 정의 데이터 형식 열은 ROWGUIDCOL로 지정할 수 없습니다.  
  
 ROWGUIDCOL 속성은 열에 저장된 값이 고유하도록 강제 적용하지 않습니다. 또한 테이블에 삽입된 새 행에 대한 값을 자동으로 생성하지도 않습니다. 각 열에 대해 고유한 값을 생성, 사용 하 여는 [NEWID](../../t-sql/functions/newid-transact-sql.md) 또는 [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) 작동 [삽입](../../t-sql/statements/insert-transact-sql.md) 문에 대 한 기본값으로 이러한 함수를 사용 하거나는 열입니다.  
  
 사용 하 여 암호화  
 암호화 열을 사용 하 여 지정 된 [항상 암호화](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능입니다.  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 열 암호화 키를 지정합니다. 자세한 내용은 참조 [열 암호화 키 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
 ENCRYPTION_TYPE = {결정적 | 임의}  
 **결정적 암호화** 는 지정된 일반 텍스트 값에 대해 항상 동일한 암호화된 값을 생성하는 방법을 사용합니다. 결정적 암호화를 사용 하 여 같음 비교를 암호화 된 값을 기반으로 동등 조인을 사용 하 여 테이블 조인 및 그룹화를 사용 하 여 검색을 허용 하지만 패턴을 검사 하 여 암호화 된 값에 대 한 정보를 추측할 권한이 없는 사용자가 사용할 수 있습니다. 암호화 된 열입니다. 명확 하 게 암호화 된 열에서 두 테이블을 조인는 두 열은 동일한 열 암호화 키를 사용 하 여 암호화 하는 경우에 가능 합니다. 결정적 암호화에서는 문자 열에 대해 binary2 정렬 순서를 적용하는 열 데이터 정렬을 사용해야 합니다.  
  
 **임의 암호화** 는 예측하기 어려운 방식으로 데이터를 암호화하는 방법을 사용합니다. 임의 암호화는 더 안전 하지만 동등 검색, 그룹화 및 암호화 된 열에서 조인를 금지 합니다. 임의 암호화를 사용 하 여 열을 인덱싱할 수 없습니다.  
  
 한 열을 검색 매개 변수 또는 그룹화 매개 변수를 예: 정부 ID 번호에 대 한 결정적 암호화를 사용 합니다. 임의 암호화를 사용 하 여, 신용 카드 번호 등 데이터용 하지 다른 레코드와 같은 그룹에 있거나, 테이블과 조인 하는 검색 되지 않습니다에 대 한 암호화 된 포함 된 행을 찾습니다 (예: transaction number) 다른 열을 사용 하는 데 사용 관심 있는 열입니다.  
  
 조건에 맞는 데이터 형식의 열 이어야 합니다.  
  
 알고리즘  
 해야 **'AEAD_AES_256_CBC_HMAC_SHA_256'**합니다.  
  
 기능 제약 조건을 비롯 한 자세한 내용은 참조 하십시오. [상시 암호화 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)합니다.  
  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 SPARSE  
 열이 스파스 열임을 나타냅니다. 스파스 열의 저장소는 Null 값에 대해 최적화됩니다. 스파스 열은 NOT NULL로 지정할 수 없습니다. 추가 제한 사항 및 스파스 열에 대 한 자세한 내용은 참조 [스파스 열을 사용 하 여](../../relational-databases/tables/use-sparse-columns.md)합니다.  
  
 마스크 된 (함수 = ' *mask_function* ')  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 동적 데이터 마스크를 지정합니다. *mask_function* 적절 한 매개 변수를 사용 하 여 마스킹 함수 이름입니다. 세 개의 함수를 사용할 수 있습니다.  
  
-   default)  
  
-   email()  
  
-   partial()  
  
-   random()  
  
 함수 매개 변수를 참조 하십시오. [동적 데이터 마스킹](../../relational-databases/security/dynamic-data-masking.md)합니다.  
  
 FILESTREAM  
   
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion.md)].

 에 대해서만 유효 **varbinary (max)** 열입니다. 에 대 한 FILESTREAM 저장소를 지정 된 **varbinary (max)** BLOB 데이터입니다.  
  
 테이블의 열이 있어야도 **uniqueidentifier** ROWGUIDCOL 특성을 갖는 데이터 형식입니다. 이 열은 Null 값을 허용하지 않으며 UNIQUE 또는 PRIMARY KEY 단일 열 제약 조건을 가져야 합니다. 열의 GUID 값은 응용 프로그램에서 데이터를 삽입할 때 제공하거나 NEWID () 함수를 사용하는 DEFAULT 제약 조건을 통해 제공해야 합니다.  
  
 테이블에 대해 정의된 FILESTREAM 열이 있는 동안에는 ROWGUIDCOL 열을 삭제하고 관련 제약 조건을 변경할 수 없습니다. ROWGUIDCOL 열은 마지막 FILESTREAM 열이 삭제된 이후에만 삭제될 수 있습니다.  
  
 열에 대해 FILESTREAM 저장소 특성이 지정된 경우 해당 열의 모든 값이 파일 시스템에 있는 FILESTREAM 데이터 컨테이너에 저장됩니다.  
  
 COLLATE *데이터 정렬 이름*  
 열에 대한 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. *데이터 정렬 이름* 의 열에만 적용할 수는 **char**, **varchar**, **텍스트**, **nchar**, **nvarchar**, 및 **ntext** 데이터 형식입니다. 지정하지 않은 경우 열이 사용자 정의 데이터 형식이면 사용자 정의 데이터 형식의 데이터 정렬에 열이 할당되고 그렇지 않은 경우에는 데이터베이스의 기본 데이터 정렬에 할당됩니다.  
  
 Windows 및 SQL 데이터 정렬 이름에 대 한 자세한 내용은 참조 [Windows 데이터 정렬 이름](../../t-sql/statements/windows-collation-name-transact-sql.md) 및 [SQL 데이터 정렬 이름](../../t-sql/statements/sql-server-collation-name-transact-sql.md)합니다.  
  
 COLLATE 절에 대 한 자세한 내용은 참조 하십시오. [collate&#40; Transact SQL &#41; ](~/t-sql/statements/collations.md).  
  
 CONSTRAINT  
 PRIMARY KEY, NOT NULL, UNIQUE, FOREIGN KEY 또는 CHECK 제약 조건 정의의 시작을 표시하는 선택적인 키워드입니다.  
  
 *제약 조건 이름*  
 제약 조건의 이름입니다. 제약 조건 이름은 테이블이 속한 스키마 내에서 고유한 이름이어야 합니다.  
  
 NULL | NOT NULL  
 열의 Null 값 허용 여부를 결정합니다. NULL은 엄격하게 말해 제약 조건이 아니지만 NOT NULL처럼 지정할 수 있습니다. 계산 열에서는 PERSISTED를 지정한 경우에만 NOT NULL을 지정할 수 있습니다.  
  
 PRIMARY KEY  
 지정한 열에 고유 인덱스를 통해 엔터티 무결성을 적용하는 제약 조건입니다. PRIMARY KEY 제약 조건은 각 테이블마다 하나만 만들 수 있습니다.  
  
 UNIQUE  
 지정한 열에 대해 고유 인덱스를 통해 엔터티 무결성을 적용하는 제약 조건입니다. 하나의 테이블이 여러 개의 UNIQUE 제약 조건을 가질 수 있습니다.  
  
 CLUSTERED | NONCLUSTERED  
 PRIMARY KEY 또는 UNIQUE 제약 조건에 대해 클러스터형 또는 비클러스터형 인덱스를 만들도록 지정합니다. PRIMARY KEY 제약 조건의 기본값은 CLUSTERED이며 UNIQUE 제약 조건의 기본값은 NONCLUSTERED입니다.  
  
 CREATE TABLE 문에서는 한 가지 제약 조건에만 CLUSTERED를 지정할 수 있습니다. UNIQUE 제약 조건에 대해 CLUSTERED를 지정하고 PRIMARY KEY 제약 조건도 지정한 경우 PRIMARY KEY의 기본값은 NONCLUSTERED입니다.  
  
 다음은 디스크 기반 테이블에 있는 비클러스터형을 사용하는 방법을 보여 줍니다.  
  
```  
CREATE TABLE t1 ( c1 int, INDEX ix_1 NONCLUSTERED (c1))   
CREATE TABLE t2( c1 int INDEX ix_1 NONCLUSTERED (c1))   
CREATE TABLE t3( c1 int, c2 int INDEX ix_1 NONCLUSTERED)   
CREATE TABLE t4( c1 int, c2 int, INDEX ix_1 NONCLUSTERED (c1,c2))  
```  
  
 FOREIGN KEY REFERENCES  
 열에 있는 데이터에 대한 참조 무결성을 제공하는 제약 조건입니다. FOREIGN KEY 제약 조건을 지정하려면 열의 각 값이 참조된 테이블의 참조된 해당 열에 있어야 합니다. FOREIGN KEY 제약 조건은 참조되는 테이블의 PRIMARY KEY 또는 UNIQUE 제약 조건 열이나 참조되는 테이블의 UNIQUE INDEX에서 참조되는 열만 참조할 수 있습니다. 계산 열의 외래 키 또한 PERSISTED로 표시되어야 합니다.  
  
 [ *schema_name***.**] *referenced_table_name*]  
 FOREIGN KEY 제약 조건이 참조하는 테이블과 그 테이블이 속한 스키마의 이름입니다.  
  
 **(** *ref_column* [ **,**... *n* ] **)**  
 FOREIGN KEY 제약 조건이 참조하는 테이블의 열 또는 열 목록입니다.  
  
 ON DELETE { **아무 작업도** | CASCADE | SET NULL | SET DEFAULT}  
 행이 참조 관계를 가지고 참조된 행이 부모 테이블에서 삭제될 경우에 테이블의 행에 수행될 동작을 지정합니다. 기본값은 NO ACTION입니다.  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 오류가 발생하며 부모 테이블의 행에 대한 삭제 동작이 롤백됩니다.  
  
 CASCADE  
 부모 테이블에서 행을 삭제한 경우 참조 테이블에서 해당 행이 삭제됩니다.  
  
 SET NULL  
 부모 테이블에서 해당 행을 삭제하면 외래 키를 구성하는 모든 값이 NULL로 설정됩니다. 이 제약 조건을 실행하려면 외래 키 열이 Null을 허용해야 합니다.  
  
 SET DEFAULT  
 부모 테이블에서 해당 행을 삭제하면 외래 키를 구성하는 모든 값이 기본값으로 설정됩니다. 이 제약 조건을 실행하려면 모든 외래 키 열에 기본 정의가 있어야 합니다. 열이 Null을 허용하고 명시적 기본값이 설정되어 있지 않은 경우 NULL은 해당 열의 암시적 기본값이 됩니다.  
  
 논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 CASCADE를 지정하지 마세요. 논리적 레코드에 대한 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
 해당 테이블에 INSTEAD OF 트리거 ON DELETE가 이미 있으면 ON DELETE CASCADE를 정의할 수 없습니다.  
  
 예를 들어는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스는 **ProductVendor** 테이블에 참조 관계를는 **공급 업체** 테이블입니다. **ProductVendor.BusinessEntityID** 외래 키 참조는 **Vendor.BusinessEntityID** 기본 키입니다.  
  
 행에 대해 DELETE 문을 실행 하는 경우는 **공급 업체** 테이블과 ON DELETE CASCADE 동작에 지정 된 **ProductVendor.BusinessEntityID**, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 하나 이상의 종속을 확인 합니다. 행의 **ProductVendor** 테이블입니다. 에 종속 행이 있는 경우는 **ProductVendor** 테이블 삭제 되 고 해당 행에서 참조 되는 또한는 **공급 업체** 테이블입니다.  
  
 반대로 NO ACTION을 지정한 경우는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 오류가 발생 하 고 삭제 동작이 롤백됩니다는 **공급 업체** 에 하나 이상의 행이 행의 **ProductVendor** 참조 하는 테이블입니다.  
  
 업데이트 시 { **아무 작업도** | CASCADE | SET NULL | SET DEFAULT}  
 변경된 테이블의 행에 참조 관계가 있고 참조된 행이 부모 테이블에서 업데이트될 경우 해당 행에 대해 발생할 동작을 지정합니다. 기본값은 NO ACTION입니다.  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 오류가 발생하며 부모 테이블의 행에 대한 업데이트 동작이 롤백됩니다.  
  
 CASCADE  
 부모 테이블에서 행이 업데이트될 때 참조 테이블에서도 해당 행이 업데이트됩니다.  
  
 SET NULL  
 부모 테이블에서 행을 업데이트하면 해당 외래 키를 구성하는 모든 값이 NULL로 설정됩니다. 이 제약 조건을 실행하려면 외래 키 열이 Null을 허용해야 합니다.  
  
 SET DEFAULT  
 부모 테이블에서 행을 업데이트하면 해당 외래 키를 구성하는 모든 값이 기본값으로 설정됩니다. 이 제약 조건을 실행하려면 모든 외래 키 열에 기본 정의가 있어야 합니다. 열이 Null을 허용하고 명시적 기본값이 설정되어 있지 않은 경우 NULL은 해당 열의 암시적 기본값이 됩니다.  
  
 논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 CASCADE를 지정하지 마세요. 논리적 레코드에 대한 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
 변경할 테이블에 INSTEAD OF 트리거 ON UPDATE가 이미 존재하면 ON UPDATE CASCADE, SET NULL 또는 SET DEFAULT를 정의할 수 없습니다.  
  
 예를 들어,는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스는 **ProductVendor** 테이블 간의 관계가 참조는 **공급 업체** 테이블: **ProductVendor.BusinessEntity** 외래 키 참조는 **Vendor.BusinessEntityID** 기본 키입니다.  
  
 행에 대 한 UPDATE 문을 실행 하는 경우는 **공급 업체** 에 지정 된 테이블 및 ON UPDATE CASCADE 동작 **ProductVendor.BusinessEntityID**, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 하나 이상의 종속을 확인 합니다. 행의 **ProductVendor** 테이블입니다. 에 종속 행이 있는 경우는 **ProductVendor** 테이블 업데이트 되 고, 행에서 참조 되는 또한는 **공급 업체** 테이블입니다.  
  
 반대로 NO ACTION을 지정한 경우는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 오류가 발생 하 고 업데이트 동작이 롤백됩니다는 **공급 업체** 에 하나 이상의 행이 행의 **ProductVendor** 참조 하는 테이블입니다.  
  
 CHECK  
 열에 입력 가능한 값을 제한하여 도메인 무결성을 적용하는 제약 조건입니다. 계산 열의 CHECK 제약 조건 또한 PERSISTED로 표시되어야 합니다.  
  
 *logical_expression*  
 TRUE 또는 FALSE를 반환하는 논리 식입니다. 별칭 데이터 형식은 식에 포함될 수 없습니다.  
  
 *열*  
 제약 조건 정의에서 사용하는 열을 표시하기 위해 테이블 제약 조건에서 괄호로 묶어 사용하는 열 또는 열 목록입니다.  
  
 [ **ASC** | DESC]  
 테이블 제약 조건에 사용되는 열의 정렬 순서를 지정합니다. 기본값은 ASC입니다.  
  
 *partition_scheme_name*  
 분할된 테이블의 파티션이 매핑될 파일 그룹을 정의하는 파티션 구성표의 이름입니다. 파티션 구성표는 데이터베이스 내에 있어야 합니다.  
  
 [ *partition_column_name***합니다.** ]  
 분할된 테이블의 분할 기준 열을 지정합니다. 파티션에 지정 된 열과 일치 해야 하는 함수에 *partition_scheme_name* 데이터 형식, 길이 및 전체 자릿수에서 사용 합니다. 파티션 함수에 참여하는 계산 열은 명시적으로 PERSISTED로 표시되어야 합니다.  
  
> [!IMPORTANT]  
>  분할된 테이블 및 ALTER TABLE...SWITCH 작업의 원본이나 대상인 분할되지 않은 테이블의 분할 열에 NOT NULL을 지정하는 것이 좋습니다. 이렇게 하면 분할 열의 CHECK 제약 조건에서 Null 값을 확인하지 않아도 됩니다.  
  
 FILLFACTOR로  **=**  *fillfactor*  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 인덱스 데이터를 저장하는 데 사용하는 각 인덱스 페이지를 채우는 정도를 지정합니다. 사용자 지정 *fillfactor* 값은 1에서 100 사이일 수 있습니다. 값을 지정하지 않으면 기본값 0이 사용됩니다. 채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
> [!IMPORTANT]  
>  현재 WITH FILLFACTOR = *fillfactor* 해제 PRIMARY KEY 또는 UNIQUE 제약 조건에 적용 되는 유일한 인덱스 옵션은 이전 버전과 호환성을 위해 유지 관리 하지만 나중에이 방식으로 설명 하지 것입니다.  
  
 *column_set_name* ALL_SPARSE_COLUMNS에 대 한 XML COLUMN_SET  
 열 집합의 이름입니다. 열 집합은 구조화된 출력으로 테이블의 모든 스파스 열을 결합하는 형식화되지 않은 XML 표현입니다. 열 집합에 대한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.  
  
 PERIOD FOR SYSTEM_TIME (*system_start_time_column_name* , *system_end_time_column_name* )  
   
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.
  
 시스템에서 사용 하는 레코드의 유효 기간을 기록 하는 열의 이름을 지정 합니다. 이 인수는 생성 된 항상 AS 행과 함께에서 사용 하 여 {시작 | 최종} 테이블에 시스템 버전 관리를 사용 하도록 설정 하려면 인수에 대해 SYSTEM_VERSIONING = 및 합니다. 자세한 내용은 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)을 참조하세요.  
  
 COMPRESSION_DELAY  
   
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.
  
 메모리 액세스에 최적화에 대 한 지연 columnstore 인덱스에 압축에 적합 하기 전에 변경 되지 않은 테이블에 행이 유지 되어야 하는 시간 (분)의 최소 수를 지정 합니다. SQL Server는 마지막 업데이트 시간에 따라 압축 하려면 특정 행을 선택 합니다. 예를 들어 행 2 시간 일정 기간 동안에 자주 변경 하는 경우 COMPRESSION_DELAY 설정할 수 = 업데이트 완료 된 후에 SQL Server는 행 압축 되도록 120 분입니다.  
  
 디스크 기반 테이블에 대 한 지연 SQL Server는 압축 된 행 그룹으로 압축할 수 전에 델타 행 그룹에 델타 행 그룹을 CLOSED 상태에서 유지 되어야 하는 시간 (분)의 최소 수를 지정 합니다. 디스크 기반 테이블에서 insert를 관리 하 고 업데이트할 하지 이후 시간에 개별 행을 SQL Server에 적용 됩니다 지연 CLOSED 상태에서 델타 행 그룹입니다.  
  
 기본값은 0 분입니다.  
  
 COMPRESSION_DELAY를 사용 하는 경우에 권장 사항을 참조 하십시오 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
 \<table_option >:: = 하나 이상의 테이블 옵션을 지정 합니다.  
  
 DATA_COMPRESSION  
 지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.  
  
 없음  
 테이블 또는 지정된 파티션이 압축되지 않습니다.  
  
 ROW  
 테이블 또는 지정된 파티션이 행 압축을 사용하여 압축됩니다.  
  
 PAGE  
 테이블 또는 지정된 파티션이 페이지 압축을 사용하여 압축됩니다.  
  
 COLUMNSTORE  
   
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.
  
 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE 대부분 고성능 columnstore 압축으로 압축 하도록 지정 합니다. 이 일반적인 좋습니다.  
  
 COLUMNSTORE_ARCHIVE  
   
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. 테이블 또는 더 작은 크기로 파티션이 COLUMNSTORE_ARCHIVE 압축 추가 됩니다. 보다 적은 저장소 크기가 필요한 기타 상황에서 보관하는 데 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
 압축에 대 한 자세한 내용은 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
 ON PARTITIONS **(** { `<partition_number_expression>` | [ **,**... *n* ] **)**  
 DATA_COMPRESSION 설정을 적용할 파티션을 지정합니다. 테이블이 분할되지 않은 경우 ON PARTITIONS 인수를 사용하면 오류가 발생합니다. ON PARTITIONS 절을 지정하지 않으면 DATA_COMPRESSION 옵션이 분할된 테이블의 모든 파티션에 적용됩니다.  
  
 *partition_number_expression* 다음과 같은 방법으로 지정할 수 있습니다.  
  
-   파티션의 파티션 번호를 지정합니다(예: ON PARTITIONS (2)).  
  
-   여러 개별 파티션의 파티션 번호를 쉼표로 구분하여 지정합니다(예: ON PARTITIONS (1,5)).  
  
-   범위와 개별 파티션을 모두 지정합니다(예: ON PARTITIONS (2,4,6 TO 8)).  
  
 `<range>`예를 들어, TO로 구분 된 파티션 번호로 지정할 수 있습니다: ON PARTITIONS (6 TO 8)).  
  
 여러 파티션에 대해 서로 다른 데이터 압축 유형을 설정하려면 DATA_COMPRESSION 옵션을 두 번 이상 지정합니다. 예를 들면 다음과 같습니다.  
  
```  
WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
```  
  
 \<index_option >:: =  
 하나 이상의 인덱스 옵션을 지정합니다. 이러한 옵션에 대 한 전체 설명은 참조 하세요. [CREATE index&#40; Transact SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = {ON | **OFF** }  
 ON이면 FILLFACTOR로 지정한 사용 가능한 공간의 비율을 인덱스의 중간 수준 페이지에 적용합니다. OFF이거나 FILLFACTOR 값을 지정하지 않으면 중간 페이지의 키 집합을 고려하여 인덱스가 가질 수 있는 최대 크기의 행을 최소한 하나만큼 저장할 공간을 남기고 용량 한계에 가깝게 중간 수준 페이지를 채웁니다. 기본값은 OFF입니다.  
  
 FILLFACTOR  **=**  *fillfactor*  
 인덱스를 만들거나 변경할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. *fillfactor* 100 1 까지의 정수 값 이어야 합니다. 기본값은 0입니다. 채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려는 경우에 대한 오류 응답을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. 실행할 때이 옵션에 영향을 주지 않습니다 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), 또는 [업데이트](../../t-sql/queries/update-transact-sql.md)합니다. 기본값은 OFF입니다.  
  
 ON  
 중복된 키 값이 고유 인덱스에 삽입되는 경우 경고 메시지가 나타나고 고유성 제약 조건을 위반하는 행만 실패합니다.  
  
 OFF  
 중복된 키 값이 고유 인덱스에 삽입되는 경우 오류 메시지가 나타나고 전체 INSERT 작업이 롤백됩니다.  
  
 뷰, 비고유 인덱스, XML 인덱스, 공간 인덱스 및 필터링된 인덱스에 생성된 인덱스의 경우 IGNORE_DUP_KEY를 ON으로 설정할 수 없습니다.  
  
 IGNORE_DUP_KEY를 보려면 사용 하 여 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.  
  
 이전 버전과 호환되는 구문에서 WITH IGNORE_DUP_KEY는 WITH IGNORE_DUP_KEY = ON과 같습니다.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | **OFF** }  
 ON이면 오래된 인덱스 통계를 자동으로 다시 계산하지 않습니다. OFF이면 자동 통계 업데이트를 활성화합니다. 기본값은 OFF입니다.  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** | OFF}  
 ON이면 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다. OFF이면 행 잠금을 사용하지 않습니다. 기본값은 ON입니다.  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** | OFF}  
 ON이면 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다. OFF이면 페이지 잠금을 사용하지 않습니다. 기본값은 ON입니다.  
  
 FILETABLE_DIRECTORY = *directory_name*  
   
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 Windows 호환 FileTable 디렉터리 이름을 지정합니다. 이 이름은 데이터베이스의 모든 FileTable 디렉터리 이름 중에서 고유해야 합니다. 고유성을 비교할 때는 데이터 정렬 설정과 관계없이 대/소문자가 구분되지 않습니다. 이 값을 지정하지 않으면 Filetable의 이름이 사용됩니다.  
  
 FILETABLE_COLLATE_FILENAME = { *데이터 정렬 이름* | database_default}  
   
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 FileTable의 **Name** 열에 적용할 데이터 정렬의 이름을 지정합니다. 데이터 정렬은 Windows 파일 명명 의미 체계를 따르도록 대/소문자를 구분하지 않아야 합니다. 이 값을 지정하지 않으면 데이터베이스 기본 데이터 정렬이 사용됩니다. 데이터베이스 기본 데이터 정렬이 대/소문자를 구분하면 오류가 발생하고 CREATE TABLE 작업이 실패합니다.  
  
 *데이터 정렬 이름*  
 대/소문자를 구분하지 않는 데이터 정렬의 이름입니다.  
  
 database_default  
 데이터베이스의 기본 데이터 정렬을 사용하도록 지정합니다. 이 데이터 정렬은 대/소문자를 구분하지 않아야 합니다.  
  
 FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = *제약 조건 이름*  
   
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 FileTable에 자동으로 만들어지는 기본 키 제약 조건에 사용할 이름을 지정합니다. 이 값을 지정하지 않으면 시스템에서 제약 조건 이름을 생성합니다.  
  
 FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = *제약 조건 이름*  
   
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 자동으로 만들어지는 unique 제약 조건에 사용할 이름을 지정는 **stream_id** FileTable의 열입니다. 이 값을 지정하지 않으면 시스템에서 제약 조건 이름을 생성합니다.  
  
 FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = *제약 조건 이름*  
   
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 자동으로 만들어지는 unique 제약 조건에 사용할 이름을 지정는 **parent_path_locator** 및 **이름** FileTable의 열입니다. 이 값을 지정하지 않으면 시스템에서 제약 조건 이름을 생성합니다.  
  
 SYSTEM_VERSIONING  **=**  ON [(HISTORY_TABLE  **=**  *schema_name* 합니다.  *history_table_name* [, DATA_CONSISTENCY_CHECK  **=**  { **ON** | OFF}])]  
   
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.   
  
 시스템 버전 관리 테이블의 데이터 형식, null 허용 제약 조건 및 primary key 제약 조건 요구 사항을 충족 하도록 합니다. 경우는 **HISTORY_TABLE** 인수가 사용 되지 않으면, 시스템 일치 하는 두 테이블 간에 링크를 만들 현재 테이블과 동일한 파일 그룹에 현재 테이블의 스키마를 사용 하는 새 기록 테이블을 생성 하 고로 인해 시스템 기록 테이블에서 현재 테이블의 각 레코드의 기록을 기록 합니다. 이 기록 테이블의 이름은 됩니다 `MSSQL_TemporalHistoryFor<primary_table_object_id>`합니다. 기본적으로 기록 테이블은 **PAGE** (으)로 압축됩니다. 에 대 한 링크를 만들고 기존 기록 테이블을 사용 하 여 HISTORY_TABLE 인수를 사용 하는 경우 현재 테이블과 지정된 된 테이블 간에 링크가 만들어집니다. 구성 분할은 현재 테이블에서 기록 테이블로 자동 복제를 수행하지 않기 때문에 현재 테이블이 분할된 경우 기록 테이블은 기본 파일 그룹에 생성됩니다. 기록 테이블 생성 도중 기록 테이블의 이름을 지정하는 경우 스키마와 테이블 이름을 지정해야 합니다. 기존 기록 테이블에 대한 링크를 만드는 경우 데이터 일관성 검사를 수행하도록 선택할 수 있습니다. 이 데이터 일관성 검사는 기존 레코드가 겹치지 않고 확인 합니다. 기본값은 데이터 일관성 검사를 수행하는 것입니다. 이 인수를 사용 하 여 PERIOD FOR SYSTEM_TIME 및 생성 된 항상 AS 행 함께 {시작 | 테이블에 시스템 버전 관리를 사용 하도록 설정 하려면 인수 끝}입니다. 자세한 내용은 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)을 참조하세요.  
  
 REMOTE_DATA_ARCHIVE = {ON [( *table_stretch_options* [, … n])] | OFF (MIGRATION_STATE = 일시 중지)을 (를)  
   
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 스트레치 데이터베이스 활성화 또는 비활성화를 새 테이블을 만듭니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
 **테이블에 대 한 스트레치 데이터베이스를 활성화합니다.**  
  
 지정 하 여 테이블에 대 한 확대를 사용 하는 경우 `ON`, 선택적으로 지정할 수 `MIGRATION_STATE = OUTBOUND` 하려면 즉시 데이터 마이그레이션 또는 `MIGRATION_STATE = PAUSED` 데이터 마이그레이션을 연기 하 합니다. 기본값은 `MIGRATION_STATE = OUTBOUND`합니다. 테이블에 스트레치를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)합니다.  
  
 **필수 구성 요소**. 테이블에 대해 스트레치를 사용 하기 전에 서버에서를 데이터베이스에서 스트레치를 사용 하도록 설정 해야 합니다. 자세한 내용은 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)를 참조하십시오.  
  
 **사용 권한**. 데이터베이스 또는 테이블에 스트레치를 사용 하려면 db_owner 권한이 필요 합니다. 테이블에 대해 스트레치를 사용 하도록 설정 하면 테이블에 대 한 ALTER 권한이 있어야 합니다.  
  
 [FILTER_PREDICATE = {null | *조건자* }]  
   
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 필요에 따라 기록 및 현재 데이터가 포함 된 테이블에서 마이그레이션할 행을 선택 하는 필터 조건자를 지정 합니다. 조건자는 결정적 인라인 테이블 반환 함수를 호출 해야 합니다. 자세한 내용은 참조 하십시오. [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 및 [필터 함수를 사용 하 여 마이그레이션할 행을 선택](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)합니다. 
   
> [!IMPORTANT]  
>  제대로 수행되지 않는 필터 조건자를 제공하면 데이터 마이그레이션 성능도 저하됩니다. 스트레치 데이터베이스는 CROSS APPLY 연산자를 사용하여 테이블에 필터 조건자를 적용합니다.  
  
 필터 조건자를 지정하지 않으면 전체 테이블이 마이그레이션됩니다.  
  
 도 지정 해야 필터 조건자를 지정 하면 *MIGRATION_STATE*합니다.  
  
 MIGRATION_STATE = {아웃 바운드 |  인바운드 | (를) 일시 중지  
   
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 및 Azure SQL 합니다. 
  
-   지정 `OUTBOUND` SQL Server에서 데이터를 Azure로 합니다.  
  
-   지정 `INBOUND` 원격 복사 하려면 Azure에서 테이블에 대 한 데이터 테이블에 대해 스트레치를 비활성화 하 고 SQL server를 다시 합니다. 자세한 내용은 [Stretch Database 비활성화 및 원격 데이터 다시 가져오기](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)를 사용하세요.  
  
     이 작업으로 인해 데이터 전송 비용이 발생하며 이 작업은 취소할 수 없습니다.  
  
-   지정 `PAUSED` 을 일시 중지 또는 데이터 마이그레이션을 연기 합니다. 자세한 내용은 참조 하십시오. [일시 중지 및 데이터 마이그레이션 다시 시작 &#40; 스트레치 데이터베이스 &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
 MEMORY_OPTIMIZED  
   
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 값 ON 테이블이 메모리 액세스에 최적화 임을 나타냅니다. 메모리 액세스에 최적화 된 테이블은 트랜잭션 처리의 성능을 최적화 하는 데 사용 되는 메모리 내 OLTP 기능을 일부입니다. 메모리 내 OLTP를 시작 하려면 참조 [빠른 시작 1: 더 빠르게 TRANSACT-SQL 성능을 위한 메모리 내 OLTP 기술](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)합니다. 메모리 액세스에 최적화 된 테이블에 대 한 자세한 내용은 참조 하십시오. [메모리 최적화 된 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)합니다.  
  
 기본값은 OFF 디스크 기반 테이블 임을 나타냅니다.  
  
 DURABILITY  
   
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.   
  
 SCHEMA_AND_DATA 값 즉 변경 내용을 디스크에 유지 되 고 다시 시작 또는 장애 조치 이후에 내구성이 있는 테이블이 임을 나타냅니다.  SCHEMA_AND_DATA는 기본값입니다.  
  
 SCHEMA_ONLY 값은 테이블이 비영구적임을 나타냅니다. 테이블 스키마는 저장 되지만 데이터 업데이트를 다시 시작 또는 데이터베이스의 장애 조치 시 유지 되지 않습니다. DURABILITY = SCHEMA_ONLY는 MEMORY_OPTIMIZED만 사용할 수 = ON입니다.  
  
> [!WARNING]  
>  와 테이블을 만들면 **DURABILITY = SCHEMA_ONLY**, 및 **READ_COMMITTED_SNAPSHOT** 를 사용 하 여 변경 이후에 **ALTER DATABASE**, 테이블의 데이터는 손실 됩니다.  
  
 BUCKET_COUNT  
   
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 
  
 해시 인덱스에서 만들어야 하는 버킷 수를 나타냅니다. 해시 인덱스에서 BUCKET_COUNT의 최대값은 1,073,741,824입니다. 버킷 수에 대 한 자세한 내용은 참조 [메모리 최적화 된 테이블에 대 한 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)합니다.  
  
 Bucket_count는 필수 인수입니다.  
  
 INDEX  
   
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 
  
CREATE TABLE 문의 일부로 열 및 테이블 인덱스를 지정할 수 있습니다. 추가 하 고 메모리 액세스에 최적화 된 테이블에 인덱스를 제거 하는 방법에 대 한 내용은 참조 하십시오: [에 최적화 된 테이블](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)
  
 HASH  
   
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 
  
 HASH 인덱스가 만들어졌음을 나타냅니다.  
  
 해시 인덱스는 메모리 액세스에 최적화된 테이블에서만 지원됩니다.  
  
## <a name="remarks"></a>주의  
 허용 되는 테이블, 열, 제약 조건 및 인덱스 수에 대 한 정보를 참조 하십시오. [Maximum Capacity Specifications for SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md)합니다.  
  
 테이블 및 인덱스에 대한 공간 할당은 일반적으로 한 번에 한 익스텐트씩 이루어집니다. ALTER DATABASE의 설정 MIXED_PAGE_ALLOCATION 옵션이로 설정 된 경우 TRUE, 또는 항상 이전에 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]는 테이블이 나 인덱스를 만들 때 충분 한 페이지를 균일 익스텐트를 채울 때까지 혼합 익스텐트에서 페이지 할당 됩니다. 균일 익스텐트를 채울 정도로 충분한 페이지를 받은 이후에는 현재 할당된 익스텐트가 가득 찰 때마다 추가 익스텐트가 할당됩니다. 할당 되 고 테이블에서 사용 하는 공간의 크기에 대 한 보고서의 경우 실행 **sp_spaceused**합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 열 정의에 DEFAULT, IDENTITY, ROWGUIDCOL 또는 열 제약 조건을 지정하는 특정한 순서를 요구하지는 않습니다.  
  
 QUOTED IDENTIFIER 옵션은 테이블을 만들 때 OFF로 설정되어 있더라도 해당 테이블의 메타데이터에 항상 ON으로 저장됩니다.  
  
## <a name="temporary-tables"></a>임시 테이블  
 로컬 및 전역 임시 테이블을 만들 수 있습니다. 로컬 임시 테이블은 현재 세션에서만 볼 수 있으며 전역 임시 테이블은 모든 세션에서 볼 수 있습니다. 임시 테이블은 분할할 수 없습니다.  
  
 로컬 임시 테이블 이름 앞에 단일 숫자 기호 (#*table_name*), 및 전역 임시 테이블 이름 앞에 이중 숫자 기호 (# #*table_name*).  
  
 에 지정 된 값을 사용 하 여 임시 테이블을 참조 하는 SQL 문을 *table_name* 예제 # # #에 대 한 CREATE TABLE 문에서:  
  
```  
CREATE TABLE #MyTempTable (cola INT PRIMARY KEY);  
  
INSERT INTO #MyTempTable VALUES (1);  
```  
  
 단일 저장 프로시저나 일괄 처리 내에 둘 이상의 임시 테이블을 만드는 경우 그 이름이 서로 달라야 합니다.  
  
 여러 사용자가 동시에 실행할 수 있는 저장 프로시저 또는 응용 프로그램에서 로컬 임시 테이블을 만드는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 다른 사용자가 만든 테이블을 구별할 수 있어야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 내부적으로 각 로컬 임시 테이블 이름에 숫자 접미사를 추가하여 구별합니다. 임시 테이블에 저장 된 것과 전체 이름을 **sysobjects** 테이블에 **tempdb** CREATE TABLE 문과 시스템에서 생성 된 숫자 접미사에 지정 된 테이블 이름으로 이루어집니다. 접미사를 허용 하려면 *table_name* 지정 된 로컬 임시 이름에는 116 자를 초과할 수 없습니다.  
  
 임시 테이블은 DROP TABLE을 사용하여 명시적으로 삭제하지 않으면 범위를 벗어날 때 자동으로 삭제됩니다.  
  
-   저장 프로시저에서 만든 로컬 임시 테이블은 저장 프로시저를 마칠 때 자동으로 삭제합니다. 테이블은 해당 테이블을 만든 저장 프로시저가 실행하는 모든 중첩된 저장 프로시저에서 참조할 수 있습니다. 테이블을 만든 저장 프로시저를 호출한 프로세스는 해당 테이블을 참조할 수 없습니다.  
  
-   기타 모든 로컬 임시 테이블은 현재 세션이 끝날 때 자동으로 삭제됩니다.  
  
-   전역 임시 테이블은 테이블을 만든 세션이 끝나고 이를 참조하는 다른 모든 태스크가 중지되면 자동으로 삭제됩니다. 태스크와 테이블 간의 연결은 단일 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 사용 기간 동안만 유지 관리됩니다. 즉, 전역 임시 테이블은 만들기 세션이 끝났을 때 활동적으로 테이블을 참조하는 마지막 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 완료되면 삭제됩니다.  
  
 저장 프로시저 또는 트리거에서 만드는 로컬 임시 테이블은 저장 프로시저 또는 트리거를 호출하기 전에 만든 임시 테이블과 동일한 이름을 사용할 수 있습니다. 그러나 쿼리가 임시 테이블을 참조하고 이때 같은 이름을 가진 두 개의 임시 테이블이 동시에 존재하면 쿼리가 확인할 테이블은 정의되지 않습니다. 중첩된 저장 프로시저도 이를 호출한 저장 프로시저가 만든 임시 테이블과 동일한 이름으로 임시 테이블을 만들 수 있습니다. 그러나 중첩된 프로시저에서 만든 테이블에 대한 수정 사항을 확인하려면 테이블의 구조 및 열 이름이 호출 프로시저에서 만든 테이블과 같아야 합니다. 이는 다음 예에서 확인할 수 있습니다.  
  
```  
CREATE PROCEDURE dbo.Test2  
AS  
    CREATE TABLE #t(x INT PRIMARY KEY);  
    INSERT INTO #t VALUES (2);  
    SELECT Test2Col = x FROM #t;  
GO  
  
CREATE PROCEDURE dbo.Test1  
AS  
    CREATE TABLE #t(x INT PRIMARY KEY);  
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
  
 `(1 row(s) affected)`  
  
 `Test1Col`  
  
 `-----------`  
  
 `1`  
  
 `(1 row(s) affected)`  
  
 `Test2Col`  
  
 `-----------`  
  
 `2`  
  
 로컬 또는 전역 임시 테이블을 만들 때 CREATE TABLE 구문은 FOREIGN KEY 제약 조건을 제외한 다른 모든 제약 조건 정의를 지원합니다. 임시 테이블에서 FOREIGN KEY 제약 조건을 지정하면 문에서 해당 제약 조건을 건너뛰었다는 경고 메시지를 반환하며 FOREIGN KEY 제약 조건 없이 테이블을 만듭니다. 임시 테이블은 FOREIGN KEY 제약 조건에서 참조할 수 없습니다.  
  
 명명된 제약 조건으로 사용자 정의 트랜잭션의 범위 내에 임시 테이블을 만드는 경우 한 번에 한 사용자만 임시 테이블을 만드는 문을 실행할 수 있습니다. 예를 들어 저장 프로시저에서 명명된 기본 키 제약 조건을 사용하여 임시 테이블을 만드는 경우 여러 사용자가 동시에 저장 프로시저를 실행할 수 없습니다.  


## <a name="database-scoped-global-temporary-tables-azure-sql-database"></a>데이터베이스 범위 전역 임시 테이블 (Azure SQL 데이터베이스)

SQL Server에 대 한 전역 임시 테이블 (된 시작 # # 테이블 이름)은 tempdb에 저장 되 고 전체 SQL Server 인스턴스에서 모든 사용자의 세션 간에 공유 합니다. SQL 테이블 형식에 대 한 내용은 테이블 만들기에 위의 섹션을 참조 합니다.  

Azure SQL 데이터베이스도 tempdb에 저장 되 고 데이터베이스 수준으로 범위는 전역 임시 테이블을 지원 합니다.  즉, 전역 임시 테이블은 동일한 Azure SQL 데이터베이스 내에서 모든 사용자의 세션에 대 한 공유 됩니다. 다른 Azure SQL 데이터베이스에서 사용자 세션 전역 임시 테이블에 액세스할 수 없습니다.

Azure SQL DB에 대 한 전역 임시 테이블 구문 및 의미 체계를 임시 테이블에 대 한 SQL Server 사용 하 여 동일한 따릅니다.  마찬가지로, 전역 임시 저장된 프로시저에서 데이터베이스 수준에서 Azure SQL DB의 범위 지정도 됩니다. 로컬 임시 테이블 (# 테이블 이름으로 시작) Azure SQL 데이터베이스에 대해 지원 되 고 동일한 구문 및 의미 체계를 SQL Server를 사용 합니다.  위의 섹션을 참조 하십시오 [임시 테이블](#temporary-tables)합니다.  

> [!IMPORTANT]
> 이 기능은 공개 미리 보기 중 이며 Azure SQL 데이터베이스에 사용할 수 있습니다.
>

### <a name="troubleshooting-global-temporary-tables-for-azure-sql-db"></a>Azure SQL DB에 대 한 전역 임시 테이블을 문제 해결 

문제 해결 tempdb에 대 한 참조 [문제 해결에 디스크 공간이 부족 tempdb](https://technet.microsoft.com/library/ms176029%28v=sql.105%29.aspx?f=255&MSPPError=-2147217396)합니다. Azure SQL 데이터베이스의 문제 해결 Dmv에 액세스 하려면 서버 관리자 여야 합니다.
  
### <a name="permissions"></a>Permissions  

 모든 사용자는 전역 임시 개체를 만들 수 있습니다. 사용자가 추가 사용 권한을 받는 경우를 제외하고 자신의 고유 개체에만 액세스할 수 있습니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.  
  
### <a name="examples"></a>예 

- Session A가 testdb1 Azure SQL 데이터베이스에서에서 전역 임시 테이블 ##test을 만들고 1 개 행 추가

```tsql
CREATE TABLE ##test ( a int, b int);
INSERT INTO ##test values (1,1);

--Obtain object ID for temp table ##test 
SELECT OBJECT_ID('tempdb.dbo.##test') AS 'Object ID'; 

---Result
1253579504

---Obtain global temp table name for a given object ID 1253579504 in tempdb (2)
SELECT name FROM tempdb.sys.objects WHERE object_id = 1253579504

---Result
##test
```
- 세션 B testdb1 Azure SQL 데이터베이스에 연결 하 고 ##test A 세션에서 만든 테이블에 액세스할 수 있습니다.

```tsql
SELECT * FROM ##test
---Results
1,1
```

- 세션 C testdb2 Azure SQL 데이터베이스의에서 다른 데이터베이스에 연결 및 testdb1에서 만든 ##test에 액세스 하려고 합니다. 전역 임시 테이블에 대 한 데이터베이스 범위이 선택이 실패 

```tsql
SELECT * FROM ##test
---Results
Msg 208, Level 16, State 0, Line 1
Invalid object name '##test'
```

- 현재 사용자 데이터베이스 testdb1에서 Azure SQL 데이터베이스 tempdb에 시스템 개체를 주소 지정

```tsql
SELECT * FROM tempdb.sys.objects
SELECT * FROM tempdb.sys.columns
SELECT * FROM tempdb.sys.database_files
```



## <a name="partitioned-tables"></a>분할된 테이블  
 CREATE TABLE을 사용하여 분할된 테이블을 만들기 전에 테이블이 분할되는 방식을 지정하는 파티션 함수를 만들어야 합니다. 파티션 함수를 사용 하 여 만들 [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)합니다. 그런 다음 파티션 구성표를 만들어 파티션 함수가 표시하는 파티션을 유지하는 파일 그룹을 지정해야 합니다. 파티션 구성표를 사용 하 여 만들 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)합니다. 분할된 테이블에는 파일 그룹을 분리하는 PRIMARY KEY 또는 UNIQUE 제약 조건을 지정할 수 없습니다. 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)을 참조하세요.  
  
## <a name="primary-key-constraints"></a>PRIMARY KEY 제약 조건  
  
-   테이블은 하나의 PRIMARY KEY 제약 조건만 포함할 수 있습니다.  
  
-   PRIMARY KEY 제약 조건에 의해 생성된 인덱스 수는 비클러스터형 인덱스 999개, 클러스터형 인덱스 1개인 테이블의 인덱스 수 제한을 초과할 수 없습니다.  
  
-   PRIMARY KEY 제약 조건에 대해 CLUSTERED 또는 NONCLUSTERED를 지정하지 않은 경우 UNIQUE 제약 조건에 대해 클러스터형 인덱스를 지정하지 않으면 CLUSTERED가 사용됩니다.  
  
-   PRIMARY KEY 제약 조건 내에서 정의된 모든 열은 NOT NULL로 정의되어야 합니다. NULL 허용 여부를 지정하지 않은 경우에는 PRIMARY KEY 제약 조건에 참여하는 모든 열의 NULL 허용 여부가 NOT NULL로 설정됩니다.  
  
    > [!NOTE]  
    >  메모리 액세스에 최적화 된 테이블의 null을 허용 하는 키 열은 사용할 수 있습니다.  
  
-   CLR 사용자 정의 형식 열에 기본 키를 정의하는 경우 형식 구현이 이진 순서를 지원해야 합니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.  
  
## <a name="unique-constraints"></a>UNIQUE 제약 조건  
  
-   UNIQUE 제약 조건에 CLUSTERED 또는 NONCLUSTERED를 지정하지 않은 경우에는 기본적으로 NONCLUSTERED가 사용됩니다.  
  
-   각 UNIQUE 제약 조건은 인덱스를 생성합니다. UNIQUE 제약 조건의 수가 많아도 테이블의 비클러스터형 인덱스는 999개, 클러스터형 인덱스는 1개를 초과할 수 없습니다.  
  
-   CLR 사용자 정의 형식 열에 UNIQUE 제약 조건을 정의하는 경우 형식 구현이 이진 순서 또는 연산자 기반의 순서를 지원해야 합니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.  
  
## <a name="foreign-key-constraints"></a>FOREIGN KEY 제약 조건  
  
-   FOREIGN KEY 제약 조건의 열에 NULL 외의 다른 값을 입력한 경우에는 그 값이 참조되는 열에 있어야 합니다. 그렇지 않은 경우에는 외래 키 위반 오류 메시지가 반환됩니다.  
  
-   원본 열을 지정하지 않는 한 FOREIGN KEY 제약 조건이 선행 열에 적용됩니다.  
  
-   FOREIGN KEY 제약 조건은 같은 서버의 같은 데이터베이스 내에 있는 테이블만 참조할 수 있습니다. 상호 데이터베이스 참조 무결성은 트리거를 통해 구현해야 합니다. 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)를 참조하세요.  
  
-   FOREIGN KEY 제약 조건은 같은 테이블에 있는 다른 열을 참조할 수 있습니다. 이것을 자체 참조라고 합니다.  
  
-   열 수준 FOREIGN KEY 제약 조건의 REFERENCES 절은 참조 열을 하나만 나열할 수 있습니다. 이 열의 데이터 형식은 제약 조건이 정의된 열의 데이터 형식과 같아야 합니다.  
  
-   테이블 수준 FOREIGN KEY 제약 조건의 REFERENCES 절에는 제약 조건 열 목록의 열 개수와 같은 수의 참조 열이 있어야 합니다. 각 참조 열의 데이터 형식도 열 목록의 해당 열과 같아야 합니다.  
  
-   CASCADE, SET NULL 또는 SET DEFAULT를 지정할 수 없습니다 경우 형식의 열 **타임 스탬프** 외래 키 또는 참조 되는 키의 일부입니다.  
  
-   CASCADE, SET NULL, SET DEFAULT 및 NO ACTION은 서로 참조 관계를 가진 테이블에서 결합될 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 NO ACTION을 발견하면 관련된 CASCADE, SET NULL 및 SET DEFAULT 동작을 멈추고 롤백합니다. DELETE 문으로 CASCADE, SET NULL, SET DEFAULT 및 NO ACTION 동작을 결합하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 NO ACTION을 확인하기 전에 모든 CASCADE, SET NULL 및 SET DEFAULT 동작을 적용합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 테이블에 포함하여 다른 테이블을 참조하는 FOREIGN KEY 제약 조건의 수나 특정 테이블을 참조하는 다른 테이블 소유의 FOREIGN KEY 제약 조건의 수에 미리 한계를 정의하지 않습니다.  
  
     하지만 실제로 사용할 수 있는 FOREIGN KEY 제약 조건의 수는 하드웨어 구성 및 데이터베이스와 응용 프로그램의 디자인에 따라 제한됩니다. 테이블에 포함되거나 이 테이블을 참조하는 FOREIGN KEY 제약 조건의 수가 각각 253개를 넘지 않도록 하는 것이 좋습니다. 유효 한계는 응용 프로그램과 하드웨어에 따라 더 많거나 적을 수 있습니다. 데이터베이스와 응용 프로그램을 디자인할 때는 FOREIGN KEY 제약 조건을 적용하는 비용도 고려하십시오.  
  
-   임시 테이블에는 FOREIGN KEY 제약 조건이 적용되지 않습니다.  
  
-   FOREIGN KEY 제약 조건은 참조되는 테이블의 PRIMARY KEY 또는 UNIQUE 제약 조건에 있는 열이나 참조되는 테이블의 UNIQUE INDEX에 있는 열만 참조할 수 있습니다.  
  
-   CLR 사용자 정의 형식 열에 외래 키를 정의하는 경우 형식 구현이 이진 순서를 지원해야 합니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.  
  
-   외래 키 관계에 참여하는 열은 같은 길이와 배율로 정의되어야 합니다.  
  
## <a name="default-definitions"></a>DEFAULT 정의  
  
-   하나의 열에는 하나의 DEFAULT 정의만 있을 수 있습니다.  
  
-   DEFAULT 정의는 상수 값, 함수, SQL 표준 무항 함수 또는 NULL을 포함할 수 있습니다. 다음 표에서는 무항 함수 및 무항 함수가 INSERT 문에서 기본적으로 반환하는 값을 보여 줍니다.  
  
    |SQL-92 무항 함수|반환 값|  
    |------------------------------|--------------------|  
    |CURRENT_TIMESTAMP|현재 날짜 및 시간입니다.|  
    |CURRENT_USER|삽입을 수행하는 사용자의 이름입니다.|  
    |SESSION_USER|삽입을 수행하는 사용자의 이름입니다.|  
    |SYSTEM_USER|삽입을 수행하는 사용자의 이름입니다.|  
    |User|삽입을 수행하는 사용자의 이름입니다.|  
  
-   *constant_expression* 또는 다른 테이블, 뷰 또는 저장된 프로시저는 테이블의 다른 열에는 기본 정의 참조할 수 없습니다.  
  
-   열에 DEFAULT 정의 만들 수 없습니다는 **타임 스탬프** 데이터 형식 또는 IDENTITY 속성이 있는 열입니다.  
  
-   별칭 데이터 형식이 기본 개체에 바인딩된 경우에는 별칭 데이터 형식의 열에 대해 DEFAULT 정의를 만들 수 없습니다.  
  
## <a name="check-constraints"></a>CHECK 제약 조건  
  
-   하나의 열은 원하는 수만큼의 CHECK 제약 조건을 가질 수 있으며 조건은 AND 및 OR로 결합된 여러 논리 식을 포함할 수 있습니다. 열에 대한 여러 CHECK 제약 조건은 만든 순서대로 검사됩니다.  
  
-   검색 조건은 부울 식으로 계산되어야 하며 다른 테이블을 참조할 수 없습니다.  
  
-   열 수준의 CHECK 제약 조건은 제약된 열만 참조할 수 있으며 테이블 수준의 CHECK 제약 조건은 같은 테이블의 열만 참조할 수 있습니다.  
  
     CHECK CONSTRAINTS 및 규칙은 INSERT 및 UPDATE 문 동안 데이터의 유효성을 검사하는 동일한 역할을 합니다.  
  
-   열에 규칙 및 하나 이상의 CHECK 제약 조건이 있는 경우에는 모든 제한을 평가합니다.  
  
-   CHECK 제약 조건을 정의할 수 없습니다 **텍스트**, **ntext**, 또는 **이미지** 열입니다.  
  
## <a name="additional-constraint-information"></a>추가 제약 조건 정보  
  
-   제약 조건으로 생성된 인덱스는 DROP INDEX 문으로 삭제할 수 없으며 제약 조건은 ALTER TABLE 문으로 삭제해야 합니다. 제약 조건이 만들고 사용하는 인덱스는 ALTER INDEX...REBUILD를 사용하여 다시 작성할 수 있습니다. 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
-   제약 조건 이름에 대 한 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)한다는 점을 제외 하는 이름은 #로 시작할 수 없습니다 (#). 경우 *constraint_name* 는 제공 하지는 시스템에서 생성 된 이름이 제약 조건에 지정 됩니다. 제약 조건 이름은 제약 조건 위반에 대한 모든 오류 메시지에 표시됩니다.  
  
-   INSERT, UPDATE 또는 DELETE 문에서 제약 조건을 위반한 경우에는 문이 종료됩니다. 하지만 SET XACT_ABORT를 OFF로 설정하면 문이 명시적 트랜잭션의 일부인 경우 그 트랜잭션은 계속 처리됩니다. SET XACT_ABORT를 ON으로 설정하면 전체 트랜잭션이 롤백됩니다. 선택 하 여 트랜잭션 정의와 함께 ROLLBACK TRANSACTION 문을 사용할 수도 있습니다는 @@ERROR 시스템 함수입니다.  
  
-   ALLOW_ROW_LOCKS = ON이고 ALLOW_PAGE_LOCK = ON이면 인덱스에 액세스할 때 행, 페이지 및 테이블 수준 잠금이 허용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 적절한 잠금을 선택하고 행 또는 페이지 잠금에서 테이블 잠금으로 잠금을 에스컬레이션할 수 있습니다. ALLOW_ROW_LOCKS = OFF이고 ALLOW_PAGE_LOCK = OFF이면 인덱스에 액세스할 때 테이블 수준 잠금만 허용됩니다.  
  
-   테이블에 FOREIGN KEY 또는 CHECK CONSTRAINTS 및 트리거가 있는 경우에는 트리거를 실행하기 전에 제약 조건에 대한 조건을 평가합니다.  
  
 테이블과 해당 열에 대 한 보고서를 사용 하 여 **sp_help** 또는 **sp_helpconstraint**합니다. 사용 하 여 테이블의 이름을 바꾸려면 **sp_rename**합니다. 에 대 한 보고서 뷰 및 테이블에 종속 된 저장된 프로시저를 사용 하 여 [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) 및 [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)합니다.  
  
## <a name="nullability-rules-within-a-table-definition"></a>테이블 정의 내의 NULL 허용 여부 규칙  
 열의 Null 허용 여부에 따라 해당 열의 데이터로 Null 값(NULL)을 허용할 수 있는지 여부가 결정됩니다. NULL은 0 또는 공백이 아니며 항목을 만들지 않았거나 명시적인 NULL을 지정했음을 의미하는 것으로 일반적으로 값을 알 수 없거나 적용할 수 없음을 나타냅니다.  
  
 CREATE TABLE 또는 ALTER TABLE 문을 사용하여 테이블을 만들거나 변경할 때는 데이터베이스 및 세션 설정이 열 정의에 사용된 데이터 형식의 Null 허용 여부에 영향을 미치고 덮어 쓸 가능성이 있습니다. 비계산 열은 항상 NULL 또는 NOT NULL로 명시적으로 정의하는 것이 좋으며 사용자 정의 데이터 형식을 사용할 때는 열에 해당 데이터 형식의 기본 Null 허용 여부를 적용하는 것이 좋습니다. 스파스 열은 항상 NULL을 허용해야 합니다.  
  
 열의 Null 허용 여부를 명시적으로 지정하지 않은 경우 열의 Null 허용 여부는 다음 표의 규칙을 따릅니다.  
  
|열 데이터 형식|규칙|  
|----------------------|----------|  
|별칭 데이터 형식|[!INCLUDE[ssDE](../../includes/ssde-md.md)]은 데이터 형식을 만들 때 지정한 Null 허용 여부를 사용합니다. 데이터 형식의 기본 null 허용 여부를 확인 하려면 사용 하 여 **sp_help**합니다.|  
|CLR 사용자 정의 형식(CLR user-defined type)|열 정의에 따라 Null 허용 여부를 결정합니다.|  
|시스템이 제공하는 데이터 형식|시스템이 제공하는 데이터 형식에 옵션이 하나뿐인 경우에는 이 옵션이 우선 순위를 갖습니다. **타임 스탬프** NULL이 아님 데이터 형식 이어야 합니다. SET를 사용하여 모든 세션 설정을 ON으로 설정한 경우:<br />**ANSI_NULL_DFLT_ON** = ON, NULL이 할당 됩니다.  <br />**ANSI_NULL_DFLT_OFF** = ON, NOT NULL이 할당 됩니다.<br /><br /> ALTER DATABASE를 사용하여 모든 데이터베이스 설정을 구성한 경우:<br />**ANSI_NULL_DEFAULT_ON** = ON, NULL이 할당 됩니다.  <br />**ANSI_NULL_DEFAULT_OFF** = ON, NOT NULL이 할당 됩니다.<br /><br /> ANSI_NULL_DEFAULT에 대 한 데이터베이스 설정을 보려면 사용 하 여는 **sys.databases** 카탈로그 뷰|  
  
 세션에 대해 어떠한 ANSI_NULL_DFLT 옵션도 설정하지 않고 데이터베이스를 기본값(ANSI_NULL_DEFAULT가 OFF)으로 설정하면 기본값인 NOT NULL이 할당됩니다.  
  
 열이 계산 열인 경우에는 항상 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 열의 Null 허용 여부를 자동으로 결정합니다. 이러한 유형의 열 null 허용 여부를 확인 하려면 COLUMNPROPERTY 함수를 사용 하 여는 **AllowsNull** 속성입니다.  
  
> [!NOTE]  
>  SQL Server ODBC 드라이버 및 SQL Server용 Microsoft OLE DB Provider는 모두 기본적으로 ANSI_NULL_DFLT_ON이 ON으로 설정되어 있습니다. ODBC 및 OLE DB 사용자는 ODBC 데이터 원본에서 이를 구성하거나 응용 프로그램이 설정한 연결 속성 또는 특성을 사용하여 이를 구성할 수 있습니다.  
  
## <a name="data-compression"></a>Data Compression  
 시스템 테이블에는 압축을 사용할 수 없습니다. 테이블을 만들 때 데이터 압축은 달리 지정하지 않는 한 NONE으로 설정됩니다. 범위를 벗어난 파티션 목록을 지정하면 오류가 발생합니다. 데이터 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
 압축 상태를 변경할 경우 테이블, 인덱스 또는 파티션에 어떤 영향을 주는지 확인하려면 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 저장 프로시저를 사용합니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에는 CREATE TABLE 권한이 필요하고 테이블을 만들 구성표에는 ALTER 권한이 필요합니다.  
  
 CREATE TABLE 문에 있는 열을 CLR 사용자 정의 형식으로 정의하는 경우 해당 유형의 소유권이나 이에 대한 REFERENCES 권한이 필요합니다.  
  
 CREATE TABLE 문의 열에 연관된 XML 스키마 컬렉션이 있는 경우 XML 스키마 컬렉션의 소유권이나 이에 대한 REFERENCES 권한이 필요합니다.  
  
 모든 사용자는 tempdb에 임시 테이블을 만들 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-create-a-primary-key-constraint-on-a-column"></a>1. 열에 PRIMARY KEY 제약 조건 만들기  
 다음 예에서는 `EmployeeID` 테이블의 `Employee` 열에 클러스터형 인덱스가 있는 PRIMARY KEY 제약 조건에 대한 열 정의를 보여 줍니다. 제약 조건 이름을 지정하지 않았기 때문에 시스템에서 제약 조건 이름을 제공합니다.  
  
```  
CREATE TABLE dbo.Employee (EmployeeID int  
PRIMARY KEY CLUSTERED);  
```  
  
### <a name="b-using-foreign-key-constraints"></a>2. FOREIGN KEY 제약 조건 사용  
 FOREIGN KEY 제약 조건은 다른 테이블을 참조하는 데 사용됩니다. 외래 키는 단일 열 키 또는 복수 열 키가 될 수 있습니다. 다음 예에서는 `SalesOrderHeader` 테이블을 참조하는 `SalesPerson` 테이블에 대한 단일 열 FOREIGN KEY 제약 조건을 보여 줍니다. 단일 열 FOREIGN KEY 제약 조건에는 REFERENCES 절만 필요합니다.  
  
```  
SalesPersonID int NULL  
REFERENCES SalesPerson(SalesPersonID)  
```  
  
 또한 명시적으로 FOREIGN KEY 절을 사용하여 열 특성을 다시 정할 수 있습니다. 두 테이블에서 같은 열 이름을 사용할 필요는 없습니다.  
  
```  
FOREIGN KEY (SalesPersonID) REFERENCES SalesPerson(SalesPersonID)  
```  
  
 테이블 제약 조건으로 복수 열 키 제약 조건을 만듭니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 `SpecialOfferProduct` 테이블은 복수 열 PRIMARY KEY를 포함합니다. 다음 예에서는 다른 테이블에서 이 키를 참조하는 방법을 보여 줍니다. 명시적인 제약 조건 이름은 선택적입니다.  
  
```  
CONSTRAINT FK_SpecialOfferProduct_SalesOrderDetail FOREIGN KEY  
 (ProductID, SpecialOfferID)  
REFERENCES SpecialOfferProduct (ProductID, SpecialOfferID)  
```  
  
### <a name="c-using-unique-constraints"></a>3. UNIQUE 제약 조건 사용  
 UNIQUE 제약 조건은 기본 키가 아닌 열에 고유성을 적용합니다. 다음 예에서는 `Name` 테이블의 `Product` 열이 고유한 것이어야 한다는 제한을 적용합니다.  
  
```  
Name nvarchar(100) NOT NULL  
UNIQUE NONCLUSTERED  
```  
  
### <a name="d-using-default-definitions"></a>4. DEFAULT 정의 사용  
 기본값은 값을 지정하지 않은 경우 사용할 값을 INSERT 및 UPDATE 문으로 제공합니다. 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스는 회사에서 직원이 담당하는 각기 다른 업무를 나열하는 조회 테이블을 포함할 수 있습니다. 각각의 업무를 기술하는 열에 실제 설명을 명시적으로 입력하지 않으면 문자열 기본값으로 설명을 제공할 수 있습니다.  
  
```  
DEFAULT 'New Position - title not formalized yet'  
```  
  
 DEFAULT 정의는 제약 조건 외에도 함수를 포함할 수 있습니다. 항목의 현재 날짜를 보려면 다음 예를 사용하십시오.  
  
```  
DEFAULT (getdate())  
```  
  
 무항 함수 검색도 데이터 무결성을 향상시킵니다. 행을 삽입한 사용자를 추적하려면 USER에 대한 무항 함수를 사용하십시오. 무항 함수를 괄호로 묶지 마십시오.  
  
```  
DEFAULT USER  
```  
  
### <a name="e-using-check-constraints"></a>5. CHECK 제약 조건 사용  
 다음 예에서는 `CreditRating` 테이블의 `Vendor` 열에 입력한 값에 대한 제한을 보여 줍니다. 제약 조건은 명명되지 않았습니다.  
  
```  
CHECK (CreditRating >= 1 and CreditRating <= 5)  
```  
  
 다음 예에서는 테이블의 열에 입력된 문자 데이터에 대한 패턴 제한이 있는 명명된 제약 조건을 보여 줍니다.  
  
```  
CONSTRAINT CK_emp_id CHECK (emp_id LIKE   
'[A-Z][A-Z][A-Z][1-9][0-9][0-9][0-9][0-9][FM]'   
OR emp_id LIKE '[A-Z]-[A-Z][1-9][0-9][0-9][0-9][0-9][FM]')  
```  
  
 다음 예에서는 값이 특정 목록에 있도록 하거나 지정한 패턴을 따르도록 지정합니다.  
  
```  
CHECK (emp_id IN ('1389', '0736', '0877', '1622', '1756')  
OR emp_id LIKE '99[0-9][0-9]')  
```  
  
### <a name="f-showing-the-complete-table-definition"></a>6. 전체 테이블 정의 표시  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 만든 `PurchaseOrderDetail` 테이블에 대한 모든 제약 조건 정의를 가진 전체 테이블 정의를 보여 줍니다. 예제를 실행하기 위해 테이블 스키마가 `dbo`로 변경됩니다.  
  
```  
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
    rowguid uniqueidentifier ROWGUIDCOL  NOT NULL  
        CONSTRAINT DF_PurchaseOrderDetail_rowguid DEFAULT (newid()),  
    ModifiedDate datetime NOT NULL   
        CONSTRAINT DF_PurchaseOrderDetail_ModifiedDate DEFAULT (getdate()),  
    LineTotal  AS ((UnitPrice*OrderQty)),  
    StockedQty  AS ((ReceivedQty-RejectedQty)),  
    CONSTRAINT PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber  
               PRIMARY KEY CLUSTERED (PurchaseOrderID, LineNumber)  
               WITH (IGNORE_DUP_KEY = OFF)  
)   
ON PRIMARY;  
```  
  
### <a name="g-creating-a-table-with-an-xml-column-typed-to-an-xml-schema-collection"></a>7. XML 스키마 컬렉션 유형의 xml 열을 가진 테이블 만들기  
 다음 예에서는 XML 스키마 컬렉션 `xml` 유형의 `HRResumeSchemaCollection` 열이 있는 테이블을 만듭니다. `DOCUMENT` 키워드를 지정 하는 각 인스턴스에 `xml` 데이터 형식에 *column_name* 하나의 최상위 요소만 포함 될 수 있습니다.  
  
```  
CREATE TABLE HumanResources.EmployeeResumes   
   (LName nvarchar(25), FName nvarchar(25),   
    Resume xml( DOCUMENT HumanResources.HRResumeSchemaCollection) );  
```  
  
### <a name="h-creating-a-partitioned-table"></a>8. 분할된 테이블 만들기  
 다음 예에서는 테이블이나 인덱스를 4개의 파티션으로 분할하는 파티션 함수를 만듭니다. 그런 다음 4개의 파티션을 각각 보관할 파일 그룹을 지정하는 파티션 구성표를 만듭니다. 마지막으로 파티션 구성표를 사용하는 테이블을 만듭니다. 이 예에서는 데이터베이스에 이미 파일 그룹이 있다고 가정합니다.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES (1, 100, 1000) ;  
GO  
  
CREATE PARTITION SCHEME myRangePS1  
    AS PARTITION myRangePF1  
    TO (test1fg, test2fg, test3fg, test4fg) ;  
GO  
  
CREATE TABLE PartitionTable (col1 int, col2 char(10))  
    ON myRangePS1 (col1) ;  
GO  
```  
  
 `col1`의 `PartitionTable` 열 값을 바탕으로 하여 다음과 같은 방법으로 파티션을 할당합니다.  
  
|파일 그룹|test1fg|test2fg|test3fg|test4fg|  
|---------------|-------------|-------------|-------------|-------------|  
|**파티션**|1.|2|3|4|  
|**값**|열 1 \<= 1|c o l 1 > 1 AND col1 \<= 100|c o l 1 > 100 AND col1 \<= 1, 000|col1 > 1000|  
  
### <a name="i-using-the-uniqueidentifier-data-type-in-a-column"></a>9. 열에 uniqueidentifier 데이터 형식 사용  
 다음 예에서는 `uniqueidentifier` 열이 있는 테이블을 만듭니다. 이 예에서는 PRIMARY KEY 제약 조건을 사용하여 사용자가 중복 값을 삽입하지 못하도록 테이블을 보호하고 `NEWSEQUENTIALID()` 제약 조건의 `DEFAULT` 함수를 사용하여 새 행에 대한 값을 제공합니다. `uniqueidentifier` 열을 $ROWGUID 키워드로 참조할 수 있도록 이 열에 ROWGUIDCOL 속성이 적용됩니다.  
  
```  
CREATE TABLE dbo.Globally_Unique_Data  
    (guid uniqueidentifier   
        CONSTRAINT Guid_Default DEFAULT   
        NEWSEQUENTIALID() ROWGUIDCOL,  
    Employee_Name varchar(60)  
    CONSTRAINT Guid_PK PRIMARY KEY (guid) );  
```  
  
### <a name="j-using-an-expression-for-a-computed-column"></a>10. 계산 열에 식 사용  
 다음 예에서는 `(low + high)/2` 계산 열을 계산하기 위해 식(`myavg`)을 사용하는 방법을 보여 줍니다.  
  
```  
CREATE TABLE dbo.mytable   
    ( low int, high int, myavg AS (low + high)/2 ) ;  
```  
  
### <a name="k-creating-a-computed-column-based-on-a-user-defined-type-column"></a>11. 사용자 정의 형식의 열을 기반으로 계산 열 만들기  
 다음 예에서는 유형의 어셈블리와 유형 자체를 현재 데이터베이스에 이미 만들었다고 가정하고 사용자 정의 형식 `utf8string`으로 정의된 하나의 열을 가진 테이블을 만드는 방법을 보여 줍니다. 두 번째 열에 따라 정의 됩니다 `utf8string`, 메서드를 사용 하 여 `ToString()` 의 **type(class)** `utf8string` 열에 대 한 값을 계산 합니다.  
  
```  
CREATE TABLE UDTypeTable   
    ( u utf8string, ustr AS u.ToString() PERSISTED ) ;  
```  
  
### <a name="l-using-the-username-function-for-a-computed-column"></a>12. 계산 열에 USER_NAME 함수 사용  
 다음 예에서는 `USER_NAME()` 열에 `myuser_name` 함수를 사용하는 방법을 보여 줍니다.  
  
```  
CREATE TABLE dbo.mylogintable  
    ( date_in datetime, user_id int, myuser_name AS USER_NAME() ) ;  
```  
  
### <a name="m-creating-a-table-that-has-a-filestream-column"></a>13. FILESTREAM 열이 있는 테이블 만들기  
 다음 예에서는 `FILESTREAM` 열 `Photo`가 있는 테이블을 만듭니다. 하나 이상의 `FILESTREAM` 열이 있는 테이블에는 하나의 `ROWGUIDCOL` 열이 있어야 합니다.  
  
```  
CREATE TABLE dbo.EmployeePhoto  
    (  
    EmployeeId int NOT NULL PRIMARY KEY,  
    ,Photo varbinary(max) FILESTREAM NULL  
    ,MyRowGuidColumn uniqueidentifier NOT NULL ROWGUIDCOL  
        UNIQUE DEFAULT NEWID()  
    );  
```  
  
### <a name="n-creating-a-table-that-uses-row-compression"></a>14. 행 압축을 사용하는 테이블 만들기  
 다음 예에서는 행 압축을 사용하는 테이블을 만듭니다.  
  
```  
CREATE TABLE dbo.T1   
(c1 int, c2 nvarchar(200) )  
WITH (DATA_COMPRESSION = ROW);  
```  
  
 추가 데이터 압축 예 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
### <a name="o-creating-a-table-that-has-sparse-columns-and-a-column-set"></a>15. 스파스 열 및 열 집합이 있는 테이블 만들기  
 다음 예에서는 스파스 열이 있는 테이블과 두 개의 스파스 열 및 열 집합이 있는 테이블을 만드는 방법을 보여 줍니다. 이 예에서는 기본 구문을 사용합니다. 더 복잡 한 예제를 참조 하십시오. [스파스 열을 사용 하 여](../../relational-databases/tables/use-sparse-columns.md) 및 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)합니다.  
  
 이 예에서는 스파스 열이 있는 테이블을 만듭니다.  
  
```  
CREATE TABLE dbo.T1  
    (c1 int PRIMARY KEY,  
    c2 varchar(50) SPARSE NULL ) ;  
```  
  
 이 예에서는 두 개의 스파스 열과 `CSet`이라는 열 집합이 있는 테이블을 만듭니다.  
  
```  
CREATE TABLE T1  
    (c1 int PRIMARY KEY,  
    c2 varchar(50) SPARSE NULL,  
    c3 int SPARSE NULL,  
    CSet XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ) ;  
```  
  
### <a name="p-creating-a-system-versioned-disk-based-temporal-table"></a>16. 시스템 버전 관리 디스크 기반 임시 테이블 만들기  
   
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.
  
 다음 예제는 새 기록 테이블에 연결 된 임시 테이블을 만드는 방법과 기존 기록 테이블에 연결 된 임시 테이블을 만드는 방법을 보여 줍니다. 임시 테이블을 시스템 버전 관리에 사용할 테이블을 설정 하도록 정의 된 기본 키가 있어야 하는 참고 합니다. 참조에서 시스템 버전 관리를 추가 하거나 기존 테이블에 시스템 버전 관리를 제거 하는 방법을 보여 주는 예제를 보려면 [예제](../../t-sql/statements/alter-table-transact-sql.md#Example_Top)합니다. 사용 사례를 참조 하십시오. [임시 테이블](../../relational-databases/tables/temporal-tables.md)합니다.  
  
 이 예제는 새 기록 테이블에 연결 된 새 임시 테이블을 만듭니다.  
  
```  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH (SYSTEM_VERSIONING = ON);  
```  
  
 이 예에서는 기존 기록 테이블에 연결 된 새 임시 테이블을 만듭니다.  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (SYSTEM_VERSIONING = ON   
        (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON )  
    );  
```  
  
### <a name="q-creating-a-system-versioned-memory-optimized-temporal-table"></a>17. 시스템 버전 메모리 액세스에 최적화 된 임시 테이블 만들기  
   
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.
  
 다음 예제에는 시스템 버전 메모리 액세스에 최적화 된 임시 테이블을 새 디스크 기반 기록 테이블에 연결을 만드는 방법을 보여 줍니다.  
  
 이 예제는 새 기록 테이블에 연결 된 새 임시 테이블을 만듭니다.  
  
```  
CREATE SCHEMA History  
GO  
CREATE TABLE dbo.Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH   
    (  
        MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,  
            SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )   
    );  
```  
  
 이 예에서는 기존 기록 테이블에 연결 된 새 임시 테이블을 만듭니다.  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (SYSTEM_VERSIONING = ON   
        (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON )  
    );  
```  
  
### <a name="r-creating-a-table-with-encrypted-columns"></a>18. 암호화 된 열이 있는 테이블 만들기  
 다음 예제에서는 두 개의 암호화 된 열이 있는 테이블을 만듭니다. 자세한 내용은 [상시 암호화&#40;데이터베이스 엔진#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요.  
  
```  
CREATE TABLE Customers (  
    CustName nvarchar(60)   
        ENCRYPTED WITH   
            (  
             COLUMN_ENCRYPTION_KEY = MyCEK,  
             ENCRYPTION_TYPE = RANDOMIZED,  
             ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
            ),   
    SSN varchar(11) COLLATE  Latin1_General_BIN2  
        ENCRYPTED WITH   
            (  
             COLUMN_ENCRYPTION_KEY = MyCEK,  
             ENCRYPTION_TYPE = DETERMINISTIC ,  
             ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
            ),   
    Age int NULL  
);  
```

### <a name="s-create-an-inline-filtered-index"></a>S.는 인라인 필터링 된 인덱스 만들기 
인라인 필터링 된 인덱스는 테이블을 만듭니다.
  
  ```
  CREATE TABLE t1 
 (
      c1 int,
      index IX1  (c1) WHERE c1 > 0   
 )
GO
 ```
 
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Columnproperty&#40; Transact SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DROP index&#40; Transact SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [DROP table&#40; Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helpconstraint &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpconstraint-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_spaceused&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
  
  



