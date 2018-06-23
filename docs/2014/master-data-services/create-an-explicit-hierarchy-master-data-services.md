---
title: 명시적 계층 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: de4402b3baf2991d8334eec9e679d6fac2390310
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092020"
---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>명시적 계층 만들기(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 멤버가 임의의 수준에 존재할 수 있는 비정형 계층이 필요할 때 명시적 계층을 만듭니다. 명시적 계층에는 단일 엔터티의 멤버가 포함됩니다.  
  
 명시적 계층을 만든 후에는 **탐색기** 기능 영역에서 해당 계층에 멤버를 추가할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
-   명시적 계층 및 컬렉션에 엔터티가 사용되어야 합니다. 자세한 내용은 참조 [명시적 계층 및 컬렉션에 엔터티 사용 &#40;Master Data Services&#41;](../../2014/master-data-services/enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)합니다.  
  
### <a name="to-create-an-explicit-hierarchy"></a>명시적 계층을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  명시적 계층을 만들려는 엔터티의 행을 선택합니다.  
  
5.  **선택한 엔터티 편집**을 클릭합니다.  
  
6.  에 **엔터티 편집** 페이지는 **명시적 계층** 창에서 클릭 **명시적 계층 추가**합니다.  
  
7.  에 **명시적 계층 추가** 페이지는 **명시적 계층 이름** 상자에 계층의 이름을 입력 합니다.  
  
8.  또는 **필수 계층** 확인란의 선택을 취소하여 계층을 필수가 아닌 계층으로 만듭니다. 계층 형식에 대한 자세한 내용은 [명시적 계층&#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)을 참조하세요.  
  
9. 클릭 **계층 저장**합니다.  
  
10. 에 **엔터티 편집** 페이지 **엔터티 저장**합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [통합된 멤버 만들기 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-consolidated-member-master-data-services.md)  
  
-   [계층 구조 내에서 멤버 이동 &#40;Master Data Services&#41;](../../2014/master-data-services/move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [명시적 계층 &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [명시적 캡이 포함된 파생 계층&#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [명시적 계층 이름 변경 &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  