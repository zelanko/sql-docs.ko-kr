---
title: 계층 내에서 멤버 이동 (MDS(Master Data Services)) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 58b39d2dc660fd51d1ba21308ff056874a239731
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054087"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>계층 내에서 멤버 이동(Master Data Services)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서는 계층 내에서 멤버를 이동하여 할당된 위치나 부모를 변경할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   명시적 계층의 경우 엔터티에 대 한 **업데이트** 이상의 권한이 있어야 합니다.  
  
-   파생 계층의 경우 모델에 대 한 **업데이트** 와 계층에 사용 되는 모든 도메인 기반 특성이 있어야 합니다.  
  
### <a name="to-move-members-within-a-hierarchy"></a>계층 내에서 멤버를 이동하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
2.  **버전** 목록에서 버전을 선택합니다.  
  
3.  **탐색기**를 클릭합니다.  
  
4.  메뉴 모음에서 **계층** 을 가리키고 *hierarchy_name*를 클릭 합니다.  
  
5.  **계층 구조 창에서** 계층 구조가 트리 구조로 표시 되 면 이동할 각 멤버의 확인란을 클릭 합니다.  
  
6.  **계층** 창 맨 위에서 **잘라내기**를 클릭 합니다.  
  
7.  **계층** 창에서 멤버를 이동할 멤버의 확인란을 클릭 합니다.  
  
8.  **붙여넣기**를 클릭 합니다.  
  
    > [!NOTE]  
    >  파생 계층에서는 같은 수준으로만 멤버를 이동할 수 있습니다. 또한 멤버 정렬 순서는 변경할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services) &#40;준비 프로세스를 사용 하 여 명시적 계층 멤버를 이동&#41;](add-update-and-delete-data-master-data-services.md)   
 [파생 계층 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [명시적 계층&#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
