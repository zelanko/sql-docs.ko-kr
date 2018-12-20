---
title: '자습서: Azure Data Studio TRANSACT-SQL 편집기를 사용 하 여 데이터베이스 개체를 만드는 | Microsoft Docs'
description: 이 자습서에서는 T-SQL을 사용 하 여 단순화 하는 Azure Data Studio의 주요 기능을 보여줍니다.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2a517b1efb6a86d70bd05f9a1418792c0b61098
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49355934"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>자습서: TRANSACT-SQL 편집기를 사용하여 데이터베이스 개체 만들기 - [!INCLUDE[name-sos](../includes/name-sos-short.md)]

쿼리 작성 및 실행, 저장된 프로시저, 스크립트 등은 데이터베이스 전문가의 핵심 작업입니다. 이 자습서에서는 데이터베이스 개체를 만드는 T-SQL 편집기의 주요 기능을 설명합니다.

이 자습서에서 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 사용법을 알아봅니다.
> [!div class="checklist"]
> * 데이터베이스 개체 검색
> * 테이블 데이터 편집 
> * 코드 조각을 사용하여 T-SQL을 신속하게 작성
> * *정의 피킹*과 *정의로 이동*을 사용하여 데이터베이스 개체 자세히 보기


## <a name="prerequisites"></a>필수 구성 요소

이 자습서에서는 SQL Server 또는 Azure SQL Database의 *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면, 다음 빠른 시작 중 하나를 수행합니다.

