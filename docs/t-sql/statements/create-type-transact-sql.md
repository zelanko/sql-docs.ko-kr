---
title: "유형 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql13.swb.sysdatatype.properties.f1
- CREATE TYPE
- TYPE_TSQL
- TYPE
- CREATE_TYPE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- UDTs [SQL Server], creating
- CLR user-defined types [SQL Server]
- user-defined table types [SQL Server]
- user-defined types [SQL Server], creating
- CREATE TYPE statement
- alias data types [SQL Server], creating
- data types [SQL Server], creating
ms.assetid: 2202236b-e09f-40a1-bbc7-b8cff7488905
caps.latest.revision: "92"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 145f60bcec81e8a29761a44146df025f66a21b80
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="create-type-transact-sql"></a>CREATE TYPE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 현재 데이터베이스에 별칭 데이터 형식 또는 사용자 정의 형식을 만듭니다. 별칭 데이터 형식의 구현은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 시스템 형식을 기반으로 합니다. 사용자 정의 형식에 있는 어셈블리의 클래스를 통해 구현 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 공용 언어 런타임 (CLR). 사용자 정의 형식을 구현 바인딩할 형식의 구현을 포함 하는 CLR 어셈블리를 등록 해야에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR 코드 실행 기능이 기본적으로 해제되어 있습니다. 이러한 참조가 실행 되지 것입니다 수를 만들고 수정, 관리 코드 모듈을 참조 하는 데이터베이스 개체를 삭제 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우가 아니면는 [clr enabled 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) 사용 하 여 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
 
> [!NOTE]  
>  SQL Server의 통합의.NET Framework CLR은이 항목에서 설명 합니다. CLR 통합 Azure에 적용 되지 않습니다 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Disk-Based Type Syntax  
CREATE TYPE [ schema_name. ] type_name  
{   
    FROM base_type   
    [ ( precision [ , scale ] ) ]  
    [ NULL | NOT NULL ]   
  | EXTERNAL NAME assembly_name [ .class_name ]   
  | AS TABLE ( { <column_definition> | <computed_column_definition> }  
        [ <table_constraint> ] [ ,...n ] )    
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
```  
  
```  
-- Memory-Optimized Table Type Syntax  
CREATE TYPE [schema_name. ] type_name  
AS TABLE ( { <column_definition> }  
    |  [ <table_constraint> ] [ ,... n ]    
    | [ <table_index> ] [ ,... n ]    } )
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
 별칭 데이터 형식 또는 사용자 정의 형식의 이름입니다. 형식 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 *base_type*  
 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 별칭 데이터 형식의 기반이 되는 데이터 형식을 제공 합니다. *base_type* 은 **sysname**, 수 및 기본값은 없고 다음 값 중 하나일:  
  
