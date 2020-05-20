---
title: 전체 자릿수, 소수 자릿수 및 길이(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], length
- data types [SQL Server], scale
- precision [SQL Server], data types
- lengths [SQL Server], data types
- number of digits
- scale [SQL Server]
- scale [SQL Server], data types
- data types [SQL Server], precision
ms.assetid: fbc9ad2c-0d3b-4e98-8fdd-4d912328e40a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 65154f6e4ffd67a207db9a3b6c5044710249c1eb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71682057"
---
# <a name="precision-scale-and-length-transact-sql"></a>전체 자릿수, 소수 자릿수 및 길이(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

전체 자릿수는 숫자의 모든 자릿수이고 소수 자릿수는 숫자에서 소수점 오른쪽에 있는 자릿수입니다. 예를 들어 123.45의 전체 자릿수는 5이고 소수 자릿수는 2입니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 **숫자** 및 **10진수** 데이터 형식의 기본 최대 전체 자릿수는 38입니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본 최대 전체 자릿수는 28입니다.
  
숫자 데이터 형식의 길이는 해당 숫자를 저장하는 데 사용된 바이트 수이고 varchar와 char에서 문자열의 길이는 바이트 수입니다. nvarchar와 nchar에서 문자열의 길이는 바이트 쌍 수입니다. **binary**, **varbinary** 및 **image** 데이터 유형의 길이는 바이트 수입니다. 예를 들어 **int** 데이터 형식은 10자리까지 지정할 수 있고 4바이트로 저장되며 소수점은 허용되지 않습니다. **int** 데이터 형식의 전체 자릿수는 10이고 길이는 4, 소수 자릿수는 0입니다.
  
**char**, **varchar**, **binary** 또는 **varbinary** 식 2개를 연결하는 경우 결과 식의 길이는 두 원본 식의 길이를 합한 값으로 최대 8,000바이트입니다.
  
**nchar** 또는 **nvarchar** 식 2개를 연결하는 경우 결과 식의 길이는 두 원본 식의 길이를 합한 값으로 최대 4,000바이트 쌍입니다.
  
UNION, EXCEPT 또는 INTERSECT를 사용하여 데이터 형식은 같지만 길이가 다른 두 식을 비교할 때 결과 길이는 두 식의 더 긴 길이가 됩니다.
  
**10진수**를 제외한 숫자 데이터 형식의 전체 자릿수와 소수 자릿수는 고정되어 있습니다. 데이터 형식이 동일한 두 식을 산술 연산자로 결합할 때 결과는 해당 형식에 정의된 전체 자릿수와 소수 자릿수를 가진 동일한 데이터 형식이 됩니다. 다른 숫자 데이터 형식을 가진 두 식을 연산자로 결합하면 데이터 형식 우선 순위에 따라 결과의 데이터 형식이 정의됩니다. 결과는 해당 데이터 형식에 대해 정의된 전체 자릿수와 소수 자릿수를 갖습니다.
  
다음 표에서는 연산의 결과가 **10진수** 형식일 경우 결과의 전체 자릿수와 소수 자릿수를 계산하는 방법을 정의합니다. 다음 중 하나일 때 결과는 **10진수**입니다.
-   두 식은 모두 **10진수**입니다.  
-   한 식이 **10진수**이고 다른 식이 **10진수**보다 선행 규칙이 낮은 데이터 형식일 경우  
  
피연산자 식은 전체 자릿수 p1과 소수 자릿수 s1을 가진 식 e1, 전체 자릿수 p2와 소수 자릿수 s2를 가진 식 e2로 표시합니다. **10진수**가 아닌 모든 식의 전체 자릿수와 소수 자릿수는 해당 식의 데이터 형식에 대해 정의된 전체 자릿수와 소수 자릿수입니다. 함수 max(a,b)는 "a" 또는 "b"의 더 큰 값을 사용합니다. 마찬가지로 min(a,b)은 "a" 또는 "b"의 더 작은 값을 사용합니다.
  
|작업(Operation)|결과 전체 자릿수|결과 소수 자릿수 *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|e1 { UNION &#124; EXCEPT &#124; INTERSECT } e2|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\* 결과 전체 자릿수와 소수 자릿수의 최대값은 38입니다. 결과 전체 자릿수가 38보다 크면 38로 줄어들고 결과의 정수 부분이 잘리지 않도록 해당 소수 자릿수가 줄어듭니다. 곱하기나 나누기 같은 일부의 경우에는 오버플로 오류가 발생할 수 있지만 소수점 이하 자릿수를 유지하기 위해 소수 자릿수가 줄어들지 않습니다.

더하기 및 빼기 연산에서 10진수의 정수 부분을 저장할 `max(p1 - s1, p2 - s2)` 장소가 필요합니다. `max(p1 - s1, p2 - s2) < min(38, precision) - scale`을 저장할 공간이 충분하지 않으면 소수 자릿수는 정수 부분에 충분한 공간을 제공하도록 줄어듭니다. 결과 소수 자릿수는 `MIN(precision, 38) - max(p1 - s1, p2 - s2)`이므로 소수 부분은 결과 소수 자릿수에 맞게 반올림될 수 있습니다.

곱하기 및 나누기 연산에서 결과의 정수 부분을 저장하기 위해 `precision - scale` 장소가 필요합니다. 다음 규칙을 사용하여 소수 자릿수를 줄일 수 있습니다.
1.  정수 부분이 32보다 작으면 결과적인 소수 자릿수가 `38 - (precision-scale)`보다 클 수 없으므로 `min(scale, 38 - (precision-scale))`로 줄어듭니다. 이 경우 결과가 반올림 될 수도 있습니다.
1. 6보다 작고 정수 부분이 32보다 큰 경우 소수 자릿수는 변경되지 않습니다. 이 경우 10진수(38, 소수 자릿수)에 맞지 않아 오버플로 오류가 발생할 수 있습니다. 
1. 6보다 크고 정수 부분이 32보다 큰 경우 소수 자릿수는 6으로 설정됩니다. 이 경우 정수 부분과 소수 자릿수 모두 줄어들 수도 있고 결과 형식은 10진수(38,6)입니다. 정수 부분이 32 자릿수에 맞지 않으면 결과가 소수점 이하 6 자리로 반올림되거나 오버플로 오류가 발생합니다.

## <a name="examples"></a>예
다음 표현식은 결과가 `decimal(38,17)`에 맞을 수 있으므로 결과 `0.00000090000000000`을 반올림하지 않고 반환합니다.
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
이 경우 전체 자릿수는 61이고 소수 자릿수는 40입니다.
정수 부분(전체 자릿수-소수 자릿수 = 21)은 32보다 작으므로 이 경우에는 곱하기 규칙에서 case(1)이고 소수 자릿수는 `min(scale, 38 - (precision-scale)) = min(40, 38 - (61-40)) = 17`로 계산됩니다. 결과 형식은 `decimal(38,17)`입니다.

다음 식은 결과 `0.000001`을 `decimal(38,6)`에 맞게 반환합니다.
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
이 경우 전체 자릿수는 61이고 소수 자릿수는 20입니다.
소수 자릿수는 6보다 크고 정수 부분은(`precision-scale = 41`)은 32보다 큽니다. 이 경우는 곱하기 규칙에서 case(3)이고 결과 형식은 `decimal(38,6)`입니다.

## <a name="see-also"></a>참고 항목
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
