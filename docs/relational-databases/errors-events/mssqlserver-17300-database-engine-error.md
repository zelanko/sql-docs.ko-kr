---
title: "MSSQLSERVER_17300 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ef809a200d3544e5e24549440506b77d6f1a79e5
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17300"></a>MSSQLSERVER_17300
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17300|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PROC_OUT_OF_SYSTASK_SESSIONS|  
|메시지 텍스트|SQL Server에서 메모리가 부족하거나 구성된 세션의 수가 서버에서 허용되는 최대 수를 초과하므로 새 시스템 태스크를 실행할 수 없습니다. 서버에 적당한 메모리가 있는지 확인하십시오. 허용되는 최대 세션 수를 확인하려면 'user connections' 옵션과 함께 sp_configure를 사용하십시오. 사용자 프로세스를 비롯하여 현재 세션 수를 확인하려면 sys.dm_exec_sessions를 사용하십시오.|  
  
## <a name="explanation"></a>설명  
메모리가 부족하거나 서버에 구성된 세션 수가 초과되어 새 시스템 태스크를 실행하려는 시도가 실패했습니다.  
  
## <a name="user-action"></a>사용자 동작  
서버에 충분한 메모리가 있는지 확인합니다. sys.dm_exec_sessions를 사용하여 현재 시스템 태스크 수를 확인하고 sp_configure를 사용하여 구성된 최대 사용자 연결 값을 확인합니다.  
  
다음 태스크를 적절하게 수행합니다.  
  
-   서버에 메모리를 더 많이 추가합니다.  
  
-   하나 이상의 세션을 종료합니다.  
  
-   서버에 허용되는 최대 사용자 연결 수를 늘립니다.  
  
## <a name="see-also"></a>관련 항목:  
[sp_configure&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
[서버 구성 옵션&#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[sys.dm_exec_sessions&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[user connections 서버 구성 옵션 구성](~/database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
[KILL&#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md)  
  

