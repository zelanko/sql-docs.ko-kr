---
title: 보안 고려사항
description: 이 문서에서는 SQL Server를 설치하기 전과 후에 모두 고려해야 하는 보안 권장 사항에 대해 설명합니다.
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [SQL Server]
- server message blocks [SQL Server]
- disabling protocols
- security [SQL Server], installations
- protocols [SQL Server], disabling
- NetBIOS [SQL Server]
- services [SQL Server], security
- SMB [SQL Server]
- isolating services [SQL Server]
- Setup [SQL Server], security
- low SQL Server installation privileges
- NTFS [SQL Server]
- physical security [SQL Server]
- file system security [SQL Server]
- installing SQL Server, security
ms.assetid: cf96155f-30a8-48b7-8d6b-24ce90dafdc7
author: cawrites
ms.author: chadam
ms.openlocfilehash: cfba4d529ee851f3e27bdbdc8b89f44ad1608361
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96121093"
---
# <a name="security-considerations-for-a-sql-server-installation"></a>SQL Server 설치에 대한 보안 고려 사항
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

 보안은 모든 제품과 모든 비즈니스에서 중요합니다. 간단한 권장 사항을 따르면 많은 보안상의 취약점을 방지할 수 있습니다. 이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하기 전과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치한 후에 모두 고려해야 하는 보안 권장 사항에 대해 설명합니다. 특정 기능에 대한 보안 지침은 해당 기능에 대한 참조 문서에 포함되어 있습니다.  
  
## <a name="before-installing-ssnoversion"></a>다음 설치 전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 서버 환경을 설정하는 경우 다음 권장 사항을 따르십시오.  
  
