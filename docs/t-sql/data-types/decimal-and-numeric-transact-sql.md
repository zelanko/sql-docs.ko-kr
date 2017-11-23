---
title: "decimal 및 numeric (Transact SQL) | Microsoft Docs"
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
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs: TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 614025c21f0f021a4b1ad3a193afec8f5115b845
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="decimal-and-numeric-transact-sql"></a>decimal 및 numeric(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

전체 자릿수와 소수 자릿수가 고정된 숫자 데이터 형식입니다. Decimal 및 numeric 동의어 이며 서로 바꿔 사용할 수 있습니다.
  
## <a name="arguments"></a>인수  
**10 진수**[ **(***p*[ **,***s*] **)**] 및 **숫자** [ **(***p*[ **,***s*] **)**]  
고정 전체 자릿수 및 소수 자릿수 값입니다. 최대 전체 자릿수를 사용하는 경우 유효한 값은 - 10^38 + 1부터 10^38 - 1까지입니다. ISO 동의어 **10 진수** 는 **dec** 및 **dec (***p*, *s***)**. **숫자** 기능적으로 **10 진수**합니다.
  
p(전체 자릿수)  
소수점 왼쪽과 오른쪽에 저장할 최대 전체 자릿수입니다. 전체 자릿수 값은 1에서 최대 전체 자릿수인 38 사이여야 합니다. 기본 전체 자릿수는 18입니다.
  
> [!NOTE]  
>  Informatica와 지정 된 소수 자릿수에 관계 없이 16 유효 자릿수를 지원 합니다.  
  
*s* (배율)  
소수점 오른쪽에 저장할 소수 자릿수입니다. 이 값에서 빼면 *p* 소수점의 왼쪽에 있는 숫자의 최대 수를 결정 합니다. 소수점 오른쪽에 저장할 수 있는 10진수의 최대 수입니다. 눈금에 0 ~ 사이의 값 이어야 합니다. *p*합니다. 소수 자릿수는 전체 자릿수를 지정한 경우에만 지정할 수 있습니다. 기본 소수 자릿수는 0; 따라서 0 < = *s* \< =  *p*합니다. 전체 자릿수에 따라 최대 저장소 크기가 달라집니다.
  
|전체 자릿수|저장소 크기(바이트)|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica (SQL Server PDW Informatica 커넥터를 통해 연결)와 지정 된 소수 자릿수에 관계 없이 16 유효 자릿수를 지원 합니다.  
  
## <a name="converting-decimal-and-numeric-data"></a>Decimal 및 numeric 데이터 변환
에 대 한는 **10 진수** 및 **숫자** 데이터 형식, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 각 특정 조합을 전체 자릿수 및 소수 자릿수의 다른 데이터 형식으로 간주 합니다. 예를 들어 **decimal(5,5)** 및 **decimal(5,0)** 데이터 형식이 서로 다른 것으로 간주 됩니다.
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 소수점이 있는 상수도 자동 변환 됩니다는 **숫자** 데이터 최소 전체 자릿수를 사용 하 여 값을 필요한 크기를 조정 합니다. 예를 들어 상수 12.345는 변환할는 **숫자** 5의 전체 자릿수 및 소수 자릿수가 3의 값입니다.
  
변환 **10 진수** 또는 **숫자** 를 **float** 또는 **실제** 자릿수 손실이 발생할 수 있습니다. 변환 **int**, **smallint**, **tinyint**, **float**, **실제**, **money** , 또는 **smallmoney** 을 **10 진수** 또는 **숫자** 오버플로가 발생할 수 있습니다.
  
기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 숫자를 변환할 때 반올림을 사용 하 여 한 **10 진수** 또는 **숫자** 낮은 자릿수 및 소수 자릿수 값입니다. 그러나 SET ARITHABORT 옵션이 ON이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오버플로가 발생할 때 오류를 일으킵니다. 전체 자릿수 및 소수 자릿수의 손실만으로는 오류가 발생하지 않습니다.
  
float 또는 real 값을 decimal 또는 numeric으로 변환하는 경우 10진수 값은 17자리를 넘을 수 없습니다. 5E-18보다 작은 모든 float 값은 항상 0으로 변환됩니다.
  
## <a name="examples"></a>예  
다음 예에서는 사용 하 여 테이블을 만듭니다는 **10 진수** 및 **숫자** 데이터 형식입니다.  값이 각 열에 삽입되고 SELECT 문을 사용해서 결과가 반환됩니다.
  
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
  
## <a name="see-also"></a>참고 항목
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
