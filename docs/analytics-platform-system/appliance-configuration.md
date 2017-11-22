---
title: "어플라이언스 구성 (분석 플랫폼 시스템)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 064e7485-7026-4acf-8084-f5d30757d177
caps.latest.revision: "43"
ms.openlocfilehash: ebb797e3fdb24bad79857f83c163dbf92a439883
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-configuration"></a>어플라이언스 구성
사용자가 자신의 환경에 대 한 분석 플랫폼 시스템을 구성 하는 데 필요한 작업에 대 한 검사 목록을 제공 합니다. 어플라이언스를 사용 하려면 먼저 이러한 구성 작업은 필요 합니다.  
  
> [!WARNING]  
> 분석 플랫폼 시스템을 사용 하 여**Configuration Manager** 는 가장 좋은 방법은 및 지원 되는 유일한 도구에서 사용할 수 있는 작업을 수행할 수 있습니다.  
  
## <a name="BeforeTasks"></a>시작하기 전 주의 사항  
  
### <a name="prerequisites"></a>필수 구성 요소  
  
1.  어플라이언스에는 데이터 센터에 설치 하 고 전원이 켜져 해야 합니다.  
  
2.  IHV 사용자가 제공 하는 다음 정보가 있는지 확인 합니다.  
  
    -   PDW 제어 노드에 대 한 외부 IP 주소 (*PDW_region-*CTL01)  
  
    -   응용 프로그램 도메인 이름  
  
    -   사용자 이름 및 암호는 기기 도메인 관리자 암호  
  
3.  신뢰할 수 있는 인증서를 가져옵니다. 클라이언트에 연결할 수 있도록 하는 이후 단계에서 가져올이 **관리 콘솔** 보안 연결을 사용 합니다. 하는 제어 노드에 암호로 보호 된 PFX 파일에 인증서를 저장 합니다.  
  
4.  시작 된 **Configuration Manager**, 다음 단계를 사용 하 여:  
  
    1.  사용 하 여 **원격 데스크톱** PDW 제어 노드에 연결 하려면 (*PDW_region*-CTL01). (CTL01에 대 한 외부 IP 주소와 연결 해야 할 수 있습니다.)  
  
    2.  시작 된 **Configuration Manager** 에서 **시작** PDW 제어 노드의 메뉴. Configuration Manager의 첫 번째 화면 IHV에 의해 생성 된 어플라이언스 토폴로지를 표시 합니다. 이 어플라이언스의 일환으로 SQL Server PDW 소프트웨어에서 인식 하는 하드웨어 노드의 목록입니다. 어플라이언스 토폴로지 화면에서 설정을 변경할 필요가 없습니다.  
  
## <a name="CMTasks"></a>Configuration Manager 작업을 수행 합니다.  
SQL Server PDW**Configuration Manager** (PDWCM)는 기기 수준 작업을 수행 하 고 어플라이언스에 수준 설정을 변경 하려면 SQL Server PDW 시스템 관리자를 사용 하는 어플라이언스 관리 도구입니다. 예를 들어 암호를 다시 설정, 표준 시간대 설정, IP 주소를 변경, SSL 인증서를 구성, 방화벽을 통해 원격 액세스, 시작 또는 중지 기기를 하 고 즉시 파일 초기화를 설정 PDWCM 사용 합니다.  
  
사용 하 여 **Configuration Manager** 다음 구성 작업을 수행할 수 있습니다.  
  
