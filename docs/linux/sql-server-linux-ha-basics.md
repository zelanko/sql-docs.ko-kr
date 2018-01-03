---
title: "Linux 배포에 대 한 SQL Server 가용성 기본 사항 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: b137d8badf44bf1c7d181b490bcf6d06e2bd087f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Linux 배포에 대 한 SQL Server 가용성 기본 사항

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

부터는 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 및 Windows에서 지원 됩니다. Windows 기반 같은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux에서 항상 사용 가능한 데이터베이스와 인스턴스 필요 합니다. 이 문서에서는 계획 하 고 항상 사용 가능한 배포의 기술적인 측면도 Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 데이터베이스 및 인스턴스도 Windows 기반 설치 간의 차이점 중 일부입니다. 때문에 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 전문가 및 Linux에 대 한 새 수에 대 한 새로울 수도 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 전문가 위한 문서 때때로 개념을 소개 일부에 대 한 친숙 하 고 다른 사용자에 게 생소 한 될 수 있습니다.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 배포에 대 한 가용성 옵션
백업 및 복원 외에도 동일한 세 가지 가용성 기능 경우 Windows 기반 배포와 Linux에서 사용할 수 있는 가지
-   Always On 가용성 그룹 (Ag)
-   Always On 장애 조치 클러스터 인스턴스 (Fci)
-   [로그 전달](sql-server-linux-use-log-shipping.md)

Windows에서 Fci는 기본 Windows Server 장애 조치 클러스터 (WSFC) 항상 필요 합니다. 배포 시나리오에 따라 AG 일반적으로 기본 WSFC와 함께 필요 새 것을 제외 하 고 없음에서 variant [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]합니다. WSFC는 Linux에서 존재 하지 않습니다. Linux에서 구현에 대해서는 설명 아래 [Linux에서 Always On 가용성 그룹 및 장애 조치 클러스터에 대 한 Pacemaker 인스턴스](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux)합니다.

## <a name="a-quick-linux-primer"></a>빠른 Linux 입문서
일부 Linux 설치 인터페이스와 함께 설치할 수 있습니다, 대부분은 그렇지 명령줄을 통해 운영 체제 계층에 거의 모든 항목을 수행할지를 의미 합니다. Linux 상황에서이 명령줄에 대 한 일반적인 용어는 *bash 셸은*합니다.

Linux에서 많은 명령을 많은 요소에서 관리자 권한으로 Windows Server에서 수행 해야 할 처럼 상승 된 권한으로 실행 해야 합니다. 두 가지 주요 방법을 상승 된 권한으로 실행 하는
1. 적절 한 사용자의 컨텍스트에서 실행 됩니다. 다른 사용자를 변경 하려면 명령을 사용 하 여 `su`합니다. 경우 `su` 자체적으로 실행 되는 사용자 이름 없이 암호가으로 이제 됩니다으로 셸에서 *루트*합니다.
   
2. 더 많은 공통 및 보안을 인식 실행 하는 방법은 작업 사용 하는 것 `sudo` 아무 것도 실행 하기 전에. 사용 하 여 다양 한이 예제에서는 문서 `sudo`합니다.

몇 가지 일반적인 명령에는 다양 한 스위치 및 옵션을 각각 온라인에서 확인할 수 있습니다.
-   `cd`– 디렉터리 변경
-   `chmod`-파일 또는 디렉터리의 사용 권한을 변경
-   `chown`-파일 또는 디렉터리의 소유권을 변경
-   `ls`– 디렉터리의 내용을 표시 합니다.
-   `mkdir`– 드라이브에 폴더 (디렉터리)를 만듭니다.
-   `mv`– 한 위치에서 파일 이동
-   `ps`– 작업 프로세스 모두 표시
-   `rm`-서버에서 로컬로 파일 삭제
-   `rmdir`– 폴더 (디렉터리)를 삭제 합니다.
-   `systemctl`– 시작, 중지 또는 서비스를 사용 하도록 설정
-   텍스트 편집기 명령입니다. Linux에서 vi emacs 등 다양 한 텍스트 편집기 옵션, 있습니다.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>가용성 구성에 대 한 일반적인 작업 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux
이 섹션에서는 모든 Linux 기반에 공통적인 작업 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포 합니다.

