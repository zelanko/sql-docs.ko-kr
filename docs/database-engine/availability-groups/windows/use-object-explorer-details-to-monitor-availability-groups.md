---
title: 개체 탐색기 정보를 사용하여 가용성 그룹 모니터링 | Microsoft Docs
description: SQL Server Management Studio를 사용하여 기존 Always On 가용성 그룹, 가용성 복제본 및 가용성 데이터베이스를 모니터링하고 관리하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.OEdetails.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: 84affc47-40e0-43d9-855e-468967068c35
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e7ee1430cd764c02c05f2bf3f8f935d397a6155a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894165"
---
# <a name="use-object-explorer-details-to-monitor-availability-groups"></a>개체 탐색기 정보를 사용하여 가용성 그룹 모니터링
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 **의** 개체 탐색기 정보 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 창을 사용하여 기존 Always On 가용성 그룹, 가용성 복제본 및 가용성 데이터베이스를 모니터링하고 관리하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  개체 탐색기 정보 창을 사용하는 방법은 [개체 탐색기 정보 창](../../../ssms/object/object-explorer-details-pane.md)을 참조하세요.  
  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
 주 복제본 또는 보조 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스(서버 인스턴스)에 연결해야 합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹, 가용성 복제본 및 가용성 데이터베이스를 모니터링하려면**  
  
1.  보기 메뉴에서 **개체 탐색기 정보**를 클릭하거나 **F7** 키를 누릅니다.  
  
2.  개체 탐색기에서 가용성 그룹을 모니터링할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 연결하고 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
3.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
4.  **개체 탐색기 정보** 창에 연결된 서버 인스턴스에서 복제본을 호스팅하는 모든 가용성 그룹이 표시됩니다. 각 가용성 그룹에 대해 **서버 인스턴스(기본)** 열에 주 복제본을 현재 호스트 중인 서버 인스턴스의 이름이 표시됩니다.  지정된 가용성 그룹에 대한 자세한 정보를 표시하려면 개체 탐색기에서 해당 가용성 그룹을 선택합니다.  
  
