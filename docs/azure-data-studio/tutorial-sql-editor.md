---
title: '자습서: Transact-SQL 편집기를 사용하여 데이터베이스 개체 만들기'
titleSuffix: Azure Data Studio
description: 이 자습서에서는 T-SQL 작업을 간소화하는 Azure Data Studio의 주요 기능을 보여 줍니다.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 06554c42bb7f98263fe48aa43f2366059ad5541f
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278239"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>자습서: Transact-SQL 편집기를 사용하여 데이터베이스 개체 만들기 - [!INCLUDE[name-sos](../includes/name-sos-short.md)]

쿼리, 저장 프로시저, 스크립트 등을 만들고 실행하는 것은 데이터베이스 전문가의 핵심 작업입니다. 이 자습서에서는 데이터베이스 개체를 만드는 T-SQL 편집기의 주요 기능을 보여 줍니다.

이 자습서에서는 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 다음을 수행하는 방법을 알아봅니다.
> [!div class="checklist"]
> * 데이터베이스 개체 검색
> * 테이블 데이터 편집 
> * 코드 조각을 사용하여 빠르게 T-SQL 작성
> * ‘정의 피킹(Peeking)’ 및 ‘정의로 이동’을 사용하여 데이터베이스 개체 세부 정보 보기  


## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 SQL Server 또는 Azure SQL Database *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면 다음 빠른 시작 중 하나를 완료합니다.

- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>데이터베이스 개체를 빠르게 찾고 일반 작업 수행

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]는 데이터베이스 개체를 빠르게 찾을 수 있는 검색 위젯을 제공합니다. 결과 목록에는 테이블에 대한 ‘데이터 편집’과 같이 선택한 개체와 관련된 일반 작업의 상황에 맞는 메뉴가 제공됩니다. 

1. 서버 사이드바를 열고(**Ctrl+G**), **데이터베이스**를 확장하고, **TutorialDB**를 선택합니다. 

