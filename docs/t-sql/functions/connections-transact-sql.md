---
title: '@@CONNECTIONS(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 3c7a4a11e3f77316d0f219c4733e3d16fd93ffbc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827093"
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONNECTIONS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 함수에서는 마지막으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작한 이후 성공하거나 성공하지 못한 시도된 모든 연결 수를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>반환 형식
**integer**
  
## <a name="remarks"></a>설명  
연결은 사용자와 다릅니다. 예를 들어 애플리케이션은 해당 연결을 관찰하는 사용자 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 여러 연결을 열 수 있습니다.
  
연결 시도 횟수를 포함한 여러 **통계를 포함하는 보고서의 경우**sp_monitor[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행합니다.
  
@@MAX_CONNECTIONS는 서버에 대해 허용되는 최대 동시 연결 수입니다. @@CONNECTIONS는 로그인을 시도할 때마다 증가하므로 @@CONNECTIONS는 @@MAX_CONNECTIONS을 초과할 수 있습니다.
  
## <a name="examples"></a>예  
이 예제에서는 로그인 시도 횟수를 현재 날짜 및 시간으로 반환합니다.
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>참고 항목
[시스템 통계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  
