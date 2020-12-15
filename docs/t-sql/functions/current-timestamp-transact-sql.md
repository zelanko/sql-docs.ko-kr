---
description: CURRENT_TIMESTAMP(Transact-SQL)
title: CURRENT_TIMESTAMP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMESTAMP
- CURRENT_TIMESTAMP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- niladic functions
- current date and time [SQL Server]
- time [SQL Server], current
- date and time [SQL Server], CURRENT_TIMESTAMP
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- CURRENT_TIMESTAMP function [SQL Server]
- time [SQL Server], system
ms.assetid: c724d9cc-7b1f-4c71-bdf5-08bc52b33afc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 75cb9104b167373ea2657c796a238a7a087bfbd6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97408283"
---
# <a name="current_timestamp-transact-sql"></a>CURRENT_TIMESTAMP(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 현재 데이터베이스 시스템 타임스탬프를 데이터베이스 표준 시간대 오프셋 없이 **datetime** 값으로 반환합니다. `CURRENT_TIMESTAMP`는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되는 컴퓨터의 운영 체제에서 이 값을 끌어냅니다.
  
> [!NOTE]  
>  `SYSDATETIME` 및 `SYSUTCDATE`는 소수 자릿수 초 단위이므로 `GETDATE` 및 `GETUTCDATE`보다 정확합니다. `SYSDATETIMEOFFSET` 함수에는 시스템 표준 시간대 오프셋이 포함되어 있습니다. `SYSDATETIME`, `SYSUTCDATE`, 및 `SYSDATETIMEOFFSET`을 모든 날짜 및 시간 형식의 변수에 할당할 수 있습니다.  
  
이 함수는 ANSI SQL의 [GETDATE](../../t-sql/functions/getdate-transact-sql.md)와 동등합니다.
  
[!INCLUDE[tsql](../../includes/tsql-md.md)]의 모든 날짜 및 시간 데이터 형식과 함수에 대한 개요는 [날짜 및 시간 데이터 형식과 함수](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)를 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CURRENT_TIMESTAMP  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
이 함수에는 인수가 필요하지 않습니다.
  
## <a name="return-type"></a>반환 형식  
**datetime**
  
## <a name="remarks"></a>설명  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 **datetime** 식을 참조할 수 있는 모든 곳에서 `CURRENT_TIMESTAMP`를 참조할 수 있습니다.
  
`CURRENT_TIMESTAMP`는 비결정 함수입니다. 이 열을 참조하는 뷰와 식은 인덱싱될 수 없습니다.
  
## <a name="examples"></a>예제  
이 예에서는 현재 날짜 및 시간 값을 반환하는 6개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 함수를 사용하여 시간, 날짜 또는 두 가지 모두 반환합니다. 이 예에서는 값을 순차적으로 반환하므로 소수 자릿수 초가 서로 다를 수 있습니다. 반환되는 실제 값은 실제 실행 날짜/시간을 나타냅니다.
  
### <a name="a-get-the-current-system-date-and-time"></a>A. 현재 시스템의 날짜 및 시간 가져오기  
  
```sql
SELECT SYSDATETIME()  
    ,SYSDATETIMEOFFSET()  
    ,SYSUTCDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE()  
    ,GETUTCDATE();  
/* Returned:  
SYSDATETIME()      2007-04-30 13:10:02.0474381  
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00  
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381  
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047  
GETDATE()          2007-04-30 13:10:02.047  
GETUTCDATE()       2007-04-30 20:10:02.047  
*/
```  
  
### <a name="b-get-the-current-system-date"></a>B. 현재 시스템의 날짜 가져오기  
  
```sql
SELECT CONVERT (DATE, SYSDATETIME())  
    ,CONVERT (DATE, SYSDATETIMEOFFSET())  
    ,CONVERT (DATE, SYSUTCDATETIME())  
    ,CONVERT (DATE, CURRENT_TIMESTAMP)  
    ,CONVERT (DATE, GETDATE())  
    ,CONVERT (DATE, GETUTCDATE());  
  
/* Returned   
SYSDATETIME()      2007-05-03  
SYSDATETIMEOFFSET()2007-05-03  
SYSUTCDATETIME()   2007-05-04  
CURRENT_TIMESTAMP  2007-05-03  
GETDATE()          2007-05-03  
GETUTCDATE()       2007-05-04  
*/  
```  
  
### <a name="c-get-the-current-system-time"></a>C. 현재 시스템의 시간 가져오기  
  
```sql
SELECT CONVERT (TIME, SYSDATETIME())  
    ,CONVERT (TIME, SYSDATETIMEOFFSET())  
    ,CONVERT (TIME, SYSUTCDATETIME())  
    ,CONVERT (TIME, CURRENT_TIMESTAMP)  
    ,CONVERT (TIME, GETDATE())  
    ,CONVERT (TIME, GETUTCDATE());  
  
/* Returned  
SYSDATETIME()      13:18:45.3490361  
SYSDATETIMEOFFSET()13:18:45.3490361  
SYSUTCDATETIME()   20:18:45.3490361  
CURRENT_TIMESTAMP  13:18:45.3470000  
GETDATE()          13:18:45.3470000  
GETUTCDATE()       20:18:45.3470000  
*/  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT CURRENT_TIMESTAMP;  
```  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

