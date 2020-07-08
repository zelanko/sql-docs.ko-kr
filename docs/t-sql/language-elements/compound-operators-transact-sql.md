---
title: 복합 연산자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators
- compound operators, described
ms.assetid: 5072fe91-02d3-42a7-831f-756eff714a17
author: rothja
ms.author: jroth
ms.openlocfilehash: 274eabcf6db0902f18bc8d6348e9b5e5a2314d12
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85706569"
---
# <a name="compound-operators-transact-sql"></a>복합 연산자(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  복합 연산자는 특정 연산을 실행하고 원래 값을 연산 결과로 설정합니다. 예를 들어 @x 변수가 35일 경우 @x += 2는 원래 값 @x에서 2를 더하고 @x를 새 값(37)으로 설정합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 다음과 같은 복합 연산자를 제공합니다.  
  
|연산자|추가 정보 링크|작업|  
|--------------|------------------------------|------------|  
|+=|[+=&#40;더하기 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)|원래 값에 특정 양을 더하고 원래 값을 연산 결과로 설정합니다.|  
|-=|[-=&#40;빼기 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)|원래 값에서 특정 양을 빼고 원래 값을 연산 결과로 설정합니다.|  
|*=|[&#42;=&#40;곱하기 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/multiply-equals-transact-sql.md)|특정 양으로 곱하고 원래 값을 연산 결과로 설정합니다.|  
|/=|[&#40;나누기 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)|특정 양으로 나누고 원래 값을 연산 결과로 설정합니다.|  
|%=|[모듈러스 대입&#40;Transact-SQL&#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)|특정 양으로 나누고 원래 값을 나머지로 설정합니다.|  
|&=|[&=&#40;비트 AND 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)|비트 AND를 수행하고 원래 값을 연산 결과로 설정합니다.|  
|^=|[^=&#40;배타적 비트 OR 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)|배타적 비트 OR를 수행하고 원래 값을 연산 결과로 설정합니다.|  
|&#124;=|[&#124;=&#40;비트 OR 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)|비트 OR를 수행하고 원래 값을 연산 결과로 설정합니다.|  
  
## <a name="syntax"></a>구문  
  
```  
  
expression operator expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 숫자 범주의 데이터 형식 중 하나로 된 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="result-types"></a>결과 형식  
 우선 순위가 높은 인수의 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
 자세한 내용은 각 연산자와 관련된 항목을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 복합 연산을 보여 줍니다.  
  
```  
DECLARE @x1 int = 27;  
SET @x1 += 2 ;  
SELECT @x1 AS Added_2;  
  
DECLARE @x2 int = 27;  
SET @x2 -= 2 ;  
SELECT @x2 AS Subtracted_2;  
  
DECLARE @x3 int = 27;  
SET @x3 *= 2 ;  
SELECT @x3 AS Multiplied_by_2;  
  
DECLARE @x4 int = 27;  
SET @x4 /= 2 ;  
SELECT @x4 AS Divided_by_2;  
  
DECLARE @x5 int = 27;  
SET @x5 %= 2 ;  
SELECT @x5 AS Modulo_of_27_divided_by_2;  
  
DECLARE @x6 int = 9;  
SET @x6 &= 13 ;  
SELECT @x6 AS Bitwise_AND;  
  
DECLARE @x7 int = 27;  
SET @x7 ^= 2 ;  
SELECT @x7 AS Bitwise_Exclusive_OR;  
  
DECLARE @x8 int = 27;  
SET @x8 |= 2 ;  
SELECT @x8 AS Bitwise_OR;  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
