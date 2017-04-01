---
title: "모델 개체 사용 권한 할당(Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "모델 [Master Data Services], 개체 사용 권한 할당"
  - "사용 권한 [Master Data Services], 모델 개체 사용 권한 할당"
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 모델 개체 사용 권한 할당(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 **의** 탐색기 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]기능 영역에 있는 데이터에 대해 사용자 또는 그룹 액세스 권한을 부여해야 하거나 사용자나 그룹을 관리자로 지정해야 할 경우 모델 개체에 사용 권한을 할당합니다.  
  
> [!NOTE]  
>  모델에 사용 권한을 할당하면 다른 모든 모델에 대한 사용 권한이 암시적으로 거부됩니다. 모델 개체 사용 권한을 할당하지 않으면 사용자나 그룹이 **탐색기**에서 데이터에 액세스할 수 없습니다.  
  
## 필수 구성 요소  
 이 절차를 수행하려면  
  
-   **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### 모델 개체 사용 권한을 할당하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **사용자 및 그룹 권한**을 클릭합니다.  
  
2.  **사용자** 또는 **그룹** 페이지에서 편집하려는 사용자나 그룹의 행을 선택합니다.  
  
3.  **선택한 사용자 편집**을 클릭합니다.  
  
4.  **모델** 탭을 클릭합니다.  
  
5.  또는 **모델** 목록에서 모델을 선택합니다.  
  
6.  **편집**을 클릭합니다.  
  
7.  트리를 확장하고 사용 권한을 할당하려는 모델 개체를 클릭합니다.  
  
8.  메뉴에서 읽기, 만들기, 업데이트 및 삭제 또는 거부의 조합을 선택합니다.  
  
9. 사용자 모델 관리자를 만들어야 하는 경우 최상위 모델 수준에서 **Admin** 을 선택합니다.  
  
10. **저장**을 클릭합니다.  
  
## 다음 단계  
  
-   (옵션) [계층 멤버 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## 참고 항목  
 [모델 개체 사용 권한 삭제&#40;Master Data Services&#41;](../master-data-services/delete-model-object-permissions-master-data-services.md)   
 [모델 개체 권한&#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [모델 관리자 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)  
  
  