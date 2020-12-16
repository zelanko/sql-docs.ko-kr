---
description: CREATE TABLE(Azure Synapse Analytics)
title: CREATE TABLE(Azure Synapse Analytics) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ea21c73c-40e8-4c54-83d4-46ca36b2cf73
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: fdadefa5b898a2b37c7e5a7f087c429ccc6b8d4f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438966"
---
# <a name="create-table-azure-synapse-analytics"></a>CREATE TABLE(Azure Synapse Analytics)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 새 테이블을 만듭니다.  

테이블 및 테이블 사용 방법을 알아보려면 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]의 테이블](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-overview/)을 참조하세요.

> [!NOTE]
>  다른 설명이 없는 한, 이 문서의 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 관련 내용은 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 모두 적용됩니다.

 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

<a name="Syntax"></a>

## <a name="syntax"></a>구문
  
```syntaxsql
-- Create a new table.
CREATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]
    )  
    [ WITH ( <table_option> [ ,...n ] ) ]  
[;]  

<column_options> ::=
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ] -- default is NULL  
    [ <column_constraint> ]

<column_constraint>::=
    {
        DEFAULT DEFAULT constant_expression
        | PRIMARY KEY NONCLUSTERED  NOT ENFORCED -- Applies to Azure Synapse Analytics only
        | UNIQUE NOT ENFORCED -- Applies to Azure Synapse Analytics only
    }

<table_option> ::=
    {
       CLUSTERED COLUMNSTORE INDEX --default for Azure Synapse Analytics 
      | CLUSTERED COLUMNSTORE INDEX ORDER (column [,...n])  
      | HEAP --default for Parallel Data Warehouse
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) -- default is ASC
    }  
    {
        DISTRIBUTION = HASH ( distribution_column_name )
      | DISTRIBUTION = ROUND_ROBIN -- default for Azure Synapse Analytics
      | DISTRIBUTION = REPLICATE -- default for Parallel Data Warehouse
    }
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] -- default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) )

<data type> ::=
      datetimeoffset [ ( n ) ]  
    | datetime2 [ ( n ) ]  
    | datetime  
    | smalldatetime  
    | date  
    | time [ ( n ) ]  
    | float [ ( n ) ]  
    | real [ ( n ) ]  
    | decimal [ ( precision [ , scale ] ) ]   
    | numeric [ ( precision [ , scale ] ) ]   
    | money  
    | smallmoney  
    | bigint  
    | int   
    | smallint  
    | tinyint  
    | bit  
    | nvarchar [ ( n | max ) ]  -- max applies only to Azure Synapse Analytics 
    | nchar [ ( n ) ]  
    | varchar [ ( n | max )  ] -- max applies only to Azure Synapse Analytics  
    | char [ ( n ) ]  
    | varbinary [ ( n | max ) ] -- max applies only to Azure Synapse Analytics  
    | binary [ ( n ) ]  
    | uniqueidentifier  
```  

<a name="Arguments"></a>
## <a name="arguments"></a>인수

 *database_name*  
 새 테이블을 포함할 데이터베이스의 이름입니다. 기본값은 현재 데이터베이스입니다.  
  
 *schema_name*  
 테이블의 스키마입니다. *schema* 지정은 선택 사항입니다. 공백이면 기본 스키마가 사용됩니다.  
  
 *table_name*  
 새 테이블의 이름입니다. 로컬 임시 테이블을 만들려면 테이블 이름 앞에 #을 붙입니다.  임시 테이블에 대한 설명 및 지침은 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]의 임시 테이블](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-temporary/)을 참조하세요. 

 *column_name*  
 테이블 열의 이름입니다.

### <a name="column-options"></a><a name="ColumnOptions"></a> 열 옵션

 `COLLATE` *Windows_collation_name*  
 식에 대한 데이터 정렬을 지정합니다. 데이터 정렬은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원하는 Windows 데이터 정렬 중 하나여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 Windows 데이터 정렬 목록의 경우 [Windows 데이터 정렬 이름(Transact-SQL)](windows-collation-name-transact-sql.md)을 참조하세요.  
  
 `NULL` | `NOT NULL`  
 열에서 `NULL` 값이 허용되는지 여부를 지정합니다. 기본값은 `NULL`입니다.  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 기본 열 값을 지정합니다.  
  
 | 인수 | 설명 |
 | -------- | ----------- |
 | *constraint_name* | 제약 조건에 대한 선택적 이름입니다. 제약 조건 이름은 데이터베이스 내에서 고유합니다. 이름은 다른 데이터베이스에서 다시 사용할 수 있습니다. |
 | *constant_expression* | 열의 기본값입니다. 식은 리터럴 값이거나 상수여야 합니다. 예를 들어 `'CA'`, `4`와 같은 상수 식이 허용됩니다. `2+3`, `CURRENT_TIMESTAMP`와 같은 상수 식은 허용되지 않습니다. |
  
