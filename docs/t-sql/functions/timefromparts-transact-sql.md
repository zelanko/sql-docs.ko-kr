---
title: TIMEFROMPARTS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2ff372996e307f02d1d434cadae36ea0d89115d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079023"
---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  지정한 전체 자릿수를 사용하여 지정한 시간에 대한 **time** 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>인수  
 *hour*  
 시간을 지정하는 정수 식입니다.  
  
 *minute*  
 분을 지정하는 정수 식입니다.  
  
 *초*  
 초를 지정하는 정수 식입니다.  
  
 *fractions*  
 소수 자릿수를 지정하는 정수 식입니다.  
  
 *전체 자릿수*  
 반환할 **time** 값의 전체 자릿수를 지정하는 정수 리터럴입니다.  
  
## <a name="return-types"></a>반환 형식  
 **time(** *precision* **)**  
  
## <a name="remarks"></a>Remarks  
 TIMEROMPARTS는 완전히 초기화된 시간 값을 반환합니다. 인수가 유효하지 않으면 오류가 발생합니다. 매개 변수에 Null이 포함되어 있으면 Null이 반환됩니다. 그러나 *precision* 인수가 Null일 경우에는 오류가 발생합니다.  
  
 *fractions* 인수는 *precision* 인수에 의존합니다. 예를 들어 *precision*이 7이면 각 소수 자릿수가 100나노초를 나타내고 *precision*이 3이면 각 소수 자릿수가 1밀리초를 나타냅니다. *precision*의 값이 0이면 *fractions*의 값도 0이어야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
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
 다음 예에서는 *fractions* 및 *precision* 매개 변수의 사용 방법을 설명합니다.  
  
1.  *fractions*의 값이 5이고 *precision*의 값이 1이면, *fractions*의 값은 1초의 5/10를 나타냅니다.  
  
2.  *fractions*의 값이 50이고 *precision*의 값이 2이면 *fractions*의 값은 1초의 50/100을 나타냅니다.  
  
3.  *fractions*의 값이 500이고 *precision*의 값이 3이면 *fractions*의 값은 1초의 500/1000을 나타냅니다.  
  
```sql  
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
  

