---
title: 어플라이언스 물리적 구성 요소-분석 플랫폼 시스템 | Microsoft Docs
description: 이름 및 PDW 및 어플라이언스 패브릭 물리적 구성 요소에 대 한 설명입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0adbd92d1a29a98a80de65268c53ea63e3941d07
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538883"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>어플라이언스 물리적 구성 요소-분석 플랫폼 시스템
이름 및 PDW 및 어플라이언스 패브릭 물리적 구성 요소에 대 한 설명입니다. 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>구성 요소 다이어그램  
물리적 구성 요소와 6 계산 노드 어플라이언스의 첫 번째 랙에 있는 위치 이름을 표시 합니다.  
  
![PDW 영역 구성 요소 이름-HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
PDW 구성 요소에 대 한 실제 이름은 PDW 영역 이름, 대시, 다음 구성 요소 이름에 밑줄입니다. 예를 들어 PDW 영역 이름이 PDW123 경우 실제 이름을 **PDW123 CTL01**, **PDW123-c m p 01**등입니다.  
  
마찬가지로, 기기 패브릭 구성 요소에 대 한 실제 이름 뒤에 구성 요소 이름 뒤에 대시를 기기 도메인 됩니다. 예를 들어 기기 도메인이 FSW123 이면 기기 패브릭 Vm은 **FSW123 WDS**, **FSW123 AD01**, **FSW123 VMM**등입니다.  
  
다음은 계산 노드가 6 개인 있는 PDW 영역의 통합된 보기입니다.  
  
![PDW 구성 요소 이름](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW 구성 요소  
PDW 가상 컴퓨터는 PDW 영역의 일부입니다.  
  
*PDW_region*-CTL01  
제어 노드를 실행 하는 가상 컴퓨터 이렇게 HST01에서 실행 되 고 HST02을 장애 조치할 수 있습니다.  
  
> [!WARNING]  
> SQL Server PDW Hyper-v 관리자를 사용 하 여 CTL01 가상 컴퓨터의 스냅숏 만들기를 지원 하지 않습니다. 스냅숏 가상 컴퓨터 장애 조치를 백업 하려고 할 경우 오류가 발생할 수 있는 로컬 저장소에 의존 합니다. 스냅숏 만들기도 문제가 발생할 수 있습니다 안정성 다른 VM의 수동 서버로 해당 장애 조치 합니다.  
  
*PDW_region*-c m p 01을 통해 *PDW_Region*-CMP06  
계산 노드를 실행 하는 가상 컴퓨터 이 6 계산 노드 다이어그램에서 HSA06 실행을 통해 호스트 HSA01 각각 CMP06 통해 Vm c m p 01 노드를 계산 합니다.  
  
## <a name="fabric"></a>어플라이언스 패브릭 구성 요소  
이러한 구성 요소는 기기 패브릭의 일부입니다.  
  
### <a name="virtual-machines"></a>가상 컴퓨터  
*appliance_domain*-WDS  
이 가상 컴퓨터 호스트 배포 WDS (Windows 서비스), 분석 플랫폼 시스템을 사용 하는 어플라이언스 네트워크를 통해 Windows 운영 체제를 배포 합니다. 또한 DHCP 서비스를 통해 미리 구성 된 IP 주소를 사용 하지 않고도 어플라이언스 네트워크를 연결할 기기 호스트를 호스트 합니다.  
  
*appliance_domain*-WDS 가상 컴퓨터 HST01에서 실행 되 고 HST02을 장애 조치할 수 있습니다. WDS 가상 컴퓨터 및 VMM 가상 컴퓨터로 어플라이언스를 설치 하는 동안 Windows 실제 호스트에 배포 합니다. 어플라이언스 수명 주기 동안 WDS 및 VMM 호스트를 교체 하는 등의 작업을 수행 합니다.  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM)는 가상 컴퓨터에서 실행 되며 HST02을 장애 조치할 수 있습니다. VMM에서 물리적 호스트 운영 체제를 배포 하기 위해 System Center를 호스팅합니다. 또한 VMM WSUS Windows Server Update Services ()을 적용 하거나 모든 호스트 및 가상 컴퓨터에서 Windows 업데이트 제거를 제공 합니다.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
(DNS (Domain Name System), 포함 하는 active Directory 도메인 서비스 HST01와 HST02 둘 다에서 가상 컴퓨터에서 실행 됩니다. 어플라이언스의 고가용성을 위해 AD01 및 AD02는 복제 된 도메인 컨트롤러 및 장애 조치 되지 않으므로 합니다. 하나가 실패 하면 다른 컨트롤러는 이미 올바른 데이터와 함께 사용할 수 있습니다.  
  
*appliance_domain*-ISCSI01  
하나의 ISCSI 가상 컴퓨터와 연결 된 저장소 (HSA01 HSA06) 각 호스트에서 실행 됩니다. 이 VM 장애 조치 되지 않습니다.  
  
### <a name="hosts"></a>호스트  
*appliance_domain*-통해 HST01 *appliance_domain*-HST06  
PDW 제어 노드와 기기 패브릭 가상 컴퓨터에 대 한 호스트입니다. HST03 선택적 수동 호스트 됩니다.  
  
*appliance_domain*-통해 HSA01 *appliance_domain*-HSA08  
연결 된 저장소 (HSA)를 호스트 합니다. 각 HAS 호스트 실행 한 계산 노드 VM 및 ISCSI VM 하나.  
  
### <a name="cluster-for-pdw"></a>PDW에 대 한 클러스터  
*appliance_domain*-WFOHST01  
PDW 클러스터 WFOHST01 라고 합니다. 모든 물리적 호스트 및 PDW에 속한 가상 컴퓨터를 관리 합니다.  
  
### <a name="direct-attached-storage"></a>직접 연결된 저장소  
*appliance_domain*-통해 DAS01 *appliance_domain*-DAS03  
계산 노드에 연결 된 직접 연결된 저장소입니다. HP 마다 두 개의 계산 노드를 위해 하나의 DAS에 있습니다. Dell 및 퀀텀 마다 3 개의 계산 노드를 위해 하나의 DAS 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[어플라이언스 구성 &#40;분석 플랫폼 시스템&#41;](appliance-configuration.md)  
[어플라이언스 관리 작업 &#40;분석 플랫폼 시스템&#41;](appliance-management-tasks.md)  
  
