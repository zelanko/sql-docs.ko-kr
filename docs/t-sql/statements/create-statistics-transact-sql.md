---
title: "통계 (Transact SQL) 만들기 | Microsoft Docs"
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
caps.latest.revision: 105
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e09604deac2b823243515c10398dc27c75941bd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-statistics-transact-sql"></a>CREATE STATISTICS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  테이블, 인덱싱된 뷰 또는 외부 테이블의 하나 이상의 열에 쿼리 최적화 통계를 만듭니다. 쿼리 최적화 프로그램은 대부분의 쿼리에 대해 고품질의 쿼리 계획에 필요한 통계를 기본적으로 생성합니다. 따라서 쿼리 성능을 향상시키기 위해 CREATE STATISTICS를 사용하여 추가 통계를 만들거나 쿼리 설계를 수정해야 하는 경우는 드뭅니다.  
  
 자세한 내용은 참고 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
          | STATS_STREAM = stats_stream ] ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ]  
    ] ;  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE STATISTICS statistics_name   
    ON [ database_name . [schema_name ] . | schema_name. ] table_name   
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
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
## <a name="arguments"></a>인수  
 *statistics_name*  
 만들 통계의 이름입니다.  
  
 *table_or_indexed_view_name*  
 테이블, 인덱싱된 뷰 또는 외부 테이블을 만들 통계의 이름이입니다. 다른 데이터베이스에서 통계를 만들려면 정규화 된 테이블 이름을 지정 합니다.  
  
 *열 [, … n]*  
 하나 이상의 열을 통계에 포함 합니다. 우선 순위에 따라 왼쪽에서 오른쪽으로 열 이어야 합니다. 첫 번째 열만 히스토그램을 만드는 데 사용 됩니다. 모든 열은 밀도 호출 하는 열 간 상관 관계 통계에 사용 됩니다.  
  
 다음 예외 사항을 제외하고 인덱스 키 열로 지정할 수 있는 모든 열을 지정할 수 있습니다.  
  
-   **Xml**, 전체 텍스트 및 FILESTREAM 열을 지정할 수 없습니다.  
  
-   ARITHABORT 및 QUOTED_IDENTIFIER 데이터베이스 설정이 ON으로 설정된 경우에만 계산 열을 지정할 수 있습니다.  
  
