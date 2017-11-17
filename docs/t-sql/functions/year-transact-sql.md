---
title: "연도 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- YEAR
- YEAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server], years
- date and time [SQL Server], YEAR
- functions [SQL Server], date and time
- YEAR function [SQL Server]
- dateparts [SQL Server], year
ms.assetid: 74aa7ccc-8575-4018-80cf-14aeca379687
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 80a38599ae04209d0f8e479b8cbad16d39bef31a
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="year-transact-sql"></a>YEAR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정 된 연도 나타내는 정수를 반환 *날짜*합니다.  
  
 모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
YEAR ( date )  
```  
  
## <a name="arguments"></a>인수  
 *date*  
 식으로 확인 될 수 있는 한 **시간**, **날짜**, **smalldatetime**, **datetime**, **datetime2**, 또는 **datetimeoffset** 값입니다. *날짜* 인수는 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴이 될 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>반환 값  
 과 동일한 값을 반환 하는 연도 [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**연도**, *날짜*).  
  
 경우 *날짜* 만 시간 부분만 포함 된 경우 반환 값은 1900 년 기본 연도입니다.  
  
## <a name="examples"></a>예  
 다음 문은 `2010`을 반환합니다. 이는 연도입니다.  
  
```  
SELECT YEAR('2010-04-30T01:01:01.1234567-07:00');  
```  
  
 다음 문은 `1900, 1, 1`을 반환합니다. 에 대 한 인수 *날짜* 수 `0`합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `0`을 1900년 1월 1일로 해석합니다.  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 문은 `1900, 1, 1`을 반환합니다. 에 대 한 인수 *날짜* 수 `0`합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `0`을 1900년 1월 1일로 해석합니다.  
  
```  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


