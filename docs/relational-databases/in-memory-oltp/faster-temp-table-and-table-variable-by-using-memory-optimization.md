---
title: "메모리 최적화를 사용한 더 빠른 임시 테이블 및 테이블 변수 | Microsoft 문서"
ms.custom: 
ms.date: 10/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 38512a22-7e63-436f-9c13-dde7cf5c2202
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 72f4daeb47e7c023e14cdd5a87a51e5dcbee2436
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="faster-temp-table-and-table-variable-by-using-memory-optimization"></a>메모리 최적화를 사용한 더 빠른 임시 테이블 및 테이블 변수
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
임시 테이블, 테이블 변수 또는 테이블 반환 매개 변수를 사용하는 경우 메모리 최적화 테이블 및 테이블 변수를 활용하도록 변환하여 성능을 향상시키는 것이 좋습니다. 코드는 일반적으로 최소로 변경됩니다.  
  
이 문서에서는 다음에 대해 설명합니다.  
  
- 메모리 내로 변환을 위한 시나리오  
- 메모리 내로 변환의 기술 구현 단계  
- 메모리 내로 변환하기 전의 필수 구성 요소  
- 메모리 액세스에 최적화된 성능 이점을 강조하는 코드 샘플
  
  
## <a name="a-basics-of-memory-optimized-table-variables"></a>1. 메모리 최적화 테이블 변수 기본 사항  
  
메모리 최적화 테이블 변수는 메모리 최적화 테이블에서 사용하는 동일한 메모리 최적화 알고리즘 및 데이터 구조를 사용하여 훌륭한 효율성을 제공합니다. 테이블 변수가 고유하게 컴파일된 모듈 내에서 액세스될 때 효율성은 최대가 됩니다.  
  
  
메모리 최적화 테이블 변수:  
  
- 메모리에만 저장되고 디스크에 구성 요소가 없습니다.  
- IO 작업이 관여되지 않습니다.  
- tempdb 사용 또는 경합이 관여되지 않습니다.  
- 저장 프로시저에 TVP(테이블 반환 매개 변수)로 전달될 수 있습니다.  
- 하나 이상의 인덱스(해시 또는 비클러스터형)가 있어야 합니다.  
  - 해시 인덱스의 경우 버킷 수는 예상 고유 인덱스 키 수의 1-2배가 되어야 이상적이지만 버킷 수를 최대 10배까지 고려하는 것이 좋습니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블의 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)를 참조하세요.  

  
  
#### <a name="object-types"></a>개체 유형  
  
메모리 내 OLTP는 메모리 액세스 최적화 임시 테이블 및 테이블 변수에 사용할 수 있는 다음과 같은 개체를 제공합니다.  
  
- 메모리 액세스에 최적화된 테이블  
  - Durability = SCHEMA_ONLY  
- 메모리 액세스에 최적화된 테이블 변수  
  - 인라인 대신 두 단계로 선언해야 합니다.  
    - `CREATE TYPE my_type AS TABLE ...;` 그런 다음  
    - `DECLARE @mytablevariable my_type;`를 참조하세요.  
  
  
## <a name="b-scenario-replace-global-tempdb-x23x23table"></a>2. 시나리오: 전역 tempdb &#x23;&#x23;table 바꾸기  
  
메모리 최적화 SCHEMA_ONLY 테이블이 포함된 전역 임시 테이블을 교체하는 작업은 매우 간단합니다. 런타임 시가 아니라 배포 시 테이블을 만든다는 것이 가장 큰 차이점입니다. 컴파일 시간 최적화로 인해 메모리 최적화 테이블을 만드는 시간은 기존의 테이블을 만드는 것보다 오래 걸립니다. 온라인 워크로드의 일부로 메모리 최적화 테이블을 만들고 삭제하는 작업은 워크로드의 성능뿐만 아니라 AlwaysOn 보조 데이터베이스와 데이터베이스 복구에 대한 다시 실행 성능에도 영향을 미칩니다.

