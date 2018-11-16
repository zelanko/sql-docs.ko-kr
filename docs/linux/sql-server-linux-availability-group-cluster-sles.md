---
title: SQL Server 가용성 그룹에 대 한 SLES 클러스터 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: 3db679a5df861cbdbf08443b5fdd85e99b01d3b3
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670622"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>SQL Server 가용성 그룹에 대 한 SLES 클러스터 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 가이드는 SQL Server의 Enterprise Server SLES (SUSE Linux) 12 SP2에 대 한 3 개 노드 클러스터를 만드는 지침을 제공 합니다. 고가용성을 위해 Linux에서 가용성 그룹을 필요한 3 개의 노드가-참조 [가용성 그룹 구성에 대 한 높은 가용성 및 데이터 보호](sql-server-linux-availability-group-ha.md)합니다. SUSE 클러스터링 계층 더해서 [높은 가용성 확장 (HAE)](https://www.suse.com/products/highavailability) 기반으로 구축 [Pacemaker](https://clusterlabs.org/)합니다. 

클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대 한 자세한 내용은 참조 하세요. [SUSE Linux Enterprise 높은 가용성 확장 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)합니다.

>[!NOTE]
>이 시점에서 Linux의 Pacemaker 사용 하 여 SQL Server의 통합은 Windows에 WSFC를 사용 하 여으로 결합 없습니다. Linux의 SQL Server 서비스가 클러스터 인식 아닙니다. Pacemaker는 클러스터 리소스를 가용성 그룹 리소스를 포함 하 여 오케스트레이션의 모든 제어 합니다. Linux에서 하지 항상에서 가용성 그룹 동적 관리 뷰 (Dmv) sys.dm_hadr_cluster 같은 클러스터 정보를 제공 하는에서 사용 해야 합니다. 또한 가상 네트워크 이름은 WSFC 관련, Pacemaker에 동일한 동등한 옵션이 없습니다. 장애 조치 후 투명 하 게 연결에 사용 하려면 수신기를 만들 수 있습니다 하지만 (다음 섹션에서 설명)으로 가상 IP 리소스를 만드는 데 사용 된 IP를 사용 하 여 DNS 서버에서 수신기 이름의 수동으로 등록 해야 합니다.


## <a name="roadmap"></a>로드맵

고가용성을 위해 가용성 그룹을 만드는 절차는 Windows Server 장애 조치 클러스터 및 Linux 서버 간에 다릅니다. 다음과 같은 단계를 간략히 설명 합니다. 

1. [SQL Server 클러스터 노드에서 구성](sql-server-linux-setup.md)합니다.

2. [가용성 그룹을 만들](sql-server-linux-availability-group-failover-ha.md)합니다. 

3. Pacemaker와 같은 클러스터 리소스 관리자를 구성 합니다. 이러한 지침은이 문서에 있습니다.
   
   클러스터 리소스 관리자를 구성 하는 방법은 특정 Linux 배포에 따라 달라 집니다. 

   >[!IMPORTANT]
   >프로덕션 환경에 같은 고가용성에 대 한 STONITH는 펜싱 에이전트가 필요합니다. 이 문서의 예제는 펜싱 에이전트를 사용 하지 마세요. 테스트 및 유효성 검사에만 됩니다. 
   
   >Pacemaker 클러스터는 클러스터를 알려진된 상태로 반환할 펜싱을 사용 합니다. 펜스를 구성 하는 방법은 배포 및 환경에 따라 달라 집니다. 이때 펜싱 일부 클라우드 환경에서는 제공 되지 않습니다. 참조 [SUSE Linux Enterprise 고가용성 확장](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)합니다.

5. [가용성 그룹에 클러스터 리소스로 추가](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)합니다. 

## <a name="prerequisites"></a>필수 구성 요소

다음 종단 간 시나리오를 완료 하려면 세 개의 머신을 세 개의 노드 클러스터를 배포 해야 합니다. 다음 단계에는 이러한 서버를 구성 하는 방법을 간략하게 설명 합니다.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>설정 하 고 각 클러스터 노드의 운영 체제를 구성 합니다. 

먼저는 클러스터 노드의 운영 체제를 구성 하는 것입니다. 이 연습에서는 대 한 유효한 구독을 사용 하 여 SLES 12 SP2를 사용 하 여 HA 추가 기능에 대 한 합니다.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 SQL Server 서비스를 구성 합니다.

