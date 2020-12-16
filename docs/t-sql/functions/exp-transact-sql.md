---
description: EXP(Transact-SQL)
title: EXP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EXP_TSQL
- EXP
dev_langs:
- TSQL
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 5a9b8c52-6fb6-4e33-8b02-a878785b2f51
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ef214d08fcb57514e3cabef3a35649967c3e719
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481994"
---
# <a name="exp-transact-sql"></a>EXP(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정한 **float** 식의 지수 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
EXP ( float_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *float_expression*  
 **float** 형식 또는 **float** 로 암시적으로 변환되는 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>설명  
 상수 **e** 는 자연 로그의 밑이며 대략적인 값은 2.718281...입니다.  
  
 숫자의 지수는 해당 숫자의 거듭제곱으로 올려진 **e** 입니다. 예를 들어 EXP(1.0) = e^1.0 = 2.71828182845905이며 EXP(10) = e^10 = 22026.4657948067입니다.  
  
 숫자의 자연 로그 값을 계산하고 다시 그 값의 지수를 계산하면 결국 원래 숫자가 됩니다. EXP (LOG (*n*)) = *n*. 마찬가지로 숫자의 지수를 계산하고 다시 그 값의 자연 로그 값을 구하면 원래 숫자가 됩니다. LOG (EXP (*n*)) = *n*.  
  
## <a name="examples"></a>예제  
  
### <a name="a-finding-the-exponent-of-a-number"></a>A. 숫자의 지수 찾기  
 다음 예에서는 변수를 선언하고 텍스트 설명과 함께 지정된 변수(`10`)의 지수 값을 반환하는 방법을 보여 줍니다.  
  
```sql  
DECLARE @var FLOAT  
SET @var = 10  
SELECT 'The EXP of the variable is: ' + CONVERT(VARCHAR, EXP(@var))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------------------------------  
The EXP of the variable is: 22026.5  
(1 row(s) affected)  
```  
  
### <a name="b-finding-exponentials-and-natural-logarithms"></a>B. 지수 및 자연 로그 찾기  
 다음 예에서는 `20`의 자연 로그 값을 구한 후 그 값의 지수 값을 계산하고, 다시 `20`의 지수 값을 구한 후 그 값의 자연 로그 값을 계산하여 반환합니다. 이 함수는 서로 역함수 관계에 있으며 두 함수의 반환 값은 모두 `20`입니다.  
  
```sql  
SELECT EXP(LOG(20)), LOG(EXP(20))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------- ----------------------  
20                     20  
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-finding-the-exponent-of-a-number"></a>C. 숫자의 지수 찾기  
 다음 예에서는 지정한 값(`10`)의 지수 값을 반환합니다.  
  
```sql  
SELECT EXP(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------  
22026.4657948067  
```  
  
### <a name="d-finding-exponential-values-and-natural-logarithms"></a>D. 지수 값 및 자연 로그 찾기  
 다음 예에서는 `20`의 자연 로그 값을 구한 후 그 값의 지수 값을 계산하고, 다시 `20`의 지수 값을 구한 후 그 값의 자연 로그 값을 계산하여 반환합니다. 이 함수는 서로 역함수 관계에 있으며 두 함수의 반환 값은 모두 `20`입니다.  
  
```sql  
SELECT EXP( LOG(20)), LOG( EXP(20));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------- -----------------  
20                  20  
```  
  
## <a name="see-also"></a>참고 항목  
 [수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [LOG &#40;Transact-SQL&#41;](../../t-sql/functions/log-transact-sql.md)   
 [LOG10&#40;Transact-SQL&#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  

