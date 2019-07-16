---
title: 모델 권한(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 027240f161ec2853aa2d40a7b4792ccea82c7e64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000028"
---
# <a name="model-permissions-master-data-services"></a>모델 권한(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  모델 권한은 모델 내의 모든 엔터티, 파생 계층, 명시적 계층 및 컬렉션에 적용됩니다. 모델에 할당된 사용 권한은 개별 개체에 대해 재정의할 수 있습니다.  
  
> [!NOTE]  
>  사용자가 모델 관리자인 경우 사용자 인터페이스의 모든 기능 영역에 모델이 표시됩니다. 그렇지 않은 경우에는 **탐색기** 기능 영역에만 모델이 표시됩니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
|사용 권한|설명|  
|----------------|-----------------|  
|**읽기**|사용자는 멤버, 특성, 계층 멤버 자격 또는 컬렉션 멤버를 읽을 수 있습니다.|  
|**만들기**|사용자는 멤버를 만들고 만드는 동안 특성 값을 할당할 수 있습니다.|  
|**Update 함수**|사용자는 멤버, 특성, 계층 멤버 자격 또는 컬렉션 멤버를 업데이트할 수 있습니다.|  
|**Delete**|사용자는 멤버를 삭제할 수 있습니다.|  
|**거부**|모델에 대한 모든 액세스를 거부 합니다.|  
|**Admin**|모델에 대한 관리자 권한입니다. 관리자 권한은 모델 수준에서만 사용할 수 있습니다.|  
  
 읽기, 만들기, 업데이트 및 삭제 권한을 결합할 수도 있습니다. 만들기, 업데이트 및 삭제 권한이 할당될 때 읽기 권한은 자동으로 할당됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [모델 개체 권한&#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [엔터티 권한&#40;Master Data Services&#41;](../master-data-services/entity-permissions-master-data-services.md)   
 [컬렉션 권한&#40;Master Data Services&#41;](../master-data-services/collection-permissions-master-data-services.md)  
  
  
