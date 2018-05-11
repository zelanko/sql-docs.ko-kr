---
title: 필터 함수를 사용하여 마이그레이션할 행 선택(Stretch Database) | Microsoft 문서
ms.custom: ''
ms.date: 06/27/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: stretch-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, predicates
- predicates for Stretch Database
- Stretch Database, inline table-valued functions
- inline table-valued functions for Stretch Database
ms.assetid: 090890ee-7620-4a08-8e15-d2fbc71dd12f
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fece0ae561d4dbb615b885ce639a30bf61be4c41
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="select-rows-to-migrate-by-using-a-filter-function-stretch-database"></a>필터 함수를 사용하여 마이그레이션할 행 선택(Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  콜드 데이터를 별도 테이블에 저장하는 경우 전체 테이블을 마이그레이션하도록 스트레치 데이터베이스를 구성할 수 있습니다. 반면, 테이블에 핫 데이터와 콜드 데이터가 모두 포함된 경우 필터 조건자를 지정하여 마이그레이션할 행을 선택할 수 있습니다. 필터 조건자는 인라인 테이블 반환 함수입니다. 이 문서에서는 인라인 테이블 반환 함수를 작성하여 마이그레이션할 행을 선택하는 방법을 설명합니다.  
  
> [!IMPORTANT]
> 제대로 수행되지 않는 필터 함수를 제공하면 데이터 마이그레이션 성능도 저하됩니다. 스트레치 데이터베이스는 CROSS APPLY 연산자를 사용하여 테이블에 필터 함수를 적용합니다.  
  
 필터 함수를 지정하지 않으면 전체 테이블이 마이그레이션됩니다.  
  
 스트레치에 데이터베이스 사용 마법사를 실행할 때, 전체 테이블을 마이그레이션하거나 마법사에서 간단한 필터 함수를 지정할 수 있습니다. 다른 유형의 필터 함수를 사용하여 마이그레이션할 행을 선택하려면 다음 중 하나를 수행합니다.  
  
-   마법사를 종료하고 ALTER TABLE 문을 실행하여 테이블에 대해 스트레치를 사용하도록 설정하고 필터 함수를 지정합니다.  
  
-   마법사를 종료한 후 ALTER TABLE 문을 실행하여 필터 함수를 지정합니다.  
  
 함수를 추가하기 위한 ALTER TABLE 구문은 이 문서의 뒷부분에 설명되어 있습니다.  
  
## <a name="basic-requirements-for-the-filter-function"></a>필터 함수에 대한 기본 요구 사항  
 스트레치 데이터베이스 필터 조건자에 필요한 인라인 테이블 반환 함수는 다음 예제와 유사합니다.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datatype1, @column2 datatype2 [, ...n])  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE <predicate>  
```  
  
 이 함수의 매개 변수는 테이블의 열에 대한 식별자여야 합니다.  
  
 스키마 바인딩은 필터 함수에 사용되는 열이 삭제되거나 변경되는 것을 방지하는 데 필요합니다.  
  
### <a name="return-value"></a>반환 값  
 함수에서 비어 있지 않은 결과가 반환되는 경우 해당 행은 마이그레이션에 적합합니다. 그렇지 않으면, 즉 함수에서 결과가 반환되지 않으면 해당 행은 마이그레이션에 적합하지 않습니다.  
  
### <a name="conditions"></a>조건  
 &lt;*predicate*&gt; 는 하나의 조건 또는 AND 논리 연산자로 조인된 여러 조건으로 구성될 수 있습니다.  
  
```  
<predicate> ::= <condition> [ AND <condition> ] [ ...n ]  
```  
  
 각 조건은 하나의 기본 조건 또는 OR 논리 연산자로 조인된 여러 기본 조건으로 구성될 수 있습니다.  
  
```  
<condition> ::= <primitive_condition> [ OR <primitive_condition> ] [ ...n ]  
```  
  
### <a name="primitive-conditions"></a>기본 조건  
 기본 조건은 다음 비교 중 하나를 수행할 수 있습니다.  
  
```  
<primitive_condition> ::=   
{  
<function_parameter> <comparison_operator> constant  
| <function_parameter> { IS NULL | IS NOT NULL }  
| <function_parameter> IN ( constant [ ,...n ] )  
}  
  
