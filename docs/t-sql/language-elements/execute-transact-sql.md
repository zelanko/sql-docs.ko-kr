---
title: EXECUTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EXEC
- EXECUTE_TSQL
- EXECUTE
- EXEC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- command strings [SQL Server]
- extended stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- Transact-SQL statements, executing
- strings [SQL Server], executing
- statements [SQL Server], executing
- context switching [SQL Server], execution context
- user-defined functions [SQL Server], executing
- character strings [SQL Server], executing
- switching execution context
- EXECUTE statement
ms.assetid: bc806b71-cc55-470a-913e-c5f761d5c4b7
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74ab018b017b675e08abb53036f88c3eaf2e5618
ms.sourcegitcommit: 05fdc50006a9abdda79c3a4685b075796068c4fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84748591"
---
# <a name="execute-transact-sql"></a>EXECUTE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 내에서 또는 시스템 저장 프로시저, 사용자 정의 저장 프로시저, CLR 저장 프로시저, 스칼라 반환 사용자 정의 함수, 확장 저장 프로시저 등과 같은 모듈 중 하나에서 명령 문자열이나 문자열을 실행합니다. EXECUTE 문은 연결된 서버로 통과 명령을 보내는 데 사용할 수 있습니다. 또한 문자열이나 명령이 실행되는 컨텍스트를 명시적으로 설정할 수도 있습니다. WITH RESULT SETS 옵션을 사용하여 결과 집합에 대한 메타데이터를 정의할 수 있습니다.
  
> [!IMPORTANT]  
>  문자열을 사용하여 EXECUTE를 호출하려면 먼저 문자열의 유효성을 검사해야 합니다. 유효성을 검사하지 않은 사용자 입력으로 생성된 명령은 실행하지 마세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
다음 코드 블록은 SQL Server 2019에서의 구문을 보여줍니다. 대신 [SQL Server 2017 이하에서의 구문](execute-transact-sql.md?view=sql-server-2017)을 참조하셔도 됩니다. 

```syntaxsql
-- Syntax for SQL Server 2019
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name [ ;number ] | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH <execute_option> [ ,...n ] ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS { LOGIN | USER } = ' name ' ]  
[;]  
  
Execute a pass-through command against a linked server  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'command_string [ ? ]' } [ + ...n ]  
        [ { , { value | @variable [ OUTPUT ] } } [ ...n ] ]  
    )   
    [ AS { LOGIN | USER } = ' name ' ]  
    [ AT linked_server_name ]  
    [ AT DATA_SOURCE data_source_name ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML   
}  
```  
::: moniker-end

::: monikerRange=">=sql-server-2016 ||=sqlallproducts-allversions"

다음 코드 블록은 SQL Server 2017 이하에서의 구문을 보여줍니다. 대신 [SQL Server 2019에서의 구문](execute-transact-sql.md?view=sql-server-ver15)을 참조하셔도 됩니다.


```syntaxsql
-- Syntax for SQL Server 2017 and earleir  
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name [ ;number ] | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH <execute_option> [ ,...n ] ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS { LOGIN | USER } = ' name ' ]  
[;]  
  
Execute a pass-through command against a linked server  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'command_string [ ? ]' } [ + ...n ]  
        [ { , { value | @variable [ OUTPUT ] } } [ ...n ] ]  
    )   
    [ AS { LOGIN | USER } = ' name ' ]  
    [ AT linked_server_name ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML   
}  
```  
::: moniker-end

  
```syntaxsql
-- In-Memory OLTP   

Execute a natively compiled, scalar user-defined function  
[ { EXEC | EXECUTE } ]   
    {   
      [ @return_status = ]   
      { module_name | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable   
                           | [ DEFAULT ]   
                           }  
        ]   
      [ ,...n ]   
      [ WITH <execute_option> [ ,...n ] ]   
    }  
<execute_option>::=  
{  
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}  
```  
  
```syntaxsql
-- Syntax for Azure SQL Database   
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name  | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH RECOMPILE ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS {  USER } = ' name ' ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML  
  
```

  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Execute a stored procedure  
[ { EXEC | EXECUTE } ]  
    procedure_name   
        [ { value | @variable [ OUT | OUTPUT ] } ] [ ,...n ] }  
[;]  
  
