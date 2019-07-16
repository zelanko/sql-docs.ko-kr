---
title: '빠른 시작: Azure SQL database 연결 및 쿼리'
titleSuffix: Azure Data Studio
description: 이 빠른 시작에서는 Azure 데이터 Studio를 사용 하 여 SQL database에 연결 하 고 쿼리를 실행 하는 방법을 보여 줍니다.
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: bdb1a9c8efb8ebdf5d2e35c1da00c12578ade7d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959432"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>빠른 시작: [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 사용하여 Azure SQL database에 연결하고 쿼리하기

이 빠른 시작에서는 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 사용하여 Azure SQL Database 서버에 연결합니다. 그리고 나서 다른 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 자습서에서 사용하는 TutorialDB 데이터베이스를 생성하고 쿼리하기 위해서 TRANSACT-SQL (T-SQL)문을 실행합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 완료하려면 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 및 Azure SQL Database 서버가 필요합니다.

- [[!INCLUDE[name-sos](../includes/name-sos-short.md)] 설치](download.md)

Azure SQL server가 없는 경우, 다음 Azure SQL Database 빠른 시작 중 하나를 수행합니다. 이후 단계를 위해서 정규화된 서버 이름과 로그인 자격 증명을 기억합니다.

- [DB 만들기-포털](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [DB 만들기-CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [DB 만들기-PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Azure SQL Database 서버에 연결

Azure SQL Database 서버에 연결하기 위해서 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 사용합니다.

1. 처음 실행 하면 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 는 **시작** 페이지가 열려야 합니다. 표시 되지 않는 경우는 **시작** 페이지에서 **도움말** > **시작**합니다. 선택 **새 연결** 열려는 합니다 **연결** 창:
   
   ![새 연결 아이콘](media/quickstart-sql-database/new-connection-icon.png)

2. 이 문서에서는 SQL 로그인을 사용하지만 Windows 인증도 지원합니다. Azure SQL server에 대한 서버 이름, 사용자 이름 및 암호를 사용하여 다음 필드를 입력합니다.

   | 설정       | 제안된 값 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 정규화된 서버 이름 | 같은: **servername.database.windows.net**합니다. |
   | **인증** | SQL 로그인| 이 자습서에서는 SQL 인증을 사용합니다. |
   | **사용자 이름** | 서버 관리자 계정의 사용자 이름 | 서버를 만드는 데 사용된 계정의 사용자 이름입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정의 암호 | 서버를 만드는 데 사용된 계정의 암호입니다. |
   | **암호를 저장하시겠습니까?** | Yes 또는 No | 매번 암호를 입력하지 않으려면 **Yes**를 선택합니다. |
   | **데이터베이스 이름** | *비워 둡니다* | 여기에는 서버에만 연결합니다. |
   | **서버 그룹** | 선택 <Default> | 사용자가 만든 특정 서버 그룹으로 이 필드를 설정할 수 있습니다. | 

   ![새 연결 아이콘](media/quickstart-sql-database/new-connection-screen.png)  

3. **연결**을 선택합니다.

4. 서버에 Azure Data Studio가 연결할 수 있게 허용하는 방화벽 규칙이 없는 경우, **새 방화벽 규칙 만들기** 양식이 열립니다. 새 방화벽 규칙을 생성하는 양식을 작성합니다. 자세한 내용은 [방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)을 참조합니다.

   ![새 방화벽 규칙](media/quickstart-sql-database/firewall.png)  

성공적으로 연결되면 서버가 **서버** 사이드바에 표시됩니다.

## <a name="create-the-tutorial-database"></a>Tutorial 데이터베이스 생성하기

다음 섹션에서는 다른 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 자습서에서 사용했던 TutorialDB 데이터베이스를 생성합니다.

1. **서버** 사이드바에서 Azure SQL 서버에서 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

1. 다음 SQL을 쿼리 편집기에 붙여 넣습니다.

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

1. 도구 모음에서 **실행**을 선택합니다. **메시지** 창에 쿼리 진행률을 표시하는 알림이 표시됩니다.

## <a name="create-a-table"></a>테이블 생성하기

쿼리 편집기가 **master** 데이터베이스에 연결되었지만, **TutorialDB** 데이터베이스에 테이블을 생성하려고 합니다. 

1. **TutorialDB** 데이터베이스에 연결합니다.

   ![컨텍스트 변경](media/quickstart-sql-database/change-context2.png)



1. `Customers` 테이블을 생성합니다. 

   쿼리 편집기에서 이전 쿼리를 다음 쿼리로 바꾸고, **실행**을 선택합니다.

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


## <a name="insert-rows-into-the-table"></a>테이블에 행을 삽입하기

이전 쿼리를 다음 쿼리로 바꾸고, **실행**을 선택합니다.

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

## <a name="view-the-result"></a>결과 확인하기

이전 쿼리를 다음 쿼리로 바꾸고, **실행**을 선택합니다.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

쿼리 결과가 표시됩니다.

   ![결과 선택](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>리소스 정리

이후 빠른 시작 문서에서는 여기에서 만든 리소스를 기반으로 합니다. 이 문서을 계속 진행하려는 경우를 이 리소스를 삭제하지 않도록 해야 합니다. 그렇지 않으면, Azure portal에서 더 이상 필요하지 않은 리소스를 삭제합니다. 자세한 내용은 [리소스를 정리](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources) 참조합니다.

## <a name="next-steps"></a>다음 단계

Azure SQL database에 성공적으로 연결하고 쿼리를 실행했습니다. [코드 편집기 자습서](tutorial-sql-editor.md)를 시도해보세요.
