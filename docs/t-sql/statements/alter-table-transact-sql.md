---
title: ALTER TABLE (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WAIT_AT_LOW_PRIORITY
- ABORT_AFTER_WAIT
- ABORT_AFTER_WAIT_TSQL
- ALTER_TABLE_TSQL
- ALTER TABLE
- WAIT_AT_LOW_PRIORITY_TSQL
- ALTER_COLUMN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- columns [SQL Server], resizing
- changing column size
- MAXDOP index option, ALTER TABLE statement
- table modifications [SQL Server], ALTER TABLE
- ALTER TABLE statement
- modifying tables
- partitioned tables [SQL Server], lock escalation
- resizing columns
- removing columns
- switching partitions
- reassigning partitions
- removing constraints
- triggers [SQL Server], disabling
- columns [SQL Server], adding
- LOCK_ESCALATION option of ALTER TABLE
- constraints [SQL Server], deleting
- constraints [SQL Server], disabling
- triggers [SQL Server], enabling
- re-enabling constraints
- index modifications [SQL Server]
- disabling constraints
- columns [SQL Server], removing
- max degree of parallelism option
- locking [SQL Server], tables
- ONLINE option
- disabling triggers
- constraints [SQL Server], adding
- deleting constraints
- adding constraints
- adding columns
- SWITCH partitions
- partitioned tables [SQL Server], switching
- lock escalation [SQL Server], option of ALTER TABLE
- constraints [SQL Server], enabling
- dropping constraints
- dropping columns
- table changes [SQL Server]
ms.assetid: f1745145-182d-4301-a334-18f799d361d1
caps.latest.revision: 281
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cee79406283aa3b75d41b968370f490cb454ea5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-transact-sql"></a>ALTER TABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  열과 제약 조건을 변경, 추가 또는 삭제하거나 파티션을 재할당하고 다시 작성하거나 제약 조건과 트리거를 설정 또는 해제하여 테이블 정의를 수정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name   
{   
    ALTER COLUMN column_name   
    {   
        [ type_schema_name. ] type_name   
            [ (   
                {   
                   precision [ , scale ]   
                 | max   
                 | xml_schema_collection   
                }   
            ) ]   
        [ COLLATE collation_name ]   
        [ NULL | NOT NULL ] [ SPARSE ]  
      | { ADD | DROP }   
          { ROWGUIDCOL | PERSISTED | NOT FOR REPLICATION | SPARSE | HIDDEN }  
      | { ADD | DROP } MASKED [ WITH ( FUNCTION = ' mask_function ') ]  
    }   
    [ WITH ( ONLINE = ON | OFF ) ]  
    | [ WITH { CHECK | NOCHECK } ]  
  
    | ADD   
    {   
        <column_definition>  
      | <computed_column_definition>  
      | <table_constraint>   
      | <column_set_definition>   
    } [ ,...n ]  
      | [ system_start_time_column_name datetime2 GENERATED ALWAYS AS ROW START   
                   [ HIDDEN ] [ NOT NULL ] [ CONSTRAINT constraint_name ] 
           DEFAULT constant_expression [WITH VALUES] ,  
            system_end_time_column_name datetime2 GENERATED ALWAYS AS ROW END   
                   [ HIDDEN ] [ NOT NULL ]  [ CONSTRAINT constraint_name ] 
           DEFAULT constant_expression [WITH VALUES] ,  
         ]  
       PERIOD FOR SYSTEM_TIME ( system_start_time_column_name, system_end_time_column_name )  
    | DROP   
     [ {  
         [ CONSTRAINT ]  [ IF EXISTS ]  
         {   
              constraint_name   
              [ WITH   
               ( <drop_clustered_constraint_option> [ ,...n ] )   
              ]   
          } [ ,...n ]  
          | COLUMN  [ IF EXISTS ]  
          {  
              column_name   
          } [ ,...n ]  
          | PERIOD FOR SYSTEM_TIME  
     } [ ,...n ]  
    | [ WITH { CHECK | NOCHECK } ] { CHECK | NOCHECK } CONSTRAINT   
        { ALL | constraint_name [ ,...n ] }   
  
    | { ENABLE | DISABLE } TRIGGER   
        { ALL | trigger_name [ ,...n ] }  
  
    | { ENABLE | DISABLE } CHANGE_TRACKING   
        [ WITH ( TRACK_COLUMNS_UPDATED = { ON | OFF } ) ]  
  
    | SWITCH [ PARTITION source_partition_number_expression ]  
        TO target_table   
        [ PARTITION target_partition_number_expression ]  
        [ WITH ( <low_lock_priority_wait> ) ]  
    | SET   
        (  
            [ FILESTREAM_ON =   
                { partition_scheme_name | filegroup | "default" | "NULL" } ]  
            | SYSTEM_VERSIONING =   
                  {   
                      OFF   
                  | ON   
                      [ ( HISTORY_TABLE = schema_name . history_table_name   
                          [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] 
                          [, HISTORY_RETENTION_PERIOD = 
                          { 
                               INFINITE | number {DAY | DAYS | WEEK | WEEKS 
                 | MONTH | MONTHS | YEAR | YEARS } 
                          } 
                          ]  
                        )  
                      ]  
                  }  
          )  
    | REBUILD   
      [ [PARTITION = ALL]  
        [ WITH ( <rebuild_option> [ ,...n ] ) ]   
      | [ PARTITION = partition_number   
           [ WITH ( <single_partition_rebuild_option> [ ,...n ] ) ]  
        ]  
      ]  
  
    | <table_option>  
  
    | <filetable_option>  
  
    | <stretch_configuration>  
  
}  
[ ; ]  
  
-- ALTER TABLE options  
  
<column_set_definition> ::=   
    column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
  
<drop_clustered_constraint_option> ::=    
    {   
        MAXDOP = max_degree_of_parallelism  
      | ONLINE = { ON | OFF }  
      | MOVE TO   
         { partition_scheme_name ( column_name ) | filegroup | "default" }  
    }  
<table_option> ::=  
    {  
        SET ( LOCK_ESCALATION = { AUTO | TABLE | DISABLE } )  
    }  
  
<filetable_option> ::=  
    {  
       [ { ENABLE | DISABLE } FILETABLE_NAMESPACE ]  
       [ SET ( FILETABLE_DIRECTORY = directory_name ) ]  
    }  
  
<stretch_configuration> ::=  
    {  
      SET (  
        REMOTE_DATA_ARCHIVE   
        {  
            = ON (  <table_stretch_options>  )  
          | = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED )  
          | ( <table_stretch_options> [, ...n] )  
        }  
            )  
    }  
  
<table_stretch_options> ::=  
    {  
     [ FILTER_PREDICATE = { null | table_predicate_function } , ]  
       MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }  
    }  
  
<single_partition_rebuild__option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ], 
        ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER TABLE [ database_name . [schema_name ] . | schema_name. ] source_table_name   
{  
    ALTER COLUMN column_name  
        {   
            type_name [ ( precision [ , scale ] ) ]   
            [ COLLATE Windows_collation_name ]   
            [ NULL | NOT NULL ]   
        }  
    | ADD { <column_definition> | <column_constraint> FOR column_name} [ ,...n ]  
    | DROP { COLUMN column_name | [CONSTRAINT] constraint_name } [ ,...n ]  
    | REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_option> ] ]
      } 
    | { SPLIT | MERGE } RANGE (boundary_value)  
    | SWITCH [ PARTITION source_partition_number  
        TO target_table_name [ PARTITION target_partition_number ]  
}  
[;]  
  
<column_definition>::=  
{  
    column_name  
    type_name [ ( precision [ , scale ] ) ]   
    [ <column_constraint> ]  
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ]  
}  
  
<column_constraint>::=  
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression  

