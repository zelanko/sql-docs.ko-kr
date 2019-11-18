---
title: CREATE COLUMNSTORE INDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE INDEX
- COLUMNSTORE_INDEX_TSQL
- CREATE CLUSTERED COLUMNSTORE INDEX
- COLUMNSTORE_TSQL
- CREATE NONCLUSTERED COLUMNSTORE INDEX
- CREATE_NONCLUSTERED_COLUMNSTORE_INDEX_TSQL
- CREATE COLUMNSTORE INDEX
- CREATE_CLUSTERED_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE
dev_langs:
- TSQL
helpviewer_keywords:
- index creation [SQL Server], columnstore indexes
- columnstore index, creating
- CREATE COLUMNSTORE INDEX statement
- CREATE INDEX statement
ms.assetid: 7e1793b3-5383-4e3d-8cef-027c0c8cb5b1
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2e917d4dcd2f722bb9d683ebe0a6a8777487c61d
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729923"
---
# <a name="create-columnstore-index-transact-sql"></a>CREATE COLUMNSTORE INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

rowstore 테이블을 클러스터형 columnstore 인덱스로 변환하거나 비클러스터형 columnstore 인덱스를를 만듭니다. OLTP 워크로드에서 실시간 운영 분석을 효율적으로 실행하거나 데이터웨어 하우징 워크로드에 대한 데이터 압축 및 쿼리 성능을 향상시키기 위해 columnstore 인덱스를 사용합니다.  
  
> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 테이블을 클러스터형 columnstore 인덱스로 만들 수 있습니다.   더 이상 rowstore 테이블을 생성하여 클러스터형 columnstore 인덱스로 변환할 필요가 없습니다.  

