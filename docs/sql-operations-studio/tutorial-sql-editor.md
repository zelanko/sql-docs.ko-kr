---
title: "자습서: SQL 작업 (미리 보기) Studio TRANSACT-SQL 편집기를 사용 하 여 데이터베이스 개체를 만드는 | Microsoft Docs"
description: "이 자습서에서는 T-SQL을 사용 하 여 단순화 하는 SQL 작업 Studio (미리 보기)의 주요 기능에 설명 합니다."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2754a998963be5a25d00aa58dcb9b4105bb8f37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>자습서: TRANSACT-SQL 편집기를 사용 하 여 데이터베이스 개체-를 만들려면[!INCLUDE[name-sos](../includes/name-sos-short.md)]

쿼리 작성 및 실행, 저장된 프로시저, 스크립트 등은 데이터베이스 전문가의 핵심 작업입니다. 이 자습서에서는 데이터베이스 개체를 만드는 T-SQL 편집기의 주요 기능에 설명 합니다.

이 자습서에서 사용 하는 방법을 배웁니다 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 에:
> [!div class="checklist"]
> * 검색 데이터베이스 개체
> * 테이블 데이터 편집 
> * 조각을 사용 하 여 T-SQL을 신속 하 게 작성
> * 데이터베이스 개체 자세히 보기를 사용 하 여 *정의 피킹* 및 *정의로 이동*


## <a name="prerequisites"></a>사전 요구 사항

이 자습서에서는 SQL Server 또는 Azure SQL 데이터베이스 *TutorialDB*합니다. 만들려는 *TutorialDB* 데이터베이스에서 다음 퀵 스타트 중 하나를 완료 합니다.

- [연결 및 SQL Server를 사용 하 여 쿼리[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [연결 및 Azure SQL 데이터베이스를 사용 하 여 쿼리[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>빠르게 데이터베이스 개체를 찾아 일반적인 작업 수행

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]데이터베이스 개체를 빠르게 찾기 위해 검색 위젯을 제공 합니다. 결과 목록 선택된 된 개체와 관련 된 일반적인 작업에 대 한와 같은 상황에 맞는 메뉴를 제공 *데이터 편집* 테이블에 대 한 합니다.

1. 서버 사이드바 열기 (**Ctrl + G**)를 확장 하 고 **데이터베이스**, 선택 하 고 **TutorialDB**합니다. 

1. 열기는 *TutorialDB 대시보드* 선택 하 여 **관리** 상황에 맞는 메뉴입니다.

   ![상황에 맞는 메뉴-관리](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 찾을 *고객* 입력 하 여 테이블 *사용자* 검색 위젯에서 합니다.
1. 마우스 오른쪽 단추로 클릭 **dbo입니다. 고객** 선택 **데이터 편집**합니다.

   ![빠른 검색 위젯](./media/tutorial-sql-editor/quick-search-widget.png)

1. 편집 된 **전자 메일** 첫 번째 행 형식에서에서 열  *orlando0@adventure-works.com* , 한 키를 누릅니다 **Enter** 의 변경 내용을 저장 합니다.

   ![데이터 편집](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-a-stored-procedure"></a>T-SQL 조각을 사용 하 여 저장된 프로시저 만들기

### <a name="use-snippets-in-includename-sos-shortincludesname-sos-shortmd"></a>코드 조각을 사용합니다[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]

1. 키를 눌러 새 쿼리 편집기를 열고 **Ctrl + N**합니다.

2. 형식 **sql** 편집기 아래쪽 화살표에서에서 **sqlCreateStoredProcedure**, 한 키를 누릅니다는 *탭* 새 저장된 프로시저 코드 조각을 로드 하는 키입니다.

   ![목록 코드 조각](./media/tutorial-sql-editor/snippet-list.png)

3. 형식 *getCustomer* 및 모든 *StoredProcedureName* 항목 변경 *getCustomer*합니다. 

   ![코드 조각](./media/tutorial-sql-editor/snippet.png)

4. 저장된 프로시저의 나머지 부분을 T-SQL 아래 바꿉니다.

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
    SELECT  c.CustomerID, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerID = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. 키를 눌러 저장된 프로시저를 만들고 테스트 실행을 지정 하려면 **F5**합니다.

## <a name="use-peek-definition-and-go-to-definition"></a>정의 피킹 사용 및 정의로 이동 

1. 키를 눌러 새 편집기를 열고 **Ctrl + N**합니다. 

2. 입력 하 고 선택 **sqlCreateStoredProcedure** 조각 제안 합니다. 에 입력 **setCustomer** 에 대 한 **StoredProcedureName** 및 **dbo** 에 대 한 **SchemaName**

3. 대체는 @param 다음과 같은 매개 변수 정의가 포함 된 줄:

   ```sql
       @json_val nvarchar(max)
   ```

4. 다음으로 저장된 프로시저의 본문을 바꿉니다.
   ```sql
   -- body of the stored procedure
   INSERT INTO dbo.Customers
   ```

5. 마우스 오른쪽 단추로 클릭 **dbo입니다. 고객** 선택 **정의 피킹**합니다.

   ![정의 피킹](./media/tutorial-sql-editor/peek-definition.png)

6. 테이블 정의 사용 하 여 다음 insert 문을 완료 하려면:

   ```sql
   INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
   ```
7. 마지막 문은 같아야 합니다.

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
       INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. 키를 눌러 스크립트를 실행 하려면 **F5**합니다.

## <a name="use-save-query-results-as-json-to-test-our-stored-procedure"></a>사용 하 여 저장된 프로시저를 테스트 하는 JSON으로 쿼리 결과 저장

1. **상위 1000 개 행 선택** 에서 *dbo입니다. 고객* 테이블입니다.

2. 결과 보기 및 클릭에서 첫 번째 행을 선택 **JSON으로 저장**합니다.  
3. 클릭 **저장**, JSON 형식으로 강조 표시 된 행을 엽니다.

   ![JSON으로 저장](./media/tutorial-sql-editor/save-as-json.png)

4. JSON 데이터를 선택 하 고 복사 합니다.

5. 에 대 한 새 쿼리 열기 *TutorialDB* 이전 단계에서 템플릿으로 JSON 데이터를 사용 하 여 다음 테스트 스크립트를 완료 합니다. 값을 수정 *CustomerID*, *이름*, *위치*, 및 *전자 메일*합니다.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerID": 5,
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


사용 하도록 설정 하는 방법에 알아보려면는 **가장 느린 쿼리 5** 샘플 통찰력, 다음 자습서를 완료:

> [!div class="nextstepaction"]
> [느린 쿼리 샘플 통찰력 위젯 사용](tutorial-qds-sql-server.md)
