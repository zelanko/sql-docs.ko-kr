---
title: decimal 및 numeric(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e487b66d13b4dcaba83219cc1fa6edf8eadc37d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530018"
---
# <a name="decimal-and-numeric-transact-sql"></a>decimal 및 numeric(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

> [!div class="nextstepaction"]
> [SQL Server 문서 개선에 참여해주세요.](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

전체 자릿수와 소수 자릿수가 고정된 숫자 데이터 형식입니다. decimal과 numeric은 동의어이며 서로 대체해 사용할 수 있습니다.
  
## <a name="arguments"></a>인수  
**decimal**[ **(**_p_[ **,**_s_] **)**] 및 **numeric**[ **(**_p_[ **,**_s_] **)**]  
고정 전체 자릿수 및 소수 자릿수 값입니다. 최대 전체 자릿수를 사용하는 경우 유효한 값은 - 10^38 + 1부터 10^38 - 1까지입니다. 국제 표준화 기구에서 정한 **decimal**의 동의어는 **dec** 및 **dec(**_p_, _s_**)** 입니다. **numeric**은 **decimal**과 기능적으로 동일합니다.
  
p(전체 자릿수)  
소수점 왼쪽과 오른쪽에 저장할 최대 전체 자릿수입니다. 전체 자릿수 값은 1에서 최대 전체 자릿수인 38 사이여야 합니다. 기본 전체 자릿수는 18입니다.
  
> [!NOTE]  
>  Informatica는 지정된 전체 자릿수 및 소수 자릿수와 상관없이 16 유효 자릿수만 지원합니다.  
  
*s* (소수 자릿수)  
소수점 오른쪽에 저장할 소수 자릿수입니다. *p*에서 이 숫자를 빼서 소수점 왼쪽의 최대 자릿수가 결정됩니다. 소수 자릿수 값은 0에서 *p* 사이여야 합니다. 소수 자릿수는 전체 자릿수를 지정한 경우에만 지정할 수 있습니다. 기본 소수 자릿수는 0입니다. 따라서 0 <= *s* \<= *p*입니다. 전체 자릿수에 따라 최대 저장소 크기가 달라집니다.
  
|전체 자릿수|스토리지 크기(바이트)|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica(SQL Server PDW Informatica Connector를 통해 연결)는 지정된 최대 자릿수 및 소수 자릿수와 상관없이 16 유효 자릿수만 지원합니다.  
  
## <a name="converting-decimal-and-numeric-data"></a>decimal 및 numeric 데이터 변환
**decimal** 및 **numeric** 데이터 형식의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 전체 자릿수와 소수 자릿수의 각 특정 조합을 다른 데이터 형식으로 간주합니다. 예를 들어 **decimal(5,5)** 및 **decimal(5,0)** 은 다른 데이터 형식으로 간주됩니다.
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 소수점이 있는 상수는 필요한 최소 전체 자릿수 및 소수 자릿수를 사용하여 **numeric** 데이터 값으로 자동 변환됩니다. 예를 들어 상수 12.345는 전체 자릿수가 5이고 소수 자릿수가 3인 **numeric** 값으로 변환됩니다.
  
**decimal** 또는 **numeric**에서 **float** 또는 **real**로 변환할 경우 전체 자릿수가 일부 손실될 수 있습니다. **int**, **smallint**, **tinyint**, **float**, **real**, **money** 또는 **smallmoney**에서 **decimal** 또는 **numeric**으로 변환할 경우 오버플로가 발생할 수 있습니다.
  
기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 숫자를 전체 자릿수 및 소수 자릿수가 낮은 **decimal** 또는 **numeric** 값으로 변환할 때 반올림을 사용합니다. 그러나 SET ARITHABORT 옵션이 ON이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오버플로가 발생할 때 오류를 일으킵니다. 전체 자릿수 및 소수 자릿수의 손실만으로는 오류가 발생하지 않습니다.
  
float 또는 real 값을 decimal 또는 numeric으로 변환하는 경우 10진수 값은 17자리를 넘을 수 없습니다. 5E-18보다 작은 모든 float 값은 항상 0으로 변환됩니다.
  
## <a name="examples"></a>예  
다음 예에서는 **decimal** 및 **numeric** 데이터 형식을 사용하여 테이블을 만듭니다.  값이 각 열에 삽입되고 SELECT 문을 사용해서 결과가 반환됩니다.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn decimal(5,2)  
,MyNumericColumn numeric(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>관련 항목:
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
