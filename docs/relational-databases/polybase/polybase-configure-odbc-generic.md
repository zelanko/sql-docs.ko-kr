---
title: '외부 데이터 액세스: ODBC 제네릭 형식 - PolyBase'
description: SQL Server의 PolyBase를 사용하면 ODBC 커넥터를 통해 호환 데이터 원본에 연결할 수 있습니다. ODBC 드라이버를 설치하고 외부 테이블을 만듭니다.
ms.date: 07/16/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15'
ms.openlocfilehash: ac4fa22e2d0aea57f25aaa9ef2d8c570f8bb130b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475934"
---
# <a name="configure-polybase-to-access-external-data-with-odbc-generic-types"></a>ODBC 제네릭 형식의 외부 데이터를 액세스하도록 PolyBase 구성

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2019의 PolyBase를 사용하면 ODBC 커넥터를 통해 ODBC 호환 데이터 원본에 연결할 수 있습니다.

이 문서에서는 ODBC 데이터 원본을 사용하여 연결 구성을 만드는 방법을 보여 줍니다. 제공된 지침에서는 하나의 특정 ODBC 드라이버를 예로 사용합니다. 해당 ODBC 공급자의 구체적인 예제를 확인하세요. 적절한 연결 문자열 옵션을 결정하려면 데이터 원본에 대한 ODBC 드라이버 설명서를 참조하세요. 이 문서의 예제는 특정 ODBC 드라이버에는 적용되지 않을 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

>[!NOTE]
>이 기능을 사용하려면 Windows에서 SQL Server가 필요합니다.

* SQL Server 인스턴스 [PolyBase 설치](polybase-installation.md)에 대해 PolyBase가 설치되고 사용하도록 설정되어 있어야 합니다.

* 데이터베이스 범위 자격 증명을 만들기 전에 [마스터 키](../../t-sql/statements/create-master-key-transact-sql.md)를 만들어야 합니다.

## <a name="install-the-odbc-driver"></a>ODBC 드라이버 설치

각 PolyBase 노드에서 연결할 데이터 원본의 ODBC 드라이버를 다운로드하여 설치합니다. 드라이버가 제대로 설치되면 **ODBC 데이터 원본 관리자** 에서 드라이버를 보고 테스트할 수 있습니다.

![PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

위의 예제에서 드라이버의 이름은 빨간색 원으로 되어 있습니다. 외부 데이터 원본을 만들 때 이 이름을 사용합니다.

> [!IMPORTANT]
> 쿼리 성능을 향상하기 위해 연결 풀링을 사용하도록 설정합니다. **ODBC 데이터 원본 관리자** 에서 이를 수행할 수 있습니다.

## <a name="create-dependent-objects-in-sql-server"></a>SQL Server에서 종속 개체 만들기

ODBC 데이터 원본을 사용하려면 먼저 몇 가지 개체를 만들어 구성을 완료해야 합니다.

이 섹션에서는 다음 Transact-SQL 명령이 사용됩니다.

* [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 

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
    WITH ( LOCATION = 'odbc://<ODBC server address>[:<port>]',
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
    WITH ( LOCATION = 'odbc://SERVERNAME:4444',
    CONNECTION_OPTIONS = 'Driver={CData ODBC Driver For SAP 2015};
    ServerNode = sap_server_node:5555',
    PUSHDOWN = ON,
    CREDENTIAL = credential_name );
    ```
    
## <a name="create-an-external-table"></a>외부 테이블 만들기

종속 개체를 만든 후에는 T-SQL을 사용하여 외부 테이블을 만들 수 있습니다. 

이 섹션에서는 다음 Transact-SQL 명령이 사용됩니다.
* [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)
* [CREATE STATISTICS(Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. 하나 이상의 외부 테이블을 만듭니다.

   외부 테이블을 만듭니다. `DATA_SOURCE` 인수를 사용하여 위에서 만든 외부 데이터 원본을 참조하고 원본 테이블을 `LOCATION`으로 지정해야 합니다. 모든 열을 참조할 필요는 없지만 형식이 올바르게 매핑되었는지 확인해야 합니다.  

   ```sql
     CREATE EXTERNAL TABLE <your_table_name>
     (
     <col1_name>     DECIMAL(38) NOT NULL,
     <col2_name>     DECIMAL(38) NOT NULL,
     <col3_name>     CHAR COLLATE Latin1_General_BIN NOT NULL
     )
     WITH (
     LOCATION='<sap_table_name>',
     DATA_SOURCE= <external_data_source_name>
     )
     ;
   ```

   > [!NOTE]
   > 이 외부 데이터 원본을 사용하여 모든 외부 테이블에 대한 종속 개체를 재사용할 수 있습니다.

1. **선택 사항:** 외부 테이블에 대한 통계를 만듭니다.

    최적의 쿼리 성능을 위해서는 특히 조인, 필터 및 집계에 사용되는 외부 테이블 열에 대해 통계를 만드는 것이 좋습니다.

    ```sql
    CREATE STATISTICS statistics_name ON contact (FirstName) WITH FULLSCAN; 
    ```
    
## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [SQL Server PolyBase 개요](polybase-guide.md)를 참조하세요.
