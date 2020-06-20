---
title: 메모리 액세스에 최적화 된 테이블의 트랜잭션에 대 한 재시도 논리 지침 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2a35c37-4449-49ee-8bba-928028f1de66
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3cebe052a91dbf414f63f82efdfca88c64faabd0
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932892"
---
# <a name="guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 트랜잭션에 대한 재시도 논리 지침
  메모리 최적화 테이블에 액세스하는 트랜잭션에서 발생하는 오류 조건이 있습니다.  
  
-   41302. 현재 트랜잭션이 시작된 이후에 업데이트된 레코드를 업데이트하려고 시도했습니다.  
  
-   41305. 반복 읽기 유효성 검사 실패로 인해 현재 트랜잭션을 커밋하지 못했습니다.  
  
-   41325. 직렬화 유효성 검사 실패로 인해 현재 트랜잭션을 커밋하지 못했습니다.  
  
-   41301. 현재 트랜잭션이 종속성을 갖고 있는 이전 트랜잭션이 중단되어 현재 트랜잭션을 더 이상 커밋할 수 없습니다.  
  
 이러한 오류의 일반적인 원인은 동시에 실행되는 트랜잭션 간의 간섭 때문입니다. 일반적인 수정 동작은 트랜잭션을 다시 시도하는 것입니다.  
  
 이러한 오류 조건에 대 한 자세한 내용은 메모리 액세스에 [최적화 된 테이블의 트랜잭션에서](../relational-databases/in-memory-oltp/memory-optimized-tables.md)충돌 검색, 유효성 검사 및 커밋 종속성 확인에 대 한 섹션을 참조 하세요.  
  
 교착 상태(오류 코드 1205)는 메모리 최적화 테이블에 대해 발생할 수 없습니다. 잠금은 메모리 최적화 테이블에 대해 사용되지 않습니다. 그러나 애플리케이션에 교착 상태에 대한 재시도 논리가 이미 포함되어 있는 경우에는 기존 논리를 확장하여 새 오류 코드를 포함할 수 있습니다.  
  
## <a name="considerations-for-retrying"></a>재시도 고려 사항  
 일반적으로 애플리케이션에서 트랜잭션 간 충돌이 발생하면 재시도 논리를 구현하여 이러한 충돌을 해결해야 합니다. 발생하는 충돌 횟수는 다음과 같은 여러 가지 요인에 따라 달라집니다.  
  
-   개별 행에 대한 경합. 동일한 행을 업데이트하려고 시도하는 트랜잭션 수가 증가할수록 충돌 가능성도 증가합니다.  
  
-   REPEATABLE READ 트랜잭션에서 읽는 행 수. 읽는 행이 많을수록 동시 트랜잭션이 이러한 행 중 일부를 업데이트할 가능성도 높아집니다. 따라서 반복 읽기 유효성 검사가 실패합니다.  
  
-   SERIALIZABLE 트랜잭션에서 사용하는 검색 범위의 크기. 검색 범위가 클수록 동시 트랜잭션이 가상 행을 제공할 가능성도 높아집니다. 따라서 직렬화 유효성 검사가 실패합니다.  
  
     애플리케이션이 재시도 논리를 필요로 하는 이러한 충돌을 피하는 것은 어렵습니다.  
  
> [!IMPORTANT]  
>  메모리 최적화 테이블에 액세스하는 읽기-쓰기 트랜잭션에는 재시도 논리가 필요합니다.  
  
### <a name="considerations-for-read-only-transactions-and-natively-compiled-stored-procedures"></a>읽기 전용 트랜잭션 및 고유하게 컴파일된 저장 프로시저에 대한 고려 사항  
 고유하게 컴파일된 저장 프로시저의 단일 실행을 처리하는 읽기 전용 트랜잭션에는 REPEATABLE READ 및 SERIALIZABLE 트랜잭션에 대한 유효성 검사가 필요하지 않습니다. 읽기 전용 트랜잭션이기 때문에 쓰기 충돌이 발생할 수 없습니다.  
  
 그러나 종속성 오류는 여전히 발생할 수 있습니다. 종속성 오류는 충돌로 인해 발생하는 오류보다 드물게 발생합니다. 따라서 대부분의 경우 고유하게 컴파일된 저장 프로시저의 단일 실행을 처리하는 읽기 전용 트랜잭션에는 특정 재시도 논리가 필요하지 않습니다.  
  
### <a name="considerations-for-read-only-transactions-and-cross-container-transactions"></a>읽기 전용 트랜잭션 및 크로스 컨테이너 트랜잭션에 대한 고려 사항  
 메모리 최적화 테이블이 모두 SNAPSHOT 격리에서 액세스되는 경우, 고유하게 컴파일된 저장 프로시저의 컨텍스트 밖에서 시작되는 컨텍스트인 읽기 전용 크로스 컨테이너 트랜잭션은 유효성 검사를 수행하지 않습니다. 그러나 메모리 최적화 테이블이 REPEATABLE READ 또는 SERIALIZABLE 격리에서 액세스되는 경우에는 커밋할 때 유효성 검사가 수행됩니다. 이 경우 재시도 논리가 필요할 수 있습니다.  
  
 자세한 내용은 [트랜잭션 격리 수준](../../2014/database-engine/transaction-isolation-levels.md)에서 크로스 컨테이너 트랜잭션에 대 한 섹션을 참조 하세요.  
  
