---
title: "CREATE 함수 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FUNCTION
- CREATE FUNCTION
- CREATE_FUNCTION_TSQL
- FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- invoking functions
- extended stored procedures [SQL Server], functions
- table-valued parameters
- user-defined functions [SQL Server], creating
- CLR functions [SQL Server]
- CREATE FUNCTION statement
- nondeterministic functions
- user-defined data types
- functions [SQL Server], creating
- inline table-valued functions [SQL Server]
- multi-statement table-valued functions [SQL Server]
- table-valued functions [SQL Server], CREATE FUNCTION
- parameters [SQL Server], functions
- nesting user-defined functions
- deterministic functions
- scalar-valued functions
- functions [SQL Server], invoking
ms.assetid: 864b393f-225f-4895-8c8d-4db59ea60032
caps.latest.revision: 162
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: c74e3a3322dcc2268fa8e386fda5d55f59be98c5
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="create-function-transact-sql"></a>CREATE FUNCTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 사용자 정의 함수를 만듭니다. 사용자 정의 함수는 매개 변수를 허용하고 복잡한 계산 등의 동작을 수행하며 해당 동작의 결과를 값으로 반환하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CLR(공용 언어 런타임) 루틴입니다. 반환 값은 단일 스칼라 값이나 테이블일 수 있습니다. 이 문을 사용하여 다음과 같은 상황에서 다시 사용할 수 있는 루틴을 만들 수 있습니다.  
  
-   SELECT 등의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문  
  
-   함수를 호출하는 응용 프로그램  
  
-   다른 사용자 정의 함수의 정의  
  
-   뷰를 매개 변수화하거나 인덱싱된 뷰의 기능 향상  
  
-   테이블의 열 정의  
  
-   열에 CHECK 제약 조건 정의  
  
-   저장 프로시저 바꾸기  
  
-   인라인 함수를 필터 조건자로 사용 하 여 보안 정책에 대 한  
  
> [!NOTE]  
>  SQL Server의 통합의.NET Framework CLR은이 항목에서 설명 합니다. CLR 통합 Azure SQL 데이터베이스에 적용 되지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Transact-SQL Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
```  
  
```  
-- Transact-SQL Inline Table-Valued Function Syntax   
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
    [ ,...n ]  
  ]  
)  
RETURNS TABLE  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    RETURN [ ( ] select_stmt [ ) ]  
[ ; ]  
  
```  
  
```  
-- Transact-SQL Multi-Statement Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [READONLY] }   
    [ ,...n ]  
  ]  
)  
RETURNS @return_variable TABLE <table_type_definition>  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN  
    END  
[ ; ]  
  
