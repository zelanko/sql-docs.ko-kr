---
title: 역할 만들기, 삭제 또는 수정(Management Studio) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
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
ms.openlocfilehash: f079b7b16f485b92c60952d082281a1dba52d024
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65570551"
---
# <a name="role-definitions---create-delete-or-modify"></a>역할 정의 - 만들기, 삭제 또는 수정

Reporting Services에서는 보고서 서버에 대한 액세스 수준을 정의하는 미리 정의된 역할을 제공합니다. 보고서 서버에 액세스해야 하는 각 사용자 또는 그룹에 허용된 태스크를 정의하는 역할이 할당됩니다. 역할은 보고서 서버 전체에 대해 정의됩니다. 보고서 서버의 모든 영역에서 일관된 방식으로 역할을 정의하고 사용해야 합니다.

역할을 생성, 수정 또는 삭제하려면 [!INCLUDE[SQL Server Management Studio](../../includes/ssmanstudiofull-md.md)]를 사용할 수 있습니다. 사용되지 않은 역할만 삭제할 수 있습니다.

 직접 만든 역할에 사용자와 그룹을 할당하려면 SSRS 웹 포털을 사용합니다. 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여](../../reporting-services/security/grant-user-access-to-a-report-server.md)를 참조하세요.

> [!NOTE]  
>보고서 서버가 SharePoint 통합 모드용으로 구성되고 보고서 서버가 통합된 SharePoint 사이트에 연결된 경우 보고서 서버 내용 및 작업에 대한 액세스를 제어하는 사용 권한 수준을 보고 수정할 수 있습니다.

## <a name="to-create-a-role-definition"></a>역할 정의를 만들려면

1. 개체 탐색기에서 보고서 서버 노드를 확장합니다.

2. 보안 폴더를 확장합니다.

3. 항목 수준의 역할 정의를 만드는 경우 **역할**을 마우스 오른쪽 단추로 클릭하고 > **새 역할**을 선택합니다.

    또는 시스템 수준의 역할 정의를 만드는 경우 **시스템 역할**을 마우스 오른쪽 단추로 클릭하고 > **새 시스템 역할**을 선택합니다.

4. 역할의 고유 이름을 입력합니다. 이름은 한 글자 이상이어야 합니다. 공백 및 특정 기호도 포함할 수 있지만 `[; : \ / @ & = + , $ / * < > | "]` 문자는 포함할 수 없습니다.

5. 설명을 입력합니다(옵션). [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 이 설명은 이 페이지에만 표시됩니다. 웹 포털을 통해 이 항목을 보는 사용자는 해당 도구에서 이 설명을 볼 수 있습니다.

6. 이 역할의 구성원이 수행할 수 있는 태스크를 선택합니다.

7. **확인**을 선택합니다.

### <a name="to-delete-or-modify-a-role-definition"></a>역할 정의를 삭제하거나 수정하려면  

1. 개체 탐색기에서 보고서 서버 노드를 확장합니다.

2. 보안 폴더를 확장합니다.

3. 항목 수준의 역할 정의를 삭제하거나 수정하려면 역할 폴더를 확장하고 다음 작업 중 하나를 수행합니다.

    1. 역할 정의를 삭제하려면 항목을 마우스 오른쪽 단추로 클릭하고 > **삭제**를 선택합니다. **카탈로그 항목 삭제** 대화 상자가 표시됩니다. **확인**을 선택하여 역할을 삭제합니다.
  
    2. 역할 정의를 수정하려면 항목을 마우스 오른쪽 단추로 클릭하고 > **속성**을 선택합니다. **사용자 역할 속성** 대화 상자의 일반 페이지가 표시됩니다.

         이 역할의 구성원이 수행할 수 있는 태스크를 선택하고 **확인**을 선택합니다.
  
4. 시스템 수준의 역할 정의를 삭제하거나 수정하려면 **시스템 역할** 폴더를 확장합니다. 다음 작업 중 하나를 수행합니다.

- 시스템 역할 정의를 삭제하려면 항목을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다. **카탈로그 항목 삭제** 대화 상자가 표시됩니다. **확인**을 선택하여 역할을 삭제합니다.

- 시스템 역할 정의를 수정하려면 항목을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **시스템 역할 속성** 대화 상자의 일반 페이지가 표시됩니다. 이 역할의 구성원이 수행할 수 있는 태스크를 선택하고 **확인**을 선택하여 변경 내용을 적용합니다.

## <a name="see-also"></a>참고 항목

 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
 [역할 할당 만들기 및 관리](../../reporting-services/security/create-and-manage-role-assignments.md)  
 [SQL Server Management Studio의 Reporting Services&#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
