---
title: 어플라이언스 물리적 구성 요소-Analytics Platform System | Microsoft Docs
description: 이름 및 PDW 및 어플라이언스 패브릭 물리적 구성 요소에 대해 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0adbd92d1a29a98a80de65268c53ea63e3941d07
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639925"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>어플라이언스 물리적 구성 요소-Analytics Platform System
이름 및 PDW 및 어플라이언스 패브릭 물리적 구성 요소에 대해 설명 합니다. 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>구성 요소 다이어그램  
물리적 구성 요소 및 6-Compute 노드 어플라이언스의 첫 번째 랙에 위치 이름을 표시 합니다.  
  
![PDW Region Component Names - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
PDW 구성 요소에 대 한 실제 이름에는 구성 요소 이름 뒤에 대시를 뒤에, PDW 영역 이름이입니다. 예를 들어 PDW 영역 이름을 PDW123 이면 실제 이름이 됩니다 **PDW123 CTL01**를 **PDW123-CMP01**등입니다.  
  
마찬가지로, 어플라이언스 패브릭 구성 요소에 대 한 실제 이름을 뒤에 구성 요소 이름 뒤에 대시를 어플라이언스 도메인입니다. 예를 들어, 어플라이언스 도메인 FSW123 경우 어플라이언스 패브릭의 Vm은 **FSW123 WDS**를 **FSW123 AD01**합니다 **FSW123 VMM**등입니다.  
  
6 개 계산 노드가 있는 PDW 영역 통합된 된 뷰는 다음과 같습니다.  
  
![PDW 구성 요소 이름](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW 구성 요소  
PDW 가상 머신은 PDW 영역 부분입니다.  
  
*PDW_region*-CTL01  
제어 노드를 실행 하는 가상 컴퓨터. 이 HST01에서 실행 되 고 HST02로 장애 조치할 수 있습니다.  
  
> [!WARNING]  
> SQL Server PDW는 Hyper-v 관리자를 사용 하 여 CTL01 가상 머신의 스냅숏 만들기를 지원 하지 않습니다. 스냅숏 가상 컴퓨터 백업 장애 조치 하는 경우 오류가 발생할 수 있는 로컬 저장소에 의존 합니다. 스냅숏 만들기도 문제가 발생할 수 있으므로 안정성 다른 VM의 수동 서버는 장애 조치.  
  
*PDW_region*-통해 CMP01 *PDW_Region*-CMP06  
계산 노드를 실행 하는 가상 컴퓨터. 이 6-Compute 노드 다이어그램에서 HSA06 실행을 통해 호스트 HSA01 계산 노드 Vm CMP01 CMP06 통해 각각.  
  
## <a name="fabric"></a>어플라이언스 패브릭 구성 요소  
이러한 구성 요소는 어플라이언스 패브릭의 일부입니다.  
  
### <a name="virtual-machines"></a>Virtual Machines  
*appliance_domain*-WDS  
이 가상 컴퓨터 호스트의 Windows 배포 서비스 (WDS), Analytics Platform System을 사용 하는 어플라이언스 네트워크를 통해 Windows 운영 체제를 배포 합니다. 또한 미리 구성 된 IP 주소를 사용 하지 않고도 어플라이언스 네트워크에 가입 하도록 어플라이언스에 호스트를 허용 하는 DHCP 서비스를 호스트 합니다.  
  
합니다 *appliance_domain*-WDS 가상 머신 HST01에서 실행 되 고 HST02로 장애 조치할 수 있습니다. WDS 가상 머신과 VMM 가상 컴퓨터로 어플라이언스를 설치 하는 동안 실제 호스트의 Windows를 배포 합니다. 어플라이언스 수명 주기 동안 WDS 및 VMM 호스트를 대체 하는 등의 작업을 수행 합니다.  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM) 가상 컴퓨터에서 실행 되며 HST02에 장애 조치할 수 있습니다. VMM은 물리적 호스트의 운영 체제를 배포 하려면 System Center를 호스팅합니다. 또한 VMM Windows Server Update Services (WSUS)을 적용 하거나 모든 호스트 및 virtual machines에서 Windows 업데이트를 제거를 제공 합니다.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
도메인 이름 시스템 (DNS)를 포함 하는 active Directory Domain Services에 모두 HST01 HST02 가상 컴퓨터에서 실행 됩니다. 어플라이언스의 고가용성을 위해 AD01 AD02와 복제 된 도메인 컨트롤러 및 장애 조치 하지 않습니다. 하나가 실패 하면 다른 하나는 올바른 데이터를 사용할 수 있는 이미 있습니다.  
  
*appliance_domain*-ISCSI01  
각 호스트에 연결 된 저장소 (HSA01 HSA06)를 사용 하 여 ISCSI 가상 머신 하나를 실행합니다. 이 VM에 장애 조치 되지 않습니다.  
  
### <a name="hosts"></a>호스트  
*appliance_domain*-HST01 through *appliance_domain*-HST06  
PDW 제어 노드 및 어플라이언스 패브릭 가상 머신에 대 한 호스트입니다. HST03 선택적 수동 호스트 됩니다.  
  
*appliance_domain*-통해 HSA01 *appliance_domain*-HSA08  
연결 된 저장소 (HSA)를 사용 하 여 호스트입니다. 각 HAS 호스트 실행 한 계산 노드 VM 및 ISCSI VM 하나입니다.  
  
### <a name="cluster-for-pdw"></a>PDW에 대 한 클러스터  
*appliance_domain*-WFOHST01  
PDW 클러스터 WFOHST01 이라고 합니다. 모든 물리적 호스트 및 PDW에 속하는 가상 컴퓨터를 관리 합니다.  
  
### <a name="direct-attached-storage"></a>직접 연결된 저장소  
*appliance_domain*-통해 DAS01 *appliance_domain*-DAS03  
이 직접 연결 된 저장소를 계산 노드에 연결할입니다. HP는 두 개의 모든 계산 노드에 대 한 하나의 DAS입니다. Dell 및 퀀텀 모든 세 가지 계산 노드에 대 한 하나의 DAS에 있습니다.  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[어플라이언스 구성 &#40;Analytics Platform System&#41;](appliance-configuration.md)  
[어플라이언스 관리 작업 &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
