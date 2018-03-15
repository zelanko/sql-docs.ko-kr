---
title: EXECUTE AS Clause(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- AS
- AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permission sets [SQL Server]
- queues [SQL Server]
- stored procedures [SQL Server], executing
- user-defined functions [SQL Server], execution context
- EXECUTE AS
- triggers [SQL Server], execution context
- execution context [SQL Server]
- switching execution context
- functions [SQL Server], execution context
ms.assetid: bd517aa3-f06e-4356-87d8-70de5df4494a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: baf3fdc592265f1c2117ef3358820ae94ce8536c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="execute-as-clause-transact-sql"></a>EXECUTE AS 절(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자 정의 모듈인 함수(인라인 테이블 반환 함수 제외), 프로시저, 큐 및 트리거의 실행 컨텍스트를 정의할 수 있습니다.  
  
 모듈이 실행되는 컨텍스트를 지정해서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 사용자 계정을 제어하면 모듈에서 참조하는 개체에 대한 사용 권한을 검사할 수 있습니다. 이렇게 하면 사용자 정의 모듈 및 해당 모듈에서 참조하는 개체 사이에 있는 개체 체인에서 좀 더 유연하게 사용 권한 관리를 제어할 수 있습니다. 참조된 개체에 대한 명시적 사용 권한이 아닌 모듈 자체에 대한 사용 권한만 사용자에게 부여해야 합니다. 모듈을 실행하고 있는 사용자만이 모듈에서 액세스하는 개체에 대한 사용 권한을 가져야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- SQL Server Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }   
  
DDL Triggers with Server Scope and logon triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'login_name' }   
  
Queues  
{ EXEC | EXECUTE } AS { SELF | OWNER | 'user_name' }   
```  
  
```  
  
-- Windows Azure SQL Database Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }  
  
