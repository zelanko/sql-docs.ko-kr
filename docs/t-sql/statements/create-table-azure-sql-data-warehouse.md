---
title: "테이블 (Azure SQL 데이터 웨어하우스) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ea21c73c-40e8-4c54-83d4-46ca36b2cf73
caps.latest.revision: 59
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11df71495b55ca72074c6ab928caaf6474bb2576
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-azure-sql-data-warehouse"></a>테이블 (Azure SQL 데이터 웨어하우스) 만들기
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  새 테이블을 만들고 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
 
참조 테이블 및 사용 하는 방법을 이해 하려면 [SQL 데이터 웨어하우스의 테이블](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-overview/)합니다.

참고:이 문서에서 SQL 데이터 웨어하우스에 대 한 토론에 적용할 SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스를 모두 언급이 없는 경우. 
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

<a name="Syntax"></a>   
## <a name="syntax"></a>구문  
  
```  
-- Create a new table. 
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]   
    )  
    [ WITH [ <table_option> [ ,...n ] ) ]  
[;]  
   
<column_options> ::=
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ] -- default is NULL  
    [ [ CONSTRAINT constraint_name ] DEFAULT constant_expression  ]
  
<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) -- default is ASC 
    }  
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN -- default for SQL Data Warehouse
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
    | nvarchar [ ( n | max ) ]  -- max applies only to SQL Data Warehouse 
    | nchar [ ( n ) ]  
    | varchar [ ( n | max )  ] -- max applies only to SQL Data Warehouse  
    | char [ ( n ) ]  
    | varbinary [ ( n | max ) ] -- max applies only to SQL Data Warehouse  
    | binary [ ( n ) ]  
    | uniqueidentifier  
```  

<a name="Arguments"></a>   
## <a name="arguments"></a>인수  
 *database_name*  
 새 테이블을 포함할 데이터베이스의 이름입니다. 기본값은 현재 데이터베이스입니다.  
  
 *schema_name*  
 테이블의 스키마입니다. 지정 *스키마* 선택 사항입니다. 이 옵션이 공백인 경우 기본 스키마 사용 됩니다.  
  
 *table_name*  
 새 테이블의 이름입니다. 로컬 임시 테이블을 만들려면 # 테이블 이름을 앞에 둡니다.  설명 및 임시 테이블에 대 한 지침에 대 한 참조 [Azure SQL 데이터 웨어하우스의 임시 표로](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-temporary/)합니다. 
 
 *column_name*  
 테이블 열의 이름입니다.
   
