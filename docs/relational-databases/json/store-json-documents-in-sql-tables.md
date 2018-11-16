---
title: SQL Server 또는 SQL 데이터베이스에 JSON 문서 저장 | Microsoft Docs
ms.description: This article describes why and how to store and index JSON documents in SQL Server or SQL Database, and how to optimize queries over the JSON documents.
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: 608021d678f57bda86b1fc77950e029efceea7ad
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51663612"
---
# <a name="store-json-documents-in-sql-server-or-sql-database"></a>SQL Server 또는 SQL 데이터베이스에 JSON 문서 저장
SQL Server 및 Azure SQL Database에는 표준 SQL 언어를 사용하여 JSON 문서를 구문 분석할 수 있는 네이티브 JSON 함수가 있습니다. 이제 JSON 문서를 SQL Server 또는 SQL Database에 저장하고 JSON 데이터를 NoSQL 데이터베이스에서처럼 쿼리할 수 있습니다. 이 문서에서는 JSON 문서를 SQL Server 또는 SQL Database에 저장하는 옵션에 대해 설명합니다.

## <a name="classic-tables"></a>클래식 테이블

SQL Server 또는 SQL Database에 JSON 문서를 저장하는 가장 간단한 방법은 문서의 ID와 문서의 내용을 포함하는 2열 테이블을 만드는 것입니다. 예를 들어 다음과 같이 사용할 수 있습니다.

```sql
create table WebSite.Logs (
    _id bigint primary key identity,
    log nvarchar(max)
);
```

이 구조는 클래식 문서 데이터베이스에서 찾을 수 있는 컬렉션과 같습니다. 기본 키 `_id`는 모든 문서에 고유 식별자를 제공하고 빠른 검색을 가능하게 하는 자동 증분 값입니다. 이 구조는 ID로 문서를 검색하거나 저장된 문서를 ID로 업데이트하려는 고전적인 NoSQL 시나리오에 적합한 선택입니다.

nvarchar(max) 데이터 형식을 사용하면 최대 2GB 크기의 JSON 문서를 저장할 수 있습니다. 그러나 JSON 문서가 8KB보다 크지 않은 것으로 확인되면 성능상의 이유로 NVARCHAR(max) 대신 NVARCHAR(4000)을 사용하는 것이 좋습니다.

앞의 예에서 만든 샘플 테이블은 유효한 JSON 문서가 `log` 열에 저장되어 있다고 가정합니다. 유효한 JSON이 `log` 열에 저장되었는지 확인하려는 경우 열에 CHECK 제약 조건을 추가할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.

```sql
ALTER TABLE WebSite.Logs
    ADD CONSTRAINT [Log record should be formatted as JSON]
                   CHECK (ISJSON(log)=1)
```

누군가가 테이블에 문서를 삽입하거나 업데이트할 때마다 이 제약 조건은 JSON 문서의 형식이 올바른지 확인합니다. 제약 조건이 없으면 모든 JSON 문서가 아무런 처리 없이 열에 직접 추가되기 때문에 테이블이 삽입에 최적화됩니다.

JSON 문서를 테이블에 저장하면 표준 Transact-SQL 언어를 사용하여 문서를 쿼리할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.

```sql
SELECT TOP 100 JSON_VALUE(log, ‘$.severity’), AVG( CAST( JSON_VALUE(log,’$.duration’) as float))
 FROM WebSite.Logs
 WHERE CAST( JSON_VALUE(log,’$.date’) as datetime) > @datetime
 GROUP BY JSON_VALUE(log, ‘$.severity’)
 HAVING AVG( CAST( JSON_VALUE(log,’$.duration’) as float) ) > 100
 ORDER BY AVG( CAST( JSON_VALUE(log,’$.duration’) as float) ) DESC
```

