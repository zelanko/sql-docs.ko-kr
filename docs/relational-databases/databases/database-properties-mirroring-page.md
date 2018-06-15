---
title: 데이터베이스 속성(미러링 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.mirroring.f1
ms.assetid: 5bdcd20f-532d-4ee6-b2c7-18dbb7584a87
caps.latest.revision: 86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a14e748959ca5553dc6a8e2af6d26700ab418e7d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32932448"
---
# <a name="database-properties-mirroring-page"></a>데이터베이스 속성(미러링 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  주 데이터베이스에서 이 페이지에 액세스한 다음 이 페이지를 사용하여 데이터베이스의 데이터베이스 미러링 속성을 구성하고 수정할 수 있습니다. 또한 이 페이지를 사용하여 데이터베이스 미러링 보안 구성 마법사를 시작하면 미러링 세션의 상태를 보거나 데이터베이스 미러링 세션을 일시 중지 또는 제거할 수 있습니다.  
  
> **중요** 보안을 구성해야 미러링을 시작할 수 있습니다. 미러링이 시작되지 않은 경우 마법사를 사용하여 시작해야 합니다. 마법사를 완료할 때까지 **미러링** 페이지 입력란은 사용할 수 없습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링 구성**  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="options"></a>변수  
 **보안 구성**  
 **데이터베이스 미러링 보안 구성 마법사**를 시작하려면 이 단추를 클릭합니다.  
  
 마법사가 성공적으로 완료되면 미러링이 이미 시작되었는지 여부에 따라 다른 동작이 수행됩니다.  
  
|||  
|-|-|  
|미러링이 시작되지 않은 경우|속성 페이지는 해당 연결 정보를 캐시할 뿐만 아니라 미러 데이터베이스에 파트너 속성 집합이 있는지 여부를 나타내는 값을 캐시합니다.<br /><br /> 마법사 완료 시 기본 서버 네트워크 주소 및 운영 모드를 사용하여 데이터베이스 미러링을 시작하라는 메시지가 표시됩니다. 주소나 운영 모드를 변경해야 할 경우 **미러링 시작 안 함**을 클릭합니다.|  
|미러링이 시작된 경우|마법사에서 미러링 모니터 서버를 변경한 경우 그에 따라 미러링 모니터 서버가 설정됩니다.|  
  
 **서버 네트워크 주소**  
 **주 서버**, **미러 서버**및 **미러링 모니터 서버**등 각 서버 인스턴스마다 해당하는 옵션이 있습니다.  
  
 데이터베이스 미러링 보안 구성 마법사를 완료하면 서버 인스턴스의 서버 네트워크 주소가 자동으로 지정됩니다. 마법사를 완료한 후 필요한 경우 네트워크 주소를 수동으로 수정할 수 있습니다.  
  
 서버 네트워크 주소의 기본 구문은 다음과 같습니다.  
  
 TCP**://***fully_qualified_domain_name***:***port*  
  
 여기서  
  
-   *fully_qualified_domain_name* 은 서버 인스턴스가 존재하는 서버입니다.  
  
-   *port* 는 서버 인스턴스의 데이터베이스 미러링 끝점에 할당된 포트입니다.  
  
     데이터베이스 미러링에 참가하려면 서버에 데이터베이스 미러링 끝점이 필요합니다. 데이터베이스 미러링 보안 구성 마법사를 사용하여 서버 인스턴스의 첫 번째 미러링 세션을 설정하면 끝점이 자동으로 생성되고 Windows 인증을 사용하도록 구성됩니다. 인증서 기반 인증으로 마법사를 사용하는 방법은 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)을 클릭합니다.  
  
    >**중요!!**  지원할 미러링 세션 수에 관계없이 각 서버 인스턴스에 한 개의 데이터베이스 미러링 끝점이 필요하고, 또 하나만 가질 수 있습니다.  
  
 예를 들어 끝점이 포트 `DBSERVER9` 를 사용하는 `7022`라는 컴퓨터 시스템의 서버 인스턴스에 대한 네트워크 주소는 다음과 같을 수 있습니다.  
  
```  
TCP://DBSERVER9.COMPANYINFO.ADVENTURE-WORKS.COM:7022  
```  
  
 자세한 내용은 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)을 클릭합니다.  
  
> **참고:** 주 서버 인스턴스와 미러 서버 인스턴스는 데이터베이스 미러링 세션 중에 변경할 수 없지만 미러링 모니터 서버 인스턴스는 세션 중에 변경할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 **미러링 시작**  
 다음 조건이 모두 충족될 때 미러링을 시작하려면 클릭합니다.  
  
