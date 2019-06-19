---
title: 특성 값 요구(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], requiring attribute values
- attributes [Master Data Services], requiring values
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ae1eb0a03e7387c7985a4b05f9f0fba562d03d67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65485970"
---
# <a name="require-attribute-values-master-data-services"></a>특성 값 요구(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 마스터 데이터를 완전한 상태로 유지하려면 특성 값을 요구합니다.  
  
> [!NOTE]  
>  도메인 기반 특성 값이 없는 멤버는 이러한 관계를 기반으로 하는 파생 계층에 표시되지 않습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-require-attribute-values"></a>특성 값 요청  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙** 페이지의 **모델** 드롭다운 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 드롭다운 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 드롭다운 목록에서 비즈니스 규칙을 적용할 멤버 유형을 선택합니다.  
  
6.  **추가**를 클릭합니다.  
  
7.  **이름** 상자에 비즈니스 규칙의 이름을 입력합니다.  
  
8.  필요에 따라 **설명** 필드에 비즈니스 규칙 설명을 입력합니다.  
  
9. **Then** 블록에서 **추가**를 클릭합니다. 그러면 패널이 표시됩니다.  
  
10. **연산자** 드롭다운 목록에서 **필수 동작**을 선택합니다.  
  
11. **특성** 드롭다운 목록에서 특성을 선택합니다.  
  
12. **저장**을 클릭합니다. 새 행이 **Then** 표에 추가됩니다.  
  
13. **저장**을 클릭합니다.  
  
14. **모두 게시**를 클릭합니다.  
  
15. 확인 대화 상자에서 **확인**을 클릭합니다. **비즈니스 규칙 상태** 열의 값은 **활성**입니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   다음 절차 중 하나를 수행하여 비즈니스 규칙을 데이터에 적용합니다.  
  
    -   [비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [파생 계층&#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