<rebuild_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
```    

   
## <a name="arguments"></a>인수  
 *database_name*  
 테이블이 생성된 데이터베이스 이름입니다.  
  
 *schema_name*  
 테이블이 속한 스키마의 이름입니다.  
  
 *table_name*  
 변경할 테이블의 이름입니다. 테이블이 현재 데이터베이스에 없거나 현재 사용자가 소유한 스키마에 포함되지 않은 경우에는 데이터베이스와 스키마를 명시적으로 지정해야 합니다.  
  
 ALTER COLUMN  
 명명된 열을 변경하도록 지정합니다.  
  
 다음과 같은 열은 수정할 수 없습니다.  
  
-   지정 된 열을 **타임 스탬프** 데이터 형식입니다.  
  
-   테이블의 ROWGUIDCOL  
  
-   계산 열 또는 계산 열에 사용되는 열  
  
-   열이 하지 않으면 CREATE STATISTICS 문에 의해 생성 된 통계에 사용 되는 **varchar**, **nvarchar**, 또는 **varbinary** 데이터 형식, 데이터 형식이 변경 되지 않은, 및 새 크기가 원래 크기 보다 크거나 같은 경우 또는 열은 null을 null이 아닌에서 변경 합니다. 먼저 DROP STATISTICS 문을 사용하여 통계를 제거합니다. 쿼리 최적화 프로그램에 의해 자동으로 생성된 통계는 ALTER COLUMN에 의해 자동으로 삭제됩니다.  
  
-   PRIMARY KEY 또는 [FOREIGN KEY] REFERENCES 제약 조건에 사용된 열  
  
-   CHECK 또는 UNIQUE 제약 조건에 사용된 열. 그러나 CHECK 또는 UNIQUE 제약 조건에 사용된 가변 길이 열의 길이는 변경할 수 있습니다.  
  
-   DEFAULT 정의와 연결되는 열. 그러나 데이터 형식이 변경되지 않은 경우 열의 길이, 전체 자릿수 또는 소수 자릿수를 변경할 수 있습니다.  
  
데이터 형식이 **텍스트**, **ntext** 및 **이미지** 열은 다음과 같은 방식 으로만 변경할 수 있습니다.  
  
    -   **텍스트** 를 **varchar (max)**, **nvarchar (max)**, 또는 **xml**  
  
    -   **ntext** 를 **varchar (max)**, **nvarchar (max)**, 또는 **xml**  
  
    -   **이미지** 를 **varbinary (max)**  
  
데이터 형식을 변경하면 데이터 자체가 변경되는 경우도 있습니다. 예를 들어 변경는 **nchar** 또는 **nvarchar** 열을 **char** 또는 **varchar** 확장된 문자가 변환 될 수 있습니다. 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요. 열의 전체 자릿수 또는 소수 자릿수를 줄이면 데이터가 잘릴 수 있습니다.  
  
     The data type of a column of a partitioned table cannot be changed.  
  
 인덱스에 포함 된 열 데이터 형식의 열이 경우가 아니면 변경할 수 없습니다는 **varchar**, **nvarchar**, 또는 **varbinary** 데이터 형식이 고 같거나 더 큰 새 크기는 보다 이전 크기입니다.  
  
 기본 키 제약 조건에 포함 된 열은 변경할 수 없습니다 **NOT NULL** 를 **NULL**합니다.  
  
 수정 중인 열은 암호화 된 WITH를 사용 하 여 암호화 하는 경우 (예: INT BIGINT로) 호환 되는 데이터 형식으로 데이터 형식을 변경할 수 있습니다 하지만 한 암호화 설정을 변경할 수 없습니다.  
  
 *column_name*  
 변경, 추가 또는 삭제할 열의 이름입니다. *column_name* 최대 128 자가 될 수 있습니다. 새 열에 대 한 *column_name* 사용 하 여 만든 열에 대 한 생략 될 수 있습니다는 **타임 스탬프** 데이터 형식입니다. 이름 **타임 스탬프** 되지 않은 경우 사용 되는 *column_name* 에 대해 지정 된는 **타임 스탬프** 데이터 형식 열입니다.  
  
 [ *type_schema_name***합니다.** ] *type_name*  
 변경된 열의 새 데이터 형식 또는 추가된 열의 데이터 형식입니다. *type_name* 분할 된 테이블의 기존 열에 지정할 수 없습니다. *type_name* 다음 중 하나가 될 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 기반으로 하는 별칭 데이터 형식. 별칭 데이터 형식은 CREATE TYPE 문으로 만들어진 다음 테이블 정의에 사용됩니다.  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 사용자 정의 형식 및 이 형식이 속한 스키마. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 사용자 정의 형식은 CREATE TYPE 문으로 만들어진 다음 테이블 정의에서 사용됩니다.  
  
다음은에 대 한 조건을 *type_name* 변경 된 열의:  
  
-   이전 데이터 형식은 암시적으로 새 데이터 형식으로 변환 가능해야 합니다.  
  
-   *type_name* 안 **타임 스탬프**합니다.  
  
-   ALTER COLUMN에 대해 ANSI_NULL 기본값이 항상 설정되어 있습니다. 값을 지정하지 않으면 열에 Null이 허용됩니다.  
  
-   ALTER COLUMN에 대해 ANSI_PADDING 패딩이 항상 ON으로 설정되어 있습니다.  
  
-   수정 된 열이 id 열 *new_data_type* identity 속성을 지 원하는 데이터 형식 이어야 합니다.  
  
-   SET ARITHABORT의 현재 설정이 무시됩니다. ALTER TABLE은 ARITHABORT가 ON으로 설정된 것처럼 동작합니다.  
  
> [!NOTE]  
>  COLLATE 절을 지정하지 않으면 열의 데이터 형식을 변경했을 때 데이터 정렬이 데이터베이스의 기본 데이터 정렬로 변경됩니다.  
  
 *전체 자릿수*  
 지정된 데이터 형식의 전체 자릿수입니다. 유효한 전체 자릿수 값에 대 한 자세한 내용은 참조 [전체 자릿수, 소수 자릿수 및 길이 &#40; Transact SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 *소수 자릿수*  
 지정된 데이터 형식의 소수 자릿수입니다. 유효한 소수 자릿수 값에 대 한 자세한 내용은 참조 [전체 자릿수, 소수 자릿수 및 길이 &#40; Transact SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 **max**  
 에 적용 됩니다는 **varchar**, **nvarchar**, 및 **varbinary** 2를 저장 하기 위한 데이터 형식 ^31-1 바이트 문자, 이진 데이터 및 유니코드 데이터입니다.  
  
 *xml_schema_collection*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 에 적용 됩니다는 **xml** 형식과 XML 스키마를 연결 하기 위한 데이터 형식입니다. 입력 하기 전에 **xml** 스키마 컬렉션에 대 한 열에서 스키마 컬렉션 만들어야 데이터베이스에서 사용 하 여 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)합니다.  
  
COLLATE \< *데이터 정렬 이름* > 변경된 된 열에 대 한 새 데이터 정렬을 지정 합니다. 이를 지정하지 않으면 열에 데이터베이스의 기본 데이터 정렬이 할당됩니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 목록 및 자세한 정보에 대 한 참조 [Windows 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) 및 [SQL Server 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 열에 대해서만 되는 데이터 정렬을 변경 하려면 COLLATE 절을 사용할 수는 **char**, **varchar**, **nchar**, 및 **nvarchar** 데이터 형식입니다. 사용자 정의 별칭 데이터 형식 열의 데이터 정렬을 변경하려면 별도의 ALTER TABLE 문을 실행하여 열을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식으로 변경하고 해당 데이터 정렬을 변경한 다음 그 열을 별칭 데이터 형식으로 다시 변경해야 합니다.  
  
 다음 조건이 하나 이상 해당되는 경우 ALTER COLUMN으로 데이터 정렬을 변경할 수 없습니다.  
  
-   CHECK 제약 조건, FOREIGN KEY 제약 조건 또는 계산 열이 변경된 열을 참조하는 경우  
  
-   인덱스, 통계 또는 전체 텍스트 인덱스가 열에 생성된 경우. 변경된 열에 자동으로 만들어진 통계는 열 데이터 정렬이 변경되면 삭제됩니다.  
  
-   스키마 바운드 뷰 또는 함수가 열을 참조하는 경우  
  
 자세한 내용은 [COLLATE&#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)를 참조하세요.  
  
NULL | NOT NULL  
 열에 Null 값 허용 여부를 지정합니다. Null 값이 허용되지 않는 열은 기본값이 지정된 경우 또는 테이블이 비어 있는 경우에만 ALTER TABLE을 사용하여 추가할 수 있습니다. 계산 열에서는 PERSISTED를 지정한 경우에만 NOT NULL을 지정할 수 있습니다. 새 열이 Null 값을 허용하고 기본값이 지정되어 있지 않으면 테이블에서 각 행의 새 열은 Null 값을 포함합니다. 새 열이 Null 값을 허용하고 해당 열에 기본 정의가 추가되어 있으면 WITH VALUES를 사용하여 테이블에서 기존 행의 새 열에 기본값을 저장할 수 있습니다.  
  
 새 열이 Null 값을 허용하지 않고 테이블이 비어 있지 않은 경우에는 DEFAULT 정의가 새 열에 추가되어야 합니다. 그러면 각 기존 행의 새 열에 기본값이 자동으로 로드됩니다.  
  
 PRIMARY KEY 제약 조건이 있는 열을 제외하고 ALTER COLUMN에 NULL을 지정하여 NOT NULL 열이 Null 값을 허용하도록 강제 설정할 수 있습니다. 열에 Null 값이 포함되어 있지 않을 경우에만 ALTER COLUMN에 NOT NULL을 지정할 수 있습니다. ALTER COLUMN NOT NULL을 허용하려면 다음과 같이 Null 값을 다른 값으로 업데이트해야 합니다.  
  
```  
UPDATE MyTable SET NullCol = N'some_value' WHERE NullCol IS NULL;  
ALTER TABLE MyTable ALTER COLUMN NullCOl NVARCHAR(20) NOT NULL;  
```  
  
 CREATE TABLE 또는 ALTER TABLE 문을 사용하여 테이블을 만들거나 변경하는 경우 데이터베이스 및 세션 설정은 열 정의에 사용되는 데이터 형식의 Null 허용 여부에 영향을 주거나 이를 재정의할 가능성이 있습니다. 비계산 열은 항상 NULL 또는 NOT NULL로 명시적으로 정의하는 것이 좋습니다.  
  
 사용자 정의 데이터 형식이 있는 열을 추가할 경우에는 사용자 정의 데이터 형식과 같은 Null 허용 여부를 사용하여 열을 정의하고 열의 기본값을 지정하는 것이 좋습니다. 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
>  경우 NULL 또는 NOT ALTER COLUMN으로 NULL을 지정 *new_data_type* [(*정밀도* [, *배율* ])]도 지정 해야 합니다. 데이터 형식, 전체 자릿수 및 소수 자릿수가 변경되지 않으면 현재 열 값을 지정합니다.  
  
 [ {ADD | DROP} ROWGUIDCOL ]  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 지정된 열에 대해 ROWGUIDCOL 속성을 추가하거나 삭제하도록 지정합니다. ROWGUIDCOL은 열이 행 GUID 열임을 나타냅니다. 하나의 **uniqueidentifier** 테이블당 열 ROWGUIDCOL 열으로 지정할 수 있습니다 및 ROWGUIDCOL 속성에만 할당할 수 있는 한 **uniqueidentifier** 열입니다. ROWGUIDCOL은 사용자 정의 데이터 형식의 열에 지정할 수 없습니다.  
  
 ROWGUIDCOL은 열에 저장된 값이 고유하도록 설정하지 않으며 테이블에 삽입된 새 행의 값을 자동으로 생성하지 않습니다. 각 열에 대해 고유한 값을 생성하려면 INSERT 문에 NEWID 함수를 사용하거나 NEWID 함수를 열의 기본값으로 지정합니다.  
  
 [ {ADD | DROP} PERSISTED ]  
 지정된 열에 대해 PERSISTED 속성을 추가하거나 삭제하도록 지정합니다. 이 열은 결정적인 식으로 정의된 계산 열이어야 합니다. PERSISTED로 지정된 열인 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 계산된 값을 테이블에 저장하고 계산 열이 종속된 다른 열이 업데이트될 때 해당 값을 업데이트합니다. 계산 열을 PERSISTED로 표시하면 결정적이지만 정확하지는 않은 식에 정의된 계산 열에 인덱스를 만들 수 있습니다. 자세한 내용은 [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md)을 참조하세요.  
  
 분할된 테이블의 분할 열로 사용되는 계산 열은 명시적으로 PERSISTED로 표시해야 합니다.  
  
 DROP NOT FOR REPLICATION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 복제 에이전트가 삽입 작업을 수행할 때 ID 열의 값이 증가하도록 지정합니다. 경우에이 절을 지정할 수 *column_name* 은 id 열입니다.  
  
 SPARSE  
 열이 스파스 열임을 나타냅니다. 스파스 열의 저장소는 Null 값에 대해 최적화됩니다. 스파스 열은 NOT NULL로 지정할 수 없습니다. 스파스 열에서 스파스가 아닌 열로 또는 스파스가 아닌 열에서 스파스 열로 열을 변환하면 명령이 실행되는 동안 테이블이 잠깁니다. 공간을 절약하기 위해 REBUILD 절을 사용해야 할 수 있습니다. 추가 제한 사항 및 스파스 열에 대 한 자세한 내용은 참조 [스파스 열을 사용 하 여](../../relational-databases/tables/use-sparse-columns.md)합니다.  
  
 와 마스킹된 추가 (함수 = ' *mask_function* ')  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 동적 데이터 마스크를 지정합니다. *mask_function* 적절 한 매개 변수를 사용 하 여 마스킹 함수 이름입니다. 세 개의 함수를 사용할 수 있습니다.  
  
-   default)  
-   email()  
-   partial()  
-   random()  
  
 마스크를 삭제 하려면 사용 `DROP MASKED`합니다. 함수 매개 변수를 참조 하십시오. [동적 데이터 마스킹](../../relational-databases/security/dynamic-data-masking.md)합니다.  
  
와 (ONLINE = ON | OFF) \<열 변경에 적용 >  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 테이블을 사용 가능한 상태로 유지하면서 많은 열 변경 작업을 수행할 수 있게 해줍니다. 기본값은 OFF입니다. 열 변경은 데이터 형식, 열 길이 또는 전체 자릿수, Null 허용 여부, 스파스 및 데이터 정렬과 관련된 열 변경 내용에 대해 온라인으로 수행할 수 있습니다.  
  
 온라인 열 변경을 통해, 사용자가 만든 통계과 자동 통계가 ALTER COLUMN 작업 기간 동안 변경된 열을 참조할 수 있습니다. 따라서 평소와 같이 쿼리를 수행할 수 있습니다. 작업 종료 시 열을 참조하는 자동 통계는 삭제되고 사용자가 만든 통계는 무효화됩니다. 사용자는 작업이 완료된 후 사용자가 생성한 통계를 수동으로 업데이트해야 합니다. 열 통계 또는 인덱스에 대 한 필터 식의 일부인 경우 alter 열 동작을 수행할 수 없습니다.  
  
-   온라인 열 변경 작업이 실행되고 있는 동안 해당 열(인덱스, 뷰 등)에 대한 종속성을 사용할 수 있는 모든 작업은 차단되거나 적절한 오류가 발생하고 실패합니다. 따라서 작업이 실행되고 있는 동안 도입된 종속성으로 인해 온라인 열 변경이 실패하지 않습니다.  
  
-   변경된 열이 비클러스터형 인덱스에서 참조되는 경우 열을 NOT NULL에서 NULL로 변경하는 작업은 온라인 작업으로 지원되지 않습니다.  
  
-   열이 CHECK 제약 조건에서 참조되고 변경 작업이 열의 전체 자릿수(numeric 또는 datetime)를 제한하는 경우 온라인 변경은 지원되지 않습니다.  
  
-   **low_priority_lock_wait** 옵션을 사용할 수 없습니다 온라인 열 변경과 함께 합니다.  
  
-   열을 변경 하는 중... ADD/DROP PERSISTED에 지원 되지 않습니다 온라인 열 변경 합니다.  
  
-   열을 변경 하는 중... ADD/DROP ROWGUIDCOL/하지 복제 영향을 받지 않는 온라인에 대 한 열을 변경 합니다.  
  
-   온라인 열 변경은 변경 내용 추적이 설정되었거나 병합 복제의 게시자인 테이블 변경을 지원하지 않습니다.  
  
-   온라인 열 변경은 CLR 데이터 형식에서의 변경 또는 CLR 데이터 형식으로의 변경을 지원하지 않습니다.  
  
-   온라인 열 변경은 현재 스키마 컬렉션과 다른 스키마 컬렉션이 포함된 XML 데이터 형식으로의 변경을 지원하지 않습니다.  
  
-   온라인 열 변경에서는 열을 변경할 수 있는 경우에 대한 제한이 줄어들지 않습니다. 인덱스/통계 등에 의한 참조로 인해 alter가 실패할 수 있습니다.  
  
-   온라인 열 변경은 동시에 둘 이상의 열 변경을 지원하지 않습니다.  
  
-   온라인 열에 시스템 버전 임시 테이블의 경우 영향을 주지 않습니다. ONLINE 옵션에 지정된 값과 관계없이 열 변경은 온라인으로 수행되지 않습니다.  
  
온라인 열 변경의 요구 사항, 제한 및 기능은 온라인 인덱스 다시 작성과 유사합니다. 다음을 포함합니다.  
  
-   테이블에 레거시 LOB 또는 FILESTREAM 열이 포함되어 있거나 테이블에 columnstore 인덱스가 있는 경우 온라인 인덱스 다시 작성은 지원되지 않습니다. 동일한 제한이 온라인 열 변경에도 적용됩니다.  
  
-   기존 열을 변경하려면 원본 열과 새로 만들어진 숨겨진 열에 대한 공간 할당이 필요하므로 두 배의 공간 할당이 필요합니다.  
  
-   온라인 열 변경 작업 동안 잠금 전략은 온라인 인덱스 작성에 사용되는 것과 동일한 잠금 패턴을 따릅니다.  
  
WITH CHECK | WITH NOCHECK  
 새로 추가되거나 다시 설정된 FOREIGN KEY 또는 CHECK 제약 조건에 대해 테이블의 데이터 유효성을 검사할지 여부를 지정합니다. 값을 지정하지 않으면 새 제약 조건에는 WITH CHECK가 지정되고 다시 설정된 제약 조건에는 WITH NOCHECK가 지정된 것으로 간주됩니다.  
  
 기존 데이터에 대해 새 CHECK 또는 FOREIGN KEY 제약 조건을 확인하지 않으려면 WITH NOCHECK를 사용합니다. 이 방법은 꼭 필요한 경우가 아니면 사용하지 않는 것이 좋습니다. 새 제약 조건은 나중에 데이터가 업데이트될 때마다 평가됩니다. 따라서 제약 조건이 추가될 때 WITH NOCHECK에 의해 제약 조건 위반이 알려지지 않으면 제약 조건에 맞지 않는 데이터가 있는 행을 업데이트할 경우 업데이트 오류가 발생할 수 있습니다.  
  
 쿼리 최적화 프로그램은 WITH NOCHECK가 정의된 제약 조건을 고려하지 않습니다. 이러한 제약 조건은 ALTER TABLE `ALTER TABLE table WITH CHECK CHECK CONSTRAINT ALL`을 사용하여 다시 설정될 때까지 무시됩니다.  
  
 ADD  
 하나 이상의 열 정의 계산된 열 정의 또는 테이블 제약 조건 추가 된 지정 이나 시스템은 시스템 버전 관리에 사용 된 열입니다.  
  
 PERIOD FOR SYSTEM_TIME (system_start_time_column_name, system_end_time_column_name)  
 **적용 대상**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 시스템에서 사용 하는 레코드의 유효 기간을 기록 하는 열의 이름을 지정 합니다. 기존 열을 지정 하거나 ADD PERIOD FOR SYSTEM_TIME 인수의 일부로 새 열을 만들 수 있습니다. 열 데이터 형식이 datetime2 있어야 하며 NOT로 정의 되어야 합니다 NULL입니다. 기간 열이 NULL로 정의 된 경우 오류가 throw 됩니다. 정의할 수는 [column_constraint &#40; Transact SQL &#41; ](../../t-sql/statements/alter-table-column-constraint-transact-sql.md) 및/또는 [열에 대 한 기본 값 지정](../../relational-databases/tables/specify-default-values-for-columns.md) system_start_time 및 system_end_time 열에 대 한 합니다. 예제 A를 참조는 [시스템 버전 관리](#system_versioning) 아래의 system_end_time 열에 대 한 기본값 사용을 보여주는 예입니다.  
  
 SYSTEM_VERSIONING을 설정 인수와 함께에서이 인수를 사용 하 여 기존 테이블에 시스템 버전 관리를 활성화 합니다. 자세한 내용은 참조 [임시 테이블](../../relational-databases/tables/temporal-tables.md) 및 [Azure SQL 데이터베이스에서 임시 테이블 시작](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/)합니다.  
  
 일부로 [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)], 사용자가 하나 또는 둘 다 기간 열을 표시할 수는 **HIDDEN** 암시적으로 이러한 열 숨기기 위한 플래그를 되도록 **선택 \* FROM**  *\<테이블 >* 해당 열에 대 한 값을 반환 하지 않습니다. 기본적으로 기간 열 숨겨지지 않습니다. 를 사용 하려면 숨겨진된 열 임시 테이블을 직접 참조 하는 모든 쿼리에 명시적으로 포함 되어야 합니다.  
  
 DROP  
 하나 이상의 열 정의 계산된 열 정의 또는 테이블 제약 조건 삭제 될 지정 하거나 시스템에서 시스템 버전 관리에 사용 된 열 사양을 삭제 합니다.  
  
 제약 조건 *제약 조건 이름*  
 지정 하는 *constraint_name* 테이블에서 제거 합니다. 여러 제약 조건은 나열할 수 있습니다.  
  
 제약 조건의 사용자 정의 된 또는 시스템 제공 이름을 쿼리하여 확인할 수 있습니다는 **sys.check_constraint**, **sys.default_constraints**, **sys.key_constraints**, 및 **sys.foreign_keys** 카탈로그 뷰.  
  
 XML 인덱스가 테이블에 있는 경우 PRIMARY KEY 제약 조건을 삭제할 수 없습니다.  
  
 열 *column_name*  
 지정 하는 *constraint_name* 또는 *column_name* 테이블에서 제거 합니다. 여러 열을 나열할 수 있습니다.  
  
 다음과 같은 열은 삭제할 수 없습니다.  
  
-   인덱스에 사용된 열  
  
-   CHECK, FOREIGN KEY, UNIQUE 또는 PRIMARY KEY 제약 조건에 사용되는 열  
  
-   DEFAULT 키워드로 정의된 기본값과 연결되거나 기본 개체에 바인딩된 열  
  
-   규칙에 바인딩된 열  
  
> [!NOTE]  
>  열을 삭제해도 해당 열의 디스크 공간은 회수되지 않습니다. 테이블의 행 크기가 제한에 근접하거나 제한을 초과한 경우에는 삭제된 열의 디스크 공간을 회수해야 할 수도 있습니다. 테이블에 클러스터형된 인덱스를 만들거나 사용 하 여 기존 클러스터형된 인덱스를 다시 작성 하 여 공간을 회수 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)합니다. 이 참조의 LOB 데이터 형식의 삭제 영향에 대 한 정보를 [CSS 블로그 항목](http://blogs.msdn.com/b/psssql/archive/2012/12/03/how-it-works-gotcha-varchar-max-caused-my-queries-to-be-slower.aspx)합니다.  
  
 PERIOD FOR SYSTEM_TIME  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 시스템에서 시스템 버전 관리에 사용 된 열 사양을 삭제 합니다.  
  
 와 \<drop_clustered_constraint_option >  
 하나 이상의 클러스터형 제약 조건 삭제 옵션이 설정되도록 지정합니다.  
  
 MAXDOP = *max_degree_of_parallelism*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 재정의 **x degree of** 작업의 기간에 대 한 구성 옵션입니다. 자세한 내용은 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.  
  
 MAXDOP 옵션을 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한합니다. 최대값은 64개입니다.  
  
 *max_degree_of_parallelism* 다음 값 중 하나일 수 있습니다.  
  
 1.  
 병렬 계획이 생성되지 않습니다.  
  
 \>1  
 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 지정된 값으로 제한합니다.  
  
 0(기본값)  
 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]  
>  병렬 인덱스 작업은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. 자세한 내용은 참조 [버전 및 SQL Server 2016에 대 한 지원 되는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)합니다.  
  
 온라인  **=**  {ON | **OFF** } \<drop_clustered_constraint_option에 적용 >  
 인덱스 작업 중 쿼리 및 데이터 수정에 기본 테이블과 관련 인덱스를 사용할 수 있는지 여부를 지정합니다. 기본값은 OFF입니다. REBUILD 작업은 ONLINE 작업으로만 수행할 수 있습니다.  
  
 ON  
 인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 작업의 주 단계 중 내재된 공유(IS) 잠금만 원본 테이블에 유지됩니다. 따라서 기본 테이블과 인덱스를 계속 쿼리하거나 업데이트할 수 있습니다. 작업이 시작될 때 아주 짧은 기간 동안 S(공유) 잠금이 원본 개체에 유지됩니다. 작업이 끝날 때 짧은 기간 동안 비클러스터형 인덱스가 생성되는 경우에는 원본에 대해 공유(S) 잠금이 획득되고, 온라인 상태에서 클러스터형 인덱스가 생성 또는 삭제될 때와 클러스터형 또는 비클러스터형 인덱스가 다시 작성될 때는 스키마 수정(SCH-M) 잠금이 획득됩니다. 로컬 임시 테이블에서 인덱스를 생성하는 경우에는 ONLINE을 ON으로 설정할 수 없습니다. 단일 스레드 힙 다시 작성 작업만 허용됩니다.  
  
 에 대 한 DDL을 실행 하려면 **스위치** 또는 온라인 인덱스 다시 작성 된 모든 활성 차단 트랜잭션이 특정 테이블에서 실행을 완료 해야 합니다. 를 실행할 때의 **스위치** 있는지 또는 다시 작성 작업이 새 트랜잭션이 시작 되지 않도록 하 고 수는 작업 처리량에 큰 영향을 기본 테이블에 대 한 액세스를 일시적으로 지연 합니다.  
  
 OFF  
 인덱스 작업 중에 테이블 잠금이 적용됩니다. 클러스터형 인덱스를 생성, 다시 작성 또는 삭제하거나 비클러스터형 인덱스를 다시 작성 또는 삭제하는 오프라인 인덱스 작업을 통해 테이블의 SCH-M(스키마 수정) 잠금을 획득합니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다. 비클러스터형 인덱스를 만드는 오프라인 인덱스 작업을 통해 테이블의 S(공유) 잠금을 획득합니다. 따라서 기본 테이블을 업데이트할 수 없지만 SELECT 문과 같은 읽기 작업은 허용됩니다. 다중 스레드 힙 다시 작성 작업이 허용됩니다.  
  
 자세한 내용은 참조 [어떻게 온라인 인덱스 작동](../../relational-databases/indexes/how-online-index-operations-work.md)합니다.  
  
> [!NOTE]  
>  온라인 인덱스 작업은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. 자세한 내용은 참조 [버전 및 SQL Server 2016에 대 한 지원 되는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)합니다.  
  
 MOVE TO { *partition_scheme_name***(***column_name* [1**,** ...  *n* ] **)** | *파일 그룹* | **"**기본**"**  }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 현재 클러스터형 인덱스의 리프 수준에 있는 데이터 행을 이동할 위치를 지정합니다. 테이블이 새 위치로 이동됩니다. 이 옵션은 클러스터형 인덱스를 만드는 제약 조건에만 적용됩니다.  
  
> [!NOTE]  
>  이 컨텍스트에서 default는 키워드가 아니라 기본 파일 그룹에 대 한 식별자 이며 MOVE TO 같이 구분 되어야 합니다 **"**기본**"** 또는 MOVE TO **[**기본**]**합니다. 경우 **"**기본**"** 지정, QUOTED_IDENTIFIER 옵션은 현재 세션에 대 한 ON 이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
 { CHECK | NOCHECK } CONSTRAINT  
 지정 하는 *constraint_name* 활성화 하거나 비활성화 합니다. 이 옵션은 FOREIGN KEY 및 CHECK 제약 조건에만 사용할 수 있습니다. NOCHECK를 지정하면 제약 조건이 해제되고 향후 해당 열에 삽입하거나 해당 열을 업데이트할 때 제약 조건에 대한 유효성 검사가 수행되지 않습니다. DEFAULT, PRIMARY KEY 및 UNIQUE 제약 조건은 해제할 수 없습니다.  
  
 ALL  
 NOCHECK 옵션을 사용하여 모든 제약 조건을 해제하거나 CHECK 옵션을 사용하여 모든 제약 조건을 설정하도록 지정합니다.  
  
 { ENABLE | DISABLE } TRIGGER  
 지정 하는 *trigger_name* 활성화 하거나 비활성화 합니다. 트리거를 해제해도 테이블에는 계속 정의되어 있습니다. 그러나 테이블에 대해 INSERT, UPDATE 또는 DELETE 문이 실행되면 트리거가 다시 설정될 때까지 트리거의 동작이 수행되지 않습니다.  
  
 ALL  
 테이블의 모든 트리거를 설정하거나 해제하도록 지정합니다.  
  
 *trigger_name*  
 설정하거나 해제할 트리거의 이름을 지정합니다.  
  
 { ENABLE | DISABLE } CHANGE_TRACKING  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 테이블에 대해 변경 내용 추적이 설정되는지 여부를 지정합니다. 기본적으로 변경 내용 추적은 비활성화됩니다.  
  
 이 옵션은 데이터베이스에 대해 변경 내용 추적이 설정된 경우에만 사용할 수 있습니다. 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
 변경 내용 추적을 설정하려면 테이블에 기본 키가 있어야 합니다.  
  
 와 **(** TRACK_COLUMNS_UPDATED  **=**  {ON | **OFF** } **)**  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 업데이트된 변경 내용 추적 열을 추적하는지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 스위치 [파티션 *source_partition_number_expression* ] TO [ *schema_name***합니다.** ] *target_table* [파티션 *target_partition_number_expression* ]  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 다음 방법 중 하나를 사용하여 데이터 블록을 전환합니다.  
  
-   테이블의 모든 데이터를 기존의 분할된 테이블에 파티션으로 재할당합니다.  
  
-   분할된 테이블 간에 파티션을 전환합니다.  
  
-   분할된 테이블의 한 파티션에 있는 모든 데이터를 기존의 분할되지 않은 테이블에 재할당합니다.  
  
경우 *테이블* 분할된 된 테이블은 *source_partition_number_expression* 지정 해야 합니다. 경우 *target_table* 분할 되어 *target_partition_number_expression* 지정 해야 합니다. 테이블의 데이터를 기존의 분할된 테이블에 파티션으로 재할당하거나 분할된 한 테이블의 파티션을 다른 테이블로 전환하는 경우에는 비어 있는 대상 파티션이 있어야 합니다.  
  
 한 파티션의 데이터를 재할당하여 단일 테이블을 구성하는 경우 비어 있는 대상 테이블이 미리 만들어져 있어야 합니다. 원본 테이블 또는 파티션과 대상 테이블 또는 파티션이 모두 같은 파일 그룹에 있어야 합니다. 해당하는 인덱스 또는 인덱스 파티션도 같은 파일 그룹에 있어야 합니다. 파티션 전환에는 여러 가지 추가 제한 사항이 적용됩니다. *테이블* 및 *target_table* 같을 수 없습니다. *target_table* 다중 부분 식별자가 될 수 있습니다.  
  
 *source_partition_number_expression* 및 *target_partition_number_expression* 는 변수 및 함수를 참조할 수 있는 상수 식입니다. 이러한 식은 사용자 정의 형식 변수와 사용자 정의 함수를 포함하며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식을 참조할 수 없습니다.  
  
 클러스터 된 columstore 인덱스가 있는 분할 된 테이블 분할된 된 힙에서 처럼 동작 합니다.  
  
-   기본 키는 파티션 키를 포함 해야 합니다.  
  
-   고유 인덱스는 파티션 키를 포함 해야 합니다.  참고 고유 인덱스를 파티션 키를 포함 하 여 고유성을 변경할 수 있습니다.  
  
-   파티션을 전환 하기 위해 모든 비클러스터형 인덱스는 파티션 키를 포함 해야 합니다.  
  
에 대 한 **스위치** 제한 복제를 사용 하는 경우 참조 [복제 Partitioned Tables and Indexes](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)합니다.  
  
 비클러스터형 columnstore 인덱스에 대해 작성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CTP1, 2016 및 SQL 데이터베이스의 읽기 전용으로 버전 V12 되기 전에 합니다. 비클러스터형 columnstore 인덱스는 파티션 작업을 수행 하려면 (이 업데이트할 수 있는) 현재 형식으로 빌드해야 합니다.  
  
 설정 **(** FILESTREAM_ON = { *partition_scheme_name* | *filestream_filegroup_name* |         **"** 기본**"** | **"**NULL**"** }**)**  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. |  
  
 FILESTREAM 데이터가 저장되는 위치를 지정합니다.  
  
 SET FILESTREAM_ON 절이 있는 ALTER TABLE은 테이블에 FILESTREAM 열이 없는 경우에만 성공합니다. FILESTREAM 열은 두 번째 ALTER TABLE 문을 사용하여 추가할 수 있습니다.  
  
 경우 *partition_scheme_name* 지정에 대 한 규칙 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 적용 합니다. 테이블은 이미 행 데이터를 위해 분할되어 있어야 하며 테이블의 파티션 구성표는 FILESTREAM 파티션 구성표와 동일한 파티션 함수 및 열을 사용해야 합니다.  
  
 *filestream_filegroup_name* FILESTREAM 파일 그룹의 이름을 지정 합니다. 파일 그룹 사용 하 여 하나의 정의 된 파일을 파일 그룹에 대 한 있어야는 [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) 또는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문 또는 오류가 발생 합니다.  
  
 **"**기본**"** 기본 속성이 설정 된 FILESTREAM 파일 그룹을 지정 합니다. FILESTREAM 파일 그룹이 없으면 오류가 발생합니다.  
  
 **"**NULL**"** 테이블에 대 한 FILESTREAM 파일 그룹에 대 한 모든 참조는 제거 하도록 지정 합니다. All FILESTREAM 열을 먼저 삭제해야 합니다. SET FILESTREAM_ON을 사용 해야**= "**NULL**"** 테이블와 연결 된 모든 FILESTREAM 데이터를 삭제 하려면.  
  
 설정 **(** SYSTEM_VERSIONING  **=**  {OFF | ON [(HISTORY_TABLE schema_name = 합니다. history_table_name [, DATA_CONSISTENCY_CHECK = { **ON** | OFF}])]을 (를) **)**  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 테이블의 시스템 버전 관리를 사용 하지 않도록 설정 하거나 테이블의 시스템 버전 관리를 사용 하도록 설정 하십시오. 테이블의 시스템 버전 관리를 사용 하려면 시스템 데이터 형식, null 허용 제약 조건 및 시스템 버전 관리에 대 한 기본 키 제약 조건 요구 사항을 충족 하는지 확인 합니다. HISTORY_TABLE 인수를 사용 하지 않으면 시스템 일치 하는 두 테이블 간에 링크를 만들 현재 테이블의 스키마를 사용 하는 새 기록 테이블을 생성 하 고 기록 테이블에서 현재 테이블의 각 레코드의 변경 내용을 기록로 인해 시스템. 이 기록 테이블의 이름은 됩니다 `MSSQL_TemporalHistoryFor<primary_table_object_id>`합니다. 에 대 한 링크를 만들고 기존 기록 테이블을 사용 하 여 HISTORY_TABLE 인수를 사용 하는 경우 현재 테이블과 지정된 된 테이블 간에 링크가 만들어집니다. 기존 기록 테이블에 대한 링크를 만드는 경우 데이터 일관성 검사를 수행하도록 선택할 수 있습니다. 이 데이터 일관성 검사는 기존 레코드가 겹치지 않고 확인 합니다. 기본값은 데이터 일관성 검사를 수행하는 것입니다. 자세한 내용은 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)을 참조하세요.  
  
HISTORY_RETENTION_PERIOD = { **무한** | 번호 {일 | 일 | 주 |  주 | 월 | 월 | 연도 | 년}} **적용할**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  

임시 테이블의 기록 데이터에 대 한 유한 또는 infinte 보존을 지정합니다. 생략 하면 무한 보존 가정 합니다.
  
 설정 **(** LOCK_ESCALATION = {AUTO | 테이블 | (를) 사용 안 함 **)**  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 테이블에 대해 허용되는 잠금 에스컬레이션 방법을 지정합니다.  
  
 AUTO  
 이 옵션을 선택하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 테이블 스키마에 적절한 잠금 에스컬레이션 세분성을 선택할 수 있습니다.  
  
-   테이블이 분할되지 않은 경우에는 잠금이 파티션으로 에스컬레이션됩니다. 잠금이 파티션 수준으로 에스컬레이션된 후에는 나중에 잠금이 TABLE 세분성으로 에스컬레이션되지 않습니다.  
  
-   테이블이 분할되지 않은 경우에는 잠금이 TABLE 세분성으로 에스컬레이션됩니다.  
  
TABLE  
 잠금 에스컬레이션은 테이블이 분할되었는지 여부에 관계없이 테이블 수준 세분성으로 수행됩니다. 기본값은 TABLE입니다.  
  
 DISABLE  
 대부분의 경우 잠금 에스컬레이션이 허용되지 않습니다. 테이블 수준 잠금은 부분적으로 허용됩니다. 예를 들어 직렬화 가능 격리 수준에서 클러스터형 인덱스가 없는 테이블을 검색하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 테이블 잠금을 사용하여 데이터 무결성을 보호해야 합니다.  
  
 REBUILD  
 REBUILD WITH 구문을 사용하여 분할된 테이블의 파티션을 포함한 전체 테이블을 다시 작성할 수 있습니다. 테이블에 클러스터형 인덱스가 포함된 경우 REBUILD 옵션을 사용하면 클러스터형 인덱스가 다시 작성됩니다. REBUILD 작업은 ONLINE 작업으로만 수행할 수 있습니다.  
  
 REBUILD PARTITION 구문을 사용하여 분할된 테이블의 단일 파티션을 다시 작성할 수 있습니다.  
  
 PARTITION = ALL  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 파티션 압축 설정을 변경할 때 모든 파티션을 다시 작성합니다.  
  
 REBUILD WITH ( \<rebuild_option >)  
 모든 옵션이 클러스터형 인덱스가 있는 테이블에 적용됩니다. 테이블에 클러스터형 인덱스가 없는 경우에는 일부 옵션만 힙 구조에 영향을 줍니다.  
  
 REBUILD 작업에 특정 압축 설정이 지정되어 있지 않으면 파티션의 현재 압축 설정이 사용됩니다. 현재 설정으로 되돌리려면 쿼리는 **data_compression** 열에는 **sys.partitions** 카탈로그 뷰에 있습니다.  
  
 에 대 한 전체 설명은 rebuild 옵션을 참조 하십시오. [index_option &#40; Transact SQL &#41; ](../../t-sql/statements/alter-table-index-option-transact-sql.md).  
  
 DATA_COMPRESSION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.  
  
 없음  
 테이블 또는 지정된 파티션이 압축되지 않습니다. columnstore 테이블에는 적용되지 않습니다.  
  
 ROW  
 테이블 또는 지정된 파티션이 행 압축을 사용하여 압축됩니다. columnstore 테이블에는 적용되지 않습니다.  
  
 PAGE  
 테이블 또는 지정된 파티션이 페이지 압축을 사용하여 압축됩니다. columnstore 테이블에는 적용되지 않습니다.  
  
 COLUMNSTORE  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 columnstore 테이블에만 적용됩니다. COLUMNSTORE에서는 COLUMNSTORE_ARCHIVE 옵션으로 압축된 파티션을 압축 해제하도록 지정합니다. 데이터는 복구될 때 모든 columnstore 테이블에 사용된 columnstore 압축으로 계속 압축됩니다.  
  
 COLUMNSTORE_ARCHIVE  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 클러스터형 columnstore 인덱스로 저장된 테이블인 columnstore 테이블에만 적용됩니다. COLUMNSTORE_ARCHIVE는 지정된 파티션을 보다 작은 크기로 압축합니다. 보관하거나 보다 적은 저장소가 필요한 기타 상황에서 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
 동시에 여러 파티션을 다시 작성 하려면 참조 [index_option &#40; Transact SQL &#41; ](../../t-sql/statements/alter-table-index-option-transact-sql.md). 테이블에 클러스터형 인덱스가 없는 경우 데이터 압축을 변경하면 힙과 비클러스터형 인덱스가 다시 작성됩니다. 압축에 대 한 자세한 내용은 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
 온라인  **=**  {ON | **OFF** } \<single_partition_rebuild_option에 적용 >  
 인덱스 작업 중 쿼리 및 데이터 수정을 위해 기본 테이블의 단일 파티션 및 관련된 인덱스를 사용할 수 있는지 여부를 지정합니다. 기본값은 OFF입니다. REBUILD 작업은 ONLINE 작업으로만 수행할 수 있습니다.  
  
 ON  
 인덱스 작업 중에 장기 테이블 잠금이 유지되지 않습니다. 인덱스 다시 작성을 시작할 때 테이블에 대한 S-잠금이 필요하고 온라인 인덱스 다시 작성을 종료할 때 테이블에 대한 Sch-M 잠금이 필요합니다. 두 잠금 모두 짧은 메타데이터 잠금이지만 특히 Sch-M 잠금은 모든 차단 트랜잭션이 완료될 때까지 기다려야 합니다. 대기 시간 동안 Sch-M 잠금은 동일 테이블에 액세스할 때 이 잠금 뒤에서 기다리는 다른 모든 트랜잭션을 차단합니다.  
  
> [!NOTE]  
>  온라인 인덱스 다시 작성을 설정할 수는 *low_priority_lock_wait* 이 단원의 뒷부분에서 설명 하는 옵션입니다.  
  
 OFF  
 인덱스 작업 중에 테이블 잠금이 적용됩니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다.  
  
 *column_set_name* ALL_SPARSE_COLUMNS에 대 한 XML COLUMN_SET  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 열 집합의 이름입니다. 열 집합은 구조화된 출력으로 테이블의 모든 스파스 열을 결합하는 형식화되지 않은 XML 표현입니다. 스파스 열을 포함하는 테이블에는 열 집합을 추가할 수 없습니다. 열 집합에 대한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.  
  
 { ENABLE | DISABLE } FILETABLE_NAMESPACE  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 FileTable에 대한 시스템 정의 제약 조건을 사용하거나 사용하지 않도록 설정합니다. FileTable에서만 사용할 수 있습니다.  
  
 설정 (FILETABLE_DIRECTORY = *directory_name* )  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 Windows 호환 FileTable 디렉터리 이름을 지정합니다. 이 이름은 데이터베이스의 모든 FileTable 디렉터리 이름 중에서 고유해야 합니다. 고유성을 비교할 때는 SQL 데이터 정렬 설정과 관계없이 대/소문자가 구분되지 않습니다. FileTable에서만 사용할 수 있습니다.  
```    
 SET (  
        REMOTE_DATA_ARCHIVE   
        {  
            = ON (  <table_stretch_options> )  
          | = OFF_WITHOUT_DATA_RECOVERY  
          ( MIGRATION_STATE = PAUSED ) | ( <table_stretch_options> [, ...n] )  
        } )  
