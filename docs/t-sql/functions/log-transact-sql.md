---
title: "로그 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOG
- LOG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- logarithm of expression
- LOG function
ms.assetid: f7c39511-cd84-4362-93ba-0d93655217ee
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 7918cb0d2832e88f3e4218b98c7f606f559f2e4e
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="log-transact-sql"></a>LOG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정 된 자연 로그를 반환 **float** 에 식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
LOG ( float_expression [, base ] )  
```  
  
```  
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LOG ( float_expression )  
```  
  
## <a name="arguments"></a>인수  
 *float_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 형식의 **float** 또는 암시적으로 변환할 수 있는 형식의 **float**합니다.  
  
 *자료*  
 로그 밑을 설정하는 선택적 정수 인수입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>주의  
 기본적으로 **log ()** 자연 로그를 반환 합니다. 부터는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 선택적인을 사용 하 여 다른 값으로는 로그의 밑수를 변경할 수 있습니다 *기본* 매개 변수입니다.  
  
 자연 로그의 기본 로그는 **e**여기서 **e** 는 무리 상수 대략 2.718281828과 같은 같습니다.  
  
 숫자의 지 수 자연 로그는 번호 자체: 로그 (EXP (  *n*  )) =  *n* 합니다. 숫자의 자연 로그의 지 수는 번호 자체: EXP (로그 (  *n*  )) =  *n* 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calculating-the-logarithm-for-a-number"></a>1. 수의 로그를 계산합니다.  
 다음 예에서는 계산 된 `LOG` 지정 된 **float** 식입니다.  
  
```  
DECLARE @var float = 10;  
SELECT 'The LOG of the variable is: ' + CONVERT(varchar, LOG(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------  
The LOG of the variable is: 2.30259  
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-logarithm-of-the-exponent-of-a-number"></a>2. 수의 지수에 대한 로그를 계산합니다.  
 다음 예에서는 수의 지수에 대한 `LOG`를 계산합니다.  
  
```  
SELECT LOG (EXP (10));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------  
10  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-logarithm-for-a-number"></a>3. 숫자에 대 한 로그 계산  
 다음 예에서는 계산 된 `LOG` 지정 된 **float** 식입니다.  
  
```  
SELECT LOG(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------`  
  
 2.30
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [EXP &#40; Transact SQL &#41;](../../t-sql/functions/exp-transact-sql.md)   
 [LOG10 &#40; Transact SQL &#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  