### <a name="ColumnOptions"></a>열 옵션

 `COLLATE`*Windows_collation_name*  
 식에 대 한 데이터 정렬을 지정합니다. 데이터 정렬에서 지 원하는 Windows 데이터 정렬 중 하나 여야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 지 원하는 Windows 데이터 정렬의 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 참조 [Windows 데이터 정렬 이름 (Transact SQL)](http://msdn.microsoft.com/library/ms188046\(v=sql11\)/)합니다.  
  
 `NULL` | `NOT NULL`  
 지정 여부 `NULL` 값 열에 허용 됩니다. 기본값은 `NULL`입니다.  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 기본 열 값을 지정합니다.  
  
 | 인수 | 설명 |
 | -------- | ----------- |
 | *제약 조건 이름* | 제약 조건에 대 한 선택적 이름입니다. 제약 조건 이름은 데이터베이스 내에서 고유 합니다. 이름은 다른 데이터베이스에서 다시 사용할 수 있습니다. |
 | *constant_expression* | 열에 대 한 기본값입니다. 식에 리터럴 값 이어야 합니다. 또는 상수입니다. 이러한 상수 식이 허용 되는 예를 들어: `'CA'`, `4`합니다. 이 허용 되지 않습니다: `2+3`, `CURRENT_TIMESTAMP`합니다. |
  

### <a name="TableOptions"></a>테이블 구조 옵션
테이블의 유형을 선택 하면에 대 한 지침을 참조 하십시오. [Azure SQL 데이터 웨어하우스의 테이블](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-index/)합니다.
  
 `CLUSTERED COLUMNSTORE INDEX`  
클러스터형된 columnstore 인덱스로 테이블을 저장합니다. 클러스터형된 columnstore 인덱스의 모든 테이블 데이터에 적용 됩니다. 에 대 한 기본값 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.   
 
 `HEAP`   
  테이블을 힙으로 저장합니다. 에 대 한 기본값 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
 `CLUSTERED INDEX`( *index_column_name* [,... *n* ] )  
 하나 이상의 키 열과 함께 클러스터형된 인덱스와 테이블을 저장합니다. 이 행에서 데이터를 저장합니다. 사용 하 여 *index_column_name* 인덱스에 하나 이상의 키 열 이름을 지정할 수 있습니다.  자세한 내용은 일반 설명에는 Rowstore 테이블을 참조 하십시오.
 
 `LOCATION = USER_DB`   
 이 옵션을 사용 하는 사용 되지 않습니다. 더 이상에서는 필수 구문상 승인이 이루어지고 동작을 더 이상 영향을 줍니다.   
  
### <a name="TableDistributionOptions"></a>테이블의 배포 옵션
최상의 배포 방법을 선택 하 고 분산된 테이블을 사용 하는 방법을 참조 하십시오 [표에 Azure SQL 데이터 웨어하우스 배포](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-distribute/)합니다.

`DISTRIBUTION = HASH`( *distribution_column_name* )   
각 행에 저장 된 값을 해시 하 여 하나의 배포 할당 *distribution_column_name*합니다. 즉, 항상 동일한 값을 동일 하 게 분산 해시 알고리즘은 결정적입니다.  분포 열 NULL가 동일 하 게 분산에 할당할 수 있는 모든 행 이후 NOT NULL로 정의 되어야 합니다.

`DISTRIBUTION = ROUND_ROBIN`   
균등 하 게 라운드 로빈 방식으로 모든 분포 행 분산합니다. 에 대 한 기본값 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.

`DISTRIBUTION = REPLICATE`    
각 계산 노드에 테이블의 복사본이 두 개를 저장합니다. 에 대 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 테이블 각 계산 노드에 대해 배포 데이터베이스에 저장 됩니다. 에 대 한 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 테이블에 저장 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 노드에 걸쳐 있는 파일 그룹입니다. 에 대 한 기본값 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.
  
### <a name="TablePartitionOptions"></a>테이블 파티션 옵션
테이블 파티션 사용에 대 한 지침을 참조 하십시오. [SQL 데이터 웨어하우스의 테이블을 분할](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/)합니다.

 `PARTITION`( *partition_column_name* `RANGE` [ `LEFT`  |  `RIGHT` ] `FOR VALUES` ([ *boundary_value* [,... *n*] ] ))   
하나 이상의 테이블 파티션을 만듭니다. 이들은 힙, 클러스터형된 인덱스 또는 클러스터형된 columnstore 인덱스에 테이블을 저장 하는 여부에 관계 없이 행의 하위 집합에 대 한 작업을 수행할 수 있도록 하는 가로 테이블 분할 영역입니다. 배포 열과 달리 테이블 파티션에서 각 행 저장 된 분포를 결정 하지 않습니다. 대신, 테이블 파티션 행 그룹화 되 고 각 배포 내에 저장 되는 방식을 결정 합니다.  
 
| 인수 | 설명 |
| -------- | ----------- |
|*partition_column_name*| 열을 지정 하는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 행 분할을 사용 합니다. 이 열에는 모든 데이터 형식일 수 있습니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]파티션 열 값을 오름차순으로 정렬 합니다. 낮음-높은 순서에서 전환 되 `LEFT` 를 `RIGHT` 을 목적으로 `RANGE` 사양입니다. |  
| `RANGE LEFT` | 경계 값 (값이 낮을수록) 왼쪽에 있는 파티션을에 속하도록 지정 합니다. 기본값은 LEFT입니다. |
| `RANGE RIGHT` | 경계 값이 오른쪽 (높은 값)에 파티션에 속한 지정 합니다. | 
| `FOR VALUES`( *boundary_value* [,... *n*] ) | 파티션에 대 한 경계 값을 지정합니다. *boundary_value* 상수 식입니다. NULL이 될 수 없습니다. 일치 하거나 변수의 데이터 형식을 암시적으로 변환할 수 있어야 *partition_column_name*합니다. 크기와 값의 배율의 데이터 형식이 일치 하지 않도록 암시적으로 변환 하는 동안 자를 수 없으므로 *partition_column_name*<br></br><br></br>지정 하는 경우는 `PARTITION` 절, 경계 값을 지정 하지 않으면 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 는 하나의 파티션 분할 된 테이블을 만듭니다. 해당 하는 경우 나중에 두 개의 파티션으로 표는 분할 수 있습니다.<br></br><br></br>결과 테이블에 두 개의 파티션이; 하나씩 경계 값을 지정 하는 경우 경계 값과 경계 값 보다 높은 값에 대 한 보다 낮은 값에 대 한 하나입니다. 참고를 분할 되지 않은 테이블에 파티션을 이동 하는 경우 분할 되지 않은 테이블의 데이터를 받을 있지만 해당 메타 데이터의 파티션 경계는 없습니다.| 
 
 참조 [분할 된 테이블을 만들](#PartitionedTable) "예" 섹션에 있습니다.

### <a name="DataTypes"></a>데이터 형식
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]가장 일반적으로 사용 되는 데이터 형식입니다. 다음은 세부 정보 및 저장소 바이트와 함께 지원 되는 데이터 형식의 목록입니다. 데이터 형식 및 사용 하는 방법을 더 잘 이해 하려면 참조 [ SQL 데이터 웨어하우스의 테이블에 대 한 데이터 형식을](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-data-types)합니다.

