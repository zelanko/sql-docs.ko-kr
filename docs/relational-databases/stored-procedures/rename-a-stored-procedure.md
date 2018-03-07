---
title: "저장 프로시저 이름 바꾸기 | Microsoft 문서"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1dd52bd311a8c976ed5967c71315aca5b59923c7
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="rename-a-stored-procedure"></a>저장 프로시저 이름 바꾸기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 저장 프로시저의 이름을 바꾸는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **저장 프로시저의 이름을 바꾸려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   프로시저 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
-   저장 프로시저 이름을 바꾸어도 `object_id` 및 해당 프로시저에 명시적으로 할당된 모든 사용 권한은 유지됩니다. 개체를 삭제한 후 다시 만들면 새 `object_id`가 생성되고 프로시저에 명시적으로 할당된 모든 사용 권한이 제거됩니다.

-   저장 프로시저의 이름을 변경해도 **sys.sql_modules** 카탈로그 뷰의 정의 열에 있는 해당 개체 이름은 변경되지 않습니다. 이를 수행하려면 저장 프로시저를 삭제하고 새로운 이름으로 다시 만들어야 합니다.  

-   프로시저의 이름 또는 정의를 변경할 때 프로시저의 변경 내용이 적용되도록 개체를 업데이트하지 않으면 종속 개체가 실패할 수 있습니다. 자세한 내용은 [저장 프로시저의 종속성 보기](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 CREATE PROCEDURE  
 데이터베이스에 대한 CREATE PROCEDURE 권한과 프로시저를 만들고 있는 스키마에 대한 ALTER 권한이 필요하거나 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
 ALTER PROCEDURE  
 프로시저에 대한 ALTER 권한이나 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rename-a-stored-procedure"></a>저장 프로시저의 이름을 바꾸려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
2.  **데이터베이스**를 확장하고 해당 프로시저가 속한 데이터베이스를 확장한 다음 **프로그래밍 기능**을 확장합니다.  
3.  [저장 프로시저의 종속성을 결정합니다](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
4.  **저장 프로시저**를 확장하고 이름을 바꿀 프로시저를 마우스 오른쪽 단추로 클릭한 다음 **이름 바꾸기**를 클릭합니다.  
5.  프로시저 이름을 수정합니다.  
6.  종속 개체 또는 스크립트에서 참조된 프로시저 이름을 수정합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-rename-a-stored-procedure"></a>저장 프로시저의 이름을 바꾸려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 프로시저를 삭제하고 새 이름으로 다시 만들어 프로시저의 이름을 바꾸는 방법을 보여 줍니다. 첫 번째 예에서는 `'HumanResources.uspGetAllEmployeesTest`저장 프로시저를 만듭니다. 두 번째 예에서는 `HumanResources.uspEveryEmployeeTest`저장 프로시저의 이름을 바꿉니다.  
  
```sql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  

CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
EXEC sp_rename 'HumanResources.uspGetAllEmployeesTest', 'uspEveryEmployeeTest'; 
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [저장 프로시저 수정](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [저장 프로시저 삭제](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [저장 프로시저의 정의 보기](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [저장 프로시저의 종속성 보기](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
  