-   [물리적 보안 강화](#physical_security)  
  
-   [방화벽 사용](#firewalls)  
  
-   [서비스 격리](#isolated_services)  
  
-   [보안 파일 시스템 구성](#sa_with_least_privileges)  
  
-   [NetBIOS 및 서버 메시지 블록 비활성화](#disabled_protocols)  
  
-   [도메인 컨트롤러에 SQL Server 설치](../../sql-server/install/security-considerations-for-a-sql-server-installation.md#Install_DC)  
  
###  <a name="enhance-physical-security"></a><a name="physical_security"></a> Enhance Physical Security  
 물리적 및 논리적 격리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안의 기반이 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 물리적 보안을 강화하려면 다음 태스크를 수행하십시오.  
  
-   허가받은 사람만 출입할 수 있는 공간에 서버를 둡니다.  
  
-   데이터베이스를 호스팅하는 컴퓨터를 물리적으로 보호된 위치에 둡니다. 누수 및 화재 감지 또는 억제 시스템을 갖춘 밀폐된 컴퓨터실이 가장 좋습니다.  
  
-   데이터베이스를 기업 인트라넷의 보안 영역에 설치하고 SQL Server를 인터넷에 직접 연결하지 않습니다.  
  
-   모든 데이터를 정기적으로 백업하고 멀리 떨어진 지역에 백업을 안전하게 보관합니다.  
  
###  <a name="use-firewalls"></a><a name="firewalls"></a> Use Firewalls  
 방화벽은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 보안에 중요합니다. 방화벽의 효율적인 작동을 위해 지켜야 할 지침은 다음과 같습니다.  
  
-   방화벽을 서버와 인터넷 사이에 둡니다. 방화벽을 설정합니다. 방화벽이 해제되어 있으면 설정하고 방화벽이 설정되어 있으면 해제하지 마십시오.  
  
-   네트워크를 방화벽으로 분리된 여러 보안 영역으로 나눕니다. 모든 트래픽을 차단한 다음 필요한 것만 선택적으로 허용합니다.  
  
-   다중 계층 환경에서는 여러 방화벽을 사용하여 스크린된 서브넷을 만듭니다.  
  
-   Windows 도메인 내에 서버를 설치할 경우 Windows 인증을 허용하도록 내부 방화벽을 구성합니다.  
  
-   애플리케이션에서 분산 트랜잭션을 사용하는 경우 MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) 트래픽이 개별 MS DTC 인스턴스 간에 전달될 수 있도록 방화벽을 구성해야 합니다. 또한 MS DTC와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 같은 리소스 관리자 간에도 트래픽이 전달되도록 방화벽을 구성해야 합니다.  
  
 기본 Windows 방화벽 설정 방법과 [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 영향을 주는 TCP 포트에 대한 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
###  <a name="isolate-services"></a><a name="isolated_services"></a> Isolate Services  
 서비스를 격리하면 하나의 손상된 서비스가 다른 서비스를 손상시키는 위험을 줄일 수 있습니다. 서비스를 격리하려면 다음 지침을 따르십시오.  
  
-   별도의 Windows 계정으로 별도의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행합니다. 가능하면 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 별도의 낮은 권한의 Windows 또는 로컬 사용자 계정을 사용합니다. 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)를 참조하세요.  
  
###  <a name="configure-a-secure-file-system"></a><a name="sa_with_least_privileges"></a> Configure a Secure File System  
 올바른 파일 시스템을 사용하면 보안이 강화됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 경우 다음 태스크를 수행해야 합니다.  
  
-   NTFS 파일 시스템(NTFS)을 사용합니다. NTFS는 FAT 파일 시스템에 비해 안정적이고 복구 가능하기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 적합한 파일 시스템입니다. NTFS에서는 또한 파일 및 디렉터리 ACL(액세스 제어 목록) 및 EFS(파일 시스템 암호화) 파일 암호화와 같은 보안 옵션도 사용할 수 있습니다. 설치 중 NTFS가 감지되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 적절한 ACL을 레지스트리 키와 파일에 설정합니다. 이러한 사용 권한은 변경할 수 없습니다. 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서는 FAT 파일 시스템이 있는 컴퓨터에 대한 설치를 지원하지 않을 수 있습니다.  
  
    > [!NOTE]  
    >  EFS를 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 계정의 ID로 데이터베이스 파일이 암호화됩니다. 파일 해독도 이 계정으로만 할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 계정을 변경해야 하는 경우 먼저 이전 계정으로 파일을 해독한 다음 새 계정으로 파일을 다시 암호화해야 합니다.  
  
-   중요한 데이터 파일에는 RAID(Redundant Array of Independent Disks)를 사용합니다.  
  
###  <a name="disable-netbios-and-server-message-block"></a><a name="disabled_protocols"></a> Disable NetBIOS and Server Message Block  
 경계 네트워크에 있는 서버에는 NetBIOS 및 SMB(서버 메시지 블록) 등의 불필요한 모든 프로토콜이 비활성화되어 있어야 합니다.  
  
 NetBIOS는 다음 포트를 사용합니다.  
  
-   UDP/137(NetBIOS 이름 서비스)  
  
-   UDP/138(NetBIOS 데이터그램 서비스)  
  
-   TCP/139(NetBIOS 세션 서비스)  
  
 SMB는 다음 포트를 사용합니다.  
  
-   TCP/139  
  
-   TCP/445  
  
 웹 서버 및 DNS(Domain Name System) 서버에는 NetBIOS 또는 SMB가 필요 없습니다. 이러한 서버에서 두 프로토콜을 모두 비활성화하여 사용자 목록 노출 위협을 줄이십시오.  
  
###  <a name="installing-ssnoversion-on-a-domain-controller"></a><a name="Install_DC"></a> 도메인 컨트롤러에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치  
 보안상의 이유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 도메인 컨트롤러에 설치하지 않는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 도메인 컨트롤러 컴퓨터에 설치하는 것을 차단하지는 않지만 다음과 같은 제한 사항을 적용합니다.  
  
-   도메인 컨트롤러에서는 로컬 서비스 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 컴퓨터에 설치한 후에는 도메인 멤버에서 도메인 컨트롤러로 컴퓨터를 변경할 수 없습니다. 호스트 컴퓨터를 도메인 컨트롤러로 변경하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 제거해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 컴퓨터에 설치한 후에는 도메인 컨트롤러에서 도메인 멤버로 컴퓨터를 변경할 수 없습니다. 호스트 컴퓨터를 도메인 멤버로 변경하려면 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 제거해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스는 클러스터 노드가 도메인 컨트롤러인 경우 지원되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 읽기 전용 도메인 컨트롤러에서 보안 그룹을 만들거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 프로비전할 수 없습니다. 이 경우 설치 프로그램에서 오류가 발생합니다.  
  
## <a name="during-or-after-installation-of-ssnoversion"></a>다음 설치 도중 또는 설치 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 설치 후에도 계정 및 인증 모드에 대한 권장 사항을 수행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 보안을 강화할 수 있습니다.  
  
 **서비스 계정**  
  
-   가장 낮은 사용자 권한을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 낮은 권한을 가진 Windows 로컬 사용자 계정 또는 도메인 사용자 계정과 연결합니다.  
  
-   자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)를 참조하세요.  
  
 **인증 모드**  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결을 위해 Windows 인증이 필요합니다.  
  
-   Kerberos 인증 사용 자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.  
  
 **강력한 암호**  
  
-   **sa** 계정에는 항상 강력한 암호를 지정합니다.  
  
-   암호 강도 및 만료를 검사하는 암호 정책을 항상 사용하도록 설정합니다.  
  
-   모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 항상 강력한 암호를 사용합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 설치 중에 BUILTIN\Users 그룹에 대한 로그인이 추가됩니다. 이 로그인을 사용하면 컴퓨터의 모든 인증된 사용자가 public 역할의 멤버로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 인스턴스에 액세스할 수 있습니다. BUILTIN\Users 로그인은 개별 로그인이 있거나 로그인이 있는 기타 Windows 그룹의 멤버인 컴퓨터 사용자에 대한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 액세스를 제한하기 위해 안전하게 제거할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [네트워크 프로토콜 및 네트워크 라이브러리](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Kerberos 연결의 서비스 사용자 이름 등록](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
  
