---
description: 특성 그룹 만들기(Master Data Services)
title: 특성 그룹 만들기
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ffe84797d519961ab26e6d43fb48a5c4c2dd3e13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461845"
---
# <a name="create-an-attribute-group-master-data-services"></a>특성 그룹 만들기(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 **탐색기** 표의 개별 탭에 특성을 표시하려는 경우 특성 그룹을 만듭니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
-   하나 이상의 특성이 있어야 합니다. 자세한 내용은 [텍스트 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-an-attribute-group"></a>특성 그룹을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택 하 고 **엔터티**를 클릭 합니다.  
  
3.  **엔터티 관리** 페이지의 표에서 해당 특성 그룹을 만들려는 엔터티의 행을 선택합니다.  
  
4.  **특성 그룹**을 클릭합니다.  
  
5.  특성 관리 페이지에서 다음 작업 중 하나를 수행하고 **추가**를 클릭합니다.  
  
     리프 멤버용 특성 그룹의 경우 페이지 맨 위의 **멤버 형식** 드롭다운 목록에서 **리프** 를 선택합니다.  
  
     통합 멤버용 특성 그룹의 경우 **멤버 형식** 드롭다운 목록에서 **통합** 을 선택합니다.  
  
     컬렉션용 특성 그룹의 경우 **멤버 형식** 드롭다운 목록에서 **컬렉션** 을 선택합니다.  
  
6.  **리프 그룹**, **통합 그룹**또는 **컬렉션 그룹** 을 클릭하여 각각 리프 멤버, 통합 멤버 또는 컬렉션의 특성 그룹을 만듭니다.  
  
7.  **이름** 상자에 특성 그룹의 이름을 입력합니다. 이 이름은 **탐색기**의 탭에 표시됩니다.  
  
8.  특성을 추가하려면 **사용 가능한 특성** 상자에서 특성을 클릭하고 **추가** 화살표를 클릭합니다. 모든 특성을 추가하려면 **모두 추가** 화살표를 클릭합니다.  
  
9. **위쪽** 및 **아래쪽** 화살표를 클릭하여 왼쪽에서 오른쪽으로 정렬되는 특성 순서를 변경합니다.  
  
10. **사용 가능한 사용자** 상자에서 사용자를 클릭하고 **추가** 화살표를 클릭합니다. 모든 사용자를 추가하려면 **모두 추가** 화살표를 클릭합니다.  
  
11. **사용 가능한 그룹** 상자에서 그룹을 클릭하고 **추가** 화살표를 클릭합니다. 모든 그룹을 추가하려면 **모두 추가** 화살표를 클릭합니다.  
  
12. **저장**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [특성 그룹을 사용자에게 표시되도록 설정&#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [특성 그룹 &#40;MDS(Master Data Services)&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [특성 &#40;MDS(Master Data Services)&#41;](../master-data-services/attributes-master-data-services.md)   
 [특성 그룹 이름을 변경 &#40;MDS(Master Data Services)&#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [특성 그룹 &#40;MDS(Master Data Services) 삭제&#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)   
 [리프 권한&#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)   
   
  
  
