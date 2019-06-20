---
title: 구성 검사 목록-Analytics Platform System | Microsoft Docs
description: 자체 환경에 대 한 Analytics Platform System을 구성 하는 데 필요한 작업에 대 한 검사 목록을 제공 합니다. 이러한 구성 태스크는 어플라이언스에 사용 하기 전에 필요 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ada3d2f782a33caf5334361a9682c53cf7cdec95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63276041"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Analytics Platform System에 대 한 어플라이언스 구성 검사 목록
자체 환경에 대 한 Analytics Platform System을 구성 하는 데 필요한 작업에 대 한 검사 목록을 제공 합니다. 이러한 구성 태스크는 어플라이언스에 사용 하기 전에 필요 합니다.  
  
> [!WARNING]  
> Analytics Platform System을 사용 하 여**Configuration Manager** 는 가장 좋은 방법은 및 지원 되는 유일한 방법, 도구에서 사용할 수 있는 작업을 수행 합니다.  
  
## <a name="BeforeTasks"></a>시작하기 전 주의 사항  
  
### <a name="prerequisites"></a>사전 요구 사항  
  
1.  어플라이언스는 데이터 센터에 설치 하 고 전원이 켜져 해야 합니다.  
  
2.  IHV에서 제공 하는 다음 정보를 알고 있는지 확인 합니다.  
  
    -   PDW 제어 노드에 대 한 외부 IP 주소 (*PDW_region-* CTL01)  
  
    -   어플라이언스 도메인 이름  
  
    -   사용자 이름 및 어플라이언스 도메인 관리자 암호  
  
3.  신뢰할 수 있는 인증서를 가져옵니다. 클라이언트에 연결할 수 있도록 이후 단계에서이 가져오게 합니다 **관리 콘솔** 안전 하 게 연결 합니다. 암호로 보호 된 PFX 파일에 제어 노드에 인증서를 저장 합니다.  
  
4.  시작 합니다 **Configuration Manager**, 다음 단계를 사용 하 여:  
  
    1.  사용 하 여 **원격 데스크톱** PDW 제어 노드에 연결 하려면 (*PDW_region*-CTL01). (해야 CTL01에 대 한 외부 IP 주소를 사용 하 여 연결 합니다.)  
  
    2.  시작 합니다 **Configuration Manager** 에서 합니다 **시작** PDW 제어 노드의 메뉴. Configuration Manager의 첫 번째 화면에는 IHV에서 만든 어플라이언스 토폴로지를 표시 합니다. 어플라이언스의 일부로 SQL Server PDW 소프트웨어에서 인식 하드웨어 노드의 목록입니다. 어플라이언스 토폴로지 화면에서 설정을 변경 하지 않아도 됩니다.  
  
## <a name="CMTasks"></a>Configuration Manager 작업을 수행 합니다.  
SQL Server PDW**Configuration Manager** (PDWCM)는 어플라이언스 수준 작업을 수행 하 고 어플라이언스 수준 설정을 변경 하려면 SQL Server PDW 시스템 관리자를 사용 하는 어플라이언스 관리 도구입니다. 예를 들어 하는 데 PDWCM 암호 다시 설정, 표준 시간대 설정, IP 주소를 변경, SSL 인증서를 구성, 방화벽을 통해 원격 액세스를 사용 하도록 설정, 시작 또는 어플라이언스를 중지 및 인스턴트 파일 초기화를 설정 합니다.  
  
사용 하 여 **Configuration Manager** 다음 구성 작업을 수행할 수 있습니다.  
  
