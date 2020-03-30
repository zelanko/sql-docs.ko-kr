---
title: SWITCHOFFSET(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SWITCHTZ
- SWITCHTZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- functions [SQL Server], time
- functions [SQL Server], date and time
- SWITCHOFFSET function [SQL Server]
- time [SQL Server], functions
- date and time [SQL Server], SWITCHOFFSET
- time zones [SQL Server]
ms.assetid: 32a48e36-0aa4-4260-9fe9-cae9197d16c5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2ce69487c1550314dc7cfe3641333728fd07155e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68117558"
---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  저장된 표준 시간대 오프셋에서 지정된 새 표준 시간대 오프셋으로 변경된 **datetimeoffset** 값을 반환합니다.  
  
 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
## <a name="arguments"></a>인수  
 *DATETIMEOFFSET*  
 **datetimeoffset(n)** 값으로 확인할 수 있는 식입니다.  
  
 *time_zone*  
 [+|-]TZH:TZM 또는 부호 있는 정수(분) 형식의 문자열로, 표준 시간대 오프셋을 나타내고 일광 절약 시간제를 인식하고 조정할 수 있는 것으로 간주됩니다.  
  
## <a name="return-type"></a>반환 형식  
 **datetimeoffset**을 *DATETIMEOFFSET* 인수의 소수 자릿수로 표시합니다.  
  
## <a name="remarks"></a>설명  
 처음 저장된 표준 시간대 오프셋과 다른 표준 시간대 오프셋으로 **datetimeoffset** 값을 선택하려면 SWITCHOFFSET을 사용합니다. SWITCHOFFSET은 저장된 *time_zone* 값을 업데이트하지 않습니다.  
  
 SWITCHOFFSET을 사용하여 **datetimeoffset** 열을 업데이트 할 수 있습니다.  
  
 GETDATE() 함수에 SWITCHOFFSET을 사용하면 쿼리 실행이 느려질 수 있습니다. 이는 쿼리 최적화 프로그램에서 datetime 값에 대한 정확한 카디널리티 예측을 구할 수 없기 때문입니다. 이 문제를 해결하려면 OPTION (RECOMPILE) 쿼리 힌트를 사용하여 다음에 동일한 쿼리를 실행할 때 쿼리 최적화 프로그램에서 쿼리 계획을 다시 컴파일하도록 하세요. 그러면 최적화 프로그램에서 정확한 카디널리티 예측을 구해 더 효율적인 쿼리 계획을 생성합니다. RECOMPILE 쿼리 힌트에 대한 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>예  
 다음 예에서는 `SWITCHOFFSET`을 사용하여 데이터베이스에 저장된 값과 다른 표준 시간대 오프셋을 표시합니다.  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="see-also"></a>참고 항목  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [AT TIME ZONE&#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


