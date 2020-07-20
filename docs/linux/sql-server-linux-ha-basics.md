---
title: Linux 배포의 SQL Server 고가용성
description: Always On 가용성 그룹, FCI(장애 조치(failover) 클러스터 인스턴스), 로그 전달 등 SQL Server on Linux에 사용할 수 있는 고가용성 옵션을 알아봅니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 67a5219e955ccd9d4b0303276823d8cafbce4963
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196856"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Linux 배포의 SQL Server 가용성 기본 사항

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]부터 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]는 Linux 및 Windows에서 모두 지원됩니다. Windows 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포와 마찬가지로 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 데이터베이스 및 인스턴스는 Linux에서 가용성이 높아야 합니다. 이 문서에서는 Windows 기반 설치의 일부 차이뿐만 아니라 고가용성 Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 데이터베이스 및 인스턴스를 계획하고 배포하는 기술적 측면을 설명합니다. Linux 전문가는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 처음 사용하고 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 전문가는 Linux를 처음 사용할 수 있으므로 이 문서에서는 때때로 일부 사용자에게는 익숙하고 다른 사용자에게는 익숙하지 않을 수 있는 개념을 소개합니다.

## <a name="ssnoversion-md-availability-options-for-linux-deployments"></a>Linux 배포에 대한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 가용성 옵션
백업 및 복원 외에도 Windows 기반 배포와 동일한 세 가지 가용성 기능을 Linux에서 사용할 수 있습니다.
-   Always On AG(가용성 그룹)
-   Always On FCI(장애 조치(failover) 클러스터 인스턴스)
-   [로그 전달](sql-server-linux-use-log-shipping.md)

Windows에서 FCI에는 항상 기본 WSFC(Windows Server 장애 조치(failover) 클러스터)가 필요합니다. 배포 시나리오에 따라 AG에는 일반적으로 기본 WSFC가 필요합니다. 단, [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]에는 새로운 없음 변형이 포함됩니다. Linux에는 WSFC가 없습니다. Linux의 클러스터링 구현은 [Linux의 Always On 가용성 그룹 및 장애 조치(failover) 클러스터 인스턴스에 대한 Pacemaker](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux) 섹션에서 설명합니다.

## <a name="a-quick-linux-primer"></a>빠른 Linux 입문
일부 Linux 설치는 인터페이스와 함께 설치될 수 있지만 대부분의 경우에는 함께 설치되지 않습니다. 즉, 운영 체제 계층의 거의 모든 항목은 명령줄을 통해 설치됩니다. 일반적으로 Linux 환경에서 이 명령줄은 ‘bash 셸’이라는 용어로 사용됩니다.

Windows Server에서 많은 작업을 관리자 권한으로 수행해야 하는 것처럼 Linux에서는 많은 명령을 상승된 권한으로 실행해야 합니다. 상승된 권한으로 실행해야 하는 두 가지 주요 방법이 있습니다.
1. 적절한 사용자의 컨텍스트에서 실행합니다. 다른 사용자로 변경하려면 `su` 명령을 사용합니다. 사용자 이름 없이 `su`만 실행되는 경우 암호를 알고 있다면 이제 ‘루트’로 셸에 있는 것입니다.
   
2. 명령을 실행하는 더 일반적이고 보안이 고려된 방법은 실행하기 전에 `sudo`를 사용하는 것입니다. 이 문서의 많은 예제에서는 `sudo`를 사용합니다.

몇 가지 일반적인 명령은 각각 온라인으로 조사할 수 있는 다양한 스위치 및 옵션을 포함합니다.
-   `cd` - 디렉터리 변경
-   `chmod` - 파일 또는 디렉터리의 권한 변경
-   `chown` - 파일 또는 디렉터리의 소유권 변경
-   `ls` - 디렉터리의 콘텐츠 표시
-   `mkdir` - 드라이브에 폴더(디렉터리) 만들기
-   `mv` - 파일을 다른 위치로 이동
-   `ps` - 모든 작업 프로세스 표시
-   `rm` - 서버에서 로컬로 파일 삭제
-   `rmdir` - 폴더(디렉터리) 삭제
-   `systemctl` - 서비스 시작, 중지 또는 사용
-   텍스트 편집기 명령입니다. Linux에는 vi 및 emacs와 같은 다양한 텍스트 편집기 옵션이 있습니다.

