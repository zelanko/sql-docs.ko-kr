---
title: "특성 이름 및 데이터 형식 변경(Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [Master Data Services], changing name
ms.assetid: d348f238-f59d-41c7-ad20-3ccd55bfd9e5
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: erikre
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: b595042d299890b023edbc604ea0d87bedd0847b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="change-an-attribute-name-and-data-type-master-data-services"></a>특성 이름 및 데이터 형식 변경(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성의 이름을 변경할 수 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-change-an-attribute-name-and-type"></a>특성 이름 및 형식을 변경하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지에서 해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
4.  **특성**을 클릭합니다.  
  
5.  **특성 관리** 페이지에서 다음 작업 중 하나를 수행합니다.  
  
    -   리프 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **리프** 를 선택합니다.  
  
    -   통합 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **통합** 을 선택합니다.  
  
    -   컬렉션용 특성의 경우 **멤버 형식** 목록 상자에서 **컬렉션** 을 선택합니다.  
  
6.  편집할 특성 행을 선택하고 **편집**을 클릭합니다.  
  
7.  **이름** 상자에 특성의 업데이트된 이름을 입력합니다. 특성 이름으로 사용하지 않아야 하는 단어의 목록을 보려면 [예약어&#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)를 참조하세요.  
  
8.  **특성 유형** 목록에서 다른 유형을 선택합니다.  
  
9. **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [텍스트 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [특성 삭제&#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)   
 [특성&#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  

