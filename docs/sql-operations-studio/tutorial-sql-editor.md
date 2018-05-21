---
title: '자습서: SQL 작업 (미리 보기) Studio TRANSACT-SQL 편집기를 사용 하 여 데이터베이스 개체를 만드는 | Microsoft Docs'
description: 이 자습서에서는 T-SQL을 사용 하 여 단순화 하는 SQL 작업 Studio (미리 보기)의 주요 기능에 설명 합니다.
ms.custom: tools|sos
ms.date: 03/13/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ea03ea9ee0d45e15ec81dda9be95d38ad99c6d6
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>자습서: TRANSACT-SQL 편집기를 사용 하 여 데이터베이스 개체-를 만들려면 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

쿼리 작성 및 실행, 저장된 프로시저, 스크립트 등은 데이터베이스 전문가의 핵심 작업입니다. 이 자습서에서는 데이터베이스 개체를 만드는 T-SQL 편집기의 주요 기능에 설명 합니다.

이 자습서에서 사용 하는 방법을 배웁니다 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 에:
> [!div class="checklist"]
> * 검색 데이터베이스 개체
> * 테이블 데이터 편집 
> * 조각을 사용 하 여 T-SQL을 신속 하 게 작성
> * 데이터베이스 개체 자세히 보기를 사용 하 여 *정의 피킹* 및 *정의로 이동*


## <a name="prerequisites"></a>필수 구성 요소

이 자습서에서는 SQL Server 또는 Azure SQL 데이터베이스 *TutorialDB*합니다. 만들려는 *TutorialDB* 데이터베이스에서 다음 퀵 스타트 중 하나를 완료 합니다.

