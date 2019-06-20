---
title: 하드웨어 구성 요소-Analytics Platform System | Microsoft Docs
description: Analytics Platform System (APS) 비즈니스 요구 사항에 따라 적절 한 양의 처리 및 저장소를 구매할 수 있도록 확장 가능한 구성 요소를 사용 합니다. AP를 주문할 때 이러한 핵심 하드웨어 구성 요소 조합을 해야 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8cf7fd100f72e14b09ea086a1ebff5140a9068a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157421"
---
# <a name="hardware-components-for-analytics-platform-system"></a>Analytics Platform System에 대 한 하드웨어 구성 요소

Analytics Platform System (APS) 비즈니스 요구 사항에 따라 적절 한 양의 처리 및 저장소를 구매할 수 있도록 확장 가능한 구성 요소를 사용 합니다. AP를 주문할 때 이러한 핵심 하드웨어 구성 요소 조합을 해야 합니다. 특정 하드웨어 공급 업체는 다른 명명 규칙을 사용 하거나 추가 구성 요소를 수 있습니다.  
 
  
## <a name="rackandnetwork"></a>랙 및 네트워크 
 
AP 구성 요소는 모든 데이터 센터에 속하는 하나 이상의 랙에 저장 됩니다. 각 랙 전원 분배 장치 (Pdu), 두 개의 InfiniBand 스위치 및 두 개의 이더넷 스위치를 사용 하 여 제공 됩니다.  
  
![랙 및 네트워크](media/rack-and-network.png "APS 랙 및 네트워크")  
  
## <a name="datascaleunit"></a>데이터 배율 단위
 
데이터 배율 단위는 데이터 호스트 및 사용자 데이터를 저장 및 처리에 대 한 직접 연결된 저장소 DAS ()를 포함 합니다. 용량을 추가 하려면 하드웨어 공급 업체에서 지원 되는 구성에 따라 데이터 배율 단위 추가할 수 있습니다. 데이터 확장 단위 수가 증가 함에 따라 추가 랙을 추가 해야 & 자세히 제공 하는 데 필요한 네트워크 구성 요소, 전원, 네트워크 및 인프라를 랙입니다.  
  
### <a name="data-host"></a>데이터 호스트  

데이터 호스트는 사용자 데이터를 처리 하도록 전담 하는 서버. 병렬 데이터 웨어하우스 (PDW)에 각 데이터 호스트에서 하나의 계산 노드에서 실행 됩니다. HPE 장비를 위한 데이터 배율 단위에 두 명의 데이터 호스트 Dell과 퀀텀 장비를 위한 데이터 배율 단위에는 세 가지 데이터 호스트  
  
### <a name="direct-attached-storage"></a>직접 연결된 저장소
 
직접 연결된 저장소 DAS ()는 데이터 호스트에 연결 된 디스크의 풀입니다. 모든 데이터 호스트 디스크는 액세스할 수 있습니다. 공유 되지 않은의 일부로 아키텍처, 계산 노드 데이터 호스트에서 실행 되는 개별 디스크를 공유 하지 않습니다. 그러나 고가용성을 위해 저장소 액세스를 공유 하 고 데이터 호스트의 각 디스크에 액세스할 수 있습니다.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>데이터 크기 조정 단위 아키텍처-DELL과 퀀텀
  
![확장성 단위](media/scalability-unit-dell.png "Dell 확장성 단위")  
  
### <a name="data-scale-unit-architecture---hpe"></a>데이터 크기 조정 단위 아키텍처-HPE 
 
![HPE 확장성 단위](media/scalability-unit-hpe.png "HPE 확장성 단위")  
  
### <a name="data-scale-unit-description"></a>데이터 크기 조정 단위 설명

데이터 배율 단위는 각 Compute 노드를 사용 하 여 연결 된 SCSI (SAS (Serial) 연결 된 하나의 직접 연결 된 디스크 배열 (호스트) 서버를 하나에 있습니다. 캐비닛 저장소 디스크 배열 중복 전원 공급 장치를 포함 하는 반으로 구분 됩니다. Windows Server 저장소 공간 RAID 1 미러링 디스크 쌍에 걸쳐 데이터를 복제 하 여 사용자 데이터를 관리 합니다. 각 디스크 쌍의 디스크는 디스크 배열의 다른 절반에 저장 됩니다.  
  
디스크 배열에는 또한 핫 스패어 디스크 및 시스템 디스크를 포함합니다. 디스크에 오류가 발생 하는 경우 저장소 공간 데이터의 복사본을 작동 디스크에 사용 하 여 핫 스패어에 있는 데이터의 중복 복사본을 다시 빌드합니다. 이 데이터 손실을 방지 하는 데 도움을 주는 중요 한 자동 복구 기능입니다.  
  
계산 노드에 대 한 디스크의 총 수:  
  
-   DELL 디스크가 96 = (서버 3 개) * (서버당 16 개 디스크) \* (중복 디스크에 대 한 2).  
  
-   HPE가 64 개의 디스크 (서버 2) = * (서버당 16 개 디스크) \* (중복 디스크에 대 한 2).  
  
-   또한 각 디스크 배열에 핫 스패어 디스크와 시스템 디스크에 있습니다.  
  
**고가용성을 위해**계산 노드 장애 조치 하는 경우 작동 하 고 데이터 배율 단위에서 다른 호스트를 통해 사용자 데이터에 액세스할 수 있습니다. 직접 연결 된 실제 호스트 중 하나 이상이 작동 해야 합니다 또는 저장소에 대 한 데이터 액세스가 손실 됩니다.  
  
**디스크 크기에 대 한**, 직접 연결 된 저장소는 1, 2 또는 3 테라바이트 디스크 드라이브에 있을 수 있습니다. 모든 데이터 배율 단위에는 동일한 크기의 디스크가 있어야 합니다.  
  
## <a name="basescaleunit"></a>기본 배율 단위 
 
기본 배율 단위 뇌 power 호스트, 데이터 호스트 및 필요한 어플라이언스에 대 한 직접 연결 된 저장소의 최소 수를 포함 합니다. 다음 구성 요소가 포함 됩니다. 
  
### <a name="orchestration-host"></a>오케스트레이션 호스트  
이 서버는 PDW의 중추를 실행합니다.
  
### <a name="passive-host"></a>수동 호스트  
이 서버는 고가용성을 제공합니다. 것이 온라인 상태이 고 오케스트레이션 또는 데이터 호스트에 오류가 발생 하는 경우 작업을 실행 하도록 준비 합니다. 오케스트레이션 호스트, 수동 호스트 및 데이터 규모 단위 서버는 Windows 장애 조치 클러스터로 구성 됩니다. 각 랙 어플라이언스에서 수동 호스트를 하나 필요합니다.  
  
### <a name="optional-passive-host"></a>선택적 수동 호스트  
중복성을 추가 하려면 기본 배율 단위에 두 번째 수동 호스트를 추가 하는 옵션을 해야 합니다.  
  
### <a name="data-scale-unit"></a>데이터 배율 단위  
기본 배율 단위는 랙의 맨 아래에 배치 되는 하나의 데이터 배율 단위를 포함 합니다.  
  
이 다이어그램에서는 기본 배율 단위, 랙 및 네트워크를 보여 줍니다. 이 Analytics Platform System appliance에 대 한 최소 구성입니다.  
  
![기본 배율 단위](media/base-scale-unit.png "기본 배율 단위")  
 
