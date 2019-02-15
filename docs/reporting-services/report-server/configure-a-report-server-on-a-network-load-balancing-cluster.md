---
title: 네트워크 부하 분산 클러스터에서 보고서 서버 구성 | Microsoft Docs
author: markingmyname
ms.author: maghan
manager: kfile
ms.prod: reporting-services, reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.date: 10/03/2018
ms.openlocfilehash: 26c8423308b07c570cf289113a00fbd07a1133aa
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041774"
---
# <a name="configure-a-report-server-on-a-network-load-balancing-cluster"></a>네트워크 부하 분산 클러스터에서 보고서 서버 구성

  NLB(네트워크 부하 분산) 클러스터에서 실행되도록 보고서 서버 확장을 구성하는 경우 다음을 수행해야 합니다.  
  
- 가상 서버 IP 주소에 매핑되는 가상 서버 이름을 통해 NLB 클러스터에 액세스할 수 있는지 확인합니다. 가상 서버 이름은 NLB 클러스터에 대한 단일 진입점을 구성하기 위해 필요합니다. 각 보고서 서버 인스턴스에 대한 URL을 구성할 때는 가상 서버 이름을 호스트로 지정하게 됩니다.  
  
- 대화형 보고서 보기를 지원하도록 뷰 상태 유효성 검사를 구성합니다. 대화형 보고서는 일반적으로 단일 사용자 세션 동안 사용자 동작에 대한 응답으로 새 데이터나 다른 데이터를 시각화하기 위해 여러 번 렌더링됩니다. 뷰 상태 유효성 검사를 구성하면 실제 요청을 제공하는 보고서 서버에 관계없이 사용자 세션 내에서 근접성이 유지됩니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 스케일 아웃 배포의 부하 분산을 위한 기능, 또는 공유 URL을 통해 단일 액세스 지점을 정의하는 기능을 제공하지 않습니다. 따라서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 스케일 아웃 배포를 지원하기 위한 별도의 소프트웨어 또는 하드웨어 NLB 클러스터 솔루션을 구현해야 합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 이미 NLB 클러스터에 속하는 노드에 설치하거나 먼저 스케일 아웃 배포를 구성한 후 클러스터 소프트웨어를 설치할 수 있습니다.  
  
## <a name="steps-for-report-server-deployment-on-an-nlb-cluster"></a>NLB 클러스터에서의 보고서 서버 배포 단계

 배포를 설치하고 구성하려면 다음 지침을 따르십시오.  
  