|구성 태스크|Description|  
|----------------------|---------------|  
|물리적 구성 요소 이름에 잘 알고|[PDW 및 물리적 어플라이언스 패브릭 구성 요소 &#40; 분석 플랫폼 시스템 &#41;](pdw-and-appliance-fabric-physical-components.md)|  
|SQL Server PDW 구성 관리자를 시작 합니다.|[구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41;](launch-the-configuration-manager.md)|  
|도메인 관리자 암호를 변경 합니다.|어플라이언스는 개인 Windows Active Directory 도메인 서비스 어플라이언스에 내에 있는 노드를 인증 하는 데 사용 되는 있습니다.<br /><br />프로그램 IHV 기본 도메인 관리자 암호와 어플라이언스를 설정합니다. 이 보안 된 암호 변경 해야 합니다.<br /><br />**Configuration Manager** 도메인 관리자 암호를 변경 하려면 경우에 지원 됩니다.<br /><br />자세한 내용은 참조 [암호 다시 설정 &#40; 분석 플랫폼 시스템 &#41; ](password-reset.md).|  
|에 대 한 암호를 변경 하는 **sa** 로그온|SQL Server PDW에 명명 된 시스템 관리자 로그온 **sa**합니다. **sa** 로그온 모든 권한을 갖습니다. 권한을 부여할 수, 거부 또는 모든 권한을 취소 합니다. 또한 모든 시스템 뷰를 볼 수 있습니다.<br /><br />자세한 내용은 참조 [암호 다시 설정 &#40; 분석 플랫폼 시스템 &#41; ](password-reset.md).|  
|어플라이언스 표준 시간대 설정|모든 어플라이언스 노드에 대 한 시간 (로컬 또는 기타 원하는 시간)을 설정 합니다.<br /><br />자세한 내용은 참조 [기기 표준 시간대 구성 &#40; 분석 플랫폼 시스템 &#41; ](appliance-time-zone-configuration.md).|  
|SQL Server PDW 어플라이언스에 대 한 외부와 접한 네트워크 설정 지정|[어플라이언스 네트워크 구성 &#40; 분석 플랫폼 시스템 &#41;](appliance-network-configuration.md)|  
|관리 콘솔에 대 한 보안 인증서 가져오기|인증서는 HTTPS를 통해 Secure Sockets Layer (ssl)을 제공할 수는 [관리 콘솔 &#40;를 사용 하 여 어플라이언스에 모니터링 분석 플랫폼 시스템 &#41; ](monitor-the-appliance-by-using-the-admin-console.md). 기본적으로는 **관리 콘솔** 개인 정보 보호 하지만 하지 서버 인증을 제공 하는 자체 서명 된 인증서를 포함 합니다. 이 인증서를 Internet Explorer 없다는 오류를 반환 합니다: "이 웹이 사이트의 보안 인증서에 문제가 있습니다."는 사용자를 연결 합니다. 이 연결의 클라이언트와 서버 간에 진행 중인 데이터를 암호화 하지만 연결이 공격자 로부터 위험에 여전히 있습니다.<br /><br />SQL Server PDW 관리자 인증서 보안 연결 하 고 보고 하는 Internet Explorer는 오류를 제거 하기 위해 클라이언트에서 인식 하는 신뢰할 수 있는 인증 기관에 연결 된 획득 즉시 해야 합니다. 이 정규화 된 도메인 이름이 필요 합니다 (권장)는 제어 노드에 가상 IP 주소를 매핑합니다 또는 사용자의 브라우저 주소에 입력 하는 값과 일치 하는 인증서 이름이 막대 관리 콘솔에 액세스할 수 있습니다.<br /><br />사용 하 여는 **Configuration Manager** 를 추가 하 여 신뢰할 수 있는 인증서를 제거 합니다. Microsoft Windows HTTP 서비스 인증서 구성 도구를 사용 하 여 직접 (`winHttpCertCfg.exe`) 인증서를 관리 하는 지원 되지 않습니다.<br /><br />자세한 내용은 참조 [PDW 인증서 프로 비전이 &#40; 분석 플랫폼 시스템 &#41; ](pdw-certificate-provisioning.md).|  
|허용 하거나 SQL Server PDW 어플라이언스의 특정 포트에 액세스할 수 없도록 하는 Windows 방화벽 규칙을 사용 하지 않도록 설정 하거나 사용 합니다.|프로그램 IHV 구성 하 고 정상적으로 작동 하려면 어플라이언스에 대 한 필요한 방화벽 규칙을 사용 합니다. 대부분의 경우에서 사용 하도록 설정 하 되거나 방화벽 규칙을 사용 하지 않도록 설정 되지 않습니다.<br /><br />자세한 내용은 참조 [PDW 방화벽 구성 &#40; 분석 플랫폼 시스템 &#41; ](pdw-firewall-configuration.md).|  
|시작 하 고 SQL Server PDW 어플라이언스를 중지 합니다.|중지 하거나 SQL Server PDW 어플라이언스를 시작 합니다. 자세한 내용은 참조 [PDW 서비스 상태 &#40; 분석 플랫폼 시스템 &#41; ](pdw-services-status.md).|  
|사용 하 여 즉시 파일 초기화 옵션 검토는 **권한** 대화 상자|즉시 파일 초기화는 보다 빠르게 실행 하는 데이터 파일 작업을 허용 하는 SQL Server 기능입니다. 네트워크 서비스 계정에 SE_MANAGE_VOLUME_NAME 권한을 부여 하는 경우에 SQL Server PDW에서 설정 됩니다. 기본적으로 해제 되어 있습니다.<br /><br />자세한 내용은 참조 [인스턴트 파일 초기화 구성 &#40; 분석 플랫폼 시스템 &#41; ](instant-file-initialization-configuration.md).|  
|백업에서 master 데이터베이스를 복원 합니다.|현재 삭제 **마스터** 데이터베이스 및 백업으로 바꿉니다. 자세한 내용은 참조 [Master 데이터베이스 &#40; 복원 분석 플랫폼 시스템 &#41; ](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>추가 구성 작업을 수행 합니다.  
수행한 후는 **Configuration Manager** 다음과 같은 추가 구성 작업을 수행 하는 작업을 합니다. 이들 중 몇몇이 작업은 선택적입니다.  
  
|구성 태스크|Description|  
|----------------------|---------------|  
|타사 바이러스 백신 소프트웨어를 설치 하 고 외부 노드를 연결에 대 한 SQL Server PDW 어플라이언스에 구성 수 있습니다.<br /><br />(옵션)|자세한 내용은 참조 [바이러스 백신 소프트웨어 &#40; 분석 플랫폼 시스템 &#41; ](antivirus-software.md).|  
|DSRM에 대 한 암호를 변경할 수 있습니다.<br /><br />(옵션)|자세한 내용은 참조 [디렉터리 서비스 복원 모드 &#40; DSRM &#41; &#40; AD 노드에 로그인 하기 위해 관리자 암호 설정 분석 플랫폼 시스템 &#41; ](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|소프트웨어 업데이트를 받을 어플라이언스를 구성<br /><br />좋습니다.|어플라이언스에는 SQL Server PDW 및 기본 소프트웨어 업데이트를 수신 하도록 구성 해야 합니다.<br /><br />자세한 내용은 참조 [Windows Server Update Services 구성 &#40; WSUS &#41; &#40; 분석 플랫폼 시스템 &#41; ](configure-windows-server-update-services-wsus.md). WSUS에 대 한 정보를 참조 하십시오. [소프트웨어 서비스 &#40; 분석 플랫폼 시스템 &#41; ](software-servicing.md).|  
|Hadoop 또는 Azure blob 저장소와 같은 외부 데이터에 대 한 연결을 구성 합니다.<br /><br />(옵션)|자세한 내용은 참조 [외부 데이터 &#40; PolyBase 연결 구성 분석 플랫폼 시스템 &#41; ](configure-polybase-connectivity-to-external-data.md).|  
|바이러스 백신 소프트웨어 구성<br /><br />(옵션)|타사 바이러스 백신 솔루션 외부와 접한 노드를 보호 하기 위해 사용할 수 있지만 필요 하지 않습니다. 지침을 따릅니다.|  
|백업 및 서버를 로드에 InfiniBand 네트워크 어댑터를 구성 합니다.<br /><br />(옵션)|백업 및 서버를 로드 InfiniBand 네트워크를 사용 하 여 SQL Server PDW에 연결을 구성 하려면 기기 현재 활성 InfiniBand 네트워크에 InfiniBand 연결을 확인 하도록 DNS를 허용 하도록 네트워크 어댑터를 구성 해야 합니다.|  
|원격 분석 데이터를 Microsoft로 보내도록 구성 합니다.<br /><br />(옵션)|원격 분석 데이터를 Microsoft로 보내지 분석 플랫폼 시스템을 구성 하려면는 제어 노드에에서 PowerShell 스크립트를 실행 해야 합니다. 구체적인 지침은 참조 [Microsoft &#40; 원격 분석 사용자 의견 보내기 SQL Server PDW &#41; ](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>관련 항목:  
[바이러스 백신 소프트웨어 &#40; 분석 플랫폼 시스템 &#41;](antivirus-software.md)  
[InfiniBand 네트워크 어댑터 &#40; 구성 합니다. SQL Server PDW &#41;](configure-infiniband-network-adapters.md)  
  
