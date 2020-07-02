---
title: 엔터티
description: 엔터티는 MDS(Master Data Services) 모델에 포함 된 개체입니다. 각 엔터티에는 관리하는 마스터 데이터의 행인 멤버가 들어 있습니다.
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], about entities
- entities [Master Data Services]
ms.assetid: 0af057d5-6b73-472b-99eb-9f5eb61a9b5b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5c40c4cd565d01e7918cecd7c2dc89015f13c9f9
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811975"
---
# <a name="entities-master-data-services"></a>엔터티(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  엔터티는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 모델에 포함된 개체입니다. 각 엔터티에는 관리하는 마스터 데이터의 행인 멤버가 들어 있습니다.  
  
## <a name="how-many-entities-are-appropriate"></a>엔터티 수는 어느 정도가 적절합니까?  
 모델에는 관리할 엔터티를 원하는 만큼 포함할 수 있습니다. 각 엔터티는 유사한 종류의 데이터 그룹을 포함해야 합니다. 예를 들어 모든 회사 계정을 위한 엔터티나 직원 마스터 목록용 엔터티로 구분할 수 있습니다.  
  
 일반적으로 비즈니스에 중요하며 모델의 다른 개체와 관련되는 중앙 엔터티가 한 개 이상 있습니다. 예를 들어 Product 모델에 Product라는 중앙 엔터티와 이와 관련된 Subcategory 및 Category라는 엔터티가 있을 수 있습니다. 하지만 중앙 엔터티가 필수는 아닙니다. 요구에 따라 중요성이 동일하다고 생각되는 몇 개의 엔터티를 가질 수도 있습니다.  
  
## <a name="how-entities-relate-to-other-model-objects"></a>다른 모델 개체와 엔터티의 관계  
 엔터티는 마스터 데이터가 포함되어 있으며 멤버를 나타내는 행과 특성을 나타내는 열로 구성된 테이블이라고 생각하면 됩니다.  
  
 ![테이블로 표시된 MDS(Master Data Services) 엔터티](../master-data-services/media/mds-conc-entity-table.gif "테이블로 표시된 MDS(Master Data Services) 엔터티")  
  
 관리하려는 마스터 데이터 목록으로 엔터티를 채웁니다.  
  
 엔터티를 사용하여 파생 계층을 만들 수 있습니다. 파생 계층은 여러 엔터티를 기반으로 하는 수준 기반 계층입니다. 자세한 내용은 [파생 계층&#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)을 참조하세요.  
  
 엔터티가 명시적 계층(단일 엔터티를 기반으로 하는 비정형 구조) 및 컬렉션(멤버 하위 집합의 일회성 조합)을 포함할 수도 있습니다. 자세한 내용은 [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md) 및 [컬렉션&#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)을 참조하세요.  
  
## <a name="using-entities-as-constrained-lists"></a>엔터티를 제한된 목록으로 사용함  
 사용자가 엔터티의 멤버에 특성을 할당하는 경우 제한된 값 목록에서 선택하도록 사용자에게 허용할 수 있습니다. 그러려면 엔터티를 사용하여 특성 값 목록을 채웁니다. 이를 도메인 기반 특성이라고 합니다. 자세한 내용은 [도메인 기반 특성&#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)을 참조하세요.  
  
## <a name="base-entities"></a>기준 엔터티  
 기준 엔터티는 사용자가 모델의 개체를 탐색하는 시작 지점입니다. 기준 엔터티는 사용자가 **탐색기** 기능 영역을 열고 메뉴 모음에서 **탐색기** 를 클릭할 때 표시되는 화면의 레이아웃을 결정합니다. 엔터티를 기준 엔터티로 지정하려면 **시스템 관리** 기능 영역으로 이동합니다. **모델 뷰** 페이지에서 오른쪽 트리 컨트롤의 엔터티를 왼쪽 트리 컨트롤에 있는 모델 이름으로 끌어옵니다.  
  
## <a name="entity-security"></a>엔터티 보안  
 관련 모델 개체를 포함하여 엔터티에 대한 사용 권한을 사용자에게 부여할 수 있습니다. 자세한 내용은 [엔터티 권한&#40;Master Data Services&#41;](../master-data-services/entity-permissions-master-data-services.md)을 참조하세요.  
  
## <a name="entity-examples"></a>엔터티 예  
 다음 예의 엔터티에는 멤버를 설명하는 Name, Code, Subcategory, StandardCost, ListPrice 및 FilePhoto 특성이 있습니다. 각 멤버는 단일 특성 값 행으로 표시됩니다.  
  
 ![Bike 제품 엔터티 테이블](../master-data-services/media/mds-conc-entity-table-w-data.gif "Bike 제품 엔터티 테이블")  
  
 다음 예에서 Product 엔터티는 중앙 엔터티입니다. Subcategory 엔터티는 Product 엔터티의 도메인 기반 특성입니다. Category 엔터티는 Subcategory 엔터티의 도메인 기반 특성이고, StandardCost 및 ListPrice는 Product 엔터티의 자유 형식 특성이며, FilePhoto는 Product 엔터티의 파일 특성입니다.  
  
 ![제품 엔터티 트리 구조](../master-data-services/media/mds-conc-entity-ui.gif "제품 엔터티 트리 구조")  
  
> [!NOTE]  
>  이 예는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] UI(사용자 인터페이스)를 기반으로 합니다. 계층 트리 구조는 엔터티와 도메인 기반 특성의 관계를 표시합니다. 즉, 중요도가 아니라 관계를 보여 줍니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|새 엔터티를 만듭니다.|[엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)|  
|기존 엔터티의 이름을 변경합니다.|[엔터티 편집&#40;Master Data Services&#41;](../master-data-services/edit-an-entity-master-data-services.md)|  
|기존 엔터티를 삭제합니다.|[엔터티 삭제&#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)|  
|엔터티에 사용 권한을 할당합니다.|[모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [모델&#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
-   [멤버&#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
-   [특성&#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
