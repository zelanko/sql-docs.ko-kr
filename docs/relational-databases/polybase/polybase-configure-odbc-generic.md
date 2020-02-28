---
title: '외부 데이터 액세스: ODBC 제네릭 형식 - PolyBase'
ms.date: 02/19/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: ddee333a437ca7250252fb3938ee248bb28269f3
ms.sourcegitcommit: 87b932dc4b603a35a19f16e2c681b6a8d4df1fec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77507587"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>SQL Server의 외부 데이터에 액세스하도록 PolyBase 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2019의 PolyBase를 사용하면 ODBC 커넥터를 통해 ODBC 호환 데이터 원본에 연결할 수 있습니다.

이 문서에서는 ODBC 드라이버를 사용하는 몇 가지 예제를 제공합니다. 해당 ODBC 공급자의 구체적인 예제를 확인하세요. 적절한 연결 문자열 옵션을 결정하려면 데이터 원본에 대한 ODBC 드라이버 설명서를 참조하세요. 이 문서의 예제는 특정 ODBC 드라이버에는 적용되지 않을 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

>[!NOTE]
>이 기능을 사용하려면 Windows에서 SQL Server가 필요합니다.

* [PolyBase 설치](polybase-installation.md).

* 데이터베이스 범위 자격 증명을 만들기 전에 [마스터 키](../../t-sql/statements/create-master-key-transact-sql.md)를 만들어야 합니다.

## <a name="install-the-odbc-driver"></a>ODBC 드라이버 설치

먼저 각 PolyBase 노드에서 연결할 데이터 원본의 ODBC 드라이버를 다운로드하여 설치합니다. 드라이버가 제대로 설치되면 **ODBC 데이터 원본 관리자**에서 드라이버를 보고 테스트할 수 있습니다.

![PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

위의 예제에서 드라이버의 이름은 빨간색 원으로 되어 있습니다. 외부 데이터 원본을 만들 때 이 이름을 사용합니다.

> [!IMPORTANT]
> 쿼리 성능을 향상하기 위해 연결 풀링을 사용하도록 설정합니다. **ODBC 데이터 원본 관리자**에서 이를 수행할 수 있습니다.

## <a name="create-an-external-table"></a>외부 테이블 만들기

ODBC 데이터 원본의 데이터를 쿼리하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 외부 테이블을 만들기 위한 샘플 코드를 제공합니다.

이 섹션에서는 다음 Transact-SQL 명령이 사용됩니다.

* [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
* [CREATE STATISTICS(Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. ODBC 원본에 액세스하기 위한 데이터베이스 범위 자격 증명을 만듭니다.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL <credential_name> WITH IDENTITY = '<username>', Secret = '<password>';
    ```

    예를 들어 다음 예제에서는 ID `username`과 복잡한 암호를 사용하여 `credential_name`이라는 자격 증명을 만듭니다.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'BycA4ZjrE#*2W%!';
    ```

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다.

    ```sql
    CREATE EXTERNAL DATA SOURCE <external_data_source_name>
    WITH ( LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = [ON] | OFF,
    CREDENTIAL = <credential_name> );
    ```

    다음 예제에서는 외부 데이터 원본을 만듭니다.
    * 이름 `external_data_source_name`
    * ODBC `SERVERNAME` 및 포트 `4444`에 있음
    * `CData ODBC Driver For SAP 2015`와 연결 - [ODBC 드라이버를 설치](#install-the-odbc-driver)하는 동안 생성된 드라이버입니다.
    * `ServerNode` `sap_server_node`포트`5555`에
    * 서버로 푸시되는 처리를 위해 구성됨(`PUSHDOWN = ON`)
    * `credential_name` 자격 증명 사용

    ```sql
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = odbc://SERVERNAME:4444,
    CONNECTION_OPTIONS = 'Driver={CData ODBC Driver For SAP 2015};
    ServerNode = sap_server_node:5555',
    PUSHDOWN = ON,
    CREDENTIAL = credential_name );
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
