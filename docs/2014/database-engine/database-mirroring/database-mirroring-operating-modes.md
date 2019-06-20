---
title: 데이터베이스 미러링 운영 모드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], operating modes
ms.assetid: f8a579c2-55d7-4278-8088-f1da1de5b2e6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5975008849ec4ef8a4d50aa559bb69554b65132a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807671"
---
# <a name="database-mirroring-operating-modes"></a>데이터베이스 미러링 운영 모드
  이 항목에서는 데이터베이스 미러링 세션의 동기 운영 모드 및 비동기 운영 모드에 대해 설명합니다.  
  
> [!NOTE]  
>  데이터베이스 미러링에 대한 소개는 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring-sql-server.md)을 참조하세요.  
  
 
  
##  <a name="TermsAndDefinitions"></a> 용어 및 정의  
 이 섹션에서는 이 항목의 몇 가지 중요 용어를 소개합니다.  
  
 성능 우선 모드  
 데이터베이스 미러링 세션이 비동기적으로 작동하며 주 서버와 미러 서버만 사용합니다. 역할 전환의 유일한 형식은 강제 서비스(데이터 손실 가능)입니다.  
  
 보호 우선 모드  
 데이터베이스 미러링 세션이 동기적으로 작동하며 필요한 경우 주 서버와 미러 서버뿐 아니라 미러링 모니터 서버도 사용합니다.  
  
 트랜잭션 보안  
 데이터베이스 미러링 세션이 동기적으로 작동하는지 아니면 비동기적으로 작동하는지를 결정하는 미러링별 데이터베이스 속성입니다. 보안 수준은 FULL 및 OFF의 두 가지입니다.  
  
 미러링 모니터  
 보호 우선 모드에서만 사용할 수 있으며, 자동 장애 조치(Failover)가 시작되었는지 여부를 미러 서버에서 인식할 수 있도록 하는 SQL Server의 선택적 인스턴스입니다. 미러링 모니터 서버는 두 장애 조치(Failover) 파트너와는 달리 데이터베이스를 제공하지 않습니다. 미러링 모니터 서버는 자동 장애 조치(Failover)를 지원하는 역할만 수행합니다.  
  
##  <a name="VisualElement"></a> 비동기 데이터베이스 미러링 (성능 우선 모드)  
 이 섹션에서는 비동기 데이터베이스 미러링의 작동 방식 및 성능 우선 모드를 사용하기에 적합한 경우에 대해 설명하고 주 서버 실패 시 어떻게 반응하는지에 대해 설명합니다.  
  
