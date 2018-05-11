---
title: 사용자 및 그룹(Master Data Services) | Microsoft Docs
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
helpviewer_keywords:
- users [Master Data Services]
- groups [Master Data Services]
- users [Master Data Services], about users
- groups [Master Data Services], about groups
ms.assetid: ed08dd2d-248e-4b68-91d4-e9961cb50eed
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c754dee32b5ab9046d60f42d0b47dc15fdf9893c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="users-and-groups-master-data-services"></a>사용자 및 그룹(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램에 액세스하려면 사용자에게 Windows 도메인 계정이나 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 가 설치된 서버 컴퓨터의 계정이 있어야 합니다. [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에 대한 액세스 권한을 부여하려면 다음 중 하나를 수행합니다.  
  
-   [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 도메인 또는 로컬 그룹에 사용자 계정을 추가한 다음 그룹 목록에 그룹을 추가합니다.  
  
-   [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 사용자 목록에 사용자 계정을 추가합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에 대한 액세스 권한이 있는 그룹에 사용자가 속할 경우 사용자가 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 또는 MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]에 처음 액세스할 때 사용자의 이름이 사용자 목록에 자동으로 추가됩니다.  
  
 UI의 **탐색기** 기능 영역 내에서 동작을 수행하려면 **탐색기** 기능 영역에 대한 액세스 권한과 모델 개체에 대한 사용 권한이 그룹 또는 사용자에게 할당되어야 합니다.  
  
 사용자 또는 그룹이 다른 기능 영역에 액세스해야 하는 경우에는 특정 기능 영역에 대한 액세스 권한이 사용자 또는 그룹에 할당되어야 합니다.  
  
## <a name="best-practice"></a>최선의 구현 방법  
 관리를 간소화하려면 그룹을 만들고 각 그룹에 기능 영역 및 모델 개체에 대한 그룹 권한을 할당합니다. 그러면 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] UI에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
 개별 사용자에게는 추가 권한을 할당하지 말고 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에 대한 액세스 권한이 있는 여러 그룹에 사용자를 포함하지 마십시오. 또한 그룹에서 특정 멤버에 대해 제한된 액세스 권한을 부여하려는 경우를 제외하고는 계층 멤버 권한을 사용하지 마십시오.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 추가&#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)   
 [그룹 추가&#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)   
 [사용자 또는 그룹 삭제&#40;Master Data Services&#41;](../master-data-services/delete-users-or-groups-master-data-services.md)   
 [사용자의 사용 권한 테스트&#40;Master Data Services&#41;](../master-data-services/test-a-user-s-permissions-master-data-services.md)  
  
  
