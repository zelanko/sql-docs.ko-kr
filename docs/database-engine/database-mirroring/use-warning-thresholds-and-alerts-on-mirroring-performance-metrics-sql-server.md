---
title: 미러링 성능 메트릭에 경고 임계값 및 경고 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- thresholds [SQL Server]
- database mirroring [SQL Server], managing in SQL Server Management Studio
- alerts [SQL Server], database mirroring
- database mirroring [SQL Server], monitoring
- warnings [database mirroring]
ms.assetid: 8cdd1515-0bd7-4f8c-a7fc-a33b575e20f6
caps.latest.revision: 40
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 157842419692f2fbb70f7fc3d28c4cf920e8f228
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40409550"
---
# <a name="use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server"></a>미러링 성능 메트릭에 대해 경고 임계값 및 경고 사용(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에는 데이터베이스 미러링에 대해 경고 임계값을 구성하고 관리할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트에 대한 정보가 포함되어 있습니다. 데이터베이스 미러링 모니터 서버 또는 **sp_dbmmonitorchangealert**, **sp_dbmmonitorhelpalert**및 **sp_dbmmonitordropalert** 저장 프로시저를 사용할 수 있습니다. 또한 이 항목에는 데이터베이스 미러링 이벤트에 대해 경고를 구성하는 방법에 대한 정보도 포함되어 있습니다.  
  
 미러된 데이터베이스에 대해 모니터링을 설정하면 시스템 관리자가 여러 개의 주요 성능 메트릭에 대해 경고 임계값을 구성할 수 있습니다. 또한 관리자는 이러한 데이터베이스 미러링 이벤트 및 기타 이벤트에 대해 경고를 구성할 수 있습니다.  
  
 **항목 내용:**  
  