다음과 같은 전역 임시 테이블이 있다고 가정합니다.  
  
  
  
  
    CREATE TABLE ##tempGlobalB  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
  
  
  
  
전역 임시 테이블을 다음과 같이 DURABILITY = SCHEMA_ONLY가 선언된 메모리 최적화 테이블로 바꾸는 것이 좋습니다.  
  
  
  
  
    CREATE TABLE dbo.soGlobalB  
    (  
        Column1   INT   NOT NULL   INDEX ix1 NONCLUSTERED,  
        Column2   NVARCHAR(4000)  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
            DURABILITY        = SCHEMA_ONLY);  
  
  
  
  
#### <a name="b1-steps"></a>B.1 단계  
  
전역 임시 테이블에서 SCHEMA_ONLY로 변환하는 단계는 다음과 같습니다.  
  
  
1. 기존의 모든 디스크상 테이블에서처럼 **dbo.soGlobalB** 테이블을 한 번 만듭니다.  
2. TRANSACT-SQL에서 **&#x23;&#x23;tempGlobalB** 테이블의 생성을 제거합니다.  테이블을 만들면 제공되는 컴파일 오버헤드를 방지하기 위해 런타임 시가 아닌 배포 시 메모리 최적화 테이블을 만드는 것이 중요합니다.
3. T-SQL에서 **&#x23;&#x23;tempGlobalB**의 모든 멘션을 **dbo.soGlobalB**로 바꿉니다.  
  
  
## <a name="c-scenario-replace-session-tempdb-x23table"></a>3. 시나리오: 세션 tempdb &#x23;table 바꾸기  
  
세션 임시 테이블을 바꾸기 위한 준비 작업에는 이전의 전역 임시 테이블 시나리오보다 더 많은 T-SQL이 포함됩니다. 다행히 변환을 수행하는 데에는 추가 T-SQL이 필요하지 않습니다.  

전역 임시 테이블 시나리오에서는 컴파일 오버헤드를 방지하기 위해 런타임 시가 아닌 배포 시 테이블을 만든다는 점이 가장 큰 변화입니다.
  
다음과 같은 세션 임시 테이블이 있다고 가정합니다.  
  
  
  
  
    CREATE TABLE #tempSessionC  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
  
  
  
  
첫째, 다음과 같이 테이블 반환 함수를 만들어 **@@spid**로 필터링합니다. 함수는 세션 임시 테이블에서 변환하는 모든 SCHEMA_ONLY 테이블에서 사용할 수 있습니다.  
  
  
  
  
    CREATE FUNCTION dbo.fn_SpidFilter(@SpidFilter smallint)  
        RETURNS TABLE  
        WITH SCHEMABINDING , NATIVE_COMPILATION  
    AS  
        RETURN  
            SELECT 1 AS fn_SpidFilter  
                WHERE @SpidFilter = @@spid;  
  
  
  
  
둘째, SCHEMA_ONLY 테이블 및 테이블의 보안 정책을 만듭니다.  
  
  
메모리 최적화 각 테이블에는 하나 이상의 인덱스가 있어야 합니다.  
  
- 테이블 dbo.soSessionC의 경우 적절한 BUCKET_COUNT를 계산하는 경우 해시 인덱스가 더 나을 수 있습니다. 하지만 이 예제에서는 비클러스터형 인덱스로 간소화합니다.  
  
  
  
  
    CREATE TABLE dbo.soSessionC  
    (  
        Column1     INT         NOT NULL,  
        Column2     NVARCHAR(4000)  NULL,  
  
        SpidFilter  SMALLINT    NOT NULL   DEFAULT (@@spid),  
  
        INDEX ix_SpidFiler NONCLUSTERED (SpidFilter),  
        --INDEX ix_SpidFilter HASH  
        --    (SpidFilter) WITH (BUCKET_COUNT = 64),  
          
        CONSTRAINT CHK_soSessionC_SpidFilter  
            CHECK ( SpidFilter = @@spid ),  
    ).  
        의 모든 멘션을  
            (MEMORY_OPTIMIZED = ON,  
             DURABILITY = SCHEMA_ONLY);  
    go  
  
  
    CREATE SECURITY POLICY dbo.soSessionC_SpidFilter_Policy  
        ADD FILTER PREDICATE dbo.fn_SpidFilter(SpidFilter)  
        ON dbo.soSessionC  
        WITH (STATE = ON);  
    go  
  
  
  
  