데이터 형식 변환의 테이블에 대 한의 암시적 변환 섹션을 참조 [CAST 및 CONVERT (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms187928/)합니다.

`datetimeoffset` [ ( *n* ) ]  
 에 대 한 기본값  *n*  은 7입니다.  
  
 `datetime2` [ ( *n* ) ]  
와 동일 `datetime`제외 하 고 소수 자릿수 초를 지정할 수 있습니다. 에 대 한 기본값  *n*  은 `7`합니다.  
  
|*n*값|전체 자릿수|소수 자릿수|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1.|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
|`7`|27|7|  
  
 `datetime`  
 양력 19-23 문자로 하루 중 시간과 날짜를 저장합니다. 날짜는 연도, 월 및 일에 포함할 수 있습니다. 시간 시간, 분, 초를 포함합니다. 선택적으로 세 자리 소수 자릿수 초에 표시할 수 있습니다. 저장소 크기는 8바이트입니다.  
  
 `smalldatetime`  
 날짜 및 시간을 저장합니다. 저장소 크기는 4 바이트입니다.  
  
 `date`  
 연도, 월 및 일 양력에 대 한 최대 10 자를 사용 하 여 날짜를 저장 합니다. 저장소 크기는 3 바이트입니다. 날짜를 정수로 저장 됩니다.  
  
 `time` [ ( *n* ) ]  
 에 대 한 기본값  *n*  은 `7`합니다.  
  
 `float` [ ( *n* ) ]  
 부동 소수점 숫자 데이터와 함께 사용할 근사 숫자 데이터 형식입니다. 부동 소수점 데이터는 근사치 데이터 형식 범위에서 일부 값을 정확 하 게 표현할 수 있음을 의미 합니다. *n*가 수를 저장 하는 데 사용 되는 비트 수를 지정 된 `float` 과학적 표기법으로 합니다. 따라서  *n*  전체 자릿수 및 저장소 크기를 지정 합니다. 경우  *n*  지정, 사이의 값 이어야 `1` 및 `53`합니다. 기본값  *n*  은 `53`합니다.  
  
| *n*값 | 전체 자릿수 | 저장소 크기 |  
| --------: | --------: | -----------: |  
| 1-24   | 7 자리  | 4 바이트      |  
| 25-53  | 15자리 | 8바이트      |  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]처리  *n*  가능한 두 값 중 하나로 합니다. 경우 `1` <=   *n*   <=  `24`,  *n*  로 처리 `24`합니다. 경우 `25`  <=   *n*   <=  `53`,  *n*  로 처리 `53`합니다.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] `float` 데이터 형식의 모든 값에 대 한 ISO 표준 준수  *n*  에서 `1` 통해 `53`합니다. 배정밀도의 동의어는 `float(53)`합니다.  
  
 `real` [ ( *n* ) ]  
 Real 정의 float와 같습니다. `real`의 ISO 동의어는 `float(24)`입니다.  
  
 `decimal`[( *정밀도* [ *, 배율* ])] | `numeric` [( *정밀도* [ *, 배율* ])]  
 고정 전체 자릿수 및 규모 숫자 값을 저장 합니다.  
  
 *전체 자릿수*  
 소수점 왼쪽과 오른쪽에 저장할 수 있는 10진수의 최대 총 수입니다. 전체 자릿수 사이의 값 이어야 합니다. `1` 의 최대 전체 자릿수인 `38`합니다. 기본 전체 자릿수는 `18`합니다.  
  
 *소수 자릿수*  
 소수점 오른쪽에 저장할 수 있는 10진수의 최대 수입니다. *배율* 사이의 값 이어야 `0` 통해 *정밀도*합니다. 만 지정할 수 있습니다 *배율* 경우 *정밀도* 지정 됩니다. 기본 배율은 `0`; 따라서 `0`  <=  *배율* <= *정밀도*합니다. 전체 자릿수에 따라 최대 저장소 크기가 달라집니다.  
  
