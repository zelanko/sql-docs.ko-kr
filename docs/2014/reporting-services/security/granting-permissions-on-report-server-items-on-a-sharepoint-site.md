---
title: SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 0eb2f34a-3643-4b03-81c2-5741ba7ebefd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c52bc6b7781b6593f945d582e033653aeb61dc9f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956729"
---
# <a name="granting-permissions-on-report-server-items-on-a-sharepoint-site"></a>SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 은 SharePoint 사이트 및 라이브러리에서 액세스하는 보고서 서버 항목에 대한 액세스를 허용하는 데 사용할 수 있는 기본 제공 보안 기능을 제공합니다. 이미 사용자에게 사용 권한을 할당한 경우 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 와 보고서 서버 간의 통합 설정을 구성하는 즉시 해당 사용자가 보고서 서버 항목 및 작업에 액세스할 수 있게 됩니다. 기존 사용 권한을 사용하여 보고서 정의와 기타 문서를 업로드하고, 보고서를 보고, 구독을 만들고, 항목을 관리할 수 있습니다.  
  
 사용 권한을 할당하지 않았거나 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]의 보안 기능에 대해 잘 모르는 경우 다음 지침을 따르세요.  
  
1.  [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]에 대한 제품 설명서에서 표준 SharePoint 그룹에 대한 기본 보안 설정을 읽어 사용 권한 및 사용자 액세스를 관리하는 방법을 확인합니다.  
  
2.  보고서 서버 항목 및 작업에 대한 액세스에 특별히 영향을 주는 사용 권한 목록을 검토합니다. 자세한 내용은 [보고서 서버 항목에 대해 Windows SharePoint Services의 기본 제공 보안 사용](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)을 참조하세요.  
  
3.  미리 정의된 SharePoint 그룹에 사용자 및 그룹 계정을 할당합니다.  
  
4.  필요에 따라 새 사용 권한 수준 및 그룹을 만들거나, 기존 사용 권한 수준 및 그룹을 수정하여 특정 요구가 발생할 때마다 적절하게 서버 액세스 권한을 조정합니다.  
  
 보고서 서버 항목에 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 보안 기능을 사용하려면 SharePoint 통합 모드로 실행되는 보고서 서버가 있어야 합니다.  
  
## <a name="about-permissions-permission-levels-and-sharepoint-groups"></a>사용 권한, 사용 권한 수준 및 SharePoint 그룹 정보  
 다음 목록에서는 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]의 보안 기능에 대해 간략하게 설명합니다. 자세한 내용은 SharePoint 사이트의 "Windows SharePoint 도움말 및 방법"을 참조하십시오.  
  
-   보안 개체에는 사이트, 목록, 라이브러리, 폴더 및 문서가 있습니다.  
  
-   사용 권한은 특정 태스크를 수행하기 위한 권한 부여입니다. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 은 사용 권한 수준으로 결합할 수 있는 33개의 미리 정의된 사용 권한을 제공합니다.  
  
-   사용 권한 수준은 사이트, 라이브러리, 목록, 폴더, 항목 또는 문서와 같은 보안 개체에 대해 사용자나 SharePoint 그룹에 부여할 수 있는 사용 권한 집합입니다. 이는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 역할 정의와 같습니다. 5개의 미리 정의된 사용 권한 수준이 제공되며 필요한 경우 이러한 그룹을 사용자 지정하거나 새 그룹을 만들 수 있습니다.  
  
-   SharePoint 그룹은 사이트에 대한 사용 권한을 관리하고 사이트 멤버에 대한 전자 메일 배포 목록을 제공하기 위해 SharePoint 사이트에서 만들 수 있는 사용자 그룹입니다. SharePoint 그룹은 Windows 사용자 및 그룹 계정으로 구성되거나 폼 인증을 사용하는 경우 사용자 로그인으로 구성됩니다. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 에서는 3개의 그룹을 제공합니다. 필요한 경우 이러한 그룹을 사용자 지정하거나 새 그룹을 만들 수 있습니다.  
  
-   사용 권한 상속을 통해 하위 사이트, 목록, 라이브러리 및 항목에 부모 사이트의 보안 설정을 상속할 수 있습니다. 상속 받은 사용 권한을 사용하여 SharePoint 라이브러리에 저장된 보고서 서버 항목에 액세스할 수 있습니다. 사용 권한 상속과 미리 정의된 SharePoint 그룹을 사용하면 보다 쉽게 배포 작업을 수행하고 대부분의 보고서 서버 작업에 즉시 액세스할 수 있습니다.  
  
