---
title: SET TRANSACTION ISOLATION LEVEL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LEVEL
- LEVEL_TSQL
- SET TRANSACTION ISOLATION LEVEL
- ISOLATION
- ISOLATION_TSQL
- SET_TRANSACTION_ISOLATION_LEVEL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET TRANSACTION ISOLATION LEVEL statement
- row versioning [SQL Server], isolation levels
- TRANSACTION ISOLATION LEVEL option
- isolation levels [SQL Server], setting
- locking [SQL Server], isolation levels
- transactions [SQL Server], isolation levels
ms.assetid: 016fb05e-a702-484b-bd2a-a6eabd0d76fd
caps.latest.revision: 80
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6e9a7eefcd3ba735175e62c174fe338b2858be9f
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782654"
---
# <a name="set-transaction-isolation-level-transact-sql"></a>SET TRANSACTION ISOLATION LEVEL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)]에 연결하여 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문의 잠금 및 행 버전 관리 기능을 제어합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>구문

```
-- Syntax for SQL Server and Azure SQL Database
  
SET TRANSACTION ISOLATION LEVEL
    { READ UNCOMMITTED
    | READ COMMITTED
    | REPEATABLE READ
    | SNAPSHOT
    | SERIALIZABLE
    }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse
  
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED
```

## <a name="arguments"></a>인수  
 READ UNCOMMITTED  
 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 행을 문이 읽을 수 있도록 지정합니다.  
  
 READ UNCOMMITTED 수준에서 실행 중인 트랜잭션은 현재 트랜잭션에서 읽은 데이터를 다른 트랜잭션에서 수정하지 못하도록 하는 공유 잠금을 실행하지 않습니다. 또한 READ UNCOMMITTED 트랜잭션은 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 행을 현재 트랜잭션이 읽지 못하도록 하는 배타적 잠금에 의해 차단되지도 않습니다. 이 옵션을 설정하면 커밋되지 않은 수정 내용을 읽을 수 있습니다. 이런 경우를 더티 읽기라고 합니다. 트랜잭션이 종료되기 전에 데이터의 값을 변경하고 데이터 집합에 행을 표시하거나 표시하지 않을 수 있습니다. 이 옵션은 트랜잭션에서 모든 SELECT 문의 모든 테이블에 NOLOCK을 설정하는 것과 같습니다. 또한 격리 수준 중에서 제한이 가장 적습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다음 중 하나를 사용하여 트랜잭션에서 커밋되지 않은 데이터 수정 내용에 대해 더티 읽기를 수행할 수 없도록 하여 잠금 경합을 최소화할 수도 있습니다.  
  
-   READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON으로 설정된 READ COMMITTED 격리 수준  
  
-   SNAPSHOT 격리 수준  
  
 READ COMMITTED  
 다른 트랜잭션에 의해 수정되었지만 커밋되지 않은 데이터를 문이 읽을 수 없도록 지정합니다. 이렇게 하면 더티 읽기를 방지할 수 있습니다. 현재 트랜잭션 내에 있는 개별 문 간에 다른 트랜잭션에서 데이터를 변경하면 반복할 수 없는 읽기가 발생하거나 가상 데이터가 될 수 있습니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본값입니다.  
  
 READ COMMITTED의 동작은 다음과 같이 READ_COMMITTED_SNAPSHOT 데이터베이스 옵션 설정에 따라 달라집니다.  
  
