---
title: "Reporting Services 인증에 대한 확장된 보호 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb5c6f4a-3ed5-430b-a712-d5ed4b6b9b2b
caps.latest.revision: "15"
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 6f554b9ec04d894fbcd3da37e1bd326b39508571
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="extended-protection-for-authentication-with-reporting-services"></a>Reporting Services 인증에 대한 확장된 보호

  확장된 보호는 최신 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 운영 체제에서 향상된 기능 집합입니다. 확장된 보호는 응용 프로그램에서 자격 증명과 인증을 보호하는 방법을 개선합니다. 이 기능 자체는 자격 증명 전달과 같은 특정 공격에 대해 직접적인 보호 기능을 제공하지 않지만 인증에 대해 확장된 보호를 적용할 수 있는 인프라를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 같은 응용 프로그램에 제공합니다.  
  
 확장된 보호에서 주로 향상된 인증 기능은 서비스 바인딩과 채널 바인딩입니다. 채널 바인딩은 CBT(채널 바인딩 토큰)를 사용하여 두 끝점 간에 설정된 채널이 손상되지 않았는지 확인합니다. 서비스 바인딩은 SPN(서비스 사용자 이름)을 사용하여 인증 토큰의 대상이 유효한지 검사합니다. 확장된 보호에 대한 자세한 내용은 [확장된 보호를 사용하는 Windows 통합 인증(Integrated Windows Authentication with Extended Protection)](http://go.microsoft.com/fwlink/?LinkId=179922)을 참조하십시오.  
  
SSRS(SQL Server Reporting Services)는 운영 체제에서 사용하도록 설정되고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 구성된 확장된 보호를 지원하고 적용합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 기본적으로 Negotiate 또는 NTLM 인증을 지정하는 요청을 수락하므로 운영 체제의 확장된 보호 지원 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장된 보호 기능을 활용할 수 있습니다.  
  
> [!IMPORTANT]  
>  Windows에서는 기본적으로 확장된 보호를 사용할 수 없습니다. Windows에서 확장된 보호를 사용하는 방법은 [인증에 대한 확장된 보호](http://go.microsoft.com/fwlink/?LinkID=178431)를 참조하십시오. 운영 체제 및 클라이언트 인증 스택 모두 확장된 보호를 지원해야 인증이 성공합니다. 이전 운영 체제의 경우 확장된 보호를 사용할 수 있도록 컴퓨터가 완전하게 준비되려면 업데이트를 여러 개 설치해야 할 수도 있습니다. 확장된 보호와 관련된 최신 개발 내용은 [확장된 보호에 대한 업데이트된 정보](http://go.microsoft.com/fwlink/?LinkId=183362)를 참조하십시오.  

## <a name="reporting-services-extended-protection-overview"></a>Reporting Services 확장된 보호 개요

SSRS는 운영 체제에서 사용하도록 설정된 확장된 보호를 지원하고 적용합니다. 운영 체제에서 확장된 보호를 지원하지 않거나 해당 기능을 사용하지 않을 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장된 보호 기능으로 인해 인증이 실패합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장된 보호를 사용하려면 SSL 인증서가 필요합니다. 자세한 내용은 [기본 모드 보고서 서버에서 SSL 연결 구성](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 기본적으로 확장된 보호를 사용할 수 없습니다. **rsreportserver.config** 구성 파일을 수정하거나 WMI API를 사용하여 구성 파일을 업데이트하면 이 기능을 사용할 수 있습니다. SSRS에서는 확장된 보호 설정을 수정하거나 볼 수 있는 사용자 인터페이스를 제공하지 않습니다. 자세한 내용은 이 항목의 [구성 설정](#ConfigurationSettings) 섹션을 참조하십시오.  
  
 확장된 보호 설정의 변경이나 잘못 구성된 설정으로 인해 발생하는 일반적인 문제는 명확한 오류 메시지나 대화 상자 창을 통해 표시되지 않습니다. 확장된 보호 구성 및 호환성과 관련된 문제가 있으면 인증이 실패하고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추적 로그에 오류가 기록됩니다.  
  
> [!IMPORTANT]  
>  일부 데이터 액세스 기술은 확장된 보호를 지원하지 않을 수 있습니다. 데이터 액세스 기술은 SQL Server 데이터 원본 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 카탈로그 데이터베이스에 연결하는 데 사용됩니다. 데이터 액세스 기술이 확장된 보호를 지원하지 않는 경우 다음과 같이 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 영향을 미칩니다.  
>   
>  -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 카탈로그 데이터베이스를 실행하는 SQL Server에서 확장된 보호를 사용할 수 없습니다. 사용할 경우 보고서 서버에서 카탈로그 데이터베이스에 연결되지 않고 인증 오류가 반환됩니다.  
> -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 데이터 원본으로 사용되는 SQL Server에서 확장된 보호를 사용할 수 없습니다. 사용할 경우 보고서 서버에서 보고서 데이터 원본에 연결하려는 시도가 실패하고 인증 오류가 반환됩니다.  
>   
>  데이터 액세스 기술에 대한 설명서에서 확장된 보호 지원에 대한 정보를 참조할 수 있습니다.  
  
### <a name="upgrade"></a>업그레이드  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버를 SQL Server 2016로 업그레이드하면 기본값이 지정된 구성 설정이 **rsreportserver.config** 파일에 추가됩니다. 설정이 이미 있으면 SQL Server 2016 설치 시 해당 설정이 **rsreportserver.config** 파일에 유지됩니다.  
  
-   이 구성 설정이 **rsreportserver.config** 구성 파일에 추가될 때 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장된 보호 기능의 기본 동작이 해제되므로 이 항목의 설명에 따라 기능을 사용하도록 설정해야 합니다. 자세한 내용은 이 항목의 [구성 설정](#ConfigurationSettings) 섹션을 참조하십시오.  
  
-   **RSWindowsExtendedProtectionLevel** 설정의 기본값은 **Off**입니다.  
  
-   **RSWindowsExtendedProtectionScenario** 설정의 기본값은 **Proxy**입니다.  
  
-   업그레이드 관리자는 운영 체제나 현재 설치된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 확장된 보호 지원을 사용할 수 있는지 여부를 확인하지 않습니다.  
  
### <a name="what-reporting-services-extended-protection-does-not-cover"></a>Reporting Services 확장된 보호에서 다루지 않는 기능  
 다음과 같은 기능 영역 및 시나리오는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장된 보호 기능에서 지원되지 않습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 사용자 지정 보안 확장 프로그램을 만든 사람은 확장된 보호에 대한 지원을 사용자 지정 보안 확장 프로그램에 추가해야 합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치에서 사용하거나 추가된 타사 구성 요소는 확장된 보호를 지원하도록 타사 공급업체에서 업데이트해야 합니다. 자세한 내용은 타사 공급업체에 문의하십시오.  
  
## <a name="deployment-scenarios-and-recommendations"></a>배포 시나리오 및 권장 사항  
 다음 시나리오는 다양한 배포 및 토폴로지와 이들을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장된 보호로 보안 설정하는 데 필요한 권장 구성을 보여 줍니다.  
  
### <a name="direct"></a>직접  
 이 시나리오는 인트라넷 환경 등에서 보고서 서버에 직접 연결하는 경우를 보여 줍니다.  
  
|시나리오|시나리오 다이어그램|보안 설정 방법|  
|--------------|----------------------|-------------------|  
|직접 SSL 통신.<br /><br /> 보고서 서버가 클라이언트에서 보고서 서버로의 채널 바인딩을 적용합니다.|![RS_ExtendedProtection_DirectSSL](../../reporting-services/security/media/rs-extendedprotection-directssl.gif "RS_ExtendedProtection_DirectSSL")<br /><br /> 1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버|**RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Direct**로 설정합니다.<br /><br /> <br /><br /> -채널 바인딩에 SSL 채널이 사용되기 때문에 서비스 바인딩이 필요하지 않습니다.|  
|직접 HTTP 통신. 보고서 서버가 클라이언트에서 보고서 서버로의 서비스 바인딩을 적용합니다.|![RS_ExtendedProtection_Direct](../../reporting-services/security/media/rs-extendedprotection-direct.gif "RS_ExtendedProtection_Direct")<br /><br /> 1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버|**RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Any**로 설정합니다.<br /><br /> <br /><br /> -SSL 채널이 없으므로 채널 바인딩을 적용할 수 없습니다.<br /><br /> -서비스 바인딩의 유효성을 검사할 수는 있지만 채널 바인딩이 없으면 보안이 완전하지 않으며 서비스 바인딩만 사용하는 경우에는 기본적인 위협만 방지할 수 있습니다.|  
  
### <a name="proxy-and-network-load-balancing"></a>프록시 및 네트워크 부하 분산  
 클라이언트 응용 프로그램이 인증을 위해 SSL을 수행하고 서버에 자격 증명을 전달하는 장치나 소프트웨어(예: 익스트라넷, 인터넷 또는 보안 인트라넷)에 연결합니다. 클라이언트가 프록시에 연결하거나 모든 클라이언트가 프록시를 사용합니다.  
  
 NLB(네트워크 부하 분산) 장치를 사용할 때와 같은 경우입니다.  
  
|시나리오|시나리오 다이어그램|보안 설정 방법|  
|--------------|----------------------|-------------------|  
|HTTP 통신. 보고서 서버가 클라이언트에서 보고서 서버로의 서비스 바인딩을 적용합니다.|![RS_ExtendedProtection_Indirect](../../reporting-services/security/media/rs-extendedprotection-indirect.gif "RS_ExtendedProtection_Indirect")<br /><br /> 1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버<br /><br /> 3) 프록시|**RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Any**로 설정합니다.<br /><br /> <br /><br /> -SSL 채널이 없으므로 채널 바인딩을 적용할 수 없습니다.<br /><br /> -서비스 바인딩이 제대로 적용되려면 보고서 서버가 프록시 서버의 이름을 인식하도록 구성해야 합니다.|  
|HTTP 통신.<br /><br /> 보고서 서버가 클라이언트에서 프록시로의 채널 바인딩 및 클라이언트에서 보고서 서버로의 서비스 바인딩을 적용합니다.|![RS_ExtendedProtection_Indirect_SSL](../../reporting-services/security/media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버<br /><br /> 3) 프록시|Set <br />                    **RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Proxy**로 설정합니다.<br /><br /> <br /><br /> -프록시에 대한 SSL 채널을 사용할 수 있으므로 프록시로의 채널 바인딩이 적용될 수 있습니다.<br /><br /> -서비스 바인딩도 적용될 수 있습니다.<br /><br /> -보고서 서버에서 프록시 이름을 알 수 있어야 하므로 보고서 서버 관리자는 호스트 헤더를 사용하여 프록시에 대한 URL 예약을 만들거나 Windows 레지스트리 항목 **BackConnectionHostNames**에서 프록시 이름을 구성해야 합니다.|  
|보안 프록시를 사용한 간접 HTTPS 통신. 보고서 서버가 클라이언트에서 프록시로의 채널 바인딩 및 클라이언트에서 보고서 서버로의 서비스 바인딩을 적용합니다.|![RS_ExtendedProtection_IndirectSSLandHTTPS](../../reporting-services/security/media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버<br /><br /> 3) 프록시|Set <br />                    **RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Proxy**로 설정합니다.<br /><br /> <br /><br /> -프록시에 대한 SSL 채널을 사용할 수 있으므로 프록시로의 채널 바인딩이 적용될 수 있습니다.<br /><br /> -서비스 바인딩도 적용될 수 있습니다.<br /><br /> -보고서 서버에서 프록시 이름을 알 수 있어야 하므로 보고서 서버 관리자는 호스트 헤더를 사용하여 프록시에 대한 URL 예약을 만들거나 Windows 레지스트리 항목 **BackConnectionHostNames**에서 프록시 이름을 구성해야 합니다.|  
  
### <a name="gateway"></a>게이트웨이  
 이 시나리오는 SSL을 수행하고 사용자를 인증하는 장치나 소프트웨어에 연결하는 클라이언트 응용 프로그램을 설명합니다. 그런 다음 이 장치나 소프트웨어는 사용자의 컨텍스트 또는 다른 사용자의 컨텍스트를 가장하여 보고서 서버로 요청을 보냅니다.  
  
|시나리오|시나리오 다이어그램|보안 설정 방법|  
|--------------|----------------------|-------------------|  
|간접 HTTP 통신.<br /><br /> 게이트웨이가 클라이언트에서 게이트로의 채널 바인딩을 적용합니다. 게이트웨이에서 보고서 서버로의 서비스 바인딩이 있습니다.|![RS_ExtendedProtection_Indirect_SSL](../../reporting-services/security/media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버<br /><br /> 3) 게이트웨이 장치|**RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Any**로 설정합니다.<br /><br /> <br /><br /> -게이트웨이가 컨텍스트를 가장하여 새 NTLM 토큰을 만들기 때문에 클라이언트에서 보고서 서버로 채널을 바인딩할 수 없습니다.<br /><br /> -게이트웨이에서 보고서 서버로의 SSL이 없으므로 채널 바인딩이 적용될 수 없습니다.<br /><br /> -서비스 바인딩은 적용될 수 있습니다.<br /><br /> -채널 바인딩을 적용하려면 관리자가 게이트웨이 장치를 구성해야 합니다.|  
|보안 게이트웨이를 사용한 간접 HTTPS 통신. 게이트웨이가 클라이언트에서 게이트웨이로의 채널 바인딩을 적용하고 보고서 서버가 게이트웨이에서 보고서 서버로의 채널 바인딩을 적용합니다.|![RS_ExtendedProtection_IndirectSSLandHTTPS](../../reporting-services/security/media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버<br /><br /> 3) 게이트웨이 장치|**RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Direct**로 설정합니다.<br /><br /> <br /><br /> -게이트웨이가 컨텍스트를 가장하여 새 NTLM 토큰을 만들기 때문에 클라이언트에서 보고서 서버로 채널을 바인딩할 수 없습니다.<br /><br /> -게이트웨이에서 보고서 서버로의 SSL은 채널 바인딩이 적용될 수 있음을 의미합니다.<br /><br /> -서비스 바인딩이 필요하지 않습니다.<br /><br /> -채널 바인딩을 적용하려면 관리자가 게이트웨이 장치를 구성해야 합니다.|  
  
### <a name="combination"></a>결합  
 이 시나리오는 클라이언트가 프록시에 연결하는 익스트라넷 또는 인터넷 환경을 보여 줍니다. 이 시나리오는 클라이언트가 보고서 서버에 연결하는 인트라넷 환경과 결합되어 있습니다.  
  
|시나리오|시나리오 다이어그램|보안 설정 방법|  
|--------------|----------------------|-------------------|  
|클라이언트가 보고서 서버 서비스에 간접 및 직접 액세스(클라이언트에서 프록시로의 연결 또는 클라이언트에서 보고서 서버로의 연결에 SSL이 사용되지 않음)|1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버<br /><br /> 3) 프록시<br /><br /> 4) 클라이언트 응용 프로그램|**RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Any**로 설정합니다.<br /><br /> <br /><br /> -클라이언트에서 보고서 서버로의 서비스 바인딩이 적용될 수 있습니다.<br /><br /> -보고서 서버에서 프록시 이름을 알 수 있어야 하므로 보고서 서버 관리자는 호스트 헤더를 사용하여 프록시에 대한 URL 예약을 만들거나 Windows 레지스트리 항목 **BackConnectionHostNames**에서 프록시 이름을 구성해야 합니다.|  
|클라이언트가 보고서 서버에 간접 및 직접 액세스(클라이언트가 프록시 또는 보고서 서버에 대한 SSL 연결 설정)|![RS_ExtendedProtection_CombinationSSL](../../reporting-services/security/media/rs-extendedprotection-combinationssl.gif "RS_ExtendedProtection_CombinationSSL")<br /><br /> 1) 클라이언트 응용 프로그램<br /><br /> 2) 보고서 서버<br /><br /> 3) 프록시<br /><br /> 4) 클라이언트 응용 프로그램|**RSWindowsExtendedProtectionLevel** 을 **Allow** 또는 **Require**로 설정합니다.<br /><br /> **RSWindowsExtendedProtectionScenario** 를 **Proxy**로 설정합니다.<br /><br /> <br /><br /> -채널 바인딩이 사용될 수 있습니다.<br /><br /> -보고서 서버에서 프록시 이름을 알 수 있어야 하므로 보고서 서버 관리자가 호스트 헤더를 사용하여 프록시에 대한 URL 예약을 만들거나 Windows 레지스트리 항목 **BackConnectionHostNames**에서 프록시 이름을 구성해야 합니다.|  
  