-   미러 데이터베이스가 있어야 합니다.  
  
     WITH NORECOVERY를 사용하여 주 데이터베이스의 최근 전체 백업과 로그 백업을 미러 서버에 복원하여 미러 데이터베이스를 만들어야 미러링을 시작할 수 있습니다. 자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)을 사용합니다.  
  
-   주 서버 인스턴스와 미러 서버 인스턴스의 TCP 주소가 이미 **서버 네트워크 주소** 섹션에서 지정되었습니다.  
  
-   운영 모드를 자동 장애 조치(Failover)가 있는 보호 우선(동기)으로 설정한 경우에는 미러 서버 인스턴스의 TCP 주소도 지정됩니다.  
  
-   보안이 올바로 구성되었습니다.  
  
 세션을 시작하려면 **미러링 시작** 을 클릭합니다. 데이터베이스 엔진이 자동으로 미러링 파트너에 연결하여 미러 서버가 올바로 구성되었는지 확인하고 미러링 세션을 시작합니다. 미러링을 시작할 수 있는 경우 데이터베이스를 모니터링하기 위한 작업이 만들어집니다.  
  
 **일시 중지** 또는 **재개**  
 데이터베이스 미러링 세션 도중에 세션을 일시 중지하려면 **일시 중지** 를 클릭합니다. 확인 메시지가 나타납니다. **예**를 클릭하면 세션이 일시 중지되고 단추가 **재개**로 바뀝니다. 세션을 재개하려면 **재개**를 클릭합니다.  
  
 세션의 일시 중지에 따른 영향에 대한 자세한 내용은 [데이터베이스 미러링 일시 중지 및 재개&#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)을 클릭합니다.  
  
> **중요!!** 강제 서비스 이후에 원래 주 서버가 다시 연결되면 미러링이 일시 중지됩니다. 이 경우 미러링을 재개하면 원래 주 서버의 데이터가 손실될 수 있습니다. 데이터 손실 위험을 관리하는 방법은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)을 클릭합니다.  
  
 **미러링 제거**  
 주 서버 인스턴스에서 세션을 중지하고 데이터베이스에서 미러링 구성을 제거하려면 클릭합니다. 확인 메시지가 나타납니다. **예**를 클릭하면 세션이 중지되고 미러링이 제거됩니다. 데이터베이스 미러링 제거의 영향에 대한 자세한 내용은 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)을 클릭합니다.  
  
> **참고:** 서버 인스턴스에서 유일하게 미러된 데이터베이스인 경우 모니터 작업이 제거됩니다.  
  
 **장애 조치**  
 주 데이터베이스를 미러 데이터베이스에 수동으로 장애 조치하려면 클릭합니다.  
  
> **참고:** 미러링 세션이 성능 우선 모드에서 실행되는 경우 수동 장애 조치가 지원되지 않습니다. 수동으로 장애 조치(failover)하려면 먼저 운영 모드를 **자동 장애 조치(failover)가 없는 보호 우선(동기)** 으로 변경해야 합니다. 장애 조치(failover)가 완료된 후 새 주 서버 인스턴스에서 모드를 다시 **성능 우선(비동기)** 으로 변경할 수 있습니다.  
  
 확인 메시지가 나타납니다. **예**를 클릭하면 장애 조치가 시도됩니다. 먼저 주 서버가 Windows 인증을 사용하여 미러 서버에 대한 연결을 시도합니다. Windows 인증을 사용할 수 없는 경우 주 서버는 **서버에 연결** 대화 상자를 표시합니다. 미러 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 **인증** 상자에서 **SQL Server 인증** 을 선택합니다. **로그인** 입력란에 미러 서버에서 연결에 사용할 로그인 계정을 지정하고 **암호** 입력란에 해당 계정의 암호를 지정합니다.  
  
 장애 조치가 성공할 경우 **데이터베이스 속성** 대화 상자가 닫힙니다. 그리고 주 서버 역할과 미러 서버 역할이 전환되어 이전의 미러 데이터베이스가 주 데이터베이스가 되고 그 반대도 마찬가지입니다. 이전 주 데이터베이스가 미러 데이터베이스로 바뀌었기 때문에 **데이터베이스 속성** 대화 상자는 이전 주 데이터베이스에서 즉시 사용할 수 없게 됩니다. 이 대화 상자는 장애 조치 후 새 주 데이터베이스에서 사용할 수 있게 됩니다.  
  
 장애 조치가 실패할 경우 오류 메시지가 표시되고 대화 상자는 열린 상태로 유지됩니다.  
  
