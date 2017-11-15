---
title: "계층 멤버 권한 삭제(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
caps.latest.revision: "6"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fd240063574b189a7cb0efcc56b2699a92d02a69
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>계층 멤버 권한 삭제(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델 개체 사용 권한을 삭제하여 모든 할당을 제거합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-delete-hierarchy-member-permissions"></a>계층 멤버 권한을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **사용자 및 그룹 권한**을 클릭합니다.  
  
2.  **사용자** 또는 **그룹** 페이지에서 편집하려는 사용자나 그룹의 행을 선택합니다.  
  
3.  **선택한 사용자 편집**을 클릭합니다.  
  
4.  **계층 멤버** 탭을 클릭합니다.  
  
5.  **모델** 목록에서 모델을 선택합니다.  
  
6.  **버전** 목록에서 버전을 선택합니다.  
  
7.  **편집**을 클릭합니다.  
  
8.  **계층 멤버 권한** 패널에서 사용 권한이 있는 트리 노드를 찾습니다.  
  
9. 트리 노드를 클릭하고 상황에 맞는 메뉴에서 **없음** 을 클릭합니다.  
  
    > [!NOTE]  
    >  사용 권한이 그룹에서 상속되는 경우에는 사용자로부터 사용 권한을 제거할 수 없습니다. 대신 그룹에서 사용 권한을 제거해야 합니다.  
  
10. **저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [계층 멤버 권한&#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [계층 멤버 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