-   [성능 메트릭 및 경고 임계값](#PerfMetricsAndWarningThresholds)  
  
-   [경고 임계값 설정 및 관리](#SetUpManageWarningThresholds)  
  
-   [미러된 데이터베이스에 대해 경고 사용](#UseAlerts)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="PerfMetricsAndWarningThresholds"></a> 성능 메트릭 및 경고 임계값  
 다음 표에서는 경고를 구성할 수 있는 성능 메트릭을 보여 주고 해당 경고 임계값과 데이터베이스 미러링 모니터 레이블에 대해 나열합니다.  
  
|성능 메트릭|경고 임계값|데이터베이스 미러링 모니터 레이블|  
|------------------------|-----------------------|--------------------------------------|  
|보내지 않은 로그|주 서버 인스턴스에서 경고를 생성하는 보내지 않은 로그 크기(KB)를 지정합니다. 이 경고는 KB를 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 되며 특히 성능 우선 모드와 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 경고는 보호 우선 모드와도 관련이 있습니다.|**보내지 않은 로그가 임계값을 초과하는 경우 경고**|  
|복원되지 않은 로그|미러 서버 인스턴스에서 경고를 생성하는 복원되지 않은 로그 크기(KB)를 지정합니다. 이 경고는 장애 조치(Failover) 시간을 측정하는 데 도움이 됩니다. *장애 조치 시간* 은 주로 이전 미러 서버에서 Redo Queue에 남아 있는 로그를 롤포워드해야 하는 시간과 짧은 추가 시간으로 구성됩니다.<br /><br /> 참고: 자동 장애 조치의 경우 시스템이 오류를 감지하는 데 걸리는 시간은 장애 조치 시간과 관계가 없습니다.<br /><br /> 자세한 내용은 [역할 전환 중 서비스 중단 예측&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md)프로세스를 통해 주 역할과 미러 역할을 서로 바꿀 수 있습니다.|**복원되지 않은 로그가 임계값을 초과하는 경우 경고**|  
|보내지 않은 가장 오래된 트랜잭션|주 서버 인스턴스에서 경고가 생성되기까지 Send Queue에 누적될 수 있는 트랜잭션에 해당하는 시간(분)을 지정합니다. 이 경고는 시간을 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 되며 특히 성능 우선 모드와 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 경고는 보호 우선 모드와도 관련이 있습니다.|**보내지 않은 가장 오래된 트랜잭션 기간이 임계값을 초과하는 경우 경고**|  
|미러 커밋 오버헤드|주 서버에서 경고가 생성되기까지 허용되는 트랜잭션당 평균 지연 시간(밀리초)을 지정합니다. 이 지연 시간은 주 서버 인스턴스에서 미리 서버 인스턴스가 트랜잭션 로그 레코드를 Redo Queue에 쓸 때까지 대기하는 동안 발생한 오버헤드 양입니다. 이 값은 보호 우선 모드에만 해당됩니다.|**미러 커밋 오버헤드가 임계값을 초과하는 경우 경고**|  
  
 이러한 성능 메트릭 중 하나에 대해 시스템 관리자는 미러된 데이터베이스에서 임계값을 지정할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [경고 임계값 설정 및 관리](#SetUpManageWarningThresholds)를 참조하세요.  
  
##  <a name="SetUpManageWarningThresholds"></a> 경고 임계값 설정 및 관리  
 시스템 관리자는 주요 미러링 성능 메트릭에 대해 하나 이상의 경고 임계값을 구성할 수 있습니다. 데이터베이스가 장애 조치되는 경우에도 경고가 지속되도록 두 파트너에서 모두 지정된 경고에 대해 임계값을 설정하는 것이 좋습니다. 각 파트너에 적합한 임계값은 해당 파트너 시스템의 성능 기능에 따라 달라집니다.  
  
 다음 중 하나를 사용하여 경고 임계값을 구성하고 관리할 수 있습니다.  
  
-   데이터베이스 미러링 모니터  
  
     데이터베이스 미러링 모니터에서 관리자는 **경고** 탭 페이지를 선택하여 주 서버 인스턴스 및 미러 서버 인스턴스에 있는 선택한 데이터베이스에 대한 경고의 현재 구성을 동시에 볼 수 있습니다. 여기서 관리자는 **경고 임계값 설정** 대화 상자를 열어 경고 임계값을 하나 이상 설정하고 구성할 수 있습니다.  
  
     데이터베이스 미러링 모니터 인터페이스에 대한 개요는 [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md)를 참조하세요. 데이터베이스 미러링 모니터를 시작하는 방법은 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)을 참조하세요.  
  
-   시스템 저장 프로시저  
  
     다음 시스템 저장 프로시저 집합을 사용하면 관리자가 한 번에 한 파트너의 미러된 데이터베이스에 대해 경고 임계값을 설정하고 관리할 수 있습니다.  
  
    |절차|설명|  
    |---------------|-----------------|  
    |[sp_dbmmonitorchangealert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)|지정한 미러링 성능 메트릭에 대해 경고 임계값을 추가하거나 변경합니다.|  
    |[sp_dbmmonitorhelpalert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)|여러 가지 주요 데이터베이스 미러링 모니터 성능 메트릭 중 하나 또는 모두에 대한 경고 임계값 정보를 반환합니다.|  
    |[sp_dbmmonitordropalert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)|지정한 성능 메트릭에 대한 경고를 삭제합니다.|  
  
## <a name="performance-threshold-events-sent-to-the-windows-event-log"></a>Windows 이벤트 로그로 전송되는 성능 임계값 이벤트  
 성능 메트릭에 대해 경고 임계값을 정의하면 상태 테이블이 업데이트될 때 최신 값이 임계값에 대해 평가됩니다. 임계값에 도달하지 않은 경우 업데이트 프로시저 **sp_dbmmonitorupdate**가 메트릭에 대해 정보 이벤트( *성능 임계값 이벤트*)를 생성하고 해당 이벤트를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 이벤트 로그에 기록합니다. 다음 표에서는 성능 임계값 이벤트의 이벤트 ID를 보여 줍니다.  
  
|성능 메트릭|이벤트 ID|  
|------------------------|--------------|  
|보내지 않은 로그|32042|  
|복원되지 않은 로그|32043|  
|보내지 않은 가장 오래된 트랜잭션|32040|  
|미러 커밋 오버헤드|32044|  
  
> [!NOTE]  
>  관리자는 이러한 이벤트 중 하나 이상에 대해 경고를 정의할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [미러된 데이터베이스에 대해 경고 사용](#UseAlerts)을  
>   
>  참조하세요.  
  
##  <a name="UseAlerts"></a> 미러된 데이터베이스에 대해 경고 사용  
 미러된 데이터베이스 모니터링의 핵심은 중요한 데이터베이스 미러링 이벤트에 대해 경고를 구성하는 것입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 다음 유형의 데이터베이스 미러링 이벤트를 생성합니다.  
  
-   성능 임계값 이벤트  
  
     자세한 내용은 이 항목의 앞부분에 나오는 "Windows 이벤트 로그로 전송되는 성능 임계값 이벤트"를 참조하세요.  
  
-   상태 변경 이벤트  
  
     데이터베이스 미러링 세션의 내부 상태를 변경할 때 생성되는 WMI(Windows Management Instrumentation) 이벤트입니다.  
  
    > [!NOTE]  
    >  자세한 내용은 [서버 이벤트용 WMI 공급자 개념](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)을 참조하세요.  
  
 시스템 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 작업 관리자와 같은 다른 응용 프로그램을 사용하여 이러한 이벤트에 대해 경고를 구성할 수 있습니다.  
  
 데이터베이스 미러링 이벤트에 대해 경고를 정의하는 경우 두 파트너 서버 인스턴스에서 모두 경고 임계값과 경고를 정의하는 것이 좋습니다. 개별 이벤트는 주 서버나 미러 서버 중 하나에서 생성되지만 각 파트너가 언제든지 두 역할 중 하나를 수행할 수 있습니다. 장애 조치 후에도 경고가 계속 작동하려면 두 파트너에서 모두 경고를 정의해야 합니다.  
  
 자세한 내용은 [SQL Server 웹 사이트](http://go.microsoft.com/fwlink/?linkid=62373)에서 데이터베이스 미러링 이벤트에 대한 경고와 관련된 백서를 참조하세요. 이 백서에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트, 데이터베이스 미러링 WMI 이벤트 및 예제 스크립트를 사용하여 경고를 구성하는 방법에 대한 정보가 들어 있습니다.  
  
> [!IMPORTANT]  
>  모든 미러링 세션에서 상태 변경 이벤트에 대해 경고를 보내도록 데이터베이스를 구성하는 것이 좋습니다. 수동 구성 변경의 결과로 상태 변경이 예상되는 경우가 아니면 문제가 발생한 것이므로 데이터가 손상될 수 있습니다. 데이터를 보호하려면 예기치 않은 상태 변경의 원인을 확인하고 해결합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **SQL Server Management Studio를 사용하여 경고를 만들려면**  
  
-   [오류 번호를 사용하여 경고 만들기](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [WMI 이벤트 경고 만들기](../../ssms/agent/create-a-wmi-event-alert.md)  
  
 **데이터베이스 미러링을 모니터링하려면**  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitoraddmonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorchangealert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
-   [sp_dbmmonitorchangemonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)  
  
-   [sp_dbmmonitordropalert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
-   [sp_dbmmonitordropmonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorhelpalert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)  
  
-   [sp_dbmmonitorhelpmonitoring&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorresults&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
-   [sp_dbmmonitorupdate&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
