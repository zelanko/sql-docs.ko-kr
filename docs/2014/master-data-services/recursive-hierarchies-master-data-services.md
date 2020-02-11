---
title: 재귀 계층 구조(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- recursive hierarchies [Master Data Services]
- hierarchies [Master Data Services], recursive hierarchies
ms.assetid: 9408c6ea-d9c4-4a0b-8a1b-1457fb6944af
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0ebe093973174fe1e245ced134888d3e10417467
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478847"
---
# <a name="recursive-hierarchies-master-data-services"></a>재귀 계층 구조(Master Data Services)
  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 재귀 계층 구조는 재귀 관계를 포함하는 파생 계층입니다. 재귀 관계는 엔터티에 엔터티 자체를 기반으로 하는 도메인 기반 특성이 있는 경우에 존재합니다.  
  
## <a name="recursive-hierarchy-example"></a>재귀 계층 예  
 일반적인 재귀 계층 예는 조직 구조입니다. 
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 Manager라는 도메인 기반 특성을 가진 Employee 엔터티를 만들어서 이를 수행할 수 있습니다. Manager 특성은 직원 목록으로 채워집니다. 이 샘플 조직에서 모든 직원은 관리자가 될 수 있습니다.  
  
 ![mds_conc_recursive_table_w_data](../../2014/master-data-services/media/mds-conc-recursive-table-w-data.gif "mds_conc_recursive_table_w_data")  
  
 Employee 엔터티와 Manager 도메인 기반 특성 간의 관계를 강조하는 파생 계층을 만들 수 있습니다.  
  
 ![mds_conc_recursive_UI_structure](../../2014/master-data-services/media/mds-conc-recursive-ui-structure.gif "mds_conc_recursive_UI_structure")  
  
 계층에 각 멤버를 한 번만 포함하려면 Null 관계에 앵커를 지정할 수 있습니다. Null 관계에 앵커를 지정하는 경우 빈 도메인 기반 특성 값을 가진 멤버가 계층의 최상위 수준에 표시됩니다.  
  
 ![mds_conc_recursive_UI_example_anchored](../../2014/master-data-services/media/mds-conc-recursive-ui-example-anchored.gif "mds_conc_recursive_UI_example_anchored")  
  
 Null 관계에 앵커를 지정하지 않을 경우 멤버가 여러 번 포함됩니다. 모든 멤버가 최상위 수준에 표시되며, 자신이 특성으로 사용되는 멤버 아래에도 표시됩니다.  
  
 ![mds_conc_recursive_UI_example_nonanchored](../../2014/master-data-services/media/mds-conc-recursive-ui-example-nonanchored.gif "mds_conc_recursive_UI_example_nonanchored")  
  
 이 예에서 Marcia는 최상위 수준에 있습니다. 그녀는 다른 Employee 멤버의 도메인 기반 특성 값으로 사용되지 않으므로 어느 직원의 관리자도 아닙니다. 이와 달리 Marcia에게는 Robert가 Manager 특성 값으로 지정되어 있으므로 Robert 아래에 한 수준이 있습니다.  
  
## <a name="rules"></a>규칙  
  
-   파생 계층에는 두 개 이상의 재귀적 관계가 포함될 수 없지만 다른 파생 관계는 포함될 수 있습니다. 예를 들어 재귀적 Manager to Employee 관계가 포함된 파생 계층에 Country to Manager 및 Employee to Store 관계가 포함될 수 있습니다.  
  
-   
  **계층 멤버** 탭에서 멤버 권한을 재귀 계층 구조의 멤버에 할당할 수 없습니다.  
  
-   재귀 계층 구조는 순환 관계를 포함할 수 없습니다. 예를 들어, Sandeep이 Katherine의 관리자인 경우 Katherine은 Sandeep의 관리자일 수 없습니다. 또한 Katherine은 자신을 관리할 수 없습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|파생 계층을 만듭니다.|[파생 계층 &#40;MDS(Master Data Services)를 만듭니다&#41;](create-a-derived-hierarchy-master-data-services.md)|  
|기존 파생 계층의 이름을 변경합니다.|[파생 계층 이름 변경 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/change-a-derived-hierarchy-name-master-data-services.md)|  
|기존 파생 계층을 삭제합니다.|[파생 계층 &#40;MDS(Master Data Services)를 삭제&#41;](../../2014/master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [도메인 기반 특성 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [파생 계층 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  
