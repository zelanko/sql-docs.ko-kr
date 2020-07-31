---
title: '빠른 시작: SQL Server 연결 및 쿼리'
description: Azure Data Studio를 사용하여 SQL Server에 연결하고 T-SQL(Transact-SQL) 문을 사용하여 데이터베이스를 만들어 보는 빠른 시작을 진행합니다.
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 08/02/2019
ms.openlocfilehash: 532e210d239f8c55b99bd34828fafe160e1fb78b
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411289"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-sql-server"></a>빠른 시작: Azure Data Studio를 사용하여 SQL Server 연결 및 쿼리

이 빠른 시작에서는 Azure Data Studio를 사용하여 SQL Server에 연결한 다음 T-SQL(Transact-SQL) 문을 사용하여 Azure Data Studio 자습서에서 사용할 *TutorialDB*를 만드는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 구성 요소

이 빠른 시작을 완료하려면 Azure Data Studio와 SQL Server 액세스 권한이 필요합니다.

- [Azure Data Studio](download.md)를 설치합니다.

SQL Server에 대한 액세스 권한이 없는 경우 다음 링크에서 해당 플랫폼을 선택합니다(SQL 로그인 및 암호를 기억해야 함).

- [Windows - SQL Server 2017 Developer Edition 다운로드](https://www.microsoft.com/sql-server/sql-server-downloads)
- [macOS - Docker에서 SQL Server 2017 다운로드](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux - SQL Server 2017 Developer Edition 다운로드](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install) - ‘데이터를 만들고 쿼리’하는 단계까지만 수행하면 됩니다.

## <a name="connect-to-a-sql-server"></a>SQL Server에 연결

1. **Azure Data Studio**를 시작합니다.

2. Azure Data Studio를 처음 실행하면 **시작** 페이지가 열립니다. **시작** 페이지가 표시되지 않으면 **도움말** > **시작**을 선택합니다. **새 연결**을 선택하여 **연결** 창을 엽니다.

   ![새 연결 아이콘](media/quickstart-sql-server/new-connection-icon.png)

3. 이 문서에서는 ‘SQL 로그인’을 사용하지만 ‘Windows 인증’도 지원됩니다. 다음과 같이 필드를 채웁니다.

   - **서버 이름:** 여기에 서버 이름을 입력합니다. 예를 들어 localhost를 입력합니다.
   - **인증 유형:** SQL 로그인
   - **사용자 이름:** SQL Server의 사용자 이름
   - **암호:** SQL Server의 암호
   - **데이터베이스 이름:** \<Default\>
   - **서버 그룹:** \<Default\>

   ![새 연결 화면](media/quickstart-sql-server/new-connection-screen.png)

## <a name="create-a-database"></a>데이터베이스 만들기

다음 단계에서는 **TutorialDB**라는 데이터베이스를 만듭니다.

1. **localhost** 서버를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

2. 쿼리 창에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

    ```sql
    USE master
    GO
    IF NOT EXISTS (
     SELECT name
     FROM sys.databases
     WHERE name = N'TutorialDB'
    )
     CREATE DATABASE [TutorialDB];
    GO
    IF SERVERPROPERTY('ProductVersion') > '12'
     ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON;
    GO
    ```

   쿼리가 완료되면 데이터베이스 목록에 새 **TutorialDB**가 나타납니다. 표시되지 않는 경우 **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.

   ![데이터베이스 만들기](media/quickstart-sql-server/create-database.png)

## <a name="create-a-table"></a>테이블 만들기

쿼리 편집기는 여전히 *master* 데이터베이스에 연결되어 있지만 *TutorialDB* 데이터베이스에 테이블을 만들려고 합니다.

1. 연결 컨텍스트를 **TutorialDB**로 변경합니다.

   ![컨텍스트 변경](media/quickstart-sql-server/change-context.png)

2. 쿼리 창에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

   > [!NOTE]
   > 편집기에서 이전 쿼리에 추가하거나 이전 쿼리를 덮어쓸 수 있습니다. **실행**을 클릭하면 선택한 쿼리만 실행됩니다. 아무것도 선택하지 않은 경우 **실행**을 클릭하면 편집기의 모든 쿼리가 실행됩니다.

    ```sql
    -- Create a new table called 'Customers' in schema 'dbo'
    -- Drop the table if it already exists
    IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
     DROP TABLE dbo.Customers;
    GO
    -- Create the table in the specified schema
    CREATE TABLE dbo.Customers
    (
     CustomerId int NOT NULL PRIMARY KEY, -- primary key column
     Name nvarchar(50) NOT NULL,
     Location nvarchar(50) NOT NULL,
     Email nvarchar(50) NOT NULL
    );
    GO
    ```

쿼리가 완료되면 테이블 목록에 새 **Customers** 테이블이 나타납니다. **TutorialDB > 테이블** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택해야 할 수도 있습니다.

## <a name="insert-rows"></a>행 삽입

- 쿼리 창에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

    ```sql
    -- Insert rows into table 'Customers'
    INSERT INTO dbo.Customers
     ([CustomerId], [Name], [Location], [Email])
    VALUES
     ( 1, N'Orlando', N'Australia', N''),
     ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
     ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
     ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
    GO
    ```

## <a name="view-the-data-returned-by-a-query"></a>쿼리에서 반환된 데이터 보기

 - 쿼리 창에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

   ![결과 선택](media/quickstart-sql-server/select-results.png)

## <a name="next-steps"></a>다음 단계

이제 SQL Server에 연결하고 쿼리를 실행했으므로 [코드 편집기 자습서](tutorial-sql-editor.md)를 사용해 봅니다.
