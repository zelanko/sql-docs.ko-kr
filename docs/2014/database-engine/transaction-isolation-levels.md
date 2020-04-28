---
title: 트랜잭션 격리 수준 메모리 액세스에 최적화 된 테이블 | Microsoft Docs
ms.custom: seo-dt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 8a6a82bf-273c-40ab-a101-46bd3615db8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eea34b8ad278447d9e9085d99acb8500d14d5e7a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73637784"
---
# <a name="transaction-isolation-levels-in-memory-optimized-tables"></a>메모리 액세스에 최적화 된 테이블의 트랜잭션 격리 수준

  다음 격리 수준은 메모리 최적화 테이블에 액세스하는 트랜잭션에 대해 지원됩니다.  
  
-   SNAPSHOT  
  
-   REPEATABLE READ  
  
-   직렬화 가능  
  
-   READ COMMITTED  
  
 트랜잭션 격리 수준은 고유하게 컴파일된 저장 프로시저의 원자 블록의 일부로 지정할 수 있습니다. 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)를 참조하세요. 메모리 최적화 테이블을 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]에서 액세스하면 테이블 수준 힌트를 사용하여 격리 수준을 지정할 수 있습니다.  
  
 고유하게 컴파일된 저장 프로시저를 정의할 때는 트랜잭션 격리 수준을 지정해야 합니다. 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]의 사용자 트랜잭션에서 메모리 최적화 테이블에 액세스할 때는 테이블 힌트에서 격리 수준을 지정해야 합니다. 자세한 내용은 [메모리 최적화 테이블을 사용 하는 트랜잭션 격리 수준에 대 한 지침](../relational-databases/in-memory-oltp/memory-optimized-tables.md)을 참조 하세요.  
  
 자동 커밋 트랜잭션이 있는 메모리 최적화 테이블에는 격리 수준 READ COMMITTED가 지원됩니다. READ COMMITTED는 사용자 트랜잭션 또는 원자 블록에서 유효하지 않습니다. READ COMMITTED는 명시적 또는 암시적 사용자 트랜잭션에서 지원되지 않습니다. 격리 수준 READ_COMMITTED_SNAPSHOT은 자동 커밋 트랜잭션 기능이 있는 메모리 최적화 테이블의 경우 및 쿼리가 디스크 기반 테이블에 액세스하지 않는 경우에만 지원됩니다. 뿐만 아니라 SNAPSHOT 격리로 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]을 사용하여 시작된 트랜잭션은 메모리 최적화 테이블에 액세스할 수 없습니다. REPEATABLE READ 또는 SERIALIZABLE 격리와 함께 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]을 사용하는 트랜잭션은 SNAPSHOT 격리를 사용하여 메모리 최적화 테이블에 액세스해야 합니다. 이 시나리오에 대 한 자세한 내용은 [크로스 컨테이너 트랜잭션](cross-container-transactions.md)을 참조 하십시오.  
  
 READ COMMITTED는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 기본 격리 수준입니다. 세션의 격리 수준이 READ COMMITED 이하인 경우 다음 작업 중 하나를 수행할 수 있습니다.  
  
-   메모리 최적화 테이블에 액세스하는 데 보다 높은 격리 수준 힌트를 명시적으로 사용합니다(예: WITH (SNAPSHOT)).  
  