```    
**적용 대상**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 사용 하거나 테이블에 대 한 스트레치 데이터베이스를 사용 하지 않도록 설정 합니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
 **테이블에 대 한 스트레치 데이터베이스를 활성화합니다.**  
  
 지정 하 여 테이블에 대 한 확대를 사용 하는 경우 `ON`를 지정 해야 `MIGRATION_STATE = OUTBOUND` 시작 하려면 즉시 데이터 마이그레이션 또는 `MIGRATION_STATE = PAUSED` 데이터 마이그레이션을 연기 하 합니다. 기본값은 `MIGRATION_STATE = OUTBOUND`합니다. 테이블에 스트레치를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)합니다.  
  
 **필수 구성 요소**. 테이블에 대해 스트레치를 사용 하기 전에 서버에서를 데이터베이스에서 스트레치를 사용 하도록 설정 해야 합니다. 자세한 내용은 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)를 참조하십시오.  
  
 **사용 권한**. 데이터베이스 또는 테이블에 스트레치를 사용 하려면 db_owner 권한이 필요 합니다. 테이블에 대해 스트레치를 사용 하도록 설정 하면 테이블에 대 한 ALTER 권한이 있어야 합니다.  
  
 **테이블에 대 한 스트레치 데이터베이스 비활성화**  
  
 테이블에 대해 스트레치를 비활성화 하면 Azure로 이미 마이그레이션된 원격 데이터에 대 한 두 가지 옵션이 있습니다. 자세한 내용은 [Stretch Database 비활성화 및 원격 데이터 다시 가져오기](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)를 사용하세요.  
  
-   테이블에서 스트레치를 비활성화하고 Azure에서 SQL Server로 테이블에 대한 원격 데이터를 다시 복사하려면 다음 명령을 실행합니다. 이 명령은 취소할 수 없습니다.  
  
    ```tsql  
