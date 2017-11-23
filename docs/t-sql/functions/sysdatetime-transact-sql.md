---
title: SYSDATETIME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- SYSDATETIME_TSQL
- SYSDATETIME
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SYSDATETIME
- current date and time [SQL Server]
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- SYSDATETIME function [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- time [SQL Server], system
ms.assetid: cba4999e-a9d4-4742-abc9-4a4f109206b6
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4e0f33419d2ea3986ebeab02399066cb8efa6487
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatetime-transact-sql"></a>SYSDATETIME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  반환 된 **datetime2 (7)** 되는 컴퓨터의 시간과 날짜를 포함 하는 값의 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되 고 합니다.  
  
> [!NOTE]  
>  SYSDATETIME 및 SYSUTCDATETIME에는 GETDATE 및 GETUTCDATE보다 많은 소수 자릿수 초의 전체 자릿수가 있습니다. SYSDATETIMEOFFSET에는 시스템 표준 시간대 오프셋이 포함되어 있습니다. SYSDATETIME, SYSUTCDATETIME 및 SYSDATETIMEOFFSET은 모든 날짜 및 시간 유형의 변수에 할당할 수 있습니다.  
  
 모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SYSDATETIME ( )  
```  
  
## <a name="return-type"></a>반환 형식  
 **datetime2(7)**  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]문은 참조할 수 있습니다 SYSDATETIME을 참조할 수 있는 모든 위치는 **datetime2 (7)** 식입니다.  
  
 SYSDATETIME은 비결정적 함수입니다. 열에서 이 함수를 참조하는 뷰와 식은 인덱싱될 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]GetSystemTimeAsFileTime() Windows API를 사용 하 여 날짜 및 시간 값을 가져옵니다. 정확도는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 하드웨어와 Windows 버전에 따라 달라집니다. 이 API의 정밀도는 100나노초로 고정됩니다. GetSystemTimeAdjustment() Windows API를 사용 하 여 정확도 확인할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 날짜 및 시간을 반환하는 6개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 함수를 사용하여 시간, 날짜 또는 두 가지 모두 반환합니다. 값은 순차적으로 반환되므로 소수 자릿수 초가 서로 다를 수 있습니다.  
  
### <a name="a-getting-the-current-system-date-and-time"></a>1. 현재 시스템의 날짜 및 시간 가져오기  
  
```  
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
  
### <a name="b-getting-the-current-system-date"></a>2. 현재 시스템의 날짜 가져오기  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
  
/* All returned 2007-04-30 */  
```  
  
### <a name="c-getting-the-current-system-time"></a>3. 현재 시스템의 시간 가져오기  
  
```  
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, SYSDATETIMEOFFSET())  
    ,CONVERT (time, SYSUTCDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE())  
    ,CONVERT (time, GETUTCDATE());  
  
/* Returned  
SYSDATETIME()      13:18:45.3490361  
SYSDATETIMEOFFSET()13:18:45.3490361  
SYSUTCDATETIME()   20:18:45.3490361  
CURRENT_TIMESTAMP  13:18:45.3470000  
GETDATE()          13:18:45.3470000  
GETUTCDATE()       20:18:45.3470000  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-getting-the-current-system-date-and-time"></a>D: 현재 시스템 날짜 및 시간 가져오기  
  
```  
SELECT SYSDATETIME();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
--------------------------  
7/20/2013 2:49:59 PM
```  
  
## <a name="see-also"></a>관련 항목:  
 [CAST 및 convert&#40; Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  

