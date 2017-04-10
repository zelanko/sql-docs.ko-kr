---
title: "겹치는 사용자 및 그룹 권한(Master Data Services) | Microsoft Docs"
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
  - "사용자 [Master Data Services], 권한 확인"
  - "권한 [Master Data Services], 사용자 및 그룹 겹침"
  - "그룹 [Master Data Services], 권한 확인"
ms.assetid: 31c3cf7d-17d4-4474-b6a7-ffcb9fc45b37
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 겹치는 사용자 및 그룹 권한(Master Data Services)
  사용자의 사용 권한은 다음 요소에 따라 결정됩니다.  
  
-   그룹 멤버 자격의 사용 권한  
  
-   사용자에게 명시적으로 할당된 사용 권한  
  
 사용자가 여러 그룹의 멤버이며 이러한 그룹에 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]액세스 권한이 있는 경우 다음 규칙이 적용됩니다.  
  
-   **거부** 는 다른 모든 사용 권한을 무시합니다. 그룹 중 하나에서 개체 권한이 **거부** 이면 유효 권한은 거부입니다.  
  
-   액세스 권한은 그룹 내 모든 유효 권한의 합집합입니다. 개체 권한이 한 그룹에서는 **만들기** 이고 다른 그룹에서는 **업데이트** 인 경우 유효 권한은 **만들기** 및 **업데이트**입니다.  
  
 이러한 규칙은 **모델** 탭과 **계층 멤버** 탭 모두에 적용됩니다. 각 탭의 사용 권한이 확인된 후 결합됩니다. 자세한 내용은 [사용 권한이 결정되는 방식&#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)을 참조하세요.  
  
> [!NOTE]  
>  겹치는 사용자 및 그룹 권한은 사용자 인터페이스에서 확인할 수 있습니다. **모델** 탭과 **계층 멤버** 탭 둘 다에 **유효**를 선택하여 유효 사용 권한을 볼 수 있는 드롭다운 목록이 있습니다.  
  
## 예제 1  
 ![mds_conc_user_group_ex_1](../master-data-services/media/mds-conc-user-group-ex-1.gif "mds_conc_user_group_ex_1")  
  
 사용자가 그룹 1 및 그룹 2에 속합니다.  
  
 사용자에게 Product 엔터티에 대한 **읽기** 권한이 있습니다.  
  
 그룹 1은 Product 엔터티에 대한 **업데이트** 권한을 가지고 있습니다.  
  
 그룹 2에 Product 엔터티에 대한 **읽기** 권한이 있습니다.  
  
 결과: Product 엔터티에 대한 사용자의 유효 권한은 **업데이트** 입니다.  
  
## 예제 2  
 ![mds_conc_user_group_ex_2](../master-data-services/media/mds-conc-user-group-ex-2.gif "mds_conc_user_group_ex_2")  
  
 사용자가 그룹 1 및 그룹 2에 속합니다.  
  
 사용자에게 Product 엔터티에 대한 **읽기** 권한이 있습니다.  
  
 그룹 1은 Product 엔터티에 대한 **업데이트** 권한을 가지고 있습니다.  
  
 그룹 2는 Product 엔터티에 대한 **거부** 권한을 가지고 있습니다.  
  
 결과: Product 엔터티에 대한 사용자의 유효 권한은 **거부** 입니다.  
  
## 예 3  
 ![mds_conc_user_group_ex_3](../master-data-services/media/mds-conc-user-group-ex-3.gif "mds_conc_user_group_ex_3")  
  
 사용자가 그룹 1 및 그룹 2에 속합니다.  
  
 사용자가 계층 노드의 멤버 그룹에 대한 **업데이트** 권한을 가지고 있습니다.  
  
 그룹 1에 계층 노드의 멤버 그룹에 대한 **읽기** 권한이 있습니다.  
  
 그룹 2에 계층 노드의 멤버 그룹에 대한 **읽기** 권한이 있습니다.  
  
 결과: 멤버에 대한 사용자의 유효 권한은 **업데이트** 입니다.  
  
## 참고 항목  
 [사용 권한이 결정되는 방식&#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [겹치는 모델 및 멤버 권한&#40;Master Data Services&#41;](../master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  