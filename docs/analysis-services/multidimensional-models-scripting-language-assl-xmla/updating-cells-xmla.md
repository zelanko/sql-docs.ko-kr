---
title: "셀 업데이트 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 10803f4f2e3356d996a7c524c69ccd5121569a3e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="updating-cells-xmla"></a>셀 업데이트(XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]사용할 수는 [UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) 명령은 큐브 쓰기 저장에 대 한 가능한 큐브의 여러 셀의 값을 변경할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 업데이트할 셀이 포함 된 각 파티션에 대 한 별도 쓰기 저장 테이블에 업데이트 된 정보를 저장 합니다.  
  
> [!NOTE]  
>  **UpdateCells** 명령은 큐브 쓰기 저장 하는 동안 할당을 지원 하지 않습니다. 할당 된 쓰기 저장을 사용 하려면 사용할지는 [문을](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) 명령은 MDX (Multidimensional Expressions) UPDATE 문을 보내야 합니다. 자세한 내용은 참조 [UPDATE CUBE 문을 &#40; Mdx&#41; ](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>셀 지정  
 [셀](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) 의 속성에서 **UpdateCells** 명령 업데이트 될 셀을 포함 합니다. 각 셀을 식별할는 **셀** 해당 셀의 서 수를 사용 하 여 속성입니다. 개념적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 마치 것 처럼 큐브는 큐브의 셀에에서 번호는 *p*-차원 배열 여기서 *p* 축의 수입니다. 셀은 행 중심의 순서로 번호가 매겨집니다. 다음 그림에서는 셀의 서수 번호를 계산하는 수식을 보여 줍니다.  
  
 ![셀 서 수 위치를 계산 하는 수식](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "셀 서 수 위치를 계산 하는 수식")  
  
 셀의 서 수를 알게 되 면에 있는 셀의 의도 한 값을 나타낼 수 있습니다는 [값](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md) 의 속성은 [셀](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) 속성입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Update 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
