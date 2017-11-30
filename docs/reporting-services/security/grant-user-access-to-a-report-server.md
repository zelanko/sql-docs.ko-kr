---
title: "사용자에게 보고서 서버에 대한 액세스 권한 부여 | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing role assignments
- permissions [Reporting Services], granting report server access
- roles [Reporting Services], assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
caps.latest.revision: "54"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.openlocfilehash: a92c37165b8142b7e96a8bb99dee43ea5f12e247
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="grant-user-access-to-a-report-server"></a>보고서 서버에 데이터베이스 액세스 권한 부여

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 역할 기반 보안을 사용하여 보고서 서버에 대한 액세스 권한을 사용자에게 부여합니다. 새 보고서 서버 설치에서는 로컬 관리자 그룹의 멤버인 사용자에게만 보고서 서버 내용 및 작업에 대한 사용 권한이 있습니다. 다른 사용자가 보고서 서버를 사용할 수 있게 하려면 태스크 모음을 지정하는 미리 정의된 역할에 사용자 또는 그룹 계정을 매핑하는 역할 할당을 만들어야 합니다.

 **SharePoint 모드 보고서 서버:** SharePoint 통합 모드로 구성된 보고서 서버의 경우 SharePoint 사이트에서 SharePoint 사용 권한을 사용하여 액세스를 구성합니다. SharePoint 사이트의 사용 권한 수준에 따라 보고서 서버 내용 및 작업에 대한 액세스 권한이 결정됩니다. SharePoint 사이트에 대한 사용 권한을 부여하려면 사이트 관리자여야 합니다. 자세한 내용은 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)를 참조하세요.

 **기본 모드 보고서 서버:** 이 항목에서는 기본 모드로 구성된 보고서 서버 및 웹 포털을 사용하여 역할에 사용자를 할당하는 방법에 대해 설명합니다. 역할에는 다음과 같은 두 가지 유형이 있습니다.

- 항목 수준 역할은 보고서 서버 내용, 구독, 보고서 처리 및 보고서 기록을 보고, 추가하고, 관리하는 데 사용됩니다. 항목 수준 역할 할당은 루트 노드(홈 폴더)에 정의되거나 계층의 하위 수준에 있는 특정 폴더 또는 항목에 정의됩니다.

- 시스템 수준 역할은 특정 항목으로 한정되지 않은 사이트 전체 작업에 대한 액세스 권한을 부여합니다. 보고서 작성기를 사용하는 작업과 공유 일정을 사용하는 작업을 예로 들 수 있습니다.

    이러한 두 역할 유형은 상호 보완적이며 함께 사용해야 합니다. 따라서 보고서 서버에 사용자를 추가하는 작업은 두 부분으로 구성됩니다. 즉, 사용자를 항목 수준 역할에 할당하는 경우 시스템 수준 역할에도 할당해야 합니다. 사용자를 역할에 할당할 때는 이미 정의되어 있는 역할을 선택해야 합니다. 역할을 생성, 수정 또는 삭제하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용합니다. 자세한 내용은 [역할 만들기, 삭제 또는 수정&#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)을 참조하세요.

## <a name="before-you-start"></a>시작하기 전 주의 사항

기본 모드 보고서 서버에 사용자를 추가하기 전에 다음 목록을 검토합니다.

- 보고서 서버 컴퓨터에서 로컬 관리자 그룹의 멤버여야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 또는 Windows Server 2008에서 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 를 배포하는 경우 보고서 서버를 로컬로 관리하려면 추가 구성이 필요합니다. 자세한 내용은 [로컬 관리용으로 기본 모드 보고서 서버 구성](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)을 참조하세요.

- 이 태스크를 다른 사용자에게 위임하려면 사용자 계정을 내용 관리자 및 시스템 관리자 역할에 매핑하는 역할 할당을 만듭니다. 내용 관리자 및 시스템 관리자 권한이 있는 사용자는 보고서 서버에 사용자를 추가할 수 있습니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 각 역할의 태스크 종류에 익숙해질 수 있도록 시스템 역할 및 사용자 역할에 대해 미리 정의된 역할을 확인합니다. 웹 포털에는 작업 설명이 표시되지 않으므로 사용자를 추가하기 전에 역할에 익숙해지는 것이 좋습니다.

- 필요에 따라 필요한 태스크 모음을 포함하는 추가 역할을 정의하거나 역할을 사용자 지정합니다. 예를 들어 개별 항목에 대해 사용자 지정 보안 설정을 사용하려는 경우 폴더에 대한 보기 액세스 권한을 부여하는 새 역할 정의를 만들 수 있습니다.

### <a name="to-add-a-user-or-group-to-a-system-role"></a>시스템 역할에 사용자 또는 그룹을 추가하려면

1. [웹 포털](../web-portal-ssrs-native-mode.md)을 시작합니다.

2. 오른쪽 상단에서 *기어 아이콘*을 선택합니다.

3. **사이트 설정**을 선택합니다.

4. **보안**을 선택합니다.

5. **그룹 또는 사용자 추가**를 선택합니다.

6. **그룹 또는 사용자**에 Windows 도메인 사용자 또는 \<domain>\\<account\> 형식으로 그룹 계정을 입력합니다. 

    > [!NOTE]
    > 폼 인증 또는 사용자 지정 보안을 사용하는 경우에는 해당 배포에 적절한 형식으로 사용자 또는 그룹 계정을 지정합니다.

7. 시스템 역할을 선택한 다음 **확인**을 선택합니다.

    역할은 누적되므로 시스템 관리자와 시스템 사용자를 모두 선택하면 사용자 또는 그룹이 두 역할 모두에서 태스크를 수행할 수 있습니다.

8. 위의 단계를 반복하여 추가 사용자 또는 그룹에 대한 할당을 만듭니다.

### <a name="to-add-a-user-or-group-to-an-item-role"></a>항목 역할에 사용자 또는 그룹을 추가하려면

1. **웹 포털**을 시작하고 사용자 또는 그룹을 추가할 보고서 항목을 찾습니다.

2. 항목에서 **...**(줄임표)를 선택합니다.

3. 드롭다운 메뉴에서 **관리**를 선택합니다.

4. **보안**을 선택합니다.

5. **그룹 또는 사용자 추가**를 선택합니다.

    > [!NOTE]
    > 항목이 현재 부모 항목의 보안을 상속하는 경우에는 도구 모음에서 **보안 사용자 지정**을 선택하여 보안 설정을 변경합니다. 그런 다음 **그룹 또는 사용자 추가**를 선택합니다.

6. **그룹 또는 사용자**에 Windows 도메인 사용자 또는 \<domain>\\<account\> 형식으로 그룹 계정을 입력합니다. 폼 인증 또는 사용자 지정 보안을 사용하는 경우에는 해당 배포에 적절한 형식으로 사용자 또는 그룹 계정을 지정합니다.

7. 사용자 또는 그룹에서 항목에 액세스하는 방법을 설명하는 역할 정의를 하나 이상 선택한 다음 **확인**을 선택합니다.

8. 위의 단계를 반복하여 추가 사용자 또는 그룹에 대한 할당을 만듭니다.

## <a name="next-steps"></a>다음 단계

[역할 할당 생성 및 관리](../../reporting-services/security/create-and-manage-role-assignments.md)   
[새 역할 할당: 역할 할당 편집 페이지&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/3319ced0-4b86-42af-b18d-da41a625113c)   
[보안 속성 페이지, 항목&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/351b8503-354f-4b1b-a7ac-f1245d978da0)   
[역할 할당](../../reporting-services/security/role-assignments.md)   
[역할 정의](../../reporting-services/security/role-definitions.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)