| 전체 자릿수 | 저장소 크기(바이트)  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10-19      |             9 |  
| 20-28      |            13 |  
| 29-38      |            17 |  
  
 `money` | `smallmoney`  
 통화 값을 나타내는 데이터 형식입니다.  
  
| 데이터 형식 | 저장소 크기(바이트) |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` | `int` | `smallint` | `tinyint`  
 정수 데이터를 사용하는 정확한 숫자 데이터 형식입니다. 저장소는 다음 표에 표시 됩니다.  
  
| 데이터 형식 | 저장소 크기(바이트) |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1.|  
  
 `bit`  
 값을 사용할 수 있는 정수 데이터 형식 `1`, `0`, 또는 ' NULL입니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]bit 열의 저장소를 최적화합니다. 테이블의 8 개 이하의 비트 열의 경우 열 1 바이트로 저장 됩니다. 가 없을 경우 9-16 비트 열에서 열 2 바이트로 저장 등에입니다.  
  
 `nvarchar`[(  *n*   |  `max` )]- `max` 에 적용 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.  
 가변 길이 유니코드 문자 데이터입니다. *n*1에서 4000 사이의 값일 수 있습니다. `max`는 최대 저장소 크기가 2^31-1바이트(2GB)임을 나타냅니다. 저장소 크기 (바이트)에는 두 번 입력 한 문자 + 2 바이트의 수입니다. 입력된 데이터의 길이가 0일수도 있습니다.  
  
 `nchar` [ ( *n* ) ]  
 고정 길이 유니코드 문자 데이터의 길이 함께  *n*  문자입니다. *n*값 이어야 합니다 `1` 통해 `4000`합니다. 저장소 크기는 두 번  *n*  바이트입니다.  
  
 `varchar`[(  *n*    |  `max` )]- `max` 에 적용 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.   
 가변 길이의 비유니코드 문자 데이터의 길이 함께  *n*  바이트입니다. *n*값 이어야 합니다 `1` 를 `8000`합니다. `max`중임을 최대 저장소 크기가 2 ^31-1 바이트 (2GB)입니다. 저장소 크기에는 입력 된 데이터의 실제 길이 + 2 바이트입니다.  
  
 `char` [ ( *n* ) ]  
 고정 길이의 비유니코드 문자 데이터의 길이 함께  *n*  바이트입니다. *n*값 이어야 합니다 `1` 를 `8000`합니다. 저장소 크기는  *n*  바이트입니다. 에 대 한 기본  *n*  은 `1`합니다.  
  
 `varbinary`[(  *n*    |  `max` )]- `max` 에 적용 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.  
 가변 길이 이진 데이터입니다. *n*값 수 `1` 를 `8000`합니다. `max`는 최대 저장소 크기가 2^31-1바이트(2GB)임을 나타냅니다. 저장소 크기는 실제 입력된 데이터의 길이 + 2바이트입니다. 에 대 한 기본값  *n*  은 7입니다.  
  
 `binary` [ ( *n* ) ]  
 고정 길이 이진 데이터의 길이 함께  *n*  바이트입니다. *n*값 수 `1` 를 `8000`합니다. 저장소 크기는  *n*  바이트입니다. 에 대 한 기본값  *n*  은 `7`합니다.  
  
 `uniqueidentifier`  
 16바이트 GUID입니다.  
   
<a name="Permissions"></a>  
## <a name="permissions"></a>Permissions  
 권한이 필요 테이블 만들기는 `db_ddladmin` 고정 데이터베이스 역할 또는:
 - `CREATE TABLE`데이터베이스에 대 한 권한
 - `ALTER SCHEMA`테이블을 포함할 스키마에 대 한 권한이 있습니다. 

권한이 필요 분할된 된 테이블 만들기는 `db_ddladmin` 고정 데이터베이스 역할 또는

- `ALTER ANY DATASPACE`사용 권한
  
 로컬 임시 테이블이 생성 하는 로그인 받는 `CONTROL`, `INSERT`, `SELECT`, 및 `UPDATE` 테이블에 대 한 권한이 있습니다.  
 
<a name="GeneralRemarks"></a>  
## <a name="general-remarks"></a>일반적인 주의 사항  
 
최소 및 최대 제한에 대 한 참조 [SQL 데이터 웨어하우스 용량 제한을](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-service-capacity-limits/)합니다. 
 
### <a name="determining-the-number-of-table-partitions"></a>테이블 파티션 수를 결정합니다.
각 사용자 정의 테이블은 배포를 호출 하는 별도 위치에 저장 되는 여러 개의 작은 테이블로으로 구분 됩니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]60 분포를 사용합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 배포 수 계산 노드 수에 따라 다릅니다.
 
각 배포에는 모든 테이블 파티션이 포함 됩니다. 예를 들어 60 배포와 4 개의 테이블 파티션이 없으면 320 파티션이 됩니다. 테이블은 클러스터형된 columnstore 인덱스, columnstore 인덱스를 320 해야 의미 있는 파티션당 하나의 columnstore 인덱스가 됩니다.

Columnstore 인덱스의 이점 활용 하기 위해 충분 한 행이 각 columnstore 인덱스를 더 적은 테이블 파티션을 사용 하는 것이 좋습니다. 필요한 추가 지침에 대 한 참조 [SQL 데이터 웨어하우스의 테이블을 분할](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/) 및 [SQL 데이터 웨어하우스의 테이블](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)  

  
 ### <a name="rowstore-table-heap-or-clustered-index"></a>Rowstore 테이블 (힙 또는 클러스터형된 인덱스)  
 Rowstore 테이블에 행-순서에 저장 된 테이블이입니다. 힙 또는 클러스터형된 인덱스를입니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]페이지 압축;으로 모든 rowstore 테이블을 만듭니다. 이 사용자가 구성할 수는 있습니다.   
 
 ### <a name="columnstore-table-columnstore-index"></a>Columnstore 테이블 (columnstore 인덱스)
Columnstore 테이블에는 열 단위로 순서에 저장 된 테이블이입니다. Columnstore 인덱스는 columnstore 테이블에 저장 된 데이터를 관리 하는 기술입니다.  클러스터형된 columnstore 인덱스는 데이터; 분산 되는 방식을 그대로합니다 각 배포 내에서 데이터가 저장 되는 방식에 영향을 합니다.

Columnstore 테이블을 rowstore 테이블을 변경 하려면 테이블에 모든 기존 인덱스를 삭제 하 고 클러스터 된 columnstore 인덱스를 만듭니다. 예를 들어 참조 [CREATE COLUMNSTORE index&#40; Transact SQL &#41; ](../../t-sql/statements/create-columnstore-index-transact-sql.md).

자세한 내용은 다음 문서를 참조하세요.
- [Columnstore 인덱스 버전 형 기능 요약](https://msdn.microsoft.com/library/dn934994/)
- [인덱싱 표에 SQL 데이터 웨어하우스](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)
- [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md) 
 
<a name="LimitationsRestrictions"></a>  
## <a name="limitations-and-restrictions"></a>제한 사항  
 배포 열에 DEFAULT 제약 조건을 정의할 수 없습니다.  
  
 ### <a name="partitions"></a>파티션
 파티션을 사용할 때 파티션 열 유니코드 전용 데이터 정렬을 사용할 수 없습니다. 예를 들어 다음 문은 실패합니다.  
  
 `CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))`  
 
 경우 *boundary_value* 의 데이터 형식으로 암시적으로 변환 해야 하는 리터럴 값은 *partition_column_name*, 불일치가 발생 합니다. 리터럴 값을 통해 표시 됩니다는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 시스템 뷰만 변환 된 값에 사용 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 합니다. 
 
  
 ### <a name="temporary-tables"></a>임시 테이블
 로 시작 하는 전역 임시 테이블 # #는 지원 되지 않습니다.  
  
 로컬 임시 테이블에는 다음 제한 사항 및 제한 사항을:  
  
-   현재 세션에만 표시 됩니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]세션이 끝날 때 자동으로 삭제합니다. Explicitlt을 삭제 하려면 DROP TABLE 문을 사용 합니다.   
-   이름을 바꿀 수 없습니다. 
-   파티션 또는 뷰 여야 합니다.  
-   해당 사용 권한은 변경할 수 없습니다. `GRANT``DENY`, 및 `REVOKE` 로컬 임시 테이블 문을 사용할 수 없습니다.   
-   데이터베이스 콘솔 명령 임시 테이블에 대 한 차단 됩니다.   
-   일괄 처리 내에서 둘 이상의 로컬 임시 테이블을 사용 하는 경우 각 고유 이름이 있어야 합니다. 여러 세션 동일한 일괄 처리를 실행 하 고 동일한 로컬 임시 테이블을 만드는 경우 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 내부적으로 각 로컬 임시 테이블에 대 한 고유한 이름을 유지 하기 위해 로컬 임시 테이블 이름에 숫자 접미사를 추가 합니다.  
    
<a name="LockingBehavior"></a>   
## <a name="locking-behavior"></a>잠금 동작  
 테이블에 대 한 단독 잠금을 사용합니다. 데이터베이스, 스키마 및 SCHEMARESOLUTION 개체에 대 한 공유 잠금을 사용합니다.  
 

<a name="ExamplesColumn"></a>   
## <a name="examples-for-columns"></a>열에 대 한 예제

### <a name="ColumnCollation"></a> 1. 열 데이터 정렬 지정 
 다음 예제에서는 테이블에서에서 `MyTable` 두 개의 서로 다른 열 데이터 정렬을 사용 하 여 만들어집니다. 기본적으로 열을 `mycolumn1`, 기본 데이터 정렬을 Latin1_General_100_CI_AS_KS_WS. 열을 `mycolumn2` Frisian_100_CS_AS 데이터 정렬을 있습니다.  
  
```  
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
  
