---
title: 계층 (Master Data Services) 내에서 멤버 이동 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d5e8bf5a041458614422b3c89666ea3ffc9f5a86
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092650"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>계층 내에서 멤버 이동(Master Data Services)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서는 계층 내에서 멤버를 이동하여 할당된 위치나 부모를 변경할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   명시적 계층에 대 한 최소 있어야 **업데이트** 엔터티 수 있는 권한이 있습니다.  
  
-   파생된 계층에 대 한 최소 있어야 **업데이트** 모델을 계층 구조에서 사용 되는 모든 도메인 기반 특성 수입니다.  
  
### <a name="to-move-members-within-a-hierarchy"></a>계층 내에서 멤버를 이동하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
2.  **버전** 목록에서 버전을 선택합니다.  
  
3.  **탐색기**를 클릭합니다.  
  
4.  메뉴 모음에서 **계층** 클릭 *hierarchy_name*합니다.  
  
5.  에 **계층** 여기서 계층 트리 구조에 표시 되 면 창에서 이동할 각 멤버에 대 한 확인란을 클릭 합니다.  
  
6.  맨 위에 있는 **계층** 창에서 클릭 **잘라내기**합니다.  
  
7.  에 **계층** 창에서 멤버를 이동할 멤버에 대 한 확인란을 클릭 합니다.  
  
8.  클릭 **붙여넣기**합니다.  
  
    > [!NOTE]  
    >  파생 계층에서는 같은 수준으로만 멤버를 이동할 수 있습니다. 또한 멤버 정렬 순서는 변경할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [준비 프로세스를 사용 하 여 명시적 계층 멤버 이동 &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [파생 계층 &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [명시적 계층 &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  