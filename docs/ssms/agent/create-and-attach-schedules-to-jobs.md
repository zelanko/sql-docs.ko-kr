---
title: 일정을 만들고 작업에 연결 | Microsoft 문서
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
- jobs [SQL Server]
- scheduling jobs [SQL Server]
- jobs [SQL Server], scheduling
- CPU [SQL Server], idle conditions
- automatic job processing
- SQL Server Agent jobs, scheduling
- idle time [SQL Server]
ms.assetid: 079c2984-0052-4a37-a2b8-4ece56e6b6b5
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9aa5c92c0579fdcda7ca336e4893b1a5417dfaa0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33045080"
---
# <a name="create-and-attach-schedules-to-jobs"></a>일정을 만들고 작업에 연결
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 일정 예약이란 사용자 개입 없이 작업을 실행할 조건을 정의하는 것입니다. 작업에 대한 새로운 일정을 만들거나 기존 일정을 작업에 연결하여 작업이 자동으로 실행되도록 예약할 수 있습니다.  
  
일정을 만드는 방법에는 두 가지가 있습니다.  
  
-   작업을 만드는 동안 일정을 만듭니다.  
  
-   개체 탐색기에서 일정을 만듭니다.  
  
일정을 만든 후에는 특정 작업을 위해 만든 일정이더라도 여러 작업에 연결할 수 있습니다. 또한 작업에 연결된 일정을 분리할 수도 있습니다.  
  
일정은 시간 또는 이벤트에 기반을 둘 수 있습니다. 예를 들어 다음과 같은 시간에 작업이 실행되도록 예약할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 시작할 때마다  
  
-   컴퓨터의 CPU 사용률이 유휴로 정의한 수준에 있을 때마다  
  
-   특정 날짜와 특정 시간에 한 번  
  
-   되풀이되는 일정에 따라  
  
작업을 실행하여 이벤트에 응답하는 경고를 만들어 작업 일정을 대체할 수도 있습니다.  
  
> [!NOTE]  
> 하나의 작업 인스턴스만 동시에 실행될 수 있습니다. 일정대로 작업이 실행될 때 작업을 수동으로 실행하려고 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 요청을 거부합니다.  
  
예약된 작업이 실행되지 않도록 하려면 다음 중 하나를 수행해야 합니다.  
  
-   일정을 비활성화합니다.  
  
-   작업을 비활성화합니다.  
  
-   작업에 연결된 일정을 분리합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 중지합니다.  
  
-   일정을 삭제합니다.  
  
일정이 활성화되어 있지 않은 경우 경고에 응답하거나 사용자가 작업을 수동으로 실행할 때도 작업을 계속 실행할 수 있습니다. 작업 일정이 활성화되어 있지 않으면 해당 일정을 사용하는 모든 작업의 일정이 활성화되지 않습니다.  
  
일정이 해제되었으면 명시적으로 다시 활성화해야 합니다. 일정을 편집해도 일정이 자동으로 다시 활성화되지는 않습니다.  
  
## <a name="scheduling-start-dates"></a>시작 날짜 예약  
일정의 시작 날짜는 19900101 이상이어야 합니다.  
  
일정을 작업에 연결할 때는 일정이 처음으로 작업을 실행할 시작 날짜를 검토해야 합니다. 시작 날짜는 일정을 작업에 연결한 날짜 및 시간에 따라 달라집니다. 예를 들어 격주로 월요일 오전 8:00시에 실행되는 일정을 만들고 2008년 3월 3일 월요일 오전 10:00시에 작업을 만드는 경우 일정 시작 날짜는 2008년 3월 17일 월요일입니다. 다른 작업을 2008년 3월 4일 화요일에 만드는 경우에는 일정 시작 날짜가 2008년 3월 10일 월요일입니다.  
  
일정을 작업에 연결한 후에 일정 시작 날짜를 변경할 수 있습니다.  
  
## <a name="cpu-idle-schedules"></a>CPU 유휴 일정  
CPU 리소스를 최대화하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에 대해 CPU 유휴 상태를 정의할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 CPU 유휴 상태 설정을 사용하여 작업 실행의 최적 시기를 결정합니다. 예를 들어 CPU 유휴 시간과 프로덕션 속도가 느린 시간에 인덱스를 다시 구축하도록 작업을 예약할 수 있습니다.  
  
CPU 유휴 시간 동안 작업이 실행되도록 정의하기 전에 정상적인 처리 동안 CPU의 로드를 결정하십시오. 이렇게 하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler_md.md)] 또는 성능 모니터를 사용하여 서버 트래픽을 모니터링하고 통계 자료를 수집합니다. 수집한 정보를 사용하여 CPU 유휴 시간 백분율과 지속 시간을 설정할 수 있습니다.  
  
CPU 유휴 조건을 CPU 사용이 지정된 시간 동안 그 이하로 유지되어야 하는 백분율로 정의하십시오. 그런 다음 시간을 설정하십시오. CPU 사용률이 지정한 시간에 대해 지정한 백분율 미만이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 CPU 유휴 시간 일정이 예정된 모든 작업을 시작합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler_md.md)] 또는 성능 모니터를 사용하여 CPU 사용률을 모니터링하는 방법은 [CPU 사용 모니터링](http://msdn.microsoft.com/en-us/2a02a3b6-07b2-4ad0-8a24-670414d19812)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**설명**|**항목**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업에 대한 예약을 만드는 방법에 대해 설명합니다.|[Create a Schedule](../../ssms/agent/create-a-schedule.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업을 예약하는 방법에 대해 설명합니다.|[작업 예약](../../ssms/agent/schedule-a-job.md)|  
|서버의 CPU 유휴 상태 판단 기준을 정의하는 방법에 대해 설명합니다.|[CPU 유휴 시간 및 기간 설정&#40;SQL Server Management Studio&#41;](../../ssms/agent/set-cpu-idle-time-and-duration-sql-server-management-studio.md)|  
  
## <a name="see-also"></a>참고 항목  
[sp_help_jobschedule](http://msdn.microsoft.com/en-us/2cded902-9272-4667-ac4b-a4f95a9f008e)  
[sysjobschedules](http://msdn.microsoft.com/en-us/ccdafec7-2a9b-4356-bffb-1caa3a12db59)  
  
