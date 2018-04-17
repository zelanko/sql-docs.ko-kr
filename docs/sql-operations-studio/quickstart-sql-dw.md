---
title: '빠른 시작: 연결 하 고 SQL Operations Studio (preview) 를 사용 하는 Azure SQL 데이터 웨어하우스를 쿼리 하 | Microsoft Docs'
description: 이 빠른 시작에서는 SQL Operations Studio (preview) 를 사용 하 여 SQL 데이터베이스에 연결 하 고 쿼리를 실행 하는 방법을 보여 줍니다.
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d4ed7d25abb2780c719c5b8201ecae54e8e86bf
ms.sourcegitcommit: 6c06267f3eeeb3f0d6fc4c57e1387621720ca8bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2018
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>빠른 시작:를 사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 연결 하 고 Azure SQL 데이터 웨어하우스에 데이터를 쿼리 합니다.

이 빠른 시작 사용 방법을 보여 줍니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)] Azure SQL 데이터 웨어하우스에 연결 하 고 다음 TRANSACT-SQL 문을 사용 하 여 만들고 삽입 하 고 데이터를 선택 합니다. 

## <a name="prerequisites"></a>필수 구성 요소
이 빠른 시작을 완료 하려면 필요 [!INCLUDE[name-sos](../includes/name-sos-short.md)], 및 Azure SQL 데이터 웨어하우스 합니다.

- [설치 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)합니다.

SQL 데이터 웨어하우스를 모를 경우 참조 [SQL 데이터 웨어하우스를 만들](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision)합니다.

서버 이름 및 로그인 자격 증명 기억!


## <a name="connect-to-your-data-warehouse"></a>데이터 웨어하우스에 연결

사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)] Azure SQL 데이터 웨어하우스 서버에 연결을 설정할 수 있습니다.

1. 처음으로 실행 하면 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 는 **연결** 페이지가 열려야 합니다. 표시 되지 않으면는 **연결** 페이지 **연결 추가**, 또는 **새 연결** 아이콘에는 **서버** 사이드바:
   
   ![새 연결 상태 아이콘](media/quickstart-sql-dw/new-connection-icon.png)

2. 이 문서에서는 *SQL 로그인*, 하지만 *Windows 인증* 도 지원 합니다. 서버 이름, 사용자 이름 및 암호를 다음과 같이 사용 하 여 필드에 *프로그램* Azure SQL server:

   | 설정       | 제안된 값 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 정규화된 서버 이름 | 이름은 다음과 같이 해야: **sqldwsample.database.windows.net** |
   | **인증** | SQL 로그인| 이 자습서에서는 SQL 인증이 사용 됩니다. |
   | **사용자 이름** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정의 암호 | 서버를 만들 때 지정한 암호입니다. |
   | **암호를 저장하시겠습니까?** | Yes 또는 No | 암호를 입력 하지 않을 경우 예를 선택 합니다. |
   | **데이터베이스 이름** | *비워* | 연결할 데이터베이스의 이름입니다. |
   | **서버 그룹** | 선택 <Default> | 서버 그룹을 만든 경우에 특정 서버 그룹을 설정할 수 있습니다. | 

   ![새 연결 상태 아이콘](media/quickstart-sql-dw/new-connection-screen.png) 

3. 서버에 연결 하려면 SQL Operations Studio 허용 하는 방화벽 규칙에 없는 경우는 **새 방화벽 규칙 만들기** 양식이 열립니다. 새 방화벽 규칙을 만드는 양식을 완성 합니다. 자세한 내용은 참조 [방화벽 규칙](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)합니다.

   ![새 방화벽 규칙](media/quickstart-sql-dw/firewall.png)  

4. 연결 하 고 나면 서버에 열리면는 *서버* 사이드바 합니다.

## <a name="create-the-tutorial-data-warehouse"></a>Tutorial 데이터 웨어하우스 생성
1. 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭 하 고 선택 **새 쿼리 합니다.**

1. 다음 코드 조각은 쿼리 편집기에 붙여넣고 클릭 **실행**:

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

쿼리 편집기에 연결 되었는지는 *마스터* 했지만 데이터베이스의 테이블을 만들려고 할는 *TutorialDB* 데이터베이스입니다. 

1. 연결 컨텍스트를 변경 **TutorialDB**:

   ![컨텍스트 변경](media/quickstart-sql-database/change-context.png)


1. 다음 코드 조각은 쿼리 편집기에 붙여넣고 클릭 **실행**:

   > [!NOTE]
   > 이 추가 하거나 앞의 쿼리 편집기에서 덮어쓸 수 있습니다. 클릭 하면 **실행** 을 선택 하 여 쿼리를 실행 합니다. 어떤 영역도 선택 하는 경우 클릭 하면 **실행** 편집기에서 모든 쿼리를 실행 합니다.

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

1. 다음 코드 조각은 쿼리 편집기에 붙여넣고 클릭 **실행**:

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
1. 다음 코드 조각은 쿼리 편집기에 붙여넣고 클릭 **실행**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 쿼리 결과 표시 됩니다.

   ![결과 선택](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>리소스 정리

이 컬렉션의 다른 문서를이 퀵 스타트의 기반으로 작성 합니다. 계속 후속 퀵 스타트과 작동 하도록 하려는 경우 않습니다 정리 하지이 빠른 시작에서 만든 리소스가 있습니다. 계속 하려면 Azure 포털에서이 빠른 시작에서 만든 리소스를 삭제 하려면 다음 단계를 사용 합니다.
필요 없는 리소스 그룹을 삭제 하 여 리소스를 정리 합니다. 자세한 내용은 참조 [리소스를 정리](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources)합니다.


## <a name="next-steps"></a>다음 단계

Azure SQL 데이터 웨어하우스에 성공적으로 연결한 적 하 고 쿼리 실행 했으므로 사용해는 [코드 편집기 자습서](tutorial-sql-editor.md)합니다.