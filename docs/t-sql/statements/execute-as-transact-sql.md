---
description: EXECUTE AS(Transact-SQL)
title: EXECUTE AS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EXECUTE AS
- EXECUTE_AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- WITH NO REVERT clause
- sessions [SQL Server], execution context
- EXECUTE AS
- execution context [SQL Server]
- switching execution context
ms.assetid: 613b8271-7f7d-4378-b7a2-5a7698551dbd
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions||=azure-sqldw-latest
ms.openlocfilehash: d263f8db7e95cbc5e961d5b4d3879ce53ce99d47
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91227333"
---
# <a name="execute-as-transact-sql"></a>EXECUTE AS(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  세션의 실행 컨텍스트를 설정합니다.  
  
 기본적으로 세션은 사용자가 로그인할 때 시작되고 로그오프할 때 종료됩니다. 세션 동안 이루어진 모든 작업에 대해 해당 사용자의 권한을 확인합니다. **EXECUTE AS** 문을 실행하면 지정한 로그인 또는 사용자 이름으로 세션의 실행 컨텍스트가 전환됩니다. 컨텍스트가 전환된 후 **EXECUTE AS** 문을 호출하는 사용자 대신 해당 계정에 대한 로그인 및 사용자 보안 토큰의 권한을 확인합니다. 기본적으로 사용자 또는 로그인 계정은 세션 또는 모듈이 실행되는 동안이나 컨텍스트 전환이 명시적으로 되돌려질 때까지 가장됩니다.  
  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
{ EXEC | EXECUTE } AS <context_specification>  
[;]  
  
<context_specification>::=  
{ LOGIN | USER } = 'name'  
    [ WITH { NO REVERT | COOKIE INTO @varbinary_variable } ]   
| CALLER  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 LOGIN  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 가장할 실행 컨텍스트를 로그인으로 지정합니다. 가장의 범위는 서버 수준입니다.  
  
> [!NOTE]  
>  이 옵션은 포함된 데이터베이스, SQL 데이터베이스 또는 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 사용할 수 없습니다.  
  
 USER  
 가장할 컨텍스트를 현재 데이터베이스의 사용자로 지정합니다. 가장의 범위는 현재 데이터베이스로 제한됩니다. 데이터베이스 사용자로 컨텍스트 전환 시 해당 사용자의 서버 수준 사용 권한은 상속되지 않습니다.  
  
> [!IMPORTANT]  
>  데이터베이스 사용자로의 컨텍스트 전환이 활성화되어 있는 동안 해당 데이터베이스 외부의 리소스에 액세스하려고 하면 문이 실패합니다. USE *database* 문, 분산 쿼리, 식별자가 3-4부분으로 구성된 다른 데이터베이스를 참조하는 쿼리 등이 여기에 해당됩니다.  
  
 '*name*' 유효한 사용자 또는 로그인 이름입니다. *name*은 **sysadmin** 고정 서버 역할의 멤버이거나 [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) 또는 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)에서 각각 보안 주체여야 합니다.  
  
 *name*에 지역 변수를 지정할 수 있습니다.  
  
 *name*은 단일 계정이어야 하고 그룹, 역할, 인증서, 키 또는 NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService, NT AUTHORITY\LocalSystem 등의 기본 제공 계정이 될 수 없습니다.  
  
 자세한 내용은 이 항목의 뒤에 나오는 [사용자 또는 로그인 이름 지정](#_user)을 참조하세요.  
  
 NO REVERT  
 컨텍스트 전환을 이전 컨텍스트로 되돌릴 수 없도록 지정합니다. **NO REVERT** 옵션은 임시 수준에서만 사용할 수 있습니다.  
  
 이전 컨텍스트로 되돌리는 방법은 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)를 참조하세요.  
  
 COOKIE INTO @*varbinary_variable*  
 호출 REVERT WITH COOKIE 문에 올바른 correct @*varbinary_variable* 값이 포함되어 있는 경우에만 실행 컨텍스트를 이전 컨텍스트로 되돌릴 수 있도록 지정합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]는 쿠키를 @*varbinary_variable*로 전달합니다. **COOKIE INTO** 옵션은 임시 수준에서만 사용할 수 있습니다.  
  
 @*varbinary_variable*은 **varbinary(8000)** 입니다.  
  
