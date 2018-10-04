---
title: 장애 조치 및 장애 조치 모드 (AlwaysOn 가용성 그룹) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], failover
- Availability Groups [SQL Server], failover modes
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 378d2d63-50b9-420b-bafb-d375543fda17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0603ccd35973b27993207d634ebc89aa90e6fa1b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140612"
---
# <a name="failover-and-failover-modes-alwayson-availability-groups"></a>장애 조치(Failover) 및 장애 조치(Failover) 모드(AlwaysOn 가용성 그룹)
  가용성 그룹의 컨텍스트 내에서는 일반적으로 가용성 복제본의 주 역할과 보조 역할을 *장애 조치(Failover)* 라는 프로세스에서 서로 바꿀 수 있습니다. 자동 장애 조치(데이터가 손실되지 않음), 계획된 수동 장애 조치(데이터가 손실되지 않음)와 *강제 장애 조치(failover)* 라고 불리는 강제 수동 장애 조치(데이터가 손실될 수 있음)의 세 가지 형태가 있습니다. 자동 및 계획된 수동 장애 조치(Failover)는 모든 데이터를 보존합니다. 가용성 그룹은 가용성 복제본의 수준에서 장애 조치(Failover)됩니다. 즉, 가용성 그룹은 해당 보조 복제본 중 하나(현재 *장애 조치(Failover) 대상*)로 장애 조치(Failover)됩니다.  
  
> [!NOTE]  
>  따라서 데이터 파일 손실, 데이터베이스 삭제, 트랜잭션 로그 손상 등으로 인해 주의 대상 데이터베이스가 발생할 경우 이러한 데이터베이스 수준의 문제로는 가용성 그룹의 장애 조치(Failover)가 수행되지 않습니다.  
  
 장애 조치(Failover) 동안에는 장애 조치(Failover) 대상이 주 역할을 맡아 데이터베이스를 복구하고 이 데이터베이스를 새로운 주 데이터베이스로 하여 온라인 상태로 만듭니다. 이전 주 복제본은 사용 가능한 경우 보조 역할로 전환되고 해당 데이터베이스는 보조 데이터베이스가 됩니다. 잠재적으로 여러 오류에 대한 응답이나 관리를 위해 이러한 역할이 상호 또는 다른 장애 조치(Failover) 대상으로 전환될 수 있습니다.  
  
 지정된 가용성 복제본에서 지원하는 장애 조치(Failover)의 형태는 *장애 조치(Failover) 모드* 속성으로 지정됩니다. 지정된 가용성 복제본의 경우 가능한 장애 조치(Failover) 모드는 다음과 같이 복제본의 [가용성 모드](availability-modes-always-on-availability-groups.md) 에 따라 다릅니다.  
  
-   **동기-커밋 복제본** - 두 가지 설정(자동 또는 수동)을 지원합니다. "자동" 설정은 자동 장애 조치(Failover)와 수동 장애 조치(Failover)를 모두 지원합니다. 데이터 손실을 방지하기 위해 자동 장애 조치(Failover) 및 계획된 장애 조치(Failover)에서는 장애 조치(Failover) 대상이 동기화 상태가 정상(장애 조치(Failover) 대상의 모든 보조 데이터베이스가 해당 주 데이터베이스와 동기화된 상태)인 동기-커밋 보조 복제본이어야 합니다. 보조 복제본이 이러한 조건을 모두 충족하지 않을 때는 항상 강제 장애 조치(Failover)만 지원됩니다. 강제 장애 조치(Failover)는 또한 역할이 RESOLVING 상태인 복제본을 지원합니다.  
  
-   **비동기-커밋 복제본** 은 수동 장애 조치(Failover) 모드만 지원합니다. 또한, 절대 동기화되지 않기 때문에 강제 장애 조치(Failover)만 지원합니다.  
  