```  

```  
-- Transact-SQL Function Clauses   
<function_option>::=   
{  
    [ ENCRYPTION ]  
  | [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<table_type_definition>:: =   
( { <column_definition> <column_constraint>   
  | <computed_column_definition> }   
    [ <table_constraint> ] [ ,...n ]  
)   
<column_definition>::=  
{  
    { column_name data_type }  
    [ [ DEFAULT constant_expression ]   
      [ COLLATE collation_name ] | [ ROWGUIDCOL ]  
    ]  
    | [ IDENTITY [ (seed , increment ) ] ]  
    [ <column_constraint> [ ...n ] ]   
}  
  
<column_constraint>::=   
{  
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      [ WITH FILLFACTOR = fillfactor   
        | WITH ( < index_option > [ , ...n ] )  
      [ ON { filegroup | "default" } ]  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<computed_column_definition>::=  
column_name AS computed_column_expression   
  
<table_constraint>::=  
{   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      ( column_name [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( <index_option> [ , ...n ] )  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<index_option>::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS ={ ON | OFF }   
}  
```  
  
```  
-- CLR Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  
  
```  
-- CLR Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS TABLE <clr_table_type_definition>   
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ ORDER ( <order_clause> ) ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  

```  
-- CLR Function Clauses  
<order_clause> ::=   
{  
   <column_name_in_clr_table_type_definition>  
   [ ASC | DESC ]   
} [ ,...n]   
  
<method_specifier>::=  
    assembly_name.class_name.method_name  
  
<clr_function_option>::=  
}  
    [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<clr_table_type_definition>::=   
( { column_name data_type } [ ,...n ] )  
  
```  
  
```  
-- In-Memory OLTP: Syntax for natively compiled, scalar user-defined function  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] [ READONLY ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
     WITH <function_option> [ ,...n ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])   
        function_body   
        RETURN scalar_expression  
    END  
  
<function_option>::=   
{  
  |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
  
```  
  
## <a name="arguments"></a>인수
*또는 변경*  
 **적용 대상**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).  
  
 이미 있는 경우에 함수를 조건에 따라 변경 합니다. 
 
> [!NOTE]  
>  선택적 [또는 ALTER]에 대 한 CLR 구문은 제공 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU1 합니다.   
 
 *schema_name*  
 사용자 정의 함수가 속한 스키마의 이름입니다.  
  
 *function_name*  
 사용자 정의 함수의 이름입니다. 함수 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md) 하며 데이터베이스 내에서 고유 해야 합니다.  
  
> [!NOTE]  
>  매개 변수를 지정하지 않은 경우에도 함수 이름 뒤에 괄호를 사용해야 합니다.  
  
 @*p a r a*  
 사용자 정의 함수의 매개 변수입니다. 하나 이상의 매개 변수를 선언할 수 있습니다.  
  
 하나의 함수에 최대 2,100개의 매개 변수를 지정할 수 있습니다. 매개 변수에 기본값이 정의되지 않은 경우 함수를 실행할 때 사용자가 선언된 각 매개 변수의 값을 지정해야 합니다.  
  
 at 기호(@)를 첫 번째 문자로 사용하여 매개 변수 이름을 지정합니다. 매개 변수 이름은 식별자에 대한 규칙을 따라야 합니다. 매개 변수는 함수에서 로컬로 사용되므로 다른 함수에서 동일한 매개 변수 이름을 사용할 수 있습니다. 매개 변수는 상수 대신 사용할 수 있지만 테이블 이름, 열 이름 또는 다른 데이터베이스 개체의 이름 대신 사용할 수는 없습니다.  
  
> [!NOTE]  
>  저장 프로시저나 사용자 정의 함수에 매개 변수를 전달할 때 또는 일괄 처리 문에서 변수를 선언하고 설정할 때 ANSI_WARNINGS는 인식되지 않습니다. 예를 들어, 변수로 정의 되 면 **char (3)**를 하 고 다음 값으로 설정 된 3 자 보다 큰 데이터 잘리고 정의 된 크기는 INSERT 또는 UPDATE 문이 성공 합니다.  
  
 [ *type_schema_name*합니다. ] *parameter_data_type*  
 매개 변수 데이터 형식이며 매개 변수 데이터 형식이 속한 스키마가 될 수도 있습니다. 에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 제외한 함수, CLR 사용자 정의 형식 및 사용자 정의 테이블 형식을 비롯 한 모든 데이터 형식에 사용할 수 있습니다는 **타임 스탬프** 데이터 형식입니다. CLR 함수에 대 한 CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에는 제외 하 고 허용 **텍스트**, **ntext**, **이미지**, 사용자 정의 테이블 형식 및  **타임 스탬프** 데이터 형식입니다. 비스칼라 형식 **커서** 및 **테이블**에서 매개 변수 데이터 형식으로 지정할 수 없습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CLR 함수.  
  
 경우 *type_schema_name* 를 지정 하지 않으면는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 찾습니다는 *scalar_parameter_data_type* 다음과 같은 순서로:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식의 이름이 포함된 스키마  
  
-   현재 데이터베이스에 있는 현재 사용자의 기본 스키마  
  
-   현재 데이터베이스의 **dbo** 스키마  
  
 [=*기본* ]  
 매개 변수의 기본값입니다. 경우는 *기본* 값이 정의 해당 매개 변수에 대해 값을 지정 하지 않고 함수를 실행할 수 있습니다.  
  
> [!NOTE]  
>  기본 매개 변수 값을 제외 하 고 CLR 함수에 지정할 수 있습니다는 **varchar (max)** 및 **varbinary (max)** 데이터 형식입니다.  
  
 함수의 매개 변수에 기본값을 지정한 경우 기본값을 가져오는 함수를 호출할 때 DEFAULT 키워드를 지정해야 합니다. 이 동작은 매개 변수를 생략할 경우 자동으로 기본값이 사용되는 저장 프로시저에서 기본값이 있는 매개 변수를 사용하는 것과는 다릅니다. 그러나 DEFAULT 키워드는 EXECUTE 문을 사용하여 스칼라 함수를 호출할 때 필요하지 않습니다.  
  
 READONLY  
 함수 정의 내에서 매개 변수를 업데이트하거나 수정할 수 없음을 나타냅니다. 매개 변수 유형이 사용자 정의 테이블 형식인 경우 READONLY를 지정해야 합니다.  
  
 *return_data_type*  
 스칼라 사용자 정의 함수의 반환 값입니다. 에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 제외한 함수, CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에 사용할 수 있습니다는 **타임 스탬프** 데이터 형식입니다. CLR 함수의 경우 CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에 제외 하 고 허용 되는 **텍스트**, **ntext**, **이미지**, 및 **타임 스탬프**데이터 형식입니다. 비스칼라 형식 **커서** 및 **테이블**는 반환 데이터 형식으로 지정할 수 없습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CLR 함수.  
  
 *function_body*  
 테이블을 수정하는 경우처럼 함께 사용해도 부작용이 나타나지 않으며 함수의 값을 정의하는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지정합니다. *function_body* 스칼라 함수와 다중 문 테이블 반환 함수 에서만 사용 됩니다.  
  
 스칼라 함수에서 *function_body* 는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함께 스칼라 값으로 계산 하는 문입니다.  
  
 다중 문 테이블 반환 함수에서 *function_body* 는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블을 채우는 하는 문은 변수를 반환 합니다.  
  
 *scalar_expression*  
 스칼라 함수가 반환하는 스칼라 값을 지정합니다.  
  
 TABLE  
 테이블 반환 함수의 반환 값이 테이블임을 지정합니다. 상수 및 @*local_variables* 테이블 반환 함수에 전달 될 수 있습니다.  
  
 인라인 테이블 반환 함수에서 TABLE 반환 값은 단일 SELECT 문을 통해 정의됩니다. 인라인 함수에는 연관된 반환 변수가 없습니다.  
  
 다중 문 테이블 반환 함수에서 @*return_variable* 은 TABLE 변수를 저장 하 고 함수의 값으로 반환 되어야 하는 행이 누적 하는 데 사용 합니다. @*return_variable* 에 대해서만 지정할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 및 CLR에 대해 작동 합니다.  
  
> [!WARNING]  
>  다중 문 테이블 반환 함수는 **FROM** 절은 가능 하지만 성능 저하를 제공할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다중 문 함수에 포함할 수 있는 일부 문에 대해 결과적으로 만족스럽지 못한 쿼리 계획이 생성되는 최적화된 일부 기술은 사용할 수 없습니다. 최상의 성능을 얻으려면 가능한 경우 기본 테이블 간에 함수 대신 조인을 사용합니다.  
  
 *select_stmt*  
 인라인 테이블 반환 함수의 반환 값을 정의하는 단일 SELECT 문입니다.  
  
 순서 (\<order_clause >) 결과 테이블 반환 함수에서 반환 되는 순서를 지정 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "정렬 순서 사용에 대한 지침" 섹션을 참조하세요.  
  
 외부 이름 \<method_specifier > *assembly_name*. *class_name*. *method_name* **적용할**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.  
  
 만든 함수 이름에서 참조할 어셈블리 및 메서드를 지정합니다.  
  
-   *assembly_name* -값과 일치 해야 합니다는 `name` 의 열   
    `SELECT * FROM sys.assemblies;`을 참조하세요.  
    이 이름은 `CREATE ASSEMBLY` 문에 사용된 이름입니다.  
  
-   *class_name* -값과 일치 해야 합니다는 `assembly_name` 의 열  
    `SELECT * FROM sys.assembly_modules;`을 참조하세요.  
    흔히 이 값은 마침표 또는 점을 포함합니다. 이러한 경우는 TRANSACT-SQL 구문 해야 대괄호, 쌍과 또는 큰따옴표 쌍과 함께 값 제한 되어야 ""입니다.  
  
-   *method_name* -값과 일치 해야 합니다는 `method_name` 의 열   
    `SELECT * FROM sys.assembly_modules;`을 참조하세요.  
    메서드는 정적이어야 합니다.  
  
 일반적인 예에서 모든 형식이 MyFood 네임스페이스에 있는 MyFood.DLL의 경우 `EXTERNAL NAME` 값은 다음과 같을 수 있습니다.   
`MyFood.[MyFood.MyClass].MyStaticMethod`  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR 코드를 실행할 수 없습니다. 만들기, 수정 및 공용 언어 런타임 모듈; 참조 하는 데이터베이스 개체를 삭제 합니다. 그러나 이러한 참조를 실행할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정할 때까지 [clr enabled 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)합니다. 이 옵션을 사용 하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 *\<*table_type_definition *>*  ({ \<column_definition > \<column_constraint > | \<computed_column_definition >}    [ \<table_constraint >] [,...  *n*  ]) 테이블 데이터에 대 한 형식 정의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수입니다. 테이블 선언에는 열 정의와 열 또는 테이블 제약 조건이 포함됩니다. 테이블은 항상 주 파일 그룹에 포함됩니다.  
  
 \<clr_table_type_definition > ({ *column_name**data_type* } [,...  *n*  ]) **적용할**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([일부 지역에서는 미리 보기](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)). |  
  
 CLR 함수에 대한 테이블 데이터 형식을 정의합니다. 테이블 선언에는 열 이름과 데이터 형식만 포함됩니다. 테이블은 항상 주 파일 그룹에 포함됩니다.  
  
 NULL | NOT NULL  
 고유 하 게 컴파일된 스칼라 사용자 정의 함수에 대해서만 지원 합니다. 자세한 내용은 참조 [메모리 내 OLTP에 대 한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)합니다.  
  
 NATIVE_COMPILATION  
 사용자 정의 함수를 고유 하 게 컴파일되어 있는지 여부를 나타냅니다. 이 인수는 고유 하 게 컴파일된 스칼라 사용자 정의 함수에 필요 합니다.  
  
 BEGIN ATOMIC와  
 고유 하 게 컴파일된 사용자 정의 스칼라 함수 이며 필수만 지원 합니다. 자세한 내용은 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)을(를) 참조하십시오.  
  
 SCHEMABINDING  
 SCHEMABINDING 인수는 고유 하 게 컴파일된 스칼라 사용자 정의 함수에 필요 합니다.  
  
 EXECUTE AS  
 EXECUTE AS가 고유 하 게 컴파일된 스칼라 사용자 정의 함수에 대 한 필요 합니다.  
  
 **\<function_option >:: = 및 \<clr_function_option >:: =** 
  
 함수에 다음 옵션 중 하나 이상이 포함되도록 지정합니다.  
  
 ENCRYPTION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 CREATE FUNCTION 문의 원본 텍스트가 알아보기 어려운 형식으로 변환됨을 나타냅니다. 변조된 출력은 카탈로그 뷰 어디에서도 직접 표시되지 않습니다. 시스템 테이블 또는 데이터베이스 파일에 대한 액세스 권한이 없는 사용자는 변조된 텍스트를 검색할 수 없습니다. 그러나 텍스트를 통해 시스템 테이블에 액세스 하거나 수 있는 권한이 있는 사용자에 게 제공 됩니다는 [DAC 포트](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) 또는 데이터베이스 파일에 직접 액세스 합니다. 또한 디버거를 서버 프로세스에 연결할 수 있는 사용자는 런타임에 메모리에서 원래 프로시저를 검색할 수 있습니다. 시스템 메타 데이터에 액세스 하는 방법에 대 한 자세한 내용은 참조 [메타 데이터 표시 유형 구성은](../../relational-databases/security/metadata-visibility-configuration.md)합니다.  
  
 이 옵션을 사용하면 함수가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제의 일부로 게시되는 것을 방지할 수 있습니다. CLR 함수에는 이 옵션을 지정할 수 없습니다.  
  
 SCHEMABINDING  
 함수를 함수가 참조하는 데이터베이스 개체에 바인딩되도록 지정합니다. SCHEMABINDING을 지정하면 함수 정의에 영향을 미치는 방식으로 기본 개체를 수정할 수 없습니다. 함수 정의 자체를 먼저 수정하거나 삭제하여 수정할 개체에 대한 종속성을 제거해야 합니다.  
  
 다음 동작 중 하나만 발생해도 참조하는 개체에 대한 함수 바인딩이 제거됩니다. 
  
-   함수가 삭제된 경우  
  
-   SCHEMABINDING 옵션을 지정하지 않은 상태에서 ALTER 문을 사용하여 함수를 수정한 경우  
  
 다음 조건을 만족하는 경우에만 함수가 스키마에 바인딩될 수 있습니다.  
  
-   함수가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수입니다.  
  
-   사용자 정의 함수와 함수가 참조하는 뷰도 스키마에 바인딩되어야 합니다.  
  
-   함수가 참조하는 개체가 두 부분으로 구성된 이름을 사용하여 참조되어야 합니다.  
  
-   함수와 함수가 참조하는 개체가 동일한 데이터베이스에 속해야 합니다.  
  
-   CREATE FUNCTION 문을 실행한 사용자는 해당 함수가 참조하는 데이터베이스 개체에 대한 REFERENCES 권한이 있어야 합니다.  
  
 NULL 입력 시 NULL 반환 | **NULL 입력에 대해 호출**  
 지정 된 **OnNULLCall** 특성 스칼라 반환 함수입니다. 이 특성을 지정하지 않으면 기본적으로 CALLED ON NULL INPUT이 적용됩니다. 즉, 인수로 NULL이 전달되는 경우에도 함수 본문이 실행됩니다.  
  
 CLR 함수에 RETURNS NULL ON NULL INPUT을 지정할 경우 받은 인수 중 하나라도 NULL이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 실제로 함수의 본문을 호출하지 않고 NULL을 반환할 수 있습니다. 에 지정 된 메서드는 CLR 함수의 경우 \<method_specifier > RETURNS NULL ON NULL input을 사용자 지정 특성에 이미 있지만 CREATE FUNCTION 문을 나타냅니다 ON NULL INPUT을 수행 하는 CREATE FUNCTION 문 우선 순위입니다. **OnNULLCall** CLR 테이블 반환 함수에 대 한 특성을 지정할 수 없습니다. 
  
 EXECUTE AS 절  
 사용자 정의 함수가 실행되는 보안 컨텍스트를 지정합니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 함수가 참조하는 데이터베이스 개체에 대한 사용 권한을 확인하는 데 사용할 사용자 계정을 제어할 수 있습니다.  
  
> [!NOTE]  
>  인라인 사용자 정의 함수에는 EXECUTE AS를 지정할 수 없습니다.  
  
 자세한 내용은 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요.  
  
 **\<column_definition >:: =** 
  
 테이블 데이터 형식을 정의합니다. 테이블 선언에는 열 정의와 제약 조건이 포함됩니다. CLR 함수의 경우만 *column_name* 및 *data_type* 지정할 수 있습니다.  
  
 *column_name*  
 테이블에 있는 열 이름입니다. 열 이름은 식별자에 대한 규칙을 따라야 하며 테이블에서 고유해야 합니다. *column_name* 1-128 자로 구성 될 수 있습니다.  
  
 *data_type*  
 열 데이터 형식을 지정합니다. 에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 제외한 함수, CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에 사용할 수 있습니다 **타임 스탬프**합니다. CLR 함수에 대 한 CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에는 제외 하 고 허용 **텍스트**, **ntext**, **이미지**, **char**, **varchar**, **varchar (max)**, 및 **타임 스탬프**합니다. 스칼라가 아닌 형식 **커서** 중 하나에서 열 데이터 형식으로 지정할 수 없습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CLR 함수.  
  
 기본 *constant_expression*  
 삽입 중에 값이 명시적으로 지정되지 않은 경우에 열에 대해 제공되는 값을 지정합니다. *constant_expression* 상수, NULL 또는 시스템 함수 값입니다. DEFAULT 정의는 IDENTITY 속성을 갖는 열을 제외한 모든 열에 적용할 수 있습니다. CLR 테이블 반환 함수에는 DEFAULT를 지정할 수 없습니다.  
  
 COLLATE *데이터 정렬 이름*  
 열에 대한 데이터 정렬을 지정합니다. 이를 지정하지 않으면 열에 데이터베이스의 기본 데이터 정렬이 할당됩니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 참조의 목록 및 데이터 정렬에 대 한 자세한 내용은 [Windows 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) 및 [SQL Server 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 열에 대해서만 되는 데이터 정렬을 변경 하려면 COLLATE 절을 사용할 수는 **char**, **varchar**, **nchar**, 및 **nvarchar** 데이터 형식입니다.  
  
 CLR 테이블 반환 함수에는 COLLATE를 지정할 수 없습니다.  
  
 ROWGUIDCOL  
 새 열이 행 GUID(Globally Unique Identifier) 열임을 나타냅니다. 하나의 **uniqueidentifier** 테이블당 열 ROWGUIDCOL 열으로 지정 될 수 있습니다. ROWGUIDCOL 속성에만 할당할 수는 **uniqueidentifier** 열입니다.  
  
 ROWGUIDCOL 속성은 열에 저장된 값이 고유하도록 강제 적용하지 않습니다. 또한 테이블에 삽입된 새 행에 대한 값을 자동으로 생성하지도 않습니다. 각 열에 대해 고유한 값을 생성하려면 INSERT 문에 NEWID 함수를 사용하세요. 기본값을 지정할 수 있지만 NEWID는 기본값으로 지정할 수 없습니다.  
  
 IDENTITY  
 새 열이 ID 열임을 나타냅니다. 테이블에 새 행이 추가되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 열에 대해 고유한 증가값을 제공합니다. ID 열은 일반적으로 PRIMARY KEY 제약 조건과 함께 사용되어 테이블에 대한 고유한 행 식별자 역할을 합니다. IDENTITY 속성에 지정할 수 **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)**, 또는 **numeric(p,0)** 열입니다. ID 열은 테이블당 하나만 만들 수 있습니다. ID 열에는 바인딩된 기본값 및 DEFAULT 제약 조건을 사용할 수 없습니다. 둘 다 지정 해야 합니다는 *시드* 및 *증분* 하거나 둘 다 합니다. 둘 다 지정하지 않은 경우에는 기본값 (1,1)이 사용됩니다.  
  
 CLR 테이블 반환 함수에는 IDENTITY를 지정할 수 없습니다.  
  
 *시드*  
 테이블의 첫 번째 행에 할당되는 정수 값입니다.  
  
 *증가값*  
 정수 값을 추가 하는 *시드* 테이블의 연속 된 행에 대 한 값입니다.  
  
 **\<column_constraint >:: = 및 \< table_constraint >:: =** 
  
 지정된 열 또는 테이블에 대한 제약 조건을 정의합니다. CLR 함수의 경우 NULL 유형의 제약 조건만 허용됩니다. 명명된 제약 조건도 허용되지 않습니다.  
  
 NULL | NOT NULL  
 열의 Null 값 허용 여부를 결정합니다. NULL은 엄격하게 말해 제약 조건이 아니지만 NOT NULL처럼 지정할 수 있습니다. CLR 테이블 반환 함수에는 NOT NULL을 지정할 수 없습니다.  
  
 PRIMARY KEY  
 지정한 열에 대해 고유 인덱스를 통해 엔터티 무결성을 적용하는 제약 조건입니다. 테이블 반환 사용자 정의 함수에서 테이블당 하나의 열에만 PRIMARY KEY 제약 조건을 만들 수 있습니다. CLR 테이블 반환 함수에는 PRIMARY KEY를 지정할 수 없습니다.  
  
 UNIQUE  
 지정한 열에 대해 고유 인덱스를 통해 엔터티 무결성을 적용하는 제약 조건입니다. 하나의 테이블이 여러 개의 UNIQUE 제약 조건을 가질 수 있습니다. CLR 테이블 반환 함수에는 UNIQUE를 지정할 수 없습니다.  
  
 CLUSTERED | NONCLUSTERED  
 PRIMARY KEY 또는 UNIQUE 제약 조건에 대해 클러스터형 또는 비클러스터형 인덱스를 만들도록 지정합니다. PRIMARY KEY 제약 조건은 CLUSTERED를 사용하고 UNIQUE 제약 조건은 NONCLUSTERED를 사용합니다.  
  
 CLUSTERED는 하나의 제약 조건에 대해서만 지정할 수 있습니다. UNIQUE 제약 조건에 대해 CLUSTERED를 지정하고 PRIMARY KEY 제약 조건도 지정한 경우 PRIMARY KEY는 NONCLUSTERED를 사용합니다.  
  
 CLR 테이블 반환 함수에는 CLUSTERED 및 NONCLUSTERED를 지정할 수 없습니다.  
  
 CHECK  
 열에 입력 가능한 값을 제한하여 도메인 무결성을 적용하는 제약 조건입니다. CLR 테이블 반환 함수에는 CHECK 제약 조건을 지정할 수 없습니다.  
  
 *logical_expression*  
 TRUE 또는 FALSE를 반환하는 논리 식입니다.  
  
 **\<computed_column_definition >:: =**  
  
 계산 열을 지정합니다. 계산된 열에 대 한 자세한 내용은 참조 하세요. [CREATE table&#40; Transact SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 *column_name*  
 계산 열의 이름입니다.  
  
 *computed_column_expression*  
 계산 열의 값을 정의하는 식입니다.  
  
 **\<index_option >:: =**  
  
 PRIMARY KEY 또는 UNIQUE 인덱스에 대한 인덱스 옵션을 지정합니다. 인덱스 옵션에 대 한 자세한 내용은 참조 [CREATE index&#40; Transact SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = {ON | **OFF** }  
 인덱스 패딩을 지정합니다. 기본값은 OFF입니다.  
  
 FILLFACTOR = *fillfactor*  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 인덱스 생성 또는 변경 중에 각 인덱스 페이지의 리프 수준에 대한 채우기 정도를 나타내는 비율을 지정합니다. *fillfactor* 100 1 까지의 정수 값 이어야 합니다. 기본값은 0입니다.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려는 경우에 대한 오류 응답을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. 기본값은 OFF입니다.  
  
 STATISTICS_NORECOMPUTE = {ON | **OFF** }  
 배포 통계를 다시 계산할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ALLOW_ROW_LOCKS = { **ON** | OFF}  
 행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ALLOW_PAGE_LOCKS = { **ON** | OFF}  
 페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 SCHEMABINDING 절을 사용하여 사용자 정의 함수를 만들지 않은 경우 기본 개체에 대한 변경 내용이 함수의 정의에 영향을 주어 함수가 호출될 대 예기치 않은 결과를 초래할 수 있습니다. 기본 개체에 대한 변경으로 인해 함수가 최신 상태를 유지하지 못하게 되는 일이 발생하지 않도록 다음 메서드 중 하나를 구현하는 것이 좋습니다.  
  
-   함수를 만들 때 WITH SCHEMABINDING 절을 지정합니다. 이렇게 하면 함수도 수정되지 않는 한 함수 정의에서 참조된 개체를 수정할 수 없습니다.  
  
-   실행 된 [sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md) 함수 정의에 지정 된 모든 개체를 수정한 후 저장 프로시저입니다.  
  
## <a name="data-types"></a>데이터 형식  
 CLR 함수, 매개 변수를 지정 하는 경우 되어야 할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대해 이전에 정의 된 형식은 형식을 *scalar_parameter_data_type*합니다. 비교에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 CLR 통합 데이터 형식 또는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 공용 언어 런타임 데이터 형식 참조 [CLR 매개 변수 데이터 매핑](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)합니다.  
  
 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 표시 된 메서드는 클래스에서 오버 로드 될 때 올바른 메서드를 참조 하려면 \<method_specifier >는 다음과 같은 특징이 있어야 합니다. 
  
-   에 지정 된 대로 매개 변수 수가 같은 수신 [,... *n* ].  
  
-   참조가 아닌 값을 기준으로 모든 매개 변수를 받습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 함수에 지정된 유형과 호환되는 매개 변수 유형을 사용합니다.  
  
 CLR 함수의 반환 데이터 형식에서 메서드의 반환 데이터 형식이 테이블 유형 (RETURNS TABLE)을 지정 하는 경우 \<method_specifier > 형식 이어야 합니다 **IEnumerator** 또는 **IEnumerable**, 함수를 만든이가 인터페이스를 구현 하는 가정 합니다. 와 달리 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, CLR 함수에는 PRIMARY KEY, UNIQUE 또는 CHECK 제약 조건에 포함할 수 없습니다 \<table_type_definition > 합니다. 에 지정 된 열의 데이터 형식을 \<table_type_definition >의 메서드에 의해 반환 된 결과 집합의 해당 열 형식과 일치 해야 합니다 \<method_specifier > 실행 시. 함수를 만들 때는 이러한 형식 확인이 수행되지 않습니다. 
  
 CLR 함수 프로그래밍 하는 방법에 대 한 자세한 내용은 참조 [clr 사용자 정의 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 스칼라 반환 함수는 스칼라 식이 사용되는 위치에서 호출할 수 있습니다. 여기에는 계산 열 및 CHECK 제약 조건 정의가 포함됩니다. 스칼라 반환 함수를 사용 하 여 실행할 수 있습니다는 [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) 문. 스칼라 반환 함수는 적어도 두 부분으로 구성된 함수 이름을 사용하여 호출해야 합니다. 다중 부분 이름에 대 한 자세한 내용은 참조 하십시오. [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 테이블 반환 함수는 SELECT, INSERT, UPDATE 또는 DELETE 문 FROM 절의 테이블 식이 허용되는 위치에서 호출할 수 있습니다. 자세한 내용은 참조 [실행 사용자 정의 함수](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)합니다.  
  
## <a name="interoperability"></a>상호 운용성  
 함수에서 유효한 문은 다음과 같습니다.  
  
-   대입 문  
  
-   TRY...CATCH 문을 제외한 흐름 제어 문  
  
-   로컬 데이터 변수 및 로컬 커서를 정의하는 DECLARE 문  
  
-   지역 변수에 값을 할당하는 식이 있는 SELECT 목록이 포함된 SELECT 문  
  
-   함수에서 커서 선언, 열기, 닫기, 할당 취소 등 로컬 커서를 참조하는 커서 작업. INTO 절을 사용하여 지역 변수에 값을 할당하는 FETCH 문만 허용되며 클라이언트에게 데이터를 반환하는 FETCH 문은 허용되지 않습니다.  
  
-   지역 테이블 변수를 수정하는 INSERT, UPDATE 및 DELETE 문  
  
-   확장 저장 프로시저를 호출하는 EXECUTE 문  
  
-   자세한 내용은 참조 [만들 사용자 정의 함수 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)합니다.  
  
### <a name="computed-column-interoperability"></a>계산된 열 상호 운용성  
 함수는 다음 속성을 가집니다. 이러한 속성의 값은 지속 또는 인덱싱할 수 있는 계산 열에 함수를 사용할 수 있는지 여부를 결정합니다.  
  
|속성|Description|참고|  
|--------------|-----------------|-----------|  
|**IsDeterministic**|함수가 결정적 또는 비결정적입니다.|결정적 함수에서는 로컬 데이터 액세스가 허용됩니다. 예를 들어 동일한 데이터베이스 상태에서 특정 입력 값 집합을 사용하여 호출할 때 항상 동일한 결과를 반환하는 함수는 결정적인 함수입니다.|  
|**IsPrecise**|함수는 정확하거나 정확하지 않습니다.|정확하지 않은 함수에는 부동 소수점 연산과 같은 연산이 포함됩니다.|  
|**IsSystemVerified**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 함수의 정확성 및 결정성 속성을 확인할 수 있습니다.||  
|**SystemDataAccess**|로컬 인스턴스에서 시스템 데이터 (시스템 카탈로그 또는 가상 시스템 테이블)을 액세스 하는 함수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.||  
|**UserDataAccess**|함수가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 인스턴스의 사용자 데이터에 액세스합니다.|사용자 정의 테이블 및 임시 테이블은 포함되고 테이블 변수는 포함되지 않습니다.|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수의 정확성 및 결정성 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동으로 결정됩니다. CLR 함수의 데이터 액세스 및 결정성 속성은 사용자가 지정할 수 있습니다. 자세한 내용은 참조 [개요 CLR 통합 사용자 지정 특성의](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)합니다.  
  
 이러한 속성에 대 한 현재 값을 표시 하려면 사용 [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md)합니다.  
  
 함수가 결정적이려면 스키마 바인딩으로 생성해야 합니다.  
  
 사용자 정의 함수를 호출하는 계산 열은 사용자 정의 함수가 다음 속성 값을 가질 경우 인덱스에 사용할 수 있습니다.  
  
-   **IsDeterministic** = true  
  
-   **IsSystemVerified** = true (아닌 경우 계산된 열이 persisted)  
  
-   **UserDataAccess** = false  
  
-   **SystemDataAccess** = false  
  
 자세한 내용은 [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md)을 참조하세요.  
  
### <a name="calling-extended-stored-procedures-from-functions"></a>함수에서 확장 저장 프로시저 호출  
 함수 내부에서 호출된 확장 저장 프로시저는 클라이언트에 결과 집합을 반환할 수 없습니다. 클라이언트에 결과 집합을 반환하는 모든 ODS API는 FAIL을 반환하게 됩니다. 확장 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 다시 연결할 수 있지만 확장 저장 프로시저를 호출한 함수와 같은 트랜잭션에 조인하려고 시도해서는 안 됩니다.  
  
 일괄 처리나 저장 프로시저에서 호출하는 경우와 마찬가지로 확장 저장 프로시저도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행되고 있는 Windows 보안 계정의 컨텍스트 내에서 실행됩니다. 저장 프로시저의 소유자는 사용자에게 EXECUTE 권한을 부여할 때 이 점을 고려해야 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 사용자 정의 함수는 데이터베이스 상태 수정 동작을 수행하는 데 사용할 수 없습니다.  
  
 사용자 정의 함수에는 테이블이 대상인 OUTPUT INTO 절을 포함할 수 없습니다.  
  
 다음 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수에 포함될 수 없습니다.  
  
-   BEGIN DIALOG CONVERSATION  
  
-   END CONVERSATION  
  
-   GET CONVERSATION GROUP  
  
-   MOVE CONVERSATION  
  
-   RECEIVE  
  
-   SEND  
  
 사용자 정의 함수는 중첩될 수 있습니다. 즉, 하나의 사용자 정의 함수가 다른 사용자 정의 함수를 호출할 수 있습니다. 중첩 수준은 호출된 함수의 실행이 시작되면 늘어나고 호출된 함수의 실행이 끝나면 줄어듭니다. 사용자 정의 함수는 최대 32 수준까지 중첩될 수 있습니다. 최대 중첩 수준을 초과하면 전체 함수 호출 체인이 실패합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수의 관리 코드 참조는 32 수준의 중첩 제한에 대해 한 수준으로 계산됩니다. 관리 코드 내에서 호출된 메서드는 이 제한에 따라 계산되지 않습니다.  
  
### <a name="using-sort-order-in-clr-table-valued-functions"></a>CLR 테이블 반환 함수에서 정렬 순서 사용  
 CLR 테이블 반환 함수에서 ORDER 절을 사용할 때는 다음 지침을 따르세요.  
  
-   결과가 항상 지정된 순서로 정렬되도록 해야 합니다. 결과가 지정된 순서로 되어 있지 않으면 쿼리가 실행될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류 메시지가 발생합니다.  
  
-   ORDER 절이 지정된 경우 테이블 반환 함수의 출력은 열의 데이터 정렬(명시적 또는 암시적)에 따라 정렬되어야 합니다. 예를 들어 열 데이터 정렬이 중국어(테이블 반환 함수의 DDL에 지정하거나 데이터베이스 데이터 정렬로부터 가져옴)인 경우 반환되는 결과는 중국어 정렬 규칙에 따라 정렬되어야 합니다.  
  
-   ORDER 절이 지정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 결과를 반환하는 동안 항상 쿼리 프로세서에서 추가 최적화를 수행하기 위해 ORDER 절을 사용할지 여부를 확인합니다. 쿼리 프로세서에 유용한 경우에만 ORDER 절을 사용하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 프로세서는 다음과 같은 경우에 ORDER 절을 자동으로 활용합니다.  
  
    -   ORDER 절이 인덱스와 호환되는 삽입 쿼리  
  
    -   ORDER 절과 호환되는 ORDER BY 절  
  
    -   GROUP BY가 ORDER 절과 호환되는 집계  
  
    -   고유 열이 ORDER 절과 호환되는 DISTINCT 집계  
  
 SELECT 쿼리에도 ORDER BY를 지정하고 쿼리를 실행해야 ORDER 절에서 정렬된 결과를 얻을 수 있습니다. 참조 [sys.function_order_columns &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-function-order-columns-transact-sql.md) 테이블 반환 함수에 대 한 정렬 순서에 포함 된 열에 대 한 쿼리 하는 방법에 대 한 내용은 합니다.  
  
## <a name="metadata"></a>메타데이터  
 다음 표에서는 사용자 정의 함수에 대한 메타데이터를 반환하는 데 사용할 수 있는 시스템 카탈로그 뷰를 나열합니다.  
  
|시스템 뷰|Description|  
|-----------------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|아래 예 섹션에서 예를 참조 하십시오.|  
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|CLR 사용자 정의 함수에 대한 정보를 표시합니다.|  
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|사용자 정의 함수에 정의된 매개 변수에 대한 정보를 표시합니다.|  
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)|함수에서 참조하는 기본 개체를 표시합니다.|  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CREATE FUNCTION 권한과 함수가 생성되는 스키마에 대한 ALTER 권한이 필요합니다. 함수에 사용자 정의 형식이 지정되면 해당 유형에 대한 EXECUTE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-a-scalar-valued-user-defined-function-that-calculates-the-iso-week"></a>1. ISO 주를 계산하는 스칼라 반환 사용자 정의 함수 사용  
 다음 예에서는 사용자 정의 함수 `ISOweek`를 만듭니다. 이 함수는 날짜 인수를 사용하여 ISO 주 번호를 계산합니다. 이 함수가 계산을 제대로 수행하기 위해서는 함수를 호출하기 전에 `SET DATEFIRST 1`을 호출해야 합니다.  
  
 또한이 예제에서는 사용 하는 [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) 절 저장된 프로시저를 실행할 수 있는 보안 컨텍스트를 지정 합니다. 이 예에서 `CALLER` 옵션은 프로시저를 호출하는 사용자의 컨텍스트에서 프로시저를 실행하도록 지정합니다. 지정할 수 있는 다른 옵션은 SELF, OWNER 및 *user_name*합니다.  
  
 함수 호출은 다음과 같습니다. `DATEFIRST`가 `1`로 설정되어 있다는 점에 유의하세요.  
  
```tsql
CREATE FUNCTION dbo.ISOweek (@DATE datetime)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
     DECLARE @ISOweek int;  
     SET @ISOweek= DATEPART(wk,@DATE)+1  
          -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104');  
--Special cases: Jan 1-3 may belong to the previous year  
     IF (@ISOweek=0)   
          SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1   
               AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1;  
--Special case: Dec 29-31 may belong to the next year  
     IF ((DATEPART(mm,@DATE)=12) AND   
          ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28))  
          SET @ISOweek=1;  
     RETURN(@ISOweek);  
END;  
GO  
SET DATEFIRST 1;  
SELECT dbo.ISOweek(CONVERT(DATETIME,'12/26/2004',101)) AS 'ISO Week';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
``` 
ISO Week  
----------------  
52  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>2. 인라인 테이블 반환 함수 만들기  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 인라인 테이블 값 함수를 반환합니다. 세 개의 열을 반환 `ProductID`, `Name` 및로 대리점 별 연도-날짜까지 총 집계 `YTD Total` 저장소에 판매 된 각 제품에 대 한 합니다.  
  
```tsql  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```

 함수를 호출하려면 이 쿼리를 실행하세요.    

```tsql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
### <a name="c-creating-a-multi-statement-table-valued-function"></a>3. 다중 문 테이블 반환 함수 만들기  
 다음 예에서는 AdventureWorks2012 데이터베이스에서 테이블 값 함수 `fn_FindReports(InEmpID)`를 만듭니다. 이 함수에 유효한 직원 ID를 제공하면 해당 직원에게 보고하는 모든 직속 부하 직원 및 관련 부서 직원에 해당하는 테이블이 반환됩니다. 이 함수는 재귀 CTE(공통 테이블 식)를 사용하여 직원의 계층적 목록을 생성합니다. 재귀 Cte에 대 한 자세한 내용은 참조 [common_table_expression &AMP;#40; Transact SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
```tsql  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        -- Get the initial list of Employees for Manager n
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0   
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        -- Join recursive member to anchor
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1   
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);   
  
GO  
```  
  
### <a name="d-creating-a-clr-function"></a>4. CLR 함수 만들기  
 이 예에서는 CLR 함수를 만듭니다 `len_s`합니다. 함수를 만들기 전에 `SurrogateStringFunction.dll` 어셈블리가 로컬 데이터베이스에 등록됩니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```tsql  
DECLARE @SamplesPath nvarchar(1024);  
-- You may have to modify the value of this variable if you have  
-- installed the sample in a location other than the default location.  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 
                                              'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
    FROM master.sys.database_files   
    WHERE name = 'master';  
  
CREATE ASSEMBLY [SurrogateStringFunction]  
FROM @SamplesPath + 'StringManipulate\CS\StringManipulate\bin\debug\SurrogateStringFunction.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION [dbo].[len_s] (@str nvarchar(4000))  
RETURNS bigint  
AS EXTERNAL NAME [SurrogateStringFunction].[Microsoft.Samples.SqlServer.SurrogateStringFunction].[LenS];  
GO  
```  
  
 CLR 테이블 반환 함수를 만드는 방법의 예제를 보려면 [CLR Table-Valued 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)합니다.  
  
### <a name="e-displaying-the-definition-of-includetsqlincludestsql-mdmd-user-defined-functions"></a>5. 정의가 표시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수  
  
```tsql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o ON m.object_id = o.object_id   
    AND type IN ('FN', 'IF', 'TF');  
GO  
```  
  
 ENCRYPTION 옵션을 사용하여 만든 함수의 정의는 sys.sql_modules로 확인할 수 없지만 암호화된 함수에 대한 다른 정보는 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [DROP function&#40; Transact SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [Objectpropertyex&#40; Transact SQL &#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [CLR 사용자 정의 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [SECURITY policy&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-security-policy-transact-sql.md)  
  
 


