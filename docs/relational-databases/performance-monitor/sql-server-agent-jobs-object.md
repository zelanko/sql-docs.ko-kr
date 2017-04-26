---
title: "SQL Server 에이전트, Jobs 개체 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8f2931c070c0ed3816fb348b4ca41f3705b19a0
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-agent-jobs-object"></a>SQL Server 에이전트, Jobs 개체
  SQL Server 에이전트 **Jobs** 성능 개체에는 SQL Server 에이전트 작업에 관한 정보를 보고하는 성능 카운터가 포함되어 있습니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
 이 표에는 **SQLAgent:Jobs** 카운터가 포함되어 있습니다.  
  
|이름|설명|  
|----------|-----------------|  
|**Active Jobs**|이 카운터는 현재 실행 중인 작업의 수를 보고합니다.|  
|**Failed jobs**|이 카운터는 오류 발생으로 종료된 작업의 수를 보고합니다.|  
|**Job success rate**|이 카운터는 성공적으로 완료된 실행 작업의 비율을 보고합니다.|  
|**Jobs activated/minute**|이 카운터는 마지막 1분간 실행된 작업의 수를 보고합니다.|  
|**Queued jobs**|이 카운터는 SQL Server 에이전트에서 실행할 준비가 완료되었지만 아직 실행되지 않은 작업의 수를 보고합니다.|  
|**Successful jobs**|이 카운터는 성공적으로 종료된 작업의 수를 보고합니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|인스턴스|설명|  
|--------------|-----------------|  
|**_Total**|모든 작업에 대한 정보입니다.|  
|**경고**|경고에 의해 시작된 작업의 정보입니다.|  
|**Others**|경고나 일정에 의해 시작되지 않은 작업의 정보입니다. 대개 이런 작업은 **sp_start_job**을 사용하여 수동으로 시작됩니다.|  
|**일정**|일정에 의해 시작된 작업의 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [작업 구현](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [성능 개체 사용](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
