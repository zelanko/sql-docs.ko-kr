---
title: 성능 대시보드 | Microsoft Docs
description: SQL Server 및 Azure SQL Managed Instance에 대한 신속한 인사이트를 제공하는 SQL Server Management Studio Performance 대시보드에 대해 알아봅니다.
ms.custom: ''
ms.date: 11/13/2020
ms.prod: sql
ms.reviewer: wiassaf
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- performance dashboard [SQL Server]
- performance dashboard reports
- perf dashboard
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: pelopes
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 03bd2039fc132724ba78222c81a79c75f37764ff
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505132"
---
# <a name="performance-dashboard"></a>성능 대시보드
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 버전 17.2 이상에는 성능 대시보드가 포함되어 있습니다. 이 대시보드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]부터 시작) 및 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] Managed Instance의 성능 상태에 대한 빠른 인사이트를 시각적으로 제공하도록 설계되었습니다. 

성능 대시보드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]에 성능 병목 상태가 있는지 여부를 신속하게 식별하는 데 도움이 됩니다. 그리고 병목 상태가 있으면 문제를 해결하는 데 필요한 추가 진단 데이터를 쉽게 캡처할 수 있습니다. 성능 대시보드가 식별하는 데 도움이 되는 몇 가지 일반적인 성능 문제는 다음과 같습니다.
-  CPU 병목 상태(및 대부분의 CPU를 사용하고 있는 쿼리)
-  I/O 병목 상태(및 대부분의 IO를 수행하고 있는 쿼리)
-  쿼리 최적화에서 생성된 인덱스 권장 구성(누락된 인덱스)
-  차단
-  리소스 경합(래치 경합 포함)

또한 성능 대시보드는 이전에 실행되었을 수 있는 고가의 쿼리를 식별하는 데 도움이 되며 높은 비용을 정의하는 데 사용할 수 있는 몇 가지 메트릭이 있습니다. CPU, 논리적 쓰기, 논리적 읽기, 기간, 물리적 읽기 및 CLR 시간.

성능 대시보드는 다음 섹션과 하위 보고서로 구분됩니다.
-  시스템 CPU 사용률
-  현재 대기 중인 요청
-  현재 작업
   -  사용자 요청
   -  사용자 세션
   -  캐시 적중률
-  기록 정보
   -  대기
   -  래치
   -  I/O 통계
   -  비용이 높은 쿼리
- 기타 정보
  -  활성 추적
  -  활성 xEvent 세션
  -  데이터베이스
  -  누락된 인덱스

> [!NOTE] 
> 내부적으로 성능 대시보드는 [실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md), [인덱스](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md) 및 [I/O](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md) 관련 동적 관리 보기(DMV) 및 함수(DMF)를 사용합니다.

## <a name="to-view-the-performance-dashboard"></a>성능 대시보드를 보려면 
  
성능 대시보드를 보려면 개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 마우스 오른쪽 단추로 클릭하고, **보고서**, **표준 보고서** 를 선택하고, **성능 대시보드** 를 클릭합니다.  
  
![메뉴의 성능 대시보드](../../relational-databases/performance/media/perf_dashboard_ssms.png "메뉴의 성능 대시보드")  
  
성능 대시보드는 새 탭으로 표시됩니다. CPU 병목 현상이 명확하게 표시되는 예제는 아래와 같습니다.  
  
![성능 대시보드 주 화면](../../relational-databases/performance/media/perf_dashboard.png "성능 대시보드 주 화면")  
  
## <a name="remarks"></a>설명
**누락된 인덱스** 보고서는 쿼리 컴파일 중에 쿼리 최적화 프로그램에서 식별한 잠재적으로 누락된 인덱스를 보여줍니다. 그러나 이러한 권장 사항은 액면 그대로 받아들여서는 안됩니다. Microsoft는 점수가 100,000보다 큰 인덱스는 사용자 쿼리에 대해 예상되는 개선 효과가 가장 높기 때문에 이러한 인덱스 생성을 위해 평가해야 한다고 권장합니다. 

> [!TIP]
> 새 인덱스 제안이 동일한 테이블의 기존 인덱스와 비교 가능한지 항상 평가합니다. 새 인덱스를 만드는 대신 기존 인덱스를 변경하여 동일한 실용적인 결과를 얻을 수 있습니다. 예를 들어 C1, C2 및 C3 열에 새로운 제안 인덱스를 지정하면 먼저 C1, C2 열을 통해 기존 지수가 있는지 평가합니다. 그렇다면 새 만들지 않도록 기존 인덱스에 C3 열을 단순히 추가하는 것이 바람직할 수 있습니다(기존 열 순서 유지).
> 자세한 내용은 [인덱스 아키텍처 및 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

**대기** 보고서는 모든 유휴 상태 및 일시 중지 대기 상태를 필터링합니다. 대기에 대한 자세한 내용은 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) 및 [대기 및 큐를 사용하는 SQL Server 2005 성능 튜닝](https://download.microsoft.com/download/4/7/a/47a548b9-249e-484c-abd7-29f31282b04d/performance_tuning_waits_queues.doc)을 참조하세요.

기본 DMV의 데이터가 선택 취소되어 있으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 다시 시작될 때 **고비용 쿼리** 가 다시 설정됩니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 고비용 쿼리에 대한 자세한 내용은 쿼리 저장소에서 확인할 수 있습니다. 


> [!NOTE]
> 성능 대시보드는 [SQL Server 2005](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2005-Performance-Dashboard-Reports/ba-p/315415)에 대한 독립형 다운로드로 처음 릴리스되었으며, 이후 [SQL Server 2012](https://www.microsoft.com/download/details.aspx?id=29063)용으로 업데이트되었습니다. SQL Server Management Studio 보고서 렌더러는 보고서에 포함된 텍스트에 대한 클립보드 액세스를 지원하지 않지만, 독립 실행형 보고서를 통해 텍스트에 액세스할 수 있습니다.  보고서에서 쿼리 텍스트를 복사해야 하는 경우 독립 실행형 보고서를 다운로드합니다.

## <a name="permissions"></a>사용 권한  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 `VIEW SERVER STATE` 및 `ALTER TRACE` 권한이 필요합니다. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]에서 데이터베이스에 대한 `VIEW DATABASE STATE` 권한이 필요합니다.

## <a name="see-also"></a>참고 항목  
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [작업 모니터 열기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [작업 모니터](../../relational-databases/performance-monitor/activity-monitor.md)     
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
