---
title: 예약된 추적 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7318201b585b51f41884c85b9a5d2c6b92bb8563
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179630"
---
# <a name="schedule-traces"></a>예약된 추적
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 추적을 예약하는 두 가지 방법이 제공됩니다. 다음 작업을 수행할 수 있습니다.  
  
-   추적 중지 시간을 설정합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 추적을 예약할 수 있습니다.  
  
## <a name="specifying-a-stop-time"></a>중지 시간 지정  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하는 경우에는 추적 중지 시간을 지정할 수 있습니다. 추적이 원래 구성되어 있는 경우에는 중지 시간을 설정해야 합니다.  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>SQL Server 에이전트를 사용하여 추적 예약  
 추적을 예약하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 추적을 시작한 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저인 **sp_trace_setstatus**나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적 중지 시간을 지정하는 것이 좋습니다.  
  
 **추적 종료 시간 필터를 설정하려면**  
  
 [이벤트 종료 시간 기반의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [관리 태스크 자동화&#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)  
  
  
