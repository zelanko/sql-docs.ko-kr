---
title: 저장 프로시저 다시 컴파일 | Microsoft 문서
description: Transact-SQL을 사용하여 SQL Server 2019(15.x)에서 저장 프로시저를 다시 컴파일하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sp_recompile
- WITH RECOMPILE clause
- recompiling stored procedures
- stored procedures [SQL Server], recompiling
ms.assetid: b90deb27-0099-4fe7-ba60-726af78f7c18
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f421e3a0e07b73037e9b789bd29778791f699561
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473074"
---
# <a name="recompile-a-stored-procedure"></a>저장 프로시저 다시 컴파일
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 저장 프로시저를 다시 컴파일하는 방법에 대해 설명합니다. 이렇게 하려면 프로시저 정의에서나 프로시저가 호출될 때 **WITH RECOMPILE** 옵션을 사용하거나, 개별 문에서 **RECOMPILE** 쿼리 힌트를 사용하거나, **sp_recompile** 시스템 저장 프로시저를 사용합니다. 이 항목에서는 프로시저 정의를 만들고 기존 프로시저를 실행할 때 RECOMPILE 옵션을 사용하는 방법에 대해 설명합니다. 또한 sp_recompile 시스템 저장 프로시저를 사용하여 기존 프로시저를 다시 컴파일하는 방법에 대해서도 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **저장 프로시저를 다시 컴파일하려면:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   프로시저가 처음 컴파일되거나 다시 컴파일될 때 프로시저의 쿼리 계획은 데이터베이스와 해당 개체의 현재 상태에 맞게 최적화됩니다. 데이터베이스의 데이터나 구조가 크게 변경되는 경우 프로시저를 다시 컴파일하면 해당 변경 내용에 대한 프로시저의 쿼리 계획이 업데이트되고 최적화됩니다. 이에 따라 프로시저의 처리 성능이 향상될 수 있습니다.  
  
-   프로시저 재컴파일이 강제로 수행되어야 하는 경우도 있고 자동으로 발생하는 경우도 있습니다. 자동 재컴파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다시 시작될 때마다 발생하고 프로시저에서 참조하는 기본 테이블의 물리적 디자인이 변경되는 경우에도 발생합니다.  
  
-   프로시저를 강제로 다시 컴파일하는 또 다른 이유는 프로시저 컴파일의 "매개 변수 스니핑" 동작을 막기 위한 것입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 프로시저를 실행하면 프로시저 컴파일에 사용되는 모든 매개 변수 값이 쿼리 계획 생성 시 포함됩니다. 이러한 매개 변수 값이 나중에 프로시저를 호출할 때 사용되는 일반적인 값을 나타낼 경우 프로시저가 컴파일되고 실행될 때마다 이 쿼리 계획을 이용할 수 있습니다. 프로시저의 매개 변수 값이 흔히 부정형인 경우 여러 가지 매개 변수 값에 따라 새 계획과 프로시저 재컴파일을 강제로 적용하면 성능이 향상될 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 프로시저를 문 수준으로 다시 컴파일할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 저장 프로시저를 다시 컴파일할 때 전체 프로시저가 아닌 재컴파일이 필요한 문만 컴파일됩니다.  
  
-   프로시저의 특정 쿼리에서 비정형 값이나 임시 값을 정기적으로 사용하는 경우 해당 쿼리 내에서 RECOMPILE 쿼리 힌트를 사용하여 프로시저 성능을 높일 수 있습니다. 전체 프로시저 대신 쿼리 힌트를 사용하는 쿼리만 다시 컴파일되므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 문 수준 재컴파일 동작이 모방됩니다. 그러나 RECOMPILE 쿼리 힌트는 프로시저의 현재 매개 변수 값을 사용할 뿐만 아니라 문을 컴파일할 때 저장 프로시저에 있는 지역 변수의 값도 사용합니다. 자세한 내용은 [쿼리 힌트(Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 **WITH RECOMPILE** 옵션  
 프로시저 정의를 만들 때 이 옵션을 사용하는 경우 데이터베이스에서 CREATE PROCEDURE 권한과 프로시저를 만들고 있는 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
 EXECUTE 문에서 이 옵션을 사용하는 경우 프로시저에 대한 EXECUTE 권한이 있어야 합니다. EXECUTE 문 자체에 대한 권한은 필요하지 않지만 EXECUTE 문에서 참조되는 프로시저에 대한 실행 권한이 필요합니다. 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)을 참조하세요.  
  
 **RECOMPILE** 쿼리 힌트  
 이 기능은 프로시저를 만들고 프로시저의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 힌트를 포함할 때 사용됩니다. 따라서 데이터베이스에서 CREATE PROCEDURE 권한과 프로시저를 만들 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
 **sp_recompile** 시스템 저장 프로시저  
 지정된 프로시저에 대한 ALTER 권한이 있어야 합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  

1. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
1. 표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
1. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예에서는 프로시저 정의를 만듭니다.  

   ```sql
   USE AdventureWorks2012;  
   GO  
   IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
       DROP PROCEDURE dbo.uspProductByVendor;  
   GO  
   CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
   WITH RECOMPILE  
   AS  
       SET NOCOUNT ON;  
       SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
       FROM Purchasing.Vendor AS v   
       JOIN Purchasing.ProductVendor AS pv   
         ON v.BusinessEntityID = pv.BusinessEntityID   
       JOIN Production.Product AS p   
         ON pv.ProductID = p.ProductID  
       WHERE v.Name LIKE @Name;  
   ```  
  
### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>WITH RECOMPILE 옵션을 사용하여 저장 프로시저를 다시 컴파일하려면   
  
**새 쿼리** 를 선택한 후, 다음 코드 예제를 복사하여 쿼리 창에 붙여넣고, **실행** 을 클릭합니다. 프로시저가 실행되고 프로시저의 쿼리 계획이 다시 컴파일됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE HumanResources.uspProductByVendor WITH RECOMPILE;  
GO
```  
  
### <a name="to-recompile-a-stored-procedure-by-using-sp_recompile"></a>sp_recompile을 사용하여 저장 프로시저를 다시 컴파일하려면  

**새 쿼리** 를 선택한 후, 다음 예제를 복사하여 쿼리 창에 붙여넣고, **실행** 을 클릭합니다. 프로시저가 실행되지는 않지만 다음에 프로시저가 실행될 때 쿼리 계획이 업데이트될 수 있게 프로시저가 다시 컴파일되도록 표시됩니다.  

```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'dbo.uspProductByVendor';   
GO
```  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [저장 프로시저 수정](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [저장 프로시저 이름 바꾸기](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [저장 프로시저의 정의 보기](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [저장 프로시저의 종속성 보기](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
