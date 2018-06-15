---
title: Linux에서 다중 서브넷 Always On 가용성 그룹 및 장애 조치 클러스터 인스턴스 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 612ac9c684fa8e0383981a32a94cf82d8ec68678
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34321904"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>다중 서브넷 Always On 가용성 그룹 및 장애 조치 클러스터 인스턴스 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

때 항상에 가용성 그룹 (AG) 또는 장애 조치 클러스터 인스턴스 (FCI)에 걸쳐 있는 사이트가 둘 이상, 각 사이트 일반적으로 자체 네트워킹을 있습니다. 종종 즉, 각 사이트에 고유한 IP 주소를 지정 합니다. 예를 들어 사이트 A의 주소 192.168.1로 시작 합니다. *x* 사이트 B의 주소 192.168.2로 시작 하 고. *x*여기서 *x* 서버에 고유한 IP 주소의 일부입니다. 네트워킹 계층에서 현재 위치에서 라우팅의 일종 없이 이러한 서버 됩니다 서로 통신할 수 있습니다. 이 시나리오를 처리 하는 방법은 두 가지가: VLAN을 라는 두 개의 다른 서브넷에 연결 하는 네트워크를 설정 하거나 서브넷 간 라우팅을 구성 합니다.

## <a name="vlan-based-solution"></a>VLAN 기반 솔루션
 
**필수 구성 요소**: VLAN에 대 한 기반 솔루션 AG 또는 FCI에 참여 하는 각 서버 두 개의 Nic (네트워크 카드)에 필요한 적절 한 가용성 (NIC 이중 포트 일 단일 물리적 서버에서 실패 한)에 IP 주소 할당 될 수 있도록 해당 기본 서브넷으로 VLAN에서 하나. ISCSI는 또한 자체 네트워크 등의 다른 네트워크 요구 외에도입니다.

IP 주소 만들기 AG 또는 FCI에 대 한 VLAN에서 수행 됩니다. 다음 예제에서는 VLAN 192.168.3의 서브넷을 있습니다. *x*AG 또는 FCI에 대해 생성 하는 IP 주소는 192.168.3.104 합니다. 어떠한 추가 작업도 AG 또는 FCI에 할당 된 단일 IP 주소가 있기 때문에 구성할 수 있어야 합니다.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Pacemaker 인 구성

Windows 환경에서 Windows Server 장애 조치 클러스터 (WSFC)는 기본적으로 다중 서브넷 지원 하 고 IP 주소에 의존 하는 OR 통해 여러 개의 IP 주소를 처리 합니다. Linux, OR 종속성이 있지만 다음에 의해 표시 된 것 처럼 Pacemaker를 사용 하 여 적절 한 다중 서브넷을 고유 하 게 달성 하는 방법을 합니다. 리소스 수정 Pacemaker 일반적인 명령줄 사용 하 여이 수행할 수 없습니다. 클러스터 정보 기본 (CIB)를 수정 해야 합니다. CIB은 Pacemaker 구성 사용 하 여 XML 파일입니다.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>CIB 업데이트

1.  CIB 내보냅니다.

    **Red Hat Enterprise Linux (RHEL) 및 Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server(SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    여기서 *filename* CIB 호출 하려는 이름입니다.

2.  생성 된 파일을 편집 합니다. 에 대 한 조회는 `<resources>` 섹션. AG 또는 FCI에 대해 생성 된 다양 한 리소스에 표시 됩니다. IP 주소와 연결 된 드라이브를 찾습니다. 추가 `<instance attributes>` 하기 전에 두 번째 IP 주소 위쪽 또는 아래쪽에 기존에 대 한 정보로 섹션 `<operations>`합니다. 다음 구문을 비슷합니다.

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    여기서 *NameForAttribute* 은이 특성에 대 한 고유한 이름 *점수* 기본 서브넷의 보다 높아야, 하는 특성에 할당 된 번호는 *RuleName*해당 규칙의 이름 *ExpressionName* 식의 이름인 *NodeNameInSubnet2* 다른 서브넷에 있는 노드의 이름 *NameForSecondIP* 두 번째 IP 주소와 연결 된 이름 *IPAddress* 두 번째 서브넷의 IP 주소는 *NameForSecondIPNetmask* 네트워크 마스크를와 연결 된 이름 및 *네트워크 마스크* 두 번째 서브넷에 대 한 네트워크 마스크 됩니다.
    
    다음 예를 보여 줍니다.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  수정 된 CIB 가져오고 Pacemaker 다시 구성 합니다.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    여기서 *filename* 수정 된 IP 주소 정보를 사용 하 여 CIB 파일의 이름입니다.

### <a name="check-and-verify-failover"></a>확인 하 고 장애 조치를 확인 합니다.

1.  업데이트 된 구성과 CIB가 성공적으로 적용 된 후 Pacemaker의 IP 주소 리소스와 연결 된 DNS 이름을 ping 합니다. AG 또는 FCI를 현재 호스팅하고 서브넷과 연결 된 IP 주소를 반영 해야 합니다.
2.  AG 또는 FCI에서 다른 서브넷에 실패 합니다.
3.  AG 또는 FCI를 완벽 하 게 온라인 후 IP 주소와 연결 된 DNS 이름을 ping 합니다. 두 번째 서브넷에서 IP 주소를 반영 해야 합니다.
4.  원하는 경우 AG 또는 FCI 다시 원래 서브넷에 실패 합니다.