|단계|설명|자세한 정보|  
|----------|-----------------|----------------------|  
|1|NLB 클러스터의 서버 노드에서 Reporting Services를 설치하기 전에 스케일 아웃 배포를 위한 요구 사항을 확인합니다.|[스케일 아웃 배포 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 Reporting Services 기본 모드 &#40;Configuration Manager&#41;](https://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c)|  
|2|NLB 클러스터를 구성하고 제대로 작동하는지 확인합니다.<br /><br /> NLB 클러스터의 가상 서버 IP에 호스트 헤더 이름을 매핑합니다. 호스트 헤더 이름은 보고서 서버 URL에서 사용되며 IP 주소보다 기억하기 쉽고 입력하기도 편리합니다.|자세한 내용은 실행 중인 Windows 운영 체제 버전에 대한 Windows Server 제품 설명서를 참조하십시오.|  
|3|Windows 레지스트리에 저장된 **BackConnectionHostNames** 목록에 호스트 헤더의 NetBIOS와 FQDN(정규화된 도메인 이름)을 추가합니다. **방법 2: [KB 896861](https://support.microsoft.com/kb/896861)(https://support.microsoft.com/kb/896861)에 있는 호스트 이름 지정**의 단계를 사용하여 다음과 같이 적절하게 조정합니다. 즉, 이 KB 문서의**7단계** 에 설명된 것과 같이 "레지스트리 편집기를 끝낸 다음 IISAdmin 서비스를 다시 시작"하지 않고 컴퓨터를 다시 부팅하여 변경 내용이 적용되도록 합니다.<br /><br /> 예를 들어 호스트 헤더 이름 \<MyServer>가 Windows 컴퓨터 이름인 "contoso"의 가상 이름인 경우 FQDN 형식 "contoso.domain.com"을 참조할 수 있습니다. **BackConnectionHostNames**의 목록에 호스트 헤더 이름(MyServer)과 FQDN 이름(contoso.domain.com)을 모두 추가해야 합니다.|이 단계는 서버 환경의 로컬 컴퓨터에 NTLM 인증이 사용되어 루프백 연결이 생성되는 경우에 필요합니다.<br /><br /> 이 경우 보고서 관리자와 보고서 서버 간의 요청이 401(권한 없음) 오류와 함께 실패하게 됩니다.|  
|4|NLB 클러스터에 이미 속해 있는 노드에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 파일만 모드로 설치하고 스케일 아웃 배포를 위한 보고서 서버 인스턴스를 구성합니다.<br /><br /> 구성한 확장은 가상 서버 IP에 전송되는 요청에 응답하지 않을 수 있습니다. 가상 서버 IP를 사용하도록 확장을 구성하는 작업은 뷰 상태 유효성 검사를 구성한 후 그 다음 단계에서 수행됩니다.|[기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)|  
|5|뷰 상태 유효성 검사를 구성합니다.<br /><br /> 최상의 결과를 얻으려면 스케일 아웃 배포를 구성한 후에 가상 서버 IP를 사용하도록 보고서 서버 인스턴스를 구성하기 전에 이 단계를 수행하세요. 뷰 상태 유효성 검사를 먼저 구성하면 사용자가 대화형 보고서에 액세스할 때 상태 유효성 검사 실패에 대한 예외가 발생하는 것을 방지할 수 있습니다.|이 항목의[뷰 상태 유효성 검사 구성 방법](#ViewState) 을 참조하십시오.|  
|6|NLB 클러스터의 가상 서버 IP를 사용하도록 **Hostname** 및 **UrlRoot** 를 구성합니다.|이 항목의[Hostname 및 UrlRoot 구성 방법](#SpecifyingVirtualServerName) 을 참조하십시오.|  
|7|지정한 호스트 이름을 통해 서버에 액세스할 수 있는지 확인합니다.|이 항목의[보고서 서버 액세스 권한 확인](#Verify) 을 참조하십시오.|  
  
## <a name="ViewState"></a> 뷰 상태 유효성 검사 구성 방법

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
NLB 클러스터에서 스케일 아웃 배포를 실행하려면 사용자가 대화형 HTML 보고서를 볼 수 있도록 뷰 상태 유효성 검사를 구성해야 합니다.  보고서 서버 웹 서비스에 대해 이를 수행해야 합니다.
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
NLB 클러스터에서 스케일 아웃 배포를 실행하려면 사용자가 대화형 HTML 보고서를 볼 수 있도록 뷰 상태 유효성 검사를 구성해야 합니다.
::: moniker-end
  
 뷰 상태 유효성 검사는 ASP.NET에서 제어합니다. 뷰 상태 유효성 검사는 기본적으로 활성화되며 웹 서비스의 ID를 사용하여 유효성 검사를 수행합니다. 그러나 NLB 클러스터 시나리오에는 각기 다른 컴퓨터에서 실행되는 여러 개의 서비스 인스턴스 및 웹 서비스 ID가 있으며, 각 노드마다 서비스 ID가 다르기 때문에 하나의 프로세스 ID만으로는 유효성 검사를 수행할 수 없습니다.  
  
 이 문제를 해결하기 위해 뷰 상태 유효성 검사를 지원하도록 임의의 유효성 검사 키를 생성하고 각 보고서 서버 노드에서 같은 키를 사용하도록 수동으로 구성할 수 있습니다. 임의로 생성되는 모든 16진수 시퀀스를 사용할 수 있습니다. 16진수 시퀀스의 최대 길이는 유효성 검사 알고리즘(예: SHA1)에 따라 다릅니다.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

1. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 제공하는 자동 생성 기능을 사용하여 유효성 검사 키와 설명 키를 생성합니다. 어떤 방법을 사용하든 스케일 아웃 배포의 각 보고서 서버 인스턴스에 대한 Web.config 파일에 붙여넣을 수 있는 단일 <`MachineKey`> 항목을 만들어야 합니다.  
  
    다음 예에서는 확보해야 하는 값을 보여 줍니다. 구성 파일에 이 예를 복사하지 마세요. 키 값이 유효하지 않습니다.  
  
    ```xml
    <machineKey validationKey="123455555" decryptionKey="678999999" validation="SHA1" decryption="AES"/>  
    ```  
  
2. Reportserver에 대한 Web.config 파일을 열고 생성한 <`machineKey`> 요소를 <`system.web`> 섹션에 붙여넣습니다. 기본적으로 보고서 관리자 Web.config 파일은 \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\Reportserver\Web.config에 있습니다.  
  
3. 파일을 저장합니다.  
  
4. 스케일 아웃 배포의 각 보고서 서버에 대해 이전 단계를 반복합니다.  
  
5. \Reporting Services\Reportserver 폴더에 있는 모든 Web.Config 파일의 <`system.web`> 섹션에 동일한 <`machineKey`> 요소가 포함되어 있는지 확인합니다.  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

1. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 제공하는 자동 생성 기능을 사용하여 유효성 검사 키와 설명 키를 생성합니다. 어떤 방법을 사용하든 스케일 아웃 배포의 각 보고서 서버 인스턴스에 대한 RSReportServer.config 파일에 붙여넣을 수 있는 단일 \<**MachineKey**> 항목을 만들어야 합니다.

    다음 예에서는 확보해야 하는 값을 보여 줍니다. 구성 파일에 이 예를 복사하지 마십시오. 올바른 키 값이 아닙니다. 보고서 서버에는 올바른 대/소문자 구분이 필요합니다.

    ```xml
    <machineKey validationKey="123455555" decryptionKey="678999999" validation="SHA1" decryption="AES"/>
    ```

2. 파일을 저장합니다.

3. 스케일 아웃 배포의 각 보고서 서버에 대해 이전 단계를 반복합니다.  

4. \Reporting Services\Report Server 폴더에 있는 모든 RSReportServer.Config 파일에 동일한 \<**MachineKey**> 요소가 포함되어 있는지 확인합니다.

::: moniker-end

## <a name="SpecifyingVirtualServerName"></a> Hostname 및 UrlRoot 구성 방법

 NLB 클러스터에서 보고서 서버 스케일 아웃 배포를 구성하려면 서버 클러스터에 대한 단일 액세스 지점을 제공하는 단일 가상 서버 이름을 정의해야 합니다. 그런 다음 가상 서버 이름을 사용자 환경의 DNS(Domain Name Server)에 등록합니다.  
  
 가상 서버 이름을 정의한 후에는 RSReportServer.config 파일에서 보고서 서버 URL에 가상 서버 이름이 포함되도록 **Hostname** 및 **UrlRoot** 속성을 구성할 수 있습니다.  
  
 보고 환경에서 와일드카드 URL 예약을 사용하는 경우 **Hostname** 속성을 구성합니다. NLB 서버의 가상 서버 이름으로 사용할 **Hostname** 속성을 지정하면 보고 환경의 네트워크 트래픽이 NLB 서버로 전송됩니다. 그러면 NLB가 보고서 서버 노드에 요청을 배포합니다.  
  
 또한 Excel 또는 PDF 형식과 같은 정적 보고서로 내보낸 보고서나 메일 구독과 같은 구독을 통해 생성되는 보고서에서 보고서 링크가 작동하도록 **UrlRoot** 속성을 구성합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 또는 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007과 통합하거나 사용자 지정 웹 애플리케이션에서 보고서를 호스팅하는 경우 **UrlRoot** 속성만 구성해야 할 수 있습니다. 이 경우 **UrlRoot** 속성을 SharePoint 사이트 또는 웹 애플리케이션의 URL로 구성합니다. 이렇게 하면 보고 환경의 네트워크 트래픽이 보고서 서버나 NLB 클러스터가 아닌 보고서를 처리하는 애플리케이션으로 전송됩니다.  
  
 **ReportServerUrl**은 수정하지 마십시오. 이 URL을 수정하면 내부 요청이 처리될 때마다 가상 서버를 통해 별도의 왕복이 발생하게 됩니다. 자세한 내용은 [구성 파일의 URL&#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)를 참조하세요. 구성 파일을 편집하는 방법에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)를 참조하세요.  
  
1. 텍스트 편집기에서 RSReportServer.config를 엽니다.  
  
2. **\<서비스>** 섹션을 찾고 **Hostname** 값을 NLB 서버의 가상 서버 이름으로 바꿔 구성 파일에 다음 정보를 추가합니다.  
  
    ```xml
    <Hostname>virtual_server</Hostname>  
    ```  
  
3. **UrlRoot**찾기. 이 요소는 구성 파일에 지정되지 않지만 사용되는 기본값은 https:// 또는 `https://<computername>/<reportserver>` 형식의 URL입니다. 여기서 \<*reportserver*>는 보고서 서버 웹 서비스의 가상 디렉터리 이름입니다.  
  
4. 클러스터의 가상 이름을 포함하는 **UrlRoot** 값을 https:// 또는 `https://<virtual_server>/<reportserver>` 형식으로 입력합니다.  
  
5. 파일을 저장합니다.  
  
6. 스케일 아웃 배포의 각 보고서 서버에 대한 각 RSReportServer.config 파일에서 이 단계를 반복합니다.  
  
## <a name="Verify"></a> 보고서 서버 액세스 권한 확인

 가상 서버 이름을 통해 스케일 아웃 배포에 액세스할 수 있는지 확인합니다(예: `https://MyVirtualServerName/reportserver` 및 `https://MyVirtualServerName/reports`).  
  
 보고서 서버 로그 파일 또는 RS 실행 로그를 검토하여 실제로 보고서를 처리하는 노드를 확인할 수 있습니다. 실행 로그 테이블에는 특정 요청을 처리한 인스턴스를 나타내는 **InstanceName** 열이 포함되어 있습니다. 자세한 내용은 [온라인 설명서에서](../../reporting-services/report-server/reporting-services-log-files-and-sources.md) Reporting Services 로그 파일 및 소스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 참조하세요.  
  
 보고서 서버에 연결할 수 없으면 NLB를 검사하여 보고서 서버에 요청이 전송되었는지 확인하고 보고서 서버 HTTP 로그를 검토하여 보고서 서버에서 요청을 수신하고 있는지 확인합니다.  
  
### <a name="troubleshooting-failed-requests"></a>실패한 요청 문제 해결

 요청이 보고서 인스턴스에 도달하지 못한 경우 RSReportServer.config 파일을 확인하여 가상 서버 이름이 보고서 서버 URL의 호스트 이름으로 지정되었는지 살펴보십시오.  
  
1. 텍스트 편집기에서 RSReportServer.config 파일을 엽니다.  
  
2. \<**Hostname**>, \<**ReportServerUrl**> 및 \<**UrlRoot**>를 찾고 각 설정의 호스트 이름을 확인합니다. 호스트 이름이 올바르지 않은 경우에는 올바른 호스트 이름으로 바꾸십시오.  
  
 이러한 변경을 수행한 후 Reporting Services 구성 도구를 시작하면 \<**ReportServerUrl**> 설정이 기본값으로 변경될 수 있습니다. 구성 파일을 필요한 설정이 포함된 버전으로 바꾸어야 하는 경우에는 항상 해당 백업 복사본을 보관해 두십시오.  
  
## <a name="see-also"></a>참고 항목

 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [Reporting Services 기본 모드 보고서 서버 관리](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)