---
title: 코드 외의 특성 값 자동 생성(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b82f6f81-6e9c-4918-9ea9-4ab5f5d11b15
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 871c792780629af9b3304d82ac62939da295cae4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="automatically-generate-attribute-values-other-than-code-master-data-services"></a>코드 외의 특성 값 자동 생성(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 비즈니스 규칙이 적용될 때마다 값으로 정수가 자동 할당되도록 하려면 엔터티의 특성 값에 대해 값을 자동으로 생성합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   숫자 특성이 있어야 합니다. 자세한 내용은 [숫자 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-numeric-attribute-master-data-services.md)를 참조하세요.  
  
### <a name="to-automatically-generate-an-attribute-value"></a>특성 값을 자동으로 생성하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 목록에서 비즈니스 규칙을 적용할 멤버 유형을 선택합니다.  
  
6.  **특성** 목록에서 기본값인 **모두**를 그대로 사용합니다.  
  
7.  **비즈니스 규칙 추가**를 클릭합니다.  
  
8.  **선택한 비즈니스 규칙 편집**을 클릭합니다.  
  
9. **구성 요소** 창에서 **동작** 노드를 확장합니다.  
  
10. 기본값 노드에서 **생성되는 값을 기본값으로 설정** 을 클릭하고 **THEN** 창의 **동작** 레이블로 끌어 놓습니다.  
  
11. **특성** 창에서 생성할 값을 가진 특성을 클릭하고 이를 **동작 편집** 창의 **특성 선택** 레이블로 끌어 놓습니다.  
  
12. **시작 값** 및 **증가값** 상자에 값을 입력합니다. 멤버가 이미 있는 경우 가장 높은 기존 값을 기반으로 값이 설정됩니다. 예를 들어 가장 높은 기존 값이 299이고 **증가값** 을 **1**로 설정하는 경우 다음 멤버의 값은 300으로 설정됩니다.  
  
13. **동작 편집** 창에서 **항목 저장**을 클릭합니다.  
  
14. **뒤로**를 클릭합니다.  
  
15. 필요에 따라 **비즈니스 규칙 유지 관리** 페이지에서 비즈니스 규칙을 포함하는 행에 대해 **이름**, **설명**또는 **알림** 열의 셀을 두 번 클릭하여 값을 업데이트합니다.  
  
16. **비즈니스 규칙 게시**를 클릭합니다.  
  
17. 확인 대화 상자에서 **확인**을 클릭합니다. 규칙의 상태가 **활성**으로 변경됩니다.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
-   [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [코드 자동 생성&#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)   
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [유효성 검사&#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)  
  
  
