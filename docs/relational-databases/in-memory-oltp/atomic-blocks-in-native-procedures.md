---
title: Atomic 블록 | Microsoft 문서
description: ANSI SQL 표준의 일부인 BEGIN ATOMIC에 대해 알아봅니다. SQL Server는 기본 프로시저의 Atomic 블록을 지원합니다.
ms.custom: ''
ms.date: 10/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 40e0e749-260c-4cfc-a848-444d30c09d85
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e92f73b4f8790c80cf0ac4e790a0587593ac75e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537731"
---
# <a name="atomic-blocks-in-native-procedures"></a>기본 프로시저의 Atomic 블록
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **BEGIN ATOMIC** 은 ANSI SQL 표준의 일부입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 고유하게 컴파일된 저장 프로시저와 고유하게 컴파일된 스칼라 사용자 정의 함수에 대해 최상위 수준에서 Atomic 블록을 지원합니다. 이러한 함수에 대한 자세한 내용은 [메모리 내 OLTP에 대한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)를 참조하세요.  
  
-   고유하게 컴파일된 모든 저장 프로시저에는 항상 하나의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 블록이 포함됩니다. 이것이 ATOMIC 블록입니다.  
  
-   고유하지 않은 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저 및 임시 일괄 처리는 ATOMIC 블록을 지원하지 않습니다.  
  
 ATOMIC 블록은 트랜잭션 내에서 하나의 큰 단위로 실행됩니다. 블록의 모든 문이 성공하거나 전체 블록이 블록 시작 시 만들어진 저장점으로 롤백됩니다. 또한 세션 설정이 ATOMIC 블록에 대해 고정됩니다. 세션에서 동일한 ATOMIC 블록을 여러 가지 다른 설정으로 실행하면 현재 세션 설정과 관계없이 같은 동작이 발생합니다.  
  
## <a name="transactions-and-error-handling"></a>트랜잭션 및 오류 처리  
 세션에 트랜잭션이 이미 있는 경우( **BEGIN TRANSACTION** 문과 트랜잭션을 실행한 일괄 처리가 활성 상태로 유지되므로) ATOMIC 블록을 시작하면 트랜잭션에서 저장점을 만듭니다. 예외가 발생하지 않고 블록이 종료되면 블록 커밋에 대한 새 저장점이 만들어지지만 세션 수준에서 트랜잭션이 커밋되어야 트랜잭션이 커밋됩니다. 블록에서 예외가 발생하면 블록의 효과는 롤백되지만 예외로 인해 트랜잭션이 실패하지 않으면 세션 수준의 트랜잭션이 진행됩니다. 예를 들어, 쓰기 충돌로 인해 트랜잭션이 실패하지만 쓰기 충돌이 형식 캐스팅 오류는 아닙니다.  
  
 세션에 활성 트랜잭션이 없는 경우 **BEGIN ATOMIC** 은 새 트랜잭션을 시작합니다. 블록 범위 밖에서 예외가 발생하지 않는다면 트랜잭션은 블록 끝에서 커밋됩니다. 블록에서 예외가 발생하면(예외가 catch되지 않고 블록 내에서 처리됨) 트랜잭션이 롤백됩니다. 단일 ATOMIC 블록에 걸쳐 있는 트랜잭션(고유하게 컴파일된 단일 저장 프로시저)의 경우 **BEGIN TRANSACTION** 및 **COMMIT** 또는 **ROLLBACK** 문을 명시적으로 작성할 필요가 없습니다.  
  
 고유하게 컴파일된 저장 프로시저는 오류 처리를 위해 **TRY**, **CATCH**및 **THROW** 구문을 지원합니다. **RAISERROR** 은 지원되지 않습니다.  
  
 다음 예에서는 ATOMIC 블록 및 고유하게 컴파일된 저장 프로시저에 대한 오류 처리 동작을 설명합니다.  
  