## <a name="common-tasks-for-availability-configurations-of-ssnoversion-md-on-linux"></a>Linux에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 가용성 구성에 대한 일반 작업
이 섹션에서는 모든 Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포에 공통적인 작업에 대해 설명합니다.

### <a name="ensure-that-files-can-be-copied"></a>파일을 복사할 수 있는지 확인
한 서버에서 다른 서버로 파일을 복사하는 작업은 Linux에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 사용하는 사용자가 수행할 수 있어야 합니다. 이 작업은 AG 구성에 매우 중요합니다.

권한 문제와 같은 항목은 Windows 기반 설치뿐 아니라 Linux에도 있을 수 있습니다. 그러나 Windows에서 서버 간에 복사하는 방법에 익숙한 사용자는 Linux에서 복사하는 방법에 익숙하지 않을 수 있습니다. 일반적인 방법은 Secure Copy의 약어인 명령줄 유틸리티 `scp`를 사용하는 것입니다. 내부적으로는 `scp`는 OpenSSH를 사용합니다. SSH는 Secure Shell의 약어입니다. Linux 배포에 따라 OpenSSH 자체가 설치되지 않을 수 있습니다. 그렇지 않으면 OpenSSH가 먼저 설치되어야 합니다. OpenSSH 구성에 대한 자세한 내용은 각 배포에 대한 다음 링크의 정보를 참조하세요.
-   [Red Hat Enterprise Linux(RHEL)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server(SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

`scp`를 사용할 때 원본 또는 대상이 아닌 경우에는 서버의 자격 증명을 제공해야 합니다. 예를 들어 다음을 사용하면

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

MyAGCert.cer 파일이 다른 서버에 지정된 폴더로 복사됩니다. 복사하려면 파일에 대한 권한 및 소유권이 있어야 하므로 복사하기 전에 `chown`을 채택해야 할 수도 있습니다. 마찬가지로 받는 쪽에 있는 해당 사용자는 파일을 조작하려면 액세스 권한이 필요합니다. 예를 들어 해당 인증서 파일을 복원하려면 `mssql` 사용자가 해당 파일에 액세스할 수 있어야 합니다.

SMB(서버 메시지 블록)의 Linux 변형인 Samba는 UNC 경로(예: `\\SERVERNAME\SHARE`)를 통해 액세스하는 공유를 만드는 데 사용될 수도 있습니다. Samba 구성에 대한 자세한 내용은 각 배포에 대한 다음 링크의 정보를 참조하세요.
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Windows 기반 SMB 공유를 사용할 수도 있으며, Samba의 클라이언트 부분이 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 호스트하는 Linux 서버에서 제대로 구성되고 공유에 적절한 액세스 권한이 있는 경우에는 SMB 공유가 Linux 기반일 필요가 없습니다. 혼합 환경에 있는 사용자의 경우 Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포에 기존 인프라를 이용하는 것이 한 가지 방법입니다.

한 가지 중요한 점은 배포된 Samba 버전이 SMB 3.0 규격이어야 한다는 것입니다. SMB 지원이 [!INCLUDE[sssql11-md](../includes/sssql11-md.md)]에 추가된 경우 모든 공유가 SMB 3.0을 지원해야 했습니다. 공유에 Windows Server가 아닌 Samba를 사용하면 Samba 기반 공유는 Samba 4.0 이상을 사용해야 하며, SMB 3.1.1을 지원하는 4.3 이상을 사용하는 것이 가장 좋습니다. SMB 및 Linux에 대한 자세한 내용은 [SMB3 in Samba](https://events.static.linuxfound.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)(Samba의 SMB3)를 참조하세요.

마지막으로, NFS(네트워크 파일 시스템) 공유를 사용할 수 있습니다. NFS는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 Windows 기반 배포에서 사용할 수 없으며 Linux 기반 배포에만 사용할 수 있습니다.

### <a name="configure-the-firewall"></a>방화벽 구성
Windows와 마찬가지로 Linux 배포에는 기본 제공 방화벽이 있습니다. 회사에서 서버에 대한 외부 방화벽을 사용하는 경우 Linux에서 방화벽을 사용하지 않도록 설정할 수 있습니다. 그러나 방화벽이 사용하도록 설정된 위치에 관계없이 포트가 열려 있어야 합니다. 다음 표에서는 Linux에서 고가용성 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포에 필요한 공통 포트를 설명합니다.

| 포트 번호 | Type     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS - `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba(사용되는 경우) - 엔드포인트 매퍼                                                                                          |
| 137         | UDP      | Samba(사용되는 경우) - NetBIOS 이름 서비스                                                                                      |
| 138         | UDP      | Samba(사용되는 경우) - NetBIOS 데이터그램                                                                                          |
| 139         | TCP      | Samba(사용되는 경우) - NetBIOS 세션                                                                                           |
| 445         | TCP      | Samba(사용되는 경우) - SMB over TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] - 기본 포트, 원하는 경우 `mssql-conf set network.tcpport <portnumber>`를 사용하여 변경할 수 있음                       |
| 2049        | TCP, UDP | NFS(사용되는 경우)                                                                                                               |
| 2224        | TCP      | Pacemaker - `pcsd`에서 사용됨                                                                                                |
| 3121        | TCP      | Pacemaker - Pacemaker 원격 노드가 있는 경우 필요함                                                                    |
| 3260        | TCP      | iSCSI 초기자(사용되는 경우) - `/etc/iscsi/iscsid.config`(RHEL)에서 변경할 수 있지만 iSCSI 대상의 포트와 일치해야 함 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] - AG 엔드포인트에 사용되는 기본 포트이며, 엔드포인트를 만들 때 변경할 수 있음                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker - 멀티캐스트 UDP를 사용하는 경우 Corosync에 필요함                                                                     |
| 5405        | UDP      | Pacemaker - Corosync에 필요함                                                                                            |
| 21064       | TCP      | Pacemaker - DLM을 사용하는 리소스에 필요함                                                                                 |
| 변수    | TCP      | AG 엔드포인트 포트이며, 기본값은 5022임                                                                                           |
| 변수    | TCP      | NFS - `LOCKD_TCPPORT`에 대한 포트(RHEL의 경우 `/etc/sysconfig/nfs`에 있음)                                              |
| 변수    | UDP      | NFS - `LOCKD_UDPPORT`에 대한 포트(RHEL의 경우 `/etc/sysconfig/nfs`에 있음)                                              |
| 변수    | TCP/UDP  | NFS - `MOUNTD_PORT`에 대한 포트(RHEL의 경우 `/etc/sysconfig/nfs`에 있음)                                                |
| 변수    | TCP/UDP  | NFS - `STATD_PORT`에 대한 포트(RHEL의 경우 `/etc/sysconfig/nfs`에 있음)                                                 |

Samba에서 사용할 수 있는 추가 포트는 [Samba Port Usage](https://wiki.samba.org/index.php/Samba_Port_Usage)(Samba 포트 사용)를 참조하세요.

반대로, Linux에서 서비스 이름을 포트 대신 예외로 추가할 수도 있습니다(예: Pacemaker에 대한 `high-availability`). 이 방법을 사용하려면 이름에 대한 배포를 참조하세요. 예를 들어 RHEL에서 Pacemaker에 추가할 명령은 다음과 같습니다.

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**방화벽 설명서:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-ssnoversion-md-packages-for-availability"></a>가용성을 위한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 패키지 설치
Windows 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 설치에서 일부 구성 요소는 기본 엔진 설치에도 설치되지만 다른 구성 요소는 설치되지 않습니다. Linux에서는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 엔진만 설치 프로세스의 일부로 설치됩니다. 다른 모든 항목은 선택 사항입니다. Linux에서 고가용성 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 인스턴스의 경우 다음 두 개의 패키지가 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]와 함께 설치됩니다. [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트(*mssql-server-agent*) 및 HA(고가용성) 패키지(*mssql-server-ha*). [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 기술적으로 선택 사항이지만 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 작업 스케줄러이며 로그 전달에 필요하므로 설치하는 것이 좋습니다. Windows 기반 설치에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 선택 사항이 아닙니다.

>[!NOTE]
>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 처음 사용하는 사용자의 경우 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 기본 제공 작업 스케줄러입니다. DBA가 백업 및 기타 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 유지 관리와 같은 작업을 예약하는 일반적인 방법입니다. [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트가 완전히 다른 서비스인 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 Windows 기반 설치와 달리, Linux에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 자체의 컨텍스트에서 실행됩니다.

Windows 기반 구성에서 구성된 AG 또는 FCI는 클러스터를 인식합니다. 클러스터 인식은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]가 WSFC에서 인식하는 특정 리소스 DLL을 포함하며(FCI에 대한 sqagtres.dll 및 sqsrvres.dll, AG에 대한 hadrres.dll) WSFC에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 클러스터형 기능이 시작되어 제대로 실행되는지 확인하는 데 사용된다는 것을 의미합니다. 클러스터링은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]뿐 아니라 Linux 자체에 대해서도 외부이므로, Microsoft에서는 Linux 기반 AG 및 FCI 배포에 해당하는 리소스 DLL을 코딩해야 했습니다. 이는 Pacemaker의 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 리소스 에이전트라고도 하는 *mssql-server-ha* 패키지입니다. *mssql-server-ha* 패키지를 설치하려면 [HA 및 SQL Server 에이전트 패키지 설치](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)를 참조하세요.

[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] on Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 전체 텍스트 검색(*mssql-server-fts*) 및 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services(*mssql-server-is*)의 다른 선택적 패키지는 FCI 또는 AG의 고가용성에 필요하지 않습니다.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Linux의 Always On 가용성 그룹 및 장애 조치(failover) 클러스터 인스턴스에 대한 Pacemaker
앞에서 확인한 것처럼 현재 Microsoft에서 AG 및 FCI에 대해 지원하는 유일한 클러스터링 메커니즘은 Corosync를 사용하는 Pacemaker입니다. 이 섹션에서는 솔루션을 이해하기 위한 기본 정보와 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 구성을 위해 이 솔루션을 계획 및 배포하는 방법을 설명합니다.

### <a name="ha-add-onextension-basics"></a>HA 추가 기능/확장 기본 사항
현재 지원되는 모든 배포는 Pacemaker 클러스터링 스택을 기반으로 하는 고가용성 추가 기능/확장을 제공합니다. 이 스택은 다음과 같은 두 가지 주요 구성 요소인 Pacemaker 및 Corosync를 통합합니다. 스택의 모든 구성 요소는 다음과 같습니다.
-   Pacemaker - 클러스터형 머신에서 조정 같은 작업을 수행하는 핵심 클러스터링 구성 요소입니다.
-   Corosync - 쿼럼, 실패한 프로세스를 다시 시작하는 기능 등의 항목을 제공하는 API의 프레임워크 및 세트입니다.
-   libQB - 로깅 같은 항목을 제공합니다.
-   리소스 에이전트 - 애플리케이션이 Pacemaker와 통합될 수 있도록 제공되는 특정 기능입니다.
-   펜스 에이전트 - 노드에 문제가 있는 경우 노드를 격리하고 처리하도록 지원하는 스크립트/기능입니다.
    
> [!NOTE]
> 클러스터 스택은 일반적으로 Linux 환경에서 Pacemaker라고도 합니다.

이 솔루션은 Windows를 사용하여 클러스터형 구성을 배포하는 것과 일부 측면에서는 비슷하지만 많은 측면에서 서로 다릅니다. Windows에서는 WSFC(Windows Server 장애 조치(failover) 클러스터)라는 클러스터링의 가용성 형식이 운영 체제에 기본 제공되며, WSFC, 장애 조치(failover) 클러스터링을 만들 수 있는 기능은 기본적으로 사용하지 않도록 설정됩니다. Windows에서 AG 및 FCI는 WSFC 위에 빌드되며 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 제공하는 특정 리소스 DLL로 인해 긴밀한 통합을 공유합니다. 한 공급업체에서 모든 것을 제공하므로 대체로 솔루션을 이렇게 긴밀하게 결합할 수 있습니다.

![HA 기본 사항](./media/sql-server-linux-ha-basics/image1.png)

Linux에서 지원되는 각 배포에는 Pacemaker를 사용할 수 있지만 각 배포는 약간 다른 구현 및 버전을 사용자 지정하고 포함할 수 있습니다. 몇 가지 차이는 이 문서의 지침에 반영됩니다. 클러스터링 계층은 오픈 소스이므로 배포와 함께 제공되더라도 WSFC가 Windows에서 작동하는 것과 동일한 방식으로 긴밀하게 통합되지는 않습니다. 이런 이유로 Microsoft에서는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 및 Pacemaker 스택이 Windows 기반 AG 및 FCI에 가깝지는 똑같지는 않은 환경을 제공할 수 있도록 *mssql-server-ha*를 제공합니다.

RHEL 및 SLES의 경우 전체 참조 정보에 포함된 모든 항목에 대한 자세한 설명을 포함한 Pacemaker에 대한 전체 설명서는 다음을 참조하세요.
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu에는 가용성에 대한 가이드가 없습니다.

전체 스택에 대한 자세한 내용은 Clusterlabs 사이트의 공식 [Pacemaker 설명서 페이지](https://clusterlabs.org/doc/)를 참조하세요.

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 개념 및 용어
이 섹션에서는 Pacemaker 구현에 대한 일반적인 개념과 용어를 설명합니다.

#### <a name="node"></a>노드
노드는 클러스터에 참여하는 서버입니다. Pacemaker 클러스터는 기본적으로 최대 16개의 노드를 지원합니다. Corosync가 추가 노드에서 실행되지 않지만 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에 대해 Corosync가 필요한 경우 이 수를 초과할 수 있습니다. 따라서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 기반 구성에 대해 클러스터에 포함할 수 있는 최대 노드 수는 16개입니다. 이는 Pacemaker 한도이며 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 지정하는 AG 및 FCI에 대한 최대 제한 사항에 대해 수행할 작업은 없습니다. 

#### <a name="resource"></a>리소스
WSFC 및 Pacemaker 클러스터에는 둘 다 리소스 개념이 있습니다. 리소스는 디스크 또는 IP 주소와 같이 클러스터의 컨텍스트에서 실행되는 특정 기능입니다. 예를 들어 Pacemaker에서는 FCI 및 AG 리소스를 둘 다 만들 수 있습니다. 이는 AG를 구성할 때 FCI 또는 AG 리소스에 대한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 리소스를 확인할 수 있는 WSFC에서 수행하는 작업과 다르지 않지만, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]가 Pacemaker와 통합되는 방식의 기본적인 차이로 인해 똑같지는 같습니다.

Pacemaker에는 표준 및 복제 리소스가 있습니다. 복제 리소스는 모든 노드에서 동시에 실행되는 리소스입니다. 예를 들어 부하 분산을 위해 여러 노드에서 실행되는 IP 주소가 있습니다. 특정 시간에 하나의 노드만 FCI를 호스트할 수 있으므로 FCI에 대해 만들어지는 모든 리소스는 표준 리소스를 사용합니다.

[!INCLUDE [bias-sensitive-term-t](../includes/bias-sensitive-term-t.md)]

AG를 만들 때 다중 상태 리소스라는 특수한 형식의 복제 리소스가 필요합니다. AG에는 주 복제본이 하나만 있지만 AG 자체는 작동하도록 구성된 모든 노드에서 실행되며 읽기 전용 액세스와 같은 작업을 허용할 수 있습니다. 이는 노드의 “라이브” 사용이므로 리소스에는 두 가지 상태인 마스터 및 슬레이브의 개념이 있습니다. 자세한 내용은 [Multi-state resources: Resources that have multiple modes](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)(다중 상태 리소스: 여러 모드를 포함하는 리소스)를 참조하세요.

#### <a name="resource-groupssets"></a>리소스 그룹/세트

WSFC의 역할과 마찬가지로 Pacemaker 클러스터에는 리소스 그룹의 개념이 있습니다. 리소스 그룹(SLES의 경우 세트라고 함)은 함께 작동하고 한 노드에서 다른 노드로 단일 단위로 장애 조치(failover)될 수 있는 리소스 컬렉션입니다. 리소스 그룹은 마스터 또는 슬레이브로 구성된 리소스를 포함할 수 없으므로 AG에 사용할 수 없습니다. 리소스 그룹은 FCI에 사용될 수 있지만 일반적으로 권장되는 구성이 아닙니다.

#### <a name="constraints"></a>제약 조건
WSFC에는 두 가지 다른 리소스 간 부모/자식 관계를 WSFC에 알리는 종속성 같은 항목뿐 아니라 리소스에 대한 다양한 매개 변수가 있습니다. 종속성은 먼저 온라인으로 전환해야 하는 리소스를 WSFC에 알리는 규칙일 뿐입니다.

Pacemaker 클러스터에는 종속성 개념이 없지만 제약 조건이 있습니다. 공동 배치, 위치 및 순서 지정의 세 가지 제약 조건이 있습니다.
-   공동 배치 제약 조건은 두 리소스를 동일한 노드에서 실행해야 하는지 여부를 적용합니다.
-   위치 제약 조건은 리소스를 실행하거나 실행할 수 없는 위치를 Pacemaker 클러스터에 알려줍니다.
-   순서 지정 제약 조건은 리소스를 시작해야 하는 순서를 Pacemaker 클러스터에 알려줍니다.

> [!NOTE]
> 공동 배치 제약 조건은 모두 단일 단위로 표시되기 때문에 리소스 그룹의 리소스에 필요하지 않습니다.

#### <a name="quorum-fence-agents-and-stonith"></a>쿼럼, 펜스 에이전트 및 STONITH
Pacemaker에서 쿼럼은 WSFC 개념과 비슷합니다. 클러스터 쿼럼 메커니즘의 전체 목적은 클러스터가 계속 실행되는지 확인하는 것입니다. Linux 배포에 대한 WSFC 및 HA 추가 기능에는 각 노드가 쿼럼으로 계산되는 투표 개념이 있습니다. 대부분의 투표가 증가하기를 원합니다. 그렇지 않으면 최악의 경우 클러스터가 종료됩니다.

WSFC와 달리 쿼럼 작업을 수행할 감시 리소스가 없습니다. WSFC와 마찬가지로 목표는 투표자 수를 홀수로 유지하는 것입니다. 쿼럼 구성에는 FCI와는 다른 AG에 대한 고려 사항이 있습니다.

WSFC는 참여하는 노드의 상태를 모니터링하고 문제가 발생할 때 노드를 처리합니다. 이후 버전의 WSFC는 잘못 동작하거나 사용할 수 없는 노드를 격리하는 것과 같은 기능을 제공합니다(노드가 작동되지 않음, 네트워크 통신 작동이 중단됨 등). Linux 쪽에서는 이 유형의 기능이 펜스 에이전트에서 제공됩니다. 이 개념을 펜싱이라고도 합니다. 그러나 이 펜스 에이전트는 일반적으로 배포와 관련이 있으며 대부분은 하드웨어 공급업체에서 제공되고 일부는 하이퍼바이저를 제공하는 공급업체와 같은 소프트웨어 공급업체에서 제공됩니다. 예를 들어 VMware는 vSphere를 사용하여 가상화된 Linux VM에 사용할 수 있는 펜스 에이전트를 제공합니다.

쿼럼 및 펜싱은 STONITH 또는 Shoot the Other Node in the Head(헤드에 있는 다른 노드 맞추기)라는 다른 개념에 연결합니다. 모든 Linux 배포에 지원되는 Pacemaker 클러스터를 포함하려면 STONITH가 필요합니다. 자세한 내용은 [Fencing in a Red Hat High Availability Cluster](https://access.redhat.com/solutions/15575)(Red Hat 고가용성 클러스터의 펜싱)(RHEL)를 참조하세요.

#### <a name="corosyncconf"></a>corosync.conf
이 `corosync.conf` 파일에는 클러스터의 구성이 포함됩니다. 이 파일은 `/etc/corosync`에 있습니다. 클러스터가 제대로 설정되어 있다면 일상적인 작업을 수행하는 동안에는 이 파일을 편집할 필요가 없습니다.

#### <a name="cluster-log-location"></a>클러스터 로그 위치
Pacemaker 클러스터의 로그 위치는 배포에 따라 다릅니다.
-   RHEL 및 SLES - `/var/log/cluster/corosync.log`
-   Ubuntu - `/var/log/corosync/corosync.log`

기본 로깅 위치를 변경하려면 `corosync.conf`를 수정합니다.

## <a name="plan-pacemaker-clusters-for-ssnoversion-md"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에 대한 Pacemaker 클러스터 계획
이 섹션에서는 Pacemaker 클러스터의 중요한 계획 사항을 설명합니다.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-ssnoversion-md"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에 대한 Linux 기반 Pacemaker 클러스터 가상화
가상 머신을 사용하여 AG 및 FCI에 대해 Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포를 배포하는 작업에는 Windows 기반 배포의 경우와 동일한 규칙이 적용됩니다. [Microsoft 지원 KB 956893](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment)에는 Microsoft에서 제공하는 가상화된 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포의 지원 가능성에 대한 기본 규칙 세트가 있습니다. Microsoft의 Hyper-V 및 VMware의 ESXi와 같은 하이퍼바이저는 플랫폼 자체의 차이로 인해 서로 다른 분산을 포함할 수 있습니다.

가상화된 AG 및 FCI의 경우 지정된 Pacemaker 클러스터의 노드에 대해 선호도 방지가 설정되어 있는지 확인합니다. AG 또는 FCI 구성에서 고가용성을 위해 구성된 경우 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 호스트하는 VM은 동일한 하이퍼바이저 호스트에서 실행되지 않아야 합니다. 예를 들어 2노드 FCI가 배포된 경우에는, 특히 Live Migration 또는 vMotion 같은 기능을 사용하는 경우 호스트 오류 발생 시 이동할 노드를 호스트하는 VM 중 하나에 사용할 위치가 있도록 ‘적어도’ 세 개의 하이퍼바이저 호스트가 있어야 합니다.

자세한 내용은 다음을 참조하세요.
-   Hyper-V 설명서 - [Using Guest Clustering for High Availability](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)(고가용성을 위한 게스트 클러스터링 사용)
-   백서(Windows 기반 배포를 위해 작성되었지만 대부분의 개념이 적용됨) - [Planning Highly Available, Mission Critical SQL Server Deployments with VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)(VMware vSphere를 사용하여 중요 업무용 고가용성 SQL Server 배포 계획)

### <a name="networking"></a>네트워킹
WSFC와 달리 Pacemaker의 경우 Pacemaker 클러스터 자체에 대해 전용 이름 또는 하나 이상의 전용 IP 주소가 필요하지 않습니다. AG 및 FCI의 경우 IP 주소가 필요하지만(자세한 내용은 각 설명서 참조), 네트워크 이름 리소스가 없으므로 이름이 필요하지 않습니다. SLES는 관리를 위해 IP 주소를 구성할 수 있지만, [Pacemaker 클러스터 만들기](sql-server-linux-deploy-pacemaker-cluster.md#create)에서 볼 수 있는 것처럼 반드시 필요한 것은 아닙니다.

WSFC와 마찬가지로 Pacemaker는 중복 네트워킹을 선호합니다. 즉, 개별 IP 주소가 있는 고유한 네트워크 카드(NIC 또는 물리적 카드의 경우 pNIC)를 사용합니다. 클러스터 구성 측면에서 각 IP 주소에는 자체 링이라는 항목이 있습니다. 그러나 현재 WSFC와 마찬가지로 많은 구현이 가상화되어 있거나 실제로 서버에 제공되는 단일 vNIC(가상화된 NIC)만 있는 퍼블릭 클라우드에 있습니다. 모든 pNIC 및 vNIC가 동일한 실제 또는 가상 스위치에 연결된 경우 네트워크 계층에는 실제 중복성이 없으므로 여러 NIC를 구성하는 것은 가상 머신에 대한 약간의 오해입니다. 네트워크 중복성은 일반적으로 가상화된 배포를 위해 하이퍼바이저에 기본 제공되며, 퍼블릭 클라우드에 한정적으로 기본 제공됩니다.

여러 NIC 및 Pacemaker와 WSFC의 한 가지 차이는 Pacemaker는 동일한 서브넷에서 여러 IP 주소를 허용하지만 WSFC는 허용하지 않는다는 것입니다. 여러 서브넷 및 Linux 클러스터에 대한 자세한 내용은 [여러 서브넷 구성](sql-server-linux-configure-multiple-subnet.md) 문서를 참조하세요.

### <a name="quorum-and-stonith"></a>쿼럼 및 STONITH
쿼럼 구성 및 요구 사항은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 AG 또는 FCI 특정 배포와 관련됩니다.

지원되는 Pacemaker 클러스터에는 STONITH가 필요합니다. 배포의 설명서를 사용하여 STONITH를 구성합니다. SLES에 대한 예제는 [Storage-based Fencing](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html)(스토리지 기반 펜싱)에 있습니다. ESXI 기반 솔루션의 경우 VMware vCenter에 대한 STONITH 에이전트도 있습니다. 자세한 내용은 [Stonith Plugin Agent for VMWare VM VCenter SOAP Fencing (Unofficial)](https://github.com/olafrv/fence_vmware_soap)(VMWare VM VCenter SOAP 펜싱을 위한 Stonith 플러그 인 에이전트(비공식))을 참조하세요.

### <a name="interoperability"></a>상호 운용성
이 섹션에서는 Linux 기반 클러스터가 WSFC 또는 Linux의 다른 배포와 상호 작용하는 방법에 대해 설명합니다.

#### <a name="wsfc"></a>WSFC
현재는 WSFC 및 Pacemaker 클러스터가 함께 작동할 수 있는 직접적인 방법이 없습니다. 즉, WSFC 및 Pacemaker에서 작동하는 AG 또는 FCI를 만들 수 있는 방법이 없습니다. 그러나 두 가지 상호 운용성 솔루션이 있으며 둘 다 AG용으로 디자인됩니다. FCI가 플랫폼 간 구성에 참여할 수 있는 유일한 방법은 다음 두 가지 시나리오 중 하나에서 인스턴스로 참여하는 경우입니다.
-   클러스터 유형이 없음인 AG. 자세한 내용은 Windows [가용성 그룹 설명서](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.
-   두 가지 AG를 자체 가용성 그룹으로 구성할 수 있는 특수 가용성 그룹 유형인 분산 AG. 분산 AG에 대한 자세한 내용은 [분산 가용성 그룹](../database-engine/availability-groups/windows/distributed-availability-groups.md) 설명서를 참조하세요.

#### <a name="other-linux-distributions"></a>기타 Linux 배포
Linux에서 Pacemaker 클러스터의 모든 노드는 동일한 배포에 있어야 합니다. 예를 들어 이것은 SLES 노드가 있는 Pacemaker 클러스터에 RHEL 노드가 포함될 수 없음을 의미합니다. 이에 대한 주요 이유는 이전에 언급한 것처럼 배포의 버전과 기능이 서로 달라 항목이 제대로 작동할 수 없기 때문입니다. 배포를 함께 사용하는 것은 WSFC 및 Linux를 함께 사용하는 것인 없음 또는 분산 AG를 사용하는 것과 같습니다.

## <a name="next-steps"></a>다음 단계
[SQL Server on Linux용 Pacemaker 클러스터 배포](sql-server-linux-deploy-pacemaker-cluster.md)
