---
title: '연습: SQL Server 단위 테스트 만들기 및 실행 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 992c1d8e-3729-438b-9ef4-cd103e28f145
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b3358a05940feb1905b65242877cf951e17776a
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094920"
---
# <a name="walkthrough-creating-and-running-a-sql-server-unit-test"></a>연습: SQL Server 단위 테스트 만들기 및 실행
이 연습에서는 일부 저장 프로시저의 동작을 확인하는 SQL Server 단위 테스트를 만듭니다. SQL Server 단위 테스트는 잘못된 응용 프로그램 동작을 일으킬 수 있는 코드 결함을 식별하기 위해 만듭니다. SQL Server 단위 테스트와 응용 프로그램 테스트는 자동화된 테스트 집합의 일부로 실행할 수 있습니다.  
  
이 연습에서는 다음 작업을 수행합니다.  
  
-   [데이터베이스 스키마가 포함된 스크립트 만들기](#CreateScript)  
  
-   [데이터베이스 프로젝트를 만들고 해당 스키마 가져오기](#CreateProjectAndImport)  
  
-   [격리된 개발 환경에 데이터베이스 프로젝트 배포](#DeployDBProj)  
  
-   [SQL Server 단위 테스트 만들기](#CreateDBUnitTests)  
  
-   [테스트 논리 정의](#DefineTestLogic)  
  
-   [SQL Server 단위 테스트 실행](#RunTests)  
  
-   [부정 단위 테스트 추가](#NegativeTest)  
  
단위 테스트 중 하나에서 저장 프로시저의 오류가 검색된 후 오류를 수정하고 테스트를 다시 실행합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 연습을 완료하려면 데이터베이스를 만들고 배포할 수 있는 권한이 있는 데이터베이스 서버(또는 LocalDB 데이터베이스)에 연결할 수 있어야 합니다. 자세한 내용은 [Visual Studio의 데이터베이스 기능에 필요한 권한](http://msdn.microsoft.com/library/aa833413(VS.100).aspx)을 참조하세요.  
  
## <a name="CreateScript"></a>데이터베이스 스키마가 포함된 스크립트 만들기  
  
#### <a name="to-create-a-script-from-which-you-can-import-a-schema"></a>스키마를 가져올 수 있는 스크립트를 만들려면  
  
1.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **파일**을 클릭합니다.  
  
    **새 파일** 대화 상자가 표시됩니다.  
  
2.  **범주** 목록에서 **일반** 을 클릭합니다(아직 강조 표시되어 있지 않은 경우).  
  
3.  **템플릿** 목록에서 **SQL 파일**을 클릭한 후 **열기**를 클릭합니다.  
  
    Transact\-SQL 편집기가 열립니다.  
  
4.  다음 Transact\-SQL 코드를 복사해서 Transact\-SQL 편집기에 붙여넣습니다.  
  
    ```  
    PRINT N'Creating Sales...';  
    GO  
    CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
    GO  
    PRINT N'Creating Sales.Customer...';  
    GO  
    CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Orders...';  
    GO  
    CREATE TABLE [Sales].[Orders] (  
        [CustomerID] INT      NOT NULL,  
        [OrderID]    INT      IDENTITY (1, 1) NOT NULL,  
        [OrderDate]  DATETIME NOT NULL,  
        [FilledDate] DATETIME NULL,  
        [Status]     CHAR (1) NOT NULL,  
        [Amount]     INT      NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDOrders...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDOrders] DEFAULT 0 FOR [YTDOrders];  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDSales...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDSales] DEFAULT 0 FOR [YTDSales];  
    GO  
    PRINT N'Creating Sales.Def_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_OrderDate] DEFAULT GetDate() FOR [OrderDate];  
    GO  
    PRINT N'Creating Sales.Def_Orders_Status...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_Status] DEFAULT 'O' FOR [Status];  
    GO  
    PRINT N'Creating Sales.PK_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [PK_Customer_CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.PK_Orders_OrderID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [PK_Orders_OrderID] PRIMARY KEY CLUSTERED ([OrderID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.FK_Orders_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [FK_Orders_Customer_CustID] FOREIGN KEY ([CustomerID]) REFERENCES [Sales].[Customer] ([CustomerID]) ON DELETE NO ACTION ON UPDATE NO ACTION;  
    GO  
    PRINT N'Creating Sales.CK_Orders_FilledDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_FilledDate] CHECK ((FilledDate >= OrderDate) AND (FilledDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.CK_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_OrderDate] CHECK ((OrderDate > '01/01/2005') and (OrderDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.uspCancelOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'X'  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspFillOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspFillOrder]  
    @OrderID INT, @FilledDate DATETIME  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'F',  
           [FilledDate] = @FilledDate  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspNewCustomer...';  
    GO  
    CREATE PROCEDURE [Sales].[uspNewCustomer]  
    @CustomerName NVARCHAR (40)  
    AS  
    BEGIN  
    INSERT INTO [Sales].[Customer] (CustomerName) VALUES (@CustomerName);  
    SELECT SCOPE_IDENTITY()  
    END  
    GO  
    PRINT N'Creating Sales.uspPlaceNewOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspPlaceNewOrder]  
    @CustomerID INT, @Amount INT, @OrderDate DATETIME, @Status CHAR (1)='O'  
    AS  
    BEGIN  
    DECLARE @RC INT  
    BEGIN TRANSACTION  
    INSERT INTO [Sales].[Orders] (CustomerID, OrderDate, FilledDate, Status, Amount)   
         VALUES (@CustomerID, @OrderDate, NULL, @Status, @Amount)  
    SELECT @RC = SCOPE_IDENTITY();  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders + @Amount  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    RETURN @RC  
    END  
    GO  
    CREATE PROCEDURE [Sales].[uspShowOrderDetails]  
    @CustomerID INT=0  
    AS  
    BEGIN  
    SELECT [C].[CustomerName], CONVERT(date, [O].[OrderDate]), CONVERT(date, [O].[FilledDate]), [O].[Status], [O].[Amount]  
      FROM [Sales].[Customer] AS C  
      INNER JOIN [Sales].[Orders] AS O  
         ON [O].[CustomerID] = [C].[CustomerID]  
      WHERE [C].[CustomerID] = @CustomerID  
    END  
    GO  
    ```  
  
5.  파일을 저장합니다. 다음 절차에서 이 스크립트를 사용해야 하므로 위치를 기록해둡니다.  
  
6.  **파일** 메뉴에서 **솔루션 닫기**를 클릭합니다.  
  
    그런 다음 데이터베이스 프로젝트를 만들고 앞에서 만든 스크립트에서 스키마를 가져옵니다.  
  
## <a name="CreateProjectAndImport"></a>데이터베이스 프로젝트를 만들고 해당 스키마 가져오기  
  
#### <a name="to-create-a-database-project"></a>데이터베이스 프로젝트를 만들려면  
  
1.  **파일** 메뉴에서 **새로 만들기**를 가리키고 **프로젝트**를 클릭합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **설치된 템플릿**에서 **SQL Server** 노드를 선택한 후 **SQL Server 데이터베이스 프로젝트**를 선택합니다.  
  
3.  **이름**에 **SimpleUnitTestDB**를 입력합니다.  
  
4.  **솔루션용 디렉터리 만들기** 확인란이 아직 선택되어 있지 않은 경우 선택합니다.  
  
5.  **소스 제어에 추가** 확인란의 선택이 아직 취소되지 않은 경우 취소하고 **확인**을 클릭합니다.  
  
    데이터베이스 프로젝트가 만들어지고 **솔루션 탐색기**에 나타납니다. 그런 다음 스크립트에서 데이터베이스 스키마를 가져옵니다.  
  
#### <a name="to-import-a-database-schema-from-a-script"></a>스크립트에서 데이터베이스 스키마를 가져오려면  
  
1.  **프로젝트** 메뉴에서 **가져오기**를 클릭한 후 **스크립트(\*.sql)** 를 클릭합니다.  
  
2.  시작 페이지를 읽은 후 **다음** 을 클릭합니다.  
  
3.  **찾아보기**를 클릭하고 .sql 파일을 저장한 디렉터리로 이동합니다.  
  
4.  .sql 파일을 두 번 클릭하고 **마침**을 클릭합니다.  
  
    스크립트를 가져오고 해당 스크립트에 정의된 개체가 데이터베이스 프로젝트에 추가됩니다.  
  
5.  요약 내용을 검토하고 **마침** 을 클릭하여 작업을 완료합니다.  
  
    > [!NOTE]  
    > Sales.uspFillOrder 프로시저에는 이 절차의 뒷부분에서 검색하고 수정할 수 있도록 의도적인 코딩 오류가 포함되어 있습니다.  
  
#### <a name="to-examine-the-resulting-project"></a>결과 프로젝트를 검사하려면  
  
1.  **솔루션 탐색기**에서 프로젝트로 가져온 스크립트 파일을 검사합니다.  
  
2.  **SQL Server 개체 탐색기**의 프로젝트 노드에서 데이터베이스를 확인합니다.  
  
## <a name="DeployDBProj"></a>LocalDB에 배포  
기본적으로 F5 키를 누르면 데이터베이스가 LocalDB 데이터베이스에 배포(또는 게시)됩니다. 프로젝트 속성 페이지의 디버그 탭으로 이동하고 연결 문자열을 변경하여 데이터베이스 위치를 변경할 수 있습니다.  
  
## <a name="CreateDBUnitTests"></a>SQL Server 단위 테스트 만들기  
  
#### <a name="to-create-a-sql-server-unit-test-for-the-stored-procedures"></a>저장 프로시저에 대한 SQL Server 단위 테스트를 만들려면  
  
1.  **SQL Server 개체 탐색기**에서 **SimpleUnitTestDB**의 프로젝트 노드를 확장하고 **프로그래밍 기능** 및 **저장 프로시저** 노드를 차례로 확장합니다.  
  
2.  저장 프로시저 중 하나를 마우스 오른쪽 단추로 클릭하고 **단위 테스트 만들기**를 클릭하여 **단위 테스트 만들기** 대화 상자를 표시합니다.  
  
3.  다섯 개의 저장된 프로시저 전체에 대한 확인란을 선택합니다. **Sales.uspCancelOrder**, **Sales.uspFillOrder**, **Sales.uspNewCustomer**, **Sales.uspPlaceNewOrder**및 **Sales.uspShowOrderDetails**.  
  
4.  **프로젝트** 드롭다운 목록에서 **새 Visual C# 테스트 프로젝트 만들기**를 선택합니다.  
  
5.  프로젝트 이름 및 클래스 이름에 대해 기본 이름을 사용하고 **확인**을 클릭합니다.  
  
6.  테스트 구성 대화 상자의 **다음 데이터 연결을 사용하여 단위 테스트 실행**에서 이 연습의 초반에 배포한 데이터베이스에 대한 연결을 지정합니다. 예를 들어 기본 배포 위치인 LocalDB를 사용한 경우 **새 연결**을 클릭하고 **(LocalDB)\Projects**를 지정합니다. 그런 다음 데이터베이스의 이름을 선택합니다. 그리고 확인을 클릭하여 **연결 속성** 대화 상자를 닫습니다.  
  
    > [!NOTE]  
    > 제한된 권한을 포함하는 뷰 또는 저장 프로시저를 테스트해야 할 경우 일반적으로 이 단계에서 해당 연결을 지정합니다. 그런 다음 테스트의 유효성을 검사하기 위해 보다 포괄적인 권한이 있는 보조 연결을 지정합니다. 보조 연결이 있으면 해당 사용자를 데이터베이스 프로젝트에 추가하고 사전 배포 스크립트에서 해당 사용자에 대한 로그인을 만듭니다.  
  
7.  테스트 구성 대화 상자의 **배포** 섹션에서 **단위 테스트를 실행하기 전에 데이터베이스 프로젝트를 자동으로 배포** 확인란을 선택합니다.  
  
8.  **데이터베이스 프로젝트**에서 **SimpleUnitTestDB.sqlproj**를 클릭합니다.  
  
9. **배포 구성**에서 **디버그**를 클릭합니다.  
  
    SQL Server 단위 테스트의 일부로 테스트 데이터를 생성할 수도 있습니다. 이 연습에서는 테스트로 고유 데이터가 만들어지므로 이 단계를 건너뜁니다.  
  
10. **확인**을 클릭합니다.  
  
    테스트 프로젝트가 빌드되고 SQL Server 단위 테스트 디자이너가 나타납니다. 그런 다음, SQL Server 단위 테스트의 Transact\-SQL 스크립트에서 테스트 논리를 업데이트합니다.  
  
## <a name="DefineTestLogic"></a>테스트 논리 정의  
이 매우 간단한 데이터베이스에는 Customer 및 Order라는 두 개의 테이블이 포함됩니다. 다음 저장 프로시저를 사용하여 데이터베이스를 업데이트합니다.  
  
-   uspNewCustomer - 이 저장 프로시저는 Customer 테이블에 고객의 YTDOrders 및 YTDSales 열을 0으로 설정하는 레코드를 추가합니다.  
  
-   uspPlaceNewOrder - 이 저장 프로시저는 지정된 고객에 대한 레코드를 Orders 테이블에 추가하고 Customer 테이블에 있는 해당 레코드에서 YTDOrders 값을 업데이트합니다.  
  
-   uspFillOrder - 이 저장 프로시저는 상태를 'O'에서 'F'로 변경하여 Orders 테이블에서 레코드를 업데이트하고 Customer 테이블의 해당 레코드에서 YTDSales 값을 증분합니다.  
  
-   uspCancelOrder - 이 저장 프로시저는 상태를 'O'에서 'X'로 변경하여 Orders 테이블에서 레코드를 업데이트하고 Customer 테이블의 해당 레코드에서 YTDOrders 값을 감소시킵니다.  
  
-   uspShowOrderDetails - 이 저장 프로시저는 Orders 테이블을 Custom 테이블과 조인하고 특정 고객에 대한 레코드를 표시합니다.  
  
> [!NOTE]  
> 이 예에서는 간단한 SQL Server 단위 테스트를 만드는 방법을 보여 줍니다. 실제 환경의 데이터베이스에서는 특정 고객에 대해 상태가 'O' 또는 'F'인 모든 주문의 합계를 계산할 수 있습니다. 이 연습의 프로시저에는 오류 처리가 포함되지 않습니다. 예를 들어 이미 채워진 주문에 대해 uspFillOrder를 호출하지 못하도록 방지하는 기능이 없습니다.  
  
각 테스트는 데이터베이스가 깨끗한 상태로 시작된다고 가정합니다. 다음 조건을 확인하는 테스트를 만듭니다.  
  
-   uspNewCustomer - 저장 프로시저를 실행한 후 Customer 테이블에 행이 하나 포함되는지 확인합니다.  
  
-   uspPlaceNewOrder - CustomerID가 1인 고객에 대해 $100 주문을 입력합니다. 해당 고객의 YTDOrders 값이 100인지 확인하고 YTDSales 값이 0인지 확인합니다.  
  
-   uspFillOrder - CustomerID가 1인 고객에 대해 $50 주문을 입력합니다. 해당 주문을 채웁니다. YTDOrders 및 YTDSales 값이 모두 50인지 확인합니다.  
  
-   uspShowOrderDetails - CustomerID가 1인 고객에 대해 $100, $50 및 $5 주문을 입력합니다. uspShowOrderDetails가 올바른 열 수를 반환하고 결과 집합의 체크섬이 예상한 값인지 확인합니다.  
  
> [!NOTE]  
> 일반적으로는 전체 SQL Server 단위 테스트에 대해 다른 열이 올바르게 설정되었는지 확인합니다. 이 연습에서는 연습 내용이 너무 늘어나지 않도록 uspCancelOrder의 동작을 확인하는 방법에 대해서는 설명하지 않습니다.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspnewcustomer"></a>uspNewCustomer에 대한 SQL Server 단위 테스트를 작성하려면  
  
1.  SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspNewCustomerTest**를 클릭하고 인접한 목록에 **테스트**가 강조 표시되어 있는지 확인합니다.  
  
    이전 단계를 수행한 후에는 단위 테스트에서 테스트 작업에 대한 테스트 스크립트를 만들 수 있습니다.  
  
2.  다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    -- ssNoVersion unit test for Sales.uspNewCustomer  
    DECLARE @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @CustomerName = 'Fictitious Customer';  
  
    EXECUTE @RC = [Sales].[uspNewCustomer] @CustomerName;  
  
    SELECT * FROM [Sales].[Customer];  
    ```  
  
3.  **테스트 조건** 창에서 결과 불충분 테스트 조건을 클릭하고 **테스트 조건 삭제** 아이콘(빨간색 X)을 클릭합니다.  
  
4.  **테스트 조건** 창의 목록에서 **행 개수**를 클릭하고 **테스트 조건 추가** 아이콘(녹색 +)을 클릭합니다.  
  
5.  테스트 조건을 선택하고 F4 키를 눌러 **속성** 창을 열고 **행 개수** 속성을 1로 설정합니다.  
  
6.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
    이제 uspPlaceNewOrder에 대해 단위 테스트 논리를 정의합니다.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspplaceneworder"></a>uspPlaceNewOrder에 대한 SQL Server 단위 테스트를 작성하려면  
  
1.  SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspPlaceNewOrderTest**를 클릭하고 인접한 목록에 **테스트**가 강조 표시되어 있는지 확인합니다.  
  
    이 단계를 수행한 후에는 단위 테스트에서 테스트 작업에 대한 테스트 스크립트를 만들 수 있습니다.  
  
2.  다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    -- ssNoVersion unit test for Sales.uspPlaceNewOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- place an order for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    -- verify that the YTDOrders value is correct.  
    SELECT @RC = [YTDOrders] FROM [Sales].[Customer] WHERE [CustomerID] = @CustomerID  
  
    SELECT @RC AS RC  
    ```  
  
3.  **테스트 조건** 창에서 결과 불충분 테스트 조건을 클릭하고 **테스트 조건 삭제**를 클릭합니다.  
  
4.  **테스트 조건** 창의 목록에서 **스칼라 값** 을 클릭하고 **테스트 조건 추가**를 클릭합니다.  
  
5.  **속성** 창에서 **예상 값** 속성을 100으로 설정합니다.  
  
6.  SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspPlaceNewOrderTest**를 클릭하고 인접한 목록에 **테스트 전**이 강조 표시되어 있는지 확인합니다.  
  
    이 단계를 수행한 후 테스트를 실행하는 데 필요한 상태로 데이터를 설정하는 문을 지정할 수 있습니다. 이 예에서는 주문을 입력하기 전에 Customer 레코드를 만들어야 합니다.  
  
7.  **만들려면 여기를 클릭합니다.** 를 클릭해서 테스트 전 스크립트를 만듭니다.  
  
8.  다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    /*  
    Add Transact-SQL statements here that you want to run before  
    the test script is run.  
    */  
    -- Add a customer for this test with the name 'Fictitious Customer'  
    DECLARE @NewCustomerID AS INT, @CustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
       @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
    ```  
  
9. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
    이제 uspFillOrder에 대해 단위 테스트를 만듭니다.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspfillorder"></a>uspFillOrder에 대한 SQL Server 단위 테스트를 작성하려면  
  
1.  SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspFillOrderTest**를 클릭하고 인접한 목록에 **테스트**가 강조 표시되어 있는지 확인합니다.  
  
    이 단계를 수행한 후에는 단위 테스트에서 테스트 작업에 대한 테스트 스크립트를 만들 수 있습니다.  
  
2.  다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
    -- Get the most recently added order.  
    SELECT @OrderID = MAX([OrderID]) FROM [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspFillOrder] @OrderID, @FilledDate;  
  
    -- verify that the YTDOrders value is correct.  
    SELECT @RC = [YTDSales] FROM [Sales].[Customer] WHERE [CustomerID] = @CustomerID  
  
    SELECT @RC AS RC;  
    ```  
  
3.  **테스트 조건** 창에서 결과 불충분 테스트 조건을 클릭하고 **테스트 조건 삭제**를 클릭합니다.  
  
4.  **테스트 조건** 창의 목록에서 **스칼라 값** 을 클릭하고 **테스트 조건 추가**를 클릭합니다.  
  
5.  **속성** 창에서 **예상 값** 속성을 100으로 설정합니다.  
  
6.  SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspFillOrderTest**를 클릭하고 인접한 목록에 **테스트 전**이 강조 표시되어 있는지 확인합니다. 이 단계를 수행한 후 테스트를 실행하는 데 필요한 상태로 데이터를 설정하는 문을 지정할 수 있습니다. 이 예에서는 주문을 입력하기 전에 Customer 레코드를 만들어야 합니다.  
  
7.  **만들려면 여기를 클릭합니다.** 를 클릭해서 테스트 전 스크립트를 만듭니다.  
  
8.  다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    /*  
    Add Transact-SQL statements here that you want to run before  
    the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place an order for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
    ```  
  
9. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspshoworderdetails"></a>uspShowOrderDetails에 대한 SQL Server 단위 테스트를 작성하려면  
  
1.  SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspShowOrderDetailsTest**를 클릭하고 인접한 목록에 **테스트**가 강조 표시되어 있는지 확인합니다.  
  
    이 단계를 수행한 후에는 단위 테스트에서 테스트 작업에 대한 테스트 스크립트를 만들 수 있습니다.  
  
2.  다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspShowOrderDetails] @CustomerID;  
  
    SELECT @RC AS RC;  
    ```  
  
3.  **테스트 조건** 창에서 결과 불충분 테스트 조건을 클릭하고 **테스트 조건 삭제**를 클릭합니다.  
  
4.  **테스트 조건** 창의 목록에서 **필요한 스키마** 를 클릭하고 **테스트 조건 추가**를 클릭합니다.  
  
5.  **속성** 창의 **구성** 속성에서 찾아보기 단추(‘**…**’)를 클릭합니다.  
  
6.  **expectedSchemaCondition1에 대한 구성** 대화 상자에서 데이터베이스에 대한 연결을 지정합니다. 예를 들어 기본 배포 위치인 LocalDB를 사용한 경우 **새 연결**을 클릭하고 **(LocalDB)\Projects**를 지정합니다. 그런 다음 데이터베이스의 이름을 선택합니다.  
  
7.  **검색**을 클릭합니다. 필요한 경우 데이터가 표시될 때까지 **검색**을 클릭합니다.  
  
    단위 테스트의 Transact\-SQL 본문이 실행되고 결과 스키마가 대화 상자에 표시됩니다. 테스트 전 코드가 실행되지 않았기 때문에 데이터가 반환되지 않습니다. 스키마만 확인하고 데이터는 확인하지 않으므로 문제가 없습니다.  
  
8.  **확인**을 클릭합니다.  
  
    실행된 스키마가 테스트 조건과 함께 저장됩니다.  
  
9. SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspShowOrderDetailsTest**를 클릭하고 인접한 목록에 **테스트 전**이 강조 표시되어 있는지 확인합니다. 이 단계를 수행한 후 테스트를 실행하는 데 필요한 상태로 데이터를 설정하는 문을 지정할 수 있습니다. 이 예에서는 주문을 입력하기 전에 Customer 레코드를 만들어야 합니다.  
  
10. **만들려면 여기를 클릭합니다.** 를 클릭해서 테스트 전 스크립트를 만듭니다.  
  
11. 다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    /*  
    Add Transact-SQL statements here to run before the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'FictitiousCustomer'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place 3 orders for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 100, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 50, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 5, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
    ```  
  
12. SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspShowOrderDetailsTest**를 클릭하고 인접한 목록에서 **테스트**를 클릭합니다.  
  
    체크섬 조건을 테스트 전이 아니라 테스트에 적용할 것이므로 이 작업을 반드시 수행해야 합니다.  
  
13. **테스트 조건** 창의 목록에서 **데이터 체크섬** 을 클릭하고 **테스트 조건 추가**를 클릭합니다.  
  
14. **속성** 창의 **구성** 속성에서 찾아보기 단추(‘**…**’)를 클릭합니다.  
  
15. **checksumCondition1에 대한 구성** 대화 상자에서 데이터베이스에 대한 연결을 지정합니다.  
  
16. 대화 상자의 **연결 편집** 단추 아래에 있는 Transact\-SQL을 다음 코드로 바꿉니다.  
  
    ```  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place 3 orders for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 100, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 50, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 5, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @FilledDate AS DATETIME;  
    DECLARE @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspShowOrderDetails] @CustomerID;  
  
    SELECT @RC AS RC;  
    ```  
  
    이 코드는 테스트 전의 Transact\-SQL 코드를 테스트 자체의 Transact\-SQL과 조합합니다. 실행 시 테스트에서 반환되는 것과 동일한 결과가 반환되도록 하려면 두 코드가 모두 필요합니다.  
  
17. **검색**을 클릭합니다. 필요한 경우 데이터가 표시될 때까지 **검색**을 클릭합니다.  
  
    지정한 Transact\-SQL이 실행되고 반환된 데이터에 대해 체크섬이 계산됩니다.  
  
18. **확인**을 클릭합니다.  
  
    계산된 체크섬이 테스트 조건과 함께 저장됩니다. 예상 체크섬이 데이터 체크섬 테스트 조건의 값 열에 표시됩니다.  
  
19. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
    이제 테스트를 실행할 준비가 되었습니다.  
  
## <a name="RunTests"></a>SQL Server 단위 테스트 실행  
  
#### <a name="to-run-the-sql-server-unit-tests"></a>SQL Server 단위 테스트를 실행하려면  
  
1.  **테스트** 메뉴에서 **창**을 가리킨 후 **테스트 뷰**(Visual Studio 2010) 또는 **테스트 탐색기**(Visual Studio 2012)를 클릭합니다.  
  
2.  **테스트 뷰** 창(Visual Studio 2010)의 도구 모음에서 **새로 고침**을 클릭하여 테스트 목록을 업데이트합니다. **테스트 탐색기**(Visual Studio 2012)에서 테스트 목록을 보려면 솔루션을 빌드합니다.  
  
    **테스트 뷰** 또는 **테스트 탐색기** 창에는 이 연습의 초반에 만들었고 Transact\-SQL 문 및 테스트 조건을 추가한 테스트가 나열됩니다. 이름이 TestMethod1인 테스트는 비어 있으며 이 연습에서 사용되지 않습니다.  
  
3.  **Sales_uspNewCustomerTest**를 마우스 오른쪽 단추로 클릭하고 **선택 항목 실행**을 클릭합니다.  
  
    Visual Studio에서는 데이터베이스에 연결하고 데이터 생성 계획을 적용하기 위해 지정한 권한 있는 컨텍스트를 사용합니다. Visual Studio에서는 테스트에서 Transact\-SQL 스크립트를 실행하기 전에 실행 컨텍스트로 전환합니다. 마지막으로 Visual Studio는 테스트 조건에서 지정한 것에 대해 Transact\-SQL 스크립트를 평가하고 성공 또는 실패 결과가 **테스트 결과** 창에 표시됩니다.  
  
4.  **테스트 결과** 창에서 결과를 확인합니다.  
  
    테스트가 성공합니다. 즉, 테스트를 실행할 때 **SELECT** 문이 한 개의 행을 반환합니다.  
  
5.  Sales_uspPlaceNewOrderTest, Sales_uspFillOrderTest 및 Sales_uspShowOrderDetailsTest 테스트에 대해 3단계를 반복합니다. 결과는 다음과 같이 됩니다.  
  
    |테스트|예상 결과|  
    |--------|-------------------|  
    |Sales_uspPlaceNewOrderTest|통과|  
    |Sales_uspShowOrderDetailsTest|통과|  
    |Sales_uspFillOrderTest|다음 오류와 함께 실패: "ScalarValueCondition Condition (scalarValueCondition2) 실패: 결과 집합 1 행 1 열 1: 값이 일치하지 않습니다. '100'이(가) 필요한데 '-100'입니다." 이 오류는 저장 프로시저의 정의에 사소한 오류가 포함되었기 때문에 발생합니다.|  
  
    이제 오류를 수정하고 다시 테스트를 실행합니다.  
  
#### <a name="to-correct-the-error-in-salesuspfillorder"></a>Sales.uspFillOrder에서 오류를 수정하려면  
  
1.  **SQL Server 개체 탐색기**의 데이터베이스에 대한 프로젝트 노드에서 **uspFillOrder** 저장 프로시저를 두 번 클릭하여 Transact\-SQL 편집기에서 해당 정의를 엽니다.  
  
2.  정의에서 다음 Transact\-SQL 문을 찾습니다.  
  
    ```  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales - @Delta  
        WHERE [CustomerID] = @CustomerID  
    ```  
  
3.  다음 문과 일치하도록 문에서 SET 절을 변경합니다.  
  
    ```  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales + @Delta  
        WHERE [CustomerID] = @CustomerID  
    ```  
  
4.  **파일** 메뉴에서 **uspFillOrder.sql 저장**을 클릭합니다.  
  
5.  **테스트 뷰**에서 **Sales_uspFillOrderTest**를 마우스 오른쪽 단추로 클릭하고 **선택 항목 실행**을 클릭합니다.  
  
    테스트가 통과합니다.  
  
## <a name="NegativeTest"></a>부정 단위 테스트 추가  
테스트가 실패해야 할 때 제대로 실패하는지 확인하기 위해 부정 테스트를 만들 수 있습니다. 예를 들어 이미 채워진 주문을 취소하려고 하면 테스트가 실패해야 합니다. 이 연습의 일부에서는 Sales.uspCancelOrder 저장 프로시저에 대한 부정 단위 테스트를 만듭니다.  
  
부정 테스트를 만들고 확인하려면 다음 작업을 수행해야 합니다.  
  
-   실패 조건으로 테스트할 저장 프로시저를 업데이트합니다.  
  
-   새 단위 테스트를 정의합니다.  
  
-   실패해야 함을 나타내도록 단위 테스트의 코드를 수정합니다.  
  
-   단위 테스트를 실행합니다.  
  
#### <a name="to-update-the-stored-procedure"></a>저장 프로시저를 업데이트하려면  
  
1.  **SQL Server 개체 탐색기**의 SimpleUnitTestDB 데이터베이스에 대한 프로젝트 노드에서 프로그래밍 기능 노드, 저장 프로시저 노드를 차례로 확장하고 uspCancelOrder를 두 번 클릭합니다.  
  
2.  Transact\-SQL 편집기에서 다음 코드와 일치하도록 프로시저 정의를 업데이트합니다.  
  
    ```  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
        DECLARE @Delta INT, @CustomerID INT, @PriorStatus CHAR(1)  
        BEGIN TRANSACTION  
            BEGIN TRY  
                IF (NOT EXISTS(SELECT [CustomerID] from [Sales].[Orders] WHERE [OrderID] = @OrderID))  
                BEGIN  
                    -- Specify WITH LOG option so that the error is  
                    -- written to the application log.  
                    RAISERROR( 'That order does not exist.', -- Message text  
                               16, -- severity  
                                1 -- state  
                            ) WITH LOG;  
                END  
  
                SELECT @Delta = [Amount], @CustomerID = [CustomerID], @PriorStatus = [Status]  
                 FROM [Sales].[Orders] WHERE [OrderID] = @OrderID  
  
                IF @PriorStatus <> 'O'   
                BEGIN  
                    -- Specify WITH LOG option so that the error is  
                    -- written to the application log.  
                    RAISERROR ( 'You can only cancel open orders.', -- Message text  
                                16, -- Severity  
                                1 -- State  
                                ) WITH LOG;  
                END  
                ELSE  
                BEGIN  
                    -- If we make it to here, then we can cancel the order. Update the status to 'X' first...  
                    UPDATE [Sales].[Orders]  
                       SET [Status] = 'X'  
                    WHERE [OrderID] = @OrderID  
                    -- and then remove the amount from the YTDOrders for the customer  
                    UPDATE [Sales].[Customer]  
                           SET  
                               YTDOrders = YTDOrders - @Delta  
                    WHERE [CustomerID] = @CustomerID  
                    COMMIT TRANSACTION  
                    RETURN 1; -- indicate success  
                END  
            END TRY  
            BEGIN CATCH  
                DECLARE @ErrorMessage NVARCHAR(4000);  
                DECLARE @ErrorSeverity INT;  
                DECLARE @ErrorState INT;  
  
                SELECT @ErrorMessage = ERROR_MESSAGE(),  
                       @ErrorSeverity = ERROR_SEVERITY(),  
                       @ErrorState = ERROR_STATE();  
  
                ROLLBACK TRANSACTION  
                -- Use RAISERROR inside the CATCH block to return  
                -- error information about the original error that  
                -- caused execution to jump to the CATCH block.  
                RAISERROR (@ErrorMessage, -- Mesasge text  
                           @ErrorSeverity, -- Severity  
                           @ErrorState -- State  
                          );  
                RETURN 0; -- indicate failure  
            END CATCH;  
    END  
    ```  
  
3.  **파일** 메뉴에서 **Save uspCancelOrder.sql 저장**을 클릭합니다.  
  
4.  F5 키를 눌러 **SimpleUnitTestDB**를 배포합니다.  
  
    업데이트를 uspCancelOrder 저장 프로시저에 배포합니다. 다른 개체는 변경하지 않았으므로 저장 프로시저만 업데이트됩니다.  
  
    이제 이 프로시저에 대해 연관된 단위 테스트를 정의합니다.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspcancelorder"></a>uspCancelOrder에 대한 SQL Server 단위 테스트를 작성하려면  
  
1.  SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspCancelOrderTest**를 클릭하고 인접한 목록에 **테스트**가 강조 표시되어 있는지 확인합니다.  
  
    이 단계를 수행한 후에는 단위 테스트에서 테스트 작업에 대한 테스트 스크립트를 만들 수 있습니다.  
  
2.  다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
    -- Get the most recently added order.  
    SELECT @OrderID = MAX([OrderID]) FROM [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
  
    -- try to cancel an order for that customer that has already been filled  
    EXECUTE @RC = [Sales].[uspCancelOrder] @OrderID;  
  
    SELECT @RC AS RC;  
    ```  
  
3.  **테스트 조건** 창에서 결과 불충분 테스트 조건을 클릭하고 **테스트 조건 삭제** 아이콘을 클릭합니다.  
  
4.  **테스트 조건** 창의 목록에서 **스칼라 값** 을 클릭하고 **테스트 조건 추가** 아이콘을 클릭합니다.  
  
5.  **속성** 창에서 **예상 값** 속성을 0으로 설정합니다.  
  
6.  SQL Server 단위 테스트 디자이너의 탐색 모음에서 **Sales_uspCancelOrderTest를** 클릭하고 인접한 목록에 **테스트 전**이 강조 표시되어 있는지 확인합니다. 이 단계를 수행한 후 테스트를 실행하는 데 필요한 상태로 데이터를 설정하는 문을 지정할 수 있습니다. 이 예에서는 주문을 입력하기 전에 Customer 레코드를 만들어야 합니다.  
  
7.  **만들려면 여기를 클릭합니다.** 를 클릭해서 테스트 전 스크립트를 만듭니다.  
  
8.  다음 문과 일치하도록 Transact\-SQL 편집기에서 Transact\-SQL 문을 업데이트합니다.  
  
    ```  
    /*  
    Add Transact-SQL statements here to run before the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @FilledDate AS DATETIME, @Status AS CHAR (1), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
       @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
       @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place an order for that customer  
    EXECUTE @OrderID = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    -- fill the order for that customer  
    EXECUTE @RC = [Sales].[uspFillOrder] @OrderID, @FilledDate;  
  
    COMMIT TRANSACTION  
    ```  
  
9. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
    이제 테스트를 실행할 준비가 되었습니다.  
  
#### <a name="to-run-the-sql-server-unit-tests"></a>SQL Server 단위 테스트를 실행하려면  
  
1.  **테스트 뷰**에서 **Sales_uspCancelOrderTest**를 마우스 오른쪽 단추로 클릭하고 **선택 항목 실행**을 클릭합니다.  
  
2.  **테스트 결과** 창에서 결과를 확인합니다.  
  
    테스트가 실패하고 다음 오류가 표시됩니다.  
  
    **Test 메서드 TestProject1.SqlServerUnitTests1.Sales_uspCancelOrderTest가 예외를 throw함: System.Data.SqlClient.SqlException: 열린 주문만 취소할 수 있습니다.**  
  
    이제 예외가 예상됨을 나타내도록 코드를 수정합니다.  
  
#### <a name="to-modify-the-code-for-the-unit-test"></a>단위 테스트에 대한 코드를 수정하려면  
  
1.  **솔루션 탐색기**에서 **TestProject1**을 확장하고 **SqlServerUnitTests1.cs**를 마우스 오른쪽 단추로 클릭한 후 **코드 보기**를 클릭합니다.  
  
2.  코드 편집기에서 Sales_uspCancelOrderTest 메서드로 이동합니다. 다음 코드와 일치하도록 메서드의 특성을 수정합니다.  
  
    ```  
    [TestMethod(), ExpectedSqlException(Severity=16, MatchFirstError=false, State=1)]  
    public void Sales_uspCancelOrderTest()  
    ```  
  
    특정 예외가 표시되도록 지정합니다. 선택적으로 특정 오류 번호를 지정할 수도 있습니다. 이 특성을 추가하지 않으면 단위 테스트가 실패하고 메시지가 테스트 결과 창에 표시됩니다.  
  
    > [!IMPORTANT]  
    > 현재 Visual Studio 2012에서는 ExpectedSqlException 특성을 지원하지 않습니다. 이 문제를 해결하는 방법은 ["예상 실패" 데이터베이스 단위 테스트를 실행할 수 없음](http://social.msdn.microsoft.com/Forums/en-US/ssdt/thread/e74e06ad-e3c9-4cb0-97ad-a6f235a52345)을 참조하십시오.  
  
3.  파일 메뉴에서 SqlServerUnitTests1.cs 저장을 클릭합니다.  
  
    이제 단위 테스트를 다시 실행하여 예상한 대로 실패하는지 확인합니다.  
  
#### <a name="to-re-run-the-sql-server-unit-tests"></a>SQL Server 단위 테스트를 다시 실행하려면  
  
1.  **테스트 뷰**에서 **Sales_uspCancelOrderTest**를 마우스 오른쪽 단추로 클릭하고 **선택 항목 실행**을 클릭합니다.  
  
2.  **테스트 결과** 창에서 결과를 확인합니다.  
  
    테스트가 성공합니다. 즉, 실패해야 할 때 프로시저가 실패했습니다.  
  
## <a name="next-steps"></a>Next Steps  
일반적인 프로젝트에서는 모든 중요한 데이터베이스 개체가 올바르게 작동하는지 확인하기 위해 추가 단위 테스트를 정의해야 합니다. 테스트 집합이 완료되었으면 해당 테스트를 버전 제어에 체크 인하여 팀과 공유합니다.  
  
기준선을 설정한 후에는 데이터베이스 개체를 만들고, 수정한 후 변경 사항으로 인해 예상된 동작이 중단되는지 여부를 확인하기 위한 관련 테스트를 만들 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[방법: 빈 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[방법: SQL Server 단위 테스트 실행 구성](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
