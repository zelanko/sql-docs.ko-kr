---
title: "char 및 varchar (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- varchar
- varchar_TSQL
dev_langs: TSQL
helpviewer_keywords:
- fixed-length data types [SQL Server]
- character data type
- char data type
- varchar(max) data type
- variable-length data types [SQL Server]
- varchar data type
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
caps.latest.revision: "48"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4c383e3b3ff5b79604454f80443c9042633797bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="char-and-varchar-transact-sql"></a>char 및 varchar(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이러한 데이터 형식의 길이 고정된 길이 또는 가변 길이입니다.  
  
## <a name="arguments"></a>인수  
**char** [(  *n*  )] 고정 길이의 비유니코드 문자열 데이터. *n*문자열 길이 정의 하며 1부터 8,000 사이의 값 이어야 합니다. 저장소 크기는  *n*  바이트입니다. ISO 동의어는 **char** 은 **문자**합니다.
  
**varchar** [(  *n*   |  **max** )] 가변 길이의 비유니코드 문자열 데이터. *n*문자열 길이 정의 하며 1부터 8,000 사이의 값이 될 수 있습니다. **최대** 중임을 최대 저장소 크기가 2 ^31-1 바이트 (2GB)입니다. 저장소 크기는 입력된 실제 데이터 길이에 2바이트를 더한 값입니다. ISO 동의어 **varchar** 는 **charvarying** 또는 **charactervarying**합니다.
  
## <a name="remarks"></a>주의  
때  *n*  기본 길이 1 데이터 정의 나 변수 선언문에서 지정 하지 않으면 합니다. 때  *n*  지정 하지 않으면 CAST 및 CONVERT 함수를 사용 하는 경우 기본 길이 30입니다.
  
사용 하는 개체 **char** 또는 **varchar** COLLATE 절을 사용 하 여 특정 데이터 정렬을 할당 하지 않는 한 데이터베이스의 기본 데이터 정렬이 할당 됩니다. 데이터 정렬은 문자 데이터를 저장하는 데 사용되는 코드 페이지를 제어합니다.
  
여러 언어를 지 원하는 사이트를 사용 하는 경우 유니코드를 사용 하 여 하십시오 **nchar** 또는 **nvarchar** 문자 변환 문제를 최소화 하기 위해 데이터 형식입니다. 사용 하는 경우 **char** 또는 **varchar**, 다음 것이 좋습니다.
- 사용 하 여 **char** 열 데이터 항목의 크기가 동일 합니다.  
- 사용 하 여 **varchar** 열 데이터 항목의 크기가 크게 달라질 때.  
- 사용 하 여 **varchar (max)** 열 데이터 항목의 크기 차이 보이고 시점과 크기는 8, 000 바이트를 초과할 수 있습니다.  
  
CREATE TABLE 또는 ALTER TABLE 중 하나를 실행 하면 SET ANSI_PADDING 옵션이 OFF 면는 **char** NULL로 처리 되는 정의 된 열 **varchar**합니다.
  
데이터 정렬 코드 페이지에서 더블 바이트 문자를 사용할 경우 저장소 크기는 여전히  *n*  바이트입니다. 문자열의 저장소 크기가 따라  *n*  바이트 수 미만  *n*  문자입니다.

> [!WARNING]
> 각 null이 아닌 varchar (max) 또는 nvarchar (max) 열에는 24 바이트의 추가 고정된 할당 정렬 작업 동안 8, 060 바이트 행 제한에 따라 계산 하는 필요 합니다. 이 null이 아닌 varchar (max) 또는 테이블에서 만들 수 있는 nvarchar (max) 열 수에 암묵적인 제한이 생깁니다.  
테이블 생성 시 또는 데이터 삽입 시점에 특별한 오류(최대 행의 크기가 최대로 허용된 8060바이트를 초과한다는 일반적인 경고 외의 메시지)가 표시되지 않습니다. 이렇게 크기가 큰 행은 클러스터형 인덱스 키 업데이트 같은 일부 정상 작업이나 전체 열 집합 정렬에서 오류(오류 512 등)를 발생시킬 수 있고 사용자는 이러한 오류를 작업을 수행하기 전에는 예측할 수 없습니다.
  
##  <a name="_character"></a>문자 데이터 변환  
문자 식이 다른 크기의 문자 데이터 형식으로 변환되면 새 데이터 형식에 대해 너무 긴 값은 잘립니다. **uniqueidentifier** 형식이 문자 형식으로 간주 됩니다는 문자 식에서 변환의 목적에 대 한와 문자 형식으로 변환 하기 위한 잘림 규칙이 이므로 합니다. 뒷부분에 나오는 예 섹션을 참조하세요.
  
때 문자 식에서 변환 됩니다 크기 또는 다른 데이터 형식에는 문자 식과 같은 **char (5)** 를 **varchar(5)**, 또는 **char(20)** 를**char(15)**, 입력된 값의 데이터 정렬이 변환 된 값에 할당 됩니다. 문자 이외의 식을 문자 데이터 형식으로 변환하면 현재 데이터베이스의 기본 데이터 정렬이 변환된 값에 할당됩니다. 두 경우 모두에서 특정 데이터 정렬을 사용 하 여 할당할 수 있습니다는 [COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) 절.
  
> [!NOTE]  
>  코드 페이지 변환이 지원 되는 **char** 및 **varchar** 데이터 형식에 대 한 **텍스트** 데이터 형식입니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 마찬가지로 코드 페이지 변환 중 데이터 손실은 보고되지 않습니다.  
  
대략적인 값으로 변환 되는 문자 식 **숫자** 데이터 형식은 선택적 지 수 표기를 포함할 수 있습니다 (소문자 e 또는 대문자 E 다음에 옵션인 더하기 (+) 또는 빼기 (-) 기호가 온 다음 숫자가).
  
문자는 정확한으로 변환 중인 식 **숫자** 자릿수, 소수점 및 선택적 데이터 형식으로 구성 되어야 더하기 (+) 또는 빼기 (-). 선행 공백은 무시됩니다. 123,456.00에서 천 단위 구분 기호와 같은 쉼표 구분 기호는 문자열에서 사용할 수 없습니다.
  
문자 식으로 변환 되 고 **money** 또는 **smallmoney** 선택적 소수점 및 달러 기호 ($)에 데이터 형식을 포함할 수 있습니다. $123,456.00에서처럼 쉼표 구분자를 사용할 수 있습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>1. 변수 선언에 사용될 때 n의 기본값 표시  
다음 예제에서는 기본값인  *n*  는 1에 대 한는 `char` 및 `varchar` 변수 선언에 사용 되는 데이터 형식입니다.
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>2. CAST 및 CONVERT에 varchar가 사용될 때 n의 기본값 표시  
다음 예제에서는 기본값인  *n*  30 때는 `char` 또는 `varchar` 데이터 형식에 사용 되는 `CAST` 및 `CONVERT` 함수입니다.
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>3. 표시를 위해 데이터 변환  
다음 예에서는 두 개의 열을 문자 형식으로 변환한 후 해당 형식에 적용되는 스타일을 표시된 데이터에 적용합니다. A **money** 형식이 문자 데이터로 변환 되 고 스타일 1 표시 하는 값은 쉼표로 구분 소수점 기호 왼쪽으로 세 자리 마다 및 두 자리 숫자의 소수점 오른쪽에 적용 됩니다. A **datetime** 형식이 문자 데이터로 변환 되 고 스타일 3 적용 되는 형식 dd/mm/yy 데이터를 표시 하는 합니다. WHERE 절에는 **money** 유형은 문자열 비교 연산을 수행 하는 문자 형식으로 캐스팅 됩니다.
  
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
  
다음 예는 변환될 데이터 형식에서 해당 값이 너무 길면 데이터가 잘림을 보여 줍니다. 때문에 **uniqueidentifier** 형식은 36 자로 제한, 해당 길이 초과 하는 문자는 잘립니다.
  
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
  
## <a name="see-also"></a>참고 항목
[nchar 및 nvarchar&#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[데이터베이스 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  
