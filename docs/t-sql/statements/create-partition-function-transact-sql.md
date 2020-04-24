---
title: CREATE PARTITION FUNCTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION FUNCTION
- PARTITION
- PARTITION FUNCTION
- PARTITION_FUNCTION_TSQL
- PARTITION_TSQL
- CREATE_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RANGE RIGHT partition functions
- RANGE LEFT partition functions
- partitioned indexes [SQL Server], functions
- functions [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], functions
- CREATE PARTITION FUNCTION statement
ms.assetid: 9dfe8b76-721e-42fd-81ae-14e22258c4f2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7529d06f5adacb930debea499059b4df42a71dea
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632474"
---
# <a name="create-partition-function-transact-sql"></a>CREATE PARTITION FUNCTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 지정된 열 값에 기반하여 테이블 또는 인덱스의 행을 파티션에 매핑하는 함수를 만듭니다. 분할된 테이블 또는 인덱스를 만드는 첫 번째 단계는 CREATE PARTITION FUNCTION을 사용하는 것입니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 테이블이나 인덱스 하나에 파티션을 최대 15,000개까지 포함할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CREATE PARTITION FUNCTION partition_function_name ( input_parameter_type )  
AS RANGE [ LEFT | RIGHT ]   
FOR VALUES ( [ boundary_value [ ,...n ] ] )   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *partition_function_name*  
 파티션 함수의 이름입니다. 파티션 함수의 이름은 데이터베이스 내에서 고유해야 하며 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
 *input_parameter_type*  
 분할에 사용되는 열의 데이터 형식입니다. **text**, **ntext**, **image**, **xml**, **timestamp**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , 별칭 데이터 형식 또는 CLR 사용자 정의 데이터 형식을 제외한 모든 데이터 형식은 분할 열로 사용할 수 있습니다.  
  
 분할 열이라고 하는 실제 열은 CREATE TABLE 또는 CREATE INDEX 문에 지정됩니다.  
  
 *boundary_value*  
 *partition_function_name*을 사용하는 분할된 테이블 또는 인덱스의 각 파티션에 대한 경계값을 지정합니다. *boundary_value*가 비어 있는 경우 파티션 함수는 *partition_function_name*을 사용하여 전체 테이블이나 인덱스를 단일 파티션에 매핑합니다. CREATE TABLE 또는 CREATE INDEX 문에 지정된 하나의 분할 열만 사용할 수 있습니다.  
  
 *boundary_value*는 변수를 참조할 수 있는 상수 식입니다. 여기에는 사용자 정의 형식 변수나 함수 및 사용자 정의 함수가 포함됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 식은 참조할 수 없습니다. *boundary_value*는 *input_parameter_type*에 제공된 데이터 형식과 일치하거나 해당 데이터 형식으로 암시적으로 변환할 수 있어야 하며 암시적인 변환 중에 값의 크기 및 소수 자릿수가 해당 *input_parameter_type*과 일치하지 않는 방식으로 잘려서는 안 됩니다.  

> [!NOTE]  
>  *boundary_value*가 **datetime** 또는 **smalldatetime** 리터럴로 구성된 경우 이러한 리터럴은 us_english가 세션 언어인 것으로 가정하여 처리됩니다. 이 기능은 더 이상 지원되지 않습니다. 파티션 함수 정의가 모든 세션 언어에 대해 예상대로 작동하도록 하려면 yyyymmdd 형식과 같이 모든 언어 설정에 대해 동일한 방식으로 해석되는 상수를 사용하거나 리터럴을 특정 스타일로 명시적으로 변환하는 것이 좋습니다. 서버의 언어 세션을 결정하려면 `SELECT @@LANGUAGE`를 실행합니다.
>
> 자세한 내용은 [날짜 값으로 리터럴 날짜 문자열의 비결정적 변환](../data-types/nondeterministic-convert-date-literals.md)을 참조하세요.
  
 *...n*  
 *boundary_value*에 제공된 값 개수가 14,999개를 초과하지 않도록 지정합니다. 생성되는 파티션 수는 *n* + 1개입니다. 값은 순서대로 나열되지 않아도 됩니다. 값이 순서대로 나열되지 않은 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 값을 정렬하여 함수를 만들고 값이 순서대로 제공되지 않았다는 경고를 반환합니다. *n*에 중복 값이 있는 경우 데이터베이스 엔진에서 오류를 반환합니다.  
  
 **LEFT** | RIGHT  
 *에서 간격 값을 왼쪽에서 오른쪽으로 오름차순으로 정렬할 때* boundary_value **[** ,  ...n[!INCLUDE[ssDE](../../includes/ssde-md.md)] ]이 각 경계 값 간격의 왼쪽과 오른쪽 중 어느 쪽에 속하는지 지정합니다. 지정하지 않은 경우 LEFT가 기본값입니다.  
  
## <a name="remarks"></a>설명  
 파티션 함수의 범위는 함수가 생성된 데이터베이스로 제한됩니다. 해당 데이터베이스 내에서 파티션 함수는 다른 함수와 서로 다른 네임스페이스에 있습니다.  
  
 해당 분할 열에 Null 값이 있는 모든 행은 맨 왼쪽 파티션에 위치합니다. 단, NULL이 경계 값으로 지정되고 RIGHT가 지정된 경우에는 맨 왼쪽 파티션은 빈 파티션이 되고 NULL 값은 다음 파티션에 위치하게 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 다음 사용 권한 중 하나를 사용하여 CREATE PARTITION FUNCTION을 실행할 수 있습니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 함수가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 함수가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
