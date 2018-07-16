---
title: 도메인 기반 특성 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: fd6e0a992dd4f23b6da24ed70cb884025c969537
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320453"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>도메인 기반 특성 만들기(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 도메인 기반 특성을 만들어서 엔터티의 멤버로 특성 값을 채웁니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
-   특성 값의 원본으로 사용할 엔터티가 있어야 합니다. 예를 들어 Color 엔터티를 기반으로 하는 도메인 기반 특성을 만들려면 먼저 Color 엔터티를 만들어야 합니다. 자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
-   해당 특성을 만들 엔터티가 있어야 합니다. 자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-a-domain-based-attribute"></a>도메인 기반 특성을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
5.  **선택한 엔터티 편집**을 클릭합니다.  
  
6.  **엔터티 편집** 페이지에서  
  
    -   리프 멤버에 대한 특성일 경우 **리프 멤버 특성** 창에서 **리프 특성 추가**를 클릭합니다.  
  
    -   통합 멤버에 대한 특성일 경우 **통합 멤버 특성** 창에서 **통합 특성 추가**를 클릭합니다.  
  
    -   컬렉션에 대한 특성일 경우 **컬렉션 특성** 창에서 **컬렉션 특성 추가**를 클릭합니다.  
  
7.  에 **특성 추가** 페이지를 선택 합니다 **도메인 기반** 옵션입니다.  
  
8.  **이름** 상자에 특성의 이름을 입력합니다. 이름이 특성 값의 원본으로 사용할 엔터티와 동일할 필요는 없습니다.  
  
9. **탐색기** 표에 표시할 특성 열의 너비를 **표시 픽셀 폭** 상자에 입력합니다.  
  
10. **엔터티** 목록에서 특성 값을 채우는 데 사용할 엔터티를 선택 합니다.  
  
11. (선택 사항) 특성 그룹의 변경 내용을 추적하려면 **Enable change tracking** 을 선택합니다. 자세한 내용은 [변경 내용 추적 그룹에 특성 추가&#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)를 참조하세요.  
  
12. **특성 저장**을 클릭합니다.  
  
13. **엔터티 유지 관리** 페이지에서 **엔터티 저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [도메인 기반 특성 &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)   
 [파생된 계층을 만들려면 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [특성 이름 변경 &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [특성 삭제 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-master-data-services.md)  
  
  
