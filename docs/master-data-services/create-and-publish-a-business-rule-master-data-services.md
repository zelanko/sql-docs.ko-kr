---
title: 비즈니스 규칙 만들기 및 게시
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e8deee97bd80404df5851f0845aa02b51bfe0cfc
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729448"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>비즈니스 규칙 만들기 및 게시(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 마스터 데이터의 정확성 유지를 위한 비즈니스 규칙을 만듭니다. 규칙을 만든 후 게시해야 데이터에 적용할 수 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-and-publish-a-business-rule"></a>비즈니스 규칙을 만들어 게시하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙** 페이지의 **모델** 드롭다운 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 드롭다운 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 드롭다운 목록에서 비즈니스 규칙을 적용할 멤버 유형을 선택합니다.  
  
6.  **추가**를 클릭합니다.  
  
7.  **이름** 상자에 비즈니스 규칙의 이름을 입력합니다.  
  
8.  필요에 따라 **설명** 필드에 비즈니스 규칙 설명을 입력합니다.  
  
9. 필요에 따라 **알림 보내기** 옵션을 선택하고 드롭다운 목록에서 메일 알림을 보낼 사용자나 그룹을 선택합니다.  
  
    > [!NOTE]  
    >  유효성 검사 동작을 포함하는 규칙에 대해서만 알림이 전송됩니다.  
  
10. **If** 블록 아래에서 **추가**를 클릭합니다. 그러면 패널이 표시됩니다.  
  
11. **특성** 드롭다운 목록에서 특성을 선택합니다.  
  
12. **연산자** 드롭다운 목록에서 조건을 선택합니다.  
  
13. 모든 필수 필드에 내용을 입력합니다.  
  
14. **저장** 단추를 클릭합니다. 새 행이 **If** 표에 추가됩니다.  
  
    > [!TIP]  
    >  각 항목을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택하여 비즈니스 규칙에서 항목을 삭제할 수 있습니다.  
  
15. 필요에 따라 여러 조건을 규칙에 추가합니다. 자세한 내용은 [비즈니스 규칙에 여러 조건 추가&#40;Master Data Services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)를 참조하세요.  
  
16. **Then** 블록 아래에서 **추가** 를 클릭합니다. 그러면 패널이 표시됩니다.  
  
17. **특성** 드롭다운 목록에서 특성을 선택합니다.  
  
18. **연산자** 드롭다운 목록에서 동작을 선택합니다.  
  
19. 모든 필수 필드에 내용을 입력합니다.  
  
20. **저장**을 클릭합니다. 새 행이 **Then** 표에 추가됩니다.  
  
21. 필요에 따라 **Else** 동작을 추가하려면 다음 단계를 완료합니다.  
  
    1.  **Else** 블록 아래에서 **추가**를 클릭합니다. 그러면 패널이 표시됩니다.  
  
    2.  **특성** 드롭다운 목록에서 특성을 선택합니다.  
  
    3.  **연산자** 드롭다운 목록에서 동작을 선택합니다.  
  
    4.  모든 필수 필드에 내용을 입력합니다.  
  
    5.  **저장**을 클릭합니다. 새 행이 **Else** 표에 추가됩니다.  
  
22. **저장**을 클릭합니다. 새 행이 비즈니스 규칙 표에 추가됩니다.  
  
23. **모두 게시**를 클릭합니다.  
  
24. 확인 대화 상자에서 **확인**을 클릭합니다. **비즈니스 규칙 상태** 열의 값은 **활성**입니다.  
  
## <a name="grid-columns"></a>표 형태의 열  
 생성되는 각 비즈니스 규칙에 대해 열이 6개 포함된 행이 표에 추가됩니다. 이러한 열은 다음과 같습니다.  
  
|이름|설명|  
|----------|-----------------|  
|상태|**저장** 을 클릭하면 비즈니스 규칙이 업데이트되고 있음을 나타내는 다음 이미지가 표시됩니다.<br /><br /> ![mds_BR_refresh](../master-data-services/media/mds-br-refresh.png "mds_BR_refresh ")<br /><br /> 비즈니스 규칙을 만들거나 편집할 때 오류가 발생하면 다음 이미지가 표시됩니다.<br /><br /> ![mds_br_error](../master-data-services/media/mds-br-error.png "mds_br_error ")<br /><br /> 비즈니스 규칙이 정상 상태이면 다음 이미지가 표시됩니다.<br /><br /> ![mds_BR_success](../master-data-services/media/mds-br-success.png "mds_BR_success ")|  
|이름|비즈니스 규칙 이름입니다.|  
|설명|비즈니스 규칙 설명입니다.|  
|비즈니스 규칙 상태|규칙이 정의되지 않았습니다./활성/제외됨/변경 보류 중/제외 보류 중/삭제 보류 중 하나입니다.|  
|제외됨|비즈니스 규칙을 제외할지 여부를 지정합니다.|  
|알림|전자 메일 알림을 보내도록 선택한 사용자 또는 그룹을 지정합니다.|  
  
## <a name="next-steps"></a>다음 단계  
  
-   다음 절차 중 하나를 수행하여 비즈니스 규칙을 데이터에 적용합니다.  
  
    -   [비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>관련 항목:  
 [알림을 보내도록 비즈니스 규칙 구성&#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [비즈니스 규칙 이름 변경&#40;Master Data Services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [비즈니스 규칙에 여러 조건 추가&#40;Master Data Services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
