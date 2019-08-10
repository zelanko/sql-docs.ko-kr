---
title: 셀 업데이트 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 71279981c5fd3879d633e0fdd8cdec74bed6deac
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887704"
---
# <a name="updating-cells-xmla"></a>셀 업데이트(XMLA)
  [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) 명령을 사용 하 여 큐브 쓰기 저장 (writeback)에 사용 하도록 설정 된 큐브에 있는 하나 이상의 셀 값을 변경할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트할셀을포함하는각파티션에대해업데이트된정보를별도의쓰기저장(writeback)[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블에 저장 합니다.  
  
> [!NOTE]  
>  `UpdateCells` 명령은 큐브 쓰기 저장(writeback) 동안 할당을 지원하지 않습니다. 할당 된 쓰기 저장 (writeback)을 사용 하려면 [statement](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) 명령을 사용 하 여 MDX (Multidimensional EXPRESSIONS) UPDATE 문을 보내야 합니다. 자세한 내용은 [CUBE 문 &#40;MDX&#41;업데이트](/sql/mdx/mdx-data-manipulation-update-cube)를 참조 하세요.  
  
## <a name="specifying-cells"></a>셀 지정  
 `UpdateCells` 명령의 [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) 속성은 업데이트할 셀을 포함 합니다. 해당 셀의 서수 번호를 사용하여 `Cell` 속성의 각 셀을 식별할 수 있습니다. 개념적으로는 큐브가 *p*차원 배열인 것 처럼 큐브에서 셀의 번호를표시합니다.여기서p는축수[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 입니다. 셀은 행 중심의 순서로 번호가 매겨집니다. 다음 그림에서는 셀의 서수 번호를 계산하는 수식을 보여 줍니다.  
  
 ![셀 서 수 위치를 계산 하는 수식](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/cellordinalformula.gif "셀 서 수 위치를 계산 하는 수식")  
  
 셀의 서 수를 알고 있는 경우 [셀](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) 속성의 [value](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) 속성에 원하는 셀 값을 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소 &#40;XMLA 업데이트&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Analysis Services에서 XMLA를 사용하여 개발](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
