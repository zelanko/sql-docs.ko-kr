---
title: CREATE COLUMNSTORE INDEX (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 76
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: a4e3b602b026d359c7eac492fc44480d4b1a18a9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---

# <a name="create-columnstore-index-transact-sql"></a>CREATE COLUMNSTORE INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

비클러스터형된 columnstore 인덱스를 만들거나 rowstore 테이블을 클러스터형된 columnstore 인덱스로 변환 합니다. OLTP 워크 로드에서 실시간 운영 분석을 효율적으로 실행 하거나 데이터 웨어하우징 작업에 대 한 데이터 압축 및 쿼리 성능 향상을 위해 columnstore 인덱스를 사용 합니다.  
  
> [!NOTE]  
>  부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], 테이블을 클러스터형된 columnstore 인덱스로 만들 수 있습니다.   먼저 rowstore 테이블을 생성 한 다음 클러스터형된 columnstore 인덱스로 변환 하는 데 필요한 파일이 없습니다.  
  
예제를 건너뜁니다.  
-   [Rowstore 테이블을 columnstore로 변환 하기 위한 예제](../../t-sql/statements/create-columnstore-index-transact-sql.md#convert)  
-   [비클러스터형 columnstore 인덱스에 대 한 예제](../../t-sql/statements/create-columnstore-index-transact-sql.md#nonclustered)  
  
다음 시나리오로 이동:  
-   [실시간 운영 분석에 Columnstore 인덱스](/sql-docs/docs/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics)  
-   [데이터 웨어하우스 용 Columnstore 인덱스](/sql-docs/docs/relational-databases/indexes/columnstore-indexes-data-warehouse)  
  
더 알아보세요:  
-   [Columnstore 인덱스 가이드](/sql-docs/docs/relational-databases/indexes/columnstore-indexes-overview)  
-   [Columnstore 인덱스 기능 요약](/sql-docs/docs/relational-databases/indexes/columnstore-indexes-what-s-new)  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create a clustered columnstore index on disk-based table.  
CREATE CLUSTERED COLUMNSTORE INDEX index_name  
    ON [database_name. [schema_name ] . | schema_name . ] table_name  
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]  
[ ; ]  
  
--Create a non-clustered columnstore index on a disk-based table.  
CREATE [NONCLUSTERED]  COLUMNSTORE INDEX index_name   
    ON [database_name. [schema_name ] . | schema_name . ] table_name   
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
    ON [ database_name . [ schema_name ] . | schema_name . ] table_name  
    [ WITH ( DROP_EXISTING = { ON | OFF } ) ] --default is OFF  
[;]  
```  
  
## <a name="arguments"></a>인수  
CREATE CLUSTERED COLUMNSTORE INDEX  
모든 데이터가 압축 되며 되 열에 저장 클러스터형된 columnstore 인덱스를 만듭니다. 인덱스에 테이블의 모든 열이 포함되고 전체 테이블이 저장됩니다. 기존 테이블이 힙 또는 클러스터형된 인덱스 경우 테이블을 클러스터형된 columnstore 인덱스로 변환 합니다. 테이블을 클러스터형된 columnstore 인덱스로 이미 저장 된 기존 인덱스를 삭제 하 고 다시 작성 합니다.  
  
*index_name*  
새 인덱스에 대 한 이름을 지정합니다.  
  
테이블에 클러스터형된 columnstore 인덱스가 이미 있으면 기존 인덱스와 같은 이름을 지정할 수 있습니다 또는 DROP EXISTING 옵션을 사용 하 여 새 이름을 지정 합니다.  
  
ON [*database_name*합니다. [*schema_name* ]. | *schema_name* 합니다. ] *table_name*  
   클러스터형 columnstore 인덱스로 저장할 테이블의 한, 두 또는 세 부분으로 이루어진 이름을 지정합니다. 테이블이 힙인 경우 클러스터형된 인덱스는 테이블은 rowstore에서 columnstore로 변환 됩니다. 테이블을 columnstore 이미 있으면이 문은 클러스터형된 columnstore 인덱스 다시 작성 합니다.  
  
의 모든 멘션을  
DROP_EXISTING = [OFF] | ON  
   DROP_EXISTING = ON이 기존 클러스터형된 columnstore 인덱스를 삭제 하 고 새 columnstore 인덱스를 만들 지정 합니다.  

   기본적으로 DROP_EXISTING = OFF에서는 인덱스 이름이 기존 이름과 동일 합니다. 지정 된 인덱스 이름이 이미 있습니다.이 오류가 발생 합니다.  
  
MAXDOP = *max_degree_of_parallelism*  
   인덱스 작업 기간 동안 기존의 최대 병렬 처리 수준 서버 구성을 재정의합니다. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
   *max_degree_of_parallelism* 값 될 수 있습니다.  
   - 1 - 병렬 계획이 생성되지 않습니다.  
   - \>1-지정된 된 수 이하로 현재 시스템 작업에 따라 병렬 인덱스 작업에 사용 되는 프로세서의 최대 수를 제한 합니다. 예를 들어, MAXDOP = 4, 사용 되는 프로세서 수가 4 개 이하가 됩니다.  
   - 0(기본값) - 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
   자세한 내용은 참조 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md), 및 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)합니다.  
 
COMPRESSION_DELAY = **0** | *지연* [분]  
   적용 대상: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.

   디스크 기반 테이블에 대 한 *지연* SQL Server는 압축 된 행 그룹으로 압축할 수 전에 델타 행 그룹에 델타 행 그룹을 CLOSED 상태에서 유지 되어야 하는 시간 (분)의 최소 수를 지정 합니다. 디스크 기반 테이블에서 insert를 관리 하 고 업데이트할 하지 이후 시간에 개별 행을 SQL Server에 적용 됩니다 지연 CLOSED 상태에서 델타 행 그룹입니다.  
   기본값은 0 분입니다.  
   COMPRESSION_DELAY를 사용 하는 경우에 대 한 권장 사항은 참조 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)합니다.  
  
DATA_COMPRESSION = COLUMNSTORE | COLUMNSTORE_ARCHIVE  
   적용 대상: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.
지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.   
COLUMNSTORE  
   COLUMNSTORE는 기본 템플릿이 고 대부분 고성능 columnstore 압축으로 압축 하도록 지정 합니다. 이 일반적인 좋습니다.  
  
COLUMNSTORE_ARCHIVE  
   COLUMNSTORE_ARCHIVE 추가 테이블 또는 파티션이 더 작은 크기로 압축합니다. 와 같은 경우이 옵션을 사용 보관 하는 저장소 크기를 줄여야 및 저장과 검색에 더 많은 시간을 수용할 수 있습니다.  
  
   압축에 대 한 자세한 내용은 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  

ON  
   ON 옵션으로 파티션 구성표, 특정 파일 그룹, 기본 파일 그룹 등의 데이터 저장소 옵션을 지정할 수 있습니다. ON 옵션을 지정 하지 않으면 인덱스는 기존 테이블의 설정을 파티션 또는 파일 그룹 설정을 사용 합니다.  
  
   *partition_scheme_name* **(** *column_name* **)**  
   테이블의 파티션 구성표를 지정합니다. 파티션 구성표가 데이터베이스에 이미 있어야 합니다. 파티션 구성표를 만들려면 참조 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)합니다.  
 
   *column_name* 분할된 된 인덱스는 분할 된 열을 지정 합니다. 이 열에는 데이터 형식, 길이, 일치 해야 하 고는 함수에 파티션의 전체 자릿수가 *partition_scheme_name* 사용 합니다.  

   *filegroup_name*  
   클러스터형 columnstore 인덱스를 저장할 파일 그룹을 지정합니다. 지정된 위치가 없고 테이블이 분할되지 않은 경우 인덱스는 기본 테이블 또는 뷰와 동일한 파일 그룹을 사용합니다. 파일 그룹은 이미 존재해야 합니다.  

   **"**기본**"**  
   기본 파일 그룹에 인덱스를 만들려면 "default" 또는 [default]를 사용 합니다.  
  
   "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. QUOTED_IDENTIFIER는 기본적으로 ON입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
[비클러스터형] COLUMNSTORE 인덱스 만들기  
Rowstore 테이블에 비클러스터형 columnstore 인덱스를 만들 힙 또는 클러스터형된 인덱스를 저장 합니다. 인덱스 필터링된 된 조건을 가질 수 있습니다 및 모든 기본 테이블의 열을 포함할 필요가 없습니다. Columnstore 인덱스에는 데이터의 복사본을 저장할 충분 한 공간이 필요 합니다. 업데이트 가능 하 고 기본 테이블이 변경 될 때 업데이트 됩니다. 클러스터 된 인덱스에서 비클러스터형 columnstore 인덱스에는 실시간 분석을 지원 합니다.  
  
*index_name*  
   인덱스의 이름을 지정합니다. *index_name* 테이블 내에서 고유 해야 하지만 데이터베이스 내에서 고유할 필요가 없습니다. 인덱스 이름은의 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 **(** *열* [ **,**... *n* ] **)**  
    저장할 열을 지정합니다. 비클러스터형 columnstore 인덱스는 1024 개의 열으로 제한 합니다.  
   각 열은 columnstore 인덱스에 대해 지원되는 데이터 형식이어야 합니다. 참조 [제한 사항](../../t-sql/statements/create-columnstore-index-transact-sql.md#LimitRest) 목록은 지원 되는 데이터 형식입니다.  

ON [*database_name*합니다. [*schema_name* ]. | *schema_name* 합니다. ] *table_name*  
   1 개, 2 개 또는 세 부분으로 인덱스를 포함 하는 테이블의 이름을 지정 합니다.  

WITH DROP_EXISTING = [OFF] | ON  
   DROP_EXISTING = ON 기존 인덱스를 삭제 하 고 다시 작성 합니다. 지정된 인덱스 이름은 현재 존재하는 인덱스 이름과 같아야 합니다. 그러나 인덱스 정의는 수정할 수 있습니다. 예를 들어, 다른 열 또는 인덱스 옵션을 지정할 수 있습니다.
  
   DROP_EXISTING = OFF를 지정 된 인덱스 이름이 이미 있는 경우 오류가 표시 됩니다. 인덱스 유형은 DROP_EXISTING을 사용하여 변경할 수 없습니다. 이전 버전과 호환되는 구문에서 WITH DROP_EXISTING은 WITH DROP_EXISTING = ON과 같습니다.  

MAXDOP = *max_degree_of_parallelism*  
   재정의 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 인덱스 작업의 기간에 대 한 구성 옵션입니다. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
   *max_degree_of_parallelism* 값 될 수 있습니다.  
   - 1 - 병렬 계획이 생성되지 않습니다.  
   - \>1-지정된 된 수 이하로 현재 시스템 작업에 따라 병렬 인덱스 작업에 사용 되는 프로세서의 최대 수를 제한 합니다. 예를 들어, MAXDOP = 4, 사용 되는 프로세서 수가 4 개 이하가 됩니다.  
   - 0(기본값) - 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
   자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]  
>  병렬 인덱스 작업의 일부 버전에서 사용할 수 없는 [!INCLUDE[msC](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
ONLINE = [ON | OFF]   
   적용 대상: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]만 비클러스터형 columnstore 인덱스에 있습니다.
비클러스터형 columnstore 인덱스를 온라인 상태로 유지 하 고 인덱스의 새 복사본 동안 사용할 수 있는 빌드되는 ON을 지정 합니다.

   OFF 새 복사본은 만드는 동안 인덱스를 사용 하기 위해 사용할 수 있는지를 지정 합니다. 이것은 비클러스터형 인덱스 에서만, 기본 테이블은 유지를 사용할 수 있는 새 인덱스 완료 될 때까지 쿼리를 충족 하는 비클러스터형 columnstore 인덱스가 사용 되지 않습니다. 

COMPRESSION_DELAY = **0** | \<지연 > [분]  
   적용 대상: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다. 
  
   시간 행에에서 보관 해야 델타 행 그룹이 압축 된 행 그룹으로 마이그레이션할 수 있기 전에에 배열은 하 한을 지정 합니다. 예를 들어 고객 120 분에 대 한 행이 변경 되지 않았으면 만들어 주는 열 형식 저장소 형식으로 압축에 대 한 적격 말할 수 있습니다. 디스크 기반 테이블에서 columnstore 인덱스에 대 한 행이 삽입 되거나 업데이트 된 시간을 추적 하지 않습니다 म म 델타 행 그룹이 닫힌 시간 프록시로 행 대신 사용 합니다. 기본 시간은 0 분입니다. 행은 델타 행 그룹에 1 백만 행이 누적 않은 고 닫힌으로 표시 된 열 형식 저장소로 마이그레이션됩니다.  
  
DATA_COMPRESSION  
   지정된 테이블, 파티션 번호 또는 파티션 범위에 대한 데이터 압축 옵션을 지정합니다. 다음과 같은 옵션이 있습니다.  
COLUMNSTORE  
   적용 대상: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다. 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE는 기본 템플릿이 고 대부분 고성능 columnstore 압축으로 압축 하도록 지정 합니다. 이 일반적인 좋습니다.  
  
COLUMNSTORE_ARCHIVE  
   적용 대상: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.
클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스를 모두 포함하는 columnstore 인덱스에만 적용됩니다. COLUMNSTORE_ARCHIVE 추가 테이블 또는 파티션이 더 작은 크기로 압축합니다. 보다 적은 저장소 크기가 필요한 기타 상황에서 보관하는 데 사용할 수 있으며 저장 및 검색에 더 많은 시간을 이용할 수 있습니다.  
  
 압축에 대 한 자세한 내용은 참조 [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
여기서 \<filter_expression > [AND \<filter_expression >]에 적용: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.
  
   이 인덱스에 포함할 행을 지정 필터 조건자를 호출 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]필터링된 된 인덱스에 데이터 행에 대 한 필터링 된 통계를 만듭니다.  
  
   필터 조건자는 간단한 비교 논리를 사용합니다. 비교 연산자에는 NULL 리터럴을 사용한 비교를 사용할 수 없습니다. 대신 IS NULL 및 IS NOT NULL 연산자를 사용합니다.  
  
   다음은 `Production.BillOfMaterials` 테이블에 대한 필터 조건자의 몇 가지 예입니다.  
   `WHERE StartDate > '20000101' AND EndDate <= '20000630'`    
   `WHERE ComponentID IN (533, 324, 753)`  
   `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
   
   필터링 된 인덱스에 대 한 지침을 참조 하십시오. [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)합니다.  
  
ON  
   이러한 옵션 인덱스가 만들어질 파일 그룹을 지정 합니다.  
  
*partition_scheme_name* **(** *column_name* **)**  
   분할된 된 인덱스의 파티션이 매핑되는 파일 그룹을 정의 하는 파티션 구성표를 지정 합니다. 실행 하 여 파티션 구성표는 데이터베이스 내에 있어야 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)합니다. 
   *column_name* 분할된 된 인덱스는 분할 된 열을 지정 합니다. 이 열에는 데이터 형식, 길이, 일치 해야 하 고는 함수에 파티션의 전체 자릿수가 *partition_scheme_name* 사용 합니다. *column_name* 인덱스 정의의 열에 제한 되지 않습니다. columnstore 인덱스를 분할하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 인덱스의 열이 아직 지정되지 않은 경우 분할 열을 인덱스의 열로 추가합니다.  
   경우 *partition_scheme_name* 또는 *파일 그룹* 지정 하지 않으면 테이블이 분할 된 하 고, 동일한 분할 열을 사용 하 여 기본 테이블과 동일한 파티션 구성표에 인덱스가 있습니다.  
   분할된 테이블의 Columnstore 인덱스는 파티션 정렬됩니다.  
   인덱스를 분할 하는 방법에 대 한 자세한 내용은 참조 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)합니다.  