-- Execute a SQL string  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'tsql_string' } [ +...n ] )  
[;]  
```  


  
## <a name="arguments"></a>인수  
 @*return_status*  
 모듈의 반환 상태를 저장하는 선택적 정수 변수입니다. EXECUTE 문에서 이 변수를 사용하려면 먼저 일괄 처리, 저장 프로시저 또는 함수에서 변수를 선언해야 합니다.  
  
 스칼라 반환 사용자 정의 함수를 호출하는 데 사용하는 경우에는 모든 스칼라 데이터 형식을 @*return_status* 변수로 사용할 수 있습니다.  
  
 *module_name*  
 호출할 저장 프로시저나 스칼라 반환 사용자 정의 함수의 정규화되거나 정규화되지 않은 이름입니다. 모듈 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다. 확장 저장 프로시저의 이름은 서버의 데이터 정렬에 관계없이 항상 대/소문자를 구분합니다.  
  
 다른 데이터베이스에서 생성된 모듈은 이 모듈을 실행하는 사용자가 모듈을 소유하고 있거나 해당 데이터베이스에서 모듈을 실행할 수 있는 적절한 사용 권한이 있는 경우에 실행될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있는 다른 서버에서 모듈을 실행하려면 모듈을 실행하는 사용자가 원격 액세스를 통해 서버에 연결하여 해당 데이터베이스에서 모듈을 실행할 수 있는 적절한 사용 권한을 갖고 있어야 합니다. 서버 이름은 지정했지만 데이터베이스 이름은 지정하지 않은 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 사용자의 기본 데이터베이스에서 모듈을 찾습니다.  
  
 ;*number*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
 같은 이름의 프로시저를 그룹화하는 데 사용하는 정수입니다(선택 사항). 이 매개 변수는 확장 저장 프로시저에는 사용하지 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 프로시저 그룹에 대한 자세한 내용은[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)를 참조하세요.  
  
 @*module_name_var*  
 로컬로 정의된 변수 이름이며 모듈 이름을 나타냅니다.  
  
 이것은 고유하게 컴파일된 스칼라 사용자 정의 함수의 이름을 담는 변수일 수 있습니다.  
  
 @*parameter*  
 *module_name*에 대한 매개 변수이며 모듈에서 정의됩니다. 매개 변수 이름 앞에는 반드시 at 기호(@)를 사용해야 합니다. @*parameter_name*=*value* 형식을 사용하는 경우에는 매개 변수 이름과 상수를 모듈에서 정의된 순서대로 제공하지 않아도 됩니다. 그러나 임의의 매개 변수에 @*parameter_name*=*value* 형식을 사용한 경우에는 이후에 사용할 모든 매개 변수에도 이 형식을 사용해야 합니다.  
  
 기본적으로 매개 변수에 Null이 허용됩니다.  
  
 *value*  
 모듈이나 통과 명령에 전달할 매개 변수 값입니다. 매개 변수 이름을 지정하지 않은 경우에는 모듈에 정의된 순서대로 매개 변수 값을 제공해야 합니다.  
  
 연결된 서버에 대해 통과 명령을 실행하는 경우 연결된 서버의 OLE DB 공급자에 따라 매개 변수 값의 순서가 달라집니다. 대부분의 OLE DB 공급자는 값을 왼쪽에서 오른쪽으로 매개 변수에 바인딩합니다.  
  
 매개 변수 값이 개체 이름이거나 문자열인 경우 또는 데이터베이스 이름이나 스키마 이름으로 한정되는 경우에는 반드시 전체 이름을 작은따옴표로 묶어야 합니다. 매개 변수 값이 키워드인 경우에는 반드시 큰따옴표로 키워드를 묶어야 합니다.  
  
`@`으로 시작하지 않고 따옴표로 묶이지 않은 단일 단어를 전달하는 경우, 예를 들어 매개 변수 이름에서 `@`이 빠지면 따옴표가 없더라도 해당 단어는 nvarchar 문자열로 처리됩니다.

 기본값이 모듈에서 정의된 경우 사용자가 매개 변수를 지정하지 않고 모듈을 실행할 수 있습니다.  
  
 기본값으로 NULL을 사용할 수도 있습니다. 일반적으로 모듈 정의는 매개 변수 값이 NULL일 때 수행할 동작을 지정합니다.  
  
 @*variable*  
 매개 변수를 저장하거나 반환하는 변수입니다.  
  
 OUTPUT  
 모듈이나 명령 문자열에서 매개 변수를 반환하도록 지정합니다. 모듈이나 명령 문자열에서 일치하는 매개 변수가 반드시 OUTPUT 키워드를 사용하여 생성되어 있어야 합니다. 커서 변수를 매개 변수로 사용할 때 이 키워드를 사용합니다.  
  
 *값*이 연결된 서버에 대해 실행되는 모듈의 OUTPUT으로 정의된 경우 OLE DB 공급자가 해당@*매개 변수*에 수행한 모든 변경 내용은 모듈 실행이 끝날 때 변수로 다시 복사됩니다.  
  
 OUTPUT 매개 변수를 사용하고 있거나 호출 일괄 처리 또는 모듈 내의 다른 문에서 반환 값을 사용하려는 경우에는 매개 변수 값을 @*매개 변수* = @*값*과 같은 형식의 변수로 전달해야 합니다. 모듈에서 OUTPUT 매개 변수로 정의되지 않은 매개 변수에 대해 OUTPUT을 지정하여 모듈을 실행할 수는 없습니다. 상수는 OUTPUT을 사용하여 모듈에 전달할 수 없습니다. 반환 매개 변수에는 변수 이름이 필요합니다. 프로시저를 실행하기 전에 변수의 데이터 형식이 선언되어야 하며 값이 할당되어야 합니다.  
  
 EXECUTE를 원격 저장 프로시저에 사용하거나 연결된 서버에 대해 통과 명령을 실행하는 데 사용하는 경우 OUTPUT 매개 변수에는 LOB(Large Object) 데이터 형식을 사용할 수 없습니다.  
  
 반환 매개 변수에는 LOB 데이터 형식을 제외한 모든 데이터 형식을 사용할 수 있습니다.  
  
 DEFAULT  
 모듈에 정의된 매개 변수의 기본값을 제공합니다. 정의된 기본값이 없는 매개 변수 값이 모듈에 필요하고 매개 변수가 손실되었거나 DEFAULT 키워드가 지정된 경우에는 오류가 발생합니다.  
  
 @*string_variable*  
 지역 변수의 이름입니다. @*string_variable*은 **char**, **varchar**, **nchar** 또는 **nvarchar** 데이터 형식이 될 수 있습니다. 여기에는 **(max)** 데이터 형식이 포함됩니다.  
  
 [N] '*tsql_string*'  
 상수 문자열입니다. *tsql_string*은 **nvarchar** 또는 **varchar** 데이터 형식이 될 수 있습니다. N을 포함하면 문자열이 **nvarchar** 데이터 형식으로 해석됩니다.  
  
 AS \<context_specification>  
 문이 실행될 컨텍스트를 지정합니다.  
  
 LOGIN  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
 가장할 컨텍스트를 로그인으로 지정합니다. 가장의 범위는 서버입니다.  
  
 USER  
 가장할 컨텍스트를 현재 데이터베이스의 사용자로 지정합니다. 가장의 범위는 현재 데이터베이스로 제한됩니다. 데이터베이스 사용자로 컨텍스트 전환 시 해당 사용자의 서버 수준 사용 권한은 상속되지 않습니다.  
  
> [!IMPORTANT]  
>  데이터베이스 사용자로의 컨텍스트 전환이 활성 상태인 경우 데이터베이스 외부에 있는 리소스에 액세스하려고 시도하면 문이 실행되지 않습니다. 이러한 문에는 USE *데이터베이스* 문, 분산 쿼리, 그리고 세 부분이나 네 부분으로 된 식별자를 사용하여 다른 데이터베이스를 참조하는 쿼리가 포함됩니다.  
  
 '*name*'  
 유효한 사용자 또는 로그인 이름입니다. *name*은 sysadmin 고정 서버 역할의 멤버이거나 [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) 또는 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)에서 각각 보안 주체여야 합니다.  
  
 *name*에는 NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService 또는 NT AUTHORITY\LocalSystem과 같은 기본 제공 계정을 사용할 수 없습니다.  
  
 자세한 내용은 이 항목의 뒤에 나오는 [사용자 또는 로그인 이름 지정](#_user)을 참조하세요.  
  
 [N] '*command_string*'  
 연결된 서버로 전달될 명령을 포함하는 상수 문자열입니다. N을 포함하면 문자열이 **nvarchar** 데이터 형식으로 해석됩니다.  
  
 [?]  
 EXEC('...', \<arg-list>) AT \<linkedsrv> 문에 사용되는 통과 명령의 \<arg-list>에 값을 제공할 매개 변수를 나타냅니다.  
  
 AT *linked_server_name*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
 *command_string*이 *linked_server_name*에 대해 실행되고 결과(있을 경우)가 클라이언트로 반환되도록 지정합니다. *linked_server_name*은 로컬 서버의 기존 연결된 서버 정의를 참조해야 합니다. 연결된 서버는 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)를 사용하여 정의합니다.  
  
 WITH \<execute_option>  
 가능한 실행 옵션은 아래와 같습니다. INSERT...EXEC 문에서 RESULT SETS 옵션을 지정할 수 없습니다.  
 
AT DATA_SOURCE data_source_name **적용 대상**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 이상
  
 *command_string*이 *data_source_name*에 대해 실행되고 결과(있을 경우)가 클라이언트로 반환되도록 지정합니다. *data_source_name*은 데이터베이스의 기존 EXTERNAL DATA SOURCE 정의를 참조해야 합니다. SQL Server를 가리키는 데이터 원본만 지원됩니다. 또한 컴퓨팅 풀, 데이터 풀 또는 스토리지 풀을 가리키는 SQL Server 빅 데이터 클러스터 데이터 원본도 지원됩니다. 데이터 원본은 [CREATE EXTERNAL DATA SOURCE](../statements/create-external-data-source-transact-sql.md)를 사용하여 정의됩니다.  
  
 WITH \<execute_option>  
 가능한 실행 옵션은 아래와 같습니다. INSERT...EXEC 문에서 RESULT SETS 옵션을 지정할 수 없습니다.  
  
|용어|정의|  
|----------|----------------|  
|RECOMPILE|모듈을 실행한 후 새 계획을 컴파일하고 사용한 다음 삭제하도록 합니다. 모듈에 대한 기존 쿼리 계획이 있는 경우 이 계획은 캐시에 유지됩니다.<br /><br /> 제공하는 매개 변수가 불규칙하거나 데이터가 현저하게 변경된 경우에 이 옵션을 사용합니다. 이 옵션은 확장 저장 프로시저에는 사용하지 않습니다. 이 옵션은 비용이 많이 들기 때문에 반드시 필요한 경우에만 사용하는 것이 좋습니다.<br /><br /> **참고:** OPENDATASOURCE 구문을 사용하는 저장 프로시저를 호출할 경우 WITH RECOMPILE을 사용할 수 없습니다. WITH RECOMPILE 옵션은 네 부분으로 된 개체 이름이 지정될 때 무시됩니다.<br /><br /> **참고:** RECOMPILE은 고유하게 컴파일된 사용자 정의 스칼라 함수에서 지원되지 않습니다. 다시 컴파일해야 하는 경우 [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)을 사용합니다.|  
|**RESULT SETS UNDEFINED**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> 이 옵션은 반환되는 결과(있는 경우)를 보장하지 않으며 정의를 제공하지 않습니다. 어떤 결과가 반환되거나 결과가 반환되지 않는 경우에도 이 문은 오류 없이 실행됩니다. RESULT SETS UNDEFINED는 result_sets_option을 제공하지 않는 경우의 기본 동작입니다.<br /><br /> 해석된 스칼라 사용자 정의 함수와 고유하게 컴파일된 스칼라 사용자 정의 함수의 경우, 함수가 결과 집합을 반환하지 않기 때문에 이 옵션이 작동하지 않습니다.|  
|RESULT SETS NONE|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> execute 문이 어떠한 결과도 반환하지 않습니다. 결과가 반환되는 경우 일괄 처리가 중단됩니다.<br /><br /> 해석된 스칼라 사용자 정의 함수와 고유하게 컴파일된 스칼라 사용자 정의 함수의 경우, 함수가 결과 집합을 반환하지 않기 때문에 이 옵션이 작동하지 않습니다.|  
|*\<result_sets_definition>*|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> 결과가 result_sets_definition에 지정된 대로 반환됩니다. 여러 결과 집합을 반환하는 문의 경우 *result_sets_definition* 섹션을 여러 개 제공합니다. 각각의 *result_sets_definition*를 괄호로 묶고 쉼표로 구분합니다. 자세한 내용은 이 항목의 뒷부분에 있는 \<result_sets_definition>을 참조하세요.<br /><br /> 이 옵션에서는 함수가 결과 집합을 반환하지 않기 때문에 고유하게 컴파일된 스칼라 사용자 정의 함수에 대해 항상 오류를 냅니다.|
  
\<result_sets_definition>
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 실행된 문이 반환하는 결과 집합에 대해 설명합니다. result_sets_definition 절의 의미는 다음과 같습니다.  
  
|용어|정의|  
|----------|----------------|  
|{<br /><br /> column_name<br /><br /> data_type<br /><br /> [ COLLATE collation_name]<br /><br /> [NULL &#124; NOT NULL]<br /><br /> }|아래 표를 참조하세요.|  
|db_name|테이블, 뷰 또는 테이블 반환 함수를 포함하는 데이터베이스의 이름입니다.|  
|schema_name|테이블, 뷰 또는 테이블 반환 함수를 소유한 스키마의 이름입니다.|  
|table_name &#124; view_name &#124; table_valued_function_name|명명된 테이블, 뷰 또는 테이블 반환 함수에 지정된 열을 반환하도록 지정합니다. 테이블 변수, 임시 테이블 및 동의어는 AS 개체 구문에서 지원되지 않습니다.|  
|AS TYPE [schema_name.]table_type_name|테이블 형식에 지정된 열을 반환하도록 지정합니다.|  
|AS FOR XML|EXECUTE 문에서 호출하는 문 또는 저장 프로시저의 XML 결과를 SELECT ... FOR XML ... 문에 의해 생성된 것처럼 형식을 변환하도록 지정합니다. 원래 문의 type 지시어에서 모든 서식이 제거되고 type 지시어를 지정하지 않은 경우처럼 결과가 반환됩니다. AS FOR XML은 실행된 문 또는 저장 프로시저에서 비-XML 테이블 형식 결과를 XML로 변환하지 않습니다.|  
  
|용어|정의|  
|----------|----------------|  
|column_name|각 열의 이름입니다. 열의 개수가 결과 집합과 다른 경우 오류가 발생하고 일괄 처리가 중단됩니다. 열의 이름이 결과 집합과 다른 경우 반환된 열 이름이 정의된 이름으로 설정됩니다.|  
|data_type|각 열의 데이터 형식입니다. 데이터 형식이 다른 경우 정의된 데이터 형식으로 암시적 변환을 수행합니다. 변환에 실패하는 경우 일괄 처리가 중단됩니다.|  
|COLLATE collation_name|각 열의 데이터 정렬입니다. 데이터 정렬이 일치하지 않는 경우 암시적 데이터 정렬이 시도됩니다. 데이터 정렬이 실패하는 경우 일괄 처리가 중단됩니다.|  
|NULL &#124; NOT NULL|각 열의 null 허용 여부입니다. null 허용 여부가 NOT NULL로 정의되어 있지만 반환된 데이터에 NULL이 포함되어 있는 경우 오류가 발생하고 일괄 처리가 중단됩니다. 지정하지 않은 경우 ANSI_NULL_DFLT_ON and ANSI_NULL_DFLT_OFF 옵션 설정이 기본값으로 사용됩니다.|  
  
 실행 중에 반환되는 실제 결과 집합은 WITH RESULT SETS 절을 사용하여 결과 집합 수, 열 수, 열 이름, null 허용 여부, 데이터 형식 중 한 가지 방법으로 정의된 결과와 다를 수 있습니다. 결과 집합의 수가 다른 경우 오류가 발생하고 일괄 처리가 중단됩니다.  
  
## <a name="remarks"></a>설명  
 *value* 또는 @*parameter_name*=*value*를 사용하여 매개 변수를 제공할 수 있습니다. 를 사용하여 제공할 수 있습니다. 매개 변수는 트랜잭션의 일부가 아니므로 나중에 롤백되는 트랜잭션에서 매개 변수가 변경된 경우 해당 매개 변수의 값은 이전 값으로 되돌아가지 않습니다. 호출자에게 반환되는 값은 항상 모듈이 반환되는 시점의 값입니다.  
  
 한 모듈에서 다른 모듈을 호출하거나 CLR(공용 언어 런타임) 모듈, 사용자 정의 유형 또는 집계를 참조하여 관리 코드를 실행하면 중첩이 발생합니다. 호출된 모듈이나 관리 코드 참조가 실행될 때는 중첩 수준이 증가하고 호출된 모듈이나 관리 코드 참조가 끝날 때는 중첩 수준이 감소합니다. 최대값인 32 중첩 수준을 초과하면 전체 호출 체인이 실행되지 않습니다. 현재 중첩 수준은 @@NESTLEVEL system 함수에 저장됩니다.  
  
 BEGIN DISTRIBUTED TRANSACTION 문에서 실행되지 않았거나 다양한 구성 옵션과 함께 사용되는 경우 원격 저장 프로시저와 확장 저장 프로시저는 트랜잭션의 범위 밖에 있으므로 호출을 통해 실행되는 명령은 롤백할 수 없습니다. 자세한 내용은 [시스템 저장 프로시저 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) 및 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)을 참조하세요.  
  
 커서 변수를 사용할 때 변수에 할당된 커서와 함께 커서 변수에서 전달되는 프로시저를 실행하면 오류가 발생합니다.  
  
 문이 일괄 처리의 첫 번째 문인 경우에는 모듈을 실행할 때 EXECUTE 키워드를 지정할 필요가 없습니다.  
  
 CLR 저장 프로시저에 대한 자세한 내용은 CLR 저장 프로시저를 참조하세요.  
  
## <a name="using-execute-with-stored-procedures"></a>저장 프로시저와 함께 EXECUTE 사용  
 문이 일괄 처리의 첫 번째 문인 경우에는 저장 프로시저를 실행할 때 EXECUTE 키워드를 지정할 필요가 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 저장 프로시저는 sp_로 시작합니다. 시스템 저장 프로시저는 물리적으로 [리소스 데이터베이스](../../relational-databases/databases/resource-database.md)에 저장되지만 논리적으로는 모든 시스템 정의 데이터베이스와 사용자 정의 데이터베이스의 sys 스키마에 나타납니다. 시스템 저장 프로시저를 일괄 처리에서 실행하거나 사용자 정의 저장 프로시저 또는 함수와 같은 모듈 내에서 실행할 때는 저장 프로시저 이름을 sys 스키마 이름으로 한정하는 것이 좋습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 확장 저장 프로시저는 xp_로 시작하며 master 데이터베이스의 dbo 스키마에 들어 있습니다. 시스템 확장 저장 프로시저를 일괄 처리에서 실행하거나 사용자 정의 저장 프로시저 또는 함수와 같은 모듈 내에서 실행할 때는 저장 프로시저 이름을 master.dbo로 한정하는 것이 좋습니다.  
  
 사용자 정의 저장 프로시저를 일괄 처리에서 실행하거나 사용자 정의 저장 프로시저 또는 함수와 같은 모듈 내에서 실행할 때는 저장 프로시저 이름을 스키마 이름으로 한정하는 것이 좋습니다. 사용자 정의 저장 프로시저의 이름은 시스템 저장 프로시저의 이름과 다르게 지정하는 것이 좋습니다. 저장 프로시저 실행에 대한 자세한 내용은 [저장 프로시저 실행](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)을 참조하세요.  
  
## <a name="using-execute-with-a-character-string"></a>문자열과 함께 EXECUTE 사용  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 문자열이 8,000바이트로 제한됩니다. 따라서 동적 실행을 위해서는 긴 문자열을 연결해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 문자열에 최대 2GB의 데이터를 사용할 수 있는 **varchar(max)** 및 **nvarchar(max)** 데이터 형식을 지정할 수 있습니다.  
  
 데이터베이스 컨텍스트 내의 변경 사항은 EXECUTE 문이 종료될 때까지만 지속됩니다. 예를 들어 다음 문의 `EXEC`가 실행된 후의 데이터베이스 컨텍스트는 master입니다.  
  
```sql  
USE master; EXEC ('USE AdventureWorks2012; SELECT BusinessEntityID, JobTitle FROM HumanResources.Employee;');  
```  
  
## <a name="context-switching"></a>컨텍스트 전환  
 `AS { LOGIN | USER } = ' name '` 절을 사용하여 동적 문의 실행 컨텍스트를 전환할 수 있습니다. 컨텍스트 전환이 `EXECUTE ('string') AS <context_specification>`으로 지정된 경우 컨텍스트 전환 기간은 실행될 쿼리의 범위로 제한됩니다.  
  
###  <a name="specifying-a-user-or-login-name"></a><a name="_user"></a>사용자 또는 로그인 이름 지정  
 `AS { LOGIN | USER } = ' name '`에 지정된 사용자 또는 로그인 이름은 각각 sys.database_principals 또는 sys.server_principals에서 보안 주체로 존재해야 합니다. 그렇지 않으면 문이 실행되지 않습니다. 또한 보안 주체에 IMPERSONATE 권한을 부여해야 합니다. 호출자가 데이터베이스 소유자가 아니거나 sysadmin 고정 서버 역할의 멤버가 아니라면 사용자가 Windows 그룹 멤버 자격을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스 또는 인스턴스에 액세스하는 경우에도 반드시 보안 주체가 존재해야 합니다. 예를 들어 다음과 같은 조건을 가정해 보세요.  
  
-   CompanyDomain\SQLUsers 그룹에 Sales 데이터베이스에 대한 액세스 권한이 있습니다.  
  
-   CompanyDomain\SqlUser1은 SQLUsers의 멤버이므로 Sales 데이터베이스에 대한 암시적 액세스 권한이 있습니다.  
  
 CompanyDomain\SqlUser1은 SQLUsers 그룹의 멤버 자격을 통해 데이터베이스에 액세스할 수 있지만 `CompanyDomain\SqlUser1`이 데이터베이스의 보안 주체로 존재하지 않기 때문에 `EXECUTE @string_variable AS USER = 'CompanyDomain\SqlUser1'` 문은 실행되지 않습니다.  
  
### <a name="best-practices"></a>모범 사례  
 문이나 모듈에 정의된 작업을 수행하는 데 필요한 최소한의 권한이 있는 로그인이나 사용자를 지정합니다. 예를 들어 데이터베이스 수준 권한만 있어도 되는 경우에는 서버 수준 권한이 있는 로그인 이름을 지정하지 마세요. 마찬가지로 데이터베이스 소유자 권한이 필요한 경우가 아니라면 데이터베이스 소유자 계정을 지정하지 마세요.  
  
## <a name="permissions"></a>사용 권한  
 EXECUTE 문을 실행하는 데에는 사용 권한이 필요하지 않습니다. 그러나 EXECUTE 문자열 내에서 참조되는 보안 개체에 대해서는 사용 권한이 필요합니다. 예를 들어 문자열에 INSERT 문이 있는 경우 EXECUTE 문의 호출자에게는 대상 테이블에 대한 INSERT 권한이 있어야 합니다. EXECUTE 문이 모듈 내에 포함된 경우에도 EXECUTE 문이 실행될 때는 사용 권한 검사가 수행됩니다.  
  
 모듈에 대한 EXECUTE 권한은 기본적으로 모듈 소유자에게 부여되며 모듈 소유자는 이 권한을 다른 사용자에게 이전할 수 있습니다. 문자열을 실행하는 모듈이 실행될 때는 모듈을 만든 사용자의 컨텍스트가 아니라 모듈을 실행하는 사용자의 컨텍스트에서 사용 권한 검사가 수행됩니다. 그러나 동일한 사용자가 호출 모듈과 호출되는 모듈을 모두 소유하는 경우 두 번째 모듈에 대해서는 EXECUTE 권한 검사가 수행되지 않습니다.  
  
 모듈에서 다른 데이터베이스 개체에 액세스하는 경우 사용자에게 모듈에 대한 EXECUTE 권한이 있고 다음 조건 중 하나가 충족된다면 성공적으로 실행됩니다.  
  
-   모듈이 EXECUTE AS USER 또는 SELF로 표시되어 있으며 모듈 소유자가 참조된 개체에 대한 해당 권한을 갖고 있습니다. 모듈 내 가장에 대한 자세한 내용은 [EXECUTE AS Clause &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요.  
  
-   모듈이 EXECUTE AS CALLER로 표시되어 있으며 사용자가 개체에 대한 해당 권한을 갖고 있습니다.  
  
-   모듈이 EXECUTE AS *user_name*으로 표시되어 있으며 *user_name*이 개체에 대한 해당 권한을 갖고 있습니다.  
  
### <a name="context-switching-permissions"></a>컨텍스트 전환 권한  
 로그인에 EXECUTE AS를 지정하려면 호출자에게 지정한 로그인 이름에 대한 IMPERSONATE 권한이 있어야 합니다. 데이터베이스 사용자에 EXECUTE AS를 지정하려면 호출자에게 지정한 사용자 이름에 대한 IMPERSONATE 권한이 있어야 합니다. 실행 컨텍스트를 지정하지 않거나 EXECUTE AS CALLER를 지정한 경우에는 IMPERSONATE 권한이 필요하지 않습니다.  
  
## <a name="examples-sql-server"></a>예제: SQL Server
  
### <a name="a-using-execute-to-pass-a-single-parameter"></a>A. EXECUTE를 사용하여 단일 매개 변수 전달  
 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `uspGetEmployeeManagers` 저장 프로시저에는 하나의 매개 변수가 필요합니다(`@EmployeeID`). 다음 예에서는 매개 변수 값으로 `Employee ID 6`을 사용하여 `uspGetEmployeeManagers` 저장 프로시저를 실행합니다.  
  
```sql    
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
 변수는 실행 시 명시적으로 명명될 수 있습니다.  
  
