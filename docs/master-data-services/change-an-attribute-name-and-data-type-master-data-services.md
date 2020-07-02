---
title: 특성 이름 및 데이터 형식 변경
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], changing name
ms.assetid: d348f238-f59d-41c7-ad20-3ccd55bfd9e5
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: cb7d82f63f41baa88523f97e45a65635e1d49486
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813467"
---
# <a name="change-an-attribute-name-and-data-type-master-data-services"></a>특성 이름 및 데이터 형식 변경(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성의 이름을 변경할 수 있습니다.  
  
## <a name="prerequisites"></a>전제 조건  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
### <a name="to-change-an-attribute-name-and-type"></a>특성 이름 및 형식을 변경하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택 하 고 **엔터티**를 클릭 합니다.  
  
3.  **엔터티 관리** 페이지에서 해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
4.  **특성**을 클릭합니다.  
  
5.  **특성 관리** 페이지에서 다음 작업 중 하나를 수행합니다.  
  
    -   리프 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **리프** 를 선택합니다.  
  
    -   통합 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **통합** 을 선택합니다.  
  
    -   컬렉션용 특성의 경우 **멤버 형식** 목록 상자에서 **컬렉션** 을 선택합니다.  
  
6.  편집할 특성 행을 선택하고 **편집**을 클릭합니다.  
  
7.  **이름** 상자에 특성의 업데이트된 이름을 입력합니다. 특성 이름으로 사용 하지 않아야 하는 단어의 목록을 보려면 [예약어 &#40;MDS(Master Data Services)&#41;](../master-data-services/reserved-words-master-data-services.md)를 참조 하세요.  
  
8.  **특성 유형** 목록에서 다른 유형을 선택합니다.  
  
9. **Save**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [텍스트 특성 &#40;MDS(Master Data Services)를 만듭니다&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [MDS(Master Data Services) &#40;특성을 삭제&#41;](../master-data-services/delete-an-attribute-master-data-services.md)   
 [특성&#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