### <a name="table-structure-options"></a><a name="TableOptions"></a> 테이블 구조 옵션

테이블 형식 선택 방법에 대한 지침은 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 테이블 인덱싱](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-index/)을 참조하세요.
  
 `CLUSTERED COLUMNSTORE INDEX` 
 
테이블을 클러스터형 columnstore 인덱스로 저장합니다. 클러스터형 columnstore 인덱스는 모든 테이블 데이터에 적용됩니다. 이 동작은 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 기본값입니다.
 
 `HEAP`은 테이블을 힙으로 저장합니다. 이 동작은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 기본값입니다.  
  
 `CLUSTERED INDEX` ( *index_column_name* [ ,...*n* ] )  
 하나 이상의 키 열과 함께 클러스터형 인덱스로 테이블을 저장합니다. 이 동작은 데이터를 행별로 저장합니다. *index_column_name* 을 사용하여 인덱스에 하나 이상의 키 열 이름을 지정할 수 있습니다.  자세한 내용은 일반 설명의 Rowstore 테이블을 참조하세요.
 
 `LOCATION = USER_DB` 이 옵션은 더 이상 사용되지 않습니다. 구문적으로는 수락되지만 더 이상 필요하지 않으며 동작에 영향을 주지 않습니다.   
  
### <a name="table-distribution-options"></a><a name="TableDistributionOptions"></a> 테이블 배포 옵션

최적의 배포 방법을 선택하고 분산 테이블을 사용하는 방법을 알아보려면 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 테이블 배포](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-distribute/)를 참조하세요.

`DISTRIBUTION = HASH`( *distribution_column_name* ) *distribution_column_name* 에 저장된 값을 해시하여 각 행을 하나의 배포에 할당합니다. 알고리즘은 결정적입니다. 즉, 항상 동일한 값을 동일한 배포에 해시한다는 뜻입니다.  NULL이 있는 모든 행은 동일한 분산에 할당되므로 배포 열은 NOT NULL로 정의되어야 합니다.

`DISTRIBUTION = ROUND_ROBIN`은 행을 라운드 로빈 방식으로 모든 분산에서 동일하게 배포합니다. 이 동작은 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 기본값입니다.

`DISTRIBUTION = REPLICATE`은 각 컴퓨팅 노드에 테이블의 복사본 하나를 저장합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 경우 테이블은 각 컴퓨팅 노드에 있는 배포 데이터베이스에 저장됩니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 경우 테이블은 컴퓨팅 노드에 걸쳐 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일 그룹에 저장됩니다 이 동작은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 기본값입니다.
  
### <a name="table-partition-options"></a><a name="TablePartitionOptions"></a> 테이블 파티션 옵션
테이블 파티션 사용 방법에 대한 지침은 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 테이블 분할](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/)을 참조하세요.

 `PARTITION` ( *partition_column_name* `RANGE` [ `LEFT` | `RIGHT` ] `FOR VALUES` ( [ *boundary_value* [,...*n*] ] ))   
하나 이상의 테이블 파티션을 만듭니다. 이 파티션은 힙, 클러스터형 인덱스 또는 클러스터형 columnstore 인덱스에 테이블을 저장하는지 여부에 관계 없이 행의 하위 집합에 작업을 적용할 수 있도록 하는 가로 테이블 조각입니다. 배포 열과 달리 테이블 파티션은 각 행이 저장된 배포를 결정하지 않습니다. 대신, 테이블 파티션은 행이 그룹화되고 각 배포 내에 저장되는 방식을 결정합니다.  

