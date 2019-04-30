---
title: 역할 만들기, 삭제 또는 수정(Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 703615793c1c9ced7252a03e7597b701c977fbdd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306545"
---
# <a name="create-delete-or-modify-a-role-management-studio"></a>역할 만들기, 삭제 또는 수정(Management Studio)
  Reporting Services에서는 보고서 서버에 대한 액세스 수준을 정의한 미리 정의된 역할을 제공합니다. 보고서 서버에 액세스해야 하는 사용자나 그룹은 수행할 수 있는 태스크를 설명하는 역할을 통해 액세스합니다. 역할은 보고서 서버 전체에 대해 정의됩니다. 보고서 서버의 특정 부분에 대한 역할 정의를 다르게 하거나 환경에 따라 다르게 역할을 사용하도록 지정할 수 없습니다.  
  
 역할을 생성, 수정 또는 삭제하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용합니다. 사용되지 않은 역할만 삭제할 수 있습니다.  
  
 만든 역할에 사용자나 그룹을 할당하려면 보고서 관리자를 사용합니다. 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](grant-user-access-to-a-report-server.md)를 참조하세요.  
  
> [!NOTE]  
>  보고서 서버가 SharePoint 통합 모드용으로 구성되고 보고서 서버가 통합된 SharePoint 사이트에 연결된 경우 보고서 서버 내용 및 작업에 대한 액세스를 제어하는 사용 권한 수준을 보고 수정할 수 있습니다.  
  
### <a name="to-create-a-role-definition"></a>역할 정의를 만들려면  
  
1.  개체 탐색기에서 보고서 서버 노드를 확장합니다.  
  
2.  보안 폴더를 확장합니다.  
  
3.  항목 수준의 역할 정의를 만드는 경우 **역할**을 마우스 오른쪽 단추로 클릭하고 **새 역할**을 가리킵니다.  
  
     또는 시스템 수준의 역할 정의를 만드는 경우 **시스템 역할**을 마우스 오른쪽 단추로 클릭하고 **새 시스템 역할**을 가리킵니다.  
  
4.  역할의 고유 이름을 입력합니다. 이름은 한 글자 이상이어야 합니다. 공백 및 특정 기호도 포함할 수 있지만 ; ? : \@ & = +, $ / * \< > | "또는 /.  
  
5.  설명을 입력합니다(옵션). [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 이 설명은 이 페이지에만 표시됩니다. 보고자 관리자를 통해 이 항목을 보는 사용자는 해당 도구에서 이 설명을 볼 수 있습니다.  
  
6.  이 역할의 멤버가 수행할 수 있는 태스크를 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-or-modify-a-role-definition"></a>역할 정의를 삭제하거나 수정하려면  
  
1.  개체 탐색기에서 보고서 서버 노드를 확장합니다.  
  
2.  보안 폴더를 확장합니다.  
  
3.  항목 수준의 역할 정의를 삭제하거나 수정하려면 역할 폴더를 확장합니다. 다음 중 하나를 수행합니다.  
  
    1.  역할 정의를 삭제하려면 항목을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다. **개체 삭제** 대화 상자가 표시됩니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  역할 정의를 수정하려면 항목을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **사용자 역할 속성** 대화 상자의 일반 페이지가 표시됩니다.  
  
         이 역할의 멤버가 수행할 수 있는 태스크를 선택하고 **확인**을 클릭합니다.  
  
4.  시스템 수준의 역할 정의를 삭제하거나 수정하려면 **시스템 역할** 폴더를 확장합니다. 다음 중 하나를 수행합니다.  
  
    1.  시스템 역할 정의를 삭제하려면 항목을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다. **개체 삭제** 대화 상자가 표시됩니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  시스템 역할 정의를 수정하려면 항목을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **시스템 역할 속성** 대화 상자의 일반 페이지가 표시됩니다.  
  
         이 역할의 멤버가 수행할 수 있는 태스크를 선택하고 **확인** 을 클릭하여 변경 내용을 적용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Management Studio에서 보고서 서버에 연결](../tools/connect-to-a-report-server-in-management-studio.md)   
 (create-and-manage-role-assignments.md)   
 [SQL Server Management Studio의 Reporting Services&#40;SSRS&#41;](../tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  