|구성 태스크|Description|  
|----------------------|---------------|  
|물리적 구성 요소 이름에 잘 알고|[PDW 및 어플라이언스 패브릭 물리적 구성 요소 &#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|SQL Server PDW 구성 관리자를 시작 합니다.|[Configuration Manager 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)|  
|도메인 관리자 암호 변경|어플라이언스를 개인 Windows Active Directory Domain Services 어플라이언스 내의 노드를 인증 하는 데 사용 되는 있습니다.<br /><br />IHV는 기본 도메인 관리자 암호를 사용 하 여 어플라이언스를 설정 합니다. 보안 된 암호를 변경 해야 합니다.<br /><br />합니다 **Configuration Manager** 도메인 관리자 암호를 변경 하는 방법만 지원 됩니다.<br /><br />자세한 내용은 [암호 재설정 &#40;Analytics Platform System&#41;](password-reset.md)합니다.|  
|암호를 변경 합니다 **sa** 로그온|SQL Server PDW에 명명 된 시스템 관리자 로그온 **sa**합니다. 합니다 **sa** 로그온 모든 권한을 갖습니다. 권한을 부여할 수 있습니다, 거부 또는 모든 권한을 취소 합니다. 모든 시스템 뷰도 볼 수 있습니다.<br /><br />자세한 내용은 [암호 재설정 &#40;Analytics Platform System&#41;](password-reset.md)합니다.|  
|어플라이언스 표준 시간대 설정|모든 어플라이언스 노드에 대 한 시간 (로컬 또는 기타 원하는 시간)을 설정 합니다.<br /><br />자세한 내용은 [어플라이언스 표준 시간대 구성 &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md)합니다.|  
|SQL Server PDW 어플라이언스에 대 한 외부 연결 네트워크 설정 지정|[어플라이언스 네트워크 구성 &#40;Analytics Platform System&#41;](appliance-network-configuration.md)|  
|관리 콘솔에 대 한 보안 인증서 가져오기|인증서는 HTTPS를 통해 Secure Sockets Layer (SSL) 연결을 제공할 수는 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)합니다. 기본적으로 **관리 콘솔** 개인 정보 보호 하지 않습니다 서버를 제공 하는 자체 서명 된 인증서를 포함 합니다. 또한이 인증서 내용의 Internet Explorer에서 오류가 반환합니다. "이 웹이 사이트의 보안 인증서에 문제가" 사용자가 연결 하는 경우. 이 연결 클라이언트와 서버 간에 진행 중인 데이터를 암호화 하지만 공격자 로부터 위험이 여전히 연결이입니다.<br /><br />SQL Server PDW 관리자는 인증서 보안에 연결 하 고 Internet Explorer를 보고 하는 오류를 제거 하기 위해 클라이언트에서 인식 하는 신뢰할 수 있는 인증 기관에 연결 된 획득 즉시 해야 합니다. 이렇게 하려면 (권장) 제어 노드의 가상 IP 주소에 매핑하는 정규화 된 도메인 이름 또는 관리자 콘솔에 액세스 하려면 사용자가 브라우저 주소에 입력 하는 값과 일치 하는 인증서 이름을 막대입니다.<br /><br />사용 합니다 **Configuration Manager** 를 추가 하 여 신뢰할 수 있는 인증서를 제거 합니다. Microsoft Windows HTTP 서비스 인증서 구성 도구를 사용 하 여 직접 (`winHttpCertCfg.exe`) 인증서를 관리 하는 지원 되지 않습니다.<br /><br />자세한 내용은 [PDW 인증서 프로 비전 &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md)합니다.|
|기능 스위치|분석 플랫폼 시스템 AU7에 도입 된 기능 스위치에 대 한 정보를 표시 합니다. 이 페이지를 사용 하 여 업데이트 하거나 기능 및 Analytics Platform System에 대 한 설정을 설정/해제 합니다. 기능 스위치 값을 변경 서비스를 다시 시작을 해야 합니다.<br /><br />자세한 내용은 [PDW 기능 스위치가 &#40;Analytics Platform System&#41;](appliance-feature-switch.md)합니다.|
|허용 하거나 SQL Server PDW 어플라이언스에 특정 포트에 대 한 액세스를 방지 하는 Windows 방화벽 규칙을 사용 하지 않도록 설정 하거나 사용 합니다.|IHV를 구성 하 고 제대로 작동 하도록 어플라이언스에 대 한 필요한 방화벽 규칙을 사용 합니다. 대부분의 경우에서 사용 하도록 설정 하 되거나 방화벽 규칙을 사용 하지 않도록 설정 되지 않습니다.<br /><br />자세한 내용은 [PDW 방화벽 구성 &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md)합니다.|  
|시작 하 고 SQL Server PDW 어플라이언스를 중지 합니다.|중지 또는 SQL Server PDW appliance를 시작 합니다. 자세한 내용은 [PDW 서비스 상태 &#40;Analytics Platform System&#41;](pdw-services-status.md)합니다.|  
|사용 하 여 인스턴트 파일 초기화 옵션을 검토 합니다 **권한을** 대화 상자|즉시 파일 초기화는 더 빠르게 실행 하기 위해 데이터 파일 작업을 허용 하는 SQL Server 기능입니다. 네트워크 서비스 계정에 SE_MANAGE_VOLUME_NAME 권한을 부여 하는 경우에 SQL Server PDW에서 활성화 됩니다. 기본적으로 해제 되어 있습니다.<br /><br />자세한 내용은 [인스턴트 파일 초기화 구성 &#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md)합니다.|  
|백업에서 master 데이터베이스를 복원 합니다.|현재 삭제 **마스터** 데이터베이스 및 백업으로 대체 합니다. 자세한 내용은 [Master 데이터베이스 복원 &#40;Analytics Platform System&#41;](restore-the-master-database.md)합니다.|  
  
## <a name="AddTasks"></a>추가 구성 작업을 수행 합니다.  
수행한 후 합니다 **Configuration Manager** 다음과 같은 추가 구성 작업을 수행 하는 작업을 합니다. 이러한 태스크 중 일부는 선택적입니다.  
  
|구성 태스크|Description|  
|----------------------|---------------|  
|타사 바이러스 백신 소프트웨어를 설치 하 고 외부에서 노드를 연결 하는 것에 대 한 SQL Server PDW 어플라이언스에 구성 수 있습니다.<br /><br />(옵션)|자세한 내용은 [바이러스 백신 소프트웨어 &#40;Analytics Platform System&#41;](antivirus-software.md)합니다.|  
|DSRM 암호를 변경할 수 있습니다.<br /><br />(옵션)|자세한 내용은 [디렉터리 서비스 복원 모드로 AD 노드에 로그온에 대 한 관리자 암호 설정 &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)합니다.|  
|소프트웨어 업데이트를 받으려면 어플라이언스 구성<br /><br />좋습니다.|어플라이언스는 SQL Server PDW 및 기본 소프트웨어 업데이트를 수신 하도록 구성 해야 합니다.<br /><br />자세한 내용은 [Windows Server Update Services 구성 &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)합니다. WSUS에 대 한 자세한 내용은 [소프트웨어 설치 &#40;Analytics Platform System&#41;](software-servicing.md)합니다.|  
|Hadoop 또는 Azure blob 저장소와 같은 외부 데이터에 대 한 연결을 구성 합니다.<br /><br />(옵션)|자세한 내용은 [외부 데이터에 PolyBase 연결 구성 &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md)합니다.|  
|바이러스 백신 소프트웨어 구성<br /><br />(옵션)|타사 바이러스 백신 솔루션 외부와 접한 노드를 보호 하기 위해 사용할 수 있지만 필요 하지 않습니다. 지침을 따르세요.|  
|백업 및 서버를 로드에 InfiniBand 네트워크 어댑터 구성<br /><br />(옵션)|백업 및 서버를 로드 InfiniBand 네트워크를 사용 하 여 SQL Server PDW에 연결을 구성 하려면 현재 활성 InfiniBand 네트워크에 InfiniBand 연결을 확인 하는 DNS 어플라이언스를 허용 하도록 네트워크 어댑터를 구성 해야 합니다.|  
|Microsoft로 원격 분석 데이터를 보내도록 구성<br /><br />(옵션)|Microsoft로 보내도록 원격 분석 데이터 분석 플랫폼 시스템을 구성 하려면 제어 노드에서 PowerShell 스크립트를 실행 해야 합니다. 특정 지침은 [Microsoft로 원격 분석 피드백 보내기 &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)합니다.|  
  
## <a name="see-also"></a>관련 항목  
[바이러스 백신 소프트웨어 &#40;Analytics Platform System&#41;](antivirus-software.md)  
[InfiniBand 네트워크 어댑터를 구성 &#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
