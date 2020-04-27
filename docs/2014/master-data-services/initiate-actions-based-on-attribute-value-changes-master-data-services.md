---
title: 특성 값 변경 기반 동작 시작(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], tracking attribute changes
- change tracking groups [Master Data Services], initiating actions
ms.assetid: 5e4402ce-31db-4774-a2a1-552335f87693
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: deaa7ca2225d6de503ceb3d5d901a5a51d11aa68
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479360"
---
# <a name="initiate-actions-based-on-attribute-value-changes-master-data-services"></a>특성 값 변경 기반 동작 시작(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성 값 변경을 기반으로 동작을 시작하는 비즈니스 규칙을 만듭니다. 예를 들어, 특정 특성 값이 변경될 때 값을 변경하거나 알림을 보내거나 외부 워크플로를 시작할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](administrators-master-data-services.md)를 참조 하세요.  
  
-   특성이 변경 내용 추적 그룹 안에 있어야 합니다. 자세한 내용은 [변경 내용 추적 그룹에 특성 추가&#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) 를 참조하세요.  
  
### <a name="to-create-a-business-rule-to-initiate-actions-based-on-attribute-value-changes"></a>특성 값 변경을 기반으로 하는 동작을 시작하는 비즈니스 규칙을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 목록에서 비즈니스 규칙을 적용할 멤버 유형을 선택합니다.  
  
6.  **특성** 목록에서 특성을 선택하거나 기본값인 **모두**를 그대로 사용합니다.  
  
7.  **비즈니스 규칙 추가**를 클릭합니다.  
  
8.  **선택한 비즈니스 규칙 편집**을 클릭합니다.  
  
9. **구성 요소** 창에서 **조건** 노드를 확장합니다.  
  
10. **값 비교** 노드 아래에서 **이(가) 변경된 경우** 를 **IF** 창의 **조건** 레이블로 끌어 놓습니다.  
  
11. **특성** 창에서 특성을 클릭 하 고 **조건 편집** 창의 **특성 선택** 레이블로 끌어 놓습니다. 이 특성은 규칙에 아무 영향도 주지 않으므로 사용할 수 있는 모든 특성을 선택합니다.  
  
12. **조건 편집** 창의 **변경 내용 추적 그룹** 상자에서 필수 구성 요소의 일부로 할당한 변경 내용 추적 그룹의 번호를 입력합니다.  
  
13. **조건 편집** 창에서 **항목 저장**을 클릭합니다.  
  
14. **구성 요소** 창에서 **동작** 노드를 확장합니다.  
  
15. 동작을 클릭하고 **THEN** 창의 **동작** 레이블로 끌어 놓습니다.  
  
16. **특성** 창에서 특성을 클릭하고 **동작 편집** 창의 **특성 선택** 레이블로 끌어 놓습니다.  
  
17. **동작 편집** 창에서 모든 필수 필드를 작성합니다.  
  
18. **동작 편집** 창에서 **항목 저장**을 클릭합니다.  
  
19. **뒤로**를 클릭합니다.  
  
20. 필요에 따라 **비즈니스 규칙 유지 관리** 페이지에서 비즈니스 규칙을 포함하는 행에 대해 **이름**, **설명**또는 **알림** 열의 셀을 두 번 클릭하여 값을 업데이트합니다.  
  
    > [!NOTE]  
    >  유효성 검사 동작을 포함하는 규칙에 대해서만 알림이 전송됩니다.  
  
21. **비즈니스 규칙 게시**를 클릭합니다.  
  
22. 확인 대화 상자에서 **확인**을 클릭합니다. 규칙의 상태가 **활성**으로 변경됩니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   다음 절차 중 하나를 수행하여 비즈니스 규칙을 데이터에 적용합니다.  
  
    -   [비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [특성을 변경 내용 추적 그룹 &#40;MDS(Master Data Services)에 추가&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)   
 [비즈니스 규칙&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
