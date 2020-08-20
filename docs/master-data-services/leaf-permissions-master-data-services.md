---
description: 리프 권한(Master Data Services)
title: 리프 권한
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], permissions
- members [Master Data Services], leaf member permissions
- permissions [Master Data Services], leaf members
- leaf members [Master Data Services], attribute permissions
- attributes [Master Data Services], leaf member attribute permissions
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a50723727690307492d3d16cb3671e762dec401f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461769"
---
# <a name="leaf-permissions-master-data-services"></a>리프 권한(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  리프 권한은 엔터티의 모든 리프 멤버에 대한 특성 값에 적용됩니다.  
  
 명시적 계층이 설정되지 않은 엔터티의 경우 **리프** 에 사용 권한을 할당하는 것은 엔터티에 사용 권한을 할당하는 것과 같습니다.  
  
 **참고:**  
  
-   리프 권한은 사용자 인터페이스의 **탐색기** 기능 영역에만 적용됩니다.  
  
-   **이름** 및 **코드** 특성에 할당된 사용 권한은 적용되지 않습니다.  
  
|사용 권한|설명|  
|----------------|-----------------|  
|**읽기**|사용자는 리프 멤버, 특성을 읽을 수 있습니다.|  
|**만들기**|사용자는 리프 멤버를 만들고 만드는 동안 특성 값을 할당할 수 있습니다.|  
|**Update**|사용자는 리프 멤버 및 특성을 업데이트할 수 있습니다.|  
|**Delete**|사용자는 리프 멤버를 삭제할 수 있습니다.|  
|**거부**|리프 멤버에 대한 모든 액세스를 거부 합니다.|  
  
 읽기, 만들기, 업데이트 및 삭제 권한을 결합할 수 있습니다. 만들기, 업데이트 및 삭제가 할당될 때 읽기 권한은 자동으로 할당됩니다.  
  
## <a name="attribute-permissions"></a>특성 사용 권한  
 특성 사용 권한은 특정 엔터티의 특성 값에 적용됩니다. 특성 사용 권한만 있는 사용자는 멤버를 추가하거나 제거할 수 없습니다.  
  
|사용 권한|설명|  
|----------------|-----------------|  
|**읽기**|사용자는 특성을 읽을 수 있습니다.|  
|**만들기**|사용자는 멤버를 만들 때 값을 할당할 수 있습니다.|  
|**Update**|사용자는 특성을 업데이트할 수 있습니다.|  
|**Delete**|아무런 영향이 없습니다.|  
|**거부**|특성이 표시되지 않습니다.<br /><br /> 참고: 이름 및 코드 특성에 대한 액세스를 명시적으로 거부할 수 없습니다.|  
  
### <a name="example"></a>예제  
 Product 엔터티에 대해 Subcategory 특성에 **업데이트** 권한을 할당합니다. 모든 다른 특성에 대한 사용 권한은 거부합니다.  
  
|Name|코드|Subcategory(업데이트)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5} 산악 자전거|  
|Mountain-100|BK-M201|{5} 산악 자전거|  
  
 **탐색기**에서 Subcategory 열의 특성 값을 업데이트할 수 있습니다. 특성에 대한 사용 권한이 없는 경우에는 해당 특성이 표시되지 않습니다.  
  
> [!NOTE]  
>  이 예에서 Subcategory는 SubcategoryList 엔터티를 기반으로 하는 도메인 기반 특성입니다. Mountain-100에 대해 다른 Subcategory를 선택할 수 있지만 SubcategoryList 엔터티에서 멤버를 추가하거나 삭제할 수는 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
    
 [모델 개체 사용 권한 &#40;MDS(Master Data Services)&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [멤버가 MDS(Master Data Services)를 &#40;&#41;](../master-data-services/members-master-data-services.md)   
 [특성&#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
