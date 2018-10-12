---
title: Oracle의 외부 데이터에 액세스하도록 PolyBase 구성 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 2b6fc4d849a964aa2a3f761e5d566e78f130d4a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748041"
---
# <a name="configure-polybase-to-access-external-data-in-oracle"></a>Oracle의 외부 데이터에 액세스하도록 PolyBase 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 인스턴스에서 PolyBase를 사용하여 Oracle에서 외부 데이터를 쿼리하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

PolyBase를 설치하지 않은 경우 [PolyBase 설치](polybase-installation.md)를 참조하세요. 설치 문서에서는 필수 구성 요소를 설명합니다.

## <a name="configure-an-external-table"></a>외부 테이블 구성

Oracle 데이터 원본의 데이터를 쿼리하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다. 
 
최적의 쿼리 성능을 위해서는 특히 조인, 필터 및 집계에 사용되는 외부 테이블 열에 대해 통계를 만드는 것이 좋습니다.

이 섹션에서는 다음 개체를 만듭니다.

- CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL) 
- CREATE EXTERNAL DATA SOURCE(Transact-SQL) 
- CREATE EXTERNAL FILE FORMAT(Transact-SQL) 
- CREATE EXTERNAL TABLE(Transact-SQL) 
- CREATE STATISTICS(Transact-SQL)


1. 데이터베이스에 마스터 키를 만듭니다. 이 키는 자격 증명 비밀을 암호화하는 데 필요합니다.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
     ```

1. 데이터베이스 범위 자격 증명을 만듭니다.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
      CREATE DATABASE SCOPED CREDENTIAL OracleCredentials 
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다. Oracle 데이터 원본의 외부 데이터 원본 위치 및 자격 증명을 지정합니다.

     ```sql
     /*  LOCATION: Server DNS name or IP address.
      *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
     *  CREDENTIAL: the database scoped credential, created above.
     */  
     CREATE EXTERNAL DATA SOURCE OracleInstance
     WITH ( 
     LOCATION = '<vendor>://<server>[:<port>]',
     -- PUSHDOWN = ON | OFF,
      CREDENTIAL = OracleCredentials
     );
     ```

1. 외부 데이터에 대한 스키마 만들기
 
     ```sql
     CREATE SCHEMA oracle;
     GO
     ```

1.  외부 Oracle 시스템에 저장된 데이터를 나타내는 외부 테이블을 만듭니다. [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)
 
      ```sql
      /*  LOCATION: Oracle table/view in '<database_name>.<schema_name>.<object_name>' format
     *  DATA_SOURCE: the external data source, created above.
     */
      CREATE EXTERNAL TABLE oracle.orders(
      [O_ORDERKEY] DECIMAL(38) NOT NULL,
     [O_CUSTKEY] DECIMAL(38) NOT NULL,
     [O_ORDERSTATUS] CHAR COLLATE Latin1_General_BIN NOT NULL,
     [O_TOTALPRICE] DECIMAL(15,2) NOT NULL,
     [O_ORDERDATE] DATETIME2(0) NOT NULL,
     [O_ORDERPRIORITY] CHAR(15) COLLATE Latin1_General_BIN NOT NULL,
     [O_CLERK] CHAR(15) COLLATE Latin1_General_BIN NOT NULL,
     [O_SHIPPRIORITY] DECIMAL(38) NOT NULL,
     [O_COMMENT] VARCHAR(79) COLLATE Latin1_General_BIN NOT NULL
     )
     WITH (
      LOCATION='TPCH..ORDERS',
      DATA_SOURCE=OracleInstance
     );
     ```

1. 최적화된 성능을 위해 외부 테이블에 대해 통계를 만듭니다.

     ```sql
      CREATE STATISTICS OrdersOrderKeyStatistics ON oracle.orders(O_ORDERKEY) WITH FULLSCAN;
     ```

## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [SQL Server PolyBase 개요](polybase-guide.md)를 참조하세요.
