---
title: Azure Synapse Analytics를 사용하여 연결 및 쿼리
description: 이 빠른 시작에서는 Azure Data Studio를 사용하여 Azure Synapse Analytics에서 전용 SQL 풀에 연결하는 방법을 보여 줍니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.reviewer: maghan, jrasnick
ms.custom: seodec18; seo-lt-2019
ms.date: 10/15/2020
ms.openlocfilehash: 1b0fe9ee55f9e0e1243ea72e8160b39a95876a55
ms.sourcegitcommit: 2144a22ad4380182133e87664a907fe6f06b5f95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94570929"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-data-using-a-dedicated-sql-pool-in-azure-synapse-analytics"></a>빠른 시작: Azure Data Studio를 통해 Azure Synapse Analytics의 전용 SQL 풀을 사용하여 데이터 연결 및 쿼리

이 빠른 시작에서는 Azure Data Studio를 사용하여 Azure Synapse Analytics에서 전용 SQL 풀에 연결하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 구성 요소
이 빠른 시작을 완료하려면 Azure Data Studio 및 Azure Synapse Analytics의 전용 SQL 풀이 필요합니다.

- [Azure Data Studio를 설치](./download-azure-data-studio.md)합니다.

전용 SQL 풀이 아직 없는 경우 [전용 SQL 풀 만들기](/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision)를 참조하세요.

서버 이름 및 로그인 자격 증명을 알아둡니다.


## <a name="connect-to-your-dedicated-sql-pool"></a>전용 SQL 풀에 연결

Azure Data Studio를 통해 Azure Synapse Analytics 서버에 연결합니다.

1. Azure Data Studio를 처음 실행하면 **연결** 페이지가 열립니다. **연결** 페이지가 표시되지 않으면 **연결 추가** 또는 **서버** 사이드바의 **새 연결** 아이콘을 선택합니다.
   
   ![새 연결 아이콘이 호출된 연결 페이지 스크린샷](media/quickstart-sql-dw/new-connection-icon.png)

2. 이 문서에서는 ‘SQL 로그인’을 사용하지만 ‘Windows 인증’도 지원됩니다.  Azure SQL Server의 서버 이름, 사용자 이름 및 암호를 사용하여 다음과 같이 필드를 채웁니다.

   |   설정    | 제안 값 | Description |
   |--------------|-----------------|-------------| 
   | **서버 이름** | 정규화된 서버 이름 | 예를 들어 **sqlpoolservername.database.windows.net** 과 같은 이름이 표시됩니다. |
   | **인증** | SQL 로그인| 이 자습서에서는 SQL 인증을 사용합니다. |
   | **사용자 이름** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정의 암호 | 서버를 만들 때 지정한 암호입니다. |
   | **암호를 저장하시겠습니까?** | Yes 또는 No | 암호를 매번 입력하지 않으려면 예를 선택합니다. |
   | **데이터베이스 이름** | ‘비워 둠’ | 연결할 데이터베이스의 이름입니다. |
   | **서버 그룹** | <Default> 선택 | 서버 그룹을 만든 경우 특정 서버 그룹으로 설정할 수 있습니다. | 

3. 서버에 Azure Data Studio 연결을 허용하는 방화벽 규칙이 없으면 **새 방화벽 규칙 만들기** 양식이 열립니다. 양식을 완료하여 새 방화벽 규칙을 만듭니다. 자세한 내용은 [방화벽 규칙](/azure/sql-database/sql-database-firewall-configure)을 참조하세요.

4. 성공적으로 연결되면 서버가 ‘서버’ 사이드바에서 열립니다.

## <a name="create-a-database-in-your-dedicated-sql-pool"></a>전용 SQL 풀에서 데이터베이스 만들기

1. 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **새 쿼리** 를 선택합니다.

2. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행** 을 선택합니다.

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

1. 연결 컨텍스트를 **TutorialDB** 로 변경합니다.

2. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행** 을 선택합니다.

   > [!NOTE]
   > 편집기에서 이전 쿼리에 추가하거나 이전 쿼리를 덮어쓸 수 있습니다. **실행** 을 선택하면 선택한 쿼리만 실행됩니다. 아무것도 선택하지 않은 경우 **실행** 을 선택하면 편집기의 모든 쿼리가 실행됩니다.

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

    :::image type="content" source="media/quickstart-sql-dw/create-table.png" alt-text="TutorialDB 데이터베이스에 테이블 만들기":::


## <a name="insert-rows"></a>행 삽입

1. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행** 을 선택합니다.

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```

    :::image type="content" source="media/quickstart-sql-dw/create-rows.png" alt-text="테이블에 행 만들기":::

## <a name="view-the-result"></a>결과 보기

1. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행** 을 선택합니다.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

2. 쿼리 결과가 다음과 같이 표시됩니다.

    :::image type="content" source="media/quickstart-sql-dw/view-results.png" alt-text="결과 보기":::


## <a name="clean-up-resources"></a>리소스 정리

이 문서에서 만든 샘플 데이터베이스로 계속 작업을 수행하지 않으려는 경우 [리소스 그룹을 삭제](/azure/synapse-analytics/sql-data-warehouse/create-data-warehouse-portal#clean-up-resources)합니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 [Azure Data Studio를 사용하여 Synapse SQL에 연결](https://docs.microsoft.com/azure/synapse-analytics/sql/get-started-azure-data-studio)을 참조하세요.

이제 Azure Synapse Analytics에 연결하고 쿼리를 실행했으므로 [코드 편집기 자습서](tutorial-sql-editor.md)를 사용해 보세요.