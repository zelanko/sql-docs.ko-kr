---
title: "보고서 서버 서비스 계정 구성(SSRS 구성 관리자) | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f880c623-67c8-4167-b98b-ace17e800faa
caps.latest.revision: "14"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Active
ms.openlocfilehash: fc3bb7568ce6aeb2222ef73dba8d3e9fb42a5482
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>보고서 서버 서비스 계정 구성(SSRS 구성 관리자)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 예약된 보고서 처리와 구독 배달에 사용되는 백그라운드 처리 응용 프로그램, 보고서 서버 웹 서비스 및 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]를 포함하는 단일 서비스로 구현됩니다. 이 항목에서는 서비스 계정을 처음 구성하는 방법 Reporting Services 구성 도구를 사용하는 계정이나 암호를 수정하는 방법에 대해 설명합니다.  
  
## <a name="initial-configuration"></a>초기 구성  
 설치하는 동안 보고서 서버 서비스 계정이 정의됩니다. **가상 서비스 계정**계정과 같은 도메인 사용자 계정이나 기본 제공 계정으로 보고서 서버 서비스를 실행할 수 있습니다. 기본 계정이 없으며 설치 마법사의 **Service Accounts** 페이지에서 지정한 계정이 보고서 서버 서비스의 초기 계정이 됩니다.  
  
> [!IMPORTANT]  
>  보고서 서버 웹 서비스 및 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 은 별도의 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램이지만 동일한 보고서 서버 프로세스 ID 내의 단일 서비스 아키텍처에서 실행합니다.  
  
> [!NOTE]  
>  도메인 컨트롤러인 컴퓨터에서는 기본 제공 Windows 서비스 계정(로컬 서비스 또는 네트워크 서비스)이 보고서 서버 서비스 계정으로 지원되지 않습니다.  
  
## <a name="changing-the-service-account"></a>서비스 계정 변경  
 서비스 계정 정보를 보고 다시 구성하려면 항상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용합니다. 서비스 ID 정보는 내부적으로 여러 위치에 저장됩니다. 이 도구를 사용하면 계정 또는 암호를 변경할 때마다 모든 참조가 적절히 업데이트됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 보고서 서버를 사용 가능한 상태로 유지하기 위한 다음과 같은 추가 단계를 수행합니다.  
  
-   로컬 컴퓨터에서 생성된 보고서 서버 그룹에 새 계정을 자동으로 추가합니다. 이 그룹은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 파일의 보안을 유지하는 ACL(액세스 제어 목록)에 지정됩니다.  
  
-   보고서 서버 데이터베이스 호스팅에 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 대한 로그인 권한을 자동으로 업데이트합니다. 새 계정이 **RSExecRole**에 추가됩니다.  
  
     이전 계정에 대한 데이터베이스 로그인은 자동으로 제거되지 않습니다. 더 이상 사용하지 않는 계정을 제거해야 합니다. 자세한 내용은 SQL Server 온라인 설명서의 [보고서 서버 데이터베이스 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)를 참조하세요.  
  
     처음에 서비스 계정을 사용하도록 보고서 서버 데이터베이스 연결을 구성한 경우에만 데이터베이스 권한이 새 서비스 계정에 부여됩니다. 도메인 사용자 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인을 사용하도록 보고서 서버 데이터베이스 연결을 구성한 경우에는 연결 정보는 서비스 계정 업데이트의 영향을 받지 않습니다.  
  
-   새 계정의 프로필 정보를 포함하도록 자동으로 암호화 키를 업데이트합니다.  
  
    > [!NOTE]  
    >  보고서 서버가 스케일 아웃 배포에 속할 경우 업데이트하는 보고서 서버만 영향을 받습니다. 따라서 배포에 포함된 다른 보고서 서버의 암호화 키는 서비스 계정을 변경해도 영향을 받지 않습니다.  
      
## <a name="to-configure-the-report-server-service-account"></a>보고서 서버 서비스 계정을 구성하려면  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작한 후 보고서 서버에 연결합니다.  
  
2.  서비스 계정 페이지에서 사용하려는 계정 유형에 해당하는 옵션을 선택합니다.  
  