ALTER TABLE \<table name>
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;  
    ```  
  
     이 작업으로 인해 데이터 전송 비용이 발생하며 이 작업은 취소할 수 없습니다. 자세한 내용은 [데이터 전송 가격 정보](https://azure.microsoft.com/en-us/pricing/details/data-transfers/)를 참조하십시오.  
  
     Azure에서 SQL Server로 모든 원격 데이터를 다시 복사한 후 테이블에서 스트레치가 비활성화됩니다.  
  
-   테이블에서 스트레치를 비활성화하고 원격 데이터를 중지하려면 다음 명령을 실행합니다.  
  
    ```tsql  
ALTER TABLE \<table_name>
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ;  
    ```  
  
 테이블에서 스트레치 데이터베이스를 비활성화하면 데이터 마이그레이션이 중단되고 쿼리 결과에 원격 테이블의 결과가 더 이상 포함되지 않습니다.  
  
 스트레치를 비활성화 하면 원격 테이블을 제거 되지 않습니다. 원격 테이블을 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다.  
  
[FILTER_PREDICATE = {null | *조건자* }]  
 **적용 대상**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 필요에 따라 기록 및 현재 데이터가 포함 된 테이블에서 마이그레이션할 행을 선택 하는 필터 조건자를 지정 합니다. 조건자는 결정적 인라인 테이블 반환 함수를 호출 해야 합니다. 자세한 내용은 참조 하십시오. [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 및 [필터 함수 &#40;를 사용 하 여 마이그레이션할 행을 선택 합니다. 스트레치 데이터베이스 &#41; ](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).   
  
> [!IMPORTANT]  
>  제대로 수행되지 않는 필터 조건자를 제공하면 데이터 마이그레이션 성능도 저하됩니다. 스트레치 데이터베이스는 CROSS APPLY 연산자를 사용하여 테이블에 필터 조건자를 적용합니다.  
  
 필터 조건자를 지정하지 않으면 전체 테이블이 마이그레이션됩니다.  
  
 도 지정 해야 필터 조건자를 지정 하면 *MIGRATION_STATE*합니다.  
  
 MIGRATION_STATE = {아웃 바운드 |  인바운드 | (를) 일시 중지  
 **적용 대상**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   지정 `OUTBOUND` SQL Server에서 데이터를 Azure로 합니다.  
  
-   지정 `INBOUND` 원격 복사 하려면 Azure에서 테이블에 대 한 데이터 테이블에 대해 스트레치를 비활성화 하 고 SQL server를 다시 합니다. 자세한 내용은 [Stretch Database 비활성화 및 원격 데이터 다시 가져오기](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)를 사용하세요.  
  
     이 작업으로 인해 데이터 전송 비용이 발생하며 이 작업은 취소할 수 없습니다.  
  
-   지정 `PAUSED` 을 일시 중지 또는 데이터 마이그레이션을 연기 합니다. 자세한 내용은 참조 하십시오. [일시 중지 및 데이터 마이그레이션 다시 시작 &#40; 스트레치 데이터베이스 &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
WAIT_AT_LOW_PRIORITY  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 온라인 인덱스 다시 작성에서 이 테이블의 차단 작업을 대기해야 합니다. **WAIT_AT_LOW_PRIORITY** 온라인 인덱스 다시 작성 작업은 다른 작업을 온라인 인덱스 작성 작업을 대기 하는 동안 진행할 수 있도록 하는 낮은 우선 순위 잠금을 대기 함을 나타냅니다. 생략 된 **WAIT AT LOW PRIORITY** 옵션은 WA`IT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`합니다.  
  
 MAX_DURATION = *시간* [**분** ]  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 대기 시간 (분 단위로 지정 된 정수 값) 하는 **스위치** 또는 DDL 명령을 실행할 때 온라인 인덱스 다시 작성 잠금이 낮은 우선 순위로 대기 합니다. 작업에 대 한 차단 된 경우는 **MAX_DURATION** 시간 중 하나는 **ABORT_AFTER_WAIT** 작업 실행 됩니다. **MAX_DURATION** 시간은 항상 분 단위 이며 단어 **분** 생략할 수 있습니다.  
  
 ABORT_AFTER_WAIT = [**NONE** | **자체** | **블로 커가** }]  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 없음  
 보통(일반) 우선 순위로 잠금을 계속 대기합니다.  
  
 SELF  
 종료는 **스위치** 또는 작업을 수행 하지 않고 현재 실행 중인 온라인 인덱스 다시 작성 DDL 작업 합니다.  
  
 BLOCKERS  
 현재 차단 하는 모든 사용자 트랜잭션을 종료는 **스위치** 또는 온라인 인덱스 다시 작성 DDL 작업의 작업을 계속할 수 있도록 합니다.  
  
 필요한 **ALTER ANY CONNECTION** 권한.  
  
경우에 존재  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 열 또는 제약 조건이 이미 있는 경우에 조건에 따라 삭제 합니다.  
  
## <a name="remarks"></a>주의  
 새 데이터 행을 추가 하려면 사용 [삽입](../../t-sql/statements/insert-transact-sql.md)합니다. 데이터 행을 제거 하려면 [삭제](../../t-sql/statements/delete-transact-sql.md) 또는 [TRUNCATE TABLE](../../t-sql/statements/truncate-table-transact-sql.md)합니다. 기존 행의 값을 변경 하려면 사용 [업데이트](../../t-sql/queries/update-transact-sql.md)합니다.  
  
 프로시저 캐시에 테이블을 참조하는 실행 계획이 있는 경우 ALTER TABLE은 다음에 실행할 때 이러한 실행 계획을 다시 컴파일하도록 표시합니다.  
  
## <a name="changing-the-size-of-a-column"></a>열 크기 변경  
 ALTER COLUMN 절에 열 데이터 형식의 새 크기를 지정하여 열의 길이, 전체 자릿수 또는 소수 자릿수를 변경할 수 있습니다. 열에 데이터가 있는 경우 새 크기는 데이터의 최대 크기보다 작을 수 없습니다. 또한 열에서에서 정의할 수 없습니다, 인덱스 열이 경우가 아니면는 **varchar**, **nvarchar**, 또는 **varbinary** 데이터 형식 및 인덱스는 기본 키의 결과가 아닙니다 제약 조건입니다. 예 16을 참조하세요.  
  
## <a name="locks-and-alter-table"></a>잠금 및 ALTER TABLE  
 ALTER TABLE에 지정된 변경 내용은 즉시 구현됩니다. 변경할 때 테이블의 행을 수정해야 하는 경우 ALTER TABLE은 행을 업데이트합니다. ALTER TABLE은 테이블에 대한 스키마 수정 SCH-M 잠금을 획득하여 변경 중에 다른 연결이 테이블의 메타데이터도 참조하지 않도록 합니다. 단, 마지막에 아주 짧은 SCH-M 잠금이 필요한 온라인 인덱스 작업은 예외입니다. ALTER TABLE…SWITCH 작업에서 원본 및 대상 테이블 모두에 대해 잠금이 획득됩니다. 테이블의 수정 사항이 기록되며 완전히 복구 가능합니다. 열 삭제 또는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 경우 기본값이 있는 NOT NULL 열 추가와 같이 매우 큰 테이블의 모든 행에 영향을 주는 변경 작업은 완료하는 데 시간이 오래 걸리고 많은 로그 레코드를 생성할 수 있습니다. 이러한 ALTER TABLE 문은 많은 행에 영향을 주는 INSERT, UPDATE 또는 DELETE 문과 마찬가지로 주의해서 실행해야 합니다.  
  
### <a name="adding-not-null-columns-as-an-online-operation"></a>온라인 작업으로 NOT NULL 열 추가  
 부터는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 기본 값이 기본값은 NOT NULL 열은 온라인 작업을 추가 하는 Enterprise Edition을 *런타임 상수*합니다. 이는 테이블의 행 수에 관계없이 작업이 거의 즉시 완료된다는 의미입니다. 작업 중에 테이블의 기존 행은 업데이트되지 않고 대신 기본값이 테이블의 메타데이터에만 저장되고 이러한 행에 액세스하는 쿼리에 필요한 경우 해당 값이 조회되기 때문입니다. 이 동작은 자동이므로 온라인 작업을 구현하는 데 ADD COLUMN 구문 이상의 추가 구문이 필요하지 않습니다. 런타임 상수는 테이블의 각 행에 대해 해당 결정성과 관계없이 런타임에 동일한 값을 생성하는 식입니다. 예를 들어 상수 식 "My temporary data" 또는 시스템 함수 GETUTCDATETIME()은 런타임 상수입니다. 이와 달리 NEWID() 또는 NEWSEQUENTIALID()는 테이블의 각 행에 대해 고유 값이 생성되므로 런타임 상수가 아닙니다. 기본값이 포함된 런타임 상수가 아닌 NOT NULL 열을 추가하는 작업은 항상 오프라인으로 수행되며 작업 기간에 배타적 SCH-M 잠금이 획득됩니다.  
  
 기존 행은 메타데이터에 저장된 값을 참조하는 반면, 기본값은 새로 삽입되는 행에 대한 새 행에 저장되고 열에 대한 다른 값을 지정하지 않습니다. 메타데이터에 저장된 기본값은 행이 업데이트될 때(UPDATE 문에 실제 행이 지정되어 있지 않는 경우에도 동일) 또는 테이블이나 클러스터형 인덱스를 다시 작성하는 경우 기존 행으로 이동됩니다.  
  
 형식의 열 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **텍스트**, **ntext**, **이미지**, **hierarchyid**, **geometry**, **geography**, 또는 CLR UDT 수 없습니다. 온라인 작업에 추가할 수 있습니다. 열을 온라인으로 추가할 수 없으며, 온라인으로 추가하면 최대로 가능한 행 크기가 8,060바이트 제한을 초과합니다. 이러한 경우 열은 오프라인 작업으로 추가됩니다.  
  
## <a name="parallel-plan-execution"></a>병렬 계획 실행  
 [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] 프로세서의 수를 단일 ALTER TABLE ADD (인덱스 기반)를 실행 하는 데 사용 되는 이상 및 CONSTRAINT 또는 DROP (클러스터형된 인덱스) CONSTRAINT 문을 의해 결정 됩니다는 **x degree of** 구성 옵션 및 현재 작업 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 시스템에서 진행 중인 작업이 많음을 감지하면 작업의 병렬 처리 수준은 문 실행 시작 전에 자동으로 감소됩니다. MAXDOP 옵션을 지정하여 문을 실행하는 데 사용되는 프로세서 수를 수동으로 구성할 수 있습니다. 자세한 내용은 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.  
  
## <a name="partitioned-tables"></a>분할된 테이블  
 ALTER TABLE을 사용하면 분할된 테이블과 관련된 SWITCH 작업을 수행할 수 있을 뿐만 아니라 분할된 테이블의 열, 제약 조건 및 트리거의 상태를 분할되지 않은 테이블에 사용되는 것처럼 변경할 수 있습니다. 그러나 이 문을 사용하여 테이블 자체가 분할되는 방식을 변경할 수는 없습니다. 분할된 된 테이블 다시 분할을 사용 하 여 [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md) 및 [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md)합니다. 또한 분할된 테이블의 열 데이터 형식을 변경할 수 없습니다.  
  
## <a name="restrictions-on-tables-with-schema-bound-views"></a>스키마 바운드 뷰가 있는 테이블의 제한 사항  
 스키마 바운드 뷰가 있는 테이블에서 ALTER TABLE 문에 적용되는 제한은 단순 인덱스가 있는 테이블을 수정할 때 현재 적용되는 제한과 같습니다. 즉, 열을 추가할 수는 있지만 스키마 바운드 뷰에 포함된 열을 제거하거나 변경하는 것은 허용되지 않습니다. ALTER TABLE 문으로 스키마 바운드 뷰에 사용된 열을 변경해야 할 경우에는 ALTER TABLE이 실패하고 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류 메시지가 나타납니다. 스키마 바인딩 및 인덱싱된 뷰에 대 한 자세한 내용은 참조 하세요. [CREATE view&#40; Transact SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 기본 테이블을 참조하는 스키마 바운드 뷰를 만들어도 해당 테이블에서 트리거를 추가하거나 제거하는 데 영향을 주지 않습니다.  
  
## <a name="indexes-and-alter-table"></a>인덱스 및 ALTER TABLE  
 제약 조건의 일부로 만들어진 인덱스는 제약 조건을 삭제하면 같이 삭제됩니다. CREATE INDEX로 만든 인덱스는 DROP INDEX를 사용하여 삭제해야 합니다. ALTER INDEX 문을 사용하면 제약 조건 정의의 인덱스 부분을 다시 작성할 수 있습니다. 이때 ALTER TABLE을 사용하여 제약 조건을 다시 삭제하거나 추가할 필요가 없습니다.  
  
 열을 제거하려면 먼저 해당 열을 기반으로 하는 인덱스와 제약 조건을 모두 제거해야 합니다.  
  
 클러스터형 인덱스를 만든 제약 조건이 삭제되면 클러스터형 인덱스의 리프 수준에 저장된 데이터 행이 비클러스터형 테이블에 저장됩니다. 클러스터형 인덱스를 삭제하고 MOVE TO 옵션을 지정하여 결과 테이블을 단일 트랜잭션으로 다른 파일 그룹이나 파티션 구성표로 이동할 수 있습니다. MOVE TO 옵션에는 다음과 같은 제한 사항이 있습니다.  
  
-   인덱싱된 뷰나 비클러스터형 인덱스에는 MOVE TO를 사용할 수 없습니다.  
  
-   파티션 구성표 또는 파일 그룹이 이미 있어야 합니다.  
  
-   MOVE TO를 지정하지 않으면 테이블이 클러스터형 인덱스에 대해 정의된 것과 같은 파티션 구성표 또는 파일 그룹에 있게 됩니다.  
  
온라인 클러스터형된 인덱스를 삭제 하는 경우 지정할 수 있습니다  **=**  옵션 쿼리 및 수정에 기본 데이터와 연관 된 비클러스터형된 인덱스는 DROP INDEX 트랜잭션이 차단 하지 않도록 합니다.  
  
 온라인  **=**  ON에 다음과 같은 제한:  
  
-   온라인  **=**  ON도 비활성화 된 클러스터형된 인덱스에 적합 하지 않습니다. 비활성화 된 인덱스는 ONLINE을 사용 하 여 삭제 해야  **=**  OFF입니다.  
  
-   한 번에 하나의 인덱스만 삭제할 수 있습니다.  
  
-   온라인  **=**  ON 인덱싱된 뷰, 비클러스터형 인덱스 또는 로컬 임시 테이블의 인덱스에 적합 하지 않습니다.  
  
-   온라인  **=**  ON은 columnstore 인덱스에 대해 유효 하지 않습니다.  
  
클러스터형 인덱스를 삭제하려면 기존 클러스터형 인덱스와 크기가 같은 임시 디스크 공간이 필요합니다. 이 추가 공간은 작업이 완료되면 바로 해제됩니다.  
  
> [!NOTE]  
>  아래 나열 된 옵션은  *\<drop_clustered_constraint_option >* 테이블에 클러스터형된 인덱스에 적용 되며 뷰의 클러스터형된 인덱스 또는 비클러스터형된 인덱스에 적용할 수 없습니다.  
  
## <a name="replicating-schema-changes"></a>스키마 변경 내용 복제  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 게시된 테이블에 대해 ALTER TABLE을 실행하면 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에 변경 내용이 전파됩니다. 이 기능에는 몇 가지 제한이 있으며 해제할 수 있습니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
## <a name="data-compression"></a>Data Compression  
 시스템 테이블에는 압축을 사용할 수 없습니다. 테이블이 힙인 경우 ONLINE 모드의 다시 작성 작업은 단일 스레드 작업이 됩니다. 다중 스레드 힙 다시 작성 작업에는 OFFLINE 모드를 사용하세요. 데이터 압축에 대 한 자세한 내용은 참조 하십시오.[데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
 압축 상태를 변경할 경우 테이블, 인덱스 또는 파티션에 어떤 영향을 주는지 확인하려면 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 저장 프로시저를 사용합니다.  
  
 다음은 분할된 테이블에 적용되는 제한 사항입니다.  
  
-   테이블에 정렬되지 않은 인덱스가 있으면 단일 파티션의 압축 설정을 변경할 수 없습니다.  
  
-   ALTER TABLE \<테이블 > REBUILD PARTITION... 구문은 다시 작성 지정 된 파티션을 합니다.  
  
-   ALTER TABLE \<테이블 > REBUILD WITH... 구문은 모든 파티션을 다시 작성 합니다.  
  
## <a name="dropping-ntext-columns"></a>NTEXT 열 삭제  
 NTEXT 열을 삭제할 때 삭제된 데이터의 정리는 모든 행에서 직렬화된 작업으로 발생합니다. 여기에는 상당한 시간이 필요할 수 있습니다. 행이 많이 포함된 테이블에서 NTEXT 열을 삭제하는 경우 먼저 NTEXT 열을 NULL 값으로 업데이트한 다음 열을 삭제합니다. 병렬 작업을 수행할 수 있습니다 하 고 훨씬 빠를 수 있습니다.  
  
## <a name="online-index-rebuild"></a>온라인 인덱스 다시 작성  
 온라인 인덱스 다시 작성을 위해 DDL 문을 실행하려면 특정 테이블에서 실행 중인 모든 활성 차단 트랜잭션이 완료되어야 합니다. 온라인 인덱스 다시 작성이 실행되면 이 테이블에서 실행을 시작할 준비가 되어 있는 모든 새로운 트랜잭션이 차단됩니다. 온라인 인덱스 다시 작성에 대한 잠금 기간은 매우 짧지만 특정 테이블에서 열려 있는 모든 트랜잭션이 완료될 때까지 기다리고 새로운 트랜잭션이 시작되지 않도록 차단하기 위해서는 처리량에 상당한 영향을 주어 작업 속도가 느려지거나 시간 초과가 발생할 수 있으며, 기본 테이블에 대한 액세스가 크게 제한될 수 있습니다. **WAIT_AT_LOW_PRIORITY** 옵션을 사용 하면 DBA의 온라인 인덱스 다시 작성 하 고 3 개 옵션 중 하나를 선택 하도록 허용 하는 데 필요한 S-잠금 및 Sch-m 잠금을 관리할 수 있습니다. 세 가지 경우 모두, 대기 시간(`(MAX_DURATION =n [minutes])`) 중에 차단 활동이 없으면 대기 없이 온라인 인덱스 다시 작성이 즉시 실행되고 DDL 문이 완료됩니다.  
  
## <a name="compatibility-support"></a>호환성 지원  
 ALTER TABLE 문에는 두 부분(schema.object)으로 구성된 테이블 이름만 허용됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 다음 형식을 사용하여 테이블 이름을 지정하면 컴파일 시 오류 117이 발생합니다.  
  
-   server.database.schema.table  
  
-   .database.schema.table  
  
-   ..schema.table  
  
이전 버전에서는 server.database.schema.table 형식을 지정할 경우 오류 4902가 반환되었습니다. 그러나 .database.schema.table 또는 ..schema.table 형식을 지정하면 작업이 성공했습니다.  
  
 이 문제를 해결하려면 네 부분으로 구성된 접두사를 사용하지 않아야 합니다.  
  
## <a name="permissions"></a>Permissions  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
 ALTER TABLE 권한은 ALTER TABLE SWITCH 문과 관련된 두 테이블에 모두 적용됩니다. 전환된 데이터는 모두 대상 테이블의 보안을 상속합니다.  
  
 ALTER TABLE 문의 열을 CLR(공용 언어 런타임) 사용자 정의 형식 또는 별칭 데이터 형식으로 정의하면 해당 형식에 대한 REFERENCES 사용 권한이 필요합니다.  
  
 테이블의 행을 업데이트 하는 열을 추가 하려면 **업데이트** 테이블에 대 한 합니다. 예를 들어 추가 **NOT NULL** 열 기본값을 또는 테이블이 비어 있지 않은 경우 id 열을 추가 합니다.  
  
##  <a name="Example_Top"></a> 예  
  
|범주|중요한 구문 요소|  
|--------------|------------------------------|  
|[열 및 제약 조건 추가](#add)|ADD • 인덱스 옵션이 있는 PRIMARY KEY • 스파스 열 및 열 집합 •|  
|[열 및 제약 조건 삭제](#Drop)|DROP|  
|[열 정의 변경](#alter_column)|데이터 형식 변경 • 열 크기 변경 • 데이터 정렬|  
|[테이블 정의 변경](#alter_table)|DATA_COMPRESSION • SWITCH PARTITION • LOCK ESCALATION • 변경 내용 추적|  
|[제약 조건 및 트리거를 활성화 및 비활성화](#disable_enable)|CHECK • NO CHECK • ENABLE TRIGGER • DISABLE TRIGGER|  
  
###  <a name="add"></a>열 및 제약 조건 추가  
 이 섹션의 예에서는 테이블에 열 및 제약 조건을 추가하는 방법을 보여 줍니다.  
  
#### <a name="a-adding-a-new-column"></a>1. 새 열 추가  
 다음 예에서는 Null 값을 허용하고 DEFAULT 정의를 통해 제공된 값이 없는 열을 추가합니다. 새 열의 각 행 값은 `NULL`입니다.  
  
```  
CREATE TABLE dbo.doc_exa (column_a INT) ;  
GO  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL ;  
GO  
  
