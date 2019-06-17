---
title: 역할 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- roles [Reporting Services], security
- security [Reporting Services], role definitions
- role-based security [Reporting Services], role definitions
ms.assetid: d1b8dbf0-4462-402e-92dd-0e4835002b6e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6518a46c44a97fbb386b4479454e89a0eccb1a39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101747"
---
# <a name="role-definitions"></a>역할 정의
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 *역할**정의*는 보고서 서버에서 사용할 수 있는 작업을 정의하는 명명된 태스크 모음입니다. 역할 정의는 보고서 서버가 보안을 강화하기 위해 사용하는 규칙을 제공합니다. 사용자가 보고서 게시와 같은 태스크를 수행하려고 하면 보고서 서버가 사용자의 역할 할당을 검사하여 이 태스크가 해당 역할 정의에 포함되어 있는지 여부를 확인합니다. 해당 태스크가 역할 정의에 포함되어 있으면 요청이 제출됩니다.  
  
## <a name="using-roles-to-authorize-access-to-a-report-server"></a>역할을 사용하여 보고서 서버에 대한 액세스 권한 부여  
 역할은 역할 할당에 사용되는 경우에만 적용됩니다. 역할에서 보안을 제공하는 방법은 [역할 할당](role-assignments.md)을 참조하세요.  
  
## <a name="types-of-role-definitions"></a>역할 정의 유형  
 역할 정의는 항목 수준 또는 시스템 수준 정의 중 하나입니다. *항목 수준의 역할 정의* 에서는 보고서 서버에서 저장 및 관리되는 항목(예: 보고서, 폴더 및 모델)과 관련된 태스크에 대해 설명합니다. 항목 수준 역할 정의에 포함할 수 있는 태스크에는 보고서 관리, 폴더 보기, 개별 구독 관리 등이 있습니다. *시스템 역할 정의* 에는 사이트에 전체적으로 적용되는 태스크가 포함됩니다. 시스템 역할에 포함할 수 있는 태스크에는 보고서 서버 속성 보기가 있습니다.  
  
## <a name="predefined-roles"></a>미리 정의된 역할  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 다양한 수준의 사용자 상호 작용에 해당하는 미리 정의된 역할이 들어 있습니다. 다음 목록에는 사용할 수 있는 미리 정의된 역할이 나와 있습니다.  
  
-   내용 관리자, 게시자, 브라우저, 보고서 작성기 및 내 보고서는 보고서 서버 내용에 액세스하는 데 사용되는 역할 할당을 만들 때 사용할 수 있는 항목 수준 역할 정의입니다.  
  
-   시스템 관리자 및 시스템 사용자는 사이트 작업에 대한 액세스 권한을 부여하는 데 사용할 수 있는 시스템 수준 역할 정의입니다.  
  
 자세한 내용은 [미리 정의된 역할](role-definitions-predefined-roles.md)을 참조하세요.  
  
## <a name="creating-a-role-definition"></a>역할 정의 만들기  
 역할을 만들려면 Management Studio를 사용하여 이름과 역할에 포함할 태스크를 지정합니다. 항목 태스크와 시스템 태스크에 대해서는 별개의 역할 정의를 만들어야 합니다. 역할은 항목 수준 작업 또는 시스템 수준 태스크를 포함할 수 있지만 둘 다 포함할 수는 없습니다. 역할 정의를 만들려면 이름을 입력하고 정의에 사용할 태스크 집합을 선택합니다. 역할 정의를 만들려면 해당 권한이 있어야 합니다. "개별 항목의 보안 설정" 태스크는 이러한 권한을 제공합니다. 기본적으로 미리 정의된 **내용 관리자** 역할이 할당된 관리자 및 사용자는 이 태스크를 수행할 수 있습니다.  
  
 역할에는 고유 이름이 있어야 합니다. 역할 정의가 유효하려면 태스크를 하나 이상 포함해야 합니다. 자세한 내용은 [Tasks and Permissions](tasks-and-permissions.md)을 참조하세요.  
  
 역할 정의를 만들려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용합니다. 자세한 내용은 [역할 만들기, 삭제 또는 수정&#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)을 참조하세요.  
  
 역할 정의를 만든 후 역할 할당에서 이를 선택하여 사용할 수 있습니다. 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](grant-user-access-to-a-report-server.md)을 참조하세요.  
  
## <a name="customize-or-delete-a-role-definition"></a>역할 정의 사용자 정의 또는 삭제  
 미리 정의된 역할은 수정하거나 사용자 지정 역할로 바꿀 수 있습니다. 역할을 수정하려면 역할 정의에서 태스크를 추가 또는 제거하고, 역할 이름은 바꿀 수 없습니다. 역할 정의에 대한 모든 변경 내용은 해당 역할 정의를 포함하는 모든 역할 할당에 바로 적용됩니다.  
  
 더 이상 사용하지 않는 역할 정의는 삭제할 수 있습니다. 내 보고서 기능을 사용하는 한 해당 기능에 대해 선택된 역할 정의는 삭제할 수 없습니다. 내 보고서에서 사용되는 역할 정의를 삭제하려면 먼저 이 기능을 해제하거나 이 기능에서 다른 역할 정의를 사용하도록 선택해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Tasks and Permissions](tasks-and-permissions.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](granting-permissions-on-a-native-mode-report-server.md)   
 [역할 만들기, 삭제 또는 수정&#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)   
 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](grant-user-access-to-a-report-server.md)   
 [역할 할당 수정 또는 삭제&#40;보고서 관리자&#41;](role-assignments-modify-or-delete.md)   
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
  
  