*filegroup_name*  
   인덱스를 만들 파일 그룹 이름을 지정합니다. 경우 *filegroup_name* 지정 하지 않으면 테이블이 분할 되지 않은 경우, 인덱스는 기본 테이블과 동일한 파일 그룹을 사용 하 고 있습니다. 파일 그룹은 이미 존재해야 합니다.  
 
**"**기본**"**  
기본 파일 그룹에 지정된 인덱스를 만듭니다.  
  
이 컨텍스트에서 default는 키워드가 아닙니다. 기본 파일 그룹에 대 한 식별자 이며 ON 같이 구분 되어야 합니다 **"**기본**"** 또는 ON **[**기본**]**합니다. "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
##  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="GenRemarks"></a>일반적인 주의 사항  
 임시 테이블에 columnstore 인덱스를 만들 수 있습니다. 테이블이 삭제되거나 세션이 종료되면 인덱스도 삭제됩니다.  
 
## <a name="filtered-indexes"></a>필터링된 인덱스  
필터링된 인덱스는 테이블에서 적은 비율의 행을 선택하는 쿼리에 적합한 최적화된 비클러스터형 인덱스입니다. 이 인덱스에서는 필터 조건자를 사용하여 테이블의 일부 데이터를 인덱싱합니다. 잘 디자인된 필터링된 인덱스는 쿼리 성능을 개선하고 저장소 비용과 유지 관리 비용을 줄일 수 있습니다.  
  
