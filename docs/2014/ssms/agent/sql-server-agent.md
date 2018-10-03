---
title: SQL Server 에이전트 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, about SQL Server Agent
- automatic administration steps
ms.assetid: 8d1dc600-aabb-416f-b3af-fbc9fccfd0ec
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e0f1e8f3e76ffbe84495fc7bae6229a1b590089
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211933"
---
# <a name="sql-server-agent"></a>SQL Server 에이전트
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 *에서* 작업 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]이라고 하는 일정이 지정된 관리 태스크를 실행하는 Microsoft Windows 서비스입니다.  
  
 **항목 내용**  
  
-   [SQL Server 에이전트의 이점](#Benefits)  
  
-   [SQL Server 에이전트 구성 요소](#Components)  
  
-   [SQL Server 에이전트 관리 보안](#Security)  
  
##  <a name="Benefits"></a> SQL Server 에이전트의 이점  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 작업 정보를 저장합니다. 작업에는 하나 이상의 작업 단계가 포함됩니다. 각 단계에는 자체 태스크(예: 데이터베이스 백업)가 포함됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 특정 이벤트에 대한 응답이나 요청에 따라 일정에 있는 작업을 실행할 수 있습니다. 예를 들어 평일 근무 시간 이후에 회사 서버를 모두 백업하려는 경우 이 태스크를 자동화할 수 있습니다. 월요일부터 금요일까지 밤 10시 이후 백업이 실행되도록 일정을 만듭니다. 이 백업에 문제가 발생하면 SQL Server 에이전트가 이 이벤트를 기록하여 사용자에게 알릴 수 있습니다.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 자동으로 시작되도록 사용자가 명시적으로 선택하지 않으면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 시 해제됩니다.  
  
##  <a name="Components"></a> SQL Server 에이전트 구성 요소  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서는 다음 구성 요소를 사용하여 수행될 태스크, 태스크를 수행할 시기 및 태스크의 성공 또는 실패를 보고하는 방법을 정의합니다.  
  
### <a name="jobs"></a>에서  
 *작업* 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 수행하도록 지정된 일련의 동작입니다. 작업을 사용하면 한 번 이상 실행되고 성공과 실패에 대해 모니터링될 수 있는 관리 태스크를 정의할 수 있습니다. 작업은 한 대의 로컬 서버나 다중 원격 서버에서 실행될 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스에서 장애 조치 이벤트가 발생할 때 실행하고 있던 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 다른 장애 조치 클러스터 노드로 장애가 조치된 후 다시 시작되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Hyper-V 노드가 일시 중지될 때 실행되고 있던 에이전트 작업은 일시 중지로 인해 다른 노드로 장애 조치(failover)될 경우 다시 시작되지 않습니다. 시작되었지만 장애 조치(failover) 이벤트로 인해 완료되지 못한 작업은 시작된 것으로 기록되지만 완료 또는 실패의 추가 로그 항목이 표시되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 종료되지 않은 것처럼 나타납니다.  
  
 작업을 실행하는 방법은 다음과 같습니다.  
  
-   1회 이상의 일정에 따라 실행됩니다.  
  
-   하나 이상의 경고에 응답하여 실행됩니다.  
  
-   sp_start_job 저장 프로시저를 실행하는 방법으로 실행됩니다.  
  
 작업 내 각 동작은 *작업 단계*입니다. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하거나 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지를 실행하거나 Analysis Services 서버로 명령을 실행하는 것으로 작업 단계를 구성할 수 있습니다. 작업 단계는 작업의 일부로 관리됩니다.  
  
 각 작업 단계는 특정 보안 컨텍스트에서 실행됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하는 작업 단계의 경우 EXECUTE AS 문을 사용하여 해당 작업 단계에 대한 보안 컨텍스트를 설정합니다. 다른 작업 단계 유형의 경우에는 프록시 계정을 사용하여 해당 작업 단계에 대한 보안 컨텍스트를 설정합니다.  
  
### <a name="schedules"></a>일정  
 *일정* 은 작업이 실행되는 시기를 지정합니다. 같은 일정으로 둘 이상의 작업을 실행할 수 있으며 같은 작업에 둘 이상의 일정을 적용할 수 있습니다. 일정은 작업이 실행되는 시간에 대해 다음 조건을 정의할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 시작할 때마다  
  
-   컴퓨터의 CPU 사용률이 유휴로 정의한 수준에 있을 때마다  
  
-   특정 날짜와 특정 시간에 한 번  
  
-   되풀이되는 일정에 따라  
  
 자세한 내용은 [일정을 만들고 작업에 연결](create-and-attach-schedules-to-jobs.md)을 참조하세요.  
  
### <a name="alerts"></a>,  
 *경고* 는 특정 이벤트에 대한 자동 응답입니다. 예를 들어 이벤트는 시작되는 작업 또는 특정 임계값에 도달한 시스템 리소스일 수 있습니다. 경고가 발생할 조건을 정의합니다.  
  
 경고는 다음 조건 중 하나에 대해 응답할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 조건  
  
-   SQL Server 에이전트가 실행 중인 컴퓨터의 Microsoft WMI(Windows Management Instrumentation) 이벤트  
  
 경고는 다음 동작을 수행할 수 있습니다.  
  
-   한 명 이상의 운영자에게 알림  
  
-   작업 실행  
  
 자세한 내용은 [경고](alerts.md)를 참조하세요.  
  
### <a name="operators"></a>연산자  
 *운영자* 는 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 유지 관리하는 개인에 대한 연락처 정보를 정의합니다. 일부 기업의 경우 운영자의 업무는 한 명에게 할당되기도 합니다. 다중 서버를 사용하는 기업의 경우에는 여러 명이 운영자의 업무를 분담할 수 있습니다. 운영자는 보안 정보가 보유하지 않으며 보안 주체를 정의하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 다음 중 하나 이상을 통해 운영자에게 경고를 알릴 수 있습니다.  
  
-   전자 메일  
  
-   호출기(전자 메일 사용)  
  
-   **Net Send**  
  
> [!NOTE]  
>  **net send**를 사용하여 알림을 보내려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 상주하는 컴퓨터에서 Windows Messenger 서비스를 시작해야 합니다.  
  
> [!IMPORTANT]  
>  **이후 버전에서는** 에이전트에서 호출기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net send [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]옵션이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
 전자 메일 또는 호출기를 사용하여 운영자에게 알림을 보내려면 데이터베이스 메일을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성해야 합니다. 자세한 내용은 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)을 참조하세요.  
  
 개인으로 구성된 그룹의 별칭으로 운영자를 정의할 수 있습니다. 이런 방법으로 해당 별칭에 속하는 모든 멤버는 동시에 알림을 받습니다. 자세한 내용은 [운영자](operators.md)를 참조하세요.  
  
##  <a name="Security"></a> SQL Server 에이전트 관리 보안  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용 하는 **SQLAgentUserRole**를 **SQLAgentReaderRole**, 및 **SQLAgentOperatorRole** 고정 데이터베이스 역할의 **msdb** 액세스를 제어 하는 데이터베이스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 멤버가 아닌 사용자에 대 한 에이전트의는 `sysadmin` 고정된 서버 역할입니다. 이러한 고정 데이터베이스 역할 외에도 데이터베이스 관리자는 하위 시스템과 프록시를 사용하여 각 작업 단계가 태스크 수행에 필요한 최소 권한으로 실행되도록 합니다.  
  
### <a name="roles"></a>역할  
 멤버는 **SQLAgentUserRole**를 **SQLAgentReaderRole**, 및 **SQLAgentOperatorRole** 고정 데이터베이스 역할 **msdb**, 및 멤버는 `sysadmin` 고정된 서버 역할에 액세스할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트입니다. 이러한 역할 중 하나에 속하지 않는 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용하는 역할에 대한 자세한 내용은 [SQL Server 에이전트 보안 구현](implement-sql-server-agent-security.md)을 참조하세요.  
  
### <a name="subsystems"></a>하위 시스템  
 하위 시스템은 작업 단계에서 사용할 수 있는 기능을 나타내는 미리 정의된 개체입니다. 각 프록시는 하나 이상의 하위 시스템에 액세스할 수 있습니다. 하위 시스템은 프록시에 사용할 수 있는 기능에 대한 액세스를 구분하므로 보안을 제공합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계를 제외한 각 작업 단계는 프록시 컨텍스트에서 실행됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계는 EXECUTE AS 명령을 사용하여 보안 컨텍스트를 설정합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 정의되어 있는 하위 시스템을 나열합니다.  
  
|하위 시스템 이름|Description|  
|--------------------|-----------------|  
|Microsoft ActiveX 스크립트|ActiveX 스크립팅 작업 단계를 실행합니다.<br /><br /> **\*\* 중요 \* \***  ActiveX 스크립팅 하위 시스템에서 제거 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이후 버전에서 에이전트 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.|  
|운영 체제(**CmdExec**)|실행 프로그램을 실행합니다.|  
|PowerShell|PowerShell 스크립팅 작업 단계를 실행합니다.|  
|복제 배포자|복제 배포 에이전트를 활성화하는 작업 단계를 실행합니다.|  
|복제 병합|복제 병합 에이전트를 활성화하는 작업 단계를 실행합니다.|  
|복제 큐 판독기|복제 큐 판독기 에이전트를 활성화하는 작업 단계를 실행합니다.|  
|복제 스냅숏|복제 스냅숏 에이전트를 활성화하는 작업 단계를 실행합니다.|  
|복제 트랜잭션 로그 판독기|복제 로그 판독기 에이전트를 활성화하는 작업 단계를 실행합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령을 실행합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Query|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 쿼리를 실행합니다.|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지를 실행합니다.|  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계에서는 프록시를 사용하지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업 단계에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에이전트 하위 시스템이 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 프록시의 보안 주체에게 일반적으로 작업 단계에서 태스크를 실행할 권한이 있더라도 하위 시스템 제한 설정을 강화합니다. 예를 들어 사용자가 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지를 실행할 수 있더라도 프록시에서 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 하위 시스템에 액세스할 수 없으면 sysadmin 고정 서버 역할의 멤버인 사용자의 프록시는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 작업 단계를 실행할 수 없습니다.  
  
### <a name="proxies"></a>프록시  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 프록시를 사용하여 보안 컨텍스트를 관리합니다. 프록시는 둘 이상의 작업 단계에서 사용할 수 있습니다. 멤버는 `sysadmin` 고정된 서버 역할에서 프록시를 만들 수 있습니다.  
  
 각 프록시는 보안 자격 증명에 해당됩니다. 각 프록시는 하위 시스템 집합 및 로그인 집합과 연결할 수 있으며 프록시는 해당 프록시와 연결된 하위 시스템을 사용하는 작업 단계에서만 사용할 수 있습니다. 특정 프록시를 사용하는 작업 단계를 만들려면 작업 소유자가 해당 프록시와 연결된 로그인을 사용하거나 프록시에 무제한 액세스할 수 있는 역할의 멤버여야 합니다. 멤버는 `sysadmin` 고정된 서버 역할 액세스 프록시에 무제한입니다. **SQLAgentUserRole**, **SQLAgentReaderRole**또는 **SQLAgentOperatorRole** 의 멤버는 특정 액세스 권한이 부여된 프록시만 사용할 수 있습니다. 이러한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할의 멤버인 각 사용자에게 특정 프록시에 대한 액세스 권한을 부여해야만 사용자가 해당 프록시를 사용하는 작업 단계를 만들 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다음 단계를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리를 자동화하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성합니다.  
  
1.  정기적으로 발생하는 관리 태스크나 서버 이벤트를 설정하고 이러한 작업 또는 이벤트를 프로그래밍 방식으로 관리할 수 있는지 여부를 설정합니다. 태스크가 예측 가능한 단계 순서를 포함하고 특정 시간에 또는 특정 사건에 대한 응답으로 발생하는 경우 자동화될 수 있습니다.  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 또는 SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체)를 사용하여 작업, 일정, 경고 및 연산자 집합을 정의합니다. 자세한 내용은 [작업 만들기](create-jobs.md)를 참조하세요.  
  
3.  정의한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 실행합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스는 이름이 SQLSERVERAGENT입니다. 명명된 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 이름이 SQLAgent$*instancename*입니다.  
  
 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 실행하는 경우 다중 서버 관리를 사용하여 전체 인스턴스에 걸쳐 공통되는 태스크를 자동화할 수 있습니다. 자세한 내용은 [기업 내 관리 자동화](automated-administration-across-an-enterprise.md)를 참조하세요.  
  
 다음 태스크를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 시작합니다.  
  
|||  
|-|-|  
|**설명**|**항목**|  
|SQL Server 에이전트를 구성하는 방법을 설명합니다.|[SQL Server 에이전트 구성](configure-sql-server-agent.md)|  
|SQL Server 에이전트 서비스를 시작, 중지 및 일시 중지하는 방법을 설명합니다.|[SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](start-stop-or-pause-the-sql-server-agent-service.md)|  
|SQL Server 에이전트 서비스의 계정을 지정하기 위한 고려 사항을 설명합니다.|[SQL Server 에이전트 서비스의 계정 선택](select-an-account-for-the-sql-server-agent-service.md)|  
|SQL Server 에이전트 오류 로그를 사용하는 방법을 설명합니다.|[SQL Server 에이전트 오류 로그](sql-server-agent-error-log.md)|  
|||  
|성능 개체를 사용하는 방법을 설명합니다.|[성능 개체 사용](use-performance-objects.md)|  
|SQL Server 인스턴스의 관리를 자동화할 수 있도록 작업, 경고 및 운영자를 만드는 데 사용할 수 있는 유틸리티인 유지 관리 계획 마법사에 대해 설명합니다.|[유지 관리 계획 마법사 사용](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|SQL Server 에이전트를 사용하여 관리 태스크를 자동화하는 방법을 설명합니다.|[관리 태스크 자동화&#40;SQL Server 에이전트&#41;](automated-administration-tasks-sql-server-agent.md)|  
  
## <a name="see-also"></a>관련 항목  
 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md)  
  
  