```  
  
#### <a name="b-adding-a-column-with-a-constraint"></a>2. 제약 조건이 있는 열 추가  
 다음 예에서는 `UNIQUE` 제약 조건이 있는 새 열을 추가합니다.  
  
```  
CREATE TABLE dbo.doc_exc (column_a INT) ;  
GO  
ALTER TABLE dbo.doc_exc ADD column_b VARCHAR(20) NULL   
    CONSTRAINT exb_unique UNIQUE ;  
GO  
EXEC sp_help doc_exc ;  
GO  
DROP TABLE dbo.doc_exc ;  
GO  
```  
  
#### <a name="c-adding-an-unverified-check-constraint-to-an-existing-column"></a>3. 기존 열에 확인되지 않은 CHECK 제약 조건 추가  
 다음 예에서는 테이블의 기존 열에 제약 조건을 추가합니다. 이 열에 제약 조건을 위반하는 값이 있습니다. 따라서 기존 행에서 제약 조건이 위반되지 않도록 하고 제약 조건을 추가할 수 있도록 `WITH NOCHECK`를 사용합니다.  
  
```  
CREATE TABLE dbo.doc_exd ( column_a INT) ;  
GO  
INSERT INTO dbo.doc_exd VALUES (-1) ;  
GO  
ALTER TABLE dbo.doc_exd WITH NOCHECK   
ADD CONSTRAINT exd_check CHECK (column_a > 1) ;  
GO  
EXEC sp_help doc_exd ;  
GO  
DROP TABLE dbo.doc_exd ;  
GO  
```  
  
#### <a name="d-adding-a-default-constraint-to-an-existing-column"></a>4. 기존 열에 DEFAULT 제약 조건 추가  
 다음 예에서는 두 개의 열이 있는 테이블을 만들어 첫 번째 열에 값을 삽입하고 다른 열은 NULL로 유지합니다. 그런 다음 `DEFAULT` 제약 조건이 두 번째 열에 추가됩니다. 기본값이 적용되었는지 확인하기 위해 다른 값이 첫 번째 열에 삽입되고 테이블이 쿼리됩니다.  
  
```  
CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
GO  
INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
GO  
ALTER TABLE dbo.doc_exz  
ADD CONSTRAINT col_b_def  
DEFAULT 50 FOR column_b ;  
GO  
INSERT INTO dbo.doc_exz (column_a) VALUES ( 10 ) ;  
GO  
SELECT * FROM dbo.doc_exz ;  
GO  
DROP TABLE dbo.doc_exz ;  
GO  
```  
  
#### <a name="e-adding-several-columns-with-constraints"></a>5. 제약 조건이 있는 여러 열 추가  
 다음 예에서는 제약 조건이 정의된 여러 열을 새로 추가합니다. 첫 번째 새 열은 `IDENTITY` 속성을 가집니다. 테이블에서 각 행의 ID 열에는 새 증분 값이 있습니다.  
  
```  
CREATE TABLE dbo.doc_exe ( column_a INT CONSTRAINT column_a_un UNIQUE) ;  
GO  
ALTER TABLE dbo.doc_exe ADD   
  
