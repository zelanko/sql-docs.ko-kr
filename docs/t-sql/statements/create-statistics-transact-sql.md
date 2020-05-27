---
title: CREATE STATISTICS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STATISTICS
- STATISTICS_TSQL
- CREATE STATISTICS
- CREATE_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], creating
- indexed views [SQL Server], statistics
- FULLSCAN option
- CREATE STATISTICS statement
- filtered statistics [SQL Server]
- creating statistics [SQL Server]
- NORECOMPUTE clause
ms.assetid: b23e2f6b-076c-4e6d-9281-764bdb616ad2
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7efc30e37b1242c66df856f79944de687650b99d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73982574"
---
# <a name="create-statistics-transact-sql"></a>CREATE STATISTICS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  하나 이상의 테이블 열, 인덱싱된 뷰 또는 외부 테이블에 대한 쿼리 최적화 통계를 만듭니다. 쿼리 최적화 프로그램은 대부분의 쿼리에 대해 고품질의 쿼리 계획에 필요한 통계를 기본적으로 생성합니다. 따라서 쿼리 성능을 향상시키기 위해 CREATE STATISTICS를 사용하여 추가 통계를 만들거나 쿼리 설계를 수정해야 하는 경우는 드뭅니다.  
  
 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create statistics on an external table  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WITH FULLSCAN ] ;  
  
