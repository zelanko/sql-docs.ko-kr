---
title: char 및 varchar(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
caps.latest.revision: 48
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: adccfc220015611e154da0d9c56cd4ca05748c58
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43064675"
---
# <a name="char-and-varchar-transact-sql"></a>char 및 varchar(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

고정 길이 또는 가변 길이의 데이터 형식입니다.  
  
## <a name="arguments"></a>인수  
**char** [ ( *n* ) ] 고정 길이 비유니코드 문자열 데이터입니다. *n*은 문자열 길이를 정의하며 1에서 8,000 사이의 값이어야 합니다. 저장소 크기는 *n*바이트입니다. ISO에서 정의한 **char**의 동의어는 **character**입니다.
  
**varchar** [ ( *n* | **max** ) ] 가변 길이의 비유니코드 문자열 데이터입니다. *n*은 문자열 길이를 정의하며 1에서 8,000 사이의 값이 될 수 있습니다. **max**는 최대 저장소 크기가 2^31-1바이트(2GB)임을 나타냅니다. 저장소 크기는 입력된 실제 데이터 길이에 2바이트를 더한 값입니다. ISO에서 정의한 **varchar**의 동의어는 **charvarying** 또는 **charactervarying**입니다.
  
## <a name="remarks"></a>Remarks  
데이터 정의나 변수 선언문에서 *n*을 지정하지 않으면 기본 길이 1이 사용됩니다. CAST 및 CONVERT 함수를 사용할 경우 *n*을 지정하지 않으면 기본 길이는 30입니다.
  
**char** 또는 **varchar**를 사용하는 개체에는 COLLATE 절을 사용하여 특정 데이터 정렬을 할당하지 않는 한 데이터베이스의 기본 데이터 정렬이 할당됩니다. 데이터 정렬은 문자 데이터를 저장하는 데 사용되는 코드 페이지를 제어합니다.
  
여러 언어를 지원하는 사이트를 가진 경우에는 문자 변환 문제를 최소화할 수 있도록 유니코드 **nchar** 또는 **nvarchar** 데이터 형식의 사용을 고려하세요. **char** 또는 **varchar**를 사용하는 경우에는 다음과 같이 하는 것이 좋습니다.
- 열 데이터 항목의 크기가 일관된 경우 **char**를 사용합니다.  
- 열 데이터 항목의 크기가 비교적 큰 차이를 보일 경우 **varchar**를 사용합니다.  
- 열 데이터 항목들의 크기가 비교적 큰 차이를 보이고 크기가 8,000바이트를 초과할 수 있는 경우 **varchar(max)** 를 사용합니다.  
  
CREATE TABLE 또는 ALTER TABLE 중 하나를 실행할 때 SET ANSI_PADDING이 OFF면 NULL로 정의된 **char** 열이 **varchar**로 처리됩니다.
  
데이터 정렬 코드 페이지에서 더블바이트 문자를 사용할 경우 저장소 크기는 계속 *n*바이트입니다. 문자열에 따라 *n* 바이트의 저장소 크기가 *n*자보다 작을 수도 있습니다.

> [!WARNING]
> Null이 아닌 각 varchar(max) 또는 nvarchar(max) 열은 24바이트의 추가 고정 할당이 필요하며 정렬 작업 시 여기에 8,060바이트의 행 제한이 적용됩니다. 이로 인해 null이 아닌 varchar(max) 또는 테이블에서 생성할 수 있는 nvarchar (max)열의 수에 묵시적 제한이 적용됩니다.  
테이블 생성 시 또는 데이터 삽입 시점에 특별한 오류(최대 행의 크기가 최대로 허용된 8060바이트를 초과한다는 일반적인 경고 외의 메시지)가 표시되지 않습니다. 이렇게 크기가 큰 행은 클러스터형 인덱스 키 업데이트 같은 일부 정상 작업이나 전체 열 집합 정렬에서 오류(오류 512 등)를 발생시킬 수 있고 사용자는 이러한 오류를 작업을 수행하기 전에는 예측할 수 없습니다.
  
##  <a name="_character"></a> 문자 데이터 변환  
문자 식이 다른 크기의 문자 데이터 형식으로 변환되면 새 데이터 형식에 대해 너무 긴 값은 잘립니다. **uniqueidentifier** 형식은 문자 식에서 변환하기 위한 문자 형식으로 간주되므로, 문자 형식으로 변환하기 위한 잘림 규칙이 있습니다. 뒷부분에 나오는 예 섹션을 참조하세요.
  
문자 식이 다른 데이터 형식 또는 크기의 문자 식으로 변환되는 경우(예: **char(5)** 에서 **varchar(5)** 로, 또는 **char(20)** 에서 **char(15)** 로) 입력 값의 데이터 정렬은 변환된 값에 적용됩니다. 문자 이외의 식을 문자 데이터 형식으로 변환하면 현재 데이터베이스의 기본 데이터 정렬이 변환된 값에 할당됩니다. 두 경우 모두 [COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) 절을 사용하여 특정 데이터 정렬을 할당할 수 있습니다.
  
> [!NOTE]  
>  **char** 및 **varchar** 데이터 형식에 대해서는 코드 페이지 변환이 지원되지만 **text** 데이터 형식에 대해서는 지원되지 않습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 마찬가지로 코드 페이지 변환 중 데이터 손실은 보고되지 않습니다.  
  
근사 **numeric** 데이터 형식으로 변환되는 문자 식에는 선택적 지수 표기(소문자 e 또는 대문자 E 다음에 옵션인 더하기(+) 또는 빼기(-) 기호가 온 다음 숫자가 옴)가 포함될 수 있습니다.
  
정확한 **numeric** 데이터 형식으로 변환되는 문자 식은 숫자, 소수점 및 옵션인 더하기(+) 또는 빼기(-) 기호로 구성되어야 합니다. 선행 공백은 무시됩니다. 123,456.00에서 천 단위 구분 기호와 같은 쉼표 구분 기호는 문자열에서 사용할 수 없습니다.
  
**money** 또는 **smallmoney** 데이터 형식으로 변환되는 문자 식에는 선택적 소수점 및 달러 기호($)가 포함될 수도 있습니다. $123,456.00에서처럼 쉼표 구분자를 사용할 수 있습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>1. 변수 선언에 사용될 때 n의 기본값 표시  
다음 예에서는 `char` 및 `varchar` 데이터 형식이 변수 선언에 사용될 때 *n*의 기본값이 1임을 보여 줍니다.
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>2. CAST 및 CONVERT에 varchar가 사용될 때 n의 기본값 표시  
다음 예에서는 `char` 또는 `varchar` 데이터 형식이 `CAST` 및 `CONVERT` 함수에 사용될 때 *n*의 기본값이 30임을 보여 줍니다.
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>3. 표시를 위해 데이터 변환  
다음 예에서는 두 개의 열을 문자 형식으로 변환한 후 해당 형식에 적용되는 스타일을 표시된 데이터에 적용합니다. **money** 형식이 문자 데이터로 변환되고 스타일 1이 적용됩니다. 스타일 1은 소수점 앞 세 자리마다 쉼표를 사용하고 소수점 뒤 두 자리까지 값을 표시합니다. **datetime** 형식이 문자 데이터로 변환되고 스타일 3이 적용됩니다. 스타일 3은 데이터를 dd/mm/yy 형식으로 표시합니다. WHERE 절에서 **money** 형식은 문자열 비교 연산을 수행하기 위해 문자 형식으로 캐스팅됩니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  BusinessEntityID,   
   SalesYTD,   
   CONVERT (varchar(12),SalesYTD,1) AS MoneyDisplayStyle1,   
   GETDATE() AS CurrentDate,   
   CONVERT(varchar(12), GETDATE(), 3) AS DateDisplayStyle3  
FROM Sales.SalesPerson  
WHERE CAST(SalesYTD AS varchar(20) ) LIKE '1%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
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
  
### <a name="d-converting-uniqueidentifer-data"></a>4. Uniqueidentifer 데이터 변환  
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
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:
[nchar 및 nvarchar&#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE&#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[데이터베이스 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  