| 인수 | 설명 |
| -------- | ----------- |
|*partition_column_name*| [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]가 행을 분할하는 데 사용하는 열을 지정합니다. 이 열은 모든 데이터 형식일 수 있습니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 파티션 열 값을 오름차순으로 정렬합니다. 낮음-높은 순서는 `LEFT` 지정의 `RIGHT`에서 `RANGE`로 진행됩니다. |  
| `RANGE LEFT` | 왼쪽(낮은 값)에서 파티션에 속하는 경계 값을 지정합니다. 기본값은 LEFT입니다. |
| `RANGE RIGHT` | 오른쪽(높은 값)에서 파티션에 속하는 경계 값을 지정합니다. | 
| `FOR VALUES` ( *boundary_value* [,...*n*] ) | 파티션에 대한 경계 값을 지정합니다. *boundary_value* 는 상수 식입니다. NULL일 수 없습니다. *partition_column_name* 의 데이터 형식과 일치하거나 암시적으로 변환할 수 있어야 합니다. 암시적으로 변환하는 동안에는 자를 수 없습니다. 그러면 값의 크기와 배율이 *partition_column_name* 의 데이터 형식과 일치하지 않습니다.<br></br><br></br>`PARTITION` 절은 지정하되 경계 값을 지정하지 않으면 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 하나의 파티션으로 분할된 테이블을 만듭니다. 해당하는 경우 나중에 두 개의 파티션으로 테이블을 분할할 수 있습니다.<br></br><br></br>하나의 경계 값을 지정한 경우 결과 테이블은 경계 값보다 낮은 값에 대한 파티션 하나와 경계 값보다 높은 값에 대한 파티션 하나 이렇게 두 개의 파티션을 갖습니다. 분할되지 않은 테이블에 파티션을 이동하는 경우 분할되지 않은 테이블은 데이터를 받되 해당 메타데이터의 파티션 경계는 없습니다.| 

 예제 섹션의 [분할된 테이블 만들기](#PartitionedTable)를 참조하세요.

### <a name="ordered-clustered-columnstore-index-option"></a>순서가 지정된 클러스터형 columnstore 인덱스 옵션 

CCI(클러스터형 columnstore 인덱스)는 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 테이블을 만들기 위한 기본값입니다.  CCI의 데이터는 columnstore 세그먼트로 압축되기 전에 정렬되지 않습니다.  ORDER를 사용하여 CCI를 만드는 경우, 데이터가 인덱스 세그먼트에 추가되기 전에 정렬되며, 쿼리 성능이 향상될 수 있습니다. 자세한 내용은 [순서가 지정된 클러스터형 Columnstore 인덱스를 사용한 성능 튜닝](/azure/sql-data-warehouse/performance-tuning-ordered-cci?view=azure-sqldw-latest)을 참조하세요.  

문자열 열을 제외하고 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 지원되는 모든 데이터 형식의 열에 순서가 지정된 CCI를 만들 수 있습니다.  

사용자는 **sys.index_columns** 의 **column_store_order_ordinal** 열에서 테이블이 정렬되고 정렬에 순서가 있는 열을 쿼리할 수 있습니다.  

자세한 내용은 [순서가 지정된 클러스터형 columnstore 인덱스를 사용한 성능 튜닝](/azure/sql-data-warehouse/performance-tuning-ordered-cci)을 참조하세요.   

### <a name="data-type"></a><a name="DataTypes"></a> 데이터 형식

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 가장 일반적으로 사용되는 데이터 형식을 지원합니다. 다음은 세부 정보 및 스토리지 바이트가 포함된 지원되는 데이터 형식의 목록입니다. 데이터 형식 및 데이터 형식 사용 방법을 자세히 알아보려면 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]의 테이블 데이터 형식](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-data-types)을 참조하세요.

데이터 형식 변환의 테이블의 경우 [CAST 및 CONVERT(Transact-SQL)](../functions/cast-and-convert-transact-sql.md)에 있는 암시적 변환 섹션을 참조하세요.

>[!NOTE]
>자세한 내용은 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../functions/date-and-time-data-types-and-functions-transact-sql.md)를 참조하세요.

`datetimeoffset` [ ( *n* ) ]  
 *n* 의 기본값은 7입니다.  
  
 `datetime2` [ ( *n* ) ]  
소수 자릿수 초 숫자를 지정할 수 있다는 점 외에는 `datetime`과 동일합니다. *n* 의 기본값은 `7`입니다.  
  
