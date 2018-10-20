---
title: '빠른 시작: 연결 및 Azure Data Studio를 사용 하 여 Azure SQL Data Warehouse를 쿼리 합니다. | Microsoft Docs'
description: 이 빠른 시작에서는 Azure 데이터 Studio를 사용 하 여 SQL database에 연결 하 고 쿼리를 실행 하는 방법을 보여 줍니다.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: bf26924bc7791cf5321c32b3c127abc52780740b
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49355734"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>빠른 시작: 사용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 연결 하 고 Azure SQL Data Warehouse에서 데이터를 쿼리 합니다.

이 빠른 시작에 사용 하는 방법을 보여 줍니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)] Azure SQL data warehouse에 연결한 다음 TRANSACT-SQL 문을 사용 하 여 삽입, 만들고, 데이터를 선택 합니다. 

## <a name="prerequisites"></a>필수 구성 요소
이 빠른 시작을 완료 하려면 [!INCLUDE[name-sos](../includes/name-sos-short.md)], 및 Azure SQL data warehouse를 합니다.

- [[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)를 설치합니다.

SQL data warehouse에 아직 없는 경우 [SQL Data Warehouse 만들기](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision)합니다.

서버 이름 및 로그인 자격 증명 기억!


## <a name="connect-to-your-data-warehouse"></a>Data warehouse에 연결

사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)] Azure SQL Data Warehouse 서버에 연결 합니다.

1. 처음 실행 하면 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 는 **연결** 페이지가 열려야 합니다. 표시 되지 않는 경우는 **연결** 페이지에서 **연결 추가**, 또는 **새 연결** 아이콘에는 **서버** 사이드바:
   
   ![새 연결 아이콘](media/quickstart-sql-dw/new-connection-icon.png)

2. 이 아티클에서 *SQL 로그인*, 되지만 *Windows 인증* 도 지원 됩니다. 다음과 같이 서버 이름, 사용자 이름 및 암호를 사용 하 여 필드를 채우고 *여* Azure SQL server:

   | 설정       | 제안된 값 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 정규화된 서버 이름 | 다음과 같은 이름 이어야 합니다: **sqldwsample.database.windows.net** |
   | **인증** | SQL 로그인| SQL 인증은이 자습서에서 사용 됩니다. |
   | **사용자 이름** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정의 암호 | 서버를 만들 때 지정한 암호입니다. |
   | **암호를 저장하시겠습니까?** | Yes 또는 No | 때마다 암호를 입력 하지 않으려면 예를 선택 합니다. |
   | **데이터베이스 이름** | *비워 둡니다* | 연결할 데이터베이스의 이름입니다. |
   | **서버 그룹** | 선택 <Default> | 서버 그룹을 만든 경우에 특정 서버 그룹을 설정할 수 있습니다. | 

   ![새 연결 아이콘](media/quickstart-sql-dw/new-connection-screen.png) 

3. 서버에 연결 하려면 Azure Data Studio 허용 하는 방화벽 규칙이 없는 경우는 **새 방화벽 규칙 만들기** 양식이 열립니다. 양식을 새 방화벽 규칙을 만들려고 합니다. 자세한 내용은 참조 하세요 [방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)합니다.

   ![새 방화벽 규칙](media/quickstart-sql-dw/firewall.png)  

4. 열리면 서버 연결에 *서버* 보충 합니다.

## <a name="create-the-tutorial-data-warehouse"></a>자습서 data warehouse 만들기
1. 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭 하 고 선택 **새 쿼리 합니다.**

1. 다음 코드 조각을 쿼리 편집기에 붙여넣고 클릭 **실행**:

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

쿼리 편집기에 연결 되어는 *마스터* 했지만 데이터베이스에 테이블을 만들려면 원하는 합니다 *TutorialDB* 데이터베이스입니다. 

1. 연결 컨텍스트를 변경 **TutorialDB**:

   ![컨텍스트 변경](media/quickstart-sql-database/change-context.png)


1. 다음 코드 조각을 쿼리 편집기에 붙여넣고 클릭 **실행**:

   > [!NOTE]
   > 에 추가 수도 있고 편집기에서 이전 쿼리를 덮어쓸 수 있습니다. 클릭 **실행** 만 선택 되어 있는 쿼리를 실행 합니다. 선택한 내용이 없는 경우 클릭 **실행** 편집기에 있는 모든 쿼리를 실행 합니다.

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

1. 다음 코드 조각을 쿼리 편집기에 붙여넣고 클릭 **실행**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>결과 보려면
1. 다음 코드 조각을 쿼리 편집기에 붙여넣고 클릭 **실행**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 쿼리 결과가 표시 됩니다.

   ![결과 선택](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>리소스 정리

이 빠른 시작을 기반으로이 컬렉션의 다른 문서입니다. 후속 빠른 시작을 사용 하 여 작업을 계속 하려는 경우 정리 하지 마세요이 빠른 시작에서 만든 리소스입니다. 계속 하지 않으려는 경우 다음 단계를 사용 하 여 Azure portal에서이 빠른 시작에서 만든 리소스를 삭제 합니다.
필요 없는 리소스 그룹을 삭제 하 여 리소스를 정리 합니다. 자세한 내용은 참조 하세요 [리소스를 정리](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)합니다.


## <a name="next-steps"></a>다음 단계

Azure SQL data warehouse에 성공적으로 연결 하 고 쿼리를 실행 했으므로 사용해 합니다 [코드 편집기 자습서](tutorial-sql-editor.md)합니다.