> [!NOTE]  
>  장애 조치(Failover) 후 주 데이터베이스에 액세스해야 하는 클라이언트 응용 프로그램은 새로운 주 복제본에 연결되어야 합니다. 또한 새로운 보조 복제본이 읽기 전용 액세스를 허용하도록 구성되면 읽기 전용 클라이언트 응용 프로그램이 해당 복제본에 연결할 수 있습니다. 클라이언트가 가용성 그룹에 연결하는 방법에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)를 참조하세요.  
  
  
##  <a name="TermsAndDefinitions"></a> 용어 및 정의  
 자동 장애 조치(automatic failover)  
 주 복제본이 손실되는 경우 자동으로 발생하는 장치 조치(failover)입니다. 자동 장애 조치(Failover)는 현재 주 복제본과 하나의 보조 복제본이 모두 AUTOMATIC으로 설정된 장애 조치(Failover) 모드로 구성되고 보조 복제본이 현재 동기화된 경우에만 지원됩니다.  주 복제본 또는 보조 복제본의 장애 조치(Failover) 모드가 MANUAL인 경우 장애 조치(Failover)를 수행할 수 없습니다.  
  
 계획된 수동 장애 조치(Failover)(데이터가 손실되지 않음)  
 계획된 수동 장애 조치(Failover) 또는 *수동 장애 조치(Failover)* 는 일반적으로 관리 목적을 위해 데이터베이스 관리자가 시작하는 장애 조치(Failover)입니다. 계획된 수동 장애 조치(Failover)는 주 복제본과 보조 복제본이 동기-커밋 모드에 대해 구성되고 보조 복제본이 현재 동기화된(SYNCHRONIZED 상태) 경우에만 지원됩니다. 대상 보조 복제본이 동기화되면 보조 데이터베이스에서 장애 조치(Failover)를 수행할 준비가 되었기 때문에 주 복제본이 충돌하더라도 수동 장애 조치(Failover)(데이터가 손실되지 않음)가 가능합니다. 데이터베이스 관리자가 수동 장애 조치(Failover)를 수동으로 시작합니다.  
  
 강제 장애 조치(failover)(데이터가 손실될 수 있음)  
 보조 복제본이 주 복제본과 동기화되지 않거나 주 복제본이 실행되고 있지 않아서 보조 복제본의 장애 조치(failover)가 준비되지 않았을 때 데이터베이스 관리자가 시작할 수 있는 장애 조치(Failover)입니다. 강제 장애 조치(Failover)는 데이터가 손실될 수 있는 위험이 있으며 재해 복구용으로만 사용하는 것이 좋습니다. 강제 장애 조치(failover)는 수동으로만 시작될 수 있기 때문에 강제 수동 장애 조치(failover)라고도 합니다. 이 장애 조치(Failover)는 비동기-커밋 가용성 모드에서 지원되는 유일한 장애 조치(Failover) 형태입니다.  
  
 [!INCLUDE[ssFosAutoC](../../../includes/ssfosautoc-md.md)]  
 지정된 가용성 그룹 내에서 자동 장애 조치(Failover)를 사용하는 동기-커밋 모드(있는 경우)에 대해 구성된 가용성 복제본의 쌍(현재 주 복제본 포함)입니다. [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)]은(는) 보조 복제본이 주 복제본과 현재 SYNCHRONIZED된 경우에만 효과가 있습니다.  
  
 [!INCLUDE[ssFosSyncC](../../../includes/ssfossyncc-md.md)]  
 지정된 가용성 그룹 내에서 동기-커밋 모드(있는 경우)로 구성된 2개 또는 3개의 가용성 복제본(현재 주 복제본 포함) 집합입니다. [!INCLUDE[ssFosSync](../../../includes/ssfossync-md.md)]은(는) 보조 복제본이 수동 장애 조치(Failover) 모드로 구성되고 하나 이상의 보조 복제본이 주 복제본과 현재 SYNCHRONIZED된 경우에만 효과가 있습니다.  
  
 [!INCLUDE[ssFosEntireC](../../../includes/ssfosentirec-md.md)]  
 지정된 가용성 그룹 내에서 가용성 모드 및 장애 조치(Failover) 모드와 상관없이 작업 상태가 현재 ONLINE인 모든 가용성 복제본 집합입니다. [!INCLUDE[ssFosEntire](../../../includes/ssfosentire-md.md)]은(는) 보조 복제본이 주 복제본과 현재 SYNCHRONIZED된 경우에만 관련이 있습니다.  
  
##  <a name="Overview"></a> 장애 조치(Failover) 개요  
 다음 표에서는 다양한 가용성 모드 및 장애 조치(Failover) 모드에서 지원되는 장애 조치(Failover) 형태를 요약합니다. 각 쌍에 대해 유효한 가용성 모드 및 장애 조치(Failover) 모드는 주 복제본 모드와 하나 이상의 보조 복제본 모드의교차로 결정됩니다.  
  
||비동기-커밋 모드|수동 장애 조치(Failover) 모드를 사용하는 동기-커밋 모드|자동 장애 조치(Failover) 모드를 사용하는 동기-커밋 모드|  
|-|-------------------------------|---------------------------------------------------------|------------------------------------------------------------|  
|자동 장애 조치(automatic failover)|아니요|아니요|사용자 계정 컨트롤|  
|계획된 수동 장애 조치(Failover)|아니요|예|사용자 계정 컨트롤|  
|강제 장애 조치(failover)|사용자 계정 컨트롤|사용자 계정 컨트롤|예**<sup>*</sup>**|  
  
 **<sup>*</sup>**  동기화 된 보조 복제본에 강제 장애 조치 명령을 실행 하는 경우 보조 복제본을 수동 장애 조치의 경우와 동일 하 게 동작 합니다.  
  
 장애 조치(Failover) 중에 데이터베이스를 사용할 수 없는 시간은 장애 조치(Failover)의 유형과 원인에 따라 달라집니다.  
  
> [!IMPORTANT]  
>  포함된 데이터베이스를 제외하고 장애 조치(Failover) 후 클라이언트 연결을 지원하려면 이전 주 데이터베이스에 정의된 로그인 및 작업을 새로운 주 데이터베이스에서 수동으로 다시 만들어야 합니다. 자세한 내용은 [가용성 그룹의 데이터베이스에 대한 로그인 및 작업 관리&#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
### <a name="failover-sets"></a>장애 조치(Failover) 집합  
 지정된 가용성 그룹에 대해 가능한 장애 조치(Failover)의 형태는 장애 조치(Failover) 설정의 관점에서 이해할 수 있습니다. 장애 조치(Failover) 설정은 다음과 같이 지정된 형태의 장애 조치(Failover)를 지원하는 주 복제본과 보조 복제본으로 구성됩니다.  
  
-   **[!INCLUDE[ssFosAutoC](../../../includes/ssfosautoc-md.md)] (옵션):**  지정된 가용성 그룹 내에서 자동 장애 조치(Failover)를 사용하는 동기-커밋 모드(있는 경우)로 구성된 가용성 복제본의 쌍(현재 주 복제본 포함)입니다. 자동 장애 조치(Failover) 설정은 보조 복제본이 주 복제본과 현재 SYNCHRONIZED된 경우에만 효과가 있습니다.  
  
-   **[!INCLUDE[ssFosSyncC](../../../includes/ssfossyncc-md.md)] (옵션):**  지정된 가용성 그룹 내에서 동기-커밋 모드(있는 경우)로 구성된 2개 또는 3개의 가용성 복제본(현재 주 복제본 포함) 집합입니다. 동기 커밋 장애 조치(Failover) 설정은 보조 복제본이 수동 장애 조치(Failover) 모드에 대해 구성되고 하나 이상의 보조 복제본이 주 복제본과 현재 SYNCHRONIZED된 경우에만 효과가 있습니다.  
  
-   **[!INCLUDE[ssFosEntireC](../../../includes/ssfosentirec-md.md)] :**  지정된 가용성 그룹 내에서 가용성 모드 및 장애 조치(Failover) 모드와 상관없이 작업 상태가 현재 ONLINE인 모든 가용성 복제본 집합입니다. 전체 장애 조치(Failover) 설정은 보조 복제본이 주 복제본과 현재 SYNCHRONIZED된 경우에만 관련이 있습니다.  
  
 자동 장애 조치(Failover)를 사용하는 동기 커밋으로 가용성 복제본을 구성하면 가용성 복제본은 [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)]의 일부가 됩니다. 하지만 이 집합이 적용되는지 여부는 현재 주 복제본에 따라 다릅니다. 지정된 시간에 실제로 가능한 장애 조치(Failover) 형태는 현재 적용되는 장애 조치(Failover) 집합에 따라 다릅니다.  
  
 예를 들어, 다음과 같은 네 개의 가용성 복제본이 있는 가용성 그룹을 고려합니다.  
  
