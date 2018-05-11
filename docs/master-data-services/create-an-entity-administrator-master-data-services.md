---
title: 엔터티 관리자 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 717be1e8-488e-4219-8d1e-ca9084b864cd
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3b9e781eb81096e364acd2040c075d7f170ca545
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-entity-administrator-master-data-services"></a>엔터티 관리자 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 그룹이나 사용자에게 엔터티 하나 이상의 모든 개체에 대한 모든 권한을 제공하거나 보류 중인 변경 집합 승인 권한을 제공하려는 경우 엔터티 관리자를 만듭니다.  
  
> [!TIP]  
>  관리 작업을 간편하게 수행하려면 Windows 또는 로컬 그룹을 만든 다음 엔터티 관리자로 구성합니다. 그러면 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
## <a name="to-create-an-entity-administrator"></a>엔터티 관리자를 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **사용자 및 그룹 권한**을 클릭합니다.  
  
2.  편집할 사용자 또는 그룹의 행을 선택하고 **선택한 사용자 편집**을 클릭합니다.  
  
3.  **모델** 탭을 클릭하고 원하는 경우 **모델** 목록에서 모델을 선택한 후에 **편집**을 클릭합니다.  
  
4.  권한을 부여할 엔터티를 클릭하고 메뉴에서 **관리** 를 클릭합니다.  
  
5.  그룹 또는 사용자를 관리자로 지정할 각 엔터티에 대해 4단계를 완료합니다.  
  
6.  **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [계층 멤버 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [모델 개체 권한&#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [계층 멤버 권한&#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
