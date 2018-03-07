---
title: "비즈니스 규칙에 여러 조건 추가(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc94f027c82da03f549e70a5b7e6391902561a19
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2018
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>비즈니스 규칙에 여러 조건 추가(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 더 복잡한 규칙을 원할 경우 여러 **AND** 또는 **OR** 조건을 비즈니스 규칙에 추가합니다.  
  
> [!NOTE]  
>  **OR** 연산자를 사용하는 비즈니스 규칙을 만드는 경우 개별적으로 평가할 수 있는 각 조건 문에 대해 개별 규칙을 만드는 것을 고려해 보십시오. 그런 다음 필요에 따라 규칙을 제외시키면 유연성이 향상되고 더 쉽게 문제를 해결할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   비즈니스 규칙이 있어야 합니다. 자세한 내용은 [비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)를 참조하세요.  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>여러 조건을 비즈니스 규칙에 추가하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙** 페이지의 **모델** 드롭다운 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 드롭다운 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 드롭다운 목록에서 멤버 유형을 선택합니다.  
  
6.  편집할 비즈니스 규칙 행을 클릭합니다.  
  
7.  **편집**을 클릭합니다.  
  
8.  **If** 블록 아래의 논리 연산자 드롭다운 목록 왼쪽에서 **AND/OR/NOT**을 선택합니다.  
  
9. **추가**를 클릭합니다. 그러면 패널이 표시됩니다.  
  
10. **특성** 드롭다운 목록에서 특성을 선택합니다.  
  
11. **연산자** 드롭다운 목록에서 조건을 선택합니다.  
  
12. 모든 필수 필드에 내용을 입력합니다.  
  
13. **저장**을 클릭합니다. 새 행이 **If** 표에 추가됩니다.  
  
14. 필요에 따라 조건을 더 추가하려면 8~13단계를 완료합니다.  
  
    > [!TIP]  
    >  조건을 삭제하려면 해당 조건을 선택하고 마우스 오른쪽 단추를 클릭한 다음 **삭제**를 클릭합니다.  
  
    > [!TIP]  
    >  여러 조건을 선택할 수 있으며, 마우스 오른쪽 단추를 클릭하여 하나의 논리 연산자 내에서 조건을 그룹화하거나 특정 논리 연산자 내에서 조건의 그룹을 해제할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [비즈니스 규칙 이름 변경&#40;Master Data Services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [알림을 보내도록 비즈니스 규칙 구성&#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