> [!NOTE]  
>  대부분의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전에서는 동기 데이터베이스 미러링("Safety Full만")만 지원합니다. 데이터베이스 미러링을 모두 지 원하는 버전에 대 한 내용은의 "고가용성 (AlwaysOn)"를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 트랜잭션 보안을 OFF로 설정하면 데이터베이스 미러링 세션은 비동기적으로 작동합니다. 비동기 작업은 성능 우선 모드의 운영 모드만 지원합니다. 이 모드는 성능을 강화하지만 고가용성은 저하됩니다. 성능 우선 모드에서는 주 서버와 미러 서버만 사용됩니다. 미러 서버의 문제점은 주 서버에 영향을 주지 않습니다. 주 서버가 손실되면 미러 데이터베이스는 DISCONNECTED로 표시되지만 웜 대기로 사용할 수 있습니다.  
  
 고성능 모드는 강제 적용 서비스(데이터 손실 가능)라는 한 가지 형태의 역할 전환만 지원하며 이 역할은 웜 대기 서버(warm standby server)로 미러 서버를 사용합니다. 강제 서비스는 주 서버 실패에 대한 가능한 응답 중 하나입니다. 데이터가 손실될 수 있으므로 미러 서버에 서비스를 강제하기 전에 다른 대안을 고려해야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [주 서버 실패에 대한 응답](#WhenPrincipalFails)을 참조하세요.  
  
 다음 그림에서는 성능 우선 모드를 사용한 세션 구성을 보여 줍니다.  
  
 ![파트너 전용 세션 구성](../media/dbm-high-performance-mode.gif "파트너 전용 세션 구성")  
  
 성능 우선 모드에서 주 서버가 미러 서버로 트랜잭션 로그를 보내면 미러 서버의 확인을 기다리지 않고 즉시 클라이언트로 확인 메시지를 보냅니다. 트랜잭션은 미러 서버에서 로그를 디스크에 쓸 때까지 기다리지 않고 커밋됩니다. 비동기 작업을 통해 주 서버는 최소 트랜잭션 대기 시간을 사용하여 실행됩니다.  
  
 미러 서버는 주 서버가 보낸 로그 레코드를 유지하려고 합니다. 그러나 일반적으로 두 데이터베이스 간의 차이가 크지는 않지만 미러 데이터베이스는 주 데이터베이스보다 약간 뒤처질 수 있습니다. 그러나 주 서버에 작업이 크거나 미러 서버 시스템이 과부화된 경우 이 시간 간격은 상당히 커질 수 있습니다.  
  
 
  
###  <a name="WhenUseHighPerf"></a> 성능 우선 모드가 적합한 경우  
 성능 우선 모드는 주 서버와 미러 서버가 상당한 거리로 분리되어 있고 주 서버가 작은 오류의 영향을 받지 않도록 하려는 재해 복구 시나리오에서 유용할 수 있습니다.  
  
> [!NOTE]  
>  로그 전달은 데이터베이스 미러링을 보완하며 비동기 데이터베이스 미러링의 대안으로 사용될 수 있습니다. 로그 전달의 장점에 대한 자세한 내용은 [고가용성 솔루션&#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)을 참조하세요. 데이터베이스 미러링을 통해 로그 전달을 사용하는 방법은 [데이터베이스 미러링 및 로그 전달&#40;SQL Server&#41;](database-mirroring-and-log-shipping-sql-server.md)을 참조하세요.  
  
###  <a name="WitnessImpactOnHighPerf"></a> 성능 우선 모드에 대한 미러링 모니터 서버의 영향  
 Transact-SQL을 사용하여 성능 우선 모드를 구성하는 경우 SAFETY 속성이 OFF로 설정되어 있으면 WITNESS 속성도 OFF로 설정하는 것이 좋습니다. 미러링 모니터 서버는 성능 우선 모드에서 작동할 수 있지만 어떤 이점도 제공하지 않으며 위험만 수반됩니다.  
  
 파트너 중 하나의 작동이 중단될 때 세션에서 미러링 모니터 서버의 연결이 끊어지면 데이터베이스를 사용할 수 없게 됩니다. 이는 성능 우선 모드에 미러링 모니터 서버가 필요하지는 않지만 미러링 모니터 서버가 설정된 경우 세션에 둘 이상의 서버 인스턴스로 구성된 쿼럼이 필요하기 때문입니다. 세션에서 쿼럼이 손실되면 데이터베이스를 제공할 수 없습니다.  
  
 성능 우선 모드 세션에 미러링 모니터 서버가 설정되어 있을 때 쿼럼의 적용은 다음을 의미합니다.  
  
-   미러 서버가 손실되면 주 서버가 미러링 모니터 서버에 연결되어야 합니다. 그렇지 않으면 미러링 모니터 서버나 미러 서버가 세션에 다시 참여할 때까지 주 서버가 데이터베이스를 오프라인 상태로 유지합니다.  
  
-   주 서버가 손실된 경우 미러 서버에 서비스를 강제하려면 미러 서버가 미러링 모니터 서버에 연결되어야 합니다.  
  
> [!NOTE]  
>  쿼럼 유형에 대한 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
###  <a name="WhenPrincipalFails"></a> 주 서버 실패에 대한 응답  
 주 서버에 장애가 발생하면 데이터베이스 소유자가 선택할 수 있는 응답은 다음과 같습니다.  
  
-   주 서버를 다시 사용할 수 있을 때까지 데이터베이스를 사용하지 않습니다.  
  
     주 데이터베이스와 해당 트랜잭션 로그가 영향을 받지 않은 경우 이 선택은 가용성을 저하시켜 모든 커밋된 트랜잭션을 유지합니다.  
  
-   데이터베이스 미러링 세션을 중지하고 데이터베이스를 수동으로 업데이트한 다음 새 데이터베이스 미러링 세션을 시작합니다.  
  
     주 데이터베이스가 손실되었지만 주 서버가 계속 실행 중이면 주 데이터베이스에서 즉시 비상 로그 백업을 시도하세요. 비상 로그 백업에 성공한 경우 미러링을 제거하는 것이 좋습니다. 미러링을 제거한 다음 모든 데이터를 유지하는 이전 미러 데이터베이스로 해당 로그를 복원할 수 있습니다.  
  
    > [!NOTE]  
    >  비상 로그 백업에 실패하고 주 서버의 복구를 기다릴 수 없는 경우 세션 상태를 유지 관리할 수 있는 강제 서비스를 고려하세요.  
  
-   미러 서버에서 강제 서비스(데이터 손실 가능)를 실행합니다.  
  
     강제 서비스는 엄밀한 의미에서 재해 복구 방법이며 반드시 필요한 경우에만 사용해야 합니다. 강제 서비스는 주 서버가 다운되고 세션이 비동기적이며(트랜잭션 보안이 OFF로 설정됨) 세션에 미러링 모니터 서버가 없거나(WITNESS 속성이 OFF로 설정됨) 미러링 모니터 서버가 미러 서버에 연결된 경우(쿼럼이 있음)에만 사용할 수 있습니다.  
  
     강제 서비스를 사용하면 미러 서버는 주 서버 역할로 간주되며 주 서버의 데이터베이스 복사본을 클라이언트에게 제공합니다. 강제 서비스를 사용하면 주 서버가 미러 서버로 보내지 않은 트랜잭션 로그는 모두 손실됩니다. 따라서 강제 서비스는 데이터 손실이 허용되고 즉각적인 데이터베이스 가용성이 중요한 상황에서만 사용되어야 합니다. 강제 서비스 작동 방법과 최선의 사용 방법은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)을 참조하세요.  
  
##  <a name="Sync"></a> 동기 데이터베이스 미러링(보호 우선 모드)  
 이 섹션에서는 자동 장애 조치(Failover)가 있거나 없는 대체 보호 우선 모드를 비롯한 동기 데이터베이스 미러링의 작동 방식에 대해 설명하고 자동 장애 조치에서의 미러링 모니터 서버 역할에 대해 설명합니다.  
  
 트랜잭션 보안이 FULL로 설정되어 있으면 데이터베이스 미러링 세션은 보호 우선 모드로 실행되며 초기 동기화 단계 이후 동시에 작동합니다. 이 섹션에서는 동기화 작업에 대해 구성되어 있는 데이터베이스 미러링 세션에 대해 설명합니다.  
  
 세션에 대한 동기화 작업을 수행하려면 미러 서버에서 미러 데이터베이스를 주 데이터베이스와 동기화해야 합니다. 세션이 시작되면 주 서버에서 해당 활성 로그를 미러 서버로 보내기 시작합니다. 미러 서버는 들어오는 모든 로그 레코드를 가능한 한 빨리 디스크에 씁니다. 수신된 모든 로그 레코드가 디스크에 기록되면 즉시 데이터베이스가 동기화됩니다. 파트너와 통신이 유지되는 한 데이터베이스는 동기화 상태를 유지할 수 있습니다.  
  
> [!NOTE]  
>  데이터베이스 미러링 세션의 상태 변경을 모니터링하려면 **데이터베이스 미러링 상태 변경** 이벤트 클래스를 사용합니다. 자세한 내용은 [Database Mirroring State Change Event Class](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)을 참조하세요.  
  
 동기화가 완료되면 주 데이터베이스에서 커밋된 모든 트랜잭션이 미러 서버에서도 커밋되므로 데이터가 보호됩니다. 이 작업은 주 서버에서 미러 서버가 트랜잭션 로그를 디스크로 확정했다는 메시지를 받을 때까지 주 데이터베이스에 대한 트랜잭션 커밋을 대기함으로써 수행됩니다. 이 메시지에 대한 대기로 인해 트랜잭션의 대기 시간이 길어집니다.  
  
 동기화에 필요한 시간은 세션을 시작할 때(처음에 주 서버에서 받은 로그 레코드 수로 측정) 미러 데이터베이스의 주 데이터베이스에 대한 간격, 주 데이터베이스의 작업 및 미러 시스템의 속도에 따라 다릅니다. 세션이 동기화된 후 미러 데이터베이스에서 다시 실행되어야 하는 확정된 로그는 Redo Queue에 남아 있습니다.  
  
 미러 데이터베이스가 동기화되자마자 데이터베이스의 두 복사본의 상태는 SYNCHRONIZED로 변경됩니다.  
  
 동기화 작업은 다음 방식으로 유지 관리됩니다.  
  
1.  클라이언트로부터 트랜잭션을 받자마자 주 서버는 트랜잭션에 대한 로그를 트랜잭션 로그에 기록합니다.  
  
2.  주 서버는 데이터베이스에 트랜잭션을 기록하고 동시에 로그 레코드를 미러 서버로 보냅니다. 주 서버는 미러 서버의 승인을 기다린 후 클라이언트에게 트랜잭션 커밋 또는 롤백을 확인해 줍니다.  
  
3.  미러 서버는 로그를 디스크로 확정하고 주 서버로 승인을 반환합니다.  
  
4.  미러 서버의 승인을 받자마자 주 서버는 확인 메시지를 클라이언트에게 보냅니다.  
  
 보호 우선 모드에서는 두 위치의 데이터가 동기화되도록 하여 데이터를 보호합니다. 커밋된 모든 트랜잭션이 미러 서버의 디스크에 기록됩니다.  
  

  
###  <a name="HighSafetyWithOutAutoFailover"></a> 자동 장애 조치(Failover)를 지원하지 않는 보호 우선 모드  
 다음 그림에서는 자동 장애 조치(Failover)를 지원하지 않는 보호 우선 모드의 구성을 보여 줍니다. 이 구성은 두 개의 파트너로만 이루어져 있습니다.  
  
 ![미러링 모니터 서버 없이 통신하는 파트너](../media/dbm-high-protection-mode.gif "미러링 모니터 서버 없이 통신하는 파트너")  
  
 파트너가 연결되어 있으며 데이터베이스가 이미 동기화된 경우 수동 장애 조치가 지원됩니다. 미러 서버 인스턴스의 작동이 중단되더라도 주 서버 인스턴스는 아무런 영향을 받지 않으며 노출된 상태(데이터를 미러링하지 않음)로 실행됩니다. 주 서버가 손상되면 미러가 일시 중단되지만 서비스를 미러 서버로 강제 수행할 수 있으며 이 경우 데이터가 손실될 수 있습니다. 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)에서만 사용할 수 있습니다.  
  