|복제본|가용성 모드 및 장애 조치(Failover) 모드 설정|  
|-------------|--------------------------------------------------|  
|변수를 잠그기 위한|자동 장애 조치(Failover)를 사용하는 동기 커밋|  
|B|자동 장애 조치(Failover)를 사용하는 동기 커밋|  
|C|계획된 수동 장애 조치(failover)만 사용하는 동기-커밋|  
|d|강제 장애 조치(Failover)만 사용하는 비동기 커밋|  
  
 각 보조 복제본에 대한 장애 조치(Failover) 동작은 어떤 가용성 복제본이 현재 주 복제본인지에 따라 결정됩니다. 기본적으로 지정된 보조 복제본에 대해 장애 조치(Failover) 동작은 현재 주 복제본에서 최악의 경우입니다. 다음 그림에서는 현재 주 복제본에 따라 보조 복제본의 장애 조치(Failover) 동작이 어떻게 달라지는지와 보조 복제본의 장애 조치(Failover) 동작이 강제 장애 조치(Failover)만 사용하는 비동기-커밋 모드용으로 구성되었는지 자동 장애 조치(Failover)를 사용하거나 사용하지 않는 동기-커밋 모드용으로 구성되었는지를 보여 줍니다.  
  
 ![주 복제본 구성이 장애 조치에 미치는 영향](../../media/aoag-failoversetexample.gif "주 복제본 구성이 장애 조치에 미치는 영향")  
  
##  <a name="AutomaticFailover"></a> Automatic Failover  
 자동 장애 조치(Failover)를 수행하면 주 복제본이 사용할 수 없게 된 후 정규화된 보조 복제본이 주 역할로 자동으로 전환됩니다. 자동 장애 조치(Failover)는 주 복제본을 호스팅하는 WSFC 노드가 보조 복제본을 호스팅하는 노드에 대해 로컬인 경우에 가장 적합합니다. 이는 데이터 동기화가 컴퓨터 간의 메시지 대기 시간이 짧은 경우 가장 잘 작동하고 클라이언트 연결이 로컬로 유지될 수 있기 때문입니다.  
  
  
###  <a name="RequiredConditions"></a> 자동 장애 조치(Failover)에 필요한 상태  
 자동 장애 조치(Failover)는 다음 상태에서만 수행됩니다.  
  
