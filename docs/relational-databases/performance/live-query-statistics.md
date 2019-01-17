---
title: 활성 쿼리 통계 | Microsoft 문서
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
- query profiling
- lightweight query profiling
- lightweight profiling
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 5b60d4190ad25dd57098ef4cd107f1838886a767
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368415"
---
# <a name="live-query-statistics"></a>활성 쿼리 통계
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 활성 쿼리의 활성 실행 계획을 보는 기능을 제공합니다. 이 활성 쿼리 계획을 통해 제어권이 한 [쿼리 계획 연산자](../../relational-databases/showplan-logical-and-physical-operators-reference.md)에서 다른 연산자로 흘러갈 때 쿼리 실행 프로세스를 실시간으로 파악할 수 있습니다. 활성 쿼리 계획은 전체 쿼리 진행률 및 생성된 행 수, 경과 시간, 연산자 진행률 등과 같은 연산자 수준의 런타임 실행 통계를 표시합니다. 이 데이터는 쿼리가 완료될 때까지 기다릴 필요 없이 실시간으로 사용할 수 있으므로 이 실행 통계는 쿼리 성능 문제를 디버깅할 때 매우 유용합니다. 이 기능은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]부터 사용할 수 있지만 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 작동할 수 있습니다.  

> [!NOTE]
> 내부적으로 활성 쿼리 통계는 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV를 활용합니다.
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
> [!WARNING]  
> 이 기능은 주로 문제 해결을 위해 사용됩니다. 이 기능을 사용하면 특히 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 전체 쿼리 성능이 약간 느려질 수 있습니다. 자세한 내용은 [쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.  
> 이 기능을 [Transact-SQL 디버거](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)와 함께 사용할 수 있습니다.  
  
## <a name="to-view-live-query-statistics-for-one-query"></a>하나의 쿼리에 대한 활성 쿼리 통계를 보려면 
  
1.  활성 쿼리 실행 계획을 보려면 도구 메뉴에서 **활성 쿼리 통계 포함** 아이콘을 클릭합니다.  
  
     ![도구 모음의 활성 쿼리 통계 단추](../../relational-databases/performance/media/livequerystatstoolbar.png "도구 모음의 활성 쿼리 통계 단추")  
  
     또한 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 선택한 쿼리를 마우스 오른쪽 단추로 클릭한 다음, **활성 쿼리 통계 포함**을 클릭하여 활성 쿼리 실행 계획에 액세스하고 볼 수도 있습니다.  
  
     ![팝업 메뉴의 활성 쿼리 통계 단추](../../relational-databases/performance/media/livequerystatsmenu.png "팝업 메뉴의 활성 쿼리 통계 단추")  
  
2.  이제 쿼리를 실행합니다. 활성 쿼리 계획은 전체 쿼리 진행률 및 쿼리 계획 연산자에 대한 런타임 실행 통계(예: 경과 시간, 진행률 등)를 표시합니다. 쿼리 진행률 정보와 실행 통계는 쿼리 실행이 진행 중인 동안에 주기적으로 업데이트됩니다. 이 정보를 사용하여 전체 쿼리 실행 프로세스를 이해하고 오래 실행되는 쿼리, 무한히 실행되는 쿼리, tempdb 오버플로를 야기하는 쿼리 및 시간 초과 문제를 디버그합니다.  
  
     ![실행 계획의 활성 쿼리 통계 단추](../../relational-databases/performance/media/livequerystatsplan.png "실행 계획의 활성 쿼리 통계 단추")  
  
## <a name="to-view-live-query-statistics-for-any-query"></a>쿼리에 대한 활성 쿼리 통계를 보려면 

또한 **프로세스** 또는 **비용이 드는 활성 쿼리** 테이블에서 쿼리를 마우스 오른쪽 단추로 클릭하여 **[작업 모니터](../../relational-databases/performance-monitor/activity-monitor.md)** 에서 활성 실행 계획에 액세스할 수도 있습니다.  
  
 ![작업 모니터의 활성 쿼리 통계 단추](../../relational-databases/performance/media/livequerystatsactmon.png "작업 모니터의 활성 쿼리 통계 단추")  
  
## <a name="remarks"></a>Remarks  
 통계 프로필 인프라를 사용하도록 설정해야 활성 쿼리 통계에서 쿼리 진행률에 관한 정보를 수집할 수 있습니다. 버전에 따라 오버헤드가 중요할 수 있습니다. 이 오버헤드에 대한 자세한 내용은 [쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.
  
## <a name="permissions"></a>Permissions  
 **활성 쿼리 통계** 결과 페이지를 채우려면 데이터베이스 수준의 `SHOWPLAN` 권한이 필요하고 활성 통계를 보려면 서버 수준의 `VIEW SERVER STATE` 권한이 필요하며 쿼리를 실행하는 데 필요한 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [작업 모니터 열기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [작업 모니터](../../relational-databases/performance-monitor/activity-monitor.md)     
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
 [쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)   
