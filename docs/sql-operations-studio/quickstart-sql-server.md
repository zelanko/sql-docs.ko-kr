---
title: "빠른 시작: 연결 및 SQL 작업 Studio (미리 보기)를 사용 하 여 SQL Server에 쿼리할 | Microsoft Docs"
description: "이 빠른 시작에서는 SQL 작업 Studio (미리 보기)를 사용 하 여 SQL Server에 연결 하 고 쿼리를 실행 하는 방법을 보여 줍니다."
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c0f78537429026583fe970a65426bc909a46557
ms.sourcegitcommit: 6c06267f3eeeb3f0d6fc4c57e1387621720ca8bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2018
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>빠른 시작: 연결 하 고 사용 하 여 SQL Server 쿼리 [!INCLUDE[name-sos](../includes/name-sos-short.md)]
이 빠른 시작을 사용 하는 방법을 보여 줍니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)] SQL Server에 연결 하 고 TRANSACT-SQL (T-SQL) 문을 만드는 데 사용할는 *TutorialDB* 에 사용 된 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 자습서입니다.

## <a name="prerequisites"></a>필수 구성 요소

이 빠른 시작을 완료 하려면 필요 [!INCLUDE[name-sos](../includes/name-sos-short.md)], 및 SQL Server에 액세스 합니다.

- [설치 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)합니다.

SQL Server에 액세스할 수 없으면 다음 링크에서 플랫폼을 선택 (SQL 로그인 및 암호를 기억 하 고 있는지 확인!).
- [Windows-SQL Server 2017 Developer Edition 다운로드](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS-Docker에서 SQL Server 2017 다운로드](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)
- [Linux-다운로드 SQL 2017 Server Developer Edition](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-overview#install) -까지의 단계를 수행 하면 *만들기 및 쿼리 데이터*합니다.


## <a name="connect-to-a-sql-server"></a>SQL Server에 연결

   
1. 시작  **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** 합니다.
1. 처음으로 실행 하면  *[!INCLUDE[name-sos](../includes/name-sos-short.md)]*  는 **연결** 대화 상자가 열립니다. 경우는 **연결** 대화 상자를 열고 하지 않습니다는 **새 연결** 아이콘에는 **서버** 페이지:
   
   ![새 연결 상태 아이콘](media/quickstart-sql-server/new-connection-icon.png)

1. 이 문서에서는 *SQL 로그인*, 하지만 *Windows 인증* 지원 됩니다. 필드를 다음과 같이 입력 합니다.
 
    - **서버 이름:** localhost
    - **인증 유형:** SQL 로그인  
    - **사용자 이름:** SQL Server에 대 한 사용자 이름  
    - **암호:** SQL Server에 대 한 암호  
    - **데이터베이스 이름:** 이 필드를 비워 둡니다. 
    - **서버 그룹:** \<기본\>  

   ![새 연결 화면](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>데이터베이스 만들기

다음 단계 라는 데이터베이스를 만든 **TutorialDB**:

1. 서버를 마우스 오른쪽 단추로 클릭 **localhost**를 선택 하 고 **새 쿼리 합니다.**
1. 다음 코드 조각은 쿼리 창에 붙여 넣습니다. 

   ```sql
   USE master
   GO
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
1. 쿼리를 실행 하려면 클릭 **실행** 합니다.

쿼리가 완료 된 후 새 **TutorialDB** 데이터베이스 목록에 나타납니다. 마우스 오른쪽 단추로 표시 되지 않는 경우는 **데이터베이스** 노드 선택한 **새로 고침**합니다.


## <a name="create-a-table"></a>테이블 만들기

쿼리 편집기에 연결 되었는지는 *마스터* 했지만 데이터베이스의 테이블을 만들려고 할는 *TutorialDB* 데이터베이스입니다. 

1. 연결 컨텍스트를 변경 **TutorialDB**:

   ![컨텍스트 변경](media/quickstart-sql-server/change-context.png)



1. 다음 코드 조각은 쿼리 창에 붙여넣고 클릭 **실행**:

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
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

쿼리가 완료 된 후 새 **고객** 테이블이 테이블 목록에 나타납니다. 마우스 오른쪽 단추로 클릭 해야 할 수도 있습니다는 **TutorialDB > 테이블** 노드 선택한 **새로 고침**합니다.

## <a name="insert-rows"></a>행 삽입

- 다음 코드 조각은 쿼리 창에 붙여넣고 클릭 **실행**:

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



## <a name="view-the-data-returned-by-a-query"></a>쿼리에서 반환 된 데이터 보기
1. 다음 코드 조각은 쿼리 창에 붙여넣고 클릭 **실행**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 쿼리 결과 표시 됩니다.

   ![결과 선택](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>다음 단계
SQL Server 및 쿼리 실행에 성공적으로 연결 되었는지, 했으므로 사용해는 [코드 편집기 자습서](tutorial-sql-editor.md)합니다.


