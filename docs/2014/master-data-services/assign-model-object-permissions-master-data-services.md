---
title: 모델 개체 사용 권한 할당(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], assigning object permissions
- permissions [Master Data Services], assigning model object permissions
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7924ef8effaa3c39802fd53216814b065ff81ef4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972213"
---
# <a name="assign-model-object-permissions-master-data-services"></a>모델 개체 사용 권한 할당(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 **의** 탐색기 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]기능 영역에 있는 데이터에 대해 사용자 또는 그룹 액세스 권한을 부여해야 하거나 사용자나 그룹을 관리자로 지정해야 할 경우 모델 개체에 사용 권한을 할당합니다.  
  
> [!NOTE]  
>  모델에 사용 권한을 할당하면 다른 모든 모델에 대한 사용 권한이 암시적으로 거부됩니다. 모델 개체 사용 권한을 할당하지 않으면 사용자나 그룹이 **탐색기**에서 데이터에 액세스할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](administrators-master-data-services.md)를 참조 하세요.  
  
### <a name="to-assign-model-object-permissions"></a>모델 개체 사용 권한을 할당하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **사용자 및 그룹 권한**을 클릭합니다.  
  
2.  **사용자** 또는 **그룹** 페이지에서 편집하려는 사용자나 그룹의 행을 선택합니다.  
  
3.  **선택한 사용자 편집**을 클릭합니다.  
  
4.  **모델** 탭을 클릭합니다.  
  
5.  또는 **모델** 목록에서 모델을 선택합니다.  
  
6.  **편집**을 클릭합니다.  
  
7.  트리를 확장하고 사용 권한을 할당하려는 모델 개체를 클릭합니다.  
  
8.  메뉴에서 **읽기**전용, **업데이트**또는 **거부**를 선택 합니다.  
  
9. **저장**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   (옵션) [계층 멤버 권한 할당&#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [모델 개체 사용 권한 삭제 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/delete-model-object-permissions-master-data-services.md)   
 [모델 개체 사용 권한 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [모델 관리자 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-administrator-master-data-services.md)  
  
  
