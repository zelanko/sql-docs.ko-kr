---
title: '자습서: 소유권 체인 및 컨텍스트 전환 | Microsoft 문서'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.topic: quickstart
applies_to:
- SQL Server 2016
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc70ec0b789ba0873b4e843b77132ec14bf4d7aa
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024466"
---
# <a name="tutorial-ownership-chains-and-context-switching"></a>Tutorial: Ownership Chains and Context Switching
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 자습서에서는 시나리오를 통해 소유권 체인 및 사용자 컨텍스트 전환과 관련된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 보안 개념을 설명합니다.  
  
> [!NOTE]  
> 이 자습서의 코드를 실행하려면 혼합 모드 보안을 구성하고 AdventureWorks2017 데이터베이스를 설치해야 합니다. 혼합 모드 보안에 대한 자세한 내용은 [인증 모드 선택](../relational-databases/security/choose-an-authentication-mode.md)을 참조하세요.  
  
## <a name="scenario"></a>시나리오  
이 시나리오에서는 두 사용자에게 AdventureWorks2017 데이터베이스에 저장된 구매 주문 데이터에 액세스할 수 있는 계정이 필요합니다. 요구 사항은 다음과 같습니다.  
  
-   첫 번째 계정(TestManagerUser)은 전체 구매 주문의 세부 사항을 모두 볼 수 있어야 합니다.  
-   두 번째 계정(TestEmployeeUser)은 부분 운송을 받은 항목에 대해 구매 주문 번호, 주문 날짜, 운송 날짜, 제품 ID 번호, 구매 주문별로 주문하고 받은 항목, 구매 주문 번호별로 주문하고 받은 항목을 볼 수 있어야 합니다.  
-   다른 모든 계정은 현재의 해당 사용 권한을 유지해야 합니다.   
이 시나리오의 요구 사항을 만족시키기 위해 이 예제는 소유권 체인 및 컨텍스트 전환의 개념을 설명하는 네 부분으로 나뉘어 있습니다.  
  
1.  환경 구성   
2.  구매 주문별로 데이터에 액세스하는 저장 프로시저 만들기   
3.  저장 프로시저를 통해 데이터 액세스  
4.  환경 다시 설정  
  
이 예제의 각 코드 블록에 대한 설명도 함께 나와 있습니다. 전체 예제를 복사하려면 이 자습서 끝에 있는 [전체 예제](#CompleteExample) 를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio, SQL Server를 실행하는 서버에 대한 액세스 및 AdventureWorks 데이터베이스가 필요합니다.

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks2017 샘플 데이터베이스](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)를 다운로드합니다.

SQL Server Management Studio에서 데이터베이스를 복원하는 방법은 [데이터베이스를 복원](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)을 참조하세요.   
  
## <a name="1-configure-the-environment"></a>1. 환경 구성  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 및 다음 코드를 사용하여 `AdventureWorks2017` 데이터베이스를 열고 `CURRENT_USER` [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 사용하여 dbo 사용자가 컨텍스트로 표시되는지 확인합니다.  
  