셋째, 일반 T-SQL 코드에서 다음을 수행합니다.  
  
1. 새 메모리 최적화 테이블에 대한 Transact-SQL 문에서 임시 테이블에 대한 모든 참조를 변경합니다.
    - _이전 이름:_ &#x23;tempSessionC  
    - _새 이름:_ dbo.soSessionC  
2. 코드에서 `CREATE TABLE #tempSessionC` 문을 `DELETE FROM dbo.soSessionC`로 바꿔 동일한 session_id로 이전 세션에서 삽입한 테이블 콘텐츠에 세션이 노출되지 않도록 합니다. 테이블을 만들면 제공되는 컴파일 오버헤드를 방지하기 위해 런타임 시가 아닌 배포 시 메모리 최적화 테이블을 만드는 것이 중요합니다.
3. 코드에서 `DROP TABLE #tempSessionC` 문을 제거합니다. 메모리 크기가 잠재적 고려 사항인 경우 필요에 따라 `DELETE FROM dbo.soSessionC` 문을 삽입할 수 있습니다.
  
  
  
  
## <a name="d-scenario-table-variable-can-be-memoryoptimizedon"></a>4. 시나리오: 테이블 변수가 MEMORY_OPTIMIZED=ON일 수 있습니다.  
  
  
기존의 테이블 변수는 tempdb 데이터베이스에서 테이블을 나타냅니다. 훨씬 빠른 성능을 위해 테이블 변수를 메모리 액세스에 최적화할 수 있습니다.  
  
기존의 테이블 변수에 대한 T-SQL은 다음과 같습니다. 해당 범위는 일괄 처리 또는 세션이 끝날 때 종료됩니다.  
  
  
  
  
    DECLARE @tvTableD TABLE  
        ( Column1   INT   NOT NULL ,  
          Column2   CHAR(10) );  
  
  
  
  
#### <a name="d1-convert-inline-to-explicit"></a>D.1 명시적으로 인라인 변환  
  
위의 구문은 테이블 변수가 *인라인*으로 만들어졌습니다. 인라인 구문은 메모리 액세스에 최적화를 지원하지 않습니다. 그러면 인라인 구문을 TYPE의 명시적 구문으로 변환해 보겠습니다.  
  
*범위:* 첫 번째 go로 구분된 일괄 처리에 의해 만들어진 TYPE 정의는 서버를 종료하고 다시 시작한 후에도 유지됩니다. 하지만 첫 번째 go 구분 기호 이후 선언된 테이블 @tvTableC는 다음 go에 도달하고 일괄 처리가 종료될 때까지만 유지됩니다.  
  
  
  
  
    CREATE TYPE dbo.typeTableD  
        AS TABLE  
        (  
            Column1  INT   NOT NULL ,  
            Column2  CHAR(10)  
        );  
    go  
          
    SET NoCount ON;  
    DECLARE @tvTableD dbo.typeTableD  
    ;  
    INSERT INTO @tvTableD (Column1) values (1), (2)  
    ;  
    SELECT * from @tvTableD;  
    go  
  
  
  
  
#### <a name="d2-convert-explicit-on-disk-to-memory-optimized"></a>D.2 메모리 최적화되도록 디스크상 명시적 변환  
  
메모리 최적화 테이블 변수는 tempdb에 상주하지 않습니다. 메모리 액세스 최적화는 종종 속도가 10배 이상 빨라지는 결과를 낳습니다.  
  
메모리 최적화로 변환하는 작업은 한 단계로 구현됩니다. 다음과 같이 추가하여 명시적 TYPE 만들기를 개선합니다.  
  
