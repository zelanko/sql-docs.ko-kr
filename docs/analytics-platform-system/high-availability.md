---
title: 고가용성
description: 고가용성을 위해 AP (Analytics Platform System)를 설계 하는 방법에 대해 알아봅니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6246ed25909a2e366d8bbafcd912a4fd923cc84a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401099"
---
# <a name="analytics-platform-system-high-availability"></a>분석 플랫폼 시스템 고가용성
고가용성을 위해 AP (Analytics Platform System)를 설계 하는 방법에 대해 알아봅니다.  
  
## <a name="high-availability-architecture"></a>고가용성 아키텍처  
![어플라이언스 아키텍처](media/appliance-architecture.png "어플라이언스 아키텍처")  
  
## <a name="network"></a>네트워크  
네트워크 가용성을 위해 APS 어플라이언스는 두 개의 InfiniBand 네트워크를 포함 합니다. InfiniBand 네트워크 중 하나가 중단 되 면 다른 네트워크를 계속 사용할 수 있습니다. 또한 Active Directory는 도메인 컨트롤러를 복제 하 여 들어오는 요청을 올바른 InfiniBand 네트워크로 확인 했습니다.  
  
자세한 내용은 [Configure InfiniBand network 어댑터](configure-infiniband-network-adapters.md)항목을 참조 하세요.  
  
## <a name="storage"></a>스토리지  
데이터를 안전 하 게 유지 하기 위해 AP는 RAID 1 미러링을 사용 하 여 모든 사용자 데이터의 두 복사본을 유지 합니다. 디스크에 오류가 발생 하면 하드웨어 시스템은 데이터를 예비 디스크에 다시 작성 하 고 디스크 오류가 있음을 경고를 설정 합니다.  
  
데이터를 온라인으로 사용할 수 있도록 하기 위해 APS는 Windows 저장소 공간 및 클러스터 된 공유 볼륨을 사용 하 여 직접 연결 된 저장소의 사용자 데이터 디스크를 관리 합니다. 클러스터 공유 볼륨으로 구성 된 데이터 크기 조정 단위 당 하나의 저장소 풀이 탑재 위치를 통해 계산 노드 호스트에서 사용 가능 합니다.  
  
저장소 풀이 온라인 상태를 유지 하도록 하기 위해 데이터 배율 단위의 각 호스트에는 장애 조치 (failover) 되지 않는 ISCSI 가상 머신이 있습니다. 이 아키텍처는 호스트에 오류가 발생 하는 경우 데이터 배율 단위의 다른 호스트를 통해 데이터에 계속 액세스할 수 있으므로 중요 합니다.  
  
## <a name="hosts"></a>호스트  
호스트 가용성의 경우 모든 호스트가 Windows 장애 조치 (Failover) 클러스터로 구성 됩니다. 모든 랙에는 수동 호스트가 있습니다. 필요에 따라 PDW (병렬 데이터 웨어하우스) 및 어플라이언스 패브릭을 SQL Server 제어 하는 첫 번째 랙에는 두 번째 수동 호스트가 있을 수 있습니다. 호스트에서 오류가 발생 하는 경우 장애 조치 (failover)를 위해 구성 된 가상 컴퓨터는 사용 가능한 수동 호스트로 장애 조치 (failover) 됩니다.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 노드 및 어플라이언스 패브릭  
PDW 노드 및 어플라이언스 패브릭의 고가용성을 위해 APS는 가상화를 사용 합니다. 각 PDW 및 어플라이언스 패브릭 구성 요소는 가상 머신에서 실행 됩니다.  
  
각 가상 머신은 Windows 장애 조치 (failover) 클러스터에서 역할로 정의 됩니다. 가상 컴퓨터에 오류가 발생 하면 클러스터는 사용 가능한 수동 호스트에서 해당 가상 컴퓨터를 다시 시작 합니다. 가상 머신은 System Center Virtual Machine Manager를 사용 하 여 배포 됩니다. 장애 조치 (failover)가 발생 하면 수동 호스트에서 실행 되는 가상 머신은 여전히 InfiniBand 네트워크를 통해 해당 사용자 데이터에 액세스할 수 있습니다.  
  
제어 노드와 계산 노드 가상 머신은 각각 단일 노드 클러스터로 구성 됩니다. 단일 노드 클러스터는 클러스터가 항상 활성 InfiniBand IP를 사용 하 고 있는지 확인 하기 위해 InfiniBand 네트워크를 클러스터 리소스로 관리 합니다. 단일 노드 클러스터는 가상 머신 내에서 실행 되는 PDW 프로세스를 관리 합니다. 예를 들어 단일 노드 클러스터는 적절 한 순서로 시작할 수 있도록 DMS (데이터 이동 서비스)를 리소스로 SQL Server 합니다. 또한 제어 노드 VM은 오케스트레이션 호스트에서 실행 되는 다른 Vm의 시작 순서를 제어 합니다.  
  