|||||  
|-|-|-|-|  
|**bigint**|**이진 (**  *n*  **)**|**bit**|**char (**  *n*  **)**|  
|**date**|**datetime**|**datetime2**|**datetimeoffset**|  
|**decimal**|**float**|**image**|**int**|  
|**money**|**nchar (**  *n*  **)**|**ntext**|**numeric**|  
|**nvarchar (**  *n*  &#124; **최대)**|**real**|**smalldatetime**|**smallint**|  
|**smallmoney**|**sql_variant**|**text**|**time**|  
|**tinyint**|**uniqueidentifier**|**varbinary (**  *n*  &#124; **최대)**|**varchar (**  *n*  &#124; **최대)**|  
  
 *base_type* 이러한 시스템 데이터 형식 중 하나에 매핑되는 데이터 형식 동의어도 될 수 있습니다.  
  
 *전체 자릿수*  
 에 대 한 **10 진수** 또는 **숫자**, 왼쪽 및 소수점의 오른쪽에 저장할 수 있는 십진수의 최대 총 수를 나타내는 음수가 아닌 정수입니다. 자세한 내용은 참조 [decimal 및 numeric&#40; Transact SQL &#41; ](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *소수 자릿수*  
 에 대 한 **10 진수** 또는 **숫자**소수점의 오른쪽에 저장할 수 있는 십진수의 최대 수를 나타내는 음수가 아닌 정수 이며 전체 자릿수 보다 작거나 같은 이어야 합니다 . 자세한 내용은 참조 [decimal 및 numeric&#40; Transact SQL &#41; ](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 **NULL** | NOT NULL  
 해당 형식이 Null 값을 보관할 수 있는지 여부를 지정합니다. 이를 지정하지 않으면 기본값은 NULL입니다.  
  
 *assembly_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 지정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공용 언어 런타임에서 사용자 정의 형식의 구현을 참조 하는 어셈블리입니다. *assembly_name* 에 있는 기존 어셈블리와 일치 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 데이터베이스에 있습니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 EXTERNAL_NAME을 사용할 수 없습니다.  
  
 **[.** *class_name***]**   
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 사용자 정의 형식을 구현하는 어셈블리 내 클래스를 지정합니다. *class_name* 유효한 식별자 여야 하며 어셈블리 표시 유형이 있는 어셈블리에 클래스로 존재 해야 합니다. *class_name* 데이터베이스 데이터 정렬에 관계 없이 대/소문자 이며 해당 어셈블리의 클래스 이름과 정확히 일치 해야 합니다. 클래스 이름을 대괄호로 묶인 네임 스페이스로 한정 이름일 수 있습니다 (**[]**)는 클래스를 작성 하는 데 사용 되는 프로그래밍 언어는 C#과 같은 네임 스페이스의 개념을 사용 하는 경우. 경우 *class_name* 를 지정 하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 같은 것으로 간주 *type_name*합니다.  
  
 \<column_definition >  
 사용자 정의 테이블 형식의 열을 정의합니다.  
  
 \<데이터 형식 >  
 사용자 정의 테이블 형식에 대한 열의 데이터 형식을 정의합니다. 데이터 형식에 대 한 자세한 내용은 참조 [데이터 형식 &#40; Transact SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md). 테이블에 대 한 자세한 내용은 참조 [CREATE table&#40; Transact SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<column_constraint >  
 사용자 정의 테이블 형식에 대한 열 제약 조건을 정의합니다. 지원되는 제약 조건은 PRIMARY KEY, UNIQUE 및 CHECK입니다. 테이블에 대 한 자세한 내용은 참조 [CREATE table&#40; Transact SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<computed_column_definition >  
 계산 열 식을 사용자 정의 테이블 형식의 열로 정의합니다. 테이블에 대 한 자세한 내용은 참조 [CREATE table&#40; Transact SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<table_constraint >  
 사용자 정의 테이블 형식의 테이블 제약 조건을 정의합니다. 지원되는 제약 조건은 PRIMARY KEY, UNIQUE 및 CHECK입니다.  
  
 \<index_option >  
 고유 클러스터형 또는 고유 비클러스터형 인덱스에 여러 행을 삽입하는 작업에서 중복된 키 값이 있는 경우에 대한 오류 응답을 지정합니다. 인덱스 옵션에 대 한 자세한 내용은 참조 [CREATE index&#40; Transact SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 INDEX  
 CREATE TABLE 문의 일부로 열 및 테이블 인덱스를 지정해야 합니다. CREATE INDEX 및 DROP INDEX는 메모리 최적화 테이블에서 지원되지 않습니다.  
  
 MEMORY_OPTIMIZED  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 테이블 형식이 메모리 액세스에 최적화된 형식인지 여부를 나타냅니다. 이 옵션은 기본적으로 해제됩니다. 테이블(형식)은 메모리 액세스에 최적화된 테이블(형식)이 아닙니다. 메모리 최적화 테이블 형식은 메모리 최적화 사용자 테이블입니다. 디스크에 저장된 스키마는 다른 사용자 테이블과 비슷합니다.  
  
 BUCKET_COUNT  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 해시 인덱스에서 만들어야 하는 버킷 수를 나타냅니다. 해시 인덱스에서 BUCKET_COUNT의 최대값은 1,073,741,824입니다. 버킷 수에 대 한 자세한 내용은 참조 [메모리 최적화 된 테이블에 대 한 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)합니다. *bucket_count* 필수 인수입니다.  
  
 HASH  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 HASH 인덱스가 만들어졌음을 나타냅니다. 해시 인덱스는 메모리 액세스에 최적화된 테이블에서만 지원됩니다.  
  
## <a name="remarks"></a>주의  
 참조 되는 어셈블리의 클래스 *assembly_name*, 해당 메서드를 함께 사용자 정의 형식을 구현 하기 위한 모든 요구 사항을 만족 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이러한 요구 사항에 대 한 자세한 내용은 참조 [clr 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)합니다.  
  
 추가적인 고려 사항은 다음과 같습니다.  
  
-   클래스는 오버로드된 메서드를 가질 수 있지만 [!INCLUDE[tsql](../../includes/tsql-md.md)]이 아닌 관리 코드 내부에서만 이런 메서드를 호출할 수 있습니다.  
  
-   으로 모든 정적 멤버를 선언 해야 **const** 또는 **readonly** 경우 *assembly_name* 이 SAFE 또는 EXTERNAL_ACCESS 합니다.  
  
 데이터베이스 내의 CLR에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 업로드하는 각 형식에 대한 사용자 정의 형식은 오직 하나만 등록할 수 있습니다. 데이터베이스에 사용자 정의 형식이 존재하는 CLR 형식에 대해 다시 사용자 정의 형식을 만드는 경우 CREATE TYPE에 오류가 발생하면서 실패합니다. 이런 제한은 CLR 형식을 둘 이상의 사용자 정의 형식에 매핑할 수 있는 경우 SQL 형식 확인 과정의 모호성을 피하기 위해 필요합니다.  
  
 형식에 모든 변경자 (mutator) 메서드가 반환 하지 않는 경우 *void*, CREATE TYPE 문이 실행 되지 않습니다.  
  
 사용자 정의 형식을 수정하려면 DROP TYPE 문을 사용하여 해당 형식을 삭제한 다음 다시 만들어야 합니다.  
  
 사용 하 여 만들어진 사용자 정의 형식과 달리 **sp_addtype**, **공용** 데이터베이스 역할에 CREATE TYPE을 사용 하 여 만든 형식에 대 한 REFERENCES 권한이 자동으로 부여 됩니다. 이 권한은 별도로 허가해야 합니다.  
  
 구조적 사용자 정의 형식에 사용 되는 사용자 정의 테이블 형식에서 *column_name* \<데이터 형식 >는 테이블 형식이 정의 된 데이터베이스 스키마 범위의 일부입니다. 데이터베이스 내의 다른 범위에 있는 구조적 사용자 정의 형식에 액세스하려면 두 부분으로 된 이름을 사용하세요.  
  
 사용자 정의 테이블 형식에서 계산 열에 대한 기본 키는 PERSISTED 및 NOT NULL이어야 합니다.  
  
## <a name="memory-optimized-table-types"></a>메모리 액세스에 최적화된 테이블 형식  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 테이블 형식의 데이터 처리는 디스크가 아닌 기본 메모리에서 수행될 수 있습니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요. 메모리 액세스에 최적화 된 테이블 형식을 만드는 방법을 보여 주는 코드 샘플 [최적화 된 테이블 및 고유 하 게 컴파일된 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 현재 데이터베이스에 대한 CREATE TYPE 권한 및 *schema_name*에 대한 ALTER 권한이 필요합니다. *schema_name* 을 지정하지 않으면 현재 사용자에 대한 스키마를 결정하는 기본 이름 확인 규칙이 적용됩니다. 경우 *assembly_name* 지정은 사용자 어셈블리를 소유 하거나에 REFERENCES 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-an-alias-type-based-on-the-varchar-data-type"></a>1. varchar 데이터 형식을 기반으로 별칭 유형 만들기  
 다음 예에서는 시스템이 제공하는 `varchar` 데이터 형식을 기반으로 별칭 유형을 만드는 방법을 보여 줍니다.  
  
```  
CREATE TYPE SSN  
FROM varchar(11) NOT NULL ;  
```  
  
### <a name="b-creating-a-user-defined-type"></a>2. 사용자 정의 형식 만들기  
 다음 예제에서는 형식 `Utf8String` 클래스를 참조 하는 `utf8string` 어셈블리에서 `utf8string`합니다. 형식을 만들기 전에 로컬 데이터베이스에 `utf8string` 어셈블리를 등록합니다. CREATE ASSEMBLY의 이진 부분을 올바른 유효한 설명으로 대체합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
CREATE ASSEMBLY utf8string  
AUTHORIZATION [dbi]   
FROM 0x4D... ;  
GO  
CREATE TYPE Utf8String   
EXTERNAL NAME utf8string.[Microsoft.Samples.SqlServer.utf8string] ;  
GO  
```  
  
### <a name="c-creating-a-user-defined-table-type"></a>3. 사용자 정의 테이블 형식 만들기  
 다음 예에서는 두 개의 열이 있는 사용자 정의 테이블 형식을 만듭니다. 만들고 테이블 반환 매개 변수를 사용 하는 방법에 대 한 자세한 내용은 참조 [테이블 반환 매개 변수 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)합니다.  
  
```  
CREATE TYPE LocationTableType AS TABLE   
    ( LocationName VARCHAR(50)  
    , CostRate INT );  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [어셈블리 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [삭제 유형을 &#40; Transact SQL &#41;](../../t-sql/statements/drop-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