- 인덱스. 다시 말하지만 메모리 최적화 각 테이블에는 하나 이상의 인덱스가 있어야 합니다.  
- MEMORY_OPTIMIZED = ON.  
  
  
  
  
    CREATE TYPE dbo.typeTableD  
        AS TABLE  
        (  
            Column1  INT   NOT NULL   INDEX ix1,  
            Column2  CHAR(10)  
        ).  
        의 모든 멘션을  
            (MEMORY_OPTIMIZED = ON);  
  
  
  
  
완료되었습니다.  
  
  
## <a name="e-prerequisite-filegroup-for-sql-server"></a>5. SQL Server에 대한 필수 구성 요소 FILEGROUP  
  
Microsoft SQL Server에서 메모리 최적화 기능을 사용하려면 데이터베이스에 **MEMORY_OPTIMIZED_DATA**로 선언된 FILEGROUP이 있어야 합니다.  
  
- Azure SQL 데이터베이스에서는 이 FILEGROUP을 만들지 않아도 됩니다.  
  
  
*필수 구성 요소:* FILEGROUP에 대한 다음 TRANSACT-SQL 코드는 이 문서의 뒷부분에 나오는 섹션에서 긴 T-SQL 코드 샘플에 대한 필수 구성 요소입니다.  
  
1. SSMS.exe 또는 T-SQL을 전송할 수 있는 다른 도구를 사용해야 합니다.  
2. SSMS에 예제 FILEGROUP T-SQL 코드를 붙여넣습니다.  
3. T-SQL을 편집하여 원하는 대로 해당 특정 이름 및 디렉터리 경로를 변경합니다.  
  - 마지막 디렉터리를 제외하고 FILENAME 값의 모든 디렉터리는 기존의 디렉터리여야 합니다.  
4. 편집된 T-SQL을 실행합니다.  
  - 다음 하위 섹션에서 반복해서 조정하고 속도 비교 T-SQL을 다시 실행해도 FILEGROUP T-SQL은 한 번만 실행하면 됩니다.  
  
  
  
 
  
    ALTER DATABASE InMemTest2  
        ADD FILEGROUP FgMemOptim3  
            CONTAINS MEMORY_OPTIMIZED_DATA;  
    go  
    ALTER DATABASE InMemTest2  
        ADD FILE  
        (  
            NAME = N'FileMemOptim3a',  
            FILENAME = N'C:\DATA\FileMemOptim3a'  
                     --  C:\DATA\    preexisted.  
        ).  
        TO FILEGROUP FgMemOptim3;  
    go  
  
  
다음 스크립트는 파일 그룹을 만들고 권장되는 데이터베이스 설정을 구성합니다. [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)
  
FILE 및 FILEGROUP의 `ALTER DATABASE ... ADD` 에 대한 자세한 내용은 다음을 참조하세요.  
  
