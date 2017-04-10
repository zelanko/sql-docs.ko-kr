---
title: "겹치는 모델 및 멤버 권한(Master Data Services) | Microsoft Docs"
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
  - "모델 [Master Data Services], 유효한 권한"
  - "권한 [Master Data Services], 모델 및 멤버 겹침"
  - "멤버 [Master Data Services], 유효한 권한"
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 겹치는 모델 및 멤버 권한(Master Data Services)
  멤버에 할당된 사용 권한과 모델 개체에 할당된 사용 권한이 겹칠 수 있습니다. 사용 권한이 겹치면 보다 제한적인 사용 권한이 적용됩니다.  
  
 멤버의 사용 권한이 해당 모델 개체와 다른 경우 다음 규칙이 적용됩니다.  
  
-   **거부** 는 다른 모든 사용 권한을 무시합니다.  
  
-   **관리자** 모델 수준에 대 한 권한이 다른 모든 사용 권한을 무시 되며 하위 수준에 대 한 액세스 권한이 모든 (CRUD)로 변경 됩니다.  
  
-   유효한 액세스 권한은 멤버 및 특성에 대한 권한과 일정 부분 일치합니다.  
  
     예를 들어 멤버 권한에 **만들기** 및 **업데이트**가 포함되는 경우 특성에 대한 권한은 **업데이트**입니다. 즉, 유효한 권한이 **업데이트**가 됩니다.  
  
 다음 이미지는 특성 사용 권한이 멤버 권한과 다를 경우 개별 특성 값에 적용되는 사용 권한을 보여 줍니다.  
  
 ![mds_conc_security_member_overlap_table](../master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## 예 1  
 ![mds_conc_overlap_model_1](../master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 **모델** 탭의 Product 엔터티에는 **업데이트** 권한이 할당되어 있습니다. 엔터티의 모든 특성은 해당 사용 권한을 상속합니다.  
  
 **계층 멤버** 탭의 파생 계층에 있는 Mountain Bikes 하위 범주 노드에는 **업데이트** 권한이 할당되어 있습니다.  
  
 결과: **탐색기**에서 사용자에게는 Mountain Bikes 노드에 있는 모든 멤버의 모든 특성 값에 대한 **업데이트** 권한이 있습니다. 모든 다른 멤버와 특성은 숨겨집니다.  
  
 ![mds_conc_overlap_model_example_1](../master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## 예 2  
 ![mds_conc_overlap_model_2](../master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 **모델** 탭의 하위 범주 특성에는 **업데이트** 권한이 할당되어 있습니다.  
  
 **계층 멤버** 탭의 파생 계층에 있는 Mountain Bikes 하위 범주 노드에는 **읽기** 권한이 명시적으로 할당됩니다.  
  
 결과: **탐색기**에서 사용자에게는 Mountain Bikes 노드에 있는 멤버의 하위 범주 특성 값에 대한 **읽기** 권한이 있습니다. 모든 다른 멤버와 특성은 숨겨집니다.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## 예 3  
 ![mds_conc_overlap_model_3](../master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 **모델** 탭의 하위 범주 특성에는 **읽기** 권한이 할당되어 있습니다.  
  
 **계층 멤버** 탭의 파생 계층에 있는 Mountain Bikes 하위 범주 노드에는 **업데이트** 권한이 명시적으로 할당됩니다.  
  
 결과: **탐색기**에서 사용자에게는 특성 값에 대한 **읽기** 권한이 있습니다. 모든 다른 멤버와 특성은 숨겨집니다.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## 참고 항목  
 [사용 권한이 결정 됩니다 어떻게 & #40입니다. Master Data Services & #41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [겹치는 사용자 및 그룹 권한 & #40입니다. Master Data Services & #41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  