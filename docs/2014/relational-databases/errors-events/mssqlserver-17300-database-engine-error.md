---
title: MSSQLSERVER_17300 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34a0cf19f43561f80e9822cdf34dd43793d869c2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431372"
---
# <a name="mssqlserver17300"></a>MSSQLSERVER_17300
    
## <a name="details"></a>설명  
  
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
  
## <a name="see-also"></a>관련 항목  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql)   
 [User connections 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)   
 [KILL&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql)  
  
  
