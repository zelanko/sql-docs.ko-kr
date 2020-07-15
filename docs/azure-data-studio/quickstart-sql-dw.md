---
title: Azure SQL 데이터 웨어하우스 연결 및 쿼리
description: 이 빠른 시작에서는 Azure Data Studio를 사용하여 Azure SQL Data Warehouse에 연결하고 쿼리를 실행하는 방법을 보여 줍니다.
ms.prod: azure-data-studio
ms.technology: ''
ms.reviewer: alayu, maghan, sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: f9a8213dacb3a7f221d3a3c3e51f0ed94bb6990a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728007"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>빠른 시작: Azure Data Studio를 사용하여 Azure SQL 데이터 웨어하우스의 데이터 연결 및 쿼리

이 빠른 시작에서는 Azure Data Studio를 사용하여 Azure SQL 데이터 웨어하우스에 연결한 다음, Transact-SQL 문을 사용하여 데이터를 만들고 삽입하고 선택하는 방법을 보여 줍니다. 

## <a name="prerequisites"></a>필수 구성 요소
이 빠른 시작을 완료하려면 Azure Data Studio 및 Azure SQL 데이터 웨어하우스가 필요합니다.

- [Azure Data Studio를 설치](download.md)합니다.

SQL Data Warehouse가 아직 없는 경우 [SQL Data Warehouse 만들기](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision)를 참조하세요.

서버 이름 및 로그인 자격 증명을 알아둡니다.


## <a name="connect-to-your-data-warehouse"></a>데이터 웨어하우스에 연결

Azure Data Studio를 사용하여 Azure SQL Data Warehouse 서버에 대한 연결을 설정합니다.

1. Azure Data Studio를 처음 실행하면 **연결** 페이지가 열립니다. **연결** 페이지가 표시되지 않으면 **연결 추가** 또는 **서버** 사이드바의 **새 연결** 아이콘을 클릭합니다.
   
   ![새 연결 아이콘](media/quickstart-sql-dw/new-connection-icon.png)

2. 이 문서에서는 ‘SQL 로그인’을 사용하지만 ‘Windows 인증’도 지원됩니다.  Azure SQL Server의 서버 이름, 사용자 이름 및 암호를 사용하여 다음과 같이 필드를 채웁니다.

   | 설정       | 제안 값 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 정규화된 서버 이름 | 이름은 **sqldwsample.database.windows.net**과 같이 지정해야 합니다. |
   | **인증** | SQL 로그인| 이 자습서에서는 SQL 인증을 사용합니다. |
   | **사용자 이름** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정의 암호 | 서버를 만들 때 지정한 암호입니다. |
   | **암호를 저장하시겠습니까?** | Yes 또는 No | 암호를 매번 입력하지 않으려면 Yes를 선택합니다. |
   | **데이터베이스 이름** | ‘비워 둠’ | 연결할 데이터베이스의 이름입니다. |
   | **서버 그룹** | <Default> 선택 | 서버 그룹을 만든 경우 특정 서버 그룹으로 설정할 수 있습니다. | 

   ![새 연결 아이콘](media/quickstart-sql-dw/new-connection-screen.png) 

3. 서버에 Azure Data Studio 연결을 허용하는 방화벽 규칙이 없으면 **새 방화벽 규칙 만들기** 양식이 열립니다. 양식을 완료하여 새 방화벽 규칙을 만듭니다. 자세한 내용은 [방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)을 참조하세요.

   ![새 방화벽 규칙](media/quickstart-sql-dw/firewall.png)  

4. 성공적으로 연결되면 서버가 ‘서버’ 사이드바에서 열립니다.

## <a name="create-the-tutorial-data-warehouse"></a>자습서 데이터 웨어하우스 만들기
1. 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

1. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```


## <a name="create-a-table"></a>테이블 만들기

쿼리 편집기는 여전히 *master* 데이터베이스에 연결되어 있지만 *TutorialDB* 데이터베이스에 테이블을 만들려고 합니다. 

1. 연결 컨텍스트를 **TutorialDB**로 변경합니다.

   ![컨텍스트 변경](media/quickstart-sql-database/change-context.png)


1. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

   > [!NOTE]
   > 편집기에서 이전 쿼리에 추가하거나 이전 쿼리를 덮어쓸 수 있습니다. **실행**을 클릭하면 선택한 쿼리만 실행됩니다. 아무것도 선택하지 않은 경우 **실행**을 클릭하면 편집기의 모든 쿼리가 실행됩니다.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>행 삽입

1. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>결과 보기
1. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 쿼리 결과가 다음과 같이 표시됩니다.

   ![결과 선택](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>리소스 정리

이 컬렉션의 다른 문서는 이 빠른 시작에 따라 빌드됩니다. 후속 빠른 시작을 계속 사용하려는 경우 이 빠른 시작에서 만든 리소스를 정리하지 마세요. 계속하지 않으려는 경우 다음 단계를 사용하여 이 빠른 시작으로 만든 리소스를 Azure Portal에서 삭제합니다.
더 이상 필요하지 않은 리소스 그룹을 삭제하여 리소스를 정리합니다. 자세한 내용은 [리소스 정리](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)를 참조하세요.


## <a name="next-steps"></a>다음 단계

이제 Azure SQL Data Warehouse에 연결하고 쿼리를 실행했으므로 [코드 편집기 자습서](tutorial-sql-editor.md)를 사용해 보세요.
