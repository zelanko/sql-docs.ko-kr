---
title: 작업 활동 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- jobs [SQL Server Agent], monitoring
- monitoring [SQL Server], jobs
- activity monitoring [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- SQL Server Agent Job Activity Monitor
- SQL Server Agent jobs, monitoring
- performance [SQL Server], jobs
- current activity
ms.assetid: 71cb432b-631d-4b8b-9965-e731b3d8266d
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 37fb0194a7971809acc8227d8ac7a9cda95d73f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-job-activity"></a>작업 활동 모니터링
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 활동 모니터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 정의된 모든 작업의 현재 활동을 모니터링할 수 있습니다.  
  
## <a name="sql-server-agent-sessions"></a>SQL Server 에이전트 세션  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 서비스가 시작될 때마다 새 세션을 만듭니다. 새 세션이 만들어지면 **msdb** 데이터베이스의 **sysjobactivity** 테이블은 정의된 모든 기존 작업으로 채워집니다. 이 테이블은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 다시 시작되었을 때 작업에 대한 마지막 활동을 보존합니다. 각 세션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 정상 작업 활동을 작업 시작부터 끝까지 기록합니다. 이런 세션에 대한 정보는 **msdb** 데이터베이스의 **syssessions** 테이블에 저장됩니다.  
  
## <a name="job-activity-monitor"></a>작업 활동 모니터  
작업 활동 모니터에서는 **를 사용하여** sysjobactivity [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]테이블을 볼 수 있습니다. 서버의 모든 작업을 보거나 표시할 작업 수를 제한하는 필터를 정의할 수 있습니다. **에이전트 작업 활동** 표에서 열 머리글을 클릭하여 작업 정보를 정렬할 수도 있습니다. 예를 들어 **마지막 실행** 열 머리글을 선택하면 마지막으로 실행된 순서대로 작업을 볼 수 있습니다. 열 머리글을 다시 클릭하면 마지막 실행 날짜에 따라 작업이 오름차순이나 내림차순으로 전환됩니다.  
  
작업 활동 모니터를 사용하여 다음 태스크를 수행할 수 있습니다.  
  
-   작업을 시작 및 중지합니다.  
  
-   작업 속성을 표시합니다.  
  
-   특정 작업의 기록을 표시합니다.  
  
-   **에이전트 작업 활동** 표의 정보를 수동으로 새로 고치거나 **새로 고침 설정 보기**를 클릭하여 자동 새로 고침 간격을 설정합니다.  
  
작업 활동 모니터를 사용하여 실행이 예약된 작업과 현재 세션 동안 실행된 작업의 최종 결과를 알아보고 현재 실행 중이거나 유휴 상태의 작업을 알 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스가 예기치 않게 중지될 경우 작업 활동 모니터의 이전 세션을 살펴보면 실행 중이었던 작업을 알 수 있습니다.  
  
작업 활동 모니터를 열려면 **개체 탐색기에서** SQL Server 에이전트 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 를 확장하고 **작업 활동 모니터**를 마우스 오른쪽 단추로 클릭한 다음 **작업 활동 보기**를 클릭합니다.  
  
**sp_help_jobactivity**저장 프로시저를 사용하여 현재 세션의 작업 활동을 볼 수도 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**설명**|**항목**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업의 런타임 상태를 보는 방법에 대해 설명합니다.|[작업 활동 보기](../../ssms/agent/view-job-activity.md)|  
  
## <a name="see-also"></a>참고 항목  
[작업 활동 보기](../../ssms/agent/view-job-activity.md)  
[sysjobactivity(Transact-SQL)](http://msdn.microsoft.com/en-us/fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e)  
[syssessions(Transact-SQL)](http://msdn.microsoft.com/en-us/187819b6-c7f4-4a26-b74c-0a89e96695cf)  
[sp_help_jobactivity(Transact-SQL)](http://msdn.microsoft.com/en-us/d344864f-b4d3-46b1-8933-b81dec71f511)  
  
