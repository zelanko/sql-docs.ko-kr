---
title: '외부 데이터 액세스: SQL Server - PolyBase'
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: fa0a133e7a2c966798c168a74841350702b54295
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252321"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>SQL Server의 외부 데이터에 액세스하도록 PolyBase 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server 인스턴스에서 PolyBase를 사용하여 다른 SQL Server 인스턴스에서 외부 데이터를 쿼리하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

PolyBase를 설치하지 않은 경우 [PolyBase 설치](polybase-installation.md)를 참조하세요. 설치 문서에서는 필수 구성 요소를 설명합니다. 설치되고 나면 [PolyBase를 사용](polybase-installation.md#enable)하도록 설정합니다.

데이터베이스 범위 자격 증명을 만들기 전에 [마스터 키](../../t-sql/statements/create-master-key-transact-sql.md)를 만들어야 합니다. 

## <a name="configure-a-sql-server-external-data-source"></a>SQL Server 외부 데이터 원본 구성

SQL Server 데이터 원본의 데이터를 쿼리하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다. 
 
최적의 쿼리 성능을 위해서는 특히 조인, 필터 및 집계에 사용되는 외부 테이블 열에 대해 통계를 만듭니다.

이 섹션에서는 다음 Transact-SQL 명령이 사용됩니다.

- [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS(Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. SQL Server 원본에 액세스하기 위한 데이터베이스 범위 자격 증명을 만듭니다. 다음 예제에서는 `IDENTITY = 'username'` 및 `SECRET = 'password'`를 사용하여 외부 데이터 원본에 대한 자격 증명을 만듭니다.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials
    WITH IDENTITY = 'username', SECRET = 'password';
    ```

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다. 다음 예제를 참조하세요.

   - `SQLServerInstance`라는 외부 데이터 원본을 만듭니다.
   - 외부 데이터 원본(`LOCATION = '<vendor>://<server>[:<port>]'`)을 확인합니다. 예제에서는 SQL Server의 기본 인스턴스를 가리킵니다.
   - 계산을 원본(`PUSHDOWN`)으로 푸시해야 하는지 여부를 확인합니다. `PUSHDOWN`은 기본적으로 `ON`입니다.

   마지막으로, 예제에서는 이전에 만든 자격 증명을 사용합니다.

    ```sql
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
        WITH ( LOCATION = 'sqlserver://SqlServer',
        PUSHDOWN = ON,
        CREDENTIAL = SQLServerCredentials);
    ```

1. 필요에 따라 외부 테이블에 대한 통계를 만듭니다.

  최적의 쿼리 성능을 얻으려면 외부 테이블 열, 특히 조인 필터와 집계에 사용되는 열에 대한 통계를 만듭니다.

  ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY)
    WITH FULLSCAN;
  ```

>[!IMPORTANT] 
>외부 데이터 원본을 만든 후에는 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 명령을 사용하여 해당 원본 위에 쿼리 가능 테이블을 만들 수 있습니다.

## <a name="sql-server-connector-compatible-types"></a>SQL Server 커넥터 호환 형식

SQL Server 연결을 인식하는 다른 데이터 원본에 연결할 수 있습니다. SQL Server PolyBase 커넥터를 사용하여 Azure SQL Data Warehouse와 Azure SQL Database의 외부 테이블을 만듭니다. 이 작업을 수행하려면 이전에 나열된 것과 동일한 단계를 수행합니다. 데이터베이스 범위 자격 증명, 서버 주소, 포트 및 위치 문자열이 연결할 호환 가능한 데이터 원본의 자격 증명과 연관되는지 확인합니다.

## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [SQL Server PolyBase 개요](polybase-guide.md)를 참조하세요.