###  <a name="HighSafetyWithAutoFailover"></a> 자동 장애 조치(Failover)를 지원하는 보호 우선 모드  
 자동 장애 조치를 사용하면 서버 한 대가 손실되어도 데이터베이스가 여전히 작동되므로 고가용성이 제공됩니다. 자동 장애 조치를 사용하려면 이상적으로 세 번째 컴퓨터에 있는 세 번째 서버 인스턴스인 *미러링 모니터 서버*가 세션에 필요합니다. 다음 그림에서는 자동 장애 조치를 지원하는 보호 우선 모드 세션의 구성을 보여 줍니다.  
  
 ![세션의 미러링 모니터 서버 및 두 파트너](../media/dbm-high-availability-mode.gif "세션의 미러링 모니터 서버 및 두 파트너")  
  
 미러링 모니터 서버는 두 파트너와는 달리 데이터베이스를 제공하지 않습니다. 미러링 모니터 서버는 주 서버가 작동하는지 여부만 확인하여 자동 장애 조치를 지원합니다. 미러 서버는 미러 서버 및 미러링 모니터 서버가 주 서버와 연결이 끊어진 후에도 서로 연결되어 있는 경우에만 자동 장애 조치를 시작합니다.  
  
 미러링 모니터 서버를 설정하면 세션에 *쿼럼*이 필요합니다. 쿼럼은 데이터베이스를 사용할 수 있도록 만드는 두 개 이상 서버 인스턴스 간의 관계입니다. 자세한 내용은 [데이터베이스 미러링 모니터 서버](database-mirroring-witness.md) 및 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
 자동 장애 조치(Failover)에는 다음 조건이 필요합니다.  
  
