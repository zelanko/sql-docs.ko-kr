---
title: TIMEFROMPARTS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TIMEFROMPARTS_TSQL
- TIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- TIMEFROMPARTS function
ms.assetid: 786c65a1-2b3f-4e4b-82b6-4940d62f3801
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: e7cb7497251a0a61cff9f71c07d3c5d9e9028d5d
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  반환 된 **시간** 지정한 전체 자릿수 하 고 지정된 된 시간에 대 한 값입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>인수  
 *1 시간*  
 시간을 지정하는 정수 식입니다.  
  
 *분*  
 분을 지정하는 정수 식입니다.  
  
 *초*  
 초를 지정하는 정수 식입니다.  
  
 *분수*  
 소수 자릿수를 지정하는 정수 식입니다.  
  
 *전체 자릿수*  
 정수 리터럴 자릿수를 지정 하는 **시간** 값을 반환할 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **시간 (** *정밀도* **)**  
  
## <a name="remarks"></a>주의  
 TIMEROMPARTS는 완전히 초기화된 시간 값을 반환합니다. 인수가 유효하지 않으면 오류가 발생합니다. 매개 변수에 Null이 포함되어 있으면 Null이 반환됩니다. 그러나 경우는 *정밀도* 인수가 null 일 경우 다음 오류가 발생 합니다.  
  
 *분수* 인수에 따라 달라 집니다는 *정밀도* 인수입니다. 예를 들어 경우 *정밀도* 은 7, 다음 하는 경우 각 소수 자릿수가 100 나노초를 나타내고 *정밀도* 3 인 다음 각 소수 자릿수가 1 밀리초를 나타냅니다. 하는 경우의 값 *정밀도* 0의 값이 *분수* 또한 해야 0; 그렇지 않으면 오류가 발생 합니다.  
  
 이 함수는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 서버에 대해서는 원격으로 실행할 수 있지만 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전 버전의 서버에 대해서는 원격으로 실행할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>1. 소수 단위 초를 사용하지 않는 간단한 예  
  
```  
SELECT TIMEFROMPARTS ( 23, 59, 59, 0, 0 ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------------------  
23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>2. 소수 단위 초를 사용하는 예  
 다음 예제에서는 *분수* 및 *정밀도* 매개 변수:  
  
1.  때 *분수* 5 값 및 *정밀도* 에 값이 1 항목이 값 *분수* 5/10 초를 나타냅니다.  
  
2.  때 *분수* 50 값 및 *정밀도* 에 값이 2 항목이 값 *분수* 50/100 초를 나타냅니다.  
  
3.  때 *분수* 값이 500 및 *정밀도* 값은 값은 값 3 다음 *분수* 500/1000 초를 나타냅니다.  
  
```tsql  
SELECT TIMEFROMPARTS ( 14, 23, 44, 5, 1 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 50, 2 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 500, 3 );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------  
14:23:44.5  
  
(1 row(s) affected)  
  
----------------  
14:23:44.50  
  
(1 row(s) affected)  
  
----------------  
14:23:44.500  
  
(1 row(s) affected)  
```  
  


