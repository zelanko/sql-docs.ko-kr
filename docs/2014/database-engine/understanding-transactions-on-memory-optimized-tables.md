---
title: 메모리 최적화 테이블의 트랜잭션 이해 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 06075248-705e-4563-9371-b64cd609793c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4ceedcedae64bf2ec8f8ede0ccbb99350b979fd7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773383"
---
# <a name="understanding-transactions-on-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 트랜잭션 이해
  트랜잭션은 낙관적 동시 버전 동시성 제어의 형태를 사용하여 메모리 최적화 테이블에 액세스합니다. 즉, 데이터의 서로 다른 버전이 있습니다. 각 트랜잭션은 동시에 실행 중인 다른 트랜잭션에 독립적이면서 트랜잭션 측면에서 데이터베이스 자체의 일관된 버전에서 작동합니다. 뿐만 아니라 트랜잭션은 다른 동시 트랜잭션과 충돌이 없을 것이라는 낙관적 가정 하에서 작동합니다. 이렇게 하면 잠금을 사용할 필요가 없지만 시스템이 충돌을 감지하고 충돌하는 트랜잭션 중 하나를 종료해야 합니다. 충돌은 쓰기-쓰기 트랜잭션 및 읽기-쓰기 트랜잭션에 대해서만 발생할 수 있습니다. 쓰기-쓰기 충돌이 발생할 경우 쓰기 트랜잭션 하나가 종료됩니다.  
  
 메모리 최적화 테이블의 동시성 제어와 디스크 기반 테이블의 READ_COMMITTED_SNAPSHOT 및 SNAPSHOT 트랜잭션 격리 수준에 대한 동시성 제어 사이에는 유사성이 있습니다. (디스크 기반 테이블에 대 한 자세한 내용은 참조 하세요. [데이터베이스 엔진에서 행 버전 관리 기반 격리 수준](https://msdn.microsoft.com/library/ms177404\(v=sql.100\).aspx).)  
  
## <a name="topics-in-this-section"></a>이 섹션의 항목  
 메모리 최적화 테이블의 트랜잭션에 대한 이 섹션에는 다음 항목들이 포함됩니다.  
  
-   [메모리 액세스에 최적화된 테이블의 트랜잭션 격리 수준에 대한 지침](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
-   [메모리 액세스에 최적화된 테이블의 트랜잭션에 대한 재시도 논리 지침](guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
-   [메모리 액세스에 최적화된 테이블의 트랜잭션](transactions-in-memory-optimized-tables.md)  
  
-   [트랜잭션 격리 수준](transaction-isolation-levels.md)  
  
-   [크로스 컨테이너 트랜잭션](cross-container-transactions.md)  
  
 자세한 내용은 [트랜잭션 내구성 제어](../relational-databases/logs/control-transaction-durability.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 액세스에 최적화된 테이블](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
