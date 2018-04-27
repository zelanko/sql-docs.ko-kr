---
title: 테이블 속성 편집 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- editTabProps
ms.assetid: 95ea72ba-8e40-4177-a963-0fb4d10c56e3
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5eb90214c73b52aa476c5d214a5760d0f3aab326
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="edit-the-table-properties"></a>테이블 속성 편집
  이 대화 상자를 사용하여 변경을 캡처 중인 선택된 테이블에서 특정 열을 편집할 수 있습니다. 또한 **보안 역할** 및 **캡처 인스턴스** 정보를 편집할 수 있습니다.  
  
### <a name="to-edit-the-columns-to-include-in-the-cdc-instance"></a>CDC 인스턴스에 포함할 열을 편집하려면  
  
1.  다음 중 하나 또는 모두를 수행합니다.  
  
    -   포함할 추가 열의 옆에 있는 확인란을 선택합니다.  
  
    -   더 이상 포함하지 않을 열의 옆에 있는 확인란을 선택 취소합니다.  
  
### <a name="to-edit-the-security-role"></a>보안 역할을 편집하려면  
  
1.  **보안 역할** 필드에서 새 이름을 입력하거나 보안 역할의 이름을 편집합니다.  
  
### <a name="to-create-a-new-capture-instance"></a>새 캡처 인스턴스를 만들려면  
  
1.  **보안 역할** 섹션의 **이름** 필드에 캡처 인스턴스의 이름을 입력합니다. 기본적으로 이 필드에 입력된 이름의 끝에 **_NEW** 를 추가하면 현재 캡처 인스턴스의 이름이 됩니다(예: **old_instance_NEW**).  
  
2.  캡처 인스턴스를 다음 중 하나로 저장합니다.  
  
    -   **새 캡처 인스턴스**: 이 경우 새 캡처 인스턴스는 저장되지만, 이전 캡처 인스턴스는 삭제되지 않습니다.  
  
         **참고**: 캡처 인스턴스는 테이블당 두 개를 초과할 수 없습니다. 이미 두 개의 캡처 인스턴스가 있는 경우에는 이 옵션을 사용할 수 없습니다.  
  
    -   **기존 항목 바꾸기**: 이 경우 현재 캡처 인스턴스가 삭제되고 사용자가 만든 캡처 인스턴스로 대체됩니다. 이 테이블에 대해 두 개의 캡처 인스턴스가 정의되어 있는 경우 하나를 선택하여 바꾸어야 합니다.  
  
 **참고**: **테이블** 탭의 테이블 목록에서 캡처 인스턴스를 제거할 수 있습니다.  
  
 이 대화 상자에 정보를 입력한 후 **확인** 을 클릭하여 변경 내용을 적용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CDC 인스턴스 속성을 편집하는 방법](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [변경 캡처를 위해 선택된 테이블 변경](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)  
  
  
