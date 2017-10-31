---
title: "전체 자릿수, 소수 자릿수 및 길이 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 557d7a5c45e9cc5a0839dfb4a1fdb0d08c2bf83f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="precision-scale-and-length-transact-sql"></a>전체 자릿수, 소수 자릿수 및 길이 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

전체 자릿수는 숫자의 모든 자릿수이고 소수 자릿수는 숫자에서 소수점 오른쪽에 있는 자릿수입니다. 예를 들어 123.45의 전체 자릿수는 5이고 소수 자릿수는 2입니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 기본 최대 전체 자릿수는 **숫자** 및 **10 진수** 데이터 형식에는 38입니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본 최대 전체 자릿수는 28입니다.
  
숫자 데이터 형식의 길이는 해당 숫자를 저장하는 데 사용된 바이트 수이고 문자열이나 유니코드 데이터 형식의 길이는 문자의 개수입니다. 에 대 한 길이 **이진**, **varbinary**, 및 **이미지** 데이터 형식을 바이트의 수입니다. 예를 들어 한 **int** 데이터 형식은 10 자리까지 지정할 수 있습니다, 4 바이트에 저장 되 고 소수점이 하를 허용 하지 않습니다. **int** 데이터 형식에는 전체 자릿수 10, 4, 길이 및 소수 자릿수가 0입니다.
  
두 개의 **char**, **varchar**, **이진**, 또는 **varbinary** 식을 연결 하면 결과 식의 길이의 8, 000 자 두 원본 식의 길이의 합 더 작은 쪽입니다.
  
두 개의 **nchar** 또는 **nvarchar** 식을 연결 하면 결과 식의 길이 4, 000 자 두 원본 식의 길이의 합, 더 작은 쪽입니다.
  
데이터 형식은 같지만 길이가 다른 두 식을 UNION, EXCEPT 또는 INTERSECT를 사용하여 비교하면 결과 길이는 두 식의 최대 길이가 됩니다.
  
전체 자릿수와 소수 외에도 숫자 데이터 형식의 **10 진수** 고정 됩니다. 데이터 형식이 동일한 두 식을 산술 연산자로 결합하면 결과는 해당 형식에 정의된 전체 자릿수와 소수 자릿수를 가진 동일한 데이터 형식이 됩니다. 다른 숫자 데이터 형식을 가진 두 식을 연산자로 결합하면 데이터 형식 우선 순위에 따라 결과의 데이터 형식이 정의됩니다. 결과는 해당 데이터 형식에 대해 정의된 전체 자릿수와 소수 자릿수를 갖습니다.
  
다음 표에서 어떻게 전체 자릿수와 소수 결과의 계산 되는지를 정의 작업의 결과 유형인 경우 **10 진수**합니다. 결과 **10 진수** 다음 중 하나가 true 이면 경우:
-   두 식이 모두 **10 진수**합니다.  
-   하나의 식이 **10 진수** 보다 우선 순위가 더 낮은 데이터 형식이 다른 및 **10 진수**합니다.  
  
피연산자 식은 전체 자릿수 p1과 소수 자릿수 s1을 가진 식 e1, 전체 자릿수 p2와 소수 자릿수 s2를 가진 식 e2로 표시합니다. 전체 자릿수와 소수 하지 않은 모든 식에 대 한 **10 진수** 전체 자릿수와 소수 식의 데이터 형식에 대해 정의 됩니다.
  
|연산|결과 전체 자릿수|결과 소수 자릿수 *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|e1 {UNION &#124; 제외 하 고 &#124; INTERSECT} e2|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\*결과 전체 자릿수 및 소수 자릿수 38의 최대값이 있어야 합니다. 결과 전체 자릿수가 38 보다 큰 경우 38 이며, 감소 하 고 해당 눈금에 잘리지 않도록 결과의 정수 부분을 하지 못하도록 감소 됩니다. 곱하기 또는 나누기와 같은 일부 경우 인수의 크기를 조정 하지 줄어듭니다 10 진수 정밀도 유지 하기 위해 있지만 오버플로 오류가 발생할 수 있습니다.

더하기 및 빼기 연산에서 필요한 `max(p1 – s1, p2 – s2)` 10 진수 숫자의 정수 부분을 저장 위치입니다. 즉, 저장할 충분 한 공간이 없을 경우 `max(p1 – s1, p2 – s2) < min(38, precision) – scale`, 중요 한 부분에 대 한 충분 한 공간을 제공 하는 소수 자릿수가 줄어듭니다. 결과 소수 자릿수가 `MIN(precision, 38) - max(p1 – s1, p2 – s2)`이므로 소수 부분 결과 소수 자릿수에 맞게 반올림 될 수 있습니다.

곱하기와 나누기 작업에서 필요한 `precision - scale` 결과의 정수 부분을 저장 위치입니다. 다음 규칙을 사용 하 여 눈금 줄어들 수 있습니다.
1.  결과 소수 자릿수가 줄어듭니다 `min(scale, 38 – (precision-scale))` 경우 필수적인 부분 이므로 32 보다 작은 보다 클 수 없습니다 `38 – (precision-scale)`합니다. 결과이 경우 반올림 될 수 있습니다.
1. 6 보다 작은 경우를 중요 한 부분 32 보다 큰 경우 소수 자릿수를 변경할 수 됩니다. 10 진수 (38, 배율)에 표시할 수 없을 경우 오버플로 오류가 발생할 수 있습니다이 경우 
1. 6 보다 큰 경우 및 중요 한 부분 32 보다 큰 경우 소수 자릿수 6으로 설정 됩니다. 이 경우 정수 부분과 소수 자릿수를 줄일 것 이며 결과 형식만 decimal(38,6) 합니다. 결과 6 소수 자릿수 반올림 될 수 있습니다 또는 없어서는 안 될 부분이 32 자리 숫자를 표시할 수 없을 경우 오버플로 오류가 발생 합니다.

## <a name="examples"></a>예
다음 식은 반환 결과 `0.00000090000000000` 결과에 넣을 수 때문에 반올림 되지 않고 `decimal(38,17)`:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
이 경우 전체 자릿수는 61 및 소수 자릿수는 40입니다.
중요 한 부분 (소수 자릿수가 = 21) 이므로 32 보다 작은 경우 (1) 곱하기 규칙에서 이며 눈금으로 계산 됩니다 `min(scale, 38 – (precision-scale)) = min(40, 38 – (61-40)) = 17`합니다. 결과 형식이 `decimal(38,17)`합니다.

다음 식은 반환 결과 `0.000001` 에 맞게 `decimal(38,6)`:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
이 경우 전체 자릿수는 61 및 소수 자릿수는 20 개입니다.
소수 자릿수가 6 자에서 정수 부분 보다 큼 (`precision-scale = 41`) 32 보다 큽니다. 즉 곱하기 규칙에서는 사용할 수 있는 경우 (3) 및 결과 형식이 `decimal(38,6)`합니다.

## <a name="see-also"></a>참고 항목
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

