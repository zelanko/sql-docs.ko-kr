---
title: 서비스 계정 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serviceaccount.F1
ms.assetid: face8120-4d32-4c6c-a1e8-99f27d1ff15d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 96cee57e82cc9fbb01a43dc1ec13bf0691f737fc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079133"
---
# <a name="service-account-ssrs-native-mode"></a>서비스 계정(SSRS 기본 모드)
  서비스 계정 페이지를 사용하여 보고서 서버 서비스를 실행할 계정을 지정할 수 있습니다. 이 계정은 설치하는 동안 처음에 구성하며 계정 또는 암호를 변경하려는 경우 수정할 수 있습니다. 보고서 서버 웹 서비스, 보고서 관리자 및 백그라운드 처리 응용 프로그램은 이 페이지에서 지정하는 서비스 ID로 모두 실행됩니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 보고서 서버 서비스에 지정한 계정은 레지스트리, 보고서 서버 프로그램 파일 및 보고서 서버 데이터베이스에 액세스할 수 있는 권한이 있어야 합니다. 모든 사용 권한을 구성 된 계정에 대해 자동으로 사용 하는 경우는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager에서 계정을 설정 합니다. 서비스 계정을 사용 하 여 보고서 서버 데이터베이스에 연결 하는 경우 Configuration Manager 계정에 대 한 데이터베이스 로그인을 만들고에서 계정을 RSExecRole에 할당 하 여 데이터베이스 권한을 구성 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호스팅하는 인스턴스에 보고서 서버 데이터베이스입니다. 보고서 서버 데이터베이스는 보고서 서버가 기록하는 유일한 데이터 저장소입니다. 서비스 계정에는 다른 데이터 저장소에 대한 권한이 필요하지 않습니다.  
  
 이 페이지를 열려면 시작을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager 및 탐색 창에서 링크를 클릭 합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  계정 또는 암호를 업데이트 해야 할 경우 것이 좋습니다 사용 하 여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. 구성 관리자를 사용하여 계정을 업데이트하면 서비스 ID에 따라 달라지는 기타 내부 설정 동시에 자동으로 업데이트됩니다.  
  