```  
  
### <a name="DefaultConstraint"></a> 2. 열에 대 한 기본 제약 조건을 지정 합니다.  
 다음 예제에서는 열에 대 한 기본값을 지정 하는 구문을 보여 줍니다. ColA 열에 기본값 0 및 constraint_colA 라는 default 제약 조건이 있습니다.  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```  

<a name="ExamplesTemporaryTables"></a> 
## <a name="examples-for-temporary-tables"></a>임시 테이블에 대 한 예제

### <a name="TemporaryTable"></a> 3. 로컬 임시 테이블 만들기  
 다음 #myTable 라는 로컬 임시 테이블을 만듭니다. 테이블 3 부분으로 된 이름을로 지정 됩니다. 임시 테이블 이름이 #로 시작합니다.   
  
```  
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
## <a name="examples-for-table-structure"></a>테이블 구조에 대 한 예제

### <a name="ClusteredColumnstoreIndex"></a> 4. 클러스터형된 columnstore 인덱스가 있는 테이블 만들기  
 다음 예에서는 클러스터형된 columnstore 인덱스가 포함 된 분산된 테이블을 만듭니다. 각 배포를 columnstore로 저장 됩니다.  
  
 클러스터형된 columnstore 인덱스 데이터가 분포 되는 방식을; 영향을 주지 않습니다. 데이터는 항상 행으로 배포 됩니다. 클러스터형된 columnstore 인덱스 각 배포 내에서 데이터가 저장 되는 방식에 영향을 줍니다.  
  
```  
  
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
 
