---
title: '빠른 시작: PostgreSQL 연결 및 쿼리'
description: Azure Data Studio를 사용하여 PostgreSQL에 연결하고 SQL 문을 사용하여 데이터베이스를 만들고 쿼리해 보는 빠른 시작을 진행합니다.
ms.custom: seodec18
ms.date: 09/18/2019
ms.prod: azure-data-studio
ms.technology: ''
ms.reviewer: alayu, maghan, sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
ms.openlocfilehash: e2ba0f0123faeacd0f431a72ef35add40ee48e19
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411309"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-postgresql"></a>빠른 시작: Azure Data Studio를 사용하여 PostgreSQL 연결 및 쿼리

이 빠른 시작에서는 Azure Data Studio를 사용하여 PostgreSQL에 연결한 다음 SQL 문을 사용하여 데이터베이스 *tutorialdb*를 만들고 쿼리하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 구성 요소

이 빠른 시작을 완료하려면 Azure Data Studio, Azure Data Studio용 PostgreSQL 확장 및 PostgreSQL 서버에 대한 액세스 권한이 필요합니다.

- [Azure Data Studio를 설치합니다.](download.md)
- [Azure Data Studio용 PostgreSQL 확장을 설치합니다](postgres-extension.md).
- [PostgreSQL을 설치합니다](https://www.postgresql.org/download/). (또는 [az postgres up](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli)을 사용하여 클라우드에서 Postgres 데이터베이스를 만들 수 있습니다). 

## <a name="connect-to-postgresql"></a>PostgreSQL에 연결

1. **Azure Data Studio**를 시작합니다.

2. Azure Data Studio를 처음으로 시작하면 **연결** 대화 상자가 열립니다. **연결** 대화 상자가 열리지 않으면 **서버** 페이지에서 **새 연결** 아이콘을 클릭합니다.

   ![새 연결 아이콘](media/quickstart-postgresql/new-connection-icon.png)

3. 표시되는 양식에서 **연결 형식**으로 이동하고 드롭다운에서 **PostgreSQL**을 선택합니다.


4. 나머지 필드에 PostgreSQL 서버의 서버 이름, 사용자 이름 및 암호를 입력합니다. 

   ![새 연결 화면](media/quickstart-postgresql/new-connection-screen.png)  

   | 설정       | 예제 값 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | localhost | 정규화된 서버 이름 |
   | **사용자 이름** | postgres | 로그인할 사용자 이름입니다. |
   | **암호(SQL 로그인)** | *password* | 로그인하는 계정의 암호입니다. |
   | **암호** | *확인* | 연결할 때마다 암호를 입력하지 않으려면 이 확인란을 선택합니다. |
   | **데이터베이스 이름** | \<Default\> | 연결에서 데이터베이스를 지정하도록 하려면 이 항목을 채웁니다. |
   | **서버 그룹** | \<Default\> | 이 옵션을 사용하면 만드는 특정 서버 그룹에 이 연결을 할당할 수 있습니다. | 
   | **이름(선택 사항)** | ‘비워 둠’ | 이 옵션을 사용하면 서버의 이름을 지정할 수 있습니다. | 

5. **연결**을 선택합니다. 

성공적으로 연결되면 서버가 **서버** 사이드바에서 열립니다.


## <a name="create-a-database"></a>데이터베이스 만들기

다음 단계에서는 **tutorialdb**라는 데이터베이스를 만듭니다.

1. **서버** 사이드바에서 PostgreSQL을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

2. 열리는 쿼리 편집기에 다음 SQL 문을 붙여 넣습니다.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. 도구 모음에서 **실행**을 선택하여 쿼리를 실행합니다. **메시지** 창에 알림이 표시되어 쿼리 진행률을 보여 줍니다.

>[!TIP]
> **실행**을 사용하지 않고 키보드의 **F5** 키를 사용하여 문을 실행할 수도 있습니다.

쿼리가 완료된 후 **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택하여 **데이터베이스** 노드 아래의 목록에서 **tutorialdb**를 볼 수 있습니다.


## <a name="create-a-table"></a>테이블 만들기

 다음 단계에서는 **tutorialdb**에서 테이블을 만듭니다.

1. 쿼리 편집기의 드롭다운을 사용하여 **tutorialdb**의 연결 컨텍스트를 변경합니다. 

   ![컨텍스트 변경](media/quickstart-postgresql/change-context.png)

2. 쿼리 편집기에 다음 SQL 문을 붙여 넣고 **실행**을 클릭합니다. 

   > [!NOTE]
   > 편집기에서 이 문을 추가하거나 기존 쿼리를 덮어쓸 수 있습니다. **실행**을 클릭하면 강조 표시된 쿼리만 실행됩니다. 아무것도 선택하지 않은 경우 **실행**을 클릭하면 편집기의 모든 쿼리가 실행됩니다.

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>행 삽입

쿼리 창에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>데이터 쿼리

1. 쿼리 편집기에 다음 코드 조각을 붙여넣고 **실행**을 클릭합니다.
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. 쿼리 결과가 다음과 같이 표시됩니다.

   ![결과 보기](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>다음 단계

[Azure Data Studio에서 Postgres에 사용할 수 있는 시나리오](postgres-extension.md)에 대해 알아보세요. 