-   데이터베이스가 동기화되어 있습니다.  
  
-   서버 인스턴스 3개가 모두 연결되어 있는 동안 실패가 발생하고 미러링 모니터 서버와 미러 서버가 계속 연결되어 있습니다.  
  
 파트너가 손실되면 다음과 같은 결과가 나타납니다.  
  
-   위의 조건에서 주 서버를 사용할 수 없게 되면 자동 장애 조치가 수행됩니다. 미러 서버가 주 서버 인스턴스의 역할로 전환하여 해당 데이터베이스를 주 데이터베이스로 제공합니다.  
  
-   이러한 조건을 만족하지 않을 때 주 서버를 사용할 수 없게 되면 서비스가 강제되고 데이터가 손실될 수 있습니다. 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)을 참조하세요.  
  
-   미러 서버만 사용할 수 없는 경우 주 서버와 미러링 모니터 서버가 계속 작동됩니다.  
  
 세션에서 미러링 모니터 서버가 손실되면 쿼럼은 두 파트너를 모두 필요로 합니다. 한 파트너가 쿼럼을 잃으면 두 파트너 모두 쿼럼을 잃고 쿼럼이 다시 설정될 때까지 데이터베이스를 사용할 수 없게 됩니다. 이 쿼럼 요구 사항은 미러링 모니터 서버가 없을 때 데이터베이스가 *노출됨*상태(미러링되지 않음)로 실행되지 않도록 합니다.  
  
