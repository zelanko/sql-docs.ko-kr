---
title: 보고서 작성기 액세스 구성 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, Report Builder
- Report Builder 1.0, configuring access
- configuring servers [Reporting Services]
ms.assetid: a79003d0-c905-4d4c-9560-93a7cc1e1dd4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ce13c158cbc6d359a319a816aee9a01decabdc0b
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59938349"
---
# <a name="configure-report-builder-access"></a>보고서 작성기 액세스 구성
  보고서 작성기는 기본 모드 또는 SharePoint 통합 모드용으로 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 함께 설치되는 임시 보고 도구입니다.  
  
 보고서 작성기에 대한 액세스 권한은 다음 요소에 따라 달라집니다.  
  
-   보고서 서버에서 보고서 작성기를 사용할 수 있는지 여부를 결정하는 서버 속성  
  
-   개별 사용자 또는 그룹이 보고서 작성기를 사용할 수 있도록 하는 역할 할당 또는 사용 권한  
  
-   사용자 자격 증명을 보고서 서버로 전달할 수 있는지 여부 또는 애플리케이션 파일에 대해 익명 액세스가 구성되어 있는지 여부를 결정하는 인증 설정  
  
 보고서 작성기를 사용하려면 작업할 게시된 보고서 모델이 있어야 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 보고서 작성기를 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 클라이언트 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0이 설치되어 있어야 합니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 는 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 응용 프로그램을 실행하기 위한 인프라를 제공합니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 이상을 사용해야 합니다.  
  
 보고서 작성기는 항상 완전 신뢰 수준에서 실행되며 부분 신뢰 수준에서 실행되도록 구성할 수 없습니다. 이전 릴리스에서는 보고서 작성기를 부분 신뢰 수준에서 실행할 수 있었지만 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상의 버전에서는 해당 옵션이 지원되지 않습니다.  
  
## <a name="enabling-and-disabling-report-builder"></a>보고서 작성기 설정 및 해제  
 보고서 작성기는 기본적으로 설정되어 있습니다. 보고서 서버 관리자는 보고서 서버 시스템 속성인 `EnableReportDesignClientDownload`를 `false`로 설정하여 보고서 작성기 기능을 해제할 수 있습니다. 이 속성을 설정하면 해당 보고서 서버에 대한 보고서 작성기 다운로드가 해제됩니다.  
  
 보고서 서버 시스템 속성을 설정하려면 Management Studio 또는 스크립트를 사용합니다.  
  
-   Management Studio를 사용하려면 보고서 서버에 연결하고 고급 서버 속성 페이지를 사용하여 `EnableReportDesignClientDownload`를 `false`로 설정합니다. 이 페이지를 여는 방법에 대한 자세한 내용은 [보고서 서버 속성 설정&#40;Management Studio&#41;](../tools/set-report-server-properties-management-studio.md)를 참조하세요.  
  
-   보고서 서버 속성을 설정하는 샘플 스크립트를 보려면 [배포 및 관리 태스크 스크립팅](../tools/script-deployment-and-administrative-tasks.md)을 참조하세요.  
  
## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>기본 모드 보고서 서버에서 보고서 작성기 액세스 권한을 부여하는 역할 할당  
 기본 모드 보고서 서버에서 보고서 작성기를 사용하기 위한 태스크를 포함하는 사용자 역할 할당을 만듭니다. 항목 단위 및 사이트 수준에서 역할 정의와 역할 할당을 만들거나 수정하려면 내용 관리자 및 시스템 관리자여야 합니다.  
  
 다음 지침에서는 사용자가 미리 정의된 역할을 사용한다고 가정합니다. 역할 정의를 수정했거나 SQL Server 2000에서 업그레이드한 경우에는 필요한 태스크가 역할에 포함되어 있는지 확인합니다. 역할 할당 만들기에 대한 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](../security/grant-user-access-to-a-report-server.md)를 참조하세요.  
  
 역할 할당을 만들면 사용자에게 다음 작업을 수행할 수 있는 권한이 부여됩니다.  
  
-   시스템 사용자 및 브라우저 역할에 할당된 사용자는 보고서 작성기를 시작하지 않고도 보고서 서버에 게시된 보고서 작성기 보고서를 볼 수 있습니다.  
  