-   자동 장애 조치(Failover) 설정이 있습니다. 이 설정은 모두 동기-커밋 모드로 구성되고 자동 장애 조치(Failover)로 설정된 주 복제본과 보조 복제본(*자동 장애 조치(Failover) 대상*)으로 구성됩니다. HYPERLINK "file:///C:\\\Users\\\marshow\\\AppData\\\Local\\\Temp\\\DxEditor\\\DduePreview\\\Default\\\6fe88e12-4df1-4025-ba24-7579635ccecf\\\HTM\\\html\\\29e0ac5d-eb58-4801-82b9-e278f08db920" 주 복제본이 수동 장애 조치(failover)로 설정되면 보조 복제본이 자동 장애 조치(failover)로 설정된 경우에도 자동 장애 조치(failover)가 수행되지 않습니다.  
  
     자세한 내용은 [가용성 모드&#40;AlwaysOn 가용성 그룹&#41;](availability-modes-always-on-availability-groups.md)를 참조하세요.  
  
-   자동 장애 조치(Failover) 대상의 동기화 상태는 정상 상태, 즉 장애 조치(Failover) 대상의 모든 보조 데이터베이스가 해당 주 데이터베이스와 동기화되는 상태입니다.  
  
    > [!TIP]  
    >  AlwaysOn 가용성 그룹은 자동 장애 조치(Failover) 설정에서 두 복제본의 상태를 모니터링합니다. 복제본 중 하나가 실패하면 가용성 그룹의 상태는 CRITICAL로 설정됩니다. 보조 복제본이 실패하면 자동 장애 조치(Failover) 대상을 사용할 수 없기 때문에 자동 장애 조치(Failover)가 발생할 수 없습니다. 주 복제본이 실패하면 가용성 그룹이 보조 복제본으로 장애 조치(Failover)됩니다. 이전 주 복제본이 온라인 상태가 될 때까지는 자동 장애 조치(Failover) 대상이 존재하지 않습니다. 어떤 경우든, 드물기는 하지만 순차적 실패가 일어날 때 가용성을 보장하기 위해 다른 보조 복제본을 자동 장애 조치(Failover) 대상으로 구성하는 것이 좋습니다.  
    >   
    >  자세한 내용은 [AlwaysOn 정책을 사용하여 가용성 그룹의 상태 보기&#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md) 및 [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)을 참조하세요.  
  
-   WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터는 쿼럼이 있습니다. 자세한 내용은 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)을 참조하세요.  
  
-   주 복제본이 사용할 수 없게 되었으며 유연한 장애 조치(Failover) 정책에 정의된 장애 조치(Failover) 상태 수준을 충족합니다. 장애 조치 상태 수준에 대한 자세한 내용은 [가용성 그룹 자동 장애 조치에 대한 유연한 장애 조치(Failover) 정책&#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
###  <a name="HowAutoFoWorks"></a> 자동 장애 조치 작동 방법  
 자동 장애 조치(Failover)는 다음과 같은 일련의 동작을 시작합니다.  
  
1.  현재 주 복제본을 호스팅하는 서버 인스턴스가 여전히 실행 중인 경우 주 복제본의 상태를 DISCONNECTED로 변경하고 모든 클라이언트의 연결을 끊습니다.  
  
2.  로그 레코드가 대상 보조 복제본의 Recovery Queue에서 대기 중인 경우 보조 복제본이 나머지 로그 레코드에 적용되어 보조 데이터베이스의 롤포워드를 마칩니다.  
  
    > [!NOTE]  
    >  지정된 데이터베이스에 로그를 적용하는 데 필요한 시간은 시스템 속도, 최근 작업 로드 및 Recovery Queue에 있는 로그 양에 따라 달라집니다.  
  
3.  이전 보조 복제본이 주 역할로 전환됩니다. 해당 데이터베이스는 주 데이터베이스가 됩니다. 새로운 주 복제본은 커밋되지 않은 트랜잭션(복구의 실행 취소 단계)을 최대한 빠르게 롤백합니다. 잠금은 클라이언트가 데이터베이스를 사용하는 동안 백그라운드에서 롤백을 수행할 수 있도록 이러한 커밋되지 않은 트랜잭션을 격리합니다. 이 프로세스에서는 커밋된 트랜잭션이 롤백되지 않습니다.  
  
     지정된 보조 데이터베이스가 연결될 때까지 NOT_SYNCHRONIZED로 간략하게 표시됩니다. 롤백 복구가 시작되기 전에 보조 데이터베이스는 새로운 주 데이터베이스에 연결하여 SYNCHRONIZED 상태로 빨리 전환될 수 있습니다. 일반적으로 최상의 경우는 장애 조치(Failover) 후에 보조 역할에 유지되는 세 번째 동기 커밋 복제본입니다.  
  
4.  나중에 이전 주 복제본을 호스팅하는 서버 인스턴스가 다시 시작되면 이제 다른 가용성 복제본이 주 역할을 소유하고 있음을 인식합니다. 이전 주 복제본은 보조 역할로 전환되고 해당 데이터베이스는 보조 데이터베이스가 됩니다. 새로운 보조 복제본은 현재 주 복제본에 연결하고 최대한 빠르게 해당 데이터베이스를 현재 주 데이터베이스와 동기화합니다. 새로운 보조 복제본이 해당 데이터베이스를 다시 동기화한 후 즉시 장애 조치(Failover)를 반대 방향으로 다시 수행할 수 있습니다.  
  
###  <a name="EnableAutoFo"></a> 자동 장애 조치(Failover)를 구성하려면  
 언제든지 자동 장애 조치(Failover)를 지원하도록 가용성 복제본을 구성할 수 있습니다.  
  
 **To configure automatic failover**  
  
1.  보조 복제본이 동기-커밋 가용성 모드를 사용하도록 구성되어 있는지 확인합니다. 자세한 내용은 [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
2.  장애 조치(Failover) 모드를 자동으로 설정합니다. 자세한 내용은 [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
3.  필요에 따라 가용성 그룹의 유연한 장애 조치(Failover) 정책을 변경하여 자동 장애 조치(Failover)를 발생시킬 수 있는 오류의 유형을 지정할 수 있습니다. 자세한 내용은 [유연한 장애 조치(failover) 정책을 구성하여 자동 장애 조치(failover)의 상태 제어&#40;AlwaysOn 가용성 그룹&#41;](configure-flexible-automatic-failover-policy.md) HYPERLINK "file:///C:\\\Users\\\marshow\\\AppData\\\Local\\\Temp\\\DxEditor\\\DduePreview\\\Default\\\6a8d98a9-6e6a-40d1-9809-efa9013d7452\\\HTM\\\html\\\1ed564b4-9835-4245-ae35-9ba67419a4ce" 및 [장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)을 참조하세요.  
  
##  <a name="ManualFailover"></a> 계획된 수동 장애 조치(Failover)(데이터가 손실되지 않음)  
 수동 장애 조치(Failover)를 수행하면 대상 보조 복제본을 호스팅하는 서버 인스턴스에서 데이터베이스 관리자가 수동 장애 조치(Failover) 명령을 실행한 후에 동기화된 보조 복제본이 주 역할로 전환됩니다. 수동 장애 조치(Failover)를 지원하려면 보조 복제본과 현재 주 복제본을 모두 동기-커밋 모드(있는 경우)로 구성해야 합니다. 가용성 복제본의 모든 보조 데이터베이스를 가용성 그룹에 조인하고 해당 주 데이터베이스와 동기화해야 합니다. 즉, 보조 복제본을 동기화해야 합니다. 그러면 이전 주 데이터베이스에서 커밋된 모든 트랜잭션이 새로운 주 데이터베이스에서도 커밋됩니다. 따라서 새로운 주 데이터베이스는 기존의 주 데이터베이스와 동일합니다.  
  
 다음 그림에서는 계획된 장애 조치(Failover) 단계를 보여 줍니다.  
  
1.  장애 조치(Failover) 전에 `Node01`의 서버 인스턴스가 주 복제본을 호스팅합니다.  
  
2.  데이터베이스 관리자가 계획된 장애 조치(Failover)를 시작합니다. 장애 조치(Failover) 대상은 `Node02`의 서버 인스턴스가 호스팅하는 가용성 복제본입니다.  
  
3.  `Node02`의 장애 조치(Failover) 대상은 새로운 주 복제본이 됩니다. 계획된 장애 조치(Failover)이기 때문에 이전의 주 복제본은 장애 조치(Failover) 중에 보조 역할로 전환되고 해당 데이터베이스는 보조 데이터베이스로서 즉시 온라인 상태가 됩니다.  
  
 ![계획된 수동 장애 조치에 대한 설명](../../media/aoag-plannedmanualfailover.gif "계획된 수동 장애 조치에 대한 설명")  
  
  
###  <a name="ManualFailoverConditions"></a> 수동 장애 조치에 필요한 조건  
 수동 장애 조치(Failover)를 지원하려면 현재 주 복제본을 동기-커밋 모드로 설정해야 하며 보조 복제본은 다음과 같아야 합니다.  
  
-   동기-커밋 모드에 대해 구성되어 있어야 합니다.  
  
-   주 복제본과 현재 동기화되어 있어야 합니다.  
  
 가용성 그룹을 수동으로 장애 조치(Failover)하려면 새로운 주 복제본이 될 보조 복제본에 연결해야 합니다.  
  
###  <a name="ManualFailoverHowWorks"></a> 계획된 수동 장애 조치(Failover) 작동 방법  
 대상 보조 복제본에서 시작해야 하는 계획된 수동 장애 조치(Failover)는 다음과 같은 일련의 동작을 시작합니다.  
  
1.  원래 주 데이터베이스에서 새로운 사용자 트랜잭션이 수행되는지 확인하기 위해 WSFC 클러스터는 오프라인으로 전환하는 요청을 주 복제본에 보냅니다.  
  
2.  보조 데이터베이스의 Recovery Queue에 대기 중인 로그가 있으면 보조 복제본은 해당 보조 데이터베이스의 롤포워드를 마칩니다. 소요 시간은 시스템 속도, 최근 작업 및 Recovery Queue에 있는 로그 양에 따라 달라집니다. Recovery Queue의 현재 크기를 확인하려면 **Recovery Queue** 성능 카운터를 사용합니다. 자세한 내용은 [SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md)을 참조하세요.  
  
    > [!NOTE]  
    >  Recovery Queue의 크기를 제한하여 장애 조치(Failover) 시간을 조정할 수 있습니다. 그러나 이 경우 보조 복제본에서 동기화 상태를 계속 유지해야 하므로 주 복제본의 속도가 느려질 수 있습니다.  
  
3.  보조 복제본은 새로운 주 복제본이 되고 이전 주 복제본은 새로운 보조 복제본이 됩니다.  
  
4.  새로운 주 복제본은 커밋되지 않은 모든 트랜잭션을 롤백하고 해당 데이터베이스를 주 데이터베이스로 사용할 수 있도록 온라인 상태로 만듭니다. 모든 보조 데이터베이스는 새로운 주 데이터베이스에 연결하여 다시 동기화할 때까지 잠시 동안 NOT SYNCHRONIZED로 표시됩니다. 이 프로세스에서는 커밋된 트랜잭션이 롤백되지 않습니다.  
  
5.  이전 주 복제본이 다시 온라인 상태가 되면 이 데이터베이스가 보조 역할을 맡고 이전 주 데이터베이스는 보조 데이터베이스가 됩니다. 새로운 보조 복제본은 새로운 보조 데이터베이스를 해당 주 데이터베이스와 빠르게 다시 동기화합니다.  
  
    > [!NOTE]  
    >  새로운 보조 복제본이 해당 데이터베이스를 다시 동기화한 후 즉시 장애 조치(Failover)를 반대 방향으로 다시 수행할 수 있습니다.  
  
 장애 조치(Failover) 후 클라이언트는 현재 주 데이터베이스에 다시 연결해야 합니다. 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)개념을 소개합니다.  
  
###  <a name="ManualFailoverDuringUpgrades"></a> 업그레이드 중에 가용성 유지  
 하드웨어나 소프트웨어를 업그레이드할 때 가용성 그룹의 데이터베이스 관리자는 수동 장애 조치(Failover)를 사용하여 데이터베이스 가용성을 유지 관리할 수 있습니다. 소프트웨어 업그레이드에 가용성 그룹을 사용하려면 대상 보조 복제본을 호스팅하는 서버 인스턴스 및/또는 컴퓨터 노드는 업그레이드를 이미 수신한 상태여야 합니다. 자세한 내용은 [Upgrade and Update of Availability Group Servers with Minimal Downtime and Data Loss](upgrading-always-on-availability-group-replica-instances.md)을 참조하세요.  
  
##  <a name="ForcedFailover"></a> 강제 장애 조치(failover)(데이터가 손실될 수 있음)  
 가용성 그룹의 강제 장애 조치(Failover)(데이터가 손실될 수 있음)는 보조 복제본을 웜 대기 서버로 사용할 수 있는 재해 복구 방법입니다. 강제 장애 조치(Failover)를 수행하면 데이터가 손실될 위험이 있으므로 반드시 필요한 경우에만 주의해서 사용해야 합니다. 데이터 손실을 감수하더라도 즉시 가용성 데이터베이스 서비스를 복원해야 하는 경우에만 강제 장애 조치(Failover)를 수행하는 것이 좋습니다. 강제 장애 조치(failover)를 위한 사전 요구 사항 및 권장 사항에 대한 자세한 내용과 강제 장애 조치(failover)를 사용하여 치명적인 오류에서 복구하는 예제 시나리오는 [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
> [!WARNING]  
>  강제 장애 조치(Failover)를 수행하려면 WSFC 클러스터에 쿼럼이 있어야 합니다. 쿼럼을 구성하고 쿼럼을 강제 실행하는 방법은 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
  
###  <a name="ForcedFailoverHowWorks"></a> 강제 장애 조치(Failover) 작동 방법  
 강제 장애 조치는 주 역할을 역할이 SECONDARY 또는 RESOLVING 상태인 대상 복제본으로 전환하기 시작합니다. 장애 조치 대상은 새로운 주 복제본이 되고 클라이언트에 데이터베이스 복사본을 즉시 서비스합니다. 이전 주 복제본이 사용 가능하게 되면 보조 역할로 전환되고 해당 데이터베이스는 데이터베이스가 됩니다.  
  
 모든 보조 데이터베이스(사용할 수 있는 경우 이전 주 데이터베이스 포함)는 일시 중지됩니다. 일시 중지된 보조 데이터베이스의 이전 데이터 동기화 상태에 따라 해당 주 데이터베이스에 대한 누락된 커밋된 데이터를 복원하는 데 적합할 수 있습니다. 읽기 전용 액세스용으로 구성된 보조 복제본에서는 보조 데이터베이스를 쿼리하여 누락된 데이터를 수동으로 검색할 수 있습니다. 그런 다음 새로운 주 데이터베이스에 대해 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행하여 필요에 따라 변경할 수 있습니다.  
  
###  <a name="ForcedFailoverRisks"></a> 강제 장애 조치(Failover)의 위험  
 강제 장애 조치(Failover)를 수행하면 데이터가 손실될 수 있다는 점을 이해해야 합니다. 대상 복제본이 주 복제본과 통신할 수 없으며 따라서 데이터베이스의 동기화를 보장할 수 없기 때문에 데이터가 손실될 수 있습니다. 강제 장애 조치(Failover)를 수행하면 새 복구 분기가 시작됩니다. 원래 주 데이터베이스와 보조 데이터베이스는 서로 다른 복구 분기에 있기 때문에 각 데이터베이스에는 다른 데이터베이스에 없는 데이터가 포함됩니다. 원래 각 주 데이터베이스에는 Send Queue에서 이전 보조 데이터베이스로 아직 전송되지 않은 모든 변경 사항(보내지 않은 로그)이 포함되며, 이전 보조 데이터베이스에는 강제 장애 조치(Failover)를 수행한 후 발생한 모든 변경 사항이 포함됩니다.  
  
 주 복제본이 실패하여 강제 장애 조치(Failover)가 수행된 경우 발생 가능한 데이터 손실은 실패 전에 트랜잭션 로그를 보조 복제본으로 보냈는지 여부에 따라 달라집니다. 비동기-커밋 모드에서는 보내지 않은 누적 로그가 항상 있을 수 있습니다. 동기-커밋 모드에서는 보조 데이터베이스가 동기화될 때까지만 보내지 않은 누적 로그가 있을 수 있습니다.  
  
 다음 표에서는 강제 장애 조치(Failover)할 복제본의 특정 데이터베이스에 대한 데이터 손실 가능성을 요약하여 보여 줍니다.  
  
|보조 복제본의 가용성 모드|데이터베이스가 동기화되는지 여부|데이터가 손실될 가능성이 있는지 여부|  
|--------------------------------------------|-------------------------------|----------------------------|  
|Synchronous-commit|사용자 계정 컨트롤|아니요|  
|Synchronous-commit|아니요|사용자 계정 컨트롤|  
|Asynchronous-commit|아니요|사용자 계정 컨트롤|  
||||  
  
 보조 데이터베이스는 두 개의 복구 분기만 추적하므로 강제 장애 조치(Failover)를 여러 번 수행할 경우 이전 강제 장애 조치(Failover)와 데이터 동기화를 시작한 보조 데이터베이스는 재개하지 못할 수도 있습니다. 이 경우 재개할 수 없는 보조 데이터베이스를 올바른 시점으로 복원된 가용성 그룹에서 제거한 후 이 가용성 그룹에 다시 조인해야 합니다. 여러 복구 분기 지점에 대해 복원을 수행할 수 없으므로 둘 이상의 강제 장애 조치(Failover) 수행한 후 로그 백업을 수행해야 합니다.  
  
###  <a name="WhyFFoPostForcedQuorum"></a> 강제 쿼럼 후에 강제 장애 조치(failover)가 필요한 이유  
 WSFC 클러스터에서 쿼럼을 수행한 후에는(*강제 쿼럼*) 각 가용성 그룹에 대해 강제 장애 조치(failover)(데이터 손실 가능)를 수행해야 합니다. 강제 장애 조치(failover)가 필요한 이유는 WSFC 클러스터 값의 실제 상태가 손실되었을 수 있기 때문입니다. 강제 쿼럼 후 정상적인 장애 방지가 필요한 이유는 동기화되지 않은 보조 복제본이 다시 구성된 WSFC 클러스터에서 동기화된 것으로 나타날 수 있기 때문입니다.  
  
 세 개의 노드에서 가용성 그룹을 호스트하는 WSFC 클러스터를 예로 들어 보겠습니다. 노드 A는 주 복제본을 호스팅하며 노드 B와 노드 C는 보조 복제본을 호스팅합니다. 로컬 보조 복제본이 동기화하는 동안 노드 C는 WSFC 클러스터에서 연결이 끊어집니다.  그러나 노드 A와 노드 B는 정상 상태의 쿼럼을 유지하고 가용성 그룹을 온라인 상태로 유지합니다. 노드 A에서 주 복제본은 계속해서 업데이트를 허용하고 노드 B에서 보조 복제본은 계속해서 주 복제본과 동기화합니다. 노드 C에서 보조 복제본은 비동기화되고 주 복제본 뒤에서 점점 뒤쳐집니다. 그러나, 노드 C는 연결이 끊어졌기 때문에 복제본의 동기화 상태가 잘못 유지됩니다.  
  
 쿼럼이 손실되고 노드 A에서 강제 적용되면 WSFC 클러스터에서 가용성 그룹의 동기화 상태는 보조 복제본이 노드 C에 UNSYNCHRONIZED로 표시되는 올바른 상태여야 합니다. 그러나 노드 C에서 쿼럼이 강제 적용되면 가용성 그룹의 동기화는 잘못됩니다. 노드 C 연결이 끊어지면 클러스터의 동기화 상태는 되돌아가서 노드 C의 보조 복제본이 SYNCHRONIZED로 *잘못* 표시됩니다. 계획된 수동 장애 조치(failover)는 데이터의 안전성을 보장하므로 쿼럼이 강제 적용된 후 가용성 그룹이 다시 온라인 상태가 되도록 허용되지 않습니다.  
  
###  <a name="TrackPotentialDataLoss"></a> 잠재적인 데이터 손실 추적  
 WSFC 클러스터의 쿼럼이 정상 상태이면 데이터베이스에 대한 현재의 잠재적 데이터 손실을 예측할 수 있습니다. 지정된 보조 복제본의 경우 현재의 잠재적 데이터 손실은 로컬 보조 데이터베이스의 내용이 해당 주 데이터베이스의 내용보다 얼마나 오래되었는지에 따라 다릅니다. 지연 양은 시간에 따라 다르기 때문에 동기화되지 않은 보조 데이터베이스에 대한 잠재적인 데이터 손실을 주기적으로 추적하는 것이 좋습니다. 지연 간격 추적은 각각의 주 데이터베이스 및 보조 데이터베이스에 대한 마지막 커밋 LSN 및 마지막 커밋 시간을 다음과 같이 비교합니다.  
  
1.  주 복제본에 연결합니다.  
  
2.  쿼리는 `last_commit_lsn` (마지막으로 커밋된 트랜잭션의 LSN) 및 `last_commit_time` (마지막 커밋의 시간) 열을 [sys.dm_hadr_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql) 동적 관리 뷰.  
  
3.  각각의 주 데이터베이스와 보조 데이터베이스에 대해 반환되는 값을 비교합니다. 마지막 커밋 LSN 간 차이는 지연 양을 나타냅니다.  
  
4.  데이터베이스 또는 데이터베이스 집합의 지연 양이 지정된 기간 동안 원하는 최대 지연을 초과할 때 알림을 트리거할 수 있습니다. 예를 들어, 각 주 데이터베이스에서 1분마다 실행되는 작업을 통해 쿼리를 실행할 수 있습니다. 작업이 실행된 마지막 시간 이후 주 데이터베이스와 보조 데이터베이스의 `last_commit_time` 간 차이가 RPO(복구 시간 목표)(예: 5분)를 초과하는 경우 작업에서 알림을 발생시킬 수 있습니다.  
  
> [!IMPORTANT]  
>  WSFC 클러스터에 쿼럼이 부족 하거나 쿼럼이 강제로 때 `last_commit_lsn` 고 `last_commit_time` null입니다. 쿼럼 강제 수행 후 데이터 손실을 방지하는 방법에 대한 자세한 내용은 [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
###  <a name="ForcedFailoverManagingDataLoss"></a> 잠재적 데이터 손실 관리  
 강제 장애 조치(failover) 후 모든 보조 데이터베이스가 일시 중지됩니다. 여기에는 이전 주 복제본이 다시 온라인 상태가 되고 이제 보조 복제본임을 확인한 후의 이전 주 데이터베이스가 포함됩니다. 각 보조 복제본에서 일시 중지된 각 데이터베이스를 개별적으로 수동 재개해야 합니다.  
  
 이전 주 복제본을 사용할 수 있게 되면 데이터베이스가 손상되지 않았다고 가정할 경우 잠재적 데이터 손실을 관리할 수 있습니다. 잠재적 데이터 손실을 관리하는 데 사용할 수 있는 방법은 원래 주 복제본이 새로운 주 복제본에 연결했는지 여부에 따라 달라집니다. 원래 주 복제본이 새로운 주 인스턴스에 액세스할 수 있다고 가정하면 자동으로 투명하게 다시 연결할 수 있습니다.  
  
#### <a name="the-original-primary-replica-has-reconnected"></a>원래 주 복제본이 다시 연결된 경우  
 일반적으로 실패 후에 원래 주 복제본이 다시 시작되면 신속하게 해당 파트너에 다시 연결합니다. 다시 연결할 때 원래 주 복제본은 보조 복제본이 됩니다. 해당 데이터베이스는 보조 데이터베이스가 되고 SUSPENDED 상태가 됩니다. 새로운 보조 데이터베이스는 재개하지 않으면 롤백되지 않습니다.  
  
 그러나 일시 중지된 데이터베이스에 액세스할 수 없으므로 데이터베이스를 검사하여 지정된 데이터베이스를 재개할 경우 손실될 데이터를 평가할 수 없습니다. 따라서 다음과 같이 데이터 손실을 감수할지 여부에 따라 보조 데이터베이스를 재개할지 또는 제거할지를 결정합니다.  
  
-   데이터 손실이 허용되지 않는 경우 가용성 그룹에서 데이터베이스를 제거하여 복원해야 합니다.  
  
     이제 데이터베이스 관리자는 이전 주 데이터베이스를 복구하여 손실된 데이터를 복구할 수 있습니다. 하지만 이전 주 데이터베이스가 온라인 상태가 되면 현재 주 데이터베이스에서 분기되므로, 데이터베이스 관리자는 제거된 데이터베이스 또는 현재 주 데이터베이스에 클라이언트가 액세스할 수 없도록 하여 데이터베이스의 추가 분기를 방지하고 클라이언트 장애 조치(Failover) 문제를 예방해야 합니다.  
  
-   비즈니스 목표에 따라 데이터 손실이 허용되는 경우 보조 데이터베이스를 재개할 수 있습니다.  
  
     새로운 보조 데이터베이스를 재개하면 데이터베이스 동기화의 첫 번째 단계로 해당 데이터베이스가 롤백됩니다. 실패 시 Send Queue에서 대기 중인 로그 레코드가 있으면 커밋된 경우에도 해당 트랜잭션이 손실됩니다.  
  
#### <a name="the-original-primary-replica-has-not-reconnected"></a>원래 주 복제본이 다시 연결되지 않은 경우  
 원래 주 복제본이 네트워크를 통해 새로운 주 복제본에 다시 연결하지 않도록 일시적으로 차단할 수 있으면 원래 주 데이터베이스를 검사하여 데이터베이스를 재개할 경우 손실될 데이터를 평가할 수 있습니다.  
  
-   잠재적 데이터 손실이 허용되는 경우  
  
     원래 주 복제본을 새로운 주 복제본에 다시 연결하도록 허용합니다. 다시 연결하면 새로운 보조 데이터베이스가 일시 중지됩니다. 데이터베이스에서 데이터 동기화를 시작하려면 데이터베이스를 재개하면 됩니다. 새로운 보조 복제본은 해당 데이터베이스에 대한 원래 복구 분기를 삭제하므로 이전 보조 복제본으로 보내거나 받지 않은 모든 트랜잭션이 손실됩니다.  
  
-   데이터 손실이 허용되지 않는 경우  
  
     일시 중지된 데이터베이스를 재개할 경우 손실될 중요한 데이터가 원래 주 데이터베이스에 들어 있으면 가용성 그룹에서 원래 주 데이터베이스를 제거하여 해당 데이터를 보존할 수 있습니다. 이렇게 하면 데이터베이스는 RESTORING 상태가 됩니다. 이 시점에서 제거된 데이터베이스의 비상 로그를 백업하는 것이 좋습니다. 그러면 원래 주 데이터베이스에서 복원하려는 데이터를 내보낸 후 현재 주 데이터베이스로 가져와서 현재 주 데이터베이스(이전 보조 데이터베이스)를 업데이트할 수 있습니다. 업데이트된 주 데이터베이스의 전체 데이터베이스 백업을 최대한 빨리 수행하는 것이 좋습니다.  
  
     그러면 새로운 보조 복제본을 호스팅하는 서버 인스턴스에서 RESTORE WITH NORECOVERY를 사용하여 이 백업(및 최소한 하나 이상의 후속 로그 백업)을 복원하여 일시 중지된 보조 데이터베이스를 삭제하고 새로운 보조 데이터베이스를 만들 수 있습니다. 해당 보조 데이터베이스를 재개할 때까지 현재 주 데이터베이스의 추가 로그 백업을 늦추는 것이 좋습니다.  
  
> [!WARNING]  
>  보조 데이터베이스 중 하나라도 일시 중지되어 있는 동안에는 주 데이터베이스에서 트랜잭션 로그 잘림이 지연됩니다. 또한 일시 중지된 상태로 남아 있는 로컬 데이터베이스가 있으면 동기 커밋 보조 복제본의 동기화 상태가 정상으로 전환될 수 없습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **장애 조치(Failover) 동작을 구성하려면**  
  
-   [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [자동 장애 조치에 대 한 상태 제어 유연한 장애 조치 정책 구성 &#40;AlwaysOn 가용성 그룹&#41;](configure-flexible-automatic-failover-policy.md)  
  
 **수동 장애 조치(Failover)를 수행하려면**  
  
-   [가용성 그룹의 계획된 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 장애 조치(Failover) 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹의 데이터베이스에 대한 로그인 및 작업 관리&#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **WSFC 쿼럼 구성을 구성하려면**  
  
-   [클러스터 쿼럼 NodeWeight 설정 구성](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)  
  
-   [클러스터 쿼럼 NodeWeight 설정 보기](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)  
  
-   [쿼럼 없이 WSFC 클러스터 강제 시작](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [Microsoft SQL Server AlwaysOn 솔루션 가이드 고가용성 및 재해 복구](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](http://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 모드 &#40;AlwaysOn 가용성 그룹&#41;](availability-modes-always-on-availability-groups.md)   
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [데이터베이스 간 트랜잭션 데이터베이스 미러링 또는 AlwaysOn 가용성 그룹에 대해 지원 되지 않습니다 &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md)   
 [장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [가용성 그룹 자동 장애 조치에 대한 유연한 장애 조치 정책&#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)  
  
  
