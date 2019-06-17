---
title: sys.dm_sql_referenced_entities (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_sql_referenced_entities_TSQL
- dm_sql_referenced_entities
- sys.dm_sql_referenced_entities
- sys.dm_sql_referenced_entities_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referenced_entities dynamic management function
ms.assetid: 077111cb-b860-4d61-916f-bac5d532912f
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e4ed017d1b3571405127177bdb45857be7ccbf1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66354403"
---
# <a name="sysdmsqlreferencedentities-transact-sql"></a>sys.dm_sql_referenced_entities(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

지정한 참조 엔터티의 정의에 이름으로 참조 되는 각 사용자 정의 엔터티에 대해 하나의 행을 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 하나의 사용자 정의 엔터티가 호출 될 때 두 엔터티 간의 종속성이 만들어집니다.는 *엔터티를 참조*, 라는 다른 사용자 정의 엔터티의 영구 SQL 식에서 이름별으로 표시 된 *엔터티를 참조 하* . 예를 들어 저장 프로시저가 지정된 참조 엔터티인 경우 이 함수는 테이블, 뷰, UDT(사용자 정의 형식), 또는 다른 저장 프로시저 등 이 저장 프로시저에서 참조되는 모든 사용자 정의 엔터티를 반환합니다.  
  
 이러한 동적 관리 함수를 사용하면 지정된 참조 엔터티에 의해 참조되는 다음과 같은 엔터티 유형을 보고할 수 있습니다.  
  
-   스키마 바운드 엔터티  
  
-   비스키마 바운드 엔터티  
  
-   데이터베이스 간 및 서버 간 엔터티  
  
-   스키마 바운드 엔터티 및 비스키마 바운드 엔터티의 열 수준 종속성  
  
-   사용자 정의 형식(별칭 및 CLR UDT)  
  
-   XML 스키마 컬렉션  
  
-   파티션 함수  

## <a name="syntax"></a>구문  
  
```  
sys.dm_sql_referenced_entities (  
    ' [ schema_name. ] referencing_entity_name ' ,
    ' <referencing_class> ' )  
  
<referencing_class> ::=  
{  
    OBJECT  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
```  
  
## <a name="arguments"></a>인수  
 [ *schema_name*. ] *referencing_entity_name*  
 참조 엔터티의 이름입니다. *schema_name* 참조 클래스는 개체 때 필요 합니다.  
  
 *schema_name.referencing_entity_name* 됩니다 **nvarchar(517)** 합니다.  
  
 *<referencing_class>* ::=  { OBJECT | DATABASE_DDL_TRIGGER   | SERVER_DDL_TRIGGER }  
 지정된 참조 엔터티의 클래스입니다. 각 문에는 하나의 클래스만 지정할 수 있습니다.  
  
 *< referencing_class >* 됩니다 **nvarchar(60)** 합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|referencing_minor_id|**int**|참조 엔터티가 열인 경우 열 ID이며 그렇지 않은 경우 0입니다. Null을 허용하지 않습니다.|  
|referenced_server_name|**sysname**|참조된 엔터티의 서버 이름입니다.<br /><br /> 이 열은 네 부분으로 된 올바른 이름을 지정하여 생성되는 서버 간 종속성에 대해 채워집니다. 다중 부분 이름에 대 한 정보를 참조 하세요 [TRANSACT-SQL 구문 표기 규칙 &#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)합니다.<br /><br /> 네 부분으로 된 이름 지정 없이 엔터티가 참조된 비스키마 바운드 종속성의 경우 NULL입니다.<br /><br /> 동일한 데이터베이스에 있어야 하며 따라서만 정의 될 수는 두 부분으로 구성을 사용 하 여 스키마 바운드 엔터티에 대 한 NULL (*schema.object*) 이름입니다.|  
|referenced_database_name|**sysname**|참조된 엔터티의 데이터베이스 이름입니다.<br /><br /> 이 열은 세 부분 또는 네 부분으로 된 올바른 이름을 지정하여 생성되는 데이터베이스 간 또는 서버 간 참조에 대해 채워집니다.<br /><br /> 한 부분 또는 두 부분으로 된 이름을 사용하여 지정된 비스키마 바운드 참조의 경우 NULL입니다.<br /><br /> 동일한 데이터베이스에 있어야 하며 따라서만 정의 될 수는 두 부분으로 구성을 사용 하 여 스키마 바운드 엔터티에 대 한 NULL (*schema.object*) 이름입니다.|  
|referenced_schema_name|**sysname**|참조된 엔터티가 속한 스키마입니다.<br /><br /> 스키마 이름 지정 없이 엔터티가 참조되는 비스키마 바운드 참조의 경우 NULL입니다.<br /><br /> 스키마 바운드 참조의 경우 NULL일 수 없습니다.|  
|referenced_entity_name|**sysname**|참조된 엔터티의 이름입니다. Null을 허용하지 않습니다.|  
|referenced_minor_name|**sysname**|참조된 엔터티가 열인 경우 열 이름이며 그렇지 않은 경우 NULL입니다. 예를 들어 참조된 엔터티 자체를 나열하는 행에서 referenced_minor_name은 NULL입니다.<br /><br /> 열이 참조 엔터티에서 이름으로 식별되거나 부모 엔터티가 SELECT * 문에 사용된 경우 참조된 엔터티는 열입니다.|  
|referenced_id|**int**|참조된 엔터티의 ID입니다. referenced_minor_id가 0이 아닌 경우 referenced_id는 열이 정의된 엔터티입니다.<br /><br /> 서버 간 참조의 경우 항상 NULL입니다.<br /><br /> 데이터베이스 간 참조의 경우 데이터베이스가 오프라인 상태이거나 엔터티를 바인딩할 수 없어 ID를 확인할 수 없으면 NULL입니다.<br /><br /> 데이터베이스 내 참조의 경우 ID를 확인할 수 없으면 NULL입니다. 비 스키마 바운드 참조의 경우 참조 된 엔터티는 이름 확인이 호출자에 종속 되는 경우 또는 데이터베이스에 존재 하지 않을 경우 ID 확인할 수 없습니다.  후자의 경우,이 따라 is_caller_dependent는 1로 설정 됩니다.<br /><br /> 스키마 바운드 참조의 경우 NULL일 수 없습니다.|  
|referenced_minor_id|**int**|참조된 엔터티가 열인 경우 열 ID이며 그렇지 않은 경우 0입니다. 예를 들어 참조된 엔터티 자체를 나열하는 행에서 referenced_minor_is는 0입니다.<br /><br /> 비스키마 바운드 참조의 경우 모든 참조된 엔터티를 바인딩할 수 있는 경우에만 열 종속성이 보고됩니다. 바인딩할 수 없는 참조된 엔터티가 있는 경우 열 수준 종속성이 보고되지 않으며 referenced_minor_id는 0입니다. 예 4를 참조하십시오.|  
|referenced_class|**tinyint**|참조된 엔터티의 클래스입니다.<br /><br /> 1 = 개체 또는 열<br /><br /> 6 = 형식<br /><br /> 10 = XML 스키마 컬렉션<br /><br /> 21 = 파티션 함수|  
|referenced_class_desc|**nvarchar(60)**|참조된 엔터티의 클래스에 대한 설명입니다.<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION|  
|is_caller_dependent|**bit**|참조된 엔터티에 대한 스키마 바인딩이 런타임에 발생하며 따라서 엔터티 ID 확인은 호출자의 스키마에 종속됨을 나타냅니다. 이는 참조된 엔터티가 EXECUTE 문 내에서 호출되는 저장 프로시저, 확장 저장 프로시저 또는 사용자 정의 함수인 경우 발생합니다.<br /><br /> 1 = 참조된 엔터티가 호출자에 종속되고 런타임에 확인됩니다. 이 경우 referenced_id는 NULL입니다.<br /><br /> 0 = 참조된 엔터티 ID가 호출자에 종속되지 않습니다. 스키마 이름을 명시적으로 지정하는 스키마 바운드 참조와 데이터베이스 간 및 서버 간 참조의 경우 항상 0입니다. 예를 들어 `EXEC MyDatabase.MySchema.MyProc` 형식의 엔터티에 대한 참조는 호출자에 종속되지 않습니다. 하지만 `EXEC MyDatabase..MyProc` 형식의 참조는 호출자에 종속됩니다.|  
|is_ambiguous|**bit**|대 한 참조가 모호 하며 런타임에 사용자 정의 함수, 사용자 정의 형식 (UDT) 또는 형식의 열에 대 한 xquery 참조로 확인할 수 나타냅니다 **xml**합니다. 예를 들어 저장 프로시저에 `SELECT Sales.GetOrder() FROM Sales.MySales` 문이 정의된 경우 `Sales.GetOrder()`가 `Sales` 스키마의 사용자 정의 함수인지, 아니면 `Sales`라는 메서드가 있는 UDT 형식의 `GetOrder()` 열인지는 저장 프로시저가 실행될 때까지 알 수 없습니다.<br /><br /> 1 = 사용자 정의 함수 또는 열 UDT(사용자 정의 형식) 메서드에 대한 참조가 모호합니다.<br /><br /> 0 = 참조가 분명하거나 함수가 호출될 때 엔터티를 성공적으로 바인딩할 수 있습니다.<br /><br /> 스키마 바운드 참조의 경우 항상 0입니다.|  
|is_selected|**bit**|1 = 개체 또는 열이 선택됩니다.|  
|is_updated|**bit**|1 = 개체 또는 열이 수정됩니다.|  
|is_select_all|**bit**|1 = 개체가 SELECT * 절에서 사용됩니다(개체 수준만 해당).|  
|is_all_columns_found|**bit**|1 = 개체에 대한 모든 열 종속성을 찾을 수 있습니다.<br /><br /> 0 = 개체에 대한 열 종속성을 찾을 수 없습니다.|
|is_insert_all|**bit**|1 = 개체 (개체 수준에만 해당) 열 목록 없이 INSERT 문에서 사용 됩니다.<br /><br />이 열은 SQL Server 2016에 추가 되었습니다.|  
|is_incomplete|**bit**|1 = 개체 또는 열에 바인딩 오류가 잘못 되었습니다.<br /><br />이 열은 SQL Server 2016 SP2에 추가 되었습니다.|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="exceptions"></a>예외  
 다음과 같은 경우 빈 결과 집합을 반환합니다.  
  
-   시스템 개체가 지정되어 있습니다.  
  
-   지정된 엔터티가 현재 데이터베이스에 없습니다.  
  
-   지정된 엔터티가 아무런 엔터티도 참조하지 않습니다.  
  
-   잘못된 매개 변수가 전달되었습니다.  
  
 지정된 참조 엔터티가 번호가 매겨진 저장 프로시저인 경우 오류를 반환합니다.  
  
 열 종속성을 확인할 수 없으면 오류 2020을 반환합니다. 이 오류가 발생해도 쿼리는 개체 수준 종속성을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 데이터베이스 컨텍스트에서 실행되어 서버 수준 DDL 트리거를 참조하는 엔터티를 반환할 수 있습니다.  
  
 다음 표에서는 종속성 정보가 생성 및 유지되는 엔터티 유형을 보여 줍니다. 종속성 정보는 규칙, 기본값, 임시 테이블, 임시 저장 프로시저 또는 시스템 개체에 대해서는 생성 및 유지되지 않습니다.  
  
|엔터티 유형|참조 엔터티|참조된 엔터티|  
|-----------------|------------------------|-----------------------|  
|Table|예*|사용자 계정 컨트롤|  
|보기|사용자 계정 컨트롤|사용자 계정 컨트롤|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저**|사용자 계정 컨트롤|사용자 계정 컨트롤|  
|CLR 저장 프로시저|아니요|사용자 계정 컨트롤|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수|사용자 계정 컨트롤|사용자 계정 컨트롤|  
|CLR 사용자 정의 함수|아니요|사용자 계정 컨트롤|  
|CLR 트리거(DML 및 DDL)|아니요|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DML 트리거|사용자 계정 컨트롤|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터베이스 수준 DDL 트리거|사용자 계정 컨트롤|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 수준 DDL 트리거|사용자 계정 컨트롤|아니요|  
|확장 저장 프로시저|아니요|사용자 계정 컨트롤|  
|큐|아니요|사용자 계정 컨트롤|  
|동의어|아니요|사용자 계정 컨트롤|  
|형식(별칭 및 CLR 사용자 정의 형식)|아니요|사용자 계정 컨트롤|  
|XML 스키마 컬렉션|아니요|사용자 계정 컨트롤|  
|파티션 함수|아니요|사용자 계정 컨트롤|  
| &nbsp; | &nbsp; | &nbsp; |

 \* 테이블을 참조 하는 경우에 참조 엔터티로 추적을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈, 사용자 정의 형식 또는 계산된 열, CHECK 제약 조건 또는 DEFAULT 제약 조건 정의에서 XML 스키마 컬렉션입니다.  
  
 ** 정수 값 1보다 큰 번호가 있는 저장 프로시저는 참조 엔터티나 참조된 엔터티로 추적되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 sys.dm_sql_referenced_entities에 대한 SELECT 권한 및 참조 엔터티에 대한 VIEW DEFINITION 권한이 필요합니다. 기본적으로 SELECT 권한은 public에 부여됩니다. 참조 엔터티가 데이터 수준 DDL 트리거인 경우 데이터베이스에 대한 ALTER DATABASE DDL TRIGGER 권한 또는 데이터베이스에 대한 VIEW DEFINITION 권한이 필요합니다. 참조 엔터티가 서버 수준 DDL 트리거인 경우 서버에 대한 VIEW ANY DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-return-entities-that-are-referenced-by-a-database-level-ddl-trigger"></a>1\. 데이터베이스 수준 DDL 트리거에 의해 참조 되는 엔터티 반환  
 다음 예에서는 데이터베이스 수준 DDL 트리거 `ddlDatabaseTriggerLog`에 의해 참조되는 엔터티(테이블 및 열)를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT
        referenced_schema_name,
        referenced_entity_name,
        referenced_minor_name,
        referenced_minor_id,
        referenced_class_desc
    FROM
        sys.dm_sql_referenced_entities (
            'ddlDatabaseTriggerLog',
            'DATABASE_DDL_TRIGGER')
;
GO  
```  
  
### <a name="b-return-entities-that-are-referenced-by-an-object"></a>2\. 개체에 의해 참조 되는 엔터티 반환  
 다음 예에서는 사용자 정의 함수 `dbo.ufnGetContactInformation`에 의해 참조되는 엔터티를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT
        referenced_schema_name,
        referenced_entity_name,
        referenced_minor_name,
        referenced_minor_id,
        referenced_class_desc,
        is_caller_dependent,
        is_ambiguous
    FROM
        sys.dm_sql_referenced_entities (
            'dbo.ufnGetContactInformation',
            'OBJECT')
;
GO  
```  
  
### <a name="c-return-column-dependencies"></a>3\. 열 종속성 반환  
 다음 예에서는 `Table1` 열과 `c` 열의 합계로 정의되는 계산 열 `a`가 포함된 `b` 테이블을 만듭니다. 그런 다음 `sys.dm_sql_referenced_entities` 뷰를 호출합니다. 이 뷰는 계산 열에 정의된 각 열마다 하나씩 두 개의 행을 반환합니다.  
  
```sql  
CREATE TABLE dbo.Table1 (a int, b int, c AS a + b);  
GO  
SELECT
        referenced_schema_name AS schema_name,  
        referenced_entity_name AS table_name,  
        referenced_minor_name  AS referenced_column,  
        COALESCE(
            COL_NAME(OBJECT_ID(N'dbo.Table1'),
            referencing_minor_id),
            'N/A') AS referencing_column_name  
    FROM
        sys.dm_sql_referenced_entities ('dbo.Table1', 'OBJECT')
;
GO

-- Remove the table.  
DROP TABLE dbo.Table1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```console
 schema_name table_name referenced_column referencing_column  
 ----------- ---------- ----------------- ------------------  
 dbo         Table1     a                 c  
 dbo         Table1     b                 c  
```

### <a name="d-returning-non-schema-bound-column-dependencies"></a>4\. 비스키마 바운드 열 종속성 반환  
 다음 예에서는 `Table1`을 삭제하고 `Table2` 및 저장 프로시저 `Proc1`을 만듭니다. 이 프로시저는 `Table2` 및 존재하지 않는 테이블 `Table1`을 참조합니다. 저장 프로시저가 참조 엔터티로 지정되어 `sys.dm_sql_referenced_entities` 뷰가 실행됩니다. 결과 집합에는 `Table1`에 대한 행 하나와 `Table2`에 대한 행 세 개가 표시됩니다. `Table1`이 없기 때문에 열 종속성을 확인할 수 없고 오류 2020이 반환됩니다. `is_all_columns_found` 열은 `Table1`에 대해 검색할 수 없는 열이 있음을 나타내는 0을 반환합니다.  
  
```sql  
DROP TABLE IF EXISTS dbo.Table1;
GO  
CREATE TABLE dbo.Table2 (c1 int, c2 int);  
GO  
CREATE PROCEDURE dbo.Proc1 AS  
    SELECT a, b, c FROM Table1;  
    SELECT c1, c2 FROM Table2;  
GO  
SELECT
        referenced_id,
        referenced_entity_name AS table_name,
        referenced_minor_name  AS referenced_column_name,
        is_all_columns_found
    FROM
        sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```console
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1  
 935674381     Table2       C1                      1  
 935674381     Table2       C2                      1  
 NULL          Table1       NULL                    0  

Msg 2020, Level 16, State 1, Line 1
The dependencies reported for entity "dbo.Proc1" might not include
  references to all columns. This is either because the entity
  references an object that does not exist or because of an error
  in one or more statements in the entity.  Before rerunning the
  query, ensure that there are no errors in the entity and that
  all objects referenced by the entity exist.
 ```
  
### <a name="e-demonstrating-dynamic-dependency-maintenance"></a>5\. 동적 종속성 유지 관리 설명  

이 예제 E 예제 D 실행 된 것을 가정 합니다. 예제 E를 보여 줍니다 종속성 동적으로 유지 됩니다. 이 예제에서는 다음 작업을 수행합니다.

1. 다시 만듭니다 `Table1`, 예제 d에서 삭제
2. 그런 다음 실행 `sys.dm_sql_referenced_entities` 저장된 프로시저가 참조 엔터티로 지정을 사용 하 여 다시 실행 됩니다.

결과 집합에서는 테이블 및 저장된 프로시저에 정의 된 해당 열을 모두 반환 됩니다. 또한 `is_all_columns_found` 열은 모든 개체 및 열에 대해 1을 반환합니다.

```sql  
CREATE TABLE Table1 (a int, b int, c AS a + b);  
GO   
SELECT
        referenced_id,
        referenced_entity_name AS table_name,
        referenced_minor_name  AS column_name,
        is_all_columns_found
    FROM
        sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');
GO  
DROP TABLE Table1, Table2;  
DROP PROC Proc1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```console
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1 
 935674381     Table2       c1                      1 
 935674381     Table2       c2                      1 
 967674495     Table1       NULL                    1 
 967674495     Table1       a                       1  
 967674495     Table1       b                       1  
 967674495     Table1       c                       1  
 ```
 
### <a name="f-returning-object-or-column-usage"></a>6\. 개체 또는 열 사용법 반환  
 다음 예에서는 저장 프로시저 `HumanResources.uspUpdateEmployeePersonalInfo`의 개체 및 열 종속성을 반환합니다. 이 절차는 열을 업데이트 `NationalIDNumber`, `BirthDate,``MaritalStatus`, 및 `Gender` 의 `Employee` 테이블 기준으로 지정 된 `BusinessEntityID` 값입니다. 다른 저장된 프로시저 `upsLogError` 에 정의 된... 실행 오류를 캡처하려면 블록을 CATCH 합니다. `is_selected`, `is_updated` 및 `is_select_all` 열은 참조하는 개체 내에 이러한 개체 및 열이 사용되는 방식에 대한 정보를 반환합니다. 수정된 테이블 및 열은 is_updated 열에서 1로 표시됩니다. `BusinessEntityID` 열만 선택되며 저장 프로시저 `uspLogError`는 선택되거나 수정되지 않습니다.  

```sql  
USE AdventureWorks2012;
GO
SELECT
        referenced_entity_name AS table_name,
        referenced_minor_name  AS column_name,
        is_selected,  is_updated,  is_select_all
    FROM
        sys.dm_sql_referenced_entities(
            'HumanResources.uspUpdateEmployeePersonalInfo',
            'OBJECT')
;
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```console
 table_name    column_name         is_selected is_updated is_select_all  
 ------------- ------------------- ----------- ---------- -------------  
 uspLogError   NULL                0           0          0  
 Employee      NULL                0           1          0  
 Employee      BusinessEntityID    1           0          0  
 Employee      NationalIDNumber    0           1          0  
 Employee      BirthDate           0           1          0  
 Employee      MaritalStatus       0           1          0  
 Employee      Gender              0           1          0
 ```
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
