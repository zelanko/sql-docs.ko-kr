---
title: REVERT (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REVERT_TSQL
- REVERT
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- context switching [SQL Server], reverting
- reverting execution context
- REVERT WITH COOKIE statement
- execution context [SQL Server]
- COOKIE clause
ms.assetid: 4688b17a-dfd1-4f03-8db4-273a401f879f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3350f92afbb6d6ed0278a9ae41ee25f5ed4096b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="revert-transact-sql"></a>REVERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  실행 컨텍스트를 마지막 EXECUTE AS 문의 호출자로 다시 전환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
REVERT  
    [ WITH COOKIE = @varbinary_variable ]  
```  
  
## <a name="arguments"></a>인수  
 WITH COOKIE = @*varbinary_variable*  
 해당에서 작성 된 쿠키 지정 [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) 독립 실행형 문입니다. *@varbinary_variable***varbinary(100)**합니다.  
  
## <a name="remarks"></a>주의  
 REVERT는 저장 프로시저 또는 사용자 정의 함수 같은 모듈 내에서 지정하거나 독립 실행형 문으로 지정할 수 있습니다. 모듈 내에서 지정하면 REVERT는 모듈에 정의된 EXECUTE AS 문에만 적용할 수 있습니다. 예를 들어 다음 저장 프로시저는 `EXECUTE AS` 문과 `REVERT` 문을 차례로 실행합니다.  
  
```  
CREATE PROCEDURE dbo.usp_myproc   
  WITH EXECUTE AS CALLER  
AS   
    SELECT SUSER_NAME(), USER_NAME();  
    EXECUTE AS USER = 'guest';  
    SELECT SUSER_NAME(), USER_NAME();  
    REVERT;  
    SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
 저장 프로시저가 실행되는 세션에서 실행 컨텍스트는 다음 예와 같이 `login1`로 명시적으로 변경된다고 가정합니다.  
  
```  
  -- Sets the execution context of the session to 'login1'.  
EXECUTE AS LOGIN = 'login1';  
GO  
EXECUTE dbo.usp_myproc;   
```  
  
 `REVERT` 문 내에 정의 된 `usp_myproc` 모듈 내에서 설정 실행 컨텍스트를 전환 하지만 모듈 외부에 설정한 실행 컨텍스트는 영향을 주지 않습니다. 즉, 세션에 설정된 실행 컨텍스트가 `login1`로 유지됩니다.  
  
 독립 실행형 문으로 지정하면 REVERT는 일괄 처리나 세션 내에 정의된 EXECUTE AS 문에 적용됩니다. 해당 EXECUTE AS 문에 WITH NO REVERT 절이 있으면 REVERT가 아무런 영향을 주지 않습니다. 이 경우 실행 컨텍스트는 세션이 삭제될 때까지 계속 적용됩니다.  
  
## <a name="using-revert-with-cookie"></a>REVERT WITH COOKIE 사용  
 EXECUTE 문에 세션의 실행 컨텍스트를 설정 하는 데 사용 되는 선택적 절인 WITH NO REVERT COOKIE 포함할 수 있습니다 = @*varbinary_variabl*e입니다. 이 문이 실행 되는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿠키를 @ 전달*varbinary_variabl*e입니다. 설정한 실행 컨텍스트는 문 수 경우에 되돌릴를 이전 컨텍스트로 호출 REVERT WITH COOKIE = @*varbinary_variable* 문에 올바른 포함  *@varbinary_variable*  값입니다.  
  
 이 메커니즘은 연결 풀링을 사용하는 환경에 유용합니다. 연결 풀링은 여러 일반 사용자가 응용 프로그램에서 다시 사용할 수 있도록 데이터베이스 연결 그룹을 유지 관리하는 것입니다. 에 전달 된 값  *@varbinary_variable*  EXECUTE 호출자 에게만 알려지므로 호출자 (이 경우 응용 프로그램)에서 문으로 호출자에 게 최종 사용자가 자신이 설정한 실행 컨텍스트를 변경할 수 없습니다 보장할 수 응용 프로그램을 호출 합니다. 실행 컨텍스트가 되돌려지면 응용 프로그램에서 컨텍스트를 다른 보안 주체로 전환할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 사용 권한이 필요 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-execute-as-and-revert-to-switch-context"></a>1. EXECUTE AS 및 REVERT를 사용하여 컨텍스트 전환  
 다음 예에서는 여러 보안 주체를 사용하여 컨텍스트 실행 스택을 만듭니다. 그런 다음 REVERT 문을 사용하여 실행 컨텍스트를 이전 호출자로 다시 설정합니다. REVERT 문은 실행 컨텍스트가 원래 호출자로 설정될 때까지 스택 위로 이동하면서 여러 번 실행됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create two temporary principals.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
-- Give IMPERSONATE permissions on user2 to user1  
-- so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
-- Verify that the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
-- Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1, and login2.  
-- The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
-- Remove the temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>2. WITH COOKIE 절 사용  
 다음 예제에서는 지정된 된 사용자에 세션의 실행 컨텍스트를 설정 하 고 지정 WITH NO REVERT COOKIE = @*varbinary_variabl*절. 컨텍스트를 호출자로 되돌리려면 `REVERT` 문에 `@cookie` 문의 `EXECUTE AS` 변수로 전달되는 값을 지정해야 합니다. 이 예를 실행하려면 예 1에서 생성된 `login1` 로그인 및 `user1` 사용자가 있어야 합니다.  
  
```  
DECLARE @cookie varbinary(100);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie somewhere safe in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(100);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [실행 AS &#40; Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SUSER_NAME &#40; Transact SQL &#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [USER_NAME &#40; Transact SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
  
