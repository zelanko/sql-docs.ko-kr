---
title: '@@DATEFIRST (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SET DATEFIRST
- first day of week [SQL Server]
- dates [SQL Server], first day of week
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- date and time [SQL Server], DATEFIRST
- DATEFIRST option [SQL Server]
- date and time [SQL Server], @@DATEFIRST
- weekdays [SQL Server]
- '@@DATEFIRST function [SQL Server]'
- functions [SQL Server], date and time
- options [SQL Server], date
ms.assetid: a178868e-49d5-4bd5-a5e2-1283409c8ce6
caps.latest.revision: "46"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fc8cff9f51841d085314f8100550aa35a80a4463
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40datefirst-transact-sql"></a>&#x40;&#x40; DATEFIRST (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

세션에 대 한 현재 값을 반환 합니다. [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)합니다.
  
모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
@@DATEFIRST  
```  
  
## <a name="return-type"></a>반환 형식  
**tinyint**
  
## <a name="remarks"></a>주의  
SET DATEFIRST는 주의 시작 요일을 지정합니다. 미국 영어 기본값은 7, 일요일입니다.
  
이 언어 설정은 데이터베이스에 저장하기 위해 문자열을 날짜 값으로 변환할 때 문자열의 해석, 그리고 데이터베이스에 저장되는 날짜 값의 표시에 영향을 미칩니다. 이 설정은 날짜 데이터의 저장소 형식에는 영향을 주지 않습니다. 다음 예에서는 언어를 먼저 `Italian`으로 설정합니다. `SELECT @@DATEFIRST;` 문은 `1`을 반환합니다. 그런 다음 언어가 `us_english`로 설정됩니다. `SELECT @@DATEFIRST;` 문은 `7`을 반환합니다.
  
```sql
SET LANGUAGE Italian;  
GO  
SELECT @@DATEFIRST;  
GO  
SET LANGUAGE us_english;  
GO  
SELECT @@DATEFIRST;  
```  
  
## <a name="examples"></a>예  
다음 예에서는 주의 시작 요일을 `5`(금요일)로 설정하고 현재 날짜인 `Today`를 토요일로 가정합니다. `SELECT` 문은 주의 현재 날짜의 `DATEFIRST` 값과 현재 날짜 번호를 반환합니다.
  
```sql
SET DATEFIRST 5;  
SELECT @@DATEFIRST AS 'First Day'  
    ,DATEPART(dw, SYSDATETIME()) AS 'Today';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
First Day         Today  
----------------  --------------  
5                 2  
```  
  
## <a name="example"></a>예제
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>참고 항목
[구성 함수 &#40; Transact SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  

