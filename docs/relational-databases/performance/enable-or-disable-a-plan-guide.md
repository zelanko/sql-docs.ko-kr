---
title: "계획 지침 사용 또는 사용 안 함 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- plan guides [SQL Server], disabling
- enabling plan guides
- plan guides [SQL Server], enabling
- disabling plan guides
ms.assetid: b00ab550-5308-4cb8-8330-483cd1d25654
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1d76a7087ce1225c2ae3f4f685cb234b53dbf0b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="enable-or-disable-a-plan-guide"></a>계획 지침 사용 또는 사용 안 함
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 계획 지침을 사용하거나 사용하지 않도록 설정할 수 있습니다. 데이터베이스에 있는 단일 계획 지침 또는 모든 계획 지침을 사용하거나 사용하지 않도록 설정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **계획 지침을 사용하거나 사용하지 않도록 설정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   활성화 여부에 관계없이 계획 지침에서 참조하는 함수, 저장 프로시저 또는 DML 트리거를 삭제하거나 수정하려고 하면 오류가 발생합니다. 위에 나열된 개체를 삭제하거나 수정하기 전에 항상 종속성을 확인합니다.  
  
-   비활성화된 계획 지침을 비활성화하거나 활성화된 계획 지침을 활성화하면 아무런 영향을 미치지 않고 오류 없이 실행됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 OBJECT 계획 지침을 사용하거나 사용하지 않도록 설정하려면 계획 지침에서 참조되는 개체(예: 함수, 저장 프로시저)에 대한 변경 권한이 있어야 합니다. 다른 모든 계획 지침에는 ALTER DATABASE 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>계획 지침을 사용하거나 사용하지 않도록 설정하려면  
  
1.  더하기 기호를 클릭하여 계획 지침을 사용하거나 사용하지 않도록 설정할 데이터베이스를 확장한 다음 더하기 기호를 클릭하여 **프로그래밍 기능** 폴더를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **계획 지침** 폴더를 확장합니다.  
  
3.  사용하거나 사용하지 않도록 설정할 계획 지침을 마우스 오른쪽 단추로 클릭하고 **사용 안 함** 또는 **사용**을 선택합니다.  
  
4.  **계획 지침 사용 안 함** 또는 **계획 지침 사용** 대화 상자에서 선택한 작업이 성공했는지 확인한 다음 **닫기**를 클릭합니다.  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>데이터베이스의 모든 계획 지침을 사용하거나 사용하지 않도록 설정하려면  
  
1.  더하기 기호를 클릭하여 계획 지침을 사용하거나 사용하지 않도록 설정할 데이터베이스를 확장한 다음 더하기 기호를 클릭하여 **프로그래밍 기능** 폴더를 확장합니다.  
  
2.  **계획 지침** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **모두 사용** 또는 **모두 사용 안 함**을 선택합니다.  
  
3.  **모든 계획 지침 사용 안 함** 또는 **모든 계획 지침 사용** 대화 상자에서 선택한 작업이 성공했는지 확인한 다음 **닫기**를 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>계획 지침을 사용하거나 사용하지 않도록 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    --Create a procedure on which to define the plan guide.  
    IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetSalesOrderByCountry;  
    GO  
    CREATE PROCEDURE Sales.GetSalesOrderByCountry   
        (@Country nvarchar(60))  
    AS  
    BEGIN  
        SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country;  
    END  
    GO  
    --Create the plan guide.  
    EXEC sp_create_plan_guide N'Guide3',  
        N'SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country',  
        N'OBJECT',  
        N'Sales.GetSalesOrderByCountry',  
        NULL,  
        N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
    --Disable the plan guide.  
    EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
    GO  
    --Enable the plan guide.  
    EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
    GO  
  
    ```  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>데이터베이스의 모든 계획 지침을 사용하거나 사용하지 않도록 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    --Disable all plan guides in the database.  
    EXEC sp_control_plan_guide N'DISABLE ALL';  
    GO  
    --Enable all plan guides in the database.  
    EXEC sp_control_plan_guide N'ENABLE ALL';  
    GO  
  
    ```  
  
 자세한 내용은 [sp_control_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)를 참조하세요.  
  
  
