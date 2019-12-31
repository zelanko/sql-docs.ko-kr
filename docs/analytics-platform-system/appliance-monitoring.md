---
title: 어플라이언스 모니터링
description: 이 어플라이언스 모니터링 가이드에서는 분석 플랫폼 시스템 어플라이언스를 모니터링 하기 위한 도구 및 태스크에 대해 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cec604ff1a93213fc6308455cadda90e6efa2d61
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401419"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 어플라이언스 모니터링
이 어플라이언스 모니터링 가이드에서는 분석 플랫폼 시스템 어플라이언스를 모니터링 하기 위한 도구 및 태스크에 대해 설명 합니다.  
  
## <a name="Basics"></a>기본 사항 및 도구 모니터링  
SQL Server PDW 어플라이언스에서 모니터링할 수 있는 값과 정보는 광범위 합니다. 예를 들어 일반적인 모니터링 작업은 다음과 같습니다.  
  
-   SQL Server PDW에서 발급 한 경고를 확인 합니다.  
  
-   실패 한 하드웨어 모니터링  
  
-   네트워크 연결 문제를 모니터링 합니다.  
  
-   쿼리를 처리 하는 동안 사용자에 게 반환 되는 오류를 확인 합니다.  
  
-   현재 활성 세션 및 쿼리 수를 표시 합니다.  
  
-   로드, 백업 및 복원의 상태를 확인 합니다.  
  
### <a name="appliance-monitoring-tools"></a>어플라이언스 모니터링 도구  
어플라이언스를 모니터링 하는 데 사용할 수 있는 여러 도구가 있습니다.  
  
관리 사용자  
SQL Server PDW에는 관리 콘솔이 있습니다. 쿼리, 로드, 백업 및 복원, 잠금, 세션, 경고 및 어플라이언스 상태에 대 한 정보를 표시 하는 웹 기반 도구입니다. 관리 콘솔은 어플라이언스에서 실행 됩니다. 사용자는 Internet Explorer를 통해 관리 콘솔에 연결 합니다. 자세한 내용은 다음을 참조하세요.  
  
-   [관리 콘솔 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 관리 콘솔 경고](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
시스템 뷰  
SQL Server PDW에는 어플라이언스 상태, 상태 및 성능에 대 한 자세한 정보를 얻을 수 있는 포괄적인 시스템 뷰가 포함 되어 있습니다. 모니터링 작업에 대 한 시스템 뷰 목록은 다음을 참조 하세요.  
  
-   [시스템 뷰 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW는 시스템 센터 Operations Manager와 광범위 하 게 통합 됩니다. SQL Server PDW 관리 팩은 무료로 다운로드할 수 있습니다. System Center를 사용 하 여 SQL Server PDW를 모니터링 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.  
  
-   [System Center Operations Manager &#40;Analytics Platform System을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
사용자 지정 솔루션  
데이터 센터 모니터링 도구에서 System Center를 사용할 수 없는 경우 타사 모니터링 솔루션을 사용 하 여 어플라이언스를 모니터링할 수 있습니다. 외부 소프트웨어 에이전트의 설치는 현재 PDW에서 지원 되지 않지만 대부분의 모니터링 솔루션은 Transact-sql\-통합을 지원 하므로 시스템 관리자는 pdw 어플라이언스에 대\-한 직접 transact-sql 쿼리를 구현할 수 있습니다.  
  
모니터링 솔루션에서 직접 Transact-sql\-SQL 쿼리를 지원 하지 않거나 모니터링 도구가 없는 경우 스크립트를 사용 하 여 경고가 발생 했을 때 전자 메일을 보내는 등의 모니터링 작업을 수행할 수 있습니다.  TechNet wiki에는 스크립팅된 모니터링 솔루션 예제가 포함 되어 있습니다.  
  
-   [SQL Server PDW에 대 한 Power Shell 모니터링 예제](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>관련 모니터링 태스크  
  
|모니터링 태스크|설명|  
|-------------------|---------------|  
|관리 콘솔을 사용 하 여 어플라이언스를 모니터링 합니다.|[관리 콘솔 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|시스템 뷰를 사용 하 여 어플라이언스를 모니터링 합니다.|[시스템 뷰 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-system-views.md)|  
|System Center를 사용 하 여 어플라이언스 모니터링|[System Center Operations Manager &#40;Analytics Platform System을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|어플라이언스의 상태를 모니터링 합니다.|[&#40;분석 플랫폼 시스템&#41;어플라이언스 상태를 모니터링 합니다.](monitor-appliance-health-state.md)|  
|하트 비트 모니터링.|[Microsoft &#40;SQL Server PDW에 원격 분석 피드백을 보냅니다&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|어플라이언스 경고를 추적 합니다.|[분석 플랫폼 시스템&#41;&#40;어플라이언스 경고 추적](track-appliance-alerts.md)|  
|사용 중인 용량의 크기를 확인 합니다.|[분석 플랫폼 시스템&#41;&#40;용량 사용률을 확인 합니다.](view-capacity-utilization.md)|  
|어플라이언스를 폴링하는 빈도를 결정 합니다.|[&#40;분석 플랫폼 시스템&#41;폴링 빈도를 결정 합니다.](determine-polling-frequency.md)|  
|클러스터 오류가 발생 하면 실패 한 클러스터 노드를 확인 합니다.|[분석 플랫폼 시스템 &#40;실패 한 클러스터 노드를 확인&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[기기 관리 작업 &#40;분석 플랫폼 시스템&#41;](appliance-management-tasks.md)  
  