-   시스템 사용자 및 보고서 작성기 역할에 할당된 사용자는 모델을 생성하고, 보고서 작성기를 시작하고, 보고서를 만들고, 보고서를 보고서 서버에 저장할 수 있습니다.  
  
-   시스템 사용자 및 게시자 역할에 할당된 사용자는 모델을 모델 디자이너에서 보고서 서버로 게시할 수 있습니다. 모델은 보고서 작성기에서 데이터 원본으로 사용됩니다.  
  
-   시스템 관리자 및 내용 관리자 역할에 할당된 사용자에게는 보고서 작성기 보고서를 만들고, 보고, 관리할 수 있는 모든 권한이 부여됩니다.  
  
#### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>필요한 태스크가 역할 정의에 있는지 확인하려면  
  
1.  Management Studio를 열고 보고서 서버에 연결합니다.  
  
2.  **보안** 폴더를 엽니다.  
  
3.  **시스템 역할** 폴더를 엽니다.  
  
4.  **시스템 관리자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
5.  **보고서 정의 실행** 을 선택하고 **확인**을 클릭합니다.  
  
6.  **시스템 사용자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
7.  **보고서 정의 실행** 을 선택하고 **확인**을 클릭합니다.  
  
8.  **역할** 폴더를 엽니다.  
  
9. **브라우저**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
10. **모델 보기** 를 선택하고 **확인**을 클릭합니다.  
  
11. **내용 관리자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
12. **모델 보기**, **모델 관리**, **보고서 사용**을 선택하고 **확인**을 클릭합니다.  
  
13. **게시자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
14. **모델 관리** 를 선택하고 **확인**을 클릭합니다.  
  
15. 보고서 작성기 역할이 없는 경우 해당 역할을 만듭니다.  
  
    1.  **보안** 폴더를 엽니다.  
  
    2.  **역할**을 마우스 오른쪽 단추로 클릭하고 **새 역할**을 선택합니다.  
  
    3.  이름에 **Report Builder**를 입력합니다.  
  
    4.  보고서 관리자 사용자가 역할의 용도를 파악할 수 있도록 설명에 역할에 대한 설명을 입력합니다.  
  
    5.  다음 작업을 추가 합니다. **보고서 사용**, **보고**를 **모델 보기**를 **리소스 보기**를 **폴더 보기**, 및  **개별 구독 관리**s입니다.  
  
    6.  **확인** 을 클릭하여 역할을 저장합니다.  
  
#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>보고서 작성기에 대한 액세스 권한을 부여하는 역할 할당을 만들려면  
  
1.  보고서 관리자를 시작합니다.  
  
2.  **사이트 설정**을 클릭합니다.  
  
3.  **보안**을 클릭합니다.  
  
4.  보고서 작성기 액세스 권한을 구성할 사용자 또는 그룹에 대한 역할 할당이 이미 있는 경우 **편집**을 클릭합니다.  
  
     그렇지 않으면 **새 역할 할당**을 클릭합니다. 그룹 또는 사용자에 Windows 도메인 사용자 또는 그룹 계정을 \<domain>\\<account\> 형식으로 입력합니다. 폼 인증 또는 사용자 지정 보안을 사용하는 경우에는 해당 배포에 적절한 형식으로 사용자 또는 그룹 계정을 지정합니다.  
  
5.  **시스템 사용자**를 선택한 다음 **확인**을 클릭합니다.  
  
6.  **홈**을 클릭합니다.  
  
7.  **폴더 설정** 탭을 클릭합니다.  
  
8.  **보안** 탭을 클릭합니다.  
  
9. 보고서 작성기 액세스 권한을 구성할 사용자 또는 그룹에 대한 역할 할당이 이미 있는 경우 **편집**을 클릭합니다.  
  
     그렇지 않으면 **새 역할 할당**을 클릭합니다. 그룹 또는 사용자에 Windows 도메인 사용자 또는 그룹 계정을 \<domain>\\<account\> 형식으로 입력합니다. 폼 인증 또는 사용자 지정 보안을 사용하는 경우에는 해당 배포에 적절한 형식으로 사용자 또는 그룹 계정을 지정합니다.  
  
10. **보고서 작성기**를 선택한 다음 **적용**을 클릭합니다.  
  
11. 위의 단계를 반복하여 추가 사용자 또는 그룹에 대한 역할 할당을 만들거나 수정합니다.  
  
## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>SharePoint 통합 모드 보고서 서버에서 보고서 작성기 액세스 권한을 부여하는 사용 권한  
 SharePoint 통합 모드 보고서 서버에서 보고서 작성기 액세스 권한은 Contribute 또는 Full Control 권한 수준을 갖는 SharePoint 사용자에게 부여됩니다.  
  
 사용자 지정 권한 수준을 사용하는 경우 권한 수준에 항목 추가 및 항목 편집을 포함해야 합니다. 기본 제공 권한 수준을 통한 보고서 작성기 액세스에 대한 자세한 내용은 [보고서 서버 항목에 대해 Windows SharePoint Services의 기본 제공 보안 사용](../security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)을 참조하세요. 사용자 지정 권한 수준의 권한 요구 사항에 대한 자세한 내용은 [SharePoint 웹 애플리케이션에서 보고서 서버 작업에 대한 사용 권한 설정](../security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)을 참조하세요.  
  
## <a name="authentication-considerations-and-credential-reuse"></a>인증 고려 사항 및 자격 증명 다시 사용  
 보고서 작성기는 ClickOnce 기술을 사용하여 해당 애플리케이션 파일을 클라이언트 컴퓨터로 다운로드하고 설치합니다. ClickOnce 기술은 프로그램 파일을 클라이언트 컴퓨터에 배치하고 애플리케이션을 기본 사용자의 ID를 사용하여 별도의 프로세스로 실행하는 단방향 애플리케이션 배포를 위해 제공됩니다. 보고서 작성기는 애플리케이션 파일 및 보고서 서버 데이터를 가져오기 위해 보고서 서버에 다시 연결해야 하므로 다양한 시나리오에서 ClickOnce가 보안 컨텍스트를 설정하고 원격 컴퓨터에 대한 요청을 실행하는 방법을 이해해야 합니다.  
  
-   ClickOnce는 항상 클라이언트 컴퓨터에서 별도의 프로세스로 실행되며 프로세스 ID는 기본 Windows 사용자 자격 증명입니다. ClickOnce는 Internet Explorer와 세션 데이터를 공유하거나 Internet Explorer에서 현재 사용자 보안 컨텍스트를 가져오지 않습니다.  
  
-   ClickOnce는 인증 헤더에 Windows 통합 보안을 지정하는 요청을 보냅니다. 서버가 다른 인증 유형용으로 구성된 경우 서버에서 ClickOnce의 요청이 인증 오류와 함께 실패합니다. 이 문제를 해결하려면 서버를 Windows 통합 보안용으로 구성하거나 익명 액세스를 사용하여 인증 검사가 진행되지 않도록 해야 합니다.  
  
-   보고서 작성기는 보고서 서버에 대한 자체 연결을 엽니다. Windows 통합 보안을 Single Sign On과 함께 사용하지 않는 경우 보고서 서버에 대한 보고서 작성기 연결을 위해 사용자가 자격 증명을 다시 입력해야 합니다.  
  
 다음 표에서는 보고서 서버에 지원되는 인증 유형과 보고서 작성기에 액세스하기 위해 추가 구성이 필요한지 여부를 설명합니다.  
  
