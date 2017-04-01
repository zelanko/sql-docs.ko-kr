---
title: "SQL Server 에이전트, Alerts 개체 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Alerts 개체"
  - "SQLAgent:Alerts"
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# SQL Server 에이전트, Alerts 개체
  SQL Server 에이전트 **Alerts** 성능 개체는 SQL Server 에이전트 경고에 대한 정보를 보고하는 성능 카운터를 포함합니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
 다음 표에서는 **SQLAgent:Alerts** 카운터를 나열합니다.  
  
|이름|설명|  
|----------|-----------------|  
|**Activated alerts**|이 카운터는 SQL Server 에이전트가 마지막으로 다시 시작된 이후 SQL Server 에이전트가 활성화한 총 경고 수를 보고합니다.|  
|**Alerts activated/minute**|이 카운터는 마지막 시간(분) 내에 SQL Server 에이전트가 활성화한 경고의 수를 보고합니다.|  
  
> [!NOTE]  
>  이 SQL Server 에이전트 개체를 사용하려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## 참고 항목  
 [경고](../../ssms/agent/alerts.md)   
 [성능 개체 사용](../../ssms/agent/use-performance-objects.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  