---
title: 분석 플랫폼 시스템의 고가용성 | Microsoft Docs
description: Analytics Platform System (APS)의 고가용성을 위해 구성 하는 방법에 대해 알아봅니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5c8a562ab105e1bc40b590916d0881757036aeff
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539593"
---
# <a name="analytics-platform-system-high-availability"></a>분석 플랫폼 시스템에 대 한 고가용성 정보
Analytics Platform System (APS)의 고가용성을 위해 구성 하는 방법에 대해 알아봅니다.  
  
## <a name="high-availability-architecture"></a>고가용성 아키텍처  
![어플라이언스 구조](media/appliance-architecture.png "어플라이언스 구조")  
  
## <a name="network"></a>네트워크  
네트워크, 가용성, APS 기기 두 개의 InfiniBand 네트워크에 있습니다. InfiniBand 네트워크 중 하나는 다운 되 면 다른 컨트롤러는 계속 사용할 수 있습니다. 또한 Active Directory가 올바른 InfiniBand 네트워크에 들어오는 요청을 해결 하려면 도메인 컨트롤러를 복제 합니다.  
  
자세한 내용은 참조 [구성 InfiniBand 네트워크 어댑터](configure-infiniband-network-adapters.md)합니다.  
  
## <a name="storage"></a>스토리지  
데이터를 안전 하 게 유지 하기 APS RAID 1 미러링 모든 사용자 데이터의 두 복사본을 유지 관리를 사용 합니다. 디스크 오류가 발생할 때 하드웨어 시스템 예비 디스크에 데이터를 다시 작성 하 고는 디스크 오류 경고를 설정 합니다.  
  
온라인을 사용할 수 있는 데이터를 유지 하려면 AP를 사용 하 여 Windows 저장소 공간 및 클러스터 된 공유 볼륨 직접 연결 된 저장소에서 사용자 데이터 디스크를 관리 합니다. 탑재 지점을 통해 계산 노드 호스트에 사용할 수 있는 클러스터 공유 볼륨으로 구성 하는 데이터 크기 단위 별로 저장소 풀 하나씩 있습니다.  
  
저장소 풀을 온라인 상태로 유지 되도록 데이터 배율 단위에 각 호스트에는 ISCSI 가상 컴퓨터를 장애 조치 되지 않습니다. 데이터는 여전히 데이터 배율 단위로 다른 호스트를 통해 액세스할 수, 한 호스트가 실패 하면이 아키텍처는 중요 합니다.  
  
## <a name="hosts"></a>호스트  
호스트 가용성에 대 한 모든 호스트를 Windows 장애 조치 클러스터로 구성 됩니다. 모든 랙 수동 호스트를 있습니다. 필요에 따라 SQL Server 병렬 데이터 웨어하우스 (PDW) 및 어플라이언스 패브릭을 제어 하는 첫 번째 랙 수동 두 번째 호스트를 가질 수 있습니다. 한 호스트가 실패 하면 장애 조치에 대해 구성 된 가상 컴퓨터는 장애 조치 수동 사용 가능한 호스트에 있습니다.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 노드와 기기 패브릭  
PDW 노드와 기기 패브릭의 고가용성을 위해 APS 가상화를 사용 합니다. 가상 컴퓨터에서 실행 될 때마다는 PDW 어플라이언스에 패브릭 구성 요소.  
  
각 가상 컴퓨터는 Windows 장애 조치 클러스터에서 역할로 정의 됩니다. 가상 컴퓨터에서 오류가 발생 하는 경우 클러스터 다시 사용할 수 있는 수동 호스트에서 시작 합니다. 가상 컴퓨터는 System Center Virtual Machine Manager를 사용 하 여 배포 됩니다. 장애 조치가 발생 하는 경우에 수동 호스트에서 실행 중인 가상 컴퓨터는 여전히 InfiniBand 네트워크를 통해 사용자 데이터에 액세스할 수 있습니다.  
  
컨트롤 노드와 계산 노드 가상 컴퓨터는 각각 단일 노드 클러스터로 구성 됩니다. 단일 노드 클러스터는 클러스터에서 항상 활성 InfiniBand IP를 사용 하도록를 클러스터 리소스로 InfiniBand 네트워크를 관리 합니다. 단일 노드 클러스터는 가상 컴퓨터 내에서 실행 되는 PDW 프로세스를 관리 합니다. 예를 들어 단일 노드 클러스터에 있는 SQL Server 및 데이터 이동 서비스 (DMS) 리소스 그룹으로 적절 한 순서로 이러한를 시작할 수 있도록 합니다. 제어 노드에 VM은 오케스트레이션 호스트에서 실행 되는 다른 Vm에 대 한 시작 순서를 제어 합니다.  
  
