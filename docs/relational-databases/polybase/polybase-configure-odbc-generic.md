---
title: ODBC 제네릭 형식의 외부 데이터를 액세스하도록 PolyBase 구성 | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 3cb5efcb4c4abdc29aa71bf4a5e59ebe039d8a9e
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072848"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>SQL Server의 외부 데이터에 액세스하도록 PolyBase 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2019의 PolyBase를 사용하면 ODBC 커넥터를 통해 ODBC 호환 데이터 원본에 연결할 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항

참고 = 이 기능은 Windows의 SQL Server에서만 작동합니다. 

PolyBase를 설치하지 않은 경우 [PolyBase 설치](polybase-installation.md)를 참조하세요.

먼저 각 PolyBase 노드에서 연결할 데이터 원본의 ODBC 드라이버를 다운로드하여 설치합니다. 드라이버가 제대로 설치되면 "ODBC 데이터 원본 관리자"에서 드라이버를 보고 테스트할 수 있습니다.

![PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

> **중요!**
> 
> 쿼리 성능을 향상시키려면 드라이버에서 연결 풀링을 사용할 수 있도록 설정해야 합니다. "ODBC 데이터 원본 관리자"에서 이를 수행할 수 있습니다.
> 
> **참고**
> 
> 외부 데이터 원본을 생성할 때 드라이버 이름(예: 원으로 표시)을 지정해야 합니다(아래 3단계).

## <a name="create-an-external-table"></a>외부 테이블 만들기

ODBC 데이터 원본의 데이터를 쿼리하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 외부 테이블을 만들기 위한 샘플 코드를 제공합니다.

이 섹션에서 이들 개체를 만듭니다.

- CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL) 
- CREATE EXTERNAL DATA SOURCE(Transact-SQL) 
- CREATE EXTERNAL TABLE(Transact-SQL) 
- CREATE STATISTICS(Transact-SQL)

1. 데이터베이스에 마스터 키가 없는 경우 하나 만듭니다. 이 키는 자격 증명 비밀을 암호화하는 데 필요합니다.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>인수
    PASSWORD ='password'

    데이터베이스의 마스터 키를 암호화하는 데 사용되는 암호입니다. password는 SQL Server의 인스턴스를 호스팅하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다.

1. ODBC 데이터 원본에 액세스하기 위한 데이터베이스 범위 자격 증명을 만듭니다.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다.

     ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( 
    LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = credential_name
    );

     ```


1.  [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)을 사용하여 외부 데이터 원본의 데이터를 나타내는 외부 테이블을 만듭니다.
 
     ```sql
     /*  LOCATION: ODBC data source table/view
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE customer(
     C_CUSTKEY INT NOT NULL,
     C_NAME VARCHAR(25) NOT NULL,
     C_ADDRESS VARCHAR(40) NOT NULL,
     C_NATIONKEY INT NOT NULL,
     C_PHONE CHAR(15) NOT NULL,
     C_ACCTBAL DECIMAL(15,2) NOT NULL,
     C_MKTSEGMENT CHAR(10) NOT NULL,
     C_COMMENT VARCHAR(117) NOT NULL
      )
      WITH (
      LOCATION='customer',
      DATA_SOURCE= external_data_source_name
     );
      ```

1. **선택 사항:** 외부 테이블에 대한 통계를 만듭니다.

    최적의 쿼리 성능을 위해서는 특히 조인, 필터 및 집계에 사용되는 외부 테이블 열에 대해 통계를 만드는 것이 좋습니다.

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [SQL Server PolyBase 개요](polybase-guide.md)를 참조하세요.
