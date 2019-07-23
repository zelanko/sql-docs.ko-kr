---
title: SSMS(SQL Server Management Studio)를 사용하여 SQL Server 인스턴스에 연결 및 쿼리
description: SQL Server Management Studio를 사용하고 기본 T-SQL 쿼리를 실행하여 SQL Server 인스턴스에 연결하는 방법에 대한 자습서입니다.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.reviewer: sstein
ms.topic: quickstart
ms.prod_service: sql-tools
ms.prod: sql
ms.technology: ssms
ms.custom: ''
ms.date: 03/13/2018
ms.openlocfilehash: 105bcea172a91496c664578befc33f022b5c8d9e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256713"
---
# <a name="tutorial-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio-ssms"></a>자습서: SSMS(SQL Server Management Studio)를 사용하여 SQL Server 인스턴스에 연결 및 쿼리

이 자습서에서는 SSMS(SQL Server Management Studio)를 사용하여 SQL Server 인스턴스에 연결하고 몇 가지 기본 T-SQL(Transact-SQL) 명령을 실행하는 방법을 설명합니다. 이 문서에서는 아래 단계를 수행하는 방법을 보여줍니다.

> [!div class="checklist"]
> * SQL Server 인스턴스에 연결
> * 데이터베이스 만들기("TutorialDB")
> * 새 데이터베이스에서 테이블("Customers") 만들기
> * 새 테이블에 행 삽입
> * 새 테이블 쿼리 및 결과 보기
> * 쿼리 창 테이블을 사용하여 연결 속성 확인
> * 쿼리 창이 연결된 서버 변경

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 SQL Server Management Studio 및 SQL Server 인스턴스에 대한 액세스 권한이 필요합니다. 

