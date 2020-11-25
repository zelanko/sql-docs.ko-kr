---
description: sp_data_source_objects (Transact-sql)
title: sp_data_source_objects | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_data_source_objects
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d30a5190d88a0b3714f670f5f253c2a31e98f69e
ms.sourcegitcommit: 2e7154475ba1f31d1aeebc8f48ac05846f793736
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126601"
---
# <a name="sp_data_source_objects-transact-sql"></a>sp_data_source_objects (Transact-sql)

[!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

가상화 할 수 있는 테이블 개체의 목록을 반환 합니다.

> [!NOTE]
> 이 절차는 [SQL 2019 CU5](../../big-data-cluster/release-notes-big-data-cluster.md#cu5)에서 도입 되었습니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>구문  

```syntaxsql
sp_data_source_objects  
         [ @data_source = ] 'data_source'
     [ , [ @object_root_name = ] 'object_root_name' ]
     [ , [ @max_search_depth = ] max_search_depth ]
     [ , [ @search_options = ] 'search_options' ]
[ ; ]
```  
  
## <a name="arguments"></a>인수  

`[ @data_source = ] 'data_source'`   
메타 데이터를 가져올 외부 데이터 원본의 이름입니다. `@data_source`은 `sysname`입니다.  

`[ @object_root_name = ] 'object_root_name'`   
이 매개 변수는 검색할 개체의 이름에 대 한 루트입니다. `@object_root_name` 는 이며 `nvarchar(max)` 기본값은 `NULL` 입니다.

이 호출은에 대해 설정 된 값으로 시작 하는 외부 개체만 반환 `@object_root_name` 합니다.

ODBC 데이터 원본이 세 부분으로 된 이름을 사용 하는 RDBMS (관계형 데이터베이스 관리 시스템)에 연결 하는 경우에는에서 `@object_root_name` 부분 데이터베이스 이름을 포함할 수 없습니다. 이러한 경우 매개 변수는 `@object_root_name` 세 부분을 모두 포함 해야 하며 세 번째 부분은 검색할 개체 이름입니다.
> [!CAUTION]
> 외부 데이터 플랫폼 간의 차이로 인해의 기본값이 제공 되는 경우 일부 플랫폼은 결과를 반환 하지 않습니다 `NULL` . 일부 `NULL` 는 필터 부족으로 처리 됩니다. 예를 들어 `NULL` 에 대해가 제공 된 경우 ORACLE RMB는 결과를 반환 하지 않습니다 `@object_root_name` .

`[ @max_search_depth = ] max_search_depth`   
이 값은 검색 하려는의 최대 깊이 (부분)를 지정 합니다 `@object_root_name` . `@max_search_depth` 는 이며 `int` 기본값은 1입니다.

예를 들어 `@max_search_depth` `@object_root_name` SQL Server 데이터베이스의 이름인가 있는 1은 데이터베이스 내에 포함 된 schemata를 반환 합니다.

`@max_search_depth`의는 `NULL` `@object_root_name` 카탈로그 또는 스키마의 경우가 존재 하 고 비어 있지 않은 경우에 대 한 정보를 반환 합니다.

`[ @search_options = ] 'search_options'`   
`search_options`매개 변수는 nvarchar (max) 이며 기본값은입니다 `NULL` .

이 매개 변수는 사용 되지 않지만 나중에 구현할 수 있습니다.

## <a name="result-sets"></a>결과 집합

| 열 이름 | 데이터 형식 | Description |
|--|--|--|
| Object_Type | nvarchar(200) | 개체의 유형 (예: 테이블 또는 데이터베이스)입니다. |
| OBJECT_NAME | nvarchar(max) | 개체의 정규화 된 이름입니다. 백 엔드 특정 따옴표 문자를 사용 하 여 이스케이프 됩니다. |
| OBJECT_LEAF_NAME | nvarchar(max) | 정규화 되지 않은 개체 이름입니다. |
| TABLE_LOCATION | nvarchar(max) | CREATE EXTERNAL TABLE 문에 사용할 수 있는 유효한 테이블 위치 문자열입니다. `NULL`해당 되지 않을 경우입니다. |
  
## <a name="permissions"></a>사용 권한

ALTER ANY EXTERNAL DATA SOURCE 권한이 필요합니다.  

## <a name="remarks"></a>설명  

SQL Server 인스턴스에  [PolyBase](../../relational-databases/polybase/polybase-guide.md) 기능이 설치 되어 있어야 합니다.

이 저장 프로시저는 다음에 대 한 커넥터를 지원 합니다.

- SQL Server
- Oracle
- Teradata
- MongoDB
- CosmosDB

저장 프로시저는 일반 ODBC dta 원본 커넥터를 지원 하지 않습니다.

빈 vs와 비어 있지 않은 개념은 ODBC 드라이버 및 [ `SQLTables` 함수의](../native-client-odbc-api/sqltables.md)동작과 관련이 있습니다. 비어 있지 않음은 개체가 행이 아닌 테이블을 포함 하 고 있음을 나타냅니다. 예를 들어 빈 스키마에는 SQL Server의 테이블이 포함 되어 있지 않습니다. Teradata 안에 테이블이 없는 빈 데이터베이스에는가 포함 됩니다.

개체 유형은 외부 데이터 원본의 ODBC 드라이버에 의해 결정 됩니다. 각 외부 데이터 원본에서는 테이블로 한정 되는 항목을 결정 합니다. 여기에는 TeraData의 함수 같은 데이터베이스 개체 또는 Oracle의 동의어가 포함 될 수 있습니다. PolyBase는 일부 ODBC 개체에 외부 테이블로 연결할 수 없기 때문에 TABLE_LOCATION 열에 값이 없습니다. 이와 달리 이러한 개체 중 하나가 있으면 데이터베이스나 스키마를 비워 둘 수 없습니다.

`sp_data_source_objects`및 [`sp_data_source_table_columns`](sp-data-source-table-columns.md) 를 사용 하 여 외부 개체를 검색 합니다. 이러한 시스템 저장 프로시저는 가상화 할 수 있는 테이블의 스키마를 반환 합니다. Azure Data Studio은 이러한 두 저장 프로시저를 사용 하 여 [데이터 가상화](../../azure-data-studio/extensions/data-virtualization-extension.md)를 지원 합니다. [Sp_data_source_table_columns](sp-data-source-table-columns.md) 를 사용 하 여 SQL Server 데이터 형식으로 표현 되는 외부 테이블 스키마를 검색 합니다.

### <a name="data-source-type-specific-remarks"></a>데이터 원본 유형 관련 설명

* Teradata

   Teradata 시스템 뷰는 RLS (행 수준 보안)를 사용 하지 않으므로 사용자가 쿼리할 수 없는 테이블의 존재를 볼 수 있습니다.

* MongoDB

   일부 이전 버전의 MongoDB에서는 모든 데이터베이스를 관리자와 같은 사용자에 게 나열 하는 기능을 제한 합니다. 이 권한이 없는 사용자는 null로이 프로시저를 실행 하는 동안 인증 오류가 발생할 수 있습니다 `@object_root_name` .

## <a name="examples"></a>예  

### <a name="sql-server"></a>SQL Server

다음 예에서는 모든 데이터베이스, schemata 및 테이블/뷰를 반환 합니다.

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 3;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "database" | 데이터베이스 | NULL |
| SCHEMA | "데이터베이스". dbo | dbo | NULL |
| TABLE | "데이터베이스". dbo "." customer | 고객 | [데이터베이스]. [dbo]. customer |
| TABLE | "데이터베이스". dbo "." 항목만 | 항목 | [데이터베이스]. [dbo]. 항목만 |
| TABLE | "데이터베이스". dbo "." 파괴 | 파괴 | [데이터베이스]. [dbo]. 파괴 |

다음 예에서는 모든 데이터베이스를 반환 합니다.

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "UserDatabase" | UserDatabase | NULL |
| DATABASE | "master" | master | NULL |
| DATABASE | 데이터베이스가 | msdb | NULL |
| DATABASE | tempdb | tempdb | NULL |
| DATABASE | "database" | 데이터베이스 | NULL |

다음 예에서는 데이터베이스의 모든 schemata를 반환 합니다.

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[database]'; 
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| SCHEMA | "데이터베이스". dbo | dbo | NULL |
| SCHEMA | "데이터베이스". INFORMATION_SCHEMA " | INFORMATION_SCHEMA | NULL |
| SCHEMA | "데이터베이스". 시스템 | sys | NULL |

다음 예에서는 스키마의 모든 테이블을 반환 합니다. 

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[database].[dbo]'; 
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| TABLE | "데이터베이스". dbo "." customer | 고객 | [데이터베이스]. [dbo]. customer |
| TABLE | "데이터베이스". dbo "." 항목만 | 항목 | [데이터베이스]. [dbo]. 항목만 |
| TABLE | "데이터베이스". dbo "." 파괴 | 파괴 | [데이터베이스]. [dbo]. 파괴 |
| TABLE | "데이터베이스". dbo "." 주문과 | 주문 | [데이터베이스]. [dbo]. 주문과 |
| TABLE | "데이터베이스". dbo "." 속하지 | 구성 요소 | [데이터베이스]. [dbo]. 속하지 |

### <a name="oracle"></a>Oracle

다음 예에서는 전체 schemata 및 테이블, 함수, 뷰 및 등을 반환 합니다.

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[OracleObjectRoot]'; 
DECLARE @max_search_depth INT = 2; 
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| VIEW | "SYS". " ALL_SQLSET_STATEMENTS " | ALL_SQLSET_STATEMENTS | [ORACLEOBJECTROOT]. [SYS]. [ALL_SQLSET_STATEMENTS] |
| SYSTEM TABLE | "SYS". " 부트스트랩 $ " | 부트스트랩 $ | [ORACLEOBJECTROOT]. [SYS]. [부트스트랩 $] |
| SYNONYM | "PUBLIC". " ALL_ALL_TABLES " | ALL_ALL_TABLES | NULL |
| SCHEMA | "database" | 데이터베이스 | NULL |
| TABLE | "데이터베이스". customer | 고객 | [ORACLEOBJECTROOT]. [데이터베이스]. customer |

### <a name="teradata"></a>Teradata

다음 예에서는 모든 데이터베이스와 테이블, 함수, 뷰 등을 반환 합니다.

```SQL
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 2;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |  
|--|--|--|--|
| FUNCTION | "SYSLIB"." ExtractRoles " | ExtractRoles | NULL |  
| SYSTEM TABLE | "DBC". " UDTCast" | UDTCast | [DBC]. [UDTCast] |  
| TYPE | "SYSUDTLIB". " XML | XML | NULL |  
| DATABASE | "database" | 데이터베이스 | NULL |
| TABLE | "데이터베이스". customer | 고객 | [데이터베이스]. customer |  

### <a name="mongo-db"></a>MongoDB

다음 예에서는 모든 데이터베이스와 테이블을 반환 합니다.

```SQL
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 2;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| Object_Type | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "database" | 데이터베이스 | NULL |
| TABLE | "데이터베이스". customer | 고객 | [데이터베이스]. customer |
| TABLE | "데이터베이스". 항목만 | 항목 | [데이터베이스]. 항목만 |
| TABLE | "데이터베이스". 파괴 | 파괴 | [데이터베이스]. 파괴 |
| TABLE | "데이터베이스". 주문과 | 주문 | [데이터베이스]. 주문과 |

## <a name="see-also"></a>참고 항목

- [sp_data_source_columns](/sql/relational-databases/system-stored-procedures/sp-data-source-table-columns)   
- [CREATE EXTERNAL TABLE AS SELECT(Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)
- [CREATE EXTERNAL TABLE(Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)
- [Azure Data Studio용 데이터 가상화 확장](../../azure-data-studio/extensions/data-virtualization-extension.md)   
- [PolyBase 시작하기](../polybase/polybase-guide.md)   
- [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