> [!NOTE]  
>  미러링 모니터 서버가 오랫동안 연결 해제된 상태로 유지될 것으로 예상되면 세션에서 미러링 모니터 서버를 일시적으로 제거하는 것이 좋습니다.  
  
##  <a name="TsqlSettingsAndOpModes"></a> Transact-SQL 설정 및 데이터베이스 미러링 작업 모드  
 이 섹션에서는 ALTER DATABASE 설정과 미러된 데이터베이스 및 미러링 모니터 서버의 상태를 중심으로 데이터베이스 미러링 세션에 대해 설명합니다. 이 섹션은 [!INCLUDE[tsql](../../includes/tsql-md.md)]보다는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]을 사용하여 데이터베이스 미러링을 관리하는 사용자를 위한 것입니다.  
  
> [!TIP]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하는 대신 개체 탐색기에서 **데이터베이스 속성** 대화 상자의 **미러링** 페이지를 사용하여 세션의 운영 모드를 제어할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)을 참조하세요.  
  

  
###  <a name="TxnSafetyAndWitness"></a> 트랜잭션 보안 및 미러링 모니터 상태가 운영 모드에 영향을 주는 방식  
 세션 운영 모드는 트랜잭션 보안 설정 및 미러링 모니터 상태의 조합에 의해 결정됩니다. 데이터베이스 소유자는 언제든지 트랜잭션 보안 수준을 변경하고 미러링 모니터를 추가 또는 제거할 수 있습니다.  
  

  
####  <a name="TxnSafety"></a> Transaction Safety  
 트랜잭션 보안은 데이터베이스 미러링 세션이 동기적으로 작동하는지 아니면 비동기적으로 작동하는지를 결정하는 미러링별 데이터베이스 속성입니다. 보안 수준은 FULL 및 OFF의 두 가지입니다.  
  
