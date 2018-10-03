---
title: 차원에 특성 추가 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- adding attributes
- automatic attribute creation
- attributes [Analysis Services], creating
- attributes [Analysis Services], adding
- manual attribute creation [Analysis Services]
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c45184e5be13193dc8b77924bc05debdc1911361
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189665"
---
# <a name="add-an--attribute-to-a-dimension"></a>차원에 특성 추가
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 자동으로 또는 수동으로 차원에 특성을 추가할 수 있습니다.  
  
 특성을 자동으로 만들려면 **에 있는 차원 디자이너의** 차원 구조 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭에서 특성에 매핑할 열을 선택하고 **데이터 원본 뷰** 창에서 **특성** 창으로 해당 열을 끌어서 놓습니다. 이렇게 하면 열에 매핑되는 특성이 생성되고 특성에 열과 동일한 이름이 할당됩니다. 해당 이름으로 된 특성이 이미 있는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 첫 번째 중복 이름에 대해 "1"로 시작하는 서수 접미사 추가됩니다.  
  
 특성을 수동으로 만들려면 **특성** 창을 표 뷰로 설정합니다. 표의 마지막 행의 이름 열을 클릭 합니다  **\<새 특성 >** 항목입니다. 새 특성의 이름을 입력합니다. 이렇게 하면 열에 매핑되지 않고 모든 해당 속성에 대한 기본 설정이 있는 특성이 생성됩니다. 새 특성에 대한 **KeyColumns** 속성을 구성하여 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 의 **속성** 창에서 매핑을 설정할 수 있습니다.  
  
 자세한 내용은 [자동으로 새 특성 정의](attribute-properties-define-a-new-attribute-automatically.md), [수동으로 새 특성 정의](../define-a-new-attribute-manually.md), [이름 열로 특성 바인딩](attribute-properties-bind-an-attribute-to-a-name-column.md), [특성의 KeyColumn 속성 수정](attribute-properties-modify-the-keycolumn-property.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [차원 특성 속성 참조](dimension-attribute-properties-reference.md)  
  
  