|*n* 값|자릿수|확장|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
|`7`|27|7|  
  
 `datetime`  
 그레고리력에 따라 19-23자로 하루의 시간과 날짜를 저장합니다. 날짜는 연도, 월 및 일을 포함할 수 있습니다. 시간에는 시간, 분, 초를 포함합니다. 선택적으로 세 자리 소수 자릿수 초를 표시할 수 있습니다. 스토리지 크기는 8바이트입니다.  
  
 `smalldatetime`  
 날짜 및 시간을 저장합니다. 스토리지 크기는 4바이트입니다.  
  
 `date`  
 그레고리력에 따라 연도, 월 및 일에 대해 최대 10자를 사용하여 날짜를 저장합니다. 스토리지 크기는 3바이트입니다. 날짜는 정수로 저장됩니다.  
  
 `time` [ ( *n* ) ]  
 *n* 의 기본값은 `7`입니다.  
  
 `float` [ ( *n* ) ]  
 부동 소수점 숫자 데이터에 사용하는 근사 숫자 데이터 형식입니다. 부동 소수점 데이터는 근사값이므로 해당 데이터 형식 범위에 있는 모든 값을 정확하게 표현할 수는 없습니다. *n* 은 과학적 표기법으로 `float`의 가수를 저장하는 데 사용되는 비트 수를 지정합니다. *n* 은 전체 자릿수 및 스토리지 크기를 결정합니다. *n* 이 지정된 경우 그 값은 `1`에서 `53` 사이여야 합니다. *n* 의 기본값은 `53`입니다.  
  
| *n* 값 | 자릿수 | 스토리지 크기 |  
| --------: | --------: | -----------: |  
| 1-24   | 7자리  | 4바이트      |  
| 25-53  | 15자리 | 8바이트      |  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서는 *n* 을 가능한 두 값 중 하나로 처리합니다. `1`<= *n* <= `24`이면 *n* 은 `24`으로 처리됩니다. `25` <= *n* <= `53`이면 *n* 은 `53`으로 처리됩니다.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] `float` 데이터 형식은 *부터* 까지의 모든 `1`n`53` 값에 대해 ISO 표준을 준수합니다. 배정밀도의 동의어는 `float(53)`입니다.  
  
 `real` [ ( *n* ) ]  
 실제 정의는 float와 같습니다. `real`의 ISO 동의어는 `float(24)`입니다.  
  
 `decimal` [ ( *precision* [ *, scale* ] ) ] | `numeric` [ ( *precision* [ *, scale* ] ) ]  
 고정 전체 자릿수 및 비율 숫자를 저장합니다.  
  
 *전체 자릿수*  
 소수점 왼쪽과 오른쪽에 저장할 수 있는 10진수의 최대 총 수입니다. 전체 자릿수 값은 `1`에서 최대 전체 자릿수인 `38` 사이여야 합니다. 기본 전체 자릿수는 `18`입니다.  
  
 *scale*  
 소수점 오른쪽에 저장할 수 있는 10진수의 최대 수입니다. *Scale* 값은 `0`에서 *precision* 사이여야 합니다. *precision* 이 지정된 경우 *scale* 만 지정할 수 있습니다 기본 비율은 `0`이므로 `0` <= *scale* <= *precision* 입니다. 전체 자릿수에 따라 최대 스토리지 크기가 달라집니다.  
  
| 자릿수 | 스토리지 크기(바이트)  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10-19      |             9 |  
| 20-28      |            13 |  
| 29-38      |            17 |  
  
 `money` | `smallmoney`  
 통화 값을 나타내는 데이터 형식입니다.  
  
