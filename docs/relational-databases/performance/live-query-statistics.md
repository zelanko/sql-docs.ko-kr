---
title: "활성 쿼리 통계 | Microsoft 문서"
ms.custom: 
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e81e49b14a91f809c4c3452369069ff4d856a99f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="live-query-statistics"></a>활성 쿼리 통계
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]는 활성 쿼리의 활성 실행 계획을 보는 기능을 제공합니다. 이 활성 쿼리 계획을 통해 제어권이 한 쿼리 계획 연산자에서 다른 연산자로 흘러갈 때 쿼리 실행 프로세스를 실시간으로 파악할 수 있습니다. 활성 쿼리 계획은 전체 쿼리 진행률 및 생성된 행 수, 경과 시간, 연산자 진행률 등과 같은 연산자 수준의 런타임 실행 통계를 표시합니다. 이 데이터는 쿼리가 완료될 때까지 기다릴 필요 없이 실시간으로 사용할 수 있으므로 이 실행 통계는 쿼리 성능 문제를 디버깅할 때 매우 유용합니다. 이 기능은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]부터 사용할 수 있지만 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 작동할 수 있습니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
> [!WARNING]  
>  이 기능은 주로 문제 해결을 위해 사용됩니다. 이 기능을 사용하면 전체 쿼리 성능이 약간 느려질 수 있습니다. 이 기능을 [Transact-SQL 디버거](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)와 함께 사용할 수 있습니다.  
  
#### <a name="to-view-live-query-statistics"></a>활성 쿼리 통계를 보려면  
  
1.  활성 쿼리 실행 계획을 보려면 도구 메뉴에서 **활성 쿼리 통계** 아이콘을 클릭합니다.  
  
     ![도구 모음의 활성 쿼리 통계 단추](../../relational-databases/performance/media/livequerystatstoolbar.png "도구 모음의 활성 쿼리 통계 단추")  
  
     또한 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 선택한 쿼리를 마우스 오른쪽 단추로 클릭한 다음 **활성 쿼리 통계 포함**을 클릭하여 활성 쿼리 실행 계획에 액세스하고 볼 수도 있습니다.  
  
     ![팝업 메뉴의 활성 쿼리 통계 단추](../../relational-databases/performance/media/livequerystatsmenu.png "팝업 메뉴의 활성 쿼리 통계 단추")  
  
2.  이제 쿼리를 실행합니다. 활성 쿼리 계획은 전체 쿼리 진행률 및 쿼리 계획 연산자에 대한 런타임 실행 통계(예: 경과 시간, 진행률 등)를 표시합니다. 쿼리 진행률 정보와 실행 통계는 쿼리 실행이 진행 중인 동안에 주기적으로 업데이트됩니다. 이 정보를 사용하여 전체 쿼리 실행 프로세스를 이해하고 오래 실행되는 쿼리, 무한히 실행되는 쿼리, tempdb 오버플로를 야기하는 쿼리 및 시간 초과 문제를 디버그합니다.  
  
     ![실행 계획의 활성 쿼리 통계 단추](../../relational-databases/performance/media/livequerystatsplan.png "실행 계획의 활성 쿼리 통계 단추")  
  
 또한 **비용이 드는 활성 쿼리** 테이블에서 쿼리를 마우스 오른쪽 단추로 클릭하고 **작업 모니터** 에서 활성 쿼리 계획에 액세스할 수도 있습니다.  
  
 ![작업 모니터의 활성 쿼리 통계 단추](../../relational-databases/performance/media/livequerystatsactmon.png "작업 모니터의 활성 쿼리 통계 단추")  
  
## <a name="remarks"></a>주의  
 통계 프로필 인프라를 사용하도록 설정해야 활성 쿼리 통계에서 쿼리 진행률에 관한 정보를 수집할 수 있습니다. **에서** 활성 쿼리 통계 포함 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 을 지정하면 현재 쿼리 세션에 대한 통계 인프라가 사용하도록 설정됩니다. 
 
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]까지는 다른 세션(예: 작업 모니터)에서 활성 쿼리 통계를 보는 데 사용할 수 있는 통계 인프라를 사용하도록 설정하는 두 가지 다른 방법이 있습니다.  
  
-   대상 세션에서 `SET STATISTICS XML ON;` 또는 `SET STATISTICS PROFILE ON;` 을 실행합니다.  
  
 또는  
  
-   **query_post_execution_showplan** 확장 이벤트를 사용하도록 설정합니다. 이는 모든 세션에 대해 활성 쿼리 통계를 사용하도록 설정하는 서버 전체 설정입니다. 확장 이벤트를 사용하도록 설정하려면 [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)을 참조하세요.  

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 통계 프로필 인프라의 경량 버전이 포함되어 있습니다. 다른 세션(예: 작업 모니터)에서 활성 쿼리 통계를 보는 데 사용할 수 있는 경량 통계 인프라를 사용하도록 설정하는 다음 두 가지 방법이 있습니다.

-   전역 추적 플래그 7412 사용.  
  
 또는  
  
-   **query_thread_profile** 확장 이벤트 사용. 이는 모든 세션에 대해 활성 쿼리 통계를 사용하도록 설정하는 서버 전체 설정입니다. 확장 이벤트를 사용하도록 설정하려면 [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)을 참조하세요.
  
 > [!NOTE]
 > 고유하게 컴파일된 저장 프로시저는 지원되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **활성 쿼리 통계** 결과 페이지를 채우려면 데이터베이스 수준의 **SHOWPLAN** 권한이 필요하고 활성 통계를 보려면 서버 수준의 **VIEW SERVER STATE** 권한이 필요하며 쿼리를 실행하는 데 필요한 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [작업 모니터 열기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [작업 모니터](../../relational-databases/performance-monitor/activity-monitor.md)   
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)   
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)   
 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
