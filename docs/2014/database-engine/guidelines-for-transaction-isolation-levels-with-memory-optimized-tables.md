---
title: 메모리 최적화 테이블을 사용 하 여 트랜잭션 격리 수준에 대 한 지침 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e365e9ca-c34b-44ae-840c-10e599fa614f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aced288e62fefe46777993fd46130b8dd65e8d1b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510017"
---
# <a name="guidelines-for-transaction-isolation-levels-with-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 트랜잭션 격리 수준에 대한 지침
  대부분의 경우 트랜잭션 격리 수준을 지정해야 합니다. 메모리 최적화 테이블에 대한 트랜잭션 격리는 디스크 기반 테이블과 다릅니다.  
  
 트랜잭션 격리 수준을 지정하기 위한 요구 사항:  
  
-   트랜잭션 격리 수준은 고유하게 컴파일된 저장 프로시저의 콘텐츠를 구성하는 ATOMIC 블록에 대한 필수 옵션입니다.  
  
-   크로스 컨테이너 트랜잭션에서 격리 수준을 사용할 때 적용되는 제한 사항 때문에 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]에서 메모리 최적화 테이블을 사용할 때는 종종 테이블에 액세스하는 데 사용되는 격리 수준을 지정하는 테이블 힌트가 있어야 합니다. 격리 수준 힌트 및 크로스 컨테이너 트랜잭션에 대한 자세한 내용은 [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md)을 참조하십시오.  
  
-   원하는 트랜잭션 격리 수준을 명시적으로 선언해야 합니다. 트랜잭션에서 특정 행 또는 테이블의 격리를 보증하기 위해 잠금 힌트(예: XLOCK)를 사용할 수 없습니다.  
  
-   데이터베이스에 액세스하는 애플리케이션은 트랜잭션 실패 충돌, 위반 오류 및 커밋 종속성 오류로 인해 발생하는 오류를 처리하는 다시 시도 논리를 구현해야 합니다. 커밋 종속성 오류는 읽기 전용 트랜잭션에서도 발생할 수 있습니다.  
  
-   장기적으로 실행되는 트랜잭션은 메모리 최적화 테이블 사용을 피해야 합니다. 이러한 트랜잭션은 충돌 및 후속 트랜잭션 종료 가능성을 높입니다. 장기 실행 트랜잭션으로 인해 가비지 수집도 지연됩니다. 트랜잭션 실행 시간이 늘어날수록, 메모리 내 OLTP에서 최근에 삭제된 행 버전을 더 오래 유지하며, 이는 새 트랜잭션에 대한 조회 성능을 저하시킬 수 있습니다.  
  
 일반적으로 디스크 기반 테이블은 잠금과 차단을 사용하여 트랜잭션 격리를 처리합니다. 메모리 액세스에 최적화된 테이블은 다중 버전 관리 및 충돌 검색을 사용하여 격리를 보증합니다. 자세한 내용은 [Transactions in Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)의 충돌 검색, 유효성 검사 및 커밋 종속성 확인에 대한 섹션을 참조하십시오.  
  
 디스크 기반 테이블은 SNAPSHOT 및 READ_COMMITTED_SNAPSHOT 격리 수준을 사용한 다중 버전 관리를 허용합니다. 메모리 최적화 테이블의 경우 모든 격리 수준이 REPEATABLE READ 및 SERIALIZABLE을 비롯한 여러 버전을 기반으로 합니다.  
  
## <a name="types-of-transactions"></a>트랜잭션 유형  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 모든 쿼리는 트랜잭션의 컨텍스트에서 실행됩니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에는 다음과 같은 세 가지 유형의 트랜잭션이 있습니다.  
  
-   자동 커밋 트랜잭션. 세션에 활성 트랜잭션 컨텍스트가 없고 암시적 트랜잭션이 ON으로 설정되지 않은 경우 쿼리마다 고유한 트랜잭션 컨텍스트가 사용됩니다. 트랜잭션은 문 실행이 시작되면 시작되고 문 실행이 끝나면 완료됩니다.  
  
-   명시적 트랜잭션. 사용자는 명시적 BEGIN TRAN 또는 BEGIN ATOMIC을 통해 트랜잭션을 시작합니다. 트랜잭션은 해당 COMMIT 및 ROLLBACK 또는 END(ATOMIC 블록의 경우) 다음에 완료됩니다.  
  
