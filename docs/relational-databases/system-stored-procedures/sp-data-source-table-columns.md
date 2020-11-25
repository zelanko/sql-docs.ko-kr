---
description: sp_data_source_table_columns (Transact-sql)
title: sp_data_source_table_columns | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_data_source_table_columns
helpviewer_keywords:
- PolyBase
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4153b7546dfce226cb056b7a548efb69f5175e06
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2020
ms.locfileid: "96128769"
---
# <a name="sp_data_source_table_columns-transact-sql"></a>sp_data_source_table_columns (Transact-sql)

[!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

외부 데이터 원본 테이블의 열 목록을 반환 합니다.
  
> [!NOTE]
> 이 절차는 [SQL 2019 CU5](../../big-data-cluster/release-notes-big-data-cluster.md#cu5)에서 도입 되었습니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sqlsyntax
sp_data_source_table_columns
         [ @data_source = ] 'data_source'
       , [ @table_location = ] 'table_location'
[ ; ]
```  

## <a name="arguments"></a>인수

`[ @data_source = ] 'data_source'`   
메타 데이터를 가져올 외부 데이터 원본의 이름입니다. 유형입니다 `sysname` .

`[ @table_location = ] 'table_location'`   
테이블을 식별 하는 테이블 위치 문자열입니다. `table_location` 유형입니다 `nvarchar(max)` .

## <a name="returns"></a>반환

저장 프로시저는 다음 정보를 반환 합니다.

|열 이름 |데이터 형식 |Description|
|---|---|---|
|NAME|nvarchar(max)|열 이름입니다.
|TYPE|nvarchar(200)|SQL Server 형식 이름
|LENGTH|int|열의 길이
|PRECISION|int|열의 전체 자릿수
|SCALE|int|열 크기 조정
|COLLATION|nvarchar(200)|열의 데이터 정렬 SQL Server
|IS_NULLABLE|bit|이 열이 null을 허용 합니다.
|SOURCE_TYPE_NAME|nvarchar(max)|백 엔드 특정 형식 이름입니다. 주로 디버깅에 사용 됩니다. ODBC 원본의 경우 SQLColumns ()의 TYPE_NAME 결과 열에 해당 합니다.
|REMARKS|nvarchar(max)|열에 대 한 일반 설명 또는 설명입니다. 현재는 항상 NULL입니다.|

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

빈 vs와 비어 있지 않은 개념은 ODBC 드라이버 및 [ `SQLTables` 함수의](../native-client-odbc-api/sqltables.md)동작과 관련이 있습니다. 비어 있지 않음은 개체가 행이 아닌 테이블을 포함 하 고 있음을 나타냅니다. 예를 들어 빈 스키마에는 SQL Server의 테이블이 포함 되어 있지 않습니다. Teradata에 테이블이 없는 빈 데이터베이스에는가 포함 되어 있습니다. 결과는 백 엔드에 대 한 PolyBase 커넥터에서 해석 되는 백엔드 스키마의 SQL Server 표현입니다. 여기서의 차이점은 ODBC 호출 결과를 백 엔드에 전달 하는 것이 아니라 PolyBase 형식 매핑 코드의 결과를 기반으로 한다는 것입니다.

[`sp_data_source_objects`](sp-data-source-objects.md)및 `sp_data_source_table_columns` 를 사용 하 여 외부 개체를 검색 합니다. 이러한 시스템 저장 프로시저는 가상화 할 수 있는 테이블의 스키마를 반환 합니다. Azure Data Studio은 이러한 두 저장 프로시저를 사용 하 여 [데이터 가상화](../../azure-data-studio/extensions/data-virtualization-extension.md)를 지원 합니다. `sp_data_source_table_columns`를 사용 하 여 SQL Server 데이터 형식으로 표현 되는 외부 테이블 스키마를 검색 합니다.

Hadoop 원본 데이터의 데이터 정렬과 SQL Server 2019에서 지원 되는 데이터 정렬 간의 차이 때문에 외부 테이블의 varchar 데이터 형식 열에 권장 되는 데이터 형식 길이가 예상 보다 훨씬 클 수 있습니다. 이것은 의도적인 것입니다.

## <a name="example"></a>예제  

다음 예에서는 라는 스키마에 속하는 이라는 SQL Server의 외부 테이블에 대 한 테이블 열을 반환 합니다 `server` `schema` .
  
```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @table_location NVARCHAR(400) = N'[database].[schema].[table]';
EXEC sp_data_source_table_columns @data_source, @table_location
```  
  
## <a name="see-also"></a>참고 항목

- [PolyBase 시작하기](../polybase/polybase-guide.md)
- [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
- [CREATE EXTERNAL TABLE AS SELECT(Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)
- [CREATE EXTERNAL TABLE(Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)