- [연결 및 SQL Server를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [연결 및 Azure SQL Database를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>신속 하 게 데이터베이스 개체를 찾아 일반적인 작업 수행

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 데이터베이스 개체를 빠르게 찾으려는 검색 위젯을 제공 합니다. 결과 목록의 선택된 된 개체와 관련 된 일반적인 작업에 대 한와 같은 상황에 맞는 메뉴를 제공 *데이터 편집* 테이블에 대 한 합니다.

1. 서버 보충 기사를 엽니다 (**Ctrl + G**), 확장 **데이터베이스**를 선택 하 고 **TutorialDB**합니다. 

1. 엽니다는 *TutorialDB 대시보드* 마우스 오른쪽 단추로 클릭 하 여 **TutorialDB** 를 선택 하 고 **관리** 상황에 맞는 메뉴에서:

   ![상황에 맞는 메뉴 관리](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 대시보드를 마우스 오른쪽 단추로 클릭 **dbo입니다. 고객이** (검색 위젯)에서 선택한 **데이터 편집**합니다.
   
   > [!TIP]
   > 많은 개체를 사용 하 여 데이터베이스를 신속 하 게 찾을 테이블, 뷰 등 찾고자 하는 검색 위젯을 사용 합니다.

   ![빠른 검색 위젯](./media/tutorial-sql-editor/quick-search-widget.png)

1. 편집 합니다 **전자 메일** 첫 번째 행을 유형 열 *orlando0@adventure-works.com*, 키를 누릅니다 **Enter** 변경 내용을 저장 합니다.

   ![데이터 편집](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>저장된 프로시저를 만드는 T-SQL 코드 조각을 사용 하 여

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 문을 신속 하 게 만들기 위한 많은 기본 제공 T-SQL 코드 조각을 제공 합니다.


1. 키를 눌러 새 쿼리 편집기를 엽니다 **Ctrl + N**합니다.

2. 형식 **sql** 편집기에서 화살표를 아래로 **sqlCreateStoredProcedure**, 키를 누릅니다를 *탭* 키 (또는 *Enter*) 저장 만들기를 로드 하려면 프로시저 코드 조각입니다.

   ![snippet-list](./media/tutorial-sql-editor/snippet-list.png)

3. 만들기 저장된 프로시저 코드 조각에 빠른 편집에 대 한 설정 하는 두 필드가 *StoredProcedureName* 하 고 *SchemaName*합니다. 선택 *StoredProcedureName*를 마우스 오른쪽 단추로 **변경에 대 한 모든 정보**합니다. 이제 입력 *getCustomer* all *StoredProcedureName* 항목을 변경 *getCustomer*합니다.

   ![코드 조각](./media/tutorial-sql-editor/snippet.png)

5. 모든 항목을 변경 *SchemaName* 하 *dbo*합니다. 
6. 코드 조각을 업데이트 해야 하는 본문 텍스트 및 자리 표시자 매개 변수를 포함 합니다. 합니다 *EXECUTE* 문을 자리 표시자 텍스트를 프로시저 해야 하는 매개 변수의 개수를 알 수 없는 때문에 포함 되어 있습니다. 이 자습서에는 코드 조각을 업데이트 하므로 것 같습니다. 다음 코드를

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
    
5. 저장된 프로시저를 만들고 테스트 실행을 지정 하려면 키를 누릅니다 **F5**합니다.

저장된 프로시저가 만들어집니다 하며 **결과** 창 JSON에서 반환 된 고객을 표시 합니다. 서식이 지정 된 JSON을 확인 하려면 반환 된 레코드를 클릭 합니다. 


## <a name="use-peek-definition"></a>사용 하 여 피킹 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 정의 피킹 기능을 사용 하는 개체 정의를 볼 수가 있습니다. 이 섹션에서는 두 번째 저장된 프로시저를 만들고 보기 정의 사용 하 여 신속 하 게 저장된 프로시저의 본문을 작성 하는 테이블에 있는 열을 참조 하세요.

1. **Ctrl + N** 키를 눌러 새 편집기를 엽니다. 

2. 형식 *sql* 편집기에서 화살표를 아래로 *sqlCreateStoredProcedure*, 키를 누릅니다를 *탭* 키 (또는 *Enter*) 저장 만들기를 로드 하려면 프로시저 코드 조각입니다.
3. 입력 *setCustomer* 에 대 한 *StoredProcedureName* 하 고 *dbo* 에 대 한 *SchemaName*

3. 대체는 @param 다음 매개 변수 정의 사용 하 여 자리 표시자:

   ```sql
   @json_val nvarchar(max)
   ```

4. 저장된 프로시저의 본문을 다음 코드로 바꿉니다.
   ```sql
   INSERT INTO dbo.Customers
   ```

5. 에 *삽입* 방금 추가한 마우스 오른쪽 단추로 클릭 하면 줄 **dbo입니다. 고객이** 선택한 **피킹**합니다.

   ![피킹](./media/tutorial-sql-editor/peek-definition.png)

6. 테이블 정의 테이블의 열은 신속 하 게 볼 수 있도록 나타납니다. 저장된 프로시저에 대 한 문을 쉽게 완료 열 목록을 참조 하십시오. 저장된 프로시저의 본문을 완료 하 고 보기 정의 창의 닫을에 이전에 추가한 문 만들기를 완료 합니다.

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
7. 쿼리의 맨 아래에서 *EXECUTE* 명령을 삭제(또는 주석)합니다.
8. 전체 문이 다음 코드와 같습니다.

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

8. 만들려는 합니다 *setCustomer* 저장 프로시저를 눌러 **F5**합니다.

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>사용 하 여 setCustomer 저장 프로시저를 테스트 하려면 JSON으로 쿼리 결과 저장

*setCustomer* 이전 섹션에서 만든 저장된 프로시저 필요한 JSON 데이터를 전달할 수는 *@json_val* 매개 변수입니다. 이 섹션에는 저장된 프로시저를 테스트할 수 있도록 매개 변수로 전달 하는 JSON의 형식이 올바르게 지정 된 비트를 가져오는 방법을 보여 줍니다.

1. **서버** 사이드바에서 *dbo.Customers* 테이블을 마우스 오른쪽 단추로 클릭하고 **SELECT TOP 1000** 을 클릭합니다.

2. 결과 보기에서 첫 번째 행을 선택 합니다. 전체 행이 선택 되어 있는지 확인 합니다 (가장 왼쪽 열에서 숫자 1)를 누르고 선택한 **JSON으로 저장**합니다.  
3. 나중에 (데스크톱에 대 한 예제) 파일을 삭제 하 고 클릭 수 있도록 기억 하기 위치로 폴더를 변경할 **저장할**합니다. JSON 형식의 파일이 열립니다.

   ![JSON으로 저장](./media/tutorial-sql-editor/save-as-json.png)

4. 편집기에서 JSON 데이터를 선택하고 복사합니다.
5. **Ctrl + N** 키를 눌러 새 편집기를 엽니다.
6. 이전 단계를 쉽게 얻는 방법에 대 한 호출을 완료 하려면 올바른 형식의 데이터를 표시 합니다 *setCustomer* 프로시저입니다. 다음 코드를 사용 하 여 동일한 JSON 형식의 새 고객 세부 정보를 사용 하 여 테스트할 수 있도록 표시 합니다 *setCustomer* 프로시저입니다. 문에 매개 변수를 선언 하 고 새 get 실행 프로시저를 설정 하는 구문을 포함 합니다. 이전 섹션에서 복사한 데이터를 붙여 하 고 다음 예제와 동일 하도록 편집 하거나 쿼리 편집기에 다음 문을 붙여 수 있습니다.

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

7. **F5** 키를 눌러 스크립트를 실행합니다. 스크립트는 새 고객을 삽입하고 JSON 형식으로 새 고객의 정보를 반환합니다. 형식이 지정된 보기를 열려면 결과를 클릭합니다.

   ![테스트 결과](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서 학습하는 방법.
> [!div class="checklist"]
> * 스키마 개체 빠른 검색
> * 테이블 데이터 편집 
> * 조각을 사용하여 T-SQL 스크립트를 작성
> * 피킹 정의를 사용하여 데이터베이스 개체 정보를 알아보려면 정의로 이동


사용하도록 설정하는 방법을 알아보려면 **느린 쿼리 5** 위젯에서 다음 자습서를 완료합니다.

> [!div class="nextstepaction"]
> [느린 쿼리 샘플 정보 위젯 사용](tutorial-qds-sql-server.md)