-   READ_COMMITTED_SNAPSHOT이 OFF(기본값)로 설정되어 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 공유 잠금을 사용하여 현재 트랜잭션이 읽기 작업을 실행하는 동안 다른 트랜잭션이 행을 수정하지 못하도록 합니다. 또한 공유 잠금은 다른 트랜잭션이 완료될 때까지 해당 트랜잭션이 수정한 행을 문이 읽을 수 없도록 합니다. 공유 잠금의 해제 시기는 공유 잠금 유형에 의해 결정됩니다. 행 잠금은 다음 행이 처리되기 전에 해제되고, 페이지 잠금은 다음 페이지를 읽을 때 해제되고 테이블 잠금은 명령문이 끝나면 해제됩니다.  
  
    > [!NOTE]  
    >  READ_COMMITTED_SNAPSHOT이 ON으로 설정되어 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 행 버전 관리를 사용하여 문 시작 시와 트랜잭션별로 데이터의 일관성이 유지된 스냅숏을 각 문에 제공합니다. 다른 트랜잭션에 의한 데이터 업데이트 차단을 위해 잠금이 사용되지는 않습니다.  
    >   
    >  스냅숏 격리는 FILESTREAM 데이터를 지원합니다. 스냅숏 격리 모드에서는 트랜잭션의 문이 읽은 FILESTREAM 데이터가 트랜잭션 시작 시와 트랜잭션별로 데이터 버전의 일관성이 유지되도록 지정합니다.  
  
 READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON인 경우 READCOMMITTEDLOCK 테이블 힌트를 사용하여 READ_COMMITTED 격리 수준에서 실행 중인 트랜잭션의 개별 문에 대해 행 버전 관리 대신 공유 잠금을 요청할 수 있습니다.  
  
> [!NOTE]  
>  READ_COMMITTED_SNAPSHOT 옵션을 설정할 때는 ALTER DATABASE 명령을 실행하는 연결만 데이터베이스에서 허용됩니다. ALTER DATABASE 명령 실행이 완료될 때까지 데이터베이스에서 다른 열린 연결이 없어야 합니다. 데이터베이스가 단일 사용자 모드에 있을 필요는 없습니다.  
  
 REPEATABLE READ  
 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 데이터를 문이 읽을 수 없도록 지정하고 현재 트랜잭션이 완료될 때까지 현재 트랜잭션이 읽은 데이터를 다른 트랜잭션이 수정할 수 없도록 지정합니다.  
  
 공유 잠금은 트랜잭션의 각 문이 읽은 모든 데이터에 적용되며 트랜잭션이 완료될 때까지 유지됩니다. 따라서 다른 트랜잭션은 현재 트랜잭션이 읽은 행을 수정할 수 없습니다. 다른 트랜잭션은 현재 트랜잭션이 실행한 문의 검색 조건과 일치하는 새 행을 삽입할 수 있습니다. 그런 다음 현재 트랜잭션이 문을 다시 시도하면 새 행이 검색되고 가상 읽기가 수행됩니다. 공유 잠금은 각 문이 끝날 때 해제되지 않고 트랜잭션이 끝날 때까지 유지되므로 동시성이 기본 READ COMMITTED 격리 수준보다 낮습니다. 이 옵션은 필요한 경우에만 사용하세요.  
  
 SNAPSHOT  
 트랜잭션의 문이 읽은 데이터가 트랜잭션별로 트랜잭션을 시작할 때 존재한 데이터 버전과 일관성이 유지되도록 지정합니다. 트랜잭션은 시작되기 전에 커밋된 데이터 수정 내용만 인식할 수 있습니다. 현재 트랜잭션이 시작된 후 다른 트랜잭션에서 수정한 데이터는 현재 트랜잭션에서 실행되는 문에 표시되지 않습니다. 따라서 트랜잭션의 문이 트랜잭션 시작 당시 커밋된 데이터의 스냅숏을 가져오는 것처럼 보입니다.  
  
 데이터베이스가 복구 중인 경우를 제외하면 SNAPSHOT 트랜잭션은 데이터를 읽는 동안 잠금을 요청하지 않습니다. 데이터를 읽는 SNAPSHOT 트랜잭션은 다른 트랜잭션의 데이터 쓰기를 차단하지 않으며 데이터를 쓰는 트랜잭션은 SNAPSHOT 트랜잭션의 데이터 읽기를 차단하지 않습니다.  
  
 데이터베이스 복구를 롤백하는 동안 SNAPSHOT 트랜잭션은 롤백 중인 다른 트랜잭션이 잠근 데이터를 읽으려는 시도가 있을 경우 잠금을 요청합니다. SNAPSHOT 트랜잭션은 해당 트랜잭션이 롤백될 때까지 차단됩니다. 잠금은 부여된 후 바로 해제됩니다.  
  
 SNAPSHOT 격리 수준을 사용하는 트랜잭션을 시작하려면 먼저 ALLOW_SNAPSHOT_ISOLATION 데이터베이스 옵션을 ON으로 설정해야 합니다. SNAPSHOT 격리 수준을 사용하는 트랜잭션이 여러 데이터베이스의 데이터에 액세스할 경우 각 데이터베이스에서 ALLOW_SNAPSHOT_ISOLATION을 ON으로 설정해야 합니다.  
  
 트랜잭션은 시작된 격리 수준과 다른 SNAPSHOT 격리 수준으로 설정할 수 없습니다. 이렇게 설정하면 트랜잭션이 중단됩니다. 트랜잭션이 SNAPSHOT 격리 수준에서 시작되면 다른 격리 수준으로 변경한 다음 다시 SNAPSHOT으로 변경할 수 있습니다. 트랜잭션은 데이터에 처음 액세스할 때 시작됩니다.  
  
 SNAPSHOT 격리 수준에서 실행 중인 트랜잭션은 해당 트랜잭션에서 변경한 내용을 볼 수 있습니다. 예를 들어 트랜잭션이 테이블에서 UPDATE를 수행한 다음 동일한 테이블에 대해 SELECT 문을 실행하면 수정된 데이터가 결과 집합에 포함됩니다.  
  
