---
title: 숫자 특성 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating number attributes
- creating number attributes [Master Data Services]
ms.assetid: c0dbb6d8-ba78-485a-a40d-6d5cb7e75d0a
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: adc2a5156c84545c90a9ae904749f96a729c251a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794985"
---
# <a name="create-a-numeric-attribute-master-data-services"></a>숫자 특성 만들기(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 사용자가 숫자를 특성 값으로 입력할 수 있도록 하려면 숫자 특성을 만듭니다.  
  
> [!NOTE]  
>  숫자 특성에는 제약이 있습니다. 자세한 내용은 [특성&#40;Master Data Services&#41;](attributes-master-data-services.md)을 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   해당 특성을 만들 엔터티가 있어야 합니다. 자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-a-numeric-attribute"></a>숫자 특성을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
5.  **선택한 엔터티 편집**을 클릭합니다.  
  
6.  **엔터티 편집** 페이지에서  
  
    -   리프 멤버에 대한 특성일 경우 **리프 멤버 특성** 창에서 **리프 특성 추가**를 클릭합니다.  
  
    -   통합 멤버에 대한 특성일 경우 **통합 멤버 특성** 창에서 **통합 특성 추가**를 클릭합니다.  
  
    -   컬렉션에 대한 특성일 경우 **컬렉션 특성** 창에서 **컬렉션 특성 추가**를 클릭합니다.  
  
7.  **특성 추가** 페이지에서 **자유 형식** 옵션을 선택합니다.  
  
8.  **이름** 상자에 특성의 이름을 입력합니다. 특성 이름으로 사용하지 않아야 하는 단어의 목록을 보려면 [예약어&#40;Master Data Services&#41;](../../2014/master-data-services/reserved-words-master-data-services.md)를 참조하세요.  
  
9. **탐색기** 표에 표시할 특성 열의 너비를 **표시 픽셀 폭** 상자에 입력합니다.  
  
10. **데이터 형식** 목록에서 **숫자**를 선택합니다.  
  
11. **10진수** 상자에 10진수 다음에 입력할 수 있는 숫자 개수를 지정합니다.  
  
12. **입력 마스크** 목록에서 음수의 형식을 선택 합니다.  
  
13. 또는 특성 그룹의 변경 내용을 추적하려면 **변경 내용 추적 설정** 을 선택합니다. 자세한 내용은 [변경 내용 추적 그룹에 특성 추가&#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) 를 참조하세요.  
  
14. **특성 저장**을 클릭합니다.  
  
15. **엔터티 유지 관리** 페이지에서 **엔터티 저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [특성&#40;Master Data Services&#41;](attributes-master-data-services.md)   
 [특성 이름 변경 &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [도메인 기반 특성 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [파일 특성 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
