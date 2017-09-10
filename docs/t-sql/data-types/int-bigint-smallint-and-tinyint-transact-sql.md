---
title: "int, bigint, smallint 및 tinyint (TRANSACT-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bigint_TSQL
- smallint
- bigint
- smallint_TSQL
- tinyint_TSQL
- int_TSQL
- int
- tinyint
dev_langs:
- TSQL
helpviewer_keywords:
- exact numeric data [SQL Server]
- numeric data
- tinyint data type
- int data type
- smallint data type
ms.assetid: 9bda5b0b-2380-4931-a1c8-f362fdefa99b
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 07f5adc3d8ea7bb963b399cce22caa701021d6e9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int, bigint, smallint 및 tinyint(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

정수 데이터를 사용하는 정확한 숫자 데이터 형식입니다.
  
|데이터 형식|범위|저장소|  
|---|---|---|
|**bigint**|-2^63(-9,223,372,036,854,775,808) ~ 2^63-1(9,223,372,036,854,775,807)|8 바이트|  
|**int**|-2^31(-2,147,483,648) ~ 2^31-1(2,147,483,647)|4 바이트|  
|**smallint**|-2^15(-32,768) ~ 2^15-1(32,767)|2바이트|  
|**tinyint**|0 ~ 255|1바이트|  
  
## <a name="remarks"></a>주의  
**int** 데이터 형식이에서 주 정수 데이터 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. **bigint** 데이터 형식을 사용 하기 위한 정수 값에서 지원 되는 범위를 초과 하는 경우는 **int** 데이터 형식입니다.
  
**bigint** 사이 맞는 **smallmoney** 및 **int** 데이터 형식 우선 순위에 있습니다.
  
함수 반환 **bigint** 매개 변수 식이 있는 경우에는 **bigint** 데이터 형식입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]다른 정수 데이터 형식에 자동으로 승격 하지 않습니다 (**tinyint**, **smallint**, 및 **int**)를 **bigint**합니다.
  
> [!CAUTION]  
>  사용 하는 경우는 +,-, \*, /, 또는 % 산술 연산자의 암시적 또는 명시적 변환을 수행 하기 위해 **int**, **smallint**, **tinyint**, 또는  **bigint** 상수 값을 **float**, **실제**, **10 진수** 또는 **숫자** 규칙, 데이터 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 자동 인지 여부에 따라 다를 데이터 형식 및 식 결과 전체 자릿수를 계산할 때 적용 됩니다.  
>   
>  그러므로 경우에 따라 쿼리의 비슷한 식이 다른 결과를 생성하기도 합니다. 상수 값은 먼저 변환할 쿼리 자동 없을 때 **숫자**, 전체 자릿수가 지정 된 데이터 형식으로 변환 하기 전에 상수의 값을 보유할 수 만큼 큰 됩니다. 예를 들어 상수 값 1은 변환할 **숫자 (1, 0)**, 상수 값 250으로 변환 됩니다 **숫자 (3, 0)**합니다.  
>   
>  상수 값은 항상 변환할 쿼리 자동 이면 **숫자 (10, 0)** 최종 데이터 형식으로 변환 하기 전에. / 연산자가 들어 있는 경우 비슷한 쿼리 간에 결과 형식의 전체 자릿수뿐만 아니라 결과 값도 달라질 수 있습니다. 예를 들어 식이 포함 된 쿼리의의 결과 값 `SELECT CAST (1.0 / 7 AS float)` 자동 쿼리의 결과에 맞게 잘립니다 자동 되지 않는 동일한 쿼리의 결과 값에서 다릅니다 에 **숫자 (10, 0)** 데이터 형식입니다.  
  
## <a name="converting-integer-data"></a>Integer 데이터 변환
정수가 암시적으로 문자 데이터 형식으로 변환될 경우 정수가 너무 커서 문자 필드에 맞지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 ASCII 문자 42인 별표(*)를 입력합니다.
  
2147483647로 변환할지 보다 큰 정수 상수는 **10 진수** 데이터 형식이 아닌는 **bigint** 데이터 형식입니다. 다음 예에서는 임계값이 초과 되는 결과의 데이터 형식에서 변경 된 **int** 에 **10 진수**합니다.
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>예  
다음 예에서는 사용 하 여 테이블을 만듭니다는 **bigint**, **int**, **smallint**, 및 **tinyint** 데이터 형식입니다. 값은 각 열에 삽입되고 SELECT 문으로 반환됩니다.
  
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
[sys.types&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