## <a name="who-sets-permissions"></a>사용 권한 설정의 주체  
 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]를 설치하고 SharePoint 구성 마법사를 실행하며 포털 사이트를 만드는 관리자가 기본 포털 사이트 소유자가 됩니다. 사이트 소유자는 중앙 관리에서 팜 또는 독립 실행형 SharePoint 웹 애플리케이션에 대한 사용 권한을 설정하고 최상위 사이트에서 각 SharePoint 웹 애플리케이션에 대한 사용 권한을 설정할 수 있습니다. 또한 사이트 소유자는 추가 사이트 소유자를 지정할 수 있습니다.  
  
 SharePoint 웹 애플리케이션의 최상위 사이트에서 사이트 모음 관리자는 전체 사이트 계층의 여러 사이트에 대해 사용 권한을 설정할 수 있습니다. 개별 사이트 소유자는 하위 사이트에 대해 동일한 태스크를 수행할 수 있습니다.  
  
 서버 관리자나 사이트 모음 관리자는 다른 사이트 소유자가 사용 권한을 설정할 수 있는지 여부를 결정하는 옵션을 설정할 수 있습니다. 현재 사용 권한 수준에 따라 SharePoint 그룹 또는 사용 권한 수준을 만들거나 사용자 지정하지 못할 수 있습니다.  
  
## <a name="using-predefined-sharepoint-groups-and-permission-levels"></a>미리 정의된 SharePoint 그룹 및 사용 권한 수준 사용  
  [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 제품 설명서의 권장 사항에 따르면 표준 SharePoint 그룹( *Site name* **소유자**, *Site name* **멤버**및 *Site name* **방문자**)을 사용하고 사이트 수준에서 사용 권한을 할당하는 것이 좋습니다. 사용 권한을 할당하는 사용자는 대부분 *Site name* **방문자** 또는 *Site name* **멤버** 그룹의 멤버여야 합니다. 부모 사이트에 대한 사용 권한은 전체 사이트 계층에서 상속됩니다. 추가 제한이 필요한 항목이 있을 경우 이 항목에 대해 사용 권한 상속을 해제할 수 있습니다.  
  
 다음 SharePoint 그룹에는 아래와 같은 사용 권한 수준이 미리 정의되어 있습니다.  
  
-   **소유자** 그룹에는 그룹 멤버가 사이트 콘텐츠, 페이지 또는 기능을 변경할 수 있는 "모든 권한" 사용 권한이 있습니다. 모든 권한은 사이트 관리자에게만 부여해야 합니다.  
  
-   **멤버** 그룹에는 그룹 멤버들이 페이지를 보고, 항목을 편집하고, 승인을 받기 위해 변경 내용을 제출하고, 목록에서 항목을 추가 및 삭제할 수 있도록 하는 참가 수준의 사용 권한이 부여되어 있습니다.  
  
-   **방문자** 그룹에는 그룹 멤버가 페이지, 목록 항목 및 문서를 볼 수 있는 읽기 수준의 사용 권한이 있습니다.  
  
 SharePoint 그룹에는 많은 보고서 서버 작업에 즉시 액세스할 수 있도록 하는 사용 권한 수준이 있습니다. 기본 제공 보안 설정을 통해 필요한 액세스 수준을 얻을 수 없는 경우 사용자 지정 그룹 또는 사용 권한 수준을 만들 수 있습니다.  
  
 기본 보안 기능을 통해 지원되는 보고서 서버 작업에 대한 자세한 내용은 [보고서 서버 항목에 대해 Windows SharePoint Services의 기본 제공 보안 사용](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)을 참조하세요.  
  
 기본 제공 보안 기능을 사용하려면 SharePoint 그룹에 Windows 사용자 또는 그룹 계정을 할당해야 합니다. 소프트웨어 설치 시 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 에 대한 액세스 권한이 자동으로 부여되는 서버 관리자와 포털 사이트 소유자를 제외한 다른 모든 사용자에게 서버에 액세스할 수 있는 권한을 부여해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [보고서 서버 항목에 대해 Windows SharePoint Services의 기본 제공 보안 사용](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
 미리 정의된 SharePoint 그룹 및 사용 권한 수준을 사용하여 보고서 서버 항목에 액세스할 수 있는 방법을 설명합니다.  
  
 [보고서 서버 항목에 대한 SharePoint 사이트 및 목록 사용 권한 참조](sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
 보고서 서버 작업에 액세스하는 데 사용할 수 있는 모든 SharePoint 제품 사용 권한에 대한 참조를 제공합니다.  
  
 [SharePoint 웹 응용 프로그램에서 보고서 서버 작업에 대한 사용 권한 설정](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)  
 임시 보고에 대한 사용 권한 요구 사항을 설명하고 기능을 사용할 수 있게 만드는 방법을 제안합니다.  
  
 [Reporting Services의 역할 및 작업과 SharePoint 그룹 및 사용 권한 비교](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
 SharePoint 그룹과 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 미리 정의된 역할 정의를 비교하여 간략하게 설명합니다.  
  
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
 보고서 작성기를 시작하고 모델 항목 보안을 설정할 수 있는 권한이 있는 새 SharePoint 그룹을 만들기 위한 지침을 제공합니다. 이 항목에는 보고서 서버 항목 또는 작업에 사용자 지정 권한을 설정하는 방법에 대한 일반적인 지침도 들어 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services 보안 및 보호](reporting-services-security-and-protection.md)  
  
  