> **중요!!** **데이터베이스 속성** 대화 상자에서 속성을 수정한 후 **장애 조치(Failover)** 를 클릭하면 해당 변경 내용이 손실됩니다. 현재 변경 내용을 저장하려면 확인 메시지에 **아니요** 로 응답하고 **확인** 을 클릭하여 변경 내용을 저장합니다. 그런 다음 데이터베이스 속성 대화 상자를 다시 열고 **장애 조치(Failover)** 를 클릭합니다.  
  
 **운영 모드**  
 선택적으로 운영 모드를 변경합니다. 특정 운영 모드의 가용성은 미러링 모니터 서버에 대해 TCP 주소를 지정했는지에 따라 달라집니다. 다음과 같은 옵션이 있습니다.  
  
|옵션|미러링 모니터 여부|설명|  
|------------|--------------|-----------------|  
|**성능 우선(비동기)**|Null(있어도 사용되지 않지만 세션에 쿼럼이 필요함)|성능을 최대화하기 위해 미러 데이터베이스는 항상 주 데이터베이스와 시간 간격을 두며 앞서가지 않습니다. 그러나 두 데이터베이스의 시간 간격은 일반적으로 크지 않습니다. 파트너가 손실되면 다음과 같은 결과가 나타납니다.<br /><br /> 미러 서버 인스턴스를 사용할 수 없는 경우 주 서버 인스턴스가 계속합니다.<br /><br /> 주 서버 인스턴스를 사용할 수 없는 경우 미러 서버 인스턴스가 중지됩니다. 세션에 미러링 모니터 서버가 없거나(권장 사항) 미러링 모니터 서버가 미러 서버에 연결된 경우 미러 서버는 웜 대기 상태로 계속 액세스할 수 있습니다. 데이터베이스 소유자는 미러 서버 인스턴스에 서비스를 강제 적용할 수 있으며, 이 경우 데이터가 손실될 수 있습니다.|  
|**자동 장애 조치(failover)가 없는 보호 우선(동기)**|아니오|커밋된 모든 트랜잭션이 미러 서버의 디스크에 기록됩니다.<br /><br /> 파트너가 서로 연결되어 있는 경우 수동 장애 조치를 사용할 수 있습니다.<br /><br /> 파트너가 손실되면 다음과 같은 결과가 나타납니다.<br /><br /> 미러 서버 인스턴스를 사용할 수 없는 경우 주 서버 인스턴스가 계속합니다.<br /><br /> 주 서버 인스턴스를 사용할 수 없는 경우 미러 서버 인스턴스가 중지되지만 웜 대기 상태로 사용할 수 있습니다. 데이터베이스 소유자는 미러 서버 인스턴스에 서비스를 강제 적용할 수 있으며, 이 경우 데이터가 손실될 수 있습니다.|  
|**자동 장애 조치(Failover)가 있는 보호 우선(동기)**|예(필수)|자동 장애 조치를 지원하도록 미러링 모니터 서버 인스턴스를 포함하여 가용성을 최대화합니다. 미러링 모니터 서버 주소를 먼저 지정한 경우에만 **자동 장애 조치(failover)가 있는 보호 우선(동기)** 옵션을 선택할 수 있습니다.<br /><br /> 파트너가 서로 연결되어 있는 경우 수동 장애 조치를 사용할 수 있습니다.<br /><br /> **\*\* 중요 \*\*** 미러링 모니터 서버의 연결이 끊어지면 파트너가 서로 연결되어 있어야만 데이터베이스를 사용할 수 있습니다. 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.<br /><br /> 동기 운영 모드에서는 커밋된 모든 트랜잭션이 미러 서버의 디스크에 기록됩니다. 미러링 모니터 서버가 있을 경우 파트너가 손실되면 다음과 같은 결과가 나타납니다.<br /><br /> 주 서버 인스턴스를 사용할 수 없는 경우 자동 장애 조치가 수행됩니다. 미러 서버 인스턴스가 주 서버 인스턴스의 역할로 전환하여 해당 데이터베이스를 주 데이터베이스로 제공합니다.<br /><br /> 미러 서버 인스턴스를 사용할 수 없는 경우 주 서버 인스턴스가 계속합니다.<br /><br /> <br /><br /> 자세한 내용은 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)을(를) 참조하세요.|  
  
 미러링이 시작된 후 운영 모드를 변경하고 **확인**을 클릭하여 변경 사항을 저장할 수 있습니다.  
  
 운영 모드에 대한 자세한 내용은 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)을 참조하십시오.  
  
 **상태**  
 미러링이 시작되면 **상태** 패널에 **미러링** 페이지를 선택했을 당시의 데이터베이스 미러링 세션 상태가 표시됩니다. **상태** 패널을 업데이트하려면 **새로 고침** 단추를 클릭합니다. 가능한 상태는 다음과 같습니다.  
  
