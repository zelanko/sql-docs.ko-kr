---
title: '외부 데이터 액세스: Teradata - PolyBase'
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 2ade016ec88f6f26655fea8ab5249e1f846ee74a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75225971"
---
# <a name="configure-polybase-to-access-external-data-in-teradata"></a>Teradata의 외부 데이터에 액세스하도록 PolyBase 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server 인스턴스에서 PolyBase를 사용하여 Teradata에서 외부 데이터를 쿼리하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

PolyBase를 설치하지 않은 경우 [PolyBase 설치](polybase-installation.md)를 참조하세요. 설치 문서에서는 필수 구성 요소를 설명합니다.

데이터베이스 범위 자격 증명을 만들기 전에 [마스터 키](../../t-sql/statements/create-master-key-transact-sql.md)를 만들어야 합니다. 

Teradata에서 PolyBase를 사용하려면 VC++ 재배포 가능 패키지가 필요합니다.
 
## <a name="configure-a-teradata-external-data-source"></a>Teradata 외부 데이터 원본 구성

Teradata 데이터 원본의 데이터를 쿼리하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다. 



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

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다.

    ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (LOCATION = teradata://<server address>[:<port>],
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL =credential_name);
    ```

1. **선택 사항:** 외부 테이블에 대한 통계를 만듭니다.

    최적의 쿼리 성능을 위해서는 특히 조인, 필터 및 집계에 사용되는 외부 테이블 열에 대해 통계를 만드는 것이 좋습니다.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>외부 데이터 원본을 만든 후에는 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 명령을 사용하여 해당 원본 위에 쿼리 가능 테이블을 만들 수 있습니다.

## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [SQL Server PolyBase 개요](polybase-guide.md)를 참조하세요.