-- Add a PRIMARY KEY identity column.  
column_b INT IDENTITY  
CONSTRAINT column_b_pk PRIMARY KEY,   
  
-- Add a column that references another column in the same table.  
column_c INT NULL    
CONSTRAINT column_c_fk   
REFERENCES doc_exe(column_a),  
  
-- Add a column with a constraint to enforce that   
-- nonnull data is in a valid telephone number format.  
column_d VARCHAR(16) NULL   
CONSTRAINT column_d_chk  
CHECK   
(column_d LIKE '[0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]' OR  
column_d LIKE  
'([0-9][0-9][0-9]) [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]'),  
  
-- Add a nonnull column with a default.  
column_e DECIMAL(3,3)  
CONSTRAINT column_e_default  
DEFAULT .081 ;  
GO  
EXEC sp_help doc_exe ;  
GO  
DROP TABLE dbo.doc_exe ;  
GO  
```  
  
#### <a name="f-adding-a-nullable-column-with-default-values"></a>6. 기본값이 있는 Null 허용 열 추가  
 다음 예에서는 `DEFAULT` 정의가 있는 Null 허용 열을 추가하고 `WITH VALUES`를 사용하여 테이블의 각 기존 행에 대한 값을 제공합니다. WITH VALUES를 사용하지 않으면 각 행에서 새 열의 값은 NULL이 됩니다.  
  
```  
  
CREATE TABLE dbo.doc_exf ( column_a INT) ;  
GO  
INSERT INTO dbo.doc_exf VALUES (1) ;  
GO  
ALTER TABLE dbo.doc_exf   
ADD AddDate smalldatetime NULL  
CONSTRAINT AddDateDflt  
DEFAULT GETDATE() WITH VALUES ;  
GO  
DROP TABLE dbo.doc_exf ;  
GO  
```  
  
#### <a name="g-creating-a-primary-key-constraint-with-index-options"></a>7. 인덱스 옵션을 설정하여 PRIMARY KEY 제약 조건 만들기  
 다음 예에서는 PRIMARY KEY 제약 조건 `PK_TransactionHistoryArchive_TransactionID`를 만들고 `FILLFACTOR`, `ONLINE` 및 `PAD_INDEX` 옵션을 설정합니다. 결과 클러스터형 인덱스의 이름은 제약 조건 이름과 같습니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE Production.TransactionHistoryArchive WITH NOCHECK   
ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
WITH (FILLFACTOR = 75, ONLINE = ON, PAD_INDEX = ON);  
GO  
```  
  
#### <a name="h-adding-a-sparse-column"></a>8. 스파스 열 추가  
 다음 예에서는 T1 테이블의 스파스 열 추가 및 수정을 보여 줍니다. `T1` 테이블을 만들기 위한 코드는 다음과 같습니다.  
  
```  
CREATE TABLE T1  
(C1 int PRIMARY KEY,  
C2 varchar(50) SPARSE NULL,  
C3 int SPARSE NULL,  
C4 int ) ;  
GO  
```  
  
 추가 스파스 열 `C5`를 추가하려면 다음 문을 실행합니다.  
  
```  
ALTER TABLE T1  
ADD C5 char(100) SPARSE NULL ;  
GO  
```  
  
 스파스가 아닌 열 `C4`를 스파스 열로 변환하려면 다음 문을 실행합니다.  
  
```  
ALTER TABLE T1  
ALTER COLUMN C4 ADD SPARSE ;  
GO  
```  
  
 변환 하는 `C4` 스파스가 아닌 열을 스파스 열에는 다음 문을 실행 합니다.  
  
```  
ALTER TABLE T1  
ALTER COLUMN C4 DROP SPARSE;  
GO  
```  
  
#### <a name="i-adding-a-column-set"></a>9. 열 집합 추가  
 다음 예에서는 `T2` 테이블에 열을 추가하는 방법을 보여 줍니다. 스파스 열이 이미 포함되어 있는 테이블에는 열 집합을 추가할 수 없습니다. `T2` 테이블을 만들기 위한 코드는 다음과 같습니다.  
  
```  
CREATE TABLE T2  
(C1 int PRIMARY KEY,  
C2 varchar(50) NULL,  
C3 int NULL,  
C4 int ) ;  
GO  
```  
  
 다음 3개의 문은 `CS`라는 열 집합을 추가한 다음, `C2` 및 `C3` 열을 `SPARSE`로 수정합니다.  
  
```  
ALTER TABLE T2  
ADD CS XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ;  
GO  
  
ALTER TABLE T2  
ALTER COLUMN C2 ADD SPARSE ;   
GO  
  
ALTER TABLE T2  
ALTER COLUMN C3 ADD SPARSE ;  
GO  
```  
  
#### <a name="j-adding-an-encrypted-column"></a>10. 암호화 된 열을 추가합니다.  
 라는 암호화 된 열을 추가 하는 다음 문은 `PromotionCode`합니다.  
  
```  
ALTER TABLE Customers ADD  
    PromotionCode nvarchar(100)   
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,  
    ENCRYPTION_TYPE = RANDOMIZED,  
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') ;  
```  
  
###  <a name="Drop"></a>열 및 제약 조건 삭제  
 이 섹션의 예에서는 열 및 제약 조건을 삭제하는 방법을 보여 줍니다.  
  
#### <a name="a-dropping-a-column-or-columns"></a>1. 열 삭제  
 첫 번째 예에서는 테이블을 수정하여 열을 제거합니다. 두 번째 예에서는 여러 열을 제거합니다.  
  
```  
CREATE TABLE dbo.doc_exb   
    (column_a INT  
     ,column_b VARCHAR(20) NULL  
     ,column_c datetime  
     ,column_d int) ;  
GO  
-- Remove a single column.  
ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;  
GO  
-- Remove multiple columns.  
ALTER TABLE dbo.doc_exb DROP COLUMN column_c, column_d;  
  
```  
  
#### <a name="b-dropping-constraints-and-columns"></a>2. 제약 조건 및 열 삭제  
 첫 번째 예에서는 테이블에서 `UNIQUE` 제약 조건을 제거합니다. 두 번째 예에서는 제약 조건 두 개와 열 하나를 제거합니다.  
  
```  
CREATE TABLE dbo.doc_exc ( column_a int NOT NULL CONSTRAINT my_constraint UNIQUE) ;  
GO  
  
-- Example 1. Remove a single constraint.  
ALTER TABLE dbo.doc_exc DROP my_constraint ;  
GO  
  
DROP TABLE dbo.doc_exc;  
GO  
  
CREATE TABLE dbo.doc_exc ( column_a int    
                          NOT NULL CONSTRAINT my_constraint UNIQUE  
                          ,column_b int   
                          NOT NULL CONSTRAINT my_pk_constraint PRIMARY KEY) ;  
GO  
  
-- Example 2. Remove two constraints and one column  
-- The keyword CONSTRAINT is optional. The keyword COLUMN is required.  
ALTER TABLE dbo.doc_exc   
  
    DROP CONSTRAINT CONSTRAINT my_constraint, my_pk_constraint, COLUMN column_b ;  
GO  
  
```  
  