### <a name="ensure-that-files-can-be-copied"></a>파일을 복사할 수 있는지 확인 하십시오.
한 가지는 누구 든 지 사용 하 여 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux에 수 작업을 수행 하는 다른 서버 간에 파일을 복사 합니다. 이 작업은 AG 구성에 대 한 매우 중요 합니다.

Linux와 Windows 기반 설치에 사용 권한 문제 등으로 존재할 수 있습니다. 그러나 Windows에서 서버 간에 복사 하는 방법에 익숙한 아니어야 Linux에서 수행 되는 방법에 대해 잘 알고 합니다. 명령줄 유틸리티를 사용 하는 일반적인 메서드가 `scp`, 나타내는 안전한 복사 합니다. 내부적으로 `scp` OpenSSH를 사용 합니다. SSH는 보안 셸을 나타냅니다. Linux 배포에 따라 자체 OpenSSH는 설치할 수 있습니다. 그럴 경우 OpenSSH를 먼저 설치 해야 합니다. OpenSSH를 구성 하는 방법에 대 한 자세한 내용은 각 배포에 대 한 다음 링크에서 정보를 참조 합니다.
-   [Red Hat Enterprise Linux(RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server(SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

사용 하는 경우 `scp`, 없는 경우 소스 또는 대상 서버의 자격 증명을 제공 해야 합니다. 예를 들어,를 사용 하 여

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

다른 서버에 지정 된 폴더에 MyAGCert.cer 파일을 복사 합니다. -사용 권한 및 소유권 – 따라서 복사한 파일의 해야가 `chown` 복사 하기 전에 사용 해야 할 수도 있습니다. 마찬가지로, 수신 측에서 올바른 사용자 파일을 조작에 대 한 액세스를 해야 합니다. 예를 들어, 해당 인증서 파일을 복원 하는 `mssql` 사용자에 액세스할 수 있어야 합니다.

와 같은 UNC 경로에서 액세스할 공유를 만들 서버 메시지 블록 (SMB)의 Linux variant 인 samba 사용할 수도 있습니다 `\\SERVERNAME\SHARE`합니다. Samba를 구성 하는 방법에 대 한 자세한 내용은 각 배포에 대 한 다음 링크에서 정보를 참조 합니다.
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

SMB 공유 Windows 기반을 사용할 수도 있습니다. SMB 공유를 호스팅하는 Linux 서버에 올바르게 구성 되어 Samba의 클라이언트 부분으로 Linux 기반 사용 될 필요가 없습니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 공유에 적절 한 액세스. 에 대 한 기존 인프라를 활용 하는 한 가지 방법은 혼합된 환경에서 대해서 것 Linux 기반 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 배포 합니다.

중요 한 한 가지가 버전 Samba 배포의 SMB 3.0 호환 되어야 합니다. SMB 지원을 추가할 때 [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], 모든 공유 SMB 3.0 지원에 필요 합니다. Samba를 사용 하 여 공유 및 Windows Server가 아닌, Samba 기반의 공유 수 있도록 지 원하는 SMB 3.1.1 Samba 4.0 또는 나중에 및 이상적 4.3 이상 사용 해야 합니다. SMB 및 Linux에서 정보의 좋은 소스는 [Samba에 SMB3](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)합니다.

마지막으로, 네트워크 파일 시스템 (NFS) 공유를 사용 하는 옵션입니다. NFS를 사용 하는 배포의 경우 Windows 기반에서 옵션이 아닙니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], Linux 기반 배포에 사용할 수 있습니다.

### <a name="configure-the-firewall"></a>방화벽 구성
마찬가지로 Windows, Linux 배포판 기본 제공 방화벽을 가집니다. 회사 외부 서버에 방화벽을 사용 하는 경우 Linux에서 방화벽을 해제 하기 적당 합니다. 그러나는 방화벽이 설정 되었기 관계 없이 포트를 열어야 필요 합니다. 다음 표에서 문서에 필요한 공용 포트는 항상 사용 가능한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux 배포 합니다.

| 포트 번호 | 형식     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS –`rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | (사용) 하는 경우 samba – 끝점 매퍼                                                                                          |
| 137         | UDP      | (사용) 하는 경우 samba – NetBIOS 이름 서비스                                                                                      |
| 138         | UDP      | (사용) 하는 경우 samba – NetBIOS 데이터 그램                                                                                          |
| 139         | TCP      | (사용) 하는 경우 samba – NetBIOS 세션                                                                                           |
| 445         | TCP      | (사용) 하는 경우 samba – TCP 통한 SMB                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]– 기본 포트입니다. 원하는 경우 변경할 수 있습니다.`mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (사용 된 경우)                                                                                                               |
| 2224        | TCP      | Pacemaker-에서 사용 하는`pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker – Pacemaker 원격 노드 필수                                                                    |
| 3260        | TCP      | iSCSI 초기자 (사용) 하는 경우 – 변경 될 수 있습니다 `/etc/iscsi/iscsid.config` (RHEL), iscsi 대상 포트와 일치 해야 하지만 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-기본 AG 끝점;에 사용 되는 포트 끝점을 만들 때에 변경할 수 있습니다.                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | UDP 멀티 캐스트를 사용 하는 경우 Corosync에 필요한 pacemaker –                                                                     |
| 5405        | UDP      | Pacemaker – Corosync에 필요한                                                                                            |
| 21064       | TCP      | DLM를 사용 하 여 리소스에 필요한 pacemaker –                                                                                 |
| 변수    | TCP      | AG 끝점 포트; 기본값은 5022                                                                                           |
| 변수    | TCP      | 에 대 한 NFS – 포트 `LOCKD_TCPPORT` (에 `/etc/sysconfig/nfs` RHEL에서)                                              |
| 변수    | UDP      | 에 대 한 NFS – 포트 `LOCKD_UDPPORT` (에 `/etc/sysconfig/nfs` RHEL에서)                                              |
| 변수    | TCP/UDP  | 에 대 한 NFS – 포트 `MOUNTD_PORT` (에 `/etc/sysconfig/nfs` RHEL에서)                                                |
| 변수    | TCP/UDP  | 에 대 한 NFS – 포트 `STATD_PORT` (에 `/etc/sysconfig/nfs` RHEL에서)                                                 |

Samba에서 사용할 수 있는 추가 포트에 대 한 참조 [Samba 포트 사용](https://wiki.samba.org/index.php/Samba_Port_Usage)합니다.

반대로, linux 서비스 이름으로도으로 추가할 수 있습니다 포트; 대신 예외 예를 들어 `high-availability` Pacemaker에 대 한 합니다. 방향 관점에서 해결 하려는 경우 이름에 대 한 배포를 참조 하십시오. 예를 들어 RHEL Pacemaker에 추가할 명령을

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**방화벽 설명서:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>설치 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 가용성에 대 한 패키지
Windows 기반에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 설치 하지는 일부 구성 요소는 엔진의 기본 설치에도 설치 됩니다. Linux만 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 엔진 설치 과정의 일부로 설치 됩니다. 다른 모든 항목은 선택 사항입니다. 에 대해 항상 사용 가능한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux 인스턴스와 두 개의 패키지 설치 해야 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트 (*mssql 서버 에이전트*) 및 고가용성 (HA) 패키지 ( *mssql-서버-ha*). 반면 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 기술적으로 선택적 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]작업에 대 한 스케줄러의 세그먼트와 로그 전달에서 필요 하므로 설치를 사용 하는 것이 좋습니다. Windows 기반 설치에 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 선택 사항이 아닙니다.

>[!NOTE]
>처음 사용 하는 것에 대 한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 기본 제공 작업 스케줄러입니다. 백업 오류 코드 및 기타 등의 작업을 예약 하는 Dba에 대 한 일반적인 방법은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 유지 관리 합니다. Windows 기반 설치와 달리 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 여기서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에이전트는 linux의 완전히 다른 서비스 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 의 컨텍스트에서 에이전트가 실행 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 자체입니다.

Ag Fci 구성 되어 있는 Windows 기반 구성에서 클러스터 인식 됩니다. 클러스터 인식 됨을 의미 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 되도록 WSFC에서 사용 하 고 특정 리소스는 WSFC (sqagtres.dll 및 Fci Ag에 대 한 hadrres.dll에 대 한 sqsrvres.dll)에 대해 알고 Dll에는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 클러스터형된 기능,가 실행 되 고 제대로 작동합니다. 없기 때문에 클러스터링 외부만 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 있지만 Linux 기반 AG fci로 또는 FCI 배포에 대 한 리소스 DLL 해당 하는 코드를 작성 하려면 자체 Linux, Microsoft가 있습니다. 이는 *mssql-서버-ha* 라고도 패키지는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker에 대 한 리소스 에이전트입니다. 설치 하는 *mssql-서버-ha* 참조, 패키지 [HA 및 SQL Server 에이전트 패키지를 설치](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)합니다.

에 대 한 다른 선택적 패키지 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 전체 텍스트 검색 (*mssql-서버-fts*) 및 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql 서버는*), 되지 않습니다 높은 가용성, FCI는 또는 AG에 필요합니다.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Always On 가용성 그룹 및 Linux에서 장애 조치 클러스터 인스턴스에 대 한 pacemaker
위에서 언급 한 대로 Ag 및 Fci에 대 한 Microsoft에서 현재 지 원하는 유일한 클러스터링 메커니즘 Corosync와 Pacemaker입니다. 이 섹션에서는 솔루션을 계획 하 고 배포에 대 하는 방법을 이해 하는 기본 정보를 다룹니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 구성 합니다.

### <a name="ha-add-onextension-basics"></a>HA 추가 시/확장 기본 사항
모든 현재 지원 되는 배포는 항상 사용 가능한 추가-시/확장을 스택 클러스터링 Pacemaker에 따라 제공 됩니다. 이 스택 두 가지 주요 구성 요소를 통합: Pacemaker 및 Corosync 합니다. 스택의 모든 구성 요소는.
-   Pacemaker 클러스터링 구성 요소는 클러스터 된 모든 시스템에서 좌표와 같은 작업을 수행 하는 핵심입니다.
-   Corosync-프레임 워크 및 쿼럼, 다시 시작 하지 못했습니다 프로세스 및 기타 등등 하는 기능 등을 제공 하는 Api 집합입니다.
-   libQB – 제공과 같은 로깅.
-   리소스 에이전트 – 특정 기능을 응용 프로그램 Pacemaker와 통합할 수 있도록 제공 됩니다.
-   에이전트-스크립트/기능에 노드를 격리 하는 데 지원 하 고 문제가 있는 경우 이들을 처리 울타리 합니다.
    
> [!NOTE]
> 클러스터 스택 일반적으로 Linux 전 세계에서 Pacemaker 라고 합니다.

이 방법은 몇 가지와 비슷하기는 하지만 Windows를 사용 하 여 클러스터 된 구성을 배포한 다른 여러 가지 방법으로 있습니다. Windows에서 가용성 형태의 클러스터링 라는 Windows Server 장애 조치 클러스터 (WSFC)는 운영 체제와 WSFC 장애 조치 클러스터링를 만들 수 있도록, 기본적으로 비활성화 되어 있는 기능에 포함 됩니다. Windows에서 Ag 고 Fci는 WSFC 위에 구축 된와 긴밀 하 게 통합 특정 리소스에서 제공 되는 DLL로 인해 공유 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 이 하 게 결합 된 솔루션은 한 공급 업체에서 모두 되었기 때문에 전반적 가능 합니다.

![](./media/sql-server-linux-ha-basics/image1.png)

Linux에서 지원 되는 각 배포에 Pacemaker를 사용할 수 있을 때 각 배포 사용자 지정할 수 있으며 약간 다른 구현 및 버전입니다. 이 문서의 지침에 설명 된 일부의 차이 반영 됩니다. 계층의 클러스터링은 오픈 소스는 분포와 함께 제공 되며, 경우에 하지 긴밀 하 게 통합 되어 같은 방식으로 windows WSFC는 합니다. 이 때문에 Microsoft 제공 *mssql-서버-ha*있도록 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 및 Pacemaker 스택에 가깝게 제공할 수 있지만 Windows 아래에서 Ag 및 Fci에 대 한 환경 동일는 정확 하 게 합니다.

Pacemaker의 전체 설명서에 대 한 자세한 설명은 RHEL 및 SLES에 대 한 전체 참조 정보는 모든 항목을 포함 하 여:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu는 가용성에 대 한 가이드는 없습니다.

전체 스택에 대 한 자세한 내용은 공식 참조도 [Pacemaker 설명서 페이지](http://clusterlabs.org/doc/) Clusterlabs 사이트에 있습니다.

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 개념 및 용어
이 섹션에는 일반적인 개념 및 용어 Pacemaker 구현에 대 한 설명합니다.

#### <a name="node"></a>노드
노드는 클러스터에 참여 하는 서버. Pacemaker 클러스터 최대 16 개의 노드를 고유 하 게 지원합니다. Corosync 추가 노드에서 실행 되 고 있지 않지만 Corosync 실행 되어야 하는 경우이 값을 초과 수 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 클러스터에 대 한 개뿐입니다 노드의 최대 수 따라서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-기반 구성은 16; Pacemaker 제한을 15, 이며 Ag 또는 Fci에 따라 적용 되는 최대 제한 사항과 함께 관련이 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 

#### <a name="resource"></a>리소스
WSFC와 Pacemaker 클러스터 리소스의 개념을에 있습니다. 리소스는 클러스터 디스크, IP 주소 등의 컨텍스트에서 실행 되는 특정 기능. 예를 들어 Pacemaker에서 AG와 FCI 리소스 생성 가져올 수 있습니다. 이 나타나는 wsfc에서 수행 되는 동작과 비슷하지 않은 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 중 하나는 FCI에 대 한 리소스 또는 AG를 구성 하는 경우에 AG 리소스 하지만 정확히 동일 방법의 기본 차이로 인해 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker와 통합 되어 있습니다.

Pacemaker에 표준 및 복제 리소스가 있습니다. 복제 리소스를는 모든 노드에서 동시에 실행 하는 것입니다. 예제에는 로드 균형 조정을 위해 여러 노드에서 실행 되는 IP 주소 같습니다. Fci에 대 한 생성 되는 모든 리소스는 하나의 노드만 언제 든 지 FCI를 호스팅할 수 있으므로 표준 리소스를 사용 합니다.

AG 만들어질 때 특수 한 형태의 다중 상태 리소스 라는 복제 자원 필요 합니다. AG 하나의 주 복제본에 있는 경우 동안 자체 AG를 실행 하는 모든 노드에 걸쳐,에서 작동 하도록 구성 되 고 읽기 전용 액세스 등을 허용할 수 있습니다. 리소스는 한 두 개의 상태 개념 노드를 사용 하는 "라이브" 이기 때문에: 마스터와 종속 합니다. 자세한 내용은 참조 [다중 상태 리소스: 여러 모드를 포함 하는 리소스가](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)합니다.

#### <a name="resource-groupssets"></a>리소스 그룹/설정
마찬가지로 wsfc에서 역할, Pacemaker 클러스터 리소스 그룹의 개념을 있습니다. (SLES에서 집합 이라고 함) 리소스 그룹은 함께 작동할 수 및 단일 단위로 다른 한 노드에서 조치할 수 있는 리소스의 컬렉션입니다. 리소스 그룹 마스터/슬레이브;로 구성 된 리소스를 포함할 수 없습니다. 따라서 Ag에 대해 사용할 수 없습니다. Fci에 대 한 리소스 그룹을 사용할 수 있지만지 않습니다 일반적으로 권장된 구성.

#### <a name="constraints"></a>제약 조건
WSFCs가 두 개의 다른 리소스 간의 부모/자식 관계 WSFC를 알 수 있는 종속성 등 뿐만 아니라 리소스에 대 한 다양 한 매개 변수. 종속성은 방금는 내용의 WSFC 리소스 필요한 먼저 온라인 상태인 것입니다.

Pacemaker 클러스터에 종속 항목의 개념이 없는 있지만 제약 조건이 있습니다. 제약 조건의 세 종류: 공동 배치, 위치 및 순서 지정 합니다.
-   공동 배치 제약 조건 두 리소스가 동일한 노드에서 실행 해야 하는지 여부를 적용 합니다.
-   위치 제약 조건이 있는 리소스가 있나요 (또는 없나요) 실행 Pacemaker 클러스터를 알려 줍니다.
-   정렬 제약 Pacemaker 클러스터 리소스가 시작 해야 하는 순서를 알려 줍니다.

> [!NOTE]
> 공동 배치 제약 조건으로 하나의 단위로 표시 되는 모든 기능과 되므로 리소스 그룹의 리소스에 대 한 필요 하지 않습니다.

#### <a name="quorum-fence-agents-and-stonith"></a>쿼럼, fence 에이전트 및 STONITH
쿼럼 Pacemaker에서 개념적에서 WSFC 다소 비슷합니다. 클러스터의 쿼럼 메커니즘의 전체 목적은 유지 하 고 클러스터를 실행 합니다. WSFC 및 Linux 배포판에 대 한 HA 추가 기능 모두 개념이 투표를 각 노드의 쿼럼 합산 하는 위치입니다. 응답의 대다수, 그렇지 않으면 최악의 시나리오에서 5d; 클러스터 종료 됩니다.

WSFC, 달리은 쿼럼과 작동 하도록 미러링 모니터 서버 리소스가 없습니다. WSFC에서와 같은 목표 홀수 투표자의 수를 유지 하는 것입니다. 쿼럼 구성에 Fci 보다 Ag에 대 한 다른 고려 사항이 있습니다.

WSFCs 참여 중인 노드의 상태를 모니터링 하 고 문제가 발생 한 경우를 처리 합니다. 이후 버전의 WSFCs 제공이 잘못 되었거나 사용할 수 있는 노드 격리를 설정 하면 같은 기능 (노드는 설정, 네트워크 통신은 등 축소) 합니다. Linux 쪽에서는 이러한 유형의 기능 fence 에이전트에 의해 제공 됩니다. 개념 펜싱 라고도 합니다. 그러나 이러한 fence 에이전트 일반적으로 관련 된 배포에서는 대개 하드웨어 공급 업체 및 하이퍼바이저를 제공 하는 등 일부 소프트웨어 공급 업체에서 제공 합니다. 예를 들어 VMware vSphere를 사용 하 여 가상화 Linux Vm에 사용할 수 있는 펜스 에이전트를 제공 합니다.

쿼럼 및 다른 개념에 동률 방어 STONITH를 호출 하거나 헤드에 있는 다른 노드를 해결 합니다. STONITH 모든 Linux 배포판의 지원 되는 Pacemaker 클러스터가 필요 합니다. 자세한 내용은 참조 [Red Hat High 가용성 클러스터에서 방어](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
`corosync.conf` 클러스터의 구성 파일에 포함 되어 있습니다. 에 위치한 `/etc/corosync`합니다. 정상적인 일상 작업 과정에서이 파일 클러스터가 제대로 설정 되어 있는 경우 편집을 수행할 필요는 합니다.

#### <a name="cluster-log-location"></a>클러스터 로그 위치
Pacemaker 클러스터에 대 한 로그 위치 분포에 따라 다릅니다.
-   RHEL 및 SLES-`/var/log/cluster/corosync.log`
-   Ubuntu –`/var/log/corosync/corosync.log`

기본 로깅 위치를 변경 하려면 수정 `corosync.conf`합니다.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Pacemaker 클러스터에 대 한 계획[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
이 섹션에서는 Pacemaker 클러스터에 대 한 중요 한 계획 사항에 설명 합니다.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Linux 기반 가상화 Pacemaker 클러스터에 대 한[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
가상 컴퓨터를 사용 하 여 Linux 기반 배포할 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Ag 및 Fci에 대 한 배포의 경우 Windows 기반 대응와 동일한 규칙 적용 됩니다. 지원 가능성에 대 한 규칙의 기본 집합이 가상화 된 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 에 Microsoft에서 제공 하는 배포 [Microsoft 지원 KB 956893](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment)합니다. Microsoft의 Hyper-v 및 VMware의 ESXi 같은 다른 하이퍼바이저 플랫폼 자체의 차이 때문에 위에 해당, 다른 분산 있을 수 있습니다.

가상화에서 Ag 및 Fci에 있어 선호도 방지 특정된 Pacemaker 클러스터의 노드에 대해 설정 되어 있는지 확인 합니다. 호스트 하는 Vm AG 또는 FCI 구성에서 고가용성을 위해 구성 된 경우 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 되지 같은 하이퍼바이저 호스트에서 실행 되어야 합니다. 예를 들어 2 노드 FCI를 배포 하는 경우 없습니다는 있어야 *이상* 놓았을 하 어딘가에 호스트 실패 시 이동 하려면 노드를 호스팅하는 Vm 중 하나에 대 한 기능을 사용 하는 경우에 특히 3 하이퍼바이저 호스트 Live와 같은 마이그레이션 또는 vMotion 합니다.

자세한 내용은 다음을 참조 하십시오.
-   Hyper V 설명서- [고가용성을 위한 게스트 클러스터링을 사용 하 여](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   백서 (용으로 작성 된 Windows 기반 배포 하지만 대부분의 개념을 여전히 적용) – [고가용성 계획, VMware vsphere 업무상 중요 한 SQL Server 배포](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>STONITH와 Pacemaker 클러스터와 RHEL Hyper-v에서 아직 지원 되지 않습니다. 자세한 내용 및 업데이트 하는 지원 될 때까지 참조 [RHEL 높은 가용성 클러스터에 대 한 지원 정책](https://access.redhat.com/articles/29440#3physical_host_mixing)합니다.

### <a name="networking"></a>네트워킹
WSFC에서 달리 Pacemaker Pacemaker 클러스터 자체에 대 한 전용된 이름 또는 전용된 IP 주소를 하나 이상 필요 하지 않습니다. Ag 및 Fci (각각에 대 한 자세한 정보에 대 한 설명서 참조)는 IP 주소에 필요 합니다 이름 제외, 네트워크 이름 리소스가 없으면 때문입니다. SLES 관리 목적을 위해 IP 주소를 구성할 수는 있지만에서 볼 수 있듯이 필요 하지 않은 [Pacemaker 클러스터 만들기](sql-server-linux-deploy-pacemaker-cluster.md#create)합니다.

WSFC에서 같은 Pacemaker 하려면 중복 네트워킹 고유한 네트워크 카드 (Nic 또는 물리적에 대 한 pNICs) 의미 개별 IP 주소 필요 합니다. 클러스터 구성 기준으로 각 IP 주소는 자체 링으로 해야 합니다. 그러나 WSFCs와 오늘날 많은 구현 가상화 되었는지 또는 공용 클라우드에서는 단일 서버에 표시 되는 NIC (vNIC)를 가상화 실제로 합니다. 모든 pNICs 및 vNICs 동일한 물리적 또는 가상 스위치에 연결 되어 있으면가 true 중복 되지 않는 네트워크 계층에서 여러 Nic 구성은 가상 컴퓨터에 감의 비트. 네트워크 중복성은 일반적으로 가상화 된 배포에 대 한 하이퍼바이저에 만들어지고 공용 클라우드 내장 확실 하 게 됩니다.

여러 Nic 및 Pacemaker WSFC에 대 한 차이점 중 하나는 WSFC는 그렇지 않습니다 반면 Pacemaker 동일한 서브넷에 여러 개의 IP 주소를 허용 합니다. 다중 서브넷과 Linux 클러스터에 대 한 자세한 내용은 문서 참조 [여러 서브넷 구성](sql-server-linux-configure-multiple-subnet.md)합니다.

### <a name="quorum-and-stonith"></a>쿼럼 및 STONITH
쿼럼 구성 및 요구 사항의 AG 또는 FCI 관련 배포에 관련 된 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다.

STONITH가 지원 되는 Pacemaker 클러스터에 대 한 필요 합니다. 분포의 설명서를 사용 하 여 STONITH 구성. 예에는 [저장소 기반 펜싱](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) SLES에 대 한 합니다. ESXI 기반 솔루션에 대 한 VMware vCenter에 대 한 STONITH 에이전트 이기도합니다. 자세한 내용은 참조 [VMWare VM VCenter SOAP 방어 (Unofficial)에 대 한 플러그 인 에이전트 Stonith](https://github.com/olafrv/fence_vmware_soap)합니다.

> [!NOTE]
> 이 문서를 작성할 당시 Hyper-v 없는 솔루션 STONITH에 대 한 합니다. 온 프레미스 배포에 대 한 true 이며 RHEL 같은 특정 분포를 사용 하 여 Azure 기반 Pacemaker 배포 영향을 합니다.

### <a name="interoperability"></a>상호 운용성
이 섹션 WSFC 문제나 다른 배포판의 Linux Linux 기반 클러스터 작용 하는 방법에 대해 설명 합니다.

#### <a name="wsfc"></a>WSFC
현재는 함께 작동 하도록 WSFC와 Pacemaker 클러스터에 대 한 직접적인 방법은입니다. AG 또는 WSFC 및 Pacemaker에서 작동 하는 FCI를 만들 수 없으므로 있다는 것을 의미 합니다. 그러나 둘 다는 Ag 위한 두 가지 상호 운용성 솔루션을 있습니다. FCI는 플랫폼 간 구성에 참여할 수 있습니다 하는 유일한 방법은 다음 두 시나리오 중 하나에 있는 인스턴스로 참여 하는 경우입니다.
-   None 클러스터 유형 AG 합니다. 자세한 내용은 참조는 Windows [가용성 그룹 설명서](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)합니다.
-   분산된 AG, 즉 두 개의 서로 다른 Ag 자신의 가용성 그룹으로 구성할 수 있는 가용성 그룹의 특별 한 형식입니다. 분산된 Ag에 대 한 자세한 내용은 설명서를 참조 하십시오. [분산형 가용성 그룹](../database-engine/availability-groups/windows/distributed-availability-groups.md)합니다.

#### <a name="other-linux-distributions"></a>다른 Linux 배포판
Linux에서 Pacemaker 클러스터의 모든 노드에 동일한 배포에 있어야 합니다. 예를 들어, 즉, RHEL 노드는 SLES 노드에 있는 Pacemaker 클러스터의 일부가 될 수 없습니다. 이 주요 이유는 위에 명시 된: 때문에 작업이 제대로 작동 하지 못했습니다가 배포는 서로 다른 버전 및 기능에 있을 수 있습니다. WSFCs와 Linux와 같은 영역에 분포 혼합: None을 사용 하거나 Ag 분산 합니다.

## <a name="next-steps"></a>다음 단계
[Linux에서 SQL Server에 대 한 Pacemaker 클러스터 배포](sql-server-linux-deploy-pacemaker-cluster.md)