```sql    
EXEC dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
 다음이 일괄 처리 또는 **osql** 또는 **sqlcmd** 스크립트의 첫 번째 문인 경우에는 EXEC가 필요하지 않습니다.  
  
```sql    
dbo.uspGetEmployeeManagers 6;  
GO  
--Or  
dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
### <a name="b-using-multiple-parameters"></a>B. 여러 매개 변수 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `spGetWhereUsedProductID` 저장 프로시저를 실행합니다. 이 저장 프로시저는 두 개의 매개 변수를 전달합니다. 첫 번째 매개 변수는 제품 ID(`819`)이고 두 번째 매개 변수인 `@CheckDate,`는 `datetime` 값입니다.  
  
```sql    
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
### <a name="c-using-execute-tsql_string-with-a-variable"></a>C. 변수와 함께 EXECUTE 'tsql_string' 사용  
 다음 예에서는 `EXECUTE`가 변수가 포함된 동적으로 작성된 문자열을 처리하는 방법을 보여 줍니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 모든 사용자 정의 테이블의 목록을 유지하는 `tables_cursor` 커서를 만든 다음 해당 목록을 사용하여 테이블의 모든 인덱스를 다시 작성합니다.  
  
```sql    
DECLARE tables_cursor CURSOR  
   FOR  
   SELECT s.name, t.name   
   FROM sys.objects AS t  
   JOIN sys.schemas AS s ON s.schema_id = t.schema_id  
   WHERE t.type = 'U';  