1. **TutorialDB**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **관리**를 선택하여 ‘TutorialDB 대시보드’를 엽니다. 

   ![상황에 맞는 메뉴 - 관리](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 대시보드의 검색 위젯에서 **dbo.Customers**를 마우스 오른쪽 단추로 클릭하고 **데이터 편집**을 선택합니다.
   
   > [!TIP]
   > 많은 개체가 포함된 데이터베이스의 경우 검색 위젯을 사용하여 검색할 테이블, 뷰 등을 빠르게 찾을 수 있습니다.

   ![빠른 검색 위젯](./media/tutorial-sql-editor/quick-search-widget.png)

1. 첫 번째 행에서 **Email** 열을 편집하고 *orlando0\@adventure-works.com*을 입력한 다음 **Enter**를 눌러 변경 내용을 저장합니다.

   ![데이터 편집](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>T-SQL 코드 조각을 사용하여 저장 프로시저 만들기

[!INCLUDE[name-sos](../includes/name-sos-short.md)]는 문을 빠르게 만들기 위한 다양한 기본 제공 T-SQL 코드 조각을 제공합니다.


1. **Ctrl+N**을 눌러 새 쿼리 편집기를 엽니다.

2. 편집기에 **sql**을 입력하고, 아래쪽 화살표로 **sqlCreateStoredProcedure**를 선택하고, *Tab* 키(또는 *Enter* 키)를 눌러 저장 프로시저 만들기 코드 조각을 로드합니다.

   ![코드 조각 목록](./media/tutorial-sql-editor/snippet-list.png)

3. 저장 프로시저 만들기 코드 조각에는 빠른 편집을 위해 *StoredProcedureName* 및 *SchemaName* 필드가 설정되어 있습니다. *StoredProcedureName*을 선택하고, 마우스 오른쪽 단추를 클릭하고, **모든 항목 변경**을 선택합니다. 이제 *getCustomer*를 입력하면 모든 *StoredProcedureName* 항목이 *getCustomer*로 변경됩니다.

   ![코드 조각](./media/tutorial-sql-editor/snippet.png)

5. 모든 *SchemaName* 항목을 *dbo*로 변경합니다. 
6. 코드 조각에는 자리 표시자 매개 변수 및 업데이트해야 하는 본문 텍스트가 포함됩니다. *EXECUTE* 문에는 프로시저에 포함할 매개 변수 수를 알 수 없으므로 자리 표시자 텍스트도 포함됩니다. 이 자습서에서는 다음 코드와 같이 표시되도록 코드 조각을 업데이트합니다.

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerId, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerId = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. 저장 프로시저를 만들고 테스트 실행을 제공하려면 **F5** 키를 누릅니다.

이제 저장 프로시저가 만들어지고 **결과** 창에 JSON의 반환된 고객이 표시됩니다. 형식이 지정된 JSON을 보려면 반환된 레코드를 클릭합니다. 


## <a name="use-peek-definition"></a>정의 피킹(Peeking) 사용 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]는 정의 피킹(peeking) 기능을 사용하여 개체 정의를 보는 기능을 제공합니다. 이 섹션에서는 두 번째 저장 프로시저를 만들고 정의 피킹(peeking)을 사용하여 테이블에 있는 열을 확인하고 저장 프로시저의 본문을 빠르게 만듭니다.

1. **Ctrl+N**을 눌러 새 편집기를 엽니다. 

2. 편집기에 *sql*을 입력하고, 아래쪽 화살표로 *sqlCreateStoredProcedure*를 선택하고, *Tab* 키(또는 *Enter* 키)를 눌러 저장 프로시저 만들기 코드 조각을 로드합니다.
3. *StoredProcedureName*에 대해 *setCustomer*를 입력하고 *SchemaName*에 대해 *dbo*를 입력합니다.

3. @param 자리 표시자를 다음 매개 변수 정의로 바꿉니다.

   ```sql
   @json_val nvarchar(max)
   ```

4. 저장 프로시저의 본문을 다음 코드로 바꿉니다.
   ```sql
   INSERT INTO dbo.Customers
   ```

5. 방금 추가한 *INSERT* 줄에서 **dbo.Customers**를 마우스 오른쪽 단추로 클릭하고 **정의 피킹(Peeking)** 을 선택합니다.

   ![정의 피킹(Peeking)](./media/tutorial-sql-editor/peek-definition.png)

6. 테이블에 있는 열을 빠르게 확인할 수 있도록 테이블 정의가 표시됩니다. 열 목록을 참조하면 저장 프로시저에 대한 문을 쉽게 완료할 수 있습니다. 이전에 추가한 INSERT 문 만들기를 완료하여 저장 프로시저의 본문을 완료하고 정의 피킹(peeking) 창을 닫습니다.

   ```sql
   INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
    )
   ```
7. 쿼리 맨 아래에서 *EXECUTE* 명령을 삭제하거나 주석으로 처리합니다.
8. 전체 문은 다음 코드와 같이 표시됩니다.

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. *setCustomer* 저장 프로시저를 만들려면 **F5** 키를 누릅니다.

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>쿼리 결과를 JSON으로 저장을 사용하여 setCustomer 저장 프로시저 테스트

이전 섹션에서 만든 *setCustomer* 저장 프로시저에서는 JSON 데이터를 *\@json_val* 매개 변수에 전달해야 합니다. 이 섹션에서는 저장 프로시저를 테스트할 수 있도록 매개 변수에 전달할 올바른 형식의 JSON을 가져오는 방법을 보여 줍니다.

1. **서버** 사이드바에서 *dbo.Customers* 테이블을 마우스 오른쪽 단추로 클릭하고 **SELECT TOP 1000 Rows**를 클릭합니다.

2. 결과 뷰에서 첫 번째 행을 선택하고, 전체 행이 선택되었는지 확인하고(맨 왼쪽 열에서 숫자 1 클릭), **JSON으로 저장**을 선택합니다.  
3. 나중에 파일을 삭제할 수 있도록 기억할 위치로 폴더를 변경하고(예: 바탕 화면) **저장**을 클릭합니다. JSON 형식 파일이 열립니다.

   ![JSON으로 저장](./media/tutorial-sql-editor/save-as-json.png)

4. 편집기에서 JSON 데이터를 선택하고 복사합니다.
5. **Ctrl+N**을 눌러 새 편집기를 엽니다.
6. 이전 단계에서는 *setCustomer* 프로시저에 대한 호출을 완료하기 위해 올바른 형식의 데이터를 쉽게 가져오는 방법을 보여 줍니다. 다음 코드에서는 새 고객 세부 정보와 함께 동일한 JSON 형식을 사용하므로 *setCustomer* 프로시저를 테스트할 수 있습니다. 이 문에는 매개 변수를 선언하고 새 get 및 set 프로시저를 실행하는 구문이 포함됩니다. 이전 섹션에서 복사한 데이터를 붙여넣고 다음 예제와 동일하게 편집하거나 다음 문을 쿼리 편집기에 붙여넣을 수 있습니다.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerId": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. **F5** 키를 눌러 스크립트를 실행합니다. 이 스크립트는 새 고객을 삽입하고 새 고객의 정보를 JSON 형식으로 반환합니다. 결과를 클릭하여 형식이 지정된 뷰를 엽니다.

   ![테스트 결과](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * 스키마 개체 빠른 검색
> * 테이블 데이터 편집 
> * 코드 조각을 사용하여 T-SQL 스크립트 작성
> * 정의 피킹(Peeking) 및 정의로 이동을 사용하여 데이터베이스 개체 세부 정보에 대해 알아보기


**5개의 가장 느린 쿼리** 위젯을 사용하도록 설정하는 방법을 알아보려면 다음 자습서를 완료합니다.

> [!div class="nextstepaction"]
> [느린 쿼리 샘플 인사이트 위젯 사용](tutorial-qds-sql-server.md)
