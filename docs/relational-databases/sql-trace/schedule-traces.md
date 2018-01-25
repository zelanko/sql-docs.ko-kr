---
title: "예약된 추적 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-trace
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6693df4ddf0afbca69ad46f50bbaa49877be4450
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="schedule-traces"></a>예약된 추적
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 추적을 예약하는 두 가지 방법이 제공됩니다. 다음 작업을 수행할 수 있습니다.  
  
-   추적 중지 시간을 설정합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 추적을 예약할 수 있습니다.  
  
## <a name="specifying-a-stop-time"></a>중지 시간 지정  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하는 경우에는 추적 중지 시간을 지정할 수 있습니다. 추적이 원래 구성되어 있는 경우에는 중지 시간을 설정해야 합니다.  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>SQL Server 에이전트를 사용하여 추적 예약  
 추적을 예약하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 추적을 시작한 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저인 **sp_trace_setstatus**나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적 중지 시간을 지정하는 것이 좋습니다.  
  
 **추적 종료 시간 필터를 설정하려면**  
  
 [이벤트 종료 시간 기반의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [관리 태스크 자동화&#40;SQL Server Agent&#41;](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  
