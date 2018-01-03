---
title: "Linux에서 SQL Server에 대 한 Pacemaker 클러스터 배포 | Microsoft Docs"
description: "이 자습서에는 Linux에서 SQL Server에 대 한 Pacemaker 클러스터를 배포 하는 방법을 보여 줍니다."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 4a014c0b7eedb96375f027674d9eb2374f38c85e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Linux에서 SQL Server에 대 한 Pacemaker 클러스터 배포

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 자습서에서는 대 한 Linux Pacemaker 클러스터를 배포 하는 데 필요한 작업을 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Always On 가용성 그룹 (AG) 또는 장애 조치 클러스터 인스턴스 (FCI). 밀접 하 게 결합 된 Windows 서버와 달리 /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 스택, Pacemaker 클러스터 생성 뿐만 아니라 Linux에서 가용성 그룹 (AG) 구성 가능 전이나 설치 후 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 통합 및 Pacemaker 부분의 AG 또는 FCI 배포에 대 한 리소스의 구성에서 클러스터를 구성한 후 수행 됩니다.
> [!IMPORTANT]
> None 클러스터 유형 AG 않습니다 *하지* Pacemaker 클러스터를 필요는 없으며 Pacemaker로 관리할 수 있습니다. 

> [!div class="checklist"]
> * 항상 사용 가능한 추가 기능을 설치 하 고 Pacemaker를 설치 합니다.
> * Pacemaker (RHEL 및 Ubuntu만)에 대 한 노드를 준비 합니다.
> * Pacemaker 클러스터를 만듭니다.
> * SQL Server HA 및 SQL Server 에이전트 패키지를 설치 합니다.
 
## <a name="prerequisite"></a>사전 요구 사항
[SQL Server 2017 설치](sql-server-linux-setup.md)합니다.

## <a name="install-the-high-availability-add-on"></a>항상 사용 가능한 추가 기능 설치
각 Linux 배포에 대 한 고가용성 (HA) 추가 기능을 구성 하는 패키지를 설치 하려면 아래 구문을 사용 합니다. 

**Red Hat Enterprise Linux(RHEL)**
1.  다음 구문을 사용 하 여 서버를 등록 합니다. 유효한 사용자 이름과 암호를 묻는 메시지가 나타납니다.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  등록에 대 한 사용 가능한 풀을 나열 합니다.
    
    ```bash
    sudo subscription-manager list --available
3.  Run the following command to associate RHEL high availability with the subscription
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    여기서 *PoolId* 이전 단계에서 항상 사용 가능한 구독에 대 한 풀 ID입니다.
    
4.  항상 사용 가능한 추가 기능을 사용 하려면 저장소를 사용 하도록 설정 합니다.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Pacemaker를 설치 합니다.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server(SLES)**

고가용성 패턴 YaST에 설치 하거나 서버의 기본 설치 과정의 일환으로 합니다. 원본 또는 온라인 가져와 ISO/DVD와 설치를 수행할 수 있습니다.
> [!NOTE]
> SLES, 클러스터를 만들 때 HA 기능에 추가 초기화를 가져옵니다.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Pacemaker (RHEL 및 Ubuntu만)에 대 한 노드를 준비 합니다.
자체 pacemaker 라는 분포에 만든 사용자를 사용 하 여 *hacluster*합니다. RHEL 및 Ubuntu에 HA 추가 기능을 설치할 때 사용자를 만들 가져옵니다.
1. Pacemaker 클러스터의 노드로 역할 하는 각 서버에서 클러스터에서 사용할 사용자의 암호를 만듭니다. 예제에 사용 된 이름은 *hacluster*, 되지만 모든 이름을 사용할 수 있습니다. 이름 및 암호에 Pacemaker 클러스터에 참여 하는 모든 노드에서 동일 해야 합니다.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. Pacemaker 클러스터의 일부가 될 각 노드에서 사용 및 시작는 `pcsd` (RHEL 및 Ubuntu) 다음 명령을 사용 하 여 서비스:

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   그런 다음 실행
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   되도록 `pcsd` 시작 됩니다.
3. Pacemaker 클러스터의 가능한 각 노드에서 Pacemaker 서비스를 사용 하도록 설정 합니다.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   Ubuntu, 오류를 표시 합니다.
   
   *기본 시작 pacemaker 중단 없는 runlevels 포함 되어 있습니다.*
   
   이 오류는 알려진된 문제입니다. 오류에도 불구 하 고 Pacemaker 서비스를 설정 하면 성공 하 고 특정 시점에 나중에이 버그를 수정 합니다.
   
4. 다음으로 만들고 Pacemaker 클러스터를 시작 합니다. 이 단계에서 RHEL 및 Ubuntu 간의 한 가지 차이점이 있습니다. 두 배포 중에 설치 `pcs` Pacemaker 클러스터 RHEL,이 명령을 실행에 모든 기존 구성을 제거에 대 한 기본 구성 파일을 구성 하 고 새 클러스터를 만듭니다.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Pacemaker 클러스터 만들기 
이 섹션을 만들고 각 Linux 배포에 대 한 클러스터를 구성 하는 방법을 설명 합니다.

**RHEL**

1. 노드를 권한 부여
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 … NodeN> -u hacluster
   ```
   
   여기서 *NodeX* 노드의 이름입니다.
2. 클러스터 만들기
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   여기서 *PMClusterName* Pacemaker 클러스터에 할당 된 이름 및 *Nodelist* 공백으로 구분 하 여 노드 이름의 목록입니다.

**Ubuntu**

