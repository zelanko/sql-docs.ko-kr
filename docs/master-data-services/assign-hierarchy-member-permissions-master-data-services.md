---
title: "계층 멤버 권한 (Master Data Services) 할당 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Master Data Services], assigning member permissions
- members [Master Data Services], assigning permissions
ms.assetid: e1b8b46a-7cd1-4a7d-9345-dd7df081e145
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f7a7e6cafe48506446396b83200d4d2343aa7949
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="assign-hierarchy-member-permissions-master-data-services"></a>계층 멤버 권한 할당(Master Data Services)
  계층 멤버에 사용 권한을 할당하여 사용자나 그룹에 **의** 탐색기 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]기능 영역에서 데이터를 볼 수 있는 액세스 권한을 부여합니다.  
  
 계층 멤버 권한은 선택 사항으로서 필수 모델 개체 사용 권한을 보다 세부적으로 지정합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
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
  
10. 메뉴에서 **만들기**, **읽기, 업데이트** 및 **삭제** 권한의 조합을 선택하거나 사용 권한을 **거부** 합니다.  
  
11. **저장**을 클릭합니다.  
  
    > [!NOTE]  
    >  계층 멤버 권한은 즉시 적용되지 않습니다. 자세한 내용은 [멤버 권한 즉시 적용&#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [계층 멤버 권한 삭제&#40;Master Data Services&#41;](../master-data-services/delete-hierarchy-member-permissions-master-data-services.md)   
 [모델 개체 사용 권한 &#40; 할당 Master Data services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [계층 멤버 권한 &#40; Master Data services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
