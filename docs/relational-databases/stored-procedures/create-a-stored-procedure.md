---
title: 저장 프로시저 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- new stored procedures
- stored procedures [SQL Server], creating
- creating stored procedures
ms.assetid: 76e8a6ba-1381-4620-b356-4311e1331ca7
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0fd49b75fdb99f70d2d5b47982d8b1a7e10a7496
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-stored-procedure"></a>저장 프로시저 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 > 이전 버전의 SQL Server와 관련 된 콘텐츠를 참조 하십시오. [저장 프로시저 만들기](https://msdn.microsoft.com/en-US/library/ms345415(SQL.120).aspx)합니다.

  이 항목에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] CREATE PROCEDURE 문을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 만드는 방법에 대해 설명합니다.  
  
##  <a name="Top"></a>   
-   **시작하기 전에:**  [사용 권한](#Permissions)  
  
-   **프로시저를 만들려면:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="Permissions"></a> Permissions  
 데이터베이스의 CREATE PROCEDURE 권한과 프로시저를 만들 스키마에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="Procedures"></a> 저장 프로시저를 만드는 방법  
 다음 중 하나를 사용할 수 있습니다.  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **개체 탐색기에서 프로시저를 만들려면**  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 확장한 다음 **프로그래밍 기능**을 확장합니다.  
  
3.  **저장 프로시저**를 마우스 오른쪽 단추로 클릭한 다음 **새 저장 프로시저**를 클릭합니다.  
  
4.  **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정**을 클릭합니다.  
  
5.  **템플릿 매개 변수 값 지정** 대화 상자에 표시된 매개 변수에 대해 다음 값을 입력합니다.  
  
    |매개 변수|값|  
    |---------------|-----------|  
    |작성자|*Your name*|  
    |만든 날짜|*Today's date*|  
    |Description|Returns employee data|  
    |Procedure_name|HumanResources.uspGetEmployeesTest|  
    |@Param1|@LastName|  
    |@Datatype_For_Param1|**nvarchar**(50)|  
    |Default_Value_For_Param1|NULL|  
    |@Param2|@FirstName|  
    |@Datatype_For_Param2|**nvarchar**(50)|  
    |Default_Value_For_Param2|NULL|  
  
6.  **확인**을 클릭합니다.  
  
7.  **쿼리 편집기**에서 SELECT 문을 다음 문으로 바꿉니다.  
  
    ```sql  
    SELECT FirstName, LastName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory  
    WHERE FirstName = @FirstName AND LastName = @LastName  
        AND EndDate IS NULL;  
    ```  
  
8.  구문을 테스트하려면 **쿼리** 메뉴에서 **구문 분석**을 클릭합니다. 오류 메시지가 반환되면 필요에 따라 위의 정보와 문을 비교하여 수정합니다.  
  
9. 프로시저를 만들려면 **쿼리** 메뉴에서 **실행**을 클릭합니다. 프로시저가 데이터베이스 개체로 만들어집니다.  
  
10. 개체 탐색기에 나열된 프로시저를 보려면 **저장 프로시저** 를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  
  
11. 프로시저를 실행하려면 개체 탐색기에서 저장 프로시저 이름 **HumanResources.uspGetEmployeesTest** 를 마우스 오른쪽 단추로 클릭하고 **저장 프로시저 실행**을 선택합니다.  
  
12. **프로시저 실행** 창에서 @LastName 매개 변수의 값으로 Margheim을 입력하고 @FirstName 매개 변수의 값으로 Diane을 입력합니다.  
  
> [!WARNING]  
>  모든 사용자 입력에 대해 유효성을 검사합니다. 유효성 검사를 수행하기 전에는 사용자 입력을 연결하지 마세요. 유효성 검사가 수행되지 않은 사용자 입력으로부터 생성된 명령은 실행하지 마세요.  
  
###  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **쿼리 편집기에서 프로시저를 만들려면**  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  메뉴에서 **파일** 메뉴에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 다른 프로시저 이름을 사용하여 위와 같은 저장 프로시저를 만듭니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE PROCEDURE HumanResources.uspGetEmployeesTest2   
        @LastName nvarchar(50),   
        @FirstName nvarchar(50)   
    AS   
  
        SET NOCOUNT ON;  
        SELECT FirstName, LastName, Department  
        FROM HumanResources.vEmployeeDepartmentHistory  
        WHERE FirstName = @FirstName AND LastName = @LastName  
        AND EndDate IS NULL;  
    GO  
  
    ```  
  
4.  프로시저를 실행하려면 다음 예제를 새 쿼리 창에 복사하여 붙여 넣고 **실행**을 클릭합니다. 매개 변수 값을 지정하는 다른 메서드가 표시됩니다.  
  
    ```  
    EXECUTE HumanResources.uspGetEmployeesTest2 N'Ackerman', N'Pilar';  
    -- Or  
    EXEC HumanResources.uspGetEmployeesTest2 @LastName = N'Ackerman', @FirstName = N'Pilar';  
    GO  
    -- Or  
    EXECUTE HumanResources.uspGetEmployeesTest2 @FirstName = N'Pilar', @LastName = N'Ackerman';  
    GO  
  
    ```  
  
##  <a name="PowerShellProcedure"></a>   
## <a name="see-also"></a>참고 항목  
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
  