- [연결 및 SQL Server를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [연결 및 Azure SQL 데이터베이스를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>빠르게 데이터베이스 개체를 찾아 일반적인 작업 수행

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 데이터베이스 개체를 빠르게 찾기 위해 검색 위젯을 제공 합니다. 결과 목록 선택된 된 개체와 관련 된 일반적인 작업에 대 한와 같은 상황에 맞는 메뉴를 제공 *데이터 편집* 테이블에 대 한 합니다.

1. 서버 사이드바 열기 (**Ctrl + G**)를 확장 하 고 **데이터베이스**, 선택 하 고 **TutorialDB**합니다. 

1. 열기는 *TutorialDB 대시보드* 마우스 오른쪽 단추로 클릭 하 여 **TutorialDB** 선택 하 고 **관리** 상황에 맞는 메뉴에서:

   ![상황에 맞는 메뉴-관리](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 대시보드를 마우스 오른쪽 단추로 클릭 **dbo입니다. 고객** (검색 위젯)에서 선택 하 고 **데이터 편집**합니다.
   
   > [!TIP]
   > 많은 개체가 포함 된 데이터베이스에 대 한 검색 위젯을 사용 하 여 테이블, 뷰 등 원하는 신속 하 게 찾을 수 있습니다.

   ![빠른 검색 위젯](./media/tutorial-sql-editor/quick-search-widget.png)

1. 편집 된 **전자 메일** 첫 번째 행 형식에서에서 열 *orlando0@adventure-works.com*, 한 키를 누릅니다 **Enter** 의 변경 내용을 저장 합니다.

   ![데이터 편집](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>저장된 프로시저를 만들 T-SQL 코드 조각을 사용합니다

SQL 작업 Studio 문을 빠르게 만들기에 대 한 기본 제공 되는 많은 T-SQL 조각이 제공 합니다.


1. 키를 눌러 새 쿼리 편집기를 열고 **Ctrl + N**합니다.

2. 형식 **sql** 편집기 아래쪽 화살표에서에서 **sqlCreateStoredProcedure**, 누릅니다는 *탭* 키 (또는 *Enter*) 저장 만들기를 로드할 수 프로시저 코드 조각입니다.

   ![snippet-list](./media/tutorial-sql-editor/snippet-list.png)

3. 만들기 저장된 프로시저 조각에는 빠른 편집 하기 위해 설정 하는 두 개의 필드 *StoredProcedureName* 및 *SchemaName*합니다. 선택 *StoredProcedureName*를 마우스 오른쪽 단추로 클릭 하 고 선택 **항목을 모두 변경**합니다. 이제 입력 *getCustomer* 및 모든 *StoredProcedureName* 항목 변경 *getCustomer*합니다.

   ![코드 조각](./media/tutorial-sql-editor/snippet.png)

5. 모든 항목을 변경 *SchemaName* 를 *dbo*합니다. 
6. 자리 표시자 매개 변수 및 본문 텍스트를 업데이트 해야 하는 조각에 포함 되어 있습니다. *EXECUTE* 문 개체 틀 텍스트를 프로시저 갖습니다 매개 변수의 개수를 알 수 없기 때문에 포함 되어 있습니다. 이 자습서의 조각을 업데이트에 대 한 표시는 다음 코드:

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
    
5. 키를 눌러 저장된 프로시저를 만들고 테스트 실행을 지정 하려면 **F5**합니다.

저장된 프로시저를 만들 이제 및 **결과** JSON에서 반환 된 고객 창에 표시 됩니다. 한 형식의 JSON을 확인 하려면 반환 된 레코드를 클릭 합니다. 


## <a name="use-peek-definition"></a>정의 피킹 사용 

SQL 작업 Studio peek 정의 기능을 사용 하는 개체 정의 볼 수 있는 기능을 제공 합니다. 이 섹션 두 번째 저장된 프로시저를 만들고 신속 하 게 저장된 프로시저의 본문을 만들 수 있도록 테이블에 있는 열을 미리 보기 정의 사용 하 여 합니다.

1. 키를 눌러 새 편집기를 열고 **Ctrl + N**합니다. 

2. 형식 *sql* 편집기 아래쪽 화살표에서에서 *sqlCreateStoredProcedure*, 누릅니다는 *탭* 키 (또는 *Enter*) 저장 만들기를 로드할 수 프로시저 코드 조각입니다.
3. 에 입력 *setCustomer* 에 대 한 *StoredProcedureName* 및 *dbo* 에 대 한 *SchemaName*

3. 대체는 @param 자리 표시자는 다음 매개 변수 정의로:

   ```sql
   @json_val nvarchar(max)
   ```

4. 저장된 프로시저의 본문을 다음 코드로 바꿉니다.
   ```sql
   INSERT INTO dbo.Customers
   ```

5. 에 *삽입* 방금 추가한 마우스 오른쪽 단추로 클릭 하면 줄 **dbo입니다. 고객** 선택 **정의 피킹**합니다.

   ![정의 피킹](./media/tutorial-sql-editor/peek-definition.png)

6. 테이블 정의 된 열을 테이블에 신속 하 게 확인할 수 있도록 나타납니다. 저장된 프로시저에 대 한 문을 쉽게 끝나기를 열 목록을 참조 하십시오. 저장된 프로시저의 본문을 완료 하 고 정의 피크 (peek) 창 닫기에 이전에 추가한 INSERT 문을 만들기를 완료 합니다.

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
7. 삭제 (또는 주석으로 처리)는 *EXECUTE* 쿼리 맨 아래에 명령 합니다.
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

8. 만들려는 *setCustomer* 저장 프로시저를 눌러 **F5**합니다.

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>사용 하 여 setCustomer 저장 프로시저를 테스트 하는 JSON으로 쿼리 결과 저장

*setCustomer* 이전 섹션에서 만든 저장된 프로시저에는 JSON 필요한 데이터를 전달할 수는 *@json_val* 매개 변수입니다. 이 섹션에는 저장된 프로시저를 테스트할 수 있도록를 매개 변수로 전달 하는 JSON의 형식이 올바르게 지정 된 비트를 가져오는 방법을 보여 줍니다.

1. 에 **서버** 사이드바 단추로 클릭 하 고는 *dbo입니다. 고객* 테이블 마우스 클릭 **상위 1000 개 행 선택**합니다.

2. 결과 보기에서 첫 번째 행을 선택 합니다. 전체 행이 선택 되어 있는지 확인 합니다 (가장 왼쪽 열에 숫자 1 클릭) 하 고 선택 **JSON으로 저장**합니다.  
3. 나중에 (데스크톱에 대 한 예제) 파일을 삭제 하 고 클릭 수 있도록 기억 하기 위치에 폴더를 변경 **저장**합니다. JSON 형식의 파일이 열립니다.

   ![JSON으로 저장](./media/tutorial-sql-editor/save-as-json.png)

4. 편집기에서 JSON 데이터를 선택 하 고 복사 합니다.
5. 키를 눌러 새 편집기를 열고 **Ctrl + N**합니다.
6. 이전 단계에서는에 대 한 호출을 완료 하려면 적절 한 형식의 데이터를 쉽게 가져올 수 방법을 보여 줍니다.는 *setCustomer* 프로시저입니다. 다음 코드 사용 하 여 동일한 JSON 형식 새 고객 세부 정보를 테스트할 수 있습니다를 볼 수는 *setCustomer* 프로시저입니다. 문에 매개 변수를 선언 하 고 새 get 실행 프로시저를 설정 하는 구문을 포함 합니다. 이전 섹션에서 복사한 데이터를 붙여 하는 다음 예제와 동일 하도록 편집 하거나 쿼리 편집기에 다음 문을 붙여 넣기만 하면 수 있습니다.

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

7. 키를 눌러 스크립트를 실행 **F5**합니다. 스크립트 새 고객을 JSON 형식에 새 고객의 정보를 반환 합니다. 결과 형식이 지정 된 보기를 열려면 클릭 합니다.

   ![테스트 결과](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 알아보았습니다 하는 방법:
> [!div class="checklist"]
> * 빠른 검색 스키마 개체
> * 테이블 데이터 편집 
> * 조각을 사용 하 여 T-SQL 스크립트를 작성 합니다.
> * 정의 피킹를 사용 하 여 데이터베이스 개체 정보에 대 한 자세한 내용은 정의로 이동 하 고


사용 하도록 설정 하는 방법에 알아보려면는 **가장 느린 쿼리 5** 위젯, 다음 자습서를 완료 합니다.

> [!div class="nextstepaction"]
> [느린 쿼리 샘플 통찰력 위젯 사용](tutorial-qds-sql-server.md)
