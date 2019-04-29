---
title: 통합 멤버 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cf154f3437ed22be932fa37470f59049aea09850
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925336"
---
# <a name="create-a-consolidated-member-master-data-services"></a>통합 멤버 만들기(Master Data Services)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 명시적 계층에 대한 부모 노드가 필요한 경우 통합 멤버를 만듭니다. 통합된 멤버는 고유한 특성을 가질 수 있습니다. 이러한 특성은 그룹화에 사용됩니다. 다음 예제와 같이 계정을 포함하는 계정 그룹에 통합된 멤버를 사용할 수 있습니다.  
  
 ![MDS 통합 멤버](../../2014/master-data-services/media/mds-consolidated-members.png "MDS 통합 멤버")  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   멤버를 추가할 엔터티의 통합 모델 개체에 대한 **업데이트** 이상의 권한이 있어야 합니다.  
  
### <a name="to-create-a-consolidated-member"></a>통합 멤버를 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
2.  **버전** 목록에서 버전을 선택합니다.  
  
3.  **탐색기**를 클릭합니다.  
  
4.  메뉴 모음에서 **계층** 을 가리키고 통합 멤버를 추가하려는 계층의 이름을 클릭합니다.  
  
5.  표 위에 있는 **통합 멤버** 또는 **계층의 모든 통합 멤버** 옵션을 선택합니다.  
  
6.  **추가**를 클릭합니다.  
  
7.  오른쪽 창의 필드에 입력합니다.  
  
8.  (선택 사항) **주석** 상자에 멤버를 추가한 이유에 대한 주석을 입력합니다. 멤버에 액세스할 수 있는 모든 사용자가 주석을 볼 수 있습니다.  
  
9. **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [계층 내에서 멤버 이동 &#40;Master Data Services&#41;](move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [명시적 계층 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [리프 멤버 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)   
 [멤버 로드 또는 업데이트 Master Data Services에서 준비 프로세스를 사용 하 여](add-update-and-delete-data-master-data-services.md)   
 [멤버&#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [명시적 계층&#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
