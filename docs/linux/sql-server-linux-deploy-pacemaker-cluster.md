---
title: SQL Server on Linux용 Pacemaker 클러스터 배포
description: 이 자습서에서는 SQL Server on Linux용 Pacemaker 클러스터를 배포하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: b48511e9e737f4fb775925d8a6bff81e31ef2a5a
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196761"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>SQL Server on Linux용 Pacemaker 클러스터 배포

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 자습서에서는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Always On AG(가용성 그룹) 또는 FCI(장애 조치(failover) 클러스터 인스턴스)용 Linux Pacemaker 클러스터를 배포하는 데 필요한 작업을 설명합니다. 긴밀하게 결합된 Windows Server/[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 스택과는 달리, Linux에서 AG(가용성 그룹)를 구성하고 Pacemaker 클러스터를 만드는 작업은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 설치하기 전이나 설치 후에 수행할 수 있습니다. AG 또는 FCI 배포의 Pacemaker 부분에 대한 리소스 통합 및 구성은 클러스터가 구성된 후에 수행됩니다.
> [!IMPORTANT]
> 클러스터 유형이 None인 AG에는 Pacemaker 클러스터가 필요하지 ‘않으며’ Pacemaker에서 관리할 수도 없습니다. 

> [!div class="checklist"]
> * 고가용성 추가 기능을 설치한 다음, Pacemaker를 설치합니다.
> * Pacemaker에 사용할 노드를 준비합니다(RHEL 및 Ubuntu에만 해당).
> * Pacemaker 클러스터를 만듭니다.
> * SQL Server HA 및 SQL Server 에이전트 패키지를 설치합니다.
 
## <a name="prerequisite"></a>필수 요소
[SQL Server 2017을 설치](sql-server-linux-setup.md)합니다.

## <a name="install-the-high-availability-add-on"></a>고가용성 추가 기능 설치
다음 구문을 사용하여 각 Linux 배포의 HA(고가용성) 추가 기능을 구성하는 패키지를 설치합니다. 

**Red Hat Enterprise Linux(RHEL)**
1.  다음 구문을 사용하여 서버를 등록합니다. 유효한 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  등록에 사용할 수 있는 풀을 나열합니다.
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  다음 명령을 실행하여 RHEL 고가용성을 구독에 연결합니다.
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    여기서 *PoolId*는 이전 단계에서 사용한 고가용성 구독의 풀 ID입니다.
    
4.  리포지토리에서 고가용성 추가 기능을 사용할 수 있도록 설정합니다.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Pacemaker를 설치합니다.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server(SLES)**

YaST에서 고가용성 패턴을 설치하거나, 서버의 주 설치 과정에서 설치합니다. ISO/DVD를 원본으로 사용하거나 온라인에서 다운로드하여 설치할 수 있습니다.
> [!NOTE]
> SLES에서는 클러스터를 만들 때 HA 추가 기능이 초기화됩니다.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Pacemaker에 사용할 노드 준비(RHEL 및 Ubuntu에만 해당)
Pacemaker 자체는 *hacluster*라는 배포에서 만든 사용자를 사용합니다. 이 사용자는 RHEL 및 Ubuntu에서 HA 추가 기능을 설치할 때 생성됩니다.
1. Pacemaker 클러스터의 노드로 사용할 각 서버에서 클러스터에 사용할 사용자의 암호를 만듭니다. 예제에서 사용된 이름은 *hacluster*이지만 아무 이름이나 사용할 수 있습니다. 이름과 암호는 Pacemaker 클러스터에 참여하는 모든 노드에서 동일해야 합니다.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. Pacemaker 클러스터에 포함될 각 노드에서 다음 명령을 사용하여 `pcsd` 서비스를 사용하도록 설정하고 시작합니다(RHEL 및 Ubuntu).

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   이제 다음 명령을 실행합니다.
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   이 명령은 `pcsd`가 시작되었는지 확인합니다.
3. Pacemaker 클러스터의 가능한 각 노드에서 Pacemaker 서비스를 사용하도록 설정합니다.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   Ubuntu에서 다음과 같은 오류가 표시됩니다.
   
   *pacemaker Default-Start contains no runlevels, aborting.*
   
   이 오류는 알려진 문제입니다. 오류에 관계없이 Pacemaker 서비스를 사용하도록 설정할 수 있으며, 이 버그는 조만간 수정될 예정입니다.
   
4. 다음으로, Pacemaker 클러스터를 만들고 시작합니다. 이 단계에서는 RHEL과 Ubuntu 간에 한 가지 차이점이 있습니다. 두 배포에서 모두, `pcs`를 설치할 때 Pacemaker 클러스터의 기본 구성 파일이 구성되지만 RHEL에서 이 명령을 실행하면 기존 구성이 모두 삭제되고 새 클러스터가 생성됩니다.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Pacemaker 클러스터 만들기 
이 섹션에서는 각 Linux 배포의 클러스터를 만들고 구성하는 방법을 설명합니다.

**RHEL**

1. 노드에 권한을 부여합니다.
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   여기서 *NodeX*는 노드의 이름입니다.
2. 클러스터 만들기
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   여기서 *PMClusterName*은 Pacemaker 클러스터에 할당된 이름이고, *Nodelist*는 공백으로 구분된 노드의 이름 목록입니다.

**Ubuntu**

Ubuntu 구성도 RHEL와 비슷합니다. 그러나 Pacemaker 패키지를 설치할 때 클러스터의 기본 구성이 생성되며 `pcsd`가 사용하도록 설정되고 시작된다는 중요한 차이점이 있습니다. 정확하게 RHEL 지침에 따라 Pacemaker 클러스터를 구성하려고 하면 오류가 발생합니다. 이 문제를 해결하려면 다음 단계를 수행합니다. 
1. 각 노드에서 기본 Pacemaker 구성을 제거합니다.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Pacemaker 클러스터를 만드는 RHEL 섹션의 단계를 수행합니다.

**SLES**

RHEL 및 Ubuntu와 SLES에서 Pacemaker 클러스터를 만드는 프로세스는 완전히 다릅니다. 다음 단계에서는 SLES를 사용하여 클러스터를 만드는 방법을 설명합니다.
1. 노드 중 하나에서 다음 명령을 실행하여 클러스터 구성 프로세스를 시작합니다. 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   NTP가 구성되어 있지 않고 Watchdog 디바이스를 찾을 수 없다는 메시지가 표시될 수 있습니다. 프로세스를 시작하고 실행하는 데에는 아무 문제도 없습니다. 스토리지를 기반으로 하는 SLES의 기본 제공 펜싱을 사용하는 경우 Watchdog는 STONITH와 관련이 있습니다. NTP 및 Watchdog는 나중에 구성할 수 있습니다.
   
2. Corosync를 구성하라는 메시지가 표시됩니다. 멀티캐스트 주소 및 포트뿐만 아니라 바인딩할 네트워크 주소를 묻는 메시지가 표시됩니다. 네트워크 주소는 사용 중인 서브넷입니다. 예를 들어 192.191.190.0입니다. 모든 프롬프트에서 기본값을 그대로 적용하거나 필요한 경우 변경할 수 있습니다.
   
3. 다음으로, 디스크 기반 펜싱인 SBD을 구성할지 묻는 메시지가 표시됩니다. 이 구성은 원하는 경우 나중에 수행할 수 있습니다. SBD를 구성하지 않으면, RHEL 및 Ubuntu와 달리 `stonith-enabled`가 기본적으로 false로 설정됩니다.
   
4. 마지막으로 관리에 사용할 IP 주소를 구성할지 묻는 메시지가 표시됩니다. 이 IP 주소는 선택 사항이지만, HAWK(HA Web Konsole)를 통해 연결하는 데 사용할 IP 주소를 클러스터에 만든다는 점에서 WSFC(Windows Server 장애 조치(failover) 클러스터)의 IP 주소와 유사하게 작동합니다. 이 구성도 선택 사항입니다.
   
5. 다음 명령을 실행하여 클러스터가 시작되어 실행되고 있는지 확인합니다. 
   ```bash
   sudo crm status
   ```
   
6. 다음 명령을 사용하여 *hacluster* 암호를 변경합니다. 
   ```bash
   sudo passwd hacluster
   ```
   
7. 관리에 사용할 IP 주소를 구성한 경우 브라우저에서 테스트할 수 있습니다. 그러면 *hacluster*의 암호 변경도 테스트됩니다.
   ![hacLuster](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. 클러스터의 노드로 사용할 또 다른 SLES 서버에서 다음 명령을 실행합니다. 
   ```bash
   sudo ha-cluster-join
   ```
   
9. 메시지가 표시되면 이전 단계에서 클러스터의 첫 번째 노드로 구성된 서버의 이름 또는 IP 주소를 입력합니다. 서버가 기존 클러스터에 노드로 추가됩니다.
   
10. 다음 명령을 실행하여 노드가 추가되었는지 확인합니다. 
   ```bash
   sudo crm status
   ```
   
11. 다음 명령을 사용하여 *hacluster* 암호를 변경합니다. 
   ```bash
   sudo passwd hacluster
   ```
   
12. 클러스터에 추가할 다른 모든 서버에서 8~11단계를 반복합니다.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>SQL Server HA 및 SQL Server 에이전트 패키지 설치
다음 명령을 사용하여 SQL Server HA 패키지와 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트를 설치합니다(아직 설치되지 않은 경우). [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 설치한 후에 HA 패키지를 설치하려면 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 다시 시작해야 사용할 수 있습니다. 이 지침에서는 이때 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]가 설치되어 있어야 하기 때문에 Microsoft 패키지의 리포지토리가 이미 설정되었다고 가정합니다.
> [!NOTE]
> - 로그 전달 또는 기타 용도로 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트를 사용하지 않는 경우에는 에이전트를 설치할 필요가 없으므로 *mssql-server-agent* 패키지를 건너뛰어도 됩니다.
> - [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] on Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 전체 텍스트 검색(*mssql-server-fts*) 및 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services(*mssql-server-is*)의 다른 선택적 패키지는 FCI 또는 AG의 고가용성에 필요하지 않습니다.

**RHEL**

```bash
sudo yum install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**Ubuntu**

```bash
sudo apt-get install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**SLES**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 SQL Server on Linux용 Pacemaker 클러스터를 배포하는 방법을 알아보았습니다. 구체적으로 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * 고가용성 추가 기능을 설치한 다음, Pacemaker를 설치합니다.
> * Pacemaker에 사용할 노드를 준비합니다(RHEL 및 Ubuntu에만 해당).
> * Pacemaker 클러스터를 만듭니다.
> * SQL Server HA 및 SQL Server 에이전트 패키지를 설치합니다.

SQL Server on Linux의 가용성 그룹을 만들고 구성하려면 다음을 참조하세요.

> [!div class="nextstepaction"]
> [SQL Server on Linux의 가용성 그룹 만들기 및 구성](sql-server-linux-create-availability-group.md)

