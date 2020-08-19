---
description: TODATETIMEOFFSET(Transact-SQL)
title: TODATETIMEOFFSET(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5274a17e4de005c3947aba96956b62b5d200409
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459545"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **datetime2** 표현식에서 변환된 **datetimeoffset** 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 [datetime2](../../t-sql/language-elements/expressions-transact-sql.md) 값으로 확인되는 [식](../../t-sql/data-types/datetime2-transact-sql.md)입니다.  
  
> [!NOTE]  
>  **varchar** 또는 **nvarchar**로 암시적으로 변환할 수 없는 **text**, **ntext** 또는 **image** 형식의 식을 사용할 수 없습니다.  
  
 *time_zone*  
 분(-120과 같은 정수인 경우) 단위나 시간 및 분('+13:00'과 같은 문자열인 경우) 단위의 표준 시간대 오프셋을 나타내는 식입니다. 범위는 +14에서 -14(시간) 사이입니다. 이 식은 지정된 time_zone의 현지 시간으로 해석됩니다.  
  
> [!NOTE]  
>  식이 문자열인 경우 {+|-}TZH:THM 형식이어야 합니다.  
  
## <a name="return-type"></a>반환 형식  
 **datetimeoffset**. 소수 자릿수는 *datetime* 인수와 같습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. 현재 날짜 및 시간의 표준 시간대 오프셋 변경  
 다음 예에서는 현재 날짜 및 시간의 표준 시간대 오프셋을 표준 시간대 `-07:00`으로 변경합니다.  
  
```sql  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2019-04-22 16:23:51.7666667 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. 표준 시간대 오프셋(분) 변경  
 다음 예에서는 현재 표준 시간대를 `-120`분으로 변경합니다.  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), -120)
-- RETURNS: 2019-04-22 11:39:21.6986813 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. 13시간 표준 시간대 오프셋 추가  
 다음 예에서는 날짜 및 시간에 13시간 표준 시간대 오프셋을 추가합니다.  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), '+13:00')
-- RETURNS: 2019-04-22 11:39:29.0339301 +13:00
```  
  
## <a name="see-also"></a>관련 항목  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE&#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  

