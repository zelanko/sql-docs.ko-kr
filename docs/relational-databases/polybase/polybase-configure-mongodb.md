---
title: '외부 데이터 액세스: MongoDB - PolyBase'
description: 이 문서에서는 SQL Server 인스턴스에서 PolyBase를 사용하여 MongoDB에서 외부 데이터를 쿼리하는 방법을 설명합니다. 외부 데이터를 참조하는 외부 테이블을 만듭니다.
ms.date: 12/13/2019
ms.metadata: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 5ab1ef128b86f3426193b648c41f6cac6b324e71
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834043"
---
# <a name="configure-polybase-to-access-external-data-in-mongodb"></a>MongoDB의 외부 데이터에 액세스하도록 PolyBase 구성

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 문서에서는 SQL Server 인스턴스에서 PolyBase를 사용하여 MongoDB에서 외부 데이터를 쿼리하는 방법을 설명합니다.

## <a name="prerequisites"></a>필수 구성 요소

PolyBase를 설치하지 않은 경우 [PolyBase 설치](polybase-installation.md)를 참조하세요.

데이터베이스 범위 자격 증명을 만들기 전에 [마스터 키](../../t-sql/statements/create-master-key-transact-sql.md)를 만들어야 합니다. 
    

## <a name="configure-a-mongodb-external-data-source"></a>MongoDB 외부 데이터 원본 구성

MongoDB 데이터 원본의 데이터를 쿼리하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다.

이 섹션에서는 다음 Transact-SQL 명령이 사용됩니다.

- [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS(Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. MongoDB 소스에 액세스하기 위한 데이터베이스 범위 자격 증명을 만듭니다.

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```
    
   > [!IMPORTANT] 
   > PolyBase용 MongoDB ODBC 커넥터는 기본 인증만 지원하고 Kerberos 인증은 지원하지 않습니다.    
    
1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다.

    ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (LOCATION = 'mongodb://<server>[:<port>]',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_name);
    ```

1. **선택 사항:** 외부 테이블에 대한 통계를 만듭니다.

    최적의 쿼리 성능을 위해서는 특히 조인, 필터 및 집계에 사용되는 외부 테이블 열에 대해 통계를 만드는 것이 좋습니다.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>외부 데이터 원본을 만든 후에는 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 명령을 사용하여 해당 원본 위에 쿼리 가능 테이블을 만들 수 있습니다.
>
>예제는 [MongoDB용 외부 테이블 만들기](../../t-sql/statements/create-external-table-transact-sql.md#k-create-an-external-table-for-mongodb)를 참조하세요.

## <a name="flattening"></a>평면화
평면화는 MongoDB 문서 컬렉션에서 중첩되고 반복되는 데이터에 사용할 수 있습니다. 사용자는 `create an external table`을 활성화하고 데이터를 중첩 및/또는 반복하는 MongoDB 문서 콜렉션을 통해 관계형 스키마를 명시적으로 지정해야 합니다. JSON 중첩/반복 데이터 형식은 다음과 같이 평면화됩니다.

* 개체: 정렬되지 않은 키/값 컬렉션을 중괄호로 묶습니다(중첩).

   - SQL Server는 각 개체 키에 대한 테이블 열을 생성합니다.

     * 열 이름: objectname_keyname

* 배열: 쉼표로 구분한 정렬된 값을 대괄호로 묶습니다(반복).

   - SQL Server는 각 배열 항목에 대해 새 테이블 행을 추가합니다.

   - SQL Server는 배열 항목 인덱스를 저장하기 위해 배열당 1개의 열을 만듭니다.

     * 열 이름: arrayname_index

     * 데이터 형식: bigint

이 기술을 사용하면 다음을 비롯한 몇 가지 문제가 발생할 수 있습니다.

* 반복되는 빈 필드가 동일한 레코드의 플랫 필드에 포함된 데이터를 결과적으로 마스킹합니다.

* 반복되는 필드가 여러 개 있으면 생성되는 행 수가 폭발적으로 증가할 수 있습니다.

예를 들어 SQL Server는 비관계형 JSON 형식에 저장된 MongoDB 예제 데이터 세트 식당 컬렉션을 평가합니다. 각 식당에는 다른 날짜에 할당된 중첩된 주소 필드 및 등급 배열이 있습니다. 아래 그림은 중첩된 주소 및 중첩-반복 등급을 갖는 일반적인 식당을 보여 줍니다.

![MongoDB 평면화](../../relational-databases/polybase/media/mongo-flattening.png "MongoDB 식당 평면화")

개체 주소는 다음과 같이 평면화됩니다.

* Nested field restaurant.address.building becomes restaurant.address_building
* Nested field restaurant.address.coord becomes restaurant.address_coord
* Nested field restaurant.address.street becomes restaurant.address_street
* Nested field restaurant.address.zipcode becomes restaurant.address_zipcode

배열 등급은 아래와 같이 평면화됩니다.

| grades_date | grades_grade  | games_score | 
| ------------- | ------------------------- | -------------- |
|1393804800000 |A |2|
|1378857600000|A |6|
|135898560000 |A |10|
|1322006400000|A |9|
|1299715200000 |b |14|

## <a name="cosmos-db-connection"></a>Cosmos DB 연결

Cosmos DB mongo api 및 Mongo DB PolyBase 커넥터를 사용하여 **Cosmos DB 인스턴스**의 외부 테이블을 생성할 수 있습니다. 위에 나열된 동일한 단계를 따라 수행하면 됩니다. 데이터베이스 범위 자격 증명, 서버 주소, 포트 및 위치 문자열이 Cosmos DB 서버의 자격 증명을 반영하는지 확인합니다. 

## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [SQL Server PolyBase 개요](polybase-guide.md)를 참조하세요.