<a name="ExTableDistribution"></a> 
## <a name="examples-for-table-distribution"></a>테이블 배포에 대 한 예제

### <a name="RoundRobin"></a> 5. ROUND_ROBIN 테이블 만들기  
 다음 예제에서는 세 개의 열과 파티션 없는 ROUND_ROBIN 테이블을 만듭니다. 데이터는 모든 분포 분산 됩니다. 힙 또는 rowstore 클러스터형된 인덱스에 비해 더 나은 성능 및 데이터 압축을 제공 하는 클러스터형 COLUMNSTORE 인덱스와 테이블이 만들어집니다.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a name="HashDistributed"></a> 6. 해시 distributed 테이블 만들기  
 다음 예제에서는 이전 예제와 동일한 테이블을 만듭니다. 그러나이 테이블에 대 한 행이 배포 되 (에 `id` 열) 대신 ROUND_ROBIN 테이블 처럼 임의로 분산 합니다. 힙 또는 rowstore 클러스터형된 인덱스에 비해 더 나은 성능 및 데이터 압축을 제공 하는 클러스터형 COLUMNSTORE 인덱스와 테이블이 만들어집니다.  
  
```  
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
  
### <a name="Replicated"></a>7. 복제 된 테이블 만들기  
 다음 예제에서는 이전 예제와 비슷한 복제 된 테이블을 만듭니다. 복제 된 테이블은 각 계산 노드에 전체가 복사 됩니다. 각 계산 노드에 대해이 복사본을 쿼리에 대 한 데이터 이동을 줄어듭니다. 이 예에서는 클러스터형 인덱스를 사용 하면 힙 보다 더 나은 데이터 압축을 제공 하 고 CLUSTERED COLUMNSTORE INDEX 압축을 달성 하기 위해 충분 한 행이 포함 되지 않을 수 있습니다는 만들어집니다.  
  
```  
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
## <a name="examples-for-table-partitions"></a>테이블 분할에 대 한 예제

