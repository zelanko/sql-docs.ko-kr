---
title: DATETIMEFROMPARTS (Transact SQL) | Microsoft Docs
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
- DATETIMEFROMPARTS_TSQL
- DATETIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEFROMPARTS function
ms.assetid: 6008148b-bf75-4c98-9392-68a89fa0711c
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 12c4107410cb0c482a24e40622d1858be9f7d1b2
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

반환 된 **datetime** 지정 된 날짜 및 시간에 대 한 값입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
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
  
*분*  
분을 지정하는 정수 식입니다.
  
*초*  
초를 지정하는 정수 식입니다.
  
*시간 (밀리초)*  
밀리초를 지정하는 정수 식입니다.
  
## <a name="return-types"></a>반환 형식
**datetime**
  
## <a name="remarks"></a>주의  
**DATETIMEFROMPARTS** 는 완전히 초기화 된 반환 **datetime** 값입니다. 인수가 유효하지 않으면 오류가 발생합니다. 필수 인수가 Null일 경우에는 Null이 반환됩니다.
  
이 함수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상 서버에 대해서는 원격으로 실행할 수 있지만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전 버전이 설치되어 있는 서버에 대해서는 원격으로 실행할 수 없습니다.
  
## <a name="examples"></a>예  
  
```sql
SELECT DATETIMEFROMPARTS ( 2010, 12, 31, 23, 59, 59, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[날짜/시간 &#40; Transact SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)
  
  