## <a name="configuring-reporting-rervices-extended-protection"></a>Reporting Services 확장된 보호 구성  
 **rsreportserver.config** 파일에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장된 보호의 동작을 제어하는 구성 값이 있습니다.  
  
 **rsreportserver.config** 파일을 사용하고 편집하는 방법은 [RSReportServer 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요. WMI API를 사용하여 확장된 보호 설정을 변경하고 검토할 수도 있습니다. 자세한 내용은 [SetExtendedProtectionSettings 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)을 참조하십시오.  
  
 구성 설정 유효성 검사에 실패하면 보고서 서버에서 **RSWindowsNTLM**, **RSWindowsKerberos** 및 **RSWindowsNegotiate** 인증 유형을 사용할 수 없습니다.  
  
###  <a name="ConfigurationSettings"></a> Reporting Services 확장된 보호에 대한 구성 설정  
 다음 표에서는 **rsreportserver.config** 파일에 나오는 확장된 보호 구성 설정에 대한 정보를 제공합니다.  
  
|설정|Description|  
|-------------|-----------------|  
|**RSWindowsExtendedProtectionLevel**|확장된 보호를 적용하는 수준을 지정합니다. 유효한 값은<br /><br /> **Off**: 기본값입니다. 채널 바인딩이나 서비스 바인딩을 확인하지 않도록 지정합니다.<br /><br /> **Allow** 를 사용하는 경우 확장된 보호가 지원은 되지만 반드시 사용할 필요는 없습니다.  이 값을 사용하는 경우 다음 사항이 지정됩니다.<br /><br /> -확장된 보호를 지원하는 운영 체제에서 실행되는 클라이언트 응용 프로그램에 대해 확장된 보호가 적용됩니다. - **RsWindowsExtendedProtectionScenario**를 설정하여 보호 적용 방법을 결정합니다.<br /><br /> -확장된 보호를 지원하지 않는 운영 체제에서 실행되는 응용 프로그램에 대해 인증이 허용됩니다.<br /><br /> **Require** 를 사용하는 경우 다음 사항이 지정됩니다.<br /><br /> -확장된 보호를 지원하는 운영 체제에서 실행되는 클라이언트 응용 프로그램에 대해 확장된 보호가 적용됩니다.<br /><br /> -확장된 보호를 지원하지 않는 운영 체제에서 실행되는 응용 프로그램에 대해 인증이 허용되지 **않습니다** .|  
|**RsWindowsExtendedProtectionScenario**|유효성을 검사할 확장된 보호의 형식(채널 바인딩, 서비스 바인딩, 둘 다)을 지정합니다. 유효한 값은<br /><br /> **Proxy**: 기본값입니다. 이 값을 사용하는 경우 다음 사항이 지정됩니다.<br /><br /> -채널 바인딩 토큰이 있으면 Windows NTLM, Kerberos 및 협상 인증이 지정됩니다.<br /><br /> -서비스 바인딩이 적용됩니다.<br /><br /> **Any** 를 사용하는 경우 다음 사항이 지정됩니다.<br /><br /> -Windows NTLM, Kerberos 및 협상 인증이 지정되며 채널 바인딩은 필요하지 않습니다.<br /><br /> -서비스 바인딩이 적용됩니다.<br /><br /> **Direct** 를 사용하는 경우 다음 사항이 지정됩니다.<br /><br /> --CBT가 있고, 현재 서비스로의 SSL 연결이 있으며, SSL 연결의 CBT가 NTLM/Kerberos/협상 토큰의 CBT와 일치하면 Windows NTLM, Kerberos 및 협상 인증이 지정됩니다.<br /><br /> -서비스 바인딩이 적용되지 않습니다.<br /><br /> <br /><br /> 참고: **RsWindowsExtendedProtectionLevel** 이 **OFF** 로 설정되어 있으면 **RsWindowsExtendedProtectionScenario**설정은 무시됩니다.|  
  
 **rsreportserver.config** 구성 파일의 항목 예:  
  
```  
<Authentication>  
         <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
         <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionLevel>  
</Authentication>  
```  
  
## <a name="service-binding-and-included-spns"></a>서비스 바인딩 및 포함된 SPN  
 서비스 바인딩은 SPN(서비스 사용자 이름)을 사용하여 인증 토큰의 대상이 유효한지 검사합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 기존 URL 예약 정보를 사용하여 유효한 것으로 간주되는 SPN 목록을 만듭니다. SPN 및 URL 모두의 유효성을 검사하는 데 URL 예약 정보를 사용할 경우 시스템 관리자가 단일 위치에서 둘 모두를 관리할 수 있습니다.  
  
 유효한 SPN 목록은 보고서 서버가 시작될 때, 확장된 보호의 구성 설정이 변경될 때 또는 응용 프로그램 도메인이 재활용될 때 업데이트됩니다.  
  
 유효한 SPN 목록은 응용 프로그램마다 고유합니다. 예를 들어 보고서 관리자와 보고서 서버에서 각각 다른 유효한 SPN 목록이 계산됩니다.  
  
 응용 프로그램에 대해 계산되는 유효한 SPN 목록은 다음 요인에 따라 결정됩니다.  
  
-   각 URL 예약  
  
-   Reporting Services 서비스 계정에 대해 도메인 컨트롤러에서 검색된 각 SPN  
  
-   URL 예약에 와일드카드 문자('*' 또는 '+')가 포함된 경우 보고서 서버는 호스트 컬렉션에서 각 항목을 추가합니다.  
  
### <a name="hosts-collection-sources"></a>호스트 컬렉션 원본  
 다음 표에서는 호스트 컬렉션의 가능한 원본을 보여 줍니다.  
  
|원본 유형|Description|  
|--------------------|-----------------|  
|ComputerNameDnsDomain|로컬 컴퓨터에 할당된 DNS 도메인의 이름입니다. 로컬 컴퓨터가 클러스터의 노드인 경우 클러스터 가상 서버의 DNS 도메인 이름이 사용됩니다.|  
|ComputerNameDnsFullyQualified|로컬 컴퓨터를 고유하게 식별하는 정규화된 DNS 이름입니다. 이 이름은 *HostName*.*DomainName*형식으로 DNS 호스트 이름과 DNS 도메인 이름을 결합한 것입니다. 로컬 컴퓨터가 클러스터의 노드인 경우 클러스터 가상 서버의 정규화된 DNS 이름이 사용됩니다.|  
|ComputerNameDnsHostname|로컬 컴퓨터의 DNS 호스트 이름입니다. 로컬 컴퓨터가 클러스터의 노드인 경우 클러스터 가상 서버의 DNS 호스트 이름이 사용됩니다.|  
|ComputerNameNetBIOS|로컬 컴퓨터의 NetBIOS 이름입니다. 로컬 컴퓨터가 클러스터의 노드인 경우 클러스터 가상 서버의 NetBIOS 이름이 사용됩니다.|  
|ComputerNamePhysicalDnsDomain|로컬 컴퓨터에 할당된 DNS 도메인의 이름입니다. 로컬 컴퓨터가 클러스터의 노드인 경우 클러스터 가상 서버의 이름이 아니라 로컬 컴퓨터의 DNS 도메인 이름이 사용됩니다.|  
|ComputerNamePhysicalDnsFullyQualified|컴퓨터를 고유하게 식별하는 정규화된 DNS 이름입니다. 로컬 컴퓨터가 클러스터의 노드인 경우 클러스터 가상 서버의 이름이 아니라 로컬 컴퓨터의 정규화된 DNS 이름이 사용됩니다.<br /><br /> 정규화된 DNS 이름은 *HostName*.*DomainName*형식으로 DNS 호스트 이름과 DNS 도메인 이름을 결합한 것입니다.|  
|ComputerNamePhysicalDnsHostname|로컬 컴퓨터의 DNS 호스트 이름입니다. 로컬 컴퓨터가 클러스터의 노드인 경우 클러스터 가상 서버의 이름이 아니라 로컬 컴퓨터의 DNS 호스트 이름이 사용됩니다.|  
|ComputerNamePhysicalNetBIOS|로컬 컴퓨터의 NetBIOS 이름입니다. 로컬 컴퓨터가 클러스터의 노드인 경우 클러스터 가상 서버의 이름이 아니라 로컬 컴퓨터의 NetBIOS 이름이 사용됩니다.|  
  
 SPN이 추가되면 다음과 비슷한 항목이 추적 로그에 추가됩니다.  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalNetBIOS> - <theservername>.`  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalDnsHostname> - <theservername>.`  
  
 자세한 내용은 [보고서 서버의 SPN&#40;서비스 사용자 이름&#41; 등록](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md) 및 [URL 예약 및 등록 정보&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)를 참조하세요.  
  
## <a name="next-steps"></a>다음 단계

[확장된 보호를 사용하여 데이터베이스 엔진에 연결](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)   
[인증에 대한 확장된 보호 개요](http://go.microsoft.com/fwlink/?LinkID=177943)   
[확장된 보호를 사용하는 Windows 통합 인증(Integrated Windows Authentication with Extended Protection)](http://go.microsoft.com/fwlink/?LinkId=179922)   
[Microsoft 보안 공지: 인증에 대한 확장된 보호](http://go.microsoft.com/fwlink/?LinkId=179923)   
[보고서 서버 서비스 추적 로그](../../reporting-services/report-server/report-server-service-trace-log.md)   
[RSReportServer 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[SetExtendedProtectionSettings 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