## <a name="options"></a>변수  
 **기본 제공 계정 사용**  
 목록에서 **네트워크 서비스**, **로컬 시스템**또는 **로컬 서비스** 를 선택합니다. **네트워크 서비스** 만 사용하는 것이 좋지만 사용할 수 있는 계정을 사용하여 해당 계정을 구성할 수 있습니다.  
  
 **다른 계정 사용**  
 Windows 사용자 계정을 지정하려면 이 옵션을 선택합니다. 로컬 Windows 사용자 계정 또는 도메인 사용자 계정을 입력할 수 있습니다. 이 형식에서 도메인 계정을 지정 합니다.  *\<도메인 >\\< 사용자\>* 합니다. 이 형식으로 로컬 Windows 사용자 계정을 지정 합니다.  *\<컴퓨터 이름 >\\< 사용자\>* 합니다. 기존 계정만 선택할 수 있으며 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성에 새 계정을 만들 수는 없습니다.  
  
 계정의 최대 문자 수 제한은 20자입니다.  
  
 Kerberos 인증을 사용하는 네트워크이고 보고서 서버를 도메인 사용자 계정으로 실행하도록 구성할 경우 사용자 계정으로 서비스를 등록해야 합니다. 자세한 내용은 [보고서 서버의 SPN&#40;서비스 사용자 이름&#41; 등록](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)을 참조하세요.  
  
 Windows 계정을 다른 계정으로 바꾸거나 기본 제공 계정을 Windows 도메인 계정으로 바꾸는 등 계정 유형을 전환하면 암호화 키의 백업 복사본을 만들라는 메시지가 표시됩니다. 새 계정을 선택하면 백업 복사본이 자동으로 복원됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자에서는 사용자가 서비스 계정을 수정할 때마다 암호화 키를 백업 및 복원하라는 메시지를 표시합니다. 이는 보고서 서버에서 계속 암호화된 데이터를 사용할 수 있도록 하기 위해 반드시 필요한 단계입니다. 이러한 작업에 대 한 자세한 내용은 참조 하세요. [암호화 키 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)합니다.  
  
 또한 보고서 서버에 있는 경우 SharePoint 통합에서 실행 되도록 구성 모드가 고 서비스 계정을 변경를 사용 하 여 합니다 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager도 열어야 SharePoint 중앙 관리를 사용 하 고는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **데이터베이스 액세스 권한 부여** 페이지에서 보고서 서버 및 인스턴스 설정을 다시 적용 합니다. 이 단계 액세스 권한이 부여 됩니다 새 서비스 계정에 SharePoint 데이터베이스에 통합 하는 데 필요한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 제품 또는 기술과 함께 합니다. SharePoint 중앙 관리에서 데이터베이스 액세스 권한을 부여 하는 방법에 대 한 자세한 내용은 참조 하십시오 [구성 및 보고서 서버 관리 &#40;Reporting Services SharePoint 모드&#41; ](../../../2014/reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md) 하 고 [ Reporting Services SharePoint 모드 설치 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)합니다.  
  
## <a name="choosing-an-account"></a>계정 선택  
 최상의 결과를 얻으려면 네트워크 도메인 컨트롤러 및 회사 SMTP 서버나 게이트웨이에 액세스할 수 있는 네트워크 연결 권한이 있는 계정을 지정합니다. 다음 표에서는 계정을 간단히 보여 주고 계정 사용에 대한 권장 사항을 알려 줍니다.  
  
|계정|설명|  
|-------------|-----------------|  
|도메인 사용자 계정|보고서 서버 작업에 필요한 최소 권한이 있는 Windows 도메인 사용자 계정이 있으면 이러한 계정을 사용해야 합니다.<br /><br /> 다른 응용 프로그램에서 보고서 서버 서비스가 격리되므로 도메인 사용자 계정을 사용하는 것이 좋습니다. 네트워크 서비스와 같은 공유 계정으로 여러 응용 프로그램을 실행하는 경우 한 응용 프로그램에 대한 보안 위협이 동일한 계정으로 실행되는 모든 응용 프로그램으로 쉽게 확장될 수 있기 때문에 악의적인 사용자가 보고서 서버를 제어하는 데에 대한 위험이 증가됩니다.<br /><br /> 제한된 위임을 위해 보고서 서버를 구성할 경우 또는 기본 제공 컴퓨터 계정이 아닌 도메인 사용자 계정을 사용해야 하는 SharePoint 2010 제품의 SharePoint 통합 모드에서는 도메인 사용자 계정이 필요합니다.<br /><br /> 도메인 사용자 계정을 사용할 경우 조직에서 암호 만료 정책을 적용하면 정기적으로 암호를 변경해야 합니다. 이 사용자 계정으로 서비스를 등록해야 할 수도 있습니다. 자세한 내용은 [보고서 서버의 SPN&#40;서비스 사용자 이름&#41; 등록](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)을 참조하세요.<br /><br /> 로컬 Windows 사용자 계정을 사용하지 마십시오. 일반적으로 로컬 계정에는 다른 컴퓨터의 리소스에 액세스하기에 충분한 권한이 없습니다. 로컬 계정을 사용하여 보고서 서버 기능을 제한하는 방법에 대한 자세한 내용은 이 항목의 [로컬 계정 사용 시 고려 사항](#localaccounts) 을 참조하십시오.|  
|**네트워크 서비스**|**네트워크 서비스** 는 네트워크 로그온 권한이 있는 기본 제공 최소 권한 계정입니다. 도메인 사용자 계정을 사용할 수 없거나 암호 만료 정책으로 인해 발생할 수 있는 서비스 장애를 방지하려면 이 계정을 사용하는 것이 좋습니다.<br /><br /> **네트워크 서비스**를 선택할 경우 동일한 계정으로 실행하는 다른 서비스의 수를 최소화하십시오. 한 응용 프로그램에 대한 보안 위협으로 인해 동일한 계정으로 실행되는 다른 모든 응용 프로그램의 보안이 손상됩니다.|  
|**로컬 서비스**|**로컬 서비스** 는 인증된 로컬 Windows 사용자 계정과 같은 기본 제공 계정입니다. **로컬 서비스** 계정으로 실행되는 서비스는 자격 증명이 없는 Null 세션으로 네트워크 리소스에 액세스합니다. 이 계정은 보고서 서버를 원격 보고서 서버 데이터베이스나 네트워크 도메인 컨트롤러에 연결하여 보고서를 열거나 구독을 처리하기 전에 사용자를 인증해야 하는 인트라넷 배포 시나리오에 적합하지 않습니다.|  
|**로컬 시스템**|**로컬 시스템** 은 높은 권한이 있는 계정이므로 보고서 서버를 실행하는 데 필요하지 않습니다. 보고서 서버 설치에는 이 계정을 사용하지 마십시오. 대신 도메인 계정 또는 **네트워크 서비스** 를 선택합니다.|  
  
##  <a name="localaccounts"></a> 로컬 계정 사용 시 고려 사항  
 로컬 계정 사용 시 기본적인 고려 사항은 보고서 서버가 원격 데이터베이스 서버, 메일 서버 및 도메인 컨트롤러에 액세스해야 하는지 여부입니다. 로컬 Windows 사용자 계정, 로컬 서비스 또는 로컬 시스템으로 보고서 서버를 실행하도록 구성할 경우 다른 구성 설정 방법과 구독 만들기 및 배달에 대해 검토해야 하는 고려 사항이 있습니다.  
  
-   로컬 계정에서 서비스를 실행하면 나중에 원격 보고서 서버 데이터베이스에 대한 연결을 구성할 경우 옵션이 제한됩니다. 특히 원격 보고서 서버 데이터베이스를 사용 중일 경우 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그온할 권한이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자 또는 도메인 사용자 계정을 사용하도록 연결을 구성해야 합니다.  
  
-   로컬 계정에서 서비스를 실행하는 경우 구독을 만들 때 새로운 요구 사항이 있습니다. 보고서 서버는 구독을 만드는 사용자에 대한 정보를 저장합니다. 사용자가 도메인 계정에서 로그온한 동안 구독을 만들 경우 보고서 서버 서비스는 도메인 컨트롤러에 연결하여 구독이 처리될 때 사용자를 인증하려고 합니다. 이 서비스가 로컬 계정에서 실행될 경우 보고서 서버가 원격 도메인 컨트롤러에 요청을 보내려고 하면 인증 요청이 실패합니다. 이러한 문제를 해결하려면 사용자 지정 폼 기반 인증 확장 프로그램을 사용하거나 모든 사용자가 로컬 사용자 계정에서 보고서 서버에 연결하도록 해야 합니다.  
  
-   로컬 계정에서 서비스를 실행하는 경우 구독 배달에 대한 새로운 요구 사항이 있습니다. 일부 배달 확장 프로그램에는 구독 정의에 사용자 계정 정보가 있습니다. 도메인 사용자 계정에 기반한 전자 메일 주소로 보고서를 보내고 로컬 계정에서 보고서 서버 서비스를 실행하는 경우 원격 도메인 컨트롤러에 액세스하여 대상 전자 메일 계정을 확인할 수 없습니다.  
  
-   도메인 컨트롤러인 컴퓨터에서는 기본 제공 Windows 서비스 계정(로컬 서비스 또는 네트워크 서비스)이 보고서 서버 서비스 계정으로 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [서비스 계정 구성 &#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