OPEN tables_cursor;  
DECLARE @schemaname sysname;  
DECLARE @tablename sysname;  
FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN;  
   EXECUTE ('ALTER INDEX ALL ON ' + @schemaname + '.' + @tablename + ' REBUILD;');  
   FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
END;  
PRINT 'The indexes on all tables have been rebuilt.';  
CLOSE tables_cursor;  
DEALLOCATE tables_cursor;  
GO  
  
```  
  
### <a name="d-using-execute-with-a-remote-stored-procedure"></a>D. 원격 저장 프로시저와 함께 EXECUTE 사용  
 다음 예에서는 `uspGetEmployeeManagers` 원격 서버에서 `SQLSERVER1` 저장 프로시저를 실행하고 성공이나 실패를 나타내는 반환 상태를 `@retstat`에 저장합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
```sql    
DECLARE @retstat int;  
EXECUTE @retstat = SQLSERVER1.AdventureWorks2012.dbo.uspGetEmployeeManagers @BusinessEntityID = 6;  
```  
  
### <a name="e-using-execute-with-a-stored-procedure-variable"></a>E. 저장 프로시저 변수와 함께 EXECUTE 사용  
 다음 예에서는 저장 프로시저 이름을 나타내는 변수를 만듭니다.  
  
```sql  
DECLARE @proc_name varchar(30);  
SET @proc_name = 'sys.sp_who';  
EXEC @proc_name;  
  