1. 설치 하 고 모든 노드에서 SQL Server 서비스를 설정 합니다. 자세한 지침은 [Linux의 SQL Server 설치](sql-server-linux-setup.md)합니다.

1. 보조 복제본으로 주 및 기타 노드로 노드 하나를 지정 합니다. 이 가이드 전체에서 이러한 용어를 사용 합니다.

1. 클러스터의 일부가 될 예정인 노드가 서로 통신할 수 있는지 확인 합니다.

   다음 예제에서는 `/etc/hosts` SLES1, 그 다음에 SLES2, 및 SLES3 라는 세 개의 노드를 추가 합니다.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   모든 클러스터 노드에 SSH를 통해 서로 액세스할 수 있어야 합니다. 와 같은 도구 `hb_report` 또는 `crm_report` (문제 해결 용) Hawk의 History Explorer 노드 간에 암호 없는 SSH 액세스가 필요 하 고, 그렇지 않으면 이러한만 데이터를 수집할 수 현재 노드에서 합니다. 비표준 SSH 포트를 사용 하는 경우-X 옵션을 사용 합니다. (참조 `man` 페이지). 예를 들어 SSH 포트가 3479 이면 호출을 `crm_report` 사용 하 여:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   자세한 내용은 참조는 [SLES 관리 가이드-기타 섹션](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)합니다.


## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker 용 SQL Server 로그인 만들기

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Always On 가용성 그룹 구성

