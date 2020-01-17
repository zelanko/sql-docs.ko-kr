---
title: 다중 서브넷 가용성 그룹 및 FCI 구성(Linux)
description: SQL Server on Linux의 다중 서브넷 Always On 가용성 그룹과 FCI(장애 조치 클러스터 인스턴스)를 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: f35f1916107e8ede0e7bf7cc3df483a0c33f3355
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558614"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>다중 서브넷 Always On 가용성 그룹 및 장애 조치(failover) 클러스터 인스턴스 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Always On AG(가용성 그룹) 또는 FCI(장애 조치(failover) 클러스터 인스턴스)가 둘 이상의 사이트에 걸쳐 있는 경우 각 사이트에는 일반적으로 자체 네트워킹이 있습니다. 이는 각 사이트에 자체 IP 주소 지정이 있다는 의미이기도 합니다. 예를 들어 사이트 A의 주소는 192.168.1.*x*로 시작하고 사이트 B의 주소는 192.168.2.*x*로 시작합니다. 여기서 *x*는 서버에 고유한 IP 주소 부분입니다. 네트워킹 계층에 라우팅이 없으면 이러한 서버는 서로 통신할 수 없습니다. 이 시나리오를 처리하는 두 가지 방법은 두 개의 서브넷을 연결하는 VLAN이라고 하는 네트워크를 설정하거나 서브넷 간에 라우팅을 구성하는 것입니다.

## <a name="vlan-based-solution"></a>VLAN 기반 솔루션
 
**필수 조건:** VLAN 기반 솔루션의 경우 AG 또는 FCI에 참여하는 각 서버에는 적절한 가용성을 위해 두 개의 네트워크 카드(NIC)가 필요하므로(이중 포트 NIC는 실제 서버에서 단일 실패 지점이 됨), 서버에는 VLAN뿐 아니라 기본 서브넷의 IP 주소가 할당될 수 있습니다. 이 필수 조건은 자체 네트워크가 필요한 iSCSI 같은 다른 네트워크 요구 사항에 추가됩니다.

AG 또는 FCI에 대한 IP 주소는 VLAN에서 생성됩니다. 다음 예제에서 VLAN에는 192.168.3.*x* 서브넷이 있으므로. AG 또는 FCI에 대해 생성된 IP 주소는 192.168.3.104입니다. AG 또는 FCI에 할당된 단일 IP 주소가 있으므로 추가로 구성할 필요가 없습니다.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Pacemaker를 사용한 구성

Windows 환경에서 WSFC(Windows Server 장애 조치(failover) 클러스터)는 기본적으로 여러 서브넷을 지원하며 IP 주소에 대한 OR 종속성을 통해 여러 IP 주소를 처리합니다. Linux에는 OR 종속성이 없지만 다음과 같이 Pacemaker를 사용하여 기본적으로 적절한 다중 서브넷을 달성할 수 있는 방법이 있습니다. 단순히 일반적인 Pacemaker 명령줄을 사용하여 리소스를 수정하는 방법으로는 이 작업을 수행할 수 없습니다. CIB(Cluster Information Base)를 수정해야 합니다. CIB는 Pacemaker 구성이 포함된 XML 파일입니다.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>CIB 업데이트

1.  CIB를 내보냅니다.

    **RHEL(Red Hat Enterprise Linux) 및 Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server(SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    여기서 *filename*은 CIB를 호출할 이름입니다.

2.  생성된 파일을 편집합니다. `<resources>` 섹션을 찾습니다. AG 또는 FCI에 대해 생성된 다양한 리소스가 표시됩니다. IP 주소와 연결된 항목을 찾습니다. 두 번째 IP 주소의 정보가 포함된 `<instance attributes>` 섹션을 기존 항목 위 또는 아래의 `<operations>` 앞에 추가합니다. 다음 구문과 유사합니다.

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    여기서 *NameForAttribute*는 이 특성의 고유 이름이고, *Score*는 주 서브넷 번호보다 높은 특성에 할당된 번호이고, *RuleName*은 규칙 이름이고, *ExpressionName*은 식 이름이고, *NodeNameInSubnet2*는 다른 서브넷에 있는 노드 이름이고, *NameForSecondIP*는 두 번째 IP 주소와 연결된 이름이고, *IPAddress*는 두 번째 서브넷의 IP 주소이고, *NameForSecondIPNetmask*는 네트워크 마스크와 연결된 이름이고, *Netmask*는 두 번째 서브넷의 네트워크 마스크입니다.
    
    예제는 다음과 같습니다.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  수정된 CIB를 가져오고 Pacemaker를 다시 구성합니다.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    여기서 *filename*은 수정된 IP 주소 정보가 포함된 CIB 파일의 이름입니다.

### <a name="check-and-verify-failover"></a>장애 조치(failover) 확인

1.  업데이트된 구성으로 CIB가 적용된 후 Pacemaker에서 IP 주소 리소스와 연결된 DNS 이름을 ping합니다. 현재 AG 또는 FCI를 호스트하는 서브넷과 연결된 IP 주소를 반영해야 합니다.
2.  AG 또는 FCI를 다른 서브넷으로 장애 조치(failover)합니다.
3.  AG 또는 FCI가 완전히 온라인 상태가 된 후 IP 주소와 연결된 DNS 이름을 ping합니다. 두 번째 서브넷의 IP 주소를 반영해야 합니다.
4.  원하는 경우 AG 또는 FCI를 원래 서브넷으로 장애 복구(failback)합니다.
