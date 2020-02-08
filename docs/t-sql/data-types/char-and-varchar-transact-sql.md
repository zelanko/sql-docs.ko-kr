---
title: char 및 varchar(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- varchar
- varchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fixed-length data types [SQL Server]
- character data type
- char data type
- varchar(max) data type
- variable-length data types [SQL Server]
- varchar data type
- utf8
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efc2d749f3963f0828a70bc1506581f5bd2a35a3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75246226"
---
# <a name="char-and-varchar-transact-sql"></a>char 및 varchar(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

고정 크기(**char**) 또는 가변 크기(**varchar**)인 문자 데이터 형식입니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 UTF-8 사용 데이터 정렬을 사용할 때 이러한 데이터 형식은 전체 범위의 [유니코드](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn) 문자 데이터를 저장하고 [UTF-8](https://www.wikipedia.org/wiki/UTF-8) 문자 인코딩을 사용합니다. UTF-8이 아닌 데이터 정렬이 지정된 경우 이러한 데이터 형식은 해당 데이터 정렬의 코드 페이지에서 지원하는 문자의 하위 집합만 저장합니다.

## <a name="arguments"></a>인수

**char** [ ( *n* ) ] 고정 크기 문자열 데이터입니다. *n*은 바이트로 문자열 크기를 정의하며 1에서 8,000 사이의 값이어야 합니다. ‘라틴 문자’처럼 싱글바이트 인코딩 문자 집합의 경우 스토리지 크기는 *n*바이트이고 저장할 수 있는 문자 수도 *n*입니다.  멀티바이트 인코딩 문자 집합의 경우 스토리지 크기는 여전히 *n*바이트이지만 저장할 수 있는 문자 수는 *n*보다 작을 수 있습니다. ISO에서 정의한 **char**의 동의어는 **character**입니다. 문자 집합에 대한 자세한 내용은 [싱글바이트 및 멀티바이트 문자 집합](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)을 참조하세요.

**varchar** [ ( *n* | **max** ) ] 가변 크기의 문자열 데이터입니다. *n*을 사용하여 문자열 크기(바이트)를 정의할 수 있으며 1~8,000 사이의 값이거나 **최대**를 사용하여 2^31-1바이트(2GB)의 최대 저장소 크기로 열 제약 조건을 나타낼 수 있습니다. ‘라틴 문자’처럼 싱글바이트 인코딩 문자 집합의 경우 스토리지 크기는 *n*바이트 +2바이트이고 저장할 수 있는 문자 수도 *n*입니다.  멀티바이트 인코딩 문자 집합의 경우 스토리지 크기는 여전히 *n*바이트 + 2바이트지만 저장할 수 있는 문자 수는 *n*보다 작을 수 있습니다. ISO에서 정의한 **varchar**의 동의어는 **charvarying** 또는 **charactervarying**입니다. 문자 집합에 대한 자세한 내용은 [싱글바이트 및 멀티바이트 문자 집합](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)을 참조하세요.

## <a name="remarks"></a>설명

[CHAR(*n*) 및 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md)에서 *n*이 문자 수를 정의한다고 잘못 생각하는 경우가 많습니다. 그러나 [CHAR(*n*) 및 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md)에서 *n*은 **바이트**의 문자열 길이(0~8,000)를 정의합니다. *n*은 저장할 수 있는 문자 수를 정의하지 않습니다. [NCHAR(*n*) 및 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 정의와 비슷합니다.
싱글바이트 인코딩을 사용하는 경우 CHAR 및 VARCHAR의 스토리지 크기는 *n*바이트이고 문자 수도 *n*자이기 때문에 오해가 발생합니다. 그러나 [UTF-8](https://www.wikipedia.org/wiki/UTF-8)과 같은 멀티바이트 인코딩의 경우 상위 유니코드 범위(128~1,114,111)에서는 한 문자가 2바이트 이상을 사용합니다. 예를 들어 CHAR(10)로 정의된 열에서 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 싱글바이트 인코딩을 사용하는 문자(유니코드 범위 0~127) 10자를 저장할 수 있지만, 멀티바이트 인코딩을 사용하는 경우(유니코드 범위 128~1,114,111) 10자 미만을 저장할 수 있습니다. 유니코드 스토리지 및 문자 범위에 대한 자세한 내용은 [UTF-8과 UTF-16 간의 스토리지 차이점](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences)을 참조하세요.

데이터 정의나 변수 선언문에서 *n*을 지정하지 않으면 기본 길이는 1입니다. CAST 및 CONVERT 함수를 사용할 경우 *n*을 지정하지 않으면 기본 길이는 30입니다.

**char** 또는 **varchar**를 사용하는 개체에는 COLLATE 절을 사용하여 특정 데이터 정렬을 할당하지 않는 한 데이터베이스의 기본 데이터 정렬이 할당됩니다. 데이터 정렬은 문자 데이터를 저장하는 데 사용되는 코드 페이지를 제어합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 멀티바이트 인코딩에는 다음이 포함됩니다.

- 코드 페이지 936 및 950(중국어), 932(일본어) 또는 949(한국어)를 사용하는 일부 동아시아 언어의 경우 DBCS(더블바이트 문자 집합)입니다.
- 코드 페이지가 65001인 UTF-8입니다. **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 시작))

여러 언어를 지원하는 사이트가 있는 경우:

- [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 부터 UTF-8 사용 데이터 정렬을 사용하여 유니코드를 지원하고 문자 변환 문제를 최소화하세요.
- 더 낮은 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을(를) 사용하는 경우 유니코드 **nchar** 또는 **nvarchar** 데이터 형식을 사용하여 문자 변환 문제를 최소화하세요.

**char** 또는 **varchar**를 사용하는 경우에는 다음과 같이 하는 것이 좋습니다.

- 열 데이터 항목의 크기가 일관된 경우 **char**를 사용합니다.
- 열 데이터 항목의 크기가 비교적 큰 차이를 보일 경우 **varchar**를 사용합니다.
- 열 데이터 항목들의 크기가 비교적 큰 차이를 보이고 문자열 길이가 8,000바이트를 초과할 수 있는 경우 **varchar(max)** 를 사용합니다.

CREATE TABLE 또는 ALTER TABLE 중 하나를 실행할 때 SET ANSI_PADDING이 OFF면 NULL로 정의된 **char** 열이 **varchar**로 처리됩니다.

> [!WARNING]
> Null이 아닌 각 varchar(max) 또는 nvarchar(max) 열은 24바이트의 추가 고정 할당이 필요하며 정렬 작업 시 여기에 8,060바이트의 행 제한이 적용됩니다. 이로 인해 null이 아닌 varchar(max) 또는 테이블에서 생성할 수 있는 nvarchar (max)열의 수에 묵시적 제한이 적용됩니다.
테이블 생성 시 또는 데이터 삽입 시점에 특별한 오류(최대 행의 크기가 최대로 허용된 8,060바이트를 초과한다는 일반적인 경고 외의 메시지)가 표시되지 않습니다. 이렇게 크기가 큰 행은 클러스터형 인덱스 키 업데이트 같은 일부 정상 작업이나 전체 열 집합 정렬에서 오류(오류 512 등)를 발생시킬 수 있으며, 이 오류는 작업을 수행하는 동안에만 발생합니다.

## <a name="_character"></a> 문자 데이터 변환

문자 식이 다른 크기의 문자 데이터 형식으로 변환되면 새 데이터 형식에 대해 너무 긴 값은 잘립니다. **uniqueidentifier** 형식은 문자 식에서 변환하기 위한 문자 형식으로 간주되므로, 문자 형식으로 변환하기 위한 잘림 규칙이 있습니다. 뒷부분에 나오는 예 섹션을 참조하세요.

문자 식이 다른 데이터 형식 또는 크기의 문자 식으로 변환되는 경우(예: **char(5)** 에서 **varchar(5)** 로, 또는 **char(20)** 에서 **char(15)** 로) 입력 값의 데이터 정렬은 변환된 값에 적용됩니다. 문자 이외의 식을 문자 데이터 형식으로 변환하면 현재 데이터베이스의 기본 데이터 정렬이 변환된 값에 할당됩니다. 두 경우 모두 [COLLATE](../../t-sql/statements/collations.md) 절을 사용하여 특정 데이터 정렬을 할당할 수 있습니다.

> [!NOTE]
> **char** 및 **varchar** 데이터 형식에 대해서는 코드 페이지 변환이 지원되지만 **text** 데이터 형식에 대해서는 지원되지 않습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 마찬가지로 코드 페이지 변환 중 데이터 손실은 보고되지 않습니다.

근사 **numeric** 데이터 형식으로 변환되는 문자 식에는 선택적 지수 표기법이 포함될 수 있습니다. 이 표기법은 소문자 e 또는 대문자 E 다음에 선택적 더하기(+) 또는 빼기(-) 기호가 온 다음 숫자가 옵니다.

정확한 **numeric** 데이터 형식으로 변환되는 문자 식은 숫자, 소수점 및 옵션인 더하기(+) 또는 빼기(-) 기호로 구성되어야 합니다. 선행 공백은 무시됩니다. 123,456.00에서 천 단위 구분 기호와 같은 쉼표 구분 기호는 문자열에서 사용할 수 없습니다.

**money** 또는 **smallmoney** 데이터 형식으로 변환되는 문자 식에는 선택적 소수점 및 달러 기호($)가 포함될 수도 있습니다. $123,456.00에서처럼 쉼표 구분자를 사용할 수 있습니다.

빈 문자열이 **int**로 변환되면 해당 값은 ```0```이 됩니다. 빈 문자열이 날짜로 변환되면 해당 값은 [날짜의 기본값](date-transact-sql.md)인 ```1900-01-01```이 됩니다.

## <a name="examples"></a>예

### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. 변수 선언에 사용될 때 n의 기본값 표시

다음 예에서는 `char` 및 `varchar` 데이터 형식이 변수 선언에 사용될 때 *n*의 기본값이 1임을 보여 줍니다.

```sql
DECLARE @myVariable AS varchar = 'abc';
DECLARE @myNextVariable AS char = 'abc';
--The following returns 1
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);
GO
```

### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. CAST 및 CONVERT에 varchar가 사용될 때 n의 기본값 표시

다음 예에서는 `char` 또는 `varchar` 데이터 형식이 `CAST` 및 `CONVERT` 함수에 사용될 때 *n*의 기본값이 30임을 보여 줍니다.

```sql
DECLARE @myVariable AS varchar(40);
SET @myVariable = 'This string is longer than thirty characters';
SELECT CAST(@myVariable AS varchar);
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';
SELECT CONVERT(char, @myVariable);
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';
```

### <a name="c-converting-data-for-display-purposes"></a>C. 표시를 위해 데이터 변환

다음 예에서는 두 개의 열을 문자 형식으로 변환한 후 해당 형식에 적용되는 스타일을 표시된 데이터에 적용합니다. **money** 형식이 문자 데이터로 변환되고 스타일 1이 적용됩니다. 스타일 1은 소수점 앞 세 자리마다 쉼표를 사용하고 소수점 뒤 두 자리까지 값을 표시합니다. **datetime** 형식이 문자 데이터로 변환되고 스타일 3이 적용됩니다. 스타일 3은 데이터를 dd/mm/yy 형식으로 표시합니다. WHERE 절에서 **money** 형식은 문자열 비교 연산을 수행하기 위해 문자 형식으로 캐스팅됩니다.

```sql
USE AdventureWorks2012;
GO
SELECT BusinessEntityID,
   SalesYTD,
   CONVERT (varchar(12),SalesYTD,1) AS MoneyDisplayStyle1,
   GETDATE() AS CurrentDate,
   CONVERT(varchar(12), GETDATE(), 3) AS DateDisplayStyle3
FROM Sales.SalesPerson
WHERE CAST(SalesYTD AS varchar(20) ) LIKE '1%';
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
BusinessEntityID SalesYTD              DisplayFormat CurrentDate             DisplayDateFormat
---------------- --------------------- ------------- ----------------------- -----------------
278              1453719.4653          1,453,719.47  2011-05-07 14:29:01.193 07/05/11
280              1352577.1325          1,352,577.13  2011-05-07 14:29:01.193 07/05/11
283              1573012.9383          1,573,012.94  2011-05-07 14:29:01.193 07/05/11
284              1576562.1966          1,576,562.20  2011-05-07 14:29:01.193 07/05/11
285              172524.4512           172,524.45    2011-05-07 14:29:01.193 07/05/11
286              1421810.9242          1,421,810.92  2011-05-07 14:29:01.193 07/05/11
288              1827066.7118          1,827,066.71  2011-05-07 14:29:01.193 07/05/11
```

### <a name="d-converting-uniqueidentifer-data"></a>D. Uniqueidentifer 데이터 변환

다음 예는 `uniqueidentifier` 값을 `char` 데이터 형식으로 변환합니다.

```sql
DECLARE @myid uniqueidentifier = NEWID();
SELECT CONVERT(char(255), @myid) AS 'char';
```

다음 예는 변환될 데이터 형식에서 해당 값이 너무 길면 데이터가 잘림을 보여 줍니다. **uniqueidentifier** 형식은 36자로 제한되므로 길이가 초과된 글자는 잘립니다.

```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
String                                       TruncatedValue
-------------------------------------------- ------------------------------------
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0

(1 row(s) affected)
```

## <a name="see-also"></a>참고 항목

[nchar 및 nvarchar&#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
[COLLATE&#40;Transact-SQL&#41;](../../t-sql/statements/collations.md)
[데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
[데이터베이스 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-database.md)
[데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)
[단일 바이트 및 다중 바이트 문자 집합](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)