-   CLR 사용자 정의 형식 열은 이진 순서 정렬이 지원될 경우에만 지정할 수 있습니다. 사용자 정의 형식 열의 메서드 호출로 정의된 계산 열은 메서드가 결정적 메서드로 표시된 경우에 지정할 수 있습니다.  
  
 여기서 \<filter_predicate > 통계 개체를 만들 때 포함할 행 하위 집합을 선택 하는 식을 지정 합니다. 필터 조건자를 사용하여 만든 통계를 필터링된 통계라고 합니다. 필터 조건자는 간단한 비교 논리를 사용 하며 계산된 열, UDT 열, 공간 데이터 형식 열을 참조할 수 없습니다 또는 **hierarchyID** 데이터 형식 열입니다. 비교 연산자에는 NULL 리터럴을 사용한 비교를 사용할 수 없습니다. 대신 IS NULL 및 IS NOT NULL 연산자를 사용합니다.  
  
 다음은 Production.BillOfMaterials 테이블에 대한 필터 조건자의 예입니다.  
  
 `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 `WHERE ComponentID IN (533, 324, 753)`  
  
 `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 필터 조건자에 대 한 자세한 내용은 참조 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)합니다.  
  
 FULLSCAN  
 모든 행을 검색 하 여 통계를 계산 합니다. FULLSCAN과 SAMPLE 100 PERCENT의 결과는 같습니다. FULLSCAN은 SAMPLE 옵션과 함께 사용할 수 없습니다.  
  
 생략 하면 SQL Server 통계를 만들 샘플링을 사용 하 고 고품질의 쿼리 계획을 만드는 데 필요한 샘플 크기를 결정  
  
 샘플 *번호* {%| 행을 (를)  
 쿼리 최적화 프로그램에서 통계를 만들 때 사용할 테이블이나 인덱싱된 뷰에 있는 행의 비율이나 개수를 대략적으로 지정합니다. Percent의 경우 *번호* 에서 100 사이 행에 대 한 일 수 있습니다 *번호* 총 행 수를 0에서 일 수 있습니다. 쿼리 최적화 프로그램에서 샘플링하는 실제 행의 비율이나 개수는 지정된 비율이나 개수와 일치하지 않을 수 있습니다. 예를 들어, 쿼리 최적화 프로그램에서는 데이터 페이지의 모든 행을 검색합니다.  
  
 SAMPLE은 기본 샘플링을 기반으로 하는 쿼리 계획이 만족스럽지 못한 특별한 경우에 유용합니다. 대부분의 경우 쿼리 최적화 프로그램은 기본적으로 고품질의 쿼리 계획을 만들기 위해 필요에 따라 샘플링을 사용하고 통계적으로 중요한 샘플 크기를 결정하기 때문에 SAMPLE을 지정할 필요가 없습니다.  
  
 SAMPLE은 FULLSCAN 옵션과 함께 사용할 수 없습니다. SAMPLE과 FULLSCAN을 둘 다 지정하지 않으면 기본적으로 쿼리 최적화 프로그램에서 샘플링된 데이터를 사용하고 샘플 크기를 계산합니다.  
  
 0 PERCENT 또는 0 ROWS로 지정하지 않는 것이 좋습니다. 0 PERCENT 또는 0 ROWS로 지정하면 통계 데이터가 포함되지 않은 빈 통계 개체가 만들어집니다.  
 
 PERSIST_SAMPLE_PERCENT = {ON | OFF}  
 때 **ON**, 통계 샘플링 비율을 명시적으로 지정 하지 않으면 후속 업데이트에 대 한 만들기 샘플링 백분율을 그대로 유지 됩니다. 때 **OFF**, 통계 샘플링 비율 샘플링 비율을 명시적으로 지정 하지 않은 이후의 업데이트에서 기본 샘플링을 다시 설정 될 됩니다. 기본값은 **OFF**합니다. 
 
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 c u 4입니다.  
  
 STATS_STREAM  **=**  *stats_stream*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 NORECOMPUTE  
 에 대 한 자동 통계 업데이트 옵션인 AUTO_STATISTICS_UPDATE를 비활성화 *statistics_name*합니다. 쿼리 최적화 프로그램에 대 한 모든 진행 중인 통계 업데이트를 완료 하이 옵션을 지정 하는 경우 *statistics_name* 이후의 업데이트를 비활성화 하 고 있습니다.  
  
 통계 업데이트를 다시 사용 하려면 사용 하 여 통계 제거 [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md) 다음 NORECOMPUTE 옵션 없이 CREATE STATISTICS를 실행 합니다.  
  
> [!WARNING]  
>  이 옵션을 사용하면 최적이 아닌 쿼리 계획이 생성될 수 있습니다. 이 옵션은 자격 있는 시스템 관리자가 꼭 필요한 경우에만 사용하는 것이 좋습니다.  
  
 AUTO_STATISTICS_UPDATE 옵션에 대 한 자세한 내용은 참조 하세요. [ALTER DATABASE SET 옵션 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). 통계 업데이트를 다시 활성화 및 비활성화 하는 방법에 대 한 자세한 내용은 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
 INCREMENTAL = {ON | OFF}  
 때 **ON**, 파티션 통계 별로 통계가 작성 됩니다. 때 **OFF**, 통계는 모든 파티션에 대 한 결합 됩니다. 기본값은 **OFF**합니다.  
  
 파티션별 통계가 지원되지 않을 경우 오류가 생성됩니다. 다음 통계 유형에 대해서는 증분 통계가 지원되지 않습니다.  
  
-   기본 테이블을 기준으로 파티션 정렬되지 않은 인덱스를 사용하여 작성된 통계입니다.  
  
-   Always On 읽기 가능한 보조 데이터베이스에 대해 작성된 통계입니다.  
  
-   읽기 전용 데이터베이스에 대해 작성된 통계입니다.  
  
-   필터링된 인덱스에 대해 작성된 통계입니다.  
  
-   뷰에 대해 작성된 통계입니다.  
  
-   내부 테이블에 대해 작성된 통계입니다.  
  
-   공간 인덱스 또는 XML 인덱스를 사용하여 작성된 통계입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
## <a name="permissions"></a>Permissions  
 이러한 사용 권한 중 하나가 필요합니다.  
  
-   ALTER TABLE  
  
-   사용자는 소유자  
  
-   멤버 자격이 **db_ddladmin** 고정된 데이터베이스 역할  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]통계를 작성 하기 전에 샘플링된 한 행을 정렬 하려면 tempdb를 사용할 수 있습니다.  
  
### <a name="statistics-for-external-tables"></a>외부 테이블에 대 한 통계  
 외부 테이블 통계를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 임시에 외부 테이블을 가져오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 선택한 다음 통계를 작성 합니다. 샘플 통계에 대 한 샘플링된 한 행만 가져옵니다. 큰 외부 테이블을 설정한 경우 전체 검색 옵션 대신 기본 샘플링을 사용 하는 것이 빠르므로 됩니다.  
  
### <a name="statistics-with-a-filtered-condition"></a>필터링 된 조건 사용 하 여 통계  
 필터링된 통계는 잘 정의된 데이터의 하위 집합에서 선택하는 쿼리에 대한 쿼리 성능을 높일 수 있습니다. WHERE 절의 필터 조건자를 사용하여 통계에 포함되는 데이터의 하위 집합을 선택합니다.  
  
### <a name="when-to-use-create-statistics"></a>CREATE STATISTICS를 사용하는 경우  
 CREATE STATISTICS를 사용 하는 경우에 대 한 자세한 내용은 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
