---
title: '빠른 시작: Azure SQL database 연결 및 쿼리'
titleSuffix: Azure Data Studio
description: 이 빠른 시작에서는 Azure 데이터 Studio를 사용 하 여 SQL database에 연결 하 고 쿼리를 실행 하는 방법을 보여 줍니다.
ms.custom: seodec18
ms.date: 12/21/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: d368f38589530f27db98c3c61b9cec4610818ae4
ms.sourcegitcommit: a11e733bd417905150567dfebc46a137df85a2fa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991816"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>빠른 시작: 사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 를 연결 하 여 Azure SQL database 쿼리

이 빠른 시작에서는 [!INCLUDE[name-sos](../includes/name-sos-short.md)] Azure SQL Database 서버에 연결 합니다. TRANSACT-SQL (T-SQL) 문을 만들고 다른 사용 되는 TutorialDB 데이터베이스 쿼리 실행 후 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 자습서입니다.

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 완료 하려면 [!INCLUDE[name-sos](../includes/name-sos-short.md)], 및 Azure SQL Database 서버입니다.

- [설치 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

Azure SQL server가 없는 경우 다음 Azure SQL Database 빠른 시작 중 하나를 수행 합니다. 정규화 된 서버 이름을 기억 하 고 이후 단계에 대 한 자격 증명을 로그인 합니다.

- [DB 만들기-포털](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [DB 만들기-CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [DB 만들기-PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Azure SQL Database 서버에 연결

사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)] Azure SQL Database 서버에 연결 합니다.

1. 처음 실행 하면 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 는 **연결** 페이지가 열려야 합니다. 표시 되지 않는 경우는 **연결** 페이지에서 **연결 추가**, 또는 **새 연결** 아이콘에는 **서버** 보충 기사:
   
   ![새 연결 아이콘](media/quickstart-sql-database/new-connection-icon.png)

2. 이 문서에서는 SQL 로그인을 사용 하지만 Windows 인증도 지원 합니다. Azure SQL server에 대 한 서버 이름, 사용자 이름 및 암호를 사용 하 여 다음 필드를 입력 합니다.

   | 설정       | 제안된 값 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 정규화된 서버 이름 | 같은: **servername.database.windows.net**합니다. |
   | **인증** | SQL 로그인| 이 자습서에서는 SQL 인증을 사용 합니다. |
   | **사용자 이름** | 서버 관리자 계정 사용자 이름 | 서버를 만드는 데 사용 된 계정과에서 사용자 이름입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정 암호 | 서버를 만드는 데 사용 된 계정과에서 암호입니다. |
   | **암호를 저장하시겠습니까?** | Yes 또는 No | 선택 **예** 될 때마다 암호를 입력 하지 않으려면입니다. |
   | **데이터베이스 이름** | *비워 둡니다* | 여기에 서버에만 연결 되어 있습니다. |
   | **서버 그룹** | 선택 <Default> | 사용자가 만든 특정 서버 그룹에이 필드를 설정할 수 있습니다. | 

   ![새 연결 아이콘](media/quickstart-sql-database/new-connection-screen.png)  

3. **연결**을 선택합니다.

4. 서버에 연결 하려면 Azure Data Studio 허용 하는 방화벽 규칙이 없는 경우는 **새 방화벽 규칙 만들기** 양식이 열립니다. 양식을 새 방화벽 규칙을 만들려고 합니다. 자세한 내용은 참조 하세요 [방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)합니다.

   ![새 방화벽 규칙](media/quickstart-sql-database/firewall.png)  

성공적으로 연결 되 면 서버에서 열립니다는 **서버** 보충 합니다.

## <a name="create-the-tutorial-database"></a>Tutorial 데이터베이스 만들기

다음 섹션에 사용 되는 TutorialDB 데이터베이스를 만들 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 자습서입니다.

1. Azure SQL 서버를 마우스 오른쪽 단추로 클릭 합니다 **서버** 사이드바 가젯과 선택 **새 쿼리**합니다.

1. 이 SQL을 쿼리 편집기에 붙여 넣습니다.

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

1. 도구 모음에서 선택 **실행**합니다. 에 알림을 표시 합니다 **메시지** 창 쿼리 진행률을 표시 합니다.

## <a name="create-a-table"></a>테이블 만들기

쿼리 편집기가 연결 되는 **마스터** 했지만 데이터베이스에 테이블을 만들려면 원하는 합니다 **TutorialDB** 데이터베이스. 

1. 에 연결 합니다 **TutorialDB** 데이터베이스입니다.

   ![컨텍스트 변경](media/quickstart-sql-database/change-context2.png)



1. 만들기는 `Customers` 테이블입니다. 

   선택한 쿼리 편집기에서 이전 쿼리를이 바꿉니다 **실행**합니다.

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


## <a name="insert-rows-into-the-table"></a>테이블을 사용 하 여 행 삽입

선택한 이전 쿼리를이 바꿉니다 **실행**합니다.

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

## <a name="view-the-result"></a>결과 보려면

선택한 이전 쿼리를이 바꿉니다 **실행**합니다.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

쿼리 결과 표시 합니다.

   ![결과 선택](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>리소스 정리

여기에서 만든 리소스를 기반으로 이후 빠른 시작 문서입니다. 다음이 문서를 진행 하려는 경우를 이러한 리소스를 삭제 하지 않도록 해야 합니다. 이 고, 그렇지 Azure portal에서 더 이상 필요한 리소스를 삭제 합니다. 자세한 내용은 참조 하세요 [리소스를 정리](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)합니다.

## <a name="next-steps"></a>다음 단계

Azure SQL database 및 쿼리 실행에 성공적으로 연결한 하 고 나면 합니다 [코드 편집기 자습서](tutorial-sql-editor.md)합니다.
