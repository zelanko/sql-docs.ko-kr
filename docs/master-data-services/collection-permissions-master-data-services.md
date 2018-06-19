---
title: 컬렉션 권한(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], permissions
- permissions [Master Data Services], collections
ms.assetid: 703e1bf5-4b4b-4830-8a5b-f979b09f677d
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 778e4890ede89415ac52b1a8fd70af4366a0133b
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332617"
---
# <a name="collection-permissions-master-data-services"></a>컬렉션 권한(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  컬렉션 권한은 엔터티의 모든 컬렉션에 적용됩니다. 특정 컬렉션에 사용 권한을 부여할 수는 없습니다. 사용 권한은 모든 컬렉션에 적용됩니다.  
  
> [!NOTE]  
>  이러한 사용 권한은 사용자 인터페이스의 **탐색기** 기능 영역에만 적용됩니다.  
  
|사용 권한|설명|  
|----------------|-----------------|  
|**읽기**|사용자는 컬렉션 멤버 및 멤버 특성을 읽을 수 있습니다.|  
|**만들기**|사용자는 컬렉션 멤버를 만들고 특성 값을 할당할 수 있습니다.|  
|**Update**|사용자는 컬렉션 멤버, 특성 및 관계를 업데이트할 수 있습니다.|  
|**Delete**|사용자는 컬렉션 멤버를 삭제할 수 있습니다.|  
|**거부**|컬렉션 멤버에 대한 모든 액세스를 거부합니다.|  
  
 읽기, 만들기, 업데이트 및 삭제 권한을 결합할 수 있습니다. 만들기, 업데이트 및 삭제가 할당될 때 읽기 권한은 자동으로 할당됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [컬렉션&#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)   
 [모델 개체 권한&#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)  
  
  
