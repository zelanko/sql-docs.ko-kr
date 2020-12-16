---
description: ASIN(Transact-SQL)
title: ASIN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASIN_TSQL
- ASIN
dev_langs:
- TSQL
helpviewer_keywords:
- ASIN function
- sine
- arcsine
ms.assetid: 6256dd7d-83d5-486e-a933-1d59afc7e417
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1133bbf52506fb7732e7a835e60242a4c2e929c7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484315"
---
# <a name="asin-transact-sql"></a>ASIN(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

지정된 **float** 식을 사인 값으로 가지는 각도를 라디안 단위로 반환하는 기능입니다. 이를 **아크사인** 이라고도 합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ASIN ( float_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*float_expression*  
**float** 형식 또는 float로 암시적으로 변환할 수 있는 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. -1.00에서 1.00까지의 값만 유효합니다. 값이 이 범위를 벗어나면 NULL이 반환되고 ASIN에서 도메인 오류가 보고됩니다.
  
## <a name="return-types"></a>반환 형식
**float**
  
## <a name="examples"></a>예제  
이 예에서는 **float** 식을 받아서 지정된 각도의 ASIN 값을 반환합니다.
  
```sql
/* The first value will be -1.01. This fails because the value is   
outside the range.*/  
DECLARE @angle FLOAT  
SET @angle = -1.01  
SELECT 'The ASIN of the angle is: ' + CONVERT(VARCHAR, ASIN(@angle))  
GO  
  
-- The next value is -1.00.  
DECLARE @angle FLOAT  
SET @angle = -1.00  
SELECT 'The ASIN of the angle is: ' + CONVERT(VARCHAR, ASIN(@angle))  
GO  
  
-- The next value is 0.1472738.  
DECLARE @angle FLOAT  
SET @angle = 0.1472738  
SELECT 'The ASIN of the angle is: ' + CONVERT(VARCHAR, ASIN(@angle))  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-------------------------  
.Net SqlClient Data Provider: Msg 3622, Level 16, State 1, Line 3  
A domain error occurred.  
  
---------------------------------   
The ASIN of the angle is: -1.5708                          
  
(1 row(s) affected)  
  
----------------------------------   
The ASIN of the angle is: 0.147811                         
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
이 예에서는 1.00의 아크사인을 반환합니다.
  
```sql
SELECT ASIN(1.00) AS asinCalc;  
```  
  
허용 범위를 벗어난 값에 대해 아크사인을 요청하여 오류가 반환되는 예입니다.
  
```sql
SELECT ASIN(1.1472738) AS asinCalc;  
```  
  
## <a name="see-also"></a>참고 항목
[CEILING&#40;Transact-SQL&#41;](../../t-sql/functions/ceiling-transact-sql.md)  
[수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[SET ARITHIGNORE&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithignore-transact-sql.md)  
[SET ARITHABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)
  
  

