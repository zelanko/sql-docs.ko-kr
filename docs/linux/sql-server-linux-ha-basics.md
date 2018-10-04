---
title: Linux 배포에 대 한 SQL Server 가용성 기본 사항 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: b33acbcf74857cd6a2def74f3596e3dda2a034a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720871"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Linux 배포에 대 한 SQL Server 가용성 기본 사항

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

부터는 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 및 Windows 모두에서 지원 됩니다. Windows 기반 같은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포의 경우 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 데이터베이스 및 인스턴스 Linux에서 항상 사용 가능한 되도록 해야 합니다. 이 문서에서는 계획 및 고가용성 배포의 기술적인 측면을 다룹니다. Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 데이터베이스 및 인스턴스 뿐만 아니라 Windows 기반 설치 간의 차이점 중 일부입니다. 때문에 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 전문가 및 Linux에 대 한 새 수에 대 한 새 않을 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 전문가 게 문서는 일부에 대 한 친숙 하 고 다른 사용자에 게 생소 한 개념이 때때로 소개 합니다.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 배포의 가용성 옵션
백업 및 복원 외에도 동일한 세 가지 가용성 기능은 Windows 기반 배포와 Linux에서 사용할 수 있습니다.
-   Always On 가용성 그룹 (Ag)
-   Always On 장애 조치 클러스터 인스턴스 (Fci)
-   [로그 전달](sql-server-linux-use-log-shipping.md)

Windows, Fci는 기본 Windows Server 장애 조치 클러스터 (WSFC) 항상 필요 합니다. 배포 시나리오에 따라 AG 일반적으로 필요 기본 WSFC를 제외 하 고 새 None에서 variant [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]합니다. Linux에서 WSFC가 없습니다. 섹션에서 설명한는 linux에서 구현 클러스터링 [Linux에서 Always On 가용성 그룹 및 장애 조치 클러스터에 대 한 Pacemaker 인스턴스](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux)합니다.

## <a name="a-quick-linux-primer"></a>빠른 Linux 입문서
일부 Linux 설치 인터페이스를 사용 하 여 설치할 수 있지만 대부분은 그렇지 명령줄을 통해 거의 모든 운영 체제 레이어에서 수행 함을 의미 합니다. Linux 환경에서이 명령줄에 대 한 일반적인 용어는 한 *bash 셸을*합니다.

Linux에서 많은 명령을 여러 가지를 관리자 권한으로 Windows Server에서 수행 해야 합니다. 마찬가지로 상승 된 권한으로 실행 해야 합니다. 두 가지가 있습니다 주 상승 된 권한으로 실행 하려면:
1. 적절 한 사용자의 컨텍스트에서 실행 됩니다. 다른 사용자를 변경 하려면 명령을 사용 하 여 `su`입니다. 경우 `su` 자체적으로 실행 되는 사용자 이름 없이 암호를 알고 있다면 이제 수로 셸에서 *루트*입니다.
   
2. 자세한 공통 및 보안 인식 하는 작업 실행 방법은 데 `sudo` 아무 것도 실행 하기 전에 합니다. 이 예제는 대부분 문서 사용 `sudo`합니다.

몇 가지 일반적인 명령에는 다양 한 스위치 및 옵션을 각각 온라인에서 확인할 수 있습니다.
-   `cd` -디렉터리 변경
-   `chmod` – 파일 또는 디렉터리의 사용 권한 변경
-   `chown` – 파일 또는 디렉터리의 소유권을 변경
-   `ls` – 디렉터리의 내용을 표시 합니다.
-   `mkdir` – 드라이브에 폴더 (디렉터리)를 만듭니다.
-   `mv` – 한 위치에서 파일 이동
-   `ps` – 작업 프로세스 모두 표시
-   `rm` – 서버에서 로컬로 파일 삭제
-   `rmdir` -폴더 (디렉터리)를 삭제 합니다.
-   `systemctl` – 시작, 중지 또는 서비스를 사용 하도록 설정
-   텍스트 편집기 명령입니다. Linux에서 다양 한 텍스트 편집기 옵션, emacs 및 vi 같은 있습니다.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>가용성 구성에 대 한 일반적인 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux
이 섹션에서 다루는 모든 Linux 기반에 공통 되는 작업 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포 합니다.

