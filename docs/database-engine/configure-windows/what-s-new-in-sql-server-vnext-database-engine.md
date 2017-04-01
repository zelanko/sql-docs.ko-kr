---
title: "SQL Server vNext(데이터베이스 엔진)의 새로운 기능 | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# SQL Server vNext(데이터베이스 엔진)의 새로운 기능
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

**참고**: SQL Server vNext에는 SQL Server 2016 서비스 팩에 추가된 기능도 포함되어 있습니다. 해당 항목에 대해서는 [SQL Server 2016(데이터베이스 엔진)의 새로운 기능](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)을 참조하세요.

## <a name="sql-server-database-engine-ctp-13"></a>SQL Server 데이터베이스 엔진(CTP 1.3)
- 간접 검사점 성능 개선 사항
- 클러스터 없는 가용성 그룹 지원이 추가되었습니다.
- 최소 복제본 커밋 가용성 그룹 설정이 추가되었습니다.
- 이제 가용성 그룹은 Windows-Linux 간에 원활하게 작동되므로 OS 간 마이그레이션 및 테스트가 가능합니다.
- 임시 테이블 보존 정책 지원이 추가되었습니다.
- 새로운 DMV SYS.DM_DB_STATS_HISTOGRAM
- 온라인 비클러스터형 columnstore 인덱스 작성 및 다시 작성 지원이 추가되었습니다.
- Linux 프로세스에 대한 정보를 반환하는&5;개의 새로운 동적 관리 뷰. 자세한 내용은 [Linux 프로세스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)를 참조하세요.   
- [sys.dm_db_stats_histogram(TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)이 통계 검사를 위해 추가되었습니다.

## <a name="sql-server-database-engine-ctp-12"></a>SQL Server 데이터베이스 엔진(CTP 1.2)

- SQL Server Management Studio 버전 16.4와 함께 릴리스된 DTA(데이터베이스 튜닝 관리자)에서는 SQL Server 2016 이상에서 분석을 수행할 때 추가적인 옵션을 제공합니다.    
   - 성능 향상. 자세한 내용은 [DTA(데이터베이스 엔진 튜닝 관리자) 권장 사항을 사용한 성능 향상](../../relational-databases/performance/performance-improvements-using-dta-recommendations.md)을 참조하세요.
   - columnstore 인덱스의 권장 사항을 허용하는 `-fc` 옵션. 자세한 내용은 [DTA 유틸리티](../../tools/dta/dta-utility.md) 및 [DTA(데이터베이스 엔진 튜닝 관리자)의 Columnstore 인덱스 권장 사항](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)을 참조하세요.  
   - DTA에서 쿼리 저장소의 작업을 검토하기 위한 `-iq` 옵션. 자세한 내용은 [쿼리 저장소의 작업을 사용하여 데이터베이스 튜닝](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md)을 참조하세요.
   

## <a name="sql-server-database-engine-ctp-11"></a>SQL Server 데이터베이스 엔진(CTP 1.1)

<a name="InMemoryBulletsCtp11"/>
- 메모리 내 기능의 경우, 메모리 최적화 테이블 및 고유하게 컴파일된 함수에 대한 추가 향상 기능이 그 다음에 나열되고 [후속 텍스트](#InMemory_CodeSamples)에서 코드 샘플을 사용할 수 있습니다.
    - 계산 열의 인덱스를 비롯하여 메모리 액세스에 최적화된 테이블의 계산 열에 대한 지원
    - 고유하게 컴파일된 모듈과 CHECK 제약 조건의 JSON 함수에 대한 전체 지원
    - 고유하게 컴파일된 모듈의 `CROSS APPLY` 연산자   
- 새 문자열 함수 [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md), [TRANSLATE](../../t-sql/functions/translate-transact-sql.md) 및 [TRIM](../../t-sql/functions/trim-transact-sql.md)이 추가되었습니다.   
- [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md) 함수에 대해 이제 `WITHIN GROUP` 절이 지원됩니다.
- 새로운 두 일본어 데이터 정렬 패밀리(Japanese_Bushu_Kakusu_140 및 Japanese_XJIS_140)가 추가되었고, 데이터 정렬 옵션 Variation-selector-sensitive(_VSS)가 일본어 데이터 정렬에서 사용을 위해 추가되었습니다. 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.   
- 새로운 대량 액세스 옵션([BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md))을 통해 CSV 형식으로 지정된 파일의 데이터에 바로 액세스할 수 있으며 새 `BLOB_STORAGE` 옵션인 [EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 통해 Azure Blob Storage에 저장된 파일의 데이터에 바로 액세스할 수 있습니다.


## <a name="sql-server-database-engine-ctp-10"></a>SQL Server 데이터베이스 엔진(CTP 1.0)

- 데이터베이스 **COMPATIBILITY_LEVEL** 140이 추가되었습니다.   이 수준에서 실행하는 고객에게는 최신 언어 기능 및 쿼리 최적화 프로그램 동작이 제공됩니다. 여기에는 Microsoft에서 릴리스하는 각 시험판 버전의 변경 내용이 포함됩니다.
- 증분 통계 업데이트 임계값을 계산하는 방식이 향상되었습니다(140 호환성 모드 필요).
- [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)이 추가되었습니다.
- 메모리 내 테이블에 향상된 여러 가지 성능 및 언어 기능을 추가했습니다.
    - `sp_spaceused`가 메모리 내 테이블에서 지원됩니다.
    - `sp_rename`이 네이티브 모듈에서 지원됩니다.
    - `CASE` 문이 네이티브 모듈에서 지원됩니다.
    - 메모리 내 테이블에서 8개 인덱스 제한이 제거되었습니다.
    - `TOP (N) WITH TIES`가 네이티브 모듈에서 지원됩니다.
    - 메모리 내 테이블에 대해 `ALTER TABLE` 속도가 경우에 따라 상당히 빨라집니다.
    - 메모리 내 테이블 트랜잭션 다시 실행이 병렬로 수행됩니다. 따라서 장애 조치(failover)를 수행하는 시간이 현저하게 줄어들거나 경우에 따라 다시 시작됩니다.
    - 이제 메모리 내 검사점 파일을 Azure Storage에 저장할 수 있습니다. 따라서 이미 이 기능이 있는 LDF 파일에 비해 MDF와 동일한 기능을 제공합니다.
- 클러스터형 Columnstore 인덱스가 LOB 열(nvarchar(max), varchar(max), varbinary(max))을 지원합니다.
- [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md) 집계 함수가 추가되었습니다.  
- 새 권한: 이제 `DATABASE SCOPED CREDENTIAL`은 보안 개체 클래스로서, `CONTROL`, `ALTER`, `REFERENCES`, `TAKE OWNERSHIP`, `VIEW DEFINITION` 권한을 지원합니다. 이제 SQL Database에 한정되는 `ADMINISTER DATABASE BULK OPERATIONS`이 `sys.fn_builtin_permissions`에 표시됩니다.   
- [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) DMV가 추가되어 Windows 및 Linux 둘 다에 대한 운영 체제 정보를 제공합니다.   
- R Services로 데이터베이스 역할을 만들어 패키지와 관련된 권한을 관리합니다. 자세한 내용은 [SQL Server에 대한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)를 참조하세요.
 
<a name="InMemory_CodeSamples"/> 
## <a name="code-samples-for-new-in-memory-enhancements"></a>새로운 메모리 내 향상 기능에 대한 코드 샘플

다음 하위 섹션에서는 이 문서의 이전 텍스트에 글머리 기호로 표시된 새로운 메모리 내 기능을 보여 주는 TRANSACT-SQL 코드 샘플을 제공합니다.

메모리 내 CTP 1.1 글머리 기호 목록은 [여기](#InMemoryBulletsCtp11)에 나와 있습니다.

#### <a name="computed-column-in-a-memory-optimized-table"></a>메모리 최적화 테이블의 계산 열

이 CREATE TABLE 문은 CTP 1.1에 대한 이전 텍스트에 언급된 다음과 같은 기능을 보여 줍니다.

- 열의 JSON CHECK 제약 조건
- 새로운 계산 열
- 계산 열의 인덱스

```tsql
CREATE TABLE Product(
    ProductID  int            PRIMARY KEY NONCLUSTERED,
    Name       nvarchar(400)  NOT NULL,
    Price      float,

    Data      nvarchar(4000)  CONSTRAINT [Data contains JSON]  CHECK (ISJSON(Data)=1),

    MadeIn  AS CAST(JSON_VALUE(Data, '$.MadeIn')            as NVARCHAR(50)) PERSISTED,
    Cost    AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float       ),

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)
)
        WITH (MEMORY_OPTIMIZED=ON);
```

#### <a name="cross-apply-and-json-functions"></a>CROSS APPLY 및 JSON 함수

고유하게 컴파일된 저장 프로시저에 대한 이 CREATE PROCEDURE 문은 CTP 1.1에 대한 이전 텍스트에 언급된 다음과 같은 기능을 보여 줍니다.

- CROSS APPLY 연산자
- JSON 함수

```tsql
CREATE OR ALTER PROCEDURE ProductList()
    WITH SCHEMABINDING, NATIVE_COMPILATION
as begin
    atomic with (transaction isolation level = snapshot,  language = N'English')

    SELECT
            ProductID, Name, Price, Tags,
            Data,
            JSON_VALUE(Data,'$.MadeIn') AS MadeIn,
            value
        FROM Product
        CROSS APPLY OPENJSON(Data, '$.SalesReasons')
        FOR JSON PATH
end;
```