3.  Windows 사용자 계정을 선택한 경우 새 계정과 암호를 지정합니다. 계정은 20자를 초과할 수 없습니다.  
  
     보고서 서버가 Kerberos 인증을 지원하는 네트워크에 배포된 경우 방금 지정한 도메인 사용자 계정으로 보고서 서버 SPN(서비스 사용자 이름)을 등록해야 합니다. 자세한 내용은 [보고서 서버의 SPN&#40;서비스 사용자 이름&#41; 등록](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)을 참조하세요.  
  
4.  **적용**을 클릭합니다.  
  
5.  대칭 키를 백업하라는 메시지가 표시되면 대칭 키를 백업할 파일 이름과 위치를 입력하고 파일을 잠그거나 잠금 해제할 때 사용할 암호를 입력한 다음 **확인**을 클릭합니다.  
  
6.  보고서 서버에서 서비스 계정을 사용하여 보고서 서버 데이터베이스에 연결하는 경우 새 계정 또는 암호를 사용하도록 연결 정보가 업데이트됩니다. 연결 정보를 업데이트하려면 데이터베이스에 연결해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **데이터베이스 연결** 대화 상자가 나타나면 데이터베이스에 연결할 권한이 있는 자격 증명을 입력한 다음 **확인**을 클릭합니다.  
  
7.  대칭 키를 복원하라는 메시지가 표시되면 5단계에서 지정한 암호를 입력한 다음 **확인**을 클릭합니다.  
  
8.  결과 창에서 상태 메시지를 검토하여 모든 태스크가 성공적으로 완료되었는지 확인합니다.  
  
## <a name="choosing-an-account"></a>계정 선택  
 최상의 결과를 얻으려면 네트워크 도메인 컨트롤러 및 회사 SMTP 서버나 게이트웨이에 액세스할 수 있는 네트워크 연결 권한이 있는 계정을 지정합니다. 다음 표에서는 계정을 간단히 보여 주고 계정 사용에 대한 권장 사항을 알려 줍니다.  
  
|계정|설명|  
|-------------|-----------------|  
|도메인 사용자 계정|보고서 서버 작업에 필요한 최소 권한이 있는 Windows 도메인 사용자 계정이 있으면 이러한 계정을 사용해야 합니다.<br /><br /> 다른 응용 프로그램에서 보고서 서버 서비스가 격리되므로 도메인 사용자 계정을 사용하는 것이 좋습니다. 네트워크 서비스와 같은 공유 계정으로 여러 응용 프로그램을 실행하는 경우 한 응용 프로그램에 대한 보안 위협이 동일한 계정으로 실행되는 모든 응용 프로그램으로 쉽게 확장될 수 있기 때문에 악의적인 사용자가 보고서 서버를 제어하는 데에 대한 위험이 증가됩니다.<br /><br /> 도메인 사용자 계정을 사용할 경우 조직에서 암호 만료 정책을 적용하면 정기적으로 암호를 변경해야 합니다. 이 사용자 계정으로 서비스를 등록해야 할 수도 있습니다. 자세한 내용은 [보고서 서버의 SPN&#40;서비스 사용자 이름&#41; 등록](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)을 참조하세요.<br /><br /> 로컬 Windows 사용자 계정을 사용하지 마십시오. 일반적으로 로컬 계정에는 다른 컴퓨터의 리소스에 액세스하기에 충분한 권한이 없습니다. 로컬 계정을 사용하여 보고서 서버 기능을 제한하는 방법에 대한 자세한 내용은 이 항목의 [로컬 계정 사용 시 고려 사항](#localaccounts) 을 참조하십시오.|  
|**가상 서비스 계정**|**가상 서비스 계정** 은 Windows 서비스를 나타냅니다. 네트워크 로그온 권한이 있는 기본 제공 최소 권한 계정입니다. 도메인 사용자 계정을 사용할 수 없거나 암호 만료 정책으로 인해 발생할 수 있는 서비스 장애를 방지하려면 이 계정을 사용하는 것이 좋습니다.|  
|**네트워크 서비스**|**네트워크 서비스** 는 네트워크 로그온 권한이 있는 기본 제공 최소 권한 계정입니다. <br /><br /> **네트워크 서비스**를 선택할 경우 동일한 계정으로 실행하는 다른 서비스의 수를 최소화하십시오. 한 응용 프로그램에 대한 보안 위협으로 인해 동일한 계정으로 실행되는 다른 모든 응용 프로그램의 보안이 손상됩니다.|  
|**로컬 서비스**|**로컬 서비스** 는 인증된 로컬 Windows 사용자 계정과 같은 기본 제공 계정입니다. **로컬 서비스** 계정으로 실행되는 서비스는 자격 증명이 없는 Null 세션으로 네트워크 리소스에 액세스합니다. 이 계정은 보고서 서버를 원격 보고서 서버 데이터베이스나 네트워크 도메인 컨트롤러에 연결하여 보고서를 열거나 구독을 처리하기 전에 사용자를 인증해야 하는 인트라넷 배포 시나리오에 적합하지 않습니다.|  
|**로컬 시스템**|**로컬 시스템** 은 높은 권한이 있는 계정이므로 보고서 서버를 실행하는 데 필요하지 않습니다. 보고서 서버 설치에는 이 계정을 사용하지 마십시오. 대신 도메인 계정 또는 **네트워크 서비스** 를 선택합니다.|  
  
##  <a name="localaccounts"></a> 로컬 계정 사용 시 고려 사항  
 로컬 계정 사용 시 기본적인 고려 사항은 보고서 서버가 원격 데이터베이스 서버, 메일 서버 및 도메인 컨트롤러에 액세스해야 하는지 여부입니다. 로컬 Windows 사용자 계정, 로컬 서비스 또는 로컬 시스템으로 보고서 서버를 실행하도록 구성할 경우 다른 구성 설정 방법과 구독 만들기 및 배달에 대해 검토해야 하는 고려 사항이 있습니다.  
  
-   로컬 계정에서 서비스를 실행하면 나중에 원격 보고서 서버 데이터베이스에 대한 연결을 구성할 경우 옵션이 제한됩니다. 특히 원격 보고서 서버 데이터베이스를 사용 중일 경우 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그온할 권한이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자 또는 도메인 사용자 계정을 사용하도록 연결을 구성해야 합니다.  
  
-   로컬 계정에서 서비스를 실행하는 경우 구독을 만들 때 새로운 요구 사항이 있습니다. 보고서 서버는 구독을 만드는 사용자에 대한 정보를 저장합니다. 사용자가 도메인 계정에서 로그온한 동안 구독을 만들 경우 보고서 서버 서비스는 도메인 컨트롤러에 연결하여 구독이 처리될 때 사용자를 인증하려고 합니다. 이 서비스가 로컬 계정에서 실행될 경우 보고서 서버가 원격 도메인 컨트롤러에 요청을 보내려고 하면 인증 요청이 실패합니다. 이러한 문제를 해결하려면 사용자 지정 폼 기반 인증 확장 프로그램을 사용하거나 모든 사용자가 로컬 사용자 계정에서 보고서 서버에 연결하도록 해야 합니다.  
  
-   로컬 계정에서 서비스를 실행하는 경우 구독 배달에 대한 새로운 요구 사항이 있습니다. 일부 배달 확장 프로그램에는 구독 정의에 사용자 계정 정보가 있습니다. 도메인 사용자 계정에 기반한 전자 메일 주소로 보고서를 보내고 로컬 계정에서 보고서 서버 서비스를 실행하는 경우 원격 도메인 컨트롤러에 액세스하여 대상 전자 메일 계정을 확인할 수 없습니다.  
  
-   도메인 컨트롤러인 컴퓨터에서는 기본 제공 Windows 서비스 계정(로컬 서비스 또는 네트워크 서비스)이 보고서 서버 서비스 계정으로 지원되지 않습니다.  
  
이 섹션의 다음 지침과 링크를 통해 배포에 가장 적합한 방법을 결정할 수 있습니다.  
  
-   SQL Server 온라인 설명서의[Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
  
-   MSDN의[서비스 및 서비스 계정 보안 계획 가이드(The Services and Service Accounts Security Planning Guide)](http://go.microsoft.com/fwlink/?LinkId=69155)   
  
## <a name="updating-an-expired-password"></a>만료된 암호 업데이트  
 보고서 서버 서비스가 도메인 계정으로 실행되며 Reporting Services 구성 관리자를 사용하여 이 서비스를 업데이트할 수 있게 되기 전에 암호가 만료된 경우 새 암호를 지정할 때까지 해당 서비스를 사용할 수 없습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 서비스 계정 암호가 만료된 경우에는 보고서 서버에 연결하려고 할 때 **rsReportServerDatabaseUnavailable** 오류가 발생합니다. 이 오류를 해결하려면 암호를 다시 설정합니다.  
  
## <a name="troubleshooting-service-identity-update-errors"></a>서비스 ID 업데이트 오류 문제 해결  
 서비스 ID를 변경하면 서비스를 다시 시작하고 암호로 보호된 암호화 키, URL 예약 및 보고서 서버 데이터베이스 연결 정보(서비스 계정을 사용하여 보고서 서버 데이터베이스에 연결하는 경우)를 업데이트하는 일련의 이벤트가 시작됩니다. 이러한 이벤트의 상태는 페이지 아래쪽에 있는 결과 창의 알림을 통해 모니터링할 수 있습니다. 이 프로세스 도중 오류가 발생하면 다음 방법을 사용하여 오류를 해결할 수 있습니다.  
  
-   대칭 키를 복원할 수 없는 경우 암호화 키 페이지의 **복원** 을 사용하여 수동으로 복원할 수 있습니다. 이 방법으로 해결되지 않으면 암호화된 내용을 삭제합니다. 이 경우 데이터 원본 연결 정보와 구독은 다시 만들어야 하지만 나머지 내용은 그대로 사용할 수 있습니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요.  
  
-   서비스가 시작되지 않는 경우 관리 도구의 서비스 콘솔 응용 프로그램을 사용하여 수동으로 서비스를 다시 시작합니다.  
  
-   서비스 계정을 업데이트할 때 URL 예약 오류가 발생할 수 있습니다. 각 URL 예약에는 서비스 계정에 URL 요청을 수락할 권한을 부여하는 DACL(임의 액세스 제어 목록)이 포함된 보안 설명자가 있습니다. 계정을 업데이트할 때 URL을 다시 만들어 새 계정 정보로 DACL을 업데이트해야 합니다. URL 예약을 다시 만들 수 없지만 올바른 계정임이 확실한 경우에는 컴퓨터를 다시 시작합니다. 그래도 오류가 계속되면 다른 계정을 사용해 보십시오.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)
