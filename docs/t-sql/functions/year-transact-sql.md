---
description: YEAR(Transact-SQL)
title: YEAR(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f3f8ad5bd4d39b0fc55fad2dd68b43552bf15ab8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422587"
---
# <a name="year-transact-sql"></a>YEAR(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정한 *날짜*의 연도를 나타내는 정수를 반환합니다.  
  
 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
YEAR ( date )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *date*  
 **time**, **date**, **smalldatetime**, **datetime**, **datetime2** 또는 **datetimeoffset** 값으로 확인할 수 있는 식입니다. *date* 인수는 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>Return Value  
 YEAR는 [DATEPART](../../t-sql/functions/datepart-transact-sql.md)(**year**, *date*)와 같은 값을 반환합니다.  
  
 *date*에 시간 부분만 포함된 경우 기본 연도인 1900이 반환됩니다.  
  
## <a name="examples"></a>예제  
 다음 문은 `2010`을 반환합니다. 이는 연도입니다.  
  
```sql  
SELECT YEAR('2010-04-30T01:01:01.1234567-07:00');  
```  
  
 다음 문은 `1900, 1, 1`을 반환합니다. *date*의 인수는 숫자 `0`입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `0`을 1900년 1월 1일로 해석합니다.  
  
```sql 
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 문은 `1900, 1, 1`을 반환합니다. *date*의 인수는 숫자 `0`입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `0`을 1900년 1월 1일로 해석합니다.  
  
```sql  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>참고 항목  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

