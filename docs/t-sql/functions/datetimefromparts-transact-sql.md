---
title: DATETIMEFROMPARTS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 68a00daa99ee13d8d55044b0ce0849c30eec530f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43068284"
---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

이 함수는 지정된 날짜 및 시간 인수에 대한 **datetime** 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
```  
  
## <a name="arguments"></a>인수  
*year*  
년을 지정하는 정수 식입니다.
  
*month*  
월을 지정하는 정수 식입니다.
  
*day*  
일을 지정하는 정수 식입니다.
  
*hour*  
시간을 지정하는 정수 식입니다.
  
*minute*  
분을 지정하는 정수 식입니다.
  
*초*  
초를 지정하는 정수 식입니다.
  
*milliseconds*  
밀리초를 지정하는 정수 식입니다.
  
## <a name="return-types"></a>반환 형식
**datetime**
  
## <a name="remarks"></a>Remarks  
`DATETIMEFROMPARTS`는 완전히 초기화된 **datetime** 값을 반환합니다. `DATETIMEFROMPARTS`는 적어도 하나 이상의 필수 인수에 잘못된 값이 있는 경우 오류를 발생시킵니다. `DATETIMEFROMPARTS`는 적어도 하나 이상의 필수 인수에 null 값이 있는 경우 null을 반환합니다.
  
이 함수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 서버 이상에 대한 원격 처리를 지원합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전 버전이 설치되어 있는 서버에 대해서는 원격 처리를 지원하지 않습니다.
  
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
  
## <a name="see-also"></a>관련 항목:
[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)
  
  

