---
title: 계층 멤버 권한 할당(Master Data Services) | Microsoft Docs
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
- permissions [Master Data Services], assigning member permissions
- members [Master Data Services], assigning permissions
ms.assetid: e1b8b46a-7cd1-4a7d-9345-dd7df081e145
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 79ed00e101c252cff63e8978ef55a27e6c5c8258
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172916"
---
# <a name="assign-hierarchy-member-permissions-master-data-services"></a>계층 멤버 권한 할당(Master Data Services)
  계층 멤버에 사용 권한을 할당하여 사용자나 그룹에 **의** 탐색기 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]기능 영역에서 데이터를 볼 수 있는 액세스 권한을 부여합니다.  
  
 계층 멤버 권한은 선택 사항으로서 필수 모델 개체 사용 권한을 보다 세부적으로 지정합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-assign-hierarchy-member-permissions"></a>계층 멤버 권한을 할당하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **사용자 및 그룹 권한**을 클릭합니다.  
  
2.  **사용자** 또는 **그룹** 페이지에서 편집하려는 사용자나 그룹의 행을 선택합니다.  
  
3.  **선택한 사용자 편집**을 클릭합니다.  
  
4.  **계층 멤버** 탭을 클릭합니다.  
  
5.  **모델** 목록에서 모델을 선택합니다.  
  
6.  **버전** 목록에서 버전을 선택합니다.  
  
7.  **계층** 목록에서 계층을 선택합니다.  
  
8.  **편집**을 클릭합니다.  
  
9. 트리를 확장하고 사용 권한을 할당할 계층 노드를 클릭합니다.  
  
10. 메뉴에서 선택 **읽기 전용**, **업데이트**, 또는 **Deny**합니다.  
  
11. **저장**을 클릭합니다.  
  
    > [!NOTE]  
    >  계층 멤버 권한은 즉시 적용되지 않습니다. 자세한 내용은 [멤버 권한 즉시 적용&#40;Master Data Services&#41;](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [계층 멤버 권한 삭제 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-hierarchy-member-permissions-master-data-services.md)   
 [모델 개체 사용 권한 할당 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [계층 멤버 권한 &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  