---
title: '빠른 시작: 연결 및 쿼리 SQL Operations Studio (미리 보기)를 사용 하 여 SQL Server | Microsoft Docs'
description: 이 빠른 시작에서는 SQL Operations Studio (미리 보기)를 사용 하 여 SQL Server에 연결 및 쿼리를 실행 하는 방법을 보여 줍니다.
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 7f8963de448c39709a4df102cdf764a361b7654c
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985075"
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>빠른 시작: 연결 및 SQL Server를 사용 하 여 쿼리 [!INCLUDE[name-sos](../includes/name-sos-short.md)]
이 빠른 시작에 사용 하는 방법을 보여 줍니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)] SQL Server에 연결한 다음 TRANSACT-SQL (T-SQL) 문을 사용 하 여 만드는 합니다 *TutorialDB* 에 사용 되는 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 자습서입니다.

## <a name="prerequisites"></a>필수 구성 요소

이 빠른 시작을 완료 하려면 [!INCLUDE[name-sos](../includes/name-sos-short.md)], 및 SQL Server에 액세스 합니다.

- [설치할 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)합니다.

SQL Server에는 액세스할 수 없는 경우 다음 링크에서 플랫폼을 선택 (SQL 로그인 및 암호를 놓치지 않도록!).
- [Windows - SQL Server 2017 Developer Edition 다운로드](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS - Docker에서 SQL Server 2017 다운로드](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux-SQL Server 2017 Developer Edition 다운로드](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install) -단계를 수행 해야 *만들기 및 쿼리 데이터*입니다.


## <a name="connect-to-a-sql-server"></a>SQL Server에 연결

   
1. 시작 **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** 합니다.
1. 처음 실행 하면 *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* 는 **연결** 대화 상자가 열립니다. 경우는 **연결** 대화 상자가 열리지를 클릭 합니다 **새 연결** 아이콘에는 **서버** 페이지:
   
   ![새 연결 아이콘](media/quickstart-sql-server/new-connection-icon.png)

1. 이 아티클에서 *SQL 로그인*, 되지만 *Windows 인증* 지원 됩니다. 필드를 다음과 같이 입력 합니다.
 
    - **서버 이름:** localhost
    - **인증 유형:** SQL 로그인  
    - **사용자 이름:** SQL Server에 대 한 사용자 이름  
    - **암호:** SQL Server에 대 한 암호  
    - **데이터베이스 이름:** 이 필드를 비워 둡니다. 
    - **서버 그룹:** \<기본\>  

   ![새 연결 화면](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>데이터베이스 만들기

다음 단계에서는 명명 된 데이터베이스를 만듭니다 **TutorialDB**:

1. 서버를 마우스 오른쪽 단추로 클릭 **localhost**, 선택한 **새 쿼리 합니다.**
1. 다음 코드 조각을 쿼리 창에 붙여 넣습니다. 

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

쿼리 완료 후 새 **TutorialDB** 데이터베이스 목록에 표시 됩니다. 이 작업을 보이지 않으면 마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 노드를 선택 **새로 고침**합니다.


## <a name="create-a-table"></a>테이블 만들기

쿼리 편집기에 연결 되어는 *마스터* 했지만 데이터베이스에 테이블을 만들려면 원하는 합니다 *TutorialDB* 데이터베이스입니다. 

1. 연결 컨텍스트를 변경 **TutorialDB**:

   ![컨텍스트 변경](media/quickstart-sql-server/change-context.png)



1. 다음 조각을 쿼리 창에 붙여넣고 누릅니다 **실행**:

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
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

쿼리 완료 후 새 **고객** 테이블이 테이블 목록에 나타납니다. 마우스 오른쪽 단추로 클릭 해야 합니다 **TutorialDB > 테이블** 노드를 선택 **새로 고침**합니다.

## <a name="insert-rows"></a>행 삽입

- 다음 조각을 쿼리 창에 붙여넣고 누릅니다 **실행**:

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
1. 다음 조각을 쿼리 창에 붙여넣고 누릅니다 **실행**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 쿼리 결과가 표시 됩니다.

   ![결과 선택](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>다음 단계
SQL Server 쿼리 실행을 성공적으로 연결한 했으므로 사용해 합니다 [코드 편집기 자습서](tutorial-sql-editor.md)합니다.


