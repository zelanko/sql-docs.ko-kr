---
description: CREATE FUNCTION(Azure Synapse Analytics)
title: CREATE FUNCTION(Azure Synapse Analytics) | Microsoft Docs
ms.custom: ''
ms.date: 09/17/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
author: juliemsft
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 47073d130f6a3881c7765d74f40fa06658b02f78
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93067387"
---
# <a name="create-function-azure-synapse-analytics"></a>CREATE FUNCTION(Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssSDW](../../includes/ssazuresynapse_md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 사용자 정의 함수를 만듭니다. 사용자 정의 함수는 매개 변수를 허용하고 복잡한 계산 등의 동작을 수행하며 해당 동작의 결과를 값으로 반환하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 루틴입니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 반환 값은 스칼라(단일) 값이어야 합니다. [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]CREATE FUNCTION은 인라인 테이블 반환 함수(미리 보기) 구문을 사용하여 테이블을 반환하거나 스칼라 반환 함수 구문을 사용하여 단일 값을 반환할 수 있습니다. 이 문을 사용하여 다음과 같은 상황에서 다시 사용할 수 있는 루틴을 만들 수 있습니다.  
  
-   SELECT 등의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문  
  
-   함수를 호출하는 애플리케이션  
  
-   다른 사용자 정의 함수의 정의  
  
-   열에 CHECK 제약 조건 정의  
  
-   저장 프로시저 바꾸기  
  
-   인라인 함수를 보안 정책의 필터 조건자로 사용  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Transact-SQL Scalar Function Syntax  (in Azure Synapse Analytics and Parallel Data Warehouse)
CREATE FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] parameter_data_type   
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
  