```  
  
### <a name="f-using-execute-with-default"></a>F. DEFAULT와 함께 EXECUTE 사용  
 다음 예에서는 첫 번째 및 세 번째 매개 변수에 대한 기본값으로 저장 프로시저를 만듭니다. 프로시저가 실행될 때 호출에 값이 전달되지 않거나 기본값이 지정되는 경우 이러한 기본값은 첫 번째 및 세 번째 매개 변수용으로 삽입됩니다. `DEFAULT` 키워드를 사용할 수 있는 여러 가지 방법이 있습니다.  
  
```sql    
IF OBJECT_ID(N'dbo.ProcTestDefaults', N'P')IS NOT NULL  
   DROP PROCEDURE dbo.ProcTestDefaults;  
GO  
-- Create the stored procedure.  
CREATE PROCEDURE dbo.ProcTestDefaults (  
@p1 smallint = 42,   
@p2 char(1),   
@p3 varchar(8) = 'CAR')  
AS   
   SET NOCOUNT ON;  
   SELECT @p1, @p2, @p3  
;  
GO  
  
```  
  
 `Proc_Test_Defaults` 저장 프로시저는 여러 가지 조합으로 실행할 수 있습니다.  
  
```sql    
-- Specifying a value only for one parameter (@p2).  
EXECUTE dbo.ProcTestDefaults @p2 = 'A';  
-- Specifying a value for the first two parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'B';  
-- Specifying a value for all three parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'C', 'House';  
-- Using the DEFAULT keyword for the first parameter.  
EXECUTE dbo.ProcTestDefaults @p1 = DEFAULT, @p2 = 'D';  
-- Specifying the parameters in an order different from the order defined in the procedure.  
EXECUTE dbo.ProcTestDefaults DEFAULT, @p3 = 'Local', @p2 = 'E';  
-- Using the DEFAULT keyword for the first and third parameters.  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'H', DEFAULT;  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'I', @p3 = DEFAULT;  
  
