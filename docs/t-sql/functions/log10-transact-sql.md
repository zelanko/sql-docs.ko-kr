---
description: LOG10(Transact-SQL)
title: LOG10(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LOG10
- LOG10_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- LOG10 function
- base-10 logarithms
- logarithm of expression
ms.assetid: 1eb7fb34-1937-4a39-a936-f5c0c7c7e06f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4b4ceb286ddb1e90ebd5bd703a741f34a6cdd8bd
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88467981"
---
# <a name="log10-transact-sql"></a>LOG10(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정된 **float** 식의 상용 로그를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
LOG10 ( float_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *float_expression*  
 **float** 형식 또는 **float** 로 암시적으로 변환되는 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>설명  
 LOG10과 POWER 함수는 서로 역함수 관계에 있습니다. 예를 들어 10 ^ LOG10(*n*) = *n* 입니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-calculating-the-base-10-logarithm-for-a-variable"></a>A. 변수에 대한 상용 로그 계산  
 다음 예에서는 지정된 변수의 `LOG10`을 계산하는 방법을 보여 줍니다.  
  
```sql  
DECLARE @var FLOAT;  
SET @var = 145.175643;  
SELECT 'The LOG10 of the variable is: ' + CONVERT(VARCHAR,LOG10(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The LOG10 of the variable is: 2.16189      
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-result-of-raising-a-base-10-logarithm-to-a-specified-power"></a>B. 상용 로그를 지정된 거듭제곱으로 올린 결과 계산  
 다음 예에서는 상용 로그를 지정된 거듭제곱으로 올린 결과를 반환하는 방법을 보여 줍니다.  
  
```sql  
SELECT POWER (10, LOG10(5));   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------  
5  
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-base-10-logarithm-for-a-value"></a>3. 값에 대한 기본 10 로그 계산  
 다음 예에서는 지정된 값의 `LOG10`을 계산하는 방법을 보여 줍니다.  
  
```sql  
SELECT LOG10(145.175642);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-------------------  
2.16
```  
  
## <a name="see-also"></a>참고 항목  
 [수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [POWER &#40;Transact-SQL&#41;](../../t-sql/functions/power-transact-sql.md)   
 [LOG &#40;Transact-SQL&#41;](../../t-sql/functions/log-transact-sql.md)  
  
  