*아무* T-SQL 함수 및 쿼리 절을 사용하여 JSON 문서를 쿼리할 수 있다는 것이 큰 이점입니다. SQL Server 및 SQL Database는 JSON 문서를 분석하는 데 사용할 수 있는 쿼리에 어떠한 제약 조건을 도입하지 않습니다. `JSON_VALUE` 함수를 사용하여 JSON 문서에서 값을 추출하고 다른 값처럼 쿼리에서 사용할 수 있습니다.

다양한 T-SQL 쿼리 구문을 사용하는 이 기능은 SQL Server, SQL Database, 클래식 NoSQL 데이터베이스 간의 주요 차이점입니다. Transact-SQL에서는 JSON 데이터를 처리하는 데 필요한 기능이 있을 것입니다.

## <a name="indexes"></a>인덱스

쿼리가 일부 속성(예: JSON 문서의 `severity` 속성)으로 문서를 자주 검색하는 경우 속성에 클래식 NONCLUSTERED 인덱스를 추가하여 쿼리 속도를 높일 수 있습니다.

지정된 경로(경로 `$.severity`)의 JSON 열에서 JSON 값을 공개하는 계산 열을 만들고 이 계산 열에 표준 색인을 만들 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.

```sql
create table WebSite.Logs (
    _id bigint primary key identity,
    log nvarchar(max),

    severity AS JSON_VALUE(log, '$.severity'),
    index ix_severity (severity)
);
```

이 예에서 사용된 계산 열은 테이블에 추가 공간을 추가하지 않는 비지속형 또는 가상 열입니다. 이는 다음 예와 같이 조회 성능을 향상시키기 위해 색인 `ix_severity`에 의해 사용됩니다.

```sql
SELECT log
FROM Website.Logs
WHERE JSON_VALUE(log, '$.severity') = 'P4'
```

이 인덱스의 한 가지 중요한 특징은 데이터 정렬을 인식한다는 것입니다. 원래 NVARCHAR 열에 COLLATION 속성(예: 대/소문자 구분 또는 일본어)이 있으면 인덱스는 NVARCHAR 열과 관련된 언어 규칙 또는 대/소문자 구분 규칙에 따라 정렬됩니다. 이 데이터 정렬 인식은 JSON 문서를 처리할 때 사용자 정의 언어 규칙을 사용해야 하는 글로벌 시장용 응용 프로그램을 개발하는 경우 중요한 기능입니다.

## <a name="large-tables--columnstore-format"></a>큰 테이블 및 columnstore 형식

컬렉션에 많은 수의 JSON 문서가 있을 것으로 예상되는 경우 다음 예제와 같이 컬렉션에 CLUSTERED COLUMNSTORE 인덱스를 추가하는 것이 좋습니다.

```sql
create sequence WebSite.LogID as bigint;
go
create table WebSite.Logs (
    _id bigint default(next value for WebSite.LogID),
    log nvarchar(max),

    INDEX cci CLUSTERED COLUMNSTORE
);
```

CLUSTERED COLUMNSTORE 인덱스는 최대 25배의 높은 데이터 압축률을 제공하므로 저장소 공간 요구 사항을 크게 줄이고 저장소 비용을 낮추며 워크로드의 I/O 성능을 높일 수 있습니다. 또한 CLUSTERED COLUMNSTORE 인덱스는 JSON 문서의 테이블 스캔 및 분석에 최적화되어 있으므로 이 형식의 인덱스는 로그 분석에 가장 적합한 옵션이 될 수 있습니다.

앞의 예에서는 시퀀스 개체를 사용하여 `_id` 열에 값을 할당합니다. 시퀀스 및 ID 모두 이 ID 열에 대해 유효한 옵션입니다.

## <a name="frequently-changing-documents--memory-optimized-tables"></a>자주 변경되는 문서 및 메모리 최적화 테이블

