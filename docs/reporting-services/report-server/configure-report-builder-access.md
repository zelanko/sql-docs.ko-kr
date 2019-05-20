---
title: 보고서 작성기 액세스 구성 | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.date: 03/14/2017
ms.openlocfilehash: 50703b76ddd67ca4d41cc42625eb6cd0e5ac993b
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580380"
---
# <a name="configure-report-builder-access"></a>보고서 작성기 액세스 구성
보고서 작성기는 기본 모드 또는 SharePoint 통합 모드용으로 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 함께 설치되는 임시 보고 도구입니다.  

보고서 작성기에 대한 액세스 권한은 다음 요소에 따라 달라집니다.  

- 보고서 서버에서 보고서 작성기를 사용할 수 있는지 여부를 결정하는 서버 속성  

- 개별 사용자 또는 그룹이 보고서 작성기를 사용할 수 있도록 하는 역할 할당 또는 사용 권한  

- 사용자 자격 증명을 보고서 서버로 전달할 수 있는지 여부 또는 애플리케이션 파일에 대해 익명 액세스가 구성되어 있는지 여부를 결정하는 인증 설정

## <a name="prerequisites"></a>사전 요구 사항

일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 보고서 작성기를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2017 버전에서 지원하는 기능](~/sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.  

클라이언트 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0이 설치되어 있어야 합니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 는 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 애플리케이션을 실행하기 위한 인프라를 제공합니다.  

[!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 이상을 사용해야 합니다.  

보고서 작성기는 항상 완전 신뢰 수준에서 실행되며 부분 신뢰 수준에서 실행되도록 구성할 수 없습니다. 이전 릴리스에서는 보고서 작성기를 부분 신뢰 수준에서 실행할 수 있었지만 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상의 버전에서는 해당 옵션이 지원되지 않습니다.  

## <a name="enabling-and-disabling-report-builder"></a>보고서 작성기 설정 및 해제  

보고서 작성기는 기본적으로 설정되어 있습니다. 보고서 서버 관리자는 보고서 서버 시스템 속성인 **EnableReportDesignClientDownload** 를 **false**로 설정하여 보고서 작성기 기능을 해제할 수 있습니다. 이 속성을 설정하면 해당 보고서 서버에 대한 보고서 작성기 다운로드가 해제됩니다.  

보고서 서버 시스템 속성을 설정하려면 Management Studio 또는 스크립트를 사용합니다.  

- Management Studio를 사용하려면 보고서 서버에 연결하고 고급 서버 속성 페이지를 사용하여 **EnableReportDesignClientDownload** 를 **false**로 설정합니다. 이 페이지를 여는 방법에 대한 자세한 내용은 [보고서 서버 속성 설정&#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)를 참조하세요.  

- 보고서 서버 속성을 설정하는 샘플 스크립트를 보려면 [배포 및 관리 태스크 스크립팅](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)을 참조하세요.  

## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>기본 모드 보고서 서버에서 보고서 작성기 액세스 권한을 부여하는 역할 할당  

기본 모드 보고서 서버에서 보고서 작성기를 사용하기 위한 태스크를 포함하는 사용자 역할 할당을 만듭니다. 항목 단위 및 사이트 수준에서 역할 정의와 역할 할당을 만들거나 수정하려면 내용 관리자 및 시스템 관리자여야 합니다.  

다음 지침에서는 사용자가 미리 정의된 역할을 사용한다고 가정합니다. 역할 정의를 수정했거나 SQL Server 2000에서 업그레이드한 경우에는 필요한 태스크가 역할에 포함되어 있는지 확인합니다. 역할 할당 만들기에 대한 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)를 참조하세요.  

역할 할당을 만들면 사용자에게 다음 작업을 수행할 수 있는 권한이 부여됩니다.  

- 시스템 사용자 및 브라우저 역할에 할당된 사용자는 보고서 작성기를 시작하지 않고도 보고서 서버에 게시된 보고서 작성기 보고서를 볼 수 있습니다.  

- 시스템 사용자 및 보고서 작성기 역할에 할당된 사용자는 모델을 생성하고, 보고서 작성기를 시작하고, 보고서를 만들고, 보고서를 보고서 서버에 저장할 수 있습니다.  

- 시스템 사용자 및 게시자 역할에 할당된 사용자는 모델을 모델 디자이너에서 보고서 서버로 게시할 수 있습니다. 모델은 보고서 작성기에서 데이터 원본으로 사용됩니다.  

- 시스템 관리자 및 내용 관리자 역할에 할당된 사용자에게는 보고서 작성기 보고서를 만들고, 보고, 관리할 수 있는 모든 권한이 부여됩니다.  

### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>필요한 태스크가 역할 정의에 있는지 확인하려면  

1. Management Studio를 열고 보고서 서버에 연결합니다.  

2. **보안** 폴더를 엽니다.  

3. **시스템 역할** 폴더를 엽니다.  

4. **시스템 관리자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  

5. **보고서 정의 실행** 을 선택하고 **확인**을 클릭합니다.  

6. **시스템 사용자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  

7. **보고서 정의 실행** 을 선택하고 **확인**을 클릭합니다.  

8. **역할** 폴더를 엽니다.  

9. **브라우저**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  

10. **모델 보기** 를 선택하고 **확인**을 클릭합니다.  

11. **내용 관리자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  

12. **모델 보기**, **모델 관리**, **보고서 사용**을 선택하고 **확인**을 클릭합니다.  

13. **게시자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  

14. **모델 관리** 를 선택하고 **확인**을 클릭합니다.  

15. 보고서 작성기 역할이 없는 경우 해당 역할을 만듭니다.  

    1. **보안** 폴더를 엽니다.  

    2. **역할**을 마우스 오른쪽 단추로 클릭하고 **새 역할**을 선택합니다.  

    3. 이름에 **Report Builder**를 입력합니다.  

    4. 보고서 관리자 사용자가 역할의 용도를 파악할 수 있도록 설명에 역할에 대한 설명을 입력합니다.  

    5. 이 역할에 **보고서 사용**, **보고서 보기**, **모델 보기**, **리소스 보기**, **폴더 보기**및 **개별 구독 관리**태스크를 추가합니다.  

    6. **확인** 을 클릭하여 역할을 저장합니다.  

#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>보고서 작성기에 대한 액세스 권한을 부여하는 역할 할당을 만들려면  

1. 보고서 관리자를 시작합니다.  

2. **사이트 설정**을 클릭합니다.  

3. **보안**을 클릭합니다.  

4. 보고서 작성기 액세스 권한을 구성할 사용자 또는 그룹에 대한 역할 할당이 이미 있는 경우 **편집**을 클릭합니다.  
그렇지 않으면 **새 역할 할당**을 클릭합니다. 그룹 또는 사용자에 Windows 도메인 사용자 또는 그룹 계정을 \<domain>\\<account\> 형식으로 입력합니다. 폼 인증 또는 사용자 지정 보안을 사용하는 경우에는 해당 배포에 적절한 형식으로 사용자 또는 그룹 계정을 지정합니다.  

5. **시스템 사용자**를 선택한 다음 **확인**을 클릭합니다.  

6. **홈**을 클릭합니다.  

7. **폴더 설정** 탭을 클릭합니다.  

8. **보안** 탭을 클릭합니다.  

9. 보고서 작성기 액세스 권한을 구성할 사용자 또는 그룹에 대한 역할 할당이 이미 있는 경우 **편집**을 클릭합니다.  

    그렇지 않으면 **새 역할 할당**을 클릭합니다. 그룹 또는 사용자에 Windows 도메인 사용자 또는 그룹 계정을 \<domain>\\<account\> 형식으로 입력합니다. 폼 인증 또는 사용자 지정 보안을 사용하는 경우에는 해당 배포에 적절한 형식으로 사용자 또는 그룹 계정을 지정합니다.  

10. **보고서 작성기**를 선택한 다음 **적용**을 클릭합니다.  

11. 위의 단계를 반복하여 추가 사용자 또는 그룹에 대한 역할 할당을 만들거나 수정합니다.  

## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>SharePoint 통합 모드 보고서 서버에서 보고서 작성기 액세스 권한을 부여하는 사용 권한  

SharePoint 통합 모드 보고서 서버에서 보고서 작성기 액세스 권한은 Contribute 또는 Full Control 권한 수준을 갖는 SharePoint 사용자에게 부여됩니다.  

사용자 지정 권한 수준을 사용하는 경우 권한 수준에 항목 추가 및 항목 편집을 포함해야 합니다. 기본 제공 권한 수준을 통한 보고서 작성기 액세스에 대한 자세한 내용은 [보고서 서버 항목에 대해 Windows SharePoint Services의 기본 제공 보안 사용](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)을 참조하세요. 사용자 지정 권한 수준의 권한 요구 사항에 대한 자세한 내용은 [SharePoint 웹 애플리케이션에서 보고서 서버 작업에 대한 사용 권한 설정](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)을 참조하세요.  

## <a name="authentication-considerations-and-credential-reuse"></a>인증 고려 사항 및 자격 증명 다시 사용  

- 보고서 작성기는 보고서 서버에 대한 자체 연결을 엽니다. Windows 통합 보안을 Single Sign On과 함께 사용하지 않는 경우 보고서 서버에 대한 보고서 작성기 연결을 위해 사용자가 자격 증명을 다시 입력해야 합니다.  

다음 표에서는 보고서 서버에 지원되는 인증 유형과 보고서 작성기에 액세스하기 위해 추가 구성이 필요한지 여부를 설명합니다.  

## <a name="see-also"></a>관련 항목:  

- [보고서 서버 인증](../../reporting-services/security/authentication-with-the-report-server.md)
- [Reporting Services 및 파워 뷰 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [보고서 작성기 시작](../../reporting-services/report-builder/start-report-builder.md)
- [보고서 관리자 &#40;SSRS 기본 모드&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)- [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)
- [보고서 서버 시스템 속성](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)