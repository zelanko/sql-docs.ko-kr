---
title: "SQL Server 에이전트, JobSteps 개체 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6d6953a342ab24540da33464962712ea43579f8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-agent-jobsteps-object"></a>SQL Server 에이전트, JobSteps 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 **JobSteps** 성능 개체에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계에 대한 정보를 보고하는 성능 카운터가 포함되어 있습니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
 아래 표에는 **SQLAgent:JobSteps** 카운터가 있습니다.  
  
|이름|설명|  
|----------|-----------------|  
|**Active steps**|이 카운터는 현재 실행 중인 작업 단계 수를 보고합니다.|  
|**Queued steps**|이 카운터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행될 준비가 되어 있지만 아직 실행이 시작되지 않은 작업 단계 수를 보고합니다.|  
|**Total step retries**|이 카운터는 마지막 서버 다시 시작 이후에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 작업 단계를 다시 시도한 총 횟수를 보고합니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|인스턴스|설명|  
|--------------|-----------------|  
|**_Total**|모든 작업 단계에 대한 정보입니다.|  
|**ActiveScripting**|**ActiveScripting** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**ANALYSISCOMMAND**|ANALYSISCOMMAND 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**ANALYSISQUERY**|ANALYSISQUERY 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**CmdExec**|**CmdExec** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**배포**|**Distribution** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**Dts**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**LogReader**|**LogReader** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**병합**|**Merge** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**PowerShell**|**PowerShell** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**QueueReader**|**QueueReader** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**스냅숏**|**Snapshot** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**TSQL**|[!INCLUDE[tsql](../../includes/tsql-md.md)]을 실행하는 작업 단계에 대한 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [작업 단계 관리](http://msdn.microsoft.com/library/51352afc-a0a4-428b-8985-f9e58bb57c31)   
 [성능 개체 사용](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