-- Create statistics on a regular table or indexed view  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH   
        [ [ FULLSCAN   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | SAMPLE number { PERCENT | ROWS }   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | <update_stats_stream_option> [ ,...n ]    
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ] 
        [ [ , ] MAXDOP = max_degree_of_parallelism ]
    ] ;  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
    
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ] 
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE STATISTICS statistics_name   
    ON { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( column_name  [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH {  
           FULLSCAN   
           | SAMPLE number PERCENT   
      }  
    ]  
[;]  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
## <a name="arguments"></a>인수  
 *statistics_name*  
 만들 통계의 이름입니다.  
  
 *table_or_indexed_view_name*  
 통계를 만드는 대상이 되는 테이블, 인덱싱된 뷰 또는 외부 테이블의 이름입니다. 다른 데이터베이스에 대한 통계를 만들려면 정규화된 테이블 이름을 지정합니다.  
  
 *column [ ,...n]*  
 통계에 포함할 하나 이상의 열입니다. 열의 우선 순위는 왼쪽에서 오른쪽이어야 합니다. 히스토그램을 만드는 데에는 첫 번째 열만이 사용됩니다. 모든 열은 밀도라는 열간 상관 관계 통계에 사용됩니다.  
  
 다음 예외 사항을 제외하고 인덱스 키 열로 지정할 수 있는 모든 열을 지정할 수 있습니다.  
  
-   **Xml**, 전체 텍스트 및 파일 스트림 열은 지정할 수 없습니다.  
  
-   ARITHABORT 및 QUOTED_IDENTIFIER 데이터베이스 설정이 ON으로 설정된 경우에만 계산 열을 지정할 수 있습니다.  
  
-   CLR 사용자 정의 형식 열은 이진 순서 정렬이 지원될 경우에만 지정할 수 있습니다. 사용자 정의 형식 열의 메서드 호출로 정의된 계산 열은 메서드가 결정적 메서드로 표시된 경우에 지정할 수 있습니다.  
  
 WHERE \<filter_predicate> 통계 개체를 만들 때 포함할 행 하위 집합을 선택하는 식을 지정합니다. 필터 조건자를 사용하여 만든 통계를 필터링된 통계라고 합니다. 필터 조건자는 간단한 비교 논리를 사용하며 계산 열, UDT 열, 공간 데이터 형식 열 또는 **hierarchyID** 데이터 형식 열을 참조할 수 없습니다. 비교 연산자에는 NULL 리터럴을 사용한 비교를 사용할 수 없습니다. 대신 IS NULL 및 IS NOT NULL 연산자를 사용합니다.  
  
 다음은 Production.BillOfMaterials 테이블에 대한 필터 조건자의 예입니다.  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 필터 조건자에 대한 자세한 내용은 [필터링된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md)를 참조하세요.  
  
 FULLSCAN  
 모든 행을 검사하여 통계를 컴퓨팅합니다. FULLSCAN과 SAMPLE 100 PERCENT의 결과는 같습니다. FULLSCAN은 SAMPLE 옵션과 함께 사용할 수 없습니다.  
  
 생략하면 SQL Server는 샘플링을 사용하여 통계를 만들고 고품질의 쿼리 계획을 만드는 데 필요한 샘플 크기를 결정합니다.  
  
 SAMPLE *number* { PERCENT | ROWS }  
 쿼리 최적화 프로그램에서 통계를 만들 때 사용할 테이블이나 인덱싱된 뷰에 있는 행의 비율이나 개수를 대략적으로 지정합니다. PERCENT의 경우 *number*가 0부터 100까지일 수 있고, ROWS의 경우 *number*가 0부터 총 행 수까지일 수 있습니다. 쿼리 최적화 프로그램에서 샘플링하는 실제 행의 비율이나 개수는 지정된 비율이나 개수와 일치하지 않을 수 있습니다. 예를 들어, 쿼리 최적화 프로그램에서는 데이터 페이지의 모든 행을 검색합니다.  
  
 SAMPLE은 기본 샘플링을 기반으로 하는 쿼리 계획이 만족스럽지 못한 특별한 경우에 유용합니다. 대부분의 경우 쿼리 최적화 프로그램은 기본적으로 고품질의 쿼리 계획을 만들기 위해 필요에 따라 샘플링을 사용하고 통계적으로 중요한 샘플 크기를 결정하기 때문에 SAMPLE을 지정할 필요가 없습니다.  
  
 SAMPLE은 FULLSCAN 옵션과 함께 사용할 수 없습니다. SAMPLE과 FULLSCAN을 둘 다 지정하지 않으면 기본적으로 쿼리 최적화 프로그램에서 샘플링된 데이터를 사용하고 샘플 크기를 계산합니다.  
  
 0 PERCENT 또는 0 ROWS로 지정하지 않는 것이 좋습니다. 0 PERCENT 또는 0 ROWS로 지정하면 통계 데이터가 포함되지 않은 빈 통계 개체가 만들어집니다.  
 
 PERSIST_SAMPLE_PERCENT = { ON | OFF }  
 **ON**을 선택한 경우 통계는 샘플링 비율을 명시적으로 지정하지 않은 이후 업데이트에 대해 생성 샘플링 비율을 유지합니다. **OFF**를 선택한 경우 샘플링 비율을 명시적으로 지정하지 않은 이후 업데이트의 통계 샘플링 비율은 기본 샘플링으로 재설정됩니다. 기본값은 **OFF**입니다. 
 
 > [!NOTE]
 > 테이블이 잘린 경우 잘린 HoBT에서 작성된 모든 통계가 기본 샘플링 비율을 사용하도록 되돌아갑니다.

 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4부터) 이상([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1부터)    
  
 STATS_STREAM **=** _stats_stream_  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 NORECOMPUTE  
 *statistics_name*에 대해 자동 통계 업데이트 옵션인 AUTO_STATISTICS_UPDATE를 비활성화합니다. 이 옵션을 지정하면 쿼리 최적화 프로그램에서 *statistics_name*에 대해 진행 중인 모든 통계 업데이트를 완료하고 이후의 업데이트를 비활성화합니다.  
  
 통계 업데이트를 다시 활성화하려면 [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md)를 사용하여 통계를 제거한 다음, NORECOMPUTE 옵션 없이 CREATE STATISTICS를 실행합니다.  
  
> [!WARNING]  
> 이 옵션을 사용하면 최적이 아닌 쿼리 계획이 생성될 수 있습니다. 이 옵션은 자격 있는 시스템 관리자가 꼭 필요한 경우에만 사용하는 것이 좋습니다.  
  
 AUTO_STATISTICS_UPDATE 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요. 통계 업데이트를 비활성화하고 다시 활성화하는 방법은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
 INCREMENTAL = {ON | OFF}  
 **ON**으로 설정된 경우 파티션 통계별로 통계가 작성됩니다. **OFF**로 설정된 경우 통계는 모든 파티션에 대해 결합됩니다. 기본값은 **OFF**입니다.  
  
 파티션별 통계가 지원되지 않을 경우 오류가 생성됩니다. 다음 통계 유형에 대해서는 증분 통계가 지원되지 않습니다.  
  
-   기본 테이블을 기준으로 파티션 정렬되지 않은 인덱스를 사용하여 작성된 통계입니다.  
-   Always On 읽기 가능한 보조 데이터베이스에 대해 작성된 통계입니다.  
-   읽기 전용 데이터베이스에 대해 작성된 통계입니다.  
-   필터링된 인덱스에 대해 작성된 통계입니다.  
-   뷰에 대해 작성된 통계입니다.  
-   내부 테이블에 대해 작성된 통계입니다.  
-   공간 인덱스 또는 XML 인덱스를 사용하여 작성된 통계입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상  
  
MAXDOP = *max_degree_of_parallelism*  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작)  
  
 통계 작업 기간 동안 **최대 병렬 처리 수준** 구성 옵션을 재정의합니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
 *max_degree_of_parallelism*은 다음 중 하나일 수 있습니다.  
  
 1  
 병렬 계획이 생성되지 않습니다.  
  
 \>1  
 병렬 통계 작업에 사용되는 최대 프로세서 수를 현재 시스템 워크로드에 따라 지정된 수 또는 더 적은 수로 제한합니다.  
  
 0(기본값)  
 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 \<update_stats_stream_option> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  

## <a name="permissions"></a>사용 권한  
 다음 중 한 가지 권한이 필요합니다.  
  
-   ALTER TABLE  
-   사용자가 테이블 소유자  
-   **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 통계를 만들기 전에 tempdb를 사용하여 샘플링된 행을 정렬합니다.  
  
### <a name="statistics-for-external-tables"></a>외부 테이블에 대한 통계  
 외부 테이블 통계를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 외부 테이블을 임시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 가져온 다음, 통계를 만듭니다. 샘플 통계의 경우 샘플링된 행만 가져옵니다. 큰 외부 테이블이 있는 경우 전체 검사 옵션 대신에 기본 샘플링을 사용하는 것이 훨씬 더 빠릅니다.  
  
### <a name="statistics-with-a-filtered-condition"></a>필터링된 조건을 적용한 통계  
 필터링된 통계는 잘 정의된 데이터의 하위 집합에서 선택하는 쿼리에 대한 쿼리 성능을 높일 수 있습니다. WHERE 절의 필터 조건자를 사용하여 통계에 포함되는 데이터의 하위 집합을 선택합니다.  
  
### <a name="when-to-use-create-statistics"></a>CREATE STATISTICS를 사용하는 경우  
 CREATE STATISTICS를 사용하는 경우에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
### <a name="referencing-dependencies-for-filtered-statistics"></a>필터링된 통계의 종속성 참조  
 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 카탈로그 뷰에서는 필터링된 통계 조건자의 각 열을 참조 종속성으로 추적합니다. 필터링된 통계 조건자에서 정의된 테이블 열은 삭제, 이름 바꾸기 또는 정의 변경을 수행할 수 없으므로 필터링된 통계를 만들기 전에 테이블 열에서 수행하는 작업을 고려하세요.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
* 외부 테이블에 대해서는 통계 업데이트가 지원되지 않습니다. 외부 테이블에 대한 통계를 업데이트하려면 통계를 삭제하고 다시 만듭니다.  
* 정적 개체당 최대 64개의 열을 나열할 수 있습니다.
* MAXDOP 옵션은 STATS_STREAM, ROWCOUNT 및 PAGECOUNT 옵션과 호환되지 않습니다.
* MAXDOP 옵션은 Resource Governor 워크로드 그룹 MAX_DOP 설정으로 제한됩니다(사용된 경우).
  
## <a name="examples"></a>예  

### <a name="examples-use-the-adventureworks-database"></a>예제에서는 AdventureWorks 데이터베이스를 사용합니다.  

### <a name="a-using-create-statistics-with-sample-number-percent"></a>A. CREATE STATISTICS에 SAMPLE number PERCENT 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `ContactMail1` 테이블에서 `BusinessEntityID` 및 `EmailPromotion` 열에 대해 5% 무작위 샘플을 사용하여 `Person` 통계를 만듭니다.  
  
```sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
```  
  
### <a name="b-using-create-statistics-with-fullscan-and-norecompute"></a>B. CREATE STATISTICS에 FULLSCAN 및 NORECOMPUTE 사용  
 다음 예에서는 `NamePurchase` 테이블의 `BusinessEntityID` 및 `EmailPromotion` 열에서 모든 행에 대한 `Person` 통계를 만듭니다. 통계의 자동 다시 계산 기능은 사용하지 않습니다.  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, NORECOMPUTE;  
```  
  
### <a name="c-using-create-statistics-to-create-filtered-statistics"></a>C. CREATE STATISTICS를 사용하여 필터링된 통계 만들기  
 다음 예에서는 필터링된 통계 `ContactPromotion1`을 만듭니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 데이터의 50%를 샘플링한 다음 `EmailPromotion`이 2인 행을 선택합니다.  
  
```sql  
CREATE STATISTICS ContactPromotion1  
    ON Person.Person (BusinessEntityID, LastName, EmailPromotion)  
WHERE EmailPromotion = 2  
WITH SAMPLE 50 PERCENT;  
GO  
```  
  
### <a name="d-create-statistics-on-an-external-table"></a>D. 외부 테이블에 대한 통계 만들기  
 열 목록을 제공하는 것을 제외하고, 외부 테이블에 대한 통계를 만들 때 내려야 하는 유일한 결정은 통계를 만드는 방법이 행 샘플링인지 아니면 모든 행 검사인가 하는 것입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 통계를 만들기 위해 외부 테이블의 데이터를 임시 테이블로 가져오므로 전체 검사 옵션이 훨씬 더 오래 걸립니다. 큰 테이블의 경우 일반적으로 기본 샘플링 방법으로 충분합니다.  
  
```sql  
--Create statistics on an external table and use default sampling.  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
  
--Create statistics on an external table and scan all the rows  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  

### <a name="e-using-create-statistics-with-fullscan-and-persist_sample_percent"></a>E. FULLSCAN 및 PERSIST_SAMPLE_PERCENT와 함께 CREATE STATISTICS 사용  
 다음 예제에서는 `Person` 테이블의 `BusinessEntityID` 및 `EmailPromotion` 열에 있는 모든 행에 대한 `NamePurchase` 통계를 만들고 샘플링 비율을 명시적으로 지정하지 않은 모든 이후 업데이트에 대해 100% 샘플링 비율을 설정합니다.  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, PERSIST_SAMPLE_PERCENT = ON;  
```  
  
### <a name="examples-using-adventureworksdw-database"></a>AdventureWorksDW 데이터베이스를 사용하는 예제입니다. 
  
### <a name="f-create-statistics-on-two-columns"></a>F. 두 열에 대한 통계 만들기  
 다음 예제에서는 `DimCustomer` 테이블의 `CustomerKey` 및 `EmailAddress` 열을 기반으로 `CustomerStats1` 통계를 만듭니다. 통계는 `Customer` 테이블에 있는 행의 통계적으로 의미 있는 샘플링을 기반으로 작성됩니다.  
  
```sql  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
```  
  
### <a name="g-create-statistics-by-using-a-full-scan"></a>G. 전체 검사를 사용하여 통계 만들기  
 다음 예제에서는 `DimCustomer` 테이블의 모든 행 검사를 기반으로 `CustomerStatsFullScan` 통계를 만듭니다.  
  
```sql  
CREATE STATISTICS CustomerStatsFullScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  
  
### <a name="h-create-statistics-by-specifying-the-sample-percentage"></a>H. 샘플 비율을 지정하여 통계 만들기  
 다음 예제에서는 `DimCustomer` 테이블 행의 50% 검사를 기반으로 `CustomerStatsSampleScan` 통계를 만듭니다.  
  
```sql  
CREATE STATISTICS CustomerStatsSampleScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH SAMPLE 50 PERCENT;  
```  
  
## <a name="see-also"></a>참고 항목  
 [통계](../../relational-databases/statistics/statistics.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sys.stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

