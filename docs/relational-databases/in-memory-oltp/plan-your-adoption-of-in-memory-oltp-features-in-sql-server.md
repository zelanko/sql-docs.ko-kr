---
title: "SQL Server에 메모리 내 OLTP 기능 채택 계획 | Microsoft 문서"
ms.custom: 
ms.date: 11/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 041b428f-781d-4628-9f34-4d697894e61e
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8cfb42dd7bfa261ba364b427075280631d386b9
ms.sourcegitcommit: 50e9ac6ae10bfeb8ee718c96c0eeb4b95481b892
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2017
---
# <a name="plan-your-adoption-of-in-memory-oltp-features-in-sql-server"></a>SQL Server에 메모리 내 OLTP 기능 채택 계획
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


이 문서에서는 메모리 내 기능 채택이 비즈니스 시스템의 다른 측면에 영향을 주는 방식을 설명합니다.



## <a name="a-adoption-of-in-memory-oltp-features"></a>1. 메모리 내 OLTP 기능 채택


다음 하위 섹션에서는 메모리 내 기능을 채택하고 구현하려는 경우 고려해야 할 요소를 설명합니다. 다음에서 많은 설명 정보를 확인할 수 있습니다.

- [메모리 내 OLTP를 사용하여 Azure SQL Database에서 응용 프로그램의 성능 향상](https://azure.microsoft.com/documentation/articles/sql-database-in-memory-oltp-migration/)



### <a name="a1-prerequisites"></a>A.1 필수 조건

메모리 내 기능 사용을 위한 한 가지 필수 조건은 SQL 제품의 버전 또는 서비스 계층과 관련될 수 있습니다. 이 필수 조건 및 기타 필수 조건은 다음을 참조하세요.

- [메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)
    - [SQL Server 2016 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md)
    - [SQL Database 가격 책정 계층 권장 사항](https://azure.microsoft.com/documentation/articles/sql-database-service-tier-advisor/)


### <a name="a2-forecast-the-amount-of-active-memory"></a>A.2 활성 메모리 양 예측

시스템에 새 메모리 최적화 테이블을 지원하기에 충분한 활성 메모리가 있나요?

#### <a name="microsoft-sql-server"></a>Microsoft SQL Server

200GB의 데이터를 포함하는 메모리 최적화 테이블은 200GB 이상의 활성 메모리가 해당 지원 전용이어야 합니다. 많은 양의 데이터를 포함하는 메모리 최적화 테이블을 구현하기 전에 서버 컴퓨터에 추가해야 할 수 있는 추가 활성 메모리의 양을 예측해야 합니다. 예측 지침은 다음을 참조하세요.

- [메모리 액세스에 최적화된 테이블에 필요한 메모리 예측](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)

#### <a name="azure-sql-database"></a>Azure SQL 데이터베이스

Azure SQL Database 클라우드 서비스에 호스트된 데이터베이스의 경우 선택한 서비스 계층이 데이터베이스에서 사용할 수 있는 활성 메모리의 양에 영향을 줍니다. 경고를 사용하여 데이터베이스의 메모리 사용량 모니터링을 계획해야 합니다. 자세한 내용은 다음을 참조하세요.

- [가격 책정 계층](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-service-tiers#single-database-service-tiers-and-performance-levels)에 대한 메모리 내 OLTP 저장소 제한 검토
- [메모리 내 OLTP 저장소 모니터링](https://azure.microsoft.com/documentation/articles/sql-database-in-memory-oltp-monitoring/)

#### <a name="memory-optimized-table-variables"></a>메모리 액세스에 최적화된 테이블 변수

메모리 액세스에 최적화되도록 선언된 테이블 변수는 **tempdb** 데이터베이스에 있는 기존 #TempTable에 적합한 경우도 있습니다. 이러한 테이블 변수는 상당한 양의 활성 메모리를 사용하지 않고도 상당한 성능 향상을 제공할 수 있습니다.

### <a name="a3-table-must-be-offline-to-convert-to-memory-optimized"></a>A.3 메모리 최적화 테이블로 변환하려면 테이블이 오프라인 상태여야 함

일부 ALTER TABLE 기능은 메모리 최적화 테이블에 사용할 수 있습니다. 그러나 디스크 기반 테이블을 메모리 최적화 테이블로 변환하기 위해 ALTER TABLE 문을 실행할 수는 없습니다. 대신 더 많은 일련의 수동 단계를 사용해야 합니다. 그다음은 디스크 기반 테이블을 메모리 최적화 테이블로 변환하는 다양한 방법을 소개합니다.

#### <a name="manual-scripting"></a>수동 스크립팅

디스크 기반 테이블을 메모리 최적화 테이블로 변환하는 한 가지 방법은 필요한 TRANSACT-SQL 단계를 직접 코딩하는 것입니다.


1. 응용 프로그램 작업을 일시 중단합니다.

2. 전체 백업을 수행합니다.

3. 디스크 기반 테이블의 이름을 바꿉니다.

4. CREATE TABLE 문을 실행하여 새 메모리 최적화 테이블을 만듭니다.

5. 디스크 기반 테이블에서 하위 SELECT를 사용하여 메모리 최적화 테이블에 삽입(INSERT INTO)합니다.

6. 디스크 기반 테이블을 삭제(DROP)합니다.

7. 또 다른 전체 백업을 수행합니다.

8. 응용 프로그램 작업을 다시 시작합니다.


#### <a name="memory-optimization-advisor"></a>메모리 최적화 관리자

메모리 최적화 관리자 도구는 디스크 기반 테이블을 메모리 액세스에 최적화된 테이블로 변환하는 작업을 구현하는 데 유용한 스크립트를 생성할 수 있습니다. 이 도구는 SSDT(SQL Server Data Tools)의 일부로 설치됩니다.

- [메모리 최적화 관리자](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md)
- [SSDT(SQL Server Data Tools) 다운로드](../../ssdt/download-sql-server-data-tools-ssdt.md)


#### <a name="dacpac-file"></a>.dacpac 파일

SSDT에서 관리하는 .dacpac 파일을 사용하여 데이터베이스를 현재 위치에서 업데이트할 수 있습니다. SSDT에서 .dacpac 파일로 인코딩된 스키마의 변경 내용을 지정할 수 있습니다.

*데이터베이스*형식의 Visual Studio 프로젝트 컨텍스트에서 .dacpac 파일을 사용합니다.

- [데이터 계층 응용 프로그램](../../relational-databases/data-tier-applications/data-tier-applications.md) 및 .dacpac 파일



### <a name="a4-guidance-for-whether-in-memory-oltp-features-are-right-for-your-application"></a>A.4 메모리 내 OLTP 기능이 응용 프로그램에 적합한지에 대한 지침

메모리 내 OLTP 기능이 특정 응용 프로그램의 성능을 향상할 수 있는지에 대한 지침은 다음을 참조하세요.

- [메모리 내 OLTP(메모리 내 최적화)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)



## <a name="b-unsupported-features"></a>2. 지원되지 않는 기능

특정 메모리 내 OLTP 시나리오에서 지원되지 않는 기능은 다음에 설명되어 있습니다.

- [메모리 내 OLTP에 대해 지원되지 않는 SQL Server 기능](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


다음 하위 섹션에서는 더 중요한 지원되지 않는 기능 중 일부를 강조합니다.


### <a name="b1-snapshot-of-a-database"></a>B.1 데이터베이스의 스냅숏

지정된 데이터베이스에서 처음으로 메모리 최적화 테이블 또는 모듈이 만들어진 후에는 데이터베이스의 [스냅숏](../../relational-databases/databases/database-snapshots-sql-server.md) 을 생성할 수 없습니다. 구체적인 이유는 다음과 같습니다.

- 첫 번째 메모리 최적화 항목은 메모리 최적화 FILEGROUP에서 마지막 파일을 삭제할 수 없게 만듭니다.
- 메모리 최적화 FILEGROUP에 파일이 있는 데이터베이스는 스냅숏을 지원할 수 없습니다.

일반적으로 스냅숏은 빠른 테스트 반복에 유용할 수 있습니다.


### <a name="b2-cross-database-queries"></a>B.2 데이터베이스 간 쿼리

메모리 액세스에 최적화된 테이블은 [데이터베이스 간](../../relational-databases/in-memory-oltp/cross-database-queries.md) 트랜잭션을 지원하지 않습니다. 메모리 최적화 테이블에도 액세스하는 동일한 쿼리 또는 동일한 트랜잭션에서 다른 데이터베이스에 액세스할 수 없습니다.

테이블 변수는 트랜잭션 변수가 아닙니다. 따라서 데이터베이스 간 쿼리에 [메모리 최적화 테이블 변수](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) 를 사용할 수 있습니다.


### <a name="b3-readpast-table-hint"></a>B.3 READPAST 테이블 힌트

쿼리는 READPAST [테이블 힌트](../../t-sql/queries/hints-transact-sql-table.md) 를 메모리 최적화 테이블에 적용할 수 없습니다.

READPAST 힌트는 여러 세션이 각각 큐 처리 등 같은 작은 행 집합에 액세스하고 수정하는 시나리오에서 유용합니다.


### <a name="b4-rowversion-sequence"></a>B.4 RowVersion, 시퀀스

- 메모리 최적화 테이블에서는 열에 [RowVersion](../../t-sql/data-types/rowversion-transact-sql.md) 태그를 지정할 수 없습니다.


- 
            [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md)는 메모리 최적화 테이블의 제약 조건과 함께 사용할 수 없습니다. 예를 들어 NEXT VALUE FOR 절에 DEFAULT 제약 조건을 만들 수 없습니다. SEQUENCE는 INSERT 및 UPDATE 문에서 사용할 수 있습니다.


## <a name="c-administrative-maintenance"></a>3. 유지 관리


이 섹션에서는 메모리 최적화 테이블이 사용되는 경우 데이터베이스 관리의 차이점을 설명합니다.


### <a name="c1-identity-seed-reset-increment--1"></a>C.1 ID 초기값 재설정, 증분 > 1

메모리 최적화 테이블에는 IDENTITY 열을 재설정하는[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)를 사용할 수 없습니다.

메모리 최적화 테이블에서는 IDENTITY 열의 증분 값이 정확히 1로 제한됩니다.


### <a name="c2-dbcc-checkdb-cannot-validate-memory-optimized-tables"></a>C.2 DBCC CHECKDB는 메모리 최적화 테이블의 유효성을 검사할 수 없음

대상이 메모리 최적화 테이블인 경우 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 명령은 아무 작업도 수행하지 않습니다. 다음 단계는 해결 방법입니다.


1. [트랜잭션 로그를 백업](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)합니다.

2. 메모리 최적화 FILEGROUP의 파일을 null 장치에 백업합니다. 백업 프로세스에서는 체크섬 유효성 검사를 호출합니다.

    손상이 발견되면 다음 단계를 진행합니다.

3. 임시 저장 용도로, 메모리 최적화 테이블의 데이터를 디스크 기반 테이블에 복사합니다.

4. 메모리 최적화 FILEGROUP의 파일을 복원합니다.

5. 디스크 기반 테이블에 임시로 저장된 데이터를 메모리 최적화 테이블에 삽입(INSERT INTO)합니다.

6. 임시로 데이터를 저장한 디스크 기반 테이블을 삭제(DROP)합니다.



## <a name="d-performance"></a>4. 성능

이 섹션에서는 메모리 최적화 테이블의 우수한 성능을 최대 성능 아래로 유지할 수 있는 상황을 설명합니다.


### <a name="d1-index-considerations"></a>D.1 인덱스 고려 사항

메모리 최적화 테이블의 모든 인덱스는 테이블 관련 문 CREATE TABLE 및 ALTER TABLE로 만들고 관리합니다. CREATE INDEX 문을 사용해서는 메모리 최적화 테이블을 대상으로 할 수 없습니다.

처음으로 메모리 최적화 테이블을 구현하는 경우 기존 B-트리 비클러스터형 인덱스는 합리적이고 간단한 선택일 수 있습니다. 나중에 응용 프로그램의 성능을 확인한 후 다른 인덱스 유형으로 바꾸는 것을 고려할 수 있습니다.

메모리 최적화 테이블의 컨텍스트에서는 특수한 유형의 두 가지 인덱스인 해시 인덱스와 Columnstore 인덱스에 대한 논의가 필요합니다.

메모리 최적화 테이블의 인덱스 개요는 다음을 참조하세요.

- [메모리 액세스에 최적화된 테이블의 인덱스](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)


#### <a name="hash-indexes"></a>해시 인덱스

해시 인덱스는 '**=**' 연산자를 사용하여 정확한 해당 기본 키 값으로 하나의 특정 행에 액세스하는 가장 빠른 형식일 수 있습니다.

- '**!=**', '**>**' 또는 '**BETWEEN**'과 같은 부정확한 연산자를 해시 인덱스와 함께 사용할 경우 성능이 저하됩니다.

- 해시 인덱스는 키 값 중복 비율이 너무 높은 경우에는 최선의 선택이 아닐 수도 있습니다.

- 개별 버킷 내에 긴 체인을 방지하려면 해시 인덱스에 필요할 수 있는 *버킷* 수를 과소평가하지 않아야 합니다. 자세한 내용은 다음을 참조하세요.
    - [메모리 액세스에 최적화된 테이블의 해시 인덱스](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)


#### <a name="nonclustered-columnstore-indexes"></a>비클러스터형 columnstore 인덱스

메모리 액세스에 최적화된 테이블은 *온라인 트랜잭션 처리* 또는 *OLTP*라고 하는 패러다임에서 일반적인 비즈니스 트랜잭션 데이터의 많은 처리량을 제공합니다. columnstore 인덱스는 *분석*이라고 하는 집계 및 유사한 처리의 많은 처리량을 제공합니다. 지난 수년간 OLTP와 분석 둘 다의 요구 사항을 만족하는 데 사용할 수 있는 최고의 접근 방식은 데이터 이동이 많고 어느 정도의 데이터 중복도가 있는 별도의 테이블을 사용하는 것이었습니다. 현재는 더 단순한 **하이브리드 솔루션** 을 사용할 수 있으므로 메모리 최적화 테이블에 columnstore 인덱스를 사용하세요.


- 디스크 기반 테이블을 기반으로 하여 [columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-overview.md) 를 클러스터형 인덱스로도 작성할 수 있습니다. 그러나 메모리 최적화 테이블에서는 columnstore 인덱스를 클러스터화할 수 없습니다.


- 메모리 최적화 테이블의 LOB 또는 행 외부 열은 테이블에서 columnstore 인덱스를 만들지 못하게 합니다.


- 테이블에 columnstore 인덱스가 있는 동안에는 메모리 최적화 테이블에 대해 ALTER TABLE 문을 실행할 수 없습니다.
    - 2016년 8월 현재 Microsoft는 가까운 시일 내 columnstore 인덱스 다시 만들기 성능을 향상하기 위한 계획이 있습니다.



### <a name="d2-lob-and-off-row-columns"></a>D.2 LOB 및 행 외부 열

LOB(Large Object)는varchar(**max**) 형식의 열입니다. 메모리 최적화 테이블에 LOB 열이 몇 개 있는 정도로는 중요하기 여길 정도로 성능을 저하하지 않습니다. 그러나 데이터에 필요한 것보다 많은 LOB 열은 사용하지 않도록 합니다. 같은 조언이 행 외부 열에도 적용됩니다. varchar(512)만으로 충분한 경우 열을 nvarchar(3072)로 정의하지 마세요.


LOB 및 행 외부 열에 대한 자세한 내용은 다음을 참조하세요.

- [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)
- [메모리 내 OLTP에 지원되는 데이터 형식](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)



## <a name="e-limitations-of-native-procs"></a>5. 네이티브 프로시저의 제한 사항


Transact-SQL의 특정 요소는 저장 프로시저를 포함하여 고유하게 컴파일된 T-SQL 모듈에서 지원되지 않습니다. 지원되는 기능에 대한 세부 정보는 다음을 참조하세요.

- [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)

지원되지 않는 기능을 사용하는 Transact-SQL 모듈을 고유하게 컴파일된 모듈로 마이그레이션할 때 고려해야 할 사항은 다음을 참조하세요.

- [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)

Transact-SQL의 특정 요소에 대한 제한 사항 외에도 고유하게 컴파일된 T-SQL 모듈에서 지원되는 쿼리 연산자에 대한 제한 사항도 있습니다. 이러한 제한 사항 때문에 고유하게 컴파일된 저장 프로시저는 큰 데이터 집합을 처리하는 분석 쿼리에는 적합하지 않습니다.

#### <a name="no-parallel-processing-in-a-native-proc"></a>네이티브 프로시저에서는 병렬 처리 불가

병렬 처리는 네이티브 프로시저에 대한 쿼리 계획의 일부가 될 수 없습니다. 네이티브 프로시저는 항상 단일 스레드입니다.


#### <a name="join-types"></a>조인 유형


해시 조인도 병합 조인도 네이티브 프로시저에 대한 쿼리 계획의 일부가 될 수 없습니다. 중첩 루프 조인이 사용됩니다.


#### <a name="no-hash-aggregation"></a>해시 집계 없음

네이티브 프로시저에 대한 쿼리 계획에 집계 단계가 필요한 경우 스트림 집계만 사용할 수 있습니다. 네이티브 프로시저에 대한 쿼리 계획에서는 해시 집계가 지원되지 않습니다.

- 많은 수의 행에서 데이터를 집계해야 하는 경우 해시 집계가 낫습니다.



## <a name="f-application-design-transactions-and-retry-logic"></a>6. 응용 프로그램 디자인: 트랜잭션 및 재시도 논리

메모리 최적화 테이블과 관련된 트랜잭션은 같은 테이블과 관련된 다른 트랜잭션에 종속될 수 있습니다. 종속 트랜잭션 수가 허용된 최대값을 초과하면 모든 종속 트랜잭션이 실패합니다.

SQL Server 2016에서:

- 종속 트랜잭션 수의 허용된 최대값은 8입니다. 8은 지정된 트랜잭션이 종속될 수 있는 트랜잭션의 제한이기도 합니다.
- 오류 번호는 41839입니다. (SQL Server 2014에서 오류 번호는 41301입니다.)


스크립트에 *재시도 논리* 를 추가하여 Transact-SQL 스크립트를 가능한 트랜잭션 오류에 대해 더 강력하게 만들 수 있습니다. 재시도 논리는 UPDATE 및 DELETE 호출이 빈번하거나 다른 테이블의 외래 키가 메모리 최적화 테이블을 참조하는 경우 더 유용할 수 있습니다. 자세한 내용은 다음을 참조하세요.

- [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)
- [Transaction dependency limits with memory optimized tables – Error 41839(메모리 액세스에 최적화된 테이블이 있는 트랜잭션 종속성 제한 – 오류 41839)](https://blogs.msdn.microsoft.com/sqlcat/2016/07/11/transaction-dependency-limits-with-memory-optimized-tables-error-41839/)



## <a name="related-links"></a>관련 링크

- [메모리 내 OLTP(메모리 내 최적화)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)