```  
  
### <a name="g-using-execute-with-at-linked_server_name"></a>G. AT linked_server_name과 함께 EXECUTE 사용  
 다음 예에서는 원격 서버에 명령 문자열을 전달하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스를 가리키는 `SeattleSales` 연결된 서버를 만든 다음 이 연결된 서버에 대해 DDL 문(`CREATE TABLE`)을 실행합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
```sql    
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
EXECUTE ( 'CREATE TABLE AdventureWorks2012.dbo.SalesTbl   
(SalesID int, SalesName varchar(10)) ; ' ) AT SeattleSales;  
GO  
```  
  
### <a name="h-using-execute-with-recompile"></a>H. EXECUTE WITH RECOMPILE 사용  
 다음 예에서는 `Proc_Test_Defaults` 저장 프로시저를 실행하고 모듈을 실행한 후 새 쿼리 계획을 컴파일하고 사용한 다음, 삭제하도록 합니다.  
  
```sql    
EXECUTE dbo.Proc_Test_Defaults @p2 = 'A' WITH RECOMPILE;  
GO  
```  
  
### <a name="i-using-execute-with-a-user-defined-function"></a>9\. 사용자 정의 함수와 함께 EXECUTE 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `ufnGetSalesOrderStatusText` 스칼라 사용자 정의 함수를 실행합니다. 이 예에서는 `@returnstatus` 변수를 사용하여 함수가 반환하는 값을 저장합니다. 함수에는 입력 매개 변수 하나(`@Status`)가 필요합니다. 이 매개 변수는 **tinyint** 데이터 형식으로 정의됩니다.  
  
```sql    
DECLARE @returnstatus nvarchar(15);  
SET @returnstatus = NULL;  
EXEC @returnstatus = dbo.ufnGetSalesOrderStatusText @Status = 2;  
PRINT @returnstatus;  
GO  
```  
  
### <a name="j-using-execute-to-query-an-oracle-database-on-a-linked-server"></a>J. EXECUTE를 사용하여 연결된 서버의 Oracle 데이터베이스 쿼리  
 다음 예에서는 원격 Oracle 서버에서 몇 가지 `SELECT` 문을 실행합니다. 먼저 Oracle 서버를 연결된 서버로 추가한 다음 연결된 서버 로그인을 만듭니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
```sql    
-- Setup the linked server.  
EXEC sp_addlinkedserver    
        @server='ORACLE',  
        @srvproduct='Oracle',  
        @provider='OraOLEDB.Oracle',   
        @datasrc='ORACLE10';  
  
EXEC sp_addlinkedsrvlogin   
    @rmtsrvname='ORACLE',  
    @useself='false',   
    @locallogin=null,   
    @rmtuser='scott',   
    @rmtpassword='tiger';  
  
EXEC sp_serveroption 'ORACLE', 'rpc out', true;  
GO  
  
-- Execute several statements on the linked Oracle server.  
EXEC ( 'SELECT * FROM scott.emp') AT ORACLE;  
GO  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', 7902) AT ORACLE;  
GO  
DECLARE @v INT;   
SET @v = 7902;  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', @v) AT ORACLE;  
GO   
```  
  
### <a name="k-using-execute-as-user-to-switch-context-to-another-user"></a>11. EXECUTE AS USER를 사용하여 다른 사용자 컨텍스트로 전환  
 다음 예에서는 테이블을 만들고 `AS USER` 절을 지정하여 문의 실행 컨텍스트를 호출자에서 `User1`로 전환하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문자열을 실행합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 문이 실행될 때 `User1`의 사용 권한을 확인합니다. `User1`은 데이터베이스에 사용자로 존재해야 하며 `Sales` 스키마에서 테이블을 만들 수 있는 사용 권한이 있어야 합니다. 그렇지 않으면 문이 실행되지 않습니다.  
  
```sql    
EXECUTE ('CREATE TABLE Sales.SalesTable (SalesID int, SalesName varchar(10));')  
AS USER = 'User1';  
GO  
```  
  
### <a name="l-using-a-parameter-with-execute-and-at-linked_server_name"></a>12. EXECUTE 및 AT linked_server_name과 함께 매개 변수 사용  
 다음 예에서는 매개 변수에 물음표(`?`) 자리 표시자를 사용하여 원격 서버로 명령 문자열을 전달합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스를 가리키는 `SeattleSales` 연결된 서버를 만든 다음 이 연결된 서버에 대해 `SELECT` 문을 실행합니다. `SELECT` 문은 물음표를 `ProductID` 매개 변수(`952`)에 대한 자리 표시자로 사용합니다. 이 매개 변수는 문 다음에 입력합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
```sql    
-- Setup the linked server.  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
-- Execute the SELECT statement.  
EXECUTE ('SELECT ProductID, Name   
    FROM AdventureWorks2012.Production.Product  
    WHERE ProductID = ? ', 952) AT SeattleSales;  
GO  
```  
  
### <a name="m-using-execute-to-redefine-a-single-result-set"></a>13. EXECUTE를 사용하여 단일 결과 집합 다시 정의  
 이전의 일부 예에서는 `EXEC dbo.uspGetEmployeeManagers 6;`을 실행하여 7개의 열을 반환했습니다. 다음 예에서는 `WITH RESULT SET` 구문을 사용하여 반환되는 결과 집합의 이름과 데이터 형식을 변경하는 방법을 보여 줍니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
```sql    
EXEC uspGetEmployeeManagers 16  
WITH RESULT SETS  
(   
   ([Reporting Level] int NOT NULL,  
    [ID of Employee] int NOT NULL,  
    [Employee First Name] nvarchar(50) NOT NULL,  
    [Employee Last Name] nvarchar(50) NOT NULL,  
    [Employee ID of Manager] nvarchar(max) NOT NULL,  
    [Manager First Name] nvarchar(50) NOT NULL,  
    [Manager Last Name] nvarchar(50) NOT NULL )  
);  
  
```  
  
### <a name="n-using-execute-to-redefine-a-two-result-sets"></a>14. EXECUTE를 사용하여 두 결과 집합 다시 정의  
 둘 이상의 결과 집합을 반환하는 문을 실행하는 경우 각 예상 결과 집합을 정의합니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]의 다음 예에서는 두 결과 집합을 반환하는 프로시저를 만듭니다. 그런 다음, **WITH RESULT SETS** 절을 사용하고 두 결과 집합 정의를 지정하여 프로시저를 실행합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
```sql    
--Create the procedure  
CREATE PROC Production.ProductList @ProdName nvarchar(50)  
AS  
-- First result set  
SELECT ProductID, Name, ListPrice  
    FROM Production.Product  
    WHERE Name LIKE @ProdName;  
-- Second result set   
SELECT Name, COUNT(S.ProductID) AS NumberOfOrders  
    FROM Production.Product AS P  
    JOIN Sales.SalesOrderDetail AS S  
        ON P.ProductID  = S.ProductID   
    WHERE Name LIKE @ProdName  
    GROUP BY Name;  
GO  
  
-- Execute the procedure   
EXEC Production.ProductList '%tire%'  
WITH RESULT SETS   
(  
    (ProductID int,   -- first result set definition starts here  
    Name Name,  
    ListPrice money)  
    ,                 -- comma separates result set definitions  
    (Name Name,       -- second result set definition starts here  
    NumberOfOrders int)  
);  
  
```  
  ### <a name="o-using-execute-with-at-data_source-data_source_name-to-query-a-remote-sql-server"></a>15. EXECUTE와 AT DATA_SOURCE data_source_name을 사용하여 원격 SQL Server 쿼리 
  
 다음 예에서는 명령 문자열을 SQL Server 인스턴스를 가리키는 외부 데이터 원본에 전달합니다. 
  
**적용 대상**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 이상
  
```sql    
EXECUTE ( 'SELECT @@SERVERNAME' ) AT DATA_SOURCE my_sql_server;  
GO  
```  
  
### <a name="p-using-execute-with-at-data_source-data_source_name-to-query-compute-pool-in-sql-server-big-data-cluster"></a>16. EXECUTE와 AT DATA_SOURCE data_source_name을 사용하여 SQL Server 빅 데이터 클러스터에 있는 컴퓨팅 풀 쿼리 

 다음 예에서는 명령 문자열을 SQL Server 빅 데이터 클러스터의 컴퓨팅 풀을 가리키는 외부 데이터 원본에 전달합니다. 이 예에서는 SQL Server 빅 데이터 클러스터의 컴퓨팅 풀을 상대로 `SqlComputePool` 데이터 원본을 만들고 데이터 원본을 상대로 `SELECT` 문을 실행합니다. 
  
**적용 대상**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 이상
  
```sql  
CREATE EXTERNAL DATA SOURCE SqlComputePool 
WITH (LOCATION = 'sqlcomputepool://controller-svc/default');
EXECUTE ( 'SELECT @@SERVERNAME' ) AT DATA_SOURCE SqlComputePool;  
GO  
```  

### <a name="q-using-execute-with-at-data_source-data_source_name-to-query-data-pool-in-sql-server-big-data-cluster"></a>17. EXECUTE와 AT DATA_SOURCE data_source_name을 사용하여 SQL Server 빅 데이터 클러스터에 있는 데이터 풀 쿼리 
 다음 예에서는 명령 문자열을 SQL Server 빅 데이터 클러스터의 컴퓨팅 풀을 가리키는 외부 데이터 원본에 전달합니다. 이 예에서는 SQL Server 빅 데이터 클러스터의 데이터 풀을 상대로 `SqlDataPool` 데이터 원본을 만들고 데이터 원본을 상대로 `SELECT` 문을 실행합니다. 
  
**적용 대상**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 이상
  
```sql  
CREATE EXTERNAL DATA SOURCE SqlDataPool 
WITH (LOCATION = 'sqldatapool://controller-svc/default');
EXECUTE ( 'SELECT @@SERVERNAME' ) AT DATA_SOURCE SqlDataPool;  
GO  
```

### <a name="r-using-execute-with-at-data_source-data_source_name-to-query-storage-pool-in-sql-server-big-data-cluster"></a>18. EXECUTE와 AT DATA_SOURCE data_source_name을 사용하여 SQL Server 빅 데이터 클러스터에 있는 스토리지 풀 쿼리 

 다음 예에서는 명령 문자열을 SQL Server 빅 데이터 클러스터의 컴퓨팅 풀을 가리키는 외부 데이터 원본에 전달합니다. 이 예에서는 SQL Server 빅 데이터 클러스터의 데이터 풀을 상대로 `SqlStoragePool` 데이터 원본을 만들고 데이터 원본을 상대로 `SELECT` 문을 실행합니다. 
  
**적용 대상**: [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 이상
  
```sql  
CREATE EXTERNAL DATA SOURCE SqlStoragePool
WITH (LOCATION = 'sqlhdfs://controller-svc/default');
EXECUTE ( 'SELECT @@SERVERNAME' ) AT DATA_SOURCE SqlStoragePool;  
GO  
```

  
## <a name="examples-azure-synapse-analytics"></a>예제: Azure Synapse Analytics 
  
### <a name="a-basic-procedure-execution"></a>A: 기본 프로시저 실행  
 저장 프로시저 실행:  
  
```sql  
EXEC proc1;  
```  
  
 런타임에 결정되는 이름으로 저장 프로시저 호출:  
  
```sql    
EXEC ('EXEC ' + @var);  
```  
  
 저장 프로시저 안에서 저장 프로시저 호출:  
  
```sql   
CREATE sp_first AS EXEC sp_second; EXEC sp_third;  
```  
  
### <a name="b-executing-strings"></a>B: 문자열 실행  
 SQL 문자열 실행:  
  
```sql   
EXEC ('SELECT * FROM sys.types');  
```  
  
 중첩 문자열 실행:  
  
```sql  
EXEC ('EXEC (''SELECT * FROM sys.types'')');  
```  
  
 문자열 변수 실행:  
  
```sql  
DECLARE @stringVar nvarchar(100);  
SET @stringVar = N'SELECT name FROM' + ' sys.sql_logins';  
EXEC (@stringVar);  
```  
  
### <a name="c-procedures-with-parameters"></a>C: 매개 변수가 있는 프로시저  

 다음 예제에서는 매개 변수가 있는 프로시저를 만들고 3가지 방법으로 프로시저를 실행합니다.  
  
```sql  
-- Uses AdventureWorks  
  
CREATE PROC ProcWithParameters  
    @name nvarchar(50),  
@color nvarchar (15)  
AS   
SELECT ProductKey, EnglishProductName, Color FROM [dbo].[DimProduct]  
WHERE EnglishProductName LIKE @name  
AND Color = @color;  
GO  
  
-- Executing using positional parameters  
EXEC ProcWithParameters N'%arm%', N'Black';  
-- Executing using named parameters in order  
EXEC ProcWithParameters @name = N'%arm%', @color = N'Black';  
-- Executing using named parameters out of order  
EXEC ProcWithParameters @color = N'Black', @name = N'%arm%';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [@@NESTLEVEL&#40;Transact-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [osql Utility](../../tools/osql-utility.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)   
 [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [OPENDATASOURCE&#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [메모리 내 OLTP에 대한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)  
  
  