## <a name="implementing-retry-logic"></a>재시도 논리 구현  
 메모리 최적화 테이블에 액세스하는 모든 트랜잭션과 마찬가지로 쓰기 충돌(오류 코드 41302) 또는 종속성 오류(오류 코드 41301)와 같은 잠재적인 오류를 처리하는 재시도 논리를 고려해야 합니다. 대부분의 애플리케이션에서 실패율은 낮지만 여전히 트랜잭션을 다시 시도하여 오류를 처리해야 합니다. 다음 두 가지의 재시도 논리 구현 방법이 있습니다.  
  
-   클라이언트 쪽 재시도. 클라이언트 쪽 재시도는 일반적인 경우 재시도 논리를 구현하는 기본 방법입니다. 클라이언트 애플리케이션은 트랜잭션에서 발생한 오류를 catch하여 트랜잭션을 다시 시도합니다. 기존 클라이언트 애플리케이션에 교착 상태를 처리하기 위한 재시도 논리가 포함된 경우 애플리케이션을 확장하여 새 오류 코드를 처리할 수 있습니다.  
  
-   래퍼 저장 프로시저 사용. 클라이언트는 고유하게 컴파일된 저장 프로시저를 호출하거나 트랜잭션을 실행하는 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)] 저장 프로시저를 호출합니다. 그런 다음 래퍼 프로시저는 try/catch 논리를 사용하여 오류를 catch하고 필요한 경우 프로시저 호출을 다시 시도합니다. 실패하기 전에 결과가 클라이언트에 반환될 수 있으며 클라이언트는 해당 결과를 삭제해야 할지 알 수 없습니다. 따라서 안전을 위해 클라이언트에 결과 집합을 반환하지 않는 고유하게 컴파일된 저장 프로시저가 포함된 이 메서드를 사용하는 것이 최선입니다.  
  
 재시도 논리는 [!INCLUDE[tsql](../includes/tsql-md.md)] 또는 중간 계층 애플리케이션 코드에서 구현할 수 있습니다.  
  
 재시도 논리를 고려해야 하는 두 가지 가능한 이유는 다음과 같습니다.  
  
-   클라이언트 애플리케이션에 사용자가 확장할 수 있는 1205와 같은 다른 오류 코드에 대한 재시도 논리가 포함되어 있습니다.  
  
-   충돌은 드물게 발생하므로 준비된 실행을 사용하여 엔드투엔드 대기 시간을 줄이는 것이 중요합니다. 고유 하 게 컴파일된 저장 프로시저를 직접 실행 하는 방법에 대 한 자세한 내용은 고유 하 게 [컴파일된 저장 프로시저](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)를 참조 하세요.  
  
 다음 예에서는 고유하게 컴파일된 저장 프로시저 또는 크로스 컨테이너 트랜잭션에 대한 호출이 포함된 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)] 저장 프로시저에 있는 재시도 논리를 보여 줍니다.  
  
```sql  
CREATE PROCEDURE usp_my_procedure @param1 type1, @param2 type2, ...  
AS  
BEGIN  
  -- number of retries - tune based on the workload  
  DECLARE @retry INT = 10  
  
  WHILE (@retry > 0)  
  BEGIN  
    BEGIN TRY  
  
      -- exec usp_my_native_proc @param1, @param2, ...  
  
      --       or  
  
      -- BEGIN TRANSACTION  
      --   ...  
      -- COMMIT TRANSACTION  
  
      SET @retry = 0  
    END TRY  
    BEGIN CATCH  
      SET @retry -= 1  
  
      -- the error number for deadlocks (1205) does not need to be included for   
      -- transactions that do not access disk-based tables  
      IF (@retry > 0 AND error_number() in (41302, 41305, 41325, 41301, 1205))  
      BEGIN  
        -- these error conditions are transaction dooming - rollback the transaction  
        -- this is not needed if the transaction spans a single native proc execution  
        --   as the native proc will simply rollback when an error is thrown   
        IF XACT_STATE() = -1  
          ROLLBACK TRANSACTION  
  
        -- use a delay if there is a high rate of write conflicts (41302)  
        --   length of delay should depend on the typical duration of conflicting transactions  
        -- WAITFOR DELAY '00:00:00.001'  
      END  
      ELSE  
      BEGIN  
        -- insert custom error handling for other error conditions here  
  
        -- throw if this is not a qualifying error condition  
        ;THROW  
      END  
    END CATCH  
  END  
END  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화 된 테이블의 트랜잭션 이해](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [메모리 액세스에 최적화 된 테이블의 트랜잭션](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [메모리 액세스에 최적화된 테이블의 트랜잭션 격리 수준에 대한 지침](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)  
  
  
