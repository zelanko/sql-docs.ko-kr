---
title: '외부 데이터 액세스: Oracle - PolyBase'
description: 이 문서에서는 PolyBase를 사용하여 Oracle 데이터에 액세스하기 위한 외부 데이터 원본을 만드는 방법을 보여줍니다.
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15'
ms.openlocfilehash: b0ae62c8cf7dc16529c1ca63460f7e2e6615faca
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461904"
---
# <a name="configure-polybase-to-access-external-data-in-oracle"></a>Oracle의 외부 데이터에 액세스하도록 PolyBase 구성

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 문서에서는 SQL Server 인스턴스에서 PolyBase를 사용하여 Oracle에서 외부 데이터를 쿼리하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

PolyBase를 설치하지 않은 경우 [PolyBase 설치](polybase-installation.md)를 참조하세요.

  데이터베이스 범위 자격 증명을 만들기 전에 [마스터 키](../../t-sql/statements/create-master-key-transact-sql.md)를 만들어야 합니다. 

## <a name="configure-an-oracle-external-data-source"></a>Oracle 외부 데이터 원본 구성

Oracle 데이터 원본의 데이터를 쿼리하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다.

이 섹션에서는 다음 Transact-SQL 명령이 사용됩니다.

- [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS(Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)


1. Oracle 소스에 액세스하기 위한 데이터베이스 범위 자격 증명을 만듭니다.

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```
    
   > [!IMPORTANT] 
   > PolyBase용 Oracle ODBC 커넥터는 기본 인증만 지원하고 Kerberos 인증은 지원하지 않습니다. 

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다.

    ```sql
    /* 
    * LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    * PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    * CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = 'oracle://<server address>[:<port>]',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_name)
    ```

1. **선택 사항:** 외부 테이블에 대한 통계를 만듭니다.

    최적의 쿼리 성능을 위해서는 특히 조인, 필터 및 집계에 사용되는 외부 테이블 열에 대해 통계를 만드는 것이 좋습니다.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>외부 데이터 원본을 만든 후에는 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 명령을 사용하여 해당 원본 위에 쿼리 가능 테이블을 만들 수 있습니다. 

자세한 내용 및 예제는 다음 문서를 참조하세요.

- [외부 테이블 만들기](../../t-sql/statements/create-external-table-transact-sql.md).
- [SQL Server PolyBase 개요](polybase-guide.md).