##  <a name="examples"></a><a name="BKMK_examples"></a> 예  
  
### <a name="a-creating-a-range-left-partition-function-on-an-int-column"></a>A. int 열에 RANGE LEFT 파티션 함수 만들기  
 다음 파티션 함수는 테이블이나 인덱스를 4개의 파티션으로 분할합니다.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
```  
  
 다음 표에서는 분할 열 **col1**에 대해 이 파티션 함수를 사용하는 테이블이 분할되는 방식을 보여 줍니다.  
  
|파티션|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**값**|**col1** <= `1`|**col1** > `1` AND **col1** <= `100`|**col1** > `100` AND **col1** <=`1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-range-right-partition-function-on-an-int-column"></a>B. int 열에 RANGE RIGHT 파티션 함수 만들기  
 다음 파티션 함수는 RANGE RIGHT를 지정한다는 점을 제외하고 *boundary_value* [ **,** _...n_ ]에 위 예와 동일한 값을 사용합니다.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE RIGHT FOR VALUES (1, 100, 1000);  
```  
  
 다음 표에서는 분할 열 **col1**에 대해 이 파티션 함수를 사용하는 테이블이 분할되는 방식을 보여 줍니다.  
  
|파티션|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**값**|**col1** \< `1`|**col1** >= `1` AND **col1** \< `100`|**col1** >= `100` AND **col1** \< `1000`|**col1** >= `1000`| 
  
### <a name="c-creating-a-range-right-partition-function-on-a-datetime-column"></a>C. datetime 열에 RANGE RIGHT 파티션 함수 만들기  
 다음 파티션 함수는 테이블이나 인덱스를 12개 파티션으로 분할합니다. 즉, 일년의 값을 분할하여 **datetime** 열에 각 달에 대한 하나의 파티션을 만듭니다.  
  
```sql  
CREATE PARTITION FUNCTION [myDateRangePF1] (datetime)  
AS RANGE RIGHT FOR VALUES ('20030201', '20030301', '20030401',  
               '20030501', '20030601', '20030701', '20030801',   
               '20030901', '20031001', '20031101', '20031201');  
```  
  
 다음 표에서는 분할 열 **datecol**에 대해 이 파티션 함수를 사용하는 테이블 또는 인덱스가 분할되는 방식을 보여줍니다.  
  
|파티션|1|2|...|11|12|  
|---------------|-------|-------|---------|--------|--------|  
|**값**|**datecol** \< `February 1, 2003`|**datecol** >= `February 1, 2003` AND **datecol** \< `March 1, 2003`||**datecol** >= `November 1, 2003` AND **col1** \< `December 1, 2003`|**datecol** >= `December 1, 2003`| 
  
### <a name="d-creating-a-partition-function-on-a-char-column"></a>D. char 열에 파티션 함수 만들기  
 다음 파티션 함수는 테이블이나 인덱스를 4개의 파티션으로 분할합니다.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF3 (char(20))  
AS RANGE RIGHT FOR VALUES ('EX', 'RXE', 'XR');  
```  
  
 다음 표에서는 분할 열 **col1**에 대해 이 파티션 함수를 사용하는 테이블이 분할되는 방식을 보여 줍니다.  
  
|파티션|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**값**|**col1** \< `EX`...|**col1** >= `EX` AND **col1** \< `RXE`...|**col1** >= `RXE` AND **col1** \< `XR`...|**col1** >= `XR`| 
  
### <a name="e-creating-15000-partitions"></a>E. 15,000개의 파티션 만들기  
 다음 파티션 함수는 테이블이나 인덱스를 15,000개의 파티션으로 분할합니다.  
  
```sql  
--Create integer partition function for 15,000 partitions.  
DECLARE @IntegerPartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION IntegerPartitionFunction (int) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i int = 1;  
WHILE @i < 14999  
BEGIN  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N', ';  
SET @i += 1;  
END  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N');';  
EXEC sp_executesql @IntegerPartitionFunction;  
GO  
```  
  
### <a name="f-creating-partitions-for-multiple-years"></a>F. 여러 연도에 대한 파티션 만들기  
 다음 파티션 함수는 테이블이나 인덱스를 **datetime2** 열에 50개의 파티션으로 분할합니다. 2007년 1월에서 2011년 1월 사이의 각 월마다 하나의 파티션이 있습니다.  
  
```sql  
--Create date partition function with increment by month.  
DECLARE @DatePartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION DatePartitionFunction (datetime2) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i datetime2 = '20070101';  
WHILE @i < '20110101'  
BEGIN  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10)) + '''' + N', ';  
SET @i = DATEADD(MM, 1, @i);  
END  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10))+ '''' + N');';  
EXEC sp_executesql @DatePartitionFunction;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [$PARTITION&#40;Transact-SQL&#41;](../../t-sql/functions/partition-transact-sql.md)   
 [ALTER PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_functions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

