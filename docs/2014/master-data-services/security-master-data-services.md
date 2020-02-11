---
title: 보안(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 56bc41ea-de28-4184-aa7e-99111ae55af5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 80be0aea6705ed98fd12ea3481af59e289b94604
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482583"
---
# <a name="security-master-data-services"></a>보안(Master Data Services)
  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 보안을 사용하면 사용자가 작업을 수행하는 데 필요한 특정 마스터 데이터에 액세스할 수 있도록 하며 사용해서는 안 되는 데이터에는 액세스할 수 없도록 할 수 있습니다.  
  
 또한 보안을 사용하여 사용자를 특정 모델 및 기능 영역의 관리자로 지정할 수도 있습니다. 예를 들어 특정 사용자에게 Customer 모델의 버전을 만들 수 있도록 허용하거나 보안 권한을 설정하는 능력을 부여할 수 있습니다.  
  
 
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 보안은 로컬 또는 Active Directory 도메인 사용자 및 그룹을 기반으로 합니다. MDS 보안을 사용하면 사용자가 액세스할 수 있는 데이터를 결정할 때 세부 정보를 사용할 수 있습니다. 이러한 세분성 때문에 보안은 쉽게 복잡해질 수 있으므로 겹치는 사용자 및 그룹을 사용할 때는 주의해야 합니다. 자세한 내용은 [겹치는 사용자 및 그룹 권한&#40;Master Data Services&#41;](overlapping-user-and-group-permissions-master-data-services.md)를 참조하세요.  
  
 
  **웹 애플리케이션의** 사용자 및 그룹 권한 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 기능 영역에서 또는 웹 서비스를 사용하여 보안 액세스를 할당할 수 있습니다.  
  
## <a name="types-of-users"></a>사용자 유형  
 
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에는 두 가지 사용자 유형이 있습니다.  
  
-   
  **탐색기** 기능 영역에서 데이터에 액세스하는 사용자.  
  
-   
  **탐색기**이외의 영역에서 관리 태스크를 수행할 수 있는 사용자. 이러한 사용자를 [관리자&#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)을 참조하세요.  
  
## <a name="how-to-set-security"></a>보안을 설정하는 방법  
 사용자 또는 그룹에 MDS 데이터 또는 기능에 대한 액세스 권한을 부여하려면 다음을 할당해야 합니다.  
  
-   [기능 영역 액세스](../../2014/master-data-services/functional-area-permissions-master-data-services.md)-사용자가 액세스할 수 있는 사용자 인터페이스의 다섯 가지 기능 영역을 결정 합니다.  
  
-   [모델 개체 사용 권한](../../2014/master-data-services/model-object-permissions-master-data-services.md)-사용자가 액세스할 수 있는 특성 및 해당 특성에 대 한 사용자의 액세스 유형 (읽기 또는 업데이트)을 결정 합니다.  
  
-   (선택 사항) [계층 멤버 권한](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)- 사용자가 액세스할 수 있는 멤버 및 해당 멤버에 대한 사용자의 액세스 유형(읽기 또는 업데이트)을 결정합니다.  
  
 특성 및 멤버에 사용 권한을 할당할 때는 사용 권한 Intersect와 규칙에 따라 우선 적용되는 사용 권한이 결정됩니다. 자세한 내용은 [사용 권한이 결정되는 방식&#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)을 참조하세요.  
  
 레코드 수준 보안을 구현하려면 엔터티에 대한 계층을 만들고 계층의 멤버에 사용자 권한을 할당합니다. 멤버는 데이터 레코드입니다.  계층 멤버 권한은 사용자에게 특정 멤버에 대한 제한된 액세스 권한을 부여하려는 경우에만 사용해야 합니다.  
  
 다음 이미지는 스타일 엔터티에 대한 파생 계층과 선택된 사용자에 대한 스타일 멤버 권한을 보여 줍니다. 업데이트 권한이 M {Men's} 및 U {Unisex} 멤버에 할당되고 읽기 전용 권한이 Women's Style 멤버에 할당됩니다. 즉, 사용자가 Men's 및 Unisex 제품을 업데이트할 수 있으며 Women's Style제품에 대한 레코드는 읽을 수만 있습니다.  
  
 ![스타일 파생 계층 및 멤버 권한](../../2014/master-data-services/media/style-derived-hierarchy-mds.png "스타일 파생 계층 및 멤버 권한")  
  
 계층을 만드는 방법에 대 한 자세한 내용은 [&#41;MDS(Master Data Services) 명시적 계층 &#40;만들기](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md) 를 참조 하 고 [MDS(Master Data Services)&#41;&#40;파생 계층을 만듭니다 ](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md).  
  
 멤버 권한을 할당 하는 방법에 대 한 자세한 내용은 [&#40;MDS(Master Data Services) 계층 멤버 권한 할당](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md) 을 참조 하세요&#41;  
  
## <a name="security-in-the-add-in-for-excel"></a>Excel용 추가 기능의 보안  
 
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서 설정된 보안이 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]에도 적용됩니다. 사용자는 해당 사용 권한을 가진 데이터만 보고 이를 사용할 수 있습니다. 관리자는 관리 태스크를 수행할 수 있습니다.  
  
 유일한 문제는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에서 할당된 모든 보안이 20분의 간격이 지나야 Excel에서 효력이 발생한다는 것입니다. 이 간격은 web.config 파일의 *MdsMaximumUserInformationCacheInterval* 설정에서 정의됩니다. 간격을 변경하려면 설정을 변경하고 IIS를 다시 시작하면 됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|모델에 대한 전체 권한이 있는 사용자를 만듭니다.|[모델 관리자 &#40;MDS(Master Data Services)를 만듭니다&#41;](../../2014/master-data-services/create-a-model-administrator-master-data-services.md)|  
|
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에 Active Directory 그룹을 추가합니다. 이 작업은 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 애플리케이션에서 데이터 액세스 권한을 그룹에 부여할 때 첫 번째 단계입니다.|[그룹 &#40;MDS(Master Data Services) 추가&#41;](../../2014/master-data-services/add-a-group-master-data-services.md)|  
|
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 애플리케이션의 기능 영역에 사용 권한을 할당합니다.|[MDS(Master Data Services)&#41;&#40;기능 영역 권한 할당](../../2014/master-data-services/assign-functional-area-permissions-master-data-services.md)|  
|모델 개체에 사용 권한을 할당하여 특성 값에 사용 권한을 할당합니다.|[모델 개체 사용 권한 할당 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)|  
|계층 노드에 사용 권한을 할당하여 멤버에 사용 권한을 할당합니다.|[계층 멤버 권한 할당 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)|  
  
## <a name="see-also"></a>참고 항목  
 [관리자는 MDS(Master Data Services) &#40;&#41;](../../2014/master-data-services/administrators-master-data-services.md)   
 [사용자 및 그룹 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/users-and-groups-master-data-services.md)   
 [기능 영역 권한 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [모델 개체 사용 권한 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [계층 멤버 권한 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [MDS(Master Data Services) &#40;사용 권한을 결정 하는 방법&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
