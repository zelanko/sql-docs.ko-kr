---
title: 보안 페이지(사이트 설정. 보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: acc9a905-90f8-4544-aec6-b2ab3a1b0015
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6c0b0cc68c73c66dabb237d859aba641fb234647
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102177"
---
# <a name="security-page-site-settings-report-manager"></a>보안 페이지(사이트 설정. 보고서 관리자)
  보안 페이지를 사용하여 보고서 서버 사이트에 대한 액세스를 제어하는 시스템 역할 할당을 볼 수 있습니다. 시스템 역할 할당은 보고서 서버 네임스페이스나 폴더 계층 구조의 범위 밖에 존재합니다. 시스템 역할 할당은 전역적이므로 특정 항목별로 다를 수 없습니다. 시스템 역할 할당을 통해 지원되는 작업에는 공유 일정 작성 및 사용, 보고서 작성기 사용, 일부 서버 기능에 대한 기본값 설정 등이 포함됩니다.  
  
 기본 시스템 역할 할당은 보고서 서버를 설치할 때 생성됩니다. 이 시스템 역할 할당은 로컬 시스템 관리자에게 보고서 서버 환경 관리 권한을 부여합니다. 로컬 시스템 관리자는 시스템 역할 할당이 삭제되어도 항상 로컬 보고서 서버의 보안을 설정할 수 있습니다.  
  
 보고서 작성기 또는 공유 일정에 액세스해야 하는 다른 모든 사용자는 시스템 역할 할당에 할당되어야 합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-security-page-for-site-settings"></a>사이트 설정의 보안 페이지를 열려면  
  
1.  보고서 관리자를 엽니다.  
  
2.  페이지의 맨 위에서 **사이트 설정**을 클릭합니다. 사이트의 일반 속성 페이지가 열립니다.  
  
3.  
  **보안** 탭을 선택합니다.  
  
## <a name="options"></a>옵션  
 **Delete**  
 기존 역할 할당을 삭제하려면 클릭합니다. 제거할 그룹 또는 사용자 이름 옆의 확인란을 선택한 다음에 **삭제**를 클릭하십시오. 유일하게 남은 역할 할당은 삭제할 수 없습니다. 역할 할당을 삭제해도 그룹 또는 사용자 계정이나 역할 정의는 삭제되지 않습니다.  
  
 **새 역할 할당**  
 보고서 서버 사이트에 대한 추가 시스템 역할 할당을 만드는 데 사용되는 새 시스템 역할 할당 페이지를 열려면 클릭합니다. 자세한 내용은 [새 시스템 역할 할당: 시스템 역할 할당 편집 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)를 참조 하세요.  
  
 **편집**  
 보고서 서버 사이트에 대한 개별 시스템 역할 할당을 편집하는 데 사용되는 시스템 역할 할당 편집 페이지를 열려면 클릭합니다. 자세한 내용은 [새 시스템 역할 할당: 시스템 역할 할당 편집 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)를 참조 하세요.  
  
 **그룹 또는 사용자**  
 기존 역할 할당의 일부인 그룹 및 사용자를 나열합니다. 현재 폴더의 기존 역할 할당은 이 열에 표시되는 그룹과 사용자에 대해 정의됩니다. 역할 할당 정보를 보거나 편집하려면 그룹 또는 사용자 이름 옆에 있는 **편집** 을 클릭합니다.  
  
 **역할**  
 기존 역할 할당에 속하는 하나 이상의 역할 정의를 나열합니다. 그룹 또는 사용자 계정에 여러 역할이 할당되어 있으면 해당 그룹 또는 사용자는 모든 역할에 속한 모든 태스크를 수행할 수 있습니다. 각 역할이 지 원하는 태스크 집합을 보려면를 사용 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]합니다. 보고서 관리자에서 역할을 확인, 작성, 수정 또는 삭제할 수 없습니다. 지침은 [역할 만들기, 삭제 또는 수정 &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [F1 도움말 보고서 관리자](../../2014/reporting-services/report-manager-f1-help.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