-   SAFETY FULL  
  
     FULL 트랜잭션 보안 수준으로 설정하면 세션이 동기적으로 보호 우선 모드에서 작동합니다. 또한 미러링 모니터 서버가 있으면 세션에서 자동 장애 조치(Failover)가 지원됩니다.  
  
     ALTER DATABASE 문을 사용하여 세션을 설정하면 세션은 SAFETY 속성이 FULL로 설정되어 시작됩니다. 즉, 세션이 보호 우선 모드로 시작됩니다. 이 경우 세션이 시작된 후에 미러링 모니터 서버를 추가할 수 있습니다.  
  
     자세한 내용은 이 항목의 앞부분에 나오는 [동기 데이터베이스 미러링(보호 우선 모드)](#Sync)을 참조하세요.  
  
-   SAFETY OFF  
  
     트랜잭션 보안 기능을 끄면 세션이 비동기적으로 성능 우선 모드에서 작동합니다. SAFETY 속성을 OFF로 설정하면 WITNESS 속성도 OFF(기본값)로 설정해야 합니다. 성능 우선 모드에서 미러링 모니터의 영향에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 [미러링 모니터 상태](#WitnessState)를 참조하세요. 트랜잭션 보안이 해제된 상태에서 실행하는 방법은 이 항목의 앞부분에 나오는 [비동기 데이터베이스 미러링(성능 우선 모드)](#VisualElement)을 참조하세요.  
  
 각 파트너의 데이터베이스 트랜잭션 보안 설정은 **sys.database_mirroring** 카탈로그 뷰의 **mirroring_safety_level** 및 **mirroring_safety_level_desc** 열에 기록됩니다. 자세한 내용은 [sys.database_mirroring&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql)을 참조하세요.  
  
 데이터베이스 소유자는 언제든지 트랜잭션 보안 수준을 변경할 수 있습니다.  
  
####  <a name="WitnessState"></a> 미러링 모니터 상태  
 미러링 모니터가 설정된 경우 쿼럼이 필요하므로 미러링 모니터의 상태가 항상 중요합니다.  
  
 미러링 모니터가 있을 경우 미러링 모니터는 다음 두 가지 상태 중 하나입니다.  
  
-   미러링 모니터가 파트너에 연결되어 있으면 미러링 모니터는 해당 파트너에 대해 CONNECTED 상태가 되며 이 파트너와의 쿼럼이 구성됩니다. 이 경우 파트너 중 하나를 사용할 수 없어도 데이터베이스를 사용 가능하도록 만들 수 있습니다.  
  
-   미러링 모니터가 있지만 파트너에 연결되어 있지 않으면 미러링 모니터는 해당 파트너에 대해 UNKOWN 또는 DISCONNECTED 상태가 됩니다. 이 경우 미러링 모니터와 이 파트너 간에는 쿼럼이 없으며 파트너가 서로 연결되어 있지 않으면 데이터베이스를 사용할 수 없게 됩니다.  
  
 쿼럼에 대한 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
 서버 인스턴스에서 각 미러링 모니터의 상태는 **sys.database_mirroring** 카탈로그 뷰의 **mirroring_witness_state** 및 **mirroring_witness_state_desc** 열에 기록됩니다. 자세한 내용은 [sys.database_mirroring&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql)을 참조하세요.  
  
 다음 표에서는 세션 운영 모드가 트랜잭션 보안 설정 및 미러링 모니터 상태의 조합에 따라 어떻게 달라지는지를 보여 줍니다.  
  
|운영 모드|트랜잭션 보안|미러링 모니터 상태|  
|--------------------|------------------------|-------------------|  
|성능 우선 모드|OFF|NULL (미러링 모니터 없음)<sup>2</sup>|  
|자동 장애 조치(Failover)를 지원하지 않는 보호 우선 모드|FULL|NULL(미러링 모니터 없음)|  
|자동 장애 조치 있는 보호 우선 모드<sup>1</sup>|FULL|CONNECTED|  
  
 <sup>1</sup> 미러링 모니터 서버 연결이 끊어질 경우 미러링 모니터 서버 인스턴스 사용 가능할 때까지 witness 속성을 OFF 설정 하는 것이 좋습니다.  
  
 <sup>2</sup> 미러링 모니터 서버를 성능 우선 모드에 있을 경우 미러링 모니터 서버 세션에 참여 하지 않습니다. 그러나 데이터베이스를 사용하려면 최소 두 개의 서버 인스턴스가 연결되어 있어야 합니다. 따라서 성능 우선 모드 세션에서는 WITNESS 속성을 OFF로 설정된 상태로 유지하는 것이 좋습니다. 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
###  <a name="ViewWitness"></a> 보안 설정 및 미러링 모니터 상태 보기  
 데이터베이스의 보안 설정 및 미러링 모니터 상태를 보려면 **sys.database_mirroring** 카탈로그 뷰를 사용합니다. 관련된 열은 다음과 같습니다.  
  
|요소|열|Description|  
|------------|-------------|-----------------|  
|트랜잭션 보안|**mirroring_safety_level** 또는 **mirroring_safety_level_desc**|다음 중 하나에 해당되는 미러 데이터베이스상의 업데이트를 위한 트랜잭션 보안 설정<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL<br /><br /> NULL = 데이터베이스가 온라인이 아닙니다.|  
|미러링 모니터의 존재 여부|**mirroring_witness_name**|데이터베이스 미러링 모니터의 서버 이름 또는 미러링 모니터가 존재하지 않음을 나타내는 NULL|  
|미러링 모니터 상태|**mirroring_witness_state** 또는 **mirroring_witness_state_desc**|지정된 파트너상의 데이터베이스에서 미러링 모니터의 상태<br /><br /> UNKNOWN<br /><br /> CONNECTED<br /><br /> DISCONNECTED<br /><br /> NULL = 미러링 모니터가 존재하지 않거나 데이터베이스가 온라인이 아닙니다.|  
  
 예를 들어 주 서버 또는 미러 서버에서 다음을 입력합니다.  
  
```  
SELECT mirroring_safety_level_desc, mirroring_witness_name, mirroring_witness_state_desc FROM sys.database_mirroring  
```  
  
 이 카탈로그 뷰에 대한 자세한 내용은 [sys.database_mirroring&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql)을 참조하세요.  
  
###  <a name="FactorsOnLossOfPrincipal"></a> 주 서버가 손실된 경우 동작에 영향을 주는 요소  
 다음 표에서는 트랜잭션 보안 설정, 데이터베이스 상태, 그리고 주 서버가 손실된 경우 미러링 모니터의 상태가 미러링 세션의 동작에 주는 영향을 보여 줍니다.  
  
|트랜잭션 보안|미러 데이터베이스의 미러링 상태|미러링 모니터 상태|주 서버가 손실된 경우의 동작|  
|------------------------|----------------------------------------|-------------------|-------------------------------------|  
|FULL|SYNCHRONIZED|CONNECTED|자동 장애 조치(Failover)가 수행됩니다.|  
|FULL|SYNCHRONIZED|DISCONNECTED|미러 서버가 중지되고 장애 조치를 수행할 수 없으며 데이터베이스를 사용할 수 없습니다.|  
|OFF|SUSPENDED 또는 DISCONNECTED|NULL(미러링 모니터 없음)|미러 서버로 서비스가 강제됩니다(데이터가 손실될 수 있음).|  
|FULL|SYNCHRONIZING 또는 SUSPENDED|NULL(미러링 모니터 없음)|미러 서버로 서비스가 강제됩니다(데이터가 손실될 수 있음).|  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 미러링 모니터 서버 추가 또는 바꾸기&#40;SQL Server Management Studio&#41;](../database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 세션에서 미러링 모니터 서버 제거&#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
-   [데이터베이스 미러링 세션에서 트랜잭션 보안 변경&#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](monitoring-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 모니터 서버](database-mirroring-witness.md)  
