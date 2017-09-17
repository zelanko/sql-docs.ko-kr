---
title: "계층(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Master Data Services]
- hierarchies [Master Data Services], about hierarchies
ms.assetid: 70dbb1fc-ead7-45be-9552-a45e3ccd8d21
caps.latest.revision: 11
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 5618ad01875ee9b8c222784e97f19b18c47f1bfa
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="hierarchies-master-data-services"></a>계층(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 계층은 다음 작업에 사용할 수 있는 트리 구조입니다.  
  
-   구성을 목적으로 유사한 멤버 그룹화  
  
-   보고 및 분석을 위해 멤버 통합 및 요약  
  
## <a name="what-hierarchies-contain"></a>계층에 포함된 내용  
 각 계층은 하나 이상의 엔터티에 속한 멤버를 포함합니다. 멤버가 추가, 변경 또는 삭제되면 모든 계층이 업데이트됩니다. 따라서 데이터가 모든 계층에서 정확하게 유지됩니다. 계층은 각 멤버가 한 번만 계산되도록 하는 데도 유용합니다.  
  
 멤버의 하위 집합을 그룹화하려면 컬렉션 사용을 고려하십시오. 자세한 내용은 [컬렉션&#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)을 참조하세요.  
  
## <a name="kinds-of-hierarchies"></a>계층의 종류  
 여러 계층을 만들어 다양한 방식으로 멤버를 보고 구성할 수 있습니다. 다음을 만들 수 있습니다.  
  
-   단일 엔터티에서 비정형 계층(명시적 계층이라고 함)을 만들 수 있습니다. 자세한 내용은 [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)을 참조하세요.  
  
-   엔터티와 해당 특성 간의 기존 관계를 기반으로 여러 엔터티에서 수준 기반 계층(파생 계층이라고 함)을 만들 수 있습니다. 자세한 내용은 [파생 계층&#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)을 참조하세요.  
  
> [!NOTE]  
>  계층의 모든 멤버는 같은 모델에 속해야 합니다.  
  
## <a name="hierarchies-are-not-taxonomies"></a>계층은 분류가 아님  
 계층은 분류와 다릅니다. 분류는 여러 특성을 동시에 사용하여 멤버를 구성하지만, 계층은 한 번에 하나의 특성을 사용하여 멤버를 구성합니다. 또한 분류는 같은 멤버를 여러 번 포함할 수 있지만, 계층은 멤버를 한 번만 포함합니다.  
  
 예를 들어 분류에는 같은 자전거가 빨간색이기 때문에 한 번 포함되고 크기가 38이기 때문에 또 한 번 포함되는 식으로 분류에 두 번 포함될 수 있습니다. 그러나 계층에서는 자전거가 한 번만 포함되므로 자전거를 색을 기준으로 표시할지 또는 크기를 기준으로 표시할지 결정해야 합니다.  
  
## <a name="hierarchy-example"></a>계층 예  
 다음 예에서는 Product 멤버가 Subcategory 멤버로 그룹화됩니다.  
  
 ![하위 범주로 그룹화된 계층 예제](../master-data-services/media/mds-conc-hierarchy.gif "하위 범주로 그룹화된 계층 예제")  
  
## <a name="related-tasks"></a>관련 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|명시적 계층을 만듭니다.|[명시적 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|파생 계층을 만듭니다.|[파생 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|기존 파생 계층의 수준을 숨기거나 삭제합니다.|[파생 계층의 수준 숨기기 또는 삭제&#40;Master Data Services&#41;](../master-data-services/hide-or-delete-levels-in-a-derived-hierarchy-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [파생 계층&#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [재귀 계층 구조&#40;Master Data Services&#41;](../master-data-services/recursive-hierarchies-master-data-services.md)  
  
-   [명시적 캡이 포함된 파생 계층&#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)  
  
-   [컬렉션&#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  

