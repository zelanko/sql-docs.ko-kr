---
title: Analytics Platform System의 고가용성 | Microsoft Docs
description: 고가용성을 위해 Analytics Platform System (APS)은 설계 하는 방법에 대해 알아봅니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5c8a562ab105e1bc40b590916d0881757036aeff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280352"
---
# <a name="analytics-platform-system-high-availability"></a>Analytics Platform System에 대 한 고가용성 정보
고가용성을 위해 Analytics Platform System (APS)은 설계 하는 방법에 대해 알아봅니다.  
  
## <a name="high-availability-architecture"></a>고가용성 아키텍처  
![어플라이언스 아키텍처](media/appliance-architecture.png "어플라이언스 아키텍처")  
  
## <a name="network"></a>네트워크  
APS 어플라이언스는 네트워크 가용성에 대 한 두 개의 InfiniBand 네트워크에 있습니다. InfiniBand 네트워크 중 하나 다운 되 면 다른 하나는 계속 사용할 수 있습니다. 또한 Active Directory가 올바른 InfiniBand 네트워크에 들어오는 요청을 해결 하려면 도메인 컨트롤러를 복제 합니다.  
  
자세한 내용은 [구성 InfiniBand 네트워크 어댑터](configure-infiniband-network-adapters.md)합니다.  
  
## <a name="storage"></a>스토리지  
데이터를 안전 하 게 유지, AP RAID 1 미러링 모든 사용자 데이터의 두 복사본을 유지 하려면 사용 합니다. 디스크에 오류가 발생 하는 경우 하드웨어 시스템 예비 디스크에 데이터를 다시 작성 하 고 디스크 오류가 발생 하는 경고를 설정 합니다.  
  
온라인을 사용할 수 있는 데이터를 유지 하려면 AP를 사용 하 여 Windows 저장소 공간 및 클러스터 된 공유 볼륨 직접 연결 된 저장소에서 사용자 데이터 디스크를 관리 합니다. 클러스터 공유 볼륨 탑재 지점을 통해 계산 노드 호스트에 사용할 수 있는 구조로 데이터 규모 단위당 저장소 풀 하나씩 있습니다.  
  
저장소 풀을 온라인 상태로 유지 되도록 데이터 배율 단위에서 각 호스트에는 장애 조치 하지 않습니다 하는 ISCSI 가상 머신입니다. 이 아키텍처는 호스트가 실패 하는 경우 데이터는 여전히 데이터 배율 단위에서 다른 호스트를 통해 액세스할 수 있으므로 중요 합니다.  
  
## <a name="hosts"></a>호스트  
호스트 가용성에 대 한 모든 호스트를 Windows 장애 조치 클러스터로 구성 됩니다. 모든 랙 수동 호스트를 있습니다. 필요에 따라 SQL Server 병렬 데이터 웨어하우스 (PDW) 및 어플라이언스 패브릭을 제어 하는 첫 번째 랙, 두 번째 수동 호스트를 가질 수 있습니다. 호스트 실패 하면 장애 조치에 대해 구성 된 가상 컴퓨터 장애 조치 됩니다 수동 호스트로 사용할 수 있습니다.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 노드 및 어플라이언스 패브릭  
PDW 노드 및 어플라이언스 패브릭의 고가용성을 위해 AP 가상화를 사용합니다. PDW 및 어플라이언스 패브릭 구성 요소는 각 가상 컴퓨터에서 실행 합니다.  
  
각 가상 컴퓨터는 Windows 장애 조치 클러스터에서 역할로 정의 됩니다. 가상 컴퓨터가 실패 하는 경우 클러스터 다시 사용할 수 있는 수동 호스트에서 시작 합니다. 가상 컴퓨터는 System Center Virtual Machine Manager 사용 하 여 배포 됩니다. 장애 조치가 발생 하는 경우 수동 호스트에서 실행 중인 가상 컴퓨터는 InfiniBand 네트워크를 통해 사용자 데이터에 액세스할 수 있습니다.  
  
제어 노드와 계산 노드 가상 컴퓨터는 각각 단일 노드 클러스터로 구성 됩니다. 단일 노드 클러스터는 클러스터는 항상 활성 InfiniBand IP를 사용 하도록 클러스터 리소스로 InfiniBand 네트워크를 관리 합니다. 단일 노드 클러스터는 가상 머신 내에서 실행 되는 PDW 프로세스를 관리 합니다. 예를 들어, 단일 노드 클러스터에 SQL Server 및 데이터 이동 서비스 (DMS) 리소스로 적절 한 순서로 이러한를 시작할 수 있도록 합니다. 제어 노드 VM 시작 순서 오케스트레이션 호스트에서 실행 되는 다른 Vm에 대 한 제어 합니다.  
  
