---
title: int, bigint, smallint 및 tinyint(Transact-SQL) | Microsoft Docs
description: Int, bigint, smallint, tinyint 데이터 형식의 Transact-SQL 참조입니다. 해당 데이터 형식은 정수 데이터를 나타내는 데 사용됩니다.
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Int()_TSQL
- sql13.swb.tsqlresults.f1
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- exact numeric data [SQL Server]
- numeric data
- tinyint data type
- int data type
- smallint data type
ms.assetid: 9bda5b0b-2380-4931-a1c8-f362fdefa99b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0fab6f77202c4a0fc136d760730c03d24e583870
ms.sourcegitcommit: b80364e31739d7b08cc388c1f83bb01de5dd45c1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87565621"
---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int, bigint, smallint 및 tinyint(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

정수 데이터를 사용하는 정확한 숫자 데이터 형식입니다. 데이터베이스의 공간을 절약하려면 가능한 모든 값을 안정적으로 포함할 수 있는 가장 작은 데이터 유형을 사용합니다. 예를 들어, tinyint는 255세 이상 사는 사람은 아무도 없기 때문에 사람의 나이에 충분합니다. 그러나 tinyint는 건물 수명이 255년 이상 될 수 있기 때문에 건물 수명에는 충분하지 않습니다.
  
|데이터 형식|범위|스토리지|  
|---|---|---|
|**bigint**|-2^63(-9,223,372,036,854,775,808) ~ 2^63-1(9,223,372,036,854,775,807)|8바이트|  
|**int**|-2^31(-2,147,483,648) ~ 2^31-1(2,147,483,647)|4바이트|  
|**smallint**|-2^15(-32,768) ~ 2^15-1(32,767)|2바이트|  
|**tinyint**|0 ~ 255|1바이트|  
  
## <a name="remarks"></a>설명  
**int** 데이터 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 주 정수 데이터 형식입니다. **bigint** 데이터 형식은 정수 값이 **int** 데이터 형식에서 지원하는 범위를 초과하는 경우에 사용하기 위한 것입니다.
  
**bigint**의 데이터 형식 우선 순위 위치는 **smallmoney**와 **int** 사이입니다.
  
함수는 매개 변수 식이 **bigint** 데이터 형식인 경우에만 **bigint**를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다른 정수 데이터 형식(**tinyint**, **smallint** 및 **int**)을 자동으로 **bigint**로 승격시키지 않습니다.
  
> [!CAUTION]  
>  +, -, \*, / 또는 % 산술 연산자를 사용하여 **int**, **smallint**, **tinyint** 또는 **bigint** 상수 값을 **float**, **real**, **decimal** 또는 **numeric** 데이터 형식으로 암시적 또는 명시적으로 변환하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터 형식과 식의 전체 자릿수를 계산할 때 적용하는 규칙은 쿼리에 자동으로 매개 변수가 지정되는지 여부에 따라 결과가 달라집니다.  
>   
>  그러므로 경우에 따라 쿼리의 비슷한 식이 다른 결과를 생성하기도 합니다. 쿼리에 자동으로 매개 변수가 지정되지 않는 경우 상수 값은 먼저 전체 자릿수가 상수 값을 보유할 수 있을 만큼 큰 **numeric**으로 변환된 다음, 지정된 데이터 형식으로 변환됩니다. 예를 들어 상수 값 1은 **numeric(1, 0)** 으로 변환되고 상수 값 250은 **numeric(3, 0)** 으로 변환됩니다.  
>   
>  쿼리에 자동으로 매개 변수가 지정되는 경우 상수 값은 최종 데이터 형식으로 변환하기 전에 항상 **numeric(10, 0)** 으로 변환됩니다. / 연산자가 들어 있는 경우 비슷한 쿼리 간에 결과 형식의 전체 자릿수뿐만 아니라 결과 값도 달라질 수 있습니다. 예를 들어 자동으로 매개 변수가 지정되며 `SELECT CAST (1.0 / 7 AS float)` 식이 포함된 쿼리의 결과 값은 자동으로 매개 변수가 지정되지 않는 동일한 쿼리의 결과 값과 달라집니다. 자동으로 매개 변수가 지정되는 쿼리의 결과는 **numeric(10, 0)** 데이터 형식에 맞게 잘리기 때문입니다.  
  
## <a name="converting-integer-data"></a>integer 데이터 변환
정수가 암시적으로 문자 데이터 형식으로 변환될 경우 정수가 너무 커서 문자 필드에 맞지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 ASCII 문자 42인 별표(*)를 입력합니다.
  
2,147,483,647보다 큰 정수 상수는 **decimal** 데이터 형식이 아닌 **bigint** 데이터 형식으로 변환됩니다. 다음 예에서는 임계값을 초과할 때 데이터 형식이 **int**에서 **decimal**로 변경됨을 보여 줍니다.
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>예  
다음 예에서는 **bigint**, **int**, **smallint** 및 **tinyint** 데이터 형식을 사용하여 테이블을 만듭니다. 값은 각 열에 삽입되고 SELECT 문으로 반환됩니다.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyBigIntColumn bigint  
,MyIntColumn  int
,MySmallIntColumn smallint
,MyTinyIntColumn tinyint
);  
  
GO  
  
INSERT INTO dbo.MyTable VALUES (9223372036854775807, 2147483647,32767,255);  
 GO  
SELECT MyBigIntColumn, MyIntColumn, MySmallIntColumn, MyTinyIntColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyBigIntColumn       MyIntColumn MySmallIntColumn MyTinyIntColumn  
-------------------- ----------- ---------------- ---------------  
9223372036854775807  2147483647  32767            255  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
