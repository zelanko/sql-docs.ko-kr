---
title: DBCC TRACESTATUS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_TRACESTATUS_TSQL
- DBCC TRACESTATUS
- TRACESTATUS_TSQL
- TRACESTATUS
dev_langs: TSQL
helpviewer_keywords:
- global trace flags [SQL Server]
- status information [SQL Server], trace flags
- trace flags [SQL Server], status information
- DBCC TRACESTATUS statement
- session trace flags [SQL Server]
- displaying trace flag status
ms.assetid: 9be51199-78b4-4b87-ae6e-557246b7e29a
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1c0241e43f4d9516eefb73e65889df8944ccd018
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-tracestatus-transact-sql"></a>DBCC TRACESTATUS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

추적 플래그의 상태를 표시합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC TRACESTATUS ( [ [ trace# [ ,...n ] ] [ , ] [ -1 ] ] )   
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
*trace #*  
상태를 표시할 추적 플래그의 번호입니다. 경우 *trace #*, 및-1이 지정 되지 않은 경우 세션에 대해 사용할 수 있는 추적 플래그를 모두 표시 됩니다.
  
*n*  
여러 개의 추적 플래그를 지정할 수 있음을 나타내는 자리 표시자입니다.
  
-1  
전역으로 설정된 추적 플래그의 상태를 표시합니다. 없이-1을 지정 하면 *trace #*, 사용 하도록 설정 된 모든 전역 추적 플래그가 표시 됩니다.
  
WITH NO_INFOMSGS  
심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.
  
## <a name="result-sets"></a>결과 집합  
다음 표에서는 결과 집합에 표시되는 정보를 설명합니다.
  
|열 이름|Description|  
|---|---|
|**TraceFlag**|추적 플래그의 이름입니다.|  
|**상태**|전역 또는 세션에 대한 추적 플래그의 설정 상태가 ON인지 아니면 OFF인지 여부를 나타냅니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|**전역**|추적 플래그가 전역으로 설정되었는지 여부를 나타냅니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**세션**|추적 플래그가 해당 세션에 대해서만 설정되었는지 여부를 나타냅니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
  
DBCC TRACESTATUS는 추적 플래그 번호에 대한 열과 상태에 대한 열을 반환하여 추적 플래그의 ON(1) 또는 OFF(0) 여부를 표시합니다. 추적 플래그 번호에 대 한 열 머리글 **전역 추적 플래그** 또는 **세션 추적 플래그**전역 또는 세션 추적 플래그의 상태를 확인 하는지 여부에 따라 합니다.
  
## <a name="remarks"></a>주의  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 세션 및 전역이라는 두 가지 유형의 추적 플래그가 있습니다. 세션 추적 플래그는 특정 연결에 대해 설정되며 해당 연결에서만 볼 수 있습니다. 전역 추적 플래그는 서버 수준에서 설정되며 서버의 모든 연결에서 볼 수 있습니다.
  
## <a name="permissions"></a>Permissions  
**public** 역할의 멤버 자격이 필요합니다.
  
## <a name="examples"></a>예  
다음 예에서는 현재 전역으로 설정된 모든 추적 플래그의 상태를 표시합니다.
  
```sql  
DBCC TRACESTATUS(-1);  
GO  
```  
  
다음 예에서는 추적 플래그 `2528`과 `3205`의 상태를 표시합니다.
  
```sql  
DBCC TRACESTATUS (2528, 3205);  
GO  
```  
  
다음 예에서는 추적 플래그 `3205`가 전역으로 설정되었는지 여부를 표시합니다.
  
```sql  
DBCC TRACESTATUS (3205, -1);  
GO  
```  
  
다음 예에서는 현재 세션에 대해 설정된 모든 추적 플래그의 목록을 나열합니다.
  
```sql  
DBCC TRACESTATUS();  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
