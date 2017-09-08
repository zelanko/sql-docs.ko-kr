---
title: ALTER FUNCTION (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_FUNCTION_TSQL
- ALTER FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER FUNCTION statement
- modifying functions
- functions [SQL Server], modifying
ms.assetid: 89f066ee-05ac-4439-ab04-d8c3d5911179
caps.latest.revision: 62
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3da4c3a8e76a48db0eee940e969ddf24dc147149
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-function-transact-sql"></a>ALTER FUNCTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  권한을 변경하거나 종속 함수, 저장 프로시저 또는 트리거에 영향을 주지 않고 이전에 CREATE FUNCTION 문을 실행하여 만든 기존 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CLR 함수를 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Transact-SQL Scalar Function Syntax    
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
-- Transact-SQL Multistatement Table-valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
-- CLR Scalar and Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type | TABLE <clr_table_type_definition> }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```
  
```
-- CLR Function Clauses
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
-- Syntax for In-Memory OLTP: Natively compiled, scalar user-defined function  
ALTER FUNCTION [ schema_name. ] function_name    
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])  
        function_body   
        RETURN scalar_expression  
    END  
    
<function_option>::=   
{ |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
```   
  
## <a name="arguments"></a>인수  
 *schema_name*  
 사용자 정의 함수가 속한 스키마의 이름입니다.  
  
 *function_name*  
 변경할 사용자 정의 함수입니다.  
  
> [!NOTE]  
>  매개 변수를 지정하지 않은 경우에도 함수 이름 뒤에 괄호를 사용해야 합니다.  
  
 **@***p a r a*  
 사용자 정의 함수의 매개 변수입니다. 하나 이상의 매개 변수를 선언할 수 있습니다.  
  
 하나의 함수에 최대 2,100개의 매개 변수를 지정할 수 있습니다. 매개 변수에 기본값이 정의되지 않은 경우 함수를 실행할 때 사용자가 선언된 각 매개 변수의 값을 지정해야 합니다.  
  
 매개 변수 이름을 사용 하 여 지정 된 at 기호 (**@**) 첫 번째 문자로 합니다. 매개 변수 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. 매개 변수는 함수에서 로컬로 사용되므로 다른 함수에서 동일한 매개 변수 이름을 사용할 수 있습니다. 매개 변수는 상수 대신 사용할 수 있지만 테이블 이름, 열 이름 또는 다른 데이터베이스 개체의 이름 대신 사용할 수는 없습니다.  
  
> [!NOTE]  
>  저장 프로시저 또는 사용자 정의 함수에 매개 변수를 전달할 때 또는 일괄 처리 문에서 변수를 선언하고 설정할 때 ANSI_WARNINGS는 인식되지 않습니다. 예를 들어, 변수로 정의 되 면 **char (3)**를 하 고 다음 값으로 설정 된 3 자 보다 큰 데이터 잘리고 정의 된 크기는 INSERT 또는 UPDATE 문이 성공 합니다.  
  
 [ *type_schema_name 합니다.* ] *parameter_data_type*  
 매개 변수 데이터 형식이며 매개 변수 데이터 형식이 속한 스키마가 될 수도 있습니다. 에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 제외한 함수, CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에 사용할 수 있습니다는 **타임 스탬프** 데이터 형식입니다. CLR 함수에 대 한 CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에는 제외 하 고 허용 **텍스트**, **ntext**, **이미지**, 및 **타임 스탬프** 데이터 형식입니다. 비스칼라 형식 **커서** 및 **테이블** 에서 매개 변수 데이터 형식으로 지정할 수 없습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CLR 함수.  
  
 경우 *type_schema_name* 를 지정 하지 않으면는 [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)] 찾습니다는 *parameter_data_type* 다음과 같은 순서로:  
  
-   SQL Server 시스템 데이터 형식의 이름이 들어 있는 스키마  
  
-   현재 데이터베이스에 있는 현재 사용자의 기본 스키마  
  
-   현재 데이터베이스의 **dbo** 스키마  
  
 [  **=**  *기본* ]  
 매개 변수의 기본값입니다. 경우는 *기본* 값이 정의 해당 매개 변수에 대해 값을 지정 하지 않고 함수를 실행할 수 있습니다.  
  
> [!NOTE]  
>  기본 매개 변수 값을 제외 하 고 CLR 함수에 지정할 수 있습니다 **varchar (max)** 및 **varbinary (max)** 데이터 형식입니다.  
  
 함수의 매개 변수에 기본값이 지정되면 기본값을 가져오는 함수를 호출할 때 DEFAULT 키워드를 지정해야 합니다. 이 동작은 매개 변수를 생략할 경우 자동으로 기본값이 사용되는 저장 프로시저에서 기본값이 있는 매개 변수를 사용하는 것과는 다릅니다.  
  
 *return_data_type*  
 스칼라 사용자 정의 함수의 반환 값입니다. 에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 제외한 함수, CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에 사용할 수 있습니다는 **타임 스탬프** 데이터 형식입니다. CLR 함수에 대 한 CLR 사용자 정의 형식을 비롯 한 모든 데이터 형식에는 제외 하 고 허용 **텍스트**, **ntext**, **이미지**, 및 **타임 스탬프** 데이터 형식입니다. 비스칼라 형식 **커서** 및 **테이블** 는 반환 데이터 형식으로 지정할 수 없습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CLR 함수.  
  
 *function_body*  
 테이블을 수정하는 경우처럼 함께 사용해도 부작용이 나타나지 않으며 함수의 값을 정의하는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지정합니다. *function_body* 스칼라 함수와 다중 문 테이블 반환 함수 에서만 사용 됩니다.  
  
 스칼라 함수에서 *function_body* 는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함께 스칼라 값으로 계산 하는 문입니다.  
  
 다중 문 테이블 반환 함수에서 *function_body* 는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블을 채우는 하는 문은 변수를 반환 합니다.  
  
 *scalar_expression*  
 스칼라 함수가 스칼라 값을 반환하도록 지정합니다.  
  
 TABLE  
 테이블 반환 함수의 반환 값이 테이블임을 지정합니다. 상수만 및  **@**  *local_variables* 테이블 반환 함수에 전달 될 수 있습니다.  
  
 인라인 테이블 반환 함수에서 TABLE 반환 값은 단일 SELECT 문을 통해 정의됩니다. 인라인 함수에는 연관된 반환 변수가 없습니다.  
  
 다중 문 테이블 반환 함수에서  **@**  *return_variable* 은 TABLE 변수를 저장 하 고 함수의 값으로 반환 되어야 하는 행이 누적 하는 데 사용 합니다. **@***return_variable* 에 대해서만 지정할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 및 CLR에 대해 작동 합니다.  
  
 *stmt 선택*  
 인라인 테이블 반환 함수의 반환 값을 정의하는 단일 SELECT 문입니다.  
  
 외부 이름 \<method_specifier >*assembly_name.class_name*. *method_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 함수와 바인딩할 어셈블리의 메서드를 지정합니다. *assembly_name* 에 있는 기존 어셈블리와 일치 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 표시 유형으로 현재 데이터베이스에 있습니다. *class_name* 은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자 하며 어셈블리에서 클래스로 존재 해야 합니다. 있는 경우 클래스에 마침표를 사용 하는 정규화 된 네임 스페이스 이름은 (**.**) 네임 스페이스 부분을 구분 하 클래스 이름은 대괄호를 사용 하 여 구분 합니다 (****) 나 따옴표 (**""**). *method_name* 은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자 하며 지정된 된 클래스에서 정적 메서드로 존재 해야 합니다.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR 코드를 실행할 수 없습니다. 만들기, 수정 및 공용 언어 런타임 모듈; 참조 하는 데이터베이스 개체를 삭제 합니다. 그러나 이러한 참조를 실행할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정할 때까지 [clr enabled 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)합니다. 옵션을 사용 하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 *\<*table_type_definition*>***(** { \<column_definition > \<column_constraint > | \<computed_column_definition >} [ \<table_constraint >] [ **,**... *n* ]**)**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수에 대한 테이블 데이터 형식을 정의합니다. 테이블 선언에는 열 정의와 열 또는 테이블 제약 조건이 포함됩니다.  
  
\<clr_table_type_definition > **(** { *column_name**data_type* } [ **,**...  *n*  ] **)** **적용할**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([일부에서 미리 보기 영역](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).  
  
 CLR 함수에 대한 테이블 데이터 형식을 정의합니다. 테이블 선언에는 열 이름과 데이터 형식만 포함됩니다.  
  
 NULL | NOT NULL  
 고유 하 게 컴파일된 스칼라 사용자 정의 함수에 대해서만 지원 합니다. 자세한 내용은 참조 [메모리 내 OLTP에 대 한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)합니다.  
  
 NATIVE_COMPILATION  
 사용자 정의 함수를 고유 하 게 컴파일되어 있는지 여부를 나타냅니다. 이 인수는 고유 하 게 컴파일된 스칼라 사용자 정의 함수에 필요 합니다.  
  
 NATIVE_COMPILATION 인수가 필요한 함수를 변경 하 고 사용할 수만 NATIVE_COMPILATION 인수와 함께 함수가 생성 하는 경우.  
  
 BEGIN ATOMIC와  
 고유 하 게 컴파일된 사용자 정의 스칼라 함수 이며 필수만 지원 합니다. 자세한 내용은 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)을(를) 참조하십시오.  
  
 SCHEMABINDING  
 SCHEMABINDING 인수는 고유 하 게 컴파일된 스칼라 사용자 정의 함수에 필요 합니다.  
  
 **\<function_option >:: = 및 \<clr_function_option >:: =**  
  
 함수에 다음 옵션 중 하나 이상이 적용되도록 지정합니다.  
  
 ENCRYPTION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 ALTER FUNCTION 문의 텍스트가 포함된 카탈로그 뷰 열을 암호화하도록 지정합니다. ENCRYPTION을 사용하면 함수가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제의 일부로 게시되는 것을 방지할 수 있습니다. CLR 함수에는 ENCRYPTION을 지정할 수 없습니다.  
  
 SCHEMABINDING  
 함수를 함수가 참조하는 데이터베이스 개체에 바인딩되도록 지정합니다. 이 경우 다른 스키마 바운드 개체가 이를 참조해도 함수가 변경되지 않습니다.  
  
 다음 동작 중 하나만 발생해도 참조하는 개체에 대한 함수 바인딩이 제거됩니다.  
  
-   함수가 삭제된 경우  
  
-   SCHEMABINDING 옵션을 지정하지 않은 상태에서 ALTER 문을 사용하여 함수를 수정한 경우  
  
함수는 스키마 바운드 수 전에 충족 해야 하는 조건 목록에 대 한 참조 [CREATE function&#40; Transact SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
 RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT  
 지정 된 **OnNULLCall** 특성 스칼라 반환 함수입니다. 이 특성을 지정하지 않으면 기본적으로 CALLED ON NULL INPUT이 적용됩니다. 즉, 인수로 NULL이 전달되는 경우에도 함수 본문이 실행됩니다.  
  
 CLR 함수에 RETURNS NULL ON NULL INPUT을 지정할 경우 받은 인수 중 하나라도 NULL이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 실제로 함수의 본문을 호출하지 않고 NULL을 반환할 수 있습니다. 에 지정 된 메서드가 경우 \<method_specifier > 반환 NULL ON NULL INPUT을 있지만 ALTER FUNCTION 문에서 ON NULL INPUT을 나타내고, ALTER FUNCTION 문이 우선 적용을 나타내는 사용자 지정 특성에 이미 있습니다. **OnNULLCall** CLR 테이블 반환 함수에 대 한 특성을 지정할 수 없습니다.  
  
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
 열에 대한 데이터 정렬을 지정합니다. 이를 지정하지 않으면 열에 데이터베이스의 기본 데이터 정렬이 할당됩니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 목록 및 자세한 정보에 대 한 참조 [Windows 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) 및 [SQL Server 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 열에 대해서만 되는 데이터 정렬을 변경 하려면 COLLATE 절을 사용할 수는 **char**, **varchar**, **nchar**, 및 **nvarchar** 데이터 형식입니다.  
  
 CLR 테이블 반환 함수에는 COLLATE를 지정할 수 없습니다.  
  
 ROWGUIDCOL  
 새 열이 행 전역 고유 식별자 열임을 나타냅니다. 하나의 **uniqueidentifier** 테이블당 열 ROWGUIDCOL 열으로 지정 될 수 있습니다. ROWGUIDCOL 속성에만 할당할 수는 **uniqueidentifier** 열입니다.  
  
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
  
 PAD_INDEX = { ON | OFF }  
 인덱스 패딩을 지정합니다. 기본값은 OFF입니다.  
  
 FILLFACTOR = *fillfactor*  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 인덱스 생성 또는 변경 중에 각 인덱스 페이지의 리프 수준에 대한 채우기 정도를 나타내는 비율을 지정합니다. *fillfactor* 100 1 까지의 정수 값 이어야 합니다. 기본값은 0입니다.  
  
 IGNORE_DUP_KEY = { ON | OFF }  
 삽입 작업에서 고유 인덱스에 중복된 키 값을 삽입하려는 경우에 대한 오류 응답을 지정합니다. IGNORE_DUP_KEY 옵션은 인덱스를 만들거나 다시 작성한 후의 삽입 작업에만 적용됩니다. 기본값은 OFF입니다.  
  
 STATISTICS_NORECOMPUTE = { ON | OFF }  
 배포 통계를 다시 계산할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ALLOW_ROW_LOCKS = { ON | OFF }  
 행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ALLOW_PAGE_LOCKS = { ON | OFF }  
 페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
## <a name="remarks"></a>주의  
 ALTER FUNCTION을 사용하여 스칼라 반환 함수를 테이블 반환 함수로 변경하거나 그 반대로 변경할 수 없습니다. 또한 ALTER FUNCTION을 사용하여 인라인 함수를 다중 문 함수로 변경하거나 그 반대로 변경할 수 없습니다. ALTER FUNCTION을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 CLR 함수로 변경하거나 그 반대로 변경할 수도 없습니다.  
  
 다음 Service Broker 문은의 정의에 포함 될 수 없습니다는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수:  
  
-   BEGIN DIALOG CONVERSATION  
-   END CONVERSATION  
-   GET CONVERSATION GROUP  
-   MOVE CONVERSATION  
-   RECEIVE  
-   SEND  
  
## <a name="permissions"></a>Permissions  
 함수 또는 스키마에 대한 ALTER 권한이 필요합니다. 함수에 사용자 정의 형식이 지정되면 해당 유형에 대한 EXECUTE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [DROP function&#40; Transact SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

