---
title: 셀 업데이트 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3db80cd5573e115e3ec399470a7c2a249699e49f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061189"
---
# <a name="updating-cells-xmla"></a>셀 업데이트(XMLA)
  사용할 수는 [UpdateCells](../xmla/xml-elements-commands/updatecells-element-xmla.md) 큐브 쓰기 저장이 가능한 큐브의 여러 셀의 값을 변경 하는 명령입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 업데이트할 셀이 포함 된 각 파티션에 대 한 별도 쓰기 저장 테이블의 업데이트 된 정보를 저장 합니다.  
  
> [!NOTE]  
>  `UpdateCells` 명령은 큐브 쓰기 저장(writeback) 동안 할당을 지원하지 않습니다. 할당 된 쓰기 저장을 사용 하려면 사용 해야 합니다 [문을](../xmla/xml-elements-commands/statement-element-xmla.md) 명령은 MDX (Multidimensional Expressions) UPDATE 문을 보내야 합니다. 자세한 내용은 [UPDATE CUBE 문 &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube)합니다.  
  
## <a name="specifying-cells"></a>셀 지정  
 [셀](../xmla/xml-elements-properties/cell-element-xmla.md) 의 속성을 `UpdateCells` 업데이트할 셀을 포함 하는 명령입니다. 해당 셀의 서수 번호를 사용하여 `Cell` 속성의 각 셀을 식별할 수 있습니다. 개념적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브의 처럼 큐브의 셀에에서 번호를 *p*-차원 배열에 있는 *p* 는 축의 개수입니다. 셀은 행 중심의 순서로 번호가 매겨집니다. 다음 그림에서는 셀의 서수 번호를 계산하는 수식을 보여 줍니다.  
  
 ![셀 서 수 위치를 계산 하는 수식을](../../../2014/analysis-services/dev-guide/media/cellordinalformula.gif "셀 서 수 위치를 계산 하는 수식")  
  
 셀의 서 수 번호를 알게 되 면에 있는 셀의 의도 한 값을 지정할 수 있습니다 합니다 [값](../xmla/xml-elements-properties/value-element-xmla.md) 의 속성을 [셀](../xmla/xml-elements-properties/cell-element-xmla.md) 속성입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Update 요소 &#40;XMLA&#41;](../xmla/xml-elements-commands/update-element-xmla.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
