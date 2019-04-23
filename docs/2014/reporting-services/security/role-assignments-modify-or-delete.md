---
title: 역할 할당 수정 또는 삭제(보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
manager: kfile
ms.openlocfilehash: f8810a4df8c04703667e1b817931ada65fda0e5f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59945429"
---
# <a name="modify-or-delete-a-role-assignment-report-manager"></a>역할 할당 수정 또는 삭제(보고서 관리자)
  역할 할당은 수행할 수 있는 태스크를 포함하는 미리 정의된 역할 정의에 그룹 또는 사용자 계정을 매핑하며 폴더, 보고서, 모델 또는 기타 내용 유형에 상대적으로 수행할 수 있는 작업 유형을 결정합니다. 역할 할당을 만들거나 수정하거나 삭제하려면 보고서 관리자를 사용합니다. 특정 사용자 또는 그룹에 대한 역할 할당을 만든 후에는 나중에 다른 역할을 선택하여 수정할 수 있습니다. 보고서 서버에 대한 사용 권한을 취소하려면 보고서 서버에서 역할 할당을 삭제합니다.  
  
 목적에 따라 적합한 방법이 다를 수 있습니다. 새 역할 정의 사용자 지정 또는 만들기, Active Directory에서 그룹 계정의 멤버 자격 수정 등의 목적이 있을 수 있습니다.  
  
 예를 들어 자신이 작성한 내용을 완전히 관리해야 하지만 내용 관리자와 관련된 전체 권한 집합을 가져서는 안 되는 사용자 그룹이 있다고 가정합니다. 이 경우 내용 관리자에서 **항목의 보안 정책 설정**을 제외한 모든 태스크를 포함하는 부서 내용 관리자라고 하는 새 역할 정의를 만들 수 있습니다.  
  
 마찬가지로 시스템 또는 네트워크 관리자가 보고서 관리자의 역할 할당보다 Active Directory 그룹 계정을 관리하기가 더 쉬운 경우 그룹 계정에 대한 단일 역할 할당을 만들어 역할 할당 관리로 발생하는 오버헤드를 줄이고 사용자가 보고서에 더 이상 액세스하지 않아도 되는 경우 그룹 멤버 자격을 조정할 수 있습니다.  
  
 역할 할당을 수정하거나 삭제하는 것이 적합하다고 판단되면 시스템 역할 할당과 항목 역할 할당을 모두 확인하십시오. 각 유형의 역할 할당은 보고서 관리자의 서로 다른 페이지에서 구성됩니다.  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>시스템 역할 할당을 수정하거나 삭제하려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)를 시작합니다.  
  
2.  **사이트 설정**을 클릭합니다.  
  
3.  **보안**을 클릭합니다. 서버 또는 스케일 아웃 배포에 대해 현재 정의된 모든 시스템 수준 역할 할당이 계정 이름별로 나열됩니다.  
  
4.  수정하거나 삭제할 역할 할당을 찾습니다.  
  
5.  특정 사용자 또는 그룹에 대한 역할을 추가하거나 제거하려면 **편집**을 클릭합니다.  
  
6.  역할 할당을 삭제하려면 사용자 또는 그룹 이름 옆의 확인란을 클릭한 다음 **삭제**를 클릭합니다.  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>항목 역할 할당을 수정하거나 삭제하려면  
  
1.  **보고서 관리자** 를 시작하고 역할 할당을 편집하거나 삭제하려는 항목을 찾습니다.  
  
2.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **보안**을 클릭합니다.  
  
4.  수정하거나 삭제할 역할 할당을 찾습니다.  
  
5.  특정 사용자 또는 그룹에 대한 역할을 추가하거나 제거하려면 **편집**을 클릭합니다.  
  
6.  역할 할당을 삭제하려면 사용자 또는 그룹 이름 옆의 확인란을 클릭한 다음 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 (create-and-manage-role-assignments.md)   
 [역할 할당](role-assignments.md)   
 [사이트 설정 페이지&#40;보고서 관리자&#41;](../site-settings-page-report-manager.md)   
 [새 시스템 역할 할당: 시스템 역할 할당 편집 페이지 &#40;보고서 관리자&#41;](../new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)  
  
  