| 데이터 형식 | 스토리지 크기(바이트) |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` \| `int` \| `smallint` \| `tinyint`  
 정수 데이터를 사용하는 정확한 숫자 데이터 형식입니다. 다음 표에 스토리지 용량이 나와 있습니다.  
  
| 데이터 형식 | 스토리지 크기(바이트) |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1|  
  
 `bit`  
 `1`, `0` 또는 NULL 값을 가질 수 있는 정수 데이터 형식입니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서는 bit 열의 스토리지를 최적화합니다. 테이블에 8개 이하의 bit 열이 있는 경우 열은 1바이트로 저장되고, 9-16개의 bit 열이 있을 경우 2바이트로 저장되는 식입니다.  
  
 `nvarchar` [ ( *n* | `max` ) ]  -- `max`는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에만 적용됩니다.  
 가변 길이 유니코드 문자 데이터입니다. *n* 은 1부터 4000 사이의 값이 될 수 있습니다. `max`는 최대 스토리지 크기가 2^31-1바이트(2GB)임을 나타냅니다. 스토리지 크기(바이트)는 입력된 문자 수의 두 배 + 2바이트입니다. 입력된 데이터의 길이가 0자일수도 있습니다.  
  
 `nchar` [ ( *n* ) ]  
 길이가 *n* 자인 고정 길이의 유니코드 문자 데이터입니다. *n* 은 `1`과 `4000` 사이의 값이어야 합니다. 스토리지 크기는 *n* 바이트의 두 배입니다.  
  
 `varchar` [ ( *n*  | `max` ) ]  -- `max`는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에만 적용됩니다.   
 길이가 *n* 바이트인 가변 길이의 비 유니코드 문자 데이터입니다. *n* 은 `1`과 `8000` 사이의 값이어야 합니다. `max`는 최대 스토리지 크기가 2^31-1바이트(2GB)임을 나타냅니다. 스토리지 크기는 입력된 데이터의 실제 길이 + 2바이트입니다.  
  
 `char` [ ( *n* ) ]  
 길이가 *n* 바이트인 고정 길이의 비 유니코드 문자 데이터입니다. *n* 은 `1`과 `8000` 사이의 값이어야 합니다. 스토리지 크기는 *n* 바이트입니다. *n* 에 대한 기본값은 `1`입니다.  
  
 `varbinary` [ ( *n*  | `max` ) ]  -- `max`는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에만 적용됩니다.  
 가변 길이 이진 데이터입니다. *n* 은 `1`과 `8000` 사이의 값이어야 합니다. `max`는 최대 스토리지 크기가 2^31-1바이트(2GB)임을 나타냅니다. 스토리지 크기는 실제 입력된 데이터의 길이 + 2바이트입니다. *n* 의 기본값은 7입니다.  
  
 `binary` [ ( *n* ) ]  
 길이가 *n* 바이트인 고정 길이 이진 데이터입니다. *n* 은 `1`과 `8000` 사이의 값이어야 합니다. 스토리지 크기는 *n* 바이트입니다. *n* 의 기본값은 `7`입니다.  
  
 `uniqueidentifier`  
 16바이트 GUID입니다.  
   
<a name="Permissions"></a>  
## <a name="permissions"></a>사용 권한  
 테이블을 만들려면 `db_ddladmin` 고정 데이터베이스 역할의 사용 권한이 필요합니다.
 - 데이터베이스에 대한 `CREATE TABLE` 사용 권한
 - 테이블을 포함하는 스키마에 대한 `ALTER SCHEMA` 사용 권한입니다. 

분할된 테이블을 만들려면 `db_ddladmin` 고정 데이터베이스 역할의 사용 권한이 필요합니다. 또는

- `ALTER ANY DATASPACE` 사용 권한
  
 로컬 임시 테이블을 생성하는 로그인이 테이블에 대한 `CONTROL`, `INSERT`, `SELECT` 및 `UPDATE` 사용 권한을 받습니다.  
 
<a name="GeneralRemarks"></a>  
## <a name="general-remarks"></a>일반적인 주의 사항  
 
최소 및 최대 한도는 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 용량 한도](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-service-capacity-limits/)를 참조하세요. 
 
### <a name="determining-the-number-of-table-partitions"></a>테이블 파티션 수 확인
각 사용자 정의 테이블은 배포라고 하는 개별 위치에 저장된 더 작은 테이블 여러 개로 나누어집니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 60개 배포를 사용합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 배포 수는 컴퓨팅 노드 수에 따라 다릅니다.
 
각 배포에는 모든 테이블 파티션이 포함됩니다. 예를 들어 배포 60개 및 테이블 파티션 4개와 빈 파티션 1개가 있으면 300개의 파티션이 있는 것입니다(5 x 60= 300). 테이블이 클러스터형 columnstore 인덱스인 경우 파티션당 하나의 columnstore 인덱스가 됩니다. 즉, 300개의 columnstore 인덱스를 가지게 됩니다.

columnstore 인덱스의 이점 활용하기 위해 더 적은 테이블 파티션을 사용하여 각 columnstore 인덱스에 충분한 행이 있는지 확인하는 것이 좋습니다. 자세한 내용은 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 테이블 분할](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/) 및 [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 테이블 인덱싱](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-index/)을 참조하세요.  

### <a name="rowstore-table-heap-or-clustered-index"></a>rowstore 테이블(힙 또는 클러스터형 인덱스)

rowstore 테이블은 행별 순서로 저장된 테이블입니다. 힙 또는 클러스터형 인덱스입니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 페이지 압축을 통해 모든 rowstore 테이블을 만들며 이 동작은 사용자가 구성할 수 없습니다.

### <a name="columnstore-table-columnstore-index"></a>columnstore 테이블(columnstore 인덱스)

columnstore 테이블은 열별 순서로 저장된 테이블입니다. columnstore 인덱스는 columnstore 테이블에 저장된 데이터를 관리하는 기술입니다.  클러스터형 columnstore 인덱스는 데이터가 분산되는 방식에는 영향을 주지 않으며, 오히려 각 배포 내에서 데이터가 저장되는 방식에는 영향을 줍니다.

rowstore 테이블을 columnstore 테이블로 변경하려면 테이블에서 모든 기존 인덱스를 삭제하고 클러스터형 columnstore 인덱스를 만듭니다. 예제를 보려면 [CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)를 참조하세요.

자세한 내용은 다음 문서를 참조하세요.
- [버전이 지정된 columnstore 인덱스 기능 요약](/sql/relational-databases/indexes/columnstore-indexes-what-s-new)
- [[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 테이블 인덱싱](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-index/)
- [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md) 

<a name="LimitationsRestrictions"></a>  
## <a name="limitations-and-restrictions"></a>제한 사항  
 배포 열에서 DEFAULT 제약 조건을 정의할 수 없습니다.  
  
### <a name="partitions"></a>파티션
파티션을 사용할 때 파티션 열은 유니코드 전용 데이터 정렬을 포함할 수 없습니다. 예를 들어, 다음 명령문은 실패합니다.  
  
 ```sql
CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))
```  
 
 *boundary_value* 가 *partition_column_name* 의 데이터 형식으로 암시적으로 변환해야 하는 리터럴 값인 경우 불일치가 발생합니다. 리터럴 값은 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 시스템 뷰를 통해 표시되지만 변환된 값은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업에 사용됩니다. 

### <a name="temporary-tables"></a>임시 테이블

 ##으로 시작하는 전역 임시 테이블은 지원되지 않습니다.  
  
 로컬 임시 테이블에는 다음과 같은 제한 사항이 있습니다.  
  
-   현재 세션에만 표시됩니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 세션이 끝날 때 이를 자동으로 삭제합니다. 명시적으로 삭제하려면 DROP TABLE 문을 사용합니다.   
-   해당 이름을 바꿀 수 없습니다. 
-   파티션 또는 뷰를 포함할 수 없습니다.  
-   해당 권한은 변경할 수 없습니다. `GRANT`, `DENY` 및 `REVOKE` 문은 로컬 임시 테이블과 함께 사용할 수 없습니다.   
-   데이터베이스 콘솔 명령은 임시 테이블에 대해 차단됩니다.   
-   일괄 처리 내에서 둘 이상의 로컬 임시 테이블을 사용하는 경우 각각에 고유 이름이 있어야 합니다. 여러 세션이 동일한 일괄 처리를 실행하고 동일한 로컬 임시 테이블을 만드는 경우 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 내부적으로 로컬 임시 테이블 이름에 숫자 접미사를 추가하여 각 로컬 임시 테이블에 대한 고유한 이름을 유지합니다.  
    
<a name="LockingBehavior"></a>   
## <a name="locking-behavior"></a>잠금 동작  
 테이블에서 배타적 잠금을 사용합니다. DATABASE, SCHEMA 및 SCHEMARESOLUTION 개체에서 공유 잠금을 사용합니다.  
 

<a name="ExamplesColumn"></a>   
## <a name="examples-for-columns"></a>열에 대한 예제

### <a name="a-specify-a-column-collation"></a><a name="ColumnCollation"></a> 1. 열 데이터 정렬 지정 
 다음 예제에서는 `MyTable` 테이블이 두 개의 서로 다른 열 데이터 정렬을 사용하여 만들어집니다. 기본적으로 `mycolumn1` 열에는 기본 데이터 정렬 Latin1_General_100_CI_AS_KS_WS가 있습니다. `mycolumn2` 열에는 Frisian_100_CS_AS 데이터 정렬이 있습니다.  
  
```sql
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```  
  
### <a name="b-specify-a-default-constraint-for-a-column"></a><a name="DefaultConstraint"></a> 2. 열에 대해 DEFAULT 제약 조건 지정

 다음 예제에서는 열에 대한 기본값을 지정하는 구문을 보여 줍니다. colA 열에는 기본값 0 및 constraint_colA라는 기본 제약 조건이 있습니다.  
  
```sql
CREATE TABLE MyTable
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```

<a name="ExamplesTemporaryTables"></a> 
## <a name="examples-for-temporary-tables"></a>임시 테이블에 대한 예제

### <a name="c-create-a-local-temporary-table"></a><a name="TemporaryTable"></a> 3. 로컬 임시 테이블 만들기  
 다음 예제에서는 #myTable이라는 로컬 임시 테이블을 만듭니다. 테이블은 #으로 시작하는 세 부분으로 된 이름으로 지정됩니다.
  
```sql
CREATE TABLE AdventureWorks.dbo.#myTable
  (  
   id int NOT NULL,  
   lastName varchar(20),  
   zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),  
    CLUSTERED COLUMNSTORE INDEX
  )  
