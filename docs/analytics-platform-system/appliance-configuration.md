---
title: 구성 검사 목록
description: 사용자 환경에 맞게 분석 플랫폼 시스템을 구성 하는 데 필요한 작업에 대 한 검사 목록을 제공 합니다. 어플라이언스를 사용 하려면 이러한 구성 작업이 필요 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 80fc899400be167badaae9d617d43a61e0d346b5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401461"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 어플라이언스 구성 검사 목록
사용자 환경에 맞게 분석 플랫폼 시스템을 구성 하는 데 필요한 작업에 대 한 검사 목록을 제공 합니다. 어플라이언스를 사용 하려면 이러한 구성 작업이 필요 합니다.  
  
> [!WARNING]  
> 분석 플랫폼 시스템**Configuration Manager** 를 사용 하는 것이 가장 좋은 방법 이며, 도구에서 사용할 수 있는 작업을 수행 하는 데 지원 되는 유일한 방법입니다.  
  
## <a name="BeforeTasks"></a>시작 하기 전에  
  
### <a name="prerequisites"></a>필수 구성 요소  
  
1.  어플라이언스는 데이터 센터에 설치 되어 있어야 합니다.  
  
2.  IHV에서 제공 하는 다음 정보가 있는지 확인 합니다.  
  
    -   PDW 제어 노드에 대 한 외부 IP 주소 (*PDW_region*CTL01)  
  
    -   어플라이언스 도메인 이름  
  
    -   어플라이언스 도메인 관리자의 사용자 이름 및 암호  
  
3.  신뢰할 수 있는 인증서를 가져옵니다. 클라이언트에서 보안 연결을 사용 하 여 **관리 콘솔** 에 연결 하도록 허용 하는 이후 단계에서이를 가져옵니다. 인증서를 암호로 보호 된 PFX 파일의 Control 노드에 저장 합니다.  
  
4.  다음 단계를 사용 하 여 **Configuration Manager**를 시작 합니다.  
  
    1.  **원격 데스크톱** 을 사용 하 여 PDW 컨트롤 노드*PDW_region*(CTL01)에 연결 합니다. CTL01에 대 한 외부 IP 주소를 사용 하 여 연결 해야 할 수도 있습니다.  
  
    2.  PDW 컨트롤 노드의 **시작** 메뉴에서 **Configuration Manager** 를 시작 합니다. Configuration Manager의 첫 번째 화면에는 IHV에서 만든 어플라이언스 토폴로지가 표시 됩니다. 기기의 일부로 SQL Server PDW 소프트웨어에서 인식 하는 하드웨어 노드 목록입니다. 어플라이언스 토폴로지 화면에서 설정을 변경할 필요가 없습니다.  
  
## <a name="CMTasks"></a>Configuration Manager 작업 수행  
Systemwcm (SQL Server PDW**Configuration Manager** )는 시스템 관리자가 어플라이언스 수준 작업을 수행 하 고 어플라이언스 수준 설정을 변경 하 SQL Server PDW는 데 사용 하는 어플라이언스 관리 도구입니다. 예를 들어 암호를 재설정 하 고, 표준 시간대를 설정 하 고, IP 주소를 변경 하 고, SSL 인증서를 구성 하 고, 방화벽을 통해 원격 액세스를 사용 하도록 설정 하 고, 어플라이언스를 시작 또는 중지 하 고, 즉시 파일 초기화를 설정  
  
**Configuration Manager** 를 사용 하 여 다음 구성 작업을 수행 합니다.  
  
