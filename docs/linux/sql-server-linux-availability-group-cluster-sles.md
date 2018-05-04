---
title: SLES 클러스터 SQL Server 가용성 그룹에 대 한 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: a32854d6619cc053d9dc9cfc28a9f17cba479f34
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>SQL Server 가용성 그룹에 대 한 SLES 클러스터를 구성 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 가이드를 SQL Server에서 SUSE Linux Enterprise Server (SLES) 12 s p 2에 대 한 3 개 노드 클러스터를 만드는 지침을 제공 합니다. 고가용성을 위해 Linux에서 가용성 그룹에 노드가 3 개 필요-참조 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다. 클러스터링 레이어 SUSE 기반 [높은 가용성 확장 (HAE)](https://www.suse.com/products/highavailability) 기반으로 구축 [Pacemaker](http://clusterlabs.org/)합니다. 

클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대 한 자세한 내용은 참조 하십시오. [SUSE Linux Enterprise 높은 가용성 확장 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)합니다.

>[!NOTE]
>이 시점에서 linux Pacemaker와 SQL Server의 통합 Windows에서 WSFC와으로으로 결합 된 않습니다. Linux에서 SQL Server 서비스의 클러스터를 인식할 수 없는 경우 Pacemaker 모든 가용성 그룹 리소스를 포함 하 여 클러스터 리소스의 오케스트레이션을 제어 합니다. Linux에서 항상에 가용성 그룹 동적 관리 뷰 (Dmv) sys.dm_hadr_cluster 같은 클러스터 정보를 제공 하는에 되지는지 않습니다. 또한 가상 네트워크 이름은 WSFC 관련, Pacemaker에는 동일한 동등한 옵션이 없습니다. 장애 조치 후 투명 하 게 다시 연결에 사용할 수신기를 만들 수 있지만 (다음 섹션에서 설명)으로 가상 IP 리소스를 만드는 데 IP와 함께 DNS 서버에서 수신기 이름은 수동으로 등록 해야 합니다.


## <a name="roadmap"></a>로드맵

고가용성을 위한 가용성 그룹을 만드는 절차는 Linux 서버와 Windows Server 장애 조치 클러스터 간에 다릅니다. 다음 목록에서는 단계를 간략히 설명합니다. 

1. [SQL Server 클러스터 노드에서 구성](sql-server-linux-setup.md)합니다.

2. [가용성 그룹 만들기](sql-server-linux-availability-group-failover-ha.md)합니다. 

3. Pacemaker 같은 클러스터 리소스 관리자를 구성 합니다. 이러한 지침은이 문서에 나와 있습니다.
   
   클러스터 리소스 관리자를 구성 하는 방법은 특정 Linux 배포에 따라 달라 집니다. 

   >[!IMPORTANT]
   >프로덕션 환경에서는 고가용성을 위해 STONITH 같은 펜스 에이전트를 해야 합니다. 이 문서의 예제 펜싱 에이전트를 사용 하지 마십시오. 테스트 및 유효성 검사에만 서로입니다. 
   
   >Pacemaker 클러스터 펜싱을 사용 하 여 알려진 상태로 클러스터를 반환 합니다. 펜싱을 구성 하는 방법은 배포 및 환경에 따라 달라 집니다. 이때 펜싱 일부 클라우드 환경에서 사용할 수 없는 경우 참조 [SUSE Linux Enterprise 고가용성 확장](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)합니다.

5. [가용성 그룹에 클러스터 리소스로 추가](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)합니다. 

## <a name="prerequisites"></a>필수 구성 요소

다음과 같은 종단 간 시나리오를 완료 하려면 3 개 노드 클러스터를 배포 하는 3 개의 컴퓨터가 필요 합니다. 다음 단계에는 이러한 서버를 구성 하는 방법을 간략하게 설명 합니다.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>설정 하 고 각 클러스터 노드에서 운영 체제를 구성 합니다. 

클러스터 노드에서 운영 체제를 구성 하는 첫 번째 단계가입니다. 이 연습 과정에 대 한 HA 추가 기능에 대 한 유효한 구독으로 SLES 12 s p 2를 사용 합니다.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 SQL Server 서비스를 구성 합니다.

1. 모든 노드의 SQL Server 서비스 설치 및 설정 합니다. 자세한 내용은 참조 [Linux에서 SQL Server 설치](sql-server-linux-setup.md)합니다.

1. 기본 및 다른 노드가 보조 복제본으로으로 노드 하나를 지정 합니다. 이 가이드 전체에서 이러한 용어를 사용 합니다.

1. 클러스터의 일부가 될 노드는 서로 통신할 수 있는지 확인 합니다.

   다음 예제와 `/etc/hosts` SLES1, SLES2, 및 SLES3 이라는 세 개의 노드를 추가 합니다.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   모든 클러스터 노드에 SSH를 통해 서로 액세스할 수 있어야 합니다. 도구와 같은 `hb_report` 또는 `crm_report` (에 대 한 문제 해결) 매의 기록 탐색기 노드간 passwordless SSH 액세스를 해야 하 고, 그렇지 않으면 이러한만 데이터를 수집할 수 현재 노드에서 합니다. 비표준 SSH 포트를 사용 하는 경우-X 옵션을 사용 합니다. (참조 `man` 페이지). SSH 포트 3479 이면 호출 예를 들어 한 `crm_report` 사용:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   자세한 내용은 참조는 [SLES 관리 가이드-기타 섹션](http://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)합니다.


## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker에 대 한 SQL Server 로그인 만들기

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Always On 가용성 그룹 구성

Linux 서버에 가용성 그룹을 구성 하 고 클러스터 리소스를 구성 합니다. 가용성 그룹을 구성 하려면 참조 [구성 Always On 가용성 그룹 Linux에서 SQL Server에 대 한](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 Pacemaker 구성

1. 항상 사용 가능한 확장을 설치

   참조를 참조 하세요. [SUSE Linux Enterprise Server를 설치 하 고 높은 가용성 확장](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. 두 노드에서 모두 SQL Server 리소스 에이전트 패키지를 설치 합니다.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>첫 번째 노드를 설정 합니다.

   참조 [SLES 설치 지침](http://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. 로 로그인 `root` 물리적 컴퓨터 또는 클러스터 노드로 사용 하려면 가상 컴퓨터에 있습니다.
2. 부트스트랩 스크립트를 실행 하 여 시작 합니다.
   ```bash
   sudo ha-cluster-init
   ```

   NTP 부팅 시간에 시작 하도록 구성 되지 않았습니다, 메시지가 나타납니다. 

   그래도 계속 하기로 스크립트가 자동으로 대 한 SSH 액세스 하며 Csync2 동기화 도구에 대 한 키를 생성 하 고 둘 다에 대해 필요한 서비스를 시작 합니다. 

3. 구성 하려면 클러스터 통신 계층 (Corosync): 

   a. 바인딩할 네트워크 주소를 입력 합니다. 기본적으로 스크립트에서는 t h 0의 네트워크 주소를 제안합니다. 또는 bond0의 주소 예를 들어 다른 네트워크 주소를 입력 합니다. 

   b. 멀티 캐스트 주소를 입력 합니다. 스크립트는 기본으로 사용할 수 있는 한 임의의 주소를 제안 합니다. 

   c. 멀티 캐스트 포트를 입력 합니다. 스크립트는 기본값으로 5405을 제안합니다. 

   d. 구성 하려면 `SBD ()`, SBD에 대 한 사용 하려는 차단 장치 파티션에 영구 경로 입력 합니다. 경로 클러스터의 모든 노드에서 일치 해야 합니다. 
   마지막으로 스크립트를 1 개 노드 클러스터를 온라인 상태로 전환 하 고 Hawk2의 웹 관리 인터페이스를 사용 하려면 Pacemaker 서비스를 시작 합니다. Hawk2에 사용할 URL은 화면에 표시 됩니다. 

4. 설치 프로세스에 대 한 세부 정보에 대 한 확인 `/var/log/sleha-bootstrap.log`합니다. 실행 1 노드 클러스터를 만들었습니다. Crm 상태와 함께 클러스터 상태를 확인 합니다.

   ```bash
   sudo crm status
   ```

   또한 구성 된 클러스터를 볼 수 있습니다 `crm configure show xml` 또는 `crm configure show`합니다.

5. 부트스트랩 절차에서는 암호 linux로 hacluster 라는 Linux 사용자를 만듭니다. 가능한 한 빨리 기본 암호를 안전한 것으로 바꿉니다. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>기존 클러스터에 노드 추가

하나 이상의 노드를 실행 하는 클러스터를 설정한 경우 ha 클러스터-조인 부트스트랩 스크립트와 함께 더 많은 클러스터 노드를 추가 합니다. 만 필요한 스크립트는 기존 클러스터 노드에 대 한 액세스 하 고 현재 컴퓨터에 기본 설치를 자동으로 완료 됩니다. 다음 단계를 따르십시오.

사용 하 여 기존 클러스터 노드를 구성한 경우는 `YaST` 모듈 클러스터를 실행 하기 전에 다음 선행 조건을 충족 되는지 확인 `ha-cluster-join`:
- 기존 노드에서 상의 루트 사용자에 SSH 키에 대 한 passwordless 로그인 합니다. 
- `Csync2` 기존 노드에서 구성 됩니다. 자세한 내용은 YaST와 Csync2 구성을 참조 하십시오. 

1. 물리적 컴퓨터 또는 가상 컴퓨터 클러스터에 가입 해야 하는 경우에 루트로 로그인 합니다. 
2. 부트스트랩 스크립트를 실행 하 여 시작 합니다. 

   ```bash
   sudo ha-cluster-join
   ```

   NTP 부팅 시간에 시작 하도록 구성 되지 않았습니다, 메시지가 나타납니다. 

3. 그래도 계속 하려는 경우 기존 노드의 IP 주소에 대해 묻는 메시지가 나타납니다. IP 주소를 입력 합니다. 

4. 두 컴퓨터 간의 passwordless SSH 액세스를 아직 구성 하지 있을 경우 기존 노드의 루트 암호 라는 메시지가 표시도 됩니다. 

   지정 된 노드에 로그인 한 후 스크립트 Corosync 구성을 복사, SSH 구성 및 `Csync2`, 새 클러스터 노드로 현재 컴퓨터 온라인으로 전환 합니다. 별개로 하더라도 매에 필요한 서비스를 시작 합니다. 공유 저장소를 구성한 경우 `OCFS2`에 대 한 "탑재 지점" 디렉터리를 자동으로 만듭니다는 `OCFS2` 파일 시스템입니다. 

5. 클러스터에 추가 하려는 모든 컴퓨터에 대해 이전 단계를 반복 합니다. 

6. 확인 프로세스의 자세한 `/var/log/ha-cluster-bootstrap.log`합니다. 

1. 에 대해 클러스터 상태를 확인 `sudo crm status`합니다. 두 번째 노드를 성공적으로 추가한 경우 출력이 다음과 같이 표시됩니다.

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` 초기 1 노드 클러스터 설치 중 구성 된 가상 IP 클러스터 리소스가입니다.

모든 노드를 추가한 후의 아니요-쿼럼-정책 전역 클러스터 옵션을 조정 해야 하는 경우를 확인 합니다. 이 2 노드 클러스터에 대 한 특히 중요 합니다. 자세한 내용은 옵션 no 쿼럼 정책 4.1.2, 섹션을 참조 합니다. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>클러스터 속성 클러스터-다시 확인-간격 설정

`cluster-recheck-interval` 리소스 매개 변수, 제약 조건 또는 기타 클러스터 옵션의 변경 내용에 대 한 클러스터를 확인 하는 폴링 간격을 나타냅니다. 클러스터를 연결 된 간격으로 복제본을 다시 시작 하려고 복제본의 작동이 중지 하는 경우는 `failure-timeout` 값 및 `cluster-recheck-interval` 값입니다. 예를 들어 경우 `failure-timeout` 60 초로 설정 되어 및 `cluster-recheck-interval` 설정 120 초로 다시 60 초 보다 작거나 120 초 보다 큰 간격으로 시도 됩니다. 60 초 및 클러스터-다시 확인-간격을 60 초 보다 큰 값을 실패 제한 시간을 설정 하는 것이 좋습니다. 클러스터 다시 확인 간격을 작은 값으로 설정 권장 되지 않습니다.

속성 값을 업데이트 하려면 `2 minutes` 실행:

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Pacemaker 클러스터에서 관리 하는 가용성 그룹 리소스가 이미 있는 경우에 최신 사용 가능한 Pacemaker 패키지 1.1.18-11.el7를 사용 하는 모든 분포 인해 경우 설정을 시작 실패-은-치명적이 지 클러스터에 대 한 동작 변경 하는지 유의 해당 값은 false입니다. 이 변경은 장애 조치 워크플로가 영향을 줍니다. 주 복제본에 중단 되, 사용 가능한 보조 복제본 중 하나로 장애 조치 클러스터 사용할 수 있습니다. 대신, 사용자가 클러스터 유지 실패 한 주 복제본을 시작 하려는 것을 알 수 있습니다. 해당 기본 하지 온라인 상태가 된 경우 (으로 인해 영구 작동 중단)를 클러스터 하지 장애 조치 다른 사용 가능한 보조 복제본으로 합니다. 이러한 변경으로 인해 시작 실패-은-치명적이 지 설정 하려면 이전에 권장 되는 구성이 더 이상 유효 하 고 설정의 기본 값으로 다시 되돌릴 수 해야 `true`합니다. AG 리소스를 포함 하도록 업데이트 해야 하는 또한는 `failover-timeout` 속성입니다. 
>
>속성 값을 업데이트 하려면 `true` 실행:
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>기존 AG 리소스 속성을 업데이트 `failure-timeout` 를 `60s` 실행 (대체 `ag1` 가용성 그룹 리소스의 이름으로): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Pacemaker 클러스터 속성에 대 한 자세한 내용은 참조 하십시오. [클러스터 리소스 구성](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html)합니다.

# <a name="configure-fencing-stonith"></a>펜스 (STONITH) 구성
Pacemaker 클러스터 공급 업체를 사용 하도록 설정할 STONITH와 지원 되는 클러스터 설치에 대해 구성 된 펜싱 장치에 필요 합니다. 클러스터 리소스 관리자 상태 노드 또는 노드에 있는 리소스의을 확인할 수 없는 경우 펜싱 클러스터도 알려진 상태로 다시 전환 하는 데 사용 됩니다.

리소스 수준 펜싱 하면 주로 리소스를 구성 하 여 가동 중단 시 데이터 손상 되지 않습니다. 리소스 수준 펜싱을 사용할 수 있습니다 예를 들어, 오래 된 경우 처럼 노드에서 디스크를 표시 하려면 (복제 블록 장치 Distributed) DRBD와 통신 링크의 작동이 중지 합니다.

노드 수준 펜싱 하면 노드 모든 리소스를 실행 하지 않습니다. 노드를 다시 설정 하 여 이렇게 및는 Pacemaker 구현의 STONITH (있음 "헤드에 있는 다른 노드가 해결"에 대 한 의미) 라고 합니다. Pacemaker 다양 한 방어 서버는 무정전 전원 공급 장치 또는 관리 인터페이스 카드와 같은 장치를 지원 합니다.

자세한 내용은 참조 [처음부터 Pacemaker 클러스터](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html), [펜싱 및 Stonith](http://clusterlabs.org/doc/crm_fencing.html) 및 [SUSE HA 설명서: 펜싱 및 STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html)합니다.

클러스터 초기화 시 STONITH 구성이 없는 검색 된 경우 비활성화 됩니다. 다음 명령을 실행 하 여 나중에 사용할 수 있습니다.

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>테스트 목적으로 하는 데 않습니다 STONITH를 사용 하지 않도록 설정 합니다. Pacemaker 프로덕션 환경에서 사용 하려는 경우 환경에 따라 STONITH 구현을 계획 하 고 사용 하도록 설정 유지 해야 합니다. SUSE 모든 클라우드 환경 (Azure 포함) 또는 Hyper-v에 대 한 펜스 에이전트를 제공 하지 않습니다. 검사가 클러스터 공급 업체는 이러한 환경에서 실행 중인 프로덕션 클러스터에 대 한 지원을 제공 하지 않습니다. 제작 하는 이후 릴리스에서 사용할 수 있는 이러한 차이 대 한 솔루션입니다.


## <a name="configure-the-cluster-resources-for-sql-server"></a>SQL Server에 대 한 클러스터 리소스를 구성 합니다.

참조 [SLES 관리 Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

### <a name="create-availability-group-resource"></a>가용성 그룹 리소스 만들기

다음 명령의 만들고 가용성 그룹 [ag1]의 세 개의 복제본에 대 한 가용성 그룹 리소스를 구성 합니다. 작업 모니터 및 시간 제한 기반으로 인지 시간 제한 수준이 높은 작업 부하에 따라 변하는 및 각 배포에 대해 신중 하 게 조정 해야 할 SLES에 명시적으로 지정할 수 있어야 합니다.
클러스터의 노드 중 하나에서 명령을 입력 합니다.

1. 실행 `crm configure` crm 프롬프트를 엽니다.

   ```bash
   sudo crm configure 
   ```

1. Crm 프롬프트 리소스 속성을 구성 하려면 다음 명령을 실행 합니다.

   ```bash
   primitive ag_cluster \
      ocf:mssql:ag \
      params ag_name="ag1" \
      meta failure-timeout=60s \
      op start timeout=60s \
      op stop timeout=60s \
      op promote timeout=60s \
      op demote timeout=10s \
      op monitor timeout=60s interval=10s \
      op monitor timeout=60s interval=11s role="Master" \
      op monitor timeout=60s interval=12s role="Slave" \
      op notify timeout=60s
   ms ms-ag_cluster ag_cluster \
      meta master-max="1" master-node-max="1" clone-max="3" \
     clone-node-max="1" notify="true" \
   commit
      ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>가상 IP 리소스 만들기

경우 만들지 않은 가상 IP 리소스를 실행할 때 `ha-cluster-init` 이제이 리소스를 만들 수 있습니다. 다음 명령은 가상 IP 리소스를 만듭니다. 대체 `<**0.0.0.0**>` 네트워크에서 사용 가능한 주소와 및 `<**24**>` 와 CIDR 서브넷 마스크의 비트 수입니다. 노드 하나에서 실행 합니다.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>공동 배치 제약 조건 추가
Pacemaker 클러스터에서 리소스를 실행할 위치를 선택 하는 등 거의 모든 의사 결정은 점수를 비교 하 여 수행 됩니다. 리소스 당 점수가 계산 되 고 클러스터 리소스 관리자가 특정 리소스에 대 한 점수가 가장 높은 있는 노드를 선택 합니다. (한 노드에 리소스에 대 한 음수 점수 있으면 리소스 실행할 수 없습니다 해당 노드에서.) 제약 조건 사용 하 여 클러스터의 결정을 조작할 수 있습니다. 제한에는 점수는. 제약 조건에 무한대 보다 낮은 점수를 경우만 권장 사항입니다. 무한대의 점수는 필수 사항 의미 합니다. 기본 가용성 그룹 및 가상 ip 리소스는 실행 되도록 동일한 호스트에서 무한대의 점수와 공동 배치 제약 조건 정의 하므로 하려고 합니다. 

마스터와 같은 노드에를 실행 하는 가상 IP에 대 한 공동 배치 제약을 설정 하려면 노드 하나에서 다음 명령을 실행 합니다.

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>순서 지정 제약 조건 추가
공동 배치 제약 조건을는 암시적 순서 지정 제약 합니다. 가용성 그룹 리소스를 이동 하기 전에 가상 IP 리소스를 이동 합니다. 기본적으로 이벤트의 순서는 같습니다. 

1. 사용자 문제 리소스 노드 2로 노드 1에서 가용성 그룹 마스터 마이그레이션합니다.
2. 노드 1에서 가상 IP 리소스를 중지합니다.
3. 가상 IP 리소스 노드 2에서 시작합니다. 이 시점에서 IP 주소 일시적으로 노드 2 가리키는 노드 2는 여전히 이전 장애 조치 하는 동안 보조 합니다. 
4. 노드 1에서 가용성 그룹 마스터 슬레이브 강등 합니다.
5. 노드 2에서 가용성 그룹 슬레이브 승격를 마스터 합니다. 

IP 주소를 장애 조치 이전 보조 서버와 노드를 가리키는 일시적으로 방지 하려면 정렬 제약 조건을 추가 합니다. 정렬 제약을 추가 하려면 노드 하나에서 다음 명령을 실행 합니다. 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>클러스터를 구성 하 고를 클러스터 리소스로 가용성 그룹을 추가한 후 TRANSACT-SQL 장애 조치할 가용성 그룹 리소스를 사용할 수 없습니다. Linux에서 SQL Server 클러스터 리소스 Windows Server 장애 조치 클러스터 (WSFC)에 운영 체제와 엄격히 결합 되지 됩니다. SQL Server 서비스가 클러스터의 사용 여부 인식 하지 않습니다. 모든 오케스트레이션 클러스터 관리 도구를 통해 수행 됩니다. SLES에서 사용 하 여 `crm`합니다. 

수동으로 가용성 그룹을 장애 조치할 `crm`합니다. TRANSACT-SQL로 장애 조치의 시작 하지 마십시오. 자세한 내용은 참조 [장애 조치](sql-server-linux-availability-group-failover-ha.md#failover)합니다.


참조 항목:
- [클러스터 리소스 관리](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm)합니다.   
- [HA 개념](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Pacemaker 빠른 참조](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>다음 단계

[HA 가용성 그룹 동작](sql-server-linux-availability-group-failover-ha.md)
