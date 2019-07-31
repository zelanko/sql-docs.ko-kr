---
title: 메모리 액세스에 최적화된 테이블 변경 | Microsoft 문서
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3d65b6931053c7eccbb96093fb2cd840f8277cb7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951290"
---
# <a name="altering-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 변경

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

ALTER TABLE 문을 사용하여 메모리 최적화 테이블에서 스미카 및 인덱스를 변경할 수 있습니다. 메모리 최적화 테이블에 대한 SQL Server 2016 및 Azure SQL Database ALTER TABLE 작업은 오프라인이므로 작업이 진행되는 동안 테이블을 쿼리할 수 없습니다. 데이터베이스 애플리케이션을 계속 실행할 수 있으며, 수정 프로세스가 완료될 때까지 테이블에 액세스 중인 작업이 차단됩니다. 여러 ADD, DROP 또는 ALTER 작업을 단일 ALTER TABLE 문에 결합할 수 없습니다.

> [!IMPORTANT]
> Azure SQL Database Managed Instance는 범용 서비스 계층에서 메모리 최적화 테이블을 지원하지 않습니다.
  
## <a name="alter-table"></a>ALTER TABLE  

ALTER TABLE 구문은 테이블 스키마를 변경하거나 인덱스를 추가, 삭제, 다시 빌드하는 데 사용할 수 있습니다. 색인은 테이블 정의의 일부로 간주됩니다.  
  
- ALTER TABLE ... ADD/DROP/ALTER INDEX 구문은 메모리 최적화 테이블에만 지원됩니다.  
  
- ALTER TABLE 문을 사용하지 않을 경우 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), [PAD_INDEX](../../t-sql/statements/alter-table-index-option-transact-sql.md) 문은 메모리 최적화 테이블의 인덱스로 지원되지 않습니다.  
  
다음과 같은 유형의 수정이 지원됩니다.  
  
- 버킷 수 변경  
  
- 인덱스 추가 및 제거  
  
- 열 변경, 추가, 제거  
  
- 제약 조건 추가 및 제거  
  
 ALTER TABLE 기능과 전체 구문에 대한 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
## <a name="schema-bound-dependency"></a>스키마 바운드 종속성

 고유하게 컴파일된 저장 프로시저는 스키마 바운드 형식이어야 합니다. 즉, 액세스하는 메모리 액세스에 최적화된 테이블과 참조하는 열에서 스키마 바운드 종속성을 가져야 합니다. 스키마 바운드 종속성은 참조 엔터티가 존재하는 한 참조된 엔터티가 삭제되거나 호환되지 않는 방식으로 수정되지 않도록 방지하는 두 엔터티 간 관계입니다.  
  
 예를 들어 고유하게 컴파일된 스키마 바운드 저장 프로시저가 *mytable* 테이블의 *c1*열을 참조하는 경우 *c1* 열을 삭제할 수 없습니다. 마찬가지로, 열 목록 없이 INSERT 문(예: `INSERT INTO dbo.mytable VALUES (...)`)을 사용하는 프로시저가 있는 경우 테이블에서 열을 삭제할 수 없습니다.  

## <a name="logging-of-alter-table-on-memory-optimized-tables"></a>메모리 최적화 테이블에 대한 ALTER TABLE 로깅

메모리 최적화 테이블에서 대부분 ALTER TABLE 시나리오는 이제 병렬로 실행되고 이를 통해 트랜잭션 로그에 대한 쓰기가 최적화됩니다. 최적화는 메타데이터 변경 내용을 트랜잭션 로그에 기록해야만 가능합니다. 그러나 다음 ALTER TABLE 작업은 단일 스레드를 실행하고 로그에 최적화되지 않습니다.

이 경우 단일 스레드 작업은 변경된 테이블의 전체 내용을 트랜잭션 로그에 기록합니다. 단일 스레드 작업 목록은 다음과 같습니다.

- 큰 개체(LOB) 형식인 nvarchar(max), varchar(max) 또는 varbinary(max)를 사용하도록 열을 변경하거나 추가합니다.

- COLUMNSTORE 인덱스를 추가하거나 삭제합니다.

- [행 외부 열](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)에 영향을 주는 거의 모든 항목입니다.

  - 행 내부 열이 행 외부 열을 이동하게 합니다.
  - 행 외부 열이 행 내부 열을 이동하게 합니다.
  - 새 행 외부 열을 만듭니다.
  - *예외:* 이미 행 외부 형식인 열을 늘리면 최적화된 방식으로 기록됩니다.
  
## <a name="examples"></a>예

다음 예는 기존 해시 인덱스의 버킷 수를 수정합니다. 여기서 해시 인덱스가 새 버킷 수로 다시 빌드되며 해시 인덱스의 다른 속성은 그대로 유지됩니다.  

```sql
ALTER TABLE Sales.SalesOrderDetail_inmem
       ALTER INDEX imPK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID  
              REBUILD WITH (BUCKET_COUNT=67108864);  
GO
```

다음 예는 NOT NULL 제약 조건과 DEFAULT 정의로 열을 추가하며 WITH VALUES를 사용하여 테이블에 있는 각 기존 행의 값을 제공합니다. WITH VALUES를 사용하지 않으면 각 행에서 새 열의 값은 NULL이 됩니다.  

```sql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD Comment NVARCHAR(100) NOT NULL DEFAULT N'' WITH VALUES;  
GO
```

다음 예에서는 기존 열에 기본 키 제약 조건을 추가합니다.  

```sql
CREATE TABLE dbo.UserSession (
   SessionId int not null,
   UserId int not null,
   CreatedDate datetime2 not null,
   ShoppingCartId int,
   index ix_UserId nonclustered hash (UserId) with (bucket_count=400000)
)
WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY) ;  
GO  
  
ALTER TABLE dbo.UserSession  
       ADD CONSTRAINT PK_UserSession PRIMARY KEY NONCLUSTERED (SessionId);  
GO
```

다음 예에서는 인덱스를 제거합니다.  

```sql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       DROP INDEX ix_ModifiedDate;  
GO
```  

다음 예에서는 인덱스를 추가합니다.  

```sql  
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD INDEX ix_ModifiedDate (ModifiedDate);  
GO  
```  

다음 예에서는 인덱스와 제약 조건이 포함된 여러 열을 추가합니다.  

```sql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD    CustomerID int NOT NULL DEFAULT -1 WITH VALUES,  
              ShipMethodID int NOT NULL DEFAULT -1 WITH VALUES,  
              INDEX ix_Customer (CustomerID);  
GO  
```

<a name="logging-of-alter-table-on-memory-optimized-tables-124"></a>

## <a name="see-also"></a>참고 항목  

[메모리 액세스에 최적화된 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
