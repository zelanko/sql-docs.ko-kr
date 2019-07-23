---
title: CURRENT_TIMEZONE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2019
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
ms.openlocfilehash: 6c29cfba3f47506cb88860763d6650cfb3ecab7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026393"
---
# <a name="currenttimezone-transact-sql"></a>CURRENT_TIMEZONE(Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

이 함수는 서버 또는 인스턴스에서 관찰된 표준 시간대 이름을 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`CURRENT_TIMEZONE`은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되는 컴퓨터의 운영 체제에서 반환 값을 끌어냅니다. SQL Database Managed Instance의 경우 반환 값은 기본 운영 체제의 표준 시간대가 아니라 인스턴스를 만드는 중에 할당된 인스턴스 자체의 표준 시간대를 기반으로 합니다.
  
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
  
## <a name="remarks"></a>Remarks  

`CURRENT_TIMEZONE`은 비결정 함수입니다. 이 열을 참조하는 뷰와 식은 인덱싱될 수 없습니다.
  
## <a name="example"></a>예제

반환되는 값은 서버 또는 인스턴스의 실제 표준 시간대와 언어 설정을 반영합니다.

```sql
SELECT CURRENT_TIMEZONE();  
/* Returned:  
(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna 
*/
```  
  
## <a name="see-also"></a>관련 항목:

[SQL Database Managed Instance 표준 시간대](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone)
