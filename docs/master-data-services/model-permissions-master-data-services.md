---
title: "모델 권한 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8e54b1bd5e60c600e2447f37bdcf77e6f811e869
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="model-permissions-master-data-services"></a>모델 권한(Master Data Services)
  모델 권한은 모델 내의 모든 엔터티, 파생 계층, 명시적 계층 및 컬렉션에 적용됩니다. 모델에 할당된 사용 권한은 개별 개체에 대해 재정의할 수 있습니다.  
  
> [!NOTE]  
>  사용자가 모델 관리자인 경우 사용자 인터페이스의 모든 기능 영역에 모델이 표시됩니다. 그렇지 않은 경우에는 **탐색기** 기능 영역에만 모델이 표시됩니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
|사용 권한|Description|  
|----------------|-----------------|  
|**읽기**|사용자는 멤버, 특성, 계층 멤버 자격 또는 컬렉션 멤버를 읽을 수 있습니다.|  
|**만들기**|사용자는 멤버를 만들고 만드는 동안 특성 값을 할당할 수 있습니다.|  
|**Update**|사용자는 멤버, 특성, 계층 멤버 자격 또는 컬렉션 멤버를 업데이트할 수 있습니다.|  
|**Delete**|사용자는 멤버를 삭제할 수 있습니다.|  
|**거부**|모델에 대한 모든 액세스를 거부 합니다.|  
|**Admin**|모델에 대한 관리자 권한입니다. 관리자 권한은 모델 수준에서만 사용할 수 있습니다.|  
  
 읽기, 만들기, 업데이트 및 삭제 권한을 결합할 수도 있습니다. 만들기, 업데이트 및 삭제 권한이 할당될 때 읽기 권한은 자동으로 할당됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [모델 개체 사용 권한 &#40; 할당 Master Data services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [모델 개체 사용 권한 &#40; Master Data services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [엔터티 사용 권한 &#40; Master Data services&#41;](../master-data-services/entity-permissions-master-data-services.md)   
 [컬렉션 사용 권한 &#40; Master Data services&#41;](../master-data-services/collection-permissions-master-data-services.md)  
  
  
