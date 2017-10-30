---
title: "특성 그룹을 사용자에게 표시되도록 설정(Master Data Services) | Microsoft Docs"
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
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: e3922c3ad81de37e73f08bd840def40146c8bf12
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>특성 그룹을 사용자에게 표시되도록 설정(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성 그룹이 사용자나 그룹에 표시되도록 설정하여 **탐색기** 기능 영역의 표 위에 탭이 나타나도록 할 수 있습니다.  
  
 특성 그룹을 만들면 특성 그룹은 해당 그룹을 만든 사람을 제외한 모든 사용자로부터 자동으로 숨겨집니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   하나 이상의 특성 그룹이 있어야 합니다. 자세한 내용은 [특성 그룹 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)를 참조하세요.  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>특성 그룹이 사용자에게 표시되도록 설정하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지의 표에서 특성 그룹을 편집하려는 엔터티에 대한 행을 선택합니다.  
  
4.  **특성 그룹**을 클릭합니다.  
  
5.  **특성 그룹 관리** 페이지에 있는 **멤버 유형** 드롭다운 목록 상자에서 멤버 유형을 선택하여 표시하려는 그룹의 형식에 따라 **리프**, **통합** 또는 **컬렉션**을 확장합니다.  
  
6.  표에서 편집할 특성 그룹을 선택하고 **편집**을 클릭합니다.  
  
7.  **사용 가능** 상자에서 사용자나 그룹을 클릭하고 **추가** 화살표를 클릭합니다. 모두 추가하려면 **모두 추가** 화살표를 클릭합니다.  
  
8.  **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [특성 그룹&#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [특성 그룹 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  

