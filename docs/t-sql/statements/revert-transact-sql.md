---
title: REVERT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2105b03f64ecc2e0357e5a06f0d7cb2c18fb69b0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72252179"
---
# <a name="revert-transact-sql"></a>REVERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  실행 컨텍스트를 마지막 EXECUTE AS 문의 호출자로 다시 전환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
REVERT  
    [ WITH COOKIE = @varbinary_variable ]  
```  
  
## <a name="arguments"></a>인수  
 WITH COOKIE = @*varbinary_variable*  
 해당되는 [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) 독립 실행형 문에 생성된 쿠키를 지정합니다. *\@varbinary_variable*은 **varbinary(100)** 입니다.  
  
## <a name="remarks"></a>설명  
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
  
 `REVERT` 내에 정의된 문`usp_myproc`은 모듈 내에 설정된 실행 컨텍스트를 전환하지만 모듈 외부에 설정된 실행 컨텍스트에는 영향을 주지 않습니다. 즉, 세션에 설정된 실행 컨텍스트가 `login1`로 유지됩니다.  
  
 독립 실행형 문으로 지정하면 REVERT는 일괄 처리나 세션 내에 정의된 EXECUTE AS 문에 적용됩니다. 해당 EXECUTE AS 문에 WITH NO REVERT 절이 있으면 REVERT가 아무런 영향을 주지 않습니다. 이 경우 실행 컨텍스트는 세션이 삭제될 때까지 계속 적용됩니다.  
  
## <a name="using-revert-with-cookie"></a>REVERT WITH COOKIE 사용  
 세션의 실행 컨텍스트를 설정하는 데 사용되는 EXECUTE AS 문에는 선택적 절인 WITH NO REVERT COOKIE = @*varbinary_variable*이 포함됩니다. 이 문이 실행되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 쿠키를 @*varbinary_variable*에 전달합니다. 호출하는 REVERT WITH COOKIE = @*varbinary_variable* 문에 올바른 *\@varbinary_variable* 값이 포함되어 있는 경우에만 해당 명령문으로 설정된 실행 컨텍스트를 이전 컨텍스트로 되돌릴 수 있습니다.  
  
 이 메커니즘은 연결 풀링을 사용하는 환경에 유용합니다. 연결 풀링은 여러 일반 사용자가 애플리케이션에서 다시 사용할 수 있도록 데이터베이스 연결 그룹을 유지 관리하는 것입니다. *\@varbinary_variable*에 전달된 값이 EXECUTE AS 문의 호출자(이 경우 애플리케이션)에게만 알려지므로 호출자는 자신이 설정한 실행 컨텍스트를 애플리케이션을 호출하는 일반 사용자가 변경할 수 없도록 할 수 있습니다. 실행 컨텍스트가 되돌려지면 애플리케이션에서 컨텍스트를 다른 보안 주체로 전환할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 사용 권한이 필요 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-execute-as-and-revert-to-switch-context"></a>A. EXECUTE AS 및 REVERT를 사용하여 컨텍스트 전환  
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
  
### <a name="b-using-the-with-cookie-clause"></a>B. WITH COOKIE 절 사용  
 다음 예에서는 세션 실행 컨텍스트를 지정한 사용자로 설정하고 WITH NO REVERT COOKIE = @*varbinary_variable* 절을 지정합니다. 컨텍스트를 호출자로 되돌리려면 `REVERT` 문에 `@cookie` 문의 `EXECUTE AS` 변수로 전달되는 값을 지정해야 합니다. 이 예를 실행하려면 예 1에서 생성된 `login1` 로그인 및 `user1` 사용자가 있어야 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [EXECUTE AS&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
  