;  
```

<a name="ExTableStructure"></a>  
## <a name="examples-for-table-structure"></a>테이블 구조에 대한 예제

### <a name="d-create-a-table-with-a-clustered-columnstore-index"></a><a name="ClusteredColumnstoreIndex"></a> 4. 클러스터형 columnstore 인덱스로 테이블 만들기  
 다음 예에서는 클러스터형 columnstore 인덱스가 포함된 분산된 테이블을 만듭니다. 각 배포는 columnstore로 저장됩니다.  
  
 클러스터형 columnstore 인덱스는 데이터가 분포되는 방식에는 영향을 주지 않으며 데이터는 항상 행별로 배포됩니다. 클러스터형 columnstore 인덱스는 각 배포 내에서 데이터가 저장되는 방식에 영향을 줍니다.  
  
```sql
  CREATE TABLE MyTable
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS
  )  
WITH   
  (   
    DISTRIBUTION = HASH ( colB ),  
    CLUSTERED COLUMNSTORE INDEX
  )  
;  
```  

### <a name="e-create-an-ordered-clustered-columnstore-index"></a><a name="OrderedClusteredColumnstoreIndex"></a> 5. 순서가 지정된 클러스터형 columnstore 인덱스 만들기

다음 예는 순서가 지정된 클러스터형 columnstore 인덱스를 만드는 방법을 보여줍니다. 인덱스는 SHIPDATE에 정렬되어 있습니다.

```sql
CREATE TABLE Lineitem  
WITH (DISTRIBUTION = ROUND_ROBIN, CLUSTERED COLUMNSTORE INDEX ORDER(SHIPDATE))  
AS  
SELECT * FROM ext_Lineitem
```

<a name="ExTableDistribution"></a> 
## <a name="examples-for-table-distribution"></a>테이블 배포 예제

### <a name="f-create-a-round_robin-table"></a><a name="RoundRobin"></a> 6. ROUND_ROBIN 테이블 만들기  
 다음 예에서는 세 개의 열이 있고 파티션 없는 ROUND_ROBIN 테이블을 만듭니다. 데이터는 모든 배포에 걸쳐 분산됩니다. 힙 또는 rowstore 클러스터형 인덱스에 비해 더 나은 성능 및 데이터 압축을 제공하는 CLUSTERED COLUMNSTORE INDEX를 사용하여 테이블이 만들어집니다.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a name="g-create-a-hash-distributed-table"></a><a name="HashDistributed"></a> G. 해시 배포된 테이블 만들기

 다음 예에서는 이전 예와 동일한 테이블을 만듭니다. 그러나 이 테이블의 경우 행은 ROUND_ROBIN 테이블처럼 임의로 분산되는 대신 배포됩니다(`id` 열에서). 힙 또는 rowstore 클러스터형 인덱스에 비해 더 나은 성능 및 데이터 압축을 제공하는 CLUSTERED COLUMNSTORE INDEX를 사용하여 테이블이 만들어집니다.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),   
    CLUSTERED COLUMNSTORE INDEX  
  );  
```  
  
### <a name="h-create-a-replicated-table"></a><a name="Replicated"></a> H. 복제된 테이블 만들기  
 다음 예에서는 이전 예제와 비슷한 복제된 테이블을 만듭니다. 복제된 테이블은 각 컴퓨팅 노드에 전체가 복사됩니다. 각 컴퓨팅 노드에서 이 복사본을 사용하면 쿼리에 대한 데이터 이동이 줄어듭니다. 이 예제는 힙에 비해 더 나은 데이터 압축을 제공하는 클러스터형 인덱스를 사용하여 만들어집니다. CLUSTERED COLUMNSTORE INDEX 압축을 달성하는 데 충분한 행이 힙에 포함되지 않을 수 있습니다.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = REPLICATE,
    CLUSTERED INDEX (lastName)  
  );  
