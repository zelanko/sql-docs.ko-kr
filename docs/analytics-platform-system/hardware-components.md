---
title: 분석 플랫폼 시스템 하드웨어 구성 요소
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Analytics Platform System (APS) 비즈니스 요구 사항에 따라 적절 한 양의 처리 및 저장소를 구입할 수 있도록 확장 가능한 구성 요소를 사용 합니다.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: aa1cdcc7-cfee-4658-bbce-7d319bfb7483
caps.latest.revision: 17
ms.openlocfilehash: 4b972c4b926463a67588c4ee41ed0157da7cdc80
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="analytics-platform-system-hardware-components"></a>분석 플랫폼 시스템 하드웨어 구성 요소

Analytics Platform System (APS) 비즈니스 요구 사항에 따라 적절 한 양의 처리 및 저장소를 구입할 수 있도록 확장 가능한 구성 요소를 사용 합니다. APS을 주문할 때 이러한 핵심 하드웨어 구성 요소 조합을 해야 합니다. 특정 하드웨어 공급 업체 다른 명명 규칙을 사용 하거나 추가 구성 요소가 필요.  
 
  
## <a name="rackandnetwork"></a>랙 및 네트워크 
 
APS 구성 요소는 모든 데이터 센터에 맞는 하나 이상의 선반에 저장 됩니다. 각 랙의 전원 pdu (배전), 두 개의 InfiniBand 스위치 및 두 개의 이더넷 스위치를 함께 제공 됩니다.  
  
![랙 및 네트워크](media/rack-and-network.png "APS 랙 및 네트워크")  
  
## <a name="datascaleunit"></a>데이터 배율 단위
 
데이터 배율 단위 데이터 호스트 및 사용자 데이터 처리 및 저장에 대 한 직접 연결된 저장소 DAS ()를 포함 합니다. 용량을 추가 하려면 하드웨어 공급 업체에서 지원 되는 구성 기준으로 데이터 단위를 추가 합니다. 데이터 확장 단위 수가 늘어나면 추가 랙 추가 해야 및 추가 샘플을 제공할 필요에 따라 네트워크 구성 요소, 전원, 네트워크 및 인프라를 랙 합니다.  
  
### <a name="data-host"></a>데이터 호스트  

데이터 호스트는 전용 사용자 데이터를 처리 하는 서버. 병렬 데이터 웨어하우스 (PDW) 각 데이터 호스트에서 계산 노드 하나를 실행합니다. HPE 어플라이언스에 대 한 데이터 배율 단위는 데이터는 두 명의 호스트에 있습니다. Dell 및 퀀텀 어플라이언스에 대 한 데이터 배율 단위에 세 명의 데이터 호스트가 있습니다.  
  
### <a name="direct-attached-storage"></a>직접 연결된 저장소
 
직접 연결된 저장소 DAS ()은 데이터 호스트에 연결 된 디스크의 풀입니다. 데이터 호스트의 모든 디스크에 액세스할 수 있습니다. 공유 없는의 일환으로 개별 디스크 아키텍처를 데이터 호스트에서 실행 되는 계산 노드를 공유 하지 않습니다. 그러나 고가용성을 위해 저장소 액세스 공유 및 각 데이터 호스트 디스크에 액세스할 수 있습니다.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>데이터 배율 단위 아키텍처-DELL 및 퀀텀
  
![확장성 단위](media/scalability-unit-dell.png "Dell 확장성 단위")  
  
### <a name="data-scale-unit-architecture---hpe"></a>데이터 배율 단위 아키텍처 HPE 
 
![HPE 확장성 단위](media/scalability-unit-hpe.png "HPE 확장성 단위")  
  
### <a name="data-scale-unit-description"></a>데이터 배율 단위 설명

데이터 배율 단위 각 계산 노드 및와 연결 된 SAS (Serial SCSI) 연결 되어 있는 한 직접 연결 된 디스크 배열에 대해 하나의 서버 (호스트)에 있습니다. 캐비닛 저장소 내에서 디스크 배열 중복 전원 공급 장치를 포함 하는 반으로 구분 됩니다. Windows Server 저장소 공간 RAID 1 미러링 디스크 쌍 간에 데이터를 복제 하 여 사용자 데이터를 관리 합니다. 각 디스크 쌍의 디스크는 디스크 배열의 서로 다른 키에 저장 됩니다.  
  
디스크 배열의 핫 스패어 디스크와 시스템 디스크에도 포함 됩니다. 디스크 오류가 발생할 경우 저장소 공간 데이터의 좋은 복사본 작동 디스크에서 사용 하 여 핫 스패어에 데이터의 중복 복사본을 다시 작성 합니다. 데이터 손실을 방지 하는 데 도움이 되는 중요 한 자동 복구 기능입니다.  
  
컴퓨터 노드에 대 한 디스크의 총 수:  
  
-   DELL 디스크가 96 = (3 서버) * (서버 당 16 개의 디스크) \* (중복 디스크에 대 한 2).  
  
-   HPE가 64 개의 디스크 (서버 2) = * (서버 당 16 개의 디스크) \* (중복 디스크에 대 한 2).  
  
-   또한 각 디스크 배열에는 핫 스패어 디스크와 시스템 디스크에 있습니다.  
  
**고가용성을 위해**올려 노드가 실패 하면 계산 작동 하는 데이터 배율 단위에서 다른 호스트를 통해 사용자 데이터에 액세스할 수 있는 경우, 합니다. 직접 연결 된 실제 호스트 중 하나 이상을 작동 해야 하거나 저장소에 대 한 데이터 액세스가 손실 합니다.  
  
**디스크 크기에 대 한**, 직접 연결된 저장소는 1, 2 또는 3 테라바이트 디스크 드라이브에 있을 수 있습니다. 모든 데이터 배율 단위에 같은 크기의 디스크가 있어야 합니다.  
  
## <a name="basescaleunit"></a>기본 배율 단위 
 
기본 배율 단위 뇌 전원 호스트, 데이터 호스트 및 직접 연결 된 저장소 어플라이언스에 필요한 최소 수를 포함 합니다. 이러한 구성 요소를 포함 합니다.  
  
### <a name="orchestration-host"></a>오케스트레이션 호스트  
이 서버는 PDW 브레인을 실행합니다.
  
### <a name="passive-host"></a>수동 호스트  
이 서버는 고가용성을 제공합니다. 온라인 및 오케스트레이션 또는 데이터 호스트에 오류가 발생 하는 경우 작업을 실행할 준비가있지 않습니다. 오케스트레이션 호스트, 수동 호스트 및 데이터 배율 단위 서버는 Windows 장애 조치 클러스터로 구성 됩니다. 각 랙 기기에서 수동 호스트를 하나 필요합니다.  
  
### <a name="optional-passive-host"></a>선택적 수동 호스트  
중복성을 강화를 위해 두 번째 수동 호스트 하는 기본 배율 단위를 추가 하려면 옵션도 있습니다.  
  
### <a name="data-scale-unit"></a>데이터 배율 단위  
기본 배율 단위를 랙의 맨 아래에 배치 되는 하나의 데이터 배율 단위에 포함 됩니다.  
  
이 다이어그램에서는 기본 배율 단위와 랙 및 네트워크를 보여 줍니다. 이것이 분석 플랫폼 시스템 어플라이언스에 대 한 최소 구성을 적용 합니다.  
  
![기본 배율 단위](media/base-scale-unit.png "기본 배율 단위")  
 