컬렉션에서 많은 업데이트, 삽입 및 삭제 작업이 실행되도록 하려면 JSON 문서를 메모리 최적화 테이블에 저장할 수 있습니다. 메모리 최적화 JSON 컬렉션은 항상 데이터를 메모리에 저장하기 때문에 저장소 I/O 오버헤드가 없습니다. 또한 메모리 최적화 JSON 컬렉션은 완전히 잠금 해제되어 있습니다. 즉, 문서 작업이 다른 작업을 방해하지 않습니다.

클래식 컬렉션을 메모리 최적화 컬렉션으로 변환해야 하는 유일한 경우는 다음 예제와 같이 테이블 정의 뒤에 **with(memory_optimized=on)** 옵션을 지정하는 것입니다. 그러면 JSON 컬렉션의 메모리 최적화 버전이 생깁니다.

```sql
create table WebSite.Logs (
  _id bigint identity primary key nonclustered,
  log nvarchar(4000)
) with (memory_optimized=on)
```

메모리 최적화 테이블은 자주 변경되는 문서에 가장 적합한 옵션입니다. 메모리 최적화 테이블을 고려할 때 성능도 고려합니다. 가능하면 메모리 최적화 콜렉션의 JSON 문서에 NVARCHAR (max) 대신 NVARCHAR (4000)을 사용하여 성능을 크게 향상시키세요.

클래식 테이블과 마찬가지로 계산 열을 사용하여 메모리 최적화 테이블에서 공개된 필드에 인덱스를 추가할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.

```sql
create table WebSite.Logs (

  _id bigint identity primary key nonclustered,
  log nvarchar(4000),

  severity AS cast(JSON_VALUE(log, '$.severity') as tinyint) persisted,
  index ix_severity (severity)

) with (memory_optimized=on)
```

성능을 최대화하려면 JSON 값을 속성의 값을 유지하는 데 사용할 수 있는 가능한 가장 작은 유형으로 캐스팅합니다. 앞의 예에서는 **tinyint**가 사용됩니다.

저장 프로시저에서 JSON 문서를 업데이트하는 SQL 쿼리를 넣으면 네이티브 컴파일의 이점을 얻을 수도 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.

```sql
CREATE PROCEDURE WebSite.UpdateData(@Id int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION

AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE WebSite.Logs
    SET log = JSON_MODIFY(log, @Property, @Value)
    WHERE _id = @Id;

END
```

이 네이티브 컴파일 프로시저는 쿼리를 실행하고 쿼리를 실행하는 .DLL 코드를 만듭니다. 고유하게 컴파일된 프로시저는 데이터를 쿼리하고 업데이트하기 위한 보다 빠른 방법입니다.

## <a name="conclusion"></a>결론

SQL Server 및 SQL Database의 기본 JSON 기능을 사용하면 NoSQL 데이터베이스처럼 JSON 문서를 처리할 수 있습니다. 모든 데이터베이스(관계형 또는 NoSQL)에는 JSON 데이터 처리에 대한 장단점이 있습니다. JSON 문서를 SQL Server 또는 SQL Database에 저장하는 주요 이점은 완전한 SQL 언어 지원입니다. 다양한 Transact-SQL 언어를 사용하여 데이터를 처리하고 다양한 저장 옵션을 구성할 수 있습니다(압축률이 높고 빠른 분석을 위한 columnstore 인덱스부터 잠금 해제 처리를 위한 메모리 최적화 테이블까지). 동시에 NoSQL 시나리오에서 쉽게 재사용할 수 있는 성숙한 보안 및 국제화 기능의 이점을 누릴 수 있습니다. 이 문서에서 설명한 이유로 인해 SQL Server 또는 SQL Database에 JSON 문서를 저장하는 것이 좋습니다.

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-blog-posts"></a>Microsoft 블로그 게시물  
  
특정 솔루션, 사용 사례 및 권장 사항은 SQL Server 및 Azure SQL Database의 기본 제공 JSON 지원에 대한 [블로그 게시물](https://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.  

### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