### <a name="referencing-dependencies-for-filtered-statistics"></a>필터링된 통계의 종속성 참조  
 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 카탈로그 뷰 종속성 참조로 필터링 된 통계 조건자의 각 열을 추적 합니다. 필터링된 통계 조건자에서 정의된 테이블 열은 삭제, 이름 바꾸기 또는 정의 변경을 수행할 수 없으므로 필터링된 통계를 만들기 전에 테이블 열에서 수행하는 작업을 고려하세요.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
*  외부 테이블에서 통계를 업데이트할 수 없습니다. 외부 테이블에 대 한 통계를 업데이트 하려면 삭제 하 고 통계를 다시 만듭니다.  
*  개체당 최대 64 개 열을 나열할 수 있습니다.
  
## <a name="examples"></a>예  

### <a name="examples-use-the-adventureworks-database"></a>예제는 AdventureWorks 데이터베이스를 사용합니다.  

### <a name="a-using-create-statistics-with-sample-number-percent"></a>1. CREATE STATISTICS에 SAMPLE number PERCENT 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `ContactMail1` 테이블에서 `BusinessEntityID` 및 `EmailPromotion` 열에 대해 5% 무작위 샘플링을 사용하여 `Contact` 통계를 만듭니다.  
  
```t-sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
```  
  
### <a name="b-using-create-statistics-with-fullscan-and-norecompute"></a>2. CREATE STATISTICS에 FULLSCAN 및 NORECOMPUTE 사용  
 다음 예에서는 `ContactMail2` 테이블의 `BusinessEntityID` 및 `EmailPromotion` 열에서 모든 행에 대한 `Contact` 통계를 만듭니다. 통계의 자동 다시 계산 기능은 사용하지 않습니다.  
  
```t-sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, NORECOMPUTE;  
```  
  
### <a name="c-using-create-statistics-to-create-filtered-statistics"></a>3. CREATE STATISTICS를 사용하여 필터링된 통계 만들기  
 다음 예에서는 필터링된 통계 `ContactPromotion1`을 만듭니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 데이터의 50%를 샘플링한 다음 `EmailPromotion`이 2인 행을 선택합니다.  
  
```t-sql  
CREATE STATISTICS ContactPromotion1  
    ON Person.Person (BusinessEntityID, LastName, EmailPromotion)  
WHERE EmailPromotion = 2  
WITH SAMPLE 50 PERCENT;  
GO  
```  
  
### <a name="d-create-statistics-on-an-external-table"></a>4. 외부 테이블에서 통계를 작성 합니다.  
 외부 테이블, 열 목록 외에 통계를 만들 때 판단 해야 하는 유일한 결정 행을 샘플링 하 여 또는 모든 행을 검사 하 여 통계를 만들 것인지 여부입니다.  
  
 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 검색 옵션 통계를 만들려면를 임시 테이블에 외부 테이블에서 훨씬 더 오래 걸립니다. 큰 테이블에 대 한 기본 샘플링 방법으로 충분 합니다.  
  
```t-sql  
--Create statistics on an external table and use default sampling.  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
  
--Create statistics on an external table and scan all the rows  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  

### <a name="e-using-create-statistics-with-fullscan-and-persistsamplepercent"></a>5. CREATE STATISTICS에 FULLSCAN 및 PERSIST_SAMPLE_PERCENT 사용  
 다음 예제에서는 `ContactMail2` 의 모든 행에 대 한 통계는 `BusinessEntityID` 및 `EmailPromotion` 의 열은 `Contact` 테이블을 명시적으로 되어 있어야 하지 않는 한 모든 후속 업데이트는 샘플링을 지정할 100% 샘플링 비율을 설정 합니다. 백분율입니다.  
  
```t-sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, PERSIST_SAMPLE_PERCENT = ON;  
```  
  
### <a name="examples-using-adventureworksdw-database"></a>AdventureWorksDW 데이터베이스를 사용 하는 예제입니다. 
  
### <a name="f-create-statistics-on-two-columns"></a>6. 두 열에 통계를 작성 합니다.  
 다음 예제에서는 `CustomerStats1` 기준으로 통계는 `CustomerKey` 및 `EmailAddress` 의 열은 `DimCustomer` 테이블입니다. 통계에 있는 행의 통계적으로 중요 한 샘플링을 기반으로 생성 된 `Customer` 테이블입니다.  
  
```t-sql  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
```  
  
### <a name="g-create-statistics-by-using-a-full-scan"></a>7. 전체 검색을 사용 하 여 통계를 만들어  
 다음 예제에서는 `CustomerStatsFullScan` 에 있는 행의 모든 검색 기준으로 통계는 `DimCustomer` 테이블입니다.  
  
```t-sql  
CREATE STATISTICS CustomerStatsFullScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  
  
### <a name="h-create-statistics-by-specifying-the-sample-percentage"></a>8. 샘플 비율을 지정 하 여 통계를 만들어  
 다음 예제에서는 `CustomerStatsSampleScan` 에 있는 행의 50% 검색 기준으로 통계는 `DimCustomer` 테이블입니다.  
  
```t-sql  
CREATE STATISTICS CustomerStatsSampleScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH SAMPLE 50 PERCENT;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [통계](../../relational-databases/statistics/statistics.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sys.stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  


