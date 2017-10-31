---
title: INSERT (Transact SQL) | Microsoft Docs
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
- INSERT_TSQL
- INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- inserting multiple rows
- user-defined types [SQL Server], inserting values
- DML [SQL Server], INSERT statement
- bulk load [SQL Server]
- row additions [SQL Server], INSERT statement
- inserting rows
- table value constructor [SQL Server]
- adding data
- INSERT statement [SQL Server], about INSERT statement
- INSERT statement [SQL Server]
- UDTs [SQL Server], inserting values
- adding rows
- INSERT INTO statement
- data manipulation language [SQL Server], INSERT statement
- inserting data
ms.assetid: 1054c76e-0fd5-4131-8c07-a6c5d024af50
caps.latest.revision: 136
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ef8387c2bbbc109ad7ec325e4faf632a983d96c9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="insert-transact-sql"></a>INSERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이블 또는 뷰에 새 행을 하나 이상 추가합니다. 예제를 보려면 [예제](#InsertExamples)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ ( column_list ) ]   
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
  table_or_view_name  
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  
```  
  
```  
-- External tool only syntax  

INSERT   
{  
    [BULK]  
    [ database_name . [ schema_name ] . | schema_name . ]  
    [ table_name | view_name ]  
    ( <column_definition> )  
    [ WITH (  
        [ [ , ] CHECK_CONSTRAINTS ]  
        [ [ , ] FIRE_TRIGGERS ]  
        [ [ , ] KEEP_NULLS ]  
        [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]  
        [ [ , ] ROWS_PER_BATCH = rows_per_batch ]  
        [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]  
        [ [ , ] TABLOCK ]  
    ) ]  
}  
  
[; ] <column_definition> ::=  
 column_name <data_type>  
    [ COLLATE collation_name ]  
    [ NULL | NOT NULL ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

INSERT INTO [ database_name . [ schema_name ] . | schema_name . ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    {   
      VALUES ( { NULL | expression } )  
      | SELECT <select_criteria>  
    }  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
[;]  
```  
  
## <a name="arguments"></a>인수  
 와 \<common_table_expression >  
 INSERT 문의 범위 내에 정의되는 임시로 명명된 결과 집합(공통 테이블 식이라고도 함)을 지정합니다. 결과 집합은 SELECT 문에서 파생됩니다. 자세한 내용은 참조 [common_table_expression &AMP; #40; Transact SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP (*식*) [%]  
 삽입할 임의 행의 수 또는 비율을 지정합니다. *expression* 은 행의 수 또는 비율일 수 있습니다. 자세한 내용은 참조 [top&#40; Transact SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 INTO  
 INSERT와 대상 테이블 사이에 사용할 수 있는 선택적 키워드입니다.  
  
 *server_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 테이블 또는 뷰가 있는 연결된 서버의 이름입니다. *server_name* 로 지정할 수 있습니다는 [연결 된 서버](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 이름 또는를 사용 하 여는 [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 함수입니다.  
  
 때 *server_name* 연결 된 서버로 지정 *database_name* 및 *schema_name* 필요 합니다. 때 *server_name* OPENDATASOURCE, 지정 된 *database_name* 및 *schema_name* OLE DB의 기능에 따라 되며 모든 데이터 원본에는 적용 되지 않을 수 있습니다 원격 개체에 액세스 하는 공급자입니다.  
  
 *database_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이나 뷰가 속한 스키마의 이름입니다.  
  
 *table_or view_name*  
 데이터를 받는 테이블 또는 뷰의 이름입니다.  
  
 A [테이블](../../t-sql/data-types/table-transact-sql.md) 변수는 해당 범위 내에서 INSERT 문의 테이블 원본으로 사용할 수 있습니다.  
  
 참조 되는 뷰 *table_or_view_name* 업데이트할 수 있도록 하 고 보기의 FROM 절에서 정확히 한 개의 기본 테이블을 참조 해야 합니다. 예를 들어 여러 테이블 뷰에 대해 INSERT를 사용 해야 합니다는 *column_list* 하나의 기본 테이블 열만 참조 하는 합니다. 업데이트할 수 있는 뷰에 대 한 자세한 내용은 참조 하세요. [CREATE view&#40; Transact SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이 [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 함수입니다. 이러한 함수의 사용은 원격 개체에 액세스하는 OLE DB 공급자의 기능에 영향을 받습니다.  
  
 와 ( \<table_hint_limited > [... *n* ] )  
 대상 테이블에 허용되는 하나 이상의 테이블 힌트를 지정합니다. WITH 키워드와 괄호가 필요합니다.  
  
 READPAST, NOLOCK 및 READUNCOMMITTED는 허용되지 않습니다. 테이블 힌트에 대 한 자세한 내용은 참조 [테이블 힌트 &#40; Transact SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
> [!IMPORTANT]  
>  INSERT 문의 대상 테이블에 HOLDLOCK, SERIALIZABLE, READCOMMITTED, REPEATABLEREAD 또는 UPDLOCK 힌트를 지정하는 기능은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 이러한 힌트는 INSERT 문의 성능에 영향을 주지 않습니다. 향후 개발 작업에서는 이러한 힌트를 사용하지 않도록 하고 현재 이 힌트를 사용하는 응용 프로그램은 수정하세요.  
  
 INSERT 문의 대상 테이블에 TABLOCK 힌트를 지정하는 것은 TABLOCKX 힌트를 지정하는 것과 결과가 같습니다. 두 경우 모두 테이블이 배타적으로 잠깁니다.  
  
 (*column_list*)  
 데이터를 삽입할 하나 이상의 열 목록입니다. *column_list* 괄호로 묶고 쉼표로 구분 해야 합니다.  
  
 열에 없는 경우 *column_list*, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 제공할 수 있어야 열 정의에 따라 값을, 그렇지 않으면 행을 로드할 수 없습니다. 열이 다음과 같은 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 자동으로 열의 값을 제공합니다.  
  
-   IDENTITY 속성이 있는 경우. 다음 증분 ID 값이 사용됩니다.  
  
-   기본값이 있는 경우. 열의 기본값이 사용됩니다.  
  
-   에 **타임 스탬프** 데이터 형식입니다. 현재 타임스탬프 값이 사용됩니다.  
  
-   Null을 허용합니다. Null 값이 사용됩니다.  
  
-   계산 열입니다. 계산된 값이 사용됩니다.  
  
*column_list* 명시적 값을 id 열에 삽입 되 고 SET IDENTITY_INSERT 옵션은 테이블에 대 한 ON 이어야 할 때 사용 해야 합니다.  
  
OUTPUT Clause  
 삽입 작업의 일부로 삽입된 행을 반환합니다. 결과는 처리 중인 응용 프로그램에 반환되거나 다음 처리를 위해 테이블 또는 테이블 변수에 삽입될 수 있습니다.  
  
 [OUTPUT 절](../../t-sql/queries/output-clause-transact-sql.md) 로컬 분할된 뷰, 분산형된 분할된 뷰 또는 원격 테이블을 참조 하는 DML 문 또는 INSERT 문을 포함 하는 지원 되지 않습니다는 *execute_statement*. 포함 하는 INSERT 문에서 OUTPUT INTO 절이 지원 되지 않습니다는 \<dml_table_source > 절. 
  
 VALUES  
 삽입할 데이터 값의 목록을 표시합니다. 각 열에 대해 하나의 데이터 값이 있어야 *column_list*, 지정 하거나, 테이블에 있습니다. 값 목록은 괄호로 묶어야 합니다.  
  
 값 목록의 값에는 없는 경우 테이블의 열 순서와 같거나 테이블의 각 열에 대 한 값을 포함 하지 *column_list* 는 각각의 받는 값을 저장 하는 열을 명시적으로 지정 하는 데 사용 합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 행 생성자(테이블 값 생성자라고도 함)를 사용하여 하나의 INSERT 문에 여러 행을 지정할 수 있습니다. 행 생성자는 여러 개의 값 목록을 괄호로 묶고 쉼표로 구분한 하나의 VALUES 절로 구성됩니다. 자세한 내용은 참조 [테이블 값 생성자 &#40; Transact SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 DEFAULT  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 열에 대해 정의된 기본값을 로드하도록 설정합니다. 열에 대한 기본값이 없고 열에 Null  값을 사용할 수 있는 경우에는 NULL이 삽입됩니다. 으로 정의 된 열에 대 한는 **타임 스탬프** 데이터 형식, 다음 타임 스탬프 값이 삽입 됩니다. ID  열에는 DEFAULT를 사용할 수 없습니다.  
  
 *expression*  
 상수,  변수 또는 식입니다. 식은 EXECUTE  문을 포함할 수 없습니다.  
  
 유니코드 문자 데이터 형식을 참조할 때는 **nchar**, **nvarchar**, 및 **ntext**, '*식*' 접두사로와 야는 대문자 ' N '입니다. 'N'을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 또는 열의 기본 데이터 정렬에 해당하는 코드 페이지로 문자열을 변환합니다. 이 코드 페이지에 없는 문자는 모두 손실됩니다.  
  
 *파생 _ 테이블*  
 테이블에 로드할 데이터 행을 반환하는 유효한 SELECT 문입니다. SELECT 문은 CTE(공통 테이블 식)를 포함할 수 없습니다.  
  
 *execute_statement*  
 SELECT 또는 READTEXT 문을 사용하여 데이터를 반환하는 유효한 EXECUTE 문입니다. 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)을 참조하세요.  
  
 INSERT…EXEC 문에서 EXECUTE 문의 RESULT SETS 옵션을 지정할 수 없습니다.  
  
 경우 *execute_statement* 는 insert, 각 결과 집합 또는 테이블의 열과 호환 되어야 합니다 *column_list*합니다.  
  
 *execute_statement* 는 동일한 서버 또는 원격 서버에서 저장된 프로시저를 실행 하는 데 사용할 수 있습니다. 원격 서버에서 프로시저를 실행하면 결과 집합이 로컬 서버에 반환되어 로컬 서버의 테이블에 로드됩니다. 분산 트랜잭션에서 *execute_statement* 연결에 사용할 수 있는 여러 활성 결과 집합 (MARS) 하는 경우 루프백 연결 된 서버에 대해 실행 될 수 없습니다.  
  
 경우 *execute_statement* 데이터 반환 READTEXT 문을 사용 하 여 각 READTEXT 문은 최대 1MB (1024KB)의 데이터를 반환할 수 있습니다. *execute_statement* 확장된 프로시저와 함께 사용할 수도 있습니다. *하지만 execute_statement* 확장된 프로시저의 주 스레드에서 반환 하는 데이터는 삽입 주 스레드를 제외한 스레드에서 나온 출력은 삽입 되지 않으면 합니다.  
  
 테이블 반환 매개 변수를 INSERT EXEC 문의 대상으로 지정할 수는 없지만 INSERT EXEC 문자열 또는 저장 프로시저의 원본으로 지정할 수 있습니다. 자세한 내용은 [테이블 반환 매개 변수 사용&#40;데이터베이스 엔진&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)을 참조하세요.  
  
 \<dml_table_source >  
 INSERT, UPDATE, DELETE 또는 MERGE 문의 OUTPUT 절에서 반환하고 선택적으로 WHERE 절로 필터링되는 행이 대상 테이블에 삽입되도록 지정합니다. 경우 \<dml_table_source >를 지정 외부 INSERT 문의 대상에는 다음과 같은 제한 사항을 충족 해야 합니다. 
  
-   뷰가 아니라 기본 테이블이어야 합니다.  
  
-   원격 테이블일 수 없습니다.  
  
-   정의된 트리거를 포함할 수 없습니다.  
  
-   기본 키-외래 키 관계에 참여할 수 없습니다.  
  
-   트랜잭션 복제에 대한 병합 복제 또는 업데이트할 수 있는 구독에 참여할 수 없습니다.  
  
 데이터베이스의 호환성 수준이 100 이상으로 설정되어야 합니다. 자세한 내용은 참조 [OUTPUT 절 &#40; Transact SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 \<select_list >  
 OUTPUT 절에서 반환된 열 중 삽입할 열을 지정하는 쉼표로 구분된 목록입니다. 열 \<select_list > 값은 삽입 되는 열과 호환 되어야 합니다. \<select_list > 집계 함수 또는 TEXTPTR을 참조할 수 없습니다. 
  
> [!NOTE]  
>  원래 값으로 변경의 항목에 관계 없이 SELECT 목록에 나열 된 모든 변수 참조 \<dml_statement_with_output_clause > 합니다.  
  
 \<dml_statement_with_output_clause >  
 OUTPUT 절에서 영향을 받는 행을 반환하는 유효한 INSERT, UPDATE, DELETE 또는 MERGE 문입니다. 이 문은 WITH 절을 포함할 수 없으며 원격 테이블 또는 분할 뷰를 대상으로 할 수 없습니다. UPDATE 또는 DELETE가 지정된 경우 커서 기반의 UPDATE 또는 DELETE일 수 없습니다. 원본 행은 중첩된 DML 문으로 참조될 수 없습니다.  
  
 여기서 \<c h _ c >  
 WHERE 절을 포함 하는 유효한 \<c h _ c >에서 반환 된 행을 필터링 하는 \<dml_statement_with_output_clause > 합니다. 자세한 내용은 참조 [검색 조건 &#40; Transact SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md). 이 컨텍스트에서 사용할 경우 \<c h _ c > 하위 쿼리, 데이터 액세스, 집계 함수, TEXTPTR 또는 전체 텍스트 검색 조건자를 수행 하는 스칼라 사용자 정의 함수를 포함할 수 없습니다. 
  
 DEFAULT VALUES  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 새 행이 각 열에 대해 정의된 기본값을 포함하도록 설정합니다.  
  
 BULK  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이진 데이터 스트림을 업로드하기 위해 외부 도구에서 사용됩니다. 이 옵션은이 아니며 도구와 함께 사용 하기 위해와 같은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], SQLCMD, OSQL, 또는 데이터 액세스 응용 프로그래밍 인터페이스와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client입니다.  
  
 FIRE_TRIGGERS  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이진 데이터 스트림 업로드 작업 중에 대상 테이블에 정의된 삽입 트리거가 실행되도록 지정합니다. 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
 CHECK_CONSTRAINTS  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이진 데이터 스트림 업로드 작업 중에 대상 테이블 또는 뷰의 모든 제약 조건을 검사하도록 지정합니다. 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
 KEEPNULLS  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이진 데이터 스트림 업로드 작업 중에 빈 열이 Null 값을 유지하도록 지정합니다. 자세한 내용은 [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)을 참조하세요.  
  
 KILOBYTES_PER_BATCH = kilobytes_per_batch  
 크기 (KB)로 일괄 처리당 데이터의 대략적인 수를 지정 *kilobytes_per_batch*합니다. 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이진 데이터 스트림의 데이터 행 수를 대략적으로 나타냅니다. 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
>  [!NOTE]
>  열 목록이 제공 되지 않으면 구문 오류가 발생 합니다.  

## <a name="remarks"></a>주의  
SQL 그래프 테이블에 데이터 삽입에 관련 된 정보를 참조 하십시오. [INSERT (SQL 그래프)](../../t-sql/statements/insert-sql-graph.md)합니다. 

## <a name="best-practices"></a>최선의 구현 방법  
 사용 된 @@ROWCOUNT 삽입 된 클라이언트 응용 프로그램에는 행의 수를 반환 하는 함수입니다. 자세한 내용은 참조 [@@ROWCOUNT &#40; Transact SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).  
  
### <a name="best-practices-for-bulk-importing-data"></a>데이터 대량 가져오기에 대한 최선의 구현 방법  
  
#### <a name="using-insert-intoselect-to-bulk-import-data-with-minimal-logging"></a>INSERT INTO…SELECT를 사용하여 최소 로깅으로 데이터 대량 가져오기  
 사용할 수 있습니다 `INSERT INTO <target_table> SELECT <columns> FROM <source_table>` 효율적으로 최소 로깅 사용 하 여 다른 테이블에 준비 테이블 같은 한 테이블에서 많은 수의 행을 전송할 수 있습니다. 최소 로깅은 문의 성능을 향상시키고 트랜잭션 중에 사용 가능한 트랜잭션 로그 공간을 꽉 채울 가능성을 줄일 수 있습니다.  
  
 이 문의 최소 로깅을 위해서는 다음 요구 사항이 충족되어야 합니다.  
  
-   데이터베이스의 복구 모델이 단순 또는 대량 로그로 설정되어야 합니다.  
  
-   대상 테이블은 비어 있거나 비어 있지 않은 힙이어야 합니다.  
  
-   대상 테이블이 복제에 사용되지 않아야 합니다.  
  
-   TABLOCK 힌트가 대상 테이블에 지정되어야 합니다.  
  
MERGE 문의 삽입 동작 결과로 힙에 삽입되는 행도 최소 로깅이 가능합니다.  
  
 덜 제한적인 대량 업데이트 잠금을 보유하는 BULK INSERT 문과 달리 TABLOCK 힌트를 사용하는 INSERT INTO…SELECT는 테이블에 대해 배타적(X) 잠금을 보유합니다. 즉, 병렬 삽입 작업을 사용하여 행을 삽입할 수 없습니다.  
  
#### <a name="using-openrowset-and-bulk-to-bulk-import-data"></a>OPENROWSET 및 BULK를 사용하여 데이터 대량 가져오기  
 OPENROWSET 함수에는 INSERT 문을 사용하여 대량 로드 최적화를 제공하는 다음과 같은 테이블 힌트를 사용할 수 있습니다.  
  
-   TABLOCK 힌트는 삽입 작업에 대한 로그 레코드의 수를 최소화할 수 있습니다. 데이터베이스 복구 모델은 단순 또는 대량 로그로 설정되어야 하며 대상 테이블은 복제에 사용될 수 없습니다. 자세한 내용은 참조 [대량 가져오기의 최소 로깅을 위한 선행 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)합니다.  
  
-   IGNORE_CONSTRAINTS 힌트는 FOREIGN KEY 및 CHECK 제약 조건 검사를 일시적으로 해제할 수 있습니다.  
  
-   IGNORE_TRIGGERS 힌트는 트리거 실행을 일시적으로 해제할 수 있습니다.  
  
-   KEEPDEFAULTS 힌트를 사용하면 데이터 레코드에 열 값이 없는 경우 NULL 대신 테이블 열의 기본값(있는 경우)을 삽입할 수 있습니다.  
  
-   KEEPIDENTITY 힌트를 사용하면 가져온 데이터 파일의 ID 값을 대상 테이블의 ID 열에 사용할 수 있습니다.  
  
이러한 최적화는 BULK INSERT 명령에서 사용할 수 있는 최적화와 비슷합니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
## <a name="data-types"></a>데이터 형식  
 행을 삽입할 때는 다음과 같은 데이터 형식 동작을 고려해야 합니다.  
  
-   값을 가진 열에 로드 되 면 한 **char**, **varchar**, 또는 **varbinary** 데이터 형식, 안쪽 여백 또는 후행 공백이 잘리지 (공백  **char** 및 **varchar**, 0 **varbinary**) 테이블을 만들 때 열에 정의 된 SET ANSI_PADDING 설정에 의해 결정 됩니다. 자세한 내용은 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.  
  
     다음 표에서는 SET ANSI_PADDING이 OFF일 때의 기본 작업을 보여 줍니다.  
  
    |데이터 형식|기본 작업|  
    |---------------|-----------------------|  
    |**char**|정의된 열 너비만큼 공백으로 값을 채웁니다.|  
    |**varchar**|공백이 아닌 마지막 문자 또는 단일 공백 문자(공백으로만 구성된 문자열의 경우)에 대한 후행 공백을 제거합니다.|  
    |**varbinary**|후행 0을 제거합니다.|  
  
-   빈 문자열 (' ') 인 열에 로드 되는 **varchar** 또는 **텍스트** 데이터 형식, 기본 작업은 빈 문자열을 로드 합니다.  
  
-   에 null 값을 삽입 한 **텍스트** 또는 **이미지** 8KB 텍스트 페이지 사용해 나 열에 유효한 텍스트 포인터를 만들지 않습니다.  
  
-   사용 하 여 만든 열에서 **uniqueidentifier** 데이터 형식 저장소 특별 하 게 서식이 지정 된 16 바이트 이진 값입니다. 와 달리 id 열이 있는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인 열에 대 한 값을 자동으로 생성 되지 않습니다는 **uniqueidentifier** 데이터 형식입니다. 삽입 작업 중에 데이터 형식의 변수 **uniqueidentifier** 문자열 형태로 상수 및 *xxxxxxxx-xxxx-xxxx-개의 자릿수* (하이픈을 포함 하 여 36 자 여기서 *x* 범위 0-9 또는 a-f에서 16 진수)에 사용할 수 있습니다 **uniqueidentifier** 열입니다. 예를 들어 6F9619FF-8B86-D011-B42D-00C04FC964FF는 유효한 값에 대 한는 **uniqueidentifier** 변수 또는 열입니다. 사용 하 여는 [newid ()](../../t-sql/functions/newid-transact-sql.md) 함수는 전역적으로 고유 ID (GUID)입니다.  
  
### <a name="inserting-values-into-user-defined-type-columns"></a>사용자 정의 형식 열에 값 삽입  
 다음과 같은 방법으로 사용자 정의 형식 열에 값을 삽입할 수 있습니다.  
  
-   사용자 정의 형식의 값을 제공합니다.  
  
-   사용자 정의 형식에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식의 암시적 또는 명시적 변환이 지원되는 경우 해당 형식의 값을 제공합니다. 다음 예제에서는 사용자 정의 형식의 열에 값을 삽입 하는 방법을 보여 줍니다. `Point`, 명시적으로 문자열로 변환 합니다.  
  
    ```  
    INSERT INTO Cities (Location)  
    VALUES ( CONVERT(Point, '12.3:46.2') );  
    ```  
  
     모든 사용자 정의 형식은 이진 형식에서 암시적으로 변환할 수 있으므로 명시적 변환을 수행하지 않고도 이진 값을 제공할 수 있습니다.  
  
-   사용자 정의 형식의 값을 반환하는 사용자 정의 함수를 호출합니다. 다음 예에서는 사용자 정의 함수 `CreateNewPoint()`를 사용하여 사용자 정의 형식 `Point`의 새 값을 만들고 이 값을 `Cities` 테이블에 삽입합니다.  
  
    ```  
    INSERT INTO Cities (Location)  
    VALUES ( dbo.CreateNewPoint(x, y) );  
    ```  
  
## <a name="error-handling"></a>오류 처리  
 TRY…CATCH 구문에 문을 지정하여 INSERT 문에 대한 오류 처리를 구현할 수 있습니다.  
  
 INSERT 문이 제약 조건 또는 규칙을 위반하거나 열의 데이터 형식과 호환되지 않는 값을 포함하는 경우 문이 실패하고 오류 메시지가 반환됩니다.  
  
 INSERT가 SELECT 또는 EXECUTE를 사용하여 여러 행을 로드하는 경우 로드되는 값 중에서 규칙 또는 제약 조건 위반이 발생하면 INSERT 문이 중지되고 행이 로드되지 않습니다.  
  
 식 평가 중에 INSERT 문에서 오버플로, 0으로 나누기 또는 도메인 오류와 같은 산술 오류가 발생하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 이러한 오류를 SET ARITHABORT가 ON으로 설정된 것처럼 처리합니다. 즉, 일괄 처리가 중지되고 오류 메시지가 반환됩니다. SET ARITHABORT 및 SET ANSI_WARNINGS가 OFF인 경우 식 평가 중에 INSERT, DELETE 또는 UPDATE 문에서 오버플로, 0으로 나누기 또는 도메인 오류와 같은 산술 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 NULL 값을 삽입하거나 업데이트합니다. 대상 열이 Null 허용이 아니면 삽입이나 업데이트 동작이 실패하고 사용자에게 오류 메시지가 보내집니다.  
  
## <a name="interoperability"></a>상호 운용성  
 테이블 또는 뷰에 대한 INSERT 동작에 INSTEAD OF 트리거가 정의되면 INSERT 문 대신 트리거가 실행됩니다. Instead of 트리거에 대 한 자세한 내용은 참조 하세요. [CREATE trigger&#40; Transact SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 원격 테이블에 값을 삽입하는 경우 모든 열에서 지정되지 않은 값이 있으면 지정된 값을 삽입할 열을 식별해야 합니다.  
  
 TOP을 INSERT와 함께 사용할 경우 참조된 행은 어떠한 순서로도 정렬되지 않으며 ORDER BY 절을 이 문에서 직접 지정할 수 없습니다. TOP을 사용하여 시간 순서로 행을 삽입해야 할 경우 하위 SELECT 문에서 지정된 ORDER BY 절과 함께 TOP을 사용해야 합니다. 이 항목의 뒷부분에 나오는 예 섹션을 참조하세요.
 
ORDER BY와 함께 id 값이 계산 되는 방식을 행 보장 하지만 행이 삽입 순서가 아니라를 채우는 데 사용 하는 삽입 쿼리를 선택 합니다.    
  
## <a name="logging-behavior"></a>로깅 동작  
 OPENROWSET 함수에 BULK 키워드를 사용 하는 경우 또는 사용 하는 경우를 제외 하 고 INSERT 문은 항상 모두 기록은 `INSERT INTO <target_table> SELECT <columns> FROM <source_table>`합니다. 이러한 작업을 최소한으로 기록할 수 있습니다. 자세한 내용은 이 항목의 앞부분에 나오는 "데이터 대량 로드를 위한 최선의 구현 방법" 섹션을 참조하세요.  
  
## <a name="security"></a>보안  
 연결된 서버 연결이 진행되는 동안 보내는 서버는 연결된 서버 대신 로그인 이름과 암호를 제공하여 받는 서버에 연결합니다. 이 연결이 작동 하려면 사용 하 여 연결 된 서버 간의 로그인 매핑을 만들어야 [sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)합니다.  
  
 OPENROWSET(BULK…)을 사용할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가장을 처리하는 방식을 이해하는 것이 중요합니다. 자세한 내용은의 "보안 고려 사항" 참조 [를 사용 하 여 BULK INSERT 또는 openrowset&#40; 하 여 데이터 대량 가져오기 대량... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Permissions  
 대상 테이블에 대해 INSERT 권한이 필요합니다.  
  
 멤버에 대 한 기본 권한을 삽입는 **sysadmin** 고정 서버 역할의 **db_owner** 및 **db_datawriter** 고정 데이터베이스 역할 및 테이블 소유자입니다. 멤버는 **sysadmin**, **db_owner**, 및 **db_securityadmin** 역할 및 테이블 소유자 권한을 다른 사용자에 게 위임할 수 있습니다.  
  
 INSERT OPENROWSET 함수의 BULK 옵션을 실행 하려면의 구성원 이어야는 **sysadmin** 고정된 서버 역할 또는 **bulkadmin** 고정된 서버 역할입니다.  
  
##  <a name="InsertExamples"></a> 예  
  
|범주|중요한 구문 요소|  
|--------------|------------------------------|  
|[기본 구문](#BasicSyntax)|INSERT • 테이블 값 생성자|  
|[열 값 처리](#ColumnValues)|IDENTITY • NEWID • 기본값 • 사용자 정의 형식|  
|[다른 테이블의 데이터를 삽입합니다.](#OtherTables)|INSERT…SELECT • INSERT…EXECUTE • WITH 공통 테이블 식 • TOP • OFFSET FETCH|  
|[표준 테이블 이외의 대상 개체 지정](#TargetObjects)|뷰 • 테이블 변수|  
|[원격 테이블에 행을 삽입합니다.](#RemoteTables)|연결된 서버 • OPENQUERY 행 집합 함수 • OPENDATASOURCE 행 집합 함수|  
|[테이블 또는 데이터 파일에서 데이터 대량 로드](#BulkLoad)|INSERT…SELECT • OPENROWSET 함수|  
|[힌트를 사용 하 여 쿼리 최적화 프로그램의 기본 동작 재정의](#TableHints)|테이블 힌트|  
|[INSERT 문의 결과 캡처](#CaptureResults)|OUTPUT 절|  
  
###  <a name="BasicSyntax"></a>기본 구문  
 이 섹션의 예에서는 최소 필수 구문을 사용하여 INSERT 문의 기본 기능을 보여 줍니다.  
  
#### <a name="a-inserting-a-single-row-of-data"></a>1. 단일 데이터 행 삽입  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Production.UnitMeasure` 테이블에 한 행을 삽입합니다. 이 테이블의 열은 `UnitMeasureCode`, `Name` 및 `ModifiedDate`입니다. 모든 열에 대 한 값 제공 되는 테이블의 열과 같은 순서로 나열 하므로, 열 이름 열 목록에 지정할 필요가*합니다.*  
  
```  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT', N'Feet', '20080414');  
```  
  
#### <a name="b-inserting-multiple-rows-of-data"></a>2. 여러 데이터 행 삽입  
 다음 예제에서는 [테이블 값 생성자](../../t-sql/queries/table-value-constructor-transact-sql.md) 세 개의 행을 삽입 하는 `Production.UnitMeasure` 테이블에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 단일 INSERT 문에 데이터베이스입니다. 모든 열에 대한 값이 제공되어 있고 값이 테이블 내의 열과 같은 순서로 나열되어 있기 때문에 열 목록에 열 이름을 지정할 필요가 없습니다.  
  
```  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923')
    , (N'Y3', N'Cubic Yards', '20080923');  
```  
  
#### <a name="c-inserting-data-that-is-not-in-the-same-order-as-the-table-columns"></a>3. 테이블 열과 순서가 다른 데이터 삽입  
 다음 예에서는 열 목록을 사용하여 각 열에 삽입되는 값을 명시적으로 지정합니다. 열 순서는 `Production.UnitMeasure` 테이블에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스가 `UnitMeasureCode`, `Name`, `ModifiedDate`있지만 열이에 해당 순서로 나열 되지 *column_list*합니다.  
  
```  
INSERT INTO Production.UnitMeasure (Name, UnitMeasureCode,  
    ModifiedDate)  
VALUES (N'Square Yards', N'Y2', GETDATE());  
```  
  
###  <a name="ColumnValues"></a>열 값 처리  
 이 섹션의 예에는 기본 값, IDENTITY 속성으로 정의 된 또는 같은 데이터 형식으로 정의 하는 열에 값을 삽입 하는 방법을 보여 줍니다 **uniqueidentifer** 또는 사용자 정의 형식 열입니다.  
  
#### <a name="d-inserting-data-into-a-table-with-columns-that-have-default-values"></a>4. 기본값을 갖는 열이 포함된 테이블에 데이터 삽입  
 다음 예에서는 자동으로 값을 생성하거나 기본값을 갖는 열이 있는 테이블에 행을 삽입하는 방법을 보여 줍니다. `Column_1`은 `column_2`에 삽입된 값과 문자열을 연결하여 자동으로 값을 생성하는 계산 열입니다. `Column_2`는 기본 제약 조건으로 정의됩니다. 이 열에 값이 지정되지 않으면 기본값이 사용됩니다. `Column_3`사용 하 여 정의 **rowversion** 데이터 형식으로 자동으로 고유한 증분 이진수를 생성 합니다. `Column_4`는 값을 자동으로 생성하지 않습니다. 이 열의 값이 지정되지 않으면 NULL이 삽입됩니다. INSERT 문은 전체 열이 아니라 일부 열의 값을 포함하는 행을 삽입합니다. 마지막 INSERT 문에는 열이 지정되지 않고 DEFAULT VALUES 절을 사용하여 기본값만 삽입됩니다.  
  
```  
CREATE TABLE dbo.T1   
(  
    column_1 AS 'Computed column ' + column_2,   
    column_2 varchar(30)   
        CONSTRAINT default_name DEFAULT ('my column default'),  
    column_3 rowversion,  
    column_4 varchar(40) NULL  
);  
GO  
INSERT INTO dbo.T1 (column_4)   
    VALUES ('Explicit value');  
INSERT INTO dbo.T1 (column_2, column_4)   
    VALUES ('Explicit value', 'Explicit value');  
INSERT INTO dbo.T1 (column_2)   
    VALUES ('Explicit value');  
INSERT INTO T1 DEFAULT VALUES;   
GO  
SELECT column_1, column_2, column_3, column_4  
FROM dbo.T1;  
GO  
```  
  
#### <a name="e-inserting-data-into-a-table-with-an-identity-column"></a>5. ID 열이 있는 테이블에 데이터 삽입  
 다음 예에서는 ID 열에 데이터를 삽입하는 다양한 방법을 보여 줍니다. 처음 두 INSERT 문은 새 행에 대해 ID 값을 생성할 수 있도록 합니다. 세 번째 INSERT 문은 SET IDENTITY_INSERT 문으로 열의 IDENTITY 속성을 재정의하고 ID 열에 명시적 값을 삽입합니다.  
  
```  
CREATE TABLE dbo.T1 ( column_1 int IDENTITY, column_2 VARCHAR(30));  
GO  
INSERT T1 VALUES ('Row #1');  
INSERT T1 (column_2) VALUES ('Row #2');  
GO  
SET IDENTITY_INSERT T1 ON;  
GO  
INSERT INTO T1 (column_1,column_2)   
    VALUES (-99, 'Explicit identity value');  
GO  
SELECT column_1, column_2  
FROM T1;  
GO  
```  
  
#### <a name="f-inserting-data-into-a-uniqueidentifier-column-by-using-newid"></a>6. NEWID()를 사용하여 uniqueidentifier 열에 데이터 삽입  
 다음 예제에서는 [NEWID](../../t-sql/functions/newid-transact-sql.md)() 함수에 대 한 GUID를 가져오지 `column_2`합니다. 와 달리 id 열에 대 한는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인 열에 대 한 값을 자동으로 생성 되지 않습니다는 [uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md) 데이터 형식으로는 두 번째 피연산자로 표시 된 것 처럼 `INSERT` 문.  
  
```  
CREATE TABLE dbo.T1   
(  
    column_1 int IDENTITY,   
    column_2 uniqueidentifier,  
);  
GO  
INSERT INTO dbo.T1 (column_2)   
    VALUES (NEWID());  
INSERT INTO T1 DEFAULT VALUES;   
GO  
SELECT column_1, column_2  
FROM dbo.T1;  
  
```  
  
#### <a name="g-inserting-data-into-user-defined-type-columns"></a>7. 사용자 정의 형식 열에 데이터 삽입  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 `PointValue` 테이블의 `Points` 열에 세 개의 행을 삽입합니다. 이 열에 사용 된 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) (UDT). `Point` 데이터 형식은 UDT 속성으로 노출되는 X 및 Y 정수 값으로 구성됩니다. CAST 또는 CONVERT 함수를 사용하여 쉼표로 구분된 X 및 Y 값을 `Point` 형식으로 캐스팅해야 합니다. 처음 두 문은 CONVERT 함수를 사용 하 여 문자열 값을 변환 하는 `Point` 유형 및 세 번째 문은 CAST 함수를 사용 합니다. 자세한 내용은 참조 [UDT 데이터 조작](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-manipulating-udt-data.md)합니다.  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
###  <a name="OtherTables"></a>다른 테이블의 데이터를 삽입합니다.  
 이 섹션의 예에서는 한 테이블의 행을 다른 테이블에 삽입하는 방법을 보여 줍니다.  
  
#### <a name="h-using-the-select-and-execute-options-to-insert-data-from-other-tables"></a>8. SELECT 및 EXECUTE 옵션을 사용하여 다른 테이블의 데이터 삽입  
 다음 예에서는 INSERT…SELECT 또는 INSERT…EXECUTE를 사용하여 한 테이블의 데이터를 다른 테이블에 삽입하는 방법을 보여 줍니다. 이 방법은 모두 열 목록에 리터럴 값과 식을 포함하는 다중 테이블 SELECT 문을 기반으로 합니다.  
  
 첫 번째 INSERT 문은 SELECT 문을 사용 하 여 원본 테이블에서 데이터를 파생 시키는 (`Employee`, `SalesPerson`, 및 `Person`)에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 에 결과 집합을 저장 하 고 데이터베이스는 `EmployeeSales` 테이블입니다. 두 번째 INSERT 문은 EXECUTE 절을 사용하여 SELECT 문을 포함하는 저장 프로시저를 호출하고 세 번째 INSERT 문은 EXECUTE 절을 사용하여 SELECT 문을 리터럴 문자열로 참조합니다.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( DataSource   varchar(20) NOT NULL,  
  BusinessEntityID   varchar(11) NOT NULL,  
  LastName     varchar(40) NOT NULL,  
  SalesDollars money NOT NULL  
);  
GO  
CREATE PROCEDURE dbo.uspGetEmployeeSales   
AS   
    SET NOCOUNT ON;  
    SELECT 'PROCEDURE', sp.BusinessEntityID, c.LastName,   
        sp.SalesYTD   
    FROM Sales.SalesPerson AS sp    
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY sp.BusinessEntityID, c.LastName;  
GO  
--INSERT...SELECT example  
INSERT INTO dbo.EmployeeSales  
    SELECT 'SELECT', sp.BusinessEntityID, c.LastName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY sp.BusinessEntityID, c.LastName;  
GO  
--INSERT...EXECUTE procedure example  
INSERT INTO dbo.EmployeeSales   
EXECUTE dbo.uspGetEmployeeSales;  
GO  
--INSERT...EXECUTE('string') example  
INSERT INTO dbo.EmployeeSales   
EXECUTE   
('  
SELECT ''EXEC STRING'', sp.BusinessEntityID, c.LastName,   
    sp.SalesYTD   
    FROM Sales.SalesPerson AS sp   
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE ''2%''  
    ORDER BY sp.BusinessEntityID, c.LastName  
');  
GO  
--Show results.  
SELECT DataSource,BusinessEntityID,LastName,SalesDollars  
FROM dbo.EmployeeSales;  
```  
  
#### <a name="i-using-with-common-table-expression-to-define-the-data-inserted"></a>9. WITH 공통 테이블 식을 사용하여 삽입할 데이터 정의  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 `NewEmployee` 테이블을 만듭니다. 공통 테이블 식(`EmployeeTemp`)은 하나 이상의 테이블에서 `NewEmployee` 테이블에 삽입할 행을 정의합니다. INSERT 문은 공통 테이블 식의 열을 참조합니다.  
  
```  
CREATE TABLE HumanResources.NewEmployee  
(  
    EmployeeID int NOT NULL,  
    LastName nvarchar(50) NOT NULL,  
    FirstName nvarchar(50) NOT NULL,  
    PhoneNumber Phone NULL,  
    AddressLine1 nvarchar(60) NOT NULL,  
    City nvarchar(30) NOT NULL,  
    State nchar(3) NOT NULL,   
    PostalCode nvarchar(15) NOT NULL,  
    CurrentFlag Flag  
);  
GO  
WITH EmployeeTemp (EmpID, LastName, FirstName, Phone,   
                   Address, City, StateProvince,   
                   PostalCode, CurrentFlag)  
AS (SELECT   
       e.BusinessEntityID, c.LastName, c.FirstName, pp.PhoneNumber,  
       a.AddressLine1, a.City, sp.StateProvinceCode,   
       a.PostalCode, e.CurrentFlag  
    FROM HumanResources.Employee e  
        INNER JOIN Person.BusinessEntityAddress AS bea  
        ON e.BusinessEntityID = bea.BusinessEntityID  
        INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
        INNER JOIN Person.PersonPhone AS pp  
        ON e.BusinessEntityID = pp.BusinessEntityID  
        INNER JOIN Person.StateProvince AS sp  
        ON a.StateProvinceID = sp.StateProvinceID  
        INNER JOIN Person.Person as c  
        ON e.BusinessEntityID = c.BusinessEntityID  
    )  
INSERT INTO HumanResources.NewEmployee   
    SELECT EmpID, LastName, FirstName, Phone,   
           Address, City, StateProvince, PostalCode, CurrentFlag  
    FROM EmployeeTemp;  
GO  
```  
  
#### <a name="j-using-top-to-limit-the-data-inserted-from-the-source-table"></a>10. TOP을 사용하여 원본 테이블에서 삽입되는 데이터 제한  
 다음 예에서는 `EmployeeSales` 테이블을 만들고 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `HumanResources.Employee` 테이블에서 가져온 임의의 직원 상위 5명에 대한 이름 및 연간 매출 데이터를 삽입합니다. INSERT 문은 `SELECT` 문에서 반환되는 행 중 5개를 선택합니다. OUTPUT  절은 `EmployeeSales` 테이블에 삽입되는 행을 표시합니다. SELECT 문의 ORDER BY 절은 상위 5명의 직원을 결정하는 데 사용되지 않습니다.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   nvarchar(11) NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  YearlySales  money NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, 
        inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
```  
  
 TOP을 사용하여 시간 순서로 행을 삽입해야 할 경우 다음 예와 같이 하위 SELECT 문에서 ORDER BY 절과 함께 TOP을 사용해야 합니다. OUTPUT  절은 `EmployeeSales` 테이블에 삽입되는 행을 표시합니다. 이제 임의의 행이 아니라 ORDER BY 절의 결과에 따라 상위 5명의 직원이 삽입됩니다.  
  
```  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, 
        inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
```  
  
###  <a name="TargetObjects"></a>표준 테이블 이외의 대상 개체 지정  
 이 섹션의 예에서는 뷰 또는 테이블 변수를 지정하여 행을 삽입하는 방법을 보여 줍니다.  
  
#### <a name="k-inserting-data-by-specifying-a-view"></a>11. 뷰를 지정하여 데이터 삽입  
 다음 예에서는 뷰 이름을 대상 개체로 지정하지만 새 행이 기본 테이블에 삽입됩니다. `INSERT` 문의 값 순서는 뷰의 열 순서와 일치해야 합니다. 자세한 내용은 참조 [수정 데이터 뷰를 통해](../../relational-databases/views/modify-data-through-a-view.md)합니다.  
  
```  
CREATE TABLE T1 ( column_1 int, column_2 varchar(30));  
GO  
CREATE VIEW V1 AS   
SELECT column_2, column_1   
FROM T1;  
GO  
INSERT INTO V1   
    VALUES ('Row 1',1);  
GO  
SELECT column_1, column_2   
FROM T1;  
GO  
SELECT column_1, column_2  
FROM V1;  
GO  
```  
  
#### <a name="l-inserting-data-into-a-table-variable"></a>12. 테이블 변수에 데이터 삽입  
 다음 예는 테이블 변수를 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 대상 개체로 지정합니다.  
  
```  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    LocationID int NOT NULL,  
    CostRate smallmoney NOT NULL,  
    NewCostRate AS CostRate * 1.5,  
    ModifiedDate datetime);  
  
-- Insert values into the table variable.  
INSERT INTO @MyTableVar (LocationID, CostRate, ModifiedDate)  
    SELECT LocationID, CostRate, GETDATE() 
    FROM Production.Location  
    WHERE CostRate > 0;  
  
-- View the table variable result set.  
SELECT * FROM @MyTableVar;  
GO  
```  
  
###  <a name="RemoteTables"></a>원격 테이블에 행을 삽입합니다.  
 이 섹션의 예를 사용 하 여 원격 대상 테이블에 행을 삽입 하는 방법을 보여 주기는 [연결 된 서버](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 또는 [행 집합 함수](../../t-sql/functions/rowset-functions-transact-sql.md) 원격 테이블을 참조 합니다.  
  
#### <a name="m-inserting-data-into-a-remote-table-by-using-a-linked-server"></a>13. 연결된 서버를 사용하여 원격 테이블에 데이터 삽입  
 다음 예에서는 원격 테이블에 행을 삽입합니다. 사용 하 여 원격 데이터 원본에 대 한 링크 만들기 먼저 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)합니다. 연결 된 서버 이름 `MyLinkServer`, 형태로 네 부분으로 된 개체 이름의 일부로 지정 된 다음은 *server.catalog.schema.object*합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  
```  
  
```  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
INSERT INTO MyLinkServer.AdventureWorks2012.HumanResources.Department (Name, GroupName)  
VALUES (N'Public Relations', N'Executive General and Administration');  
GO  
```  
  
#### <a name="n-inserting-data-into-a-remote-table-by-using-the-openquery-function"></a>14. OPENQUERY 함수를 사용하여 원격 테이블에 데이터 삽입  
 다음 예제에서는 지정 하 여 원격 테이블에 행을 삽입의 [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) 행 집합 함수입니다. 이 예에서는 이전 예에서 만든 연결된 서버 이름이 사용됩니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
INSERT OPENQUERY (MyLinkServer, 
    'SELECT Name, GroupName 
     FROM AdventureWorks2012.HumanResources.Department')  
VALUES ('Environmental Impact', 'Engineering');  
GO  
```  
  
#### <a name="o-inserting-data-into-a-remote-table-by-using-the-opendatasource-function"></a>15. OPENDATASOURCE 함수를 사용하여 원격 테이블에 데이터 삽입  
 다음 예제에서는 지정 하 여 원격 테이블에 행을 삽입의 [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 행 집합 함수입니다. 형식을 사용 하 여 데이터 원본에 대 한 올바른 서버 이름을 지정 *server_name* 또는 *server_name\instance_name*합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_nameinstance_name.  
  
INSERT INTO OPENDATASOURCE('SQLNCLI',  
    'Data Source= <server_name>; Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department (Name, GroupName)  
    VALUES (N'Standards and Methods', 'Quality Assurance');  
GO  
```  
  
#### <a name="p-inserting-into-an-external-table-created-using-polybase"></a>16. PolyBase를 사용 하 여 만든 외부 테이블에 삽입  
 SQL Server에서 Hadoop 또는 Azure Storage로 데이터를 내보냅니다. 먼저 대상 파일이나 디렉터리를 가리키는 외부 테이블을 만듭니다. 그런 다음 INSERT INTO를 사용하여 로컬 SQL Server 테이블에서 외부 데이터 원본으로 데이터를 내보냅니다. INSERT INTO 문은 대상 파일이나 디렉터리가 없으면 만듭니다. SELECT 문의 결과는 지정된 파일 형식으로 생성되어 지정한 위치로 내보내집니다.  자세한 내용은 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)을 참조하세요.  
  
**적용 대상**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
-- Create an external table.   
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
        [FirstName] char(25) NOT NULL,   
        [LastName] char(25) NOT NULL,   
        [YearlyIncome] float NULL,   
        [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
        LOCATION='/old_data/2009/customerdata.tbl',  
        DATA_SOURCE = HadoopHDP2,  
        FILE_FORMAT = TextFileFormat,  
        REJECT_TYPE = VALUE,  
        REJECT_VALUE = 0  
);  
  
-- Export data: Move old data to Hadoop while keeping 
-- it query-able via external table.  

INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  
  
###  <a name="BulkLoad"></a>테이블 또는 데이터 파일에서 데이터 대량 로드  
 이 섹션의 예에서는 INSERT 문을 사용하여 데이터를 테이블에 대량으로 로드하는 두 가지 방법을 보여 줍니다.  
  
#### <a name="q-inserting-data-into-a-heap-with-minimal-logging"></a>17. 최소 로깅으로 힙에 데이터 삽입  
 다음 예에서는 새 테이블(힙)을 만들고 최소 로깅을 사용하여 다른 테이블의 데이터를 새 테이블에 삽입합니다. 여기에서는 `AdventureWorks2012` 데이터베이스의 복구 모델이 FULL로 설정되었다고 가정합니다. 최소 로깅을 사용하기 위해 행 삽입 전에 `AdventureWorks2012` 데이터베이스의 복구 모델이 BULK_LOGGED로 설정되고 INSERT INTO…SELECT 문 다음에 FULL로 다시 설정됩니다. 또한 대상 테이블 `Sales.SalesHistory`에 대해 TABLOCK 힌트가 지정됩니다. 이렇게 하면 문은 트랜잭션 로그에 최소 공간을 사용하여 효율적으로 수행됩니다.  
  
```  
-- Create the target heap.  
CREATE TABLE Sales.SalesHistory(  
    SalesOrderID int NOT NULL,  
    SalesOrderDetailID int NOT NULL,  
    CarrierTrackingNumber nvarchar(25) NULL,  
    OrderQty smallint NOT NULL,  
    ProductID int NOT NULL,  
    SpecialOfferID int NOT NULL,  
    UnitPrice money NOT NULL,  
    UnitPriceDiscount money NOT NULL,  
    LineTotal money NOT NULL,  
    rowguid uniqueidentifier ROWGUIDCOL  NOT NULL,  
    ModifiedDate datetime NOT NULL );  
GO  
-- Temporarily set the recovery model to BULK_LOGGED.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY BULK_LOGGED;  
GO  
-- Transfer data from Sales.SalesOrderDetail to Sales.SalesHistory  
INSERT INTO Sales.SalesHistory WITH (TABLOCK)  
    (SalesOrderID,   
     SalesOrderDetailID,  
     CarrierTrackingNumber,   
     OrderQty,   
     ProductID,   
     SpecialOfferID,   
     UnitPrice,   
     UnitPriceDiscount,  
     LineTotal,   
     rowguid,   
     ModifiedDate)  
SELECT * FROM Sales.SalesOrderDetail;  
GO  
-- Reset the recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
#### <a name="r-using-the-openrowset-function-with-bulk-to-bulk-load-data-into-a-table"></a>18. OPENROWSET 함수를 BULK와 함께 사용하여 테이블에 데이터 대량 로드  
 다음 예에서는 OPENROWSET 함수를 지정하여 데이터 파일의 행을 테이블에 삽입합니다. 성능 최적화를 위해 IGNORE_TRIGGERS 테이블 힌트가 지정됩니다. 더 많은 예제를 참조 하십시오. [를 사용 하 여 BULK INSERT 또는 openrowset&#40; 하 여 데이터 대량 가져오기 대량... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
INSERT INTO HumanResources.Department WITH (IGNORE_TRIGGERS) (Name, GroupName)  
SELECT b.Name, b.GroupName   
FROM OPENROWSET (  
    BULK 'C:SQLFilesDepartmentData.txt',  
    FORMATFILE = 'C:SQLFilesBulkloadFormatFile.xml',  
    ROWS_PER_BATCH = 15000)AS b ;  
```  
  
###  <a name="TableHints"></a>힌트를 사용 하 여 쿼리 최적화 프로그램의 기본 동작 재정의  
 이 섹션의 예에 사용 하는 방법을 보여 줍니다 [테이블 힌트](../../t-sql/queries/hints-transact-sql-table.md) 일시적으로 INSERT 문을 처리할 때 쿼리 최적화 프로그램의 기본 동작을 무시 합니다.  
  
> [!CAUTION]  
>  일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리에 대해 최상의 실행 계획을 선택하므로 숙련된 개발자 및 데이터베이스 관리자가 마지막 방법으로만 힌트를 사용하는 것이 좋습니다.  
  
#### <a name="s-using-the-tablock-hint-to-specify-a-locking-method"></a>S.는 TABLOCK 힌트를 사용하여 잠금 방법 지정  
 다음 예에서는 Production.Location 테이블에 배타적(X) 잠금을 적용하고 INSERT 문이 끝날 때까지 유지하도록 지정합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]합니다.  
  
```  
INSERT INTO Production.Location WITH (XLOCK)  
(Name, CostRate, Availability)  
VALUES ( N'Final Inventory', 15.00, 80.00);  
```  
  
###  <a name="CaptureResults"></a>INSERT 문의 결과 캡처  
 이 섹션의 예에 사용 하는 방법을 보여 줍니다는 [OUTPUT 절](../../t-sql/queries/output-clause-transact-sql.md) INSERT 문에 의해 영향을 각 행의 정보 또는 식을 기반으로 돌아갑니다. 이러한 결과를 처리 응용 프로그램에 반환하여 확인 메시지, 보관 및 기타 응용 프로그램 요구 사항을 충족시키는 데 사용할 수 있습니다.  
  
#### <a name="t-using-output-with-an-insert-statement"></a>20. INSERT 문을 사용 하 여 출력을 사용 하 여  
 다음 예에서는 `ScrapReason` 테이블에 행을 삽입하고 `OUTPUT` 절을 사용하여 문의 결과를 `@MyTableVar` 테이블 변수에 반환합니다. `ScrapReasonID` 열은 `IDENTITY` 속성으로 정의되었으므로 해당 열에 대한 `INSERT` 문에 값이 지정되지 않습니다. 그러나 해당 열에 대해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성한 값은 `OUTPUT` 열의 `INSERTED.ScrapReasonID` 절에서 반환됩니다.  
  
```  
DECLARE @MyTableVar table( NewScrapReasonID smallint,  
                           Name varchar(50),  
                           ModifiedDate datetime);  
INSERT Production.ScrapReason  
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate  
        INTO @MyTableVar  
VALUES (N'Operator error', GETDATE());  
  
--Display the result set of the table variable.  
SELECT NewScrapReasonID, Name, ModifiedDate FROM @MyTableVar;  
--Display the result set of the table.  
SELECT ScrapReasonID, Name, ModifiedDate   
FROM Production.ScrapReason;  
```  
  
#### <a name="u-using-output-with-identity-and-computed-columns"></a>21. ID 열 및 계산 열에 OUTPUT 사용  
 다음 예에서는 `EmployeeSales` 테이블을 만들고 INSERT 문에 SELECT 문을 사용하여 이 테이블에 여러 개의 행을 삽입한 후 원본 테이블에서 데이터를 검색합니다. `EmployeeSales` 테이블에는 ID 열(`EmployeeID`)과 계산 열(`ProjectedSales`)이 포함되어 있습니다. 이러한 값은 삽입 작업 중에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성되므로 `@MyTableVar`에 이러한 열을 정의할 수 없습니다.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   int IDENTITY (1,5)NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales AS CurrentSales * 1.10   
);  
GO  
DECLARE @MyTableVar table(  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL  
  );  
  
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)  
  OUTPUT INSERTED.LastName,   
         INSERTED.FirstName,   
         INSERTED.CurrentSales  
  INTO @MyTableVar  
    SELECT c.LastName, c.FirstName, sp.SalesYTD  
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY c.LastName, c.FirstName;  
  
SELECT LastName, FirstName, CurrentSales  
FROM @MyTableVar;  
GO  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM dbo.EmployeeSales;  
```  
  
#### <a name="v-inserting-data-returned-from-an-output-clause"></a>22. OUTPUT 절에서 반환된 데이터 삽입  
 다음 예에서는 MERGE 문의 OUTPUT 절에서 반환된 데이터를 캡처하여 이 데이터를 다른 테이블에 삽입합니다. MERGE 문은 `Quantity` 테이블의 `ProductInventory` 열을 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `SalesOrderDetail` 테이블에서 처리되는 순서대로 매일 업데이트하고 또한 재고가 0이 되는 제품의 행을 삭제합니다. 이 예에서는 삭제된 행을 캡처한 후 다른 `ZeroInventory` 테이블에 삽입하여 재고가 없는 제품을 추적합니다.  
  
```  
--Create ZeroInventory table.  
CREATE TABLE Production.ZeroInventory (DeletedProductID int, RemovedOnDate DateTime);  
GO  
  
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)  
SELECT ProductID, GETDATE()  
FROM  
(   MERGE Production.ProductInventory AS pi  
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
           JOIN Sales.SalesOrderHeader AS soh  
           ON sod.SalesOrderID = soh.SalesOrderID  
           AND soh.OrderDate = '20070401'  
           GROUP BY ProductID) AS src (ProductID, OrderQty)  
    ON (pi.ProductID = src.ProductID)  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0  
        THEN DELETE  
    WHEN MATCHED  
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)  
WHERE Action = 'DELETE';  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were inserted';  
GO  
SELECT DeletedProductID, RemovedOnDate FROM Production.ZeroInventory;  
```  

#### <a name="w-inserting-data-using-the-select-option"></a>W. 선택 옵션을 사용 하 여 데이터 삽입  
 다음 예에서는 INSERT 문을 선택 옵션을 사용 하 여 데이터의 여러 행을 삽입 하는 방법을 보여 줍니다. 첫 번째 `INSERT` 문 사용 하 여는 `SELECT` 원본 테이블에서 데이터를 검색에 직접 문의 다음 결과 저장 하에서 설정 된 `EmployeeTitles` 테이블입니다.  
  
```  
CREATE TABLE EmployeeTitles  
( EmployeeKey   INT NOT NULL,  
  LastName     varchar(40) NOT NULL,  
  Title      varchar(50) NOT NULL  
);  
INSERT INTO EmployeeTitles  
    SELECT EmployeeKey, LastName, Title   
    FROM ssawPDW.dbo.DimEmployee  
    WHERE EndDate IS NULL;  
```  
  
#### <a name="x-specifying-a-label-with-the-insert-statement"></a>X입니다. INSERT 문과 함께 레이블을 지정  
 다음 예에서는 INSERT 문 사용 하 여 레이블의 사용법을 보여줍니다.  
  
```  
-- Uses AdventureWorks  
  
INSERT INTO DimCurrency   
VALUES (500, N'C1', N'Currency1')  
OPTION ( LABEL = N'label1' );  
```  
  
#### <a name="y-using-a-label-and-a-query-hint-with-the-insert-statement"></a>Y입니다. INSERT 문과 함께 레이블 및 쿼리 힌트를 사용 하 여  
 이 쿼리에서 INSERT 문을 사용 하는 레이블 및 join 쿼리 힌트를 사용 하는 기본 구문을 보여 줍니다. 쿼리 제출 하는 제어 노드에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 계산 노드에서 실행을 적용 됩니다. 해시 조인 전략을 생성할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 계획. 조인 힌트와 OPTION 절을 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [옵션 (SQL Server PDW)](http://msdn.microsoft.com/en-us/72bbce98-305b-42fa-a19f-d89620621ecc)합니다.  
  
```  
-- Uses AdventureWorks  
  
INSERT INTO DimCustomer (CustomerKey, CustomerAlternateKey, 
    FirstName, MiddleName, LastName )   
SELECT ProspectiveBuyerKey, ProspectAlternateKey, 
    FirstName, MiddleName, LastName  
FROM ProspectiveBuyer p JOIN DimGeography g ON p.PostalCode = g.PostalCode  
WHERE g.CountryRegionCode = 'FR'  
OPTION ( LABEL = 'Add French Prospects', HASH JOIN);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [NEWID &#40; Transact SQL &#41;](../../t-sql/functions/newid-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40; Transact SQL &#41;](../../t-sql/statements/merge-transact-sql.md)   
 [OUTPUT 절 &#40; Transact SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [inserted 및 deleted 테이블 사용](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)  
  
  




