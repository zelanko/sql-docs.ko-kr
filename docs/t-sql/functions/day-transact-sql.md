---
title: DAY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DAY_TSQL
- DAY
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 98e0a1f548fdec917f265595a4a06ec795c5f37e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="day-transact-sql"></a>DAY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정 된 일 (월의 일)을 나타내는 정수를 반환 *날짜*합니다.
  
모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>인수  
*date*  
식으로 확인 될 수 있는 한 **시간**, **날짜**, **smalldatetime**, **datetime**, **datetime2**, 또는 **datetimeoffset** 값입니다. *날짜* 인수는 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴이 될 수 있습니다.
  
## <a name="return-type"></a>반환 형식  
**int**
  
## <a name="return-value"></a>반환 값  
과 동일한 값을 반환 하는 일 [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**일**, *날짜*).
  
경우 *날짜* 에 시간 부분만 반환 값은 1, 기본 날짜 하나만 포함 됩니다.
  
## <a name="examples"></a>예  
다음 문은 `30`을 반환합니다. 이는 일 수입니다.
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
다음 문은 `1900, 1, 1`을 반환합니다. 에 대 한 인수 *날짜* 수 `0`합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `0`을 1900년 1월 1일로 해석합니다.
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
다음 예에서는 반환 `30`합니다. 이는 일 수입니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP 1 DAY('2010-07-30T01:01:01.1234')   
FROM dbo.DimCustomer;  
```  
  
다음 예에서는 반환 `1900, 1, 1`합니다. 에 대 한 인수 *날짜* 수 `0`합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `0`을 1900년 1월 1일로 해석합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0) FROM dbo.DimCustomer;  
```  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



