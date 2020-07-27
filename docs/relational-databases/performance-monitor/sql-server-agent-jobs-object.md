---
title: SQL Server 에이전트, Jobs 개체 | Microsoft 문서
description: SQL Server 에이전트 작업에 관한 정보를 보고하는 성능 카운터를 포함하는 SQL Server 에이전트 Jobs 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: d791edff7b4f9aa5dd8693bfec5b146fb44bb0c9
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458451"
---
# <a name="sql-server-agent-jobs-object"></a>SQL Server 에이전트, Jobs 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SQL Server 에이전트 **Jobs** 성능 개체에는 SQL Server 에이전트 작업에 관한 정보를 보고하는 성능 카운터가 포함되어 있습니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
 이 표에는 **SQLAgent:Jobs** 카운터가 포함되어 있습니다.  
  
|Name|Description|  
|----------|-----------------|  
|**Active Jobs**|이 카운터는 현재 실행 중인 작업의 수를 보고합니다.|  
|**Failed jobs**|이 카운터는 오류 발생으로 종료된 작업의 수를 보고합니다.|  
|**Job success rate**|이 카운터는 성공적으로 완료된 실행 작업의 비율을 보고합니다.|  
|**Jobs activated/minute**|이 카운터는 마지막 1분간 실행된 작업의 수를 보고합니다.|  
|**Queued jobs**|이 카운터는 SQL Server 에이전트에서 실행할 준비가 완료되었지만 아직 실행되지 않은 작업의 수를 보고합니다.|  
|**Successful jobs**|이 카운터는 성공적으로 종료된 작업의 수를 보고합니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|인스턴스|Description|  
|--------------|-----------------|  
|**_Total**|모든 작업에 대한 정보입니다.|  
|**경고**|경고에 의해 시작된 작업의 정보입니다.|  
|**Others**|경고나 일정에 의해 시작되지 않은 작업의 정보입니다. 대개 이런 작업은 **sp_start_job**을 사용하여 수동으로 시작됩니다.|  
|**일정**|일정에 의해 시작된 작업의 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [작업 구현](../../ssms/agent/implement-jobs.md)   
 [성능 개체 사용](../../ssms/agent/use-performance-objects.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
