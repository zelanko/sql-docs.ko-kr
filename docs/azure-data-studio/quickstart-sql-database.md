---
title: Azure SQL 데이터베이스 연결 및 쿼리
description: 이 빠른 시작에서는 Azure Data Studio를 사용하여 SQL 데이터베이스에 연결하고 쿼리를 실행하는 방법을 보여 줍니다.
ms.prod: azure-data-studio
ms.technology: ''
ms.reviewer: alayu; maghan; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.custom: seodec18; sqlfreshmay19; seo-lt-2019
ms.date: 05/14/2019
ms.openlocfilehash: 73e910b6d199a4918eafca067a95136e31ac079c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771953"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-azure-sql-database"></a>빠른 시작: Azure Data Studio를 사용한 Azure SQL 데이터베이스 연결 및 쿼리

이 빠른 시작에서는 Azure Data Studio를 사용하여 Azure SQL Database 서버에 연결합니다. 그런 다음, T-SQL(Transact-SQL) 문을 실행하여 다른 Azure Data Studio 자습서에서 사용되는 TutorialDB 데이터베이스를 만들고 쿼리합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 빠른 시작을 완료하려면 Azure Data Studio 및 Azure SQL Database 서버가 필요합니다.

- [Azure Data Studio 설치](download.md)

Azure SQL Server가 없는 경우 다음 Azure SQL Database 빠른 시작 중 하나를 완료합니다. 이후 단계를 위해 정규화된 서버 이름과 로그인 자격 증명을 기억합니다.

- [DB 만들기 - 포털](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [DB 만들기 - CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [DB 만들기 - PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Azure SQL Database 서버에 연결

Azure Data Studio를 사용하여 Azure SQL Database 서버에 대한 연결을 설정합니다.

1. Azure Data Studio를 처음 실행하면 **시작** 페이지가 열립니다. **시작** 페이지가 표시되지 않으면 **도움말** > **시작**을 선택합니다. **새 연결**을 선택하여 **연결** 창을 엽니다.
   
   ![새 연결 아이콘](media/quickstart-sql-database/new-connection-icon.png)

2. 이 문서에서는 SQL 로그인을 사용하지만 Windows 인증도 지원합니다. 해당 Azure SQL Server의 서버 이름, 사용자 이름 및 암호를 사용하여 다음 필드를 채웁니다.

   | 설정       | 제안 값 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 정규화된 서버 이름 | 예: **servername.database.windows.net** |
   | **인증** | SQL 로그인| 이 자습서에서는 SQL 인증을 사용합니다. |
   | **사용자 이름** | 서버 관리자 계정 사용자 이름 | 서버를 만드는 데 사용된 계정의 사용자 이름입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정 암호 | 서버를 만드는 데 사용된 계정의 암호입니다. |
   | **암호를 저장하시겠습니까?** | Yes 또는 No | 암호를 매번 입력하지 않으려면 **예**를 선택합니다. |
   | **데이터베이스 이름** | ‘비워 둠’ | 여기서는 서버에만 연결합니다. |
   | **서버 그룹** | <Default> 선택 | 직접 만든 특정 서버 그룹으로 이 필드를 설정할 수 있습니다. | 

   ![새 연결 아이콘](media/quickstart-sql-database/new-connection-screen.png)  

3. **연결**을 선택합니다.

4. 서버에 Azure Data Studio 연결을 허용하는 방화벽 규칙이 없으면 **새 방화벽 규칙 만들기** 양식이 열립니다. 양식을 완료하여 새 방화벽 규칙을 만듭니다. 자세한 내용은 [방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)을 참조하세요.

   ![새 방화벽 규칙](media/quickstart-sql-database/firewall.png)  

성공적으로 연결되면 서버가 **서버** 사이드바에서 열립니다.

## <a name="create-the-tutorial-database"></a>자습서 데이터베이스 만들기

다음 섹션에서는 다른 Azure Data Studio 자습서에서 사용되는 TutorialDB 데이터베이스를 만듭니다.

1. **서버** 사이드바에서 Azure SQL Server를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

1. 이 SQL을 쿼리 편집기에 붙여넣습니다.

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. 도구 모음에서 **실행**을 선택합니다. **메시지** 창에 알림이 표시되어 쿼리 진행률을 보여 줍니다.

## <a name="create-a-table"></a>테이블 만들기

쿼리 편집기는 **master** 데이터베이스에 연결되어 있지만 **TutorialDB** 데이터베이스에 테이블을 만들려고 합니다. 

1. **TutorialDB** 데이터베이스에 연결합니다.

   ![컨텍스트 변경](media/quickstart-sql-database/change-context2.png)



1. `Customers` 테이블을 만듭니다. 

   쿼리 편집기의 이전 쿼리를 다음 쿼리로 바꾸고 **실행**을 선택합니다.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows-into-the-table"></a>테이블에 행 삽입

이전 쿼리를 다음 쿼리로 바꾸고 **실행**을 선택합니다.

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="view-the-result"></a>결과 보기

이전 쿼리를 다음 쿼리로 바꾸고 **실행**을 선택합니다.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

쿼리 결과가 다음과 같이 표시됩니다.

   ![결과 선택](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>리소스 정리

이후의 빠른 시작 문서는 여기에서 만든 리소스를 기반으로 합니다. 해당 문서를 진행하려는 경우 이 리소스를 삭제하지 않아야 합니다. 그렇지 않으면 Azure Portal에서 더 이상 필요하지 않은 리소스를 삭제합니다. 자세한 내용은 [리소스 정리](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)를 참조하세요.

## <a name="next-steps"></a>다음 단계

이제 Azure SQL 데이터베이스에 연결하고 쿼리를 실행했으므로 [코드 편집기 자습서](tutorial-sql-editor.md)를 사용해 봅니다.