#### <a name="c-dropping-a-primary-key-constraint-in-the-online-mode"></a>3. ONLINE 모드에서 PRIMARY KEY 제약 조건 삭제  
 다음 예에서는 `ONLINE` 옵션이 `ON`으로 설정된 PRIMARY KEY 제약 조건을 삭제합니다.  
  
```  
  
ALTER TABLE Production.TransactionHistoryArchive  
DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID  
WITH (ONLINE = ON);  
GO  
```  
  
#### <a name="d-adding-and-dropping-a-foreign-key-constraint"></a>4. FOREIGN KEY 제약 조건 추가 및 삭제  
 다음 예에서는 `ContactBackup` 테이블을 만든 다음 `FOREIGN KEY` 테이블을 참조하는 `Person.Person` 제약 조건을 추가했다가 다시 `FOREIGN KEY` 제약 조건을 삭제하여 테이블을 변경합니다.  
  
```  
CREATE TABLE Person.ContactBackup  
    (ContactID int) ;  
GO  
  
ALTER TABLE Person.ContactBackup  
ADD CONSTRAINT FK_ContactBacup_Contact FOREIGN KEY (ContactID)  
    REFERENCES Person.Person (BusinessEntityID) ;  
GO  
  
ALTER TABLE Person.ContactBackup  
DROP CONSTRAINT FK_ContactBacup_Contact ;  
GO  
  
DROP TABLE Person.ContactBackup ;  
```  
  
 ![맨 위 링크를 다시 사용 되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "위쪽 링크를 다시 사용 되는 화살표 아이콘") [예제](#Example_Top)  
  
###  <a name="alter_column"></a>열 정의 변경  
  
#### <a name="a-changing-the-data-type-of-a-column"></a>1. 열의 데이터 형식 변경  
 다음 예에서는 테이블의 열을 `INT`에서 `DECIMAL`로 변경합니다.  
  
```  
CREATE TABLE dbo.doc_exy (column_a INT ) ;  
GO  
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
GO  
ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
GO  
DROP TABLE dbo.doc_exy ;  
GO  
```  
  
#### <a name="b-changing-the-size-of-a-column"></a>2. 열 크기 변경  
 다음 예제에서는의 크기를 늘리는 한 **varchar** 열 전체 자릿수 및 소수 자릿수가 **10 진수** 열입니다. 열에 데이터가 포함되어 있으므로 열 크기는 늘리기만 가능합니다. 또한 `col_a`는 고유 인덱스에 정의됩니다. 크기 `col_a` 데이터 형식이 이므로 늘릴 수 있습니다는 **varchar** 고 인덱스는 PRIMARY KEY 제약 조건의 결과가 없습니다.  
  
```  
-- Create a two-column table with a unique index on the varchar column.  
CREATE TABLE dbo.doc_exy ( col_a varchar(5) UNIQUE NOT NULL, col_b decimal (4,2));  
GO  
INSERT INTO dbo.doc_exy VALUES ('Test', 99.99);  
GO  
-- Verify the current column size.  
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale  
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');  
GO  
-- Increase the size of the varchar column.  
ALTER TABLE dbo.doc_exy ALTER COLUMN col_a varchar(25);  
GO  
-- Increase the scale and precision of the decimal column.  
ALTER TABLE dbo.doc_exy ALTER COLUMN col_b decimal (10,4);  
GO  
-- Insert a new row.  
INSERT INTO dbo.doc_exy VALUES ('MyNewColumnSize', 99999.9999) ;  
GO  
-- Verify the current column size.  
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale  
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');  
```  
  
#### <a name="c-changing-column-collation"></a>3. 열 데이터 정렬 변경  
 다음 예에서는 열의 데이터 정렬을 변경하는 방법을 보여 줍니다. 먼저 기본 사용자 데이터 정렬을 사용하여 테이블을 만듭니다.  
  
```  
CREATE TABLE T3  
(C1 int PRIMARY KEY,  
C2 varchar(50) NULL,  
C3 int NULL,  
C4 int ) ;  
GO  
```  
  
 그런 다음 `C2` 열 데이터 정렬을 Latin1_General_BIN으로 변경합니다. 데이터 형식은 변경하지 않더라도 필요합니다.  
  
```  
ALTER TABLE T3  
ALTER COLUMN C2 varchar(50) COLLATE Latin1_General_BIN;  
GO  
  
```  

  
###  <a name="alter_table"></a>테이블 정의 변경  
 이 섹션의 예에서는 테이블 정의를 변경하는 방법을 보여 줍니다.  
  
#### <a name="a-modifying-a-table-to-change-the-compression"></a>1. 테이블을 수정하여 압축 변경  
 다음 예에서는 분할되지 않은 테이블의 압축을 변경합니다. 힙 또는 클러스터형 인덱스는 다시 작성됩니다. 테이블이 힙인 경우에는 모든 비클러스터형 인덱스가 다시 작성됩니다.  
  
```  
ALTER TABLE T1   
REBUILD WITH (DATA_COMPRESSION = PAGE);  
```  
  
 다음 예에서는 분할된 테이블의 압축을 변경합니다. `REBUILD PARTITION = 1` 구문은 파티션 번호 `1`만 다시 작성합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  NONE) ;  
GO  
```  
  
다음과 같은 대체 구문을 사용하여 같은 작업을 실행하면 테이블의 모든 파티션이 다시 작성됩니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = ALL   
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1) ) ;  
```  
  
 추가 데이터 압축 예 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
#### <a name="b-modifying-a-columnstore-table-to-change-archival-compression"></a>2. columnstore 테이블을 수정하여 보관 압축 변경  
 다음 예에서는 추가 압축 알고리즘을 적용하여 columnstore 테이블 파티션을 보다 더 압축합니다. 그러면 테이블 크기는 보다 작아지지만 저장 및 검색에 필요한 시간은 증가합니다. 보관하거나 보다 적은 저장소가 필요한 기타 상황에서 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
GO  
```  
  
다음 예에서는 COLUMNSTORE_ARCHIVE 옵션으로 압축된 columnstore 테이블 파티션을 압축 해제합니다. 데이터는 복구될 때 모든 columnstore 테이블에 사용된 columnstore 압축으로 계속 압축됩니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
GO  
```  
  
#### <a name="c-switching-partitions-between-tables"></a>3. 테이블 간 파티션 전환  
 다음 예에서는 분할된 테이블을 만들고 파티션 구성표 `myRangePS1`을 데이터베이스에 이미 만들었다고 가정합니다. 그런 다음 분할되지 않은 테이블이 분할된 테이블과 같은 구조로 `PARTITION 2` 테이블의 `PartitionTable`와 같은 파일 그룹에 만들어집니다. 그러면 `PARTITION 2` 테이블의 `PartitionTable` 데이터가 `NonPartitionTable` 테이블로 전환됩니다.  
  
```  
CREATE TABLE PartitionTable (col1 int, col2 char(10))  
ON myRangePS1 (col1) ;  
GO  
CREATE TABLE NonPartitionTable (col1 int, col2 char(10))  
ON test2fg ;  
GO  
ALTER TABLE PartitionTable SWITCH PARTITION 2 TO NonPartitionTable ;  
GO  
```  
  
#### <a name="d-allowing-lock-escalation-on-partitioned-tables"></a>4. 분할된 테이블의 잠금 에스컬레이션 허용  
 다음 예에서는 분할된 테이블의 파티션 수준에 대한 잠금 에스컬레이션을 활성화합니다. 테이블이 분할되지 않은 경우 잠금 에스컬레이션은 TABLE 수준에서 설정됩니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
ALTER TABLE dbo.T1 SET (LOCK_ESCALATION = AUTO);  
GO  
```  
  
#### <a name="e-configuring-change-tracking-on-a-table"></a>5. 테이블에 변경 내용 추적 구성  
 다음 예에서는 `Person.Person` 테이블에 대해 변경 내용 추적을 사용하도록 설정합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
USE AdventureWorks2012;  
ALTER TABLE Person.Person  
ENABLE CHANGE_TRACKING;  
```  
  
다음 예에서는 변경 내용 추적을 활성화하고 변경 중에 업데이트되는 열을 추적하도록 설정합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE Person.Person  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
다음 예에서는 `Person.Person` 테이블에 대해 변경 내용 추적을 사용하지 않도록 설정합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
USE AdventureWorks2012;  
Go  
ALTER TABLE Person.Person  
DISABLE CHANGE_TRACKING;  
```  

  
###  <a name="disable_enable"></a>제약 조건 및 트리거를 활성화 및 비활성화  
  
#### <a name="a-disabling-and-re-enabling-a-constraint"></a>1. 제약 조건 해제 및 다시 설정  
 다음 예에서는 데이터에 허용되는 급여를 제한하는 제약 조건을 비활성화합니다. `NOCHECK CONSTRAINT`에 `ALTER TABLE`를 사용하면 제약 조건이 비활성화되어 일반적으로 해당 제약 조건을 위반하는 삽입을 허용합니다. `CHECK CONSTRAINT`는 제약 조건을 재설정합니다.  
  
```  
CREATE TABLE dbo.cnst_example   
(id INT NOT NULL,  
 name VARCHAR(10) NOT NULL,  
 salary MONEY NOT NULL  
    CONSTRAINT salary_cap CHECK (salary < 100000)  
);  
  
-- Valid inserts  
INSERT INTO dbo.cnst_example VALUES (1,'Joe Brown',65000);  
INSERT INTO dbo.cnst_example VALUES (2,'Mary Smith',75000);  
  
-- This insert violates the constraint.  
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);  
  
-- Disable the constraint and try again.  
ALTER TABLE dbo.cnst_example NOCHECK CONSTRAINT salary_cap;  
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);  
  
-- Re-enable the constraint and try another insert; this will fail.  
ALTER TABLE dbo.cnst_example CHECK CONSTRAINT salary_cap;  
INSERT INTO dbo.cnst_example VALUES (4,'Eric James',110000) ;  
```  
  
#### <a name="b-disabling-and-re-enabling-a-trigger"></a>2. 트리거 해제 및 다시 설정  
 다음 예에서는 `DISABLE TRIGGER`의 `ALTER TABLE` 옵션을 사용하여 트리거를 해제하고 일반적으로 트리거를 위반하는 삽입을 허용합니다. 그런 다음 `ENABLE TRIGGER`를 사용하여 트리거를 재설정합니다.  
  
```  
CREATE TABLE dbo.trig_example   
(id INT,   
name VARCHAR(12),  
salary MONEY) ;  
GO  
-- Create the trigger.  
CREATE TRIGGER dbo.trig1 ON dbo.trig_example FOR INSERT  
AS  
IF (SELECT COUNT(*) FROM INSERTED  
WHERE salary > 100000) > 0  
BEGIN  
    print 'TRIG1 Error: you attempted to insert a salary > $100,000'  
    ROLLBACK TRANSACTION  
END ;  
GO  
-- Try an insert that violates the trigger.  
INSERT INTO dbo.trig_example VALUES (1,'Pat Smith',100001) ;  
GO  
-- Disable the trigger.  
ALTER TABLE dbo.trig_example DISABLE TRIGGER trig1 ;  
GO  
-- Try an insert that would typically violate the trigger.  
INSERT INTO dbo.trig_example VALUES (2,'Chuck Jones',100001) ;  
GO  
-- Re-enable the trigger.  
ALTER TABLE dbo.trig_example ENABLE TRIGGER trig1 ;  
GO  
-- Try an insert that violates the trigger.  
INSERT INTO dbo.trig_example VALUES (3,'Mary Booth',100001) ;  
GO  
```  
 
  
### <a name="online-operations"></a>온라인 작업  
  
#### <a name="a-online-index-rebuild-using-low-priority-wait-options"></a>1. 낮은 우선 순위 대기 옵션을 사용한 온라인 인덱스 다시 작성  
 다음 예에서는 낮은 우선 순위 대기 옵션을 지정하여 온라인 인덱스 다시 작성을 수행하는 방법을 보여 줍니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
ALTER TABLE T1   
REBUILD WITH   
(  
    PAD_INDEX = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, 
                                         ABORT_AFTER_WAIT = BLOCKERS ) )  
)  
;  
```  
  
#### <a name="b-online-alter-column"></a>2. 온라인 열 변경  
 다음 예에서는 ONLINE 옵션을 사용하여 열 변경 작업을 수행하는 방법을 보여 줍니다.  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
```  
CREATE TABLE dbo.doc_exy (column_a INT ) ;  
GO  
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
GO  
ALTER TABLE dbo.doc_exy   
    ALTER COLUMN column_a DECIMAL (5, 2) WITH (ONLINE = ON);  
GO  
sp_help doc_exy;  
DROP TABLE dbo.doc_exy ;  
GO  
```  
  
