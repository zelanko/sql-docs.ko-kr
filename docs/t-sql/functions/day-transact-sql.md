---
title: DAY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8c248e735b25dbdbc2f7bd263698007acfc8600e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="day-transact-sql"></a>DAY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정된 *date*의 일(해당 월의 일) 부분을 나타내는 정수를 반환합니다
  
모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>인수  
*date*  
**time**, **date**, **smalldatetime**, **datetime**, **datetime2** 또는 **datetimeoffset** 값으로 확인할 수 있는 식입니다. *date* 인수는 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다.
  
## <a name="return-type"></a>반환 형식  
**int**
  
## <a name="return-value"></a>반환 값  
DAY는 [DATEPART](../../t-sql/functions/datepart-transact-sql.md)(**day**, *date*)와 같은 값을 반환합니다.
  
*date*에 시간 부분만 포함된 경우 기본 일인 1이 반환됩니다.
  
## <a name="examples"></a>예  
다음 문은 `30`을 반환합니다. 이는 일 수입니다.
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
다음 문은 `1900, 1, 1`을 반환합니다. *date*의 인수는 숫자 `0`입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `0`을 1900년 1월 1일로 해석합니다.
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


