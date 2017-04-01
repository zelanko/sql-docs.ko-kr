---
title: "차원에 특성 추가 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "특성 추가"
  - "특성 자동 생성"
  - "특성 [Analysis Services], 만들기"
  - "특성 [Analysis Services], 추가"
  - "특성 수동 만들기 [Analysis Services]"
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 차원에 특성 추가
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 자동으로 또는 수동으로 차원에 특성을 추가할 수 있습니다.  
  
 특성을 자동으로 만들려면 **에 있는 차원 디자이너의** 차원 구조 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭에서 특성에 매핑할 열을 선택하고 **데이터 원본 뷰** 창에서 **특성** 창으로 해당 열을 끌어서 놓습니다. 이렇게 하면 열에 매핑되는 특성이 생성되고 특성에 열과 동일한 이름이 할당됩니다. 해당 이름으로 된 특성이 이미 있는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 첫 번째 중복 이름에 대해 "1"로 시작하는 서수 접미사 추가됩니다.  
  
 특성을 수동으로 만들려면 **특성** 창을 표 뷰로 설정합니다. 표에서 마지막 행의 이름 열에서 **\<새 특성>** 항목을 클릭합니다. 새 특성의 이름을 입력합니다. 이렇게 하면 열에 매핑되지 않고 모든 해당 속성에 대한 기본 설정이 있는 특성이 생성됩니다. 새 특성에 대한 **KeyColumns** 속성을 구성하여 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 의 **속성** 창에서 매핑을 설정할 수 있습니다.  
  
 자세한 내용은 [자동으로 새 특성 정의](../../analysis-services/multidimensional-models/define-a-new-attribute-automatically.md), [수동으로 새 특성 정의](../Topic/Define%20a%20New%20Attribute%20Manually.md), [이름 열로 특성 바인딩](../../analysis-services/multidimensional-models/bind-an-attribute-to-a-name-column.md), [특성의 KeyColumn 속성 수정](../../analysis-services/multidimensional-models/modify-the-keycolumn-property-of-an-attribute.md)을 참조하세요.  
  
## 관련 항목:  
 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  