---
title: 어플라이언스 물리적 구성 요소
description: PDW 및 어플라이언스 패브릭 물리적 구성 요소에 대 한 이름 및 설명입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5cbed66f53189668518e04848002ae69adb8c614
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400926"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>어플라이언스 물리적 구성 요소-분석 플랫폼 시스템
PDW 및 어플라이언스 패브릭 물리적 구성 요소에 대 한 이름 및 설명입니다. 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>구성 요소 다이어그램  
이는 물리적 구성 요소의 이름과 6-계산 노드 어플라이언스의 첫 번째 랙에 있는 위치를 보여 줍니다.  
  
![PDW 영역 구성 요소 이름 - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
PDW 구성 요소에 대 한 실제 이름은 PDW 지역 이름과 대시, 구성 요소 이름을 차례로 입력 합니다. 예를 들어 PDW 지역 이름이 PDW123 인 경우 실제 이름은 **PDW123-CTL01**, **PDW123-CMP01**등입니다.  
  
마찬가지로 어플라이언스 패브릭 구성 요소의 실제 이름은 어플라이언스 도메인, 대시, 구성 요소 이름을 차례로 입력 합니다. 예를 들어 어플라이언스 도메인이 FSW123 인 경우 어플라이언스 패브릭 Vm은 **FSW123**, **FSW123-AD01**, **FSW123-VMM**등입니다.  
  
다음은 6 개의 계산 노드가 있는 PDW 지역에 대 한 통합 보기입니다.  
  
![PDW 구성 요소 이름](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW 구성 요소  
PDW 가상 머신은 PDW 지역의 일부입니다.  
  
*PDW_region*-CTL01  
컨트롤 노드를 실행 하는 가상 컴퓨터입니다. 이는 HST01에서 실행 되며 HST02로 장애 조치 (failover) 할 수 있습니다.  
  
> [!WARNING]  
> SQL Server PDW에서는 Hyper-v 관리자를 사용 하 여 CTL01 가상 컴퓨터의 스냅숏 만들기를 지원 하지 않습니다. 스냅숏은 로컬 저장소를 사용 하 여 가상 컴퓨터가 해당 백업으로 장애 조치 (failover)를 시도 하는 경우 오류를 발생 시킵니다. 스냅숏을 만들면 수동 서버로 장애 조치 (failover) 되는 다른 VM의 안정성 문제가 발생할 수도 있습니다.  
  
*PDW_region*- *PDW_Region*CMP01-CMP06  
계산 노드를 실행 하는 가상 컴퓨터입니다. 이 6-계산 노드 다이어그램에서 HSA06 HSA01를 통해 호스트는 계산 노드 Vm CMP01를 통해 각각 CMP06를 실행 합니다.  
  
## <a name="fabric"></a>어플라이언스 패브릭 구성 요소  
이러한 구성 요소는 어플라이언스 패브릭의 일부입니다.  
  
### <a name="virtual-machines"></a>Virtual Machines  
*appliance_domain*-WDS  
이 가상 컴퓨터는 WDS (Windows 배포 서비스을 호스트 하며,이는 분석 플랫폼 시스템이 어플라이언스 네트워크를 통해 Windows 운영 체제를 배포 하는 데 사용 합니다. 또한 미리 구성 된 IP 주소를 사용 하지 않고 어플라이언스 호스트가 어플라이언스 네트워크에 가입 하도록 허용 하는 DHCP 서비스도 호스팅합니다.  
  
*Appliance_domain*WDS 가상 머신은 HST01에서 실행 되며 HST02로 장애 조치 (failover) 할 수 있습니다. WDS 가상 컴퓨터 및 VMM 가상 컴퓨터는 어플라이언스를 설치 하는 동안 물리적 호스트에 Windows를 배포 합니다. 어플라이언스 수명 주기 동안 WDS 및 VMM은 호스트 교체와 같은 작업을 수행 합니다.  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM)는 가상 머신에서 실행 되며 HST02로 장애 조치 (failover) 할 수 있습니다. VMM은 물리적 호스트에 운영 체제를 배포 하는 System Center를 호스팅합니다. 또한 VMM은 모든 호스트 및 가상 컴퓨터에서 Windows 업데이트를 적용 하거나 제거 하는 WSUS (Windows Server Update Services)를 제공 합니다.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
DNS (Domain Name System)를 포함 하는 Active Directory Domain Services은 HST01 및 HST02 둘 다의 가상 머신에서 실행 됩니다. 어플라이언스의 고가용성을 위해 AD01 및 AD02는 복제 된 도메인 컨트롤러 이며 장애 조치 (failover) 되지 않습니다. 실패 한 경우 다른 데이터를 이미 사용할 수 있습니다.  
  
*appliance_domain*-ISCSI01  
하나의 ISCSI 가상 머신은 저장소가 연결 된 각 호스트에서 실행 됩니다 (HSA01-HSA06). 이 VM은 장애 조치 (failover) 되지 않습니다.  
  
### <a name="hosts"></a>호스트  
*appliance_domain*- *appliance_domain*HST01-HST06  
PDW 제어 노드 및 어플라이언스 패브릭 가상 컴퓨터에 대 한 호스트입니다. HST03는 선택적 수동 호스트입니다.  
  
*appliance_domain*- *appliance_domain*HSA01-HSA08  
저장소에 연결 된 호스트 (HSA). 각에는 하나의 계산 노드 VM과 하나의 ISCSI VM이 실행 됩니다.  
  
### <a name="cluster-for-pdw"></a>PDW에 대 한 클러스터  
*appliance_domain*-WFOHST01  
PDW 클러스터의 이름은 WFOHST01입니다. PDW에 속한 모든 물리적 호스트 및 가상 컴퓨터를 관리 합니다.  
  
### <a name="direct-attached-storage"></a>직접 연결 된 저장소  
*appliance_domain*- *appliance_domain*DAS01-DAS03  
이는 계산 노드에 연결 된 직접 연결 된 저장소입니다. HP에는 두 개의 계산 노드에 대 한 DAS가 하나씩 있습니다. Dell 및 퀀텀은 3 개의 계산 노드 마다 하나의 DAS를 가집니다.  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[어플라이언스 구성 &#40;분석 플랫폼 시스템&#41;](appliance-configuration.md)  
[기기 관리 작업 &#40;분석 플랫폼 시스템&#41;](appliance-management-tasks.md)  
  
