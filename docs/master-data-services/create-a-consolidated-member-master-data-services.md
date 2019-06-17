---
title: 통합 멤버 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5168e98297b28f7dce2e07e639cb64f9c62899c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481096"
---
# <a name="create-a-consolidated-member-master-data-services"></a>통합 멤버 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 명시적 계층에 대한 부모 노드가 필요한 경우 통합 멤버를 만듭니다. 대량으로 데이터를 추가하려는 경우 준비 테이블을 대신 사용합니다. 자세한 내용은 [테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)를 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   멤버를 추가할 엔터티의 통합 모델 개체에 대한 **업데이트** 이상의 권한 및 엔터티 아래에 통합 형식에 대한 **만들기 권한** 이 있어야 합니다.  
  
### <a name="to-create-a-consolidated-member"></a>통합 멤버를 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
2.  **버전** 목록에서 버전을 선택합니다.  
  
3.  **탐색기**를 클릭합니다.  
  
4.  메뉴 모음에서 **계층** 을 가리키고 통합 멤버를 추가하려는 계층의 이름을 클릭합니다.  
  
5.  표 위에 있는 **통합 멤버** 또는 **계층의 모든 통합 멤버** 옵션을 선택합니다.  
  
6.  왼쪽 창에서 통합 멤버를 만들려는 루트 노드 또는 통합 멤버를 선택합니다.  
  
7.  **추가**를 클릭합니다.  
  
8.  오른쪽 창의 필드에 입력합니다.  
  
9. (선택 사항) **주석** 상자에 멤버를 추가한 이유에 대한 주석을 입력합니다. 멤버에 액세스할 수 있는 모든 사용자가 주석을 볼 수 있습니다.  
  
10. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [명시적 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [리프 멤버 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)   
 [멤버&#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
