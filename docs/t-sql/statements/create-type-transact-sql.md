---
title: CREATE TYPE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql13.swb.sysdatatype.properties.f1
- CREATE TYPE
- TYPE_TSQL
- TYPE
- CREATE_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [SQL Server], creating
- CLR user-defined types [SQL Server]
- user-defined table types [SQL Server]
- user-defined types [SQL Server], creating
- CREATE TYPE statement
- alias data types [SQL Server], creating
- data types [SQL Server], creating
ms.assetid: 2202236b-e09f-40a1-bbc7-b8cff7488905
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 83b5031ac62e79005b4c6fb2d6d3aaf76607444b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85766928"
---
# <a name="create-type-transact-sql"></a>CREATE TYPE(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 현재 데이터베이스에 별칭 데이터 형식 또는 사용자 정의 형식을 만듭니다. 별칭 데이터 형식의 구현은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 시스템 형식을 기반으로 합니다. 사용자 정의 형식은 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)에서 어셈블리의 클래스를 통해 구현됩니다. 사용자 정의 형식을 구현에 바인딩하기 위해서는 우선 [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)를 사용하여 해당 형식의 구현을 포함하는 CLR 어셈블리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 등록해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR 코드 실행 기능이 기본적으로 해제되어 있습니다. 관리 코드 모듈을 참조하는 데이터베이스 개체를 생성, 수정 및 삭제할 수 있지만 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 [clr enabled Option](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)을 설정해야만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이러한 참조가 실행됩니다.  
 
> [!NOTE]  
>  이 항목에서는 .NET Framework CLR을 SQL Server에 통합하는 방법에 대해 설명합니다. Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에는 CLR 통합이 적용되지 않습니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- User-defined Data Type Syntax    
CREATE TYPE [ schema_name. ] type_name  
{   
    [
      FROM base_type   
      [ ( precision [ , scale ] ) ]  
      [ NULL | NOT NULL ]
    ]
    | EXTERNAL NAME assembly_name [ .class_name ]   
    | AS TABLE ( { <column_definition> | <computed_column_definition> [ ,... n ] }
      [ <table_constraint> ] [ ,... n ]    
      [ <table_index> ] [ ,... n ] } )
 
} [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   
    [ NULL | NOT NULL ]  
    [   
        DEFAULT constant_expression ]   
      | [ IDENTITY [ ( seed ,increment ) ]   
    ]  
    [ ROWGUIDCOL ] [ <column_constraint> [ ...n ] ]   
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
                [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH ( <index_option> [ ,...n ] )   
        ]  
  | CHECK ( logical_expression )   
}   
  
<computed_column_definition> ::=  
  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH ( <index_option> [ ,...n ] )  
        ]  
    | CHECK ( logical_expression )   
]   
  
<table_constraint> ::=  
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
    ( column [ ASC | DESC ] [ ,...n ] )   
        [   
    WITH ( <index_option> [ ,...n ] )   
        ]  
    | CHECK ( logical_expression )   
}   
  
<index_option> ::=  
{  
    IGNORE_DUP_KEY = { ON | OFF }  
}  

< table_index > ::=  
  INDEX constraint_name  
     [ CLUSTERED | NONCLUSTERED ]   (column [ ASC | DESC ] [ ,... n ] )} }  
```  
  
```syntaxsql
-- User-defined Memory Optimized Table Types Syntax  
CREATE TYPE [schema_name. ] type_name  
AS TABLE ( { <column_definition> [ ,... n ] }  
    | [ <table_constraint> ] [ ,... n ]    
    | [ <table_index> ] [ ,... n ] } )
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   [ NULL | NOT NULL ]    [  
      [ IDENTITY [ (1 , 1) ]  
    ]  
    [ <column_constraint> [ ... n ] ]    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
{ PRIMARY KEY {   NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count) 
                | NONCLUSTERED } }  
  
< table_constraint > ::=  
{ PRIMARY KEY { NONCLUSTERED HASH (column [ ,... n ] ) 
                   WITH (BUCKET_COUNT = bucket_count) 
               | NONCLUSTERED  (column [ ASC | DESC ] [ ,... n ] )  } }  
  
<column_index> ::=  
  INDEX index_name  
{ { [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count) 
     | NONCLUSTERED } }  
  
< table_index > ::=  
  INDEX constraint_name  
{ { [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count) 
 |  [NONCLUSTERED]  (column [ ASC | DESC ] [ ,... n ] )} }  
  