-   메모리 최적화 테이블에 대한 격리 수준을 SNAPSHOT(메모리 최적화 모든 테이블에 대한 WITH(SNAPSHOT) 힌트를 포함한 것)으로 설정할 `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT` 설정 옵션을 지정합니다. 에 대 한 `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`자세한 내용은 [ALTER database SET Options &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)를 참조 하세요.  
  
 또는 세션의 격리 수준이 READ COMMITTED인 경우 자동 커밋 트랜잭션을 사용할 수 있습니다.  
  
 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]에서 시작된 SNAPSHOT 트랜잭션은 메모리 최적화 테이블에 액세스할 수 없습니다.  
  
 메모리 최적화 테이블에 지원되는 트랜잭션 격리 수준은 디스크 기반 테이블과 동일한 논리적 보증을 제공합니다. 격리 수준 보증을 제공하는 데 사용되는 메커니즘은 다릅니다.  
  
 디스크 기반 테이블의 경우 대부분의 격리 수준 보증은 차단을 통해 충돌을 방지하는 잠금을 사용하여 구현됩니다. 메모리 최적화 테이블의 경우 잠금 필요성을 방지하는 충돌 감지 메커니즘을 사용하여 보장이 시행됩니다. 예외는 디스크 기반 테이블의 SNAPSHOT 격리입니다. 이는 충돌 감지 메커니즘을 사용하여 메모리 최적화 테이블에서 SNAPSHOT 격리에 유사하게 구현됩니다.  
  
 SNAPSHOT  
 이 격리 수준은 트랜잭션의 문이 읽은 데이터가 트랜잭션 시작 시와 트랜잭션별로 데이터 버전의 일관성이 유지되도록 지정합니다. 트랜잭션은 시작되기 전에 커밋된 데이터 수정 내용만 인식할 수 있습니다. 현재 트랜잭션이 시작된 후 다른 트랜잭션에서 수정한 데이터는 현재 트랜잭션에서 실행되는 문에 표시되지 않습니다. 트랜잭션의 문이 트랜잭션 시작 당시 커밋된 데이터의 스냅샷을 가져옵니다.  
  
 쓰기 작업(업데이트, 삽입 및 삭제)은 항상 다른 트랜잭션에서 완전히 격리됩니다. 따라서 SNAPSHOT 트랜잭션의 쓰기 작업은 다른 트랜잭션의 쓰기 작업과 충돌할 수 있습니다. 현재 트랜잭션이 시작된 후에 커밋된 다른 트랜잭션에 의해 업데이트되거나 삭제된 행을 현재 트랜잭션이 업데이트하거나 삭제하려고 시도하면 트랜잭션은 다음 오류 메시지가 표시되면서 종료됩니다.  
  
 오류 41302. 현재 트랜잭션에서 이 트랜잭션이 시작된 이후로 업데이트된 레코드를 업데이트하려고 시도했습니다. 트랜잭션이 중단되었습니다.  
  
 현재 트랜잭션 전에 커밋된 다른 트랜잭션에서 삽입한 행과 같은 기본 키 값을 갖는 행을 현재 트랜잭션이 삽입하려고 시도하면 다음 오류 메시지와 함께 커밋이 실패합니다.  
  
 오류 41325. 직렬화 유효성 검사 실패로 인해 현재 트랜잭션을 커밋하지 못했습니다.  
  
 트랜잭션이 커밋하기 전에 트랜잭션이 삭제된 테이블에 쓰는 경우 트랜잭션은 다음 오류 메시지와 함께 종료됩니다.  
  
 오류 41305. 반복 읽기 유효성 검사 실패로 인해 현재 트랜잭션을 커밋하지 못했습니다.  
  
 REPEATABLE READ  
 이 격리 수준은 SNAPSHOT 격리 수준에 의해 지정된 보증을 포함합니다. 또한 REPEATABLE READ는 트랜잭션이 읽는 행의 경우 트랜잭션 커밋 당시 행이 다른 트랜잭션에 의해 변경되지 않았음을 보증합니다. 트랜잭션의 모든 읽기 작업은 트랜잭션이 끝날 때가지 반복이 가능합니다.  
  
 현재 트랜잭션 이전에 커밋된 다른 트랜잭션에 의해 업데이트된 행을 현재 트랜잭션이 읽은 경우 커밋은 다음 오류 메시지와 함께 실패합니다.  
  
 오류 41305. 반복 읽기 유효성 검사 실패로 인해 현재 트랜잭션을 커밋하지 못했습니다.  
  
 직렬화 가능  
 이 격리 수준은 REPEATABLE READ를 통해 지정된 보증을 포함합니다. 스냅샷과 트랜잭션 종료 사이에 가상 행이 나타나지 않았습니다. 가상 행은 선택, 업데이트 또는 삭제의 필터 조건과 일치합니다.  
  
 트랜잭션은 동시 트랜잭션이 없는 것처럼 실행됩니다. 모든 작업은 거의 단일 직렬화 포인트(커밋 시간)에서 발생합니다.  
  
 이러한 보증을 위반하는 경우 트랜잭션은 다음 오류 메시지와 함께 커밋에 실패합니다.  
  
 오류 41325. 직렬화 유효성 검사 실패로 인해 현재 트랜잭션을 커밋하지 못했습니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화 된 테이블의 트랜잭션 이해](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [메모리 액세스에 최적화 된 테이블이 있는 트랜잭션 격리 수준에 대 한 지침](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [메모리 액세스에 최적화된 테이블의 트랜잭션에 대한 재시도 논리 지침](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