### <a name="required-set-options-for-filtered-indexes"></a>필터링된 인덱스에 필요한 SET 옵션  
다음 조건이 발생할 때마다 필요한 값 열에 SET 옵션을 사용해야 합니다.  
- 필터링된 인덱스를 만듭니다.  
- INSERT, UPDATE, DELETE 또는 MERGE 작업으로 필터링된 인덱스의 데이터를 수정합니다.  
- 필터링 된 인덱스는 쿼리 최적화 프로그램에서 쿼리 계획을 생성 하기 위해 사용 됩니다.  
  
    |Set 옵션|필요한 값|기본 서버 값|기본값<br /><br /> OLE DB 및 ODBC 값|기본값<br /><br /> DB-Library 값|  
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
  
 필터링 된 인덱스에 대 한 자세한 내용은 참조 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)합니다. 
  
##  <a name="LimitRest"></a> 제한 사항  

**Columnstore 인덱스의 각 열은 다음과 같은 일반적인 비즈니스 데이터 형식 중 하나 여야 합니다.** 
-   datetimeoffset [( * n * )]  
-   datetime2 [( * n * )]  
-   datetime  
-   smalldatetime  
-   date  
-   시간 [( * n * )]  
-   float [( * n * )]  
-   실제 [( * n * )]  
-   10 진수 [( *정밀도* [ *, 배율* ] **)** ]
-   숫자 [( *정밀도* [ *, 배율* ] **)** ]    
-   money  
-   smallmoney  
-   bigint  
-   int  
-   smallint  
-   tinyint  
-   bit  
-   nvarchar [( * n * )] 
-   nvarchar (max) (적용할 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 클러스터형된 columnstore 인덱스에만에서 가격 책정 계층을 premium Azure SQL 데이터베이스)   
-   nchar [( * n * )]  
-   varchar [( * n * )]  
-   varchar (max) (적용할 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 클러스터형된 columnstore 인덱스에만에서 가격 책정 계층을 premium Azure SQL 데이터베이스)
-   char [( * n * )]  
-   varbinary [( * n * )] 
-   varbinary (max) (적용할 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 클러스터형된 columnstore 인덱스에만에서 가격 책정 계층을 premium Azure SQL 데이터베이스)
-   이진 [( * n * )]  
-   고유 식별자 (적용할 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상)
  
