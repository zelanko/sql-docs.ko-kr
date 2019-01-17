---
title: 연산자 우선 순위(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], precedence
- operator precedence [Transact-SQL]
- order of operator execution [Transact-SQL]
- precedence [SQL Server], operators
ms.assetid: f04d2439-6fff-4e4c-801f-cc62faef510a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 933212da81784d7d186fc6ef7c0cdfaa4edab24b
ms.sourcegitcommit: 7ead3a042d369315fc83a9ccc3d74f62e7b05bc0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54012319"
---
# <a name="operator-precedence-transact-sql"></a>연산자 우선 순위(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  복합 식에 여러 개의 연산자가 있을 때는 연산자 우선 순위에 따라 연산자 실행 순서가 결정됩니다. 실행 순서는 결과 값에 중대한 영향을 줄 수 있습니다.  
  
 다음 표에서는 연산자 우선 순위를 보여 줍니다. 높은 수준의 연산자는 낮은 수준의 연산자 보다 먼저 평가됩니다(다음 표에서 1은 최고 수준이고 8은 가장 낮은 수준임).
  
|Level|연산자|  
|-----------|---------------|  
|1|~ (비트 NOT)|  
|2|*(곱하기), /(나누기), %(계수)|  
|3|+(양수), -(음수), +(더하기), +(연결), -(빼기), &(비트 AND), ^(비트 전용 OR), &#124;(비트 OR)|  
|4|=, >, \<, >=, <=, <>, !=, !>, !< (비교 연산자)|  
|5|NOT|  
|6|AND|  
|7|ALL, ANY, BETWEEN, IN, LIKE, OR, SOME|  
|8|=(할당)|  
  
 한 식에서 두 연산자의 연산자 우선 순위 수준이 같은 경우에는 식에서의 위치를 기준으로 왼쪽에서 오른쪽 순으로 계산됩니다. 예를 들어 다음 `SET` 문에 사용된 식에서 빼기 연산자는 더하기 연산자보다 먼저 계산됩니다.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 4 - 2 + 27;  
-- Evaluates to 2 + 27 which yields an expression result of 29.  
SELECT @MyNumber;  
```  
  
 괄호를 사용하면 식에서 연산자의 정의된 우선 순위를 바꿀 수 있습니다. 괄호 안의 모든 연산자가 먼저 계산되어 단일한 값을 만들면 괄호 밖의 다른 연산자가 그 값을 사용하게 됩니다.  
  
 예를 들어 다음 `SET` 문에 사용된 식에서 곱하기 연산자의 우선 순위가 더하기 연산자보다 높으므로 먼저 평가되어 식 결과가 `13`이 됩니다.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * 4 + 5;  
-- Evaluates to 8 + 5 which yields an expression result of 13.  
SELECT @MyNumber;  
```  
  
 다음 `SET` 문에서 사용된 식에서는 괄호 때문에 더하기가 먼저 수행되어 식 결과가 `18`이 됩니다.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + 5);  
-- Evaluates to 2 * 9 which yields an expression result of 18.  
SELECT @MyNumber;  
```  
  
 식에 중첩된 괄호가 있는 경우에는 가장 안쪽의 중첩 식이 먼저 계산됩니다. 중첩된 괄호가 있는 다음 예에서는 `5 - 3` 식이 가장 안쪽에 중첩된 괄호 안에 있습니다. 이 식의 결과 값은 `2`입니다. 그런 다음 더하기 연산자(`+`)가 이 결과를 `4`에 더하여 값이 `6`이 됩니다. 마지막으로 `6`에 `2`가 곱해져 식 결과는 `12`가 됩니다.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + (5 - 3) );  
-- Evaluates to 2 * (4 + 2) which then evaluates to 2 * 6, and   
-- yields an expression result of 12.  
SELECT @MyNumber;  
```  
  
## <a name="see-also"></a>참고 항목  
 [논리 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
