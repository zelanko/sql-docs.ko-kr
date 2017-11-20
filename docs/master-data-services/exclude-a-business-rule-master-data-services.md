---
title: "비즈니스 규칙 제외(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 6d6ae880dffcf2bf01e9a1f3444c9cc775994216
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="exclude-a-business-rule-master-data-services"></a>비즈니스 규칙 제외(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 비즈니스 규칙을 영구적으로 삭제하지는 않되 규칙에 대해 데이터 유효성을 검사하지 않으려면 규칙을 제외합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-exclude-a-business-rule"></a>비즈니스 규칙을 제외하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리**를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙** 페이지의 **모델** 드롭다운 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 드롭다운 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 드롭다운 목록에서 멤버 유형을 선택합니다.  
  
6.  표에서 제외하려는 비즈니스 규칙의 행을 선택하고 **편집**을 클릭합니다.  
  
7.  **제외됨** 확인란을 표시합니다.  
  
8.  **저장**을 클릭합니다.  
  
9. **모두 게시**를 클릭합니다.  
  
10. 확인 대화 상자에서 **확인**을 클릭합니다. **비즈니스 규칙 상태** 열의 값은 **제외됨** 이고 **제외된** 열의 값은 **예**입니다.  
  
## <a name="see-also"></a>참고 항목  
 [비즈니스 규칙 삭제&#40;Master Data Services&#41;](../master-data-services/delete-a-business-rule-master-data-services.md)   
 [비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  

