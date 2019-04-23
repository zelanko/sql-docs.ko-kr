---
title: 보고서 서버 서비스 계정 구성(SSRS 구성 관리자) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: ''
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/10/2018
ms.openlocfilehash: cb867bfdfc8d9ecb686d3ecc52c48c80bc60d9cd
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59970149"
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>보고서 서버 서비스 계정 구성(SSRS 구성 관리자)

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 예약된 보고서 처리와 구독 배달에 사용되는 백그라운드 처리 응용 프로그램, 보고서 서버 웹 서비스 및 보고서 관리자를 포함하는 단일 서비스로 구현됩니다. 이 항목에서는 서비스 계정을 처음 구성하는 방법 Reporting Services 구성 도구를 사용하는 계정이나 암호를 수정하는 방법에 대해 설명합니다.  
  
## <a name="initial-configuration"></a>초기 구성

 설치하는 동안 보고서 서버 서비스 계정이 정의됩니다. `NetworkService` 계정과 같은 도메인 사용자 계정이나 기본 제공 계정으로 보고서 서버 서비스를 실행할 수 있습니다. 기본 계정이 없으며; 지정 하는 모든 계정 합니다 [서버 구성-서비스 계정](../../sql-server/install/server-configuration-service-accounts.md) 설치 마법사의 페이지에 보고서 서버 서비스의 초기 계정이 됩니다.  
  
> [!IMPORTANT]
> 보고서 서버 웹 서비스 및 보고서 관리자가 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 애플리케이션이더라도 이들은 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 계정에서 실행되지 않습니다. 단일 서비스 아키텍처는 동일한 보고서 서버 프로세스 ID 내에서 두 ASP.NET 애플리케이션을 모두 실행합니다. 이것은 이전 버전에서의 중요한 변경 사항으로 보고서 서버 웹 서비스 및 보고서 관리자는 IIS에서 지정된 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 작업자 프로세스 ID에서 실행됩니다.
  
## <a name="changing-the-service-account"></a>서비스 계정 변경

 서비스 계정 정보를 보고 다시 구성하려면 항상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용합니다. 서비스 ID 정보는 내부적으로 여러 위치에 저장됩니다. 이 도구를 사용하면 계정 또는 암호를 변경할 때마다 모든 참조가 적절히 업데이트됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구는 보고서 서버를 사용 가능한 상태로 유지하기 위한 다음과 같은 추가 단계를 수행합니다.  
  
- 로컬 컴퓨터에서 생성된 보고서 서버 그룹에 새 계정을 자동으로 추가합니다. 이 그룹은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 파일의 보안을 유지하는 ACL(액세스 제어 목록)에 지정됩니다.  
  
