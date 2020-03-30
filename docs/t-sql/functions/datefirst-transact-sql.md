---
title: '@@DATEFIRST(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs:
- TSQL
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2fc2ca71731fa632db2a857e1b727574722058c8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68119184"
---
# <a name="x40x40datefirst-transact-sql"></a>&#x40;&#x40;DATEFIRST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 특정 세션에 대해 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)의 현재 값을 반환합니다.
  
모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
@@DATEFIRST  
```  
  
## <a name="return-type"></a>반환 형식  
**tinyint**
  
## <a name="remarks"></a>설명  
SET DATEFIRST *n*은 주에서 첫 번째 일을 지정합니다(일요일, 월요일, 화요일 등). *n* 값의 범위는 1에서 7입니다.

```sql
SET DATEFIRST 3;
GO  
SELECT @@DATEFIRST; -- 3 (Wednesday)
GO
```  

미국의 경우 영어 환경은 @@DATEFIRST 기본값을 7(일요일)로 설정합니다.
  
이 언어 설정은 SQL Server가 해당 문자열을 데이터베이스 스토리지에 대한 날짜 값으로 변환하므로 문자열 해석에 영향을 줍니다. 이 설정은 데이터베이스에 저장된 날짜 값의 표시에도 영향을 줍니다. 이 설정은 날짜 데이터의 스토리지 형식에는 영향을 주지 않습니다.

이 예제에서는 먼저 언어를 `Italian`로 설정합니다. `SELECT @@DATEFIRST;` 문은 `1`을 반환합니다. 다음 명령문은 언어를 `us_english`로 설정합니다. 마지막 명령문 `SELECT @@DATEFIRST;`는 `7`을 반환합니다.
  
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
이 예에서는 주의 시작 요일을 `5`(금요일)로 설정하고 현재 날짜인 `Today`를 토요일로 가정합니다. `SELECT` 문은 주의 현재 날짜의 `DATEFIRST` 값과 현재 날짜 번호를 반환합니다.
  
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
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>참고 항목
[구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  

