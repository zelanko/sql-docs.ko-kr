---
title: 특성 값 요구(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 03f868d679f1d51dbb672cfdab5dbeaa2b4fc8a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65478858"
---
# <a name="require-attribute-values-master-data-services"></a>특성 값 요구(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 마스터 데이터를 완전한 상태로 유지하려면 특성 값을 요구합니다.  
  
> [!NOTE]  
>  도메인 기반 특성 값이 없는 멤버는 이러한 관계를 기반으로 하는 파생 계층에 표시되지 않습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](administrators-master-data-services.md)를 참조 하세요.  
  
### <a name="to-require-attribute-values"></a>특성 값 요청  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 목록에서 비즈니스 규칙을 적용할 멤버 유형을 선택합니다.  
  
6.  **특성** 목록에서 특성을 선택하거나 기본값인 **모두**를 그대로 사용합니다.  
  
7.  **비즈니스 규칙 추가**를 클릭합니다.  
  
8.  **선택한 비즈니스 규칙 편집**을 클릭합니다.  
  
9. **구성 요소** 창에서 **동작** 노드를 확장합니다.  
  
10. **필수를** 클릭 하 고 **THEN** 창의 **동작** 레이블로 끌어 놓습니다.  
  
11. **특성** 창에서 특성을 클릭하고 **동작 편집** 창의 **특성 선택** 레이블로 끌어 놓습니다.  
  
12. **동작 편집** 창에서 **항목 저장**을 클릭합니다.  
  
13. **뒤로**를 클릭합니다.  
  
14. 필요에 따라 **비즈니스 규칙 유지 관리** 페이지에서 비즈니스 규칙을 포함하는 행에 대해 **이름**, **설명**또는 **알림** 열의 셀을 두 번 클릭하여 값을 업데이트합니다.  
  
15. **비즈니스 규칙 게시**를 클릭합니다.  
  
16. 확인 대화 상자에서 **확인**을 클릭합니다. 규칙의 상태가 **활성**으로 변경됩니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   다음 절차 중 하나를 수행하여 비즈니스 규칙을 데이터에 적용합니다.  
  
    -   [비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [비즈니스 규칙 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [파생 계층&#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  
