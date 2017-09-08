---
title: "차원 디자이너에서 특성 보기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e73cba395d806e834dc03e7f7cd79d030eb5c36e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---view-attributes-in-dimension-designer"></a>특성 속성-차원 디자이너에서 특성 보기
  특성은 차원 개체에 대해 생성됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 차원 디자이너를 사용하여 특성을 보고 구성할 수 있습니다. 차원 디자이너의 **차원 구조** 탭에 있는 **특성** 창에 차원에 포함된 특성이 나열됩니다. 이 창에서 특성을 추가하거나 제거하고 구성할 수 있습니다. 또한 새 계층에서 수준으로 사용하거나 기존 계층에 수준으로 추가할 특성을 선택할 수도 있습니다.  
  
 차원의 특성을 보려면 해당 차원의 차원 디자이너를 엽니다. 디자이너의 **차원 구조** 탭에 있는 **특성**  창에 해당 차원에 포함된 특성이 표시됩니다. **의** 차원 **메뉴의** 특성 표시 위치 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 가리킨 후 다음 명령 중 하나를 클릭하여 목록, 트리 또는 표 뷰 간에 전환할 수 있습니다.  
  
1.  **목록**에서 특성을 표시합니다. 특성을 목록 형식으로 표시합니다. 특성을 목록에서 삭제하거나, 이름을 바꾸거나, 사용법을 변경하려면 특성을 마우스 오른쪽 단추로 클릭합니다. 계층을 만들 때 이 뷰를 사용합니다. 특성 정보와 멤버 속성은 표시되지 않습니다.  
  
2.  **트리**에서 특성을 표시합니다. 특성을 트리 형식으로 표시합니다. 차원이 트리의 최상위 노드입니다. 다음 동작을 수행하여 특성 관계를 보거나 새 특성 관계를 만들 특성을 확장합니다.  
  
    -   **속성** 창에서 속성을 보려면 차원, 특성 또는 멤버 속성을 클릭합니다.  
  
    -   목록에서 삭제하거나, 이름을 바꾸거나, 사용법을 변경하려면 특성이나 멤버 속성을 마우스 오른쪽 단추로 클릭합니다.  
  
     멤버 속성을 보거나 만들 때 이 뷰를 사용합니다. 이 뷰를 사용하여 계층을 만들 수도 있습니다.  
  
3.  **표**에서 특성을 표시합니다. 특성을 표 형식으로 표시합니다. 표에는 다음 열이 표시됩니다.  
  
    -   **이름** 에는 **Name** 속성 값이 표시됩니다. 이 설정을 변경하려면 다른 이름을 입력합니다.  
  
    -   **사용법** 은 특성의 용도가 Regular, Key, Parent, AccountType 중에서 어떤 것인지를 나타냅니다. 다른 설정을 선택하려면 이 열의 값을 클릭합니다.  
  
    -   **유형** 은 특성의 비즈니스 인텔리전스 범주를 지정합니다. 다른 설정을 선택하려면 이 셀을 클릭합니다.  
  
    -   **키 열** 은 특성의 **KeyColumn** 속성에 대한 OLE DB 데이터 형식을 표시합니다. 이 열은 변경할 수 없습니다.  
  
    -   **이름 열** 은 특성에 대한 **NameColumn** 속성 설정이 **KeyColumn** 속성에 대해 설정된 열과 동일한지 여부를 나타냅니다. 이 열은 변경할 수 없습니다.  
  
     해당 특성의 속성을 보려면 표에서 아무 행이나 클릭합니다.  
  
     특성을 만들고 구성할 때 이 뷰를 사용합니다.  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서는 특성의 용도에 따라 다음 표의 아이콘이 특성에 표시됩니다.  
  
|아이콘|특성 사용법|  
|----------|---------------------|  
|![특성 아이콘](../../analysis-services/multidimensional-models/media/as-icon-attribute.gif "특성 아이콘")|Regular 또는 AccountType|  
|![키 특성 아이콘](../../analysis-services/multidimensional-models/media/as-icon-key-attribute.gif "키 특성 아이콘")|Key|  
|![부모 특성 아이콘](../../analysis-services/multidimensional-models/media/as-icon-parent-attribute.gif "부모 특성 아이콘")|Parent|  
  
## <a name="see-also"></a>관련 항목:  
 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
