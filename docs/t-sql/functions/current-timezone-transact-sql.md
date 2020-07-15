---
title: CURRENT_TIMEZONE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/28/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMEZONE
- CURRENT_TIMEZONE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- current time zone [SQL Server]
- current timezone [SQL Server]
- system time zone [SQL Server]
- system timezone [SQL Server]
- functions [SQL Server], time zone
- functions [SQL Server], timezone
- timezone [SQL Server], functions
- time zone [SQL Server], functions
- CURRENT_TIMEZONE function [SQL Server]
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 760da1491a7fbf4633cb02fe1fea8568e7ab9fa1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85684498"
---
# <a name="current_timezone-transact-sql"></a>CURRENT_TIMEZONE(Transact-SQL)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

이 함수는 서버 또는 인스턴스에서 관찰된 표준 시간대 이름을 반환합니다. SQL Database Managed Instance의 경우 반환 값은 기본 운영 체제의 표준 시간대가 아니라 인스턴스를 만드는 중에 할당된 인스턴스 자체의 표준 시간대를 기반으로 합니다.
  
> [!NOTE]  
> 단일 및 풀링된 SQL Database의 경우 표준 시간대는 항상 UTC로 설정되고 `CURRENT_TIMEZONE`은 UTC 표준 시간대의 이름을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```sql
CURRENT_TIMEZONE ( )  
```
  
## <a name="arguments"></a>인수

이 함수에는 인수가 필요하지 않습니다.
  
## <a name="return-type"></a>반환 형식  

**varchar**
  
## <a name="remarks"></a>설명  

`CURRENT_TIMEZONE`은 비결정 함수입니다. 이 열을 참조하는 뷰와 식은 인덱싱될 수 없습니다.
  
## <a name="example"></a>예제

반환되는 값은 서버 또는 인스턴스의 실제 표준 시간대와 언어 설정을 반영합니다.

```sql
SELECT CURRENT_TIMEZONE();  
/* Returned:  
(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna 
*/
```  
  
## <a name="see-also"></a>참고 항목

[SQL Database Managed Instance 표준 시간대](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone)

[CURRENT_TIMEZONE_ID()](https://docs.microsoft.com/sql/t-sql/functions/current-timezone-id-transact-sql)
