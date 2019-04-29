---
title: 알림을 보내도록 비즈니스 규칙 구성(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], configuring notifications
- e-mail [Master Data Services], configuring business rules
- notifications [Master Data Services], configuring business rules
ms.assetid: b24f7b11-ab53-4642-999c-e17b543b3558
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 05ca904445d4a13cdf957ed82e70c70d57b3ad17
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925576"
---
# <a name="configure-business-rules-to-send-notifications-master-data-services"></a>알림을 보내도록 비즈니스 규칙 구성(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 특성 값 변경 내용을 사용자에게 알리려는 경우 알림을 보내도록 비즈니스 규칙을 구성할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 와 **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. **사용자 및 그룹 권한** 기능 영역에 대한 권한이 없으면 알림을 보낼 사용자 및 그룹 목록을 볼 수 없습니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
-   유효성 검사 동작을 사용하는 비즈니스 규칙이 있어야 합니다. 자세한 내용은 [비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)를 참조하세요.  
  
-   알림을 받는 사용자 또는 그룹에게 유효성 검사를 통과하지 못한 특성에 대한 **읽기 전용** 이상의 권한이 있어야 합니다. 특성에 대한 사용 권한이 명시적 또는 암시적으로 거부된 사용자나 그룹의 경우 전자 메일을 받을 수는 있지만 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 특성에 액세스할 수는 없습니다.  
  
-   메일을 그룹에게 보내는 경우에는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에 액세스한 적이 있는 그룹의 멤버만 전자 메일을 받습니다.  
  
### <a name="to-configure-business-rules-to-send-notifications"></a>알림을 보내도록 비즈니스 규칙을 구성하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 목록에서 멤버 유형을 선택 합니다.  
  
6.  **특성** 목록에서 특성을 선택하거나 기본값인 **모두**를 그대로 사용합니다.  
  
7.  표 형태의 비즈니스 규칙에 대 한 행에서 두 번 클릭 합니다 **알림** 필드입니다.  
  
8.  하위 메뉴에서 전자 메일 알림을 보낼 사용자 또는 그룹을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   다음 절차 중 하나를 수행하여 비즈니스 규칙을 데이터에 적용합니다.  
  
    -   [비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   다음과 같이 전자 메일 프로토콜을 구성합니다.  
  
    -   [메일 알림 구성&#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [알림&#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)   
 [메일 알림 구성&#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
  
