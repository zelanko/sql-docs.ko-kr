---
title: 특성 그룹을 사용자에게 표시되도록 설정(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 14f9ad5eb733db24f47acad192dbe89543831766
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750927"
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>특성 그룹을 사용자에게 표시되도록 설정(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성 그룹이 사용자나 그룹에 표시되도록 설정하여 **탐색기** 기능 영역의 표 위에 탭이 나타나도록 할 수 있습니다.  
  
 특성 그룹을 만들면 특성 그룹은 해당 그룹을 만든 사람을 제외한 모든 사용자로부터 자동으로 숨겨집니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
-   하나 이상의 특성 그룹이 있어야 합니다. 자세한 내용은 [특성 그룹 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)를 참조하세요.  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>특성 그룹이 사용자에게 표시되도록 설정하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **특성 그룹**을 클릭합니다.  
  
3.  **모델** 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 목록에서 엔터티를 선택합니다.  
  
5.  표시되도록 설정할 그룹 유형에 따라 더하기 기호를 클릭하여 **리프 그룹**, **통합 그룹**또는 **컬렉션 그룹**을 확장합니다.  
  
6.  더하기 기호를 클릭하여 표시되도록 설정할 그룹을 확장합니다.  
  
7.  그룹을 사용자에게 표시할지 그룹에 표시할지 여부에 따라 **사용자** 또는 **그룹**을 클릭합니다.  
  
8.  **선택한 항목 편집**을 클릭합니다.  
  
9. **사용 가능** 상자에서 사용자나 그룹을 클릭하고 **추가** 화살표를 클릭합니다. 모두 추가하려면 **모두 추가** 화살표를 클릭합니다.  
  
10. **저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [특성 그룹&#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [특성 그룹 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