- 보고서 서버 데이터베이스 호스팅에 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 대한 로그인 권한을 자동으로 업데이트합니다. 새 계정이 **RSExecRole**에 추가됩니다.  
  
     이전 계정에 대한 데이터베이스 로그인은 자동으로 제거되지 않습니다. 더 이상 사용하지 않는 계정을 제거해야 합니다. 자세한 내용은 SQL Server 온라인 설명서의 [보고서 서버 데이터베이스 관리&#40;SSRS 기본 모드&#41;](../report-server/report-server-database-ssrs-native-mode.md)를 참조하세요.  
  
     처음에 서비스 계정을 사용하도록 보고서 서버 데이터베이스 연결을 구성한 경우에만 데이터베이스 권한이 새 서비스 계정에 부여됩니다. 도메인 사용자 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인을 사용하도록 보고서 서버 데이터베이스 연결을 구성한 경우에는 연결 정보는 서비스 계정 업데이트의 영향을 받지 않습니다.  
  
- 새 계정의 프로필 정보를 포함하도록 자동으로 암호화 키를 업데이트합니다.  
  
    > [!NOTE]  
    > 보고서 서버가 스케일 아웃 배포에 속할 경우 업데이트하는 보고서 서버만 영향을 받습니다. 따라서 배포에 포함된 다른 보고서 서버의 암호화 키는 서비스 계정을 변경해도 영향을 받지 않습니다.  
  
 계정을 설정 하는 방법에 지침은 [서비스 계정 구성 &#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)합니다.  
  
## <a name="choosing-an-account"></a>계정 선택

 다음 계정 유형으로 실행되도록 보고서 서버 서비스를 구성할 수 있습니다.  
  
- 최소 권한 Windows 사용자 계정  
  
- NetworkService  
  
- LocalSystem  
  
- LocalService  
  
 계정 유형을 선택하는 가장 좋은 방법이 한 가지만 있는 것은 아닙니다. 계정마다 고려해야 하는 장단점이 있습니다. 프로덕션 서버에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 배포하는 경우에는 악의적인 공격자가 공유 계정을 침해할 경우 광범위한 손상을 방지할 수 있게 도메인 사용자 계정으로 서비스를 실행하도록 구성하는 것이 가장 좋습니다. 이렇게 하면 이 계정의 로그온 활동을 감사하기도 더 쉽습니다. Windows 사용자 계정을 사용하는 데 대한 절충안으로 Kerberos 인증을 사용하는 네트워크에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 배포하는 경우에는 이 사용자 계정으로 보고서 서버 서비스를 등록해야 합니다. 자세한 내용은 [보고서 서버의 SPN&#40;서비스 사용자 이름&#41; 등록](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)을 참조하세요.  
  
 이 섹션의 다음 지침과 링크를 통해 배포에 가장 적합한 방법을 결정할 수 있습니다.  
  
- [서비스 계정 &#40;SSRS 기본 모드&#41;](../../sql-server/install/service-account-ssrs-native-mode.md)합니다.  
  
- SQL Server 온라인 설명서의[Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
  
- [서비스 및 서비스 계정 보안 계획 가이드](http://usergroup.doubletake.com/file_cabinet/download/0x000021733).  
  
## <a name="updating-an-expired-password"></a>만료된 암호 업데이트

 보고서 서버 서비스가 도메인 계정으로 실행되며 Reporting Services 구성 도구를 사용하여 이 서비스를 업데이트할 수 있게 되기 전에 암호가 만료된 경우 새 암호를 지정할 때까지 해당 서비스를 사용할 수 없습니다. 이 서비스를 시작할 수 없으면 계정을 업데이트하기 위해 해당 서버에 연결하도록 Reporting Services 구성 도구를 사용할 수 없습니다. 이런 경우 여러 가지 도구를 사용하여 서버를 다시 온라인으로 전환해야 합니다.  
  
 암호를 다시 설정하려면 다음을 수행합니다.  
  
1. **시작** 메뉴에서 **제어판**, **관리 도구**를 차례로 가리킨 다음 **서비스**를 클릭합니다.  
  
2. **SQL Server Reporting Services**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3. **로그온**을 클릭하고 새 암호를 입력합니다.  
  
4. 암호를 업데이트한 후 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작하고 서비스 계정 페이지에서 암호를 업데이트합니다. 이 추가 단계는 보고서 서버에서 내부적으로 저장한 계정 정보를 업데이트하는 데 필요합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 서비스 계정 암호가 만료된 경우에는 보고서 서버에 연결하려고 할 때 `rsReportServerDatabaseUnavailable` 오류가 발생합니다. 이 오류를 해결하려면 암호를 다시 설정합니다.  
  
## <a name="configuring-the-report-server-service-for-a-sharepoint-integrated-report-server"></a>SharePoint 통합 보고서 서버를 위한 보고서 서버 서비스 구성

 SharePoint 통합 모드에서 보고서 서버를 실행 중이며 다음 조건 중 하나가 참인 경우 SharePoint 구성 데이터베이스에 저장된 서비스 계정 정보를 업데이트해야 합니다.  
  
- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정이 수정된 경우(예: NetworkService에서 도메인 사용자 계정으로 전환).  
  
- SharePoint 팜이 추가 SharePoint 웹 애플리케이션을 포함하도록 확장된 경우. 서버 팜이 보고서 서버 통합을 위해 구성되고 새로 추가된 애플리케이션이 팜에 있는 다른 애플리케이션과 다른 사용자 계정에서 실행되도록 구성된 경우 데이터베이스 액세스 정보를 업데이트해야 합니다.  
  
 데이터베이스 액세스 정보를 다시 설정한 다음에는 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 서비스를 다시 시작하여 기존 연결이 더 이상 사용되지 않도록 해야 합니다.  
  
1. **관리 도구**에서 **SharePoint 2010 중앙 관리**를 클릭합니다.  
  
2. **응용 프로그램 관리**를 클릭합니다.  
  
3. Reporting Services 섹션에서 **데이터베이스 액세스 권한 부여**를 클릭합니다.  
  
4. **확인**을 클릭합니다. 자격 증명 입력 대화 상자가 나타납니다.  
  
5. 보고서 서버를 호스팅하는 컴퓨터의 로컬 관리자 그룹 멤버인 사용자의 자격 증명을 입력합니다. 자격 증명은 서비스 계정 정보를 조회하기 위해 보고서 서버 컴퓨터에 한 번 연결하는 데 사용됩니다. 각 서비스 계정에 대해 만든 데이터베이스 로그인은 SharePoint 데이터베이스에서 업데이트됩니다.  
  
6. 서비스를 다시 시작하려면 **작업**을 클릭합니다.  
  
7. 토폴로지 및 서비스에서 **서버 제공 서비스**를 클릭합니다.  
  
8. Windows SharePoint Services 웹 애플리케이션의 경우 **중지**를 클릭합니다.  
  
9. 서비스가 중지될 때까지 기다립니다.  
  
10. **시작**을 클릭합니다.  
  
> [!NOTE]  
> SharePoint 제품 및 기술을 사용하려면 Reporting Services SharePoint 모드 같은 서비스 구성에 사용할 도메인 계정이 필요합니다.  
  
## <a name="next-steps"></a>다음 단계

 [서비스 계정 구성 &#40;SSRS 구성 관리자&#41; ](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md) [서비스 계정 &#40;SSRS 기본 모드&#41; ](../../sql-server/install/service-account-ssrs-native-mode.md) [보고서 서버 Url 구성 &#40;SSRS 구성 관리자&#41; ](configure-report-server-urls-ssrs-configuration-manager.md) [Reporting Services 구성 관리자 &#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)
