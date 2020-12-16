---
description: ROUND(Transact-SQL)
title: ROUND(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ROUND_TSQL
- ROUND
dev_langs:
- TSQL
helpviewer_keywords:
- rounding expressions
- ROUND function [Transact-SQL]
ms.assetid: 23921ed6-dd6a-4c9e-8c32-91c0d44fe4b7
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 07513f58fef796c18a9ba92ffb59478f8f08b58d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462414"
---
# <a name="round-transact-sql"></a>ROUND(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

특정 길이나 전체 자릿수로 반올림한 숫자 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *numeric_expression*  
 **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 [expression](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 *length*  
 *numeric_expression* 을 반올림할 전체 자릿수입니다. *length* 는 **tinyint**, **smallint** 또는 **int** 형식의 식이어야 합니다. *length* 가 양수이면 *numeric_expression* 은 *length* 로 지정된 10진수 자리의 숫자로 반올림됩니다. *length* 가 음수이면 *numeric_expression* 은 *length* 로 지정된 소수점의 왼쪽에 반올림됩니다.  
  
 *function*  
 수행할 연산의 유형입니다. *function* 은 **tinyint**, **smallint** 또는 **int** 여야 합니다. *function* 이 생략되거나 값이 0(기본값)이면 *numeric_expression* 이 반올림됩니다. 0 이외의 값을 지정하면 *numeric_expression* 이 잘립니다.  
  
## <a name="return-types"></a>반환 형식  
 다음 데이터 형식을 반환합니다.  
  
|식 결과|반환 형식|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|**decimal** 및 **numeric** 범주(p, s)|**decimal(p, s)**|  
|**money** 및 **smallmoney** 범주|**money**|  
|**float** 및 **real** 범주|**float**|  
  
## <a name="remarks"></a>설명  
 ROUND는 항상 하나의 값을 반환합니다. *length* 가 음수이고 소수점 전의 자릿수보다 클 경우 ROUND는 0을 반환합니다.  
  
|예제|결과|  
|-------------|------------|  
|ROUND(748.58, -4)|0|  
  
 *length* 가 음수일 경우 ROUND는 데이터 형식에 관계없이 반올림된 *numeric_expression* 을 반환합니다.  
  
|예제|결과|  
|--------------|------------|  
|ROUND(748.58, -1)|750.00|  
|ROUND(748.58, -2)|700.00|  
|ROUND(748.58, -3)|748.58은 기본적으로 10진수(5,2)로 1000.00을 반환할 수 없기 때문에 산술 오버플로가 발행합니다.|  
|4자릿수까지 반올림하려면 입력 데이터 형식을 변경합니다. 예를 들면 다음과 같습니다.<br /><br /> `SELECT ROUND(CAST (748.58 AS decimal (6,2)),-3);`|1000.00|  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-round-and-estimates"></a>A. ROUND 및 어림값 사용  
 다음 예에서는 마지막 자릿수가 항상 어림값인 `ROUND`를 사용하는 두 개의 식을 보여 줍니다.  
  
```sql  
SELECT ROUND(123.9994, 3), ROUND(123.9995, 3);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -----------  
123.9990    124.0000      
```  
  
### <a name="b-using-round-and-rounding-approximations"></a>B. ROUND 사용 및 어림값 반올림  
 다음 예에서는 반올림과 어림값을 보여 줍니다.  
  
```  
SELECT ROUND(123.4545, 2), ROUND(123.45, -2);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
----------  ----------
123.4500    100.00
```
  
### <a name="c-using-round-to-truncate"></a>C. ROUND를 사용하여 자르기  
 다음 예에서는 두 개의 `SELECT` 문을 사용하여 반올림과 자르기 간의 차이를 보여 줍니다. 첫 번째 문은 결과를 반올림하고 두 번째 문은 결과를 자릅니다.  
  
```sql  
SELECT ROUND(150.75, 0);  
GO  
SELECT ROUND(150.75, 0, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
151.00  
  
(1 row(s) affected)  
  
--------  
150.00  
  
(1 row(s) affected)  
```
  
## <a name="see-also"></a>참고 항목  
 [CEILING&#40;Transact-SQL&#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR&#40;Transact-SQL&#41;](../../t-sql/functions/floor-transact-sql.md)   
 [수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
