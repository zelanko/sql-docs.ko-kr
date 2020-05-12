---
title: DAY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7ba1de859272254f4667cc5bb12aa836cfb1fe90
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823187"
---
# <a name="day-transact-sql"></a>DAY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 지정된 *date*의 일(월의 일)을 나타내는 정수를 반환합니다.
  
모든 [의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;[!INCLUDE[tsql](../../includes/tsql-md.md)]을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>인수  
*date*  
다음 데이터 형식 중 하나를 확인하는 식입니다.

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

*date*의 경우 `DAY`은 열 식, 식, 문자열 리터럴 또는 사용자 정의 변수를 허용합니다.
  
## <a name="return-type"></a>반환 형식  
**int**
  
## <a name="return-value"></a>Return Value  
DAY는 [DATEPART](../../t-sql/functions/datepart-transact-sql.md)(**day**, *date*)와 같은 값을 반환합니다.
  
*date*에 시간 부분만 포함된 경우 `DAY`는 기본 일인 1을 반환합니다.
  
## <a name="examples"></a>예  
이 명령문은 일 수인 `30`을 반환합니다.
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
이 명령문은 `1900, 1, 1`을 반환합니다. *날짜* 인수에는 `0`의 숫자 값이 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `0`을 1900년 1월 1일로 해석합니다.
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