```  

<a name="ExTablePartitions"></a> 
## <a name="examples-for-table-partitions"></a>테이블 파티션에 대한 예제

###  <a name="i-create-a-partitioned-table"></a><a name="PartitionedTable"></a> I. 분할된 테이블 만들기

 다음 예에서는 RANGE LEFT 분할을 `id` 열에 추가하여 예 1과 동일한 테이블을 만듭니다. 4개의 파티션 경계 값을 지정하여 파티션이 5개가 됩니다.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH
  (
  
    PARTITION ( id RANGE LEFT FOR VALUES (10, 20, 30, 40 )),  
    CLUSTERED COLUMNSTORE INDEX
  )  
;  
```  
  
 이 예제에서는 다음과 같은 파티션으로 데이터가 정렬됩니다.  
  
- 파티션 1: col <= 10
- 파티션 2: 10 < col <= 20
- 파티션 3: 20 < col <= 30
- 파티션 4: 30 < col <= 40
- 파티션 5: 40 < col  
  
 이 동일한 테이블이 RANGE LEFT(기본값) 대신 RANGE RIGHT에서 분할되면 다음과 같은 파티션으로 데이터가 정렬됩니다.  
  
- 파티션 1: col < 10  
- 파티션 2: 10 <= col < 20
- 파티션 3: 20 <= col < 30
- 파티션 4: 30 <= col < 40
- 파티션 5: 40 <= col  
  
### <a name="j-create-a-partitioned-table-with-one-partition"></a><a name="OnePartition"></a> J. 하나의 파티션으로 분할된 테이블 만들기

 다음 예제에서는 하나의 파티션으로 분할된 테이블을 만듭니다. 경계 값을 지정하지 않아 파티션이 하나가 됩니다.  
  
```sql
CREATE TABLE myTable (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH
    (
      PARTITION ( id RANGE LEFT FOR VALUES ( )),  
      CLUSTERED COLUMNSTORE INDEX  
    )  
;  
```  
  
### <a name="k-create-a-table-with-date-partitioning"></a><a name="DatePartition"></a> K. 날짜 분할로 테이블 만들기

 다음 예제에서는 `date` 열에서 분할하여 `myTable`이라는 새 테이블을 만듭니다. 경계 값에 대해 RANGE RIGHT 및 날짜를 사용하면 각 파티션에 데이터의 월을 배치합니다.  
  
```sql
CREATE TABLE myTable (  
    l_orderkey      bigint,
    l_partkey       bigint,
    l_suppkey       bigint,
    l_linenumber    bigint,
    l_quantity      decimal(15,2),  
    l_extendedprice decimal(15,2),  
    l_discount      decimal(15,2),  
    l_tax           decimal(15,2),  
    l_returnflag    char(1),  
    l_linestatus    char(1),  
    l_shipdate      date,  
    l_commitdate    date,  
    l_receiptdate   date,  
    l_shipinstruct  char(25),  
    l_shipmode      char(10),  
    l_comment       varchar(44))  
WITH
  (
    DISTRIBUTION = HASH (l_orderkey),  
    CLUSTERED COLUMNSTORE INDEX,  
    PARTITION ( l_shipdate  RANGE RIGHT FOR VALUES
      (  
        '1992-01-01','1992-02-01','1992-03-01','1992-04-01','1992-05-01',
        '1992-06-01','1992-07-01','1992-08-01','1992-09-01','1992-10-01',
        '1992-11-01','1992-12-01','1993-01-01','1993-02-01','1993-03-01',
        '1993-04-01','1993-05-01','1993-06-01','1993-07-01','1993-08-01',
        '1993-09-01','1993-10-01','1993-11-01','1993-12-01','1994-01-01',
        '1994-02-01','1994-03-01','1994-04-01','1994-05-01','1994-06-01',
        '1994-07-01','1994-08-01','1994-09-01','1994-10-01','1994-11-01',
        '1994-12-01'  
      ))
  );  
```  
  
<a name="SeeAlso"></a>
## <a name="see-also"></a>참고 항목
 
[CREATE TABLE AS SELECT&#40;Azure Synapse Analytics&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
[DROP TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
[sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md?view=azure-sqldw-latest) 