<table_option> ::=  
{  
    [MEMORY_OPTIMIZED = {ON | OFF}]  
}  
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 별칭 데이터 형식이나 사용자 정의 형식이 속한 스키마의 이름입니다.  
  
 *type_name*  
 별칭 데이터 형식 또는 사용자 정의 형식의 이름입니다. 형식 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
 *base_type*  
 별칭 데이터 형식의 기반이 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제공된 데이터 형식입니다. *base_type*은 **sysname**이고 기본값은 없으며 다음 값 중 하나를 사용할 수 있습니다.  
  
|||||  
|-|-|-|-|  
|**bigint**|**binary(** *n* **)**|**bit**|**char(** *n* **)**|  
|**date**|**datetime**|**datetime2**|**datetimeoffset**|  
|**decimal**|**float**|**image**|**int**|  
|**money**|**nchar(** *n* **)**|**ntext**|**numeric**|  
|**nvarchar(** *n* &#124; **max)**|**real**|**smalldatetime**|**smallint**|  
|**smallmoney**|**sql_variant**|**text**|**time**|  
|**tinyint**|**uniqueidentifier**|**varbinary(** *n* &#124; **max)**|**varchar(** *n* &#124; **max)**|  
  
 *base_type*은 이러한 시스템 데이터 형식 중 하나에 매핑되는 데이터 형식 동의어도 될 수 있습니다.  
  
 *전체 자릿수*  
 **decimal** 또는 **numeric**에서 소수점 왼쪽과 오른쪽에 기록할 수 있는 십진수의 최대 수를 표시하는 음이 아닌 정수입니다. 자세한 내용은 [decimal 및 numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)을 참조하세요.  
  
 *scale*  
 **decimal** 또는 **numeric**에서 소수점 오른쪽에 기록할 수 있는 십진수의 최대 수를 표시하는 음이 아닌 정수이며 전체 자릿수보다 작거나 같아야 합니다. 자세한 내용은 [decimal 및 numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)을 참조하세요.  
  
 **NULL** | NOT NULL  
 해당 형식이 Null 값을 보관할 수 있는지 여부를 지정합니다. 이를 지정하지 않으면 기본값은 NULL입니다.  
  
 *assembly_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 공용 언어 런타임에서 사용자 정의 형식의 구현을 참조하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 어셈블리를 지정합니다. *assembly_name*은 현재 데이터베이스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 있는 기존 어셈블리와 일치해야 합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 EXTERNAL_NAME을 사용할 수 없습니다.  
  
 **[.** *class_name*  **]**  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 사용자 정의 형식을 구현하는 어셈블리 내 클래스를 지정합니다. *class_name*은 유효한 식별자여야 하며 어셈블리 표시 유형이 있는 어셈블리의 클래스로 존재해야 합니다. *class_name*은 데이터베이스의 데이터 정렬과 무관하게 대/소문자를 구분하며 해당 어셈블리의 클래스 이름과 정확히 일치해야 합니다. 클래스 작성에 사용되는 프로그래밍 언어가 C#과 같이 네임스페이스 개념을 사용하는 경우 클래스 이름이 대괄호( **[ ]** )로 묶은 정식 네임스페이스 이름이 될 수 있습니다. *class_name*을 지정하지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 *type_name*과 동일한 것으로 간주합니다.  
  
 \<column_definition>  
 사용자 정의 테이블 형식의 열을 정의합니다.  
  
 \<data type>  
 사용자 정의 테이블 형식에 대한 열의 데이터 형식을 정의합니다. 데이터 형식에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요. 테이블에 대한 자세한 내용은 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.  
  
 \<column_constraint>  
 사용자 정의 테이블 형식에 대한 열 제약 조건을 정의합니다. 지원되는 제약 조건은 PRIMARY KEY, UNIQUE 및 CHECK입니다. 테이블에 대한 자세한 내용은 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.  
  
 \<computed_column_definition>  
 계산 열 식을 사용자 정의 테이블 형식의 열로 정의합니다. 테이블에 대한 자세한 내용은 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.  
  
 \<table_constraint>  
 사용자 정의 테이블 형식의 테이블 제약 조건을 정의합니다. 지원되는 제약 조건은 PRIMARY KEY, UNIQUE 및 CHECK입니다.  
  
 \<index_option>  
 고유 클러스터형 또는 고유 비클러스터형 인덱스에 여러 행을 삽입하는 작업에서 중복된 키 값이 있는 경우에 대한 오류 응답을 지정합니다. 인덱스 옵션에 대한 자세한 내용은 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)을 참조하세요.  
 
  `INDEX *index_name* [ CLUSTERED | NONCLUSTERED ] (*column_name* [ ASC | DESC ] [ ,... *n* ] )`  
     
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

테이블에 인덱스를 만들도록 지정합니다. 이는 클러스터형 인덱스 또는 비클러스터형 인덱스일 수 있습니다. 인덱스는 나열된 열을 포함하며 데이터를 오름차순 또는 내림차순으로 정렬합니다.
  
 INDEX  
 CREATE TABLE 문의 일부로 열 및 테이블 인덱스를 지정해야 합니다. CREATE INDEX 및 DROP INDEX는 메모리 최적화 테이블에서 지원되지 않습니다.  
  
 MEMORY_OPTIMIZED  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 테이블 형식이 메모리 액세스에 최적화된 형식인지 여부를 나타냅니다. 이 옵션은 기본적으로 해제됩니다. 테이블(형식)은 메모리 액세스에 최적화된 테이블(형식)이 아닙니다. 메모리 최적화 테이블 형식은 메모리 최적화 사용자 테이블입니다. 디스크에 저장된 스키마는 다른 사용자 테이블과 비슷합니다.  
  
 BUCKET_COUNT  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 해시 인덱스에서 만들어야 하는 버킷 수를 나타냅니다. 해시 인덱스에서 BUCKET_COUNT의 최대값은 1,073,741,824입니다. 메모리 최적화 테이블의 인덱스에 대한 자세한 내용은 [Memory-Optimized Tables에 대한 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)를 참조하세요. *bucket_count*는 필수 인수입니다.  
  
 HASH  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 HASH 인덱스가 만들어졌음을 나타냅니다. 해시 인덱스는 메모리 액세스에 최적화된 테이블에서만 지원됩니다.  
  
## <a name="remarks"></a>설명  
 *assembly_name*에서 참조하는 어셈블리의 클래스는 클래스의 메서드와 함께 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자 정의 형식을 구현하기 위한 모든 요구 사항을 만족시켜야 합니다. 이러한 요구 사항에 대한 자세한 내용은 [CLR User-Defined Types](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)를 참조하세요.  
  
 추가적인 고려 사항은 다음과 같습니다.  
  
-   클래스는 오버로드된 메서드를 가질 수 있지만 [!INCLUDE[tsql](../../includes/tsql-md.md)]이 아닌 관리 코드 내부에서만 이런 메서드를 호출할 수 있습니다.  
  
-   *assembly_name*이 SAFE 또는 EXTERNAL_ACCESS인 경우에는 정적 멤버를 **const** 또는 **readonly**로 선언해야 합니다.  
  
 데이터베이스 내의 CLR에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 업로드하는 각 형식에 대한 사용자 정의 형식은 오직 하나만 등록할 수 있습니다. 데이터베이스에 사용자 정의 형식이 존재하는 CLR 형식에 대해 다시 사용자 정의 형식을 만드는 경우 CREATE TYPE에 오류가 발생하면서 실패합니다. 이런 제한은 CLR 형식을 둘 이상의 사용자 정의 형식에 매핑할 수 있는 경우 SQL 형식 확인 과정의 모호성을 피하기 위해 필요합니다.  
  
 해당 형식에 *void*를 반환하는 변경자(mutator) 메서드가 전혀 없으면 CREATE TYPE 문이 실행되지 않습니다.  
  
 사용자 정의 형식을 수정하려면 DROP TYPE 문을 사용하여 해당 형식을 삭제한 다음 다시 만들어야 합니다.  
  
 **public** 데이터베이스 역할은 **sp_addtype**을 사용하여 만든 사용자 정의 형식과는 달리 CREATE TYPE을 사용하여 만든 형식에 대해서는 자동으로 REFERENCES 권한을 받지 못합니다. 이 권한은 별도로 허가해야 합니다.  
  
 사용자 정의 테이블 형식의 경우 *column_name* \<data type>에서 사용하는 구조적 사용자 정의 형식은 해당 테이블 형식이 정의된 데이터베이스 스키마 범위의 일부입니다. 데이터베이스 내의 다른 범위에 있는 구조적 사용자 정의 형식에 액세스하려면 두 부분으로 된 이름을 사용하세요.  
  
 사용자 정의 테이블 형식에서 계산 열에 대한 기본 키는 PERSISTED 및 NOT NULL이어야 합니다.  
  
## <a name="memory-optimized-table-types"></a>메모리 액세스에 최적화된 테이블 형식  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 테이블 형식의 데이터 처리는 디스크가 아닌 기본 메모리에서 수행될 수 있습니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요. 메모리 최적화 테이블을 만드는 방법을 보여주는 코드 샘플은 [메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 현재 데이터베이스에 대한 CREATE TYPE 권한 및 *schema_name*에 대한 ALTER 권한이 필요합니다. *schema_name* 을 지정하지 않으면 현재 사용자에 대한 스키마를 결정하는 기본 이름 확인 규칙이 적용됩니다. *assembly_name*을 지정하면 사용자는 어셈블리나 그에 대한 REFERENCES 권한을 소유해야 합니다.  

 CREATE TABLE 문의 열이 사용자 정의 형식으로 정의되면 해당 형식에 대한 REFERENCES 권한이 필요합니다.
 
   >[!NOTE]
  > 사용자 정의 형식을 사용하는 열을 사용하여 테이블을 만드는 사용자는 사용자 정의 형식에 대한 REFERENCES 권한이 필요합니다.
  > 이 테이블을 TempDB에서 만들어야 할 경우 테이블을 만들기 **전**마다 REFERENCES 권한을 명시적으로 부여하거나 이 데이터 형식 및 REFERENCES 권한을 모델 데이터베이스에 추가해야 합니다. 작업을 실행하면 이 데이터 형식 및 사용 권한이 TempDB에서 영구적으로 지원됩니다. 그렇지 않으면 SQL Server를 다시 시작할 경우 사용자 정의 데이터 형식 및 사용 권한이 사라집니다. 자세한 내용은 [CREATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/create-table-transact-sql?view=sql-server-2017#permissions-1)을 참조하세요.
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-an-alias-type-based-on-the-varchar-data-type"></a>A. varchar 데이터 형식을 기반으로 별칭 유형 만들기  
 다음 예에서는 시스템이 제공하는 `varchar` 데이터 형식을 기반으로 별칭 유형을 만드는 방법을 보여 줍니다.  
  
```sql  
CREATE TYPE SSN  
FROM varchar(11) NOT NULL ;  
```  
  
### <a name="b-creating-a-user-defined-type"></a>B. 사용자 정의 형식 만들기  
 다음 예에서는 `utf8string` 어셈블리 내의 `utf8string`클래스를 참조하는 `Utf8String` 형식을 만드는 방법을 보여 줍니다. 형식을 만들기 전에 로컬 데이터베이스에 `utf8string` 어셈블리를 등록합니다. CREATE ASSEMBLY의 이진 부분을 올바른 유효한 설명으로 대체합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
```sql  
CREATE ASSEMBLY utf8string  
AUTHORIZATION [dbi]   
FROM 0x4D... ;  
GO  
CREATE TYPE Utf8String   
EXTERNAL NAME utf8string.[Microsoft.Samples.SqlServer.utf8string] ;  
GO  
```  
  
### <a name="c-creating-a-user-defined-table-type"></a>C. 사용자 정의 테이블 형식 만들기  
 다음 예에서는 두 개의 열이 있는 사용자 정의 테이블 형식을 만듭니다. 테이블 반환 매개 변수를 만들고 사용하는 방법은 [Use Table-Valued Parameters &#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)를 참조하세요.  
  
```sql  
CREATE TYPE LocationTableType AS TABLE   
    ( LocationName VARCHAR(50)  
    , CostRate INT );  
GO  
```  

### <a name="d-creating-a-user-defined-table-type-with-primary-key-and-index"></a>D. 기본 키와 인덱스를 사용하여 사용자 정의 테이블 형식 만들기
다음 예제에서는 세 개의 열이 있는 사용자 정의 테이블 형식을 만듭니다. `Name` 열에는 기본 키가 있고, 다른 `Price` 열에는 비클러스터형 인덱스가 있습니다.  테이블 반환 매개 변수를 만들고 사용하는 방법은 [Use Table-Valued Parameters &#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)를 참조하세요.

```sql
CREATE TYPE InventoryItem AS TABLE
(
    [Name] NVARCHAR(50) NOT NULL,
    SupplierId BIGINT NOT NULL,
    Price DECIMAL (18, 4) NULL,
    PRIMARY KEY (
        Name
    ),
    INDEX IX_InventoryItem_Price (
        Price
    )
)
GO
```
  
## <a name="see-also"></a>참고 항목  
 [CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)    
 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)     
 [SQL Server의 사용자 정의 형식 작업](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)     
  