```sql
USE AdventureWorks2017;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
CURRENT_USER 문에 대한 자세한 내용은 [CURRENT_USER&#40;Transact-SQL&#41;](../t-sql/functions/current-user-transact-sql.md)를 참조하세요.  
  
이 코드를 dbo 사용자로 사용하여 서버와 AdventureWorks2017 데이터베이스에 두 명의 사용자를 만듭니다.  
  
```sql
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
CREATE USER 문에 대한 자세한 내용은 [CREATE USER&#40;Transact-SQL&#41;](../t-sql/statements/create-user-transact-sql.md)를 참조하세요. CREATE LOGIN 문에 대한 자세한 내용은 [CREATE LOGIN&#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md)을 참조하세요.  
  
다음 코드를 사용하여 `Purchasing` 스키마의 소유권을 `TestManagerUser` 계정이 가지도록 변경합니다. 이렇게 하면 해당 계정이 자신이 포함하는 개체에서 모든 DML(데이터 조작 언어) 문 액세스 권한(예: `SELECT` 및 `INSERT` 권한)을 사용할 수 있습니다. `TestManagerUser` 에게도 저장 프로시저를 만들 수 있는 권한이 부여됩니다.  
  
```sql
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
GRANT 문에 대한 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)를 참조하세요. 저장 프로시저에 대한 자세한 내용은 [저장 프로시저&#40;데이터베이스 엔진&#41;](../relational-databases/stored-procedures/stored-procedures-database-engine.md)를 참조하세요. 모든 [!INCLUDE[ssDE](../includes/ssde-md.md)] 사용 권한에 대한 포스터는 [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster)를 참조하세요.  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2. 데이터에 액세스하는 저장 프로시저 만들기  
데이터베이스 내에서 컨텍스트를 전환 하려면 EXECUTE AS 문을 사용합니다. EXECUTE AS를 사용하려면 IMPERSONATE 권한이 있어야 합니다.  
  
다음 코드에서 `EXECUTE AS` 문을 사용하여 컨텍스트를 `TestManagerUser` 로 변경하고 `TestEmployeeUser`에게 필요한 데이터만 표시하는 저장 프로시저를 만듭니다. 요구 사항을 만족하기 위해 저장 프로시저는 구매 주문 번호에 대해 하나의 변수를 사용하고 재무 정보를 표시하지 않으며 WHERE 절로 결과를 부분 운송을 받은 항목으로 제한합니다.  
  
```sql
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
현재 `TestEmployeeUser` 에게는 데이터베이스 개체에 대한 액세스 권한이 없습니다. 아직 `TestManagerUser` 컨텍스트에 있는 다음 코드는 저장 프로시저를 통해 기본 테이블 정보를 쿼리할 수 있는 권한을 사용자 계정에 부여합니다.  
  
```sql
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
`Purchasing` 가 기본적으로 `TestManagerUser` 스키마에 할당되므로 스키마가 명시적으로 지정되지 않더라도 저장 프로시저는 `Purchasing` 스키마의 일부가 됩니다. 다음 코드와 같이 시스템 카탈로그 정보를 사용하여 개체를 찾을 수 있습니다.  
  
```sql
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
예제의 이 섹션을 완료하면 코드가 `REVERT` 문을 사용하여 컨텍스트를 다시 dbo로 전환합니다.  
  
```sql
REVERT;  
GO  
```  
  
REVERT 문에 대한 자세한 내용은 [REVERT&#40;Transact-SQL&#41;](../t-sql/statements/revert-transact-sql.md)를 참조하세요.  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3. 저장 프로시저를 통해 데이터 액세스  
`TestEmployeeUser` 에게는 public 데이터베이스 역할에 할당된 로그인 및 권한 이외에 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스 개체에 대한 사용 권한이 없습니다. `TestEmployeeUser` 가 기본 테이블에 액세스하려고 하면 다음 코드에서 오류를 반환합니다.  
  
```sql
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  

반환된 오류:
```
Msg 229, Level 14, State 5, Line 6
The SELECT permission was denied on the object 'PurchaseOrderHeader', database 'AdventureWorks2017', schema 'Purchasing'.
```
  
`TestManagerUser` 스키마 소유권으로 인해 `Purchasing` 가 마지막 섹션에서 생성된 저장 프로시저에서 참조하는 개체를 소유하므로 `TestEmployeeUser` 는 저장 프로시저를 통해 기본 테이블에 액세스할 수 있습니다. 아직 `TestEmployeeUser` 컨텍스트를 사용하는 다음 코드는 구매 주문 952를 매개 변수로 전달합니다.  
  
```sql
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4. 환경 다시 설정  
다음 코드는 `REVERT` 명령을 사용하여 현재 계정의 컨텍스트를 `dbo`로 되돌린 다음 환경을 다시 설정합니다.  
  
```sql
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="CompleteExample"></a>전체 예제  
이 섹션에서는 전체 예제 코드를 보여 줍니다.  
  
> [!NOTE]  
> 이 코드에는 `TestEmployeeUser` 가 기본 테이블에서 데이터를 선택할 수 없음을 보여 주는 두 가지 예상 오류가 포함되어 있지 않습니다.  
  
```sql
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2017;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 보안 센터](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
  
