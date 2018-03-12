---
title: '@@CONNECTIONS(Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8422da0d4e550c99fac6c9659f771ab98196cb4a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONNECTIONS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

마지막으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작한 후 시도한 연결 수를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>반환 형식
**integer**
  
## <a name="remarks"></a>Remarks  
연결은 사용자와 다릅니다. 예를 들어 응용 프로그램은 연결을 관찰하는 사용자 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 연결 여러 개를 열 수 있습니다.
  
연결 시도 횟수를 포함한 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계를 포함하는 보고서를 표시하려면 **sp_monitor**를 실행합니다.
  
@@MAX_CONNECTIONS는 서버에서 동시에 허용되는 최대 연결 수입니다. @@CONNECTIONS는 로그인을 시도할 때마다 증가하므로 @@CONNECTIONS는 @@MAX_CONNECTIONS보다 클 수 있습니다.
  
## <a name="examples"></a>예  
다음 예에서는 현재 날짜 및 시간의 로그인 시도 수를 반환합니다.
  
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
  
## <a name="see-also"></a>관련 항목:
[시스템 통계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  