> [!NOTE]  
>  스냅숏 격리 모드에서는 트랜잭션의 문이 읽은 FILESTREAM 데이터가 문 시작 시가 아니라 트랜잭션 시작 시와 트랜잭션별로 데이터 버전의 일관성이 유지되도록 지정합니다.  
  
 SERIALIZABLE  
 다음을 지정합니다.  
  
-   문은 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 데이터를 읽을 수 없습니다.  
  
-   현재 트랜잭션이 읽은 데이터는 현재 트랜잭션이 완료될 때까지 다른 트랜잭션에서 수정할 수 없습니다.  
  
-   다른 트랜잭션은 현재 트랜잭션이 완료된 다음에야 현재 트랜잭션의 문이 읽은 키 범위 내의 키 값을 가진 새 행을 삽입할 수 있습니다.  
  
 범위 잠금은 트랜잭션에서 실행된 각 문의 검색 조건과 일치하는 키 값의 범위에 적용됩니다. 따라서 다른 트랜잭션은 현재 트랜잭션에서 실행한 문에 한정되는 행을 업데이트하거나 삽입할 수 없습니다. 즉, 트랜잭션의 문이 다시 실행되면 동일한 행 집합을 읽게 됩니다. 범위 잠금은 트랜잭션이 완료될 때까지 유지됩니다. 범위 잠금은 전체 키 범위를 잠그고 트랜잭션이 완료될 때까지 해당 잠금을 보유하므로 격리 수준 중에서 가장 제한적입니다. 동시성이 더 낮기 때문에 필요할 때만 이 옵션을 사용하도록 하세요. 이 옵션은 트랜잭션의 모든 SELECT 문의 모든 테이블에 HOLDLOCK을 설정하는 것과 같습니다.  
  