```  
  
-   함수 매개 변수를 상수 식과 비교합니다. `@column1 < 1000`)을 입력합니다.  
  
     다음은 *date* 열의 값이 &lt; 1/1/2016인지 확인하는 예제입니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
    GO  
  
    ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   IS NULL 또는 IS NOT NULL 연산자를 함수 매개 변수에 적용합니다.  
  
-   IN 연산자를 사용하여 함수 매개 변수를 상수 값 목록과 비교할 수 있습니다.  
  
     다음은 *shipment_status`IN (N'Completed', N'Returned', N'Cancelled')` 열의 값이* 인지 확인하는 예제입니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
### <a name="comparison-operators"></a>비교 연산자  
 지원되는 비교 연산자는 다음과 같습니다.  
  
 `<, <=, >, >=, =, <>, !=, !<, !>`  
  
```  
<comparison_operator> ::= { < | <= | > | >= | = | <> | != | !< | !> }  
```  
  
### <a name="constant-expressions"></a>상수 식  
 필터 함수에 사용하는 상수는 함수를 정의할 때 계산될 수 있는 모든 명확한 식일 수 있습니다. 상수 식은 다음을 포함할 수 있습니다.  
  
-   리터럴. `N’abc’, 123`)을 입력합니다.  
  
-   대수 식. `123 + 456`)을 입력합니다.  
  
-   명확한 함수. `SQRT(900)`)을 입력합니다.  
  
-   CAST 또는 CONVERT를 사용하는 명확한 변환. `CONVERT(datetime, '1/1/2016', 101)`)을 입력합니다.  
  
### <a name="other-expressions"></a>다른 식  
 BETWEEN 및 NOT BETWEEN 연산자를 동등한 AND 및 OR 식으로 바꾼 후 결과 함수가 여기에 설명된 규칙을 준수하는 경우 BETWEEN 및 NOT BETWEEN 연산자를 사용할 수 있습니다.  
  
 하위 쿼리 또는 명확하지 않은 함수(예: RAND() 또는 GETDATE())를 사용할 수 없습니다.  
  
## <a name="add-a-filter-function-to-a-table"></a>테이블에 필터 함수 추가  
 **ALTER TABLE** 문을 실행하고 기존 인라인 테이블 반환 함수를 **FILTER_PREDICATE** 매개 변수 값으로 지정하여 테이블에 필터 함수를 추가합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 함수를 테이블에 조건자로 바인딩한 후에는 다음과 같은 상황이 발생합니다.  
  
-   다음에 데이터 마이그레이션이 발생할 경우 함수에서 비어 있지 않은 값을 반환하는 행만 마이그레이션됩니다.  
  
-   함수에서 사용되는 열이 스키마 바인딩됩니다. 테이블에서 해당 함수를 필터 조건자로 사용하는 한 이러한 열을 변경할 수 없습니다.  
  
 테이블에서 해당 함수를 필터 조건자로 사용하는 한 인라인 테이블 반환 함수를 삭제할 수 없습니다. 

> [!TIP]
> 필터 함수의 성능을 향상시키려면 해당 함수에서 사용되는 열에 인덱스를 만듭니다.

 ### <a name="passing-column-names-to-the-filter-function"></a>필터 함수에 열 이름 전달
 
 테이블에 필터 함수를 할당할 때 한 부분으로 이루어진 이름을 사용하여 필터 함수에 전달되는 열 이름을 지정합니다. 열 이름을 전달할 때 세 부분으로 이루어진 이름을 지정하면 스트레치 사용 테이블에 대한 후속 쿼리가 실패합니다.

예를 들어 다음 예제와 같이 세 부분으로 이루어진 열 이름을 지정하면 문은 성공적으로 실행되지만 테이블에 대한 후속 쿼리가 실패합니다.

```sql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(dbo.SensorTelemetry.ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```

대신, 다음 예제와 같이 한 부분으로 이루어진 열 이름을 사용하여 필터 함수를 지정합니다.

```sql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON  (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```
  
## <a name="addafterwiz"></a>마법사를 실행한 후 필터 함수 추가  
  
**스트레치에 데이터베이스 사용** 마법사에서 만들 수 없는 함수를 사용하려는 경우 마법사를 종료한 후 **ALTER TABLE** 문을 실행하여 함수를 지정할 수 있습니다. 그러나 함수를 적용하려면 이미 진행 중인 데이터 마이그레이션을 중지하고 마이그레이션된 데이터를 다시 가져와야 합니다. 이 작업이 필요한 이유에 대한 자세한 내용은 [기존 필터 함수 바꾸기](#replacePredicate)를 참조하세요.
  
1. 마이그레이션 방향을 반대로 지정하고 이미 마이그레이션된 데이터를 다시 가져옵니다. 이 작업을 시작한 후에는 취소할 수 없습니다. 또한 Azure에서 아웃바운드 데이터 전송(송신) 비용이 발생합니다. 자세한 내용은 [Azure 가격 책정 방식](https://azure.microsoft.com/pricing/details/data-transfers/)을 참조하세요.  
  
    ```sql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;   
    ```  
  
2. 마이그레이션이 완료될 때까지 기다립니다. SQL Server Management Studio의 **스트레치 데이터베이스 모니터** 에서 상태를 확인하거나 **sys.dm_db_rda_migration_status** 뷰를 쿼리할 수 있습니다. 자세한 내용은 [데이터 마이그레이션 모니터 및 문제 해결](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 또는 [sys.dm_db_rda_migration_status](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)를 참조하세요.  
  
3. 테이블에 적용할 필터 함수를 만듭니다.  
  
4. 테이블에 함수를 추가하고 Azure로 데이터 마이그레이션을 다시 시작합니다.  
  
    ```sql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE  
            (           
                FILTER_PREDICATE = <predicate>,  
                MIGRATION_STATE = OUTBOUND  
            )  
            );   
    ```  
  
## <a name="filter-rows-by-date"></a>날짜별로 행 필터링  
 다음 예제에서는 **date** 열에 2016년 1월 1일 이전 값이 포함된 행을 마이그레이션합니다.  
  
```sql  
-- Filter by date  
--  
CREATE FUNCTION dbo.fn_stretch_by_date(@date datetime2)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @date < CONVERT(datetime2, '1/1/2016', 101)  
GO  
  
```  
  
## <a name="filter-rows-by-the-value-in-a-status-column"></a>상태 열의 값으로 행 필터링  
 다음 예제에서는 **status** 열에 지정된 값 중 하나가 포함된 행을 마이그레이션합니다.  
  
```sql  
-- Filter by status column  
--  
CREATE FUNCTION dbo.fn_stretch_by_status(@status nvarchar(128))  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @status IN (N'Completed', N'Returned', N'Cancelled')  
GO  
  
```  
  
## <a name="filter-rows-by-using-a-sliding-window"></a>슬라이딩 윈도우를 사용하여 행 필터링  
 슬라이딩 윈도우를 사용하여 행을 필터링하려면 필터 함수에 대한 다음 같은 요구 사항을 염두에 두어야 합니다.  
  
-   함수는 명확해야 합니다. 따라서 시간이 지남에 따라 슬라이딩 윈도우를 자동으로 다시 계산하는 함수를 만들 수 없습니다.  
  
-   함수에서 스키마 바인딩을 사용합니다. 따라서 단순히 **ALTER FUNCTION** 을 호출하여 슬라이딩 윈도우를 이동하는 방식으로 함수를 매일 “바로” 업데이트할 수 없습니다.  
  
 다음 예제와 같이 **systemEndTime** 열에 2016년 1월 1일 이전 값이 포함된 행을 마이그레이션하는 필터 함수로 시작합니다.  
  
```sql  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2016-01-01T00:00:00', 101) ;  
  
```  
  
 테이블에 필터 함수를 적용합니다.  
  
```sql  
ALTER TABLE <table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160101(SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
  
```  
  
 슬라이딩 윈도우를 업데이트하려는 경우 다음을 수행합니다.  
  
1.  새 슬라이딩 윈도우를 지정하는 새 함수를 만듭니다. 다음 예제에서는 2016년 1월 1일 대신 2016년 1월 2일 이전 날짜를 선택합니다.  
  
2.  다음 예제와 같이 **ALTER TABLE**을 호출하여 이전 필터 함수를 새 필터 함수로 바꿉니다.  
  
3.  필요에 따라 **DROP FUNCTION**을 호출하여 더 이상 사용하지 않는 이전 필터 함수를 삭제합니다. 이 단계는 예제에 표시되어 있지 않습니다.  
  
```sql  
BEGIN TRAN  
GO  
        /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2016-01-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as the filter predicate */  
        ALTER TABLE <table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
  
```  
  
## <a name="more-examples-of-valid-filter-functions"></a>유효한 필터 함수의 추가 예제  
  
-   다음 예제에서는 AND 논리 연산자를 사용하여 두 개의 기본 조건을 결합합니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate((@column1 datetime, @column2 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
      WHERE @column1 < N'20150101' AND @column2 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date, shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   다음 예제에서는 CONVERT와 함께 여러 조건 및 명확한 변환을 사용합니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example1(@column1 datetime, @column2 int, @column3 nvarchar)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101) AND (@column2 < -100 OR @column2 > 100 OR @column2 IS NULL) AND @column3 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ```  
  
-   다음 예제에서는 수학 연산자 및 함수를 사용합니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example2(@column1 float)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < SQRT(400) + 10  
    GO  
  
    ```  
  
-   다음 예제에서는 BETWEEN 및 NOT BETWEEN 연산자를 사용합니다. 이는 BETWEEN 및 NOT BETWEEN 연산자를 동등한 AND 및 OR 식으로 바꾼 후 결과 함수가 여기에 설명된 규칙을 준수하기 때문에 사용할 수 있습니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example3(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 BETWEEN 0 AND 100  
                AND (@column2 NOT BETWEEN 200 AND 300 OR @column1 = 50)  
    GO  
  
    ```  
  
     위 함수는 BETWEEN 및 NOT BETWEEN 연산자를 동등한 AND 및 OR 식으로 바꾼 후 다음 함수와 동일합니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example4(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 >= 0 AND @column1 <= 100 AND (@column2 < 200 OR @column2 > 300 OR @column1 = 50)  
    GO  
  
    ```  
  
## <a name="examples-of-filter-functions-that-arent-valid"></a>유효하지 않은 필터 함수의 예제  
  
-   다음 함수는 명확하지 않은 변환을 포함하기 때문에 유효하지 않습니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example5(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016')  
    GO  
  
    ```  
  
-   다음 함수는 명확하지 않은 함수 호출을 포함하기 때문에 유효하지 않습니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example6(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < DATEADD(day, -60, GETDATE())  
    GO  
  
    ```  
  
-   다음 함수는 하위 쿼리를 포함하기 때문에 유효하지 않습니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example7(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (SELECT SupplierID FROM Supplier WHERE Status = 'Defunct')  
    GO  
  
    ```  
  
-   다음 함수는 함수를 정의할 때 대수 연산자 또는 기본 제공 함수를 사용하는 식이 상수로 계산되어야 하기 때문에 유효하지 않습니다. 대수 식 또는 함수 호출에는 열 참조를 포함할 수 없습니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example8(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 % 2 =  0  
    GO  
  
    CREATE FUNCTION dbo.fn_example9(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE SQRT(@column1) = 30  
    GO  
  
    ```  
  
-   다음 함수는 BETWEEN 연산자를 동등한 AND 식으로 바꾼 후 여기에 설명된 규칙을 위반하기 때문에 유효하지 않습니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example10(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
    AS  
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 BETWEEN 1 AND 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
     위 함수는 BETWEEN 연산자를 동등한 AND 식으로 바꾼 후 다음 함수와 동일합니다. 이 함수는 기본 조건에서 OR 논리 연산자만 사용할 수 있으므로 유효하지 않습니다.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example11(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 >= 1 AND @column1 <= 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
## <a name="how-stretch-database-applies-the-filter-function"></a>스트레치 데이터베이스에서 필터 함수를 적용하는 방법  
 스트레치 데이터베이스는 CROSS APPLY 연산자를 사용하여 테이블에 필터 함수를 적용하고 적합한 행을 결정합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```sql  
SELECT * FROM stretch_table_name CROSS APPLY fn_stretchpredicate(column1, column2)  
```  
  
 함수에서 행에 대해 비어 있지 않은 결과가 반환되는 경우 해당 행은 마이그레이션에 적합합니다.  
  
## <a name="replacePredicate"></a>기존 필터 함수 바꾸기  
 **ALTER TABLE** 문을 다시 실행하고 **FILTER_PREDICATE** 매개 변수에 대한 새 값을 지정하여 이전에 지정된 필터 함수를 바꿀 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate2(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
  
```  
  
 새 인라인 테이블 반환 함수에는 다음 요구 사항이 있습니다.  
  
-   새 함수는 이전 함수보다 덜 제한적이어야 합니다.  
  
-   이전 함수에 있던 모든 연산자가 새 함수에 있어야 합니다.  
  
-   새 함수는 이전 함수에 없는 연산자를 포함할 수 없습니다.  
  
-   연산자 인수의 순서를 변경할 수 없습니다.  
  
-   `<, <=, >, >=`  비교의 일부인 상수 값만 함수를 덜 제한적으로 만드는 방식으로 변경할 수 있습니다.  
  
### <a name="example-of-a-valid-replacement"></a>유효한 바꾸기의 예제  
 다음 함수를 현재 필터 함수라고 가정합니다.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate_old(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 다음 함수는 새 날짜 상수(이후의 구분 날짜를 지정함)가 함수를 덜 제한적으로 만들기 때문에 유효한 바꾸기입니다.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate_new(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '2/1/2016', 101)  
            AND (@column2 < -50 OR @column2 > 50)  
GO  
  
```  
  
### <a name="examples-of-replacements-that-arent-valid"></a>유효하지 않은 바꾸기의 예제  
 다음 함수는 새 날짜 상수(이전의 구분 날짜를 지정함)가 함수를 덜 제한적으로 만들지 않으므로 유효한 바꾸기가 아닙니다.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_1(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 다음 함수는 비교 연산자 중 하나가 제거되었으므로 유효한 바꾸기가 아닙니다.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_2(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -50)  
GO  
  
```  
  
 다음 함수는 AND 논리 연산자와 함께 새 조건이 추가되었으므로 유효한 바꾸기가 아닙니다.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_3(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
            AND (@column2 <> 0)  
GO  
  
```  
  
## <a name="remove-a-filter-function-from-a-table"></a>테이블에서 필터 함수 제거  
 선택한 행이 아니라 전체 테이블을 마이그레이션하려면 **FILTER_PREDICATE**  를 null로 설정하여 기존 함수를 제거합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = NULL,  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 필터 함수를 제거한 후에는 테이블의 모든 행이 마이그레이션에 적합합니다. 따라서 나중에 동일한 테이블에 대해 필터 함수를 지정하려면 먼저 Azure에서 테이블에 대한 모든 원격 데이터를 다시 가져와야 합니다. 이 제한 사항은 새 필터 함수를 제공할 때 마이그레이션에 적합하지 않은 행이 Azure로 이미 마이그레이션된 상황을 방지하기 위한 것입니다.  
  
## <a name="check-the-filter-function-applied-to-a-table"></a>테이블에 적용된 필터 함수 확인  
 테이블에 적용된 필터 함수를 확인하려면 **sys.remote_data_archive_tables** 카탈로그 뷰를 열고 **filter_predicate** 열의 값을 확인합니다. 값이 null이면 전체 테이블이 보관에 적합합니다. 자세한 내용은 [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)을 참조하세요.  
  
## <a name="security-notes-for-filter-functions"></a>필터 함수에 대한 보안 정보  
db_owner 권한이 있는 손상된 계정은 다음 작업을 수행할 수 있습니다.  
  
-   서버 리소스를 많이 사용하거나 장시간 대기하여 서비스 거부가 발생되게 하는 테이블 반환 함수를 만들어 적용합니다.  
  
-   사용자의 읽기 권한이 명시적으로 거부된 테이블의 내용을 유추할 수 있게 하는 테이블 반환 함수를 만들어 적용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
