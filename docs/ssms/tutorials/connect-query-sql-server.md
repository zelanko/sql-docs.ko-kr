---
Title: 'Tutorial: Connect and Query SQL Server using SQL Server Management Studio'
description: SQL Server Management Studio를 사용하여 SQL Server에 연결 및 기본 T-SQL 쿼리 실행에 대한 자습서입니다.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 6f4110a0ae1b4ca349cc9b990cc9a32f7d41764d
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-connect-and-query-sql-server-using-sql-server-management-studio"></a>자습서: SQL Server Management Studio를 사용하여 SQL Server 연결 및 쿼리
이 자습서에서는 SSMS(SQL Server Management Studio)를 사용하여 SQL Server 인스턴스에 연결하고 몇 가지 기본 T-SQL(Transact-SQL) 명령을 실행하는 방법을 알려 줍니다. 이 문서에서는 다음을 수행하는 방법을 보여줍니다.

> [!div class="checklist"]
> * [SQL Server에 연결](#connect-to-a-sql-server)
> * [새 데이터베이스 만들기(**TutorialDB**)](#create-a-database)
> * [새 데이터베이스에서 테이블(**고객**) 만들기](#create-a-table)
> * [새 **고객** 테이블에 행 삽입](#insert-rows)
> * [**고객** 테이블 쿼리 및 결과 보기](#view-query-results)
> * [쿼리 창 테이블을 사용하여 연결 속성 확인](#verify-your-query-window-connection-properties)
> * [쿼리 창이 연결된 서버 변경](#change-server-connection-within-query-window)


## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio 및 SQL Server에 대한 액세스가 필요합니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.

SQL Server에 대한 액세스가 없는 경우 다음 링크에서 플랫폼을 선택합니다(SQL 인증을 선택하는 경우 SQL 로그인 및 암호를 기억하고 있는지 확인).
- [Windows - SQL Server 2017 Developer Edition 다운로드](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS - Docker에서 SQL Server 2017 다운로드](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)


## <a name="connect-to-a-sql-server"></a>SQL Server에 연결

1. SSMS(SQL Server Management Studio)를 시작합니다.
1. 처음으로 SSMS를 실행하면 **서버에 연결** 대화 상자가 열립니다. 
      - **서버에 연결** 대화 상자가 열리지 않는 경우 **개체 탐색기** > **연결**(또는 옆의 아이콘) > **데이터베이스 엔진**에서 수동으로 열 수 있습니다.

        ![개체 탐색기에서 연결](media/connect-query-sql-server/connectobjexp.png)

1. **서버에 연결** 대화 상자에서 연결 옵션을 작성합니다. 

    - **서버 유형**: 데이터베이스 엔진(일반적으로 기본적으로 선택됨)
    - **인증**: Windows 인증(이 문서에서는 Windows 인증을 사용하지만 SQL 로그인이 지원되며 선택한 경우 사용자 이름 / 암호를 입력해야 함)

      ![연결](media/connect-query-sql-server/connection.png)

        또한 **옵션** 단추를 클릭하여 추가 연결 옵션(예: 연결하려는 데이터베이스, 연결 시간 제한 값 및 네트워크 프로토콜)을 수정할 수도 있습니다. 이 문서의 목적을 위해 모든 값은 기본값으로 남겨져 있습니다. 

1. 필드를 입력하면 **연결**을 클릭합니다. 

1. **개체 탐색기**의 개체를 탐색하여 SQL Server에 대한 연결이 성공한 것을 확인할 수 있습니다. 

   ![연결 성공](media/connect-query-sql-server/successfulconnection.png)


## <a name="create-a-database"></a>데이터베이스 만들기
다음 단계에서는 TutorialDB라는 데이터베이스를 만듭니다. 

1. **개체 탐색기**에서 서버를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

   ![새 쿼리](media/connect-query-sql-server/newquery.png)
   
1. 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣습니다. 
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
   ```
2. 쿼리를 실행하려면 **실행**을 클릭합니다(또는 키보드의 F5 키를 누름). 

   ![쿼리 실행](media/connect-query-sql-server/execute.png)
  
 
쿼리가 완료된 후 **개체 탐색기** 내의 데이터베이스 목록에 새 **TutorialDB**가 나타납니다. 표시되지 않는 경우 데이터베이스 노드를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  


## <a name="create-a-table"></a>테이블 만들기
다음 단계에서는 이제 새로 만든 **TutorialDB** 데이터베이스에 테이블을 만듭니다. 그러나 쿼리 편집기는 여전히 *master* 데이터베이스의 컨텍스트에 있으며 *TutorialDB* 데이터베이스에 테이블을 만들려고 합니다. 

1. 데이터베이스 드롭다운에서 원하는 데이터베이스를 선택하여 master 데이터베이스에서 **TutorialDB**로 쿼리의 연결 컨텍스트를 변경합니다. 

   ![데이터베이스 변경](media/connect-query-sql-server/changedb.png)

1. 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣고, 강조 표시하고, **실행**을 클릭합니다(또는 키보드의 F5 키를 누름). 
    - 쿼리 창에서 기존 텍스트를 대체하거나 끝에 추가할 수 있습니다. 쿼리 창에서 모든 항목을 실행하려는 경우 **실행**을 클릭합니다. 텍스트의 일부를 실행하려는 경우 해당 부분을 강조 표시한 다음, **실행**을 클릭합니다.  
  
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
쿼리가 완료된 후 **개체 탐색기**의 테이블 목록에 새 **고객** 테이블이 나타납니다. 테이블이 표시되지 않으면 마우스 오른쪽 단추로 **개체 탐색기**의 **TutorialDB > 테이블** 노드를 클릭하고 **새로 고침**을 선택합니다.

## <a name="insert-rows"></a>행 삽입
다음 단계는 이전에 만든 **고객** 테이블에 일부 행을 삽입합니다. 

다음 T-SQL 코드 조각을 쿼리 창에 붙여넣고 **실행**을 클릭합니다. 


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

## <a name="view-query-results"></a>쿼리 결과 보기
쿼리 결과는 쿼리 텍스트 창 아래에 표시됩니다. 다음 단계를 통해 **고객** 테이블을 쿼리하고 이전에 삽입된 행을 볼 수 있습니다.  

1. 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣고 **실행**을 클릭합니다. 

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```
1. 쿼리의 결과는 텍스트가 입력된 영역 아래에 표시됩니다. 

   ![쿼리 결과](media/connect-query-sql-server/queryresults.png)


1.  이러한 옵션 중 하나를 선택하여 결과가 표시되는 방식을 수정할 수 있습니다.

     ![결과](media/connect-query-sql-server/results.png)

    - 기본적으로 결과는 중간 단추인 **그리드 보기**에 있으며 테이블에 결과를 표시합니다. 
    - 첫 번째 단추는 다음 섹션의 이미지에 표시된 것처럼 **텍스트 보기**에 결과를 표시합니다.
    - 세 번째 단추를 통해 기본적으로 *.rpt로 끝나는 파일에 결과를 저장할 수 있습니다.

## <a name="verify-your-query-window-connection-properties"></a>쿼리 창 연결 속성 확인
쿼리 결과에서 연결 속성에 대한 정보를 찾을 수 있습니다. 
- 이전 단계에서 앞에서 언급한 쿼리를 실행한 후 쿼리 창 맨 아래에 있는 연결 속성을 검토합니다.
    - 연결되어 있는 서버 및 데이터베이스와 로그인한 사용자를 확인할 수 있습니다.
    - 또한 쿼리 기간 및 이전에 실행한 쿼리에 의해 반환된 행 수를 확인할 수도 있습니다.
    
    ![연결 속성](media/connect-query-sql-server/connectionproperties.png)  
    이 이미지에서 **텍스트 보기**에 결과가 표시됩니다.  

## <a name="change-server-connection-within-query-window"></a>쿼리 창 내의 서버 연결 변경
이러한 단계를 수행하여 현재 쿼리 창이 연결된 서버를 변경할 수 있습니다.
1. 쿼리 창 내에서 마우스 오른쪽 단추로 연결 > 연결 변경을 클릭합니다.
2. 쿼리가 연결된 서버를 변경할 수 있도록 하는 **서버에 연결** 대화 상자를 다시 엽니다. 
 
   ![연결 변경](media/connect-query-sql-server/changeconnection.png)
   - **개체 탐색기**가 연결된 서버가 아닌 현재 쿼리 창을 변경합니다. 



