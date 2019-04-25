---
title: 엔터티 종속성 탐색기 | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- Master Data Services
ms.assetid: 9d922118-1412-4a9d-9c02-70d6c48d6c0d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0665b6f7d54b7f83f3edda224be4e9efad670e90
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62518127"
---
# <a name="entity-dependencies-explorer"></a>엔터티 종속성 탐색기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 2016은 파생 계층을 먼저 정의할 필요 없이 해당 도메인 기반 특성(DBA) 값에 지정된 대로 모델 내의 엔터티 멤버 간의 관계를 시각화하는 대체 방법을 제공하는 새 탐색기 페이지, 엔터티 종속성을 추가합니다.   
  
"내 엔터티를 사용하는 사람 및 방법?"의 질문에 답변하는 데 도움이 됩니다. 보기는 파생 계층 탐색기 페이지와 유사하지만 더욱 포괄적입니다. 특정 계층의 일부로 정의된 것 뿐만 아니라 모든 DBA 관계를 보여 줍니다. 표시된 계층 구조는 단순히 기존 DBA에서 유추되기 때문에 계층 정의는 필요하지 않습니다.  
  
탐색기 페이지 메뉴에서 엔터티 종속성 메뉴 항목은 하나 이상의 엔터티에 의해 종속되는 모델의 모든 엔터티를 나열합니다(즉, 하나 이상의 엔터티는 나열된 엔터티를 참조하는 DBA를 가짐). 종속성(직접 및 간접)의 수는 엔터티 이름 옆에 표시되고 맨 위쪽에 가장 많이 참조된 엔터티와 함께 이 수로 목록이 정렬됩니다. [샘플 데이터](https://msdn.microsoft.com/library/master-data-services-sample.aspx)의 Customer 모델에서 가져온 아래 스크린샷은 BigArea 엔터티가 7개의 엔터티로 참조된 것(직접 또는 간접적으로)을 보여 줍니다.  
  
![MDS_EntityDependencies_Menu.jpg](../master-data-services/media/mds-entitydependencies-menu-jpg.jpg)  
    
이 메뉴 항목을 클릭하면 엔터티 멤버가 사용되는 방법을 표시하는 BigArea 엔터티에 대한 새 엔터티 종속성 탐색기 페이지가 열립니다. 아래에 중첩된 해당 7개의 소비 엔터티의 멤버로 트리 맨 위에 BigArea 멤버와 함께 계층 뷰가 표시됩니다.  
  
![MDS_EntityDependencies_Tree.jpg](../master-data-services/media/mds-entitydependencies-tree-jpg.jpg)  
    
둘 이상의 엔터티에서 엔터티를 직접 사용할 수 있습니다. 위의 예제에서 SubRegion 및 RegionClimate 엔터티는 Region 엔터티를 사용합니다(DBA 참조가 있음). 각 소비 엔터티의 멤버는 엔터티 이름을 갖는 부모 노드 아래에서 함께 그룹화됩니다.   
  
![MDS_EntityDependencies_Entity_Node.jpg](../master-data-services/media/mds-entitydependencies-entity-node-jpg.jpg)  
  
이러한 컨테이너 트리 노드에는 엔터티 이름 왼쪽에 표 모양의 아이콘이 있고 텍스트는 계층 수준 깊이로 색이 지정됩니다. 위 예제는 "CDSR {Canada}" SubRegion에 "NAm {N. America}" BigArea, "CDA {Canada}" Area, "CDR {Canada}" Region을 차례로 참조하는 DBA 참조가 있음을 보여줍니다.  
  
계층 탐색기 페이지에서와 마찬가지로 뷰는 완벽하게 편집할 수 있습니다. 한 부모에서 다른 부모로 자식 멤버를 잘라내기-붙여넣기 또는 끌어서 놓기로 트리에서 부모-자식 관계를 수정할 수 있습니다. 트리의 오른쪽 세부 정보 창에서 다른 멤버 특성 값을 수정할 수 있습니다.   
  
  
  
  

