---
title: 역할 할당 수정 또는 삭제(SSRS 웹 포털) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 28695a4849b29c6e593f42489fc149efd9a8db53
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570642"
---
# <a name="role-assignments---modify-or-delete"></a>역할 할당 - 수정 또는 삭제

역할 할당은 수행할 수 있는 태스크를 정의하는 미리 정의된 역할에 그룹 또는 사용자 계정을 매핑하며 폴더, 보고서, 모델 또는 기타 콘텐츠 형식에 사용자가 수행하는 태스크 유형을 결정합니다. 역할 할당을 만들거나 수정하거나 삭제하려면 SSRS 웹 포털을 사용합니다. 특정 사용자 또는 그룹에 대한 역할 할당을 만든 후에는 나중에 다른 역할을 선택하여 수정할 수 있습니다. 보고서 서버에 대한 사용 권한을 취소하려면 보고서 서버에서 역할 할당을 삭제합니다.  

목적에 따라 적합한 방법이 다를 수 있습니다. 새 역할 정의 사용자 지정 또는 만들기, Active Directory에서 그룹 계정의 멤버 자격 수정 등의 목적이 있을 수 있습니다.  

예를 들어 자신의 콘텐츠를 관리해야 하지만 콘텐츠 관리자와 관련된 전체 권한 집합을 가져서는 안 되는 사용자 그룹이 있다고 가정합니다. 부서 콘텐츠 관리자라는 새 역할 정의를 만들 수 있습니다. 이 역할은 **항목에 대한 보안 정책 설정**을 제외하고 콘텐츠 관리자의 모든 태스크를 포함할 수 있습니다.

마찬가지로, 시스템 또는 네트워크 관리자인 경우 웹 포털에서 역할 할당을 관리하는 것보다 Active Directory 그룹 계정을 관리하는 것이 더 편리합니다. 그룹 계정에 대해 단일 역할 할당을 만들어 역할 할당 관리 오버헤드를 줄일 수 있습니다. 그런 다음, 사용자가 보고서에 더 이상 액세스할 필요가 없는 경우 그룹 멤버 자격을 수정할 수 있습니다.
  
 역할 할당을 수정하거나 삭제하는 것이 적합하다고 판단되면, 시스템 역할 할당과 항목 역할 할당을 모두 확인해야 합니다. 각 유형의 역할 할당은 웹 포털의 서로 다른 페이지에서 구성됩니다.
  
## <a name="to-modify-or-delete-a-system-role-assignment"></a>시스템 역할 할당을 수정하거나 삭제하려면
  
1. [보고서 서버의 웹 포털 &#40;SSRS 기본 모드&#41;](../../reporting-services/web-portal-ssrs-native-mode.md)에 액세스합니다.

2. **사이트 설정** > **보안**을 선택합니다. 서버 또는 스케일 아웃 배포에 대해 현재 정의된 모든 시스템 수준 역할 할당이 계정 이름별로 나열됩니다.

3. 수정하거나 삭제할 역할 할당을 찾습니다.

4. 특정 사용자 또는 그룹의 역할을 추가하거나 제거하려면 **편집**을 선택합니다.

5. 역할 할당을 삭제하려면 사용자 또는 그룹 이름 옆의 확인란을 선택하고 **삭제**를 선택합니다.

### <a name="to-modify-or-delete-an-item-role-assignment"></a>항목 역할 할당을 수정하거나 삭제하려면

1. 웹 포털에 액세스하고 역할 할당을 편집하거나 삭제하려는 항목을 찾습니다.

2. 항목을 마우스로 가리키고 드롭다운 화살표를 선택합니다.

3. 드롭다운 메뉴에서 **보안**을 선택합니다.

4. 수정하거나 삭제할 역할 할당을 찾습니다.

5. 특정 사용자 또는 그룹의 역할을 추가하거나 제거하려면 **편집**을 선택합니다.

6. 역할 할당을 삭제하려면 사용자 또는 그룹 이름 옆의 확인란을 선택하고 **삭제**를 선택합니다.

## <a name="see-also"></a>관련 항목:

[역할 할당 만들기 및 관리](../../reporting-services/security/create-and-manage-role-assignments.md)  
[역할 할당](../../reporting-services/security/role-assignments.md)  