## <a name="remarks"></a>Remarks  
 격리 수준 옵션은 한 번에 하나만 설정할 수 있으며 명시적으로 변경할 때까지는 해당 연결에 대한 설정이 그대로 유지됩니다. 문의 FROM 절에 있는 테이블 힌트가 테이블에 대해 다른 잠금 동작이나 버전 관리 동작을 지정하지 않는 한 트랜잭션 내에서 수행되는 모든 읽기 작업은 지정한 격리 수준의 규칙에 따라 수행됩니다.  
  
 트랜잭션 격리 수준은 읽기 작업 시 획득되는 잠금 유형을 정의합니다. 일반적으로 READ COMMITTED 또는 REPEATABLE READ에 대해 획득된 공유 잠금은 행 잠금입니다. 그러나 읽기 작업에서 페이지나 테이블의 많은 행을 참조하는 경우 이 행 잠금은 페이지 또는 테이블 잠금으로 에스컬레이션될 수 있습니다. 트랜잭션에서 행을 읽은 후 수정하면 트랜잭션은 해당 행을 보호하기 위해 배타적 잠금을 획득합니다. 이러한 배타적 잠금은 트랜잭션이 완료될 때까지 유지됩니다. 예를 들어 REPEATABLE READ 트랜잭션이 행에 공유 잠금을 설정한 다음 해당 행을 수정하면 공유 행 잠금은 배타적 행 잠금으로 변환됩니다.  
  
 한 가지 경우를 제외하고 트랜잭션 중 언제든지 다른 격리 수준으로 전환할 수 있습니다. 이 예외는 임의의 격리 수준에서 SNAPSHOT 격리로 변경할 때 발생합니다. 이렇게 하면 트랜잭션이 실패하고 롤백됩니다. 그러나 SNAPSHOT 격리에서 시작된 트랜잭션을 다른 격리 수준으로 변경할 수는 있습니다.  
  
 트랜잭션의 격리 수준을 변경하는 경우 변경 후에 읽은 리소스는 새 수준의 규칙에 따라 보호됩니다. 변경 전에 읽은 리소스는 이전 수준의 규칙에 따라 계속 보호됩니다. 예를 들어 트랜잭션이 READ COMMITTED에서 SERIALIZABLE로 변경된 경우 변경 후에 획득한 공유 잠금이 이제 트랜잭션 끝까지 유지됩니다.  
  
 저장 프로시저 또는 트리거에서 SET TRANSACTION ISOLATION LEVEL을 실행할 때 개체가 컨트롤을 반환하면 격리 수준은 개체 호출 시 수준으로 다시 설정됩니다. 예를 들어 일괄 처리에서 REPEATABLE READ를 설정한 다음 격리 수준을 SERIALIZABLE로 설정하는 저장 프로시저를 호출한 경우 저장 프로시저가 컨트롤을 일괄 처리로 반환하면 격리 수준 설정이 REPEATABLE READ로 되돌아갑니다.  
  
> [!NOTE]  
>  사용자 정의 함수와 CLR(공용 언어 런타임) 사용자 정의 유형은 SET TRANSACTION ISOLATION LEVEL을 실행할 수 없습니다. 그러나 테이블 힌트를 사용하여 격리 수준을 재정의할 수 있습니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
 sp_bindsession을 사용하여 두 세션을 바인딩하는 경우 각 세션은 해당 격리 수준 설정을 유지합니다. SET TRANSACTION ISOLATION LEVEL을 사용하여 한 세션의 격리 수준 설정을 변경해도 해당 세션에 바인딩된 다른 세션의 설정에는 영향을 주지 않습니다.  
  
 SET TRANSACTION ISOLATION LEVEL은 실행 시나 런타임에 적용되며 구문 분석 시에는 적용되지 않습니다.  
  
 힙의 최적화된 대량 로드 작업은 다음 격리 수준에서 실행되는 쿼리를 차단합니다.  
  
-   SNAPSHOT  
  
-   READ UNCOMMITTED  
  
-   행 버전 관리를 사용하는 READ COMMITTED  
  
 반대로 이러한 격리 수준에서 실행된 쿼리는 힙의 최적화된 대량 로드 작업을 차단합니다. 대량 로드 작업에 대한 자세한 내용은 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)를 참조하세요.  
  
 FILESTREAM 사용 데이터베이스는 다음 트랜잭션 격리 수준을 지원합니다.  
  
|격리 수준|Transact SQL 액세스|파일 시스템 액세스|  
|---------------------|-------------------------|------------------------|  
|커밋되지 않은 읽기|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|지원되지 않음|  
|커밋된 읽기|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|반복 읽기|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|지원되지 않음|  
|직렬화 가능|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|지원되지 않음|  
|커밋된 스냅숏 읽기|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|스냅숏|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
## <a name="examples"></a>예  
 다음 예에서는 세션에 대한 `TRANSACTION ISOLATION LEVEL`을 설정합니다. 이어지는 각 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 트랜잭션이 종료될 때까지 모든 공유 잠금을 보유합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;  
GO  
BEGIN TRANSACTION;  
GO  
SELECT *   
    FROM HumanResources.EmployeePayHistory;  
GO  
SELECT *   
    FROM HumanResources.Department;  
GO  
COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC USEROPTIONS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