|구성 태스크|설명|  
|----------------------|---------------|  
|물리적 구성 요소 이름에 익숙해져야 합니다.|[PDW 및 어플라이언스 패브릭 물리적 구성 요소 &#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|시작 SQL Server PDW Configuration Manager|[Configuration Manager &#40;Analytics Platform System을 시작&#41;](launch-the-configuration-manager.md)|  
|도메인 관리자 암호 변경|어플라이언스에는 어플라이언스 내에서 노드를 인증 하는 데 사용 되는 개인 Windows Active Directory Domain Services 있습니다.<br /><br />IHV는 기본 도메인 관리자 암호를 사용 하 여 어플라이언스를 설정 합니다. 이는 안전한 암호로 변경 해야 합니다.<br /><br />도메인 관리자 암호를 변경 하는 데 지원 되는 유일한 방법은 **Configuration Manager** 입니다.<br /><br />자세한 내용은 [암호 재설정 &#40;분석 플랫폼 시스템&#41;](password-reset.md)을 참조 하세요.|  
|**Sa** 로그온에 대 한 암호를 변경 합니다.|SQL Server PDW **sa**라는 시스템 관리자 로그온이 있습니다. **Sa** 로그온에는 모든 권한이 있습니다. 모든 사용 권한을 부여, 거부 또는 취소할 수 있습니다. 모든 시스템 뷰를 볼 수도 있습니다.<br /><br />자세한 내용은 [암호 재설정 &#40;분석 플랫폼 시스템&#41;](password-reset.md)을 참조 하세요.|  
|어플라이언스 표준 시간대 설정|모든 어플라이언스 노드에 대 한 시간 (로컬 또는 기타 원하는 시간)을 설정 합니다.<br /><br />자세한 내용은 [어플라이언스 표준 시간대 구성 &#40;분석 플랫폼 시스템&#41;](appliance-time-zone-configuration.md)을 참조 하세요.|  
|SQL Server PDW 어플라이언스에 대 한 외부 연결 네트워크 설정 지정|[어플라이언스 네트워크 구성 &#40;분석 플랫폼 시스템&#41;](appliance-network-configuration.md)|  
|관리 콘솔에 대 한 보안 인증서 가져오기|인증서는 [관리 콘솔 &#40;Analytics Platform System&#41;을 사용 하 ](monitor-the-appliance-by-using-the-admin-console.md)여 HTTPS를 통해 모니터 어플라이언스에 SSL(SECURE SOCKETS LAYER) (SSL) 연결을 제공할 수 있습니다. 기본적으로 **관리 콘솔** 에는 개인 정보를 제공 하지만 서버 인증은 제공 하지 않는 자체 서명 된 인증서가 포함 되어 있습니다. 이 인증서는 사용자가 연결할 때 Internet Explorer에 "이 웹 사이트의 보안 인증서에 문제가 있습니다." 라는 오류도 반환 합니다. 이 연결에서 클라이언트와 서버 간에 진행 중인 데이터를 암호화 하더라도 공격자의 연결이 여전히 위험에 노출 됩니다.<br /><br />SQL Server PDW 관리자는 보안 연결을 설정 하 고 Internet Explorer에서 보고 하는 오류를 제거 하기 위해 클라이언트에서 인식 하는 신뢰할 수 있는 인증 기관에 연결 된 인증서를 즉시 획득 해야 합니다. 이를 위해서는 관리 콘솔에 액세스 하기 위해 사용자가 브라우저 주소 표시줄에 입력 하는 값과 일치 하는 컨트롤 노드의 가상 IP 주소를 매핑하는 정규화 된 도메인 이름 (권장) 또는 인증서 이름을 사용 해야 합니다.<br /><br />**Configuration Manager** 를 사용 하 여 신뢰할 수 있는 인증서를 추가 하거나 제거 합니다. Microsoft Windows HTTP 서비스 인증서 구성 도구 (`winHttpCertCfg.exe`)를 사용 하 여 인증서를 직접 관리 하는 것은 지원 되지 않습니다.<br /><br />자세한 내용은 [PDW 인증서 프로 비전 &#40;분석 플랫폼 시스템&#41;](pdw-certificate-provisioning.md)을 참조 하세요.|
|기능 스위치|분석 플랫폼 시스템 AU7에 도입 된 기능 스위치에 대 한 정보를 표시 합니다. 이 페이지를 사용 하 여 분석 플랫폼 시스템의 기능 및 설정을 업데이트 하거나 사용 하지 않도록 설정할 수 있습니다. 기능 스위치 값을 변경 하려면 서비스를 다시 시작 해야 합니다.<br /><br />자세한 내용은 [PDW 기능 스위치 &#40;분석 플랫폼 시스템&#41;](appliance-feature-switch.md)을 참조 하세요.|
|SQL Server PDW 어플라이언스의 특정 포트에 대 한 액세스를 허용 하거나 차단 하는 Windows 방화벽 규칙을 사용 하거나 사용 하지 않도록 설정 합니다.|IHV는 어플라이언스를 정상적으로 작동 하는 데 필요한 방화벽 규칙을 구성 하 고 사용 하도록 설정 합니다. 대부분의 경우 방화벽 규칙을 사용 하거나 사용 하지 않도록 설정 하지 않습니다.<br /><br />자세한 내용은 [PDW 방화벽 구성 &#40;분석 플랫폼 시스템&#41;](pdw-firewall-configuration.md)을 참조 하세요.|  
|SQL Server PDW 어플라이언스 시작 및 중지|SQL Server PDW 어플라이언스를 중지 하거나 시작 합니다. 자세한 내용은 [PDW Services Status &#40;Analytics Platform System&#41;](pdw-services-status.md)를 참조 하세요.|  
|**권한** 대화 상자를 사용 하 여 즉시 파일 초기화 옵션 검토|즉시 파일 초기화는 데이터 파일 작업을 보다 신속 하 게 실행할 수 있는 SQL Server 기능입니다. 네트워크 서비스 계정에 SE_MANAGE_VOLUME_NAME 권한이 부여 된 경우에만 SQL Server PDW에서 사용 하도록 설정 됩니다. 기본적으로 꺼져 있습니다.<br /><br />자세한 내용은 [인스턴트 파일 초기화 구성 &#40;분석 플랫폼 시스템&#41;](instant-file-initialization-configuration.md)을 참조 하세요.|  
|백업에서 master 데이터베이스 복원|현재 **master** 데이터베이스를 삭제 하 고 백업으로 바꿉니다. 자세한 내용은 [Restore The Master Database &#40;Analytics Platform System&#41;](restore-the-master-database.md)을 참조 하세요.|  
  
## <a name="AddTasks"></a>추가 구성 작업을 수행 합니다.  
**Configuration Manager** 작업을 수행한 후 다음 추가 구성 작업 목록을 수행 합니다. 이러한 작업 중 일부는 선택 사항입니다.  
  
|구성 태스크|설명|  
|----------------------|---------------|  
|외부에 연결 된 노드에 대해 SQL Server PDW 어플라이언스에서 타사 바이러스 백신 소프트웨어를 설치 하 고 구성할 수 있습니다.<br /><br />(선택 사항)|자세한 내용은 [바이러스 백신 소프트웨어 &#40;분석 플랫폼 시스템&#41;](antivirus-software.md)을 참조 하세요.|  
|DSRM의 암호를 변경할 수 있습니다.<br /><br />(선택 사항)|자세한 내용은 [디렉터리 서비스 복원 모드에서 AD 노드에 로그온 하기 위한 관리자 암호 설정 &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)을 참조 하세요.|  
|소프트웨어 업데이트를 받도록 어플라이언스 구성<br /><br />좋습니다.|SQL Server PDW 및 기본 소프트웨어에 대 한 업데이트를 수신 하도록 어플라이언스를 구성 해야 합니다.<br /><br />자세한 내용은 [Configure Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)를 참조 하세요. WSUS에 대 한 자세한 내용은 [소프트웨어 서비스 &#40;분석 플랫폼 시스템&#41;](software-servicing.md)을 참조 하세요.|  
|Hadoop 또는 Azure blob 저장소와 같은 외부 데이터에 대 한 연결을 구성 합니다.<br /><br />(선택 사항)|자세한 내용은 [외부 데이터에 대 한 PolyBase 연결 구성 &#40;분석 플랫폼 시스템&#41;](configure-polybase-connectivity-to-external-data.md)을 참조 하세요.|  
|바이러스 백신 소프트웨어 구성<br /><br />(선택 사항)|타사 바이러스 백신 솔루션은 외부에 연결 된 노드를 보호 하는 데 사용할 수 있지만 반드시 필요한 것은 아닙니다. 의 지침을 따릅니다.|  
|백업 및 서버 로드 시 InfiniBand 네트워크 어댑터 구성<br /><br />(선택 사항)|InfiniBand 네트워크를 사용 하 여 SQL Server PDW에 연결 하기 위해 백업 및 로드 서버를 구성 하려면 어플라이언스 DNS가 현재 활성 InfiniBand 네트워크에 대 한 InfiniBand 연결을 확인할 수 있도록 네트워크 어댑터를 구성 해야 합니다.|  
|Microsoft에 원격 분석 데이터를 보내도록 구성<br /><br />(선택 사항)|Microsoft로 원격 분석 데이터를 보내도록 분석 플랫폼 시스템을 구성 하려면 제어 노드에서 PowerShell 스크립트를 실행 해야 합니다. 특정 지침은 [Microsoft &#40;SQL Server PDW&#41;에 원격 분석 사용자 의견 보내기를 ](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)참조 하세요.|  
  
## <a name="see-also"></a>참고 항목  
[바이러스 백신 소프트웨어 &#40;분석 플랫폼 시스템&#41;](antivirus-software.md)  
[InfiniBand 네트워크 어댑터 &#40;SQL Server PDW&#41;구성](configure-infiniband-network-adapters.md)  
  
