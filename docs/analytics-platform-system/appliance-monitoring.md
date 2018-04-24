---
title: 어플라이언스 모니터링-분석 플랫폼 시스템 | Microsoft Docs
description: 이 어플라이언스 모니터링 가이드 도구 및 분석 플랫폼 시스템 기기를 모니터링 하기 위한 작업을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f87734a14337e7e35655439ddf70f0a126147eb7
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>어플라이언스 분석 플랫폼 시스템에 대 한 모니터링
이 어플라이언스 모니터링 가이드 도구 및 분석 플랫폼 시스템 기기를 모니터링 하기 위한 작업을 설명 합니다.  
  
## <a name="Basics"></a>기본 사항 및 도구를 모니터링합니다.  
값 및 SQL Server PDW 어플라이언스에 모니터링할 수 있는 정보는 광범위 한입니다. 예를 들어 다음은 일반적인 작업을 모니터링 합니다.  
  
-   SQL Server PDW에서 발급 한 모든 경고를 확인 합니다.  
  
-   오류가 발생 한 하드웨어를 모니터링 합니다.  
  
-   네트워크 연결 문제를 모니터링 합니다.  
  
-   쿼리를 처리 하는 동안 사용자에 게 반환 되는 오류를 확인 합니다.  
  
-   현재 활성 세션 및 쿼리 수를 표시 합니다.  
  
-   부하, 백업 및 복원의 상태를 확인 합니다.  
  
### <a name="appliance-monitoring-tools"></a>어플라이언스 모니터링 도구  
어플라이언스를 모니터링할 수 있는 여러 도구가 있습니다.  
  
관리 사용자  
SQL Server PDW 관리 콘솔에 있습니다. 이 쿼리, 로드, 백업 및 복원, 잠금, 세션, 경고 및 기기 상태에 대 한 정보를 표시 하는 웹 기반 도구입니다. 관리 콘솔 어플라이언스;에서 실행 됩니다. 사용자가 Internet Explorer를 통해 관리 콘솔에 연결 합니다. 참조 항목:  
  
-   [관리 콘솔을 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 관리 콘솔 경고](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
시스템 뷰  
SQL Server PDW 어플라이언스 상태, 상태 및 성능에 대 한 자세한 정보를 얻을 수 있도록 하는 포괄적인 시스템 뷰를 포함 합니다. 모니터링 작업에 대 한 시스템 뷰 목록, 참조:  
  
-   [시스템 뷰를 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW에 Systems Center Operations Manager와 함께 광범위 하 게 통합 되었습니다. SQL Server PDW 용 관리 팩은 무료 다운로드로 제공 합니다. System Center를 사용 하 여 SQL Server PDW를 모니터링 하는 방법에 대 한 자세한 내용은 다음을 참조 합니다.  
  
-   [System Center Operations Manager를 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
사용자 지정 솔루션  
상황에 대 한 모니터링 도구를 데이터 센터와 System Center를 사용할 수 없는 경우 모니터링할 수 있습니다 기기 제 3 자 모니터링 솔루션을 사용 하 여 합니다. 외부 소프트웨어 에이전트의 설치는 현재 PDW에서 지원 되지 않지만 대부분의 모니터링 솔루션 지원 Transact\-SQL 통합, 시스템 관리자는 직접 Transact 구현할 수 있도록\-프로그램 PDW에 대 한 SQL 쿼리 구성할 수 있습니다.  
  
모니터링 솔루션 직접 Transact를 지원 하지 않는 경우\-SQL 쿼리를 보거나 변경할 필요가 없습니다 모니터링 도구를 한 다음 스크립트를 사용 하 여 경고가 발생할 때 전자 메일을 보내는 것과 같은 모니터링 작업을 수행할 수 있습니다.  TechNet wiki 스크립팅된 모니터링 솔루션 예제를 포함합니다.  
  
-   [SQL Server PDW에 대 한 예제를 모니터링 하는 power Shell](http://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>작업 모니터링 관련  
  
|모니터링 작업|Description|  
|-------------------|---------------|  
|관리 콘솔을 사용 하 여 어플라이언스에 모니터링 합니다.|[관리 콘솔을 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|시스템 뷰를 사용 하 여 어플라이언스에 모니터링 합니다.|[시스템 뷰를 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-system-views.md)|  
|System Center를 사용 하 여 어플라이언스에 모니터|[System Center Operations Manager를 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|어플라이언스의 상태를 모니터링 합니다.|[모니터 어플라이언스 상태 &#40;분석 플랫폼 시스템&#41;](monitor-appliance-health-state.md)|  
|하트 비트 모니터링 합니다.|[Microsoft 원격 분석 의견을 보내도록 &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|기기 경고를 추적 합니다.|[기기 경고 추적 &#40;분석 플랫폼 시스템&#41;](track-appliance-alerts.md)|  
|용량 사용 중인지 확인 합니다.|[용량 사용률을 볼 &#40;분석 플랫폼 시스템&#41;](view-capacity-utilization.md)|  
|어플라이언스에 폴링 빈도 결정 합니다.|[폴링 빈도 결정 &#40;분석 플랫폼 시스템&#41;](determine-polling-frequency.md)|  
|클러스터 오류가 발생할 때 결정 클러스터 노드 실패 했습니다.|[클러스터 노드 실패를 결정 &#40;분석 플랫폼 시스템&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>관련 항목:  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[어플라이언스 관리 작업 &#40;분석 플랫폼 시스템&#41;](appliance-management-tasks.md)  
  