### <a name="ensure-that-files-can-be-copied"></a>파일을 복사할 수 있는지 확인 합니다.
하나의 서버에서 파일 복사는 누구 든 지 사용 하 여 작업은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux에서 해야 할 수 있습니다. 이 작업은 AG 구성에 대 한 매우 중요 합니다.

Linux 에서도 Windows 기반 설치 사용 권한 문제 등 존재할 수 있습니다. 그러나 Windows에서 서버 간 복사 하는 방법에 익숙하다면 아닐 Linux에서 수행 되는 방법에 익숙하지 합니다. 명령줄 유틸리티를 사용 하는 일반적인 방법은 `scp`, 안전한 복사는 의미입니다. 내부적으로 `scp` OpenSSH를 사용 합니다. SSH는 보안 셸을 나타냅니다. Linux 배포에 따라 자체 OpenSSH는 설치할 수 있습니다. 없는 경우 OpenSSH를 먼저 설치 해야 합니다. OpenSSH를 구성 하는 방법에 대 한 자세한 내용은 각 배포에 대 한 다음 링크에서 정보를 참조 하세요.
-   [Red Hat Enterprise Linux(RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server(SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

사용 하는 경우 `scp`, 없는 경우 원본 또는 대상 서버의 자격 증명을 제공 해야 합니다. 예를 들어,를 사용 하 여

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

다른 서버에서 지정 된 폴더에 MyAGCert.cer 파일을 복사 합니다. 참고-사용 권한 및 소유권 – 파일을 복사 하 고, 따라서 있어야는 `chown` 복사 하기 전에 사용 해야 할 수도 있습니다. 마찬가지로 받는 쪽에서 올바른 사용자 파일을 조작에 대 한 액세스를 해야 합니다. 예를 들어, 해당 인증서 파일을 복원 하는 `mssql` 사용자가 액세스할 수 있어야 합니다.

SMB (서버 메시지 블록) Linux 변형을 인 samba 공유와 같은 UNC 경로 의해 액세스를 만들 사용할 수도 있습니다 `\\SERVERNAME\SHARE`합니다. Samba를 구성 하는 방법에 대 한 자세한 내용은 각 배포에 대 한 다음 링크에서 정보를 참조 하세요.
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Windows 기반 SMB 공유를 사용할 수도 있습니다. SMB 공유를 호스트 하는 Linux 서버에서 올바르게 구성 되어 Samba의 클라이언트 부분으로 Linux 기반 일 필요가 없습니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 및 공유에 올바른 액세스 권한이 있습니다. 혼합된 된 환경에서 대해서에 대 한 기존 인프라를 이용 하는 한 가지 방법은 것이 Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포 합니다.

중요 한 점은 Samba 배포의 버전 SMB 3.0 호환 되어야 합니다. SMB 지원은에서 추가 될 때 [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], SMB 3.0을 지원 하려면 모든 공유 해야 하는 것입니다. Samba 공유 및 Windows 서버가 아닌 사용 Samba 기반 공유 SMB 3.1.1 지 Samba 4.0 이상 및 이상적 4.3 또는 나중에 사용 해야 합니다. SMB 및 Linux에 대 한 정보는 좋은 원본은 [Samba에 SMB3](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)합니다.

마지막으로, 네트워크 파일 시스템 (NFS) 공유를 사용 하는 옵션입니다. Windows 기반 배포에 대 한 옵션 아닙니다 NFS를 사용 하 여 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], Linux 기반 배포에만 사용할 수 있습니다.

### <a name="configure-the-firewall"></a>방화벽 구성
Windows와 마찬가지로 Linux 배포는 기본 제공 방화벽입니다. 회사 외부 방화벽 서버를 사용 하는 경우에 Linux에서 방화벽을 사용 하지 않도록 설정 허용 될 수 있습니다. 그러나는 방화벽이 사용 되는 위치에 관계 없이 열려는 포트 해야 합니다. 다음 표에서 문서에 필요한 공통 포트 항상 사용 가능한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux에 배포 합니다.

| 포트 번호 | 형식     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS – `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | (사용) 하는 경우 samba – 끝점 매퍼                                                                                          |
| 137         | UDP      | (사용) 하는 경우 samba-NetBIOS 이름 서비스                                                                                      |
| 138         | UDP      | (사용) 하는 경우 samba – NetBIOS 데이터 그램                                                                                          |
| 139         | TCP      | (사용) 하는 경우 samba – NetBIOS 세션                                                                                           |
| 445         | TCP      | (사용) 하는 경우 samba – TCP 통한 SMB                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – 기본 포트입니다. 원하는 경우 변경 수 있습니다. `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (사용) 하는 경우                                                                                                               |
| 2224        | TCP      | Pacemaker-사용 `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker-Pacemaker 원격 노드 많은 경우 필요 합니다.                                                                    |
| 3260        | TCP      | iSCSI 초기자 (사용) 하는 경우 – 변경 될 수 있습니다 `/etc/iscsi/iscsid.config` (RHEL), iscsi 대상 포트와 일치 해야 하지만 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -기본 AG 끝점에 사용 되는 포트 끝점을 만들 때에 변경할 수 있습니다.                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker-멀티 캐스트 UDP를 사용 하는 경우 Corosync에 필요한                                                                     |
| 5405        | UDP      | Pacemaker-Corosync에 필요한                                                                                            |
| 21064       | TCP      | Pacemaker-DLM을 사용 하 여 리소스에 필요한                                                                                 |
| 변수    | TCP      | AG 끝점 포트 기본값은 5022                                                                                           |
| 변수    | TCP      | NFS – 포트 `LOCKD_TCPPORT` (있는 `/etc/sysconfig/nfs` RHEL에서)                                              |
| 변수    | UDP      | NFS – 포트 `LOCKD_UDPPORT` (있는 `/etc/sysconfig/nfs` RHEL에서)                                              |
| 변수    | TCP/UDP  | NFS – 포트 `MOUNTD_PORT` (있는 `/etc/sysconfig/nfs` RHEL에서)                                                |
| 변수    | TCP/UDP  | NFS – 포트 `STATD_PORT` (있는 `/etc/sysconfig/nfs` RHEL에서)                                                 |

Samba에서 사용할 수 있는 추가 포트를 참조 하세요 [Samba 포트 사용](https://wiki.samba.org/index.php/Samba_Port_Usage)합니다.

Linux에서 서비스의 이름의 포트; 대신 예외로 추가할 수도 있습니다 반대로 예를 들어 `high-availability` Pacemaker에 대 한 합니다. 이 기능을 이용 하려는 방향 경우 이름에 대 한 배포를 참조 하십시오. 예를 들어 RHEL Pacemaker에 추가 하는 명령을

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**방화벽 설명서:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>설치 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 가용성에 대 한 패키지
Windows 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 설치 반면 일부는 기본 엔진을 설치 하 고에 일부 구성 요소가 설치 됩니다. Linux에는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 엔진 설치 프로세스의 일부로 설치 됩니다. 나머지는 선택 사항입니다. 에 대 한 고가용성 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux에서 인스턴스를 사용 하 여 두 패키지 설치 해야 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트 (*mssql server 에이전트*) 및 고가용성 (HA) 패키지 ( *mssql-서버-ha*). 하는 동안 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 기술적으로 선택적 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]작업에 대 한 스케줄러의 있으며 로그 전달 되므로 설치를 사용 하는 것이 좋습니다. Windows 기반 설치에 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 선택 사항이 아닙니다.

>[!NOTE]
>처음 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 기본 제공 작업 스케줄러입니다. 백업 및 기타 등의 작업을 예약 하는 Dba 위한 일반적인 방법은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 유지 관리 합니다. Windows 기반 설치와 달리 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 위치 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 linux에서 완전히 다른 서비스 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트의 컨텍스트에서 실행 됩니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 자체입니다.

Windows 기반 구성에서 Ag 또는 Fci를 구성 하면 클러스터를 인식 됩니다. 즉 클러스터 인식 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 특정 리소스 Dll (sqagtres.dll 및 hadrres.dll Ag에 Fci에 대 한 sqsrvres.dll) 하는 방법에 대 한 WSFC를 알고 있고 되도록 WSFC에서 사용할는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 클러스터형 기능은, 실행 및 제대로 작동 합니다. 없기 때문에 클러스터링 외부만 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 자체 Linux, Microsoft 배포의 Linux 기반 AG 또는 FCI 리소스 DLL에 해당 하는 코드에 있었습니다. 이 *mssql-서버-ha* 패키지를 라고도 합니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pacemaker 리소스 에이전트. 설치 하는 *mssql-서버-ha* 패키지를 참조 하십시오 [HA 및 SQL Server 에이전트 패키지를 설치](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)합니다.

에 대 한 다른 선택적 패키지 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux에서는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Full-text Search (*mssql-서버-fts*) 및 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql server는*), 되지 고가용성을 AG 또는 FCI에 필요합니다.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Always On 가용성 그룹 및 Linux에서 장애 조치 클러스터 인스턴스에 대 한 pacemaker
이전 듯이 Ag에 Fci Microsoft에서 현재 지 원하는 유일한 클러스터링 메커니즘은 corosync는 Pacemaker 합니다. 이 섹션에서는 계획에 대 한 배포 하는 방법 뿐만 아니라 솔루션을 이해 하려면 기본 정보를 다룹니다. [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 구성 합니다.

### <a name="ha-add-onextension-basics"></a>HA 추가 시/확장 기본 사항
현재 지원 되는 배포의 모든 고가용성 추가-시/확장명을 스택 클러스터링 Pacemaker를 기반으로 하는 제공 됩니다. 이 스택이 두 가지 주요 구성 요소를 통합 합니다: Pacemaker 및 Corosync 합니다. 스택의 모든 구성 요소는:
-   Pacemaker-클러스터 된 컴퓨터에서 좌표와 같은 작업을 수행 하는 구성 요소를 클러스터링 하는 핵심입니다.
-   Corosync – 프레임 워크 및 쿼럼, 다시 시작 하지 못했습니다 프로세스 및 등 기능 등을 제공 하는 Api 집합입니다.
-   libQB – 제공 등 로깅.
-   리소스 에이전트 – 응용 프로그램은 Pacemaker와 통합할 수 있도록 제공 하는 특정 기능입니다.
-   에이전트 – 노드를 격리 하는 데 도움이 되는 문제가 있는 경우 해당 처리 스크립트/기능 울타리 합니다.
    
> [!NOTE]
> 클러스터 스택의 일반적으로 Linux 분야에서 Pacemaker 라고 합니다.

이 방법은 Windows를 사용 하 여 클러스터 된 구성을 배포에서 서로 다른 다양 하지만 비슷하지만 몇 가지에서 있습니다. Windows, 클러스터링, Windows Server 장애 조치 클러스터 (WSFC) 호출의 가용성 형태는 운영 체제 및 WSFC 장애 조치 클러스터링을 만들 수는 기본적으로 사용 하지 않도록 설정 하는 기능에 구축 되었습니다. Windows, Ag Fci는 WSFC를 기반으로 구축 하 고 긴밀 한 통합 특정 리소스에서 제공 하는 DLL로 인해 공유 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 이 밀접 하 게 결합된 솔루션은 모두 하나의 공급 업체에서에서 이기 때문에 그 수 있습니다.

![](./media/sql-server-linux-ha-basics/image1.png)

Linux에서 지원 되는 각 배포판에 Pacemaker를 사용할 수 있는 동안 각 배포 수 사용자 지정 되었고 약간 다른 구현과 및 버전입니다. 일부의 차이점은이 문서의 지침에 반영 됩니다. 클러스터링 계층은 오픈 소스, 배포를 사용 하 여 출시 예정인 경우에 통합 되지 않습니다 긴밀 하 게 동일한 방식으로 WSFC는 Windows에서. 이것이 Microsoft에서 제공 하는 이유 *mssql-서버-ha*있도록 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 및 Pacemaker 스택 닫기을 제공할 수 있지만 Windows 아래에서 Ag에 Fci 발생할 동일는 정확 하 게 합니다.

Pacemaker의 전체 설명서에 대 한 자세한 설명은 RHEL 및 SLES에 대 한 전체 참조 정보를 사용 하 여 모든 것이 무엇을 포함 합니다.
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu는 가용성에 대 한 가이드는 없습니다.

전체 스택에 대 한 자세한 내용은 공식 참조 [Pacemaker 설명서 페이지](http://clusterlabs.org/doc/) Clusterlabs 사이트입니다.

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 개념 및 용어
이 섹션에서는 일반적인 개념과 Pacemaker 구현에 대 한 용어에 설명합니다.

#### <a name="node"></a>노드
노드는 클러스터에 참여 하는 서버입니다. Pacemaker 클러스터를 최대 16 개의 노드를 고유 하 게 지원합니다. Corosync는 추가 노드에서 실행 되 고 있지 않지만 Corosync는 필요한 경우이 수를 초과 되었을 수 있습니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 노드는 클러스터에 대 한 수의 최대 수에 따라서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-기반 구성은 16; Pacemaker 제한을 이며는 Ag 또는 Fci 따른에 대 한 최대 제한은 사용 하 여 관련이 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 

#### <a name="resource"></a>리소스
WSFC와 Pacemaker 클러스터 리소스의 개념이 있습니다. 리소스는 디스크 또는 IP 주소와 같은 클러스터의 컨텍스트에서 실행 되는 특정 기능입니다. 예를 들어, Pacemaker에서 FCI와 AG 리소스 만들 수 있습니다. 이것이 표시 되는 wsfc에서 수행 되는 서로 다른를 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 중 하나는 FCI에 대 한 리소스 또는 AG를 구성 하는 경우에 AG 리소스가 하지만 동일 정확 하 게 하는 방법의 기본 차이로 인해 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker 통합 합니다.

Pacemaker에 리소스가 표준 및 복제 합니다. 복제 리소스는 모든 노드에서 동시에 실행 되는 것입니다. 예제 IP 주소 부하 분산 목적으로 여러 노드에서 실행 되는 것입니다. Fci에 대 한 생성 되는 모든 리소스는 하나의 노드만 언제 든 지 FCI를 호스팅할 수 있으므로 표준 리소스를 사용 합니다.

AG 만들어질 때 특수 한 형태의 다중 상태 리소스 라고 하는 복제 리소스 필요 합니다. AG에 주 복제본이 하나 있는 경우 하는 동안 자체 AG를 실행 하는 모든 노드에서 작동 하도록 구성 하 고 읽기 전용 액세스 등을 허용할 수 있습니다. 노드를 사용 하는 "라이브" 이기 때문에 리소스 개념이 두 가지 상태: 마스터 및 슬레이브 합니다. 자세한 내용은 [다중 상태 리소스: 여러 모드에 있는 리소스](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)합니다.

#### <a name="resource-groupssets"></a>리소스 그룹/설정
WSFC의 역할에는 마찬가지로 Pacemaker 클러스터에 리소스 그룹 개념이 있습니다. (SLES에서 집합 이라고 함) 리소스 그룹은 함께 작동 하 고 하나의 단위로 다른 노드로 장애 조치할 수 있는 리소스의 컬렉션입니다. 리소스 그룹에는 마스터/슬레이브;으로 구성 된 리소스에 포함할 수 없습니다. 따라서 Ag에 대해 사용할 수 없습니다. Fci에 대 한 리소스 그룹을 사용할 수 있지만,이 일반적으로 권장된 구성이 아닙니다.

#### <a name="constraints"></a>제약 조건
나머지가 있는 WSFC의 서로 다른 두 리소스 간의 부모/자식 관계를 알 수 있는 종속성 등 뿐만 아니라 리소스에 대 한 다양 한 매개 변수입니다. 종속성은 방금 라는 WSFC 리소스를 먼저 온라인 가능 해야 합니다. 규칙.

Pacemaker 클러스터 종속성을 개념이 없지만 제약 조건이 있습니다. 세 가지 종류의 제약 조건: 공동 배치 크기, 위치 및 순서 지정 합니다.
-   공동 배치 제약 조건을 두 리소스가 동일한 노드에서 실행 해야 하는지 여부를 적용 합니다.
-   위치 제약 조건을 리소스 수 (또는 없나요) 실행할 Pacemaker 클러스터를 알려 줍니다.
-   정렬 제약 조건을 Pacemaker 클러스터 리소스를 시작 해야 하는 순서를 알려 줍니다.

> [!NOTE]
> 공동 배치 제약 조건 이므로 단일 단위로 표시 되는 모든 리소스는 리소스 그룹에 대 한 필요 하지 않습니다.

#### <a name="quorum-fence-agents-and-stonith"></a>쿼럼, 펜스 에이전트 및 STONITH
Pacemaker에서 쿼럼 WSFC 개념에 어느 정도 비슷합니다. 클러스터의 쿼럼 메커니즘의 전체 목적은 유지는 클러스터를 실행 하는 것입니다. WSFC와 Linux 배포판에 대 한 HA 추가 기능 개념이 투표의 각 노드에 쿼럼에 대해 계산 되는 위치입니다. 응답의 대다수,이 고, 그렇지 최악의 시나리오를 클러스터 종료 됩니다.

WSFC는 달리 쿼럼을 사용 하려면 미러링 모니터 서버 리소스가 없습니다. WSFC와 같은 목표 투표자 홀수 횟수를 유지 하는 것입니다. 쿼럼 구성에 Fci 보다 Ag에 대 한 다양 한 고려 사항

나머지가 참여 하는 노드의 상태를 모니터링 하 고 문제가 발생 한 경우 처리 합니다. 이후 버전의 나머지가 오작동 하거나 사용할 수 없게 된 노드를 격리로 이러한 기능을 제공 (노드인 on, 네트워크 통신은 축소, 등). Linux 쪽에서는 이러한 유형의 기능 펜스 에이전트를 통해 제공 됩니다. 개념은 펜싱 라고도 합니다. 그러나 이러한 펜스 에이전트 배포에 일반적으로 관련이 있으며 대개 하드웨어 공급 업체 및 하이퍼바이저를 제공 하는 것과 같은 일부 소프트웨어 공급 업체에서 제공. 예를 들어, VMware vSphere를 사용 하 여 가상화 된 Linux Vm에 사용할 수는 펜스 에이전트를 제공 합니다.

쿼럼 및 다른 개념에 동률 펜싱 STONITH를 호출 하거나 헤드에 있는 다른 노드 문제를 해결 합니다. STONITH는 모든 Linux 배포판에서 지원 되는 Pacemaker 클러스터 해야 합니다. 자세한 내용은 [Red Hat 높은 가용성 클러스터에서 펜싱](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
`corosync.conf` 파일에는 클러스터의 구성이 포함 되어 있습니다. 에 있는 `/etc/corosync`합니다. 일반적인 일상적인 작업을 하는 과정에서이 파일 되지 클러스터가 제대로 설정 하는 경우 편집할 수 있어야 합니다.

#### <a name="cluster-log-location"></a>클러스터 로그 위치
Pacemaker 클러스터에 대 한 로그 위치 분포에 따라 다릅니다.
-   RHEL 및 SLES- `/var/log/cluster/corosync.log`
-   Ubuntu- `/var/log/corosync/corosync.log`

기본 로깅 위치를 변경 하려면 수정할 `corosync.conf`합니다.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Pacemaker 클러스터에 대 한 계획 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
이 섹션에서는 Pacemaker 클러스터에 대 한 계획의 중요 사항을 설명합니다.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Linux 기반 가상화 Pacemaker 클러스터 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
가상 컴퓨터를 사용 하 여 Linux 기반 배포 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Ag에 Fci 배포와 Windows 기반 함수와 동일한 규칙을 적용 됩니다. 지원 가능성에 대 한 규칙의 기본 집합이 있는 가상화 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] microsoft에서 제공 하는 배포 [Microsoft 지원 KB 956893](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment)합니다. Microsoft의 Hyper-v 및 VMware의 ESXi와 같은 다른 하이퍼바이저 플랫폼 자체의 차이로 인해 다른 차이 위쪽에, 있을 수 있습니다.

가상화 아래에 있는 10ag 및 Fci에 있어 선호도 방지 지정된 하는 Pacemaker 클러스터의 노드에 대해 설정 되어 있는지 확인 합니다. 호스팅 Vm AG 또는 FCI 구성에서 고가용성을 위해 구성 된 경우 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 되지 같은 하이퍼바이저 호스트에서 실행 되어야 합니다. 예를 들어, 2 노드 FCI를 배포 하는 경우 존재 해야 *최소한* 세 가지 하이퍼바이저 호스트 이므로 어딘가에 호스트 오류가 발생 하면 이동할 노드를 호스팅하는 Vm 중 하나에 대 한 기능을 사용 하는 경우에 특히 같은 라이브 마이그레이션 또는 vMotion 합니다.

자세한 내용은 참조 하세요.
-   Hyper-v가 설치 설명서- [고가용성을 위한 게스트 클러스터링을 사용 하 여](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   (용으로 작성 된 Windows 기반 배포 하지만 여전히 개념이 대부분 적용) – 백서 [고가용성 계획, VMware vsphere 업무상 중요 한 SQL Server 배포](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>STONITH 사용 하 여 RHEL Pacemaker 클러스터를 사용 하 여 Hyper-v에서 아직 지원 되지 않습니다. 자세한 내용 및 업데이트 하는 지원 될 때까지 참조 하세요 [RHEL 높은 가용성 클러스터에 대 한 지원 정책을](https://access.redhat.com/articles/29440#3physical_host_mixing)합니다.

### <a name="networking"></a>네트워킹
WSFC와 달리 Pacemaker는 Pacemaker 클러스터 자체 전용된 이름 또는 전용된 IP 주소를 하나 이상 필요 하지 않습니다. Ag 및 Fci IP 주소 (자세한 내용은 각각에 대 한 설명서 참조) 해야 하지만 이름, 네트워크 이름 리소스가 없다는 이므로 합니다. SLES는 관리 목적을 위해 IP 주소를 구성할 수는 있지만에서 볼 수 있듯이 필수가 아닙니다 [Pacemaker 클러스터를 만들](sql-server-linux-deploy-pacemaker-cluster.md#create)합니다.

WSFC와 같은 Pacemaker 선호 중복 네트워킹, 즉 고유 네트워크 카드 (Nic 또는 물리적 서버 pNICs) 개별 IP 주소가 있는 합니다. 클러스터 구성을 기준으로 각 IP 주소 자체 링 라고 해야 합니다. 그러나 나머지가 사용 하 여 오늘날 많은 구현 가상화 됩니다 또는 공용 클라우드에서 단일 서버에 표시 되는 NIC (vNIC)를 가상화가 실제로 합니다. 모든 pNICs 및 Vnic 동일한 물리적 또는 가상 스위치에 연결 되어 있으면 여러 Nic를 구성 하므로 가상 머신에 감 많은 네트워크 계층에서 크게 true 중복이 됩니다. 네트워크 중복성 일반적으로 가상화 된 배포에 대 한 하이퍼바이저에 빌드되고 확실 하 게 공용 클라우드로 빌드됩니다.

하나의 여러 Nic 및 WSFC와 Pacemaker를 사용 하 여 점만 Pacemaker 같은 서브넷에 여러 IP 주소를 허용 하는지 WSFC 하지 않습니다. 여러 서브넷 및 Linux 클러스터에 대 한 자세한 내용은 문서 참조 [다중 서브넷 구성](sql-server-linux-configure-multiple-subnet.md)합니다.

### <a name="quorum-and-stonith"></a>쿼럼 및 STONITH
쿼럼 구성 및 요구 사항은 배포와 관련 된 AG 또는 FCI에 따라 달라 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다.

STONITH는 지원 되는 Pacemaker 클러스터에 필요 합니다. STONITH를 구성 하는 배포에서 문서를 사용 합니다. 예로 [저장소 기반 울타리](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) SLES에 대 한 합니다. ESXI 기반 솔루션에 대 한 VMware vCenter에 대 한 STONITH 에이전트 이기도합니다. 자세한 내용은 [VMWare VM VCenter SOAP 펜싱 (Unofficial)에 대 한 Stonith 플러그 인 에이전트](https://github.com/olafrv/fence_vmware_soap)합니다.

> [!NOTE]
> 이 문서를 작성할 당시 Hyper-v 없는 솔루션 STONITH에 대 한 합니다. 온-프레미스 배포에 대 한 true 이며 또한 RHEL과 같은 특정 배포를 사용 하 여 Azure 기반 Pacemaker 배포에 영향을 줍니다.

### <a name="interoperability"></a>상호 운용성
이 섹션에서는 다른 Linux 배포 또는 WSFC를 사용 하 여 Linux 기반 클러스터를 조작할 수 있는 방법을 설명 합니다.

#### <a name="wsfc"></a>WSFC
현재 WSFC와 Pacemaker 클러스터를 함께 작동 하는 데 직접 방법이 있으면 됩니다. 이 AG 또는 FCI는 WSFC와 Pacemaker에서 작동 하는 만들 수 없습니다 임을 의미 합니다. 그러나 두 개의 상호 운용성 솔루션을 Ag에 대 한 설계는 둘 다 있습니다. FCI는 플랫폼 간 구성에 참여할 수는 유일한 방법은 다음과 같습니다. 이러한 두 시나리오 중 하나의 인스턴스로 참여 중인 경우
-   클러스터 유형이 없음인 AG입니다. 자세한 내용은 참조는 Windows [가용성 그룹 설명서](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)합니다.
-   고유한 가용성 그룹으로 구성 될 두 개의 다른 Ag를 허용 하는 가용성 그룹의 특별 한 형식인 분산된 AG입니다. 분산형된 Ag에 대 한 자세한 내용은 설명서를 참조 [분산 가용성 그룹](../database-engine/availability-groups/windows/distributed-availability-groups.md)합니다.

#### <a name="other-linux-distributions"></a>기타 Linux 배포
Linux에서는 Pacemaker 클러스터의 모든 노드에 동일한 배포에 있어야 합니다. 예를 들어, 즉, RHEL 노드 SLES 노드가 Pacemaker 클러스터의 일부를 수 없습니다. 이 대 한 이유를 설명한: 작업 제대로 작동 하지 수 있도록 배포는 서로 다른 버전 및 기능을에 있을 수 있습니다. 나머지가 및 Linux 혼합와 같은 영역에 배포판 혼합: None을 사용 하거나 분산 Ag입니다.

## <a name="next-steps"></a>다음 단계
[Linux에서 SQL Server에 대 한 Pacemaker 클러스터 배포](sql-server-linux-deploy-pacemaker-cluster.md)