-   암시적 트랜잭션. IMPLICIT_TRANSACTIONS 옵션이 ON으로 설정된 경우 활성 트랜잭션 컨텍스트가 없는 상태에서 사용자가 문을 실행할 때마다 트랜잭션이 암시적으로 시작됩니다. 트랜잭션은 명시적 COMMIT 및 ROLLBACK을 통해 완료됩니다.  
  
## <a name="baseline-read-committed-isolation"></a>기준 READ COMMITTED 격리  
 READ COMMITTED는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 기본 격리 수준입니다.  
  
 격리 수준 READ COMMITTED를 사용하면 트랜잭션은 현재 트랜잭션 외부의 변경 내용에서 커밋되지 않은 데이터를 확인하지 않습니다. 즉, 트랜잭션은 데이터베이스에 커밋되었거나 현재 트랜잭션에 의해 변경된 데이터만 읽습니다.  
  
 메모리 최적화 테이블에 대해 지원되는 모든 격리 수준은 커밋된 읽기 보증을 제공합니다. 따라서 트랜잭션에 더 강력한 보증이 필요 없는 경우에는 메모리 최적화 테이블에 대해 지원되는 아무 격리 수준이나 사용할 수 있습니다. SNAPSHOT은 다른 어떤 격리 수준보다 가장 적은 시스템 리소스를 사용합니다.  
  
 SNAPSHOT 격리 수준(메모리 최적화 테이블에 대해 지원되는 가장 낮은 격리 수준)이 제공하는 보증에는 READ COMMITTED의 보증이 포함됩니다. 트랜잭션의 각 문은 동일한 버전의 데이터베이스를 읽습니다. 트랜잭션에서 읽은 모든 행이 데이터베이스에 커밋될 뿐 아니라 모든 읽기 작업이 동일한 트랜잭션 집합에 의해 변경된 내용 집합을 참조합니다.  
  
 **지침**: READ COMMITTED 격리 보증만 필요한 경우 고유하게 컴파일된 저장 프로시저에 대해 SNAPSHOT 격리를 사용하여 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]을 통해 메모리 최적화 테이블에 액세스하세요.  
  
 자동 커밋 트랜잭션의 경우 READ COMMITTED 격리 수준이 메모리 최적화 테이블에 대한 SNAPSHOT에 암시적으로 매핑됩니다. 따라서 TRANSACTION ISOLATION LEVEL 세션 설정이 READ COMMITTED로 설정된 경우 메모리 최적화 테이블에 액세스할 때 테이블 힌트를 통해 격리 수준을 지정할 필요가 없습니다.  
  
 다음 자동 커밋 트랜잭션 예에서는 임시 일괄 처리의 일부로 메모리 최적화 테이블 Customers와 일반 테이블 [Order History] 간의 조인을 보여 줍니다.  
  
```tsql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
SELECT *   
FROM dbo.Customers AS c   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id = oh.customer_id;  
```  
  
 다음 명시적 또는 암시적 트랜잭션 예에서는 이번에는 명시적 사용자 트랜잭션에서 수행된다는 점만 다르고 위와 동일한 조인을 보여 줍니다. 테이블 힌트 WITH (SNAPSHOT)에 표시된 대로 메모리 최적화 테이블 Customers는 스냅숏 격리에서 액세스되고 일반 테이블 [Order History]는 커밋된 읽기 격리에서 액세스됩니다.  
  
```tsql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
BEGIN TRAN  
SELECT * FROM dbo.Customers c with (SNAPSHOT)   
LEFT JOIN dbo.[Order History] oh   
    ON c.customer_id=oh.customer_id  
...  
COMMIT  
```  
  
### <a name="operational-differences"></a>작동 차이  
 커밋된 읽기 보증 외에도 디스크 기반 테이블을 사용하는 애플리케이션에서 사용할 수 있는 두 가지 중요한 구현 정보가 있습니다. READ COMMITTED를 사용하여 액세스하는 디스크 기반 테이블을 SNAPSHOT 격리를 사용하여 액세스하는 메모리 최적화 테이블로 변환할 때는 다음 사항에 주의하세요.  
  