* [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.

SQL Server 인스턴스에 대한 액세스 권한이 없는 경우 다음 링크에서 플랫폼을 선택합니다. SQL 인증을 선택한 경우 SQL Server 로그인 자격 증명을 사용합니다.

* **Windows**: [SQL Server 2017 Developer Edition 다운로드](https://www.microsoft.com/sql-server/sql-server-downloads).
* **macOS**: [Docker에서 SQL Server 2017 다운로드](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

## <a name="connect-to-a-sql-server-instance"></a>SQL Server 인스턴스에 연결

1. SQL Server Management Studio를 시작합니다. 처음으로 SSMS를 실행하면 **서버에 연결** 창이 열립니다. 열리지 않으면 **개체 탐색기** > **연결** > **데이터베이스 엔진**을 수동으로 선택하여 열 수 있습니다.

    ![개체 탐색기의 연결 링크](media/connect-query-sql-server/connectobjexp.png)

2. **서버에 연결** 창에서 아래 목록에 따릅니다.

    * **서버 형식**에서 **데이터베이스 엔진**(일반적으로 기본 옵션)을 선택합니다.
    * **서버 이름**에서 SQL Server 인스턴스의 이름을 입력합니다. (이 아티클에서는 호스트 이름 NODE5[NODE5\SQL2016ST]에서 인스턴스 이름 SQL2016ST를 사용합니다.) SQL Server 인스턴스 이름을 확인하는 방법을 잘 모르는 경우 [SSMS를 사용하는 추가 팁과 요령](ssms-tricks.md#determine-sql-server-name)을 참조하세요.

    * **인증**에서 **Windows 인증**을 선택합니다. 이 아티클에서는 Windows 인증을 사용하지만 SQL Server 로그인도 지원합니다. **SQL 로그인**을 선택하는 경우 사용자 이름 및 암호를 묻는 메시지가 표시됩니다. 인증 형식에 대한 자세한 내용은 [서버에 연결(데이터베이스 엔진)](https://docs.microsoft.com/sql/ssms/f1-help/connect-to-server-database-engine)을 참조하세요.

    ![SQL Server 인스턴스를 사용하는 옵션을 포함한 "서버 이름" 필드](media/connect-query-sql-server/connection2.png)

    **옵션**을 선택하여 추가 연결 옵션을 수정할 수도 있습니다. 연결 옵션의 예제는 연결하려는 데이터베이스, 연결 제한 시간 값 및 네트워크 프로토콜입니다. 이 아티클에서는 모든 옵션에 기본값을 사용합니다.

3. 모든 필드를 완료한 후에 **연결**을 선택합니다.

### <a name="examples-of-successful-connections"></a>성공적인 연결의 예

SQL Server 연결에 성공했는지 확인하려면 **개체 탐색기** 내에서 개체를 확장하고 탐색합니다. 이러한 개체는 사용자가 연결하도록 선택한 서버 형식에 따라 달라집니다. 

* 온-프레미스 SQL 서버에 연결 - 이 경우 NODE5\SQL2016ST: ![온-프레미스 서버에 연결](media/connect-query-sql-server/connect-on-prem.png)

* SQL Azure DB에 연결 - 이 경우 msftestserver.database.windows.net: ![SQL Azure DB에 연결](media/connect-query-sql-server/connect-sql-azure.png)

  >[!NOTE]
  > 이 자습서의 앞 부분에서 *Windows 인증*을 사용하여 온-프레미스 SQL Server에 연결했지만 SQL Azure DB에는 이러한 방법이 지원되지 않습니다. 따라서 이 이미지는 SQL 인증을 사용하여 SQL Azure DB에 연결하는 방법을 보여 줍니다. 자세한 내용은 [SQL 온-프레미스 인증](../../relational-databases/security/choose-an-authentication-mode.md) 및 [SQL Azure 인증](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview#access-management)을 참조하세요. 

## <a name="create-a-database"></a>데이터베이스 만들기

아래 단계에 따라 TutorialDB라는 데이터베이스를 만듭니다.

1. 개체 탐색기에서 서버 인스턴스를 마우스 오른쪽 단추로 클릭한 다음, **새 쿼리**를 선택합니다.

   ![새 쿼리 링크](media/connect-query-sql-server/newquery.png)

2. 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣습니다. 

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

3. 쿼리를 실행하려면 **실행**(또는 키보드의 F5 키)을 선택합니다.

   ![실행 명령](media/connect-query-sql-server/execute.png)
  
    쿼리가 완료된 후에 개체 탐색기의 데이터베이스 목록에 새 TutorialDB 데이터베이스가 나타납니다. 표시되지 않는 경우 **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭한 다음, **새로 고침**을 선택합니다.  

## <a name="create-a-table-in-the-new-database"></a>새 데이터베이스에서 테이블 만들기

다음 섹션에서는 새로 만든 TutorialDB 데이터베이스에 테이블을 만듭니다. 쿼리 편집기가 *마스터*의 컨텍스트에 여전히 있기 때문에 다음 단계를 수행하여 연결 컨텍스트를 *TutorialDB* 데이터베이스로 전환합니다.

1. 다음과 같이 데이터베이스 드롭다운 목록에서 원하는 데이터베이스를 선택합니다. 

   ![데이터베이스 변경](media/connect-query-sql-server/changedb.png)

2. 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣고, 선택한 다음, **실행**(또는 키보드의 F5 키)을 선택합니다.  
   쿼리 창에서 기존 텍스트를 대체하거나 끝에 추가할 수 있습니다. 쿼리 창에서 모든 항목을 실행하려면 **실행**을 선택합니다. 텍스트의 일부를 실행하려면 해당 부분을 강조 표시한 다음, **실행**을 선택합니다.  
  
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

쿼리가 완료된 후에 개체 탐색기의 테이블 목록에 새 고객 테이블이 표시됩니다. 테이블이 표시되지 않으면 개체 탐색기에서 **TutorialDB** > **테이블** 노드를 마우스 오른쪽 단추로 클릭한 다음, **새로 고침**을 선택합니다.

## <a name="insert-rows-into-the-new-table"></a>새 테이블에 행 삽입

이전에 만든 고객 테이블에 일부 행을 삽입합니다. 이렇게 하려면 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣은 다음, **실행**을 선택합니다.

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

## <a name="query-the-table-and-view-the-results"></a>테이블 쿼리 및 결과 보기

쿼리 결과는 쿼리 텍스트 창 아래에 표시됩니다. 고객 테이블을 쿼리하고 이전에 삽입된 행을 보려면 다음 단계에 따릅니다.

1. 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣은 다음, **실행**을 선택합니다.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    쿼리의 결과는 텍스트가 입력된 영역 아래에 표시됩니다. 

   ![결과 목록](media/connect-query-sql-server/queryresults.png)

2. 다음과 같은 옵션 중 하나를 선택하여 결과가 표시되는 방식을 수정합니다.

     ![쿼리 결과를 표시하는 세 가지 옵션](media/connect-query-sql-server/results.png)

    * 가운데 단추는 **그리드 보기**에 결과를 표시합니다. 이것이 기본 옵션입니다. 
    * 첫 번째 단추는 다음 섹션의 이미지에 표시된 것처럼 **텍스트 보기**에 결과를 표시합니다.
    * 기본적으로 세 번째 단추를 통해 확장명이 .rpt인 파일에 결과를 저장할 수 있습니다.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>쿼리 창 테이블을 사용하여 연결 속성 확인

쿼리 결과에서 연결 속성에 대한 정보를 찾을 수 있습니다. 이전 단계에서 앞에서 언급한 쿼리를 실행한 후에 쿼리 창 맨 아래에 있는 연결 속성을 검토합니다.

* 연결되어 있는 서버 및 데이터베이스와 사용한 사용자 이름을 확인할 수 있습니다.
* 쿼리 기간 및 이전에 실행한 쿼리에 의해 반환된 행 수를 볼 수도 있습니다.

    ![연결 속성](media/connect-query-sql-server/connectionproperties.png)

    > [!Note]
    > 이미지의 **텍스트 보기**에 결과가 표시됩니다.

## <a name="change-the-server-based-on-the-query-window"></a>쿼리 창에 기준 서버 변경

아래 단계에 따라 현재 쿼리 창이 연결된 서버를 변경할 수 있습니다.

1. 쿼리 창을 마우스 오른쪽 단추로 클릭한 다음, **연결** > **연결 변경**을 선택합니다. **서버에 연결** 창이 다시 열립니다.

2. 쿼리가 사용하는 서버를 변경합니다.

   ![연결 변경 명령](media/connect-query-sql-server/changeconnection.png)

    > [!NOTE]
    > 이 작업에서는 개체 탐색기가 사용하는 서버가 아닌 쿼리 창이 연결된 서버만 변경합니다.

## <a name="next-steps"></a>다음 단계

실습을 통해 SSMS에 익숙해지는 것이 가장 좋습니다. 이러한 문서에서는 SSMS 내에서 사용할 수 있는 다양한 기능에 관해 도움을 얻을 수 있습니다.  이러한 문서에서는 SSMS의 구성 요소를 관리하는 방법과 정기적으로 사용하는 기능을 찾는 방법을 알아봅니다.

* [스크립팅](scripting-ssms.md)
* [SSMS에서 템플릿 사용](../template/templates-ssms.md)
* [SSMS 구성](ssms-configuration.md)
* [SSMS 사용을 위한 추가 팁과 요령](ssms-tricks.md)