> [!NOTE]  
>  현재 쿠키 **OUTPUT** 매개 변수는 정확한 최대 길이인 **varbinary(8000)** 로 정의되어 있습니다. 그러나 현재 구현은 **varbinary(100)** 입니다. 애플리케이션은 **varbinary(8000)** 를 예약하여 후속 릴리스에서 쿠키 반환 크기가 늘어날 경우에도 애플리케이션이 제대로 작동할 수 있도록 해야 합니다.  
  
 CALLER  
 모듈 내에서 사용된 경우 모듈 내의 문이 모듈 호출자의 컨텍스트에서 실행되도록 지정합니다.
모듈 외부에서 사용된 경우에는 문이 아무런 동작도 수행하지 않습니다.
 > [!NOTE]  
>  [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 실행 컨텍스트의 변경은 다음 조건 중 하나가 발생할 때까지 유효합니다.  
  
-   다른 EXECUTE AS 문이 실행됩니다.  
  
-   REVERT 문이 실행됩니다.  
  
-   세션이 삭제됩니다.  
  
-   명령이 실행된 저장 프로시저 또는 트리거가 종료됩니다.  
  
여러 보안 주체에서 EXECUTE AS 문을 여러 번 호출하여 실행 컨텍스트 스택을 만들 수 있습니다. 호출 시 REVERT 문은 컨텍스트를 컨텍스트 스택의 다음 수준에 있는 로그인 또는 사용자로 전환합니다. 이 동작을 보려면 [예 1](#_exampleA)을 참조하세요.  
  
##  <a name="specifying-a-user-or-login-name"></a><a name="_user"></a>사용자 또는 로그인 이름 지정  
 EXECUTE AS \<context_specification>에 지정된 사용자 또는 로그인 이름은 **sys.database_principals** 또는 **sys.server_principals**에서 각각 보안 주체여야 합니다. 그렇지 않으면 EXECUTE AS 문이 실패합니다. 또한 보안 주체에 IMPERSONATE 권한을 부여해야 합니다. 호출자가 데이터베이스 소유자 또는 **sysadmin** 고정 서버 역할의 멤버가 아닌 경우에는 사용자가 Windows 그룹 멤버 자격을 통해 데이터베이스 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 액세스할 때도 보안 주체가 있어야 합니다. 예를 들어 다음과 같은 조건을 가정해 보세요. 
  
-   **CompanyDomain\SQLUsers** 그룹에 **Sales** 데이터베이스에 대한 액세스 권한이 있습니다.  
  
-   **CompanyDomain\SqlUser1**은 **SQLUsers**의 멤버이므로 그룹에 **Sales** 데이터베이스에 대한 암시적 액세스 권한이 있습니다.  
  
 **CompanyDomain\SqlUser1**이 **SQLUsers** 그룹의 멤버 자격을 통해 데이터베이스에 대한 액세스 권한을 가지더라도 `CompanyDomain\SqlUser1`이 데이터베이스에서 보안 주체가 아니므로 `EXECUTE AS USER = 'CompanyDomain\SqlUser1'` 문이 실패합니다.  
  
사용자가 분리되었고(연결된 로그인이 더 이상 존재하지 않음) **WITHOUT LOGIN**으로 생성되지 않은 경우 해당 사용자에 대한 **EXECUTE AS**는 실패하게 됩니다.  
  
## <a name="best-practice"></a>모범 사례  
 세션에서 작업을 수행하는 데 필요한 최소 권한을 가진 로그인 또는 사용자를 지정합니다. 예를 들어 데이터베이스 수준 사용 권한만 필요한 경우에는 서버 수준 사용 권한을 가진 로그인 이름을 지정하지 않도록 합니다. 또한 데이터베이스 소유자 계정과 관련된 사용 권한이 필요하지 않으면 이 계정을 지정하지 않도록 합니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)]가 이름을 확인할 수 있는 한 EXECUTE AS 문은 성공할 수 있습니다. 도메인 사용자가 있는 경우 Windows 사용자에게 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 액세스 권한이 없어도 Windows는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자를 확인할 수 있습니다. 가장된 로그인은 공용 또는 게스트 사용 권한만 부여하더라도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한이 없는 로그인이 로그인된 것으로 나타날 수 있습니다.  
  
