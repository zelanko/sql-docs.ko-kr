---
title: 모델 개체 권한(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e3a46b104bd17c2eedccbc27c7b8c2581125319
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="model-object-permissions-master-data-services"></a>모델 개체 권한(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  모델 개체 권한은 필수 항목입니다. 이 사용 권한은 사용자가 UI의 **탐색기** 기능 영역에서 액세스할 수 있는 특성을 결정합니다.  
  
 예를 들어 사용자에게 Product 엔터티에 대한 **업데이트** 권한을 할당하는 경우 사용자는 Product 엔터티의 모든 특성을 업데이트할 수 있습니다. 단일 특성에 대해 **업데이트** 권한을 할당하는 경우 사용자는 해당 특성만 업데이트할 수 있습니다.  
  
 각 개별 특성 값에 할당된 보안을 확인하기 위해 모델 개체 사용 권한과 계층 멤버 사용 권한을 결합합니다. 이에 따라 사용자가 액세스할 수 있는 멤버가 결정됩니다.  
  
 **탐색기**외의 기능 영역에 대한 사용자 액세스 권한을 부여하려면 사용자가 모델 관리자여야 하며, 개체 모델에 대한 관리자 권한 할당 작업도 필요합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
 모델 개체 사용 권한은 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] UI(사용자 인터페이스)의 **모델** 탭에 있는 **사용자 및 그룹 권한** 기능 영역에서 할당됩니다. 이 탭에서 모델은 트리 구조로 표시됩니다. 트리의 개체에 사용 권한을 할당하면 모든 하위 개체가 해당 권한을 상속합니다. 개별 개체에 사용 권한을 할당하면 이 상속을 재정의할 수 있습니다.  
  
 모델 개체에 대한 읽기, 만들기, 업데이트 및 삭제 또는 거부 권한의 조합을 할당할 수 있습니다. **모델** 탭에서 사용 권한을 할당하지 않은 경우 사용자는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 모델이나 데이터를 볼 수 없습니다.  
  
## <a name="best-practice"></a>최선의 구현 방법  
 일반적으로 모델 개체에 **모든** 권한을 할당한 다음 그 아래 개체에 대한 사용 권한을 명시적으로 할당합니다.  
  
## <a name="external-resources"></a>외부 리소스  
 msdn.com의 블로그 게시물 [향상된 보안 기능](http://go.microsoft.com/fwlink/p/?LinkId=615376)  
  
## <a name="see-also"></a>참고 항목  
 [모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [모델 권한&#40;Master Data Services&#41;](../master-data-services/model-permissions-master-data-services.md)   
 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)   
 [계층 멤버 권한&#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [사용 권한이 결정되는 방식&#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
