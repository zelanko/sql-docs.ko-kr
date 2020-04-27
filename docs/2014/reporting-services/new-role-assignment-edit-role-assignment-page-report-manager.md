---
title: '새 역할 할당: 역할 할당 편집 페이지 (보고서 관리자) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 3319ced0-4b86-42af-b18d-da41a625113c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a9480b0729e7c08117ba5633c6934eca1903a61b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108162"
---
# <a name="new-role-assignment-edit-role-assignment-page-report-manager"></a>새 역할 할당: 역할 할당 편집 페이지(보고서 관리자)
  새 역할 할당 또는 역할 할당 편집 페이지를 사용하여 보고서 서버 항목 및 작업에 대한 권한을 부여할 수 있습니다. 보고서 서버에 액세스해야 하는 각 사용자에게는 액세스의 수준을 정의하는 역할 할당이 필요합니다. 루트 노드 또는 특정 보고서, 모델, 폴더, 리소스 또는 공유 데이터 원본에 대해 역할 할당을 만들 수 있습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보안은 항목에 적용하는 역할 할당을 통해 적용됩니다. 역할 할당에 따라 역할 정의가 그룹이나 사용자에 대응되며 각 역할 정의는 그룹이나 사용자가 특정 항목과 관련하여 수행할 수 있는 태스크를 식별합니다.  
  
 항목 수준 역할 할당은 광범위한 영향을 줄 수 있습니다. 이러한 할당은 단일 보고서나 폴더에 연결될 수도 있지만 폴더 계층 구조의 상위 수준에서 정의되어 트리의 하위 항목 및 폴더로 상속될 수도 있습니다. 자세한 내용은 [사용자에 게 보고서 서버에 대 한 액세스 권한 부여 &#40;보고서 관리자&#41;](security/grant-user-access-to-a-report-server.md)를 참조 하세요.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-new-role-assignment-or-edit-role-assignment-page"></a>새 역할 할당 또는 역할 할당 편집 페이지를 열려면  
  
1.  보고서 관리자를 열고 새 역할 할당을 추가하거나 역할 할당을 편집하려는 항목을 찾습니다.  
  
2.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **보안**을 클릭합니다. 항목의 보안 속성 페이지가 열립니다.  
  
4.  새 역할 할당을 추가하려면 도구 모음에서 **새 역할 할당**을 클릭합니다. 역할 할당을 편집하려면 편집할 그룹이나 사용자 이름 옆에 있는 **편집** 을 클릭합니다.  
  
    > [!NOTE]  
    >   항목이 현재 부모 항목의 보안을 상속하는 경우에는 도구 모음에서 **항목 보안 편집** 을 클릭하여 보안 설정을 변경합니다.  
  
## <a name="options"></a>옵션  
 **그룹 또는 사용자 이름**  
 역할 할당을 만들 그룹 또는 사용자 계정의 이름을 입력합니다. 그룹 또는 사용자 이름은 올바른 Windows 도메인 계정이어야 합니다. 계정을 \<도메인>\\<계정\>형식으로 입력 합니다.  
  
> [!NOTE]  
>  이 입력란은 새 역할 할당 페이지에서만 사용할 수 있습니다.  
  
 **역할**  
 항목의 보안을 정의하는 데 사용할 수 있는 보고서 서버에 정의된 모든 역할을 표시합니다. 보고서 또는 폴더에 대한 역할 할당을 만들거나 변경할 경우에는 하나 이상의 역할을 선택하면서 태스크 조합에 사용자가 수행할 수 있는 동작이 나타나도록 합니다. 각 역할이 지 원하는 태스크 집합을 보려면를 사용 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]합니다. 보고서 관리자에서 역할을 확인, 작성, 수정 또는 삭제할 수 없습니다. 지침은 [역할 만들기, 삭제 또는 수정 &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)를 참조 하세요.  
  
 **설명**  
 역할에 대한 추가 정보를 표시합니다. **브라우저** 또는 **내용 관리자**와 같은 미리 정의된 역할의 설명에는 각 역할이 지원하는 태스크가 요약되어 있습니다.  
  
 **역할 할당 삭제**  
 사용자나 그룹의 기존 역할 할당을 삭제하려면 클릭합니다. 역할 할당이 하나만 남아 있는 경우 역할 할당을 삭제할 수 없습니다. 각 항목에는 역할 할당이 하나 이상 있어야 합니다.  
  
> [!NOTE]  
>  이 단추는 역할 할당 편집 페이지에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Management Studio &#40;역할을 만들거나, 삭제 하거나, 수정&#41;](security/role-definitions-create-delete-or-modify.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](security/granting-permissions-on-a-native-mode-report-server.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [F1 도움말 보고서 관리자](../../2014/reporting-services/report-manager-f1-help.md)   
 [역할 할당](security/role-assignments.md)   
 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](security/grant-user-access-to-a-report-server.md)  
  
  