- [ALTER DATABASE 파일 및 파일 그룹 옵션(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
- [메모리 액세스에 최적화된 파일 그룹](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)    
  
  
## <a name="f-quick-test-to-prove-speed-improvement"></a>6. 속도 개선을 보여 주는 빠른 테스트  
  
  
이 섹션에서는 메모리 최적화 테이블 변수를 사용하여 INSERT-DELETE에 대한 속도 향상을 테스트하고 비교하는 데 실행할 수 있는 TRANSACT-SQL 코드를 제공합니다. 코드는 처음 절반에서 테이블 형식이 메모리 최적화되었다는 점을 제외하고는 거의 동일한 두 부분으로 구성됩니다.  
  
비교 테스트는 약 7초간 지속됩니다. 예제를 실행하려면  
  
1. *필수 구성 요소:* 이전 섹션에서 FILEGROUP T-SQL을 이미 실행했어야 합니다.  
2. 다음 T-SQL INSERT-DELETE 스크립트를 실행합니다.  
  - T-SQL을 5001번 다시 전송하는 'GO 5001' 문이 있습니다. 횟수를 조정하고 다시 실행할 수 있습니다.  
  
Azure SQL 데이터베이스에서 스크립트를 실행하는 경우 동일한 지역의 VM에서 실행해야 합니다.
  
  
    PRINT ' ';  
    PRINT '---- Next, memory-optimized, faster. ----';  
  
    DROP TYPE IF EXISTS dbo.typeTableC_mem;  
    go  
    CREATE TYPE dbo.typeTableC_mem  -- !!  Memory-optimized.  
         AS TABLE  
         (  
              Column1  INT NOT NULL INDEX ix1,  
              Column2  CHAR(10)  
         )  
         WITH  
              (MEMORY_OPTIMIZED = ON);  
    go  
    DECLARE @dateString_Begin nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_Begin, '  = Begin time, _mem.');  
    go  
    SET NoCount ON;  
    DECLARE @tvTableC dbo.typeTableC_mem;  -- !!  
  
    INSERT INTO @tvTableC (Column1) values (1), (2);  
    INSERT INTO @tvTableC (Column1) values (3), (4);  
    DELETE @tvTableC;  
  
    GO 5001  
  
    DECLARE @dateString_End nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_End, '  = End time, _mem.');  
    go  
    DROP TYPE IF EXISTS dbo.typeTableC_mem;  
    go  
  
    ---- End memory-optimized.  
    -------------------------------------------------  
    ---- Start traditional on-disk.  
  
    PRINT ' ';  
    PRINT '---- Next, tempdb based, slower. ----';  
  
    DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
    go  
    CREATE TYPE dbo.typeTableC_tempdb  -- !!  Traditional tempdb.  
        AS TABLE  
        (  
            Column1  INT NOT NULL ,  
            Column2  CHAR(10)  
        );  
    go  
    DECLARE @dateString_Begin nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_Begin, '  = Begin time, _tempdb.');  
    go  
    SET NoCount ON;  
    DECLARE @tvTableC dbo.typeTableC_tempdb;  -- !!  
  
    INSERT INTO @tvTableC (Column1) values (1), (2);  
    INSERT INTO @tvTableC (Column1) values (3), (4);  
    DELETE @tvTableC;  
  
    GO 5001  
  
    DECLARE @dateString_End nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_End, '  = End time, _tempdb.');  
    go  
    DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
    go  
    ----  
  
    PRINT '---- Tests done. ----';  
  
    go  
  
    /*** Actual output, SQL Server 2016:  
  
    ---- Next, memory-optimized, faster. ----  
    2016-04-20 00:26:58.033  = Begin time, _mem.  
    Beginning execution loop  
    Batch execution completed 5001 times.  
    2016-04-20 00:26:58.733  = End time, _mem.  
  
    ---- Next, tempdb based, slower. ----  
    2016-04-20 00:26:58.750  = Begin time, _tempdb.  
    Beginning execution loop  
    Batch execution completed 5001 times.  
    2016-04-20 00:27:05.440  = End time, _tempdb.  
    ---- Tests done. ----  
    ***/  
  

  
  
  
## <a name="g-predict-active-memory-consumption"></a>7. 활성 메모리 사용량 예측  
  
다음 리소스를 사용하면 메모리 최적화 테이블의 활성 메모리 요구량을 예측할 수 있습니다.  
  
- [메모리 액세스에 최적화된 테이블에 필요한 메모리 예측](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기: 계산 예](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
큰 테이블 변수의 경우 비클러스터형 인덱스는 메모리 최적화 *테이블*보다 더 많은 메모리를 사용합니다. 행 개수 및 인덱스 키가 클수록 차이가 증가합니다.  
  
메모리 최적화 테이블 변수가 액세스당 하나의 정확한 키 값에만 액세스하는 경우 비클러스터형 인덱스보다 해시 인덱스가 더 적합할 수 있습니다. 그러나 적절한 BUCKET_COUNT를 예측할 수 없는 경우 비클러스터형 인덱스가 차선책입니다.  
  
## <a name="h-see-also"></a>8. 참고 항목  
  
- [Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)
- [메모리 액세스에 최적화된 개체에 대한 내구성 정의](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
