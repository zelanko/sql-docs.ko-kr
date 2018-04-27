---
title: 이벤트 관리 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- event-triggered jobs [SQL Server]
- forwarding events [SQL Server]
- alerts [SQL Server], forwarded events
- alerts [SQL Server], management servers
- SQL Server Agent alerts, management servers
ms.assetid: 8f4ee7f5-80df-49fd-b2b8-d020e04b6e1b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f78bdf6ecd1e9d9b0a8d3db48f18db29243e67a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="manage-events"></a>이벤트 관리
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

특정 오류 심각도에 도달하거나 넘어선 모든 이벤트 메시지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 전달할 수 있습니다. 이를 *이벤트 전달*이라고 합니다. 전달 서버는 마스터 서버의 역할도 할 수 있는 전용 서버입니다. 이벤트 전달을 사용하면 서버 그룹에 대한 경고 관리를 중앙 집중화함으로써 많이 사용되는 서버의 작업을 줄일 수 있습니다.  
  
한 대의 서버가 다른 서버 그룹에 대한 이벤트를 받을 때 이벤트를 받는 서버를 *경고 관리 서버*라고 합니다. 다중 서버 환경에서는 마스터 서버를 경고 관리 서버로 지정합니다.  
  
## <a name="advantages-of-using-an-alerts-management-server"></a>경고 관리 서버 사용의 장점  
경고 관리 서버를 설정하면 다음과 같은 장점이 있습니다.  
  
-   **중앙 집중식**- 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스의 이벤트를 단일 서버에서 중앙 집중식으로 제어하고 간편하게 볼 수 있습니다.  
  
-   **확장성**- 많은 물리적 서버를 한 대의 논리적 서버에서 관리할 수 있습니다. 이 물리적 서버 그룹에 필요한 만큼 서버를 추가하거나 제거할 수 있습니다.  
  
-   **효율성**- 경고와 운영자를 한 번만 정의하면 되므로 구성 시간이 줄어듭니다.  
  
## <a name="disadvantages-of-using-an-alerts-management-server"></a>경고 관리 서버 사용의 단점  
경고 관리 서버를 설정하면 다음과 같은 단점이 있습니다.  
  
-   **트래픽 증가**- 이벤트를 경고 관리 서버에 전달하면 네트워크 트래픽이 증가할 수 있습니다. 지정한 심각도를 넘는 이벤트만 전달하도록 제한하면 이러한 트래픽 증가를 완화할 수 있습니다.  
  
-   **단일 지점에서 실패**- 경고 관리 서버가 오프라인인 경우 관리되는 서버 그룹의 어떠한 이벤트에 대해서도 경고가 발생하지 않습니다.  
  
-   **서버 부하**- 전달된 이벤트에 대한 경고를 처리하면 경고 관리 서버의 처리량이 증가됩니다.  
  
## <a name="guidelines-for-using-an-alerts-management-server"></a>경고 관리 서버 사용을 위한 지침  
경고 관리 서버를 구성하는 경우 다음 지침을 따르십시오.  
  
-   또한 전달된 이벤트를 수신하려면 경고 관리 서버가 SQL Server의 기본 인스턴스여야 합니다.  
  
-   많이 사용되거나 중요한 응용 프로그램을 경고 관리 서버에서 실행하지 않습니다.  
  
-   하나의 경고 관리 서버를 많은 서버에서 공유하도록 구성하는 데 있어 네트워크 트래픽을 신중히 계획합니다. 정체되는 경우에는 특정 경고 관리 서버를 사용하는 서버의 수를 줄입니다.  
  
    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 에 등록된 서버는 경고 전달 서버에서 선택할 수 있는 서버 목록의 일부로 구성됩니다.  
  
-   서버별 응답이 필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 로컬 인스턴스에서는 경고를 경고 관리 서버에 전달하지 않고 로컬 인스턴스에 경고를 정의합니다.  
  
    경고 관리 서버는 자신에게 경고를 전달하는 모든 서버를 논리적인 통합체로 간주합니다. 예를 들어 경고 관리 서버는 서버 A에서 전달된 605 이벤트와 서버 B에서 전달된 605 이벤트에 같은 방법으로 응답합니다.  
  
-   경고 시스템을 구성한 후 정기적으로 Microsoft Windows 응용 프로그램 로그에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 이벤트를 확인합니다.  
  
    경고 엔진에서 발생한 실패 내용은 "SQL Server 에이전트"라는 원본 이름으로 로컬 Windows 응용 프로그램 로그에 기록됩니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 정의된 전자 메일 알림을 보낼 수 없으면 이벤트가 응용 프로그램 로그에 기록됩니다.  
  
로컬에 정의된 경고가 비활성화되고 경고를 표시하는 이벤트가 발생하는 경우 경고 전달 조건을 만족하면 그 이벤트는 경고 관리 서버로 전달됩니다. 이러한 전달을 통해 로컬 사이트에 있는 사용자의 필요에 따라 경고 관리 서버에 정의된 경고가 로컬에서도 정의되는 경우 로컬에 정의된 경고를 무시하도록 설정하거나 해제할 수 있습니다. 또한 로컬 경고에서 처리할 때라도 이벤트가 항상 전달되도록 요청할 수 있습니다.  
  
다중 서버 환경에서 이벤트를 관리하는 일반 태스크는 다음과 같습니다.  
  
**경고 관리 서버를 지정하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/designate-an-events-forwarding-server-sql-server-management-studio.md)  
  
**경고에 대한 응답을 정의하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
## <a name="running-event-triggered-jobs"></a>이벤트 트리거된 작업의 실행  
경고에 응답하여 작업이 실행되도록 작업을 정의할 수 있습니다. 예를 들어 작업을 실행하여 경고에서 감지한 문제를 진단하거나 해결할 수 있습니다.  
  
> [!NOTE]  
> 작업에서 이벤트를 발생시킬 수 있으므로 재귀 경고 작업 루프를 만들지 않도록 주의하십시오.  
  
## <a name="see-also"></a>참고 항목  
[sp_add_notification(Transact-SQL)](http://msdn.microsoft.com/en-us/44bee7d9-7517-4071-99be-8b36f979c7cc)  
  