<function_option>::=   
{  
    [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
}  
```

```syntaxsql
-- Transact-SQL Inline Table-Valued Function Syntax (Preview in Azure Synapse Analytics only)
CREATE FUNCTION [ schema_name. ] function_name
( [ { @parameter_name [ AS ] parameter_data_type
    [ = default ] }
    [ ,...n ]
  ]
)
RETURNS TABLE
    [ WITH SCHEMABINDING ]
    [ AS ]
    RETURN [ ( ] select_stmt [ ) ]
[ ; ]
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
## <a name="arguments"></a>인수  
 *schema_name*  
 사용자 정의 함수가 속한 스키마의 이름입니다.  
  
 *function_name*  
 사용자 정의 함수의 이름입니다. 함수 이름은 식별자에 대한 규칙을 따라야 하며 데이터베이스 내에서 그리고 각 스키마별로 고유해야 합니다.  
  
> [!NOTE]  
>  매개 변수를 지정하지 않은 경우에도 함수 이름 뒤에 괄호를 사용해야 합니다.  
  
 @*parameter_name*  
 사용자 정의 함수의 매개 변수입니다. 하나 이상의 매개 변수를 선언할 수 있습니다.  
  
 하나의 함수에 최대 2,100개의 매개 변수를 지정할 수 있습니다. 매개 변수에 기본값이 정의되지 않은 경우 함수를 실행할 때 사용자가 선언된 각 매개 변수의 값을 지정해야 합니다.  
  
 at 기호(@)를 첫 번째 문자로 사용하여 매개 변수 이름을 지정합니다. 매개 변수 이름은 식별자에 대한 규칙을 따라야 합니다. 매개 변수는 함수에서 로컬로 사용되므로 다른 함수에서 동일한 매개 변수 이름을 사용할 수 있습니다. 매개 변수는 상수 대신 사용할 수 있지만 테이블 이름, 열 이름 또는 다른 데이터베이스 개체의 이름 대신 사용할 수는 없습니다.  
  
> [!NOTE]  
>  저장 프로시저나 사용자 정의 함수에 매개 변수를 전달할 때 또는 일괄 처리 문에서 변수를 선언하고 설정할 때 ANSI_WARNINGS는 인식되지 않습니다. 예를 들어 변수가 **char(3)** 로 정의된 경우 3자보다 큰 값으로 설정하면 해당 데이터가 정의된 크기로 잘리고 INSERT 또는 UPDATE 문은 성공합니다.  
  
 *parameter_data_type*  
 매개 변수 데이터 형식입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수의 경우 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 지원되는 모든 스칼라 데이터 형식이 허용됩니다. 타임스탬프(rowversion) 데이터 형식은 지원되는 형식이 아닙니다.  
  
 [ = *default* ]  
 매개 변수의 기본값입니다. *기본* 값이 정의되어 있으면 해당 매개 변수 값을 지정하지 않아도 함수를 실행할 수 있습니다.  
  
 함수의 매개 변수에 기본값을 지정한 경우 기본값을 가져오는 함수를 호출할 때 DEFAULT 키워드를 지정해야 합니다. 이 동작은 매개 변수를 생략할 경우 자동으로 기본값이 사용되는 저장 프로시저에서 기본값이 있는 매개 변수를 사용하는 것과는 다릅니다.  
  
 *return_data_type*  
 스칼라 사용자 정의 함수의 반환 값입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수의 경우 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 지원되는 모든 스칼라 데이터 형식이 허용됩니다. 타임스탬프(rowversion) 데이터 형식은 지원되는 형식이 아닙니다. 커서 및 테이블 스칼라가 아닌 형식은 허용되지 않습니다.  
  
 *function_body*  
 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.  function_body는 SELECT 문을 포함할 수 없으며 데이터베이스 데이터를 참조할 수 없습니다.  function_body는 테이블이나 뷰를 참조할 수 없습니다. 함수 본문은 다른 결정적인 함수를 호출할 수 있지만 비결정적 함수는 호출할 수 없습니다. 
  
 스칼라 함수에서 *function_body* 는 함께 계산되어 스칼라 값을 반환하는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.  
  
 *scalar_expression*  
 스칼라 함수가 반환하는 스칼라 값을 지정합니다.  

 *select_stmt* **적용 대상** : Azure Synapse Analytics  
 인라인 테이블 반환 함수(미리 보기)의 반환 값을 정의하는 단일 SELECT 문입니다.

 TABLE **적용 대상** : Azure Synapse Analytics  
 TVF(테이블 반환 함수)의 반환 값이 테이블임을 지정합니다. 상수 및 @ *local_variables* 만 TVF에 전달할 수 있습니다.

 인라인 TVF(미리 보기)에서 TABLE 반환 값은 단일 SELECT 문을 통해 정의됩니다. 인라인 함수에는 연관된 반환 변수가 없습니다.
  
 **\<function_option>::=** 
  
 함수에 다음 옵션 중 하나 이상이 포함되도록 지정합니다.  
  
 SCHEMABINDING  
 함수를 함수가 참조하는 데이터베이스 개체에 바인딩되도록 지정합니다. SCHEMABINDING을 지정하면 함수 정의에 영향을 미치는 방식으로 기본 개체를 수정할 수 없습니다. 함수 정의 자체를 먼저 수정하거나 삭제하여 수정할 개체에 대한 종속성을 제거해야 합니다.  
  
 다음 동작 중 하나만 발생해도 참조하는 개체에 대한 함수 바인딩이 제거됩니다.  
  
-   함수가 삭제된 경우  
  
-   SCHEMABINDING 옵션을 지정하지 않은 상태에서 ALTER 문을 사용하여 함수를 수정한 경우  
  
 다음 조건을 만족하는 경우에만 함수가 스키마에 바인딩될 수 있습니다.  
  
-   함수가 참조하는 사용자 정의 함수도 스키마에 바인딩됩니다.  
  
-   함수가 참조하는 함수 및 다른 UDF 함수는 부분 또는 두 부분으로 이루어진 이름을 사용하여 참조됩니다.  
  
-   기본 제공 함수 및 동일한 데이터베이스의 다른 UDF만 UDF의 본문 내에서 참조할 수 있습니다.  
  
-   CREATE FUNCTION 문을 실행한 사용자는 해당 함수가 참조하는 데이터베이스 개체에 대한 REFERENCES 권한이 있어야 합니다.  
  
 SCHEMABINDING을 제거하려면 ALTER 사용  
  
 RETURNS NULL ON NULL INPUT | **CALLED ON NULL INPUT**  
 스칼라 반환 함수의 **OnNULLCall** 특성을 지정합니다. 이 특성을 지정하지 않으면 기본적으로 CALLED ON NULL INPUT이 적용됩니다. 즉, 인수로 NULL이 전달되는 경우에도 함수 본문이 실행됩니다.  
  
## <a name="best-practices"></a>모범 사례  
 SCHEMABINDING 절을 사용하여 사용자 정의 함수를 만들지 않은 경우 기본 개체에 대한 변경 내용이 함수의 정의에 영향을 주어 함수가 호출될 대 예기치 않은 결과를 초래할 수 있습니다. 기본 개체에 대한 변경으로 인해 함수가 최신 상태를 유지하지 못하게 되는 일이 발생하지 않도록 다음 메서드 중 하나를 구현하는 것이 좋습니다.  
  
-   함수를 만들 때 WITH SCHEMABINDING 절을 지정합니다. 이렇게 하면 함수도 수정되지 않는 한 함수 정의에서 참조된 개체를 수정할 수 없습니다.  
  
## <a name="interoperability"></a>상호 운용성  
 스칼라 반환 함수에서 유효한 문은 다음과 같습니다.  
  
-   대입 문  
  
-   TRY...CATCH 문을 제외한 흐름 제어 문  
  
-   로컬 데이터 변수를 정의하는 DECLARE 문  

인라인 테이블 반환 함수(미리 보기)에서는 단일 select 문만 사용할 수 있습니다.
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 사용자 정의 함수는 데이터베이스 상태 수정 동작을 수행하는 데 사용할 수 없습니다.  
  
 사용자 정의 함수는 중첩될 수 있습니다. 즉, 하나의 사용자 정의 함수가 다른 사용자 정의 함수를 호출할 수 있습니다. 중첩 수준은 호출된 함수의 실행이 시작되면 늘어나고 호출된 함수의 실행이 끝나면 줄어듭니다. 사용자 정의 함수는 최대 32 수준까지 중첩될 수 있습니다. 최대 중첩 수준을 초과하면 전체 함수 호출 체인이 실패합니다.   
  
## <a name="metadata"></a>메타데이터  
 이 섹션에서는 사용자 정의 함수에 대한 메타데이터를 반환하는 데 사용할 수 있는 시스템 카탈로그 뷰를 나열합니다.  
  
 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md): [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수의 정의를 표시합니다. 예를 들면 다음과 같습니다.  
  
```sql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md): 사용자 정의 함수에 정의된 매개 변수에 대한 정보를 표시합니다.  
  
 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md): 함수에서 참조하는 기본 개체를 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 CREATE FUNCTION 권한과 함수가 생성되는 스키마에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>A. 데이터 형식을 변경하는 스칼라 반환 사용자 정의 함수 사용  
 이 간단한 함수는 **int** 데이터 형식을 입력으로 사용하며 **decimal(10,2)** 데이터 형식으로 출력으로 반환합니다.  
  
```sql  
CREATE FUNCTION dbo.ConvertInput (@MyValueIn int)  
RETURNS decimal(10,2)  
AS  
BEGIN  
    DECLARE @MyValueOut int;  
    SET @MyValueOut= CAST( @MyValueIn AS decimal(10,2));  
    RETURN(@MyValueOut);  
END;  
GO  
  
SELECT dbo.ConvertInput(15) AS 'ConvertedValue';  
```  

## <a name="examples-sssdwfull"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  

### <a name="a-creating-an-inline-table-valued-function-preview"></a>A. 인라인 테이블 반환 함수(미리 보기) 만들기
 다음 예제에서는 `objectType` 매개 변수를 기준으로 필터링하여 모듈에 대한 일부 키 정보를 반환하는 인라인 테이블 반환 함수를 만듭니다. 함수가 DEFAULT 매개 변수를 사용하여 호출될 때 모든 모듈을 반환하는 기본값을 포함합니다. 이 예제에서는 [메타데이터](#metadata)에 설명된 일부 시스템 카탈로그 뷰를 사용합니다.

```sql
CREATE FUNCTION dbo.ModulesByType(@objectType CHAR(2) = '%%')
RETURNS TABLE
AS
RETURN
(
    SELECT 
        sm.object_id AS 'Object Id',
        o.create_date AS 'Date Created',
        OBJECT_NAME(sm.object_id) AS 'Name',
        o.type AS 'Type',
        o.type_desc AS 'Type Description', 
        sm.definition AS 'Module Description'
    FROM sys.sql_modules AS sm  
    JOIN sys.objects AS o ON sm.object_id = o.object_id
    WHERE o.type like '%' + @objectType + '%'
);
GO
```
그러면 다음을 사용하여 함수를 호출해 모든 뷰( **V** ) 개체를 반환할 수 있습니다.
```sql
select * from dbo.ModulesByType('V');
```

### <a name="b-combining-results-of-an-inline-table-valued-function-preview"></a>B. 인라인 테이블 반환 함수(미리 보기)의 결과 결합
 이 간단한 예제에서는 이전에 만든 인라인 TVF에서 cross apply를 사용하여 결과를 다른 테이블과 결합할 수 있는 방법을 보여 줍니다. 여기서는 sys.objects에서 모든 열을 선택하고 유형 열에서 일치하는 모든 행의 `ModulesByType` 결과도 선택합니다. APPLY 사용에 대한 자세한 내용은 [FROM 절과 JOIN, APPLY, PIVOT](../../t-sql/queries/from-transact-sql.md)을 참조하세요.

```sql
SELECT * 
FROM sys.objects o
CROSS APPLY dbo.ModulesByType(o.type);
GO
```
  
## <a name="see-also"></a>참조  
 [ALTER FUNCTION(SQL Server PDW)](/previous-versions/sql/)   
 [DROP FUNCTION(SQL Server PDW)](/previous-versions/sql/)  
  
  

