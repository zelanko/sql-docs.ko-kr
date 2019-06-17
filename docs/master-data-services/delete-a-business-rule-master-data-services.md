---
title: 비즈니스 규칙 삭제(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting business rules [Master Data Services]
- business rules [Master Data Services], deleting
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8dee36c433cc1fec26bd66bf3498e505fd3edc9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65487757"
---
# <a name="delete-a-business-rule-master-data-services"></a>비즈니스 규칙 삭제(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 비즈니스 규칙이 더 이상 필요하지 않으면 삭제할 수 있습니다.  
  
> [!NOTE]  
>  비즈니스 규칙을 삭제하지 않고 제외하면 비즈니스 규칙에 대해 데이터 유효성을 검사하지 않을 수 있습니다. 자세한 내용은 [비즈니스 규칙 제외&#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md)를 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-delete-a-business-rule"></a>비즈니스 규칙을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙** 페이지의 **모델** 드롭다운 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 드롭다운 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형** 드롭다운 목록에서 비즈니스 규칙을 적용할 멤버 유형을 선택합니다.  
  
6.  표 형태에서 삭제할 비즈니스 규칙 행을 클릭합니다.  
  
7.  **삭제**를 클릭합니다.  
  
8.  확인 대화 상자에서 **확인**을 클릭합니다. **비즈니스 규칙 상태** 열의 값은 **삭제 보류 중**입니다.  
  
9. **모두 게시**를 클릭합니다.  
  
10. 확인 대화 상자에서 **확인**을 클릭합니다. 삭제된 비즈니스 규칙은 더 이상 눈금에 표시되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [비즈니스 규칙 제외&#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md)   
 [비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