|보고서 서버 인증 유형|보고서 작성기 및 ClickOnce 애플리케이션 실행 프로그램의 응답 방식|  
|---------------------------------------|--------------------------------------------------------------------|  
|Negotiate(기본값)<br /><br /> NTLM(기본값)|Windows 통합 보안에서는 클라이언트와 서버가 동일한 도메인에 배포되어 있고, 사용자가 보고서 작성기에 액세스할 수 있는 권한이 있는 도메인 계정을 사용하여 클라이언트 컴퓨터에 로그인하고, 보고서 서버에 Windows 인증이 구성된 경우 일반적으로 ClickOnce 및 보고서 작성기의 인증된 요청이 성공적으로 수행됩니다.<br /><br /> 보고서 서버에 대한 ClickOnce 및 브라우저 연결의 사용자 ID가 동일하므로 요청이 성공적으로 수행됩니다.<br /><br /> 사용자가 Internet Explorer를 다음 계정으로 실행을 사용하여 열고 기본값이 아닌 자격 증명을 지정한 경우 요청이 실패합니다. 보고서 서버의 사용자 세션이 특정 계정으로 설정되어 있고 ClickOnce가 다른 계정으로 실행되는 경우 보고서 서버에서 파일에 대한 액세스를 거부합니다.|  
|Kerberos|보고서 작성기를 사용하기 위해 필요한 Internet Explorer는 Kerberos를 직접 지원하지 않습니다.|  
|기본 인증|ClickOnce는 기본 인증을 지원하지 않습니다. ClickOnce는 인증 헤더에 기본 인증을 지정하는 요청을 작성하지 않으며 자격 증명을 전달하거나 자격 증명을 지정하라는 메시지를 표시하지 않습니다. 보고서 작성기 애플리케이션 파일에 대한 익명 액세스를 사용하여 이러한 문제를 해결할 수 있습니다.<br /><br /> 보고서 작성기 애플리케이션 파일에 대한 익명 액세스를 사용하는 경우 보고서 서버에서 인증 헤더를 무시하므로 요청이 성공적으로 수행됩니다. 보고서 작성기에 대한 익명 액세스를 사용하도록 설정하는 방법에 대한 자세한 내용은 [보고서 서버의 기본 인증 구성](../security/configure-basic-authentication-on-the-report-server.md)을 참조하세요.<br /><br /> ClickOnce가 애플리케이션 파일을 검색한 후 보고서 작성기는 보고서 서버에 대한 별도의 연결을 엽니다. 보고서 작성기가 보고서 서버에 연결하려면 사용자가 자격 증명을 다시 입력해야 합니다. 보고서 작성기는 Internet Explorer 또는 ClickOnce에서 자격 증명을 수집하지 않습니다.<br /><br /> 보고서 서버가 기본 인증용으로 구성되어 있고 보고서 작성기 프로그램 파일에 대한 익명 액세스를 사용하지 않는 경우 요청이 실패합니다. ClickOnce가 해당 요청에 대해 Windows 통합 보안을 지정하기 때문에 요청이 실패합니다. 보고서 서버를 기본 인증용으로 구성하는 경우 요청에서 잘못된 보안 패키지를 지정하고 보고서 서버에 필요한 자격 증명이 없기 때문에 서버에서 요청을 거부합니다.<br /><br /> 또한 보고서 서버가 SharePoint 통합 모드를 사용하도록 구성되어 있고 SharePoint 사이트에서 기본 인증을 사용하는 경우 ClickOnce를 사용하여 클라이언트 컴퓨터에 보고서 작성기를 설치하려고 하면 401 오류가 발생합니다. 이는 SharePoint에서는 쿠키를 사용하여 세션이 지속되는 동안 사용자를 인증된 상태로 유지하지만 ClickOnce에서는 쿠키를 지원하지 않기 때문입니다. 사용자가 보고서 작성기 등의 ClickOnce 애플리케이션을 실행하면 애플리케이션에서 SharePoint에 쿠키를 전달하지 않으므로 SharePoint에서 액세스를 거부하고 401 오류를 반환합니다.<br /><br /> 다음 방법 중 하나를 사용하여 이 문제를 해결할 수 있습니다.<br /><br /> 선택 된 **암호를 기억할** 사용자 자격 증명을 제공 하는 경우 옵션입니다.<br /><br /> SharePoint 사이트 모음에 대한 익명 액세스를 허용합니다.<br /><br /> 사용자가 자격 증명을 제공하지 않도록 환경을 구성합니다. 예를 들어 인트라넷 환경에서는 SharePoint 서버가 작업 그룹에 속하도록 구성한 다음 로컬 컴퓨터에 사용자 계정을 만들 수 있습니다.|  
|사용자 지정|보고서 서버가 사용자 지정 인증을 사용하도록 구성하는 경우 보고서 서버에서 익명 액세스가 사용되고 인증 검사 없이 요청이 허용됩니다.<br /><br /> ClickOnce가 애플리케이션 파일을 검색한 후 보고서 작성기는 보고서 서버에 대한 별도의 연결을 엽니다. 보고서 작성기가 보고서 서버에 연결하려면 사용자가 자격 증명을 다시 입력해야 합니다. 보고서 작성기는 Internet Explorer 또는 ClickOnce에서 자격 증명을 수집하지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 인증](../security/authentication-with-the-report-server.md)   
 [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [보고서 작성기를 시작 &#40;보고서 작성기&#41;](../report-builder/start-report-builder.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)   
 [Management Studio에서 보고서 서버에 연결](../tools/connect-to-a-report-server-in-management-studio.md)   
 [보고서 서버 시스템 속성](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)  
  
  