Linux 서버에서 가용성 그룹을 구성 하 고 그런 다음 클러스터 리소스를 구성 합니다. 가용성 그룹을 구성 하려면 참조 [구성 Always On 가용성 그룹 SQL Server Linux에 대 한](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 Pacemaker 구성

1. 고가용성 확장 설치

   참조를 참조 하십시오 [SUSE Linux Enterprise Server를 설치 하 고 높은 가용성 확장](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. 두 노드에서 모두 SQL Server 리소스 에이전트 패키지를 설치 합니다.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>첫 번째 노드 설정

   참조 [SLES 설치 지침](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. 으로 로그인 `root` 물리적 또는 가상 머신 클러스터 노드로 사용 하려면.
2. 부트스트랩 스크립트를 실행 하 여 시작 합니다.
   ```bash
   sudo ha-cluster-init
   ```

   NTP 부팅 시 시작 되도록 구성 되지 않았습니다, 메시지가 나타납니다. 

   계속 하려는 경우 스크립트를 자동으로 Csync2 동기화 도구에 대 한 SSH 액세스를 위한 키를 생성 하 고 둘 다에 대해 필요한 서비스를 시작 합니다. 

3. 클러스터 통신 계층 (Corosync)를 구성 합니다. 

   1. 에 바인딩할 네트워크 주소를 입력 합니다. 기본적으로 스크립트에서는 eth0의 네트워크 주소를 제안합니다. 또는 bond0 주소의 예를 들어 다른 네트워크 주소를 입력 합니다. 

   2. 멀티 캐스트 주소를 입력 합니다. 스크립트는 기본적으로 사용할 수 있는 임의 주소를 제안 합니다. 

   c. 멀티 캐스트 포트를 입력 합니다. 스크립트는 기본적으로 5405을 제안합니다. 

   d. 구성 하려면 `SBD ()`, SBD에 사용 하려는 차단 장치 파티션에 영구 경로 입력 합니다. 경로 클러스터의 모든 노드 간에 일치 해야 합니다. 
   마지막으로 스크립트 1 개 노드 클러스터를 온라인 상태로 전환 하 고 Hawk2 웹 관리 인터페이스를 사용 하도록 설정 하려면 Pacemaker 서비스를 시작 됩니다. Hawk2에 사용할 URL은 화면에 표시 됩니다. 

4. 설치 프로세스의 세부 정보를 확인 `/var/log/sleha-bootstrap.log`합니다. 이제 실행 1 개 노드 클러스터가 생깁니다. Crm 상태를 사용 하 여 클러스터 상태를 확인 합니다.

   ```bash
   sudo crm status
   ```

   클러스터 구성을 사용 하 여 확인할 수 있습니다 `crm configure show xml` 또는 `crm configure show`합니다.

5. 부트스트랩 절차에서는 hacluster 암호 linux 사용 하 여 명명 된 Linux 사용자를 만듭니다. 가능한 한 빨리 기본 암호를 안전한 것으로 바꿉니다. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>기존 클러스터에 노드 추가

하나 이상의 노드를 사용 하 여 실행 하는 클러스터를 사용 하는 경우 ha 클러스터-가입 부트스트랩 스크립트를 사용 하 여 더 많은 클러스터 노드를 추가 합니다. 만 필요한 스크립트는 기존 클러스터 노드에 액세스 하 고 현재 컴퓨터의 기본 설치를 자동으로 완료 됩니다. 다음 단계를 사용 합니다.

사용 하 여 기존 클러스터 노드를 구성한 경우 합니다 `YaST` 모듈을 클러스터를 실행 하기 전에 다음 필수 조건이 충족 되는지 확인 `ha-cluster-join`:
- 기존 노드에서 루트 사용자 암호 없는 로그인에 대 한 위치에 SSH 키 
- `Csync2` 기존 노드에서 구성 됩니다. 자세한 내용은 YaST 사용 하 여 Csync2 구성을 참조 하세요. 

1. 물리적 컴퓨터 또는 클러스터에 가입 하도록 해야 하는 가상 컴퓨터를 루트로 로그인 합니다. 
2. 부트스트랩 스크립트를 실행 하 여 시작 합니다. 

   ```bash
   sudo ha-cluster-join
   ```

   NTP 부팅 시 시작 되도록 구성 되지 않았습니다, 메시지가 나타납니다. 

3. 계속 진행 하려는 경우 기존 노드의 IP 주소에 대해 묻는 메시지가 나타납니다. IP 주소를 입력 합니다. 

4. 두 컴퓨터 간에 암호 없는 SSH 액세스를 아직 구성 하지 않은 경우 기존 노드의 루트 암호에 대 한 라는 메시지가 표시도 됩니다. 

   지정 된 노드에 로그인 한 후 스크립트 Corosync 구성을 복사, SSH 구성 및 `Csync2`, 새 클러스터 노드로 온라인 현재 컴퓨터를 가져옵니다. 외에도, Hawk에 필요한 서비스를 시작 합니다. 사용 하 여 공유 저장소를 구성한 경우 `OCFS2`, 탑재 지점 디렉터리를 자동으로 만듭니다는 `OCFS2` 파일 시스템입니다. 

5. 클러스터에 추가 하려는 모든 컴퓨터에 대해 이전 단계를 반복 합니다. 

6. 확인 프로세스의 자세한 `/var/log/ha-cluster-bootstrap.log`합니다. 

1. 사용 하 여 클러스터 상태 확인 `sudo crm status`합니다. 두 번째 노드를 성공적으로 추가한 경우 출력이 다음과 같이 표시됩니다.

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` 초기 단일 노드 클러스터 설치 중 구성 된 가상 IP 클러스터 리소스가입니다.

모든 노드를 추가한 후 없음-쿼럼-정책에 전역 클러스터 옵션을 조정 해야 하는 경우를 확인 합니다. 이 2 노드 클러스터에 대 한 특히 중요 합니다. 자세한 내용은 섹션 4.1.2, 옵션 없음-쿼럼-정책을 참조 하세요. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>클러스터 속성 클러스터-다시 확인-간격 설정

`cluster-recheck-interval` 리소스 매개 변수, 제약 조건 또는 다른 클러스터 옵션에 대 한 변경 내용에 대 한 클러스터 확인 하는 폴링 간격을 나타냅니다. 클러스터를 연결 된 간격으로 복제본을 다시 시작 하려고 복제본이 다운 되 면 합니다 `failure-timeout` 값 및 `cluster-recheck-interval` 값입니다. 예를 들어 경우 `failure-timeout` 60 초로 설정 됩니다 및 `cluster-recheck-interval` 설정 120 초 이내 60 초 보다 큰 간격을 120 초로 다시 시작 시도 됩니다. 오류 제한 60s와 클러스터-다시 확인-간격은 60 초 보다 큰 값으로 설정 하는 것이 좋습니다. 클러스터 다시 확인 간격을 작은 값으로 설정 하는 것은 좋지 않습니다.

속성 값을 업데이트 하려면 `2 minutes` 실행:

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Pacemaker 클러스터에서 관리 하는 가용성 그룹 리소스가 이미 있는 경우에 최신 사용 가능한 Pacemaker 패키지 1.1.18-11.el7를 사용 하는 모든 분산 발생 경우 설정을 시작 실패-는-치명적이 지 클러스터에 대 한 동작 변경 참고 해당 값은 false입니다. 이 변경에 장애 조치 워크플로 적용 합니다. 주 복제본 중단이 발생 하는 경우 클러스터는 사용 가능한 보조 복제본 중 하나에 장애 조치 해야 합니다. 대신 사용자 클러스터 유지 실패 한 주 복제본을 시작 하는 것을 알 수 있습니다. 해당 기본 되지 온라인 상태가 되 면 (때문에 영구 작동 중단)를 클러스터 하지 장애 조치 다른 사용 가능한 보조 복제본으로 합니다. 이러한 변경으로 인해 시작 실패-는-치명적이 지 설정 하려면 이전에 권장 되는 구성이 더 이상 유효 하며 설정의 기본 값으로 다시 되돌릴 `true`합니다. AG 리소스를 포함 하도록 업데이트 해야 하는 또한는 `failover-timeout` 속성입니다. 
>
>속성 값을 업데이트 하려면 `true` 실행:
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>기존 AG 리소스 속성을 업데이트 `failure-timeout` 하 `60s` 실행 (대체 `ag1` 가용성 그룹 리소스의 이름): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Pacemaker 클러스터 속성에 대 한 자세한 내용은 참조 하세요. [클러스터 리소스가 구성](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html)합니다.

## <a name="configure-fencing-stonith"></a>펜싱 (STONITH) 구성
Pacemaker 클러스터 공급 업체는 STONITH를 사용 하도록 설정 및 지원 되는 클러스터 설치를 구성 하는 펜싱 장치에 필요 합니다. Cluster resource manager는 노드 또는 노드 리소스의 상태를 확인할 수 없습니다, 하는 경우 펜스를 알려진된 상태로 클러스터를 다시 표시 하려면 사용 됩니다.

리소스 수준 펜싱 주로 리소스를 구성 하 여 중단 시간 동안 데이터 손상이 없는지 있는지 확인 합니다. 리소스 수준 펜싱을 사용할 수 있습니다 예를 들어, 오래 된 경우 처럼 노드에서 디스크를 표시 하려면 (복제 된 블록 장치 Distributed) DRBD를 사용 하 여 통신 링크 중단 합니다.

노드 수준 펜싱 노드 리소스 실행 되지 않도록 보장 합니다. 노드를 다시 설정 하 여 이렇게 하 고는 Pacemaker 구현의 STONITH (약자인 "헤드에 있는 다른 노드가 특이") 이라고 합니다. 키를 누릅니다. Pacemaker는 다양 한 서버는 무정전 전원 공급 장치 또는 관리 인터페이스 카드와 같은 장치 펜싱을 지원 합니다.

자세한 내용은 [부터 Pacemaker 클러스터](https://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html), [펜싱 및 Stonith](https://clusterlabs.org/doc/crm_fencing.html) 하 고 [SUSE HA 설명서: 펜싱 및 STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html)합니다.

클러스터 초기화 시 STONITH 구성이 감지 되 면 비활성화 됩니다. 다음 명령을 실행 하 여 나중에 활성화할 수 있습니다.

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>STONITH를 사용 하지 않도록 설정 하는 것은 테스트 목적에 대해서만 합니다. 프로덕션 환경에서 Pacemaker를 사용 하려는 경우 환경에 따라 STONITH 구현 계획을 계속 사용 합니다. SUSE는 모든 클라우드 환경 (Azure 포함) 또는 Hyper-v에 대 한 펜스 에이전트를 제공 하지 않습니다. 검사가 클러스터 공급 업체는 이러한 환경에서 실행 중인 프로덕션 클러스터에 대 한 지원을 제공 하지 않습니다. 이후 릴리스에서 제공 되는이 간격에 대 한 솔루션을 제작 하는 합니다.


## <a name="configure-the-cluster-resources-for-sql-server"></a>SQL Server에 대 한 클러스터 리소스를 구성 합니다.

참조 [SLES 관리 Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

## <a name="enable-pacemaker"></a>Pacemaker를 사용 하도록 설정

자동으로 시작 되도록 Pacemaker를 사용 하도록 설정 합니다.

클러스터의 모든 노드에서 다음 명령을 실행 합니다.

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>가용성 그룹 리소스 만들기

명령을 만들고 세 개의 복제본 가용성 그룹 [ag1]에 대 한 가용성 그룹 리소스를 구성 합니다. 모니터링 작업 및 시간 제한 기반 사실에 시간 제한 수준이 높은 워크 로드에 따라 다릅니다 및 각 배포에 대해 신중 하 게 조정 해야 SLES에서 명시적으로 지정할 수 있어야 합니다.
클러스터의 노드 중 하나에서 명령을 입력 합니다.

1. 실행 `crm configure` crm 프롬프트를 엽니다.

   ```bash
   sudo crm configure 
   ```

1. Crm 프롬프트가 표시 되 면 리소스 속성을 구성 하려면 다음 명령을 실행 합니다.

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

경우 만들지 않고 가상 IP 리소스를 실행할 때 `ha-cluster-init` 이제이 리소스를 만들 수 있습니다. 다음 명령은 가상 IP 리소스를 만듭니다. 바꿉니다 `<**0.0.0.0**>` 네트워크에서 사용 가능한 주소를 사용 하 여 및 `<**24**>` CIDR 서브넷 마스크의 비트 수를 사용 하 여 합니다. 하나의 노드에서 실행 합니다.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>공동 배치 제약 조건 추가
Pacemaker 클러스터에서 리소스를 실행할 위치를 선택 하는 등 거의 모든 의사 결정은 점수를 비교 하 여 수행 됩니다. 리소스 당 점수 계산 하 고 클러스터 리소스 관리자가 특정 리소스에 대 한 점수가 가장 높은 노드를 선택 합니다. (노드는 리소스에 대 한 음수 점수 있으면 리소스 수 없습니다. 해당 노드에서 실행 합니다.) 에서는 제약 조건 사용 하 여 클러스터의 결정을 조작할 수 있습니다. 제한에는 점수는. 제약 조건에는 무한대 보다 낮은 점수를 인지만 권장 합니다. 무한대의 점수를 반드시 것을 의미 합니다. 기본 가용성 그룹 및 가상 ip 리소스 실행 되는지 확인 동일한 호스트에서 무한대의 점수를 사용 하 여 공동 배치 제약 조건을 정의 하도록 하려고 합니다. 

마스터와 동일한 노드에서 실행 되도록 가상 IP에 대 한 공동 배치 제약을 설정 하려면 노드 하나에서 다음 명령을 실행 합니다.

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>정렬 제약 조건을 추가 합니다.
공동 배치 제약 조건을 암시적 순서 제약 조건이 있습니다. 가용성 그룹 리소스를 이동 하기 전에 가상 IP 리소스를 이동 합니다. 기본적으로 이벤트 순서는: 

1. 사용자 문제 리소스 가용성 그룹 마스터 노드 2에는 node1에서 마이그레이션합니다.
2. 가상 IP 리소스를 노드 1에서 중지합니다.
3. 가상 IP 리소스를 노드 2에서 시작합니다. 이 시점에서 IP 주소 일시적으로 노드 2에는 지점 2 노드는 여전히 이전 장애 조치 하는 동안 보조 합니다. 
4. 노드 1에서 마스터 되는 가용성 그룹에 복제본이 슬레이브를 강등 합니다.
5. 가용성 그룹 슬레이브 노드 2에서 수준이 master입니다. 

IP 주소를 사전 장애 조치 보조 노드를 일시적으로 가리키는 방지 하려면 정렬 제약 조건을 추가 합니다. 정렬 제약 조건을 추가할 노드 하나에서 다음 명령을 실행 합니다. 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>클러스터를 구성 하 고를 클러스터 리소스로 가용성 그룹을 추가한 후에 가용성 그룹 리소스를 장애 조치할 Transact SQL을 사용할 수 없습니다. Linux의 SQL Server 클러스터 리소스 연계 되지 않습니다와 긴밀 하 게 운영 체제에는 서버 장애 조치 클러스터 (WSFC (Windows) 같습니다. SQL Server 서비스를 클러스터의 현재 상태 인식 없습니다. 모든 오케스트레이션은 클러스터 관리 도구를 통해 수행 됩니다. SLES에서 사용 하 여 `crm`입니다. 

수동으로 가용성 그룹 장애 조치할 `crm`합니다. TRANSACT-SQL을 사용 하 여 장애 조치를 시작 하지 마십시오. 자세한 내용은 [장애 조치](sql-server-linux-availability-group-failover-ha.md#failover)합니다.


참조 항목:
- [클러스터 리소스 관리](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm)합니다.   
- [HA 개념](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Pacemaker 빠른 참조](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>다음 단계

[HA 가용성 그룹을 작동](sql-server-linux-availability-group-failover-ha.md)
