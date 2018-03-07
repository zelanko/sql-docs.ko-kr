---
title: DATETIME2FROMPARTS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ce109671228e82bc0f02e9920b2ef98c9bbcdb83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

반환 된 **datetime2** 지정한 전체 자릿수 하 고 지정 된 날짜 및 시간에 대 한 값입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>인수  
*연도*  
연도를 지정하는 정수 식입니다.
  
*월*  
월을 지정하는 정수 식입니다.
  
*일*  
일을 지정하는 정수 식입니다.
  
 *1 시간*  
시간을 지정하는 정수 식입니다.
  
*분* 분을 지정 하는 정수 식입니다.
  
*초*  
초를 지정하는 정수 식입니다.
  
*분수*  
소수 자릿수를 지정하는 정수 식입니다.
  
*전체 자릿수*  
정수 리터럴 자릿수를 지정 하는 **datetime2** 값을 반환할 수 있습니다.
  
## <a name="return-types"></a>반환 형식
**datetime2 (** *정밀도* **)**
  
## <a name="remarks"></a>주의  
**DATETIME2FROMPARTS** 는 완전히 초기화 된 반환 **datetime2** 값입니다. 인수가 유효하지 않으면 오류가 발생합니다. 필수 인수가 Null일 경우에는 Null이 반환됩니다. 그러나 경우는 *정밀도* 인수가 null 일 경우 다음 오류가 발생 합니다.
  
*분수* 인수에 따라 달라 집니다는 *정밀도* 인수입니다. 예를 들어 경우 *정밀도* 은 7, 다음 하는 경우 각 소수 자릿수가 100 나노초를 나타내고 *정밀도* 3 인 다음 각 소수 자릿수가 1 밀리초를 나타냅니다. 하는 경우의 값 *정밀도* 0의 값이 *분수* 또한 해야 0; 그렇지 않으면 오류가 발생 합니다.
  
이 함수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상 서버에 대해서는 원격으로 실행할 수 있지만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전 버전이 설치되어 있는 서버에 대해서는 원격으로 실행할 수 없습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>1. 소수 단위 초를 사용하지 않는 간단한 예  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>2. 소수 단위 초를 사용하는 예  
다음 예제에서는 *분수* 및 *정밀도* 매개 변수:
  
1.  때 *분수* 5 값 및 *정밀도* 에 값이 1 항목이 값 *분수* 5/10 초를 나타냅니다.  
  
2.  때 *분수* 50 값 및 *정밀도* 에 값이 2 항목이 값 *분수* 50/100 초를 나타냅니다.  
  
3.  때 *분수* 값이 500 및 *정밀도* 값은 값은 값 3 다음 *분수* 500/1000 초를 나타냅니다.  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[datetime2&#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  