```sql  
-- sample table  
CREATE TABLE dbo.t1 (  
  c1 int not null primary key nonclustered  
)  
WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- sample proc that inserts 2 rows  
CREATE PROCEDURE dbo.usp_t1 @v1 bigint not null, @v2 bigint not null  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC  
WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english', DELAYED_DURABILITY = ON)  
  
  INSERT dbo.t1 VALUES (@v1)  
  INSERT dbo.t1 VALUES (@v2)  
  
END  
GO  
  
-- insert two rows  
EXEC dbo.usp_t1 1, 2  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify the rows 1 and 2 were committed  
SELECT c1 FROM dbo.t1  
GO  
  
-- execute proc with arithmetic overflow  
EXEC dbo.usp_t1 3, 4444444444444  
GO  
-- expected error message:  
-- Msg 8115, Level 16, State 0, Procedure usp_t1  
-- Arithmetic overflow error converting bigint to data type int.  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 was not committed; usp_t1 has been rolled back  
SELECT c1 FROM dbo.t1  
GO  
  
-- start a new transaction  
BEGIN TRANSACTION  
  -- insert rows 3 and 4  
  EXEC dbo.usp_t1 3, 4  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify the rows 3 and 4 were inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
  -- catch the arithmetic overflow error  
  BEGIN TRY  
    EXEC dbo.usp_t1 5, 4444444444444  
  END TRY  
  BEGIN CATCH  
    PRINT N'Error occurred: ' + error_message()  
  END CATCH  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify rows 3 and 4 are still in the table, and row 5 has not been inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
COMMIT  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 and 4 has been committed  
SELECT c1 FROM dbo.t1  
ORDER BY c1  
GO  
```  
  
 메모리 최적화 테이블에 대한 다음 오류 메시지가 발생하면 트랜잭션이 실패합니다. Atomic 블록 범위 내에서 10772, 41301, 41302, 41305, 41325, 41332, 41333 및 41839 오류가 발생하면 트랜잭션이 중단됩니다.  
  
## <a name="session-settings"></a>세션 설정  
 저장 프로시저가 컴파일되면 ATOMIC 블록의 세션 설정은 고정됩니다. 설정은 **BEGIN ATOMIC** 으로 지정할 수도 있고 같은 값으로 항상 고정할 수도 있습니다.  
  
 **BEGIN ATOMIC**에는 다음 옵션이 필요합니다.  
  
|필요한 설정|Description|  
|----------------------|-----------------|  
|**TRANSACTION ISOLATION LEVEL**|지원되는 값은 **SNAPSHOT**, **REPEATABLEREAD**및 **SERIALIZABLE**입니다.|  
|**LANGUAGE**|날짜 및 시간 형식과 시스템 메시지를 결정합니다. [sys.syslanguages&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)의 모든 언어와 별칭이 지원됩니다.|  
  
 다음 설정은 선택 사항입니다.  
  
|선택적 설정|Description|  
|----------------------|-----------------|  
|**DATEFORMAT**|모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 형식이 지원됩니다. 지정되면 **DATEFORMAT** 에서 **LANGUAGE**와 관련된 기본 날짜 형식을 재정의합니다.|  
|**DATEFIRST**|지정되면 **DATEFIRST** 에서 **LANGUAGE**와 관련된 기본값을 재정의합니다.|  
|**DELAYED_DURABILITY**|지원되는 값은 **OFF** 및 **ON**입니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션은 완전 내구성이 있는(기본값) 커밋 또는 지연된 내구성이 있는 커밋을 수행할 수 있습니다. 자세한 내용은 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md)를 참조하세요.|  
  
 다음 SET 옵션은 고유하게 컴파일된 모든 저장 프로시저의 모든 ATOMIC 블록에 대해 동일한 시스템 기본값을 가집니다.  
  
|SET 옵션|ATOMIC 블록의 시스템 기본값|  
|----------------|--------------------------------------|  
|ANSI_NULLS|켜기|  
|ANSI_PADDING|켜기|  
|ANSI_WARNING|켜기|  
|ARITHABORT|켜기|  
|ARITHIGNORE|OFF|  
|CONCAT_NULL_YIELDS_NULL|켜기|  
|IDENTITY_INSERT|OFF|  
|NOCOUNT|켜기|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|켜기|  
|ROWCOUNT|0|  
|TEXTSIZE|0|  
|XACT_ABORT|OFF<br /><br /> catch되지 않는 예외는 ATOMIC 블록을 롤백시키지만 오류로 인해 트랜잭션이 실패하지 않는다면 트랜잭션이 중단되지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
