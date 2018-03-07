---
title: "보안(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 56bc41ea-de28-4184-aa7e-99111ae55af5
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0768294a9e8d555e8405e642c7cda3ecc639c5b2
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2018
---
# <a name="security-master-data-services"></a>보안(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 보안을 사용하면 사용자가 작업을 수행하는 데 필요한 특정 마스터 데이터에 액세스할 수 있도록 하며 사용해서는 안 되는 데이터에는 액세스할 수 없도록 할 수 있습니다.  
  
 또한 보안을 사용하여 사용자를 특정 모델 및 기능 영역의 관리자로 지정할 수도 있습니다. 예를 들어 특정 사용자에게 Customer 모델의 버전을 만들 수 있도록 허용하거나 보안 권한을 설정하는 능력을 부여할 수 있습니다.  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 보안은 로컬 또는 Active Directory 도메인 사용자 및 그룹을 기반으로 합니다. MDS 보안을 사용하면 사용자가 액세스할 수 있는 데이터를 결정할 때 세부 정보를 사용할 수 있습니다. 이러한 세분성 때문에 보안은 쉽게 복잡해질 수 있으므로 겹치는 사용자 및 그룹을 사용할 때는 주의해야 합니다. 자세한 내용은 [겹치는 사용자 및 그룹 권한&#40;Master Data Services&#41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)을 참조하세요.  
  
 **웹 응용 프로그램의** 사용자 및 그룹 권한 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 기능 영역에서 또는 웹 서비스를 사용하여 보안 액세스를 할당할 수 있습니다.  
  
## <a name="types-of-users"></a>사용자 유형  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에는 두 가지 사용자 유형이 있습니다.  
  
-   **탐색기** 기능 영역에서 데이터에 액세스하는 사용자.  
  
-   **탐색기**이외의 영역에서 관리 태스크를 수행할 수 있는 사용자. 이러한 사용자를 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)을 참조하세요.  
  
## <a name="how-to-set-security"></a>보안을 설정하는 방법  
 사용자 또는 그룹에 MDS 데이터 또는 기능에 대한 액세스 권한을 부여하려면 다음을 할당해야 합니다.  
  
-   [기능 영역 액세스 권한](../master-data-services/functional-area-permissions-master-data-services.md)- 다섯 가지 기능 영역 중 사용자가 액세스할 수 있는 영역을 결정합니다.  
  
-   [모델 개체 권한](../master-data-services/model-object-permissions-master-data-services.md)- 사용자가 액세스할 수 있는 특성 및 해당 특성에 대한 사용자의 액세스 유형(읽기, 만들기 및 업데이트)을 결정합니다. 사용자가 모델 수준에서 관리자 권한을 할당할 수도 있습니다.  
  
-   (옵션) [계층 멤버 권한](../master-data-services/hierarchy-member-permissions-master-data-services.md)- 사용자가 액세스할 수 있는 멤버 및 해당 멤버에 대한 사용자의 액세스 유형(읽기, 업데이트 및 삭제)을 결정합니다.  
  
 특성 및 멤버에 사용 권한을 할당할 때는 사용 권한 Intersect와 규칙에 따라 우선 적용되는 사용 권한이 결정됩니다. 자세한 내용은 [사용 권한이 결정되는 방식&#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)을 참조하세요.  
  
## <a name="security-in-the-add-in-for-excel"></a>Excel용 추가 기능의 보안  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램에서 설정된 보안이 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]에도 적용됩니다. 사용자는 해당 사용 권한을 가진 데이터만 보고 이를 사용할 수 있습니다. 관리자는 관리 태스크를 수행할 수 있습니다.  
  
 유일한 문제는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에서 할당된 모든 보안이 20분의 간격이 지나야 Excel에서 효력이 발생한다는 것입니다. 이 간격은 web.config 파일의 *MdsMaximumUserInformationCacheInterval* 설정에서 정의됩니다. 간격을 변경하려면 설정을 변경하고 IIS를 다시 시작하면 됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|모델에 대한 전체 권한이 있는 사용자를 만듭니다.|[모델 관리자 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에 Active Directory 그룹을 추가합니다. 이 작업은 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 응용 프로그램에서 데이터 액세스 권한을 그룹에 부여할 때 첫 번째 단계입니다.|[그룹 추가&#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 응용 프로그램의 기능 영역에 사용 권한을 할당합니다.|[기능 영역 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-functional-area-permissions-master-data-services.md)|  
|모델 개체에 사용 권한을 할당하여 특성 값에 사용 권한을 할당합니다.|[모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)|  
|계층 노드에 사용 권한을 할당하여 멤버에 사용 권한을 할당합니다.|[계층 멤버 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)|  
  
## <a name="see-also"></a>참고 항목  
 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [사용자 및 그룹&#40;Master Data Services&#41;](../master-data-services/users-and-groups-master-data-services.md)   
 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)   
 [모델 개체 권한&#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [계층 멤버 권한&#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [사용 권한이 결정되는 방식&#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