5.  그러면 **개체 탐색기 정보** 창에 이 가용성 그룹에 대한 **가용성 복제본** 및 **가용성 데이터베이스** 노드가 표시됩니다.  
  
    -   개체 탐색기에서 **가용성 그룹** 노드를 확장하고 **가용성 복제본** 노드를 선택하면 **개체 탐색기 정보** 창에 그룹의 각 가용성 복제본에 대한 정보가 표시됩니다. 자세한 내용은 이 항목 뒷부분에 나오는 [가용성 복제본 정보](#AvReplicaDetails)를 참조하세요.  
  
         여러 가용성 복제본에 대해 작업을 수행하려면 원하는 가용성 복제본을 선택한 후 마우스 오른쪽 단추로 클릭하여 사용 가능한 명령을 나열하는 상황에 맞는 메뉴를 엽니다.  
  
    -   개체 탐색기에서 **가용성 그룹** 노드를 확장하고 **가용성 데이터베이스** 노드를 선택하면 **개체 탐색기 정보** 창에 그룹에 있는 각 가용성 데이터베이스에 대한 정보가 표시됩니다. 자세한 내용은 이 항목 뒷부분의 [가용성 데이터베이스 정보](#AvDbDetails)를 참조하세요.  
  
         여러 가용성 데이터베이스에 대해 작업을 수행하려면 원하는 가용성 데이터베이스를 선택한 후 마우스 오른쪽 단추로 클릭하여 사용 가능한 명령을 나열하는 상황에 맞는 메뉴를 엽니다.  
  
##  <a name="availability-groups-details"></a><a name="AvGroupsDetails"></a> 가용성 그룹 정보  
 **가용성 그룹** 정보 화면에 다음 열이 표시됩니다.  
  
 **이름**  
 선택한 가용성 그룹의 **가용성 복제본**, **가용성 데이터베이스**및 **가용성 그룹** 수신기 폴더를 나열합니다.  
  
##  <a name="availability-replica-details"></a><a name="AvReplicaDetails"></a> 가용성 복제본 정보  
 **가용성 복제본** 정보 화면에 다음 열이 표시됩니다.  
  
 **서버 인스턴스**  
 가용성 복제본을 호스팅하는 서버 인스턴스 이름을 로컬 서버 인스턴스에 대한 서버 인스턴스의 현재 연결 상태를 나타내는 아이콘과 함께 표시합니다.  
  
 **역할**  
 가용성 복제본의 현재 역할( **주** 또는 **보조**)을 나타냅니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 역할에 대한 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
 **보조 역할의 연결 모드**  
 보조 역할, 즉 보조 복제본의 역할을 수행하는 지정된 가용성 복제본의 데이터베이스에서 클라이언트의 연결을 허용할 수 있는지 여부를 나타냅니다.  
  
 가능한 값은 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**연결 허용 안 함**|이 가용성 복제본이 보조 복제본 역할을 하는 동안 가용성 데이터베이스에 직접 연결할 수 없습니다. 보조 데이터베이스를 읽기 액세스에 사용할 수 없습니다.|  
|**읽기 전용 연결만 허용**|이 복제본이 보조 복제본 역할을 하는 경우 직접 읽기 전용 연결만 허용됩니다. 복제본의 모든 데이터베이스에 대한 읽기 액세스가 가능합니다.|  
|**모든 연결 허용**|이 복제본이 보조 복제본 역할을 하는 동안 읽기 전용 액세스를 위한 모든 데이터베이스 연결이 허용됩니다.|  
  
 **연결 상태**  
 보조 복제본이 주 복제본에 현재 연결되어 있는지 여부를 나타냅니다. 가능한 값은 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**연결 끊김**|원격 가용성 복제본의 경우 로컬 가용성 복제본에서 연결이 끊어져 있는지를 나타냅니다. 연결이 끊긴 상태에 대한 로컬 복제본의 응답은 역할별로 다음과 같이 다릅니다.<br /><br /> 주 복제본에서 보조 복제본의 연결이 끊어지면 보조 데이터베이스는 주 복제본에 **동기화되지 않음** 으로 표시되고 주 복제본은 보조 복제본이 다시 연결될 때까지 기다립니다.<br /><br /> 보조 복제본에서 보조 복제본의 연결이 끊어지면 보조 복제본은 주 복제본에 다시 연결하려고 시도합니다.|  
|**연결됨**|로컬 복제본에 현재 연결되어 있는 원격 가용성 복제본입니다.|  
|**NULL**|로컬 복제본이 보조 복제본인 경우 이 값은 다른 보조 복제본에 대해 NULL입니다.|  
  
 **동기화 상태**  
 보조 복제본이 주 복제본에 현재 동기화되어 있는지 여부를 나타냅니다. 가능한 값은 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**동기화되지 않음**|데이터베이스가 동기화되지 않았거나 가용성 그룹에 아직 조인되지 않았습니다.|  
|**동기화됨**|데이터베이스가 현재 주 복제본 또는 마지막 주 복제본(있는 경우)의 주 데이터베이스와 동기화되어 있습니다.<br /><br /> 참고: 성능 모드에서는 데이터베이스가 절대 Synchronized 상태로 되지 않습니다.|  
|**NULL**|알 수 없는 상태입니다. 이 값은 로컬 서버 인스턴스가 WSFC 장애 조치(Failover) 클러스터와 통신할 수 없는 경우(즉, 로컬 노드가 WSFC 쿼럼의 일부가 아닌 경우)에 발생합니다.|  
  
> [!NOTE]  
>  가용성 복제본의 성능 카운터에 대한 자세한 내용은 [SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)을 참조하세요.  
  
##  <a name="availability-database-details"></a><a name="AvDbDetails"></a> 가용성 데이터베이스 정보  
 **가용성 데이터베이스** 정보 화면에는 지정된 가용성 그룹의 다음 가용성 데이터베이스 속성이 표시됩니다.  
  
 **이름**  
 가용성 데이터베이스의 이름입니다.  
  
 **동기화 상태**  
 가용성 데이터베이스가 주 복제본에 현재 동기화되어 있는지 여부를 나타냅니다.  
  
 가능한 동기화 상태는 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|동기화 중|보조 데이터베이스가 디스크에 아직 기록(확정)되지 않은 주 데이터베이스에 대한 트랜잭션 로그 기록을 수신했습니다.<br /><br /> 참고: 비동기 커밋 모드에서 동기화 상태는 항상 **동기화 중**입니다.|  
|||  
  
 **일시 중지됨**  
 가용성 데이터베이스가 현재 온라인 상태인지 여부를 나타냅니다. 가능한 값은 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**일시 중지됨**|이 상태는 데이터베이스를 로컬로 일시 중지하여 수동으로 다시 시작해야 함을 나타냅니다.<br /><br /> 주 복제본에서 보조 데이터베이스에 대한 값을 읽을 수 없습니다. 보조 데이터베이스가 일시 중지되었는지 여부를 안정적으로 결정하려면 데이터베이스를 호스팅하는 보조 복제본에서 보조 데이터베이스를 쿼리합니다.|  
|**조인되지 않음**|보조 데이터베이스가 가용성 그룹에 조인되지 않았거나 그룹에서 제거되었음을 나타냅니다.|  
|**온라인**|데이터베이스가 로컬 가용성 복제본에서 일시 중지되지 않고 연결되어 있음을 나타냅니다.|  
|**연결되지 않음**|보조 복제본이 주 복제본에 현재 연결할 수 없음을 나타냅니다.|  
  
> [!NOTE]  
>  가용성 데이터베이스의 성능 카운터에 대한 자세한 내용은 [SQL Server, 데이터베이스 복제본](../../../relational-databases/performance-monitor/sql-server-database-replica.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sys.dm_os_performance_counters&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)   
 [가용성 그룹 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)   
 [가용성 복제본 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
  