-   디스크 기반 테이블에 대해 READ COMMITTED 격리 수준(READ_COMMITTED_SNAPSHOT이 OFF라고 가정)을 구현할 때는 판독기와 기록기가 충돌하는 것을 방지하기 위해 잠금이 사용됩니다. 기록기가 행을 업데이트하기 시작하면 잠금이 설정되고 트랜잭션이 커밋될 때까지 잠금이 해제되지 않습니다. 모든 읽기 작업은 차단되고 쓰기 트랜잭션이 커밋될 때까지 대기합니다.  
  
     일부 애플리케이션의 경우 판독기는 항상 기록기가 커밋할 때까지 기다린다고 가정할 수도 있습니다. 특히 애플리케이션 계층에서 두 트랜잭션 간의 동기화가 있을 경우 그렇습니다.  
  
     **지침:** 응용 프로그램은 차단 동작을 사용할 수 없습니다. 동시 트랜잭션 간의 동기화 해야 하는 응용 프로그램을 하는 경우 이러한 논리 응용 프로그램 계층 또는 데이터베이스 계층을 통해 구현할 수 [sp_getapplock &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getapplock-transact-sql)합니다.  
  
-   READ COMMITTED 격리를 사용하는 트랜잭션에서는 각 문이 데이터베이스에 있는 행의 최신 버전을 참조합니다. 따라서 이후 문은 데이터베이스 상태에 대한 변경 내용을 참조합니다.  
  
     이 가정을 사용하는 애플리케이션 패턴의 예로 새 행을 찾을 때까지 WHILE 루프를 사용하여 테이블을 폴링하는 경우를 들 수 있습니다. 루프가 반복될 때마다 쿼리는 데이터베이스에 있는 최신 업데이트를 참조합니다.  
  
     **지침:** 응용 프로그램에서 테이블에 쓰여진 최신 행을 가져오기 위해 메모리 최적화 테이블을 폴링해야 하는 경우 폴링 루프를 트랜잭션 범위 밖으로 이동합니다.  
  
     다음은 이 가정을 사용하는 애플리케이션 패턴의 예입니다. 새 행을 찾을 때까지 WHILE 루트를 사용하여 테이블을 폴링합니다. 루프가 반복될 때마다 쿼리는 데이터베이스에 있는 최신 업데이트에 액세스합니다.  
  
 다음 스크립트 예에서는 행을 찾을 때까지 t1 테이블을 폴링합니다. 그런 다음 추가 처리를 위해 테이블에서 행 하나를 제거합니다.  
  
 폴링 논리는 스냅숏 격리를 사용하여 t1 테이블에 액세스하므로 트랜잭션 범위 밖에 있어야 합니다. 트랜잭션 범위 내에서 폴링 논리를 사용하면 장기 실행 트랜잭션이 만들어지는데, 이는 좋은 방법이 아닙니다.  
  
```tsql  
-- poll table  
WHILE NOT EXISTS (SELECT 1 FROM dbo.t1)  
BEGIN   
  -- if empty, wait and poll again  
  WAITFOR DELAY '00:00:01'  
END  
  
BEGIN TRANSACTION  
  DECLARE @id int  
  SELECT TOP 1 @id=id FROM dbo.t1 WITH (SNAPSHOT)  
  DELETE FROM dbo.t1 WITH (SNAPSHOT) WHERE id=@id  
  
  -- insert processing based on @id  
COMMIT  
```  
  
## <a name="locking-table-hints"></a>테이블 잠금 힌트  
 잠금 힌트 ([테이블 힌트 &#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)) 할 HOLDLOCK과 XLOCK 디스크 기반 테이블을 사용 하 여 사용할 수와 같은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 지정된 된 격리 수준에 필요한 것 보다 많은 잠금을 수행 합니다.  
  
 메모리 액세스에 최적화된 테이블은 잠금을 사용하지 않습니다. REPEATABLE READ와 SERIALIZABLE 같은 더 높은 격리 수준을 사용하여 원하는 보증을 선언할 수 있습니다.  
  
 잠금 힌트는 지원되지 않습니다. 대신 트랜잭션 격리 수준을 통해 필요한 보증을 선언하십시오. ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 메모리 최적화 테이블을 잠그지 않기 때문에 NOLOCK이 지원됩니다. 디스크 기반 테이블과 달리 NOLOCK은 메모리 최적화 테이블에 대한 READ UNCOMMITTED 동작을 의미하지는 않습니다.)  
  
## <a name="see-also"></a>관련 항목  
 [메모리 최적화 테이블의 트랜잭션 이해](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [메모리 최적화 테이블의 트랜잭션에 대 한 재시도 논리에 대 한 지침](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)   
 [트랜잭션 격리 수준](../../2014/database-engine/transaction-isolation-levels.md)  
  
  
