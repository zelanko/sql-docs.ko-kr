---
title: 비즈니스 규칙에 여러 조건 추가(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f9f8114186aa3593f2218037add9a0611a8fe23
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792957"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>비즈니스 규칙에 여러 조건 추가(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 더 복잡한 규칙을 원할 경우 여러 **AND** 또는 **OR** 조건을 비즈니스 규칙에 추가합니다.  
  
> [!NOTE]  
>  **OR** 연산자를 사용하는 비즈니스 규칙을 만드는 경우 개별적으로 평가할 수 있는 각 조건 문에 대해 개별 규칙을 만드는 것을 고려해 보십시오. 그런 다음 필요에 따라 규칙을 제외시키면 유연성이 향상되고 더 쉽게 문제를 해결할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
-   비즈니스 규칙이 있어야 합니다. 자세한 내용은 [비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)를 참조하세요.  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>여러 조건을 비즈니스 규칙에 추가하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 목록에서 멤버 유형을 선택 합니다.  
  
6.  **특성** 목록에서 특성을 선택하거나 기본값인 **모두**를 그대로 사용합니다.  
  
7.  편집할 비즈니스 규칙 행을 클릭합니다.  
  
8.  **선택한 비즈니스 규칙 편집**을 클릭합니다.  
  
9. 에 **구성 요소** 창 확장 된 **논리 연산자** 노드.  
  
10. 클릭 **AND** 또는 **OR** 로 끌어다 놓습니다 합니다 **IF** 창의 **AND** 레이블.  
  
11. **구성 요소** 창에서 **조건** 노드를 확장합니다.  
  
12. 조건을 클릭 하 고 끌어 옵니다 **경우** 창에는 **AND** 또는 **OR** 10 단계에서 레이블.  
  
13. 에 **특성** 창에 특성을 클릭 하 고 끌어 옵니다 합니다 **조건 편집** 창의 **특성 선택** 레이블.  
  
14. 에 **조건 편집** 창에 모든 필수 필드를 완료 합니다.  
  
15. **조건 편집** 창에서 **항목 저장**을 클릭합니다.  
  
16. 필요에 따라에서 조건을 더 추가 하는 **구성 요소** 창으로 끕니다 **AND** 또는 **OR** 에 **AND** 또는 **OR**에 **경우** 창입니다. 그런 다음 13-15단계를 수행합니다.  
  
    > [!TIP]  
    >  조건을 삭제 하 고 조건의 이름을 클릭 합니다 **조건 편집** 창 클릭 **삭제 항목**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [비즈니스 규칙&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [비즈니스 규칙 이름 변경&#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [알림을 보내도록 비즈니스 규칙 구성&#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