> [!TIP]
> 인덱스 디자인 지침에 대한 자세한 내용은 [SQL Server 인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

예제로 건너뛰기:  
-   [Rowstore 테이블을 columnstore로 변환하는 예제](../../t-sql/statements/create-columnstore-index-transact-sql.md#convert)  
-   [비클러스터형 columnstore 인덱스에 대한 예제](../../t-sql/statements/create-columnstore-index-transact-sql.md#nonclustered)  
  
시나리오로 이동:  
-   [실시간 운영 분석을 위한 Columnstore 인덱스](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
-   [데이터 웨어하우스용 Columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
자세히 알아보기  
-   [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)  
-   [Columnstore 인덱스 기능 요약](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create a clustered columnstore index on disk-based table.  
CREATE CLUSTERED COLUMNSTORE INDEX index_name  
    ON { database_name.schema_name.table_name | schema_name.table_name | table_name }  
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ] 
[ ; ]  
  
--Create a nonclustered columnstore index on a disk-based table.  
CREATE [NONCLUSTERED]  COLUMNSTORE INDEX index_name   
    ON { database_name.schema_name.table_name | schema_name.table_name | table_name }
        ( column  [ ,...n ] )  
    [ WHERE <filter_expression> [ AND <filter_expression> ] ]
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]
[ ; ]  
  
<with_option> ::=  
      DROP_EXISTING = { ON | OFF } -- default is OFF  
    | MAXDOP = max_degree_of_parallelism 
    | ONLINE = { ON | OFF } 
    | COMPRESSION_DELAY  = { 0 | delay [ Minutes ] }  
    | DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { partition_number_expression | range } [ ,...n ] ) ]  
  
<on_option>::=  
      partition_scheme_name ( column_name )
    | filegroup_name
    | "default"
  
<filter_expression> ::=  
      column_name IN ( constant [ ,...n ]  
    | column_name { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< } constant  
  
```  
  
```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CLUSTERED COLUMNSTORE INDEX index_name
    ON { database_name.schema_name.table_name | schema_name.table_name | table_name } 
    [ORDER (column [,...n] ) ]  
    [ WITH ( DROP_EXISTING = { ON | OFF } ) ] --default is OFF  
[;]  

```
## <a name="arguments"></a>인수  

일부 옵션은 모든 데이터베이스 엔진 버전에서 사용하지 못할 수 있습니다. 다음 표에서는 CLUSTERED COLUMNSTORE 및 NONCLUSTERED COLUMNSTORE 인덱스에 옵션이 도입된 버전을 보여 줍니다.

|옵션| CLUSTERED | NONCLUSTERED |
|---|---|---|
| COMPRESSION_DELAY | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] |
| DATA_COMPRESSION | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] | 
| ONLINE | [!INCLUDE[ssSQLv15_md](../../includes/sssqlv15-md.md)] | [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] |
| WHERE 절 | 해당 사항 없음 | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] |

모든 옵션을 Azure SQL Database에서 사용할 수 있습니다.

### <a name="create-clustered-columnstore-index"></a>CREATE CLUSTERED COLUMNSTORE INDEX

모든 데이터가 압축되고 열로 저장되는 클러스터형 columnstore 인덱스를 만듭니다. 인덱스에 테이블의 모든 열이 포함되고 전체 테이블이 저장됩니다. 기존 테이블이 힙 또는 클러스터형 인덱스인 경우 테이블이 클러스터형 columnstore 인덱스로 변환됩니다. 테이블이 클러스터형 columnstore 인덱스로 이미 저장된 경우 기존 인덱스가 삭제되고 다시 작성됩니다.  
  
*index_name*  
새 인덱스에 대한 이름을 지정합니다.  
  
테이블에 클러스터형 columnstore 인덱스가 이미 있다면 같은 이름을 기존 인덱스로 지정하거나 DROP EXISTING 옵션을 사용하여 새 이름을 지정할 수 있습니다.  
  
ON [*database_name*. [*schema_name* ] . | *schema_name* . ] *table_name*

클러스터형 columnstore 인덱스로 저장할 테이블의 한, 두 또는 세 부분으로 이루어진 이름을 지정합니다. 테이블이 힙 또는 클러스터형 인덱스인 경우 테이블이 rowstore에서 columnstore로 변환됩니다. 테이블이 이미 columnstore인 경우 이 명령문은 클러스터형 columnstore 인덱스를 다시 작성합니다. 순서가 지정된 클러스터형 열 저장소 인덱스로 변환하려면 기존 인덱스가 클러스터형 columnstore 인덱스여야 합니다.
  
#### <a name="with-options"></a>WITH 옵션

##### <a name="drop_existing--off--on"></a>DROP_EXISTING = [OFF] | ON

   `DROP_EXISTING = ON`은 기존 인덱스를 삭제하고 새로운 columnstore 인덱스를 생성하도록 지정합니다.  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH (DROP_EXISTING = ON);
```
   기본값인 DROP_EXISTING = OFF는 인덱스 이름이 기존 이름과 동일할 것으로 예상합니다. 지정된 인덱스 이름이 이미 존재하는 경우 오류가 발생합니다.  
  
##### <a name="maxdop--max_degree_of_parallelism"></a>MAXDOP = *max_degree_of_parallelism*  
   인덱스 작업 기간 동안 기존의 최대 병렬 처리 수준 서버 구성을 재정의합니다. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
   *max_degree_of_parallelism* 값은 다음 중 하나일 수 있습니다.  
   - 1 - 병렬 계획이 생성되지 않습니다.  
   - \>1 - 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 현재 시스템 작업에 따라 지정된 수 또는 더 적은 수로 제한합니다. 예를 들어, MAXDOP = 4인 경우 사용되는 프로세서 수는 4개 이하가 됩니다.  
   - 0(기본값) - 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH (MAXDOP = 2);
```

   자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 및 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
 
###### <a name="compression_delay--0--delay--minutes-"></a>COMPRESSION_DELAY = **0** | *delay* [ Minutes ]  
   디스크 기반 테이블의 경우 *지연*은 CLOSED 상태의 델타 rowgroup이 SQL Server에서 압축된 rowgroup으로 압축할 수 있게 될 때까지 델타 rowgroup에 남아 있어야 하는 최소 분 수를 지정합니다. 디스크 기반 테이블은 개별 행에 대한 삽입 및 업데이트 시간을 추적하지 않으므로 SQL Server가 CLOSED 상태의 델타 rowgroup에 지연을 적용합니다.  
   기본값은 0분입니다.  
   
```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH ( COMPRESSION_DELAY = 10 Minutes );
```

   COMPRESSION_DELAY 사용 시기에 관한 권장 사항은 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)을 참조하세요.  
  
##### <a name="data_compression--columnstore--columnstore_archive"></a>DATA_COMPRESSION = COLUMNSTORE | COLUMNSTORE_ARCHIVE  
   지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.   
- `COLUMNSTORE`는 기본값이고 성능이 가장 우수한 columnstore 압축으로 압축하도록 지정합니다. 이는 일반적인 선택입니다.  
- `COLUMNSTORE_ARCHIVE`는 테이블 또는 파티션을 보다 작은 크기로 더욱 압축합니다. 이 옵션을 스토리지 크기를 줄여야 하고 스토리지 및 검색에 더 많은 시간을 이용할 수 있는 보관 상황에 사용합니다.  
  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH ( DATA_COMPRESSION = COLUMNSTORE_ARCHIVE );
```
   압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  

###### <a name="online--on--off"></a>ONLINE = [ON | OFF]
- `ON`은 인덱스 새 복사본이 작성되는 동안 columnstore 인덱스가 온라인 상태를 유지하고 있으며 사용할 수 있음을 지정합니다.
- `OFF`는 새 사본이 작성되는 동안 인덱스를 사용할 수 없도록 지정합니다.

```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
       WITH ( ONLINE = ON );
```

#### <a name="on-options"></a>ON 옵션 
   ON 옵션으로 파티션 구성표, 특정 파일 그룹, 기본 파일 그룹 등의 데이터 스토리지 옵션을 지정할 수 있습니다. ON 옵션을 지정하지 않으면 기존 테이블의 파일 그룹 설정이나 설정 파티션이 인덱스에 사용됩니다.  
  
   *partition_scheme_name* **(** _column_name_ **)**  
   테이블의 파티션 구성표를 지정합니다. 파티션 구성표가 데이터베이스에 이미 있어야 합니다. 파티션 구성표를 만들려면 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)을 참조하세요.  
 
   *column_name*은 분할된 인덱스가 분할되는 기준으로 사용할 열을 지정합니다. 이 열은 *partition_scheme_name*에서 사용하는 파티션 함수의 인수와 데이터 형식, 길이 및 전체 자릿수가 일치해야 합니다.  

   *filegroup_name*  
   클러스터형 columnstore 인덱스를 저장할 파일 그룹을 지정합니다. 지정된 위치가 없고 테이블이 분할되지 않은 경우 인덱스는 기본 테이블 또는 뷰와 동일한 파일 그룹을 사용합니다. 파일 그룹은 이미 존재해야 합니다.  

   **"** default **"**  
   기본 파일 그룹에 인덱스를 만들려면 "default" 또는 [ default ]를 사용합니다.  
  
   "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. QUOTED_IDENTIFIER는 기본적으로 ON입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
### <a name="create-nonclustered-columnstore-index"></a>CREATE [NONCLUSTERED] COLUMNSTORE INDEX  
힙 또는 클러스터형 인덱스로 저장된 rowstore 테이블에 메모리 내 비 클러스터형 columnstore 인덱스를 만듭니다. 인덱스는 필터링된 조건을 가질 수 있으며 기본 테이블의 모든 열을 포함할 필요가 없습니다. Columnstore 인덱스에 데이터 복사본을 저장할 충분한 공간이 필요합니다. 업데이트가 가능하며 기본 테이블이 변경될 때 업데이트됩니다. 클러스터형 인덱스에 대한 비 클러스터형 columnstore 인덱스는 실시간 분석이 가능합니다.  
  
*index_name*  
   인덱스의 이름을 지정합니다. *index_name*은 테이블에서 고유해야 하지만 데이터베이스에서 고유할 필요는 없습니다. 인덱스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.  
  
 **(** _column_  [ **,** ...*n* ] **)**  
    저장할 열을 지정합니다. 비클러스터형 columnstore 인덱스는 1024개 열로 제한됩니다.  
   각 열은 columnstore 인덱스에 대해 지원되는 데이터 형식이어야 합니다. 지원되는 데이터 형식 목록은 [제한 사항](../../t-sql/statements/create-columnstore-index-transact-sql.md#LimitRest)을 참조하세요.  

ON [*database_name*. [*schema_name* ] . | *schema_name* . ] *table_name*  
   인덱스를 포함할 테이블의 1, 2 또는 3 부분 이름을 지정합니다.  

#### <a name="with-options"></a>WITH 옵션
##### <a name="drop_existing--off--on"></a>DROP_EXISTING = [OFF] | ON  
   DROP_EXISTING = ON 기존 인덱스가 삭제되고 다시 작성됩니다. 지정된 인덱스 이름은 현재 존재하는 인덱스 이름과 같아야 합니다. 그러나 인덱스 정의는 수정할 수 있습니다. 예를 들어, 다른 열 또는 인덱스 옵션을 지정할 수 있습니다.
  
   DROP_EXISTING = OFF 지정된 인덱스 이름이 이미 존재하는 경우 오류가 표시됩니다. 인덱스 유형은 DROP_EXISTING을 사용하여 변경할 수 없습니다. 이전 버전과 호환되는 구문에서 WITH DROP_EXISTING은 WITH DROP_EXISTING = ON과 같습니다.  

###### <a name="maxdop--max_degree_of_parallelism"></a>MAXDOP = *max_degree_of_parallelism*  
   인덱스 작업 기간 동안 [max degree of parallelism 서버 구성 옵션 ](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 구성 옵션을 재정의합니다. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
   *max_degree_of_parallelism* 값은 다음 중 하나일 수 있습니다.  
   - 1 - 병렬 계획이 생성되지 않습니다.  
   - \>1 - 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 현재 시스템 작업에 따라 지정된 수 또는 더 적은 수로 제한합니다. 예를 들어, MAXDOP = 4인 경우 사용되는 프로세서 수는 4개 이하가 됩니다.  
   - 0(기본값) - 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
   자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]
>  병렬 인덱스 작업은 일부 [!INCLUDE[msC](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
###### <a name="online--on--off"></a>ONLINE = [ON | OFF]   
- `ON`은 인덱스 새 복사본이 작성되는 동안 columnstore 인덱스가 온라인 상태를 유지하고 있으며 사용할 수 있음을 지정합니다.
- `OFF`는 새 사본이 작성되는 동안 인덱스를 사용할 수 없도록 지정합니다. 비 클러스터형 인덱스에서 기본 테이블은 사용 가능하게 그대로 유지되고 비 클러스터형 columnstore 인덱스는 새 인덱스가 완료될 때까지 쿼리를 충족시키는 데 사용되지 않습니다. 

```sql
CREATE COLUMNSTORE INDEX ncci ON Sales.OrderLines (StockItemID, Quantity, UnitPrice, TaxRate) WITH ( ONLINE = ON );
```

##### <a name="compression_delay--0--delayminutes"></a>COMPRESSION_DELAY = **0** | \<delay>[Minutes]  
   압축된 rowgroup으로 마이그레이션할 수 있기 전에 행이 델타 rowgroup에 얼마나 남아 있어야 하는지 하한을 지정합니다. 예를 들어, 고객은 한 행이 120분 동안 변경되지 않은 경우 열 형식 스토리지 형식으로 압축하기에 적합하다고 말할 수 있습니다. 디스크 기반 테이블의 columnstore 인덱스인 경우 행을 삽입하거나 업데이트할 때 시간을 추적하지 않고, 델타 rowgroup 닫힌 시간을 행에 대한 프록시로 대신 사용합니다. 기본 기간은 0분입니다. 델타 rowgroup에 백만 개의 행이 누적되면 행이 열 형식 스토리지에 마이그레이션되고 닫힌 것으로 표시됩니다.  
  
###### <a name="data_compression"></a>DATA_COMPRESSION  
   지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. 다음과 같은 옵션이 있습니다.
   
- `COLUMNSTORE` - 기본값이고 성능이 가장 우수한 columnstore 압축으로 압축하도록 지정합니다. 이는 일반적인 선택입니다.  
- `COLUMNSTORE_ARCHIVE` - COLUMNSTORE_ARCHIVE는 테이블 또는 파티션을 보다 작은 크기로 더욱 압축합니다. 보다 적은 스토리지 크기가 필요한 기타 상황에서 보관하는 데 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
##### <a name="where-filter_expression--and-filter_expression-"></a>WHERE \<filter_expression> [ AND \<filter_expression> ]
  
   필터 조건자라고 하며 인덱스에 어떤 열을 포함할지 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 필터링된 인덱스의 데이터 행에 대한 필터링된 통계를 만듭니다.  
  
   필터 조건자는 간단한 비교 논리를 사용합니다. 비교 연산자에는 NULL 리터럴을 사용한 비교를 사용할 수 없습니다. 대신 IS NULL 및 IS NOT NULL 연산자를 사용합니다.  
  
   다음은 `Production.BillOfMaterials` 테이블에 대한 필터 조건자의 몇 가지 예입니다.  
   `WHERE StartDate > '20000101' AND EndDate <= '20000630'`    
   `WHERE ComponentID IN (533, 324, 753)`  
   `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
   
   필터링된 인덱스에 대한 지침은 [필터링된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md)를 참조하세요.  
  
#### <a name="on-options"></a>ON 옵션  
   이러한 옵션은 인덱스를 만들 파일 그룹을 지정합니다.  
  
*partition_scheme_name* **(** _column_name_ **)**  
   분할된 인덱스의 파티션이 매핑될 파일 그룹을 정의하는 파티션 구성표를 지정합니다. 파티션 구성표는 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)을 실행하여 데이터베이스 내에 포함해야 합니다. 
   *column_name*은 분할된 인덱스가 분할되는 기준으로 사용할 열을 지정합니다. 이 열은 *partition_scheme_name*에서 사용하는 파티션 함수의 인수와 데이터 형식, 길이 및 전체 자릿수가 일치해야 합니다. *column_name*은 인덱스 정의의 열만 사용할 필요는 없으며 columnstore 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 인덱스의 열이 아직 지정되지 않은 경우 분할 열을 인덱스의 열로 추가합니다.  
   *partition_scheme_name* 또는 *filegroup*이 지정되지 않고 테이블이 분할된 경우 인덱스는 동일한 분할 열을 사용하여 동일한 파티션 구성표에 기본 테이블로 배치됩니다.  
   분할된 테이블의 Columnstore 인덱스는 파티션 정렬됩니다.  
   분할된 인덱스에 대한 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.  

*filegroup_name*  
   인덱스를 만들 파일 그룹 이름을 지정합니다. *filegroup_name*이 지정되지 않고 테이블이 분할되지 않은 경우 인덱스는 기본 테이블과 동일한 파일 그룹을 사용합니다. 파일 그룹은 이미 존재해야 합니다.  
 
**"** default **"**  
기본 파일 그룹에 지정된 인덱스를 만듭니다.  
  
이 컨텍스트에서 default는 키워드가 아닙니다. 이것은 기본 파일 그룹에 대한 식별자이며 ON **"** default **"** 또는 ON **[** default **]** 와 같이 구분되어야 합니다. "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
##  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="GenRemarks"></a> 일반적인 주의 사항  
임시 테이블에 대한 columnstore 인덱스를 만들 수 있습니다. 테이블이 삭제되거나 세션이 종료되면 인덱스도 삭제됩니다.  

정렬된 클러스터형 columnstore 인덱스는 문자열 열을 제외하고 Azure SQL Data Warehouse에서 지원되는 모든 데이터 형식의 열에서 만들 수 있습니다.  
 
## <a name="filtered-indexes"></a>필터링된 인덱스  
필터링된 인덱스는 테이블에서 적은 비율의 행을 선택하는 쿼리에 적합한 최적화된 비클러스터형 인덱스입니다. 이 인덱스에서는 필터 조건자를 사용하여 테이블의 일부 데이터를 인덱싱합니다. 잘 디자인된 필터링된 인덱스는 쿼리 성능을 개선하고 스토리지 비용과 유지 관리 비용을 줄일 수 있습니다.  
  
### <a name="required-set-options-for-filtered-indexes"></a>필터링된 인덱스에 필요한 SET 옵션  
다음 조건이 발생할 때마다 필요한 값 열에 SET 옵션을 사용해야 합니다.  
- 필터링된 인덱스를 만듭니다.  
- INSERT, UPDATE, DELETE 또는 MERGE 작업으로 필터링된 인덱스의 데이터를 수정합니다.  
- 필터링된 인덱스는 쿼리 최적화 프로그램이 쿼리 계획을 작성할 때 사용됩니다.  
  
    |Set 옵션|필요한 값|기본 서버 값|Default<br /><br /> OLE DB 및 ODBC 값|Default<br /><br /> DB-Library 값|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|   
  
     *데이터베이스 호환성 수준이 90 이상으로 설정된 경우 ANSI_WARNINGS를 ON으로 설정하면 암시적으로 ARITHABORT가 ON으로 설정됩니다. 데이터베이스 호환성 수준이 80 이하로 설정된 경우에는 명시적으로 ARITHABORT 옵션을 ON으로 설정해야 합니다.  
  
 SET 옵션이 올바르지 않은 경우 다음 조건이 발생할 수 있습니다.  
  
-   필터링된 인덱스가 만들어지지 않습니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 오류를 생성하고 인덱스의 데이터를 변경하는 INSERT, UPDATE, DELETE 또는 MERGE 문을 롤백합니다.  
  
-   쿼리 최적화 프로그램에서 Transact-SQL 문의 실행 계획에 있는 인덱스를 고려하지 않습니다.  
  
 필터링된 인덱스에 대한 자세한 내용은 [필터링된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md)를 참조하세요. 
  
##  <a name="LimitRest"></a> 제한 사항  

**columnstore 인덱스의 각 열은 다음 일반적인 비즈니스 데이터 형식 중 하나여야 합니다.** 
-   datetimeoffset [ ( *n* ) ]  
-   datetime2 [ ( *n* ) ]  
-   DATETIME  
-   smalldatetime  
-   날짜  
-   time [ ( *n* ) ]  
-   float [ ( *n* ) ]  
-   real [ ( *n* ) ]  
-   decimal [ ( *precision* [ *, scale* ] **)** ]
-   numeric [ ( *precision* [ *, scale* ] **)** ]    
-   money  
-   SMALLMONEY  
-   BIGINT  
-   int  
-   SMALLINT  
-   TINYINT  
-   bit  
-   nvarchar [ ( *n* ) ] 
-   nvarchar(max) ([!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 프리미엄 계층, 표준 계층(S3 이상) 및 모든 VCore 제품 계층에 적용됨, 클러스터형 columnstore 인덱스에서만)   
-   nchar [ ( *n* ) ]  
-   varchar [ ( *n* ) ]  
-   varchar(max) ([!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 프리미엄 계층, 표준 계층(S3 이상) 및 모든 VCore 제품 계층에 적용됨, 클러스터형 columnstore 인덱스에서만)
-   char [ ( *n* ) ]  
-   varbinary [ ( *n* ) ] 
-   varbinary(max) ([!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 프리미엄 계층, 표준 계층(S3 이상)에서 Azure SQL Database 및 모든 VCore 제품 계층에 적용됨, 클러스터형 columnstore 인덱스에서만)
-   binary [ ( *n* ) ]  
-   uniqueidentifier([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상에 적용됨)
  
기본 테이블에 columnstore 인덱스에 대해 지원되지 않는 데이터 형식의 열이 있는 경우 비클러스터형 columnstore 인덱스에서 해당 열을 빼야 합니다.  
  
**다음 데이터 형식을 사용하는 열은 columnstore 인덱스에 포함할 수 없습니다.**
-   ntext, text 및 image  
-   nvarchar (max), varchar (max) 및 varbinary (max) ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 포함 이전 버전 및 비클러스터형 columnstore 인덱스에 적용) 
-   rowversion(및 timestamp)  
-   sql_variant  
-   CLR 유형(hierarchyid 및 공간 형식)  
-   xml  
-   uniqueidentifier([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 적용)  

**비클러스터형 columnstore 인덱스:**
-   최대 1,024개의 열만 사용할 수 있습니다.
-   제약 조건 기반 인덱스로 만들 수 없습니다. columnstore 인덱스가 있는 테이블에 고유한 제약 조건, 기본 키 제약 조건 또는 외래 키 제약 조건을 가질 수 없습니다. 제약 조건은 항상 행 저장소 인덱스에서 적용됩니다. 제약 조건은 columnstore(클러스터형 또는 비클러스터형) 인덱스에서 적용될 수 없습니다.
-   스파스 열을 포함할 수 없습니다.  
-   **ALTER INDEX** 문을 사용하여 변경할 수 없습니다. 비클러스터형 인덱스를 변경하려면 인덱스를 삭제하고 해당 columnstore 인덱스를 대신 다시 만들어야 합니다. **ALTER INDEX**를 사용하여 columnstore 인덱스를 해제하고 다시 만들 수 있습니다.  
-   **INCLUDE** 키워드를 사용하여 만들 수 없습니다.  
-   인덱스를 정렬하기 위해 **ASC** 또는 **DESC** 키워드를 포함할 수 없습니다. columnstore 인덱스는 압축 알고리즘에 따라 정렬됩니다. 정렬을 사용하면 성능상의 많은 이점이 없어집니다.  
-   비클러스터형 열 저장소 인덱스에는 nvarchar(max), varchar(max) 및 varbinary(max) 형식의 LOB(대형 개체) 열을 포함할 수 없습니다. 클러스터형 columnstore 인덱스 만이 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 버전부터 LOB 형식 및 프리미엄 계층, 표준 계층(S3 이상)에서 구성된 Azure SQL Database 및 모든 VCore 제품 계층을 지원합니다. 참고: 이전 버전에서는 클러스터형 및 비클러스터형 columnstore 인덱스에서 LOB 형식을 지원하지 않습니다.


> [!NOTE]  
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 인덱싱 된 뷰에서 비클러스터형 columnstore 인덱스를 만들 수 있습니다.  


 **columnstore 인덱스는 다음 기능과 함께 사용할 수 없습니다.**  
-   계산 열 SQL Server 2017부터는 클러스터형 columnstore 인덱스에 비지속형 계산 열을 포함할 수 있습니다. 그러나 SQL Server 2017에서는 클러스터형 columnstore 인덱스에 지속형 계산 열을 포함할 수 없으며 계산 열에 비클러스터형 인덱스를 만들 수 없습니다. 
-   페이지 및 행 압축과 **vardecimal** 스토리지 형식(columnstore 인덱스가 이미 다른 형식으로 압축되어 있음)  
-   복제  
-   Filestream

클러스터형 columnstore 인덱스가 있는 테이블에서는 커서 또는 트리거를 사용할 수 없습니다. 비클러스터형 columnstore 인덱스에는 이러한 제한이 적용되지 않습니다. 즉 비클러스터형 columnstore 인덱스가 있는 테이블에서는 커서 및 트리거를 사용할 수 있습니다.

**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 특정 제한 사항**  
이러한 제한 사항은 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에만 적용됩니다. 이 릴리스에서는 업데이트 가능한 클러스터형 columnstore 인덱스를 사용했습니다. 비클러스터형 columnstore 인덱스는 여전히 읽기 전용이었습니다.  

-   변경 내용 추적 columnstore 인덱스에는 변경 내용 추적을 사용할 수 없습니다.  
-   변경 데이터 캡처 읽기 전용인 NCCI(비클러스터형 columnstore 인덱스)에 대해 변경 데이터 캡처를 사용할 수 없습니다. CCI(클러스터형 columnstore 인덱스)에서 작동합니다.  
-   읽기용 보조 Always OnReadable 가용성 그룹의 읽기 가능한 보조에서 CCI(클러스터형 columnstore 인덱스)에 액세스할 수 없습니다.  읽기 가능한 보조에서 NCCI(비클러스터형 columnstore 인덱스)에 액세스할 수 있습니다.  
-   MARS(Multiple Active Result Sets) [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]는 MARS를 사용하여 columnstore 인덱스가 있는 테이블에 대한 읽기 전용 연결을 합니다. 그러나 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]는 columnstore 인덱스가 있는 테이블에서 동시 DML(데이터 조작 언어) 작업에는 MARS를 지원하지 않습니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 연결을 종료하고 트랜잭션을 중단합니다.  
-  비클러스터형 columnstore 인덱스는 뷰 또는 인덱싱된 뷰에서 만들 수 없습니다.
  
 columnstore 인덱스의 성능상 이점 및 제한 사항에 대한 자세한 내용은 [Columnstore 인덱스 개요](../../relational-databases/indexes/columnstore-indexes-overview.md)를 참조하세요.
  
##  <a name="Metadata"></a> 메타데이터  
 columnstore 인덱스에 있는 모든 열이 메타데이터에 포괄 열로 저장됩니다. columnstore 인덱스에는 키 열이 없습니다. 이들 시스템 뷰는 columnstore 인덱스에 대한 정보를 제공합니다.  
  
-   [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
-   [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
-   [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
-   [sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
-   [sys.column_store_dictionaries&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  

##  <a name="convert"></a>Rowstore 테이블을 columnstore로 변환하는 예제  
  
### <a name="a-convert-a-heap-to-a-clustered-columnstore-index"></a>1\. 클러스터형 columnstore 인덱스로 힙 변환  
 이 예에서는 테이블을 힙으로 만들고 이를 cci_Simple라는 클러스터형 columnstore 인덱스로 변환합니다. 이렇게 하면 전체 테이블의 스토리지가 rowstore에서 columnstore로 변경됩니다.  
  
```sql  
CREATE TABLE SimpleTable(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_Simple ON SimpleTable;  
GO  
```  
  
### <a name="b-convert-a-clustered-index-to-a-clustered-columnstore-index-with-the-same-name"></a>2\. 클러스터형 인덱스를 같은 이름의 클러스터형 columnstore 인덱스로 변환합니다.  
 이 예에서는 클러스터형 인덱스가 있는 테이블을 만든 후 클러스터형 인덱스를 클러스터형 columnstore 인덱스로 변환하는 구문을 보여 줍니다. 이렇게 하면 전체 테이블의 스토리지가 rowstore에서 columnstore로 변경됩니다.  
  
```sql  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cl_simple ON SimpleTable  
WITH (DROP_EXISTING = ON);  
GO  
```  
  
### <a name="c-handle-nonclustered-indexes-when-converting-a-rowstore-table-to-a-columnstore-index"></a>C. rowstore 테이블을 columnstore 인덱스로 변환할 때 비클러스터형 인덱스를 처리합니다.  
 이 예에서는 rowstore 테이블을 columnstore 인덱스로 변환할 때 비클러스터형 인덱스를 처리하는 방법을 보여줍니다. 사실, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 특별한 작업이 필요하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 새로운 클러스터형 columnstore 인덱스에서 비클러스터형 인덱스를 자동으로 정의하고 다시 작성합니다.  
  
 비클러스터형 인덱스를 삭제하려면 columnstore 인덱스를 만들기 전에 DROP INDEX 문을 사용합니다. DROP EXISTING 옵션은 변환중인 클러스터형 인덱스만 삭제합니다. 비클러스터형 인덱스는 삭제하지 않습니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 columnstore 인덱스에 비클러스터형 인덱스를 만들 수 없습니다. 이 예에서는 columnstore 인덱스을 만들기 전에 이전 릴리스에서 어떻게 비클러스터형 인덱스를 삭제해야 하는지 보여줍니다.  
  
```sql  
--Create the table for use with this example.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
  
--Create two nonclustered indexes for use with this example  
CREATE INDEX nc1_simple ON SimpleTable (OrderDateKey);  
CREATE INDEX nc2_simple ON SimpleTable (DueDateKey);   
GO  
  
--SQL Server 2012 and SQL Server 2014: you need to drop the nonclustered indexes  
--in order to create the columnstore index.   
  
DROP INDEX SimpleTable.nc1_simple;  
DROP INDEX SimpleTable.nc2_simple;  
  
--Convert the rowstore table to a columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_simple ON SimpleTable;   
GO  
```  
  
### <a name="d-convert-a-large-fact-table-from-rowstore-to-columnstore"></a>D. rowstore에서 columnstore로 큰 팩트 테이블 변환  
 이 예에서는 큰 팩트 테이블을 rowstore 테이블에서 columnstore 테이블로 변환하는 방법을 설명합니다.  
  
 rowstore 테이블을 columnstore 테이블로 변환하려면:  
  
1.  먼저 이 예에서 사용할 작은 테이블을 만듭니다.  
  
    ```sql  
    --Create a rowstore table with a clustered index and a nonclustered index.  
    CREATE TABLE MyFactTable (  
        ProductKey [int] NOT NULL,  
        OrderDateKey [int] NOT NULL,  
         DueDateKey [int] NOT NULL,  
         ShipDateKey [int] NOT NULL )  
    )  
    WITH (  
        CLUSTERED INDEX ( ProductKey )  
    );  
  
    --Add a nonclustered index.  
    CREATE INDEX my_index ON MyFactTable ( ProductKey, OrderDateKey );  
    ```  
  
2.  rowstore 테이블에서 모든 비클러스터형 인덱스를 삭제합니다.  
  
    ```sql  
    --Drop all nonclustered indexes  
    DROP INDEX my_index ON MyFactTable;  
    ```  
  
3.  클러스터형 인덱스를 삭제합니다.  
  
    -   클러스터형 columnstore 인덱스로 변환할 때 인덱스에 새 이름을 지정하려는 경우 이 작업을 수행합니다. 클러스터형 인덱스를 삭제하지 않으면 새 클러스터형 columnstore 인덱스에 동일한 이름이 지정됩니다.  
  
        > [!NOTE]  
        > 고유의 이름을 사용하면 인덱스 이름을 더 쉽게 기억할 수 있습니다. 모든 rowstore 클러스터형 인덱스는 'ClusteredIndex_\<GUID>'라는 기본 이름을 사용합니다.  
  
    ```sql  
    --Process for dropping a clustered index.  
    --First, look up the name of the clustered rowstore index.  
    --Clustered rowstore indexes always use the DEFAULT name 'ClusteredIndex_<GUID>'.  
    SELECT i.name   
    FROM sys.indexes i   
    JOIN sys.tables t  
    ON ( i.type_desc = 'CLUSTERED' ) WHERE t.name = 'MyFactTable';  
  
    --Drop the clustered rowstore index.  
    DROP INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09 ON MyDimTable;  
    ```  
  
4.  rowstore 테이블을 클러스터형 columnstore 인덱스가 있는 columnstore 테이블로 변환합니다.  
  
    ```sql  
    --Option 1: Convert to columnstore and name the new clustered columnstore index MyCCI.  
    CREATE CLUSTERED COLUMNSTORE INDEX MyCCI ON MyFactTable;  
  
    --Option 2: Convert to columnstore and use the rowstore clustered   
    --index name for the columnstore clustered index name.  
    --First, look up the name of the clustered rowstore index.  
    SELECT i.name   
    FROM sys.indexes i  
    JOIN sys.tables t   
    ON ( i.type_desc = 'CLUSTERED' )  
    WHERE t.name = 'MyFactTable';  
  
    --Second, create the clustered columnstore index and   
    --Replace ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    --with the name of your clustered index.  
    CREATE CLUSTERED COLUMNSTORE INDEX   
    ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
     ON MyFactTable  
    WITH DROP_EXISTING = ON;  
    ```  
  
### <a name="e-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>E. columnstore 테이블을 클러스터형 인덱스가 있는 rowstore 테이블로 변환  
 columnstore 테이블을 클러스터형 인덱스가 있는 rowstore 테이블로 변환하려면 CREATE INDEX 문을 DROP_EXISTING 옵션과 함께 사용합니다.  
  
```sql  
CREATE CLUSTERED INDEX ci_MyTable   
ON MyFactTable  
WITH ( DROP EXISTING = ON );  
```  
  
### <a name="f-convert-a-columnstore-table-to-a-rowstore-heap"></a>F. columnstore 테이블을 rowstore 힙으로 변환  
 columnstore 테이블을 rowstore 힙으로 변환하려면 간단히 클러스터형 columnstore 인덱스를 삭제하면 됩니다.  
  
```sql  
DROP INDEX MyCCI   
ON MyFactTable;  
```  
  

### <a name="g-defragment-by-rebuilding-the-entire-clustered-columnstore-index"></a>G. 전체 클러스터형 columnstore 인덱스를 다시 빌드하여 조각 모음  
   적용 대상: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 두 가지 방법으로 전체 클러스터형 columnstore 인덱스를 다시 작성할 수 있습니다. CREATE CLUSTERED COLUMNSTORE INDEX 또는 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)와 REBUILD 옵션을 사용할 수 있습니다. 두 방법 모두 동일한 결과를 얻을 수 있습니다.  
  
> [!NOTE]  
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 이 예에서 설명된 방법을 사용하여 다시 작성하는 대신에 `ALTER INDEX...REORGANIZE`를 사용합니다.  
  
```sql  
--Determine the Clustered Columnstore Index name of MyDimTable.  
SELECT i.object_id, i.name, t.object_id, t.name   
FROM sys.indexes i   
JOIN sys.tables t  
ON (i.type_desc = 'CLUSTERED COLUMNSTORE')  
WHERE t.name = 'RowstoreDimTable';  
  
--Rebuild the entire index by using CREATE CLUSTERED INDEX.  
CREATE CLUSTERED COLUMNSTORE INDEX my_CCI   
ON MyFactTable  
WITH ( DROP_EXISTING = ON );  
  
--Rebuild the entire index by using ALTER INDEX and the REBUILD option.  
ALTER INDEX my_CCI  
ON MyFactTable  
REBUILD PARTITION = ALL  
WITH ( DROP_EXISTING = ON );  
```  
  
##  <a name="nonclustered"></a> 비클러스터형 columnstore 인덱스 사용  
  
### <a name="a-create-a-columnstore-index-as-a-secondary-index-on-a-rowstore-table"></a>1\. Rowstore 테이블에서 columnstore 인덱스를 보조 인덱스로 만들기  
 이 예에서는 rowstore 테이블에 비클러스터형 columnstore 인덱스를 만듭니다. 이 경우 columnstore 인덱스는 하나만 만들 수 있습니다. Columnstore 인덱스는 rowstore 테이블에 데이터 복사본을 포함하고 있으므로 추가 스토리지가 필요합니다. 이 예에서는 간단한 테이블 및 클러스터형 인덱스를 만든 다음, 비클러스터형 columnstore 인덱스를 만드는 구문을 보여 줍니다.  
  
```sql  
CREATE TABLE SimpleTable  
(ProductKey [int] NOT NULL,   
OrderDateKey [int] NOT NULL,   
DueDateKey [int] NOT NULL,   
ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey);  
GO  
```  
  
### <a name="b-create-a-simple-nonclustered-columnstore-index-using-all-options"></a>2\. 모든 옵션을 사용하여 단순 비클러스터형 columnstore 인덱스 만들기  
 다음 예에서는 모든 옵션을 사용하여 비클러스터형 columnstore 인덱스를 만드는 구문을 보여 줍니다.  
  
```sql  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey)  
WITH (DROP_EXISTING =  ON,   
    MAXDOP = 2)  
ON "default"  
GO  
```  
  
 분할된 테이블을 사용하는 전체 예를 보려면 [Columnstore 인덱스 개요](../../relational-databases/indexes/columnstore-indexes-overview.md)를 참조합니다.  
  
### <a name="c-create-a-nonclustered-columnstore-index-with-a-filtered-predicate"></a>C. 필터링된 조건자를 사용하여 비클러스터형 columnstore 인덱스 만들기  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 Production.BillOfMaterials 테이블에 필터링된 비클러스터형 columnstore 인덱스를 만듭니다. 필터 조건자는 필터링된 인덱스에 키 열이 아닌 열을 포함할 수 있습니다. 이 예에서 조건자는 EndDate가 NULL이 아닌 행만 선택합니다.  
  
```sql  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithEndDate'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
```  
  
###  <a name="ncDML"></a> 4. 비클러스터형 Columnstore 인덱스의 데이터 변경  
   적용 대상: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]까지
  
 테이블에 비클러스터형 columnstore 인덱스를 만든 후에는 해당 테이블에서 데이터를 직접 수정할 수 없습니다. INSERT, UPDATE, DELETE 또는 MERGE를 사용한 쿼리는 실패하며 오류 메시지를 반환합니다. 테이블에서 데이터를 추가하거나 수정하려면 다음 중 하나를 수행합니다.  
  
-   columnstore 인덱스를 사용하지 않도록 설정하거나 삭제합니다. 그런 다음 테이블에서 데이터를 업데이트할 수 있습니다. columnstore 인덱스를 사용하지 않도록 설정하는 경우 데이터 업데이트를 완료할 때 columnstore 인덱스를 다시 작성할 수 있습니다. 예:  
  
    ```sql  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   columnstore 인덱스가 없는 준비 테이블에 데이터를 로드합니다. 준비 테이블에서 columnstore 인덱스를 작성합니다. 준비 테이블을 주 테이블의 빈 파티션으로 전환합니다.  
  
-   columnstore 인덱스가 있는 테이블에서 빈 준비 테이블로 파티션을 전환합니다. 준비 테이블에 columnstore 인덱스가 있는 경우 columnstore 인덱스를 사용하지 않도록 설정합니다. 업데이트를 수행합니다. columnstore 인덱스를 작성 또는 다시 작성합니다. 준비 테이블을 주 테이블의 파티션(현재 비어 있음)으로 다시 전환합니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-change-a-clustered-index-to-a-clustered-columnstore-index"></a>1\. 클러스터형 인덱스를 클러스터형 columnstore 인덱스로 변환합니다.  
 DROP_EXISTING = ON과 함께 CREATE CLUSTERED COLUMNSTORE INDEX 문을 사용하면 다음을 수행할 수 있습니다.  
  
-   클러스터형 인덱스를 클러스터형 columnstore 인덱스로 변환합니다.  
  
-   클러스터형 Columnstore 인덱스 다시 작성  
  
 이 예에서는 xDimProduct 테이블을 클러스터형 인덱스가 있는 rowstore 테이블로 만든 다음, CREATE CLUSTERED COLUMNSTORE INDEX를 사용하여 테이블을 rowstore 테이블에서 columnstore 테이블로 변경합니다.  
  
```sql  
-- Uses AdventureWorks  
  
IF EXISTS (SELECT name FROM sys.tables  
    WHERE name = N'xDimProduct'  
    AND object_id = OBJECT_ID (N'xDimProduct'))  
DROP TABLE xDimProduct;  
  
--Create a distributed table with a clustered index.  
CREATE TABLE xDimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey)  
WITH ( DISTRIBUTION = HASH(ProductKey),  
    CLUSTERED INDEX (ProductKey) )  
AS SELECT ProductKey, ProductAlternateKey, ProductSubcategoryKey FROM DimProduct;  
  
--Change the existing clustered index   
--to a clustered columnstore index with the same name.  
--Look up the name of the index before running this statement.  
CREATE CLUSTERED COLUMNSTORE INDEX <index_name>   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="b-rebuild-a-clustered-columnstore-index"></a>2\. 클러스터형 Columnstore 인덱스 다시 작성  
 앞의 예를 기반으로 이 예에서는 CREATE CLUSTERED COLUMNSTORE INDEX를 사용하여 cci_xDimProduct라는 기존 클러스터형 columnstore 인덱스를 다시 작성합니다.  
  
```sql  
--Rebuild the existing clustered columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_xDimProduct   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="c-change-the-name-of-a-clustered-columnstore-index"></a>C. 클러스터형 Columnstore 인덱스의 이름 바꾸기  
 클러스터형 columnstore 인덱스의 이름을 변경하려면 기존 클러스터형 columnstore 인덱스를 삭제한 다음, 새 이름으로 인덱스를 다시 만듭니다.  
  
 작은 테이블 또는 빈 테이블에서만 이 작업을 수행하는 것이 좋습니다. 대규모 클러스터형 columnstore 인덱스을 삭제하고 다른 이름으로 다시 작성하려면 시간이 오래 걸립니다.  
  
 이전 예제에서의 cci_xDimProduct 클러스터형 columnstore 인덱스를 사용하여 이 예제는 cci_xDimProduct 클러스터형 columnstore 인덱스를 삭제한 다음, mycci_xDimProduct라는 이름으로 클러스터형 columnstore 인덱스를 다시 생성합니다.  
  
```sql  
--For illustration purposes, drop the clustered columnstore index.   
--The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xDimProduct;  
  
--Create a clustered index with a new name, mycci_xDimProduct.  
CREATE CLUSTERED COLUMNSTORE INDEX mycci_xDimProduct  
ON xdimProduct  
WITH ( DROP_EXISTING = OFF );  
```  
  
### <a name="d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>D. columnstore 테이블을 클러스터형 인덱스가 있는 rowstore 테이블로 변환  
 클러스터형 columnstore 인덱스를 삭제하고 클러스터형 인덱스를 만들고자 하는 상황이 있을 수도 있습니다. 이렇게 하면 테이블을 rowstore 형식으로 저장합니다. 이 예에서는 columnstore 테이블을 클러스터형 인덱스가 있는 같은 이름의 rowstore 테이블로 변환합니다. 데이터가 손실되지 않습니다. 모든 데이터는 rowstore 테이블로 이동하고 나열된 열은 클러스터형 인덱스에서 키 열이 됩니다.  
  
```sql  
--Drop the clustered columnstore index and create a clustered rowstore index.   
--All of the columns are stored in the rowstore clustered index.   
--The columns listed are the included columns in the index.  
CREATE CLUSTERED INDEX cci_xDimProduct    
ON xdimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey, WeightUnitMeasureCode)  
WITH ( DROP_EXISTING = ON);  
```  
  
### <a name="e-convert-a-columnstore-table-back-to-a-rowstore-heap"></a>E. columnstore 테이블을 rowstore 힙으로 변환  
 클러스터형 columnstore 인덱스를 삭제하고 테이블을 rowstore 힙으로 변환하려면 [DROP INDEX(SQL Server PDW)](drop-index-transact-sql.md)를 사용합니다. 이 예에서는 cci_xDimProduct 테이블을 rowstore 힙으로 변환합니다. 테이블은 계속 배포되지만 힙으로 저장됩니다.  
  
```sql  
--Drop the clustered columnstore index. The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xdimProduct;  
```  

### <a name="f-create-an-ordered-clustered-columnstore-index-on-a-table-with-no-index"></a>F. 인덱스가 없는 테이블에 순서가 지정된 클러스터형 columnstore 인덱스 만들기

```sql
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
ORDER ( SHIPDATE );
```

### <a name="g-convert-a-clustered-columnstore-index-to-an-ordered-clustered-columnstore-index"></a>G. 클러스터형 columnstore 인덱스를 순서가 지정된 클러스터형 columnstore 인덱스로 변환

```sql  
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
ORDER ( SHIPDATE );
WITH (DROP_EXISTING = ON)
```

### <a name="h-add-a-column-to-the-ordering-of-an-ordered-clustered-columnstore-index"></a>H. 순서가 지정된 클러스터형 columnstore 인덱스의 순서에 열 추가

```sql
-- The original ordered clustered columnstore index was ordered on SHIPDATE column only.  Add PRODUCTKEY column to the ordering.
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
ORDER ( SHIPDATE, PRODUCTKEY );
WITH (DROP_EXISTING = ON)
```
### <a name="i-change-the-ordinal-of-ordered-columns"></a>9\. 정렬된 열의 서수 변경  
```sql
-- The original ordered clustered columnstore index was ordered on SHIPDATE, PRODUCTKEY.  Change the ordering to PRODUCTKEY, SHIPDATE.  
CREATE CLUSTERED COLUMNSTORE INDEX cci ON Sales.OrderLines
ORDER ( PRODUCTKEY,SHIPDATE );
WITH (DROP_EXISTING = ON)
```