###  <a name="PartitionedTable"></a>8. 분할된 된 테이블 만들기  
 다음 예에서는 예 1에서 RANGE LEFT 분할을 추가 하 여 표시 된 것 처럼 동일한 테이블을 만듭니다는 `id` 열입니다. 5 개의 파티션을 줄어들고 결과적 4 개의 파티션 경계 값을 지정 합니다.  
  
```  
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
  
 이 예제에서는 다음과 같은 파티션으로 데이터 정렬:  
  
-   파티션 1: col < = 10   
-   분할 2시 10분 < col < = 20   
-   파티션 3시 20분 < col < = 30   
-   파티션 4시 30분 < col < = 40   
-   파티션 5시 40분 < 열  
  
 이 동일한 테이블이 분할 된 경우 RANGE LEFT (기본값) 이면 데이터 대신 RANGE RIGHT 파티션에 정렬 됩니다.  
  
-   파티션 1: col < 10  
-   분할 2시 10분 < = col < 20   
-   파티션 3시 20분 < = col < 30    
-   파티션 4시 30분 < = col < 40   
-   파티션 5시 40분 < = 열  
  
### <a name="OnePartition"></a>I입니다. 하나의 파티션 분할된 된 테이블 만들기  
 다음 예제에서는 하나의 파티션 분할된 된 테이블을 만듭니다. 지정 하지 않습니다 경계 값을 하나의 파티션을 생성 합니다.  
  
```  
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
  
### <a name="DatePartition"></a>10. 분할 날짜 테이블 만들기  
 다음 예에서는 라는 새 테이블을 만들어 `myTable`와 분할을 `date` 열입니다. 경계 값에 대 한 날짜 및 RANGE RIGHT를 사용 하 여 각 파티션에 있는 데이터의 월을 배치 합니다.  
  
```  
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
 
 [TABLE AS SELECT &#40; 만들기 Azure SQL 데이터 웨어하우스 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP table&#40; Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

