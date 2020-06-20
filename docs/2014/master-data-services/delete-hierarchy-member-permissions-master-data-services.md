---
title: 계층 멤버 권한 삭제(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1562bc5d71bdf873c7be1f01a1dbf48fe85c05a5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950551"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>계층 멤버 권한 삭제(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델 개체 사용 권한을 삭제하여 모든 할당을 제거합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](administrators-master-data-services.md)를 참조 하세요.  
  
### <a name="to-delete-hierarchy-member-permissions"></a>계층 멤버 권한을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **사용자 및 그룹 권한**을 클릭합니다.  
  
2.  **사용자** 또는 **그룹** 페이지에서 편집하려는 사용자나 그룹의 행을 선택합니다.  
  
3.  **선택한 사용자 편집**을 클릭합니다.  
  
4.  **계층 멤버** 탭을 클릭합니다.  
  
5.  **모델** 목록에서 모델을 선택합니다.  
  
6.  **버전** 목록에서 버전을 선택합니다.  
  
7.  **계층 멤버 권한 요약** 창에서 삭제 하려는 사용 권한의 행을 선택 합니다.  
  
8.  **선택한 사용 권한 삭제**를 클릭 합니다.  
  
    > [!NOTE]  
    >  사용 권한이 그룹에서 상속되는 경우에는 사용자로부터 사용 권한을 제거할 수 없습니다. 대신 그룹에서 사용 권한을 제거해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [계층 멤버 권한 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [계층 멤버 권한 할당&#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
