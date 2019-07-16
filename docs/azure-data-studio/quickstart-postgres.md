---
title: '빠른 시작: 연결 및 쿼리 PostgreSQL'
titleSuffix: Azure Data Studio
description: 이 빠른 시작에서는 Azure Data Studio를 사용 하 여 PostgreSQL에 연결 하 고 쿼리를 실행 하는 방법
ms.custom: seodec18
ms.date: 03/19/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
ms.openlocfilehash: 9dcbbe621ab237eeceff55cd5f931d7d650dd3b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959462"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>빠른 시작: 연결 하 고 사용 하 여 PostgreSQL 쿼리 [!INCLUDE[name-sos](../includes/name-sos-short.md)]
이 빠른 시작에 사용 하는 방법을 보여 줍니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)] Postgres에 연결한 다음 SQL 문을 사용 하 여 데이터베이스를 만들 *tutorialdb* 하 고 쿼리 하 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 완료 하려면 [!INCLUDE[name-sos](../includes/name-sos-short.md)], 용 PostgreSQL 확장 [! 포함[이름을 sos](../includes/name-sos-short.md), 및 PostgreSQL 서버에 액세스 합니다.

- [[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)를 설치합니다.
- [Azure Data Studio 용 PostgreSQL 확장을 설치할](postgres-extension.md)합니다.
- [PostgreSQL 설치](https://www.postgresql.org/download/)합니다. (또는 사용 하 여 클라우드 Postgres 데이터베이스를 만들 수 있습니다 [az postgres 등록](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli)). 

## <a name="connect-to-postgresql"></a>PostgreSQL에 연결

1. **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** 를 시작합니다.

2. 처음 시작 하면 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 는 **연결** 대화 상자가 열립니다. **연결** 대화 상자가 열리지 않는 경우 **서버** 페이지에서 **새 연결** 아이콘을 클릭합니다.

   ![새 연결 아이콘](media/quickstart-postgresql/new-connection-icon.png)

3. 로 표시 되는 형태로 **연결 유형** 선택한 **PostgreSQL** 드롭다운 목록에서.


4. 서버 이름, 사용자 이름 및 암호를 사용 하 여 PostgreSQL 서버에 대 한 나머지 필드를 입력 합니다. 

   ![새 연결 화면](media/quickstart-postgresql/new-connection-screen.png)  

   | 설정       | 예제 값 | 설명 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | localhost | 정규화된 서버 이름 |
   | **사용자 이름** | postgres | 사용 하 여 로그인 하려는 사용자 이름입니다. |
   | **암호(SQL 로그인)** | *password* | 로그인에 사용 된 계정의 암호입니다. |
   | **암호** | *확인* | 연결할 때마다 암호를 입력 하지 않으려면이 확인란을 선택 합니다. |
   | **데이터베이스 이름** | \<Default\> | 데이터베이스를 지정 하는 연결 하려는 경우이 입력 합니다. |
   | **서버 그룹** | \<Default\> | 이 옵션을 통해이 연결을 만들면 특정 서버 그룹을 할당할 수 있습니다. | 
   | **이름 (선택 사항)** | *비워 둡니다* | 이 옵션에는 서버에 대 한 이름을 지정할 수 있습니다. | 

5. **연결**을 선택합니다. 

성공적으로 연결되면 서버가 **서버** 사이드바에 표시됩니다.


## <a name="create-a-database"></a>데이터베이스 만들기

다음 단계에서는 명명 된 데이터베이스를 만듭니다 **tutorialdb**:

1. PostgreSQL 서버를 마우스 오른쪽 단추로 클릭 합니다 **서버** 사이드바 가젯과 선택 **새 쿼리**합니다.

2. 이 SQL 문은 열리는 쿼리 편집기에 붙여 넣습니다.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. 도구 모음에서 선택 **실행** 쿼리를 실행 합니다. 에 알림을 표시 합니다 **메시지** 창 쿼리 진행률을 표시 합니다.

>[!TIP]
> 사용할 수 있습니다 **F5** 문을 사용 하는 대신 실행 하거나 키보드에서 **실행**합니다.

쿼리 완료 후 마우스 오른쪽 단추로 클릭 **데이터베이스** 선택한 **새로 고침** 보려는 **tutorialdb** 아래의 목록에는 **데이터베이스** 노드 .


## <a name="create-a-table"></a>테이블 생성하기

 다음 단계는 테이블을 만들 합니다 **tutorialdb**:

1. 연결 컨텍스트를 변경 **tutorialdb** 드롭다운을 사용 하 여 쿼리 편집기에서. 

   ![컨텍스트 변경](media/quickstart-postgresql/change-context.png)

2. 다음 SQL 문을 쿼리 편집기에 붙여넣고 클릭 **실행**합니다. 

   > [!NOTE]
   > 이 항목을 추가 하거나 편집기에서 기존 쿼리를 덮어쓸 수 있습니다. 클릭 **실행** 만 강조 표시 되는 쿼리를 실행 합니다. 아무 것도 강조 표시 되 면 클릭 **실행** 편집기에 있는 모든 쿼리를 실행 합니다.

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

다음 조각을 쿼리 창에 붙여넣고 누릅니다 **실행**:

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

## <a name="query-the-data"></a>데이터를 쿼리 합니다.

1. 다음 코드 조각을 쿼리 편집기에 붙여넣고 클릭 **실행**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. 쿼리 결과가 표시 됩니다.

   ![결과 보기](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>다음 단계

에 대 한 자세한 합니다 [postgres Azure 데이터 스튜디오에서 사용할 수 있는 시나리오](postgres-extension.md)합니다. 