```  
  
## <a name="arguments"></a>인수  
 **CALLER**  
 모듈 내부의 문이 모듈 호출자의 컨텍스트에서 실행되도록 지정합니다. 모듈을 실행하는 사용자는 모듈 자체에 대한 알맞은 사용 권한뿐만 아니라 모듈에서 참조하는 모든 데이터베이스 개체에 대한 사용 권한도 갖고 있어야 합니다.  
  
 CALLER는 큐를 제외한 모든 모듈의 기본값이며 이것은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 동작과 동일합니다.  
  
 CREATE QUEUE 또는 ALTER QUEUE 문에서는 CALLER를 지정할 수 없습니다.  
  
 **SELF**  
 EXECUTE AS SELF는 EXECUTE AS *user_name*과 동일합니다. 여기에서 지정된 사용자는 모듈을 만들거나 변경하는 사용자입니다. 모듈을 만들거나 수정하는 사용자의 실제 ID는 **sys.sql_modules** 또는 **sys.service_queues** 카탈로그 뷰의 **execute_as_principal_id** 열에 저장됩니다.  
  
 SELF는 큐의 기본값입니다.  
  
> [!NOTE]  
>  **sys.service_queues** 카탈로그 뷰에서 **execute_as_principal_id**의 사용자 ID를 변경하려면 ALTER QUEUE 문에서 명시적으로 EXECUTE AS를 설정해야 합니다.  
  
 OWNER  
 모듈 내부의 문이 현재 모듈 소유자의 컨텍스트에서 실행되도록 지정합니다. 모듈에 지정된 소유자가 없으면 이 모듈의 스키마 소유자를 사용합니다. DDL 또는 로그온 트리거에 대해서는 OWNER를 지정할 수 없습니다.  
  
> [!IMPORTANT]  
>  OWNER는 단일 계정으로 매핑되어야 하며 역할이나 그룹이 될 수 없습니다.  
  
 **'** *user_name* **'**  
 모듈 내부의 문이 *user_name*에 지정된 사용자의 컨텍스트에서 실행되도록 지정합니다. 모듈 내의 모든 개체에 대한 사용 권한은 *user_name*과 비교 검증됩니다. 서버 범위의 DDL 트리거 또는 로그온 트리거에는 *user_name*을 지정할 수 없습니다. 대신 *login_name*을 사용합니다.  
  
 *user_name*은 현재 데이터베이스에 있어야 하며 단일 계정이어야 합니다. *user_name*은 그룹, 역할, 인증서 또는 키이거나 NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService 또는 NT AUTHORITY\LocalSystem과 같은 기본 제공 계정이 될 수 없습니다.  
  
 실행 컨텍스트의 사용자 ID는 메타데이터에 저장되고 **sys.sql_modules** 또는 **sys.assembly_modules** 카탈로그 뷰의 **execute_as_principal_id** 열에 표시될 수 있습니다.  
  
 **'** *login_name* **'**  
 모듈 내부의 문이 *login_name*에 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 컨텍스트에서 실행되도록 지정합니다. 모듈 내의 모든 개체에 대한 사용 권한은 *login_name*과 비교 검증됩니다. *login_name*은 서버 범위의 DDL 트리거 또는 로그온 트리거에만 지정할 수 있습니다.  
  
 *login_name*은 그룹, 역할, 인증서 또는 키이거나 NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService 또는 NT AUTHORITY\LocalSystem과 같은 기본 제공 계정이 될 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 모듈이 참조하는 개체에 대한 사용 권한을 평가하는 방법은 호출 개체와 참조된 개체 간에 존재하는 소유권 체인에 따라 다릅니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 호출 사용자에게 참조된 모든 개체에 대한 액세스 권한을 부여하지 않도록 하는 유일한 방법은 소유권 체인이었습니다.  
  
 소유권 체인에는 다음과 같은 제한 사항이 있습니다.  
  
-   SELECT, INSERT, UPDATE 및 DELETE와 같은 DML 문에만 적용됩니다.  
  
-   호출 개체의 소유자와 호출된 개체의 소유자가 동일해야 합니다.  
  
-   모듈 내의 동적 쿼리에는 적용되지 않습니다.  
  
 다음 동작은 모듈에 지정된 실행 컨텍스트에 관계없이 항상 적용됩니다.  
  
-   모듈이 실행될 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 먼저 모듈을 실행하는 사용자에게 모듈에 대한 EXECUTE 권한이 있는지 확인합니다.  
  
-   소유권 체인 규칙은 지속적으로 적용됩니다. 즉, 호출 개체의 소유자와 호출된 개체의 소유자가 동일한 경우 원본 개체에 대한 사용 권한을 확인하지 않습니다.  
  
 사용자가 CALLER 이외의 컨텍스트에서 실행되도록 지정된 모듈을 실행하는 경우 이 모듈을 실행하는 사용자의 사용 권한은 확인되지만 모듈이 액세스하는 개체에 대한 추가 사용 권한 확인은 EXECUTE AS 절에 지정된 사용자 계정에 대해 수행됩니다. 결과적으로 모듈을 실행하는 사용자는 지정된 사용자를 가장하게 됩니다.  
  
 모듈의 EXECUTE AS 절에 지정된 컨텍스트는 모듈이 실행되는 동안에만 유효합니다. 모듈 실행이 완료되면 컨텍스트는 호출자로 되돌아갑니다.  
  
## <a name="specifying-a-user-or-login-name"></a>사용자 또는 로그인 이름 지정  
 모듈이 다른 컨텍스트에서 실행되도록 수정하기 전에는 모듈의 EXECUTE AS 절에 지정된 데이터베이스 사용자나 서버 로그인을 삭제할 수 없습니다.  
  
 EXECUTE AS 절에 지정된 사용자 또는 로그인 이름은 각각 **sys.database_principals** 또는 **sys.server_principals**에서 보안 주체로 존재해야 합니다. 그렇지 않으면 모듈을 만들거나 변경할 수 없습니다. 또한 모듈을 만들거나 변경하는 사용자에게는 보안 주체에 대한 IMPERSONATE 권한이 있어야 합니다.  
  
 사용자가 Windows 그룹 멤버 자격을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스나 인스턴스에 대한 암시적 액세스 권한을 갖고 있는 경우 다음 요구 사항 중 하나가 충족된다면 모듈이 생성될 때 EXECUTE AS 절에 지정된 사용자가 암시적으로 생성됩니다.  
  
-   지정된 사용자 또는 로그인이 **sysadmin** 고정 서버 역할의 멤버입니다.  
  
-   모듈을 만드는 사용자에게 보안 주체를 만들 사용 권한이 권한이 있습니다.  
  
 이러한 요구 사항이 충족되지 않는 경우에는 모듈을 만들 수 없습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](MSSQLSERVER) 서비스가 로컬 서비스 또는 로컬 사용자 계정과 같은 로컬 계정으로 실행되고 있는 경우에는 EXECUTE AS 절에 지정된 Windows 도메인 계정의 그룹 멤버 자격을 가져올 수 있는 권한이 없습니다. 따라서 모듈 실행이 실패하게 됩니다.  
  
 예를 들어 다음과 같은 조건을 가정해 보세요.  
  
-   **CompanyDomain\SQLUsers** 그룹에 **Sales** 데이터베이스에 대한 액세스 권한이 있습니다.  
  
-   **CompanyDomain\SqlUser1**은 **SQLUsers**의 멤버이므로 **Sales** 데이터베이스에 대한 액세스 권한이 있습니다.  
  
-   모듈을 만들거나 변경하는 사용자에게 보안 주체를 만들 사용 권한이 있습니다.  
  
 다음 `CREATE PROCEDURE` 문을 실행하면 `CompanyDomain\SqlUser1` 데이터베이스에서 `Sales`이 데이터베이스 보안 주체로 암시적으로 생성됩니다.  
  
```  
USE Sales;  
GO  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'CompanyDomain\SqlUser1'  
AS  
SELECT user_name();  
GO  
```  
  
## <a name="using-execute-as-caller-stand-alone-statement"></a>EXECUTE AS CALLER 독립 실행형 문 사용  
 모듈 내에서 EXECUTE AS CALLER 독립 실행형 문을 사용하여 실행 컨텍스트를 모듈 호출자로 설정할 수 있습니다.  
  
 `SqlUser2`가 다음 저장 프로시저를 호출한다고 가정합니다.  
  
```  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'SqlUser1'  
AS  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
EXECUTE AS CALLER;  
SELECT user_name(); -- Shows execution context is set to SqlUser2, the caller of the module.  
REVERT;  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
GO  
```  
  
## <a name="using-execute-as-to-define-custom-permission-sets"></a>EXECUTE AS를 사용하여 사용자 지정 권한 집합 정의  
 사용자 지정 권한 집합을 정의할 때는 모듈의 실행 컨텍스트를 지정하면 편리합니다. 예를 들어 TRUNCATE TABLE과 같은 일부 동작에는 부여할 수 있는 사용 권한이 없습니다. 모듈 내에 TRUNCATE TABLE 문을 삽입하고 해당 모듈이 테이블을 변경할 수 있는 사용 권한이 부여된 사용자로 실행되도록 지정하면 모듈에 대한 EXECUTE 권한을 부여한 사용자에게 테이블을 자를 수 있는 사용 권한도 부여할 수 있습니다.  
  
 지정된 실행 컨텍스트가 있는 모듈 정의를 보려면 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰를 사용합니다.  
  
## <a name="best-practice"></a>최선의 구현 방법  
 모듈에 정의된 작업을 수행하는 데 필요한 최소한의 권한이 있는 로그인이나 사용자를 지정합니다. 예를 들어 데이터베이스 소유자 계정은 해당 권한이 필요한 경우에만 지정하세요.  
  
## <a name="permissions"></a>사용 권한  
 EXECUTE AS로 지정된 모듈을 실행하려면 호출자에게 해당 모듈에 대한 EXECUTE 권한이 있어야 합니다.  
  
 다른 데이터베이스 또는 서버의 리소스에 액세스하는 EXECUTE AS로 지정된 CLR 모듈을 실행하려면 대상 데이터베이스나 서버가 모듈이 원래 속한 원본 데이터베이스의 인증자를 트러스트해야 합니다.  
  
 모듈을 만들거나 수정할 때 EXECUTE AS 절을 지정하려면 지정된 보안 주체에 대한 IMPERSONATE 권한과 모듈을 만들 수 있는 권한이 있어야 합니다. 사용자는 항상 자신을 가장할 수 있습니다. 실행 컨텍스트를 지정하지 않거나 EXECUTE AS CALLER를 지정한 경우에는 IMPERSONATE 권한이 필요하지 않습니다.  
  
 Windows 그룹 멤버 자격을 통해 데이터베이스에 대한 암시적 액세스 권한이 있는 *login_name* 또는 *user_name*을 지정하려면 해당 데이터베이스에 대한 CONTROL 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 저장 프로시저를 만들고 실행 컨텍스트를 `OWNER`로 할당합니다.  
  
```  
CREATE PROCEDURE HumanResources.uspEmployeesInDepartment   
@DeptValue int  
WITH EXECUTE AS OWNER  
AS  
    SET NOCOUNT ON;  
    SELECT e.BusinessEntityID, c.LastName, c.FirstName, e.JobTitle  
    FROM Person.Person AS c   
    INNER JOIN HumanResources.Employee AS e  
        ON c.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS edh  
        ON e.BusinessEntityID = edh.BusinessEntityID  
    WHERE edh.DepartmentID = @DeptValue  
    ORDER BY c.LastName, c.FirstName;  
GO  
  
-- Execute the stored procedure by specifying department 5.  
EXECUTE HumanResources.uspEmployeesInDepartment 5;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.service_queues &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-queues-transact-sql.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
