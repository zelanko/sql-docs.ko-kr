---
title: Linux에서 다중 서브넷 Always On 가용성 그룹과 장애 조치 클러스터 인스턴스 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 595add5d077136c4093776fae8e3a2f7ab04bb26
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396176"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>다중 서브넷 Always On 가용성 그룹 및 장애 조치 클러스터 인스턴스 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

경우 Always On 가용성 그룹 (AG) 또는 장애 조치 클러스터 인스턴스 (FCI)에 걸쳐 사이트가 둘 이상, 각 사이트 일반적으로 자체 네트워킹을 있습니다. 이 경우 대체로 각 사이트에 자체 IP 주소를 지정 합니다. 사이트 A의 주소는 예를 들어 192.168.1로 시작합니다. *x* 하 고 사이트 B의 주소 192.168.2를 시작 합니다. *x*, 여기서 *x* 서버에 고유한 IP 주소의 일부입니다. 네트워킹 계층에서 적절 한 라우팅을의 몇 가지 정렬 하지 않고 이러한 서버 됩니다 서로 통신할 수 있습니다. 이 시나리오를 처리 하는 방법은 두 가지가 있습니다: VLAN을 라고 하는 두 개의 다른 서브넷에 연결 하는 네트워크를 설정 하거나 서브넷 간에 라우팅을 구성 합니다.

## <a name="vlan-based-solution"></a>VLAN 기반 솔루션
 
**필수 구성 요소**: VLAN 기반 솔루션의 경우 각 서버는 AG 또는 FCI를 참여 해야 적절 한 가용성 (NIC 이중 포트는 단일 물리적 서버에서 실패 한 수 없음)에 대 한 두 개의 네트워크 카드 (Nic) 하나 뿐 아니라 네이티브 해당 서브넷에 IP 주소 할당 될 수 있도록 VLAN에서. ISCSI는 또한 자체 네트워크 등의 다른 네트워크 요구 하는 것 외에도입니다.

AG 또는 FCI에 대 한 IP 주소 만들기 VLAN에서 수행 됩니다. 다음 예제에서는 VLAN 192.168.3의 서브넷을 있습니다. *x*이므로 AG 또는 FCI에 대해 만든 IP 주소는 192.168.3.104 합니다. 어떠한 추가 작업도 이므로 AG 또는 FCI에 할당 되는 단일 IP 주소를 구성 해야 합니다.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Pacemaker 사용 하 여 구성

Windows 환경에서 Windows Server 장애 조치 클러스터 (WSFC)는 고유 하 게 여러 서브넷을 지원 하 고 IP 주소에서 OR 종속성을 통해 여러 IP 주소를 처리 합니다. Linux에서 종속성이 없으므로 OR, 이지만 Pacemaker를 사용 하 여 고유 하 게 적절 한 다중 서브넷을 달성 하는 방법 다음과 같이 합니다. 단순히 리소스를 수정 하려면 일반 Pacemaker 명령줄을 사용 하 여이 수행할 수 없습니다. 클러스터 정보를 기본 (CIB)를 수정 해야 합니다. CIB은 Pacemaker 구성 사용 하 여 XML 파일입니다.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>CIB 업데이트

1.  CIB를 내보냅니다.

    **Ubuntu 및 Red Hat Enterprise Linux (RHEL)**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server(SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    여기서 *filename* CIB 호출 하려는 이름입니다.

2.  생성 된 파일을 편집 합니다. 검색할는 `<resources>` 섹션입니다. AG 또는 FCI에 대해 생성 된 다양 한 리소스에 표시 됩니다. 연결이 된 IP 주소를 찾습니다. 추가 된 `<instance attributes>` 하기 전에 기존 것 보다 높은 것인지 아니면 두 번째 IP 주소에 대 한 정보를 사용 하 여 섹션 `<operations>`합니다. 다음 구문을 비슷합니다.

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    여기서 *NameForAttribute* 은이 특성에 대 한 고유한 이름 *점수 매기기* 보다 높아야 합니다 기본 서브넷에 있는 특성을 할당할 수 *RuleName*규칙의 이름입니다 *ExpressionName* 식의 이름인 *NodeNameInSubnet2* 다른 서브넷의 노드 이름은 *NameForSecondIP* 두 번째 IP 주소와 연결 된 이름인 *IPAddress* , 두 번째 서브넷의 IP 주소인 *NameForSecondIPNetmask* 네트워크 마스크를 사용 하 여 연결 된 이름 및 *넷마스크* 두 번째 서브넷에 대 한 네트워크 마스크 됩니다.
    
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

3.  수정 된 CIB 가져오고 Pacemaker를 다시 구성 합니다.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    여기서 *filename* 수정된 된 IP 주소 정보를 사용 하 여 CIB 파일의 이름입니다.

### <a name="check-and-verify-failover"></a>확인 하 고 장애 조치를 확인 합니다.

1.  CIB가 성공적으로 업데이트 된 구성과 적용 후 Pacemaker에 IP 주소 리소스와 연결 된 DNS 이름을 ping 합니다. 현재는 AG 또는 FCI를 호스팅하는 서브넷을 사용 하 여 연결 된 IP 주소를 반영 해야 합니다.
2.  다른 서브넷에는 AG 또는 FCI를 실패 합니다.
3.  AG 또는 FCI를 완벽 하 게 온라인 상태가 되 면 IP 주소에 연결 된 DNS 이름을 ping 합니다. 두 번째 서브넷의 IP 주소를 반영 해야 합니다.
4.  원하는 경우 AG 또는 FCI은 원래 서브넷으로 실패 합니다.
