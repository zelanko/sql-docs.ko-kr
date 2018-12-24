---
title: 복제 구독자 및 AlwaysOn 가용성 그룹 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a0617135d1e7a07d30f4581783cefb7add601c88
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153236"
---
# <a name="replication-subscribers-and-alwayson-availability-groups-sql-server"></a>복제 구독자 및 AlwaysOn 가용성 그룹(SQL Server)
  복제 구독자인 데이터베이스를 포함하는 AlwaysOn 가용성 그룹이 장애 조치(Failover)되면 복제 구독은 실패할 수 있습니다. 트랜잭션 구독자의 경우 구독에서 구독자의 가용성 그룹 수신기 이름을 사용 중인 경우 배포 에이전트가 자동으로 계속 복제합니다. 병합 구독자의 경우 복제 관리자가 복제를 다시 만들어 수동으로 구독자를 다시 구성해야 합니다.  
  
## <a name="what-is-supported"></a>지원되는 기능  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제는 게시자에 대한 자동 장애 조치, 트랜잭션 구독자에 대한 자동 장애 조치 및 병합 구독자에 대한 수동 장애 조치를 제공합니다. 가용성 데이터베이스의 배포자에 대한 장애 조치는 지원되지 않습니다. AlwaysOn은 Websync 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Compact 시나리오와 함께 사용할 수 없습니다.  
  
 **병합 끌어오기 구독의 장애 조치**  
  
 서버 인스턴스가 실패하여 사용할 수 없으므로 끌어오기 에이전트가 주 복제본을 호스팅하는 서버 인스턴스의 **msdb** 데이터베이스에 저장된 작업을 찾을 수 없어 가용성 그룹 장애 조치 시 끌어오기 구독이 실패합니다.  
  
 **병합 밀어넣기 구독의 장애 조치**  
  
 밀어넣기 에이전트가 더 이상 원래 구독자의 원래 구독 데이터베이스에 연결할 수 없으므로 가용성 그룹 장애 조치 시 밀어넣기 구독이 실패합니다.  
  
## <a name="how-to-create-transactional-subscription-in-an-alwayson-environment"></a>AlwaysOn 환경에서 트랜잭션 구독을 만드는 방법  
 트랜잭션 복제의 경우 다음 단계를 사용하여 구독자 가용성 그룹을 구성 및 장애 조치(Failover)합니다.  
  
1.  구독을 만들기 전에 구독자 데이터베이스를 적절한 AlwaysOn 가용성 그룹에 추가합니다.  
  
2.  가용성 그룹의 모든 노드에 구독자의 가용성 그룹 수신기를 연결된 서버로 추가합니다. 이 단계를 수행하면 모든 잠재적인 장애 조치(Failover) 파트너가 수신기를 인식하고 수신기에 연결할 수 있습니다.  
  
3.  아래 **트랜잭션 복제 밀어넣기 구독 만들기** 섹션의 스크립트를 사용하여 구독자의 가용성 그룹 수신기 이름으로 구독을 만듭니다. 장애 조치(Failover) 후 수신기 이름은 항상 유효하게 유지되지만 구독자의 실제 서버 이름은 새로운 주 서버가 된 실제 노드에 따라 달라집니다.  
  
    > [!NOTE]  
    >  구독은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 사용하여 만들어야 하며 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]를 사용해서는 만들 수 없습니다.  
  
4.  끌어오기 구독을 만드는 경우:  
  
    1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]의 주 구독자 노드에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 엽니다.  
  
    2.  **끌어오기 배포 에이전트** 작업을 식별하고 작업을 편집합니다.  
  
    3.  **에이전트 실행** 작업 단계에서 `-Publisher` 및 `-Distributor` 매개 변수를 확인합니다. 이러한 매개 변수에 올바른 직접 서버 및 게시자 및 배포자의 인스턴스 이름이 포함되어 있는지 확인합니다.  
  
    4.  `-Subscriber` 매개 변수를 구독자의 가용성 그룹 수신기 이름으로 변경합니다.  
  
 다음 단계에 따라 구독을 만드는 경우 장애 조치 이후 아무 것도 수행하지 않아도 됩니다.  
  
## <a name="creating-a-transactional-replication-push-subscription"></a>트랜잭션 복제 밀어넣기 구독 만들기  
  
```  
-- commands to execute at the publisher, in the publisher database:  
use [<publisher database name>]  
EXEC sp_addsubscription @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @destination_db = N'<subscriber database name>',   
       @subscription_type = N'Push',   
       @sync_type = N'automatic', @article = N'all', @update_mode = N'read only', @subscriber_type = 0;  
GO  
  
EXEC sp_addpushsubscription_agent @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @subscriber_db = N'<subscriber database name>',   
       @job_login = null, @job_password = null, @subscriber_security_mode = 1;  
GO  
```  
  
## <a name="to-resume-the-merge-agents-after-the-availability-group-of-the-subscriber-fails-over"></a>구독자의 가용성 그룹 장애 조치 이후 병합 에이전트를 다시 시작하려면  
 병합 복제의 경우 복제 관리자가 다음 단계에 따라 수동으로 구독자를 다시 구성해야 합니다.  
  
1.  실행 `sp_subscription_cleanup` 구독자에 대 한 이전 구독을 제거 합니다. 새로운 주 복제본(이전에 보조 복제본이었음)에서 이 동작을 수행합니다.  
  
2.  새 구독을 만들고 새 스냅숏부터 시작하여 구독을 다시 만듭니다.  
  
> [!NOTE]  
>  현재 프로세스는 병합 복제 구독자에는 불편하지만 병합 복제의 기본 시나리오는 구독자에서 AlwaysOn 가용성 그룹을 사용하지 않는 연결이 끊긴 사용자(데스크톱, 랩톱, 핸드셋 디바이스)입니다.  
  
  
