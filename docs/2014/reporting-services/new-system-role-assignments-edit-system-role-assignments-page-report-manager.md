---
title: '새 시스템 역할 할당: 시스템 역할 할당 편집 페이지 (보고서 관리자) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 62a22ab9-1eb4-4ce5-8dd7-06b5ed2d9a2a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 661ae0cafe5b484839bbee2531f82f3b62f72c75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108127"
---
# <a name="new-system-role-assignments-edit-system-role-assignments-page-report-manager"></a>새 시스템 역할 할당: 시스템 역할 할당 편집 페이지 (보고서 관리자)
  새 시스템 역할 할당 또는 시스템 역할 할당 편집 페이지를 사용하여 보고서 서버의 보안을 정의할 수 있습니다. 모든 보안은 특정 사용자나 그룹을 각기 수행 가능한 태스크에 매핑하는 역할 할당을 통해 정의됩니다. 태스크 목록은 역할 할당을 만들 때 선택하는 역할 정의로 표시됩니다.  
  
 시스템 수준에서 만들거나 수정하는 역할 할당은 보고서 서버 전체에 적용됩니다. 예를 들어 공유 일정은 시스템 전체에서 사용되므로 공유 일정을 만드는 기능은 시스템 수준에서 지정됩니다.  
  
 기본적으로 Reporting Services는 다음과 같은 두 개의 미리 정의된 시스템 수준 역할을 제공합니다.  
  
-   시스템 사용자에는 사용자가 보고서 서버 속성과 공유 일정을 보도록 허용하는 태스크와 사용자가 보고서 서버에 게시된 클릭 광고 보고서를 보도록 허용하는 보고서 정의 실행 태스크가 포함됩니다. 대부분의 사용자는 이 역할에 할당됩니다.  
  
-   시스템 관리자에는 공유 일정 작성 및 관리, 서버 속성 설정, 다른 사용자에 대한 시스템 수준 역할 할당 생성을 위한 태스크가 포함됩니다. 이 수준의 권한이 필요한 사용자는 극소수입니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-new-system-role-assignments-or-edit-system-role-assignments-page"></a>새 시스템 역할 할당 또는 시스템 역할 할당 편집 페이지를 열려면  
  
1.  보고서 관리자를 엽니다.  
  
2.  페이지 맨 위에서 오른쪽 모퉁이에 있는 **사이트 설정**을 클릭합니다. 사이트의 일반 속성 페이지가 열립니다.  
  
3.  **보안** 탭을 선택합니다. 이 페이지에 액세스하려면 내용 관리자 및 시스템 관리자 권한이 있어야 합니다.  
  
4.  새 역할 할당을 만들려면 도구 모음에서 **새 역할 할당** 을 클릭합니다. 기존 역할 할당을 편집하려면 보안 속성 페이지에서 그룹이나 사용자 옆에 있는 **편집** 을 클릭합니다.  
  
## <a name="options"></a>변수  
 **그룹 또는 사용자**  
 사용자 도메인의 그룹 또는 사용자 계정의 이름을 입력합니다. 보고서 서버가 로컬 계정으로 실행되고 있는 경우에는 로컬 그룹 또는 사용자를 지정해야 하고, 보고서 서버가 도메인 계정으로 실행되고 있는 경우에는 도메인 그룹 또는 사용자를 지정해야 합니다. 이 형식으로 계정을 입력 합니다. \<도메인 >\\< 계정\>합니다.  
  
> [!NOTE]  
>  이 입력란은 새 역할 할당 페이지에서만 사용할 수 있습니다.  
  
 **Roles**  
 다른 사용자에게 할당할 수 있는 시스템 수준 역할의 목록을 제공합니다. 하나의 역할 할당에 대해 여러 역할을 지정할 수 있습니다.  
  
 보고서 관리자는 각 역할의 태스크를 표시하지 않으며 태스크를 추가 또는 수정하는 방법을 제공하지 않습니다. 정의된 그대로 역할을 사용해야 합니다. 역할을 생성, 수정 또는 삭제하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 사용합니다. 자세한 내용은 [역할 만들기, 삭제 또는 수정&#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)을 참조하세요.  
  
 [!INCLUDE[ssExpressEd2005](../includes/ssexpressed2005-md.md)] with Advanced Services를 사용하는 경우에는 제공된 기본 역할을 사용해야 합니다.  
  
 **설명**  
 역할에 대한 추가 정보를 표시합니다. 시스템 사용자 또는 시스템 관리자와 같은 미리 정의된 역할의 경우 설명에는 각 역할이 지원하는 태스크가 요약되어 표시됩니다.  
  
 **역할 할당 삭제**  
 사용자나 그룹의 기존 역할 할당을 삭제하려면 클릭합니다. 역할 할당이 하나만 남아 있는 경우 역할 할당을 삭제할 수 없습니다. 각 항목에는 역할 할당이 하나 이상 있어야 합니다.  
  
> [!NOTE]  
>  이 단추는 역할 할당 편집 페이지에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)   
 [역할 할당](security/role-assignments.md)   
 [역할 정의](security/role-definitions.md)  
  
  
