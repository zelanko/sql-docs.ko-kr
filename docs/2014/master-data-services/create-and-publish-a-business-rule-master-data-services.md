---
title: 비즈니스 규칙 만들기 및 게시(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2b52be0b8c76333b069c018415ff698f13f824ae
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479891"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>비즈니스 규칙 만들기 및 게시(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 마스터 데이터의 정확성 유지를 위한 비즈니스 규칙을 만듭니다. 규칙을 만든 후 게시해야 데이터에 적용할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-and-publish-a-business-rule"></a>비즈니스 규칙을 만들어 게시하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 목록에서 비즈니스 규칙을 적용할 멤버 유형을 선택합니다.  
  
6.  **특성** 목록에서 특성을 선택하거나 기본값인 **모두**를 그대로 사용합니다.  
  
7.  **비즈니스 규칙 추가**를 클릭합니다.  
  
8.  **선택한 비즈니스 규칙 편집**을 클릭합니다.  
  
9. **구성 요소** 창에서 **조건** 노드를 확장합니다.  
  
10. 조건을 클릭 하 고 끌어 옵니다 합니다 **IF** 창의 **조건** 레이블.  
  
    > [!TIP]  
    >  마우스 오른쪽 단추로 클릭 하 고 선택 하 여 비즈니스 규칙에서 항목을 삭제할 수 있습니다 **삭제**합니다.  
  
11. 에 **특성** 창에 특성을 클릭 하 고 끌어 옵니다 합니다 **조건 편집** 창의 **특성 선택** 레이블.  
  
12. 에 **조건 편집** 창에 모든 필수 필드를 완료 합니다.  
  
13. **조건 편집** 창에서 **항목 저장**을 클릭합니다.  
  
14. **구성 요소** 창에서 **동작** 노드를 확장합니다.  
  
15. 동작을 클릭하고 **THEN** 창의 **동작** 레이블로 끌어 놓습니다.  
  
16. **특성** 창에서 특성을 클릭하고 **동작 편집** 창의 **특성 선택** 레이블로 끌어 놓습니다.  
  
17. **동작 편집** 창에서 모든 필수 필드를 작성합니다.  
  
18. **동작 편집** 창에서 **항목 저장**을 클릭합니다.  
  
19. 필요에 따라 여러 조건을 규칙에 추가합니다. 자세한 내용은 [비즈니스 규칙에 여러 조건 추가&#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)를 참조하세요.  
  
20. **뒤로**를 클릭합니다.  
  
21. 필요에 따라 **비즈니스 규칙 유지 관리** 페이지에서 비즈니스 규칙을 포함하는 행에 대해 **이름**, **설명**또는 **알림** 열의 셀을 두 번 클릭하여 값을 업데이트합니다.  
  
    > [!NOTE]  
    >  유효성 검사 동작을 포함하는 규칙에 대해서만 알림이 전송됩니다.  
  
22. **비즈니스 규칙 게시**를 클릭합니다.  
  
23. 확인 대화 상자에서 **확인**을 클릭합니다. 규칙의 상태가 **활성**으로 변경됩니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   다음 절차 중 하나를 수행하여 비즈니스 규칙을 데이터에 적용합니다.  
  
    -   [비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [알림을 보내도록 비즈니스 규칙 구성&#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [비즈니스 규칙 이름 변경&#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [비즈니스 규칙에 여러 조건 추가&#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