## <a name="using-with-no-revert"></a>WITH NO REVERT 사용  
 EXECUTE AS 문에 선택적 WITH NO REVERT 절이 포함되어 있으면 REVERT를 사용하거나 다른 EXECUTE AS 문을 실행하여 세션의 실행 컨텍스트를 다시 설정할 수 없습니다. 해당 문으로 설정한 컨텍스트는 세션이 삭제될 때까지 유효합니다.  
  
 WITH NO REVERT COOKIE = @*varbinary_variabl* 절을 지정하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]이 쿠키 값을 @*varbinary_variabl*e에 전달합니다. 호출하는 REVERT WITH COOKIE = @*varbinary_variable* 문에 동일한 *\@varbinary_variable* 값이 포함된 경우에만 해당 문에서 설정된 실행 컨텍스트를 이전 컨텍스트로 되돌릴 수 있습니다.  
  
 이 옵션은 연결 풀링을 사용하는 환경에서 유용합니다. 연결 풀링은 애플리케이션 서버의 애플리케이션이 다시 사용할 수 있도록 데이터베이스 연결 그룹을 유지 관리하는 것입니다. *\@varbinary_variable*에 전달된 값은 EXECUTE AS 문의 호출자에게만 알려지므로 호출자는 자신이 설정한 실행 컨텍스트를 다른 사람이 변경할 수 없도록 할 수 있습니다.  
  
## <a name="determining-the-original-login"></a>원래 로그인 결정  
 [ORIGINAL_LOGIN](../../t-sql/functions/original-login-transact-sql.md) 함수를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 로그인의 이름을 반환할 수 있습니다. 이 함수를 사용하여 명시적 또는 암시적 컨텍스트 전환이 많이 있는 세션의 원래 로그인 ID를 반환할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 로그인에 **EXECUTE AS**를 지정하려면 호출자에게 지정한 로그인 이름에 대한 **IMPERSONATE** 권한이 있어야 하며 **IMPERSONATE ANY LOGIN** 권한에 의해 거부되지 않아야 합니다. 데이터베이스 사용자에 **EXECUTE AS**를 지정하려면 호출자에게 지정한 사용자 이름에 대한 **IMPERSONATE** 권한이 있어야 합니다. **EXECUTE AS CALLER**를 지정한 경우에는 **IMPERSONATE** 권한이 필요하지 않습니다.  
  
## <a name="examples"></a>예제  
  
###  <a name="a-using-execute-as-and-revert-to-switch-context"></a><a name="_exampleA"></a> 1. EXECUTE AS 및 REVERT를 사용하여 컨텍스트 전환  
 다음 예에서는 여러 보안 주체를 사용하여 컨텍스트 실행 스택을 만듭니다. 그런 다음 `REVERT` 문을 사용하여 실행 컨텍스트를 이전 호출자로 다시 설정합니다. `REVERT` 문은 실행 컨텍스트가 원래 호출자로 설정될 때까지 스택 위로 이동하면서 여러 번 실행됩니다.  
  
```sql
USE AdventureWorks2012;  
GO  
--Create two temporary principals  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
--Give IMPERSONATE permissions on user2 to user1  
--so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
--Verify the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
--Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1 and login2.  
--The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
--Remove temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. WITH COOKIE 절 사용  
 다음 예에서는 세션 실행 컨텍스트를 지정한 사용자로 설정하고 WITH NO REVERT COOKIE = @*varbinary_variabl*e 절을 지정합니다. 컨텍스트를 호출자로 되돌리려면 `REVERT` 문에 `@cookie` 문의 `EXECUTE AS` 변수로 전달되는 값을 지정해야 합니다. 이 예를 실행하려면 예 1에서 생성된 `login1` 로그인 및 `user1` 사용자가 있어야 합니다.  
  
```sql
DECLARE @cookie varbinary(8000);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie in a safe location in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(8000);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS Clause &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)  
  
  