기본 테이블에 columnstore 인덱스에 대해 지원 되지 않는 데이터 형식의 열을 비클러스터형 columnstore 인덱스에서 해당 열을 생략 해야 합니다.  
  
**다음 데이터 형식 중 하나를 사용 하는 열은 columnstore 인덱스에 포함할 수 없습니다.**
-   ntext, text 및 image  
-   nvarchar (max), varchar (max), 및 varbinary (max) (적용할 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 비클러스터형 columnstore 인덱스 및 이전 버전) 
-   rowversion(및 timestamp)  
-   sql_variant  
-   CLR 유형(hierarchyid 및 공간 형식)  
-   xml  
-   고유 식별자 (적용할 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  

**비클러스터형 columnstore 인덱스:**
-   최대 1,024개의 열만 사용할 수 있습니다.  
-   비클러스터형 columnstore 인덱스가 있는 테이블은 UNIQUE 제약 조건, PRIMARY KEY 제약 조건 또는 FOREIGN KEY 제약 조건을 가질 수 있지만 비클러스터형 columnstore 인덱스에 제약 조건을 포함할 수 없습니다.  
-   뷰 또는 인덱싱된 뷰에서는 만들 수 없습니다.  
-   스파스 열을 포함할 수 없습니다.  
-   사용 하 여 변경할 수 없습니다는 **ALTER INDEX** 문. 비클러스터형 인덱스를 변경하려면 인덱스를 삭제하고 해당 columnstore 인덱스를 대신 다시 만들어야 합니다. 사용할 수 있습니다 **ALTER INDEX** 를 사용 하지 않고 columnstore 인덱스 다시 작성 합니다.  
-   사용 하 여 만들 수 없습니다는 **INCLUDE** 키워드입니다.  
-   포함할 수 없습니다는 **ASC** 또는 **DESC** 인덱스를 정렬 하는 것에 대 한 키워드입니다. columnstore 인덱스는 압축 알고리즘에 따라 정렬됩니다. 정렬을 사용하면 성능상의 많은 이점이 없어집니다.  
-   비클러스터형 열 저장소 인덱스의 형식 nvarchar (max), varchar (max), varbinary (max)의 (large object) 열을 포함할 수 없습니다. 클러스터형된 columnstore 인덱스를 LOB 형식을 지원만 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 버전 및 Azure SQL 데이터베이스 프리미엄 가격 책정 계층에서 구성 합니다. Note: 이전 버전 클러스터형 및 비클러스터형 columnstore 인덱스에서 LOB 형식을 지원 하지 않습니다.


 **Columnstore 인덱스는 다음과 같은 기능이 함께 사용할 수 없습니다.**  
-   계산 열 SQL Server 2017 부터는 클러스터형된 columnstore 인덱스는 비지속형 계산된 열을 포함할 수 있습니다. 그러나 SQL Server 2017 년 1에서 클러스터형된 columnstore 인덱스는 지속형된 계산된 열을 포함할 수 없습니다 하며 계산된 열에 생성된 된 비클러스터형된 인덱스 수는 없습니다. 
-   페이지 및 행 압축 및 **vardecimal** 저장소 형식 (columnstore 인덱스를 다른 형식으로 이미 압축 됩니다.)  
-   복제  
-   Filestream

클러스터형된 columnstore 인덱스가 있는 테이블에서 커서 또는 트리거를 사용할 수 없습니다. 비클러스터형 columnstore 인덱스;에이 제한이 적용 되지 않습니다. 비클러스터형 columnstore 인덱스가 있는 테이블에서 커서 및 트리거를 사용할 수 있습니다.

**SQL Server 2014 특정 제한 사항**  
이러한 제한은 SQL Server 2014에만 적용 됩니다. 이 릴리스에서 업데이트 가능한 클러스터형된 columnstore 인덱스를 사용 했습니다. 비클러스터형 columnstore 인덱스는 여전히 읽기 전용 이었습니다.  

-   변경 내용 추적 합니다. 변경 내용 추적는 읽기 전용 비클러스터형 columnstore 인덱스 (NCCI)을 사용할 수 없습니다. 클러스터형된 columnstore 인덱스 (CCI)에 대 한 작동지 않습니다.  
-   변경 데이터 캡처 합니다. 변경 데이터는 읽기 전용 비클러스터형 columnstore 인덱스 (NCCI)에 대 한 캡처를 사용할 수 없습니다. 클러스터형된 columnstore 인덱스 (CCI)에 대 한 작동지 않습니다.  
-   읽기 가능한 보조 복제본입니다. 항상 OnReadable 가용성 그룹의 읽기 가능한 보조 서버에서 클러스터 된 클러스터형된 columnstore 인덱스 CCI ()를 액세스할 수 없습니다.  비클러스터형 columnstore 인덱스 (NCCI)를 읽기 가능한 보조 복제본에서 액세스할 수 있습니다.  
-   Multiple Active Result Sets MARS ()입니다. SQL Server 2014 columnstore 인덱스가 있는 테이블에 대 한 읽기 전용 연결에 MARS를 사용합니다.    그러나 SQL Server 2014는 columnstore 인덱스가 있는 테이블에 동시 데이터 조작 언어 (DML) 작업에 대 한 MARS를 지원 하지 않습니다. 이 경우 SQL Server의 연결을 종료 하 고 트랜잭션을 중단 합니다.  
  
 성능상의 이점 및 columnstore 인덱스의 제한 사항에 대 한 정보를 참조 하십시오. [Columnstore 인덱스 개요](../../relational-databases/indexes/columnstore-indexes-overview.md)합니다.
  
##  <a name="Metadata"></a> 메타데이터  
 columnstore 인덱스에 있는 모든 열이 메타데이터에 포괄 열로 저장됩니다. columnstore 인덱스에는 키 열이 없습니다. 이들 시스템 뷰는 columnstore 인덱스에 대한 정보를 제공합니다.  
  
-   [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
-   [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
-   [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
-   [sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
-   [sys.column_store_dictionaries&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  

##  <a name="convert"></a>Rowstore 테이블을 columnstore로 변환 하기 위한 예제  
  
### <a name="a-convert-a-heap-to-a-clustered-columnstore-index"></a>1. 클러스터형 columnstore 인덱스로 힙 변환  
 이 예에서는 테이블을 힙으로 만들고 이를 cci_Simple라는 클러스터형 columnstore 인덱스로 변환합니다. 이렇게 하면 전체 테이블의 저장소가 rowstore에서 columnstore로 변경됩니다.  
  
```  
CREATE TABLE SimpleTable(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_Simple ON SimpleTable;  
GO  
```  
  
### <a name="b-convert-a-clustered-index-to-a-clustered-columnstore-index-with-the-same-name"></a>2. 클러스터형 인덱스를 같은 이름의 클러스터형 columnstore 인덱스로 변환합니다.  
 이 예에서는 클러스터형 인덱스가 있는 테이블을 만든 후 클러스터형 인덱스를 클러스터형 columnstore 인덱스로 변환하는 구문을 보여 줍니다. 이렇게 하면 전체 테이블의 저장소가 rowstore에서 columnstore로 변경됩니다.  
  
```  
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
  
### <a name="c-handle-nonclustered-indexes-when-converting-a-rowstore-table-to-a-columnstore-index"></a>3. Rowstore 테이블을 columnstore 인덱스로 변환 하는 경우 비클러스터형 인덱스를 처리 합니다.  
 이 예제에는 rowstore 테이블을 columnstore 인덱스로 변환 하는 경우 비클러스터형 인덱스를 처리 하는 방법을 보여 줍니다. 실제로, 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 특별 한 작업이 필요 하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자동으로 정의 하 고 새 클러스터형된 columnstore 인덱스에서 비클러스터형 인덱스가 다시 작성 합니다.  
  
 비클러스터형 인덱스를 삭제 하려는 경우에 columnstore 인덱스를 만들기 전에 DROP INDEX 문을 사용 합니다. DROP EXISTING 옵션만 변환 되는 클러스터형된 인덱스를 삭제 합니다. 비클러스터형 인덱스를 삭제 하지 않습니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], columnstore 인덱스에서 비클러스터형 인덱스를 만들 수 없습니다. 이 예제에서는 어떻게 이전 릴리스에서 필요한 인덱스를 삭제 한 비클러스터형 columnstore 인덱스를 만들기 전에 보여 줍니다.  
  
```  
  
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
  
### <a name="d-convert-a-large-fact-table-from-rowstore-to-columnstore"></a>4. rowstore에서 columnstore로 큰 팩트 테이블 변환  
 이 예에서는 큰 팩트 테이블을 rowstore 테이블에서 columnstore 테이블로 변환하는 방법을 설명합니다.  
  
 rowstore 테이블을 columnstore 테이블로 변환하려면:  
  
1.  먼저 이 예에서 사용할 작은 테이블을 만듭니다.  
  
    ```  
    --Create a rowstore table with a clustered index and a non-clustered index.  
    CREATE TABLE MyFactTable (  
        ProductKey [int] NOT NULL,  
        OrderDateKey [int] NOT NULL,  
         DueDateKey [int] NOT NULL,  
         ShipDateKey [int] NOT NULL )  
    )  
    WITH (  
        CLUSTERED INDEX ( ProductKey )  
    );  
  
    --Add a non-clustered index.  
    CREATE INDEX my_index ON MyFactTable ( ProductKey, OrderDateKey );  
    ```  
  
2.  rowstore 테이블에서 모든 비클러스터형 인덱스를 삭제합니다.  
  
    ```  
    --Drop all non-clustered indexes  
    DROP INDEX my_index ON MyFactTable;  
    ```  
  
3.  클러스터형 인덱스를 삭제합니다.  
  
    -   클러스터형 columnstore 인덱스로 변환할 때 인덱스에 새 이름을 지정하려는 경우 이 작업을 수행합니다. 클러스터형된 인덱스를 삭제 하지 않은 경우 새 클러스터형된 columnstore 인덱스 이름이 동일 합니다.  
  
        > [!NOTE]  
        >  고유의 이름을 사용하면 인덱스 이름을 더 쉽게 기억할 수 있습니다. 모든 rowstore 클러스터형 인덱스는 기본 이름을 사용 하 여 ' ClusteredIndex_\<GUID >'입니다.  
  
    ```  
    --Process for dropping a clustered index.  
    --First, look up the name of the clustered rowstore index.  
    --Clustered rowstore indexes always use the DEFAULT name ‘ClusteredIndex_<GUID>’.  
    SELECT i.name   
    FROM sys.indexes i   
    JOIN sys.tables t  
    ON ( i.type_desc = 'CLUSTERED' ) WHERE t.name = 'MyFactTable';  
  
    --Drop the clustered rowstore index.  
    DROP INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09 ON MyDimTable;  
    ```  
  
4.  rowstore 테이블을 클러스터형 columnstore 인덱스가 있는 columnstore 테이블로 변환합니다.  
  
    ```  
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
  
### <a name="e-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>5. columnstore 테이블을 클러스터형 인덱스가 있는 rowstore 테이블로 변환  
 columnstore 테이블을 클러스터형 인덱스가 있는 rowstore 테이블로 변환하려면 CREATE INDEX 문을 DROP_EXISTING 옵션과 함께 사용합니다.  
  
```  
CREATE CLUSTERED INDEX ci_MyTable   
ON MyFactTable  
WITH ( DROP EXISTING = ON );  
```  
  
### <a name="f-convert-a-columnstore-table-to-a-rowstore-heap"></a>6. columnstore 테이블을 rowstore 힙으로 변환  
 columnstore 테이블을 rowstore 힙으로 변환하려면 간단히 클러스터형 columnstore 인덱스를 삭제하면 됩니다.  
  
```  
DROP INDEX MyCCI   
ON MyFactTable;  
```  
  

### <a name="g-defragment-by-rebuilding-the-entire-clustered-columnstore-index"></a>7. 전체 클러스터형된 columnstore 인덱스를 다시 작성 하 여 조각 모음  
   적용 대상: SQL Server 2014  
  
 두 가지 방법으로 전체 클러스터형 columnstore 인덱스를 다시 작성할 수 있습니다. CREATE CLUSTERED COLUMNSTORE INDEX를 사용할 수 있습니다 또는 [ALTER index&#40; Transact SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md) 와 REBUILD 옵션입니다. 두 방법 모두 동일한 결과를 얻을 수 있습니다.  
  
> [!NOTE]  
>  SQL Server 2016 부터는이 예에 설명 된 방법을 사용 하 여 다시 작성 하지 않고 ALTER INDEX REORGANIZE를 사용 합니다.  
  
```  
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
  
##  <a name="nonclustered"></a>비클러스터형 columnstore 인덱스에 대 한 예제  
  
### <a name="a-create-a-columnstore-index-as-a-secondary-index-on-a-rowstore-table"></a>1. Rowstore 테이블에서 보조 인덱스와 columnstore 인덱스 만들기  
 이 예제는 rowstore 테이블에 비클러스터형 columnstore 인덱스를 만듭니다. 이 경우 columnstore 인덱스는 하나만 만들 수 있습니다. Columnstore 인덱스는 rowstore 테이블의 데이터의 복사본이 포함 되어 있으므로 추가 저장소가 필요 합니다. 이 예제에서는 간단한 테이블 및 클러스터형된 인덱스를 만들고 비클러스터형된 columnstore 인덱스를 만드는 구문을 보여 줍니다.  
  
```  
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
  
### <a name="b-create-a-simple-nonclustered-columnstore-index-using-all-options"></a>2. 모든 옵션을 사용 하 여 단순 비클러스터형 columnstore 인덱스 만들기  
 다음 예에서는 모든 옵션을 사용하여 비클러스터형 columnstore 인덱스를 만드는 구문을 보여 줍니다.  
  
```  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey)  
WITH (DROP_EXISTING =  ON,   
    MAXDOP = 2)  
ON "default"  
GO  
```  
  
 분할 된 테이블을 사용 하 여 보다 복잡 한 예제를 보려면 [Columnstore 인덱스 개요](../../relational-databases/indexes/columnstore-indexes-overview.md)합니다.  
  
### <a name="c-create-a-nonclustered-columnstore-index-with-a-filtered-predicate"></a>3. 필터링 된 조건자가 있는 비클러스터형 columnstore 인덱스 만들기  
 다음 예에서는 Production.BillOfMaterials 테이블에 대해 필터링 된 비클러스터형 columnstore 인덱스를 만듭니다는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다. 필터 조건자는 필터링된 인덱스에 키 열이 아닌 열을 포함할 수 있습니다. 이 예에서 조건자는 EndDate가 NULL이 아닌 행만 선택합니다.  
  
```  
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
   적용 대상: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]합니다.
  
 테이블에 비클러스터형 columnstore 인덱스를 만든 후에는 해당 테이블에서 데이터를 직접 수정할 수 없습니다. INSERT, UPDATE, DELETE 또는 MERGE를 사용 하 여 쿼리는 실패 하 고 오류 메시지를 반환 합니다. 테이블에서 데이터를 추가하거나 수정하려면 다음 중 하나를 수행합니다.  
  
-   columnstore 인덱스를 사용하지 않도록 설정하거나 삭제합니다. 그런 다음 테이블에서 데이터를 업데이트할 수 있습니다. columnstore 인덱스를 사용하지 않도록 설정하는 경우 데이터 업데이트를 완료할 때 columnstore 인덱스를 다시 작성할 수 있습니다. 예를 들면 다음과 같습니다.  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   columnstore 인덱스가 없는 준비 테이블에 데이터를 로드합니다. 준비 테이블에서 columnstore 인덱스를 작성합니다. 준비 테이블을 주 테이블의 빈 파티션으로 전환합니다.  
  
-   columnstore 인덱스가 있는 테이블에서 빈 준비 테이블로 파티션을 전환합니다. 준비 테이블에 columnstore 인덱스가 있는 경우 columnstore 인덱스를 사용하지 않도록 설정합니다. 업데이트를 수행합니다. columnstore 인덱스를 작성 또는 다시 작성합니다. 준비 테이블을 주 테이블의 파티션(현재 비어 있음)으로 다시 전환합니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-change-a-clustered-index-to-a-clustered-columnstore-index"></a>1. 클러스터형된 columnstore 인덱스를 클러스터형된 인덱스 변경  
 = ON, CREATE CLUSTERED COLUMNSTORE INDEX 문에 DROP_EXISTING을 사용 하 여 수행할 수 있습니다.  
  
-   클러스터형된 columnstore 인덱스로 클러스터형된 인덱스를 변경 합니다.  
  
-   클러스터형된 columnstore 인덱스 다시 작성 합니다.  
  
 이 예에서는 클러스터형된 인덱스가 있는 rowstore 테이블로 xDimProduct 표를 만들고 클러스터형 COLUMNSTORE 인덱스 만들기를 사용 하 여 테이블을 rowstore 테이블에서 columnstore 테이블로 변경 합니다.  
  
```  
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
  
### <a name="b-rebuild-a-clustered-columnstore-index"></a>2. 클러스터형된 columnstore 인덱스 다시 작성  
 이 예에서는 앞의 예제를 빌드한 cci_xDimProduct 라는 기존 클러스터형된 columnstore 인덱스를 다시 작성 하려면 CREATE CLUSTERED COLUMNSTORE INDEX를 사용 합니다.  
  
```  
--Rebuild the existing clustered columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_xDimProduct   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="c-change-the-name-of-a-clustered-columnstore-index"></a>3. 클러스터형된 columnstore 인덱스의 이름 변경  
 클러스터형된 columnstore 인덱스의 이름을 변경 하려면 기존 클러스터형된 columnstore 인덱스를 삭제 하 고 새 이름으로 인덱스를 다시 만듭니다.  
  
 작은 테이블 또는 빈 테이블으로이 작업을 수행 하는 것이 좋습니다. 대규모 클러스터형된 columnstore 인덱스를 삭제 하 고 다른 이름으로 다시 작성 하는 오랜 시간이 걸립니다.  
  
 이전 예제에서 cci_xDimProduct 클러스터형된 columnstore 인덱스를 사용 하면이 예제에서는 cci_xDimProduct 클러스터형된 columnstore 인덱스를 삭제 하 고 이름 mycci_xDimProduct 사용 하 여 클러스터형된 columnstore 인덱스를 다시 만듭니다.  
  
```  
--For illustration purposes, drop the clustered columnstore index.   
--The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xDimProduct;  
  
--Create a clustered index with a new name, mycci_xDimProduct.  
CREATE CLUSTERED COLUMNSTORE INDEX mycci_xDimProduct  
ON xdimProduct  
WITH ( DROP_EXISTING = OFF );  
```  
  
### <a name="d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>4. columnstore 테이블을 클러스터형 인덱스가 있는 rowstore 테이블로 변환  
 클러스터형된 columnstore 인덱스를 삭제 하 고 클러스터형된 인덱스를 만들 않을 수 있습니다. Rowstore 형식 테이블을 저장 됩니다. 이 예에서는 동일한 이름의 클러스터형된 인덱스가 있는 rowstore 테이블로 columnstore 테이블을 변환합니다. 데이터는 손실 됩니다. Rowstore 테이블에 모든 데이터가 이동 되 고 나열 된 열에 클러스터형된 인덱스의 키 열 됩니다.  
  
```  
--Drop the clustered columnstore index and create a clustered rowstore index.   
--All of the columns are stored in the rowstore clustered index.   
--The columns listed are the included columns in the index.  
CREATE CLUSTERED INDEX cci_xDimProduct    
ON xdimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey, WeightUnitMeasureCode)  
WITH ( DROP_EXISTING = ON);  
  
```  
  
### <a name="e-convert-a-columnstore-table-back-to-a-rowstore-heap"></a>5. Columnstore 테이블을 rowstore 힙으로 다시 변환  
 사용 하 여 [DROP INDEX (SQL Server PDW)](http://msdn.microsoft.com/en-us/f59cab43-9f40-41b4-bfdb-d90e80e9bf32) 클러스터형된 columnstore 인덱스를 삭제 하는 테이블을 rowstore 힙으로 변환 합니다. 이 예에서는 cci_xDimProduct 테이블을 rowstore 힙으로 변환 합니다. 테이블은 계속 배포 될 것으로 서 되지만 힙으로 저장 됩니다.  
  
```  
--Drop the clustered columnstore index. The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xdimProduct;  
```  


