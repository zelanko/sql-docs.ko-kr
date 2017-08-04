---
title: "통합된 멤버 (Master Data Services) 만들기 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
caps.latest.revision: 12
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a50e1b7136542b4a230a461a81813e10730fba09
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-consolidated-member-master-data-services"></a>Create a Consolidated Member (Master Data Services)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 명시적 계층에 대한 부모 노드가 필요한 경우 통합 멤버를 만듭니다. 대량으로 데이터를 추가하려는 경우 준비 테이블을 대신 사용합니다. 자세한 내용은 [테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)를 참조하세요.  
  
## <a name="prerequisites"></a>필수 구성 요소  
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
  
## <a name="see-also"></a>관련 항목:  
 [명시적 계층 &#40; 만들기 Master Data services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [리프 멤버 &#40; 만들기 Master Data services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)   
 [멤버 &#40; Master Data services&#41;](../master-data-services/members-master-data-services.md)   
 [명시적 계층 &#40; Master Data services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  

