---
title: "멤버 또는 컬렉션 다시 활성화(Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "컬렉션 [Master Data Services], 다시 활성화"
  - "통합 멤버 [Master Data Services], 다시 활성화"
  - "멤버 다시 활성화 [Master Data Services]"
  - "멤버 [Master Data Services], 다시 활성화"
  - "컬렉션 다시 활성화 [Master Data Services]"
  - "리프 멤버 [Master Data Services], 다시 활성화"
ms.assetid: bb4884c0-3658-4763-92d1-636804278b1c
caps.latest.revision: 11
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 11
---
# 멤버 또는 컬렉션 다시 활성화(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 다음과 같은 멤버를 다시 활성화할 수 있습니다.  
  
-   준비 프로세스로 비활성화된 멤버  
  
-   MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]에서 삭제된 멤버  
  
-   [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램에서 삭제된 멤버  
  
 멤버를 다시 활성화하면 계층 및 컬렉션에서 해당 특성 및 멤버 자격이 복원됩니다.  
  
 또한 컬렉션을 다시 활성화할 수 있습니다. 컬렉션을 다시 활성화하면 컬렉션의 특성과 컬렉션에 속하는 멤버가 복원됩니다.  
  
 컬렉션이나 멤버를 다시 활성화하면 이전 트랜잭션이 모두 복원됩니다.  
  
## 필수 구성 요소  
 이 절차를 수행하려면  
  
-   [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서는 **버전 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### 멤버 또는 컬렉션을 다시 활성화하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지에서 **버전 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **트랜잭션**을 클릭합니다.  
  
3.  **트랜잭션** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **버전** 목록에서 버전을 선택합니다.  
  
5.  **트랜잭션** 창에서 다시 활성화할 멤버 또는 컬렉션의 행을 클릭합니다. 이 행의 **이전 값** 열에 **활성**이 표시되고 **새 값** 열에 **비활성화됨**이 표시됩니다.  
  
6.  **트랜잭션 되돌리기**를 클릭합니다.  
  
7.  확인 대화 상자에서 **확인**을 클릭합니다. 새 트랜잭션이 추가되고 **새 값** 열에 **활성** 이 표시됩니다.  
  
## 참고 항목  
 [멤버 또는 컬렉션 삭제&#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)   
 [멤버&#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [컬렉션&#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  