Ubuntu를 구성 하는 것은 RHEL 유사 합니다. 그러나 한 가지 주요 차이점은: 클러스터 및 사용 하도록 설정 및 시작에 대 한 기본 구성을 만듭니다 Pacemaker 패키지 설치 `pcsd`합니다. RHEL의 지침에 따라 정확 하 게 Pacemaker 클러스터를 구성 하려고 하면 오류가 발생 합니다. 이 문제를 해결 하려면 다음 단계를 수행 합니다. 
1. 각 노드에서 기본 Pacemaker 구성을 제거 합니다.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Pacemaker 클러스터를 만드는 데 RHEL 섹션의 단계를 수행 합니다.

**SLES**

Pacemaker 클러스터를 만드는 프로세스는 RHEL 및 Ubuntu는 SLES에 완전히 다릅니다. 아래 단계에 따라 클러스터 SLES를 만드는 방법을 문서화 합니다.
1. 실행 하 여 클러스터 구성 프로세스를 시작 합니다. 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   노드 중 하나입니다. NTP 구성 되지 않은 및 watchdog 장치가 있는 라는 메시지가 수 있습니다. 작업 시작 및 실행에 대 한 괜찮습니다. Watchdog STONITH 저장소 기반 SLES의 기본 제공 펜싱을 사용 하는 경우 관련 되어 있습니다. NTP 및 감시를 나중에 구성할 수 있습니다.
   
2. Corosync를 구성 하 라는 메시지가 표시 됩니다. 멀티 캐스트 주소와 포트 뿐 아니라,에 바인딩할 네트워크 주소는 단계가 있습니다. 네트워크 주소는 사용 중인; 서브넷 예를 들어 192.191.190.0 합니다. 모든 프롬프트에서 기본값을 사용 하거나 필요한 경우 변경할 수 있습니다.
   
3. 다음으로, 디스크 기반 펜싱 변수인 SBD, 구성 하려는 경우에 대해 묻는 클릭 합니다. 이 구성은 필요한 경우 나중에 수행할 수 있습니다. SBD 없으면 RHEL 및 Ubuntu, 달리 구성 `stonith-enabled` 는 기본적으로 false로 설정 합니다.
   
4. 마지막으로 관리에 대 한 IP 주소를 구성 하려는 경우에 대해 묻는 클릭 합니다. 이 IP 주소는 선택적 이지만 함수는 IP 주소를 통해 HA 웹 Konsole (매) 연결에 사용할 클러스터에 생성 됩니다. Windows Server 장애 조치 클러스터 (WSFC)에 대 한 IP 주소와 유사 합니다. 이 구성에서는도 선택 사항입니다.
   
5. 클러스터 인지 확인 실행 되 고 실행 하 여 
   ```bash
   sudo crm status
   ```
   
6. 변경 된 *hacluster* 포함 된 암호 
   ```bash
   sudo passwd hacluster
   ```
   
7. 관리에 대 한 IP 주소를 구성한 경우 테스트에 대 한 암호를 변경 하는 브라우저에서 테스트할 수 있습니다 *hacluster*합니다.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. 클러스터의 노드 수 있는 다른 SLES 서버에서 실행 
   ```bash
   sudo ha-cluster-join
   ```
   
9. 메시지가 표시 되 면 이름 또는 이전 단계에서 클러스터의 첫 번째 노드로 구성 된 서버의 IP 주소를 입력 합니다. 서버는 기존 클러스터에 노드 추가 됩니다.
   
10. 실행 하 여 노드 추가 되었는지 확인 
   ```bash
   sudo crm status
   ```
   
11. 변경 된 *hacluster* 포함 된 암호 
   ```bash
   sudo passwd hacluster
   ```
   
12. 클러스터에 추가할 다른 모든 서버에 대 한 8-11 단계를 반복 합니다.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>SQL Server HA 및 SQL Server 에이전트 패키지를 설치 합니다.
아래 명령을 사용 하 여 SQL Server HA 패키지를 설치 하 고 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트를 아직 설치 되지 않습니다. HA 패키지를 설치한 후 설치 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 를 다시 시작 해야 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 를 사용할 수 있습니다. 이 지침에서는 Microsoft 패키지에 대 한 저장소는 이미 설정 되어 있는지, 이후 가정 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 이 시점에서 설치 해야 합니다.
> [!NOTE]
> - 사용 하지 않는 경우 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 로그 전달 또는 기타 사용에 대 한 에이전트, 없기 설치 되므로 패키지를 *mssql 서버 에이전트* 건너뛸 수 있습니다.
> - 에 대 한 다른 선택적 패키지 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 전체 텍스트 검색 (*mssql-서버-fts*) 및 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql 서버는*), 되지 않습니다 높은 가용성, FCI는 또는 AG에 필요합니다.

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

이 자습서에서는 Linux에서 SQL Server에 대 한 Pacemaker 클러스터를 배포 하는 방법을 배웠습니다. 방법에 대해 배웠습니다에:
> [!div class="checklist"]
> * 항상 사용 가능한 추가 기능을 설치 하 고 Pacemaker를 설치 합니다.
> * Pacemaker (RHEL 및 Ubuntu만)에 대 한 노드를 준비 합니다.
> * Pacemaker 클러스터를 만듭니다.
> * SQL Server HA 및 SQL Server 에이전트 패키지를 설치 합니다.

을 만들고 Linux에서 SQL Server에 대 한 가용성 그룹을 구성 하려면 다음을 참조 하세요.

> [!div class="nextstepaction"]
> [만들기 및 Linux에서 SQL Server에 대 한 가용성 그룹 구성](sql-server-linux-create-availability-group.md)합니다.