|상태|설명|  
|------------|-----------------|  
|**이 데이터베이스는 미러링용으로 구성되지 않았습니다.**|데이터베이스 미러링 세션이 없으며 **미러링** 페이지에 대해 보고할 활동이 없습니다.|  
|**일시 중지됨**|주 데이터베이스는 사용 가능하지만 미러 서버로 로그를 보내지 않습니다.|  
|**연결 없음**|주 서버 인스턴스를 해당 파트너에 연결할 수 없습니다.|  
|**동기화 중**|미러 데이터베이스의 내용이 주 데이터베이스의 내용보다 오래된 것입니다. 주 서버 인스턴스에서 로그 레코드를 미러 서버 인스턴스로 보내면 미러 서버 인스턴스에서 변경 사항을 미러 데이터베이스에 적용하여 롤포워드합니다.<br /><br /> 데이터베이스 미러링 세션을 시작할 때는 미러 데이터베이스와 주 데이터베이스가 이 상태입니다.|  
|**장애 조치**|주 서버 인스턴스에서 수동 장애 조치(역할 전환)가 시작되었지만 서버에서 미러 역할로 현재 전환하는 중입니다. 이 상태에서 주 데이터베이스에 대한 사용자 연결이 신속하게 종료되면 데이터베이스는 즉시 미러 역할을 수행합니다.|  
|**동기화됨**|미러 서버가 주 서버와 충분히 동기화되면 데이터베이스 상태가 **동기화됨**으로 변경됩니다. 주 서버에서 계속 변경 내용을 미러 서버로 보내고 미러 서버에서 계속 변경 내용을 미러 데이터베이스에 적용하면 데이터베이스는 이 상태로 유지됩니다.<br /><br /> 보호 우선 모드의 경우 데이터 손실 없이 장애 조치가 가능합니다.<br /><br /> 성능 우선 모드의 경우 **동기화됨** 상태에서도 일부 데이터 손실이 항상 발생할 수 있습니다.|  
  
 자세한 내용은 [미러링 상태&#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)를 참조하세요.  
  
 **새로 고침**  
 **상태** 상자를 업데이트하려면 클릭합니다.  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 미러링에 익숙하지 않으면 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 클릭합니다.  
  
### <a name="adding-a-witness-to-an-existing-session"></a>기존 세션에 미러링 모니터 서버 추가  
 미러링 모니터 서버를 기존 세션에 추가하거나 기존 미러링 모니터 서버를 바꿀 수 있습니다. 미러링 모니터 서버의 서버 네트워크 주소를 알고 있는 경우 **미러링 모니터 서버** 필드에 수동으로 입력할 수 있습니다. 미러링 모니터 서버의 서버 네트워크 주소를 모를 경우 데이터베이스 미러링 보안 구성 마법사를 사용하여 미러링 모니터 서버를 구성할 수 있습니다. 필드에 주소가 있으면 **자동 장애 조치(failover)가 있는 보호 우선(동기)** 옵션이 선택되었는지 확인합니다.  
  
 새 미러링 모니터 서버를 구성한 후 **확인** 을 클릭하여 미러링 세션에 추가해야 합니다.  
  
 **Windows 인증 사용 시 미러링 모니터 서버를 추가하려면**  
  
 [데이터베이스 미러링 모니터 서버 추가 또는 바꾸기&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
### <a name="removing-a-witness"></a>미러링 모니터 서버 제거  
 미러링 모니터 서버를 제거하려면 **미러링 모니터 서버** 필드에서 서버 네트워크 주소를 삭제합니다. 자동 장애 조치(failover)가 있는 보호 우선 모드에서 성능 우선 모드로 전환하면 **미러링 모니터 서버** 필드가 자동으로 지워집니다.  
  
 미러링 모니터 서버를 삭제한 다음에는 **확인** 을 클릭해야 미러링 세션에서 해당 서버가 제거됩니다.  
  
### <a name="monitoring-database-mirroring"></a>데이터베이스 미러링 모니터링  
 서버 인스턴스에서 미러된 데이터베이스를 모니터링하려면 데이터베이스 미러링 모니터 또는 sp_dbmmonitorresults 시스템 저장 프로시저를 사용합니다.  
  
 **미러된 데이터베이스를 모니터링하려면**  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitorresults&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
 자세한 내용은 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)을 클릭합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 일시 중지 및 재개&#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 모니터 서버](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