##  <a name="system_versioning"></a>시스템 버전 관리  
 다음 4 개의 예제에서는 시스템 버전 관리를 사용 하는 구문에 익숙해지는 데 도움이 됩니다. 추가 지원이 필요한 경우 참조 [시스템 버전 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
### <a name="a-add-system-versioning-to-existing-tables"></a>1. 기존 테이블에 시스템 버전 관리 추가  
 다음 예제에서는 기존 테이블에 시스템 버전 관리를 추가 하 고 이후 기록 테이블을 만들도록 하는 방법을 보여 줍니다. 이 예에서는 라는 기존 테이블 임을 가정 `InsurancePolicy` 와 기본 키가 정의 합니다. 이 예제에서는 이러한 값은 null 일 수 없습니다 때문에 시작 및 종료 시간에 대 한 기본값을 사용 하는 시스템 버전 관리에 대해 새로 만든된 기간 열을 채웁니다. 이 예제에서는 HIDDEN 절을 사용 하 여 현재 테이블과 상호 작용 하는 기존 응용 프로그램에 영향을 주지에 되도록 합니다.  사용할 수 있는 HISTORY_RETENTION_PERIOD 사용 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 만 합니다. 
  
```  
--Alter non-temporal table to define periods for system versioning  
ALTER TABLE InsurancePolicy  
ADD PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime),   
SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL 
    DEFAULT GETUTCDATE(),   
SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL 
    DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59.99999999');  
--Enable system versioning with 1 year retention for historical data
ALTER TABLE InsurancePolicy 
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 1 YEAR));  
```  
  
### <a name="b-migrate-an-existing-solution-to-use-system-versioning"></a>2. 시스템 버전 관리를 사용 하는 기존 솔루션 마이그레이션  
 다음 예제에서는 기본 제공 임시 지원 모방 하기 위해 트리거를 사용 하는 솔루션에서 시스템 버전 관리로 마이그레이션 방법을 보여 줍니다. 이 예제에서는 사용 하는 기존 솔루션은 가정는 `ProjectTaskCurrent` 테이블 및 `ProjectTaskHistory` 이러한 기간 열은 datetime2 데이터 형식을 사용 하지 않는 해당 기간에 대 한 변경 된 날짜 및 수정 된 날짜 열을 사용 하 여를 기존 솔루션에 대 한 테이블 와 `ProjectTaskCurrent` 테이블에 기본 키가 정의 합니다.  
  
```  
-- Drop existing trigger  
DROP TRIGGER ProjectTaskCurrent_Trigger;  
-- Adjust the schema for current and history table  
-- Change data types for existing period columns  
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [Changed Date] datetime2 NOT NULL;  
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [Revised Date] datetime2 NOT NULL;  
  
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Changed Date] datetime2 NOT NULL;  
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Revised Date] datetime2 NOT NULL;  
  
-- Add SYSTEM_TIME period and set system versioning with linking two existing tables  
-- (a certain set of data checks happen in the background)  
ALTER TABLE ProjectTaskCurrent  
ADD PERIOD FOR SYSTEM_TIME ([Changed Date], [Revised Date])  
  
ALTER TABLE ProjectTaskCurrent  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON))  
```  
  
### <a name="c-disabling-and-re-enabling-system-versioning-to-change-table-schema"></a>3. 시스템 버전 관리 테이블 스키마를 변경 하려면 다시 활성화 및 비활성화  
 시스템 버전 관리를 사용 하지 않도록 설정 하는 방법을 보여 주는이 예제는 `Department` 테이블 열을 추가 하 고 다시 시스템 버전 관리를 사용 하도록 설정 합니다. 테이블 스키마를 수정 하는 데 필요한 시스템 버전 관리를 사용 하지 않도록 설정 합니다. 그러면 DBA는 데이터 일관성을 건너뛰려면 다시 시스템 버전 관리를 사용 하도록 설정 하는 경우를 확인 하 고는 성능을 활용 테이블 스키마를 업데이트 하는 동안 두 테이블 모두로 업데이트 되지 않도록 하려면 트랜잭션 내에서 이러한 단계를 수행 합니다. Note 통계를 작성, 파티션 전환 하거나 하나 또는 두 테이블에 압축을 적용 등의 작업에 필요 하지 않음을 시스템 버전 관리를 사용 하지 않도록 설정 합니다.  
  
```  
BEGIN TRAN  
/* Takes schema lock on both tables */  
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = OFF);  
/* expand table schema for temporal table */  
ALTER TABLE Department  
     ADD Col5 int NOT NULL DEFAULT 0;  
/* Expand table schema for history table */  
ALTER TABLE DepartmentHistory  
    ADD Col5 int NOT NULL DEFAULT 0;  
/* Re-establish versioning again  */
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE=dbo.DepartmentHistory, 
                                 DATA_CONSISTENCY_CHECK = OFF));  
COMMIT   
```  
  
### <a name="d-removing-system-versioning"></a>4. 시스템 버전 관리를 제거합니다.  
 Department 테이블 및 drop에서 시스템 버전 관리를 완전히 제거 하는 방법을 보여 주는이 예제는 `DepartmentHistory` 테이블입니다. 필요에 따라 시스템 버전 관리 정보를 기록 하는 시스템에서 사용 하는 기간 열을 삭제할 수도 있습니다. 참고 하거나 삭제할 수 없습니다는 `Department` 또는 `DepartmentHistory` 시스템 버전 관리를 사용 하는 동안 테이블입니다.  
  
```  
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = OFF);  
ALTER TABLE Department  
DROP PEROD FOR SYSTEM_TIME;  
DROP TABLE DepartmentHistory;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 A-C 사용에서 FactResellerSales 테이블의 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스입니다.  
  
### <a name="e-determining-if-a-table-is-partitioned"></a>5. 테이블이 분할 되었는지 여부를 결정  
 다음 쿼리는 `FactResellerSales` 테이블이 분할된 경우 하나 이상의 행을 반환합니다. 테이블이 분할되지 않은 경우 행이 반환되지 않습니다.  
  
```  
SELECT * FROM sys.partitions AS p  
JOIN sys.tables AS t  
    ON  p.object_id = t.object_id  
WHERE p.partition_id IS NOT NULL  
    AND t.name = 'FactResellerSales';  
```  
  
### <a name="f-determining-boundary-values-for-a-partitioned-table"></a>6. 분할된 된 테이블에 대 한 경계 값 결정  
 다음 쿼리는 `FactResellerSales` 테이블의 각 파티션에 대해 경계 값을 반환합니다.  
  
```  
SELECT t.name AS TableName, i.name AS IndexName, p.partition_number, 
    p.partition_id, i.data_space_id, f.function_id, f.type_desc, 
    r.boundary_id, r.value AS BoundaryValue   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.partitions AS p  
    ON i.object_id = p.object_id AND i.index_id = p.index_id   
JOIN  sys.partition_schemes AS s   
    ON i.data_space_id = s.data_space_id  
JOIN sys.partition_functions AS f   
    ON s.function_id = f.function_id  
LEFT JOIN sys.partition_range_values AS r   
    ON f.function_id = r.function_id and r.boundary_id = p.partition_number  
WHERE t.name = 'FactResellerSales' AND i.type <= 1  
ORDER BY p.partition_number;  
```  
  
### <a name="g-determining-the-partition-column-for-a-partitioned-table"></a>7. 분할된 된 테이블에 대 한 파티션 열 확인  
 다음 쿼리는 테이블에 대한 분할 열의 이름을 반환합니다. `FactResellerSales`을 참조하세요.  
  
```  
SELECT t.object_id AS Object_ID, t.name AS TableName, 
    ic.column_id as PartitioningColumnID, c.name AS PartitioningColumnName   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.columns AS c  
    ON t.object_id = c.object_id  
JOIN sys.partition_schemes AS ps  
    ON ps.data_space_id = i.data_space_id  
JOIN sys.index_columns AS ic  
    ON ic.object_id = i.object_id 
    AND ic.index_id = i.index_id AND ic.partition_ordinal > 0  
WHERE t.name = 'FactResellerSales'  
AND i.type <= 1  
AND c.column_id = ic.column_id;  
```  
  
### <a name="h-merging-two-partitions"></a>8. 두 개의 파티션을 병합  
 다음 예에서는 테이블에 두 개의 파티션을 병합합니다.  
  
 `Customer` 테이블에 다음과 같이 정의 합니다.  
  
```  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 10, 25, 50, 100)));  
```  
  
 다음 명령은 10-25 파티션 경계를 결합합니다.  
  
```  
ALTER TABLE Customer MERGE RANGE (10);  
```  
  
 테이블에 대 한 새 DDL은입니다.  
  
```  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 25, 50, 100)));  
```  
  
### <a name="i-splitting-a-partition"></a>9. 파티션 분  
 다음 예에서는 테이블의 파티션을 분할합니다.  
  
 `Customer` 테이블에 DDL:  
  
```  
DROP TABLE Customer;  
  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 10, 25, 50, 100 )));  
```  
  
 다음 명령은 50과 100 사이의 75 이며이 값에 의해 바인딩된 새 파티션을 만듭니다.  
  
```  
ALTER TABLE Customer SPLIT RANGE (75);  
```  
  
 테이블에 대 한 새 DDL은입니다.  
  
```  
CREATE TABLE Customer (  
   id int NOT NULL,  
   lastName varchar(20),  
   orderCount int,  
   orderDate date)  
   WITH DISTRIBUTION = HASH(id),  
   PARTITION ( orderCount (RANGE LEFT  
      FOR VALUES (1, 5, 10, 25, 50, 75, 100 )));  
```  
  
### <a name="j-using-switch-to-move-a-partition-to-a-history-table"></a>10. 스위치를 사용 하 여 기록 테이블에 파티션을 이동 하려면  
 파티션에 있는 데이터를 이동 하는 다음 예제는 `Orders` 의 파티션으로 테이블의 `OrdersHistory` 테이블입니다.  
  
 `Orders` 테이블에 DDL:  
  
```  
CREATE TABLE Orders (  
    id INT,  
    city VARCHAR (25),  
    lastUpdateDate DATE,  
    orderDate DATE )  
WITH   
    (DISTRIBUTION = HASH ( id ),  
    PARTITION ( orderDate RANGE RIGHT   
    FOR VALUES ('2004-01-01', '2005-01-01', '2006-01-01', '2007-01-01' )));  
```  
  
 이 예제는 `Orders` 테이블에는 다음과 같은 파티션이 있습니다. 각 파티션에 데이터를 포함 합니다.  
  
|Partition|데이터에 게 있나요?|경계 범위|  
|---------------|---------------|--------------------|  
|1.|예|OrderDate < ' 2004-01-01'|  
|2|예|' 2004-01-01' < = 주문일 < ' 2005-01-01'|  
|3|예|' 2005-01-01' < = 주문일 < ' 2006-01-01'|  
|4|예|' 2006-01-01'< = 주문일 < ' 2007-01-01'|  
|5|예|' 2007-01-01' < = 주문일|  
  
-   파티션 1 (데이터에 있음): OrderDate < ' 2004-01-01'  
-   파티션 2 (데이터에 있음): ' 2004-01-01' < = 주문일 < ' 2005-01-01'  
-   파티션 3 (데이터에 있음): ' 2005-01-01' < = 주문일 < ' 2006-01-01'  
-   파티션 4 (데이터에 있음): ' 2006-01-01'< = 주문일 < ' 2007-01-01'  
-   파티션 5 (데이터에 있음): ' 2007-01-01' < = 주문일  
  
`OrdersHistory` 테이블에 동일한 열 및 열 이름에는 다음 DDL로는 `Orders` 테이블입니다. 둘 다에 해시 배포는 `id` 열입니다.  
  
```  
CREATE TABLE OrdersHistory (  
   id INT,  
   city VARCHAR (25),  
   lastUpdateDate DATE,  
   orderDate DATE )  
WITH   
    (DISTRIBUTION = HASH ( id ),  
    PARTITION ( orderDate RANGE RIGHT   
    FOR VALUES ( '2004-01-01' )));  
```  
  
 열 및 열 이름은 여야 하지만 동일한, 파티션 경계 않아도 동일 하 게 됩니다. 이 예제는 `OrdersHistory` 테이블에는 다음 두 개의 파티션이 및 두 파티션이 비어 있습니다.  
  
-   파티션 1 (데이터 없음): OrderDate < ' 2004-01-01'  
-   파티션 (비어 있음) 2: ' 2004-01-01' < = 주문일  
  
다음 명령은 이전 두 테이블에 대 한 모든 행을 이동 `OrderDate < '2004-01-01'` 에서 `Orders` 테이블는 `OrdersHistory` 테이블입니다.  
  
```  
ALTER TABLE Orders SWITCH PARTITION 1 TO OrdersHistory PARTITION 1;  
```  
  
 첫 번째 파티션에 결과적으로, `Orders` 가 비어 있고의 첫 번째 파티션에 `OrdersHistory` 데이터를 포함 합니다. 이제는 테이블이 다음과 같이 표시 됩니다.  
  
 `Orders`테이블  
  
-   파티션 1 (비어 있음): OrderDate < ' 2004-01-01'  
-   파티션 2 (데이터에 있음): ' 2004-01-01' < = 주문일 < ' 2005-01-01'  
-   파티션 3 (데이터에 있음): ' 2005-01-01' < = 주문일 < ' 2006-01-01'  
-   파티션 4 (데이터에 있음): ' 2006-01-01'< = 주문일 < ' 2007-01-01'  
-   파티션 5 (데이터에 있음): ' 2007-01-01' < = 주문일  
  
 `OrdersHistory`테이블  
  
-   파티션 1 (데이터에 있음): OrderDate < ' 2004-01-01'  
-   파티션 (비어 있음) 2: ' 2004-01-01' < = 주문일  
  
정리는 `Orders` 테이블 파티션 1 및 2를 다음과 같이 병합 하 여 빈 파티션을 제거할 수 있습니다.  
  
```  
ALTER TABLE Orders MERGE RANGE ('2004-01-01');  
```  
  
 병합 후의 `Orders` 테이블에는 다음과 같은 파티션이:  
  
 `Orders`테이블  
  
-   파티션 1 (데이터에 있음): OrderDate < ' 2005-01-01'  
-   파티션 2 (데이터에 있음): ' 2005-01-01' < = 주문일 < ' 2006-01-01'  
-   파티션 3 (데이터에 있음): ' 2006-01-01'< = 주문일 < ' 2007-01-01'  
-   파티션 4 (데이터에 있음): ' 2007-01-01' < = 주문일  
  
다른 연도 전달 하 고 2005 년을 보관할 준비가 되었습니다. 가정 합니다. 2005 년에 대 한 빈 파티션이 할당할 수는 `OrdersHistory` 다음과 같이 빈 파티션 분할 하 여 테이블:  
  
```  
ALTER TABLE OrdersHistory SPLIT RANGE ('2005-01-01');  
```  
  
 그러나 분할 작업 이후는 `OrdersHistory` 테이블에는 다음과 같은 파티션이:  
  
 `OrdersHistory`테이블  
  
-   파티션 1 (데이터에 있음): OrderDate < ' 2004-01-01'  
-   파티션 (비어 있음) 2: ' 2004-01-01' < ' 2005-01-01'  
-   파티션 3 (비어 있음): ' 2005-01-01' < = 주문일  
  
## <a name="see-also"></a>관련 항목:  
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP table&#40; Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [ALTER PARTITION scheme&#40; Transact SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [ALTER PARTITION function&#40; Transact SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


